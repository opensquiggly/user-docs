---
weight: 30
Title: Alternatives
Order: 3
description: >
  Comparing OpenSquiggly to static site generators and other approaches to team documentation.
---
## What Is OpenSquiggly, Revisited?

We answered this question in the Foreword, but let's come back to this question again
and look at it from a different perspective.

Another way of describing OpenSquiggly is that it is a new class of documentation tool,
a *dynamic* site generator as opposed to traditional *static* site generators.

OpenSquiggly is a hosting environment for files and documentation that can be stored
externally from the hosting environment (namely, Git repositories) and synchronized with
the hosting environment. In other words, OpenSquiggly is a user-configurable "smart web
server" with the ability to auto-synchronize with external file sources.

It serves up your files like an ordinary web server does, except that it surrounds that
content with extra infrastructure that makes the content manageable and interactive.
You provide the content of your documentation and files, and OpenSquiggly provides the
table of contents management, the indexing and search infrastructure, account management
and access control, etc.

## Static vs. Dynamic Site Generation

Traditional static site generators are a viable way of building a documentation-oriented
web site.

The workflow generally looks as follows:

```
+---------------------------------------------+
| Your Files + Table of Contents File         |
+---------------------------------------------+
                   |
                   v
+---------------------------------------------+
| Static Site Generator Command Line Tool     |
| (e.g., MkDocs)                              |
+---------------------------------------------+
                   |
                   v
+---------------------------------------------+
| Set of Static HTML Output Files             |
+---------------------------------------------+
                   |
                   v           
+---------------------------------------------+
| Deploy files to host (Using FTP, SCP, etc.) |
+---------------------------------------------+
                   |
                   v       
+---------------------------------------------+
| Web Server (e.g., GitHub Pages, etc.)       |
+---------------------------------------------+  
                   |
                   v       
+---------------------------------------------+
| User visits and navigates the site          |
+---------------------------------------------+                                                      
```

The basic problem here is that HTML was not designed to cleanly separate content from a table
of contents in a multi-document knowledge base. If one wanted to skip the first two steps in
the above workflow and author HTML content directly, then each HTML file you authored would
need to embed or somehow include a link to the table of contents (perhaps using server-side
includes or some other mechanism). If you later decided to change your table of contents, you
might need to modify every file in your document site.

That's obviously not workable in a large knowledge base of documents, and so static site
generators were designed to be able to shuffle the content and table of contents together
in the statically generated output.

Another advantage of SSGs, and a big reason that people use them, is so that the static files
can be delivered via a distributed content delivery network and then delivered to the end
user's browser very quickly.

However, that high performance content delivery is not needed in most cases (there are other
ways to scale if you really need it), and comes at the cost of a lot more work to build a fully 
functioning documentation site. All capabilities and features of the site must be built into 
those HTML files somehow. Of course they can contain active JavaScript content that will run 
client side, and those scripts can make calls back to cloud-hosted serverless functions, and 
together users can build some really amazing sites with static site generators.

But that means as the content author, you have to be thinking about all the site's capabilities 
and building that into the pages. At this point you aren't writing documentation for your project, 
you are building a whole other *application*, which presumably is going to be just as much work
to maintain as the project you're already working on that you are trying to document!

OpenSquiggly was written with the idea that the content author doesn't have the time to do all this work,
especially not busy software developers who just want a quick and painless way to publish
technical information about their projects. They just want to write the core content, 
describe the desired table of contents in some place that is separate from the core content, 
check the files into Git, and then let a document hosting environment take care of all the rest 
(document retrieval, Markdown formatting, authenticated access, indexing, searching, bookmarks, etc.).

## Dynamic Site Generation

With that context in mind, you can think of OpenSquiggly as a cousin of static site generators.
It is a *dynamic* site generator / hosting environment.

The OpenSquiggly workflow then looks as follows:

```
                                                     +---------------------------------------------+
                                                     | User creates external content mount points  |
                                                     | in their OpenSquiggly account               |
                                                     +---------------------------------------------+
                                                                        |
                                                                        v
                                                     +---------------------------------------------+
                                                     | Git repositories stores and serves document |
                                                     | content                                     |
                                                     +---------------------------------------------+
                                                                        |
+---------------------------------------------+                         |
| OpenSquiggly Portal                         |  <----------------------+
+---------------------------------------------+
                   |
                   v
+---------------------------------------------+
| OpenSquiggly retrieves document content     |
| from external Git hosts                     |
+---------------------------------------------+  
                   |
                   v
+---------------------------------------------+
| OpenSquiggly dyanamically arranges pages,   |
| table of contents navigator, and all other  |
| user interactivity features                 |
+---------------------------------------------+
                   |
                   v           
+---------------------------------------------+
| User visits and navigates the site          |
+---------------------------------------------+                                                      
```

## Hybrid Approaches

OpenSquiggly has rich, built-in capabilities for retrieving, formatting, and displaying documents.
We've designed it to cover all the usual use cases that software development teams are expected to
face.

It can't do anything and everything however. It's not a Turing-complete programming environment.
It doesn't run custom code processing logic the way SSGs can do. There could be times where you
need to perform complex processing of your documentation in order to format the final presentation
of the document.

In a situation like this, you can combine the best of both worlds of SSGs and OpenSquiggly. Use
SSGs to process your documents and generate presentation-level HTML (or XML - OpenSquiggly has
built-in support for XSLT processing), and then feed that output into OpenSquiggly so that it
can manage the document hosting environment.

Such a workflow might look like:

```
+---------------------------------------------+
| Your Files + Table of Contents File         |
+---------------------------------------------+
                   |
                   v
+---------------------------------------------+
| Static Site Generator Command Line Tool     |
| (e.g., MkDocs)                              |
+---------------------------------------------+
                   |
                   v
+---------------------------------------------+
| Set of Static HTML Output Files             |
+---------------------------------------------+
                   |                                 +---------------------------------------------+
                   |                                 | User creates external content mount points  |
                   |                                 | in their OpenSquiggly account               |
                   |                                 +---------------------------------------------+
                   |                                                    |
                   |                                                    v
                   |                                 +---------------------------------------------+
                   +-------------------------------> | Git repositories stores and serves document |
                                                     | content                                     |
                                                     +---------------------------------------------+
                                                                        |
+---------------------------------------------+                         |
| OpenSquiggly Portal                         |  <----------------------+
+---------------------------------------------+
                   |
                   v
+---------------------------------------------+
| OpenSquiggly retrieves document content     |
| from external Git hosts                     |
+---------------------------------------------+  
                   |
                   v
+---------------------------------------------+
| OpenSquiggly dyanamically arranges pages,   |
| table of contents navigator, and all other  |
| user interactivity features                 |
+---------------------------------------------+
                   |
                   v           
+---------------------------------------------+
| User visits and navigates the site          |
+---------------------------------------------+                                                      
```

Basically what we're doing here is using Git as a delivery vehicle. Instead of trying to directly push
new content to OpenSquiggly using FTP, SSH, or some other final transfer mechanism, we deliver it 
indirectly by checking the files into Git, and then taking advantage of OpenSquiggly's ability to
retrieve files from Git.

This is an advanced topic and we won't give it further treatment here. For now, we just want to leave you
with the thought that, one way or another, OpenSquiggly is flexible enough to handle all your project 
documentation needs.

## Summary

In conclusion, OpenSquiggly can be thought of as a "smart web server" that performs dynamic
processing on simply-written documents and dynamically creates and serves a web site from them.

