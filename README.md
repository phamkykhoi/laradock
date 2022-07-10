
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

### Note
Restart a container
Ex: 
    - docker exec f416f7321dce nginx -s reload
    - docker-compose restart nginx
    - docker-compose up -d --build --force-recreate mysql
    
Mutltil PHP Version

https://msirius.medium.com/1-n-php-versions-and-projects-via-laradock-51938b337071

https://raw.githubusercontent.com/dog5tar/laradock-configs/master/docker-compose.yml
