---
Order: 3
Title: Mounting Private Repos
---
# Overview of Private Repositories

Private repositories are repositories that require some type of authentication
credentials in order to clone.

Connecting to private repositories is almost the same as the process for 
connecting to public repositories. Before creating the mount point, we create
an "External Connection" that stores the credentials (which can be either
a personal access token or an OAuth token), and then we specify the desired
external connection when we create the mount point.

# Creating an External Connection

1. Click on your name in the right hand side of the application header bar. This will open
   up the User Options pane.
2. Expand the External Connections section of the User Options form, and press the Add New
   button.
3. In the External Connections form, select the Connection Type to specify what type of
   Git hosting system you are using (Generic Git Host, Azure DevOps, Bitbucket, GitHub,
   or GitLab).
4. Enter the name of the External Connection. This is a short, human readable name of the
   connection that will appear in the selection list in the Mount Point form.
5. Enter the description of the External Connection. This is a longer string of text that
   can help serve as a reminder as to the purpose of the connection.
6. Choose the desired authentication type, either a personal access token / password, or
   OAuth authentication.
   * If you select OAuth authentication, next click the Authorize button and follow the
     OAuth prompts to grant access to your repository.
7. Fill in the remaining fields in the form with the appropriate information.
   The remain fields are specific to the connection type.

# Fields Common to All External Connections

* *Name* - This is a friendly, user-displayed name of the external connection as it will appear in your
  list of active connections.
* *Description* - This is a longer description of the external connection that will help you remember
  the purpose and/or contents of the connection.
* *Git Host Display Name* - When you view within OpenSquiggly, a button link to view the content
  in it's original Git host is displayed in right hand side of the page header. This allows quick,
  convenient acces to the file where it is hosted. The text of the button says "View in XXX" where
  XXX is the name of the Git display name that you enter into this field. For example, if you enter
  "Azure DevOps", then the view button will display "View in Azure DevOps". This field can be
  overridden in the mount point.
* *Git Repo URL Pattern* - This field holds the pattern for how to build the repository URL to
  use for cloning the repository. The pattern can contain macros that will be expanded and runtime
  to the appropriate values. See the Pattern Macros section later in this page. Normally this field
  is filled in with the appropriate default value and you should not need to modify it unless the
  Git hosting system has changed, or you are creating a generic Git host mount point. This field
  can be overridden in the mount point.
* *Git View URL Pattern* - Similar to the URL pattern, this field contains a pattern that is used
  to build the viewing URL when the user clicks the "View in XXX" button. Normally this field is
  filled in with the appropriate defaults. This field can be overridden in the mount point.

# Azure DevOps-Specific Fields
Azure DevOps uses a three-tiered organization of repositories: the organization, project, and
repository. You can specify the default organization name in the external connection, the assumption
being that you will connect to multiple repositories within the same organization. Therefore, the
target organization name can be stored in the external connection so that you don't need to specify
it when you create each mount point.

The project and repository are specified when you create the actual mount point. You can also override
the default organization name in the mount point, although in this case we recommend that you create
one external connection per organization in your Azure DevOps account.

* *Organization Name* - The name of the organization in your Azure DevOps account.

### Default Values for Pattern Fields
* Git Repo URL Pattern
  * Authentication Type = Personal Access Token
  ```
  https://$PAT@dev.azure.com/$ORGNAME/$PROJECTNAME/_git/$REPONAME
  ```
  * Authentication Type = OAuth
  ```
  https://$ORGNAME:$PAT@dev.azure.com/$ORGNAME/$PROJECTNAME/_git/$REPONAME
  ```
* Git View URL Pattern
  ```
  https://dev.azure.com/$REPONAME/_git/$PROJECTNAME?path=$URLENCODED_RELATIVEPATH
  ```
  
# Bitbucket-Specific Fields
Bitbucket uses a two-tiered organization of repositories: the workspace id (for company accounts) or
the username (for individual accounts), and the repository name.

The external connection stores the workspace id or username, while the repository name is specified
later in the mount point. You can override the workspace id / username in the mount point, but we
recommend creating one external connection per workspace id or username.

* *Workspace ID (or Username)* - The workspace id or username of your Bitbucket account. 
Each workspace/username can contain multiple repositories.

### Default Values for Pattern Fields
* Git Repo URL Pattern (Public Repositories)
  * Authentication Type = User Credentials
  ```
  https://$AUTH_USERNAME:$AUTH_PASSWORD@bitbucket.org/$WORKSPACEID/$REPONAME.git
  ```
  * Authentication Type = OAuth
  ```
  https://x-token-auth:$PAT@bitbucket.org/$WORKSPACEID/$REPONAME.git
  ```
* Git View URL Pattern
  ```
  https://bitbucket.org/$WORKSPACEID/$REPONAME/src/master/$URLENCODED_RELATIVEPATH
  ```

# GitHub-Specific Fields
GitHub uses a two-tiered organization of repositories: the owner name, which is either the username
of the account for individual users, or the organization name for company accounts, and the repository
name.

The external connection stores the owner name, while the repository name is specified
later in the mount point. You can override the owner name in the mount point, but we
recommend creating one external connection per owner name.

* *Owner Name* - The username or organization name of the GitHub account.

### Default Values for Pattern Fields
* Git Repo URL Pattern (Public Repositories)
  ```
  https://$PAT@github.com/$OWNERNAME/$REPONAME.git
  ```
* Git View URL Pattern
  ```
  https://github.com/$OWNERNAME/$REPONAME/blob/master/$URLENCODED_RELATIVEPATH
  ```

# GitLab-Specific Fields
GitHub uses a two-tiered organization of repositories: the owner or group name, which is either the
name of the account for individual users, or the name of the group for company accounts, and the
"project slug" which represents the repository. In GitLab, a project is a repository.

The external connection stores the owner name, while the project slug is specified
later in the mount point. You can override the owner name in the mount point, but we
recommend creating one external connection per owner name.

* *Owner Name* - The username or group name of the account on GitLab.

### Default Values for Pattern Fields
* Git Repo URL Pattern (Public Repositories)
  ```
  https://oauth2:$PAT@gitlab.com/$OWNERNAME/$PROJECTSLUG.git
  ```
* Git View URL Pattern
  ```
  https://gitlab.com/$OWNERNAME/$PROJECTSLUG/-/tree/main/$URLENCODED_RELATIVEPATH
  ```

# External Connections for Generic Git Hosts

External connections for generic git hosts can also be created to store a personal access token to
access the desired Git repository.

There are no connection type specific fields to fill out, such as the organization
name, repository name, project name, workspace ID, or owner name.

This means that these fields are not available to be injected into the Git Repo URL Pattern
and Git View URL Pattern fields via macros ($ORGNAME, $REPONAME, etc.), and you must therefore fill in
these full, raw Git Repo URL as provided by your Git hosting system.

The only macros that are valid for a generic external connection Git host are $PAT, $RELATIVE_PATH, and 
$URLENCODED_RELATIVEPATH that you can use in the Git View URL Pattern field.

# General Instructions for Mounting Private Repositories

1. Click on your name in the right hand side of the application header bar. This will open
   up the User Options pane.
2. Expand the Mount Points section of the User Options form.
3. In the Mount Points form, select Private in the Git Access Type dropdown field.
4. In the External Connection dropdown, pick the external connection you previously created that
   contains your connection credentials to the desired Git host.
5. Fill in the remaining fields in the form with the appropriate information.

# Fields Common to All Private Connections

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

# Completing the Form

Fill in the remaining Git-host specific forms, depending on the Git hosting system you are targeting.

Note that in certain cases you'll be able to override information that was specified in the
External Connection.
