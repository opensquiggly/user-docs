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

Beware, however, that EKS is also one of the more complex and difficult to create and
configure Kubernetes systems on the market, and so you'll want to be prepared for some
learning and some effort in the process. If you have access to a cloud engineering team
that you can go to fo advice and guidance within your company, then we highly suggest
reaching out to those resources.

If you aren't sure you really want to use EKS, don't have access to an internal cloud
engineering team, or work for a smaller company that may not need everything that Amazon
and EKS has to offer, then you might want to consider going with a simpler Kubernetes
provider such as Linode or Digital Ocean, which we also have documented in this chapter.

There are so many EKS configuration options, that our videos and documents will only be
able to cover the very basics, so once again, if you have advanced requirements please
reach out to your company's cloud engineering team if possible.

