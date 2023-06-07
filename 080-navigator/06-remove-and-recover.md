---
weight: 60
Order: 6
Title: Removing & Recovering Pages
description: How to remove pages and recover pages after they've been removed.
---
## Removing Documents

Your document tree is a hierarchically arranged set of references to pages. When you
remove a page from the document tree, it merely removes a reference to the page. The
page still exists and can be added back into your document tree at any time.

As we discussed in the section "Moving and Copying Pages", only the child page list of
a regular topic page can be modified. Therefore a page can be removed from the tree only
if its parent is a topic page.

To remove a document, locate the document in your document tree. Click the elipsis icon
(the "..." icon) corresponding to the document entry, and choose Remove from the menu.
Note that the ellipsis icon and/or the Remove menu option may not appear if the page
is a child of a mapped or virtual pages.

You'll be asked to confirm the operation before the page is removed. Click "Remove" to
confirm the operation or "Cancel" to abort and return to the normal navigator state.

## Recovering Documents by Moving or Copying Them

If you removed a document, but at least one reference to that document still exists in
your document tree, you can recover the document at the desired location by moving or
copying it from one of the references that still exist.

See the section "Moving or Copying Pages" for details on these operations.

## Recovering Documents by Searching For Them

Another way of recovering a document and adding it back into your tree is by searching
for it, and then dragging it from the search result list and dropping it onto the tree
at the desired location.

See the chapter "Searching for Documents" for more details on how to perform searches.

When you find the desired document drag it from the search result list into your tree.

## Recovering Unreferenced Documents

If all references to a document have been removed from the tree, then it is referred
to as an "unreferenced" document.

There's a special search syntax to search for unreferenced documents.

Enter the following query into the search bar:

```
ref:none
```

Note: There's currently a bug with this that gives an error:

```
Search Engine Error: 1
```

To work around the bug, enter:

```
. ref:none
```

This will return a list of documents that have no references to them.

From here, you can add the document back into your document tree by dragging and dropping it
as described in the previous section.
