# Learning OpenShift with Minecraft
It has been said that games are a new avenue to learning technology [(Command Line Heros Podcast S3E2)](https://www.redhat.com/en/command-line-heroes/season-3/learning-the-basics). In this workshop you will learn how to deploy and configure an application in OpenShift.

Minecraft is a sandbox adventure game that has become one of the most well known video games in the world. One of the things that makes this game unique besides it's infinite worlds and 3rd party modding support is the ability for you to run your own game servers in multiplayer.

This workshop goes through how to deploy a multi-server network, supporting the java edition of the game, using two world servers and a reverse proxy allowing users to connect to either one of the worlds.

# Outline
The following will be covered in this workshop

* Creating Projects in OKD
* Deploying and Exposing Applications in OKD
* Editing Deployment Configurations in OKD
* Inter-pod Networking

The workshop itself will be separated into several steps. Be sure to complete the initial setup before moving to step one. There is a section called background provided that will teach you about many of the underlying architectures and technologies.

After you are done you should have a working game server network that you can connect to.

# Software

All software used in this workshop is free, opensource, and well documented. Links will be provided thoughout the workshop as references to the official documentation for each product used.

## OKD
[OKD](https://www.okd.io/) is the origin community edition of Kubernetes that powers [Red Hat OpenShift](https://www.openshift.com/). It's basically "OpenShift" but free. At it's core it is a hybrid cloud solution.

## MInishift
[Minishift](https://www.okd.io/minishift/) is a set of tools for deploying a single node OKD cluster in a virtual machine running on either Windows, Mac, or Linux.

## PaperSpigot
[PaperSpigot](https://papermc.io/) is 3rd party server software for minecraft that adds support for plugins and other server-side mods.

## BungeeCord
[BungeeCord](https://www.spigotmc.org/wiki/bungeecord/) is a reverse proxy for minecraft that allows you to connect to multiple game servers though one connection.

# Hardware Requirements
By default the Minishift VM is allocated 4GB of ram 2 CPU cores and 20GB of hard drive space. You will want to have more than this however in order to leave room for other processes running on your computer.
***
>[Continue with Workshop](https://github.com/kloct/openshift-workshop/wiki/home)