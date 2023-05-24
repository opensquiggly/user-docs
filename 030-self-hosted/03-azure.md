---
order: 3
title: "VM Install : Azure"
---
# Overview of Installing on Azure

We've provided a quick setup script that makes it easy to configure your disk space and
install dependencies on a virtual machin in Microsoft Azure.

In this document, you'll complete the following steps:

* Create a Virtual Machine
* Configure the VM for SSH Access
* Download the OpenSquiggly zip file and run the setup script
* Perform post-installation testing by creating an account, logging in, and
  create some quick content to verify the instance is working

<hr>

# Part 1 : Creating a Virtual Machine

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
Not available yet. Please check back later.

<hr>

# Part 2 : Enabling SSH Access to the VM
1. Copy the downloaded SSH key into your ~/.ssh folder
   ```
   cd ~/.ssh
   cp ~/Downloads/file_name_here.pem .
   chmod 400 file_name_here.pem
   ```
2. Test the SSH access with:
   ```
   ssh -o "IdentitiesOnly=yes" -i ~/.ssh/file_name_here.pem azureuser@VM.IP.ADDRESS.HERE
   ```
3. Create an alias in your .bashrc file to make it easier to SSH:
   ```
   echo alias ssh_vm=\'ssh -o "IdentitiesOnly=yes" -i ~/.ssh/file_name_here.pem azureuser@VM.IP.ADDRESS.HERE\' >> ~/.bashrc
   source ~/.bashrc
   ```
4. Test your SSH alias
   ```
   ssh_vm
   ```

# Video
<iframe
  width="1024"
  height="800"
  src="https://www.loom.com/embed/fa111a415dd044b283939d396f142371"
  frameborder="0"
  webkitallowfullscreen
  mozallowfullscreen
  allowfullscreen>
</iframe>

<hr>

# Part 3 : Running the Setup Script
1. SSH into the VM
   ```
   ssh_vm
   ```
2. Change to the /opt folder
   ```
   cd /opt
   ```
3. Install unzip
   ```
   sudo apt update
   sudo apt install unzip
   ```
4. Retrieve the Application Files. Visit the OpenSquiggly website at https://opensquiggly.com for the latest download instructions which have have changed since this document was published.
   ```
   sudo wget http://files.opensquiggly.com/opensquiggly.latest.zip
   ```
5. Unzip the file
   ```
   sudo unzip opensquiggly.latest.zip -d OpenSquiggly
   ```
6. Change to the /opt/OpenSquiggly/setup folder
   ```
   cd /opt/OpenSquiggly/setup
   ```
7. Invoke the setup script.
   ```
   sudo bash azure-setup.sh
   ```
8. Follow the setup instructions and enter the information when prompted. Please see the
   video below for additional guidance.

# Video
<iframe
  width="1024"
  height="778"
  src="https://www.loom.com/embed/5b55c2204bc4469796b42982abfa6f49"
  frameborder="0"
  webkitallowfullscreen
  mozallowfullscreen
  allowfullscreen>
</iframe>

<hr>

# Part 4 : Post-Installation Testing

1. From your browser, navigate to the IP address DNS address where you VM is registered.
2. Click the "Create account" button and create a new account.
3. Login with your login id and password.
4. Enter some content in the home page.
5. Enter a search phrase in the search bar and hit <Enter>. Verify that the correct
   page(s) are returned.
6. Mount one or more repositories and graft them into your document tree.
7. Try searching for some content in your repositories to verify that the search is
   working.
8. Experiment with the Navigator to arrange your document tree to your liking.

# Video
<iframe
  width="1024"
  height="840"
  src="https://www.loom.com/embed/0977d4e58f2e4eb193e758fbe96889c5"
  frameborder="0"
  webkitallowfullscreen
  mozallowfullscreen
  allowfullscreen>
</iframe>

