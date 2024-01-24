---
weight: 115
url: /docs/self-hosted/k8s/docker-desktop
order: 11
title: "Kubernetes : Docker Desktop"
description: How to install OpenSquiggly on Docker Desktop Kubernetes.
---
## Overview of Installing on Docker Desktop

The Kubernetes distribution that comes as part of 
<a href="https://www.docker.com/products/docker-desktop/" target="_blank">Docker Desktop<a> is,
similar to <a href="/docs/self-hosted/k8s/minikube/">Minikube</a>, a lightweight, desktop installable
Kubernetes manager and an excellent option for evaluating OpenSquiggly.

## Install Prerequisites

* Install Docker Desktop
* Install the ```kubectl``` and ```helm``` tools using the instructions <a href="/docs/self-hosted/kubernetes/#installing-kubectl">here</a>.
* Add the OpenSquiggly Helm chart repository to your list of Helm repositories:

```bash
helm repo add opensquiggly https://opensquiggly.github.io/helm-charts
```

## Enable Kubernetes

Kubernetes comes as part of the Docker Desktop installation, but is not enabled by default.

To enable Docker Desktop Kubernetes, open your Docker Desktop preferences, navigate to the
Kubernetes section, and click the "Enable Kubernetes" checkbox.

Doing so will add "docker-desktop" to your Kubernetes context list.

To verify that Docker Desktop Kubernetes is available, open a terminal and issue the command:

```bash
kubectl config get-contexts
```

Confirm that "docker-desktop" appears in the list and is set as your current context.

## Install OpenSquiggly Using the Helm Chart

Install OpenSquiggly using the command:

```bash
helm install release-name-here opensquiggly/allinone --set cloudType=docker-desktop[,diskSize=xx]
```

where ```xx``` is the desired disk size in gigabytes. If omitted, the default disk size is 32Gb.

Example:

```bash
helm install opensquiggly1 opensquiggly/allinone --set cloudType=docker-desktop,diskSize=40
```

## Navigating to OpenSquiggly

After the installation has succeeded, and your deployment and associated pod is running, 
retrieve the port number that the OpenSquiggly Load Balancer is running on with the
command:

```bash
kubectl get svc
```

Sample Output

```bash
NAME            TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
kubernetes      ClusterIP      10.96.0.1        <none>        443/TCP        185d
opensquiggly1   LoadBalancer   10.97.179.94     localhost     80:30893/TCP   13m
                                                                 -----
                                                                   ^
                                                                   |
       This is the port number you'll need for the next step  -----+
```

Navigate your browser to ```localhost``` followed by a colon followed by the port number
of the service. For example:

```bash
localhost:30893
```
