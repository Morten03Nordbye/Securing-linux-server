# Securing-linux-server and setting up ufw firewall
This is a collection of useful commands for securing your linux server

### Step 1: Enable automatic updates
Manual Updates:
```sh
apt update
apt dist-upgrade
``` 

Automatic Updates:
```sh
apt install unattended-upgrades
dpkg-reconfigure --priority=low unattended-upgrades
``` 

### Step 2: Create a limited user account
```sh
adduser {username}
usermod -aG sudo {username}
``` 

### Step 3: SSH KEY
1) Create the Public Key Directory on your Linux Server
```sh
mkdir ~/.ssh && chmod 700 ~/.ssh
```
2) Create Public/Private keys on your computer
```sh
ssh-keygen -b 4096
```
3) Upload your Public key to the your Linux Server (Windows)

```sh
scp $env:USERPROFILE/.ssh/id_rsa.pub {username}@{server ip}:~/.ssh/authorized_keys
``` 

### Step 4: Lockdown Logins
```sh
sudo nano /etc/ssh/sshd_config
PermitRootLogin no
PasswordAuthentication no (if you want to only permit certification-login)
```

### Step 5: Firewall it up
Install, configure and enable ufw
```sh
apt install ufw
```
if unable to find ufw, add repository (debian):
```sh
add-apt-repository "deb http://http.debian.net/debian/ jessie main contrib non-free"
```
See UFW status:
```sh
sudo ufw status
```
Allow port through firewall:
```sh
sudo ufw allow 22
```
Start firewall:
```sh
sudo ufw enable
```
Restart firewall:
```sh
sudo ufw reload
```
