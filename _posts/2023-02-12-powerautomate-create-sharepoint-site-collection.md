---
layout: post
feature-img: assets/img/posts/2023-02-02/header-image.png
author: MarvinBangert
excerpt_separator: "<!--more-->"
title: PowerAutomate - Create SharePoint site collection
date: 2023-02-12T00:00:00+01:00
tags:
- Quick Tip
- Power Platform
- REST API
- API
- SharePoint
- Power Automate
description: In this post you will learn how to create a SharePoint site collection
  using Power Automate. I will also explain the different parameters to configure,
  prerequisites and how to check if a site already exists. Also you will learn about
  the parameter "SensitivityLabel" to actually apply a sensitivity label to your site
  while creation and why you shouldn't use "Classification" anymore.
keywords: []

---
Hey folks,

In this post you will learn how to create a SharePoint site collection using Power Automate. I will also explain the different parameters to configure, prerequisites and how to check if a site already exists. Also you will learn about the parameter "SensitivityLabel" to actually apply a sensitivity label to your site while creation and why you shouldn't use "Classification" anymore.

<!--more-->

As there is no out-of-the-box action, we need to use the "Send an HTTP request to SharePoint" action. Here is the quick answer on how to create a new site collection. You will find more information about it below.

![]({{"assets/img/posts/2023-02-12/2023-02-12-02-12-52.png" | relative_url}})

    Site Address: https://<yourtenant>-admin.sharepoint.com
    Method: POST
    URI: /_api/SPSiteManager/create
    Headers:
    Accept: Application/json;odata.metadata=none
    Odata-version: 4.0
    Body:
    {
    "request": {
    	"Title": "Site Title",
    	"Url": "https://cloudkumpel.sharepoint.com/sites/NewSite",
    	"Lcid": 1033,
    	"ShareByEmailEnabled": false,
    	"Description": "Here is a description",
    	"WebTemplate": "STS#3 or SITEPAGEPUBLISHING#0",
    	"SensitivityLabel": "bd6fb9cd-7d7c-44e9-9c75-af0e71ac279e",
    	"SiteDesignId": "00000000-0000-0000-0000-000000000000",
    	"Owner": "user@contoso.com",
    	"WebTemplateExtensionId": "00000000-0000-0000-0000-000000000000"
    	}
    }

## Prerequisites

Depending on your user account and your tenant configuration, not every user might be allowed to create a new SharePoint site collection.

Microsoft recently added a second option within the SharePoint admin center to not only allow or deny the creation of SharePoint sites, but to allow/deny the creation using PowerShell or REST API and then if it should be visible to users:

![]({{"assets/img/posts/2023-02-12/2023-02-11-22-40-08.png" | relative_url}})

You will find this setting within the SharePoint admin center - settings - site creation.

As a normal user, at least the first checkbox would need to be checked. Changing this settings will take a couple of minutes to be effective.

If you are using an administrative account to create the site collections, you need to be SharePoint Administrator or Global Administrator. The above setting can be turned off then.

Let's check out the request body now:

**Body Details**

Required fields will have a * (asterisk).

* Title*: The title of the SharePoint site collection.
* URL*: The URL of the SharePoint site collection.
* LCID*: Is the locale identifier (LCID) for the language. This will be the default language for your SharePoint site collection. Here are some examples:
  * 1033 = English (US)
  * 1031 = German (Germany)
  * 1036 = French (France)
  * 3082 = Spanish (Spain)
  * 1046 = Portuguese (Brazil)
  * 1028 = Chinese (Traditional)
  * 1025 = Arabic
  * 1043 = Dutch (Netherlands)

  You can find more here: [Reference: SharePoint Online Language IDs (pkbullock.com)](https://pkbullock.com/resources/reference-sharepoint-online-languages-ids/).
* WebTemplate*: You are only able to create a modern non-group connected team site (STS#3) or a modern communication site (SITEPAGEPUBLISHING#0).
* ShareByEmailEnabled: false or true; This will set the external file sharing option of the SharePoint site. False = "Only people in your organization" (no external sharing), true = "New and existing guests" (external sharing possible).
* Description: The description of the SharePoint site collection.
* SensitivityLabel: If you are using sensivity labels within your organization, you can add them to the site collection on creation. Recently, I already updated the [Microsoft Learn article](https://learn.microsoft.com/en-us/sharepoint/dev/apis/site-creation-rest#:\~:text=the%20REST%20endpoint.-,Note,-The%20%22Classification%22%20parameter) as there are two parameters. The "Classification" which will only set any value inside the label, so it looks like there is a sensitivity label applied to your side, but in fact it isn't. You need to use the "SensitivityLabel" parameter, to actually apply a sensitivity label to your site. It requires an sensitivity label ID. The easiest way to get a sensitivity label is: just select an existing site with the label you are looking for and add "/_api/site" to the url:

  [https://cloudkumpel.sharepoint.com/sites/sitecollection/_api/site](https://cloudkumpel.sharepoint.com/sites/sitecollection/_api/site "https://cloudkumpel.sharepoint.com/sites/sitecollection/_api/site")

  This will give you an XML with the properties of your site. Copy it to Visual Studio Code (or any text editor/source-code editor) to format it properly and make reading easier. Look for the "SensitivityLabelID" property, this is the ID we are looking for. Within Power Automate, you only need the Sensitivity Label parameter within the request, the "Classification" property is not required.
* Owner: You can specify the site collection admin for this new site collection. If it's empty, the admin will be the user who did the request.
* SiteDesignId: You can apply some out-of-the-box designs from Microsoft on your site, here are some examples, which will work for both team and communication site:
  * Topic: 96c933ac-3698-44c7-9f4a-5fd17d71af9e or 00000000-0000-0000-0000-000000000000 or null
  * Showcase: 6142d2a0-63a5-4ba0-aede-d9fefca2c767
  * Blank: f6cc5403-0d63-442e-96c0-285923709ffc

  If you want to apply a custom template/design from your company, you need to use "WebTemplateExtensionId" instead.
* WebTemplateExtensionId: If you want to apply your custom SharePoint design right on creation, you need to add the site design ID here. You can get the Site Design using [Get-SPOSiteDesign](https://learn.microsoft.com/en-us/powershell/module/sharepoint-online/get-spositedesign?view=sharepoint-ps) (Microsoft SharePoint Online Management Shell) or [Get-PnPSiteDesign](https://learn.microsoft.com/en-us/sharepoint/dev/declarative-customization/site-design-pnppowershell) (PnP PowerShell). You can use both parameters, SiteDesignId and WebTemplateExtensionId as from both the design will be applied to the site.

Other parameters you are able to use, which are not documented:

* TimeZoneId: If you want to automatically set a specific time zone, you can add this parameter to the body request. You need to define the time zone id like:
  
  
  "TimeZoneID" : 4
  
  
  Here you will find some more IDs you can use for the specific time zone: Reference: [SharePoint Time Zone IDs (pkbullock.com)](https://pkbullock.com/resources/reference-sharepoint-time-zone-ids/)
* HubSiteId: To automatically add a site collection to a hub, you can use the following parameter:


  "HubSiteId": "00000000-0000-0000-0000-000000000000"


  To get the HubSiteId, similar to the SensitivityLabel, you can use the same technique to look for an existing hub id. You can execute this on either the hubsite itself or a site associated to the hub. The parameter you are looking for is "HubSiteId".

**Response**

If your site was created successfully, you will get the following output:

    {
    	"SiteId": "<SharePoint Site ID>",
    	"SiteStatus": 2,
    	"SiteUrl": "https://cloudadmin.sharepoint.com/sites/NewSite"
    }

If it wasn't successful, you might get something like this output:

    {
    	"status": 400,
    	"message": "Unexpected response from the service\r\nclientRequestId: 00000000-0000-0000-0000-000000000000\r\nserviceRequestId: 00000000-0000-0000-0000-000000000000",
    	"error": {
    		"message": "Unexpected response from the service"
    	},
    	"source": "sharepointonline-we.azconn-we-002.p.azurewebsites.net"
    }

In this case, review your body, you might missed a required field, a value is not valid or just an (extra) comma. The site collection will not be created.

**Check if Site exists**

Before you can create a SharePoint site collection, you might want to check if the URL is already taken. You can use the following SharePoint REST API call to check it:

![]({{"assets/img/posts/2023-02-12/2023-02-12-02-14-47.png" | relative_url}})

To make this call, you need to be at least SharePoint Administrator. A user, even if the prerequisites from above are activated, is not able to make this call, it will result in an error.

    Site Address: https://<yourtenant>-admin.sharepoint.com
    Method: GET
    URI: /_api/SPSiteManager/status?url='https://'

**Response**

Depending on if a site already exists or not or something else is with the site, you will get the following SiteStatus codes:

* 0 - Not found. Site doesn't exist.
* 1 - Provisioning. Site is currently being provisioned.
* 2 - Ready. Site is created.
* 3 - Error. An error occurred while provisioning the site.
* 4 - Site with requested URL already exists.

If the site exists, the response will be:

    {
    	"d": {
    		"Status": {
    			"__metadata": {
    				"type": "Microsoft.SharePoint.Portal.SPSiteCreationResponse"
    			},
    		"SiteId": "00000000-0000-0000-0000-000000000000",
    		"SiteStatus": 2,
    		"SiteUrl": "https://cloudkumpel.sharepoint.com/sites/NewSite"
    		}
    	}
    }

If the site doesn't exists, you will get the following response:

    {
    	"d": {
    		"Status": {
    			"__metadata": {
    				"type": "Microsoft.SharePoint.Portal.SPSiteCreationResponse"
    			},
    		"SiteId": "",
    		"SiteStatus": 0,
    		"SiteUrl": ""
    		}
    	}
    }

**FAQ**

Q: What will happen, if you are not checking if a site already exists, before you are creating a SharePoint site?

A: Before creating a Site Collection, the SharePoint provisioning process we are calling also checks, if the site url is already used. The result of your "Create" call will be:

    {
    	"SiteId": "",
    	"SiteStatus": 4,
    	"SiteUrl": ""
    }

Overall, you should use check first, if the site already exists and use the "SiteStatus" for further automation. As if you don't handle your flow properly after creating a site collection, you could override existing configurations.

**Summary**

As you can see, it's very easy to create a new SharePoint site collection using Power Automate. There are some requirements for normal users and as an admin you should review your SharePoint settings, as otherwise even if it's not visible to users, they might be able to create new site collections on their own.

**Reference**

[Create Modern SharePoint Sites using REST](https://learn.microsoft.com/en-us/sharepoint/dev/apis/site-creation-rest)

Thanks for reading, I hope you liked it and it will help you!

[Glück auf](https://en.wikipedia.org/wiki/Gl%C3%BCck_auf)

Marvin
