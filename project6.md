# PROJECT 6: WEB SOLUTION WITH WORDPRESS

In this project I will prepare a storage infrastructure on two Linux servers and implement a basic web solution using WordPress

This project will consist of 2 parts;

1. Configure storage subsystem for the Web and Database servers based on Linux OS

2. Install WordPress and connect it to a remote MySQL database server.

## Step 1: PREPARING THE WEB SERVER

We start by launching an instance that will serve as web server, then create 3 volumes (10 GiB) each and attache them to the web server.

We then open up the terminal and start configuring the web servewr.

Codes:

lsblk

df -h

sudo gdisk /dev/xvdf

sudo gdisk /dev/xvdg

sudo gdisk /dev/xvdh

sudo yum install lvm2

sudo pvcreate /dev/xvdf1

sudo pvcreate /dev/xvdg1

sudo pvcreate /dev/xvdh1

sudo pvs

sudo vgcreate webdata-vg /dev/xvdh1 /dev/xvdg1 /dev/xvdf1

sudo vgs

sudo lvcreate -n apps-lv -L 14G webdata-vg

sudo lvcreate -n logs-lv -L 14G webdata-vg

sudo lvs

sudo vgdisplay -v #view complete setup - VG, PV, and LV

sudo lsblk

sudo mkfs -t ext4 /dev/webdata-vg/apps-lv

sudo mkfs -t ext4 /dev/webdata-vg/logs-lv

sudo mkdir -p /var/www/html

sudo mkdir -p /home/recovery/logs

sudo mount /dev/webdata-vg/apps-lv /var/www/html/

sudo rsync -av /var/log/. /home/recovery/logs/

sudo mount /dev/webdata-vg/logs-lv /var/log

sudo rsync -av /home/recovery/logs/. /var/log

sudo blkid

sudo vi /etc/fstab

sudo mount -a

sudo systemctl daemon-reload

df -h

![webserver-config1](https://user-images.githubusercontent.com/111616140/232260676-71429cc5-f03a-40df-b865-a40ff3c3bff1.jpg)

![webserver-config2](https://user-images.githubusercontent.com/111616140/232260677-65709c57-5baa-4574-bd94-cd8ad6396760.jpg)

![webserver-config3](https://user-images.githubusercontent.com/111616140/232260684-07c7284d-2f42-4ea7-9bd9-f5664b316db6.jpg)

![webserver-config4](https://user-images.githubusercontent.com/111616140/232260693-123e6ac1-5b05-4b6e-9868-67afb8f53b05.jpg)

![webserver-config5](https://user-images.githubusercontent.com/111616140/232260695-764ce690-0b09-4491-b144-58c968d85698.jpg)

![webserver-config6](https://user-images.githubusercontent.com/111616140/232260698-b73c121d-36c9-4572-ba98-66e8550dfd1b.jpg)

![webserver-config7](https://user-images.githubusercontent.com/111616140/232260702-24a1c7e9-f140-41fa-9f60-4c97c69414b2.jpg)

![webserver-config8](https://user-images.githubusercontent.com/111616140/232260705-0f6ea0fd-75df-4abf-93ca-56d07888a2c5.jpg)

![webserver-config9](https://user-images.githubusercontent.com/111616140/232260708-1eec185d-63ee-4677-a499-ebc4c9a0abcb.jpg)

![webserver-config10](https://user-images.githubusercontent.com/111616140/232260715-b9e8d9ec-7276-4a76-b677-e2b1d0334c20.jpg)

![webserver-config11](https://user-images.githubusercontent.com/111616140/232260718-9d8f728e-e277-4f6e-9a61-c6c457a7f16d.jpg)

![webserver-config12](https://user-images.githubusercontent.com/111616140/232260722-8233d165-5af6-489b-bc27-218dc1c23a4e.jpg)

![webserver-config13](https://user-images.githubusercontent.com/111616140/232260727-6d780822-6eea-4900-9261-99f88122f896.jpg)

## STEP 2: PREPARING THE DATABASE SERVER

lsblk

sudo gdisk /dev/xvdf

sudo gdisk /dev/xvdg

sudo gdisk /dev/xvdh

sudo yum install lvm2

sudo lvmdiskscan

sudo pvcreate /dev/xvdf1 /dev/xvdg1 /dev/xvdh1

sudo pvs

sudo vgcreate vg-database /dev/xvdf1 /dev/xvdg1 /dev/xvdh1

sudo vgs

sudo lvcreate -n db-lv -L 20G vg-database

sudo lvs

sudo mkdir /db

sudo mkfs.ext4 /dev/vg-database/db-lv

sudo mount /dev/vg-database/db-lv /db

df -h

sudo blkid

sudo vi /etc/fstab

sudo mount -a

sudo systemctl daemond-reload

df -h

![db-config1](https://user-images.githubusercontent.com/111616140/232348911-dcb6f26d-0ea3-41d1-97f5-b17780c4054f.jpg)

![db-config2](https://user-images.githubusercontent.com/111616140/232348920-ecfc93e9-6bef-4e1f-bb35-438510cb8081.jpg)

![db-config3](https://user-images.githubusercontent.com/111616140/232348928-ac584486-c922-4106-94d7-85e677b3bdba.jpg)

![db-config4](https://user-images.githubusercontent.com/111616140/232348932-2d509364-7820-475b-9ff4-3933491bfa42.jpg)

![db-config5](https://user-images.githubusercontent.com/111616140/232348934-612e615c-a30f-473d-ae93-344d3c8e6087.jpg)

![db-config6](https://user-images.githubusercontent.com/111616140/232348939-85dba2e3-4196-403d-b766-17b8d08bd8a3.jpg)

![db-config7](https://user-images.githubusercontent.com/111616140/232348941-a0495605-5a53-44c1-88d8-b02b992c670b.jpg)

## Step 3 — Install WordPress on your Web Server EC2

Update the repository

sudo yum -y update

Start Apache

sudo systemctl enable httpd

To install PHP and it’s depemdencies

sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm

sudo yum install yum-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm

sudo yum module list php

sudo yum module reset php

sudo yum module enable php:remi-7.4

sudo yum install php php-opcache php-gd php-curl php-mysqlnd

sudo systemctl start php-fpm

sudo systemctl enable php-fpm

setsebool -P httpd_execmem 1

sudo systemctl start httpd

Restart Apache

sudo systemctl restart httpd

mkdir wordpress

cd   wordpress

sudo wget http://wordpress.org/latest.tar.gz
  
sudo tar xzvf latest.tar.gz
  
sudo cp -R wp-config-sample.php wp-config.php

cp R wordpress/. /var/www/html/

cd /var/www/html

sudo yum install mysql-server
