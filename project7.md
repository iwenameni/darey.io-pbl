# PROJECT7: DEVOPS TOOLING WEBSITE SOLUTION

## STEP 1 PREPARE NFS SERVER

We create a new EC2 instance with RHEL Linux 8 Operating System, then we configure LVM on the Server

lsblk

sudo gdisk /dev/xvdf

sudo gdisk /dev/xvdg

sudo gdisk /dev/xvdh

sudo yum install lvm2 -y

sudo lvmdiskscan

sudo pvcreate /dev/xvdf1

sudo pvcreate /dev/xvdg1
 
sudo pvcreate /dev/xvdh1

sudo pvs

sudo vgcreate webdata-vg /dev/xvdh1 /dev/xvdg1 /dev/xvdf1

sudo vgs

sudo lvcreate -n lv-apps -L 9G webdata-vg

sudo lvcreate -n lv-log -L 9G webdata-vg

sudo lvcreate -n lv-opt -L 9G webdata-vg

sudo lvs

sudo vgdisplay -v #view complete setup - VG, PV, and LV

sudo mkfs -t xfs /dev/webdata-vg/lv-apps

sudo mkfs -t xfs /dev/webdata-vg/lv-logs

sudo mkfs -t xfs /dev/webdata-vg/lv-opt

sudo mkdir /mnt/apps

sudo mkdir /mnt/logs

sudo mkdir /mnt/opt

sudo mount /dev/webdata-vg/lv-apps /mnt/apps

sudo mount /dev/webdata-vg/lv-logs /mnt/logs

sudo mount /dev/webdata-vg/lv-opt /mnt/opt

Having created our logical volumes, we now install the NFS and configure it to start on reboot

sudo yum -y update

sudo yum install nfs-utils -y

sudo systemctl start nfs-server.service

sudo systemctl enable nfs-server.service

sudo systemctl status nfs-server.service

sudo chown -R nobody: /mnt/apps

sudo chown -R nobody: /mnt/logs

sudo chown -R nobody: /mnt/opt

sudo chmod -R 777 /mnt/apps

sudo chmod -R 777 /mnt/logs

sudo chmod -R 777 /mnt/opt

sudo systemctl restart nfs-server.service

sudo vi /etc/exporrts

sudo exportfs -arv

rpcinfo -p | grep nfs

![step1-1](https://github.com/iwenameni/darey.io-pbl/assets/111616140/6afe33f0-b074-42f7-90c2-89cf1834d9c9)
![step1-2](https://github.com/iwenameni/darey.io-pbl/assets/111616140/c4f61d18-a43e-4c6e-9708-bd9aab3a5838)
![step1-3](https://github.com/iwenameni/darey.io-pbl/assets/111616140/b0880324-859b-4f1a-8f99-9ff5db129d07)
11616140/523ea010-b3e1-4244-b1a2-d7b2c40d8ad1)
![step1-4](https://github.com/iwenameni/darey.io-pbl/assets/111616140/24f353c4-fc86-4986-b3a2-e3539cbfa3e4)
![step1-5](https://github.com/iwenameni/darey.io-pbl/assets/111616140/4f5b363a-85da-4e8b-bfec-a8e0b4f13171)
![step1-6](https://github.com/iwenameni/darey.io-pbl/assets/111616140/29eee219-df8f-4cd7-b950-52c2e686258e)
![step1-7](https://github.com/iwenameni/darey.io-pbl/assets/111616140/639c44c0-5ebd-47c9-85f3-c30ea9d91f58)
![step1-8](https://github.com/iwenameni/darey.io-pbl/assets/111616140/6b94c2fd-a88e--4e8b-bfec-a8e0b4f13171)
![step1-9](https://github.com/iwenameni/darey.io-pbl/assets/111616140/145d9ecf-1698-4f6d-a3d6-d627bc103dab)
![step1-10](https://github.com/iwenameni/darey.io-pbl/assets/111616140/3557c9b4-8add-4762-a933-a06b9ecb6f86)
![step1-11](https://github.com/iwenameni/darey.io-pbl/assets/111616140/dc51bf1c-5ab744e4-9071-f4bd05f66246)
![step1-12](https://github.com/iwenameni/darey.io-pbl/assets/111616140/8bde9b95-eee9-41e8-bc50-d8d4e1b87cad)
![step1-13](https://github.com/iwenameni/darey.io-pbl/assets/111616140/1d5d53a0-0349-480f-b47e-d3a8588b2b26)
![step1-14](https://github.com/iwenameni/darey.io-pbl/assets/111616140/b101b3eb-7c69-48ec-85ed-ad0adb6ab74a)
![step1-15](https://github.com/iwenameni/darey.io-pbl/assets/111616140/b731171d-4db0-4ef5-ba24-47d99b674cdc)
![step1-17](https://github.com/iwenameni/darey.io-pbl/assets/111616140/6232916c-d738-43aa-833f-7ff89adea68c)
![step1-18](https://github.com/iwenameni/darey.io-pbl/assets/111616140/bf46edba-ee05-45ac-8db5-4a6c8ce80d4a)
![step1-19](https://github.com/iwenameni/darey.io-pbl/assets/111616140/0e75e0d3-49cc-421c-9079-45d00a3d3d17)
![step1-20](https://github.com/iwenameni/darey.io-pbl/assets/111616140/b5c0b411-4af8-46e8-bbb1-c3e6df4d1975)

## STEP 2 — CONFIGURE THE DATABASE SERVER

We now  configure a MySQL DBMS to work with remote Web Server

sudo apt update

sudo apt install mysql-server

sudo mysql

sudo create database tooling;

create user 'webaccess'@'172.31.80.0/20' identified by 'password';

grant all privileges on tooling.* to 'webaccess'@'172.31.80.0/20';

flush privileges;

show databases;

## Step 3 — Prepare the Web Servers

sudo yum install nfs-utils nfs4-acl-tools -y

sudo mkdir /var/www

sudo mount -t nfs -o rw,nosuid <NFS-Server-Private-IP-Address>:/mnt/apps /var/www

sudo vi /etc/fstab
  
<NFS-Server-Private-IP-Address>:/mnt/apps /var/www nfs defaults 0 0

sudo yum install httpd -y

sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm

sudo dnf install dnf-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm

sudo dnf module reset php

sudo dnf module enable php:remi-7.4

sudo dnf install php php-opcache php-gd php-curl php-mysqlnd

sudo systemctl start php-fpm

sudo systemctl enable php-fpm

setsebool -P httpd_execmem 1
 
ls /var/www
 
ls /var/log
 
sudo ls /var/log/httpd
 
sudo mount -t nfs -o rw,nosuid 172.31.88.122:/mnt/logs /var/log/httpd
 
sudo vi /etc/fstab
 
sudo yum install git
 
git init

We then fork  the tooling source code from Darey.io Github Account to my Github account:
 
git clone https://github.com/darey-io/tooling.git
 
cd tooling/
 
sudo cp -R html/. /var/www/html
 
ls /var/www/html

ls html
 
sudo setenforce 0
 
sudo vi /etc/sysconfig/selinux
 
sudo systemctl start httpd
 
 sudo systemctl status httpd
 
 sudo vi /var/www/html/functions.php
 
 cd tooling
 
 sudo yum install mysql -y
 
 myqsl -h 172.31.83.103 -u webaccess -p tooling < tooling-db.sql
                                                                
 We repeat these steps for the other 2 webservers (WEBSERVER 2 and 3)                                                           
