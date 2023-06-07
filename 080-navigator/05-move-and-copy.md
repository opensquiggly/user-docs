---
weight: 50
Order: 5
Title: Moving & Copying Pages
description: How to move and copy pages to different locations in the document tree.
---
## Overview of Page Types

There are 3 types of pages in OpenSquiggly: topic pages, mapped topic pages (sometimes more simply
called 'mapped pages'), and virtual pages.

Topic pages and mapped topic pages are physical entities represented and stored as a record
in the OpenSquiggly system database.

The Home page is a special topic page created for each user that represents the top-level node
of each user's document tree.

Virtual pages are non-physical entities. They are not stored in OpenSquiggly's database of pages.
Instead, they are created dynamically in memory in the system when they are referenced. A virtual
page stores a reference to the mount point id, and the path within that mount point.

A more detailed explanation of page types and how they are structured and stored in the system
is covered in the chapger "Page Theory".

## Moving and Copying Children of Topic Pages

The *children* of regular topic page (not mapped pages) can be moved to a different place in the
document tree, or they can be removed from the document tree entirely. Note that remove a document
from the tree merely removes a reference to the page. It does dot delete the page, and the page
can be recovered and re-added to the document tree at a later time.

Likewise, new pages of any kind can be placed *into* the child list of a regular topic page.

## Moving and Copying Children of Mapped Pages

A mapped page itself can be moved (because by definition it must be a child of a regular topic page),
but it's children cannot be moved, and new children cannot be added to a mapped page.

This is because a mapped page is a hybrid between a physical topic page and a virtual page. The page
itself is physically stored in the database, however it's table of contents list is not stored in
the database. It's table of contents is generated dynamically by reading the subdirectories from the
path corresponding to that mount point. Because the table of contents is generated dynamically from
the external source, the user cannot modify that pages list of child pages.

The children of mapped pages can, however, be copied to other locations in the document tree.

## Moving and Copying Children of Virtual Pages

A virtual page can be moved only if it is a child of a regular topic page.

As with mapped pages, the children of a virtual page cannot be moved, nor can new children be
added to a virtual page.

Also as with mapped pages, the children of virtual pages can be copied to other locations in
the tree.

## How to Move Pages

To move a page (assuming it is moveable according to the rules above), click and hold the page
with the mouse and drag it to the desired location.

If you drop the page onto another topic page, it will be added as the last child of that topic
page.

If you drop the page in between two pages, it will become a sibling of those two pages and
inserted into the document tree at that location.

When you move a page, it's original location in the document tree is removed, and a new entry
is created at the destination location where you dropped the page. In other words, a move 
operation is essentially a "remove-and-insert" operation.

## How to Copy Pages

Copying a page copies a *reference* to the page to another location in the document tree. It does
not create two copies of the content of the page, it merely creates two references to the same
page.

Copying in similar to moving. Hold down the CTRL key (or CMD key on a Mac) while clicking and
dragging the desired page.

Dropping the page onto another page will create a new reference to the page as the last child
of the page you dropped onto.

Dropping in between two pages will create a new reference to the page as a sibling of the pages
where you dropped.

Copying works exactly the same as moving, except the original reference in the document tree
is not removed. In other words, a copy operation is essentially an "insert-but-don't-remove"
operation.

