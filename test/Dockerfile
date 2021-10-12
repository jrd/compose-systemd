# syntax=docker/dockerfile:1.2
FROM debian:11
VOLUME /var/lib/docker
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y \
        curl \
        docker.io \
        python3 \
        python3-pip \
        ssh \
        sudo \
        systemd \
        tmux \
        vim \
        && \
    pip3 install docker-compose
RUN sed -ri '/#PermitRootLogin/a PermitRootLogin yes\n' /etc/ssh/sshd_config && \
    echo 'root:root' | chpasswd
COPY compose-dirs /usr/local/bin/
COPY compose-dirs.conf /etc/
COPY docker-entrypoint /usr/local/bin/docker-entrypoint
EXPOSE 22
ENTRYPOINT ["/usr/local/bin/docker-entrypoint"]
WORKDIR /etc/compose
