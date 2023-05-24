---
order: 13
Title: OAuth on Azure DevOps
---
# About Azure DevOps

Azure DevOps, by Microsoft, is one of the Git hosting systems explicitly supported by OpenSquiggly.
Once you've installed your OpenSquiggly instance, users can connect to their repositories on Azure DevOps
and bring them into their OpenSquiggly accounts.

Public repositories can always be brought into OpenSquiggly with no additional configuration work
on the part of the OpenSquiggly instance administrator.

Private repositories can also be brought into OpenSquiggly using the user's personal access token
which they've manually created within the Azure DevOps system. Use of personal access tokens does
not require any additional configuration work on the part of the OpenSquiggly instance administrator.

Another way of connecting to private repositories is to use OAuth authentication. This is more convenient
for the user because they do not need to manually create and maintain their personal access tokens.

In order for users to use OAuth authentication, the OpenSquiggly instance administrator must follow some
additional steps to enable OAuth authentication. This section covers how to configure OAuth for Azure DevOps.

Note that in the cloud-hosted shared OpenSquiggly portal, these steps are not necessary because we've already
performed the setup and configured the cloud portal. However, the keys we use are private and cannot be shared
with the public, as that would defeat the purpose of OAuth authentication. Each private OpenSquiggly instance
must be configured to use it's own private keys.

# Configure Azure DevOps for OAuth

1. Create an account and an organization on the Azure DevOps system by visiting https://dev.azure.com.
2. With your account, register a new OAuth Application
   * To register a new OAuth application, visit: https://app.vsaex.visualstudio.com/app/register
   * In the left-hand portion of the screen, underneath "Applications and services", click "Create new application"
   * Fill in the Company information fields:
      - Company name
      - Company website - The URL for the company website
      - Terms of service URL - Optional
      - Private statement URL - Optional
   * Fill in the Application information fields:
      - Application name - You should fill in this field with information that let's the user know what
        they are authorizing. It's a good idea to include both "OpenSquiggly" and your company name,
        such as "OpenSquiggly at YourCompany". This will let users know that they are authorizing the
        private instance within your company to access their repositories, and not some other public
        or private OpenSquiggly instance.
      - Description - Enter a description for OpenSquiggly such as "A documentation portal and notebook for developers".
      - Logo URL - Optional
      - Application website - Enter the full URL where the OpenSquiggly instance is installed, for example
        "https://opensquiggly.yourcompany.com"
      - Authorization callback URL - Enter the full URL plus the suffix "/home", for example "https://opensquiggly.yourcompany.com/home".
        IMPORTANT: The callback URL must EXACTLY MATCH the location where you have installed OpenSquiggly with
        the "/home" suffix appended.
   * Authorized scopes - Check the Code (read) checkbox. This limits the access that users receive from the
      OAuth connection request to reading repositories. It's always a good idea to limit the total access that
      users receive.
   * Click "Create application". Take note of the AppId and ClientSecret and store them in a secure location
      such as your password vault.
3. After you've registered an OAuth application, you can view all your current registrations by visiting:
   https://app.vsaex.visualstudio.com/me
4. Open an SSH connection to your virtual machine on your cloud provider where you installed OpenSquiggly
5. Open the appsettings.json file with the command:
   ```bash
   sudo vi /opt/OpenSquiggly/bin/appsettings.json
   ```
6. Add the following section to your appsettings.json file:
   ```json
    "AzureOAuthTokenProviderOptions": {
      "AppId": "[The AppId assigned by Azure DevOps]",
      "AppSecret": "[The ClientSecret assigned by Azure DevOps]",
      "RedirectUri": "https://[OpenSquiggly URL]/home",
      "Scope": "vso.code"
   }
   ```
   
   Example:
   ```json
    "AzureOAuthTokenProviderOptions": {
      "AppId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
      "AppSecret": "..... Long key omitted for brevity .....",
      "RedirectUri": "https://opensquiggly.yourcompany.com/home",
      "Scope": "vso.code"
   }
   ```
7. Save the appsettings.json file
8. Restart the OpenSquiggly service with:
   ```bash
   sudo systemctl restart opensquiggly
   ```
   
# Videos

In the following videos we set up and configure on OAuth registration for a fictitious company named WeegoSolar.

## Part 1 : Creating the Application Registration

<iframe 
  width="1024"
  height="840" 
  src="https://www.loom.com/embed/90447e7f0e5f456e817920dfb775c446" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>

## Part 2 : Configuring the OpenSquiggly Instance

<iframe 
  width="1024" 
  height="807" 
  src="https://www.loom.com/embed/bc4bee39ca9d4570ac86a5cce1e8657a" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>

## Part 3 : User Demo

<iframe 
  width="1024"
  height="840" 
  src="https://www.loom.com/embed/d1f6b9e069004b75ae104d1ccb9ff757" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen
  allowfullscreen>
</iframe>

## Part 4 : User Verification and Revocation

<iframe 
  width="1024" 
  height="840"
  src="https://www.loom.com/embed/8ee763dfca894cb4806439a20d3416f8" 
  frameborder="0" 
  webkitallowfullscreen
  mozallowfullscreen 
  allowfullscreen>
</iframe>
