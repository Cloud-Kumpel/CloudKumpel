---
layout: post
title: SharePoint Migration Manager Helper
tags: [SharePoint Online,Power Automate,SharePoint Migration Manager]
author: MarvinBangert
excerpt_separator: <!--more-->
---

Hey folks,

already a while ago I came up an idea and solution to support you while migrating from File Server to SharePoint Online using the SharePoint Migration Manager. The solution uses some basic SharePoint and Power Automate tools and doesn't require any premium connectors. This article will show you how to build this solution on your own, you can also download the solution from [<u>GitHub</u>]().

<!--more-->

## The Idea

So the basic idea is that you can manage the migration from a SharePoint Online list, to get an overview about the current status and making the migration itself easier. In total there will be two lists and the default documents library. Within the lists you can plan the time a folder will get migrated, generate the CSV file you need to import into SharePoint Migration Manager.


> SharePoint Migration Manager can already handle a lot of different scenarios, but please completly check all requirements if it fits to your needs. Otherwise you should consider using a third party migration tool.
> You can find all information about the SharePoint Migration Manager in the [<u>Microsoft docs</u>](https://docs.microsoft.com/en-us/sharepointmigration/mm-get-started).


