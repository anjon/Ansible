# BASE image - used as a starting point by MASTER and HOST images
FROM ubuntu:latest
LABEL org.opencontainers.image.authors="anjon.sarker@gmail.com"

# install required packages
RUN apt-get update \
    && apt-get install --no-install-recommends --no-install-suggests -y \
        aptitude iputils-ping net-tools man vim openssh-server python3 \
    && rm -rf /var/lib/apt/lists/* 

# ensure that required directories are created
RUN mkdir /var/run/sshd /root/.ssh
