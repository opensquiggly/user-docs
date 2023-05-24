order: 4
title: Attaching & Formatting the Disk
---
# Steps to Complete
1. SSH into your VM
   ```
   # Using your SSH alias
   ssh_vm
   ```
2. Determine which disk device you need to partition
   ```
   lsblk -o NAME,HCTL,SIZE,MOUNTPOINT | grep -i "sd"
   ```
3. Examine the output to verify the disk device. Assuming you only have one disk attached
   to your VM, the device name will probably be "sdc".
   ```
   sda     0:0:0:0      30G 
   ├─sda1             29.9G /
   ├─sda14               4M
   └─sda15             106M /boot/efi
   sdb     0:0:0:1      16G
   └─sdb1               16G /mnt
   sdc     1:0:0:0      32G   <--------- This should be the newly attached disk you want to format
   ```
4. Create a disk partition on the newly attached disk
   ```
   sudo parted /dev/sdc --script mklabel gpt mkpart xfs 0% 100%
               --------
               The name of the device from the above command
   ```
5. Reissue the lsblk command to verify the partition has been created.
   ```
   lsblk -o NAME,HCTL,SIZE,MOUNTPOINT | grep -i "sd"
   ```
   Should show:

   ```
   sda     0:0:0:0      30G
   ├─sda1             29.9G /
   ├─sda14               4M
   └─sda15             106M /boot/efi
   sdb     0:0:0:1      16G
   └─sdb1               16G /mnt
   sdc     1:0:0:0      32G
   └─sdc1               32G  <------- This should be the newly created partition
   ```
6. Format the partition to install a file system onto it.
   ```
   sudo mkfs.xfs /dev/sdc1
                 ---------
                 The name of the partition
   ```
   
   ```
   sudo partprobe /dev/sdc1
   ```
7. Create the /data folder in your file system and mount the new partition.
   ```
   sudo mkdir /data && sudo mount /dev/sdc1 /data
                                  ---------
                                  The name of theh partition
   ```
8. Verify the new mount point
   ```
   df -h | grep -i "sd"
   ```
   
   Should show:
   ```
   /dev/sda15      105M  5.2M  100M   5% /boot/efi
   /dev/sdb1        16G   45M   15G   1% /mnt
   /dev/sdc1        32G  261M   32G   1% /data  <------ New partition mounted at /data
   ```
9. You might want to give full read/write access to your /data drive, however consult your
   network operations team for security advice. The goal is to ensure that the OpenSquiggly service,
   MongoDB, and ElasticSearch processes have full read/write access to the /data folder.
    ```
    sudo chmod 777 /data
    ```
10. Determine the UUID of /dev/sdc1 to use in your fstab file (next step)
    ```
    sudo -i blkid
    ```
    And copy the UUID associated with /dev/sdc1 to your clipboard
11. Edit your fstab file
    ```
    sudo vi /etc/fstab
    ```
12. Add the following line to the bottom of your fstab file.
    ```
    UUID=put_uuid_from_above_here<<<TAB>>>/data<<<TAB>>>xfs<<<TAB>>>defaults,nofail<<<TAB>>>1<<<TAB>>>2
    ```
13. Save the file and exit from vi. 
14. Verify that you can write files to your /data folder
    ```
    cd ~/data
    echo hello > hello.txt
    ls
    cat hello.txt
    ```
15. Verify your disk free space on /data
    ```
    df
    ```
    Should show:
    ```
    Filesystem     1K-blocks    Used Available Use% Mounted on
    /dev/root       30309264 2956816  27336064  10% /
    devtmpfs         4068768       0   4068768   0% /dev
    tmpfs            4072340       0   4072340   0% /dev/shm
    tmpfs             814468    1000    813468   1% /run
    tmpfs               5120       0      5120   0% /run/lock
    tmpfs            4072340       0   4072340   0% /sys/fs/cgroup
    /dev/loop0         63488   63488         0 100% /snap/core20/1518
    /dev/loop1         69504   69504         0 100% /snap/lxd/22753
    /dev/loop2         48128   48128         0 100% /snap/snapd/16010
    /dev/sda15        106858    5321    101537   5% /boot/efi
    /dev/sdb1       16446332   45084  15546108   1% /mnt
    /dev/sdc1       33536004  266948  32918276   1% /data   <------ Disk usage on /data
    tmpfs             814468       0    814468   0% /run/user/1000
    ```

# Video
<iframe 
  width="1024" 
  height="800" 
  src="https://www.loom.com/embed/a1e1d57eb737449ea51cdb88ec2c2f20" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>
