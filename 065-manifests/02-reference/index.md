---
weight: 20
Order: 2
url: /docs/manifests/reference
Title: Manifest File Reference
description: Describes the format of the manifest file and the kinds of resources it can contain.
---

## File Format

Manifest files are YAML-formatted files. The file can contain multiple resource definitions, with the
type of each resource definition specified by the ```kind``` property. Separate each resource definition 
with three dashes.

Resources to create are identified by a ```kind``` and a ```name```. Note that if the resource already exists
(by a matching name) when the import runs, it will be skipped. This is convenient as it allows the same
manifest file to be reimported if new items are added to it.

However, existing resources that do not match anything in the manifest file WILL NOT be deleted. Manifest
imports are always non-destructive.

## kind: topicPage

Used to generate topic pages from the manifest file.

<table>
  <tr>
    <th>Property Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>name</td>
    <td>The name of the topic page to be created</td>
  </tr>
    <td>parentPageName</td>
    <td>
      The name of the topic page's primary parent within the document tree.
      If omitted, the topic page will be created underneath the users Home page.
    </td>
  </tr>
</table>

### Examples:

```
kind: topicPage
name: OpenSquiggly
---
kind: topicPage
name: Archived Work
parentPageName: OpenSquiggly
---
kind: topicPage
name: Current Work
parentPageName: OpenSquiggly
```

## kind: mountPoint

<table>
  <tr>
    <th>Property Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>name</td>
    <td>The name of the mount point to create</td>
  </tr>
  <tr>
    <td>gitType</td>
    <td>
      The type Git hosting system that stores the target repository.<br>
      <code>azure-devops</code><br>
      <code>bitbucket</code><br>
      <code>github</code><br>
      <code>gitlab</code><br>
      <code>generic</code><br>
    </td>
  </tr>
  <tr>
    <td>accessType</td>
    <td>
      Specifies the type of access to use for the repository.<br>
      <code>public</code> - Repository is publicly accessible; no credentials required<br>
      <code>private</code> - Repository is private; use credentials provided by the connection specified by <code>connectionName</code><br>
      <code>reuse</code> - Reuse an existing repository
    </td>
  </tr>
  <tr>
    <td>connection</td>
    <td>
      If <code>connection=self</code> is specified when accessing a private repository, then the credentials
      used will be from the same external connection as that of the manifest file mount point. This setting
      is convenient for connecting to private repositories residing on the same Git account as the manifest
      mount point without needing to create a store additional external connections.
      <br><br>
      If this property is omitted, then specify the desired external connection in the <code>connectionName</code>
      property.
    </td>
  </tr>
  <tr>
    <td>connectionName</td>
    <td>
      When <code>accessType=private</code> and <code>connection=self</code> is not specified, enter the
      name of the external connection that contains the credentials. Note that for security reasons manifest
      files cannot create external connections. You need to create the external connections needed by the
      manifest before importing the manifest.
    </td>
  </tr>
  <tr>
    <td>innerMountPointName</td>
    <td>
      When <code>accessType=reuse</code>,  specify the name of underlying mount point you are reusing.
    </td>
  </tr>
  <tr>
    <td>description</td>
    <td>The description for the mount point (optional).</td>
  </tr>
  <tr>
    <td>startPath</td>
    <td>
      The startingPath of where to retrieve files within the mounted
      repository. The default is <code>/</code> (i.e., the root).
    </td>
  </tr>   
  <tr>
    <td>treeFormatter</td>
    <td>
      The desired tree formatter for the mount point.<br>
      <code>raw</code> - Display raw file and folder names.<br>
      <code>doc</code> - Use the OpenSquiggly document tree formatter to display a processed, formatted
      view of the documents. See <a href="/docs/mount-points/doc-repos/intro">here</a> for more details.
    </td>
  </tr>
  <tr>
    <td>username</td>
    <td>
      The user name or group name of the account on the Git hosting system.
    </td>
  </tr>
  <tr>
    <td>orgName</td>
    <td>
      The organization name on the Git hosting system. Used by Azure DevOps.
    </td>
  </tr>
  <tr>
    <td>projectName</td>
    <td>
      The project name on the Git hosting system. Used by Azure DevOps.
    </td>
  </tr>
  <tr>
    <td>repoName</td>
    <td>
      The repository name.
    </td>
  </tr>
  <tr>
    <td>mappedPageName</td>
    <td>
      To create a mapped page in the document tree corresponding to the mount point,
      enter the name of the mapped page here. If omitted, a mapped page will not be
      created for the mount point.
    </td>
  </tr>
  <tr>
    <td>parentPageName</td>
    <td>
      When a mapped page is specified, this property specifies the desired parent page
      for the new mapped page. If mappedPageName is omitted, this propert is ignored.
    </td>
  </tr>
</table>

### Examples:

```
kind: mountPoint
name: OpenSquiggly Source Code
gitType: azure-devops
accessType: private
connection: self
description: Optional description here
startPath: /
treeFormatter: raw
projectName: OpenSquiggly
repoName: OpenSquiggly
mappedPageName: Full Source
parentPageName: OpenSquiggly
---
kind: mountPoint
name: OpenSquiggly Documentation
accessType: reuse
innerMountPointName: OpenSquiggly Source Code
description: Optional
startPath: /docs
treeFormatter: doc
mappedPageName: Documentation
parentPageName: OpenSquiggly
---
kind: mountPoint
name: OpenSquiggly Deploy
gitType: azure-devops
accessType: private
connection: self
startPath: /
treeFormatter: raw
projectName: OpenSquiggly
repoName: OpenSquigglyDeploy
mappedPageName: Deployment Repo
parentPageName: OpenSquiggly
---
kind: mountPoint
name: OpenSquiggly Web Site Source
gitType: github
accessType: private
connectionName: GitHub OpenSquiggly
startPath: /
treeFormatter: raw
repoName: opensquiggly.com
mappedPageName: Web Site Source
parentPageName: OpenSquiggly
---
kind: mountPoint
name: OpenSquiggly User Docs
accessType: reuse
innerMountPointName: OpenSquiggly Web Site Source
startPath: /Source/opensquiggly.com/input/docs/user-docs
treeFormatter: doc
mappedPageName: User Documentation
parentPageName: OpenSquiggly
```