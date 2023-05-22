---
Order: 1
Title: Overview
---
# Overview of Authoring Capabilities

In addition to being able to host and curate documents from external sources,
you can directly author documents from within the OpenSquiggly system itself.
You are likely already familiar with this authoring paradigm if you have used
other "wiki" software in the past.

Both internally authored and externally hosted documents have their usages, and
that is why OpenSquiggly supports both paradigms.

Internal authoring provides a more direct content creation experience, and is
preferable in cases where the document author wants a faster way to put something
into OpenSquiggly, or does not regularly use developer tools such as text editors,
Markdown formatters, and Git.

For example, extended stakeholders on the software development team such as project
managers, product managers, quality assurance professionals, and technical support
agents may find that they are empowered to contribute to the team's knowledgebase when 
they can directly author documents within OpenSquiggly.

Even the software developers themselves may at times choose to use internal document
authoring for content that they want to get done more quickly, or which may not benefit
from being stored and versioned alongside the source code in a version control system.

# Summary of Authoring Approaches

* Internally Authored
  * Advantages
    * Faster, more direct auhoring experience
    * Author can see the final presentation format of the document immediately
    * Hyperlinks work immediately and can be tested in-place
    * Images embedded within the document can be seen in-place immediately
    * Can author content using the web browser without needing any additional specialized software
  * Disadvantage
    * The embedded text editing capabilities may not be as feature-rich as a dedicated,
      external text editor
    * Documents are stored in OpenSquiggly's database and less able to be acted upon by
      other tools in the developer's toolchain
    * Documents not able to be cross-posted to multiple portals and/or search engines as easily
      when they are stored in the database vs. the file system
    * Documents not stored and versional alongside the source code it relates to
* Externally Hosted
  * Advantages
    * Fits in well with the developer's ordinary daily workflow
    * Users can edit the document using their favorite tools
    * Documents stored and versioned with the source code
    * Documents not "held hostage" by the hosting system's database
    * An especially good choice if the intention is to cross-post the document to multiple
      hosting systems or search engines
  * Disadvantages
    * Takes more effort to author a piece of content
    * Can't see the final presentation format of the document until the change has propagated
      to OpenSquiggly for hosting
    * Correcting small typographical errors is more difficult
