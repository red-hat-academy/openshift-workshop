# Introduction
> Objective: Make data persistent in OpenShift.

So now we have the game server running and available so we are able to connect to it. Only problem is now that our configuration, and world isn't saved when a new deployment of the pod is made.

This may seem strange but that is because the containers used in the cluster are ephemeral by nature; meaning that any data they hold is temporary. This is perfect for services that are **stateless**, or don't need to store data, like web servers, but not so good for **stateful** services like databases.

# Persistent Volumes
So a our Minecraft server is stateful. How do we save the data?
Well in the containerized world there are a few ways to do this but the way we are going to use is persistent volumes.

A 
**volume** is just a place to store data. When you tell a container to use a volume you are mounting that volume to the container.

In the OpenShift web console navigate to: *Application -> Deployments -> hub -> Configuration*

Here you will find an overview of the deployment configuration for the hub pod. A **deployment configuration** (dc) contains instructions that tell the cluster how to rollout a pod. Under Volumes you can see the volumes available to the pod. Notice that the type field it says empty dir. This means that OpenShift has no where to save the data during a new deployment so the data will be lost.

What we will be doing is creating a volume that is persistent and adding it to the deployment config.

Take note of the volume name that mounts to the directory `/data` in the pod.
***
## Creating Persistent Volumes
There are a ton of ways you can setup the storage for a volume. You could use NFS, or GlusterFS, even something like Amazon's Elastic Block Storage (AWS EBS). In this exercise we will be simply be creating a volume backend directory on the local Minishift virtual machine.

### Creating the directory:
The first thing you will need to do is create a folder on the minishift virtual machine.
First connect to the vm by typing `minishift ssh` into the terminal.
Next type `sudo -i` to gain super user privileges

You will now create the folder for the volume to mount to

Create a new directory called hub inside a directory called minecraft.

`mkdir -p /mnt/sda1/var/lib/minishift/openshift.local.volumes/pv/minecraft/hub`

Then set it's permission to rwx for user group and other.

`chmod 777 -R /mnt/sda1/var/lib/minishift/openshift.local.volumes/pv/minecraft`

Now that the directory is accessible you there is one more thing you have to do. SELinux, by default doesn't allow container volumes to access storage on their host machine. So you have to change the context of the folder to allow it. 

`chcon -Rt svirt_sandbox_file_t /mnt/sda1/var/lib/minishift/openshift.local.volumes/pv/minecraft`
***
### Persistent Volume:
Next you have to mount a **PersistentVolume** to the directory you just created making is accessible by openoshift.

* Exit minishift ssh back to your machine.
* Login to the cluster with `oc login -u system:admin` 
  * If the oc command isn't recongnized type `eval $(minishift oc-env)` to add it to your `$PATH`

* Once logged in switch to the minecraft-server project.

* Create and edit a new file called `hubpv.yml`.
  * Here you will define the persistent volume.
  * This definition will mount the folder you just created as persistent volume called *hub*.
  * Add the folowing to mount the folder you created as a persistent volume:
```
apiVersion: v1
kind: PersistentVolume
metadata:
 name: hub
spec:
 capacity:
  storage: 5Gi
 accessModes:
  - ReadWriteOnce
hostPath:
 path: /mnt/sada1/var/lib/minishfit/openshift.local.volumes/pv/registry
```

* Now add this definition for the persistent volume to the minecraft-server project

    `oc create -f hubpv.yml`

***
### Persistent Volume Claim:
Now there is a volume resource sitting out there in the minecraft-project ether. 

To use this volume you first have to claim it. Using a **PersistentVolumeClaim**(pvc) you can request the PersistentVolume resource. Then use it to claim as a volume in a pod making OpenShift take the volume backing the claim, mounting it to the pod.

* First you'll need to create another new file called `hubpvc.yml`
* Edit this file and enter the following:
```
kind: PersistentVolume
apiVersion: v1
metadata:
 name: hubclaim
spec:
 accessModes:
   - ReadWriteOnce
 resources:
  requests:
   storage: 5Gi
selector:
 name: hub
```
* Save and quit that file then create a new persistent claim using this definition:

`oc create -f hubpvc.yml`

***
### Patching the Deployment Config
Now that you've made the pvc you have to add it to the hub pod's deployment config.

`oc get volume dc/hub --add --name=hub-storage -t pvc --claim-name=hubclaim --overwrite`

Be sure to replace `hub-storage` with the volume you noted earlier from the deployment config that mounts to `/data` in the pod.

The above command modifies the current deployment config of hub (`--overwrite`).

It makes the volume called hub-storage(`--name=hub-storage`) use the persistent volume claim(`-t pvc`) called hubclaim(`--claim-name=hubclaim`).

# Conclusion
After entering in the command from the last step you should see the pod start a new deployment.

Connect to the terminal of the hub

*Application -\> pods -\> hub-\*\*\*-\*\*\* -\> Terminal*

* Add a player to the ops list (if you have a minecraft java account make this your account)

    `op player`

* Now type `ops` to see the changes.

* Navigate to hub's deployment *Application -> Deployment -> hub*
* Now click `Deploy` to start a new deployment
* Wait for the deployment to finish and then go back to the terminal and type `ops`
* You should see that the ops list now didn't change

It took a few steps but now you have made the /data directory in this pod persistent!

To go over the steps in brief again you:

1) Added a local volume backend directory
2) Created a PersistentVolume
3) Created a PersistentVolumeClaim
4) Added the PersistentVolumeClaim to the deployment config of the hub pod