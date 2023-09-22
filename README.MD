<div align="center">

![Docker Build](https://img.shields.io/badge/docker-build-green)    ![Docker Automated](https://img.shields.io/docker/automated/jrottenberg/ffmpeg.svg)   ![example workflow](https://github.com/Tony-Dja/Docker-static-website/actions/workflows/github-ci.yml/badge.svg) <br /><br />
![Static Badge](https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)     ![Static Badge](https://img.shields.io/badge/Docker-2CA5E0?style=for-the-badge&logo=docker&logoColor=white)     ![Nginx](https://img.shields.io/badge/nginx-%23009639.svg?style=for-the-badge&logo=nginx&logoColor=white)     ![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white)

</div>

Site Web
----------------------

Conteneurisation d'un site web avec Docker + NGINX <br />
Automatisation GitHub Actions => Build & Push sur Dockerhub <br />
Image Docker : <br />
https://hub.docker.com/repository/docker/tonydja/static-website/general

Le conteneur Docker embarque un serveur web NGINX. Il est exposé sur son port 80.

Les fichiers du site web sont copiés directement dans le conteneur, à la racine du dossier HTML du serveur web.<br />
Dans le Dockerfile => COPY . /var/www/html/

Vous pouvez remplacer ces fichiers par ceux de votre site web.

Template
----------------------

Le site est basé sur un template Dimension en HTML 5 UP => https://html5up.net/


Builder l'image
----------------------

docker build -t webapp:v1 .<br />
docker images


Lancemant du conteneur NGINX
----------------------

docker run --name webapp -d -p 80:80 webapp:v1<br />
docker ps

Se connecter sur le conteneur "webapp"<br />
docker exec -it webapp /bin/bash<br />
cd /var/www/html


Afficher le site web
----------------------

http://localhost



