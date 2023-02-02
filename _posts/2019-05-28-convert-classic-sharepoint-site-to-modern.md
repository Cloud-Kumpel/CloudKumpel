---
title: Convert classic SharePoint site to modern
date: 2019-05-28 00:00:00 Z
tags:
- Office 365
- PowerShell
- SharePoint Online
- PnP
layout: post
author: MarvinBangert
feature-img: assets/img/posts/2019-05-28/PowerShell_Icon.png
excerpt_separator: "<!--more-->"
---

If you want to convert your classic SharePoint sites into modern SharePoint sites, there were released a new commandlets to PnP PowerShell which allows you to achieve this. 
<!--more-->

```PowerShell
ConvertTo-PnPClientSidePage
```

This is our current classic SharePoint Site: 

![classic SharePoint site]({{"assets/img/posts/2019-05-28/classic-876x1024.png" | relative_url}})

```PowerShell
Connect-PnPOnline -Url "https://tenantname.sharepoint.com/sites/sitename"

ConvertTo-PnPClientSidePage -Identity Home.aspx
```

This commandlet requires PnP PowerShell version 3.4.1812.0 (December 2018 release) or higher.

After sign in, the home site will be migrated to modern design. Instead of overwriting the home site it will create a new page "migrated\_home.aspx".

![Modern]({{"assets/img/posts/2019-05-28/modern-815x1024.png" | relative_url}})

As you can see, there are some webparts that are currently not available in modern SharePoint. You will see a notification:

![NoReplacement]({{"assets/img/posts/2019-05-28/noReplacement.png" | relative_url}})
