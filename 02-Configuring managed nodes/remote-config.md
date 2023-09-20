**Setting up remote ansible server**
1. In vscode, make sure the "remote-SSH" and "Remote Development" extensions are installed.
2. Configure remote ssh on vscode with user as ubuntu
   a. Click on settings, --> Command Palette, and type or select "Remote-SSH: Open SSH Configuration file",  
   then select *C:\users\username\.ssh\config*
   b. In the ansible configuration file, do the following:
                Host "alias name"  
		    HostName ansible_server_IP  
		    User ubuntu #(default ubuntu user)  
                    IdentityFile path/to/private_key.pem  

4. Log into the remote server as ubuntu and switch user to ansible

        $ sudo su - ansible
5. Create .ssh directory in the home of ansible
   
        $ sudo mkdir .ssh
        $ sudo chown -R ansible:ansible .ssh
6. Copy the authorized keys from the home of ubuntu to the home of ansible
  - cd into the .ssh directory and run the command below.

        $ sudo cp /home/ubuntu/.ssh/authorized_keys .

  - Change ownership of the key to ansible

         $ sudo chown ansible:ansible authorized_keys
5. Also change the ownership of /etc/ansible from root to ansible

        $ sudo chown -R ansible:ansible /etc/ansible
6. Now change the default user in the vscode config to log in as ansible
```
Host Ansible
    HostName 54.183.22.101
    User ansible
    IdentityFile ~/Downloads/ansible-key.pem
```

7. You can use the script below to install vscode on ubuntu using the script below.
```   
   sudo apt update
   sudo apt upgrade -y
   sudo apt install software-properties-common apt-transport-https wget -y
   wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
   sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" -y
   sudo apt install code -y
```
