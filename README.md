[![Stories in Ready](https://badge.waffle.io/autocorp/autobot.svg?label=ready&title=Ready)](http://waffle.io/autocorp/autobot)

# Autobot

Autobot provides an easy software delivery mechanism for maintaining your very own Hubot installation.

The key techologies Autobot wraps up are: hubot, ansible, docker and drone.

The stack looks like this:
- Git (for this repository)
- Ansible (to control Docker)
- Docker, Docker-Machine, Docker-Compose (to maintain the containers)
- Virtual Machine & AWS (for compute power)

## Ansible

Ansible is responsible for the following (via site.yaml):

- on localhost: Checking for a docker container called 'autobot'. If it doesn't exist, make a new one.
- on autobot: Add ubuntu to the docker group, and create a self-signed cert for drone.
- on localhost: Executing docker-compose build. Passing ENV vars. Running docker-compose up.

and for storing private data in `group_vars/all`.

# Docker

The `Dockerfile` holds the configuration for spining up an instance of Hubot. 

## Docker Compose

`docker-compose.yaml` configures the following containers:
- hubot
- redis (data persistance layer)
- drone (continuous delivery)

## Drone

`drone.yaml` takes an ubuntu image and installs docker-compose on it. A deployment script builds hubot with the latest code. Notifications are sent to a hipchat room.

# Hosts Wrapper

`hosts` is a python script to create a dynamic inventory from docker-machine
