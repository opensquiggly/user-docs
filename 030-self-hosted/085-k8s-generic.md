---
weight: 85
url: /docs/self-hosted/k8s/generic
order: 9
Title: "Kubernetes : Generic"
description: How to install OpenSquiggly on any Kubernetes service.
---
## Overview of Installing on a Generic Kubernetes Engine

Although we've written specific installation instructions for some of the most
commonly used Kubernetes engines on the market, OpenSquiggly can be installed on
any Kubernetes system of your choice. You just need to specify the appropriate
values when installing the Helm chart to control the various resources that the
Helm chart creates.

If you're installing on a supported cloud provider, you can skip this section and
go to the section for your target cloud provider.

In this section we'll walk you through the process of installing OpenSquiggly on
an unlisted Kubernetes system.

## Parameter Simplification
A primary goal of our Helm charts is to simplify and minimize the number of settings you
need to specify to get OpenSquiggly running. Though we have quite a few potential settings
you can use, we hope that you don't need to read and understand the entire list of settings
to get a basic instance running.

Toward that end, we have the ```cloudType``` setting that provides appropriate default
values for that particular flavor of Kubernetes. For any specific cloudType, you can always
replicate an equivalent configuration using ```cloudType=other``` and specifying additional
parameters.

<table>
  <tr>
    <th>cloudType Value</th>
    <th>Equivalent To</th>
  </tr>
  <tr>
    <td><code>cloudType=aws</code></td>
    <td><code>cloudType=other,storageProvisioner=ebs.csi.aws.com</code></td>    
  </tr>
  <tr>
    <td><code>cloudType=azure</code></td>
    <td><code>cloudType=other,storageProvisioner=disk.csi.azure.com,diskSkuName=LRS_Premium</code></td>    
  </tr>
  <tr>
    <td><code>cloudType=digitalocean</code></td>
    <td><code>cloudType=other,storageProvisioner=dobs.csi.digitalocean.com</code></td>    
  </tr>
  <tr>
    <td><code>cloudType=docker-desktop</code></td>
    <td><code>cloudType=other,storageProvisioner=docker.io/hostpath</code></td>    
  </tr>
  <tr>
    <td><code>cloudType=google</code></td>
    <td><code>cloudType=other,storageProvisioner=pd.csi.storage.gke.io,diskType=pd-ssd</code></td>    
  </tr>
  <tr>
    <td><code>cloudType=linode</code></td>
    <td><code>cloudType=other,storageProvisioner=linodebs.csi.linode.com</code></td>    
  </tr>
  <tr>
    <td><code>cloudType=minikube</code></td>
    <td><code>cloudType=other,storageProvisioner=hostpath.csi.k8s.io</code> (assumes the <a href="https://minikube.sigs.k8s.io/docs/tutorials/volume_snapshots_and_csi/" target="_blank">Host Path CSI driver</a> addon has been installed)</td>    
  </tr>            
</table>     

As you can see from the above table, using an unlisted flavor of Kubernetes is simply a matter of
determining which ```storageProvisioner``` the Kubernetes engine provides, along with any customized
disk parameters (the ```diskSkuName``` and ```diskType```).

## Persistent Volumes, Claims, & Storage Classes

OpenSquiggly needs a persistent volume (PV), which it gets by asking a persistent volume claim (PVC) to
give it one. A PVC can be configured to dynamically provision a new PV on request, or it can be configured
to serve up an already existing PV.

If the PVC is going to dynamically provision a new PV, then it needs to know needs to know what StorageClass 
class it should use, and the StorageClass in turn needs to know what Storage Provisioner it should use. Our
Helm chart provides switches that can control what resources are needed depending on what you want.

In the following table, we assume you are using Helm to install an OpenSquiggly release named ```releasename```
such as with the following command:

```bash
helm install releasename opensquiggly/allinone --set cloudType=other,...other parameters to set go here as shown below...
```

<table>
  <tr>
    <th>What You Want</th>
    <th>How to Get It</th>
    <th>What Happens</th>
  </tr>
  <tr>
    <td>Use an already existing PV named <code>xyz</code></td>
    <td><code>useExistingPv=xyz,diskSize=xxx</code></td>
    <td>
      Creates a new PVC named <code>releasename-pvc</code> that serves the existing PV named <code>xyz</code>.
      You must specify a disk size that is equal to or smaller than the PV you are 
      trying to reuse. Also, the PV you are trying to use must be in the <code>Available</code> state.
    </td>
  </tr>
  <tr>
    <td>Get a PV from an already existing PVC named <code>xyz</code></td>
    <td><code>useExistingPvc=xyz</code></td>
    <td>
      The <code>opensquiggly</code> container in the deployment created by the Helm chart 
      will reference the PVC named <code>xyz</code>. The PVC will either create a new PV or
      serve up an existing PV depending on how it is configured. The size of the PV will
      also depend on how the PVC is configured. The <code>diskSize</code> setting, if specified, 
      is ignored.
    </td>
  </tr>  
  <tr>
    <td>Dynamically provision a 40Gb PV using an existing storage class named <code>xyz</code></td>
    <td><code>diskSize=40,useExistingStorageClass=xyz</code></td>
    <td>
      Dynamically creates a PV with a name assigned by Kubernetes, and a PVC named <code>releasename-pvc</code> 
      but does not create a storage class.<br><br>
      Note that most default storage classes in Kubernetes have a ReclaimPolicy set to <code>Delete</code>. 
      This means if you uninstall the Helm chart, the PV will be automatically deleted and
      you will lose your data if you don't have a backup. Be careful about using existing storage classes
      to ensure you get the behavior you want.
    </td>
  </tr>
  <tr>
    <td>
      Dynamically provision a 50Gb PV that will not be deleted automatically when the release is
      uninstalled (<code>ReclaimPolicy = Retain</code>)
    </td>
    <td><code>diskSize=50,storageProvisioner=xyz</td>
    <td>
      A new StorageClass is created which uses the specified storage provisioner, with the StorageClass's
      <code>ReclaimPolicy</code> set to <code>Retain</code>.<br><br>
      Note that additional parameters in the StorageClass may be needed to control what type of disk
      to use. For example, some cloud providers allow you to choose between a regulard hard drive vs.
      a higher performance SSD drive (which costs extra, of course).<br><br>
      We recommend using high speed SSD drives when possible.<br><br>
      For SSD drives on Azure, add the setting <code>diskSkuName=LRS_Premium</code><br>
      For SSD drives on Google, add the setting <code>diskType=pd-ssd</code><br><br>
      If your cloud provider requires additional parameters in the StorageClass, then you'll need
      to create the StorageClass yourself and then use it with the <code>useExistingStorageClass</code>
      setting.
    </td>
  </tr>    
</table>

## Creating a Custom Storage Class

There are limits to OpenSquiggly's Helm charts for creating storage classes. They don't have the ability to
apply custom annotations or to apply any other parameters to the StorageClass except ```skuname``` and ```type```.

In this case, you can always create the StorageClass yourself using a custom manifest file, and then pass
the name of the StorageClass to the Helm chart using the ```useExistingStorageClass``` parameter.

Here is a template for creating a StorageClass:

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
allowVolumeExpansion: true
metadata:
  labels:
    addonmanager.kubernetes.io/mode: EnsureExists
    kubernetes.io/cluster-service: "true"
  name: your-storageclass-name-here
parameters:
  skuname:   # For Azure SSD, enter Premium_LRS
  type:      # For Google SSD, enter pd-ssd
provisioner: storageprovisioner-name-here
reclaimPolicy: Retain    # Enter Retain or Delete (Retain recommended)
volumeBindingMode: WaitForFirstConsumer
```

Save the above template to ```filename.yaml```, fill in the parameters as appropriate, and run the command:

```bash
kubectl apply -f filename.yaml
```

We always recommend using a ```reclaimPolicy``` of ```Retain``` to prevent accidental deletion of your 
data in the event you uninstall the Helm chart.

## List of All Helm Chart Values

<table>
  <tr>
    <th>Value Name</th>
    <th>Default Value</th>
    <th>Allowed Values</th>
    <th>Description</th>
  </tr>
  <tr>
    <td colspan="4" style="background-color: darkgray; font-weight: bold;">Basic Settings</td>
  </tr>
  <tr>
    <td><code>cloudType</code></td>
    <td>other</td>
    <td>
      aws<br>
      azure<br>
      digitalocean<br>
      docker&#8209;desktop<br>
      google<br>
      linode<br>
      minikube<br>
      other
    </td>
    <td>
      Enter the cloud provider type or choose other for a generic system.
      If you enter 'other', then you must also enter a value for storageProvisioner,
      or specify one of useExistingPv, useExistingPvc, or useExistingStorageClass.      
    </td>
  </tr> 
  <tr>
    <td><code>diskSize</code></td>
    <td>32</td>
    <td>An integer, in gigabytes (example: 32 means 32Gb)</td>
    <td>
      The size of the persistent volume you wish to create, in gigabytes. The persistent
      volume should be large enough to store your internally authored pages, cloned
      repos (for your mount points), logs, and indexes. 
    </td>
  </tr>  
  <tr>
    <td colspan="4" style="background-color: darkgray; font-weight: bold;">Core Storage-Related Settings</td>
  </tr>  
  <tr>
    <td><code>storageProvisioner</code></td>
    <td>Empty</td>
    <td>Any String</td>
    <td>
      If you want the storage class created by the Helm chart to use a specific storage
      provisioner supplied by your cloud provider, enter the name of the storage provisioner
      here. We recommend using the highest performing storage provisioner that your cloud
      provider allows, but if you need to choose a specific provisioner, enter it here.
      This option is only valid if useExistingPv, useExistingPvc and useExistingStorageClass
      are all empty. Consult the opensquiggly.com documentation for additional information
      on each cloud type and the available provisioners.    
    </td>
  </tr> 
  <tr>
    <td><code>useExistingPv</code></td>
    <td>Empty</td>
    <td>Any String</td>
    <td>
      If you don't want the Helm chart to create a persistent volume, and instead
      use an existing persistent volume, enter the persistent volume name here    
    </td>
  </tr>
  <tr>
    <td><code>useExistingPvc</code></td>
    <td>Empty</td>
    <td>Any String</td>
    <td>
      If you don't want the Helm chart to create a persistent volume claim, and instead
      use an existing persistent volume claim, enter the PVC claim name here. This
      option is only valid if useExistingPv is empty.    
    </td>
  </tr>  
  <tr>
    <td><code>useExistingStorageClass</code></td>
    <td>Empty</td>
    <td>Any String</td>
    <td>
      If you don't want the Helm chart to create a storage class, and instead use
      an existing storage class, enter the storage class name in useExistingStorageClass.
      This option is only valid if BOTH useExistingPv and useExistingPvc are empty.    
    </td>
  </tr> 
  <tr>
    <td colspan="4" style="background-color: darkgray; font-weight: bold;">Advanced Storage-Related Settings</td>
  </tr>    
  <tr>
    <td><code>diskSkuName</code></td>
    <td>Empty</td>
    <td>Any String</td>
    <td>
      <code>parameters:</code><br>
      <code>&nbsp;&nbsp;skuname: value-here</code>
    </td>
  </tr>   
  <tr>
    <td><code>diskType</code></td>
    <td>Empty</td>
    <td>Any String</td>
    <td>
    </td>
  </tr>    
  <tr>
    <td><code>azureSkuName</code></td>
    <td>LRS_Premium</td>
    <td>Any String</td>
    <td>
      For Azure cloud type only, this variable supplies the Azure skuname you wish
      to use for your storage class and associated persistent volume claim. By default
      we select the highest performance option.    
    </td>
  </tr> 
  <tr>
    <td><code>googleDiskType</code></td>
    <td>pd-ssd</td>
    <td>Any String</td>
    <td>
      For Google cloud type only, this variable supplies the Google disk type you wish
      to use for your storage class and associated persistent volume claim. By default
      we select the highest performance option.    
    </td>
  </tr> 
  <tr>
    <td colspan="4" style="background-color: darkgray; font-weight: bold;">HTTP/HTTPS, Ingress, and DNS-Related Settings</td>
  </tr>    
  <tr>
    <td><code>exposeWith</code></td>
    <td>LoadBalancer</td>
    <td>
      LoadBalancer or
      An available Ingress class name
      such as 'nginx'
    </td>
    <td>
      How would you like the OpenSquiggly web service exposed to the outside world?
      Enter 'LoadBalancer' to use a standard load balancer service, or 'nginx' to use
      an Nginx-powered ingress controller. Note that using an ingress controller may 
      require additional configuration depending on your cloud provider.    
    </td>
  </tr> 
  <tr>
    <td><code>dnsHostName</code></td>
    <td></td>
    <td>
    </td>
    <td>
      To use OpenSquiggly with a custom DNS name, enter the desired DNS name here.
      This option is only valid when exposeWith is set to nginx.    
    </td>
  </tr>     
  <tr>
    <td><code>tlsSecretName</code></td>
    <td></td>
    <td>
    </td>
    <td>
      To use OpenSquiggly with HTTPS, upload your TLS certificate as a Kubernetes secret,
      then enter the name of the secret that stores the certificate here. This option is
      only valid when exposeWith is set to nginx. Consult the documentation at opensquiggly.com
      for additional information on installing OpenSquiggly with HTTPS.    
    </td>
  </tr>   
  <tr>
    <td colspan="4" style="background-color: darkgray; font-weight: bold;">Application Configuration</td>
  </tr>    
  <tr>
    <td><code>configSecretName</code></td>
    <td></td>
    <td>
    </td>
    <td>
      The Kubernetes secret name containing configuration values for the OpenSquiggly
      application.
    </td>
  </tr> 
  <tr>
    <td><code>esMinHeapSize</code></td>
    <td></td>
    <td>
    </td>
    <td>
      Specify the initial (mininum) ElasticSearch heap size, depending on the size of 
      the nodes in your cluster. Heap size should be no larger that 50% of available 
      memory of the node. Use the "m" suffix for megabytes and the "g" suffix for 
      gigabytes.    
    </td>
  </tr>   
  <tr>
    <td><code>esMaxHeapSize</code></td>
    <td></td>
    <td>
    </td>
    <td>
      Specify the maximum ElasticSearch heap size.    
    </td>
  </tr>     
</table>  
