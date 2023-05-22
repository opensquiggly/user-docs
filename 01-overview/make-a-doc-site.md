---
Title: Use Cases
Order: 4
ShowInSidebar: false
---
# Internal vs. External Target Audience

One of the reasons why we created OpenSquiggly was because we felt the industry was
lacking in really good tools for *internal* distribution of technical documentation
by teams to either themselves (other developers on the team), or other teams with the
organization.

However, another potential use of OpenSquiggly is publishing documents for external
users as a front-facing part of your web site.

In this document we'll focus on this second use case, publishing documents for external
consumption.

# How to Build a Customer-Facing Documentation Site

For the purpose of this chapter, we'd like to call your attention to Microsoft Docs,
which is Microsoft's front-facing documentation portal (http://docs.microsoft.com).

Up until a few years ago, Microsoft had two documentation portals, MSDN and TechNet.
Together they weren't very well organized, and customers constantly complained that
Microsoft documentation was too hard to find and use. We're not trash talking Microsoft
here ... Microsoft themselves say as much in their blog about why they migrated away
from these portals
(https://docs.microsoft.com/en-us/teamblog/introducing-docs-microsoft-com).

So, beginning a few years ago (starting in about 2016), Microsoft set out to change that
and rolled out Microsoft Docs. It's been a big improvement, customers are much happier
with the new site, and it's helped create a cohesive platform for all of the teams in
Microsoft to publish their documentation. Wikipedia has a brief article about Microsoft
Docs here (https://en.wikipedia.org/wiki/Microsoft_Docs).

It's a good mental exercise to stop at this point and think about how they did it.
What technology drives Microsoft Docs? Taken another way, if a company wanted to produce
their own documentation site similar to Microsoft Docs, how would they do it?

The first thing to understand is that Microsoft uses, and many other companies have since
begun to adopt, a "docs-as-code" publishing pipeline. This is much different than tools
of the last decade that many technical writers may be familiar with - tools such as
Adobe Framemaker.

Instead of using a proprietary file format like Adobe Framemaker to author documents,
Microsoft Docs uses the open and popular Markdown file format. All of these documents
are open source and accessible via GitHub. Anyone that wants to change a document can
submit a pull request on GitHub for Microsoft to review and (hopefully) accept.

This approach opens the whole document authoring and publishing pipeline to a much wider
audience of users. In essence, they've crowd-sourced the documentation process (though
of course, Microsoft still hires internal tech writers to do most of the writing).

Alright, so far so good. Microsoft has open source Markdown files sitting in GitHub
repos. But now what? A Markdown file in GitHub is a long, long way from the curated,
cohesive document portal that is Microsoft Docs.

In the next step in the process, Microsoft's internal build servers grab the files from
all the projects around the company, and runs them through a static site generator
called DocFX (https://github.com/dotnet/docfx). Remember we talked about static site
generators in the last chapter and how they can be used to produce documentation sites.

So that's it then, right? Microsoft takes the output from DocFX, throws them up on a web
server somewhere, and whala, out comes Microsoft Docs.

Well, no, not really. A company could, in theory, directly publish the static files produced by
DocFX and host them, but that would only work for one web site / project. Microsoft, being
a big company of course, has thousands of projects and teams all over the company. Microsoft
Docs isn't just a portal for ONE project, it's a portal for ALL of them.

There's an extra step in the process that Microsoft doesn't really tell us about. Internally
they have a hosting environment that grabs all of the output from all of the DocFX sites
everywhere, and hosts them in their own internally-built hosting environment / web server.

As we discussed in the last chapter, the hosting environment makes the documents interactive.
Users can create an account and login as themselves, make comments on documents, add documents
to their favorites list, give documents a helpfulness rating, etc. These interactive capabilities
are centrally managed by the hosting environment, not the content in the statically generated 
output files, so content authors don't have to think about how all that happens. It ends up 
being very similar to a wiki, except the files are stored externally instead of being stored 
in the wiki's database.

And so we see that the DocFX static site generator is only part of the process. There's a
missing piece in the form of the hosting environment that forms the totality of Microsoft
Docs. If a company wanted to produce a truly functional Microsoft Docs-like web site, then
they'd need to either build a hosting environment of their own, or find an open source or
commercial tool that can act as such.

The punchline of this chapter then is that, of course, OpenSquiggly is a hosting environment
that can do this sort of thing. Now just to be clear about what we're saying, we're not
saying that OpenSquiggly can do everything that Microsoft Docs can do right now. Microsoft
Docs was designed specifically to serve the needs of Microsoft, and their needs are more
complex than most other companies.

The biggest difference is that OpenSquiggly's structure is limited to navigator-on-the-left /
content-on-the-right structure. Microsoft Docs pages can have page links across the top,
with sub-menus in some cases, and they can also have plain pages that don't have any left-hand
navigator at all, let's call them top-level navigation pages.

The limited navigation options offered by OpenSquiggly is somewhat intentional, and while it
may sound like a limitation, is actually a benefit. Our assumption is that you are linking
to multiple projects all around the company, and you want to build a UNIFIED table of contents
tree from all the content trees of all the projects you are linking to. In order to unify
multiple projects, we need to have a lowest-common-denominator paradigm that all the projects
can follow. If there are too many paradigms (top navigator, sub-menu navigator, top-level
navigation pages, right-hand navigator), then that becomes a more complex endeavor to try to
unify many projects together.

We think this approach works really well for INTERNAL document publishing of technical errata
for software teams. However, if you can live with OpenSquiggly's single navigator / content
paradigm, then there's no reason why you can't also use OpenSquiggly for external document
publishing.

Now with all that said, this is obviously something we're thinking about. In the future we're
considering adding some of the other navigation pardigms we discussed to make OpenSquiggly
a more flexible environment for publishing external content. If any of these topics are of
interest to you, please, get in touch with us and let's talk about your specific needs.


