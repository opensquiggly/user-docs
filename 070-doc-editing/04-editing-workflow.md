---
weight: 40
Order: 4
Title: Page Editing Workflow
description: This section describes the general workflow for editing pages and the various actions the user can perform.
---
## Overview

To edit a page, click the "Edit Page" icon (the Pencil icon) in the right hand side of that page header.

To return to view mode after editing, click the "View Page" icon (the Eyeball icon).

Note that there is no "Save" button. Changes are saved to the page as soon as you append a new
snippet or save changes to an existing snippet.

## Appending Text to a Page

Click the Add icon (+ sign) in the page header to expand the content editor at the bottom section.
The page is split into two sections with a snippet previewer in the top pane and the content editor
in the bottom pane.

Select the Append Text tab in the content editor.

You have five different text formats to use. We recommend using Markdown in most cases. We will
cover each text format type, and the purpose of each, in a later section.

When you've completed writing the text snippet, click the Add or Add & Close buttons at the bottom
of the content editor.

The new text snippet will be appended to the bottom of the page.

## Inserting Text within the Page

To insert text, first append a new text snippet to the page, then use the gripper icon to drag the
snippet with your mouse and move it to the desired location within the document.

In the future we will add the ability to insert snippets directly within the page at desired locations.

## Editing Existing Text

Notice the three icons in the highlighted left margin of the page. Click the Pencil icon in the
row associated with the snippet you wish to edit.

Edit the text content in the content editor pane and press Update or Update & Close.

## Deleting Text

In the highlighted left margin of the page, click the Delete icon (the X icon) in the row associated
with the snippet you wish to delete.

Confirm the deletion process by clicking OK at the confirmation prompt.

Question: Is there a way to recover deleted text? Is there a way to permanently delete deleted snippets.

## Rearranging Snippets

In the highligted left margin, click and hold the mouse on the Gripper icon in the row associated
with the snippet you wish to move.

While holding the left mouse button down, drag the snippet up or down on the page to the new location
you wish to place the snippet, and release the mouse button.

## Hyperlinks

??? Should this section be here ???

Need to discuss URL slugs.

## Embedding Images

??? Should this section be here ???

This is different between internal authoring and externally hosted.

Do we allow the user to reference an attached file within the Markdown. I don't think we allow
this right now. The user must embed the file by uploading it.

Tried it. There is no way to reference the image from Markdown because there is no way to add
an URL slug to the image. I should add this to the backlog.

Also, file uploads are limited to certain sizes, which are annoying, and fail without returning
any error to the user.

## Embedding Files

??? Should this section be here ???

The user should be able to upload a file and "hide" it. There needs to be a show hidden / not hidden
toggle button or check box. One attribute of a file needs to indicate whether to hide the file on 
the page or not.

Users should be able to reference the file from their Markdown regardless of whether it is hidden
or not.
