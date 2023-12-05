# Sample Docker Compose file

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
$ docker exec curl curl http://nginx01 -s
nginx01

$ docker exec curl curl http://nginx02 -s
nginx02
```

<br>Access to the VIP
```
$ docker exec curl curl http://haproxy -s
nginx01

$ docker exec curl curl http://haproxy -s
nginx02
```