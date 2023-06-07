---
weight: 140
order: 14
Title: OAuth on Bitbucket
description: How to configure OpenSquiggly to use OAuth authentication for Bitbucket Cloud.
---
## About Bitbucket

Bitbucket, by Atlassian, is one of the Git hosting systems explicitly supported by OpenSquiggly.
Once you've installed your OpenSquiggly instance, users can connect to their repositories on Bitbucket
and bring them into their OpenSquiggly accounts.

Public repositories can always be brought into OpenSquiggly with no additional configuration work
on the part of the OpenSquiggly instance administrator.

Private repositories can also be brought into OpenSquiggly using the user's personal access token
which they've manually created within the Bitbucket system. Use of personal access tokens does
not require any additional configuration work on the part of the OpenSquiggly instance administrator.

Another way of connecting to private repositories is to use OAuth authentication. This is more convenient
for the user because they do not need to manually create and maintain their personal access tokens.

In order for users to use OAuth authentication, the OpenSquiggly instance administrator must follow some
additional steps to enable OAuth authentication. This section covers how to configure OAuth for Bitbucket.

Note that in the cloud-hosted shared OpenSquiggly portal, these steps are not necessary because we've already
performed the setup and configured the cloud portal. However, the keys we use are private and cannot be shared
with the public, as that would defeat the purpose of OAuth authentication. Each private OpenSquiggly instance
must be configured to use it's own private keys.

## Configuring Bitbucket for OAuth

1. Create an account and an organization on the Bitbucket system by visiting https://bitbucket.org.
2. With your account, register a new OAuth Application
  * To register a new OAuth application, navigate to the desired workspace where you wish to create the application
    registration
  * In the navigation bar, select Settings
  * In the General section of the navigation bar, OAuth consumers
  * Click the "Add Consumer" button
  * Fill in the fields of the form:
    - Name - You should fill in this field with information that let's the user know what
      they are authorizing. It's a good idea to include both "OpenSquiggly" and your company name,
      such as "OpenSquiggly at YourCompany". This will let users know that they are authorizing the
      private instance within your company to access their repositories, and not some other public
      or private OpenSquiggly instance.
    - Description - Enter a description for OpenSquiggly such as "A documentation portal and notebook for developers".
    - Callback URL - Enter the full URL plus the suffix "/home", for example "https://opensquiggly.yourcompany.com/home".
      IMPORTANT: The callback URL must EXACTLY MATCH the location where you have installed OpenSquiggly with
      the "/home" suffix appended. 
    - URL - Enter the full URL where the OpenSquiggly instance is installed, for example
      "https://opensquiggly.yourcompany.com"
    - Privacy policy URL - Optional
    - End user license agreement URL - Optional
    - Permissions - Check the checkbox Repository -> Read
  * Click "Save". Take note of the App and Secret and store them in a secure location
    such as your password vault.
3. Open an SSH connection to your virtual machine on your cloud provider where you installed OpenSquiggly
4. Open the appsettings.json file with the command:
   ```bash
   sudo vi /opt/OpenSquiggly/bin/appsettings.json
   ```
5. Add the following section to your appsettings.json file:
   ```json
    "BitbucketOAuthTokenProviderOptions": {
      "AppId": "[The Key assigned by Bitbucket]",
      "AppSecret": "[The Secret assigned by Bitbucket]",
      "RedirectUri": "https://[OpenSquiggly URL]/home",
      "Scope": "repository"
   }
   ```

   Example:
   ```json
    "BitbucketOAuthTokenProviderOptions": {
      "AppId": "XXXXXXXXXXXXXXXXXX",
      "AppSecret": "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
      "RedirectUri": "https://opensquiggly.yourcompany.com/home",
      "Scope": "repository"
   }
   ```
7. Save the appsettings.json file
8. Restart the OpenSquiggly service with:
   ```bash
   sudo systemctl restart opensquiggly
   ```
   
## Videos

### Part 1 : Registering an OAuth Consumer

<iframe width="1024" height="854" src="https://www.loom.com/embed/75e4382fbe7249cabb2054d949fb309b" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

### Part 2 : Configuring Bitbucket OAuth

<iframe width="1024" height="802" src="https://www.loom.com/embed/39810e93a60c41a8ae0ae0b69410e68c" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

### Part 3 : Demo of Bitbucket OAuth

<iframe width="1024" height="854" src="https://www.loom.com/embed/b76ab7b0676b4e1b8b01e50056754b78" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

### Part 4 : Viewing and Revoking Authorizations

<iframe width="1024" height="854" src="https://www.loom.com/embed/6b1bab56be2c495490d985b0c0631b6a" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
