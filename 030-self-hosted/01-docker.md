---
weight: 15
url: /docs/self-hosted/docker
order: 1
title: Installing With Docker
description: Information on using Docker to run OpenSquiggly
---
## Docker and OpenSquiggly
OpenSquiggly is delivered as a multi-container pod, and therefore cannot simply
be installed as a Docker image the way some users might be used to with other
Docker applications.

If you are looking for a fast and easy way to evaluate OpenSquiggly on your local
desktop, we recommend using one of the lightweight, desktop-installable Kubernetes
distributions on the market.

The OpenSquiggly Helm charts provide direct support for both Docker Desktop Kubernetes
and Minikube, both of which are documented in this chapter.

* <a href="/docs/self-hosted/k8s/docker-desktop">Docker Desktop Kubernetes Instructions</a>
* <a href="/docs/self-hosted/k8s/minikube">Minikube Instructions</a>