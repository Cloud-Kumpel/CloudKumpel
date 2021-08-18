---
layout: post
title: Microsoft Lists Sync is comming back
tags: [Lists, SharePoint, OneDrive, Nucleus]
author: get-adr
excerpt_separator: <!--more-->
---
# Back to the future
Back in 2010 there was SharePoint Workspace, that enables sync of SharePoint On-Prem content including lists. Last year at Ignite Jeff Teper announced Project Nucleus to bring back that kind of functionality and more. Jeff spoke about the following key features:
<!--more-->
* Offline sync / access to lists
* Much better performance in large lists
* Better performance on list filtering, grouping and sorting

Jeff didn't go in much detail on how this functionality will be implemented. A look at the Microsoft 365 Message Center gives us some more infomation on this.

As announced in message [MC261538](https://admin.microsoft.com/AdminPortal/Home?ref=MessageCenter/:/messages/MC261538) Microsoft will deploy a binary alongside the OneDrive client using the OneDrive Update mechanism. 

In Message MC261538 the List sync client is called Nucleus.exe, in the newer message [MC277196](https://admin.microsoft.com/AdminPortal/Home#/MessageCenter/:/messages/MC277196) the service is called Microsoft.SharePoint.exe so we will see which name is correct when the rollout of this feature starts. This should happen somewhere between now and the end of september.

## How does it work?
As soon as the List sync client is installed, you will see a new icon in your Lists dashboard:
![List Sync Icon]("assets/img/posts/2021-08-18/ListSync.png")
The content of the synced lists is stored in a local database and is available for offline Access. The easiest way to access lists is to install the Lists PWA:
![Install Lists app]("assets/img/posts/2021-08-18/InstallListsApp.jpg")
