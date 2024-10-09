-    # AWS_Route53-Cert_bot
This Repo has project how to impliment dns record in route53 and configure cert_bot for tls ssl certification to domain name records.

-    # Use ubuntu 20.04
    sudo apt update && apt install -y nginx
    sudo apt update && sudo apt install certbot python3-certbot-nginx

-    # Creation of files and permissions
    sudo mkdir -p /var/www/mohitmeshram.shop/html
    sudo chown -R $USER:$USER /var/www/mohitmeshram.shop/html
    sudo chmod -R 755 /var/www/mohitmeshram.shop
    sudo vim /var/www/mohitmeshram.shop/html/index.html

-    # Copy the following data in index.html file
    <html>
    <head>
        <title>Welcome to mohitmeshram.shop!</title>
    </head>
    <body>
        <h1>Success! The mohitmeshram.shop server block is working!</h1>
    </body>
    </html>

-    # Creation of nginx site availibility file
    sudo vim /etc/nginx/sites-available/mohitmeshram.shop

-    # Copy the following data in nginx site availibility file
    server {
        listen 80;
        listen [::]:80;

        root /var/www/mohitmeshram.shop/html;
        index index.html index.htm index.nginx-debian.html;

        server_name mohitmeshram.shop www.mohitmeshram.shop;

        location / {
                try_files $uri $uri/ =404;
        }
    }

-    # Enable the site-availbility file
    sudo ln -s /etc/nginx/sites-available/mohitmeshram.shop /etc/nginx/sites-enabled/

-    # Test the nginx server and restart the nginx service
    sudo nginx -t
    sudo systemctl restart nginx
    
-    # Cert-Bot installation
    sudo certbot certonly \
    --agree-tos \
    --email mohitmeshram0301@gmail.com \
    --manual \
    --preferred-challenges=dns \
    -d *.mohitmeshram.shop \
    --server https://acme-v02.api.letsencrypt.org/directory

![COPY THIS -challenge to create a dns txt record in route53](https://github.com/user-attachments/assets/3fdcc8f1-ec35-4340-b1a3-b30ecc1f28d2)



-    # If we need to get individual ssl certs we can perform following:
         sudo certbot --nginx



