# HOW TO CREATE A TOMCAT IMAGE FROM OUR BASE IMAGE
#
#--tag or -t to name the image
#--file or -f path to Dockerfile
# docker image build --file <path_to_Dockerfile> --tag <REPOSITORY>:<TAG> .
# dont forget the "." at the end of the line, it tells docker to build the image in the current folder
# for example: docker image build --tag local:dockerfile-example .



#The structure of the ENV instruction is as follows:
#ENV <key> <value>
#ENV username admin
#Alternatively, you can always use an equals sign between the two:
#ENV <key>=<value>
#ENV username=admin
#Now, the question is why do they have two and what are the differences? With the
#first example, you can only set one ENV per line. With the second ENV example, you
#can set multiple environmental variables on the same line:
#ENV username=admin database=db1 tableprefix=pr2_
#You can view what environmental variables are set on an image using the Docker
#inspect command:
#$ docker image inspect <IMAGE_ID>


#DOCKER NETWORKING
#Creates a network between docker containers

Beispiel: 1 redis_Datencontainer und 1 Anwendungscontainer werden vernetzt, Anwendungsserver sichert sein SystemState in den Redis-Daten-Container:
$ docker image pull redis:alpine
$ docker image pull russmckendrick/moby-counter
$ docker network create moby-counter

Redis Container starten:
$ docker container run -d --name redis --network moby-counter redis:alpine
#--network defines the network that the Redis container is launched

Anwendungscontainer starten:
$ docker container run -d --name moby-counter --network moby-counter -p 8080:80 russm
check: http://localhost:8080/

docker container exec moby-counter ping -c 3 redis
# ping the redis container from the moby-counter application

$ docker container exec moby-counter cat /etc/hosts
# check hostfile of the redis container

$ docker container exec moby-counter cat /etc/resolv.conf
# check resolv.conf

$ docker container exec moby-counter nslookup redis 127.0.0.11
#DNS lookup on redis against 127.0.0.11 to return the IP Adress of the redis container

#Laufwerke / Volumes anzeigen:
docker volume ls

# Volume beim Starten einhängen:
$ docker container run -d --name redis -v 719d0cc415dbc76fed5e9b8893e2cf547f0ac6c91233451604fdba31f0dd2d2a

# Inhalt des Volumes auslesen:
docker container exec redis ls -lhat /data

#Infos auslesen
$ docker volume inspect redis_data

$ docker-compose run --volume data_volume:/app composer install
This would run the composer container with the install command and mount the
data_volume to /app within the container.
