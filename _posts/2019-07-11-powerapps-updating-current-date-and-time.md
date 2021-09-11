---
layout: post
title: "PowerApps - Updating current Date and Time"
date: "2019-07-11"
tags: [Office 365, Power Apps, HowTo]
feature-img: "assets/img/posts/2019-07-11/microsoft-powerapps-stacked400x200.png"
author: MarvinBangert
excerpt_separator: <!--more-->
---

Hey folks,

in this post i want to show you how you could create an always up to date timestamp within PowerApps. Just follow the next few steps:

<!--more-->

![Add Timer]({{"assets/img/posts/2019-07-11/Timer-300x237.png" | relative_url}})

1. In the menu bar, click on "Insert" - "Controls" and add a "Timer" to your screen
2. Now change the following Timer settings:
    1. Duration = 0
    2. AutoStart = true
    3. Repeat = true
    4. OnTimerEnd = Set(CurrentDateTime,Now())

Now the timer starts if we start the app, runs and will repeat endless times. Every time the timer ends, it will set the variable "CurrentDateTime" to the current date and time.

![]({{"assets/img/posts/2019-07-11/TimerAndLabel.png" | relative_url}})

To display the current date and time, you need to add a label to your screen and change the text:

1. Text =Text(CurrentDateTime,"dddd mm/dd/yyyy hh:mm:ss")

The current date and time should appear in the label field. If not, please start your app (play button in the upper right corner or F5) or check if your variable "CurrentDateTime" is correct.

![]({{"assets/img/posts/2019-07-11/TimerAndCurrentDateTime.png" | relative_url}})

If it works fine, you could hide the timer, so that only the label will be visible to your users. Just select the timer on your screen and change the setting:

1. Visible = false

Now you have a Timer with the current date and time in PowerApps.

If you want to use different formats, here are some more:

"ddd mm/dd/yyyy hh:mm:ss"
![]({{"assets/img/posts/2019-07-11/Timer002.png" | relative_url}})

"dd.mm.yyyy hh:mm:ss"
![]({{"assets/img/posts/2019-07-11/Timer004.png" | relative_url}})

"yyyy-mm-dd hh:mm:ss"
![]({{"assets/img/posts/2019-07-11/Timer003.png" | relative_url}})

if you want to change the shown language, just add a comma within the Text()-function:  
Text(CurrentDateTime,"dddd dd.mm.yyyy hh:mm:ss","de-DE")  
German:  
![]({{"assets/img/posts/2019-07-11/Image-1928.png" | relative_url}})

Text(CurrentDateTime,"dddd dd.mm.yyyy hh:mm:ss","nl-NL")  
Dutch:

![]({{"assets/img/posts/2019-07-11/Image-1927.png" | relative_url}})

Text(CurrentDateTime,"dddd dd.mm.yyyy hh:mm:ss","da-DK")  
Danisch:
![]({{"assets/img/posts/2019-07-11/Image-1929.png" | relative_url}})