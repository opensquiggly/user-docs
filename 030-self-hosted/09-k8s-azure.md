---
weight: 90
url: /docs/self-hosted/k8s/azure
order: 9
Title: "Kubernetes : Azure"
descripton: How to install OpenSquiggly on Microsoft's Azure Kubernetes Service (AKS).
---
## Overview of Installing on AKS

Azure Kubernetes Service, or AKS for short, is Azure's managed Kubernetes service.
The steps for installing OpenSquiggly on Kubernetes from any cloud provider are similar.
In this section, we'll offer up some extra information and suggestions that are 
relevant to AKS.

<hr>

## Part 1 : Creating the AKS Cluster

### Steps to Complete

1. Visit your Azure Portal at https://portal.azure.com and login to your Azure account.
2. In the search box, search for "Kubernetes services", and select it from the list.
3. Click the Create button near the top left portion of the portal, and choose the "Create a Kubernetes cluster"
   option from the dropdown list.
4. Under the Basics tab, fill in the desired parameters for the VM:
   * Subscription
   * Resource Group
   * Enter a cluster name
   * Pick one of the preset configurations (Production Standard, Dev/Test, etc.)
   * Review any of the other options you may wish to change, or leave the defaults selected
5. To set advanced options, navigate to the Node pools, Networking, Integrations, Monitoring,
   Advanced, or Tags tabs.
6. When you've finished reviewing all of your options, click the "Review + create" button to start the provisioning process.

### Video
<iframe 
  width="1024" 
  height="818" 
  src="https://www.youtube.com/embed/ZAYrg92wRzw" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>

<div>
   <ul>
     <li><a href="https://www.youtube.com/watch?v=ZAYrg92wRzw" target="_blank">Open Video in YouTube</a></li>
   <ul> 
</div>

<hr>

## Part 2 : Connecting kubectl to AKS

We assume you've followed the instructions provided earlier to install the kubectl
command line tool.

In order to use kubectl with AKS, you'll need to use the az command line tool to
create a context that points to your cluster.

Issue the following command:

```bash
az aks get-credentials --resource-group your-resource-group-here --name your-cluster-name-here
                                        ------------------------        ----------------------
                                                   ^                               ^
                                                   |                               |
                                                   +-- Enter your information  ----+
```

If you're not already logged into Azure, you'll get a message and/or prompt with additional
information. If necessary, you can log into Azure with:

```bash
az login
```

This may open up a browser window and ask you to follow instructions for two factor authentication.

For additional help, consult the Microsoft documentation here:

* https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-cluster

### Verifying Your Connection

Verify that your desired AKS cluster is set as your current context.

```bash
kubectl config get-contexts
```

Issue the command:

```bash
kubectl get nodes
```

If you are successfully connected to Azure, you should see a list containing at least one
agent node pool.

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

## Part 5 : Install OpenSquiggly with Helm

```bash
helm install your-helm-relelase-name-here opensquiggly/allinone --set cloudType=azure[,diskSize=xx]
```

Helm release names can contain alphanumeric characters and the hyphen.

### With Default Parameters

```bash
helm install opensquiggly-test1 opensquiggly/allinone --set cloudType=azure
```

### Example With 100G Storage

```bash
helm install opensquiggly-test1 opensquiggly/allinone --set cloudType=azure,diskSize=100
```

### Testing the Install

Ensure that the pod has started by issuing the command:

```bash
kubectl get pods [--watch]
```

When the pod is running, retrieve the load balancer IP address with:

```bash
kubectl get svc
```

Hit the IP address with your browser and that should take you to the OpenSquiggly login screen.

### Video of Installing with Helm

<iframe width="1024" height="795" src="https://www.youtube.com/embed/YdVtCwnj2jk" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

<div>
  <ul>
    <li><a href="https://www.youtube.com/watch?v=YdVtCwnj2jk" target="_blank">Open Video in YouTube</a></li>
  <ul>
</div>