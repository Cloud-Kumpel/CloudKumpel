---
layout: post
title: "Error: Azure Automation - Runbook fails when using PnP-PowerShell"
date: "2019-05-12"
tags: [Azure, Azure Automation, PowerShell, Runbooks, PnP]
feature-img: "assets/img/posts/2019-05-12/PnPError002.png"
author: MarvinBangert
excerpt_separator: <!--more-->
---

Recently I worked on a project using Azure Automation Runbooks and PnP-PowerShell (for SharePoint Online) to automate some changes on a SharePoint site. When I used any commandlet that creates, adds or changes something - like "Add-PnP...", "New-PnP...", "Update-PnP...", "Set-PnP..." - the runbook enters a loop for three times without any error message and then the runbooks failed.
<!--more-->

So from the console and logs, you could access, you are not able to see more information about the problem. Also if you want to use catch{$\_.Exception.Message} it wouldn't work, because the runbook is never going to this state and just restarts when executing the commandlet:

![PnPError]({{"assets/img/posts/2019-05-12/PnPError001-1024x872.png" | relative_url}})

As you can see, after executing the commandlet (Add-PnPView) - "Microsoft.SharePoint.Client.View" - the runbook stops for about one to two minutes and then restarts again.

Here you can see my code snippet. The script/runbook crushed everytime on the line "Add-PnPView..."

```PowerShell
#Connect to PnP Online
Write-Output ("Connecting to PnPOnline")
Connect-PnPOnline -Url $siteurl -Credentials $cred

#Add new View
Write-Output ("Add new View")
Add-PnPView -List $listname -Title $viewname -Fields "Title"
```

After a few emails, I got feedback from Microsoft Support with a similar issue: https://github.com/SharePoint/PnP-PowerShell/issues/1541

In this article, the user "jwiersem" gives the hint to add a variable before the commandlet

```PowerShell
#Connect to PnP Online
Write-Output ("Connecting to PnPOnline")
Connect-PnPOnline -Url $siteurl -Credentials $cred

#Add new View
Write-Output ("Add new View")
$view = Add-PnPView -List $listname -Title $viewname -Fields "Title"
```

Then the runbook runs successfully without any loop.

![PnPError003]({{"assets/img/posts/2019-05-12/PnPError003-1024x329.png" | relative_url}})

Thanks again to the Microsoft Support for a great collaboration on this issue and the very fast contacting.

I hope this helps you too if you are struggling with this error
