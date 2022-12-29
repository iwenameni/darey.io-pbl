
# LAMP STACK IMPLEMENTATION

## Step 1: Installing Apache and updating the firewall

Commands:

sudo apt update

sudo apt install apache2

sudo systemctl status apache2

![sudo-apt-update](https://user-images.githubusercontent.com/111616140/209890803-8d32deaa-13dd-4311-9ca0-36db8da3cce0.png)

![sudo-apt-install-apache2](https://user-images.githubusercontent.com/111616140/209890816-64769d1b-b3b1-49cc-bcec-3cecf204ed97.png)

![sudo systemctl status apache2](https://user-images.githubusercontent.com/111616140/209890825-646ccc73-7e6f-40c0-a641-290c42692e6b.png)

![testing-my-http-server](https://user-images.githubusercontent.com/111616140/209891118-ab016578-f88e-41ec-acad-040ab6ce95eb.png)

## Step 2: Installing MYSQL

Commands:

sudo apt install mysql-server

![sudo-apt-install-mysql-server](https://user-images.githubusercontent.com/111616140/209891629-3ea1436d-9a1d-4d3b-9c1c-95bbc3a7c629.png)

sudo mysql

![sudo mysql](https://user-images.githubusercontent.com/111616140/209891644-fb4f0eaf-8f00-4132-a525-e0b1bf2dc803.png)

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';

sudo mysql_secure_installation

![mysql-secure-installation](https://user-images.githubusercontent.com/111616140/209892012-9b5f4ea9-f0dd-44bb-b1a1-9a13d00ece85.jpg)

sudo mysql -p

![password login on MySQL](https://user-images.githubusercontent.com/111616140/209892022-7e31f093-375a-4d0b-bf11-fc9e102c2ee5.png)

## Step 3: Installing PHP

Commands:

sudo apt install php libapache2-mod-php php-mysql

php -v

![installing-php](https://user-images.githubusercontent.com/111616140/209892510-9fb90e3a-e5a2-42fa-93dd-fe1b2c682dd2.jpg)

##Step 4: Creating a virtual host for my website using Apache

Commands:

sudo mkdir /var/www/projectlamp

sudo chown -R $USER:$USER /var/www/projectlamp

sudo vi /etc/apache2/sites-available/projectlamp.conf

sudo ls /etc/apache2/sites-available

sudo a2ensite projectlamp

sudo a2dissite 000-default

sudo apache2ctl configtest

sudo systemctl reload apache2

![creating-a-virtual-host-for-my-website](https://user-images.githubusercontent.com/111616140/209893157-adbe1aeb-43b7-4b87-9060-69673159d0c9.jpg)

## Step 5: Enable PHP on the website

sudo vim /etc/apache2/mods-enabled/dir.conf

sudo systemctl reload apache2

vim /var/www/projectlamp/index.php

sudo rm /var/www/projectlamp/index.php

![enabling-php-on-my-website](https://user-images.githubusercontent.com/111616140/209893180-00a6b807-5cc8-45b6-9d96-b445c3290fc5.jpg)

![testing-my-php-installation-environment](https://user-images.githubusercontent.com/111616140/209893186-dd2247d7-e53e-4c10-ad1b-5a32672219c5.jpg)
