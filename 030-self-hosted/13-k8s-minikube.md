---
weight: 130
url: /docs/self-hosted/k8s/minikube
order: 13
title: "Kubernetes : Minikube"
description: How to install OpenSquiggly on Minikube
---
## Overview of Installing on Minikube

Minikube is a lightweight distribution of Kubernetes that can be installed
on your local desktop. This is an excellent option for evaluating OpenSquiggly
with an environemtn that is both isolated and very easy to get running.

## Prerequistes

* Install Minikube by following the directions <a href="https://minikube.sigs.k8s.io/docs/start/" target="_blank">here</a>.
* Install the ```kubectl``` and ```helm``` tools using the instructions <a href="http://localhost:1313/docs/self-hosted/kubernetes/#installing-kubectl >here</a>.
* Set your kubectl context to minikube.
* Add the OpenSquiggly Helm chart repository to your list of Helm repositories:

```bash
helm repo add opensquiggly https://opensquiggly.github.io/helm-charts
```

## Install the Helm Chart

From your terminal, run the command:

```bash
helm install release-name-here opensquiggly/allinone --set \
  cloudType=other \
  [diskSize=xxx] (optional - where xxx is the desired volume size in Gigabytes)
  storageProvisioner=k8s.io/minikube-hostpath \
  useExistingStorageClass=standard
```

Example:

```bash
helm install opensquiggly-test1 opensquiggly/allinone --set \
  cloudType=other \
  diskSize=100 \
  storageProvisioner=k8s.io/minikube-hostpath \
  useExistingStorageClass=standard
```

The chart should install and OpenSquiggly should install in a matter of a few seconds to
a minute.

Afterwards, retrieve the port number that the OpenSquiggly Load Balancer is running on with the
command:

```bash
kubectl get svc
```

Sample Output

```bash
NAME                     TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
kubernetes               ClusterIP      10.96.0.1        <none>        443/TCP        185d
opensquiggly-test1-svc   LoadBalancer   10.97.179.94     <pending>     80:30893/TCP   13m
                                                                          -----
                                                                            ^
                                                                            |
                This is the port number you'll need for the next step  -----+
```


## Navigating to OpenSquiggly

Retrieve your Minikube IP address with the command:

```bash
minikube ip
```

Sample Output:
```bash
192.168.49.2
```

Navigate your browser to the IP address followed by a colon followed by the port number
of the service. For example:

```bash
192.168.49.2:30893
```