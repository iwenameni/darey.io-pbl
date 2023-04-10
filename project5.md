PROJECT 5: IMPLEMENT A CLIENT SERVER ARCHITECTURE USING MYSQL DATABASE MANAGEMENT SYSTEM (DBMS).

Firstly we Created and configured two Linux-based virtual servers (EC2 instances in AWS).

Server A name - `mysql server`

Server B name - `mysql client`

On mysql server Linux Server we installed MySQL Server software.

On mysql client Linux Server install MySQL Client software.

We then configured the client server by running these various codes;

sudo apt update -y

sudo apt install mysql-server -y

sudo systemctl enable mysql

ssh into the client server and install mysql client

Codes:

sudo apt update

sudo apt install mysql-client -y

Going back to the mysql server instance, we set configure and set up mysql

sudo mysql_secure_installation

mysql -u root -p

CREATE USER 'remote_user'@'%' IDENTIFIED WITH mysql_native_password BY 'Bigboy2zones@';

CREATE DATABASE test_db

GRANT ALL ON test_db.* TO 'remote_user'@'%' WITH GRANT OPTION;

FLUSH PRIVILEGES

sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf

sudo systemctl restart mysql



We have successfully set up mysql on sevrer 

We then try to connect remotely to the mysql server via the client instance

sudo mysql -u remote_user -h 172.31.48.247 -p

We try to run some basic mysql commands;

Show databases;
