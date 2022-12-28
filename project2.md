# WEB STACK IMPLEMENTATION (LEMP STACK)
## Step 1: Installing the Nginx web server
Commands:

sudo apt update

sudo apt install nginx

sudo systemctl status nginx

![sudo-apt-update](https://user-images.githubusercontent.com/111616140/209610136-d013cc76-8c62-49a8-a606-7a17ec6589de.png)
![sudo-apt-install-nginx](https://user-images.githubusercontent.com/111616140/209610245-f1cbe912-233f-4bcc-b982-baf37a067cf0.png)
![sudo-systemctl-status-nginx](https://user-images.githubusercontent.com/111616140/209610316-174359ef-d982-417e-ac6f-2986951546b1.png)
## Step 2 — Installing MYSQL

Commands:

sudo apt install mysql-server

sudo mysql
![sudo-apt-install-mysql-server-1](https://user-images.githubusercontent.com/111616140/209611228-1499238e-95b2-4242-bd38-cc47a977d702.png)
![sudo-apt-install-mysql-server-2](https://user-images.githubusercontent.com/111616140/209611246-e5740e22-94aa-4037-97b7-9b9c875ca548.png)
![sudo-mysql](https://user-images.githubusercontent.com/111616140/209611264-77e30767-a8ff-4ce9-8b85-44400ac7c762.jpg)
##Step 3: Installing php

Commands:

sudo apt install php-fpm php-mysql
![Installing-php](https://user-images.githubusercontent.com/111616140/209612120-d99976f9-1f6a-4c2b-b69f-63cc8e6ede28.jpg)
## Step 4: Configuring Nginx to use PHP Processor

Commands:

sudo mkdir /var/www/projectLEMP

sudo chown -R $USER:$USER /var/www/projectLEMP

sudo nano /etc/nginx/sites-available/projectLEMP

sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/

sudo nginx -t

sudo unlink /etc/nginx/sites-enabled/default

sudo systemctl reload nginx
![Configuring-Nginx](https://user-images.githubusercontent.com/111616140/209766306-da1f6485-cf7a-4aba-ab08-5cedcd7618eb.jpg)
![Website-test](https://user-images.githubusercontent.com/111616140/209766455-7cfdc9a2-01d5-4e3e-b57f-ab1dd99299db.jpg)
