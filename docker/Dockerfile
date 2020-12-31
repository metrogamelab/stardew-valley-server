FROM mono:latest

ARG STEAM_USER
ARG STEAM_PASS
ARG SRCDS_APPID

RUN apt-get update && \
    apt-get install -y --no-install-recommends curl lib32gcc1 ca-certificates wget unzip xvfb x11vnc xterm i3

# Install Game via steamcmd
RUN mkdir -p /mnt/server/steamcmd && \
    curl -sSL -o steamcmd.tar.gz https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz && \
    tar -xzvf steamcmd.tar.gz -C /mnt/server/steamcmd && \
    cd /mnt/server/steamcmd && \
    chown -R root:root /mnt && \
    export HOME=/mnt/server  && \
    mkdir -p /mnt/server/Stardew\ Valley/ && \
    ./steamcmd.sh +login ${STEAM_USER} ${STEAM_PASS} +force_install_dir /mnt/server/Stardew\ Valley/ +app_update ${SRCDS_APPID} validate +quit && \
    mkdir -p /mnt/server/.steam/sdk32 && \
    cp -v linux32/steamclient.so ../.steam/sdk32/steamclient.so && \
    mkdir -p /mnt/server/.steam/sdk64 && \
    cp -v linux64/steamclient.so ../.steam/sdk64/steamclient.so && \
    mkdir -p /mnt/server/nexus && \
    wget https://github.com/Pathoschild/SMAPI/releases/download/3.8/SMAPI-3.8.0-installer.zip -qO /mnt/server/nexus.zip && \
    unzip /mnt/server/nexus.zip -d /mnt/server/nexus/ && \
    /bin/bash -c "echo -e \"2\n/mnt/server/Stardew\ Valley\n1\n\" | /usr/bin/mono /mnt/server/nexus/SMAPI\ 3.8.0\ installer/internal/unix-install.exe"

# Add Mods
COPY ./docker/mods/alwayson.zip /mnt/server/alwayson.zip
COPY ./docker/mods/unlimitedplayers.zip /mnt/server/unlimitedplayers.zip
COPY ./docker/mods/autoloadgame.zip /mnt/server/autoloadgame.zip

RUN unzip /mnt/server/alwayson.zip -d /mnt/server/Stardew\ Valley/Mods && \
    unzip /mnt/server/unlimitedplayers.zip -d /mnt/server/Stardew\ Valley/Mods && \
    unzip /mnt/server/autoloadgame.zip -d /mnt/server/Stardew\ Valley/Mods && \
    rm /mnt/server/alwayson.zip /mnt/server/unlimitedplayers.zip /mnt/server/autoloadgame.zip && \
    chmod +x /mnt/server/Stardew\ Valley/StardewValley

COPY ./docker/docker-entrypoint.sh /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]
