**AWS_Route53-Cert_bot**

![aws-route53-certbot-logo](https://github.com/user-attachments/assets/ce157e99-53aa-4fc0-9ef8-7edf5f20e39d)<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 400 200">
  <rect width="400" height="200" fill="#232F3E"/>
  <text x="200" y="80" font-family="Arial, sans-serif" font-size="24" fill="#FF9900" text-anchor="middle">AWS Route53</text>
  <text x="200" y="120" font-family="Arial, sans-serif" font-size="24" fill="#00A86B" text-anchor="middle">Cert-bot Project</text>
  <path d="M100,140 Q200,180 300,140" stroke="#FF9900" stroke-width="4" fill="none"/>
  <circle cx="200" cy="160" r="15" fill="#00A86B"/>
  <path d="M185,160 L215,160 M200,145 L200,175" stroke="#232F3E" stroke-width="3"/>
</svg>



This Repo has project how to impliment dns record in route53 and configure cert_bot for tls ssl certification to domain name records.

- Use ubuntu 20.04

      sudo apt update && apt install -y nginx
      sudo apt update && sudo apt install certbot python3-certbot-nginx

- Creation of files and permissions

      sudo mkdir -p /var/www/mohitmeshram.shop/html
      sudo chown -R $USER:$USER /var/www/mohitmeshram.shop/html
      sudo chmod -R 755 /var/www/mohitmeshram.shop
      sudo vim /var/www/mohitmeshram.shop/html/index.html

- Copy the following data in index.html file

        <html>
        <head>
        <title>Welcome to mohitmeshram.shop!</title>
        </head>
        <body>
        <h1>Success! The mohitmeshram.shop server block is working!</h1>
        </body>
        </html>

- Creation of nginx site availibility file

        sudo vim /etc/nginx/sites-available/mohitmeshram.shop

- Copy the following data in nginx site availibility file

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

- Enable the site-availbility file

        sudo ln -s /etc/nginx/sites-available/mohitmeshram.shop /etc/nginx/sites-enabled/

- Test the nginx server and restart the nginx service

      sudo nginx -t
        sudo systemctl restart nginx
    
- Cert-Bot installation

        sudo certbot certonly \
        --agree-tos \
        --email mohitmeshram0301@gmail.com \
        --manual \
        --preferred-challenges=dns \
        -d *.mohitmeshram.shop \
        --server https://acme-v02.api.letsencrypt.org/directory

![COPY THIS -challenge to create a dns txt record in route53](https://github.com/user-attachments/assets/3fdcc8f1-ec35-4340-b1a3-b30ecc1f28d2)



- If we need to get individual ssl certs we can perform following:

        sudo certbot --nginx



