# Cjdns docker container with Debian base.
`Complexity is the enemy of security.`  This containers aim will be to attempt to reduce/eliminate any impact that this appliance will have on its host, while also reducing the initial learning curve required to get started.  You also have the added benefit of having `a no cost learning experience` meaning this will not break your host machine in the process of you learning how to use it.

This container will also not only help you learn how to get going, it will also aim to be capable of being run in container services such as Amazon's EC2 Container service.  Its not intended necessarily to be run at home but to actually be run as a point of presence in a public datacenter which can give you a dedicated external access point to Hyperboria or any other meshnets.

## Disclaimer
This readme may drift from the readme associated with the repository used in this installation so if it seems to be broken at all.  Please feel free to try checking out the [main repository](https://registry.hub.docker.com/u/chamunks/debian-cjdns/) for the latest documentation.  I also encourage [bug reports and feature requests](https://github.com/chamunks/debian-cjdns/issues) they help improve the quality of open source projects like these.

## Installation and Operation
Generate yourself some configs

    docker run -ti --volume $(pwd)/cjdns:/etc/cjdns --name debian-cjdns chamunks/debian-cjdns
This will create cjdns config files in a directory named cjdns nested inside of your current working directory.

You can then modify these config files to your liking. This includes modifying the port you wish to bind cjdns to inside of your container.

Once you've done this you'll want to remove the old container and start a new one with docker run again.

    docker run -d -P hostPort:containerPort --name debian-cjdns chamunks/debian-cjdns

## The Old Method
this method was inspired by [this repository](https://registry.hub.docker.com/u/mildred/cjdns/) this method is the only tested method but the other one should also work.

    Installation is simple. On first run, cjdns will generate your IP
    address. The cjdns configuration lies in `/etc/cjdns` (which is a
    docker volume).

    To be useful you'll have to run this in privileged mode, with the
    same network stack as the host. This can be accomplished using the
    docker options `--privileged --net=host`.

        docker pull mildred/cjdns
        docker run --privileged --net=host mildred/cjdns --volume /etc/cjdns:/etc/cjdns

## Links
[Docker Hub Image](https://registry.hub.docker.com/u/chamunks/debian-cjdns/)
[GitHub Repository](https://github.com/chamunks/debian-cjdns)

## Health & Statistics
#### Repository Health
[![GitHub issues](https://img.shields.io/github/issues/chamunks/debian-cjdns.svg?style=flat-square)](https://github.com/chamunks/debian-cjdns) out of [![GitHub total issues](https://img.shields.io/github/issues-raw/chamunks/debian-cjdns.svg?style=flat-square)](https://github.com/chamunks/debian-cjdns)

#### Container Build Health
[![Docker Pulls](https://img.shields.io/docker/pulls/chamunks/debian-cjdns.svg?style=flat-square)](https://registry.hub.docker.com/u/chamunks/debian-cjdns/)
[![Docker Stars](https://img.shields.io/docker/stars/chamunks/debian-cjdns.svg?style=flat-square)](https://registry.hub.docker.com/u/chamunks/debian-cjdns/)
[![Docker Build Status](http://hubstatus.container42.com/chamunks/debian-cjdns)](https://registry.hub.docker.com/u/chamunks/debian-cjdns)

#### Repository Statistics/Info
[![GitHub license](https://img.shields.io/github/license/chamunks/debian-cjdns.svg?style=flat-square)](https://github.com/chamunks/debian-cjdns)

[![GitHub forks](https://img.shields.io/github/forks/chamunks/debian-cjdns.svg?style=flat-square)](https://github.com/chamunks/debian-cjdns)
[![GitHub stars](https://img.shields.io/github/stars/chamunks/debian-cjdns.svg?style=flat-square)](https://github.com/chamunks/debian-cjdns)
