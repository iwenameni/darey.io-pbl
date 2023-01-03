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
## Step 3: Installing php

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
![website-test1](https://user-images.githubusercontent.com/111616140/210191478-8afdecaf-b080-4a64-be01-9d7a2c7bc271.jpg)
## Step 5: Testing PHP with Nginx

Commands:

sudo nano /var/www/projectLEMP/info.php

I tested my php website using: http://`server_domain_or_IP`/info.php
![testing-php-with-nginx1](https://user-images.githubusercontent.com/111616140/209767962-46fddf73-c2c2-45f2-a6b1-0beaecfcea69.jpg)
![testing-php-with-nginx2](https://user-images.githubusercontent.com/111616140/209767973-33c3a219-1100-450d-8d93-b5107703d280.jpg)
## Step 6: Retrieving Data from mysql Data base with PHP

Commands:

sudo mysql

mysql> CREATE DATABASE `example_database`;

mysql>  CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'password';

mysql> GRANT ALL ON example_database.* TO 'example_user'@'%';

mysql -u example_user -p

mysql> SHOW DATABASES;

CREATE TABLE example_database.todo_list (

item_id INT AUTO_INCREMENT,

content VARCHAR(255),

PRIMARY KEY(item_id)

);

mysql> INSERT INTO example_database.todo_list (content) VALUES ("My first important item");

mysql>  SELECT * FROM example_database.todo_list;

nano /var/www/projectLEMP/todo_list.php

http://<Public_domain_or_IP>/todo_list.php

![retrieving-data-from-mysql-database-1](https://user-images.githubusercontent.com/111616140/210290478-00fc25a4-9000-404d-9b85-3b35ca6dabb2.jpg)
![retrieving-data-from-mysql-database-2](https://user-images.githubusercontent.com/111616140/210290486-4b3bfc85-dab6-4fe8-95ad-8ca24fe82bdb.jpg)
![testing-my-php-environment](https://user-images.githubusercontent.com/111616140/210290501-7db7eb15-1ce6-4db3-be31-a8443ef4661e.jpg)
