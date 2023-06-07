# About this Repository
This repository contains user documentation for OpenSquiggly. OpenSquiggly
is an Internal Developer Portal (IDP) dedicated to helping developers be
happier and more productive in their jobs.

The content in this repository is published to the OpenSquiggly web site
at https://opensquiggly.com/docs, and can also be imported as a "doc tree"
mount point into any OpenSquiggly instance.

# Docs-As-Code Philosophy
We intend this repository to serve as a good example repository for how
documentation can be authored independently of the final document hosting
system that ultimately serves it to readers.

We believe in the docs-as-code approach, as it is a highly flexible workflow
that fits in well with the daily life of developers, but we want to see
documentation repos exist as pure documentation, free from all of the other
distracting cruft that is typically found in documentation sites, most 
typically in documentation sites that are built using static site generators.

By keeping the documentation content separate from the dev-ops cruft that is
used to build it, technical document authors have a better user experience
because they do not have to wade through all of the surrounding errata, and
can focus purely on authoring content.

# How Files are Organized for Authors
Notice that we prefix our folder and file names with numerical prefixes. This
is a convenience aimed at the document authors (not the readers), so that
they can view the files in the order in which readers will read them.

Most raw source code file hosting systems, such as GitHub, will display the
file and folder names in alphabetical order. By using numerical prefixes,
we can make the files appear in the same order for authors as the final
intended reading order that is intended for users.

In order to make it easier to add new chapters in the middle of a long document,
we recommend spacing out the numerical prefixes by 10, leaving room to inject
new documents in the middle.

Old timer programmers who first learned to program on BASIC on early microcomputers
should appreciate the approach here. BASIC used line numbers, and programmers
typically numbered their lines by increments of 10 for the same reason.

You can always renumber your file prefixes if you run out of space. It's a little
tedious to do it by hand. It would be nice if there was a tool out there that
could help renumber numerically prefixed files in folders.

# How Files are Ordered when Published
The final order of the published table of contents is controlled in one
of three ways:

* By using front matter embedded at the top of each document, using
  either the ```order```, ```weight```, or other similarly named attribute,
  depending on the final hosting system or static site generator.
* By using the order entered in the .opensquiggly file contained within the
  same folder.  
* By using the numerical prefixes in the file names. Depending on your static
  site generator or hosting system, you may be able to configure the system
  to respect and/or strip off the prefixes. OpenSquiggly supports ordering
  of table of contents by using numerical prefixes if neither the front matter
  ordering or the .opensquiggly ordering is available.