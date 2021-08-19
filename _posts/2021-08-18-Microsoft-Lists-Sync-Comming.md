---
layout: post
title: Microsoft Lists Sync is coming back
tags: [Lists, SharePoint, OneDrive, Nucleus]
author: adr-tag
excerpt_separator: <!--more-->
---
# Back to the future

Back in 2010 there was SharePoint Workspace, that enables sync of SharePoint On-Prem content including lists. Last year at Ignite Jeff Teper announced Project Nucleus to bring back that kind of functionality and more. Jeff spoke about the following key features:
<!--more-->

-   Offline sync / access to lists

-   Much better performance in large lists

-   Better performance on list filtering, grouping, and sorting

Jeff didn’t go in much detail on how this functionality will be implemented. Some Microsoft Admin Center Messages and documentation is going deeper in details while the Rollout is starting. So, this is the summary of what we know so far.

A look at the Microsoft 365 Message Center gives us some more information on the list sync service.

As announced in message [<u>MC261538</u>](https://admin.microsoft.com/AdminPortal/Home?ref=MessageCenter/:/messages/MC261538) Microsoft will deploy a binary alongside the OneDrive client using the OneDrive Update mechanism.

In Message MC261538 the List sync client is called Nucleus.exe, in the newer message [<u>MC277196</u>](https://admin.microsoft.com/AdminPortal/Home#/MessageCenter/:/messages/MC277196) the service is called Microsoft.SharePoint.exe so we will see which name is correct when the rollout of this feature starts. This should happen somewhere between now and the end of September.

## How does it work?

Based on the available information it works as follows: As soon as the List sync client is installed, you will see a new icon in your Lists dashboard:

![List Sync Icon]({{"assets/img/posts/2021-08-18/ListSync.jpg" | relative_url}})


Lists that are in sync are marked with a checkmark in a circle.

The content of the synced lists is stored in a local database and is available for offline Access. The easiest way to access lists is to install the Lists PWA:

![Install Lists app]({{"assets/img/posts/2021-08-18/InstallListsApp.jpg" | relative_url}})

To stop the sync of a list, there is an option for that in the list context menu:

![Stop Sync]({{"assets/img/posts/2021-08-18/StopListSync.jpg" | relative_url}})

In case of sync issues, there will be a dedicated view containing all conflicts. From this view you can export conflicting list items as csv.

When starting the synchronization, the whole list will be synced. All changes are a differential sync. Compared to file sync the required bandwidth is to neglect.

## Known limitations

With the start of the new feature, there are some limitations according to this [<u>Microsoft Support article</u>](https://support.microsoft.com/en-us/office/edit-lists-offline-41403c3e-1795-4e07-b56b-ae591cbde2f9):

### Only Windows 10
Microsoft List Sync is only available on Windows 10

### Not all List features available offline

Not all List operations are available offline. Features that are not available offline, are grayed out in the options:

![Not available options]({{"assets/img/posts/2021-08-18/ListOptionsOffline.jpg" | relative_url}})

### Not all List types supported

As expected, if the option “Allow items from this list to be downloaded to offline clients” is disabled the list cannot be synced. (kind of retro) Speaking of retro, lists in “Classic Experience” aren’t supported too. To sync a list, you must have access to the list, either it is your List or shared with you. If you lose access, the list is removed from sync.

Content type enabled lists or lists with folders are currently not supported. 
Lists with enabled content approval are also not supported.
Lists with the following field types are not supported:

-   Calculated fields

-   Lookup fields

-   Validation of fields

-   Fields with default values

-   Multiple lines of text with “Append changes to existing Text” option enabled

## Administrative considerations and options

By default, List sync is enabled for all users. To control the list sync behavior there are three group policies available. The policies are part of the OneDrive group policies. The GPOs are:

-   Prevent Lists sync from running on the device

-   Prevent users from syncing lists shared from other organizations

-   Prevent users from getting silently signed in to Lists sync with their Windows credentials

You can find details on the GPOs in the following [<u>Microsoft Docs Article</u>](https://docs.microsoft.com/en-us/SharePoint/lists-sync-policie).

To control List sync on unmanaged devices there are the usual options to control access to SharePoint like conditional access.

## User Adoption
As List sync is a new feature with some limitations, it should be part of the adoption strategy.
