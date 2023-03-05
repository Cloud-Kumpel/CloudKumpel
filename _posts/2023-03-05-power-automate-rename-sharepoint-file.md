---
layout: post
feature-img: assets/img/posts/2023-02-02/header-image.png
author: MarvinBangert
excerpt_separator: "<!--more-->"
title: Power Automate - Rename SharePoint file
date: 2023-03-05T20:00:00+01:00
tags:
- Quick Tip
- REST API
- SharePoint Online
- Power Automate
description: ''
keywords: []

---
Hey folks,

Today, there is a short quick tip on how to change the name of a document using Power Automate.

<!--more-->

As you figured out already, when you are using the "Update file properties" action within Power Automate, you are only able to update the title field of a document, but not the name of the document. To update the file name, you need to use the "Send an HTTP request to SharePoint" action and update the field "FileLeafRef" as it references to the "name column" of the SharePoint library.

![]({{"assets/img/posts/2023-03-05/2023-03-05-1-2.png" | relative_url}})

    Site Address: <Your SharePoint site address>
    Method: POST
    URI: _api/web/lists/getbytitle('<Library name>')/items(<Item ID>)
    Headers:
    	{
     		"Accept": "Application/json;odata=verbose",
      		"Content-Type": "Application/json;odata=verbose",
      		"IF-MATCH": "*",
    		"X-HTTP-Method": "MERGE"
    	}
        
     Body:
     {
        '__metadata':
        {
            'type':'SP.Data.<internal library name>Item'
        },
        'FileLeafRef':'<new file name + extension>'
    }

### Result

![]({{"assets/img/posts/2023-03-05/2023-03-05-2.png" | relative_url}})

turns to

![]({{"assets/img/posts/2023-03-05/2023-03-05-3.png" | relative_url}})

Make sure you are also setting the right document type, otherwise your file might not work anymore.

Thanks for reading, I hope you liked it and it will help you!

[Glück auf](https://en.wikipedia.org/wiki/Gl%C3%BCck_auf)

Marvin
