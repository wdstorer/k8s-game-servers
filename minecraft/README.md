# Minecraft Server

This configuration file creates a Kubernetes Deployment and NodePort Service for running Minecraft. It's assumed that the Minecraft server files are available to mount on the host Node at `/srv/k8s_nfs/minecraft-server`. Customize accordingly.

## Kubernetes Resources
* Deployment: Create a 1 replica deployment that mounts the server files in a container pod
* NodePort Service: Exposes the game server by mapping the container port `25565` to an available NodePort on the cluster

## Setting up the Minecraft server directory
Follow the instructions here: https://paper.readthedocs.io/en/latest/server/getting-started.html
1. Run the server once to accept the EULA and configure an initial `server.properties` file
2. Update `k8s-minecraft-server.yaml` to reflect the name of the PaperMC jar file:
  ```
  args: ["-Xms2G", "-Xmx2G", "-jar", "paper-1.18.1-164.jar"] <-- update this
  ```
