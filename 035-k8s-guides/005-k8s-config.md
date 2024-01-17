---
weight: 5
url: /docs/k8s-guides/configs
Order: 1
Title: Managing Multiple Config Files
description: >
  How to easily manage and switch between multiple Kubernetes
  environments.
---

## Introduction

If you frequently switch between multiple Kuberentes clusters from
different cloud providers, it can be tedious to manage your Kubernetes
configuration.

In this document we offer some helpful hints for configuring and switching
between multiple Kubernetes clusters.

## Where Configurations are Stored

### Main Config File

By default, Kubernetes creates a configuration file stored at ```~/.kube/config```.

This file is referenced by an environment variable named KUBECONFIG.

The kubeconfig file can contain contexts for multiple Kubernetes clusters. It
is often the case when using the command line tools provided by cloud vendors
(for example, ```aws``` from Amazon, ```az``` from Microsoft Azure, and ```gcloud``` from Google)
that the kubeconfig file will be automatically updated and new configuration from
newly created contexts can be merged into it by the CLI.

It is convenient when multiple configurations are stored in a single file, because
it means you don't have to update your KUBECONFIG environment variable to connect
to a new cluster.

### Alternate Config Files

Unfortunately, not every cloud vendor provides a command line tool that can retrieve
the configuration and merge it into the ```~/.kube/config file```.

Another common method that cloud vendors give to retrieve the cluster configuration is to
download it from their web portal. In this case, you need to store the configuration
as a separate file. It helps to keep all of these alternate configuration files
together in a single folder.

We suggest creating a folder at ```~/.kube/configs``` and placing kubeconfig files there.
You then need to update your KUBECONFIG environment variable to reference every file
that is in ```~/.kube/configs```.

## Keeping KUBECONFIG Updated

Here is a script you can run that will refresh your KUBECONFIG environment variable to
reference all the files contained within ```~/.kube/configs```.

```bash
#!/usr/bin/env bash
# If there's already a kubeconfig file in ~/.kube/config it will import that too and all the contexts
DEFAULT_KUBECONFIG_FILE="$HOME/.kube/config"
if test -f "${DEFAULT_KUBECONFIG_FILE}"
then
  export KUBECONFIG="$DEFAULT_KUBECONFIG_FILE"
fi
# Your additional kubeconfig files should be inside ~/.kube/configs
ADD_KUBECONFIG_FILES="$HOME/.kube/configs"
mkdir -p "${ADD_KUBECONFIG_FILES}"OIFS="$IFS"
IFS=$'\n'
for kubeconfigFile in `find "${ADD_KUBECONFIG_FILES}" -type f -name "*.yml" -o -name "*.yaml"`
do
    export KUBECONFIG="$kubeconfigFile:$KUBECONFIG"
done
IFS="$OIFS"
```

Create a file ending in the ```.sh``` extension and place the file in a folder in your PATH.

After that, whenever you add a new file to your ```~/.kube/configs``` folder, you can run
this script to refresh your KUBECONFIG environment variable.

## Setting KUBECONFIG at Shell Startup

If you're using Bash (the default terminal shell for most Linux, Mac, and Windows Subsystem for Linux
installations), set your KUBECONFIG file by running the script in your ```.bashrc``` or
```.bash_profile``` files.

For example, if you named your script ```load-k8s-configs.sh``` and placed it in your
```~/scripts``` folder, you can call it from your shell loading script with the line:

```bash
source ~/scripts/load-k8s-configs.sh
```

## Aliasing kubectl

In many of our videos, you may see us shorten the typing of ```kubectl``` and instead
simply type ```k```. To create a similar alias for yourself, add an alias command to your
```.bashrc``` or ```.bash_profile``` file.

```bash
alias k='kubectl'
```

## Using krew to Manage kubectl Plugins

There are many ```kubectl``` plugins available that can extend the command line functionality
and make it easier to perform tasks. Plugins are managed using ```krew``` which itself is a
```kubectl``` plugin.

To install ```krew```, follow the instructions [here](https://krew.sigs.k8s.io/docs/user-guide/setup/install/).

Once you've installed ```krew```, you can add a plugin with the command:

```bash
kubectl krew install plugin-name-here
```

For a list of plugins, [click here](https://krew.sigs.k8s.io/plugins/).

## Switching Contexts Using the ctx Plugin

The ```ctx``` plugin can speed up the way you switch Kubernetes contexts.
See [here](https://github.com/ahmetb/kubectx) for more information.

To install ```ctx``` do:

```bash
kubectl krew install ctx
```

Similarly, the ```ns``` plugin makes it faster to switch namespaces. To install
```ns``` do:

```bash
kubectl krew install ns
```

To get a list of current contexts with ```ctx``` do:

```bash
kubectl ctx
```

To switch to a different context, do:

```bash
kubectl ctx context-name-here
```