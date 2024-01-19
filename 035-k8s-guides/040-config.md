---
weight: 40
url: /docs/k8s-guides/config
Order: 4
Title: Managing Configuration Settings
description: >
  Here we show you how to set configuration settings to control your
  OpenSquiggly instance, such as setting the database connection URL.
---

## Introduction

The opensquiggly/allinone Helm chart does not require any configuration settings.
This is because the chart installs all the resources it needs to run in a fully
self-contained pod. The database configuration settings and all other controllable
application settings default to appropriate values.

However, in some cases, you may want to change the default application configuration
settings.

The primary reason why you'd want to do this is if you want to run the MongoDB database
separately from your OpenSquiggly pod. In that case, you need to set the connection
string and the database name to point to the location where the MongoDB server is running.

If you're running on the Microsoft Azure cloud, OpenSquiggly provides a setting that lets
you connect to an Azure App Configuration resource. In this case, you can locate all of
your configuration settings separately from your Kubernetes cluster, and then reference the
location of the App Configuration vault using a single value. It can be easier to manage
your Kubernetes environment if you can offload configuration data to a separate place.

In the future we'll be adding support for other configuration sources, such as Hashicorp
Vault, AWS Secrets Manager, Azure Key Vault, and others.

## Basic Configuration Settings

<table>
  <tr>
    <th>Setting Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>ConnectionStrings__AppConfig</code></td>
    <td>
      For Azure deployments only, this value contains a resource locator that references
      an Azure App Configuration vault. Note that additional configuration within Azure
      is needed to link your Kubernetes cluster with your App Configuration.
    </td>
  <tr>
    <td><code>DatabaseOptions__ConnectionString</code></td>
    <td>
      A resource locator provided by your MongoDB host that allows you to establish
      a connection with the database.
    </td>
  </tr>
  <tr>
    <td><code>DatabaseOptions__DatabaseName</code></td>
    <td>
      The name of the database. Note that multiple databases with different names can
      exist within the same database server referenced by the connection string.
    </td>
</table>

The separator character between the "DatabaseOptions" component and the second component
("ConnectionString" or "DatabaseName") is two underscores.

## Storing the Configuration in a Kubernetes Secret

Use the ```kubectl``` command to create a multi-value secret in your Kubernetes cluster.

Example:

```bash
kubectl create secret config-settings \
  --from-literal=DatabaseOptions__ConnectionString="YourDatabaseConnectionStringHere" \
  --from-literal=DatabaseOptions__DatabaseName="OpenSquigglyTestDb1"
```

## Using the Secrets in the Helm Chart

Use the Helm chart value "configSecretName" to reference the secret you created in the
previous step.

Example:

```bash
helm install opensquiggly-test2 --set cloudType=azure,diskSize=50,configSecretName=config-settings
```