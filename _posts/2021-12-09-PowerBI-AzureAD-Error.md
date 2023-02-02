---
title: Power BI Azure AD Error - Power BI App Permission required
date: 2021-12-09 00:00:00 Z
tags:
- Azure AD
- Power BI
layout: post
author: MarvinBangert
excerpt_separator: "<!--more-->"
---

Hey folks,

today I came across a problem on a customer site within Power BI when trying to update an App and giving access to other users within a workspace. I want to share the solution with you, hope it will help you.

<!--more-->

## The error messages

![]({{"assets/img/posts/2021-12-09/PermissionNeeded.png" | relative_url}})

When trying to update an App within Power BI, you receive the error message "Permission needed: You don't have permission to search for Azure Active Directory (Azure AD) objects. Please contact your Azure AD administrator for permission.". The second error appeared when trying to give access to a workspace, you enter the user name but it will not show any results and the loading circle at the end of the textfield will go on. Maybe even show an error message like "These email addresses are invalid or duplicate"

![]({{"assets/img/posts/2021-12-09/GiveAccess.png" | relative_url}})

![]({{"assets/img/posts/2021-12-09/GiveAccessError.png" | relative_url}})


## Solution

This symptoms are sideeffects from the disabling a company setting "Users Permission To Read Other Users Enabled" within PowerShell:

```PowerShell
Set-MsolCompanySettings -UsersPermissionToReadOtherUsersEnabled $false
```


By default this is set to true, if you want to change it, please run the following:

```PowerShell
## Install the module
Install-Module -Name MSOnline

## Connect to Msol Service using Global Admin
Connect-MsolService

## Set company setting
Set-MsolCompanySettings -UsersPermissionToReadOtherUsersEnabled $true
```


It took about 15 minutes to effect on my Test-Tenant.


## More details

Checking this command within the [<u>Microsoft Docs</u>](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0#parameters), we get the following information for this parameter:

> Indicates whether to allow users to view the profile info of other users in their company. This setting is applied company-wide.
> Set to $False to disable users' ability to use the Azure AD module for Windows PowerShell to access user information for their organization.

So the basic idea with this parameter is to disable the ability of users accessing other users details like phone number, address, etc. using Azure AD PowerShell or the Microsoft Graph API Endpoint. As a side effect, this also effects to Power BI and (as far as I tested it) Microsoft Planner to disable the ability to assign tasks to users.

Thanks for reading, I hope it will help you!

[Glück auf](https://en.wikipedia.org/wiki/Gl%C3%BCck_auf)

Marvin
