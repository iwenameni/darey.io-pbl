### LOAD BALANCER SOLUTION WITH APACHE

Install apache2

sudo apt update

sudo apt install apache2 -y

sudo apt-get install libxml2-dev

Enable following modules:

sudo a2enmod rewrite

sudo a2enmod proxy

sudo a2enmod proxy_balancer

sudo a2enmod proxy_http

sudo a2enmod headers

sudo a2enmod lbmethod_bytraffic

Now restart apache2 service

sudo systemctl restart apache2

sudo systemctl status apache2

Open the default etc file file and add the configurations provided

sudo vi /etc/apache2/sites-available/000-default.conf

Restart apache server

sudo systemctl restart apache2

Verify that our configuration works – try to access your LB’s public IP address or Public DNS name from your browser:

http://<Load-Balancer-Public-IP-Address-or-Public-DNS-Name>/index.php
  
  ![prj8-1](https://github.com/iwenameni/darey.io-pbl/assets/111616140/8b630fec-27f0-47e6-a4ba-7c554cdee76b)
  
![prj8-2](https://github.com/iwenameni/darey.io-pbl/assets/111616140/5d57c55d-c9c3-4609-be4f-7f001f642828)
  
![prj8-3](https://github.com/iwenameni/darey.io-pbl/assets/111616140/c8192a79-3c53-4c43-9c7f-2cc7bc72a737)
  
![prj8-4](https://github.com/iwenameni/darey.io-pbl/assets/111616140/0535bf28-9042-4d4b-8449-e057157e5f26)
  
![prj8-5](https://github.com/iwenameni/darey.io-pbl/assets/111616140/bc771728-86e9-4659-93eb-1d1afd0ae9cb)
  
![testing-lb-config](https://github.com/iwenameni/darey.io-pbl/assets/111616140/a6b4348f-d9a8-44a5-be4b-3a0f96a119df)
