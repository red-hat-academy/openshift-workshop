# Introduction
> Objective: Create a minecraft server app

One or more containers in an OpenShift cluster are configured in what is called a pod. Pods are distributed across cluster nodes which contain the resourses and services required to run the containers.

We're going to be using a publicly avalible image from the Docker Hub to deploy our minecraft server on openshift.

This guide will cover 2 ways to create new apps in OpenShift. The first is though the web console and the second is in the oc cli.

## Creating a project in the web console
Before doing anything you need to create a project for all of your apps to run in.

* Navigate to the web console.
* One the home page click create new project.
* Name the project `minecraft-server`
* You can also add a Display name and Description if you would like.

![create project screenshot](./Screenshots/createProject.png)

Now your ready to create your app.

## Creating an app in the Web Console
* Click the project you just created to enter it
* Now click the Add to Project Dropdown on the top right and then Deploy Image

![add to project](./Screenshots/addToProject.png)

