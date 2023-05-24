order: 7
title: Installing .NET 6.0 Runtime
---
# Steps to Complete

1. SSH into VM
   ```
   ssh_vm
   ```
2. Download .deb file
   ```
   wget https://packages.microsoft.com/config/ubuntu/22.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
   ```
3. Run dpkg
   ```
   sudo dpkg -i packages-microsoft-prod.deb
   ```
4. Remove .deb file
   ```
   rm packages-microsoft-prod.deb
   ```
5. Update apt and Install
   ```
   sudo apt-get update; \
     sudo apt-get install -y apt-transport-https && \
     sudo apt-get update && \
     sudo apt-get install -y dotnet-sdk-6.0
   ```
   
# Links
* https://docs.microsoft.com/en-us/dotnet/core/install/linux-ubuntu#2004

# Video
<iframe 
  width="1024" 
  height="800" 
  src="https://www.loom.com/embed/52e5188687df4ff3b25af0a4e4885d36" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>
