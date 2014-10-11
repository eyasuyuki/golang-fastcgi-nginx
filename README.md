# About this project

Golang fastcgi served from Nginx on Docker.

# Build and start golang fastcgi container

    cd golang-docker/hello
    docker build -t google/golang-hello .
    docker run -d -p 9001:9001 --name fcgihost google/golang-hello

# Build and start nginx and link fastcgi container

    cd ../../nginx
    docker build -t dockerfile/nginx .
    docker run -d -p 80:80 --link fcgihost:fcgihost --name nginx dockerfile/nginx

# For boot2docker user:

## Logging in boot2docker host

    boot2docker ssh

## Install nsenter

    docker run --rm -v /usr/local/bin:/target jpetazzo/nsenter

## Logging in nginx container

    sudo docker-enter `docker ps | grep "dockerfile/nginx" | cut -d " " -f 1`

## Check golang container IP address

    [ root@ff9ebd359af1:~ ]$ cat /etc/hosts
    172.17.0.16	ff9ebd359af1
    ff02::2	ip6-allrouters
    127.0.0.1	localhost
    ::1	localhost ip6-localhost ip6-loopback
    fe00::0	ip6-localnet
    ff00::0	ip6-mcastprefix
    ff02::1	ip6-allnodes
    172.17.0.14	fcgihost

    [ root@ff9ebd359af1:~ ]$ ping fcgihost
    PING fcgihost (172.17.0.14) 56(84) bytes of data.
    64 bytes from fcgihost (172.17.0.14): icmp_seq=1 ttl=64 time=0.206 ms
    64 bytes from fcgihost (172.17.0.14): icmp_seq=2 ttl=64 time=0.130 ms
    ^C
    --- fcgihost ping statistics ---
    2 packets transmitted, 2 received, 0% packet loss, time 999ms
    rtt min/avg/max/mdev = 0.130/0.168/0.206/0.038 ms

