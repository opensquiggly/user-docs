---
Order: 7
weight: 70
Title: Granting Permissions to Members
description: How to grant permissions to members of a group.
---
## About Access Control Lists

Each group you've created as an associated "access control list", where each entry
in the access control list grants a permission to a mount point. You can have as many
entries in the access control list as needed.

## Granting a Permission to a Group

While logged into a personal account to which you have administrative privileges on an
organization, open the User Options form and expand the Organizations accordion.

In the organizations table, click the "Managed Groups" button in the row
corresponding to the desired organization.

A list of existing groups will be displayed.

In the row corresponding to the group you wish to grant permissions, click the "Manage
Group Permissions" button.

This will open up a list showing all the current entries in that group's access control
list.

To grant a new permission, click the "Grant Permissions to Mount Point" button.

Pick the desired mount point from the drop down list and select any or all of the
three permissions you wish to grant:

* Read - Allows the user to graft the mount point into their document tree and view
  the documents and files in the mount point
* Refresh - Allows the user to refresh the mount point. Refreshing a mount point will
  update the content from the Git repository by issuing a "git fetch" command.
* Search - Makes the mount point available in the search results from the user's account

When finished, click the Save button to add the new entry to the access control list.

## Editing an Existing Permission

To modify an existing permission, click the Edit button in the row corresponding to the
access control list entry you wish to modify.

Change the permissions as desired and click the Save button to save the changes.

## Removing a Permission

To remove a permission, click the Remove button in the row corresponding to the access
control list entry you wish to remove.
