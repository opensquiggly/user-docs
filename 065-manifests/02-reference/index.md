---
weight: 20
Order: 2
Title: Manifest File Reference
description: Describes the format of the manifest file and the kinds of resources it can contain.
---

## File Format

Manifest files are YAML-formatted files. The file can contain multiple resource definitions, with the
type of each resource definition specified by the ```kind``` property. Separate each resource definition 
with three dashes.

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

```
  public string Name { get; set; }
  public string GitType { get; set; }
  public string AccessType { get; set; }
  public string Connection { get; set; }
  public string ConnectionName { get; set; }
  public string InnerMountPointName { get; set; }
  public string Description { get; set; }
  public string StartPath { get; set; }
  public string TreeFormatter { get; set; }
  public string Username { get; set; }
  public string OrgName { get; set; }
  public string ProjectName { get; set; }
  public string RepoName { get; set; }
  public string MappedPageName { get; set; }
  public string ParentPageName { get; set; }
```  