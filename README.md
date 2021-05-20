# SharePoint User Custom Hover Card
The default experience within the *GCC High* and *DoD* clouds for SharePoint Online does not show a hover card for users.  This code repository provides working JSON column formatting to add a useful hover card.

## Commercial Experience ##
What you see in the *Commercial* and *GCC* cloud environments when hovering over a user is something like this:
![Example of person card](https://docs.microsoft.com/en-us/sharepoint/dev/images/hoverimage-4.png)

## US Federal Government Experience ##
What you see in the *GCC High* and *DoD* cloud environments is...
> Well, **no hover card** at all. And that's what this repo is addressing.

### Desired End Result ###
This is an example of what this solution provides:

![Result of this solution](https://github.com/mikevasiloff/sp-hover-card/blob/main/PersonCard.png?raw=true)
> Note that if you are browsing from a DoD network you probably won't be able to see the above image 😟

## Solution Composition ##
This is a very simple solution using the [column formatting](https://docs.microsoft.com/en-us/sharepoint/dev/declarative-customization/column-formatting) feature of SharePoint which lets you "customize how fields in SharePoint lists and libraries are displayed". This is accomplished by constructing a JSON object that describes the elements and styles that are displayed when a field is shown in a view, and part of this includes the ability to create a custom hover card.

Unfortunately, there are some limitations with this feature. You are unable to:
* Access the phone #, location/office, and most other user profile property values
* Make the text in the hover card selectable/highlightable
* Use URI schemes such as sip: or msteams: to add a "💬 Chat" option
* Use any JavaScript for custom functionality

## Deployment ##
You have a few options for how you can apply this JSON formatting.

### Option #1 ###
You can apply it to the "Created By" and "Modified By" fields across an entire site collection by browsing to:

**For the "Created By" Field**
> {YourSiteUrl}/_layouts/15/FldEditEx.aspx?field=Author

**For the "Modified By" Field**
> {YourSiteUrl}/_layouts/15/FldEditEx.aspx?field=Editor

1. Then scroll down to the *Column Formatting* section
2. Paste in the JSON from the [AuthorEditorField.json](https://github.com/mikevasiloff/sp-hover-card/blob/main/AuthorEditorField.json) file
3. Ensure  *Update all list columns* is set to *Yes*, and then click OK

> **NOTE:** You will not be able to use this approach on "NoScript" sites such as the backend SharePoint sites for a Team. You'll need to use Option #2 instead.

### Option #2 ###
1. Open the list(s)/library(ies) you want it applied to
2. Ensure the field (Created/Modified By) is shown in the view
3. Click on the field's header title > *Column settings* > *Format this column*
4. Click the Advanced mode at the bottom, and overwrite it with the JSON from the [AuthorEditorField.json](https://github.com/mikevasiloff/sp-hover-card/blob/main/AuthorEditorField.json) file
5. Click the Save button

## Future Changes ##
I also have a modified version of this that I'm still refining for **custom** People/Group fields where you could have a person or a group be shown. Once completed I'll add that to this page as well.
