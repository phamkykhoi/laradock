
## 1. Download docker and install
- Link download: https://docs.docker.com/desktop/windows/install/
## 2. Login to docker with an account
- Create an account on https://hub.docker.com/signup

## 3. Install Laradock 

After clone code from repo: https://github.com/phamkykhoi/laradock.git

- Step1. Change copy file .env.example to .env
- Step2. Config in .env file
```
APP_CODE_PATH_HOST: Your local folder include project folder
```
- Step3: Run command bellow 
    - docker-compose build --no-cache php-fpm
    - docker-compose build --no-cache nginx
    - docker-compose build --no-cache mysql
    - docker-compose build --no-cache phpmyadmin
    - docker-compose build --no-cache redis
    - docker-compose up -d php-fpm nginx mysql phpmyadmin redis
    - docker exec -it laradock_workspace_1 bash
## How to run a PHP Project in Laradock
- Config virtual host
    - Create a file in folder nginx/sites. Ex: demo.app.conf
    - Content in demo.app.conf like bellow
    ```
        server {
        listen 80;
        listen [::]:80;

        # For https
        # listen 443 ssl;
        # listen [::]:443 ssl ipv6only=on;
        # ssl_certificate /etc/nginx/ssl/default.crt;
        # ssl_certificate_key /etc/nginx/ssl/default.key;

        server_name demo.app.local;
        root /var/www/your-project-folder-name;
        index index.php index.html index.htm;

        location / {
            try_files $uri $uri/ /index.php$is_args$args;
        }

        location ~ \.php$ {
            try_files $uri /index.php =404;
            fastcgi_pass php-upstream;
            fastcgi_index index.php;
            fastcgi_buffers 16 16k;
            fastcgi_buffer_size 32k;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            fastcgi_read_timeout 600;
            include fastcgi_params;
        }

        location ~ /\.ht {
            deny all;
        }

        location /.well-known/acme-challenge/ {
            root /var/www/letsencrypt/;
            log_not_found off;
        }

        error_log /var/log/nginx/app_error.log;
        access_log /var/log/nginx/app_access.log;
    }
    ```
    
   - Config file hosts on your machine
    
      - Ex: 127.0.0.1 demo.app.local
      - Guide: https://docs.google.com/document/d/10vIofJLGKrtpIh3A9ztczSFyf71xUcvKDnLcTVw4AuU/edit?usp=sharing
## Run your website
- Open chrome and run with domain: demo.app.local


### Note
Restart a container

Ex: 

    - docker exec f416f7321dce nginx -s reload
    
    - docker-compose restart nginx
    
    - docker-compose up -d --build --force-recreate mysql
    
Mutltil PHP Version

https://msirius.medium.com/1-n-php-versions-and-projects-via-laradock-51938b337071

https://raw.githubusercontent.com/dog5tar/laradock-configs/master/docker-compose.yml
