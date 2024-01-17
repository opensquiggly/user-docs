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

This is not very convenient for OpenSquiggly users, as they would need
to know the IP address in order to access the system. We need to create a 
custom DNS name that users can use instead of a fixed IP address.

While you can always manually create DNS names in your DNS server, its much
more convenient to automate the creation of these DNS names. That way, any
time you install an OpenSquiggly instance in your Kubernetes cluster, you
can simply specify the DNS host name you'd like to use, and the system will 
create an associated DNS record on your behalf.

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

To install ExternalDNS on your cluster, you'll need to follow the specific steps for your
DNS name server provider. Each provider is a little different. In each case, you need to
retrieve some kind of connection credential that will allow the ExternalDNS service running
on your Kubernetes cluster to create DNS records on the DNS name server.

A full list of tutorials can be found <a href="https://github.com/kubernetes-sigs/external-dns/tree/master/docs/tutorials" target="_blank">here</a>.

Here is a partial list of some of the more commonly used DNS name server providers. Note that the cloud provider that provides your DNS name server
doesn't necessarily need to be the same cloud provider as that provides your Kubernetes cluster. For example, you can create a Kubernetes
cluster on Linode and let the DNS names be managed by Azure. Be sure to read the instructions corresponding to the cloud service that provides
your DNS server, not your Kubernetes cluster.

<table>
  <tr>
    <th>Name</th>
    <th>Tutorial Link</th>
  </tr>
  <tr>
    <td>AWS</td>
    <td><a href="https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/aws.md" target="_blank">https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/aws.md</a></td>
  </tr>
  <tr>
    <td>Azure</td>
    <td><a href="https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/azure.md" target="_blank">https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/azure.md</a></td>
  </tr>  
  <tr>
    <td>Civo</td>
    <td><a href="https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/civo.md" target="_blank">https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/civo.md</a></td>
  </tr>    
  <tr>
    <td>CloudFlare</td>
    <td><a href="https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/cloudflare.md" target="_blank">https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/cloudflare.md</a></td>
  </tr>   
  <tr>
    <td>DigitalOcean</td>
    <td><a href="https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/digitalocean.md" target="_blank">https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/digitalocean.md</a></td>
  </tr> 
  <tr>
    <td>GoDaddy</td>
    <td><a href="https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/godaddy.md" target="_blank">https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/godaddy.md</a></td>
  </tr>   
  <tr>
    <td>Google</td>
    <td><a href="https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/gke.md" target="_blank">https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/gke.md</a></td>
  </tr> 
  <tr>
    <td>Linode</td>
    <td><a href="https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/linode.md" target="_blank">https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/linode.md</a></td>
  </tr>          
</table>  