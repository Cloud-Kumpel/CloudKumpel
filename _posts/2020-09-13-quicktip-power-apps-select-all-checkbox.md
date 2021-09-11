---
layout: post
title: "quickTip: Power Apps select all checkbox"
date: "2020-09-13"
tags: [Power Apps,Quick Tip]
feature-img: "assets/img/posts/2020-09-13/Image-1629.png"
author: MarvinBangert
excerpt_separator: <!--more-->
---

Recently a user from the Power Apps Community asked if there is a way to make a "select all" checkbox in Power Apps? You can find the question here: [https://powerusers.microsoft.com/t5/Building-Power-Apps/1-checkbox-Select-All-checkboxes/m-p/686443#M219603](https://powerusers.microsoft.com/t5/Building-Power-Apps/1-checkbox-Select-All-checkboxes/m-p/686443#M219603)

The answer is "yes, it is possible" and today I will show you how to do it.

<!--more-->

First of all, we need our checkboxes. We will create three checkboxes "Option 1-3" and a fourth "Select all".

![]({{"assets/img/posts/2020-09-13/Image-1628.png" | relative_url}})

Then we update the default value for each "Option" Checkbox to "box\_SelectAll.value" ("box\_SelectAll" = name of your control). Now you can select either one option or if you check or uncheck "Select all" you will update all checkboxes.

Thanks for reading, hope this will help you!
