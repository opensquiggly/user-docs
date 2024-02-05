---
weight: 30
url: /docs/k8s-guides/tls-certs
Order: 3
Title: Installing a TLS Certificate
description: >
  How to install TLS certificates that will allow you to expose
  your OpenSquiggly instance using https.
---

## Introduction

If you want to expose your OpenSquiggly instance via https instead of
just http, then you need to obtain a TLS certificate and give your 
Kubernetes cluster access to it.

## Options

There are three basic methods of obtaining a TLS certificate. 

* __Purchase__ - The traditional way is to purchase the certificate from a Certificate Authority (CA) or
one of its market partners.
* __Self-Signed__ - You can also generate a self-signed certificate instead of using a CA. However,
  we don't recommend using self-signed certificates because they generate user warnings in the
  browser. They should only be used for development and testing purposes. For this reason, we won't cover
  the usage of self-signed certificates in this chapter.
* __Free Auto-Generated__ - The final option is to use <a href="https://letsencrypt.org" target="_blank">Let's Encrypt</a>
  to automatically obtain and install free TLS certificates. Let's Encrypt certificates don't generate browser
  warnings the way self-signed certificates do, however, some users my perceive them as less trustworthy because
  they do don't come from a CA that audits the certificate receivers. It takes more work to set up the Let's Encrypt
  certificate generation process, but the effort can be worth it both for cost savings and auto-regeneration. We
  won't cover the topic further here in this chapter. For now, we leave it as an exercise to the reader.
  
In this chapter we assume you have purchased a certificate and wish to use it in conjunction with your
Kubernetes cluster and OpenSquiggly instance.

## Purchasing a Certificate

Major cloud providers such as Amazon, Azure, and Google offer TLS certificates
directly through their portals (for a fee of course). This gives the customer
the convenience of paying for the certificate through their normal cloud
billing cycle.

There are also numerous other places on the web where you can purchase a 
certificate.

## Installing the Certificate as a Secret on Kubernetes

The easiest way to link your Kubernetes cluster to your certificate is to install
it as a Kubernetes secret. In Kubernetes, "secrets" are a means of storing sensitive
parameters that can be used by other resources.

Once you've purchased and downloaded the certificate, install it as follows:

```bash
kubectl create secret tls name-of-secret-here --key="your-key-file-here" --cert="your-cert-file-here"
```

Example

```bash
kubectl create secret tls mycertsecret --key="mycert.rsa" --cert="mycert.crt"
```

To verify the secret was successfully installed, do:

```bash
kubectl get secrets
```

## Using the Secret When Installing OpenSquiggly

To use the TLS certificate and simultaneously expose the OpenSquiggly instance with
https support, add the following parameters to your helm install command:

* tlsSecretName="secret-name-here"
* exposeWith=nginx   <---- This is your ingress class name. See 
  [here for details](/docs/k8s-guides/nginx).
* dnsHostName="your.company.com"

Example:

```bash
helm install opensquiggly-test1 opensquiggly/allinone --set \
  cloudType=azure,diskSize=30,exposeWith=nginx,tlsSecretName=mycertsecret,dnsHostName="opensquiggly-test1.yourcompany.com"
```

Assuming you followed the instructions for setting up ExternalDNS, OpenSquiggly should be installed and a
DNS name opensquiggly-test1.yourcompany.com will be automatically created on your DNS server. If you aren't
running ExternalDNS, you'll need to manually add the DNS name to your DNS name server.

## Updating an Existing Instance
If you've already installed OpenSquiggly as a basic installation without TLS and a custom domain name,
and wish to update the instance while leaving all other settings unchanged, you can use the ```helm upgrade```
command as follows:

```bash
helm upgrade opensquiggly-test1 opensquiggly/allinone --reuse-values --set \
  exposeWith=nginx,tlsSecretName=mycertsecret,dnsHostName="opensquiggly-test1.yourcompany.com"
```