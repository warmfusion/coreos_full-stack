# The container ensures the consul agent is made avaliable at /bin/consul

FROM debian:wheezy
MAINTAINER Toby Jackson <toby@warmfusion.co.uk>


RUN apt-get update && apt-get install unzip
ADD https://dl.bintray.com/mitchellh/consul/0.5.2_linux_amd64.zip /tmp/consul.zip
RUN cd /bin && unzip /tmp/consul.zip && chmod +x /bin/consul && rm /tmp/consul.zip


# Clean up after ourselves to slim down the dockerfile
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Flatten the docker image with:
#
#ID=$(docker run -d image-name /bin/bash)
#docker export $ID | docker import – flat-image-name