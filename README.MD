<div align="center">

![Docker Build](https://img.shields.io/badge/docker-build-green)    ![Docker Automated](https://img.shields.io/docker/automated/jrottenberg/ffmpeg.svg)   ![example workflow](https://github.com/Tony-Dja/Docker-static-website/actions/workflows/github-ci.yml/badge.svg) <br /><br />
![Static Badge](https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)     ![Static Badge](https://img.shields.io/badge/Docker-2CA5E0?style=for-the-badge&logo=docker&logoColor=white)     ![Nginx](https://img.shields.io/badge/nginx-%23009639.svg?style=for-the-badge&logo=nginx&logoColor=white)     ![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white)

</div>

Site Web
----------------------

Conteneurisation d'un site web avec Docker + NGINX <br />

<strong>Automatisation GitHub Actions</strong> => Build & Push sur Dockerhub <br />

<div align="center">

![Screen](https://github.com/Tony-Dja/Docker-contenerized-website/blob/4ed25e9c079d1e200becd87664d73295129705c4/screenshots/build-push.png)

</div>

Le conteneur Docker embarque un serveur web NGINX. Il est exposé sur son port 80.

Les fichiers du site web sont copiés directement dans le conteneur, à la racine du dossier HTML du serveur web.<br />
Dans le Dockerfile => COPY . /var/www/html/

Vous pouvez remplacer ces fichiers par ceux de votre propre site web.


Template
----------------------

Le site est basé sur un template Dimension en HTML 5 UP => https://html5up.net/


Pipeline CI/CD
----------------------

Nous utiliserons les GitHub Actions pour effectuer la livraison continue de notre image Docker.
Pour chaque modification du site envoyée sur le Repository, action "PUSH", une nouvelle version de l'image sera builder automatiquement et stocker sur DockerHub

```
# CI/CD Docker Website => Build & Push to DockerHub

name: Web site > Build & Push
# Trigger
on:
  # Push ou Pull Request on @main
  push:
    branches: [ main ] 

# Start Jobs
jobs:
  configuration: # Environnement config
    runs-on: ubuntu-latest
    steps:

    # Checkout du repo
    - name: Checkout App Code
      uses: actions/checkout@v3

    # Login to DockerHub
    - name: Login to Docker Hub
      uses: docker/login-action@v2
      with:
        username: ${{ secrets.DOCKERHUB_USERNAME }}
        password: ${{ secrets.DOCKERHUB_TOKEN }}

    # Setup BuildKit builder
    - name: Set up Docker Buildx
      uses: docker/setup-buildx-action@v2
    
    # Build & Push website
    - name: Build and push website
      uses: docker/build-push-action@v4
      with:
        push: true
        tags: ${{ secrets.DOCKERHUB_USERNAME }}/static-website:latest
```

Image Docker : <br />
https://hub.docker.com/repository/docker/tonydja/static-website/general

<div align="center">

![Screen](https://github.com/Tony-Dja/Docker-contenerized-website/blob/6844912bdbc3d61d07958bac0c192fb337e61800/screenshots/image-docker.png)

</div>


Builder l'image
----------------------

```
docker build -t webapp:v1 .
docker images
```

Lancemant du conteneur NGINX
----------------------

```
docker run --name webapp -d -p 8080:80 webapp:v1
docker ps
```

Se connecter sur le conteneur "webapp"<br />

```
docker exec -it webapp /bin/bash
cd /var/www/html
```

Docker compose
----------------------

L'image Docker étant déjà existante sur mon Registry DockerHub, si vous le souhaitez, vous pouvez déployer directement sans passer par le Build et le Run, en utilisant le fichier docker-compose.yml<br />

```
docker compose up -d
```


Afficher le site web
----------------------

http://localhost:8080


![Screen](https://github.com/Tony-Dja/Docker-contenerized-website/blob/6a419e725c7aec615cbaeca6213b02b641ced525/screenshots/website.png)
