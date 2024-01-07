---
weight: 10
url: /docs/overview/foreword
Order: 1
Title: Foreword
description: >
  An introduction to OpenSquiggly from its founder and creator.
---
## Introduction

Hello and thank you for choosing OpenSquiggly for your software project documentation needs. My name is Kevin Dietz,
a long-time veteran of the software industry and the founder of OpenSquiggly. Let me tell you my story, the
challenges I see that face the software industry, and why I created OpenSquiggly.

## Software Agility, Then and Now

We all know the history of the Agile Manifesto that started the agile software development movement over the last
two decades; a small group of software veterans, many of them consultants and authors, met in February 2001 at the
Snowbird Lodge in Utah to pontificate the future of software development and author the Agile Manifesto.

So who were these people? 

I may have have met a few of them at conferences from time to time, but I don't know them personally. However, I 
don't think I'm mischaracterizing the situation with the following observations: they were all highly seasoned 
software veterans; they all had approximately the same level of very high technical skill; they were independent 
workers who worked as software consultants; most of them were US, British, or Canadian citizens; they all spoke 
fluent English; they were all excellent communicators, in both verbal and written forms; they were all about the 
same age; they all watched the same movies and knew the same jokes.

I imagine that their expectation of a software project was a small group of highly experienced software engineers, 
all fluently speaking the same language, co-located together in the same office, working on a reasonably well-bounded 
software project, consisting of a relatively new codebase with limited interfacing requirements with legacy code.

They expected to come in to the office, work side-by-side with their fellow equally-talented team members, solve 
problems together at the whiteboard, all of them engaging in well-mannered active listening and polite assumption
challenging, and when they were done with the day, they'd go out for happy hour together at the local pub down the 
street. In other words, a tight-knit team working closely together, firing on all cylinders.

With that kind of shared understanding of what a software project looked like, it's not hard to see how they came
up with the Agile Manifesto:

* Favor individuals and interactions over processes and tools
* Favor working software over comprehensive documentation
* Favor customer collaboration over contract negotiation
* Favor responding to change over following a plan

## Where Did We Go Wrong?

Sadly, I think the state of affairs at an average software project in corporate America today looks very different from the
quaint notion that the Agile Manifesto authors had in mind in 2001. Things are much messier in the world now. 
Consider the current context that can be found in practically any software project in the world:

* The team is scattered in multiple locations around the world.
* The team is separated by large timezone differences.
* There is a large spread in the age range of the team.
* Verbal and written communication skills vary throughout the team.
* Team members may be fluent in different technology stacks than their coworkers.
* Some people are brand new to the project, while others have already worked on the project for years.
* Recruiting senior engineering talent is difficult and expensive.
* Project managers may or may not be well acquainted with the problem domain of the project.
* Codebases are very large and often older.
* The requirements of the project are not always as well-bounded as one would like.
* The project has a large number of external dependencies that need to be managed.

If I had to pick a single word that summed up all the challenges that face a modern software project, I would choose
"complexity". Every aspect of software projects today are more complex than their counterparts from 20 years ago. What's
needed then in the industry are new techniques and tools for dealing with this massive increase in complexity.

It's not that I think the Agile Manifesto is wrong per se, but I just don't think it offers much in the way of guidance about
how to manage a modern, large software project, replete with the massive layers of complexity that I mentioned above. Sometimes,
in my darker moments of reflection, I think that if the American nuclear defense system were engineered the way we write
software today, we would have blown ourselves to Kingdom Come long ago.

Different approaches are needed to continue the march of progress, and that's what we're trying to create with
OpenSquiggly.

## The Role of Documentation

Let's dig deeper into that second Agile Manifesto principle:

  "Favor working software over comprehensive documentation"

Not wanting to pick a fight with the giants upon whose shoulders I'm standing, but let's get real here - you're going
to need some level of documentation if you want to run an effective software project. The manifesto doesn't say that
we shouldn't write documentation at all, but it does downplay it, and in many cases I think teams have taken this
anti-documentation philosophy too far.

Let's break this down a little. First, I think the kinds of documentation the authors were referring to is very different
from the kinds of documentation that we are espousing with OpenSquiggly. What they were talking
about are those big-design-up-front, multi-volumed specification documents that were written before any software was written 
at all, that attempted to describe, in the minutest detail, every last aspect of the behavior of the software. That doesn't 
usually work in commercial, for-profit software development projects. Perhaps government agencies and highly-regulated 
industries still need to work that way, but that approach is too slow for fast-moving commercial software development.

We're talking about something different. What we're talking about is the as-you-go type of architecture documents, diagrams, 
reference documents, code narratives, and other technical errata that you should maintain alongside your source code, 
allowing you to effectively communicate with the team and to maintain the codebase as time goes on. It is a living knowledge 
base that you cultivate throughout the lifetime of your project. We espouse an adaptive, lightweight documentation process 
that fits in with the developer's ordinary daily workflow; documentation that supports and empowers the team, not 
hinders it.

## What is It?

What is OpenSquiggly? 

OpenSquiggly is a software developer productivity platform, focused on curating documentation and source code from many
projects across the organization, with the goal of helping developers find information faster and do their jobs better.

### Document Authoring

You can author documents inside of OpenSquiggly in the same way you can author documents in a corporate wiki, with
a couple of differences.

First, the documents are, or at least can be, multi-fragmented. You can arrange and delete fragments (we call them
"snippets") within the page of the document, but you edit each snippet one at a time, rather than having a unified 
editing surface that lets you edit the entire document all at once. You can think of this very much like object-oriented 
programming. Each snippet can be of a particular snippet type, and each snippet type has different operations that 
can be performed on it, that are specific to that snippet type. In this type of system, it makes more sense, and is
more feasible to implement, individual editors for each snippet type, rather than trying to develop a single, unified
editing experience for the whole document.

Second, for authoring textual content, we provide an integrated text editing experience that lets you directly enter
Markdown, HTML, or XML content. Since the product is aimed at software developers, and because software developers
love Markdown, we've adopted an approach that gets out of your way and allows you to directly enter Markdown content.
While we may add a rich text editor some day in the future, we'll always keep the ability to directly enter Markdown
and HTML content, as it gives developers the most control over the type of content they wish to author.

Document editing via a traditional corporate wiki experience is just the beginning, however. OpenSquiggly adds several
features beyond that to make it a documentation portal developers will love. These include:

### Docs-As-Code Publishing Workflow

You don't need to author your documents internally within the OpenSquiggly system. You can author them and store them
in your favorite Git hosting system, using any text editor of your choosing, and then host those externally-stored
documents within OpenSquiggly. This works by "mounting" your repositories in OpenSquiggly, and then grafting documents
from those mounted repositories into your document tree.

With this approach, your documents aren't held hostage by the wiki's database. They can live outside of the document hosting
system, where they can be edited and versioned the same as ordinary source code. This approach is highly flexible. You
can merge content from separate sources, split them apart, and recombine them in highly adaptable ways to meet the needs
of your project.

### Source Code & Documentation Together

Besides bringing formatted documents into your document tree, you can also bring in the actual source code of your
project or your project's dependencies. This gives you a unified environment for perusing and searching your documentation
and source code together. This is important because if the documentation you need doesn't exist, you can resort
to reading through the source code. Having source code and documentation living side-by-side in one hosting system supports 
this type of workflow.

You might ask, why not just view the source code in your favorite IDE? If it's the main project repository you work with
on a daily basis, that works fine. But developers are often dealing with many other ancillary repositories that provide external
libraries, subsystems supplied by other groups, plugins, microservices, etc. There might also be times where you want to
peruse projects from other teams just to see how they solved a particular problem. Having access to all the company's
repositories in a unified system where all the source code can be easily explored and searched from one place helps to
breakdown communication barriers and facilitate synergistic problem solving.

### Reference Documentation Support

When we designed OpenSquiggly, we wanted a way to host class-and-method level reference documentation alongside your
high level architecture documents and source code, giving you a complete end-to-end view of your project. The secret sauce
that drives this is our table-of-contents management system. By separating the table-of-contents of the document structure
from the actual textual content, you can mix-and-match reference documentation generated from tools such as JavaDocs, JS Doc,
DocFX, Sandcastle, etc., and merge reference documentation generated from different tools into a single, unified hosting
environment.

Other corporate wikis on the market don't do a good job of letting you mix in reference documentation
generated from the code structure, and since this is an important feature for developers, we wanted to bake these
capabilities into the platform.

### Customizability

Each developer can customize their documentation tree to their liking, based on their needs and the tasks they are working
on. With other wikis, you're stuck with a document structure as it was laid out by the author.

Since developers can quickly become overwhelmed with too much information, it is important that each developer
can create customized views of exactly what they need to see for their specific work.

### Regular Expression Searching

Often times, there is no existing documentation that will provide the technical details you are looking for.
When that happens, a good strategy is to start searching and reading the source code.

To help you do that, we've built in some nice code searching capabilities that can let your search across all
your repositories and documentation all at once. We support regular expression-based searching, which is great
for searching for patterns in the code, and we provide a extensive set of include/exclude filtering conditions
that let you easily search for specific files, repositories, and other conditions to help you narrow down your
search to exactly what you're looking for. Read the chapter on "Searching" for more details on how to create
very specific filtering conditions.

### And Even More

As you use OpenSquiggly you'll discover more features and more nuances to the product that we haven't explicitly
covered here. And of course, we're always working hard to add more relevant functionality to the product.

The end result we're aiming for is a product that lets developers curate, index, organize, customize, annotate,
tag, search, save, bookmark, take notes, write code narratives and walkthroughs, and share their research results with
others in the organization.
