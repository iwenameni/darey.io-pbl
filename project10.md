### PROJECT 10: LOADBALANCER SOLUTION WITH NGINX AND SSL/TLS

STEP 1: CONFIGURE NGINX AS A LOAD BALANCER

We start by creating an EC2 VM based on Ubuntu Server 20.04 LTS and name it Nginx LB (we open TCP port 80 for HTTP connections, also open TCP port 443 – this port is used for secured HTTPS connections)

Update /etc/hosts file for local DNS with Web Servers’ names (e.g. Web1 and Web2) and their local IP addresses

We Install and configure Nginx as a load balancer to point traffic to the resolvable DNS names of the webservers

We then connect to the instance via terminal and make further configurations.

We update the instance and install Nginx

codes;

sudo apt update && sudo apt install nginx -y

sudo systemctl enable nginx && sudo systemctl start nginx


Restart Nginx and make sure the service is up and running

sudo systemctl restart nginx

sudo systemctl status nginx

Open the default nginx configuration file and insert following configuration

sudo vi /etc/nginx/sites-available/load_balancer.conf

 upstream myproject {
 
    server Web1 weight=5;
    
    server Web2 weight=5;
    
  }

server {

    listen 80;
    
    server_name www.domain.com;
    
    location / {
    
      proxy_pass http://myproject;
      
    }
    
  }

 sudo rm -f /etc/nginx/sites-enabled/default
 
sudo nginx -t

cd /etc/nginx/sites-enabled/

sudo ln -s ../sites-available/load_balancer.conf

ll

load_balancer.conf -> ../sites-available/load_balancer.conf

Restart Nginx and make sure the service is up and running

sudo systemctl reload nginx

STEP 2: REGISTER A NEW DOMAIN NAME AND CONFIGURE SECURED CONNECTION USING SSL/TLS CERTIFICATES

sudo apt install certbot -y

sudo apt install python3-certbot-nginx -y

sudo nginx -t && sudo nginx -s reload

sudo certbot --nginx -d toolingike.site -d www.toolingike.site

crontab -e

![prj10-1](https://github.com/iwenameni/darey.io-pbl/assets/111616140/ba9ca869-23d0-4fc9-bf6b-638e6e4c3c08)

![prj10-2](https://github.com/iwenameni/darey.io-pbl/assets/111616140/da9debcb-0ac2-4b0c-a652-a8a852b5d23d)

![prj10-3](https://github.com/iwenameni/darey.io-pbl/assets/111616140/8da1f6cd-e273-48ee-905e-49cb4b59c708)

![prj10-4](https://github.com/iwenameni/darey.io-pbl/assets/111616140/28c8bdd4-304b-4bca-b2a9-12b9de79fee6)

![prj10-5](https://github.com/iwenameni/darey.io-pbl/assets/111616140/f57a88a2-786c-4e1f-81a7-5bc3d093771f)

![prj10-6](https://github.com/iwenameni/darey.io-pbl/assets/111616140/b21519f7-ec28-4828-9491-6533a28ba154)

![secure-web-lb](https://github.com/iwenameni/darey.io-pbl/assets/111616140/3d298fe4-944d-43a8-92ec-152114cb8ecd)

![unsecure-nginx-lb-web](https://github.com/iwenameni/darey.io-pbl/assets/111616140/84b7d269-6523-40ec-87b7-f5cac3c5ee39)

![cert](https://github.com/iwenameni/darey.io-pbl/assets/111616140/7d78bee7-0813-4317-8b5e-af87ab7aa14d)
