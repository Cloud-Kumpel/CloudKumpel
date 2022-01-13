---
layout: post
title: Power Automate - Add Business Days to Date (Excludes Weekends)
tags: [Power Automate]
author: MarvinBangert
excerpt_separator: <!--more-->
---

Hey folks,

today I came across a problem on within the Power Platform forum on how to ["Add days to a date without weekends"](https://powerusers.microsoft.com/t5/Building-Flows/Add-days-to-a-date-without-wekeends/m-p/1417222#M159360).
Thanks Matthew Devaney who posted a blog post about ["How to add business days to a date in Power Apps(Excludes Weekends)"](https://www.matthewdevaney.com/how-to-add-business-days-to-a-date-in-power-apps-excludes-weekends/), so I could use this as an guideline to translate it into Power Automate.
Here you will find the code on how to add business days to a date in Power Automate:
<!--more-->
The setup is pretty simple, I just added a trigger "Manually trigger a flow" with a date input "myDate" (triggerBody()['date']) and a number input "addBusinessDays" (triggerBody()['number']).
Next I added a "compose" action and used the following code:

```
addDays(
    triggerBody()['date'],
    add(
        triggerBody()['number'],
        mul(
            div(
                sub(
                    add(
                        sub(
                            dayOfWeek(triggerBody()['date']),
                            1
                        ),
                        triggerBody()['number']
                    ),
                    1
                ),
                5
            ),
            2
        )
    )
)
```

So what's happending here? Other than in Power Apps, there are two things missing. Using "dayOfWeek()" only allows us to add a timestamp and not a date and start of the week.
Instead of defining the first day to Monday in our formula, we always start on a "Sunday" and are not able to change this. For calculation this means:

| Day | Sunday Start | Monday Start |
|-----|--------------|--------------|
| Sunday | 1 | 7 |
| Monday | 2 | 1 |
| Tuesday | 3 | 2 |
| Wednesday | 4 | 3 |
| Thursday | 5 | 4 |
| Friday | 6 | 5 |
| Saturday | 7 | 6 |
| Sunday | 1 | 7 |
| Monday | 2 | 1 |

To still get the right calculation, we subtract 1 from our date in the beginning. The second formula missing is the round(), but we are kinda lucky and Power Automate automatically rounds down the value for us, so we don't need to change anything here.

I just tested it with the same dates as Matthew did in his blogpost and I get the same results, but did not fully test it in every scenario (like leap year or within February) so please report if you notice any problems.

Thanks for reading, I hope it will help you!

[Glück auf](https://en.wikipedia.org/wiki/Gl%C3%BCck_auf)

Marvin
