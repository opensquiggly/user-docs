---
Order: 4
Title: Implicit Table of Contents
---
# Introduction

There are two ways to set up your documentation to let OpenSquiggly managed your
table of contents navigation for you: implicitly or explicitly. In this chapter
we'll cover the implicit method.

In general we highly recommend using an explicit table of contents, as discussed in
the next chapter. However, this is alightly more work and involves adding a ".opensquiggly"
file to each folder in your documents folder structure.

With implicit table of contents, OpenSquiggly builds the table of contents and determines
the order of files in the table of contents by using the names of the files in the folder.

# How File Names are Transformed into Table of Contents Entries

File and folder names are transformed into their final display names in the table of
contents as follows:

* Casing is preserved
* Spaces are preserved (though not recommended - use underscores or dashes instead)
* Punctuation marks normally allowed by the operating system are preserved except:
  - Single underscores are replaced with a space
  - Double underscores are replaced with a single underscore
  - Single dashes are replaced with a space
  - Double dashes are replaced with a single dash
  - Double at signs (@) are replaced with a single at sign
  - Single at signs are used as an escape character for special punctuations marks
* Punctuation marks not normally allowed by the operating system can be inserted using
  @ as an escape character, followed by an escape code:
  - @SL@ becomes a forward slash (/)
  - @BSL@ becomes a backslash (\\)
  - @QM@ becomes a question mark (?)
  - @PERC@ becomes a percent sign (%)
  - @STAR@ becomes an asterisk (*)
  - @CLN@ or $COLON becomes a colon (:)
  - @VB@ becomes a vertical bar (|)
  - @DQ@ becomes a double quote (")
  - @SQ@ or $AP$ becomes a single quote or apostrophe (')
  - @LT@ becomes a less than sign (<)
  - @GT@ becomes a greater than sign (>)
  - @DOT@ becomes a period (.)
  - @CM@ or $COMMA$ becomes a comma (,)
  - @SC@ becomes a semicolon (;)
  - @EQ@ becomes an equal sign (=)
* Numerical prefixes separated with dashes are removed (they are used for file ordering - see below)
* The ending file extension is removed

# Ordering of Table of Contents Entries

With implicit table of contents, the table of contents are ordered as follows:

* Folders are displayed first, in numerical prefix order before removing any numerical prefix,
  and the numerical prefix is removed before rendering
* Files are displayed next, ordered in the same manner as folders

# Numerical Prefixes Used for Ordering

A numerical file prefix can be applied to the folder or filename, of the form:

```
###-[###-[###-]]
---  ---  ---
 |    |    |
 |    |    +---> Section 3
 |    +---> Section 2
 +---> Section 1
```

The maximum number of sections is 3. If the number of sections is greater than 3, the
remaining sections are ignored for sorting purposes, but are still removed from the item
name prior to rendering.

The prefix should end with a single dash. The system uses everything after the final dash
as the page name when the item is rendered. The numbers are split into their sections
and the items are then sorted NUMERICALLY (NOT alphabetically) according to their values.
For example:

```
1-First_Item.md
2-Second_Item.md
2-1-Third_Item.md
2-10-Fourth_Item.md
3-Fifth_Item.md
3-1-Sixth_Item.md
3-2-Seventh_Item.md
```

The above set of files would result in a table of contents looking like:

```
First Item
Second Item
Third Item
Fourth Item
Fifth Item
Sixth Item
Seventh Item
```

It's generally recommended to just use a single section in the prefix, but multiple sections
are allowed because they may be useful to avoid renumbering of the entire list when a new
item is added to the middle of the list.

For example, consider the list:

```
1-Come.md
2-Ye.md
3-Faithful.md
```

and I now wish to insert a new item named "All" between the first and second item, I can
now do:

```
1-Come.md
1-1-All.md
2-Ye.md
3-Faithful.md
```

If a file or folder has no prefix at all, then it is still sorted within the overall list
of items as if "0-0-0" were the prefix. In other words:

```
My_Item.md
```

is equivalent to:

```
0-0-0-My_Item.md
```

Items with the same numerical prefix are sorted alphabetically relative to each other.

# Example

## The /docs folder contains
```
(folder) 1-Overview
(folder) 2-Reference
(folder) 3-Proposals
(folder) images
(file)   index.md
```

## /docs/index.md contains
```
Here is some system documentation.
```

## The /docs/1-Overview folder contains
```
(file) 1-History.md
(file) 2-Concepts.md
(file) 3-Development_Environment_Setup.md
(file) index.md
```

## /docs/1-Overview/index.md contains
```
Here is some overview documentation.
```

## The /docs/2-Reference folder contains
```
(file) 1-Database_Schema.md
(file) 2-Folder_Layout.md
(file) index.md
```

## The /docs/2-Reference/index.md contains
```
Here is some reference documentation
```

## The /docs/3-Proposals folder contains
```
(file) 1-External_Content.md
(file) 2-Mapped_Pages.md
(file) 3-System_Identifiers.md
(file) index.md
```

## The /docs/3-Proposals/index.md contains
```
Here are specifications for work proposals.
```

# The /docs/images folder contains
```
AddMappedPageMockup.jpg
AzureDevOpsMockup.jpg
```

Assume the /docs folder is connected via a mapped topic page named Documentation.

Now the Navigator renders the following navigation of child topic pages.

```
Documentation -> Overview  -> History
                              Concepts
                              Development Environment Setup
                 Reference -> Database Schema
                              Folder Layout
                 Proposals -> External Content
                              Mapped Pages
                              System Identifiers
```
