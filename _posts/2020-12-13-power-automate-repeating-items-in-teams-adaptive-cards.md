---
title: Power Automate - Repeating items in Teams adaptive cards
date: 2020-12-13 00:00:00 Z
tags:
- Adaptive Cards
- Microsoft Teams
- Power Automate
layout: post
feature-img: assets/img/posts/2020-12-13/Image-1932-1.png
author: MarvinBangert
excerpt_separator: "<!--more-->"
---

Hey folks,

today i want to share with you a workaround for the Power Automate Microsoft Teams actions "Post an Adaptive Card to a Teams user and wait for a response", "Post an Adaptive Card to a Teams channel and wait for a response", "Post your own Adaptive Card as the Flow bot to a channel" and "Post your own Adaptive Card as the Flow bot to a user". Please notice these actions are all in preview so this could change after time. It took me a lot of time to find this information so I hope it will help you to not waste your time and nerves.

<!--more-->

Recently I came across the request to create a repeating items table within a Microsoft Teams Adaptive Card to send a user multiple information. Within the Adaptive Cards Designer, I found a sample which contains the way I want to show the data to a user: a dynamic table using repeating items from a JSON data:  
[Adaptive Cards Designer Expense Report](https://www.adaptivecards.io/designer/index.html?card=/payloads/ExpenseReport.template.json&data=/payloads/ExpenseReport.data.json)

If you check the "Card Payload Editor" you will find a Container containing the "ColumnSet" to display the data.

The "$data" defines where the data comes from to insert it in the Adaptive Card. You can find the "expenses" on the right side within the Adaptive Cards designer, it is an array with a lot of information. Within the "items" section you can define your lookup repeating information within the "expenses" array by "${created\_time}".  
If you want to learn more about Adaptive Cards Template Language, please visit the Microsoft Adaptive Cards Docs: [https://docs.microsoft.com/en-us/adaptive-cards/templating/language](https://docs.microsoft.com/en-us/adaptive-cards/templating/language)  
Within the docs there is also a chapter about [Repeating items in an array](https://docs.microsoft.com/en-us/adaptive-cards/templating/language#repeating-items-in-an-array). 

We will use this example from the docs for our flow because it is very simple:

```JSON
{
    "type": "Container",
    "items": [
        {
            "type": "TextBlock",
            "$data": [
                {"name": "Matt"}, 
                {"name": "David"}, 
                {"name": "Thomas"}
            ],
            "text": "${name}"
        }
    ]
}
```

Just copy the following code within your "Card Payload Editor" to test it:

```JSON
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "Container",
            "items": [
                {
                    "type": "TextBlock",
                    "$data": [
                        {
                            "name": "Matt"
                        },
                        {
                            "name": "David"
                        },
                        {
                            "name": "Thomas"
                        }
                    ],
                    "text": "${name}"
                }
            ]
        }
    ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

The only output should be an "${name}" if you click "Preview mode" you should see the data from "$data". So, we are not referencing our "text": "${name}" to the Sample Data Editor like before but to our "$data" and if we actual need the information, it will show all values:

 ![]({{"assets/img/posts/2020-12-13/Image-1934-1024x712.png" | relative_url}})

![]({{"assets/img/posts/2020-12-13/Image-1933-1024x748.png" | relative_url}})

We will copy this piece of code from the Card Payload Editor into our Power Automate action "Post your own adaptive card as the Flow bot to a user":

![]({{"assets/img/posts/2020-12-13/Image-1935.png" | relative_url}})

If we test our flow, you will see it ran successfully but if you check your Teams Flow Chat, you will not see the expected result:

![]({{"assets/img/posts/2020-12-13/Image-1936.png" | relative_url}}) ![]({{"assets/img/posts/2020-12-13/Image-1937.png" | relative_url}})

Unfortunately, it is currently not supported to use repeating items within the Power Automate actions. Please check out this [forum discussion](https://powerusers.microsoft.com/t5/Building-Flows/Providing-data-property-to-adaptive-card/m-p/674016#M90765) on this topic, until now I couldn't find any official documentation or statement but from the test above it seems to be right...

So, we need to find another solution to display the repeating items within our Microsoft Teams Adaptive Card. One would be to use another Language Template like:

```JSON
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "Container",
            "items": [ 
                {
                    "type": "TextBlock",
                    "text": "Matt"
                },
                {
                    "type": "TextBlock",
                    "text": "David"
                },
                {
                    "type": "TextBlock",
                    "text": "Thomas"
                }
            ]
        }
    ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

This Language Template works:  
![]({{"assets/img/posts/2020-12-13/Image-1938.png" | relative_url}})  
  
But most of the output within Power Automate is in JSON format and we may be having an output data from another action we want to use, we need to automatically transform our data to this working format. I added a "Compose" action where I inserted the JSON code we need to transform (this will simulate the output from any action):  
This can be any JSON formatted code you have, I used our previous code from the first Power Automate run and just added two more section above our array:

![]({{"assets/img/posts/2020-12-13/Image-1940.png" | relative_url}})

First, we need to Parse the JSON to get all values:

![]({{"assets/img/posts/2020-12-13/Image-1941.png" | relative_url}})  
Content comes from the "Compose" action (or any other action you use). You can use the "Generate from sample" button to autogenerate the Schema.

Now we need the "Select" action to select data from one array and create a new array with the values in the format we need:

![]({{"assets/img/posts/2020-12-13/Image-1942.png" | relative_url}})  
Please check your spelling because Adaptive Cards are case sensitive. The dynamic content comes from the "Parse JSON" action.

Now we can replace our "items" content within the Microsoft Teams action with the following expression (The select output is not visible within the dynamic content, only after you switched to "expression", entered any character and switch back to "dynamic content"; seems like a bug)

```R
body('Select')
```

![]({{"assets/img/posts/2020-12-13/Image-1943.png" | relative_url}})

If we test our flow, it works as expected and we are using any kind of repeating information from any JSON output we receive within Power Automate.

![]({{"assets/img/posts/2020-12-13/Image-1944.png" | relative_url}}) ![]({{"assets/img/posts/2020-12-13/Image-1945.png" | relative_url}})

I hope this will help you with your Adaptive Card in Power Automate! If you are looking for more information about Microsoft Adaptive Cards please check out Tomasz Poszytek's [Microsoft Adaptive Cards - The ultimate guide](https://poszytek.eu/en/microsoft-en/microsoft-adaptive-cards-the-ultimate-guide/)
