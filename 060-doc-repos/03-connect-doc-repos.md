---
weight: 30
Order: 3
Title: Reusing Mount Points
description: >
  In this section we discuss how you can reuse mount points to create different
  formatted views of the same underlying files.
---
## How to Mount Documentation Repositories

To connect to a documentation repository, follow the same basic steps outlined in the
previous chapter about connecting to source code repositories.

You'll fill in all the fields in the mount point form the same way you filled them
in for source code repositories, with two exceptions:

*Start Path* - If your documentation is part of a larger source code repository, you might
want to set a different Start Path. For example, if your documentation is located in the
"/docs" folder, then set the Start Path to "/docs". Only files in the /docs directory and
below will be included in the mount point.

*Tree Format Type* - As we've already discussed, you'll choose the OpenSquiggly Simplified
Document Tree Formatter as your tree type instead of the Raw Files and Folders tree type.

## Reusing Repositories

There are times when you want to mount the same repository twice - once to get the raw
files and folders, and once again to get the formatted documents.

Although you could simply connect to the repository twice and create two entirely separate
mount points, this is inefficient. The repository will be cloned and indexed twice, taking
up twice as much disk space.

To solve that problem, you can reuse the first repository when you create your second mount
point.

Example:

Create your primary mount point by connecting to your source code repository, setting the
Start Path to "/" and the Tree Format Type to raw.

Next, create a secondary mount point. In the Connection Type dropdown, select "Reuse Existing
Repository". In the mount point dropdown, pick the mount point you wish to reuse.

Set the Start Path to the location of the subfolder containing your documenation, for example,
"/docs".

Set the Tree Format Type to doc to get formatted documenation.

Save the mount point.

You'll now have two mount points created for the same underlying repository, one for your
source code, and one for your documentation.

The nice thing about this set up is that when you refresh the parent mount point to pull down
updated files, the secondary documenation mount point will also automatically update. This
makes sense since both mount points are tied to the same cloned repository.
