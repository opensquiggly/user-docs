---
Order: 5
Title: Explicit Table of Contents
---
## Introduction

Explicit table of contents management is done by placing a ".opensquiggly" file within
each folder containing your documents.

## Format of .opensquiggly Files

For any given folder in the document tree, if a .opensquiggly file is present in that folder,
then the .opensquiggly ordering technique is used, otherwise the numerical prefix method is
used. The two techniques can be mixed-and-matched together within a document tree, though
generally it is recommended that an author pick one technique or the other and use it
consistently throughout the document tree.

The .opensquiggly file is a simple text file format with lines of the form:

```console
file_or_folder_name=title
```

The table of contents items are rendered in the order in which they appear in the file.

## Example Using .opensquiggly Files

### The /docs folder contains

```console
(folder) overview
(folder) reference
(folder) proposals
(folder) images
(file)   index.md
(file)   .opensquiggly
```

### /docs/index.md contains

```console
Here is some system documentation.
```

### /docs/.opensquiggly contains

```console
overview=Overview
reference=Reference
proposals=Proposals
```

### The /docs/overview folder contains

```console
(file) history.md
(file) concepts.md
(file) devenv-setup.md
(file) index.md
(file) .opensquiggly
```

### /docs/overview/index.md contains

```console
Here is some overview documentation.
```

### /docs/overview/.opensquiggly contains

```console
history.md=History
concepts.md=Concepts
devenv-setup.md=Development Environment Setup
```

### The /docs/reference folder contains

```console
(file) db-schema.md
(file) folder-layout.md
(file) index.md
```

### /docs/reference/.opensquiggly contains

```console
db-schema.md=Database Schema
folder-layout.md=Folder Layout
```

### The /docs/reference/index.md contains

```console
Here is some reference documentation
```

### The /docs/proposals folder contains

```console
(file) external-content.md
(file) mapped-pages.md
(file) system-ids.md
(file) index.md
```

### /docs/proposals/.opensquiggly contains

```console
external-content.md=External Content
mapped-pages.md=Mapped Pages
system-ids.md=System Identifiers
```

### The /docs/proposals/index.md contains

```console
Here are specifications for work proposals.
```

### The /docs/images folder contains

```console
AddMappedPageMockup.jpg
AzureDevOpsMockup.jpg
```

Assume the /docs folder is connected via a mapped topic page named Documentation.

Now the Navigator renders the following navigation of child topic pages.

```console
Documentation -> Overview  -> History
                              Concepts
                              Development Environment Setup
                 Reference -> Database Schema
                              Folder Layout
                 Proposals -> External Content
                              Mapped Pages
                              System Identifiers
```
