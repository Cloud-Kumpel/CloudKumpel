---
layout: post
title: "Power Automate: Trigger conditions"
date: "2022-03-22"
tags: [Power Automate,HowTo]
feature-img: "/assets/img/header%20image.png"
author: MarvinBangert
excerpt_separator: <!--more-->
---

In Microsoft Power Automate, flows are executed as soon as the trigger is met, e.g. an item is created or edited in SharePoint, a new Microsoft Forms survey has been filled out, or an email is received. But sometimes the flow should only start when a certain condition is met, for example the SharePoint list value has a certain value. For this there are the trigger conditions in Power Automate, which I would like to go into in more detail below.

<!--more-->

Let's take the example that we want to receive an email notification as soon as a SharePoint list item is set to "Completed". To do this, one could use the SharePoint trigger "When an item is created or modified", then add a condition "Completed is equal to True" (assuming the "Completed" field is a "Yes/No" field, a choice field would be 'Status is equal to "Completed"') and "If yes", an email is sent.

![]({{"assets/img/posts/2022-03-22/2022-03-22-TriggerConditions01.png" | relative_url}})

Common structure of a condition in Power Automate

However, this means that our flow will always be triggered as soon as a new item is edited (or created; depending on your trigger) in our list, regardless of whether our Completed field is True or False, the check then only takes place in the flow itself. However, if we look at the number of API requests that a user's license can make in 24 hours, if there is a lot of editing in the SharePoint list, it could cause problems:

| Products                                | Requests per paid license per 24 hours |
|-------------------------------------------------|---------------------------------------|
| Paid licensed users for Power Platform (excludes Power Apps per App, Power Automate per flow, and Power Virtual Agents) and Dynamics 365 excluding Dynamics 365 Team Members | 40.000 |
| Power Apps pay-as-you-go-plan, and paid licensed users for Power Apps per App, Microsoft 365 apps with Power Platform access, and Dynamics 365 Team Member | 6.000 |
| Power Automate per Flow plan, Power Virtual Agents base offer, and Power Virtual Agents add-on pack | 250.000 |

(Source: [https://docs.microsoft.com/de-de/power-platform/admin/api-request-limits-allocations](https://docs.microsoft.com/de-de/power-platform/admin/api-request-limits-allocations#microsoft-power-platform-requests-allocations-based-on-licenses) Date: March 22, 2022; Please refer to the Docs article for restrictions in the licenses )

(More Information: [What counts as Power Platform request](https://docs.microsoft.com/en-us/power-platform/admin/power-automate-licensing/types#what-counts-as-power-platform-request) )

### What is a Microsoft Power Platform request?

Requirements consist of different actions that a user performs for different products. On a general level, below is what constitutes an API call:

- Power Apps – all API requests to connectors and Microsoft Dataverse.
- Power Automate – all API requests to connectors, process advisor analysis, HTTP actions, and built-in actions from initializing variables to a simple compose action. Both succeeded and failed actions count towards these limits. Additionally, retries and other requests from pagination count as action executions as well. For more information, see What counts as Power Platform request?
- Power Virtual Agents - API requests (or calls) to Power Automate flows from within a chatbot conversation.
- Dataverse – all create, read, update, and delete (CRUD), assign, and share operations including user-driven and internal system requests required to complete CRUD transactions, and special operations like share or assign. These can be from any client or application (including Dynamics 365) and using any endpoint (SOAP or REST). These include, but are not limited to, plug-ins, classic workflows, and custom controls making the earlier-mentioned operations.

(Source: [What is a Microsoft Power Platform request](https://docs.microsoft.com/en-us/power-platform/admin/api-request-limits-allocations#what-is-a-microsoft-power-platform-request) Date: March 22, 2022)

So we keep running (unnecessary) requests, even though our element isn't even complete yet.

### How can we prevent this? 

Microsoft has built a function into the trigger settings for Microsoft Power Automate, with which we can already integrate a condition in the trigger so that our flow only starts when this condition has been met. To find them, we click on the three dots of our trigger and select "Settings" 

![]({{"assets/img/posts/2022-03-22/2022-03-22-TriggerConditions02.png" | relative_url}})


![]({{"assets/img/posts/2022-03-22/2022-03-22-TriggerConditions03.png" | relative_url}})


At the end of the settings we find the "Trigger conditions" function that allows us to define an expression that must have the value TRUE for our trigger and therefore our flow to start. We can set up to ten trigger conditions here.

### How do I specify a new trigger condition?

If we click on "Add", a field will open where we have to add our trigger condition. But what are we saying here? 

Here we have to work with expressions that we already know from our Dynamic Content:

![]({{"assets/img/posts/2022-03-22/2022-03-22-TriggerConditions04.png" | relative_url}})


To write our expression, the "Compose" Action can also help us, in case we want to check our expression:

![]({{"assets/img/posts/2022-03-22/2022-03-22-TriggerConditions06.png" | relative_url}})


Since we only want our flow to start when our SharePoint "Completed" column is equal to Yes/TRUE, we use the following "equals" expression:

```JavaScript
equals(triggerBody()?['Completed'],true)
```

Or Choice column:

```JavaScript
equals(triggerOutputs()?['body/Status/Value'],'Completed')
```

"equals" compares two values and returns "true" if the values are equal, or "false" if the values are not equal. It is important to ensure that in our "equals" true is specified as a Boolean value and not as text. 

You can now test run your flow and check, if the condition is met on the different situations.

Once we've found our expression that returns the correct results, we simply copy that expression into our trigger condition. It is important that an @ symbol is added before the expression.

![]({{"assets/img/posts/2022-03-22/2022-03-22-TriggerConditions05.png" | relative_url}})


Also, we can remove our condition: 

![]({{"assets/img/posts/2022-03-22/2022-03-22-TriggerConditions07.png" | relative_url}})

If you now save your flow and change any item within SharePoint, your flow should only trigger, when the condition is met. This will not only save you some API requests per day, but also making your flow more easily to read and getting a better overview about your flow runs.
You should consider to leave a description/note within the trigger, to help others finding it, if they are reviewing your flow.

Thanks for reading, I hope it will help you!

[Glück auf](https://en.wikipedia.org/wiki/Gl%C3%BCck_auf)

Marvin
