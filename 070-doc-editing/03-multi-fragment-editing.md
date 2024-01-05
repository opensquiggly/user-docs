---
weight: 30
Order: 3
url: /docs/mount-points/doc-authoring/fragments
Title: Multi-Fragment Documents
description: Describes how content within OpenSquiggly pages are broken into smaller fragments.
---
## Editing Document Fragments

One big difference that you may notice right away in OpenSquiggly vs. other similar types
of software you may be familiar with is that the documents are multi-fragmented. That is,
you edit the document in smaller individual pieces rather than editing the entirety of the
document all at once.

We call these document fragments "snippets", which is how we will refer to them from now on.

That doesn't necessarily mean that you _have_ to use multiple snippets on a page. If all you
need is multiple paragraphs of text, with possibly some embedded images or hyperlinks within
the paragraphs, you can simply place a single Markdown or HTML-formatted text snippet on the
page, and author all of your content within that one snippet.

However, in some cases uses multiple snippets is helpful because you can have different types
of snippets on the page surface.

A special type of snippet called a File snippet allows you to upload a file to the page, and
optionally embed the content of the file in the page when it is rendered. This is useful for
uploading images to the page.

If you are entering code blocks onto the page, then you might want to place a code block
in a separate text snippet using the "Source Code Viewer" formatter, which gives you a bit
more control over how the code block is rendered vs. embedded the code block within a larger
Markdown fragment.

In the future we'll be adding other types of snippets to the system as well.

These are some of the reasons you might want to use multiple snippets on a page. If none of those
reasons apply to your content, then it simply becomes a matter of preference as to whether you
want to use one big snippet or lots of small snippets on the page.

## Rich Text vs. Plain Text Editing

Another area where OpenSquiggly differs from other systems you may have used in the past is
that OpenSquiggly uses a plain text editor rather than a rich text editor for editing content.
Rich text editors are sometimes called What-You-See-Is-What-You-Get, or WYSIWYG.

If you've ever used a modern wordprocessor such as Microsoft Word or OpenOffice, then you've
used a WYSIWYG editor.

The problem with rich text editors is that they are difficult to implement inside of a web
browser, andy tend to be buggy and clunky as a result. Certainly they are popular among less
technical user audiences, and for that reason we may add rich text editing capabilities in a
future version of OpenSquiggly.

However, a plain text editor, combined with Markdown, HTML, and XML formatting support, offers
a more precise way of authoring technical content such as software developers will likely be
writing. In our experience, many developers actually prefer plain text editors to rich text
editors, and for that reason we chose a plain text editor for our editing experience.
