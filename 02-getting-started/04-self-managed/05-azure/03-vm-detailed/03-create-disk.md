order: 3
title: Creating a Virtual Disk
---
# Steps to Complete
1. Visit your Azure Portal at https://portal.azure.com and login to your Azure account.
2. Navigate to the previously created virutal machine in the Azure Portal
3. Click on the Disks section under your VM resource
4. Under the Data disks section, click "Crate and attach a new disk".
5. Enter a Disk name
6. For Storage type, select Premium SSD (it's important for OpenSquiggly to have high performance
   disk space because cloning Git repos is disk access intensive)
7. Select an appropriate disk size. Choose a size that is large enough to accommodate current
   and future needs based on the number of Git repos you plan on cloning. Disks can be resized in
   the future if needed, but it requires some manual steps to do so.
8. Click Save in the upper left area of the header to provision the disk.

# Video

<iframe 
  width="1024" 
  height="809" 
  src="https://www.loom.com/embed/121b38598ba04ac3985b406904144f9c" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>
