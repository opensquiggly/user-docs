---
weight: 100
url: /docs/self-hosted/k8s/digital-ocean
order: 10
Title: "Kubernetes : Digital Ocean"
description: How to install OpenSquiggly on Digital Ocean Kubernetes Service (DOKS).
---
## Overview of Installing on DOKS

DigitalOcean Kubernetes, or DOKS for short, is DigitalOcean's managed Kubernetes service. Similar
to Linode, DigitalOcean offers a simpler and easier to understand pricing model compared to the
larger cloud providers, and has a broader array of services compared to Linode, though it tends
to get more expensive than Linode as you move upstream into beefier Kubernetes nodes with more
processing power and memory. As such it can be a good choice for customers who want the simplicity
of pricing model like Linode, but need more services than Linode offers.

This section will walk you through install OpenSquiggly on DOKS.

<hr>

## Part 1 : Creating a Kubernetes Cluster on DigitalOcean

To create a DigitalOcean cluster, visit:

```bash
digitalocean.com
```

then:

1. In the sidebar menu, select Kubernetes
2. Click the button "Create a Kubernetes Cluster"
3. Choose a datacenter region from the dropdown list
4. Select the desired Kubernetes version in the dropdown list
6. In "Choose cluster capacity" section, enter a node pool name and the machine type, 
   node plan, and the number of nodes. We recommend you choose a plan with at least two
   dedicated vCPUs and 4GB of memory per CPU. As per usual, all cloud providers recommend
   you choose at least 3 nodes for your node pool.
7. For production workloads, DigitalOceans recommends choosing the "Add high availabilty"
   option to create a high availability control plan. As of this writing, the HA Control Plane 
   adds $40 per month to the pricing. Note that you can always upgrade your control plane 
   later, but once you choose it, you can't downgrade it without creating a new cluster.
9. In the "Finalize" section, enter a name for the cluster.
10. When you've selected all options, click Create Cluster to checkout and start provisioning
   the cluster.
11. After the cluster is provisioned, follow the instructions provided by DigitalOcean (and
    covered in more detail in the next section) to connect your kubectl command to the newly
    created cluster. DigitalOcean gives you two options for this - either using the doctl
    command line program (which you'll need to install first), or downloading the kubeconfig.yaml
    file and referencing it in your KUBECONFIG path.

### Video of Creating DOKS Cluster
<iframe width="1024" height="804" src="https://www.youtube.com/embed/MXpJjtvC38E" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

<hr>

## Part 2 : Connecting kubectl to the DigitalOcean Cluster

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
helm install your-helm-relelase-name-here opensquiggly/allinone --set cloudType=digitalocean
```

Helm release names can contain alphanumeric characters and the hyphen.

Example:

```bash
helm install opensquiggly-test1 opensquiggly/allinone --set cloudType=digitalocean
```

This will create a persistent volume of 32GB in size, using the block storage provisioner
linodebs.csi.linode.com that comes supply by Linode.

### Setting the Disk Size

If you need more or less disk space, you can change the size using the diskSize parameter
and setting it to an integer value in gigabytes.

For example, to install OpenSquiggly and create a 100GB persistent volume, do:

```bash
helm install opensquiggly-test1 opensquiggly/allinone --set cloudType=digitalocean,diskSize=100
```

### Video of Installing with Helm

<iframe width="1024" height="754" src="https://www.loom.com/embed/86eca9cc4fac4b9bb8bfdddb0887aacf" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
