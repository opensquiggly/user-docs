---
weight: 80
url: /docs/self-hosted/k8s/aws
order: 8
Title: "Kubernetes : Amazon"
description: How to install OpenSquiggly on Amazon's Elastic Kubernetes Service (EKS).
---
# Overview of Installing on EKS

Elastic Kubernetes Service, or EKS for short, is Amazon's managed Kubernetes service.
This chapter describes the specifics of installing OpenSquiggly on EKS, and outlines
any places where EKS installation may differ from the general Kubernetes installation
instructions.

# Should You Choose EKS?

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

# Links to Helpful Resources

For additional information on EKS, you may find these links helpful:

* <a href="https://docs.aws.amazon.com/eks/" target="_blank">EKS Documentation (by Amazon)</a>
* <a href="https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html" target="_blank">Install or update the latest version of the AWS CLI (by Amazon)</a>
* <a href="https://docs.aws.amazon.com/emr/latest/EMR-on-EKS-DevelopmentGuide/setting-up-eksctl.html" target="_blank">Install eksctl (by Amazon)</a>
* <a href="https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html" target="_blank">Getting started with Amazon EKS – eksctl (by Amazon)</a>
* <a href="https://www.youtube.com/watch?v=pNECqaxyewQ" target="_blank">eksctl - How to Create and Manage AWS EKS clusters (by DevOps Toolkit)</a>
* <a href="https://www.youtube.com/watch?v=p6xDCz00TxU" target="_blank">AWS EKS - Create Kubernetes cluster on Amazon EKS | the easy way (by TechWorld with Nana)</a>
* <a href="https://www.youtube.com/watch?v=CukYk43agA4" target="_blank">AWS EKS Tutorial | What is EKS? | EKS Explained (by KodeKloud)</a>

There are numerous other videos and resources on YouTube and the Web which can easily be found by searching. The links above should give you a good start.

# Part 1 : Creating the EKS Cluster

There are four main ways to create an EKS cluster.

* Use the AWS Web UI Portal
* Use the AWS Console
* Use the ```eksctl``` command line program
* Use an Infrastructure as Code solution such as Terraform or Pulumi

If you watched any of the above videos, then you'll know that using the ```eksctl``` program has
the unanimous consensus of being the fastest and easiest way to create an EKS cluster, and so that
is what we will use in this section.

In progress. Please check back later.

# Part 2 : Connecting kubectl to EKS

In progress. Please check back later.

# Part 3 : Setting up Helm

In progress. Please check back later.

# Part 4 : Create a Kubernetes Namespace (Optional)

In progress. Please check back later.

# Part 5 : Installing OpenSquiggly with Helm

In progress. Please check back later.