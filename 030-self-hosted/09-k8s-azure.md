---
order: 9
Title: "Kubernetes : Azure"
---
# Overview of Installing on AKS

Azure Kubernetes Service, or AKS for short, is Azure's managed Kubernetes service.
The steps for installing OpenSquiggly on Kubernetes from any cloud provider are similar.
In this section, we'll offer up some extra information and suggestions that are 
relevant to AKS.

<hr>

# Part 1 : Creating the AKS Cluster

TODO

<hr>

# Part 2 : Connecting kubectl to AKS

We assume you've followed the instructions provided earlier to install the kubectl
command line tool.

In order to use kubectl with AKS, you'll need to use the az command line tool to
create a context that points to your cluster.

Issue the following command:

```
az aks get-credentials --resource-group your-resource-group-here --name your-cluster-name-here
                                        ------------------------        ----------------------
                                                   ^                               ^
                                                   |                               |
                                                   +-- Enter your information  ----+
```

If you're not already logged into Azure, you'll get a message and/or prompt with additional
information. If necessary, you can log into Azure with:

```
az login
```

This may open up a browser window and ask you to follow instructions for two factor authentication.

For additional help, consult the Microsoft documentation here:

* https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-cluster

# Verifying Your Connection

Verify that your desired AKS cluster is set as your current context.

```
kubectl config get-contexts
```

Issue the command:

```
kubectl get nodes
```

If you are successfully connected to Azure, you should see a list containing at least one
agent node pool.

<hr>

# Part 3 : Setting up Helm

View your current helm repos with:

```
helm repo list
```

Add the OpenSquiggly Helm charts repository to your local Helm repository list with the
command:

```
helm repo add opensquiggly https://opensquiggly.github.io/helm-charts
```

<hr>

# Part 4 : Create a Kubernetes Namespace (Optional)

It's a good idea to create a namespace to contain your OpenSquiggly resources that will
be installed by the Helm charts. This keeps your resources isolated from any other resources
you have installed on Kubernetes, avoids any naming conflicts, and makes it easier to
manage the resources later.

Create a namespace with the command:

```
kubectl create namespace your-namespace-here
```

Make the namespace your current namespace with the command:

```
kubectl config set-context --current --namespace=your-namespace-here
```

If this is a newly created namespace, issue the command:

```
kubectl get all
```

and verify that the namespace contains no existing resources.

<hr>

# Part 5 : Install OpenSquiggly with Helm

```
helm install your-helm-relelase-name-here opensquiggly/allinone --set cloudType=azure[,diskSize=xx]
```

Helm release names can contain alphanumeric characters and the hyphen.

## Example with Default 32G Storage:

```
helm install opensquiggly-test1 opensquiggly/allinone --set cloudType=azure
```

## Example with 100G Storage

```
helm install opensquiggly-test1 opensquiggly/allinone --set cloudType=azure,diskSize=100
```

## Testing the Install

Ensure that the pod has started by issuing the command:

```
kubectl get pods [--watch]
```

When the pod is running, retrieve the load balancer IP address with:

```
kubectl get svc
```

Hit the IP address with your browser and that should take you to the OpenSquiggly login screen.

## Video:

<iframe width="1024" height="795" src="https://www.loom.com/embed/bb167e75db3848fd9f4e98f578cb0d13" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>