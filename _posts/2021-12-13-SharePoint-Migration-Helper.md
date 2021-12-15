---
layout: post
title: SharePoint Migration Manager Helper
tags: [SharePoint Online,Power Automate,SharePoint Migration Manager]
author: MarvinBangert
excerpt_separator: <!--more-->
---

Hey folks,

already a while ago I came up with an idea and solution to support you while migrating from File Server to SharePoint Online using the SharePoint Migration Manager. The solution uses some basic SharePoint and Power Automate tools and doesn't require any premium connectors. This article will show you how to build this solution on your own, you can also download the solution from [<u>GitHub</u>]().

<!--more-->

## Getting things ready

So the basic idea is that you can manage the migration from a SharePoint Online list, to plan and monitor the status and making the migration easier. In total there will be two lists and the default documents library. Within the lists you can plan the time a folder will get migrated, generate the CSV file you need to import into SharePoint Migration Manager and update the status after the migration is completed.


> SharePoint Migration Manager can already handle a lot of different scenarios, but please completly check all requirements if it fits to your needs. Otherwise you should consider using a third party migration tool. You can find all information about the SharePoint Migration Manager in the [<u>Microsoft docs</u>](https://docs.microsoft.com/en-us/sharepointmigration/mm-get-started).


### Setting up the SharePoint site

First, you need a new SharePoint Site Collection, it doesn't matter if you are using a Communication Site or Team Site (without a Microsoft 365 Group), in this example we will use Communication Site. Just create it within your SharePoint Admin Center and access it.
We will use the standard "Documents" library, that is already on your SharePoint site, so we just need to create two more lists. The first list will be called "Batches", in this list we can create different "packages" called "batches" to split the migration into multiple parts, if you have too much folders to migrate within one session or want to have a test, pilot and productive migration.
We need to create the following Columns next to the default column "Title":

| Name           | Internal Name | Type          | Settings      |
|----------------|---------------|---------------|---------------|
| Title          | Title         | Single Line   | Default settings from "Title" column |
| Status         | Status        | Choice        | Choices: Not started, Planned, In Migration, Finished, Error |
|                |               |               | Display Choices: Drop-Down Menu |
|                |               |               | Allow 'Fill-in' choices: No |
| Migration Date | MigrationDate | Date and Time | Date and Time |
|                |               |               | Date and Time Format: Date & Time |
|                |               |               | Display Format: Standard |
|                |               |               | Default Value: None |
| Generate CSV   | GenerateCSV   | Single Line   | Single Line   |

> If you want the "Status" column to also appear within the other list, you need to select the 'Single line' type, a choice cannot be displayed using SharePoint lookup.

> The column "Generate CSV" is only required to add some JSON Formatting, you don't need to put any data into this and can disable the field from the entry form.

The other table is called "Migration", in this table you need to add all kind of information from source folder and target site. Your target could be a SharePoint site or OneDrive for Business storage.

| Name           | Internal Name | Type          | Settings      |
|----------------|---------------|---------------|---------------|
| Title          | Title         | Single Line   | Default settings from "Title" column |
| Source         | Source        | Single Line   | Required: Yes |
| Source Document Library | SourceDocLib        | Single Line   | Required: No |
| Source Optional Subfolder | SourceOptionalSubfolder        | Single Line   | Required: No |
| Target | Target        | Single Line   | Required: Yes |
| Target Document Library | TargetDocLib        | Single Line   | Required: Yes |
| Target Optional Subfolder | TargetOptionalSubfolder        | Single Line   | Required: No |
| Site Type         | SiteType        | Choice        | Choices: SharePoint, OneDrive |
| Batch | Batch | Lookup | Required: No |
|                |               |               | Get information from: Batches |
|                |               |               | Column: Title |
|                |               |               | Show Columns: Migration Date (and Status if it is a Single Line column) |

