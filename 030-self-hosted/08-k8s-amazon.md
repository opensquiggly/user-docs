---
weight: 80
url: /docs/self-hosted/k8s/aws
order: 8
Title: "Kubernetes : Amazon AWS"
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
5. You'll also need to create an access key associated with the AWS account that you're using. You can then use the access key
   id and the secret access key in your environment variable or ~/.aws/config file. Follow these steps;
   1. From the AWS Console, click on the username dropdown in the upper-right corner, and select "Security credentials"
      from the list.
   2. Scroll down to the "Access keys" section and click the "Create access key" button, and confirm any prompts given.
      If you're logged in as the root user, the system will warn you about best practices, but will still let you
      create an access key.
   3. Retrieve the generated access key id and the secret access key and store it in a secure location such as a password
      vault. Note that you will not be able to retrieve the secret access key after closing the window.
6. In your command line environment, set the access key id using one of the following methods:<br>
   To store the value in your ~/.aws/configure file do:
   ```bash
   aws configure set access_key access-key-id-goes-here
   ```
   OR, to store the value in your environment variables do:<br>
   ```bash
   export AWS_ACCESS_KEY_ID=access-key-id-goes-here
   ```
7. In your command line environment, set the secret access key using one of the following methods:<br>
   To store the value in your ~/.aws/configure file do:
   ```bash
   aws configure set secret_key secret-access-key-goes-here
   ```
   OR, to store the value in your environment variables do:<br>
   ```bash
   export AWS_SECRET_ACCESS_KEY=secret-access-key-goes-here
   ```
8. Set a default AWS region using:
   ```bash
   aws configure set region region-name-here
   ```   
9. Confirm your configuration settings with the command:
   ```bash
   aws configure list
   ```  
10. Confirm your ```eksctl``` command is configured correctly using:
    ```bash
    eksctl get clusters
    ```
    and ensure that there are no error messages.

If everything looks good and you're not receiving any error messages, you should be ready to proceed with
creating the cluster.    

### Video
<iframe 
  width="1024" 
  height="818" 
  src="https://www.youtube.com/embed/4EDqlVaGLGE" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>

<div>
   <ul>
     <li><a href="https://www.youtube.com/watch?v=4EDqlVaGLGE" target="_blank">Open Video in YouTube</a></li>
   <ul> 
</div 

<hr>

## Part 2 : Creating the EKS Cluster

1. Use ```eksctl``` to initiate the cluster creation process using the command:
   ```bash
   eksctl create cluster --name your-cluster-name-here [--region your-region-name]
   ```
   Example:
   ```bash
   eksctl create cluster --name awscluster1 --region us-east-2
   ```
   Note: If you omit the region, it defaults to the setting specified in your ~/.aws/config file.
2. If everything is configured properly, you should start seeing messages on the screen regarding
   the cluster creation process, such as:
   ```bash
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

### Video
<iframe 
  width="1024" 
  height="818" 
  src="https://www.youtube.com/embed/U_z-4hjsqP4" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>

<div>
   <ul>
     <li><a href="https://www.youtube.com/watch?v=U_z-4hjsqP4" target="_blank">Open Video in YouTube</a></li>
   <ul> 
</div 

<hr>

## Part 3 : Configuring the Elastic Block Store CSI Driver

Now that the cluster is created, we're *almost* ready to run the ```helm``` command to install the OpenSquiggly
Helm chart. But, we've got one more step to do. While many other Kubernetes services on the market come with
a pre-installed block storage system and an associated CSI driver 
(<a href="https://kubernetes.io/blog/2019/01/15/container-storage-interface-ga/">Container Storage Interface</a>),
this is an add-on feature for EKS, and we need to install it separately.

The purpose of the block storage CSI driver with respect to OpenSquiggly is the auto-provisioning of the disk
space that OpenSquiggly uses for logs, databases, indexes, and repository cloning.

Without the EBS CSI driver, OpenSquiggly's Helm chart will get "stuck" at the point in the spin up process where
it tries to create the persistent volume and wait for it to be ready. Therefore, we need to install the CSI
driver before we run the Helm chart.

For additional documentation, see <a href="https://docs.aws.amazon.com/eks/latest/userguide/ebs-csi.html">Amazon EBS CSI driver</a>.

1. Associate the OIDC provider with your cluster with:
   ```bash
   eksctl utils associate-iam-oidc-provider --cluster=your-cluster-name-here --approve [--region=your-region-name-here]
   ```
1. First, create an IAM role with the following command:
   ```bash
   eksctl create iamserviceaccount \
     --name ebs-csi-controller-sa \
     --namespace kube-system \
     --cluster your-cluster-name-here \            <----- The name of your cluster goes on this line
     --role-name AmazonEKS_EBS_CSI_DriverRole \    <----- You can name the role as you choose, this is the suggested name
     --role-only \
     --attach-policy-arn arn:aws:iam::aws:policy/service-role/AmazonEBSCSIDriverPolicy \
     --approve
   ```
   Here is a one-line version for easier copy/pasting:
   ```bash
   eksctl create iamserviceaccount --name ebs-csi-controller-sa --namespace kube-system --cluster your-cluster-name-here --role-name AmazonEKS_EBS_CSI_DriverRole --role-only --attach-policy-arn arn:aws:iam::aws:policy/service-role/AmazonEBSCSIDriverPolicy --approve   
   ```
2. Create the ```eksctl``` addon for the CSI driver:
   ```bash
   eksctl create addon \
     --name aws-ebs-csi-driver \
     --cluster your-cluster-name-here \
     --service-account-role-arn arn:aws:iam::111122223333:role/AmazonEKS_EBS_CSI_DriverRole \
                                             ------------      ----------------------------
                                                 ^                          ^
                                                 |                          |
         Your account id  -----------------------+                          |
                                                                            |
                   The name of the role you specified previously -----------+
     --force
   ```
   Here is a one-line version for easier copy/pasting:
   ```bash
   eksctl create addon --name aws-ebs-csi-driver --cluster your-cluster-name-here --service-account-role-arn arn:aws:iam::111122223333:role/AmazonEKS_EBS_CSI_DriverRole --force   
   ```
   If needed, you can retrieve your account id by logging into the AWS Console and clicking on your account name in the upper-right corner
   in the menu bar.
3. Verify the CSI addon was successfully created using:
   ```bash
   eksctl get addon --name aws-ebs-csi-driver --cluster your-cluster-name-here 
   ```  

### Video
<iframe 
  width="1024" 
  height="818" 
  src="https://www.youtube.com/embed/VGuB2oCCDkg" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>

<div>
   <ul>
     <li><a href="https://www.youtube.com/watch?v=VGuB2oCCDkg" target="_blank">Open Video in YouTube</a></li>
   <ul> 
</div>

<hr>

## Part 4 : Connecting kubectl to EKS

After the cluster is created, the ```eksctl``` program should have modified your kube configuration file
(typically stored at ```~/.kube/config``` or in any locations specified by the ```KUBECONFIG```) environment
variable.

To ensure that ```kubectl``` is configured to connect to the cluster, issue the command:

```bash
kubectl config current-context
```

You should see the newly created cluster in the list and it should be selected as the default.

If you did not create the cluster using ```eksctl```, then you will need to set your kube config context
separately. To do this, use the followign command:

```bash
aws eks update-kubeconfig --name <cluster-name> [--region <region>]
```

To see a list of all contexts, use the command:

```bash
kubectl config get-contexts
```

To change the current context to a different default, use the command:

```bash
kubectl config use-context context-name-here
```

<hr>

## Part 5 : Setting up Helm

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

## Part 6 : Create a Kubernetes Namespace (Optional)

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

## Part 7 : Installing OpenSquiggly with Helm

```bash
helm install your-helm-release-name-here opensquiggly/allinone --set cloudType=aws[,diskSize=xx]
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

### Video
<iframe 
  width="1024" 
  height="818" 
  src="https://www.youtube.com/embed/TRLuEEojlBc" 
  frameborder="0" 
  webkitallowfullscreen 
  mozallowfullscreen 
  allowfullscreen>
</iframe>

<div>
   <ul>
     <li><a href="https://www.youtube.com/watch?v=TRLuEEojlBc" target="_blank">Open Video in YouTube</a></li>
   <ul> 
</div>

<hr>

## Part 8 : Testing the Install

Ensure that the pod has started by issuing the command:

```bash
kubectl get pods [--watch]
```

When the pod is running, retrieve the load balancer IP address with:

```bash
kubectl get svc
```

Hit the IP address with your browser and that should take you to the OpenSquiggly login screen.