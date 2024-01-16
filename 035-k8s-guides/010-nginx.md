---
weight: 10
url: /docs/k8s-guides/nginx
Order: 1
Title: Custom Domain Names with NGINX
description: >
  How to install an NGINX ingress controller in your Kubernetes cluster
  so that you can configure you OpenSquiggly instance to use custom
  domain names.
---

## Introduction

In the quick setup guides give in the Self-Hosted chapter, we should you how
to expose your OpenSquiggly instance using a Load Balancer and a hard-coded IP
address.

We provided these instructions to give you a very fast way to configure OpenSquiggly
for a quick evaluation setup. However, if you decide you want to continue to use
OpenSquiggly for your team, you'll want to move away from hard-coded IP address
so that teams can access the instance via a bona fide DNS name.

In Kubernetes, the way to accomplish this is by installing an ingress controller.
The ingress controller provides a way to map an inbound domain name to your
Kubernetes service.

There are various ingress controllers available. The NGINX ingress controller is 
one of the most commonly used, and we discuss how to use it in this document.



## Install the NGINX Controller using Helm

There are multiple ways to install the NGINX ingress controller, but for the purposes
of these instructions, we're going to use a Helm chart. Consult your cloud engineering
team to see if an NGINX controller is already installed on your cluster, or if the team
prefers an alternate installation method.

### Steps to Complete
1. Ensure your ```kubectl``` and ```helm``` CLI programs are install using
   the instructions <a href="/docs/self-hosted/kubernetes/#installing-kubectl">here</a>.
2. Add the ingress-nginx repository to your helm repositories list with
   the command:
   ```bash
   helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
   ```
3. Verify that the ingress-nginx repository was successfully added with
   the command:
   ```bash
   helm repo list
   ```   
   which should show you a list of your current Helm repositories such as:
   ```bash
   NAME             URL                                       
   stable           https://charts.helm.sh/stable             
   bitnami          https://charts.bitnami.com/bitnami         
   ingress-nginx    https://kubernetes.github.io/ingress-nginx   <---- Newly added Helm repository
   opensquiggly     https://opensquiggly.github.io/helm-charts
   .
   .  (... etc ...)
   .   
   ```
4. Install the NGINX controller into your current Kubernetes context using the
   command:
   ```bash
   helm install ingress-nginx ingress-nginx/ingress-nginx --create-namespace --namespace ingress-nginx
   ``` 
5. Verify that the NGINX Helm chart successfully installed the NGINX ingress controller using the
   command:
   ```bash
   kubectl get all --namespace ingress-nginx
   ``` 
   This should give you a list of all the resouces that the Helm chart installed, such as:
   ```bash
   NAME                                           READY   STATUS    RESTARTS   AGE
   pod/ingress-nginx-controller-bfc454775-vsqmb   1/1     Running   0          40m

   NAME                                         TYPE           CLUSTER-IP     EXTERNAL-IP       PORT(S)                      AGE
   service/ingress-nginx-controller-admission   ClusterIP      10.43.123.52   <none>            443/TCP                      40m
   service/ingress-nginx-controller             LoadBalancer   10.43.103.33   131.153.226.147   80:30544/TCP,443:31551/TCP   40m

   NAME                                       READY   UP-TO-DATE   AVAILABLE   AGE
   deployment.apps/ingress-nginx-controller   1/1     1            1           40m

   NAME                                                 DESIRED   CURRENT   READY   AGE
   replicaset.apps/ingress-nginx-controller-bfc454775   1         1         1       40m
   ```
6. In the event that your cluster has multiple ingress controllers running in it, to see the
   list of available ingress class names, use the command:
   ```bash
   kubectl get ingressclass
   ```       
   which should display an output list such as:
   ```bash
   NAME    CONTROLLER             PARAMETERS   AGE
   nginx   k8s.io/ingress-nginx   <none>       29m
   -----
     ^
     |
     +------ This is the name you will use in later steps to expose the OpenSquiggly service
   ```
7. Assuming you installed the ingress controller into the suggested namespace "ingress-nginx", use
   the following command to determine the external IP address of the associated Load Balancer that
   is tied to the ingress controller.
   ```bash
   kubectl get service --namespace ingress-nginx
   ```   
   which should display an output such as:
   ```bash
   NAME                                 TYPE           CLUSTER-IP     EXTERNAL-IP       PORT(S)                      AGE
   ingress-nginx-controller-admission   ClusterIP      10.43.123.52   <none>            443/TCP                      34m
   ingress-nginx-controller             LoadBalancer   10.43.103.33   131.153.226.147   80:30544/TCP,443:31551/TCP   34m
   ```
   In the above example, we see the NGINX ingress controler is available on the external IP address "131.152.226.147".
   We can now create DNS names, either manually or automatically using ExternalDNS, and users should be able to
   access services on the cluster that are exposed via the ingress controller.

