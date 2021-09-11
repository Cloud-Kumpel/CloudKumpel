---
layout: post
title: "Power Automate: Configure \"run after\""
date: "2020-03-01"
tags: [Office 365, Power Automate, HowTo, Flow, Workflow]
feature-img: "assets/img/posts/2020-03-01/Image-294.png"
author: MarvinBangert
excerpt_separator: <!--more-->
---

There are several moments in Power Automate where unexpected things could happen, like an approval has timed out or send an action has failed. To react on this kind of errors, you could use the "run after" functionality from Power Automate to maybe send an email to the owner of the flow. "Run after" is a functionality to define what will happen if an action "is successful", "has failed", "is skipped" and/or "has timed out". You configure the "run after" always on the action after the action which could get in one of the four states.

> _You cannot configure run after on an action directly following a trigger_

![]({{"assets/img/posts/2020-03-01/Image-283.png" | relative_url}})

Here you see an very easy flow that starts with a manuall trigger, then starts an approval and afterwards send me an email notification. Now we want to configure what will happen if this approval has timed out, so there was no response to the approval. To do this we need to click on the three dots of our "Send me an email notification" action and select "configure run after".

![]({{"assets/img/posts/2020-03-01/Image-284.png" | relative_url}})

![]({{"assets/img/posts/2020-03-01/Image-285.png" | relative_url}})

On this screen you can define what will happen after the action "start and wait for an approval" has changed it status. In general "is successful" is always selected, so if your flow works fine, the next action will be executed. But you can also configure what will happen if your flows does not work properly. To make it a little bit more visible, i created a second branch between the actions "Start and wait for an approval" and "Send me an email notification".

![]({{"assets/img/posts/2020-03-01/Image-286.png" | relative_url}})

Click on the line between the two actions and select "add a parallel branch"

![]({{"assets/img/posts/2020-03-01/Image-291-1024x198.png" | relative_url}})

If the second branch was created, you can select an action as before. In this case i also just want to send me an email notification, so i select the same action. To define what will happen on the different notification action i already renamed them like "Send me an email notification if the approval failed or timed out" and "Send me an email notification if the approval succeed". Then click again on the three dots of each notification action to configure the run after.

![]({{"assets/img/posts/2020-03-01/Image-288-1024x306.png" | relative_url}})

![]({{"assets/img/posts/2020-03-01/Image-290-1-1024x204.png" | relative_url}})

After our changes we will see that our arrow to the left notification action has changed, if we click on the little information button right next to it, you will get the information 'View when "Send me an email notification if the approval failed or timed out" will run under "Configure run after"', so this branch will be executed if the condition we defined under "Configure run after" are valid.

Here are our results if we test our flow:

![]({{"assets/img/posts/2020-03-01/Image-292-1024x283.png" | relative_url}})

As you can see from the "Start and wait for an approval" error message "The workflow action 'Start\_and\_wait\_for\_an\_approval' timed out while waiting for webhook callback". (I modified the action to time out after 35 seconds)

![]({{"assets/img/posts/2020-03-01/Image-293-1024x230.png" | relative_url}})

In this run the approval was approved/rejected within the response time so the flow just go on
