---
weight: 20
Order: 2
url: /docs/mount-points/doc-repos/ssgs
Title: Compared with Static Sites
description: >
  In this section we compare how OpenSquiggly's built-in document formatter can
  be used as an alternative to static site generators for building documentation
  sites.
---
## Why OpenSquiggly for Documentation?

Now might be a good time for a brief comparison with some other document formatting
options. The biggest alternatives to OpenSquiggly are static site generators.

Some examples of static site generators are:

* Hugo
* MkDocs
* Sphinx
* DocFX

and many others not listed here.

A static site generator will take a document tree and transform all of the files all
at once into a static site containing HTML files. These HTML files can then be hosted
on a web server somewhere of your choosing.

By contrast, OpenSquiggly does very much the same thing, except instead of transforming
the files all at once, it transforms them dynamically as-needed when the user reads the
content.

What we're aiming for is a much more convenient set up and documentation publishing workflow.

## Life without OpenSquiggly

To highlight this last point, let's conduct a thought experiment of what it might be like
to get your team to adopt a documentation initiative driven by a static site generator.

Imagine you are a staff level software developer working inside a company of a few thousand
people. You recognize that your project needs some good internal documentation for your team
to be effective. You look around the organization for guidance on how you might go about
doing so, but you quickly realize that there is no single documentation standard used by
other software development teams in your organization. Some teams have no documentation at
all, while other teams have at least tried to create some documentation using a corporate
wiki. A corporate wiki isn't really what you're looking for though - you want to store documents
inside your Git repositories, where they can be operated on using all the tools that the
developers on your team are already using.

Therefore, you decide to embark on a documentation initiative of your own. You talk to your
manager about it, who doesn't fully buy into what you want to do, but at least agrees to 
let you use some of your 20% time to work on it.

Since you've never heard of OpenSquiggly, the only tools you know that can do something like
this are static site generators. You put in a considerable amount of research, investigating
the pros and cons of each tool, and finally pick the one you think is best for you.

You get it all running on your local desktop, and sure enough, it generates some HTML output
for you. You want to actually see the formatted documentation, so you install Apache locally
on your desktop, point it at your statically generated HTML, and behold, you have a documentation
site. Great.

Now what? Now that you've proven the concept you want to get your team to adopt it. But how
do you do that? You've got to tie the scripts that run your static site generator into the
team's continuous integration server so your documents can get built every time your developers
check in new files.

But now you have a little bit of a problem. You don't actually control the continuous integration
server. That's done by a whole separate DevOps group, and now you've gotta go talk to them to
convince them to add your build step into the process. And maybe it's not that simple. There's
work requests that need to be logged, approvals that need to be signed off on, compliance
measures that need to be tracked and monitored, etc. This is starting to chew up a lot of your
20% time, and there's no guarantee of success. You are at the mercy of others to do things for
you.

Eventually you persevere through whatever needs to be done, and a few days or weeks later, you
finally have your static site generator running as part of the team's CI server. Great.

Now what? All that build step has done is run the static site generator and tossed your statically
generated HTML output into a folder somewhere. You go back to the DevOps team and after a little
bit of back-and-forth, you finally figured out where the CI server actually put your documents.

But that's not enough. You need to get those files deployed out to a web server somewhere that's
going to serve up the files so that your team can read them. How do you do that?

You're not actually sure, so you've gotta do some more sleuthing around the organization to
figure out who you need to talk to to make that happen. Can you deploy the files to GitHub Pages?
Netlify? Amazon? What about access privileges? What about the hosting costs? Etc.

Eventually you land at the desk of someone on the Cloud Architecture team who might be able to
help you. Of course he tells you that you need more approvals and budget sign offs. It's kind 
of hard to get that done, considering that this is an experimental skunkworks project that you're
running on your 20% time. But once again you persevere, pull some strings, call in some favors,
and at last you have a behind-the-firewall documentation site running that anyone within the
organization can access, and no one outside the organization can access.

Okay, you're making progress.

Now you want readers to be able to perform searches on the documentation. How do you do that?
Well there are various techniques to make your SSG site searchable. The preferred method these
days is to use an external service that will index the site for you. This is a big problem
though, since the search service you've found runs in the cloud, and therefore can't access
your behind-the-firewall documentation site. This is beyond the scope of your 20% time project
so you decide to stop here, show your manager what you've got, and hope he'll give you some
real time and a real budget to work on it.

You've made some progress but you're still a long way from getting what OpenSquiggly will
give you:

* Source code and documentation living together in one site
* Pulling together source code and documentation from multiple Git hosting systems
* Regular expression-based searching of source code and documentation
* Class-and-method level reference documentation
* Authenticated access with user self-registration
* Mixing together externally hosted and internally authored documenation
* An interactive document tree that let's your users customize, create bookmarks, etc.

In addition to the missing features, all you will have done is created a standalone island
of documentation for your team. Your equally motivated cohorts on all the rest of the teams
in the organization will need to repeat all of the work you've done, inevitiable making 
different decisions than you made along the way, the end result being a patch quilt of
documentation sites scattered around the organization. There will be no unified documentation
site that provides a set of common services for everyone in the organization.

In summary, there is a lot of work and steps involved in getting a fully featured documentation
site up and running. Using an SSG is a viable option, but it is only one part of the overall
publishing pipeline and workflow. OpenSquiggly combines all of these steps into a single tool that can
do the job.

## Life with OpenSquiggly

Let's take the same scerio now and add OpenSquiggly into the mix.

You talk to your manager and get the same 20% time as before.

But now you have two viable options for using OpenSquiggly that can help you make much
better use of your precious 20% time:

* You can install the personal edition of OpenSquiggly on your desktop
* You can create an account on the cloud-based shared portal

In a very short amount of time you can have a fully featured knowledge base consisting of
source code, architecture documents, and reference documentation, pulled together from 
repositories living in different Git hosting systems around the organization. There is no
need to get the DevOps team involved, since all of the required document processing is
built into OpenSquiggly itself, and there is no need for you to beg at the desk of the
Cloud Architecture team to get them to help you with deployment.

You show it to your manager, who finally has the "aha!!!" moment you've been hoping for
because she can now see the value of what you've been campaigning for all along.

Other teams get wind of what you're doing, they get jealous, and they start using it too.
Everyone is starting to fire on all cylinders. Developers are happy and project work is
starting to get done more efficiently.

It doesn't take very long before this idea bubbles up to the CTO. He sees what the teams
are doing and agrees its a great way to get the whole company to adopt a stanard methodogly
for documentation among all the software teams in the organization.

But the CTO decides that he wants a private instance instead of the shared instance. Given
the clout that he has, he easily commands a sitdown with the entire Cloud Architecture team.
It's no longer just you begging at the feet of other engineers in the organization to help
you - you've now got the CTO doing your bidding for you.

They debate the benefit of using a cloud hosted private instance vs. a self-managed private
instance. The Cloud Architecture team says they're willing to do it, but after further 
discussion, they decide to let us manage their private instance for them. They sign up for
our hosted private instance plan, and make it available to all teams in the organization.
Adoption is technically voluntary, but teams are highly encouraged to use this system for
their documentation teams, versus inventing their own documentation workflow for each project.

Within six months, every team in the organization has adopted OpenSquiggly, not because they
were forced to, but because it provides so much value and is so easy to adopt that it
becomes a no-brainer decision for every software project team in the company. After a year
or so of widespread adoption, the CTO decides to do what has already become the de facto
decision in the organization; teams are now required to publish their documentation using
OpenSquiggly.

Life within the organization is now beautifully efficient. Any developer that needs to 
coordinate or integrate with any other team in the organization has a single site that they
can go to for documentation, source code, or reference material within the entire organization.
Bugs that have been buried in backlogs for years suddenly start falling away as the increased
communication and coordination allows a "connecting of the dots" in ways never before possible.

Everyone lives happily everafter.

## Summary

|                                 | Without OpenSquiggly                        | With OpenSquiggly                                                                                                                                                                                               |
|---------------------------------|---------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Time you scam from your manager | 20%                                         | 20%                                                                                                                                                                                                             |
| Document Formatter              | SSG you pick after research                 | Built into OpenSquiggly                                                                                                                                                                                         |
| Viewing Documents for Demo      | Apache installed locally                    | Built into OpenSquiggly                                                                                                                                                                                         |
| Continuous document processing  | Beg the DevOps team to help you             | Built into OpenSquiggly                                                                                                                                                                                         |
| Deployment of documents for team | Beg the Cloud Architecture team to help you | OpenSquiggly Cloud Hosted Instance                                                                                                                                                                              |
| Document searching               | Beyond the scope of 20% time                | Built into OpenSquiggly                                                                                                                                                                                         |
| User authentication / self-registration | Beyond the scope of 20% time                | Built into OpenSquiggly                                                                                                                                                                                         |
| Other goodies | Beyond the scope of 20% time                | Built into OpenSquiggly                                                                                                                                                                                         |
| Adoption by other teams | Doesn't happen                              | Happens organically by word-of-mouth                                                                                                                                                                            |
| Adoption by entire company | Doesn't happen                              | (1) Keep using shared instance, or (2) CTO approves purchase of cloud-hosted private instance, or (3) CTO uses his clout the get the Cloud Architecture team to install a self-managed instance of OpenSquiggly |
| Life Everafter | Same ole disjointed corporate bureaucracy   | Perfect harmony |
