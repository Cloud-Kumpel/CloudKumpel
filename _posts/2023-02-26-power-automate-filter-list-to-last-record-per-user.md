---
layout: post
feature-img: assets/img/posts/2023-02-02/header-image.png
author: MarvinBangert
excerpt_separator: "<!--more-->"
title: 2023-02-26-Power-Automate-Filter-list-to-last-record-per-user
date: 2023-02-26T21:00:00+01:00
tags:
- Quick Tip
- SharePoint
- Power Automate
description: ''
keywords: []

---
Hi folks,

In this blog post, you will learn how to filter a list to get the last record per user, category etc. In this post we will use a SharePoint list, but the process works with any kind of list.

<!--more-->

First, this is the overall process. I will explain and go through it step by step:

![](assets/img/posts/2023-02-26/2023-02-26-01.png)

**Manually trigger a flow:**

First define a trigger. If you want to have it automated (like each week, month etc.) you can use a "recurrence" trigger or a manual trigger to start the flow as you need it.

**Initialize variable:**

![](assets/img/posts/2023-02-26/2023-02-26-02.png)

We need an array variable later, so we initialize it here.

**Get items:**

![](assets/img/posts/2023-02-26/2023-02-26-03.png)

Define the list your items are loaded from. This is mine:

![](assets/img/posts/2023-02-26/2023-02-26-04.png)

* ID = Standard SharePoint ID column
* Responsible = Person column
* Category = Choice column
* aModified = Date and Time column (used like the standard column "Modified" to set different date and times for demonstration purposes only)

To make this flow work, you need a column to sort (order) like the "ID" or "Modified" or "Created" or a date field etc. (I recreated the "Modified" field to set it to different values). Also, the next thing that is important, you need to order the loaded list by "desc" (desc = descending). As you want to get the very last item a user added and the higher the ID/modified, the more recent the item is.

You can also limit the columns by view to not get all columns (you maybe don't need), but this not required.

This example will return all columns from the list view "All items". You don't need to sort the SharePoint list, I just sort it for demonstration purposes to show you which items should be returned.

**Select:**

![](assets/img/posts/2023-02-26/2023-02-26-05.png)

![](assets/img/posts/2023-02-26/2023-02-26-06.png)

Next, we need to first get all the users from the list. It can also be the category or anything else you want. You need to use a unique value here, so instead of the display name of a person, use the email address.

    From: @{outputs('Get_items')?['body/value']}
    Map: Responsible @item()?['Responsible/Email']
    
    Or Map: Category @item()?['Category/Value']

The action "Select" allows us to select the specified properties from all elements of the "From" array into a new array. In this case the email of the responsible column or the category column.

**Apply to each:**

![](assets/img/posts/2023-02-26/2023-02-26-07.png)

    union(body('select'),body('select'))

As there could be multiple entries per user or category, we want to get the unique email of each user. Using "union()" on the same array, you will receive this unique array with just each user or category once in it. For each email / category in the array, apply the following:

**Filter array:**

![](assets/img/posts/2023-02-26/2023-02-26-08.png)

![](assets/img/posts/2023-02-26/2023-02-26-09.png)

First, we need to filter all the items we received from "Get items". As we already loaded all items, we don't need to make another call to SharePoint and just filter the items.

    From: @outputs('Get_items')?['body/value']
    Condition: @item()?['Responsible/Email'] is equal to @items('Apply_to_each')?['Responsible']
    
    or Condition: Condition: @item()?['Category/Value'] is equal to @items('Apply_to_each')?['Category']

This will give us an array with just the items where the "responsible" is equal to the current item we are running on of the apply to each. On the right side we define, that the value should be the one we are currently running on ( "items('Apply_to_each')" ) and the field should be the same as we defined it in the "select map" ("Responsible" or "Category")

**Append to array variable:**

![](assets/img/posts/2023-02-26/2023-02-26-10.png)

Now is the important part why we needed to sort the "get items" properly while loading the items.

    Name: <yourArrayvariable>
    Value: @{body('Filter_array')[0]}

We add the first item of the array into the flow array we created in the beginning. As we always have the latest item (with the highest date) at the beginning of the array and we are now filtering the array to just get the items from each unique user/category, we don't care how many items from a user are in there, we just add the item at position 0 (in arrays it starts counting with a 0) to our flow array.

**Parse JSON:**

![](assets/img/posts/2023-02-26/2023-02-26-11.png)

When the "Apply to each" ran to each unique item and added the latest item into an array, we can parse the array to make it easier to select within the next action. I would recommend you add a "compose" action after the "apply to each" and add the array variable "varArray" in it. Start your flow, open the "compose" action and get the output (just copy it somewhere like notepad on your desktop). Afterwards add the "Parse JSON", add the array variable as the Content and click on "Generate from sample". Put in the copied output into the field and click "Done". Now you have a autogenerated schema for your own list.

**Create HTML table:**

![](assets/img/posts/2023-02-26/2023-02-26-12.png)

This will create an HTML table you can use to not receive a message or mail per each item within the array, but to get a proper table returned with just the information you are looking for. From is the body of "Parse JSON", then click on "show advanced options" to change the "columns" field to "custom", afterwards on the left side give it a name and on the right side select the appropriate dynamic value from the "Parse JSON" action what you want to have display.

If you just add a date time column as it is, the output will be in ISO 8601 format. If you want to have a more user-friendly format, I recommend using the "Format data by examples" within the expressions:

Just select the column you want to get an expression for, add an example of how it is currently and then start writing how it should look like. Power Automate will recommend you some formats you can select and apply to expression to the field.

**Send an email:**

![](assets/img/posts/2023-02-26/2023-02-26-14.png)

Last, but not least, send an email or Microsoft Teams message etc. to yourself or someone else and add the HTML table inside the body.

**Result:**

Here is the list again, the last items should be ID 2 by Albert, ID 4 by Nikola, ID 5 by Michael, and ID 3 by Marie.

When looking for the category, it would be ID 2 by Choice 2, ID 1 by Choice 1, and ID 6 by Choice 3.

![](assets/img/posts/2023-02-26/2023-02-26-15.png)

![](assets/img/posts/2023-02-26/2023-02-26-16.png)

![](assets/img/posts/2023-02-26/2023-02-26-17.png)