---
weight: 40
url: /docs/self-hosted/vm/digital-ocean
order: 4
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
  src="https://www.loom.com/embed/8a6527282649452a9e8761e85dfd4988" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>

<hr>

## Part 2 : Running the Setup Script

### Steps to Complete
1. SSH into the VM
   ```
   ssh ubuntu@your_droplet_address
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
4. Retrieve the Application Files. Visit the OpenSquiggly website at https://opensquiggly.com for
   the latest download instructions which have have changed since this document was published.
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
   sudo bash digitalocean-setup.sh
   ```
8. Follow the setup instructions and enter the information when prompted. Please see the
   video below for additional guidance.


### Video
<iframe 
  width="1024" 
  height="818" 
  src="https://www.loom.com/embed/3b57d73586f64cd59cceddef218f4b4b" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>

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
  src="https://www.loom.com/embed/ff93d10cbfcd4a609f10a419744d5455" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>