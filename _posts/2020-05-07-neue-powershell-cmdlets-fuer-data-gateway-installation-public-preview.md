---
title: Neue PowerShell cmdlets für Data Gateway Installation (Public Preview)
date: 2020-05-07 00:00:00 Z
tags:
- Power Automate
- Power Apps
- Power BI
- PowerShell
- Deutsch
- Gateway
layout: post
feature-img: assets/img/posts/2020-05-07/PowerShell_Icon.png
author: MarvinBangert
excerpt_separator: "<!--more-->"
---

Am 06. Mai 2020 wurde über den Power BI Blog die Public Preview für die Automatisierung des Data Gateway angekündigt. Dabei wurden neue PowerShell cmdlets angekündigt, die die Automatisierung des Data Gateway Connectors ermöglichen.
<!--more-->

Das Module kann über folgenden Befehl installiert und hinzugefügt werden:

```PowerShell
Install-Module -Name DataGateway
```

```PowerShell
Import-Module DataGateway
```

> Hinweis:
> 
> 1\. Diese cmdlets erfordern [Power Shell 7 oder höher](https://docs.microsoft.com/en-us/powershell/scripting/whats-new/what-s-new-in-powershell-70?view=powershell-7). Weitere Informationen gibt es in der [Microsoft Online Dokumentation](https://docs.microsoft.com/en-us/powershell/gateway/overview?view=datagateway-ps)
> 
> 2\. Die aktuelle Releaseversion unterstützt die Installation eines Gateway Cluster mit nur einer Gatewayperson. Weitere Gatewaypersonen hinzufügen wird über die cmdlets aktuell nicht unterstützt.
> 
> [Automation of Data Gateway Installation(Public Preview)](https://powerbi.microsoft.com/en-us/blog/announcing-automation-of-data-gateway-installationpublic-preview/)

Weitere Informationen zum DataGateway Module gibt es hier: [https://www.powershellgallery.com/packages/DataGateway/3000.37.39](https://www.powershellgallery.com/packages/DataGateway/3000.37.39)

Hier sind die neuen cmdlets für die Installation/Configuration des Data Gateway Connectors:

Zuerst verbinden wir uns zum Data Gateway Service über:

```PowerShell
Connect-DataGatewayServiceAccount -ApplicationId <String> -ClientSecret <SecureString> [-Environment {Public | Germany | USGov | China | USGovHigh | USGovMil}] [-Tenant <String>] [<CommonParameters>]

ODER

Connect-DataGatewayServiceAccount -ApplicationId <String> -CertificateThumbprint <String> [-Environment {Public | Germany | USGov | China | USGovHigh | USGovMil}] [-Tenant <String>] [<CommonParameters>]
```

**Installieren**: Installieren des Gateways.

```PowerShell
Install-DataGateway [-AcceptConditions] [-InstallerLocation <String>] [<CommonParameters>]
```

**Konfigurieren**: Sobald die Installation abgeschlossen ist, kann das Gateway konfiguriert werden.

```PowerShell
Add-DataGatewayCluster -GatewayName <String> [-OverwriteExistingGateway] -RecoveryKey <SecureString> [-RegionKey <String>] [<CommonParameters>]
```

_**Wichtig! RecoveryKey gut speichern!**_

**Admins hinzufügen**: Jetzt können weitere Admins für zu dem Gateway hinzugefügt werden.

```PowerShell
Add-DataGatewayClusterUser [-AllowedDataSourceTypes {Sql | AnalysisServices | SAPHana | File | Folder | Oracle | Teradata | SharePointList | Web | OData | DB2 | MySql | PostgreSql | Sybase | Extension | SAPBW | AzureTables | AzureBlobs | Informix | ODBC | Excel | SharePoint | PubNub | MQ | BizTalk | GoogleAnalytics | CustomHttpApi | Exchange | Facebook | HDInsight | AzureMarketplace | ActiveDirectory | Hdfs | SharePointDocLib | PowerQueryMashup | OleDb | AdoDotNet | R | LOB | Salesforce | CustomConnector | SAPBWMessageServer | AdobeAnalytics | Essbase | AzureDataLakeStorage | SapErp | UIFlow | Unknown}] -GatewayClusterId <Guid> -PrincipalObjectId <Guid> [-RegionKey <String>] -Role {Admin | ConnectionCreator | ConnectionCreatorWithReshare} [-Scope {Individual | Organization}] [<CommonParameters>]
```

Hier sind noch weitere cmdlets, die genutzt werden können:

```PowerShell
Add-DataGatewayServiceAccount
Login-DataGateway
Login-DataGatewayServiceAccount
Logout-DataGateway
Logout-DataGatewayServiceAccount
Remove-DataGatewayServiceAccount
Set-DataGatewayServiceAccount
Add-DataGatewayClusterDatasourceUser
Get-DataGatewayCluster
Get-DataGatewayClusterDatasource
Get-DataGatewayClusterDatasourceStatus
Get-DataGatewayClusterDatasourceUser
Get-DataGatewayClusterStatus
Get-DataGatewayInstaller
Get-DataGatewayRegion
Get-DataGatewayTenantPolicy
Remove-DataGatewayCluster
Remove-DataGatewayClusterDatasource
Remove-DataGatewayClusterDatasourceUser
Remove-DataGatewayClusterMember
Remove-DataGatewayClusterUser
Set-DataGatewayCluster
Set-DataGatewayClusterDatasource
Set-DataGatewayInstaller
Set-DataGatewayTenantPolicy
Disconnect-DataGatewayServiceAccount
Get-DataGatewayAccessToken
Resolve-DataGatewayError
```

Außerdem gibt es hier noch ein [Beispiel-Skript](https://www.powershellgallery.com/packages/DataGateway/3000.37.39/Content/Samples%5CInstallAndAddDataGateway-Sample.ps1) von Microsoft.

Originaler Beitrag von Microsoft: [https://powerbi.microsoft.com/en-us/blog/announcing-automation-of-data-gateway-installationpublic-preview/](https://powerbi.microsoft.com/en-us/blog/announcing-automation-of-data-gateway-installationpublic-preview/)

Inhalt aus dem Microsoft Beitrag übernommen und durch eigene Inhalte erweitert.
