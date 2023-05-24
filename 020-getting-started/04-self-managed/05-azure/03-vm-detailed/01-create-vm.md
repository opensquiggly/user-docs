order: 1
title: Creating a VM on Azure
---
# Steps to Complete
1. Visit your Azure Portal at https://portal.azure.com and login to your Azure account.
2. In the search box, search for "virtual machine", and select Virtual Machines from the list.
3. Click the Create button near the top left portion of the portal, and choose the Azure virtual machine
   from the dropdown list.
4. Under the Basics tab, fill in the desired parameters for the VM:
   * Subscription
   * Resource Group
   * Enter a Virtual machine name
   * For image type, choose Ubuntu Server 20.04 LTS - Gen2
   * Pick a Size for the VM. A Standard_D2s_v3 should be sufficient for a basic OpenSquiggly
     installation with up to 100 users
   * Fill in other parameters based on your security preferences
   * We recommend leaving the SSH public key radio button selected
5. Click the Create button to start the provisioning process.
6. Download the private key using the popup window that will appear.

# Video
<iframe 
  width="1024" 
  height="809" 
  src="https://www.loom.com/embed/09f6db2bc85041b6a84aa4b564318e33" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>
