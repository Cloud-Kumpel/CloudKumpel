---
layout: post
feature-img: assets/img/posts/2023-02-02/header-image.png
author: MarvinBangert
excerpt_separator: "<!--more-->"
title: Power Automate - SharePoint trigger non-default flows
date: 2023-02-19T00:00:00+01:00
tags:
- Quick Tip
- SharePoint
- Power Automate
description: This post will be a brief overview of how to trigger a Power Automate
  flow, which is not inside the default environment, from SharePoint.
keywords: []

---
Hey folks,

This post will be a brief overview of how to trigger a Power Automate flow, which is not inside the default environment, from SharePoint.

<!--more-->

As you may have noticed, if you create a flow using the SharePoint triggers "For a selected item" or "For a selected file" within a non-default environment, you cannot find it within the "Automate" option inside a SharePoint list or library.

![]({{"assets/img/posts/2023-02-19/2023-02-19-01.png" | relative_url}})

When hovering over / clicking on "Automate", in the background the method "SyncFlowInstances" is triggered and returns a list of flow instances from the default environment, attached to the list and available by the current user.

But as flows from other environments are not returned (yet?), we need to use a workaround:

1. Create a SharePoint text column

    ![]({{"assets/img/posts/2023-02-19/2023-02-19-02.png" | relative_url}})
    
    First, we need to create a new SharePoint column within the library. You can call it as you like, the name is not important, we just need to have a column that can be formatted and show the "trigger button".
   
2. Format the column

    ![]({{"assets/img/posts/2023-02-19/2023-02-19-03.png" | relative_url}})
    
    Next, we need to format this new created column.
   
3. Switch to "Advanced mode" and add the following code

    ![]({{"assets/img/posts/2023-02-19/2023-02-19-04.png" | relative_url}})
    
    Inside the advanced mode, we can add some custom JSON, you can see a simple example script below.

       {
           "$schema": "https://developer.microsoft.com/json-schemas/sp/v2/column-formatting.schema.json",
           "elmType": "button",
           "customRowAction": {
               "action": "executeFlow",
               "actionParams": "{\"id\": \"<Flow ID>\"}"
           },
           "attributes": {
               "class": "ms-fontColor-themePrimary ms-fontColor-themeDarker--hover"
           },
           "style": {
               "border": "none",
               "background-color": "transparent",
               "cursor": "pointer"
           },
           "children": [
               {
                   "elmType": "span",
                   "attributes": {
                       "iconName": "Flow"
                   },
                   "style": {
                       "padding-right": "6px"
                   }
               },
               {
                   "elmType": "span",
                   "txtContent": "<Display Name>"
               }
           ]
       }

    Using the action "executeFlow" and the parameter of the Flow ID, we are able to trigger a flow.

4. Open Power Automate, click on "the three dots" - "Export" - "Get flow identifier" and copy the the flow identifier.

    ![]({{"assets/img/posts/2023-02-19/2023-02-19-05.png" | relative_url}})
    
    To be able to trigger the flow, we need to unique identifier of the flow we want to trigger within our non-default environment.
  
5. Now replace the <Flow ID> with the flow identifier:

       {
           "$schema": "https://developer.microsoft.com/json-schemas/sp/v2/column-formatting.schema.json",
           "elmType": "button",
           "customRowAction": {
               "action": "executeFlow",
               "actionParams": "{\"id\": \"v1/00000000-0000-0000-0000-000000000000/00000000-0000-0000-0000-000000000000\"}"
           },
           "attributes": {
               "class": "ms-fontColor-themePrimary ms-fontColor-themeDarker--hover"
           },
           "style": {
               "border": "none",
               "background-color": "transparent",
               "cursor": "pointer"
           },
           "children": [
               {
                   "elmType": "span",
                   "attributes": {
                       "iconName": "Flow"
                   },
                   "style": {
                       "padding-right": "6px"
                   }
               },
               {
                   "elmType": "span",
                   "txtContent": "Start flow"
               }
           ]
       }

    You should also replace the "<Display Name>" value to something more speaking for the users:

    ![]({{"assets/img/posts/2023-02-19/2023-02-19-06.png" | relative_url}})
  
    e.g., you can use the same name as the flow or just "start flow".

6. Clicking on the item will open the "Run flow" dialog and you are able to trigger the flow:
  
    ![]({{"assets/img/posts/2023-02-19/2023-02-19-07.png" | relative_url}})
  
    Click on the link of an item to open the run flow dialog and start the flow.


Thanks for reading, I hope you liked it and it will help you!

[Glück auf](https://en.wikipedia.org/wiki/Gl%C3%BCck_auf)

Marvin
