---
Order: 1
Title: Repo Types & Formats
---
# Introduction to Mounting External Content
A big feature of OpenSquiggly is the ability to bring in content, namely source code files
and documentation from external Git repositories. Our aim is to provide a flexible, lightweight
process tool that puts you in control of how you want to arrange and format your content. OpenSquiggly
provides you with a document access tool, stopping short of imposing any particular workflows on you.

To mount repositories, open up your User Options panel by clicking on your login id in the upper
right corner of the screen, then expand the "Mount Points" accordion in the form.

From here you can attach to external content by mounting them (the term "mount" derives from the
terminology used in UNIX-based operating systems to graft network mounted drives into your file
system).

You can connect to either public or private repositories.

Public repositories are repositories that are open to the world and do not require any authentication
credentials to access. This is covered in the next section, "Connecting to Public Repositories".

Private repositories work similarly, except one extra step is need to create an "external connection"
record which stores the credentials. See the section, "Mounting Private Repositories" for more details
on external connections and private repositories.

After you've mounted a repository, the content is available to be grafted into your document tree,
but it is not placed in your document tree immediately (unless you used the Quick Add feature). To
learn how to add mounted content to your document tree, see Chapter 6, "Managing and Navigating
Your Document Tree".

# Source Code vs. Documentation Repositories

The main difference between mounting source code repositories, as discussed in this chapter, and
documentation repositories, as discussed in the next chapter, is the specification of the mount
point's *tree type*, which controls how the content is filtered and formatted.

OpenSquiggly currently offers two tree types:

* Raw Files and Folder Names (which we'll call *raw* tree type for brevity)
* OpenSquiggly Simplified Document Tree Formatter (which we'll call *doc* tree type for brevity)

The raw tree type is the most appropriate tree type to use when you want to mount a repository
containing source code, or any time you want the system to display the actual contents of each
file, instead of displaying formatted content.

With the raw tree type, all files and folders present in the repository are displayed in the document
tree within OpenSquiggly. In other words, OpenSquiggly is presenting you with an unfiltered, unformatted
view of the contents of the repository you are mounting. That is why we call it the "raw" tree type, and
since presumably when you are viewing your source code files you want to see all your files, this is
the tree type you'll want to use.

For the remainder of this chapter we'll recommend that you select the raw tree type, and we'll assume
you've done so.

In the next chapter we'll discuss the usage of the second tree type, the OpenSquiggly Simplified Document
Tree Formatter.

# Cloud-Based Git Hosting Systems vs. Behind-the-Firewall Systems

Generally speaking, if you've chosen a cloud-hosted OpenSquiggly deployment option, such
as our shared cloud hosting plan or our private hosting plan, then you would expect to be able to
access any cloud-hosted Git system. If you've deployed your own Git server behind a corporate firewall,
then ordinarily you would not be able to access and use those private Git servers from a cloud-based
OpenSquiggly instance.

However, even this apparent limitation is not absolute. You could (at least in theory) use some Internet-based
tunneling software, such as NGrok, to create a tunnel to your internal Git server, and by doing so you'd
be able to create a pathway that would allow OpenSquiggly to get to those private repositories.

We don't necessarily recommend this approach for accessing private repositories, as we assume that most
organizations that have taken the trouble to install a private, behind-the-firewall Git server have done
so for security reasons, and therefore wouldn't want to allow access via a tunnel. The decision ultimately
depends on your security needs and the skills of your network administrators.

In most cases, if you must have access to private, behind-the-firewall Git repositories, then using our
self-managed private hosting plan may be the best option for you. In this case, you would create a VPN
within your cloud provider and install and configure an access point device approved by your cloud vender
in your data center. The OpenSquiggly instance running within your cloud-based infrastructure would then
be able to use the VPN to access Git systems that are hosted on physical systems in your own data center.

There's also a final option to install OpenSquiggly on your own servers in your own data centers, but
since most companies these days are migrating away from private data centers to cloud-based systems,
we've tailored our processes with an emphasis on using cloud providers and containerization tools
such as Docker and Kubernetes. However, on-premise deployment is still an option if that is what works
best for you.

In summary, as long as there is a way for your OpenSquiggly instance to reach your Git hosting system 
via an HTTP URL, then you will be able to connect and use those repositories within OpenSquiggly.

# HTTP vs. SSH Protocol Access

Currently OpenSquiggly supports HTTP/HTTPS access to your Git system. We do not support SSH access.
The main reason why we do not support SSH access is due to security issues.

Particularly in the case of our shared cloud hosting plan, supporting SSH would mean that we would
need to allow each user to upload their private SSH keys to our server. Our system would need to manage
and store each of our user's SSH private keys and ensure that no other user could access another
user's SSH keys accidentally. To reduce the risk of a security breach, we support HTTP access only.

One might say that the same problem applies to OAuth access tokens which we do store in our database.
The difference is that OAuth access tokens can be audited and easily revoked if there in any question
regarding its security status.
