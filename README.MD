![Static Badge](https://img.shields.io/badge/Docker-2CA5E0?style=for-the-badge&logo=docker&logoColor=white)     ![Nginx](https://img.shields.io/badge/nginx-%23009639.svg?style=for-the-badge&logo=nginx&logoColor=white)     ![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white)

Site Web
----------------------

Conteneurisation d'un site web statique avec Docker + NGINX


Template
----------------------

Le site est basé sur un template Dimension en HTML 5 UP => https://html5up.net/


Builder l'image
----------------------

docker build -t webapp:v1 .
docker images


Lancemant du conteneur NGINX
----------------------

docker run --name webapp -d -p 80:80 webapp:v1
docker ps

Se connecter sur le conteneur webapp
docker exec -ti webapp /bin/bash
cd /var/www/html


Afficher le site web
----------------------

http://localhost


