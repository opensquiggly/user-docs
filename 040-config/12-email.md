---
weight: 120
url: /docs/config/email
order: 12
Title: E-Mail Configuration
description: How to configure OpenSquiggly to send e-mail notifications.
---
## About E-Mail Notifications

E-Mail notifications are not configured by default with the OpenSquiggly
setup scripts. While not strictly necessary, it is a very good idea to
configure your OpenSquiggly instance for sending e-mail notifications after
you get your basic instance up and running.

E-Mail Notifications are used by OpenSquiggly in the following areas:

* Self-Registration: When a new user self-registers themselves as a user in the OpenSquiggly
  instance, they will receive an introductory e-mail after registering.
  This helps the user confirm that their registration was successful and
  that they can receive e-mail notifications.
* Communications Test: A user can send a test message to themselves to confirm that their
  e-mail notifications are working.
* Resetting Forgotten Passwords: Letting a user reset their forgotten password
  requires sending them an e-mail with a link and a key to reset their password.

## Supported E-Mail Systems

OpenSquiggly currently supports the MailGun e-mail service, and we'll be adding
support for other e-mail services in the future.

[MailGun](https://mailgun.com) is free to use for up to 1000 e-mails per month.
This should be sufficient for most organizations to handle occassional new user
registrations and/or password reset requests.

## Steps to Configure MailGun E-Mail Notifications

1. Create your MailGun account by visiting https://mailgun.com
2. In the MailGun dashboard, create a domain for sending e-mails
3. Follow the instructions provided by MailGun to validate and
   activate your domain.
4. Follow the instructions provided by MailGun to send a test e-mail
   message to verify the MailGun domain is working.
5. In the MailGun dashboard, create an API key that can be used to send
   e-mails via the MailGun API service. Be sure to store the API key in 
   a safe place such as a password vault.
6. Use SSH to connect to the virtual machine where your OpenSquiggly instance
   is installed
7. Edit your appsettings.json file with the following command:
   ```bash
   sudo vi /opt/OpenSquiggly/bin/appsettings.json
   ```
8. Add the following section to your appsettings.json file:
   ```json
   "MailgunEmailOptions": {
     "Domain": "your_mailgun_email_domain",
     "ApiKey": "your_mailgun_api_key",
     "ReturnEmailAddress": "return_email_address",
     "ServiceEmail": "address_to_send_admin_notifications"
   }
   ```
   Example:
9. ```json
   "MailgunEmailOptions": {
   "Domain": "mg.yourcompany.com",
   "ApiKey": "abcdef1234567890abcdef1234567890-98765421-abcdef12",
   "ReturnEmailAddress": "mailgun@yourcompany.com",
   "ServiceEmail": "opensquigglyadmin@yourcompany.com"
   }
   ```
   - Domain: This will be the domain that you created in MailGun.
     For example: ```mg.yourcompany.com```
   - ApiKey: This is the API key that you created in the MailGun dashboard
     and have stored in a secure location.
   - ReturnEmailAddress: This is the return e-mail address that will be injected
     into the e-mails that OpenSquiggly sends. For example: ```mailgun@mg.yourcompany.com```
   - ServiceEmail: This is an e-mail address of an OpenSquiggly administrator that will also
     receive an e-mail when something is sent to a user. This e-mail address helps the OpenSquiggly
     administrator monitor e-mail activity.
10. Also add the following section to your appsettings.json file:
   ```json
   "HostConfigOptions": {
     "HostName": "full_url_where_instance_is_installed"
   }
   ```
   Example:
   ```json
   "HostConfigOptions": {
     "HostName": "https://opensquiggly.yourcompany.com"
   }
   ```
   The HostName setting under the HostConfigOptions setting is needed by
   the e-mail system so that it can include a link back to the OpenSquiggly
   instance that the user can click on to complete the password reset workflow.
   For this reason, the OpenSquiggly server needs to know the URL where the
   instance is installed.
11. Save the changes to your appsettings.json file.
12. Restart the OpenSquiggly service with the command:
    ```bash
    sudo systemctl restart opensquiggly
    ```


