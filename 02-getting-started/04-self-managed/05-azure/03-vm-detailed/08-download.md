order: 8
title: Downloading the Application Files
---
# Steps to Complete
1. SSH into the VM
   ```
   ssh_vm
   ```
2. Install unzip
   ```
   sudo apt update
   sudo apt install unzip
   ```
3. Retrieve the Application Files. Visit the OpenSquiggly website at https://opensquiggly.com for
   the latest download instructions which have have changed since this document was published.
   ```
   wget http://files.opensquiggly.com/opensquiggly.latest.zip
   ```
4. Unzip the file
   ```
   unzip opensquiggly.latest.zip -d OpenSquiggly
   ```
5. Verify the files have been extracted
   ```
   ls OpenSquiggly
   ```
   
# Video

<iframe 
  width="1024" 
  height="800" 
  src="https://www.loom.com/embed/6ea142fcea7442cea0aa9f702f9a0f88" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>
