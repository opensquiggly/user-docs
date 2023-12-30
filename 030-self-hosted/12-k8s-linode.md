---
weight: 120
url: /docs/self-hosted/k8s/linode
order: 12
title: "Kubernetes : Linode"
description: How to install OpenSquiggly on Linode Kubernetes Engine (LKE).
---
## Overview of Installing on LKE

Linode Kubernetes Engine, or LKE for short, is Linodes's managed Kubernetes service.
If you don't already have access to a Kubernetes environment, Linode can be a good choice
because of its easy configuration and simplified pricing model compared to larger cloud
providers.

This section will walk you through install OpenSquiggly on LKE.

<hr>

## Part 1 : Creating a Kubernetes Cluster on Linode

To create a Linode cluster, visit:

```bash
linode.com
```

then:

1. In the sidebar menu, select Kubernetes
2. In the upper right corner, click "Create Cluster"
3. Enter the Cluster Label
4. Select a Region
5. Select a Kubernetes Version
6. In the Add Node Pools section, select and add nodes of desired sizes. If you are just
   experimenting with OpenSquiggly on Kubernetes, we recommend selecting the Dedicated CPU / 4GB
   option.
7. For production workloads, Linode recommends choosing the High Availability Control Plane
   option. As of this writing, the HA Control Plane adds $60 per month to the pricing.
8. When you've selected all options, click Create Cluster to checkout and start provisioning
   the cluster.
9. After the cluster is provisioned, click on the cluster in your list of Kubernetes cluster,
   and download the kubeconfig.yaml file. You'll need this yaml file for the next section where
   you connect kubectl to the newly created cluster.

### Video of Creating LKE Cluster
<iframe width="1024" height="878" src="https://www.loom.com/embed/f7705295fbbb47cf8225ce18d7c4eaae" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

<hr>

## Part 2 : Connecting kubectl to the Linode Cluster

To access the cluster from the kubectl command on your desktop OS, do the following:

1. Download the kubeconfig.yaml file as discussed in the previous steps and the previous
   video.
2. Make a directory in your local ~/.kube folder named configs
   ```bash
   cd ~/.kube
   mkdir configs
   ```
3. Copy the kubeconfig.yaml file from your ~/Downloads folder into the ~/.kube/configs folder.
   ```bash
   mv ~/Downloads/<your-cluster-name>-kubeconfig.yaml ~/.kube/configs
   ```
4. Add an environment variable to your .bashrc or .bash_profile file (or equivalent actions on
   Windows or MacOS).
   ```bash
   export KUBECONFIG=$HOME/.kube/config:$HOME/.kube/configs/<your-cluster-name>-kubeconfig.yaml
   ```
5. Restart your terminal or update your current terminal session with:
   ```bash
   source ~/.bashrc
   ```
   
### Video of kubectl Setup
<iframe width="1024" height="754" src="https://www.loom.com/embed/20c9f698f80d4a019082965623d76994" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

<hr>

## Part 3 : Setting up Helm

View your current helm repos with:

```bash
helm repo list
```

Add the OpenSquiggly Helm charts repository to your local Helm repository list with the
command:

```bash
helm repo add opensquiggly https://opensquiggly.github.io/helm-charts
```

<hr>

## Part 4 : Create a Kubernetes Namespace (Optional)

It's a good idea to create a namespace to contain your OpenSquiggly resources that will
be installed by the Helm charts. This keeps your resources isolated from any other resources
you have installed on Kubernetes, avoids any naming conflicts, and makes it easier to
manage the resources later.

Create a namespace with the command:

```bash
kubectl create namespace your-namespace-here
```

Make the namespace your current namespace with the command:

```bash
kubectl config set-context --current --namespace=your-namespace-here
```

If this is a newly created namespace, issue the command:

```bash
kubectl get all
```

and verify that the namespace contains no existing resources.

<hr>

## Part 5 : Install OpenSquiggly using Helm

You should now be all set to install OpenSquiggly on LKE using the helm command line
tool.

### With Default Parameters

For a default install using all default variables, issue the command:

```bash
helm install your-helm-relelase-name-here opensquiggly/allinone --set cloudType=linode
```

Helm release names can contain alphanumeric characters and the hyphen.

Example:

```bash
helm install opensquiggly-test1 opensquiggly/allinone --set cloudType=linode
```

This will create a persistent volume of 32GB in size, using the block storage provisioner
linodebs.csi.linode.com that comes supply by Linode.

### With Custom Disk Size

If you need more or less disk space, you can change the size using the diskSize parameter
and setting it to an integer value in gigabytes.

For example, to install OpenSquiggly and create a 100GB persistent volume, do:

```bash
helm install opensquiggly-test1 opensquiggly/allinone --set cloudType=linode,diskSize=100
```

### Video of Helm Installation

<iframe width="1024" height="754" src="https://www.loom.com/embed/4106ec21c42e43bf86aeecde3f077114" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
