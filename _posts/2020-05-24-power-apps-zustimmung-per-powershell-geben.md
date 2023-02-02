---
title: 'Power Apps: Zustimmung per PowerShell geben'
date: 2020-05-24 00:00:00 Z
tags:
- Power Apps
- HowTo
- Deutsch
- PowerShell
layout: post
feature-img: assets/img/posts/2020-05-24/Image-1217.png
author: MarvinBangert
excerpt_separator: "<!--more-->"
---

Moin zusammen,  
jeder, der schon einmal auf eine App aus Power App zugegriffen hat, kennt das Bild sicherlich: Bevor die App das erste Mal genutzt werden kann, muss die Zustimmung durch den Benutzer/die Benutzerin gegeben werden. Diese Zustimmung kann durch einen kurzen PowerShell-Befehl direkt für jeden Benutzer gegeben werden, der auf diese App zugreifen möchte.

<!--more-->

Um die Power Apps Admin cmdlets auszuführen, muss der Benutzer Tenant Admin sein, ansonsten wird eine Fehlermeldung ausgegeben. Zuerst müssen die Module geladen und installiert werden

```PowerShell
Install-Module -Name Microsoft.PowerApps.Administration.PowerShell
Install-Module -Name Microsoft.PowerApps.PowerShell -AllowClobber
Import-Module -Name Microsoft.PowerApps.Administration.PowerShell
Import-Module -Name Microsoft.PowerApps.PowerShell
```

Als nächstes muss man sich über die Azure AD Anmeldedaten anmelden:

```PowerShell
Add-PowerAppsAccount
```

Sobald man sich angemeldet hat, kann auch schon der PowerShell Befehl eingegeben werden

```PowerShell
Set-AdminPowerAppApisToBypassConsent -AppName <App ID>
```

Damit wird der Zustimmungsbildschirm unterdrückt und sobald der Benutzer/die Benutzerin die App das erste Mal öffnet, wird der Verbindung direkt zugestimmt. Über [https://make.powerapps.com](https://make.powerapps.com) - Daten - Verbindungen kann diese Zustimmung/Verbindung auch wieder entfernt werden.

### Wo finde ich die App ID?

Die App ID kann direkt über über https://make.powerapps.com abgerufen werden. Klicke hierzu auf "App" und wähle dann die drei Punkte der App aus. Wähle dann "Details". Dort kann dann direkt die App ID kopiert werden.

![]({{"assets/img/posts/2020-05-24/Image-1219.png" | relative_url}})

![]({{"assets/img/posts/2020-05-24/Image-1220.png" | relative_url}})

Um die Zustimmung wieder erscheinen zu lassen, kann das folgende Cmdlet genutzt werden:

```PowerShell
Clear-AdminPowerAppApisToBypassConsent -AppName <App ID>
```

Ich hoffe der Beitrag war hilfreich und viel Erfolg!
