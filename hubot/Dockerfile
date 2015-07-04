FROM ubuntu:trusty
MAINTAINER Autocorp <https://github.com/autocorp>

LABEL Description="This image is used to start an installation of Hubot"
LABEL Version="0.1"

ENV DEBIAN_FRONTEND noninteractive
ENV USER root

RUN apt-get update && apt-get install -y curl

# script to install the NodeSource Node.js repo into ubuntu's apt repo
RUN curl -sL https://deb.nodesource.com/setup | sudo bash -

RUN apt-get install -y \
build-essential \ 
libexpat1-dev \
libicu-dev \
nodejs \
openssh-client \
python

RUN npm set prefix /usr && npm install -g coffee-script hubot hubot-hipchat

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

COPY package.json /usr/src/app/
COPY scripts /usr/src/app/scripts

RUN npm install

RUN useradd -m hubot && chown -R hubot:hubot /usr/src/app


#####################################
# everything below here runs as hubot
#####################################

USER hubot
CMD hubot -a hipchat

