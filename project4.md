PROJECT 4: MEAN STACK DEPLOYMENT TO UBUNTU ON AWS

Step 1: Install NodeJs

Commands:

sudo apt update

sudo apt upgrade

Add certiciates with the following commands

sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates

curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -

sudo apt install -y nodejs

![installing-nodeJs-1](https://user-images.githubusercontent.com/111616140/221384559-5a005814-ccb9-4370-af45-586fa24c0422.jpg)

![installing-nodeJs-2](https://user-images.githubusercontent.com/111616140/221384562-4b2a2afe-2f85-42c8-9c30-da43f75fb42e.jpg)

![installing-nodeJs-3](https://user-images.githubusercontent.com/111616140/221384566-3dc5cfae-5615-41b4-afd8-19e29e6128bc.jpg)

![installing-nodeJs-4](https://user-images.githubusercontent.com/111616140/221384569-f4285f2a-8c08-404c-a44f-a343d3bcf3e7.jpg)

![installing-nodeJs-5](https://user-images.githubusercontent.com/111616140/221384571-1c6ddaec-3221-4397-a49e-94e5fd577d9e.jpg)

![installing-nodeJs-6](https://user-images.githubusercontent.com/111616140/221384576-264e1495-d9b3-4f14-911b-829e9b251de2.jpg)


Step 2: Install MongoDB

Commands:

sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6

echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list

sudo apt install -y mongodb

sudo service mongodb start

sudo systemctl status mongodb

sudo apt install -y npm

sudo npm install body-parser

mkdir Books && cd Books

npm init

vi server.js

![installing-mongoDB-1](https://user-images.githubusercontent.com/111616140/221384933-cc0c339f-50ad-4dd8-b17d-a9f1918f3927.jpg)

![installing-mongoDB-2](https://user-images.githubusercontent.com/111616140/221384936-b30a9eef-fdd2-48fe-9acb-9e7d9387e355.jpg)

![installing-mongoDB-3](https://user-images.githubusercontent.com/111616140/221384938-b1c6d3dc-447b-4910-a2f3-f1ea6f560d90.jpg)

![installing-mongoDB-4](https://user-images.githubusercontent.com/111616140/221384945-c9ba8b8e-be6f-47e3-8aa1-3c2002576083.jpg)

![installing-mongoDB-5](https://user-images.githubusercontent.com/111616140/221384946-3a639839-4b73-4ecf-926a-4546249cbf7f.jpg)

![installing-mongoDB-6](https://user-images.githubusercontent.com/111616140/221384954-50d9172a-447e-4157-8842-f7ad3adab187.jpg)

![installing-mongoDB-7](https://user-images.githubusercontent.com/111616140/221385027-9e37f830-20aa-4265-a3ef-3cd6b0dcb6c3.jpg)


Step 3: Install Express and set up routes to the server

Commands:

sudo npm install express mongoose

mkdir apps && cd apps

vi routes.js

mkdir models && cd models

vi book.js

![installing-mongoDB-7](https://user-images.githubusercontent.com/111616140/221385027-9e37f830-20aa-4265-a3ef-3cd6b0dcb6c3.jpg)
![install-express-1](https://user-images.githubusercontent.com/111616140/221385158-119dd182-bf54-4d59-973a-9a2b9583efcb.jpg)
![install-express-2](https://user-images.githubusercontent.com/111616140/221385162-6662bc2b-aed7-488f-a52f-560b5e41db1a.jpg)


Step 4: Access the routes with AngularJS

cd ../..

mkdir public && cd public

vi script.js

vi index.html

cd ..

node server.js

curl -s http://localhost:3300

![accessing-the-routes-with-AngularJs](https://user-images.githubusercontent.com/111616140/221385309-52cb5fa4-8edc-46a3-b326-6667750e18f1.jpg)
![access-book-register-from-web](https://user-images.githubusercontent.com/111616140/224818682-6859a0a2-09c6-4147-8480-0c54cf0c0876.jpg)

