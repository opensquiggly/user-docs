---
weight: 150
order: 15
Title: OAuth on GitHub
description: How to configure OpenSquiggly to use OAuth authentication for GitHub.
---
## About GitHub

GitHub is one of the Git hosting systems explicitly supported by OpenSquiggly.
Once you've installed your OpenSquiggly instance, users can connect to their repositories on GitHub
and bring them into their OpenSquiggly accounts.

Public repositories can always be brought into OpenSquiggly with no additional configuration work
on the part of the OpenSquiggly instance administrator.

Private repositories can also be brought into OpenSquiggly using the user's personal access token
which they've manually created within the GitHub system. Use of personal access tokens does
not require any additional configuration work on the part of the OpenSquiggly instance administrator.

Another way of connecting to private repositories is to use OAuth authentication. This is more convenient
for the user because they do not need to manually create and maintain their personal access tokens.

In order for users to use OAuth authentication, the OpenSquiggly instance administrator must follow some
additional steps to enable OAuth authentication. This section covers how to configure OAuth for GitHub.

Note that in the cloud-hosted shared OpenSquiggly portal, these steps are not necessary because we've already
performed the setup and configured the cloud portal. However, the keys we use are private and cannot be shared
with the public, as that would defeat the purpose of OAuth authentication. Each private OpenSquiggly instance
must be configured to use it's own private keys.

## Configuring GitHub for OAuth

1. Create an account and an organization on GitHub by visiting https://github.com.
2. Since we are assuming that you are creating an OpenSquiggly self-managed instance for a company, vs. a 
   personal instance, you'll want to create an "organization" on GitHub and associate your personal account
   with the company's GitHub organization.
3. Select the GitHub organization for which you wish to create the OAuth application.
   * In the user options drop in the upper-right of the GitHub header bar, select "Settings" to open up
     the settings for your user account.
   * In the sidebar, select "Organizations".
   * In the list of organizations, click on the organization for which you wish to create the OAuth application.
4. Navigate to the organization settings by clicking on the "Settings" icon in the menu across the top. Note
   that you are now entering the screen for ORGANIZATION settings, not your personal settings.
5. In the sidebar, select the "Developer settings" dropdown, and within the dropdown list, select "OAuth Apps".
6. Create a new OAuth App by clicking on the button "New OAuth App", and fill in the fields in the form:
   * Application name - You should fill in this field with information that let's the user know what
     they are authorizing. It's a good idea to include both "OpenSquiggly" and your company name,
     such as "OpenSquiggly at YourCompany". This will let users know that they are authorizing the
     private instance within your company to access their repositories, and not some other public
     or private OpenSquiggly instance.
   * Homepage URL - Enter the full URL where the OpenSquiggly instance is installed, for example
     "https://opensquiggly.yourcompany.com"
   * Application description - Enter a description for OpenSquiggly such as "A documentation portal and notebook for developers".
   * Authorization callback URL - Enter the full URL plus the suffix "/home", for example "https://opensquiggly.yourcompany.com/home".
     - IMPORTANT: The callback URL must EXACTLY MATCH the location where you have installed OpenSquiggly with
       the "/home" suffix appended.
   * Enable Device Flow - Leave this checkbox unchecked
   * When finished, click the "Register application" button to create OAuth App.
7. Take note of the "Client ID" for the newly registered application and store it in a secure location. You will
   need the Client ID for later steps.
8. Click the "Generate a new client secret" and take note of the client secret value that is generated for you.
   Store the client secret in a secure location. You will need the client secret for later steps.
   * Note that after you exit this screen, you can no longer retrieve the client secret value, so you need to 
     enter the value in your secure location before proceeding further. However, if you lose your client secret
     you can always generate a new client secret and reconfigure OpenSquiggly with the new secret.
9. Open an SSH connection to your virtual machine on your cloud provider where you installed OpenSquiggly
10. Open the appsettings.json file with the command:
    ```bash
    sudo vi /opt/OpenSquiggly/bin/appsettings.json
    ```
11. Add the following section to your appsettings.json file:
    ```json
     "GitHubOAuthTokenProviderOptions": {
       "AppId": "[The Client ID assigned by GitHub]",
       "AppSecret": "[The client secret generated by GitHub]",
       "RedirectUri": "https://[OpenSquiggly URL]/home",
       "Scope": "repo"
    }
    ```
 
    Example:
    ```json
     "GitHubOAuthTokenProviderOptions": {
       "AppId": "XXXXXXXXXXXXXXXXXX",
       "AppSecret": "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
       "RedirectUri": "https://opensquiggly.yourcompany.com/home",
       "Scope": "repo"
    }
    ```
12. Save the appsettings.json file
13. Restart the OpenSquiggly service with:
    ```bash
    sudo systemctl restart opensquiggly
    ```

## Videos

### Part 1 : Registering an OAuth Application

<iframe width="1024" height="854" src="https://www.loom.com/embed/458e2a2359114b718d1ec5d0fcfa44ca" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

### Part 2 : Configuring GitHub OAuth

<iframe width="1024" height="818" src="https://www.loom.com/embed/aff1cb5ef4f841b987fd9de4f8bd416d" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

### Part 3 : Demo of GitHub OAuth

<iframe width="1024" height="854" src="https://www.loom.com/embed/5dea8f0ead1e4f05b38f572701956179" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

### Part 4 : Viewing and Revoking Authorizations

<iframe width="1024" height="854" src="https://www.loom.com/embed/c9ccc15595cf411a8db0739139e230ab" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
