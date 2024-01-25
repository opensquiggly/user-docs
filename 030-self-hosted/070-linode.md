---
weight: 70
url: /docs/self-hosted/vm/linode
order: 7
Title: "VM Install : Linode"
description: How to install OpenSquiggly on Linode.
---
## Overview of Installing on Linode

We've provided a quick setup script that makes it easy to configure your disk space and
install dependencies on a virtual machine in Linode.

In this section, you'll complete the following steps:

* Create a Virtual Machine
* Configure the VM for SSH Access
* Download the OpenSquiggly zip file and run the setup script
* Perform post-installation testing by creating an account, logging in, and
  create some quick content to verify the instance is working

<hr>

## Part 1 : Creating a Virtual Machine

### Steps to Complete
1. Log into your Linode cloud portal.
2. Create a Linode and fill in the following parameters:
   * Image - Choose Ubuntu 20.04 LTS
   * Pick your region
   * Choose the size of the Linode. We recommend you choose the Dedicated 4GB
     Linode at minimum.
   * Enter the Linode Label
   * Enter a Root Password
   * Add an SSH key or choose an existing SSH key that you've previously uploaded
3. Wait for the Linode to be provisioned
4. Click the Storage tab to add storage
5. Add a Volume. Choose a size big enough to accommodate the Git repos you expect
   to attach.
6. Enter a Label for the Volume.

### Video
<iframe
  width="1024"
  height="785"
  src="https://www.youtube.com/embed/HIPoKRW0mHk"
  frameborder="0"
  webkitallowfullscreen
  mozallowfullscreen
  allowfullscreen>
</iframe>

<div>
  <ul>
    <li><a href="https://www.youtube.com/watch?v=HIPoKRW0mHk" target="_blank">Open Video in YouTube</a></li>
  <ul>
</div>

<hr>

## Part 2 : Running the Setup Script

### Steps to Complete
1. SSH into the VM
   ```bash
   ssh root@your_linode_ip_address
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
4. Retrieve the Application Files. Visit the OpenSquiggly website at https://opensquiggly.com for
   the latest download instructions which have have changed since this document was published.
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
   sudo bash linode-setup.sh
   ```
8. Follow the setup instructions and enter the information when prompted. Please see the
   video below for additional guidance.


### Video
<iframe
  width="1024"
  height="800"
  src="https://www.youtube.com/embed/XthjSYtgb_M"
  frameborder="0"
  webkitallowfullscreen
  mozallowfullscreen
  allowfullscreen>
</iframe>

<div>
  <ul>
    <li><a href="https://www.youtube.com/watch?v=XthjSYtgb_M" target="_blank">Open Video in YouTube</a></li>
  <ul>
</div>

<hr>

## Part 3 : Post-Installation Testing

### Steps to Complete
1. From your browser, navigate to the IP address DNS address where your Linode VM is registered.
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
  height="785"
  src="https://www.youtube.com/embed/uwGwHBfd57I"
  frameborder="0"
  webkitallowfullscreen
  mozallowfullscreen
  allowfullscreen>
</iframe>

<div>
  <ul>
    <li><a href="https://www.youtube.com/watch?v=uwGwHBfd57I" target="_blank">Open Video in YouTube</a></li>
  <ul>
</div>
