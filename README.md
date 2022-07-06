
Change file .env
APP_CODE_PATH_HOST: Your local folder
APP_CODE_PATH_CONTAINER: Folder in docker
COMPOSE_PROJECT_NAME: project_name (default is laradock)

- docker-compose build --no-cache php-fpm
- docker-compose build --no-cache nginx
- docker-compose build --no-cache mysql
- docker-compose build --no-cache phpmyadmin
- docker-compose build --no-cache redis
- docker-compose build --no-cache laravel-echo-server
- docker-compose up -d php-fpm nginx mysql postgres phpmyadmin redis
- docker-compose up -d --build --force-recreate mysql
- docker exec -it laradock_workspace_1 bash

Restart a container

Ex: docker exec f416f7321dce nginx -s reload
    docker-compose restart nginx

Mutltil PHP Version

https://msirius.medium.com/1-n-php-versions-and-projects-via-laradock-51938b337071

https://raw.githubusercontent.com/dog5tar/laradock-configs/master/docker-compose.yml