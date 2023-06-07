---
weight: 20
Order: 2
Title: Private Portals
description: >
  This section gives an overview of hosted private portals. Private portals are the half-way house
  between the public instance and self-hosted portals. We manage the portal for you in a private instance
  with a separate database that is not shared with other users. Private portals will be available in the
  future. In the mean time, please consider a self-hosted option.
---
## Cloud Hosted Private Portals

Our cloud hosted private portals work and act a lot like our shared portal, except they provide additional
data security by storing your data on a private database instance and indexed by a privately managed document
indexing service. Thus, your data is not stored alongside other users as it is in our shared portal.

As with the shared portal, there is nothing for you to install and no software dependencies to manage. We do 
all the work for you and provide you with a clean, solid, no-fuss, no-muss working system. We provide logging,
analytics, maintenance tools, and all the things you'd expect from a modern, cloud-hosted system.

Of course private portals cost a little more, because it's more expensive for us to manage all the private
resources we need to keep your instance up and running. It's up to you to decide if the additional security
benefits of private hosting are worth the extra cost. We do our best to negotiate prices with our cloud
vendors and partners to provide you with competitive prices.

If you think our prices are too high, think you can purchase cloud resources at better prices than we can,
and you don't mind the extra labor investments needed to install and manage the software, then our
self-managed private portals may be the right choice for you.

## Creating a Private Portal

Private portals are currently under development and in beta testing. Please contact us for the current status
and for instructions on how to create a private portal.

## Securing Private Portals with Virtual Private Networks

When you create your portal, you have two general access choices: 1) allow any user on the Internet to access
the portal at it's installed domain address (of coure, they'll still need login credentials to sign in), 
or 2) Only allow access to select users via a virtual private network. 

Access via a virtual private network provides an even higher level of security than ordinary private portals,
and come at the expense of some extra configuration that will need to be done by your network administrators
to allow access from your corporate network to the VPN where your OpenSquiggly instance is installed.

By default, private instances use general Internet access. Please contact us for information about setting
up VPN access for your private portal.

Virtual Private Network access will be available at a future dat, based on user demand. To learn more, please 
contact us regarding our product roadmap and to express your interest in VPN access.

## Where Your Private Portal is Hosted

After your private portal is provisioned and configured you will receive an e-mail containing access instructions.

By default, your private portal will be accessible via an instance name you choose, and hosted on the opensquiggly.com
domain. For example, if you named your private portal "myawesomedocs", then the portal would be available by
visiting: https://myawesomedocs.opensquiggly.com. Instance names must be unique.

All private portal plans also come with the ability to assign a custom domain name. You will receive additional
instructions on how to configure a custom domain name. This is typically done by going to your domain provider
and configuring the DNS server to route traffic from your desired custom domain to the private instance name.
Contact your domain provider for more information on configuring your DNS server.

For example, suppose you work at MegaCorp and want your "myawesomedocs" instance to be available using your
megacorp.com domain name that you have registered with your domain provider.

You'll use the software provide by your domain provider to configure a link (known as an "A Record") to the 
OpenSquiggly instance, such as:

```
     myawesomedocs.megacorp.com  -->  myawesomedocs.opensquiggly.com
```

After that, your users can access the portal by visiting: https://myawesomedocs.megacorp.com.

## Managing Self-Registration Access on Private Portals

Depending on your security needs, there are three ways users can be created on the system:

* The instance administrator can create accounts on behalf of users
* The instance administrator can configure access to an LDAP directory server
* Users can self-register an account for themselves on the system

Note: LDAP access will be available in the future. Please contact us to express interest and learn about our
product roadmap.

When you configure your private portal, you can decide whether or not you want to allow user self-registration.
User self-registration is a convenient feature, however, some organizations may not want to allow self-registration
for security reasons.

If you do decide to allow user self-registration, there are two extra options you can choose to help restrict
which users can register. 

* Users can be required to supply an invitation code
* Users can be required to have an e-mail address at one more more given domains (example: user must have
  a megacorp.com e-mail address)

This is important, since surely you do not want any user anywhere in the world to be able to register themselves 
on your system (unless you truly are intending to create a public portal for global access, such as you might
want to do for publishing end user documentation).

## Two Factor Authentication

You can optionally provision your instance to require two-factor authentication for users to log in.

## Summary of Cloud Hosted Private Portal Security Measures

* Data is stored on a private database instance
* Documents are indexed on a private document indexing instance
* Can be restricted to VPN access (future roadmap)
* Can be assigned a custom domain name
* Can use either a shared, OpenSquiggly-assigned, or organization-provided TLS/SSL certificate
* Can use LDAP directory services (future roadmap)
* Can allow or disallow user self-registration
* User self-registration can be restricted by invitation codes or e-mail addresses
* Two Factor Authentication options can be configured

In summary, our private portal hosting options offer the best security provisions available via today's technology.

However, for some ultra-security-conscious organizations, even this may not be enough. Some organizations may
not be satisfied unless they can completely control data access via their own computing servers and resources.

For those users, we offer self-managed private portal hosting plans.

### Creating an Account

Access the system by visiting the web address sent to you by OpenSquiggly or using the custom domain name
configured by your network administrator.

If your OpenSquiggly administrator has not allowed self-registration, then you'll need to obtain login
credentials from your administrator.

If your administrator has allowed self-registration, the complete the sign up process by entering your
e-mail address, login id, name, and password.

Your portal administrator may also require you to provide an invitation code.

IMPORTANT: Be sure to remember and use your LOGIN ID when you sign in. Don't use your e-mail address as the
login id - it won't work. The reason why we do it this way is because we allow you to create multiple accounts
with the same e-mail address. Therefore, the LOGIN ID is the only thing that we can be sure is unique.

### Signing In

After you've created your account, sign in using your LOGIN ID and PASSWORD. From here you'll be taken to your
Home page, which is the root page from which you navigate to all your documents.

### Resetting Forgotten Passwords

If you've forgotten your password, click on the "Forgot your password" link near the bottom of the
sign in form.

The Reset Password form will open. Enter your login id or e-mail address of the account for wish to
reset your password. Note that while you can enter either your login id or e-mail address here, be sure
to use your actual login id (not your e-mail address) after you reset the password and are ready to log in.

You will receive an e-mail containing a link to reset your password. Click on the link and enter a new
password, and a second time to confirm it. After resetting your password, go back to the sign in page and
login with your login id and new password.

## Next Steps

Initially your Home Page will be completely empty until you add documents to your navigator, but it doesn't need
to stay that way for very long. Because we allow you to quickly connect your account to source code repositories
and documentation stored in externally hosted Git repositories (Azure DevOps, Bitbucket, GitHub, and GitLab),
your account can very quickly be populated with many thousands of source code files and documents for you to
start doing deep, focused work on your project!

To learn how to use OpenSquiggly as a wiki and author documents directly within the OpenSquiggly system, see
the chapter titled "Document Authoring".

To learn how to connect your account to external source code repositories, see the chapter titled "Connecting to
Source Code Repositories".

To learn how to connect your account to external documentation repositories, see the chapter titled "Connecting to
Document Repositories".

Once you've added a bunch of files and documents to your account, you'll probably want to organize and manage
them so you can find them easily. To learn more about using the document navigator and managing your overall
document structure, see the chapter titled "Managing the Navigator".

That should be enough to get you out of the starting gate and using OpenSquiggly in earnest. We've designed
OpenSquiggly with an eye for making life better for software developers. We sincerely hope that you enjoy
using OpenSquiggly and can begin using it to do your best work and make positive impacts on your projects
and for your customers.