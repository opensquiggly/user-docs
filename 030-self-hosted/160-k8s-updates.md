---
weight: 160
url: /docs/self-hosted/k8s/install-updates
order: 16
title: "Kubernetes : Installing Updates"
description: How to update to a newer version of OpenSquiggly.
---
## Introduction
When you install OpenSquiggly using the Helm chart, the ```version``` setting
specifies which build number of the container image it should use. The latest
version is built into the Helm chart, and you don't normally specify the version
when you install OpenSquiggly for the first time.

However, after installation, you can update OpenSquiggly to a newer version than
the version you are running.

## Determining Your Current Version
To determine which version of OpenSquiggly you are currently running, run the
following command and examine the ```version``` setting. It should be the last
value in the list.

```bash
helm get values --all your-release-name-here
```

For example:

```bash
helm get values --all opensquiggly-test1
```

Sample Output:

```
COMPUTED VALUES:
cloudType: other
configSecretName: ""
diskSize: 50
diskSkuName: ""
diskType: ""
dnsHostName: civokube2-test1.opensquiggly.com
esMaxHeapSize: 512m
esMinHeapSize: 512m
existingPvStorageClass: ""
exposeWith: nginx
ingressClassName: nginx
start: true
storageProvisioner: ""
tlsSecretName: opensquigglycert
useExistingPv: ""
useExistingPvc: ""
useExistingStorageClass: civo-volume
version: 1347   <--------- Currently installed OpenSquiggly version number
```

## Determining the Latest Version
To determine if there is a later published version of OpenSquiggly than the version
you are running, first update your Helm chart with the command:

```bash
helm repo update
```

Then issue the following command and examine the ```version``` value. Once again, it
should be the last value in the list.

```bash
helm show values opensquiggly/allinone
```

Sample Output:

```
.
. Other values omitted for brevity
.

# To use the Nginx ingress controller with a custom ingress class name that you've
# previously created, enter the name of the ingress class here. 
ingressClassName: "nginx"

# Specify the initial (mininum) ElasticSearch heap size, depending on the size of 
# the nodes in your cluster. Heap size should be no larger that 50% of available 
# memory of the node. Use the "m" suffix for megabytes and the "g" suffix for 
# gigabytes.
esMinHeapSize: "512m"

# Specify the maximum ElasticSearch heap size.
esMaxHeapSize: "512m"

configSecretName: ""

# If start=true, set deploy replicas to 1, otherwise set to 0
start: true

version: 1347   <--------- Latest published version of OpenSquiggly
```

## Updating to a Newer Version
To update your OpenSquiggly release to a new version, leaving all other existing
Helm chart settings unchanged, issue the command:

```bash
helm upgrade release-name-here opensquiggly/allinone --reuse-values --set version=xxxx
```

where ```xxxx``` is the desired version.

For example, to update the ```opensquiggly-test1``` release to version ```1348```, issue
the command:

```bash
helm upgrade opensquiggly-test1 opensquiggly/allinon --reuse-values --set version=1348
```
