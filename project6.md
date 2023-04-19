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

sudo yum -y install wget httpd php php-mysqlnd php-fpm php-json

Start Apache

sudo systemctl enable httpd

sudo systemctl start httpd

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

sudo cp R wordpress/. /var/www/html/

cd /var/www/html

sudo yum install mysql-server

sudo systemctl start mysqld

sudo systemctl enable mysqld

sudo systemctl status mysqld

sudo chown -R apache:apache /var/www/html/wordpress

sudo chcon -t httpd_sys_rw_content_t /var/www/html/wordpress -R
  
sudo setsebool -P httpd_can_network_connect=1

sudo mv /etc/httpd/conf.d/welcome.conf /etc/httpd/conf.d/welcome.conf_backup

![step3-1](https://user-images.githubusercontent.com/111616140/232941516-063da16a-c2d6-4688-8a1b-0c388a2943c6.jpg)

![step3-2](https://user-images.githubusercontent.com/111616140/232941573-4852483f-e050-4988-b179-b2b8899256dd.jpg)

![step3-3](https://user-images.githubusercontent.com/111616140/232941587-a3cdd51a-e3fb-4d7e-b633-5f8ace11a4de.jpg)

![step3-4](https://user-images.githubusercontent.com/111616140/232941619-e06c9ca6-2b15-4c04-9662-f1f1a46347bd.jpg)

![step3-5](https://user-images.githubusercontent.com/111616140/232941664-7a5d3e5b-3eb3-4e02-bd2c-285439fb422d.jpg)

![step3-6](https://user-images.githubusercontent.com/111616140/232941675-b4b02c52-d0df-4ef3-b892-127dbcc25c0c.jpg)

![step3-7](https://user-images.githubusercontent.com/111616140/232941689-1d09a33e-50a0-4750-83cf-39b7b0770f6c.jpg)

![step3-8](https://user-images.githubusercontent.com/111616140/232941698-3ca89bc2-a8a0-4266-9fe7-6c96ce5c6031.jpg)

![step3-9](https://user-images.githubusercontent.com/111616140/232941719-a7058870-d425-4ac4-a7a5-00074f0e9254.jpg)

![step3-10](https://user-images.githubusercontent.com/111616140/232941738-da9b1407-9548-419f-ba48-7d4df388f859.jpg)

![step3-11](https://user-images.githubusercontent.com/111616140/232941745-25e52dca-7fb4-4472-87aa-dd95b1a8b399.jpg)

![step3-12](https://user-images.githubusercontent.com/111616140/232941774-a32cf47d-24fe-48ac-8995-b4c41f8932c5.jpg)

![step3-13](https://user-images.githubusercontent.com/111616140/232941786-036eb727-3a77-437c-b5f9-b69f1d284fdd.jpg)

![step3-14](https://user-images.githubusercontent.com/111616140/232941804-25df0b22-d7c7-40cc-a31b-5590f07554a2.jpg)

![step3-15](https://user-images.githubusercontent.com/111616140/232941850-4ff31ab1-4cdd-4793-8717-d9295020fbc2.jpg)

![step3-16](https://user-images.githubusercontent.com/111616140/232941966-1624cb50-8a82-42c0-bea6-45054a33e393.jpg)

![step3-17](https://user-images.githubusercontent.com/111616140/232941981-2162cfc5-47be-4e59-86e0-7fff302b6b98.jpg)

![step3-18](https://user-images.githubusercontent.com/111616140/232941994-21aa6614-db63-4af4-9fd8-6c1f81871d52.jpg)

![step3-19](https://user-images.githubusercontent.com/111616140/232942006-4b69737d-3bbd-4814-9dd6-6b81409b19f4.jpg)

![step3-20](https://user-images.githubusercontent.com/111616140/232942018-8810d5b7-70ff-4711-ab44-87c93a1c9435.jpg)

![step3-21](https://user-images.githubusercontent.com/111616140/232942024-429fab6a-d526-45a3-9b38-c2ce78922647.jpg)

![step3-22](https://user-images.githubusercontent.com/111616140/232942038-dae5ea9f-af39-432e-bcb4-d259fa70129e.jpg)

![step3-23](https://user-images.githubusercontent.com/111616140/232942056-ef590d00-6456-45a1-a2b1-ca5359a5332a.jpg)

![step3-24](https://user-images.githubusercontent.com/111616140/232942063-fe90847a-2116-48e8-8b72-bbd80cb223d2.jpg)

![step3-25](https://user-images.githubusercontent.com/111616140/232942074-bae550f9-a136-4d7c-9ac0-24f3c7f1b7d2.jpg)

![step3-26](https://user-images.githubusercontent.com/111616140/232942088-efbc7cd8-4019-4dfc-9ac7-bb0538a939b9.jpg)

![step3-27](https://user-images.githubusercontent.com/111616140/232942101-17c9aa4a-5560-4e3b-9be5-4314781cf77a.jpg)

![step3-28](https://user-images.githubusercontent.com/111616140/232942114-e6fd14f5-2e3d-4b2e-9bde-2ee270ef0336.jpg)

![step3-29](https://user-images.githubusercontent.com/111616140/232942127-738d8e41-f545-4e7e-889e-5fcbb5bdab3c.jpg)

![step3-30](https://user-images.githubusercontent.com/111616140/232942147-1c2231ef-ae52-4230-906c-9eb3ce98946e.jpg)

![step3-31](https://user-images.githubusercontent.com/111616140/232942251-be70257a-a952-466e-a600-133d1a541f1f.jpg)

![step3-32](https://user-images.githubusercontent.com/111616140/232942260-2296abd4-e9f1-4663-a420-bb31f5bd1dd8.jpg)

![step3-33](https://user-images.githubusercontent.com/111616140/232942280-ca0c3659-8961-4161-967f-35cb9ce75390.jpg)

![step3-34](https://user-images.githubusercontent.com/111616140/232942295-ea06ef82-bb1a-4261-bcfc-2d991c5a3098.jpg)

![step3-35](https://user-images.githubusercontent.com/111616140/232942308-62dfd02a-2eda-416d-b7cd-7081c42f0aba.jpg)


## Step 4 — Install MySQL on your DB Server EC2

SQL on your DB Server EC2

sudo yum update

sudo yum install mysql-server

Verify that the service is up and running by using sudo systemctl status mysqld, if it is not running, restart the service and enable it so it will be running even after reboot:

sudo systemctl restart mysqld

sudo systemctl enable mysqld

sudo systemctl status mysqld

![mysqlinstallation-on-DB](https://user-images.githubusercontent.com/111616140/232931119-e45fbf3b-0972-4bdf-b00f-1d17c438df17.jpg)

![mysqlinstallation-on-DB2](https://user-images.githubusercontent.com/111616140/232931141-d97d5f86-64ce-4842-ace9-8177b31705b8.jpg)

![mysqlinstallation-on-DB3](https://user-images.githubusercontent.com/111616140/232931147-2f6132bd-793c-4dfd-903f-a2caf57600d4.jpg)

![mysqlinstallation-on-DB4](https://user-images.githubusercontent.com/111616140/232931155-2089c8b8-75e7-4b25-a6f7-6307328bbd73.jpg)

![mysqlinstallation-on-DB5](https://user-images.githubusercontent.com/111616140/232931168-437e84f9-547a-41f3-91ed-96fd790be5bd.jpg)

![mysqlinstallation-on-DB6](https://user-images.githubusercontent.com/111616140/232931177-3aa1b798-bba3-48a4-9189-128c6b0aef3b.jpg)

![mysqlinstallation-on-DB7](https://user-images.githubusercontent.com/111616140/232931205-1568b8c4-160d-45a1-a240-cbb81dea3e48.jpg)

![mysqlinstallation-on-DB8](https://user-images.githubusercontent.com/111616140/232931216-8526ad28-c55e-48cf-a518-6ccedb1faf6f.jpg)

![mysqlinstallation-on-DB9](https://user-images.githubusercontent.com/111616140/232931227-38cbc9c0-26e0-4b13-adcb-5431eefd7f2b.jpg)

![mysqlinstallation-on-DB10](https://user-images.githubusercontent.com/111616140/232931242-477c9daf-e488-452c-b12e-154058fd068e.jpg)


## Step 5 — Configure DB to work with WordPress
sudo mysql_secure_installation

sudo mysql -u root -p

CREATE DATABASE wordpress;

show databases;

CREATE USER `myuser`@`<Web-Server-Private-IP-Address>` IDENTIFIED BY 'mypass';

GRANT ALL PRIVILEGES ON wordpress.* TO 'myuser'@'<Web-Server-Private-IP-Address>';
  
FLUSH PRIVILEGES;
  
SHOW DATABASES;
  
exit

![step5-1](https://user-images.githubusercontent.com/111616140/232935029-11619bf3-6721-4241-bb88-557f2f3ab1c7.jpg)

![step5-2](https://user-images.githubusercontent.com/111616140/232935037-4d010e39-2cdb-4a97-a9a0-585b1f7e094f.jpg)

![step5-3](https://user-images.githubusercontent.com/111616140/232935053-daf2f836-f8e5-4c6b-a158-aba0d85f2599.jpg)


 Step 6 — Configure WordPress to connect to remote database/Testing the configurations 
  
![testing-the-webconfig](https://user-images.githubusercontent.com/111616140/232939438-27d2df73-44a9-4cb5-a88c-37910ebb3918.jpg)

![testing-the-webconfig2](https://user-images.githubusercontent.com/111616140/232940878-5acbd5ef-9492-4ab7-96c4-9e7f501c2201.jpg)

![testing-the-webconfig3](https://user-images.githubusercontent.com/111616140/232940886-b23226e8-28ad-4b41-b913-e39ff0e792a8.jpg)

![testing-the-webconfig4](https://user-images.githubusercontent.com/111616140/232940898-b1358da6-911a-4fe2-8bd2-c0c577ad4f1c.jpg)

![testing-the-webconfig-wordpress](https://user-images.githubusercontent.com/111616140/232940908-468da11e-e0e2-4b41-9895-78262a8d7d0b.jpg)

![testing-the-webconfig-wordpress2](https://user-images.githubusercontent.com/111616140/232940913-01b76e79-b2a6-4e92-986d-1aa7ddc86535.jpg)
