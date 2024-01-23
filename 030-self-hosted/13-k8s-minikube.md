---
weight: 130
url: /docs/self-hosted/k8s/minikube
order: 13
title: "Kubernetes : Minikube"
description: How to install OpenSquiggly on Minikube.
---
## Overview of Installing on Minikube

Minikube is a lightweight distribution of Kubernetes that can be installed
on your local desktop. This is an excellent option for evaluating OpenSquiggly
with an environment that is both isolated and easy to get running.

## Prerequistes

* Install Minikube by following the directions <a href="https://minikube.sigs.k8s.io/docs/start/" target="_blank">here</a>.
* Install the ```kubectl``` and ```helm``` tools using the instructions <a href="/docs/self-hosted/kubernetes/#installing-kubectl">here</a>.
* Set your ```kubectl``` context to minikube.
* Add the OpenSquiggly Helm chart repository to your list of Helm repositories:

```bash
helm repo add opensquiggly https://opensquiggly.github.io/helm-charts
```

## Option 1 : Use the Host Path CSI Driver and Install the Helm Chart

We recommend you install the Host Path CSI driver before installing OpenSquiggly. This
will make the ```hostpath.csi.k8s.io``` storage provisioner available in your cluster,
which is the default provisioner that the OpenSquiggly Helm charts uses for minikube.

This is the safest option, because the Helm chart can create its own storage class with
a ReclaimPolicy of ```Retain``` instead of the default ReclaimPolicy of ```Delete```. This
means that if you delete your OpenSquiggly installation, either purposefully or accidentally,
the associated persistent volume will not be deleted, and you'll have a chance to make
a backup of it or reuse it in another deployment.

For more information on the Host Path CSI driver, see the documentation <a href="https://minikube.sigs.k8s.io/docs/tutorials/volume_snapshots_and_csi/" target="_blank">here</a>.

To install the driver, run:
```bash
minikube addons enable csi-hostpath-driver
```

Then, verify that the installation was successful with:

```bash
kubectl get storagesclass
```

The ```hostpath.csi.k8s.io``` storage provisioner should appear in the output list.

```bash
NAME                 PROVISIONER                RECLAIMPOLICY   VOLUMEBINDINGMODE   ALLOWVOLUMEEXPANSION   AGE
csi-hostpath-sc      hostpath.csi.k8s.io        Delete          Immediate           false                  18m  <----
standard (default)   k8s.io/minikube-hostpath   Delete          Immediate           false                  185d

```

From your terminal, run the command:

```bash
helm install release-name-here opensquiggly/allinone --set \
  cloudType=minikube \
  [diskSize=xxx] (optional - where xxx is the desired volume size in Gigabytes)
```

Example:

```bash
helm install opensquiggly-test1 opensquiggly/allinone --set cloudType=minikube,diskSize=30
```

The chart should install and OpenSquiggly should install in a matter of a few seconds to
a minute.

To check the storage class that the Helm chart created, run:
```bash
kubectl get storageclass
```

Sample Output:
```bash
NAME                         PROVISIONER                RECLAIMPOLICY   VOLUMEBINDINGMODE      ALLOWVOLUMEEXPANSION   AGE
csi-hostpath-sc              hostpath.csi.k8s.io        Delete          Immediate              false                  100m
opensquiggly1-storageclass   hostpath.csi.k8s.io    --> Retain <--      WaitForFirstConsumer   true                   75m  <----
standard (default)           k8s.io/minikube-hostpath   Delete          Immediate              false                  185d
```

Notice that the newly created storage class ```opensquiggly1-storageclass``` has a ReclaimPolicy of Retain. 

Next, examine the persistent volume created by the Helm chart with the command:

```bash
kubectl get pv
```

Sample Output
```bash
NAME              CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                       STORAGECLASS                 
pvc-xxx-omitted   30Gi       RWO        --> Retain <--       Bound    default/opensquiggly1-pvc   opensquiggly1-storageclass
```

Notice that the persistent volume also has its ReclaimPolicy set to Retain. From here, if you uninstall the Helm chart,
the persistent volume will not be deleted until you issue an explicit delete command. We designed the Helm chart this
way to help prevent unintentional deletion of data.

## Option 2 : Use the Standard Storage Class

If you don't wish to activate the CSI driver, you can use the ```standard``` storage class that comes with minikube
by default. In that case, you can tell the Helm chart to use the existing storage class with the command:

```bash
helm install opensquiggly2 opensquiggly/allinone --set cloudType=minikube,useExistingStorageClass=standard
```

Aftwards, if you list your persistent volumes, notice the ReclaimPolicy is set to ```Delete```.

```bash
NAME              CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                       STORAGECLASS
pvc-xxx-omitted   32Gi       RWO        --> Delete <--       Bound    default/opensquiggly2-pvc   standard
```

Now if you uninstall the Helm chart, your data will be deleted along with the installation and you'll have no
chance to recover the data. For this reason, we recommend using the Host Path CSI driver option if possible.

## Navigating to OpenSquiggly

After the installation has succeeded, and your deployment and associated pod is running, 
retrieve the port number that the OpenSquiggly Load Balancer is running on with the
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