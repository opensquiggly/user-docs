---
weight: 70
order: 7
Title: Installing on Kubernetes
description: >
  Installing OpenSquiggly on the Kubernetes cloud orchestrator, instead of a virtual
  machine is also possible. In this section we give an overview of the installation
  process on Kubernetes, and discuss pros and cons of using Kubernetes vs. a virtual
  machine.
---
## Overview of Installing on Kubernetes

Kubernetes is an open-source container orchestration platform that enables automated 
deployment, scaling, and management of containerized applications. It is a powerful 
tool for managing complex distributed systems and has gained popularity among developers 
and IT teams for its ability to simplify deployment and management of applications. In 
this section, and in the subsequent cloud-specifc sections, we will walk you through the 
steps for installing OpenSquiggly on Kubernetes.

For more information on Kubernetes in general, visit https://kubernetes.io

When it comes to choosing between installing OpenSquiggly on a virtual machine, as discussed
in the prior sections, or a Kubernetes cluster, there are several factors to consider.

### Pros

1. *__Fewer Installation Steps__*: While Kubernetes brings with it a learning curve and some
   some added complexity, you may actually find it easier and faster to install OpenSquiggly
   on Kubernetes because the Helm chats we provide making it possible to install OpenSquiggly
   with a single command.

2. *__Managing External Disks__*: Kubernetes' usage of persistent volumes and persistent volume
   claims, along with dynamic provisioning, makes it easier to add external disk space to your
   OpenSquiggly service. With a VM installation, you need to manually create the disk using
   your cloud provider's tools, then attach it to the VM, then partition and format it, then
   mount it, then add the mounting spec to your fstab file. Even if it only takes a few minutes
   to do, it's still a hassle. With Kubernetes and our Helm charts, you just tell us how big
   you want your disk, and Kubernetes will dynamically provision it and set it all up with no
   extra steps.

3. *__Standardization__*: Kubernetes provides a standardized way of deploying and managing
   applications, which makes it easier to manage and maintain your application infrastructure.
   Kubernetes is generally cloud-agnostic and is available as a managed service on all popular
   cloud providers.

4. *__Familiarity__*: In recent years Kubernetes has become the dominant, and arguably the
   de facto standard container orchestrator in cloud computing. Most IT departments are 
   already familiar with it.

5. *__Better Resource Utilization__*: Kubernetes enables better resource utilization by scheduling 
   containers on nodes based on available resources. This means that you can get the most out 
   of your hardware resources, without having to manually optimize virtual machines.

6. *__High Availability__*: Kubernetes ensures that your applications are highly available by 
   automatically detecting and replacing failed containers. This means that your application 
   can recover quickly from failures, without having to manually manage virtual machines.

### Cons:

1. *__Complexity__*: Kubernetes has a steep learning curve and requires a significant 
   investment in terms of time and effort to set up and manage. This means that it may 
   not be the best choice for small projects or teams with limited resources. With that
   being said, we've tried our best to provide thorough setup documentation and instructional
   videos to make installation on Kubernetes as easy as possible.

2. *__Overhead__*: Kubernetes adds an additional layer of abstraction between your 
   application and the underlying infrastructure. This means that there is some overhead 
   involved in managing Kubernetes clusters, which may impact the performance of your application.

3. *__Cost__*: Kubernetes requires additional resources to run, such as nodes and 
   networking infrastructure. This means that there may be additional costs associated 
   with running Kubernetes clusters, compared to running virtual machines.

Overall, installing OpenSquiggly on Kubernetes can provide a more robust, easier to install,
and easier to maintain experience than installing it on a virtual machine.

<hr>

## Installing kubectl

The kubectl command line tool is used to connect to your Kubernetes cluster and create
and manage its resources, including the OpenSquiggly resources that we cover in later
sections. You'll need the kubectl command installed in your desktop in order to execute
the installation instructions provided in later sections.

### Installing kubectl on Windows

Download the latest release `kubectl.exe` from the [official Kubernetes releases page on GitHub](https://github.com/kubernetes/kubernetes/releases).

After downloading the executable, place it in a directory that's in your system's PATH.

### Installing kubectl on MacOS

The easiest way to install `kubectl` on macOS is through Homebrew. If you don't have Homebrew installed, you can install it by following the instructions at [https://brew.sh/](https://brew.sh/).

### Installing kubectl on Linux

1. On Linux, you can use `curl` to download `kubectl`. Replace `VERSION` with the version number of Kubernetes you want to download:

```bash
curl -LO "https://dl.k8s.io/release/vVERSION/bin/linux/amd64/kubectl"
```

### Testing Your kubectl Installation

After installing kubectl, verify it is in your path and accessible from your command line shell.

```bash
kubectl version --short
```

<hr>

## Installing Helm

Helm is often referred to as the 'package manager for Kubernetes'. It's a tool that
streamlines the process of installing, configuring, and upgrading applications that
are deployed on Kubernetes. Helm uses a packaging format called 'charts', which are
collections of files that describe a related set of Kubernetes resources. By using Helm,
you can manage complexity and simplify the deployment of applications in your Kubernetes
clusters. In the following sections, we'll guide you through the process of installing
Helm on your system.

### Installing Helm on Windows

1. Install Chocolatey, a package manager for Windows. You can find the instructions at
   [https://chocolatey.org/install](https://chocolatey.org/install).

2. Once Chocolatey is installed, install Helm by running the following command in your
   command prompt:


### Installing Helm on MacOS

1. The easiest way to install Helm on macOS is through Homebrew. If you don't have
   Homebrew installed, you can install it by following the instructions at [https://brew.sh/](https://brew.sh/).

2. Once Homebrew is installed, you can install Helm with the following command:

### Installing Helm on Linux

1. On Linux, you can use `curl` to download the latest Helm binary. Run:
```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
