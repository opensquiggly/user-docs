order: 3
title: Enabling SSH Access
---
# Steps to Complete
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
