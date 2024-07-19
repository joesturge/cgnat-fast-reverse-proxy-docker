# cgnat-fast-reverse-proxy-docker

This README details the deployment of a Minecraft Forge server accessible through a Fast Reverse Proxy (FRP) setup, allowing players to connect to a Minecraft server hosted behind CGNAT.

## Overview

This project uses https://github.com/fatedier/frp, and the docker packaging provided by https://github.com/snowdreamtech/frp

## External

The [docker-compose-external.yaml](docker-compose-external.yaml) file can be deployed on a external vm which has a public IP, such as oracle free tier. Make sure to set the FRP_SERVER_TOKEN environment var.

The frps service is dployed using network_mode: host to ensure that FRP clients which connect can have the port opened. Also make sure to allow port 7000 tcp on the VM so that FRP clients can connect to the server.

## Internal

The [docker-compose-internal.yaml](docker-compose-internal.yaml) can be deployed on your home server which is behind a CGNAT. This example shows how to deploy a minecraft server, but it can also work with UDP, HTTP and HTTPS services.

In this example, the FRP client is configured to connect to the FRP server running on the external vm. A tunnel is created when the client connects which routes traffic to the external vm port 25565 to the minecraft server port 25565.