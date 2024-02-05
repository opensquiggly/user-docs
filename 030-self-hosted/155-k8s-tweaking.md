---
weight: 155
url: /docs/self-hosted/k8s/tweaks
order: 16
title: "Kubernetes : Tweaking Your Settings"
description: How to fine tune your settings to get the most out of OpenSquiggly.
---
## Introduction
After you've done the initial installation of OpenSquiggly on your Kubernetes cluster,
you may want to adjust your settings after-the-fact to add functionality or change some
important configuration values.

## General Approach for Updating Settings
If you've installed OpenSquiggly using the provided Helm charts, then you should always make changes
through Helm. You shouldn't be using ```kubectl``` to go behind the scenes to make changes that were
initially set by Helm. By always using Helm to make changes, you'll ensure that the Helm ```history```,
```upgrade```, and ```rollback``` functions are in sync with the actual state of the cluster.

To change any Helm chart setting after the initial installation, use the command of the format:

```bash
helm upgrade your-release-name opensquiggly/allinone --reuse-values --set new-values-here
```

The ```--reuse-values``` flag will keep all existing values in the Helm installation unmodified except
the ones specified after the ```--set``` flag.

For example, if your release is named ```opensquiggly1``` and you want to change the ```dnsHostName```
to ```new.yourcompany.com``` while keeping all other settings unmodified do:

```bash
helm upgrade opensquiggly1 opensquiggly/allinone --reuse-values --set dnsHostName=new.yourcompany.com
```

## Stopping & Restarting OpenSquiggly
Most of the time you won't need to stop the OpenSquiggly instance (which in Kubernetes parlance
would mean killing the OpenSquiggly pod), but occassionaly you may need to. One example of
when you might need to stop the instance is if you are resizing the disk volume and are using
a cloud provider that doesn't support online resizing. Another example would be if you wanted to
relocate the database from the default internal MongoDB database to an externally hosted database.

The ```start``` flag in the Helm chart can be used to set whether the pod is active or inactive.

To stop the OpenSquiggly instance, do:

```bash
helm upgrade release-name opensquiggly/allinone --reuse-values --set start=false
```

Afterwards, confirm that the OpenSquiggly pod is no longer running with the command:

```bash
kubectl get pods
```

The associated OpenSquiggly pod should no longer appear in the list of pods.

To restart the instance after you've stopped it, do:

```bash
helm upgrade release-name opensquiggly/allinone --reuse-values --set start=true
```

Aftwards, confirm the pod has restarted with the command:

```bash
kubectl get pods --watch
```

It may take a few minutes for the pod to fully initialize.

## Resizing Volumes
We've created our Helm charts to make it easy to resize your disk space after the installation. By
doing it this way, you don't need to over allocate your disk space, and over pay for your hosting costs.

We recommend starting with a modest disk size in the order of 10 - 50 GB. Later, after you've attached a 
lot of mount points and run low on disk space, you can increase the disk size as-needed.

Note that you can never make the disk size smaller after you've increased it. This phenomenon also
means you won't be able to do a ```helm rollback``` to rollback to a prior revision that existed before
resizing.

### If Your Cloud Provider Supports Online Resizing
In many cases, depending on your cloud provider and the storage class you are using, your cluster
may support online resizing of the disk space. This means you can resize the disk while keeping the
OpenSquiggly instance running.

In this case, increasing the disk space is a simple matter of changing the ```diskSize``` property
with the command:

```bash
helm upgrade release-name opensquiggly/allinone --reuse-values --set diskSize=new-size-in-gigabytes
```

For example, to change your disk space for the ```opensquiggly1``` release to 50GB, do:

```bash
helm upgrade opensquiggly1 opensquiggly/allinone --reuse-values --set diskSize=50
```

### If Your Cloud Provider Requires Offline Resizing
If your cloud provider doesn't support online resizing, then you'll need to stop the instance,
resize the disk, and restart.

Here is the sequence of commands for such:

```bash
# Stop the instance
helm upgrade release-name opensquiggly/allinone --reuse-values --set start=false

# Wait for pod to shut down (should shut down immediately)
kubectl get pods --watch

# Do the resize independent of the restart. This gives the new size a chance to
# take affect before restarting
helm upgrade release-name opensquiggly/allinone --reuse-values --set diskSize=new-size

# Restart only after resizing
helm upgrade release-name opensquiggly/allinone --reuse-values --set start=true

# Wait for pod to start
kubectl get pods --watch
```

## Revision History
Each time you make any changes to a Helm release, a new revision is created with the
updated settings. To view the list of revisions do:

```bash
helm history release-name-here
```

## Viewing Current Values
To see the list of all Helm chart values for the current revision, do:

```bash
helm get values release-name-here --all
```

## Viewing Values for a Prior Revision
To see the list of all Helm chart values for a past revision, do:

```bash
helm get values release-name-here --all --revision rev-number-here
```

## Rollbacks
To perform a rollback to a prior revision of the release, do:

```bash
helm rollback release-name-here rev-number-here
```

This creates a new revision with the settings equal to that of the specified
prior revision.