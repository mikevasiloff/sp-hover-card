# SharePoint User Custom Hover Card
> **June 2022 Update**: Somewhere between April 2022 and June 15th Microsoft updated the _GCC High_ and _DoD_ clouds to support the _native_ person hover experience.  As a result this solution is no longer needed.

Original (now outdated) article content is below with some strike-throughs were applicable:

~~The default experience within the *GCC High* and *DoD* clouds for SharePoint Online does not show a hover card for users.~~  This code repository provides working JSON column formatting to add a useful hover card.

## Commercial Experience ##
What you see in the *Commercial* and *GCC* cloud environments when hovering over a user is something like this:
![Example of person card](https://docs.microsoft.com/en-us/sharepoint/dev/images/hoverimage-4.png)

## US Federal Government Experience ##
What you see in the *GCC High* and *DoD* cloud environments is...
> ~~Well, **no hover card** at all. And that's what this repo is addressing.~~

### Desired End Result ###
This is an example of what this solution provides:

![Result of this solution](https://user-images.githubusercontent.com/8918397/118977860-ebe70f00-b976-11eb-9023-a7f6a4aa5313.png)

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

## Other Person/Group Fields ##
There's a separate [PersonGroupField](https://github.com/mikevasiloff/sp-hover-card/blob/main/PersonGroupField.json) file to handle the extra complexities that custom Person/Group fields can introduce, such as:
* SharePoint Groups (shows a "View Members" button)
* AD Security Groups
* Office 365 Groups (shows the group's profile pic)
* Multiple entries/selections (shows cards stacked on top of each other)

### Caveats ###
Please be aware of the following items:
1. When the person/group field allows multiple entries it does **not** provide values for Department or JobTitle
2. Rendering Office 365 Group profile pics is handled via OWA and the file is already set with the DoD URL. To use within **GCC High** change [PersonGroupField line 69](https://github.com/mikevasiloff/sp-hover-card/blob/main/PersonGroupField.json#L69) from *https://webmail.apps.mil* (DoD) to *https://outlook.office365.us* (GCC High)
