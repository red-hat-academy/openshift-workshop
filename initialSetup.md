# Initial Setup
> How to setup the workshop enviornment

This lab is designed to work with Minishift but it will also work with any OpenShift or OKD derivative with little modification.

This is not a guide for setting up Minishift but you can find one [here](https://docs.okd.io/latest/minishift/getting-started/installing.html)

Once you have that installed and started minishift you will be given a url to access the web console through a browser. You can also type `minishift oc-env` to be given a command to add the cli tools to your shell.

You may want to run minishift with more than the default 4GB of RAM.

To do that type add `--memory 8GB` to the end of the `minishift start` command when you are starting the cluster replacing `8GB` with your desired amount of memory.