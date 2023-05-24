title: Running the Setup Script
---
# Steps to Complete
1. SSH into the VM
   ```
   ssh root@you_linode_ip_address
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
   unzip opensquiggly.latest.zip -d OpenSquiggly
   ```
6. Change to the /opt/OpenSquiggly/setup folder
   ```
   cd /opt/OpenSquiggly/setup
   ```
7. Invoke the setup script.
   ```
   sudo bash linode-setup.sh
   ```
8. Follow the setup instructions and enter the information when prompted. Please see the
   video below for additional guidance.


# Video
<iframe 
  width="1024" 
  height="800" 
  src="https://www.loom.com/embed/65eac393ee58471081f21f7dfd0d9157" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>
