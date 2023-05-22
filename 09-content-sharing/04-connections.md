---
Order: 4
Title: Managing External Connections
---
# Overview of External Connections

As discussed in the chapters "Mounting Source Code Repositories" and "Mounting
Documentation Repositories", an external connection is used to store the credentials
needed to clone a private repository in a Git repository, namely, Azure DevOps, Bitbucket,
GitHub, or GitLab.

A connection credential can be one of two types: a personal access token / password, or
an OAuth-issued token obtained by following the OAuth handshaking workflow.

External connections for an organization are managed the same was an external connections
for a personal account. The only thing that is different is that the owner of the external
connection is an organization account instead of an individual account.

# Adding External Connections to an Organization

While logged into a personal account to which you have administrative privileges on an
organization, open the User Options form and expand the Organizations accordion.

In the organizations table, click the "Managed External Connections" button in the row
corresponding to the desired organization.

A list of existing external connections will be displayed.

Next, click the Add New button to open the form for adding a new connection.

Select the desired connection type and fill in the form with the appropriate fields. Select
the desired credential type. For personal access tokens, enter the access token you want to
use. For OAuth connections, click the Authorize button and follow the instructions for granting
access to your repository.

For more information on the fields used by the external connection type, see the section
"Connecting to Private Repositories" in the chapter "Mounting Source Code Repositories".

When finished, click the Save button to add and save the external connection.

# Editing External Connections

To edit an external connection, click the Edit button on the row corresponding to the desired
External Connection in the connections list.

Enter the desired changes into the form and click Save.

# Deleting External Connections

To delete an external connection, you should first remove any mount points that use that
external connection. Then, click the Delete button on the row corresponding to the external
connection you wish to delete.
