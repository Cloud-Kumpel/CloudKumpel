---
layout: post
feature-img: assets/img/posts/2023-02-02/header-image.png
author: MarvinBangert
excerpt_separator: "<!--more-->"
title: 2023-03-12-Power-Automate-Desktop-merge-csv-files
date: 2023-03-12T00:00:00+01:00
tags:
- Quick Tip
- SharePoint Online
- Power Automate
description: ''
keywords: []

---
Hey folks,

Today, we will learn how to use Power Automate Desktop to merge two or more csv files into one. In my case, I am using the SharePoint Migration Manager to migrate files from a file share to SharePoint Online and I want to combine a couple of files to import them easily into Power BI for further analysis.

<!--more-->

### What is Power Automate Desktop

Power Automate Desktop is an app that lets you create and manage **desktop flows** in Windows using Robotic Process Automation (RPA) to automate all repetitive desktop processes. Like cloud flows in Power Automate, desktop flows use low-code connectors to connect to services or automate different tasks on a local device. [Learn more.](https://learn.microsoft.com/en-us/power-automate/desktop-flows/introduction)

### What is SharePoint Migration Manager

The SharePoint Migration Manager is a tool within the SharePoint Admin Center, which lets you migrate from various sources to SharePoint, OneDrive, and Microsoft Teams without any additional costs. After a Migration, you can download the results of a migration as csv files, like "ItemReport", "ItemSummary", "ScanSummary", "StructureReport" or "TaskInfoSummary" for further analysis like on which item there was a failure and why. [Learn More.](https://learn.microsoft.com/en-us/sharepointmigration/migrate-to-sharepoint-online)

In my case, I have different migration jobs to the same SharePoint site collection and for further analysis in Power BI about the potential issues, I want to have one "ItemReport" that contains all "ItemReports" from the different migration jobs and rounds (up to five rounds). Of course, I don't want to do this manually for a couple of thousand reports, but lucky I can use Power Automate Desktop.

### Getting started

First, I need to download the csv files from SharePoint Admin Center, just select the migration job and click on "Download task report". Within your download folder on your client, you should see one or multiple zip folders with a GUID (the GUID of the migration task). 

![](assets/img/posts/2023-03-12/2023-03-12-01-1.png)

When you unzip these folders, you will see all the different csv files:

![](assets/img/posts/2023-03-12/2023-03-12-02-1.png)

I am interested in all "ItemReport" files, as they give me an overview about which item was migrated or not migrated. Also, I am looking for the "StructureReport" file to get the site collection name.

Before we start, the first action in my flow is to select all the zip files I want to go through:

![](assets/img/posts/2023-03-12/2023-03-12-03.png)

(I am using subflows, that's why this action is not the first action in the other screenshots):

![](assets/img/posts/2023-03-12/2023-03-12-05-1.png)

### Create file

As I could have different SharePoint site collections where I migrated to and I want to group the merged csv files by these site collections, I need to create a new file with the name of the site collection (if it doesn't exist). Here is the first part of the flow:

![](assets/img/posts/2023-03-12/2023-03-12-04.png)

As we loaded all files into the variable "SelectedFiles", we use a "For each" action to go through each of the zip files and save this current file in the variable "CurrentZip".

My structure for the unzip is having a folder "Demo" and a folder "Exporte" (eng.: "Exports"), within the "Demo" folder I want the results, within "Exporte" I want all the unzipped files from the current zip. This makes it easier to clear everything before I unzip the next zip file. And this is also the first action, "Delete file(s)" removes all existing files within the "Exporte" folder using

    C:\Demo\Exporte\*

Afterwards we unzip the current zip file we are running on into the "Exporte" folder:

![](assets/img/posts/2023-03-12/2023-03-12-06.png)

Next, we can already delete the zip file, as we have all documents extracted and want to keep our downloads clean afterwards (to also see we run through every zip file, of course you can also put this action to the end).

Now, we need to find the name of the site collection it migrated to. The easiest is by using the "StructureReport" file and getting the information from a specific column and row.

![](assets/img/posts/2023-03-12/2023-03-12-08.png)

![](assets/img/posts/2023-03-12/2023-03-12-10.png)

Depending on your CSV file and, you need to change the encoding and the seperator. Also, it's helpful to activate "First line contains column names".

There should always be a "StructureReport_R1" file and as the R1 and R2 only stands for the rounds and the target shouldn't change, we can always reference on the R1 file and save it into a variable "StructureReportFile". In the next action, we set a variable with the specific value from this file.

To understand what is happening in the formula, let's have a look inside the variable "StructureReportFile":  
![](assets/img/posts/2023-03-12/2023-03-12-09.png)

When you run the flow until this point and check the variable, you will see the following table. As you can see, we have rows (and a row number on the left) and headers. Like Excel, we can now reference this information to get a specific value from the data table.

> **Note**
>
> To stop a flow at a specific point, click infront of the numbers of the actions in Power Automate Desktop until there is a red circle. Start your flow and your flow will stop at this point. This is extremely helpful for debugging and checking variables before going on.

    C:\Demo\%StructureReportFile[1]['Structure title']%.csv

The syntax for a variable within Power Automate Desktop is using two percent symbols. If you are looking for a specific value inside the variable, you can add more information right into the variable like:

    %VariableName[Row][Column]%

In this case we set another variable "OutputFile" with the value "C:\\Demo\\Torchwood.csv" (see the screenshot above as "Torchwood" is our SharePoint site collection name).

As we only want one file, we check if this file already exists:

![](assets/img/posts/2023-03-12/2023-03-12-11.png)

If the file doesn't exist, it will be created by writing the header from the "ItemReport" files into it (so we don't need to come up with a way how to extract the headers (of course we could also make it more dynamic, maybe a topic for another blog post). If somewhen in the future the headers change, we need to update this, but this will not happen so often. You can just open an "ItemReport" file and copy the header or use the one below:

![](assets/img/posts/2023-03-12/2023-03-12-12.png)

    Source,Destination,Item name,Extension,Item size (bytes),Type,Status,Result category,Message,Source item ID,Destination item ID,Package number,Migration job ID,Incremental round,Task ID,Device name

Now, for each zip file we are running on, first we will get the name of the target site collection and create a new CSV document with it.

### Merge CSV files

Next, we need to combine all the "ItemReport" files. Also, this part isn't difficult:

![](assets/img/posts/2023-03-12/2023-03-12-13-1.png)

As there could be a different number of rounds for each migration job, we first get all of them using an asterisk (*):

![](assets/img/posts/2023-03-12/2023-03-12-14.png)

The asterisk (*) can stand for anything, so we will get all files of "ItemReport" regardless of if there are 1 or 5 of them.

Then, we do another "for each", to go through each of the files found by the "Get files in folder".

![](assets/img/posts/2023-03-12/2023-03-12-15.png)

Make sure you select the "First line contains column names" again, as we then don't need to deal with them writing to the new file.

Last this we need to do is appending the content into the new CSV file:

![](assets/img/posts/2023-03-12/2023-03-12-16.png)

Make sure to not include the column names (headers) here and to select "Append content" if the file already exists.

Running the flow will create different CSV files with all content from other CSV files merged into it:

![](assets/img/posts/2023-03-12/2023-03-12-17.png)

Currently, I upload these files to a SharePoint site afterwards, where a Power BI is pulling this information into a Power BI report. In the future this could also be implemented within Power Automate Desktop, but the SharePoint connectors are currently in Preview and require an additional license.