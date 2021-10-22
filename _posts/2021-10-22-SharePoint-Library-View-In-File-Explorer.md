---
layout: post
title: SharePoint Library View In File Explorer
tags: [Libraries,SharePoint Online,WebDAV,Windows Explorer, Edge, HowTo]
author: get-adr
excerpt_separator: <!--more-->
---
Back in the days in SharePoint On Prem there was a control that let you open a SharePoint Library in Windows Explorer. This was a handy feature, for example mass copying of documents.
This feature also made it to SharePoint online, but always was depending on Internet Explorer.
<!--more-->
Last year Microsoft announced that it will bring this functionality to Microsoft Edge and the Modern UI of SharePoint Online Libraries.

Today I noticed that the SharePoint part of the necessary configuration is available in one of my lab tenants, so it was time to play :)


According to the [<u>docs</u>](https://docs.microsoft.com/en-us/sharepoint/sharepoint-view-in-edge) article there are several requirements that needs to be met:

First of all, Edge needs to be on Versio 93 or newer
ConfigureViewInFileExplorer policy must be configured for Edge
The device must be managed via AD or Intune to enroll the policy
SharePoint Online PowerShell Version 16.0.21610.12000 or higher.
The SharePoint Online Tenant property ViewInFileExplorerEnabled has to be set to true.

Ok, so to configure the Edge policy, the device needs to be managed. The docs article references the ADMX templates to configure the policy via GPO or the according Intune policies.

Since my device isn't managed by Intune of my lab tenant, I thought i could simply apply the reg key documented for the GPO:

```
Windows Registry Editor Version 5.00
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Edge]
"ConfigureViewInFileExplorer"="[{\"cookies\": [\"rtFa\", \"FedAuth\"], \"domain\": \"sharepoint.com\"}]"
```
Or via GUI, create a new string value in
```
HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Edge
```
![reg edit new key]({{"assets/img/posts/2021-10-22/regedit.png" | relative_url}})
Value: 
```
[{"cookies": ["rtFa", "FedAuth"], "domain": "sharepoint.com"}]
```
**Hint:**
If you choose to add your complete SharePoint Online URL, "View in File Explorer" only works for that SharePoint Online Domain.

This policy tells Edge how to handle authentication and to open "viewinfileexplorer:" URLs for the specified domain via WebDAV.

Unfortunately it is not that easy, if I had read the whole docs article (especially the troubleshooting part), I've came over the following Error when checking the new policy via edge://policy  🤨:
![Edge Policy Error]({{"assets/img/posts/2021-10-22/policyError.png" | relative_url}})

So it looks like Edge checks, that the device is not enrolled in AD or Intune.

A quick search brought up a [<u>blog post</u>](https://hitco.at/blog/apply-edge-policies-for-non-domain-joined-devices/) of Gunnar Haslinger on how to fake the device enrollment to apply Edge policies, thanks Gunnar 🙂 Gunnar describes the process for Windows 10 but it works the same way on Windows 11.

There are two reg keys that needs to be set, to fake the device enrollment:
```
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Enrollments\FFFFFFFF-FFFF-FFFF-FFFF-FFFFFFFFFFFF] 
"EnrollmentState"=dword:00000001 
"EnrollmentType"=dword:00000000 
"IsFederated"=dword:00000000

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Provisioning\OMADM\Accounts\FFFFFFFF-FFFF-FFFF-FFFF-FFFFFFFFFFFF]
"Flags"=dword:00d6fb7f
"AcctUId"="0x000000000000000000000000000000000000000000000000000000000000000000000000"
"RoamingCount"=dword:00000000
"SslClientCertReference"="MY;User;0000000000000000000000000000000000000000"
"ProtoVer"="1.2"
```
After adding both keys and restarting Edge, the ConfigureViewInFileExplorer Edge Policy is applied:
![Edge Policy Success]({{"assets/img/posts/2021-10-22/policySuccess.png" | relative_url}})

Now it's time to configure SharePoint to offer the "View in File Explorer" option in document libraries.
If it's already available in the tenant, it's just two Command in the SharePoint Online PowerShell.
When you’re connected to your tenant just update the tenant settings:

The first command enables "View in File Explorer" option in library view menu:
```ps
Set-SPOTenant -VieInFileExplorerEnabled $true
```
The second command enables a special cookie, to let the feature work even if the "Keep me signed in" option isn't active. The persited cookie is required for "View in File Explorer" to operate correctly, if the user didn't choose "Keep me signed in" on sign-in.

```ps
Set-SPOTenant -UsePersistentCookiesForExplorerView $true
```
A quick check if the property is in place:
```ps
(get-spotenant).ViewInFileExplorerEnabled
(get-spotenant).UsePersistentCookiesForExplorerView
```
Both should return True.

Now it's time to visit a SharePoint Library.
In the view menu, a new option "View in File Explorer" is available and opens the library via WebDAV in Windows Explorer.

![View Library in File Explorer]({{"assets/img/posts/2021-10-22/viewIn.png" | relative_url}})

## To wrap things up:
Ensure you are using the newest version of Microsoft Edge and SharePoint Online PowerShell.
Configuration consists of two parts:

**Client side:**

Apply the required policy (ConfigureViewInFileExplorer) via GPO or Intune 
If the device isn't managed use the workaround.

**SharePoint side:**

Set the SharePoint Tenant Property (ViewInFileExplorerEnabled) to display the "View in File Explorer" option in the view menu, enable persistent cookies and you are good to go.
