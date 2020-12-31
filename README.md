# Stardew Valley Server

This repository is for Pterdactyl docker container to run a Stardew Valley Server based on the printfuck's [Stardew multiplayer docker compose container](https://github.com/printfuck/stardew-multiplayer-docker) and parkervcp's [Starbound Pterodactyl Egg](https://github.com/parkervcp/eggs/tree/master/steamcmd_servers/starbound) for templating out how to get steamcmd to install the game.

## Setup

### Docker-Compose
Clone our repository:
```
git clone https://github.com/metrogamelab/stardew-valley-server
cd stardew-valley-server
```
Next using the provided `env.example` file, create a hidden `.env` file locally containing your Steam credentials and desired VNC password. 

Finally you can start the server using:
```
docker-compose up -d
```
To stop the server issue the command:
```
docker-compose down
```

## Game Setup

Intially you have to create or load a game once at first startup via VNC. After that the Autoload Mod jumps into the previously loaded savegame everytime you rerun the container. You can also edit the config file of the Autoload Mod to archieve similar behaviour.

### Server Ports
Stardew Valley for the PCrequires a single port to be oepened

game ports (default 24642)

| Port    | default |
|---------|---------|
| Game    |  24642  |

### VNC

Use a vnc client like `TightVNC` on Windows or plain `vncviewer` on any Linux distribution to connect to the server. 

## How it works

The game is downloaded using `steamcmd` so this only works currently with steam versions of the game. The Docker file fetches the latest modloader (SMAPI). The latest working versions of the mods are included in this repo. Feel free to grab newer versions from the links below. The `docker-entrypoint.sh` script will start `Xvfb` and `x11vnc` before starting the game. You can control the game via vnc with the settings within the `docker-compose.yml` file.

## Used Mods

* [AutoLoadGame](https://www.nexusmods.com/stardewvalley/mods/2509)
* [Always On](https://community.playstarbound.com/threads/updating-mods-for-stardew-valley-1-4.156000/page-20#post-3353880)
* [Unlimited Players](https://www.nexusmods.com/stardewvalley/mods/2213)

## TODO:

- disable VNC via Petrodactyl for security purposes
- provide initial game saves so server can boot after install


## Troubleshooting

### Error Messages in Console

Usually you should be able to ignore any message there. If the game doesn't start or any errors appear, you should look for messages like "cannot open display", which would most likely indicate permission errors.

### VNC

Access the game via VNC to initially load or start a pregenerated savegame. You can control the Server from there or edit the config.json files in the configs folder.

### Performance

Suggeted server configurations is 1GB Ram and 1 logical CPU for every 2 players.
