---
Order: 5
Title: Managing Mount Points
---
# Overview of Mount Points

As discussed in the chapters "Mounting Source Code Repositories" and "Mounting
Documentation Repositories", a mount point is used to attach to an external
Git repository, either public or private, and make that content available for
grafting into your document tree.

Mount points for an organization are managed the same was as mount points
for a personal account. The only thing that is different is that the owner of the mount
point is an organization account instead of an individual account.

# Adding Mount Points to an Organization

While logged into a personal account to which you have administrative privileges on an
organization, open the User Options form and expand the Organizations accordion.

In the organizations table, click the "Managed Mount Points" button in the row
corresponding to the desired organization.

A list of existing mount points will be displayed.

Next, click the Add New button to open the form for adding a new mount point.

Select the desired Git Access Type along the External Connection for if using a private
repository,a nd fill in the form with the appropriate fields.

For more information on the fields used by the mount point type, see the chapters
"Mounting Source Code Repositories" and "Mounting Documentation Repositories".

When finished, click the Save button to add and save the external connection.

# Editing Mount Points

To edit a mount point, click the Edit button on the row corresponding to the desired
Mount Point in the connections list.

Enter the desired changes into the form and click Save.

# Deleting Mount Points

To delete a mount point, it is recommended (though not required) that you first remove any
documents in your document tree that reference the mount point. Then, click the Delete button
on the row corresponding to the mount point you wish to delete.

If you do happen to have any remaining pages in your document tree that references the deleted
mount point, they will now display a message indicating that the content is missing when you
try to view them in your navigator.
