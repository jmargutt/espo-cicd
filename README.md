### setup

delete all branches except `main`

create a new branch `dev` from `main`

setup git repo in dev VM: ssh into the VM
```
sudo apt update && sudo apt upgrade
sudo apt install git
cd /var/www/espocrm/data/espocrm
sudo git config --global init.defaultBranch dev
sudo git config --global credential.helper store
sudo git init
sudo git config --global --add safe.directory /var/www/espocrm/data/espocrm
sudo git remote add origin https://github.com/jmargutt/espo-cicd.git
sudo git fetch
sudo git checkout dev
sudo git add data/config.php
sudo git commit -m "first commit"
sudo git push origin dev
--> add your github username and password
---> N.B. as password use a token that never expires #safety
```
add user to sudoers list
1. Edit sudoers file: `sudo nano /etc/sudoers`
2. Find a line which contains `includedir /etc/sudoers.d`
3. Below that line add: `username ALL=(ALL) NOPASSWD: ALL`, where `username` will be your passwordless sudo username
4. Save your changes: CTRL+O ENTER, CTRL+X ENTER


setup git repo in prod VM: ssh into the VM
```
sudo apt update && sudo apt upgrade
sudo apt install git
cd /var/www/espocrm/data/espocrm
sudo git config --global init.defaultBranch main
sudo git config --global credential.helper store
sudo git init
sudo git config --global --add safe.directory /var/www/espocrm/data/espocrm
sudo git remote add origin https://github.com/jmargutt/espo-cicd.git
sudo git pull origin main
--> add your github username and password
---> N.B. as password use a token that never expires #safety
```
add user to sudoers list
1. Edit sudoers file: `sudo nano /etc/sudoers`
2. Find a line which contains `includedir /etc/sudoers.d`
3. Below that line add: `username ALL=(ALL) NOPASSWD: ALL`, where `username` will be your passwordless sudo username
4. Save your changes: CTRL+O ENTER, CTRL+X ENTER

N.B.
after running actions, do not delete dev