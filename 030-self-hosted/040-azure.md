---
weight: 40
url: /docs/self-hosted/vm/azure
order: 4
title: "VM Install : Azure"
description: How to install OpenSquiggly on an Azure virtual machine.
---
## Overview of Installing on Azure

We've provided a quick setup script that makes it easy to configure your disk space and
install dependencies on a virtual machin in Microsoft Azure.

In this document, you'll complete the following steps:

* Create a Virtual Machine
* Configure the VM for SSH Access
* Download the OpenSquiggly zip file and run the setup script
* Perform post-installation testing by creating an account, logging in, and
  create some quick content to verify the instance is working

<hr>

## Part 1 : Creating a Virtual Machine

### Steps to Complete

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
7. Go to the newly created VM resource, go to the Disks section, and add an Azure Disk.
   See below video for more details.

### Video
<iframe
  width="1024"
  height="800"
  src="https://www.youtube.com/embed/vFN9wQN0lLg"
  frameborder="0"
  webkitallowfullscreen
  mozallowfullscreen
  allowfullscreen>
</iframe>

<div>
  <ul>
    <li><a href="https://www.youtube.com/watch?v=vFN9wQN0lLg" target="_blank">Open Video in YouTube</a></li>
  <ul>
</div>

<hr>

## Part 2 : Enabling SSH Access to the VM

### Steps to Complete
1. Copy the downloaded SSH key into your ~/.ssh folder
   ```bash
   cd ~/.ssh
   cp ~/Downloads/file_name_here.pem .
   chmod 400 file_name_here.pem
   ```
2. Test the SSH access with:
   ```bash
   ssh -o "IdentitiesOnly=yes" -i ~/.ssh/file_name_here.pem azureuser@VM.IP.ADDRESS.HERE
   ```
3. Create an alias in your .bashrc file to make it easier to SSH:
   ```bash
   echo alias ssh_vm=\'ssh -o "IdentitiesOnly=yes" -i ~/.ssh/file_name_here.pem azureuser@VM.IP.ADDRESS.HERE\' >> ~/.bashrc
   source ~/.bashrc
   ```
4. Test your SSH alias
   ```bash
   ssh_vm
   ```

### Video
<iframe
  width="1024"
  height="800"
  src="https://www.youtube.com/embed/FU_ZjQWD8mQ"
  frameborder="0"
  webkitallowfullscreen
  mozallowfullscreen
  allowfullscreen>
</iframe>

<div>
  <ul>
    <li><a href="https://www.youtube.com/watch?v=FU_ZjQWD8mQ" target="_blank">Open Video in YouTube</a></li>
  <ul>
</div>

<hr>

## Part 3 : Running the Setup Script

### Steps to Complete
1. SSH into the VM
   ```bash
   ssh_vm
   ```
2. Change to the /opt folder
   ```bash
   cd /opt
   ```
3. Install unzip
   ```bash
   sudo apt update
   sudo apt install unzip
   ```
4. Retrieve the Application Files. Visit the OpenSquiggly website at https://opensquiggly.com for the latest download instructions which have have changed since this document was published.
   ```bash
   sudo wget http://files.opensquiggly.com/opensquiggly.latest.zip
   ```
5. Unzip the file
   ```bash
   sudo unzip opensquiggly.latest.zip -d OpenSquiggly
   ```
6. Change to the /opt/OpenSquiggly/setup folder
   ```bash
   cd /opt/OpenSquiggly/setup
   ```
7. Invoke the setup script.
   ```bash
   sudo bash azure-setup.sh
   ```
8. Follow the setup instructions and enter the information when prompted. Please see the
   video below for additional guidance.

### Video
<iframe
  width="1024"
  height="778"
  src="https://www.youtube.com/embed/HWsj8nkJ4v8"
  frameborder="0"
  webkitallowfullscreen
  mozallowfullscreen
  allowfullscreen>
</iframe>

<div>
  <ul>
    <li><a href="https://www.youtube.com/watch?v=HWsj8nkJ4v8" target="_blank">Open Video in YouTube</a></li>
  <ul>
</div>

<hr>

## Part 4 : Post-Installation Testing

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

### Video
<iframe
  width="1024"
  height="840"
  src="https://www.youtube.com/embed/5gpRCLTK_cQ"
  frameborder="0"
  webkitallowfullscreen
  mozallowfullscreen
  allowfullscreen>
</iframe>

<div>
  <ul>
    <li><a href="https://www.youtube.com/watch?v=5gpRCLTK_cQ" target="_blank">Open Video in YouTube</a></li>
  <ul>
</div>
