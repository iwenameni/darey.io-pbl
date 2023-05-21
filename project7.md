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

![step2-1](https://github.com/iwenameni/darey.io-pbl/assets/111616140/fbe3023e-c9eb-4588-82fa-843797b962ad)
![step2-2](https://github.com/iwenameni/darey.io-pbl/assets/111616140/5205f414-276e-4ae8-b577-5a59ed2e8896)
![step2-3](https://github.com/iwenameni/darey.io-pbl/assets/111616140/db744c1d-2254-4b2a-95a9-6b8e79b09379)
![step2-4](https://github.com/iwenameni/darey.io-pbl/assets/111616140/4136125a-2d18-4c4a-ac8a-0900d77fcf36)
![step2-5](https://github.com/iwenameni/darey.io-pbl/assets/111616140/37d5c6cd-5804-4fdf-84b3-39369ac03e77)
![step2-6](https://github.com/iwenameni/darey.io-pbl/assets/111616140/4e0b26de-a317-41b5-87f0-28128ad1b248)
![step2-7](https://github.com/iwenameni/darey.io-pbl/assets/111616140/10044aef-5556-487a-b61f-37108d36cb17)
![step2-8](https://github.com/iwenameni/darey.io-pbl/assets/111616140/bad3c5a3-53b7-4518-887d-102ac08cdf5b)
![step2-9](https://github.com/iwenameni/darey.io-pbl/assets/111616140/605f010a-1c62-4cf3-b0bb-912d5e8da514)


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

setsebool -P httpd_execmem
 
We repeat these steps for the other 2 webservers (WEBSERVER 2 and 3)
 
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

![step3-1](https://github.com/iwenameni/darey.io-pbl/assets/111616140/66a231bc-f505-4e06-94ad-1deba979ca46)
![step3-2](https://github.com/iwenameni/darey.io-pbl/assets/111616140/c1ed9132-11a6-4809-a544-d6f09eaa803f)
![step3-3](https://github.com/iwenameni/darey.io-pbl/assets/111616140/931cdfa5-064b-4575-aeaa-f5d4b19ae482)
![step3-4](https://github.com/iwenameni/darey.io-pbl/assets/111616140/b3218ebc-192d-4195-a932-0e2db142fbd1)
![step3-5](https://github.com/iwenameni/darey.io-pbl/assets/111616140/77ce881f-a89d-4160-84e8-0af6284ad608)
![step3-6](https://github.com/iwenameni/darey.io-pbl/assets/111616140/e05fda35-7c87-473f-867f-15f9cff443e5)
![step3-7](https://github.com/iwenameni/darey.io-pbl/assets/111616140/f0e9f0c9-cd80-45fa-80e5-932cf677d6be)
![step3-8](https://github.com/iwenameni/darey.io-pbl/assets/111616140/39dc3b99-ab64-4ba7-9586-241c8ed47c55)
![step3-9](https://github.com/iwenameni/darey.io-pbl/assets/111616140/34af3783-a99e-4520-8cf6-0b27912aa21e)
![step3-10](https://github.com/iwenameni/darey.io-pbl/assets/111616140/5b38c41a-39d4-4cbd-8d8e-a34794409a69)
![step3-11](https://github.com/iwenameni/darey.io-pbl/assets/111616140/55fcc5d7-0c8e-4820-aa6a-86a3fbb135c3)
![step3-12](https://github.com/iwenameni/darey.io-pbl/assets/111616140/7353552e-5d57-41f9-9625-03667185bb1a)
![step3-13](https://github.com/iwenameni/darey.io-pbl/assets/111616140/404371d0-9c9c-4e7b-9042-171a25831411)
![step3-14](https://github.com/iwenameni/darey.io-pbl/assets/111616140/fa3960e3-c421-4f1d-8097-dc7e9d1b3379)
![step3-15](https://github.com/iwenameni/darey.io-pbl/assets/111616140/1362d224-0897-4784-9449-ea9740fd84c0)
![step3-16](https://github.com/iwenameni/darey.io-pbl/assets/111616140/9c2bda90-7cd8-4b8c-b30b-5718ad730288)
![step3-17](https://github.com/iwenameni/darey.io-pbl/assets/111616140/a52e021c-44de-48f5-ac9e-650c5da0440d)
![step3-18](https://github.com/iwenameni/darey.io-pbl/assets/111616140/4c250841-0ee3-49cc-8126-96cca25fb841)
![step3-19](https://github.com/iwenameni/darey.io-pbl/assets/111616140/2aba3743-d032-42de-b859-22c671c84fb8)
![step3-20](https://github.com/iwenameni/darey.io-pbl/assets/111616140/9b3edbb1-fe5a-4542-9d54-d67972da0d35)
![step3-21](https://github.com/iwenameni/darey.io-pbl/assets/111616140/3efca016-5380-461a-aa0f-406278e431e6)
                                                               
We can now see if we can access the website via the private IP address of the webservers

![testing-the-website](https://github.com/iwenameni/darey.io-pbl/assets/111616140/d1fd5cfc-bf96-4f5f-bb00-9606de172cfc)

![website-testing](https://github.com/iwenameni/darey.io-pbl/assets/111616140/e63c3b8b-c710-457f-b680-eb9adf27a9a2)
