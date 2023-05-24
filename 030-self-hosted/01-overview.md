---
order: 1
title: Overview
---
# Self-Managed Private Portals

For those organizations that need full control over their computing servers and network resources, either
for security or cost reasons, we offer self-managed private portals.

A self-managed private portal works almost exactly the same as a cloud hosted private portal, except you
install the software yourself on your own resources, either in your own self-managed cloud portal such as
Amazon AWS, Microsoft Azure, Google Cloud, Digital Ocean, Linode, or on your own physical servers manged
by your organization on a private corporate network.

# Deployment Options

We currently offer setup scripts, documentation, and walk-through videos for installing OpenSquiggly
onto a virtual machine in the five popular cloud providers listed above. Within this virtual machine
our setup script installs MongoDB (the database engine), ElasticSearch (the document search indexing
engine), and the OpenSquiggly service itself.

While this is a single-node solution, it can still scale to meet the needs of your team by adjusting
the size of the VM in your cloud provider, and by providing the VM with an adequate amount of disk
space. In our experience, this setup should scale to support all but the largest teams.

We are also working on multi-node options and plan to offer Kubernetes support in the future for
those that need the ultimate in high-availability and high-scalability.

# Considerations

When sizing your deployment, the main considerations should be:

* Choosing a VM size with enough CPU bandwidth and memory
* Choosing an amount high-speed disk space needed to store the amount of repos you plan to ingest
