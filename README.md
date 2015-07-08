[![Stories in Ready](https://badge.waffle.io/autocorp/autobot.svg?label=ready&title=Ready)](http://waffle.io/autocorp/autobot)

# autobot

The autobot project provides an easy delivery mechanism for maintaining your very own Hubot installation.

# Getting Started
```
# Get yourself a copy of the repo
git clone git@github.com:autocorp/autobot.git

# Run Jeeves, who will guide you through autobot setup and usage
cd autobot; ./bin/jeeves
```

## The Stack

The key techologies the make up Autobot are: hubot, ansible, docker and drone.

The stack looks like this:

- Ansible (to configure the hosts)
- Docker, Docker-Machine, Docker-Compose (to maintain the containers)
- Virtual Machine & AWS (for compute power)
- Hubot with a Redis data store, deployed via drone

## This Repo

### bin/

The bin directory contains scripts used by the project (though not strictly binary files).

- jeeves

`jeeves` is a python script to help setup and manage autobot

### /

- Dockerfile
- package.json
- docker-compose.yaml
- site.yaml
- hosts

The `Dockerfile` holds the configuration for spining up an instance of Hubot and loading scripts from the `hubot-scripts` directory. 

`package.json` is a supporting file, which gets fed in by `Dockerfile`.


`docker-compose.yaml` configures the following containers:

- hubot
- redis (data persistance layer)
- drone (continuous delivery)

Ansible uses `site.yaml` to do the following:

- on localhost: Checking for a docker container called 'autobot'. If it doesn't exist, make a new one.
- on autobot: Add ubuntu to the docker group, and create a self-signed cert for drone.
- on localhost: Executing docker-compose build. Passing ENV vars. Running docker-compose up.

and for storing private data in `group_vars/all`.

### hubot-scripts/

Any scripts in this directory are loaded by the hubot Dockerfile.

- example.coffee (robot.hear /badger/i)

`hosts` is a python script to create a dynamic inventory from docker-machine

### continuous-delivery/

- .drone.yaml

`.drone.yaml` is the configuration file for drone (a continuous delivery pipeline). It takes an ubuntu image and installs docker-compose on it. A deployment script builds hubot with the latest code. Notifications are sent to a hipchat room.

### docs/

project documentation
