---
weight: 120
url: /docs/self-hosted/k8s/docker-desktop
order: 12
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
Docker Desktop works a little different in exposing LoadBalancer services than does
<a href="/docs/self-hosted/k8s/minikube">Minikube</a>.

Get a list of your current Kubernetes services with the command:

```bash
kubectl get svc
```

Sample Output

```bash
NAME                TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
kubernetes          ClusterIP      10.96.0.1        <none>        443/TCP        185d
opensquiggly1-svc   LoadBalancer   10.97.179.94     localhost     80:30893/TCP   13m
                                                    ---------
                                                        ^
                                                        |
               Load balancer is exposed to localhost ---+
```

Notice that the LoadBalancer has been assigned ```localhost``` as the external-ip address.
For comparison, Minikube, doesn't do this ... it leaves the external-ip address as ```pending```.

Since the OpenSquiggly LoadBalancer service is published to localhost, that means we can simply
navigate the browser to ```localhost``` (without any other port numbers) and we should get to
the OpenSquiggly login page.

```bash
localhost
```

## Limitations and Workarounds
While it is convenient that Docker Desktop exposes the external-ip address of the service to
```localhost```, there's an obvious problem. What happens if you install two services that both
need LoadBalancers, and therefore both want access to ```localhost``` as their external-ip address?

Docker Desktop will only expose one LoadBalancer to ```localhost```. Any other LoadBalancers will
remain in the ```pending``` state for their external-ip address. This means you can only
have one service at a time accessible to your browser.

To get around this, you can use Kubernete's <a href="https://kubernetes.io/docs/reference/kubectl/generated/kubectl_port-forward/" target="_blank">port forwarding</a>
feature.

```bash
kubectl port-forward svc/service-name port_number:80
```

For example, in the above example we could expose the opensquiggl1-svc to port 4000 with the command:

```bash
kubectl port-forward svc/opensquiggly1-svc 4000:80
```

Note that the external port number we choose (4000 in this case), does not need to match the internal
port number (30893 in this case). 

We can now access OpenSquiggly by navigating the browser to:

```bash
localhost:4000
```
