---
weight: 130
url: /docs/self-hosted/k8s/google
order: 13
draft: false
Title: "Kubernetes : Google"
description: How to install OpenSquiggly on Google Kubernetes Engine (GKE).
---
## Overview of Installing on GKE

Google Kubernetes Engine, or GKE for short, is Google Cloud's managed Kubernetes service.
Setting up GKE is somewhat complex due to all the configuration options that Google offers.
However, they at least provide sane defaults for most of the settings. You can create a new
cluster with as little as a name and a region.

## Part 1 : Installing Prerequisites

* Install the ```kubectl``` and ```helm``` tools using the instructions <a href="/docs/self-hosted/kubernetes/#installing-kubectl">here</a>.
* Install the ```gcloud``` CLI tool from Google using the instructions <a href="https://cloud.google.com/sdk/docs/install" target="_blank">here</a>.
* Verify that ```gcloud``` is installed using the command:
  ```bash
  gcloud --version
  ```
* If not already installed, install the ```gke-gcloud-auth-plugin``` using the command:
  ```bash
  gcloud components install gke-gcloud-auth-plugin
  ```
* Verify that the ```gke-gcloud-auth-plugin``` is installed using the command:
  ```bash
  gke-cloud-auth-plugin --version
  ```
* Add the OpenSquiggly Helm chart repository to your list of Helm repositories:
  ```bash
  helm repo add opensquiggly https://opensquiggly.github.io/helm-charts
  ```

## Part 2 : Creating the GKE Cluster

### Steps to Complete

1. Visit your Google cloud console at <a href="https://console.cloud.google.com" target="_blank">console.cloud.google.com</a> 
   and login to your Google account.
2. Select Kubernetes Engine from the Quick Access list, or search for "Kubernetes" in the search box at the top
   and select it from the list.
3. Navigate to the "Clusters" section and click the "Create" button to start the process to create a new cluster.
4. Choose between an Auto Pilot cluster or Standard cluster.
   * The default option is Auto Pilot
   * To switch to a Standard cluster, click on the "Switch to Standard Cluster" in the upper-right portion
     of the header bar at the top.
   * Choose Auto Pilot cluster if you want the system to manage and auto-scale your node pools and other resources.
     The benefit of Auto Pilot is it can save costs by not over-allocating unneeded resources.
   * Choose Standard cluster if you want precise control over your cluster resources, and want to manage your
     node pools and compute resources yourself. The benefit of a Standard cluster is increased control, at the
     risk of possibly overpaying for over-allocated or unused resources.    
4. Under the "Cluster basics" section, enter the desired name of the cluster and select the region.
5. To set advanced options, navigate to the Networking, Advanced settings, and Fleet sections and select
   the desired options.
6. When you've finished reviewing all of your options, navigate to the "Review and create" section and
   click the "Create Cluster" button.

## Part 3 : Connecting kubectl to the GKE Cluster

### Steps to Complete

1. Retrieve the cluster connection credentials, which will add the connection information to your default
   KUBECONFIG file, with the command:
   ```bash
   gcloud container clusters get-credentials cluster-name-here --region=region-here --project=project-id-here
   ```
2. Verify the the cluster has been added to your list of contexts and is your current context using the command:
   ```bash
   kubectl config get-contexts
   ```   

## Part 4 : Install OpenSquiggly with the Helm Chart

Use the ```helm``` tool to install the OpenSquiggly Helm chart into the cluster:

```bash
helm install release-name-here opensquiggly/allinone --set cloudType=google[,diskSize=xx]
```

where ```xx``` is the desired disk size in gigabytes. The default is 32Gb if omitted.

Example:

```bash
helm install opensquiggly1 opensquiggly/allinone --set cloudType=google,50
```

The above command will create a Helm release named ```opensquiggly1``` with a 50Gb persistent volume.

## Part 5 : Testing the Install

Ensure that the pod has started by issuing the command:

```bash
kubectl get pods [--watch]
```

Note that is may take a minute or two for the persistent volume claim to be provisioned,
and the pod won't be able to install until it is completed. Be patient. We've noticed in our
testing the PVCs take longer to provision on Auto Pilot than on the Standard cluster.

When the pod is running, retrieve the load balancer IP address with:

```bash
kubectl get svc
```

Hit the IP address with your browser and that should take you to the OpenSquiggly login screen.

## End-to-End Video Demo

<iframe width="1024" height="795" src="https://www.youtube.com/embed/7qy7lyOWuCc" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

<div>
  <ul>
    <li><a href="https://www.youtube.com/watch?v=7qy7lyOWuCc" target="_blank">Open Video in YouTube</a></li>
  <ul>
</div>