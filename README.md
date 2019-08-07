# Learning OpenShift with Minecraft
As one of the most well-known video games in the world, [Minecraft](https://www.minecraft.net/) has played an influential role in the educational community exhibiting how gaming can be leveraged as an avenue for learning technology. Minecraft drives player creativity offering the ability to build infinite worlds, and customize the game with mods, and run your own game servers in multiplayer. 

Using the Java Edition of the Minecraft game server, you will learn how to deploy and configure an application in an OpenShift environment. 

By deploying a multi-server network using two world servers and a reverse proxy, through this workshop, you will create a working game server network that ultimately permits connectivity to either of the two worlds.


# Outline
The focus of this workshop is to build core knowledge in containers deployment and understand how developers will use the OpenShift cloud platform. 
OpenShift is an open source, container application platform for the development, deployment and management of container-based apps across physical, virtual, and public cloud infrastructures. OpenShift provides predefined application environments to allow enterprises to manage container deployments and scale applications using Kubernetes to provide support for DevOps principles. 

Essential skills practiced in this workshop include:

* Creating Projects in OKD
* Deploying and Exposing Applications in OKD
* Editing Deployment Configurations in OKD
* Inter-pod Networking


# Software

All software used in this workshop is free, opensource, and well documented. Links will be provided thoughout the workshop as references to the official documentation for each product used.

## OKD
[OKD](https://www.okd.io/) is the upstream community edition of Kubernetes that powers [Red Hat OpenShift](https://www.openshift.com/).

## Minishift
[Minishift](https://www.okd.io/minishift/) is a set of tools for deploying a single node OKD cluster in a virtual machine running on either Windows, Mac, or Linux.

## PaperSpigot
[PaperSpigot](https://papermc.io/) is 3rd party server software for minecraft that adds support for plugins and other server-side mods.

## BungeeCord
[BungeeCord](https://www.spigotmc.org/wiki/bungeecord/) is a reverse proxy for minecraft that allows you to connect to multiple game servers though one connection.

# Hardware Requirements
In order to run this workshop it is recommended to have at least 8GB of RAM, 4 CPU cores and 20GB of free hard drive space. Overhead will be necessary for running the operating system, hypervisor, and other applications on the host computer during the workshop.

The Minishift virtual machine is configured by default with 4GB of RAM, 2 CPU cores and 20GB of hard drive space (this is adjustable as described in “[initial setup](https://github.com/red-hat-academy/openshift-workshop/wiki/initial-setup)”). 
***
>[Continue with Workshop](https://github.com/red-hat-academy/openshift-workshop/wiki/home)
