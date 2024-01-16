---
weight: 30
url: /docs/k8s-guides/tls-certs
Order: 3
Title: Installing a TLS (SSL) Certificate
description: >
  How to install and use the ExternalDNS service to automatically
  create DNS names corresponding to your OpenSquiggly instance(s).
---

## Introduction

If you want to expose your OpenSquiggly instance via https instead of
just http, then we need to obtain an SSL certificate and give our 
Kubernetes cluster access to it.