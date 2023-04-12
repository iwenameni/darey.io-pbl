PROJECT 5: IMPLEMENT A CLIENT SERVER ARCHITECTURE USING MYSQL DATABASE MANAGEMENT SYSTEM (DBMS).

Firstly we created and configured two Linux-based virtual servers (EC2 instances in AWS).

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

CREATE USER 'remote_user'@'%' IDENTIFIED WITH mysql_native_password BY 'password';

CREATE DATABASE test_db

GRANT ALL ON test_db.* TO 'remote_user'@'%' WITH GRANT OPTION;

FLUSH PRIVILEGES

sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf

sudo systemctl restart mysql

![server-config1](https://user-images.githubusercontent.com/111616140/231011209-808e5967-c940-4050-a25a-291944461a0f.jpg)

![server-config2](https://user-images.githubusercontent.com/111616140/231011223-74da2c8d-d3a6-4fb9-b7a3-b108500ab649.jpg)

![server-config3](https://user-images.githubusercontent.com/111616140/231011233-f31cb294-13d8-4d4e-82a8-d0a1d7873740.jpg)

![server-config4](https://user-images.githubusercontent.com/111616140/231011245-d9e538c4-5770-48c7-b76b-b83e5957f18f.jpg)

![server-config5](https://user-images.githubusercontent.com/111616140/231011261-f797480d-af4b-4ff0-8a07-7c6bc0712be3.jpg)


Having successfully set up mysql on sevrer, 

we then try to connect remotely to the mysql server via the client instance

sudo mysql -u remote_user -h 172.31.48.247 -p

We try to run some basic mysql commands;

Show databases;

![connecting-to-server-via-client-instance](https://user-images.githubusercontent.com/111616140/231011288-c1e4284c-bc8e-4141-b993-77a016346230.jpg)
