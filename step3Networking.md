# Configure Bungee
Bungee is a Minecraft server proxy that can let users connect to a multi server network though one connection.

## Configuring Bungee
The First things you need to do to configure Bungee is switch both of the game server to online mode.

This can be easily accomplished with enviornment varriables.

Add the following enviornment varriable and value to smp and hub.

```
ONLINE_MODE=FALSE
```

## Networking

In Openshift everytime a new pod is created it gets a new ip address. When configureing interpod communication you should use the domain name instead. For out services the internal domain names are:
App|Domain Name
---|---
bungee | bungee.minecraft-server.svc.cluster.local
hub | hub.minecraft-server.svc.cluster.local
smp | smp.minecraft-server.svc.cluster.local

Using these we give the bungee proxy server targets

* Go to a terminal and type `minishift ssh`
* Navigate to the local bungee volume directory

  `cd /mnt/sda1/var/lib/minishift/openshift.local.volumes/pv/minecraft-server/bungee`

* Now edit the config.yml file

* Change this

```
servers:
  lobby:
    motd: '&1Just another BungeeCord - Forced Host'
    address: localhost:25565
    restricted: false
```
* To this
```
servers:
  hub:
    motd: 'Welcome to the Hub Server!'
    address: hub.minecraft-server.svc.cluster.local:25565
    restricted: false
  smp:
    motd: 'Welcome to the SMP Server!'
    address: smp.minecraft-server.svc.cluster.local:25565
    restricted: false
```

# Expose the Bungee App
Now that you have comfigured bungee it is time to expose the service so that you can connect to it.

* Go to *Applications -> Routes*
* Click `Create Route`
* Name The Route `Bungee` and ensure that `bungee` is selected as the service

Since our service is not HTTP based we need to create a NodePort Service to expose it so that we can connect.

The way we do this is by exposing it as the type `LoadBalancer`

`oc expose dc bungee --type=LoadBalancer --name=bungee-ingress`

Now see what port the server is exposed on.

`oc get svc/bungee-ingress` the second port is the one you need to connect

Now you should be able to connect to the server