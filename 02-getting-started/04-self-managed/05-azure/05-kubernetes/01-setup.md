order: 1
title: Installing on Kubernetes
---
# Status
For large teams, a deployment using a Kubernetes cluster is the preferred choice to
achieve high-availability and high scalability. Kubernetes is the de facto standard
cloud deployment option that has wide industry acceptance and knowledge.

That is why our engineering team is working hard to provide a Kubernetes deployment
option for larger teams. We're also working diligently on performance and load testing
to provide sound recommendations to teams based on the size of their team and the number
and size of their Git repositories.

It should be noted, however, that Kubernetes is not always needed to support the team,
and even a team of a few dozen, or perhaps a few hundred users can be easily accommodated
by a single-node deployment.

The primary bottleneck to focus on initially is disk size and disk performance. Because
OpenSquiggly clones Git repositories and frequently pulls updates from Git, it is important
to have high performance disk storage attached to your OpenSquiggly nodes, and that the
disk space be big enough to store the repositories you expect to attach to OpenSquiggly.

After you've addressed disk space concerns, then you can decide whether the compute 
performance of your node is sufficient to handle the volume of traffic from users. Here
again, don't discount the ability of a single node to handle the needs of your team. You
can scale up the capacity of a single node by choosing a bigger virtual machine instance,
or in the case of Azure and Amazon, you can scale up your App Service or Beanstalk
instances.

If you still need additional performance after addressing disk space and node size, or
if you need the high-availability features that Kubernetes provides, then you should
consider migrating your instance to Kubernetes when it is available.

For questions related to Kubernetes deployments, or high-scalability deployments in general,
please contact us at support@opensquiggly.com to discuss your specific needs.
