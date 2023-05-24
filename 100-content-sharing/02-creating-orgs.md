---
Order: 2
Title: Creating Organizations
---
# Overview of Organizations

An "organization" is a special type of user within a given OpenSquiggly instance.

You cannot log in directly to an organization like you can with an ordinary user
account. Instead, you grant administrative privileges to one or more members of
the organization, and they can manage the connections, mount points, and groups
of the organization while logged in as their own account with their own login id.
In effect, they act on behalf of the organization, but never log in directly as
the organization.

# Creating a New Organization

While logged in as your own user account, click on the user name icon located in
the right hand side of the top OpenSquiggly header bar. This will open up the
User Options form.

Next, expand the "Manage Organizations" according. This will show you a list of
all organizations for which you are currently allowed to administer. If you are
not an administrator of any organization, the list is empty.

To create a new organization and make yourself the first administrator of it, click
the "Add New Organization" button.

Fill in the form as follows:

* Organization Id - The organization id must be unique within the OpenSquiggly instance,
  and can contain only lowercase letters, numbers, and dashes. The organization id is
  used to construct URLs for documents associated with the organization. The id is not
  normally displayed to the user, except in the browser's address bar, and in certain other
  administrative forms for which displaying the organization id is helpful.
* Organization Name - This is a human readable name for the organization as it will appear
  most of the time in forms and lists that are displayed to the user.

Press the Save button to create the organization.

Next, you'll want to add existing OpenSquiggly users as members of the organization. These
operations are discussed in the next section, "Managing Organization Members".

# Deleting Organizations

To delete an organization, click the "Delete" button in the row corresponding to the
organization you wish to delete.

Note there is a known bug with deleting organizations. The Delete button may appear 
disabled.
