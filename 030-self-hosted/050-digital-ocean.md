---
weight: 50
url: /docs/self-hosted/vm/digital-ocean
order: 5
Title: "VM Install : Digital Ocean"
description: How to install OpenSquiggly on a Digital Ocean droplet.
---
## Overview of Installing on Digital Ocean

We've provided a quick setup script that makes it easy to configure your disk space and
install dependencies on a Digital Ocean Droplet.

In this section, you'll complete the following steps:

* Create a Droplet (i.e, a Virtual Machine)
* Download the OpenSquiggly zip file and run the setup script
* Perform post-installation testing by creating an account, logging in, and
  create some quick content to verify the instance is working

<hr>

## Part 1 : Creating a Droplet

### Steps to Complete
1. Log into your Digital Ocean cloud portal.
2. Create a Droplet and fill in the following parameters:
   * Image - Choose Ubuntu 20.04 LTS
   * Pick your region
   * Choose the size of the Droplet.
   * Enter the Label
   * Add an SSH key or choose an existing SSH key that you've previously uploaded
3. Wait for the Droplet to be provisioned
4. Click the Storage tab to add storage
5. Add a Volume. Choose a size big enough to accommodate the Git repos you expect
   to attach.
6. Enter a Label for the Volume.

### Video
<iframe 
  width="1024" 
  height="818" 
  src="https://www.youtube.com/embed/_ygIizbpe7A" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>

<div>
  <ul>
    <li><a href="https://www.youtube.com/watch?v=_ygIizbpe7A" target="_blank">Open Video in YouTube</a></li>
  <ul>
</div>

<hr>

## Part 2 : Running the Setup Script

### Steps to Complete
1. SSH into the VM
   ```bash
   ssh ubuntu@your_droplet_address
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
   ```bash
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
   sudo bash digitalocean-setup.sh
   ```
8. Follow the setup instructions and enter the information when prompted. Please see the
   video below for additional guidance.


### Video
<iframe 
  width="1024" 
  height="818" 
  src="https://www.youtube.com/embed/NZd4GhKat38" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>

<div>
  <ul>
    <li><a href="https://www.youtube.com/watch?v=NZd4GhKat38" target="_blank">Open Video in YouTube</a></li>
  <ul>
</div>

<hr>

## Part 3 : Post-Installation Testing

### Steps to Complete
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
  height="818" 
  src="https://www.youtube.com/embed/JAF2vXhh7JA" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>

<div>
  <ul>
    <li><a href="https://www.youtube.com/watch?v=JAF2vXhh7JA" target="_blank">Open Video in YouTube</a></li>
  <ul>
</div>