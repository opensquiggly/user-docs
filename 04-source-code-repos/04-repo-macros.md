---
Order: 4
Title: URL Pattern Macros
---
# Overview
In External Connections and Mount Points, as discussed in the previous sections, there
are two special fields that are treated differently by the system: the Git Repo URL Pattern
and Git View URL Pattern.

These fields can contain macros which are expanded at run time and filled in with a value
from another one of the fields in the record.

Macros begin with the <code>$</code> character.

# List of Macros

<table>
  <tr>
    <th>Macro</th>
    <th>Available in Git Host Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>$PAT</td>
    <td>All</td>
    <td>
      Allows the personal access token specified in the associated credential field
      to be injected into the final URL
    </td>
  </tr>
  <tr>
    <td><code>$ORGNAME</td>
    <td>Azure DevOps</td>
    <td>
      Allows the Azure DevOps organization name specified in the associated field
      to be injected into the final URL
    </td>
  </tr>
  <tr>
    <td><code>$PROJECTNAME</code></td>
    <td>Azure DevOps</td>
    <td>
      Allows the Azure DevOps project name specified in the associated field
      to be injected into the final URL
    </td>
  </tr>
  <tr>
    <td><code>$REPONAME</code></td>
    <td>Azure DevOps, Bitbucket, GitHub</td>
    <td>
      Allows the Azure DevOps project name specified in the associated field
      to be injected into the final URL
    </td>
  </tr>
  <tr>
    <td><code>$USERNAME</code></td>
    <td>Bitbucket</td>
    <td>
      Allows the Bitbucket user name specified in the associated credential field
      to be injected into the final URL. Used when specifying password credentials.
    </td>
  </tr>
  <tr>
    <td><code>$WORKSPACEID</code></td>
    <td>Bitbucket</td>
    <td>
      Allows the Bitbucket workspace id specified in the associated credential field
      to be injected into the final URL. TODO: Review.
    </td>
  </tr>
  <tr>
    <td><code>$OWNERNAME</code></td>
    <td>BitHub, GitLab</td>
    <td>
      Allows the account owner name specified in the associted field
      to be injected into the final URL
    </td>
  </tr>
</table>
