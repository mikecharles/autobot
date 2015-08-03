In a hurry? Try `./bin/jeeves --check software` or skip ahead to [getting started](#getting-started).

# Why do we exist?

We want to help you maintain your very own [Hubot](https://hubot.github.com/) installation, and develop your own Hubot scripts. Here is how we help:

**In Dev**
- Create a local dev environment (Hubot installed and configured for you)
- Easily test your own Hubot scripts in the dev environment
- Maintain your own private Hubot scripts

**In Prod**
- Publish your own Hubot scripts for easy consumption
- Manage a remote Hubot environment on your own server (e.g one you own in AWS)
- Make sure your Hubot environments are always up to date with your latest scripts  

## Why do I need autbot?
autobot is designed to be personalised. He doesn't come with a set of pre-defined scripts. He's there to help you manage all the back of house tasks, so you can focus on creating Hubot scripts for your very own robot.

Let's pretend your organisation is `ACME`. We hope you use autobot to create you very own robot called `ACMEbot`. He'll be populated with scripts that you've created and he'll do all the things you want him to do.

# Getting Help

The autobot project is managed through GitHub issues, and our waffle board makes it easy to see what we're working on, and any outstanding issues [![Stories in Ready](https://badge.waffle.io/autocorp/autobot.svg?label=ready&title=Ready)](http://waffle.io/autocorp/autobot)

You can also get more information by visiting our [wiki](https://github.com/autocorp/autobot/wiki).

![alt text](autobot-logo.png "autobot")

# Getting Started

We've created jeeves so he can do all the heavy lifting for you. He'll make sure you have the required software, and help you with the day to day development too.

Jeeves can check lots of things for you, but we only need to worry about software dependencies right now. Make sure you're all green for the the required software and you can move on to creating your very own local development environment.

```
# Donwload a copy of autobot
git clone git@github.com:autocorp/autobot.git; cd autobot;

# Let Jeeves check your system for the required software
./bin/jeeves --check software

# Ask Jeeves how to create a local dev environment (for testing Hubot scripts)
./bin/jeeves --run local

```

He's still learning so make sure to raise an [issue](https://github.com/autocorp/autobot/issues) if you think he could help you out a little better.


## A closer look at the development environment

You can go ahead and run the commands Jeeves gave you when you did a `jeeves -r local`, but for those that are curious we're going to breakdown what's going on here.

1. `docker-machine create -d virtualbox dev` will instruct docker-machine to create a Virtual Machine called `dev`. This will be used to house your Hubot container for local development of Hubot scripts.

2. You'll then run `eval "$(docker-machine env dev)"` to make sure all your `docker-*` commands are targeted to your dev container.

3. Finally, the `docker-compose build hubot && docker run -it --rm autobot_hubot:latest hubot` command will spin up a new Hubot container in your local `dev` Virtual Machine.

All the scripts from the `hubot-scripts` folder will be loaded for you (so you can place scripts in there while you're doing local development).

At this stage you should be at the `Hubot>` prompt, and the `badgers` demo script should be loaded for you. Try talking to Hubot, like this `Hubot> @hubot how do you feel about badgers`.

Hubot should respond with:
```
Hubot> @hubot how do you feel about badgers
Badgers? BADGERS? WE DON'T NEED NO STINKIN BADGERS
```

## Life after dev
Now that you've got a local development environment, you'll want to write your own scripts. You can read up on [Hubot Scripting](https://github.com/github/hubot/blob/master/docs/scripting.md) to get started and drop you very own Hubot script into `./hubot-scripts` when you're ready to test them out.

Other tasks will make use of more bits of technology and connections, like `Redis`, `Confluence` and `Hipchat`. We'll get stuck into those in another example.