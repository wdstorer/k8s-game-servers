# Terraria Server

This configuration file creates a Kubernetes Deployment and NodePort Service for running Terraria. It's assumed that the Terraria server files are available to mount on the host Node at `/srv/k8s_nfs/terraria-server`. Customize accordingly.

## Kubernetes Resources
* Deployment: Create a 1 replica deployment that mounts the server files in a container pod
* NodePort Service: Exposes the game server by mapping the container port `7777` to an available NodePort on the cluster

## Setting up the Terraria server directory
Follow the instructions here: https://terraria.fandom.com/wiki/Server
1. Run the server once to configure the default world settings
2. Copy the new `Worlds` directory from the default location at `~/.local/share/Terraria/Worlds` to the server directory
3. Refer to the [instructions](https://terraria.fandom.com/wiki/Server#Server_config_file) for creating a config file named `terraria-server.config` and setting the new world to autostart as default

Example `terraria-server.config`
```
worldpath=./Worlds/
motd=Hello Friends!
world=./Worlds/my_new_world.wld
password=example_password_here
```

## Notes
* The Terraria server binary requires TTY to be enabled or it will fail with a Null Exception error so tty is set to true in the container spec.
