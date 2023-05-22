---
Order: 1
Title: The Doc Formatter
---
# Outline - Remove After Completing
* Attach documentation as its own mount point
* Reusing an existing mount point
* Using the OpenSquiggly Simplified Document Tree Formatter
  * Text files: .md, .html, .xml
* How XML files are processed and rendered using XSLT transforms

# Introduction to Document Trees

In addition to displaying your files to you in an unfiltered, unformatted view, OpenSquiggly
can also dynamically process your files and display them to you in a filtered and formatted view.
This creates a pleasant, human readable view of documentation files stored in your Git repositories.

As we saw in the last chapter, when you create your mount point, the Tree Format Type fields
controls how to process and format the files in your repository. We discussed the Raw Files and
Folders tree type, which displays everything in your repository.

In this chapter we'll discuss the second tree format type available, the OpenSquiggly Simplified
Document Tree Formatter.

# Supported Files

If the document tree formatter finds any of the following files, it will render them in
the document tree's table of contents:

* Markdown Files (files with a .md extension)
* HTML Files (files with a .html extension) TODO: What about .htm - do we support it?
* XML Files (files with a .xml extension)

Any other files in the repository will be filtered out and not shown in the table of contents.

The excluded files, however, can still be referenced by your Markdown, HTML, and XML documents.
For example, if you place image files (for example, .gif, .jpg, or .png files) in your repository
you can reference and embed those image files from your documentation files, but the image files
themselves will not appear in the table of contents.

# Processing Markdown Files

When OpenSquiggly renders a Markdown file with the doc tree type, it processes the file with
a built-in Markdown processor, which turns it into HTML that the browser can render. As is the
case with any Markdown file, HTML that is embedded directly in the Markdown file is passed
through directly to the output HTML file.

Before the processed HTML file is sent to the browser, it is "sanitized" to remove scripts
and other non-document oriented HTML that could be dangerous for the browser to render.

The final processed and sanitized HTML is then sent to the browser for rendering in the content
pane for that page.

# Processing HTML Files

HTML files are processed similarly to HTML files, except there is no Markdown processor to
pre-process the file. Other than the sanitization process which is the same as used by the 
Markdown files, whatever content you enter into an HTML file is passed directly through to
the browser for rendering in the document's content pane.

Since Markdown files can also support embedded HTML, there's little reason to use HTML
files most of the time. We recommend that you author the majority of your content in Markdown
files, and falling back to HTML when there's no corresponding Markdown syntax that gives you
what you want.

The only reason to using straight HTML files is that they are formatted slightly faster, since
they do not need to be pre-processed by the Markdown formatter. It is doubtful that the end
user reading the document will notice any difference in performance.

However, if you know in advance that you are authoring pure HTML content, then you might
want to store it in an HTML file instead of a Markdown file just for reasons of content purity.

# XML Files

XML files are also supported and recognized by the doc tree type formatter. When the formatter
sees an XML file, it can optionally transform the file with a built-in XSLT processor. This
is very convenient for using semi-structured data within OpenSquiggly where an XML file 
containing data can be transformed by an XSLT-based template file into the final display format.

TODO: Is the final output also sanitized as it is with Markdown and HTML Files? Not sure.
Need to check.
