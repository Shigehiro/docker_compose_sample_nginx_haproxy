# Sample Docker Compose file

## Description

This Compose file will launch four containers: one HAProxy, two Nginx, and one cURL container. You don't have to configure Nginx and HAProxy because the Docker Compose file covers those.

[![asciicast](https://asciinema.org/a/aXNsBNtrzbKULSRGSRsBk4ZDz.png)](https://asciinema.org/a/aXNsBNtrzbKULSRGSRsBk4ZDz)

## Tested Environment

```
$ tail -1 /etc/lsb-release 
DISTRIB_DESCRIPTION="Ubuntu 22.04.3 LTS"

$ docker --version
Docker version 24.0.7, build afdd53b

$ docker-compose version
docker-compose version 1.29.2, build unknown
docker-py version: 5.0.3
CPython version: 3.10.12
OpenSSL version: OpenSSL 3.0.2 15 Mar 2022
```

## Walkthrough

<br>Start the containers
```
$ docker-compose up -d
Creating network "compose_haproxy_nginx_nginx_haproxy_seg" with driver "bridge"
Creating nginx01 ... done
Creating nginx02 ... done
Creating curl    ... done
Creating haproxy ... done
```

<br>Confirm four containers are up and running
```
$ docker-compose ps
 Name                Command               State   Ports
---------------------------------------------------------
curl      /entrypoint.sh sh                Up
haproxy   docker-entrypoint.sh hapro ...   Up
nginx01   /docker-entrypoint.sh ngin ...   Up      80/tcp
nginx02   /docker-entrypoint.sh ngin ...   Up      80/tcp
```

<br>Access to the Nginx
```
$ for i in $(seq 1 2);do docker exec nginx0$i curl 127.1 -s ;done
nginx01
nginx02
```

<br>Access to the VIP to chcek if haproxy loadbalances in round-robin fashion.
```
$ for i in $(seq 1 2);do docker exec curl curl http://haproxy -s ;done
nginx01
nginx02
```
