FROM ubuntu:latest
LABEL org.opencontainers.image.authors="anjon.sarker@gmail.com"

ARG USERNAME=anjon
EXPOSE 22

# Apt update & apt install required packages & Remove cache
RUN apt-get update && apt-get install --no-install-recommends --no-install-suggests -y \
    openssh-server sudo net-tools less aptitude iputils-ping man vim python3 && \
    apt-get -y autoremove && apt-get -y autoclean && apt-get -y clean all && \
    rm -rf /var/lib/apt/lists/*

# Add a non-root user
RUN useradd -ms /bin/bash $USERNAME 

# Create the ssh directory and authorized_keys file
USER $USERNAME
RUN mkdir /home/$USERNAME/.ssh
COPY keycontainer.pub /home/$USERNAME/.ssh/authorized_keys

USER root
RUN chown $USERNAME /home/$USERNAME/.ssh/authorized_keys && \
    chmod 600 /home/$USERNAME/.ssh/authorized_keys && \
    echo "${USERNAME} ALL=(ALL) NOPASSWD: ALL " >> /etc/sudoers

# Run ssh service
RUN service ssh start
CMD ["/usr/sbin/sshd","-D"]
