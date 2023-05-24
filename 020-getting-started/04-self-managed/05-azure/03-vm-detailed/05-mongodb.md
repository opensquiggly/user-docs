order: 5
title: Installing MongoDB
---
# Steps to Complete
1. SSH into your VM
   ```
   ssh_vm
   ```
2. Import the MongoDB public GPG key.
   ```
   wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -
   ```
3. Add MongoDB to your sources list.
   ```
   echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list
   ```
4. Update apt-get.
   ```
   sudo apt-get update
   ```
5. Install MongoDB.
   ```
   sudo apt-get install -y mongodb-org
   ```
6. Create data and logs folders for MongoDB and grant access to them. Consult your network operations
   team for additional security advice.
   ```
   mkdir /data/mongodb
   mkdir /data/logs
   mkdir /data/logs/mongodb
   ```
7. Consider granting full read/write access to these folders. Consult your security team. The goal is 
   to ensure MongoDB has read/write access to these folders.
   ```
   sudo chmod 777 /data/mongodb
   sudo chmod 777 /data/logs
   sudo chmod 777 /data/logs/mongodb
   ```
8. Grant access for these folders to the mongodb user.
   ```
   sudo chown -Rc mongodb /data/mongodb
   sudo chown -Rc mongodb /data/logs/mongodb
   ```
9. Edit your mongod.conf file to reference your database and log paths.
   ```
   sudo vi /etc/mongod.conf
   ```
   
   Make the following changes:
   ```
   # mongod.conf

   # for documentation of all options, see:
   #   http://docs.mongodb.org/manual/reference/configuration-options/

   # Where and how to store data.
   storage:
     dbPath: /data/mongodb  <------- Path to database folder
     journal:
       enabled: true
   #  engine:
   #  wiredTiger:

   # where to write logging data.
   systemLog:
     destination: file
     logAppend: true
     path: /data/logs/mongodb/mongod.log  <------- Path to logs folder
   
   .
   . Remainder of mongod.conf file
   .
   .
   ```
10. Reload the systemctl daemon.
    ```
    sudo systemctl daemon-reload
    ```
11. Start the mongod daemon.
    ```
    sudo systemctl start mongod
    ```
12. Verify the service started properly.
    ```
    sudo systemctl status mongo
    ```
    
    Should display:
    ```
    ● mongod.service - MongoDB Database Server
    Loaded: loaded (/lib/systemd/system/mongod.service; disabled; vendor preset: enabled)
    Active: active (running) since Wed 2022-06-22 01:55:04 UTC; 15h ago <------ Successfully started
    Docs: https://docs.mongodb.org/manual
    Main PID: 2512 (mongod)
    Memory: 116.9M
    CGroup: /system.slice/mongod.service
    └─2512 /usr/bin/mongod --config /etc/mongod.conf

    Jun 22 01:55:04 opensquigglyvm1 systemd[1]: Started MongoDB Database Server.
    ```

# Web Links
* https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/
  
# Video
<iframe 
  width="1024" 
  height="800" 
  src="https://www.loom.com/embed/58b5f5fe8bdd4886a7aa9cae8b9832a1" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>

# Video Timeline
* 01:45 - SSH into VM
* 02:08 - Import GPG key
* 02:25 - Create the sources list
* 02:34 - Update apt-get
* 02:58 - Install MongoDB
* 04:26 - Make data and log folders
* 05:00 - Grant read/write access to folder
* 06:00 - Edit mongod.conf file
* 07:13 - Change ownership of folders
* 08:00 - Daemon reload
* 08:13 - Start mongod
* 08:30 - Verify mongod started
