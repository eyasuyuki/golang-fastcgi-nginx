# About this project

Golang fastcgi served from Nginx on Docker.

# Clone sub-repositories

    cd golang-fastcgi-nginx
    git clone git@github.com:eyasuyuki/golang-docker.git
    git clone git@github.com:eyasuyuki/nginx.git

# Build and start all with fig

    fig build
    fig up -d

# For boot2docker user:

## Accece to nginx app

    curl -i http://$(boot2docker ip)/

## Login boot2docker host

    boot2docker ssh

## Install nsenter

    docker run --rm -v /usr/local/bin:/target jpetazzo/nsenter

## Login nginx container

    sudo docker-enter `docker ps | grep "\"nginx\"" | cut -d " " -f 1`

## Check golang container IP address

    grep "fcighost" /etc/hosts
    ping fcgihost

#  For non-fig user:

## Build and start golang fastcgi container

    cd golang-docker/hello
    docker build -t eyasuyuki/golang-hello .
    docker run -d -p 9001:9001 --name fcgihost google/golang-hello

## Build and start nginx and link fastcgi container

    cd ../../nginx
    docker build -t eyasuyuki/nginx .
    docker run -d -p 80:80 --link fcgihost:fcgihost --name nginx eyasuyuki/nginx
