# About this project

Golang fastcgi served from Nginx on Docker.

# Clone sub-repositories

    cd golang-fastcgi-nginx
    git clone git@github.com:eyasuyuki/golang-docker.git
    git clone git@github.com:eyasuyuki/nginx.git

# Build and start all with Docker Compose

    $(docker-machine env <vmname>)
    docker-compose up -d

## Accece to nginx app

    curl -i http://$(docker-machine ip <vmname>)/

## Login virtual machine

    docker-machine ssh <vmname>

## Install nsenter

    docker run --rm -v /usr/local/bin:/target jpetazzo/nsenter

## Login nginx container

    sudo docker-enter `docker ps | grep "\"nginx\"" | cut -d " " -f 1`

## Check golang container IP address

    grep "fcighost" /etc/hosts
    ping fcgihost
