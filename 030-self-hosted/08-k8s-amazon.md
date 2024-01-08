---
weight: 80
url: /docs/self-hosted/k8s/aws
order: 8
Title: "Kubernetes : Amazon"
description: How to install OpenSquiggly on Amazon's Elastic Kubernetes Service (EKS).
---
## Overview of Installing on EKS

Elastic Kubernetes Service, or EKS for short, is Amazon's managed Kubernetes service.
This chapter describes the specifics of installing OpenSquiggly on EKS, and outlines
any places where EKS installation may differ from the general Kubernetes installation
instructions.

## Should You Choose EKS?

Amazon's EKS, being from Amazon, is undoubtedly the most popular managed Kubernetes 
service on the market. If your company already uses Amazon as its main cloud provider,
then of course you're going to be drawn towards using it.

Be aware, however, that EKS is also one of the more complex and difficult to
configure Kubernetes systems on the market, and so you'll want to be prepared for some
learning and some effort in the process. If you have access to a cloud engineering team
that you can go to for advice and guidance within your company, then we highly suggest
reaching out to those resources.

If you're lucky enough to work for a company that is forward-thinking enough to deploy
an all-company Kubernetes cluster, then you can just piggyback your OpenSquiggly install
on top of the company's existing cluster. In that case, all you need to do is a couple
short configuration steps to connect your local ```kubectl``` command to the existing cluster.

If you aren't sure you really want to use EKS, don't have access to an internal cloud
engineering team, or work for a smaller company that may not need everything that Amazon
and EKS has to offer, then you might want to consider going with a simpler Kubernetes
provider such as Linode or Digital Ocean, which we also have documented in this chapter.

There are so many EKS configuration options, that our videos and documents will only be
able to cover the very basics, so once again, if you have advanced requirements, particularly
around security concerns, please reach out to your company's cloud engineering team if possible.

## Links to Helpful Resources

For additional information on EKS, you may find these links helpful:

* <a href="https://docs.aws.amazon.com/eks/" target="_blank">EKS Documentation (by Amazon)</a>
* <a href="https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html" target="_blank">Install or update the latest version of the AWS CLI (by Amazon)</a>
* <a href="https://docs.aws.amazon.com/emr/latest/EMR-on-EKS-DevelopmentGuide/setting-up-eksctl.html" target="_blank">Install eksctl (by Amazon)</a>
* <a href="https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html" target="_blank">Getting started with Amazon EKS – eksctl (by Amazon)</a>
* <a href="https://www.youtube.com/watch?v=pNECqaxyewQ" target="_blank">eksctl - How to Create and Manage AWS EKS clusters (by DevOps Toolkit)</a>
* <a href="https://www.youtube.com/watch?v=p6xDCz00TxU" target="_blank">AWS EKS - Create Kubernetes cluster on Amazon EKS | the easy way (by TechWorld with Nana)</a>
* <a href="https://www.youtube.com/watch?v=CukYk43agA4" target="_blank">AWS EKS Tutorial | What is EKS? | EKS Explained (by KodeKloud)</a>
* <a href="https://aws.amazon.com/blogs/opensource/weaveworks-and-aws-joining-forces-to-maintain-open-source-eksctl/" target="_blank">Weaveworks and AWS Joining Forces to Maintain 
Open Source eksctl</a>
* <a href="https://eksctl.io/usage/schema/" target="_blank">Config file schema for eksctl (for advanced usage of eksctl)</a>

There are numerous other videos and resources on YouTube and the Web which can easily be found by searching. The links above should give you a good start.

<hr>

## Part 1 : Installing & Configuring Prerequisites

There are many ways to create an EKS cluster, including:

* Get your cloud engineering team to do it for you
* Use the AWS Console (i.e., the web portal)
* Use the ```aws``` CLI
* Use the ```eksctl``` command utility with command line parameters
* Use the ```eksctl``` command utility with a configuration file
* Use an Infrastructure as Code solution such as Terraform or Pulumi

In these instructions we'll be using ```eksctl``` with command line parameters to create a very basic cluster
with default settings. This is only intended as a demo and a starting point.

1. If you have not already done so, install the ```aws``` CLI using the instructions <a href="https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html" target="_blank">here<a>. 
2. Install ```eksctl``` CLI using the instructions <a href="https://docs.aws.amazon.com/emr/latest/EMR-on-EKS-DevelopmentGuide/setting-up-eksctl.html" target="_blank">here.</a>
3. Install ```kubectl``` and ```helm``` per the instructions <a href="/docs/self-hosted/kubernetes/#installing-kubectl">here</a>.
4. *Important*: The AWS username that you use to create the cluster must have a role with the AmazonEKSClusterPolicy attached. Without such a role, you will get a 
   permissions error when attempting to create the cluster.
   1. Login to the AWS Console
   2. In the console's search bar, search for "IAM" (which stands for Identity and Access Management)
   3. Navigate to the Roles section.
   4. Follow the steps to create a new role.
   5. Attach the AmazonEKSClusterPolicy to the role.
   6. Apply the role to the user account.
5. You'll also need to create an access key associated with the AWS account that you're using. 

In progress. Please check back later.

<hr>

## Part 2 : Creating the EKS Cluster

1. Use ```eksctl``` to initiate the cluster creation process using the command:
   ```
   eksctl create cluster --name your-cluster-name-here [--region your-region-name]
   ```
   Example:
   ```
   eksctl create cluster --name awscluster1 --region us-east-2
   ```
   Note: If you omit the region, it defaults to the setting specified in your ~/.aws/config file.
2. If everything is configured properly, you should start seeing messages on the screen regarding
   the cluster creation process, such as:
   ```
   2024-01-08 16:00:21 [ℹ]  eksctl version 0.167.0
   2024-01-08 16:00:21 [ℹ]  using region us-east-2
   2024-01-08 16:00:22 [ℹ]  setting availability zones to [us-east-2b us-east-2a us-east-2c]
   2024-01-08 16:00:22 [ℹ]  subnets for us-east-2b - public:192.168.0.0/19 private:192.168.96.0/19
   2024-01-08 16:00:22 [ℹ]  subnets for us-east-2a - public:192.168.32.0/19 private:192.168.128.0/19
   2024-01-08 16:00:22 [ℹ]  subnets for us-east-2c - public:192.168.64.0/19 private:192.168.160.0/19
   2024-01-08 16:00:22 [ℹ]  nodegroup "ng-357e2d8e" will use "" [AmazonLinux2/1.27]
   2024-01-08 16:00:22 [ℹ]  using Kubernetes version 1.27
   2024-01-08 16:00:22 [ℹ]  creating EKS cluster "awscluster1" in "us-east-2" region with managed nodes
   2024-01-08 16:00:22 [ℹ]  will create 2 separate CloudFormation stacks for cluster itself and the initial managed nodegroup
   .
   . (... etc ...)
   . 
   ```
3. In our testing, it usually takes about 15-20 minutes for the cluster to be created, so be patient.   

<hr>

## Part 3 : Connecting kubectl to EKS

After the cluster is created, the ```eksctl``` program should have modified your kube configuration file
(typically stored at ```~/.kube/config``` or in any locations specified by the ```KUBECONFIG```) environment
variable.

To ensure that ```kubectl``` is configured to connect to the cluster, issue the command:

```
kubectl config current-context
```

You should see the newly created cluster in the list and it should be selected as the default.

To see a list of all contexts, use the command:

```
kubectl config get-contexts
```

To change the current context to a different default, use the command:

```
kubectl config use-context context-name-here
```

<hr>

## Part 4 : Setting up Helm

Once you've ensured that your ```kubectl``` context is pointing to your newly created cluster,
you can proceed with running ```helm``` to install OpenSquiggly.

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

## Part 5 : Create a Kubernetes Namespace (Optional)

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

## Part 6 : Installing OpenSquiggly with Helm

```bash
helm install your-helm-relelase-name-here opensquiggly/allinone --set cloudType=aws[,diskSize=xx]
```

Helm release names can contain alphanumeric characters and the hyphen.

### With Default Parameters

```bash
helm install opensquiggly-test1 opensquiggly/allinone --set cloudType=aws
```

### Example With 100G Storage

```bash
helm install opensquiggly-test1 opensquiggly/allinone --set cloudType=aws,diskSize=100
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