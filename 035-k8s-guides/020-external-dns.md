---
weight: 20
url: /docs/k8s-guides/external-dns
Order: 1
Title: Creating DNS Names Automatically
description: >
  How to install and use the ExternalDNS service to automatically
  create DNS names corresponding to your OpenSquiggly instance(s).
---

## Introduction

If you followed the steps to install the NGINX ingress controller
(<a href="/docs/k8s-guides/nginx">see here</a>), you know that the
ingress controller has an associated Load Balancer service, which in
turn is assigned a fixed IP address.

This is not very convenient to the OpenSquiggly users, as they would need
to know the IP address in order to access the system.

We need to create a custom DNS name that users can use to do that.

While you can always manually create DNS names in your DNS server, its much
more convenient to automate the creation of these DNS names. That way, any
time you install an OpenSquiggly instance in your Kubernetes cluster, you
can simply specify the DNS name you'd like to use, and the system will create
an associated DNS record on your behalf.

To do this on Kubernetes, we need to install ExternalDNS on your cluster.

## Overview Videos

### The missing piece - Kubernetes ExternalDNS by Lachlan Evenson
<iframe
  width="1024"
  height="800"
  src="https://www.youtube.com/embed/9HQ2XgL9YVI"
  frameborder="0"
  webkitallowfullscreen
  mozallowfullscreen
  allowfullscreen>
</iframe>

<div>
  <ul>
    <li><a href="https://www.youtube.com/watch?v=9HQ2XgL9YVI" target="_blank">Open Video in YouTube</a></li>
  <ul>
</div>

### External DNS for Kubernetes by Houssem Dellai
<iframe
  width="1024"
  height="800"
  src="https://www.youtube.com/embed/VSn6DPKIhM8"
  frameborder="0"
  webkitallowfullscreen
  mozallowfullscreen
  allowfullscreen>
</iframe>

<div>
  <ul>
    <li><a href="https://www.youtube.com/watch?v=VSn6DPKIhM8" target="_blank">Open Video in YouTube</a></li>
  <ul>
</div>

## Installing ExternalDNS

### Steps to Complete

TODO