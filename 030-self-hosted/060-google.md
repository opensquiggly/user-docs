---
weight: 60
url: /docs/self-hosted/vm/google
order: 6
Title: "VM Install : Google"
description: How to install OpenSquiggly on a Google Cloud virtual machine.
---
## Overview of Installing on Google Cloud

We've provided a quick setup script that makes it easy to configure your disk space and
install dependencies on a Google Cloud Compute Engine Instance (i.e., a Virtual Machine).

In this section, you'll complete the following steps:

* Create an Instance (i.e, a Virtual Machine)
* Download the OpenSquiggly zip file and run the setup script
* Perform post-installation testing by creating an account, logging in, and
  create some quick content to verify the instance is working

<hr>

## Part 1 : Creating an Instance

### Steps to Complete
1. Log into your Google cloud portal.
2. Create a Google Cloud Compute Instance and fill in the following parameters:
   * Name - Give the instance a name
   * Image - Choose Ubuntu 20.04 LTS
   * Pick your region
   * Choose the size of the Instance.
3. Wait for the Droplet to be provisioned
4. Click the Storage tab to add storage
5. Add a Volume. Choose a size big enough to accommodate the Git repos you expect
   to attach.
6. Enter a Label for the Volume.

### Video
<iframe 
  width="1024" 
  height="818" 
  src="https://www.youtube.com/embed/zAEL0MwrfRo" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>

<div>
  <ul>
    <li><a href="https://www.youtube.com/watch?v=zAEL0MwrfRo" target="_blank">Open Video in YouTube</a></li>
  <ul>
</div>

<hr>

## Part 2 : Running the Setup Script

### Steps to Complete
1. SSH into the VM from your web browser using the Google Cloud Portal.
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
   sudo bash google-setup.sh
   ```
8. Follow the setup instructions and enter the information when prompted. Please see the
   video below for additional guidance.


### Video
<iframe 
  width="1024" 
  height="756" 
  src="https://www.youtube.com/embed/SIHhhuYXK_8" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>

<div>
  <ul>
    <li><a href="https://www.youtube.com/watch?v=SIHhhuYXK_8" target="_blank">Open Video in YouTube</a></li>
  <ul>
</div>

<hr>

## Part 3 : Post-Installation Testing

### Steps to Complete
2. From your browser, navigate to the IP address DNS address where you VM is registered.
3. Click the "Create account" button and create a new account.
4. Login with your login id and password.
5. Enter some content in the home page.
6. Enter a search phrase in the search bar and hit <Enter>. Verify that the correct
   page(s) are returned.
7. Mount one or more repositories and graft them into your document tree.
8. Try searching for some content in your repositories to verify that the search is
   working.
9. Experiment with the Navigator to arrange your document tree to your liking.

### Video
<iframe 
  width="1024" 
  height="818" 
  src="https://www.youtube.com/embed/WCfmmHexWxg" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>

<div>
  <ul>
    <li><a href="https://www.youtube.com/watch?v=WCfmmHexWxg" target="_blank">Open Video in YouTube</a></li>
  <ul>
</div>