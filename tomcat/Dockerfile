# Version 1.0

FROM alpine:latest
#uses the latest base-image from alpine linux

#maintainer="Buzz Ruckz <buzz.ruckz@web.de>"
#description="This Dockerfile installs Tomcat"

RUN apk add --update tomcat && \
        rm -rf /var/cache/apk/* && \
        mkdir -p /tmp/tomcat/
		
# first line installs tomcat, && \ beginns a new line
# second line removes temporary files to keep the image size to a minimum
# third line creates a folder

# RUN mkdir /data && chown redis:redis /data
VOLUME /data
WORKDIR /data

COPY tomdaten/test.txt /tmp/tomcat/test.txt
#copies the text.txt file from the host folder tomdaten to the tmp/tomcat folder in the container

EXPOSE 80/tcp
# tells docker to open port 80 of the container for the service (its not mapping the port to the host)



