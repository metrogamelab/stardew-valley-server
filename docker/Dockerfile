# ----------------------------------
# Pterodactyl steamcmd Dockerfile
# Environment: Mono
# Minimum Panel Version: 1.0.0
# ----------------------------------
FROM mono:latest

ENV  USER=container HOME=/home/container

COPY ./docker/docker-entrypoint.sh /docker-entrypoint.sh

RUN apt-get update && \
    apt-get install -y --no-install-recommends curl lib32gcc1 ca-certificates wget unzip xvfb x11vnc xterm i3 && \
    adduser --disabled-password --home /home/container container && \
    chown -R ${USER}:${USER} ${HOME}

USER container
WORKDIR ${HOME}

# Install steamcmd
RUN mkdir -p ${HOME}/steamcmd && \
    curl -sSL -o steamcmd.tar.gz https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz && \
    tar -xzvf steamcmd.tar.gz -C ${HOME}/steamcmd && \
    chown -R ${USER}:${USER} ${HOME}

ENTRYPOINT ["/docker-entrypoint.sh"]
