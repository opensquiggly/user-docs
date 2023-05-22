---
Order: 1
Title: Public Portal
---
# For Evaluation Purposes Only

IMPORTANT: OUR CLOUD HOSTED SHARED PORTAL IS CURRENTLY RECOMMENDED FOR EVALUATION PURPOSES ONLY.

This is mainly because we do not yet have an elastically scalable system that can handle huge
volumes of users, in terms of computing power, network bandwidth, and disk space.

Because we can't anticipate in advance how many repositories users will attach to their accounts on
the shared portal, we don't have a good way of guaranteeing that the portal won't arbitrarily run
out of disk space. We reserve the right to impose quota limits and/or remove repositories from
accounts to conserve disk space (though we try hard not to do that).

Please try to use the system respectfully and don't attach large numbers of repositories beyond
what is necessary to try out OpenSquiggly on your project.

Once you've satisfied yourself that OpenSquiggly will work well for your team, please consider
installing your own self-managed portal, or contact us about setting up a private portal.

# Cloud Hosted Shared Portal

The fastest and easiest way for an individual user or small team of users to get started with OpenSquiggly
is to sign up for an account at https://app.opensquiggly.com, our shared portal available for self-registration.

There is nothing for you to set up or install. We manage all of the cloud resources, disk space, software
dependencies, and document indexing. Your personal data can only be accessed by you using your user id and
password login credentials, or by your organization if you created an organization account (see xxx for
more information about organization accounts).

It is important to note, however, that while your data is secured by our authentication, authorization, and
encryption systems, it is still stored on a shared database instance and shared document indexing instance, 
where your data is stored alongside other users.

Some security conscious users may want additional security over and above what is offered through our shared 
hosting plans. For those users, we offer several additional options.

An individual user who wants completely private access to their data can download the desktop edition of our
software and install it on their own system using their own disk space. This is a good option for users who
need a private note-taking and document organizational system, and aren't interested in sharing or accessing
content with other users in their organization.

Organizations that need a more secure hosting option can choose between our cloud hosted private portal and
self-managed private portal plans. It's fine to use the shared portal even for an organization account, but
if you need your data stored in a completely private database separate from any other users, then you'll want
to consider one of these two plans.

See the remaining sections of this chapter for more information on each plan to help you pick the right
plan for your needs.

One last thing: if you sign up for the cloud hosted shared portal and later decide that you need another
hosting option, we have utilities available to help you migrate your data to the new plan. So don't worry!!
Give our shared portal a chance, even if it's just to kick the tires and experiment with what the system
can do for you.

# Signing Up for a Cloud Hosted Account

To create a user on the shared portal, simply visit https://app.opensquiggly.com and follow the sign up
instructions.

## Getting an Invitation Code

If the system is still on the early access plan when you sign up, you may be asked for an invitation code. 
To receive an invitation code, click on the link in the sign in page and enter your e-mail address. Use the
invitation code sent to your e-mail address to continue the sign up process. Be sure to check your spam
folder for the invitation code to make sure your e-mail system didn't flag it for you.

## Creating an Account

Once you have the invitation code, complete the sign up process by entering your e-mail address, login id,
name, and password.

IMPORTANT: Be sure to remember and use your LOGIN ID when you sign in. Don't use your e-mail address as the
login id - it won't work. The reason why we do it this way is because we allow you to create multiple accounts
with the same e-mail address. Therefore, the LOGIN ID is the only thing that we can be sure is unique.

## Signing In

After you've created your account, sign in using your LOGIN ID and PASSWORD. From here you'll be taken to your
Home page, which is the root page from which you navigate to all your documents.

## Resetting Forgotten Passwords

If you've forgotten your password, click on the "Forgot your password" link near the bottom of the
sign in form.

The Reset Password form will open. Enter your login id or e-mail address of the account for wish to
reset your password. Note that while you can enter either your login id or e-mail address here, be sure
to use your actual login id (not your e-mail address) after you reset the password and are ready to log in.

You will receive an e-mail containing a link to reset your password. Click on the link and enter a new
password, and a second time to confirm it. After resetting your password, go back to the sign in page and
login with your login id and new password.

# Next Steps

Initially your Home Page will be completely empty until you add documents to your navigator, but it doesn't need
to stay that way for very long. Because we allow you to quickly connect your account to source code repositories
and documentation stored in externally hosted Git repositories (Azure DevOps, Bitbucket, GitHub, and GitLab),
your account can very quickly be populated with many thousands of source code files and documents for you to 
start doing deep, focused work on your project!

To learn how to use OpenSquiggly as a wiki and author documents directly within the OpenSquiggly system, see
the chapter titled "Document Authoring".

To learn how to connect your account to external source code repositories, see the chapter titled "Connecting to
Source Code Repositories".

To learn how to connect your account to external documentation repositories, see the chapter titled "Connecting to
Document Repositories".

Once you've added a bunch of files and documents to your account, you'll probably want to organize and manage
them so you can find them easily. To learn more about using the document navigator and managing your overall
document structure, see the chapter titled "Managing the Navigator".

That should be enough to get you out of the starting gate and using OpenSquiggly in earnest. We've designed
OpenSquiggly with an eye for making life better for software developers. We sincerely hope that you enjoy 
using OpenSquiggly and can begin using it to do your best work and make positive impacts on your projects
and for your customers.


