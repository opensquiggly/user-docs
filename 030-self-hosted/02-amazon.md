---
weight: 20
order: 2
Title: "VM Install : Amazon"
description: How to install OpenSquiggly on an Amazon AWS instance.
---
## Overview of Installing on Amazon

We've provided a quick setup script that makes it easy to configure your disk space and
install dependencies on an Amazon AWS instance.

In this section, you'll complete the following steps:

* Launch an Instance (i.e, a Virtual Machine)
* Download the OpenSquiggly zip file and run the setup script
* Perform post-installation testing by creating an account, logging in, and
  create some quick content to verify the instance is working

<hr>

## Part 1 : Creating a Instance

### Steps to Complete
1. Log into your Amazon AWS cloud portal.
2. Navigate to All Services.
3. Choose your desired region from the header bar in the upper right section of
   the screen.
4. Under the Compute section, choose EC2.
5. Click the button "Launch Instance" and fill in the following parameters:
   * Name - Give the instance a name
   * Image - Under Application and OS Images, choose Ubuntu 20.04 LTS
   * Choose the size of the Instance. We recommend you choose t2.medium
     at minimum. Depending on the number of users and the size of your ElasticSearch
     indexes, you may need more processors or more memory.
   * Create an SSH key or choose an existing SSH key that you've previously created
6. Under the Networking section, check the following check boxes
   * Allow HTTPS traffic from the Internet
   * Allow HTTP traffic from the Internet
7. Under the Configure Storage section, click the "Add new volume" button and add
   a disk volume large enough to accomodate the number of repositories you expect
   to clone.
8. Click Launch Instance, and wait for the Instance to be provisioned

### Video of Creating AWS Instance
<iframe 
  width="1024" 
  height="818" 
  src="https://www.loom.com/embed/a77001cca1504b00a8995d1bf9da8df6" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>

<hr>

## Part 2 : Running the Setup Script

### Steps to Complete
1. SSH into the Instance
   ```bash
   ssh ubuntu@your_aws_instance_address
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
   sudo bash aws-setup.sh
   ```
8. Follow the setup instructions and enter the information when prompted. Please see the
   video below for additional guidance.


### Video of Installing on AWS Instance
<iframe 
  width="1024" 
  height="818" 
  src="https://www.loom.com/embed/19d179773d614e17a2818855e4792f8f" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>

<hr>

## Part 3 : Post-Installation Testing

### Steps to Complete
1. From your browser, navigate to the IP address DNS address where your Instance is registered.
2. Click the "Create account" button and create a new account.
3. Login with your login id and password.
4. Enter some content in the home page.
5. Enter a search phrase in the search bar and hit <Enter>. Verify that the correct
   page(s) are returned.
6. Mount one or more repositories and graft them into your document tree.
7. Try searching for some content in your repositories to verify that the search is
   working.
8. Experiment with the Navigator to arrange your document tree to your liking.

### Video of Post-Installation Testing
<iframe 
  width="1024" 
  height="818" 
  src="https://www.loom.com/embed/4c5511d5e31e4e95a2070f72a53cec75" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>