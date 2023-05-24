---
Order: 2
Title: Mounting Public Repos
---
# About Public Repositories

When we say a "public repository" we mean to say a repository that can be connected and cloned
anonymously, without specifying any user name, password, or access token  credentials.

OpenSquiggly supports four Git hosting systems by name:

* Azure DevOps (by Microsoft)
* Bitbucket (by Atlassian)
* GitHub
* GitLab

as well as a "generic" Git host connection type that can be used to connect to any other Git
hosting system other than the four mentioned above. Connecting to a generic Git host is almost
as easy as connecting to one of the named Git hosting systems - you just need to specify a little
bit of extra metadata so that we can know how to clone the repository and access it's files via
a web interface.

In this way OpenSquiggly can use any Git hosting system, so long as your OpenSquiggly instance is
able to access your Git system via an HTTP/HTTPS URL.

# General Instructions for Mounting Repositories

1. Click on your name in the right hand side of the application header bar. This will open
   up the User Options pane.
2. Expand the Mount Points section of the User Options form.
3. In the Mount Points form, select Public or Private in the Git Access Type dropdown. For this
   chapter, we'll assume you've selected Public to connect to a public repository.
4. In the Connection Type dropdown, select the Git hosting type you wish to connect to..
5. Fill in the remaining fields in the form with the appropriate information.

See the remaining sections of this chapter for more information on each mount point field.

# Fields Common to All Public Connections Types

* *Name* - This is a friendly, user-displayed name of the mount point as it will appear in your
  list of active mount points.
* *Description* - This is a longer description of the mount point that will help you remember
  the purpose and/or contents of the mount point.
* *Start Path* - This is the starting, or root path of the repository where you want the mount
  point to start within the repository folder structure. Use the "/" character as a separator
  between each part of the path. For source code repositories, we assume you want to see the
  entire mount point starting at the root of the repository. Therefore, you should enter at
  Start Path of "/" (without the double quotes of course). However, if for some reason you wanted
  the mount point to only contain a portion of the repository starting at a particular folder
  location, you could enter the desired starting path.
* *Tree Format Type* - We discussed this field in the prior chapter. For mounting source code
  repositories, choose the Raw Files and Folders tree format type.
* *Git Host Display Name* - When you view within OpenSquiggly, a button link to view the content
  in it's original Git host is displayed in right hand side of the page header. This allows quick,
  convenient acces to the file where it is hosted. The text of the button says "View in XXX" where
  XXX is the name of the Git display name that you enter into this field. For example, if you enter
  "Azure DevOps", then the view button will display "View in Azure DevOps".
* *Git Repo URL Pattern* - This field holds the pattern for how to build the repository URL to
  use for cloning the repository. The pattern can contain macros that will be expanded and runtime
  to the appropriate values. See the Pattern Macros section later in this page. Normally this field
  is filled in with the appropriate default value and you should not need to modify it unless the
  Git hosting system has changed, or you are creating a generic Git host mount point.
* *Git View URL Pattern* - Similar to the URL pattern, this field contains a pattern that is used
  to build the viewing URL when the user clicks the "View in XXX" button. Normally this field is
  filled in with the appropriate defaults.
* *Refresh Type* - Reserved for future use.
* *Polling Interval* - Reserved for future use.

# Azure Devops-Specific Fields

Azure DevOps uses a three-tiered organization of repositories: the organization, project, and
repository.

* *Organization Name* - The name of the organization in your Azure DevOps account. In Azure DevOps,
  each organization can contain multiple projects.
* *Project Name* - The name of the project in your Azure DevOps account. Each project can contain
  multiple repositories.
* *Repository Name* - The name of the repository in your Azure DevOps account.

### Default Values for Pattern Fields
* Git Repo URL Pattern (Public Repositories)
  ```
  TODO: Verify this, might be a bug ... why is $PROJECTNAME not in here?
  https://$ORGNAME@dev.azure.com/$ORGNAME/$REPONAME/_git/$REPONAME
  ```
* Git View URL Pattern
  ```
  https://dev.azure.com/$REPONAME/_git/$PROJECTNAME?path=$URLENCODED_RELATIVEPATH
  ```

# Bitbucket-Specific Fields
Bitbucket uses a two-tiered organization of repositories: the workspace id (for company accounts) or
the username (for individual accounts), and the repository name.

* *Workspace ID (or Username)* - The workspace id or username of your Bitbucket account. Each 
  workspace/username can contain multiple repositories.
* *Repository Name* - The name of the repository in the Bitbucket account.

### Default Values for Pattern Fields
* Git Repo URL Pattern (Public Repositories)
  ```
  https://bitbucket.org/$WORKSPACEID/$REPONAME
  ```
* Git View URL Pattern
  ```
  TODO
  ```

# GitHub-Specific Fields
GitHub uses a two-tiered organization of repositories: the owner name, which is either the username
of the account for individual users, or the organization name for company accounts, and the repository
name.

* *Owner Name* - The username or organization name of the GitHub account. Each account can have
  multiple repositories.
* *Repository Name* - The name of the repository in GitHub.

### Default Values for Pattern Fields
* Git Repo URL Pattern (Public Repositories)
  ```
  https://github.com/$OWNERNAME/$REPONAME
  ```
* Git View URL Pattern
  ```
  TODO
  ```

# GitLab-Specific Fields
GitHub uses a two-tiered organization of repositories: the owner or group name, which is either the
name of the account for individual users, or the name of the group for company accounts, and the
"project slug" which represents the repository. In GitLab, a project is a repository.

* *Owner Name* - The username or group name of the account on GitLab.
* *Repository Name* - The project slug of the repository. TODO: Should rename this field to "Project Slug"
  to match the GitLab vernacular.

### Default Values for Pattern Fields
* Git Repo URL Pattern (Public Repositories)
  ```
  https://gitlab.com/$OWNERNAME/$PROJECTSLUG
  ```
* Git View URL Pattern
  ```
  TODO
  ```

# Filling in Fields for Generic Git Hosts

For a generic Git host, there are no connection type specific fields to fill out, such as the organization
name, repository name, project name, workspace ID, or owner name.

However, this means that these fields are not available to be injected into the Git Repo URL Pattern
and Git View URL Pattern fields via macros ($ORGNAME, $REPONAME, etc.), and you must therefore fill in 
these full, raw Git Repo URL as provided by your Git hosting system.

The only macros that are valid for a generic public Git host are $RELATIVE_PATH and $URLENCODED_RELATIVEPATH
that you can use in the Git View URL Pattern field.

For private connections to generic Git hosts you can also use the $USERNAME, $PASSWORD, and $PAT macros to
reference the username, password, and personal access token values from the External Connection. 
