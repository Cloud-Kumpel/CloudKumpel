---
layout: post
title: Power Apps Reorder Collection
tags: [Power Apps, HowTo]
author: MarvinBangert
excerpt_separator: <!--more-->
---

# Power Apps reorder items in collection
Hey folks,

maybe you already came around the situation, that you want to reorder your Power Apps collection before saving it, to bring your task in the correct order or just want to rearrange it in your source (like SharePoint Online). In this article you will learn how to reorder your collection in an app.
<!--more-->
The basic idea is to have an extra column in our collection, that is updated each time we rearrange items by clicking on an icon. We need not only need to prepare our collection, but also to implement the function to reorder them on click.
We start with an empty new app, on the "App" - "OnStart" we create a new empty collection "colChecklist". "col" is my prefix for collections and "Checklist" is just some name we will give our collection.
```
//Syntax ClearCollect(collection, item, ...)
ClearCollect(colChecklist,{})
```
Then we need some values in our Power Apps collection, so we just start with a text input and a button:
![Text Input]({{"assets/img/posts/2021-08-26/Image 505.png" | relative_url}})
You can also use a form, dropdown, datepicker etc. we just need to add some information in our collection. On the button we add the following code on "OnSelect":
```
//Syntax Set(variable, value)
Set(varCount,CountRows(colChecklist));
//Syntax Collect(collection, item, ...)
Collect(colChecklist,{Input:TextInput1.Text,SortOrder:varCount})
```
Whenever we click on the button, first of all we count the current amount of rows (items) in our collection "colChecklist" as save this information in a variable "varCount". On the next line we collect a new item in our collection and give two (or more) columns ("Input" & "SortOrder") to this record. It is important that we initialize the collection on the app start before, otherwise you would receive errors. How many columns you add to your collection does not matter, but the "SortOrder" column is necessary to reorder the collection.

We can also add a gallery to our app, to see our collection and input:
![New Gallery]({{"assets/img/posts/2021-08-26/Image 506.png" | relative_url}})
On your gallery you can sort the collection by the column "SortOrder" on the property "Items" using:
```
//Syntax SortByColumns(source, column, order[Ascending or Descending; Default=Ascending], ...)
SortByColumns(colChecklist,"SortOrder")
```
Now we need to add two more icons to our gallery: "Up" and "Down" and arrange them in the gallery:
![Added Up and Down Arrows]({{"assets/img/posts/2021-08-26/Image 507.png" | relative_url}})
Lets start with the "Up" arrow on property "OnSelect"
```
//Syntax UpdateIf(collection, condition, item, ...)
UpdateIf(
    colChecklist,
    SortOrder = ThisItem.SortOrder - 1,
    {SortOrder: SortOrder + 1},
    SortOrder = ThisItem.SortOrder,
    {SortOrder: SortOrder - 1}
)
```
Lets asume we are clicking on the second item in our example gallery (see picture above) "Adrian" with SortOrder "1". First we check for the item above this item by "ThisItem.SortOrder - 1" to get the item with SortOrder "0" which would be "Marvin". The Item "Marvin" needs to be updated by updating the SortOrder +1 and on the same we update our current item "Adrian" by changing the SortOrder - 1. This would be our result:
![Reorder Items]({{"assets/img/posts/2021-08-26/Image 508.png" | relative_url}})
To avoid that users will go any further when the SortOrder is "0", we implement the following code on the "Visible" property:
```
//Syntax If(logical_test, true_value, false_value)
If(ThisItem.SortOrder = 0,false,true)
```
The "Up" arrow should not be visible anymore on the first item of our gallery, but on any other item:
![Hide Up]({{"assets/img/posts/2021-08-26/Image 509.png" | relative_url}})

Now we need to configure the other arrow "Down" to bring the item down, if it is clicked. This is pretty much the same as on the "Up" arrow, we just need to change the sign:
```
//Syntax UpdateIf(collection, condition, item, ...)
UpdateIf(
    colChecklist,
    SortOrder = ThisItem.SortOrder + 1,
    {SortOrder: SortOrder - 1},
    SortOrder = ThisItem.SortOrder,
    {SortOrder: SortOrder + 1}
)
```
Also we need to configure the "Visible" property of the "Down" arrow to be hidden on the last item. Because the collection can be any size, we need to calculate it automatically based on the rows in our collection:
```
//Syntex If(logical_test, true_value, false_value)
//Syntex CountRows(source)
If(ThisItem.SortOrder = CountRows(colChecklist) - 1,false,true)
```
Whenever you add some more items to the collection, always the last item will have no "Down" arrow:
![Hide Down]({{"assets/img/posts/2021-08-26/Image 510.png" | relative_url}})

Congratulation, you created your app functionality to reorder items in a collection, you can use this before you save this in your target database or list. You can even use this with other sources, so you directly update the information in your source.

Glück Auf!
Marvin
