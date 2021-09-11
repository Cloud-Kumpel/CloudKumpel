---
layout: post
title: "Hide Power Apps and Power Automate (Flow) in SharePoint Online"
date: "2019-11-26"
tags: [Office 365,Power Apps,Power Automate,SharePoint Online,PowerShell,HowTo]
feature-img: "assets/img/posts/2019-11-26/Bild-270.png"
author: MarvinBangert
excerpt_separator: <!--more-->
---

**!!! Unfortunately this does not work anymore since a Microsoft Update!!!**

Hey folks,

today i will show you how you could hide the buttons for Flow (Power Automate) and Power Apps in your SharePoint site. We will need the SharePoint Online PnP PowerShell (check out this GitHub site for more information: https://github.com/SharePoint/PnP-PowerShell).
<!--more-->
To install the module you can use:

```PowerShell
Install-Module SharePointPnPPowerShellOnline
```

After this connect to your SharePoint site and make a change to the following options:

```PowerShell
Connect-PnPOnline –Url https://<tenantname>.sharepoint.com/sites/<sitename> –Credentials (Get-Credential)
$ctx = Get-PnPContext
$ctx.Site.DisableAppViews = $true;
$ctx.Site.DisableFlows = $true;
$ctx.ExecuteQuery();
```

![]({{"assets/img/posts/2019-11-26/Bild-265.png" | relative_url}})

SharePoint list with Flow and Power Apps visible

![]({{"assets/img/posts/2019-11-26/Bild-268.png" | relative_url}})

SharePoint list with Flow and Power Apps hidden  
Customize forms could not be hidden

![]({{"assets/img/posts/2019-11-26/Bild-266-1024x222.png" | relative_url}})

SharePoint library with Flow visible  
(Power Apps button maybe will come later this/next year)

![]({{"assets/img/posts/2019-11-26/Bild-267-1024x207.png" | relative_url}})

SharePoint library with Flow hidden

This will hide the Flow and Power Apps buttons from your whole site, currently it is not supported to disable Flow or PowerApps just for one list or librabry, so you could only disable or enable it (just change $true to $false) for the Site/Site Collection. Your Flows and Power Apps will work as well in background, this commands just hide the buttons in the UI. If the users open Power Automate or Power Apps by using the waffle menu, they can still access these services. Also if the user opens "https://flow.microsoft.com" or "https://powerapps.microsoft.com" they can sign in with there account and could get a free trial license (if they don't have a license assigned). For more information check out this Q&A: [Flow in your organization Q&A](https://docs.microsoft.com/en-us/power-automate/organization-q-and-a#can-i-block-another-person-from-signing-up-for-flow)
