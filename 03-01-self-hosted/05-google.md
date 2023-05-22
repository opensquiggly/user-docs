---
order: 5
Title: "VM Install : Google"
---
# Overview of Installing on Google Cloud

We've provided a quick setup script that makes it easy to configure your disk space and
install dependencies on a Google Cloud Compute Engine Instance (i.e., a Virtual Machine).

In this section, you'll complete the following steps:

* Create an Instance (i.e, a Virtual Machine)
* Download the OpenSquiggly zip file and run the setup script
* Perform post-installation testing by creating an account, logging in, and
  create some quick content to verify the instance is working

<hr>

# Part 1 : Creating an Instance

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
  src="https://www.loom.com/embed/f44170f793524c788e94764a6f5daa97" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>

<hr>

# Part 2 : Running the Setup Script

### Steps to Complete
1. SSH into the VM from your web browser using the Google Cloud Portal.
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
   sudo bash google-setup.sh
   ```
8. Follow the setup instructions and enter the information when prompted. Please see the
   video below for additional guidance.


### Video
<iframe 
  width="1024" 
  height="756" 
  src="https://www.loom.com/embed/11cd2aeb63e94091a5fd748824f8808f" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>

<hr>

# Part 3 : Post-Installation Testing

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
  src="https://www.loom.com/embed/b910cc7c6e09471c9cf1bd5e61705b61" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>
