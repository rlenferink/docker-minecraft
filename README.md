## docker-minecraft

[![Docker Pull](https://img.shields.io/docker/pulls/rlenferink/minecraft.svg)](https://hub.docker.com/r/rlenferink/minecraft/)

A nice and easy way to get a Minecraft server up and running using docker. For
help on getting started with docker see the [official getting started guide][0].
For more information on Minecraft and check out it's [website][1].

### Quickstart

To quickly get your container up and running execute on of the following commands

To run minecraft without volume mount, run:

    docker run -d --name=mc -p 25565:25565 rlenferink/minecraft /start

To run minecraft with volume mount, run:

    docker run -d --name=mc -p 25565:25565 -v /mnt/minecraft:/data rlenferink/minecraft /start

Running minecraft with volume mount is to save your world data.

### Running docker-minecraft

Running the first time will set your port to a static port of your choice so
that you can easily map a proxy to. If this is the only thing running on your
system you can map the port to 25565 and no proxy is needed. i.e.
`-p 25565:25565` . If you want to enable the query protocol you need
to add another -p 25565:25565/udp to forward the UDP protocol on the
same port as well.
Also be sure your mounted directory on your host machine is
already created before running `mkdir -p /mnt/minecraft`.

    docker run -d --name=mc -p 25565:25565 -v /mnt/minecraft:/data rlenferink/minecraft /start

From now on when you start/stop docker-minecraft you should use the container id
with the following commands. To get your container id, after you initial run
type `sudo docker ps` and it will show up on the left side followed by the
image name which is `rlenferink/minecraft:latest`.

    docker start <container_id>
    docker stop <container_id>


### Building docker-minecraft

Running this will build you a docker image with the latest version of both
docker-minecraft and Minecraft itself.

    git clone https://github.com/rlenferink/docker-minecraft
    cd docker-minecraft
    docker build -t rlenferink/minecraft .


#### Notes on the run command

 + `-d` allows this to run cleanly as a daemon, remove for debugging
 + `-p` is the port it connects to, `-p host_port:docker_port`
 + `-v` is the volume you are mounting `-v host_dir:docker_dir`
 + `rlenferink/minecraft` is how this docker image is called

[0]: http://www.docker.io/gettingstarted/
[1]: http://minecraft.net/
