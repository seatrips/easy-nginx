# easy-nginx

## first check easy-ssl

## 1- Installation
```
sudo apt purge apache2
sudo apt install nginx
sudo nano /etc/nginx/sites-available/default
```
## 2- Edit
```
server {
    listen 80 default;
    server_name YOURDOMAIN;
    rewrite ^/(.*) https://YOURDOMAIN/$1 permanent;
}
server {
    listen 443 ssl default;
    server_name YOURDOMAIN;

    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers on;
    ssl_ciphers 'EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH';

    ssl_certificate /etc/letsencrypt/live/YOURDOMAIN/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/YOURDOMAIN/privkey.pem;

    location / {
        proxy_pass http://127.0.0.1:USED PORT LIKE 9305 FOR SHIFT;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
    proxy_set_header X-Forwarded-For $remote_addr;
        proxy_cache_bypass $http_upgrade;
    }
}
```
## 3- Restart nginx
```
sudo service nginx restart
```
