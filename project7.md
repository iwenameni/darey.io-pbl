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
