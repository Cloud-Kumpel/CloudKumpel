---
layout: post
title: "#MSIgnite - Power Platform Updates"
date: "2021-03-04"
tags: [Power Automate,Power Apps,Power BI,Power Fx,Deutsch,Power Virtual Agents,UI Flows,Ignite]
feature-img: "assets/img/posts/2021-03-04/Ignite_Header.png"
author: MarvinBangert
excerpt_separator: <!--more-->
---

Am Dienstag, 02.03.2021, um 17:30 Uhr CET ist die #MSIgnite 2021 mit der Keynote von Microsoft CEO [Satya Nadella](https://twitter.com/SatyaNadella) gestartet. Zuerst stellte Satya fünf Schlüsselattribute der nächsten Generation von Cloudinnovationen vor:

<!--more-->

- Ubiquitous and decentralized computing
- Sovereign data and ambient intelligence
- Empowered creators and communities everywhere
- Economic opportunity for the global workforce
- Trust by design

Danach tauchten wir mit Technical Fellow für AI und Mixed Reality [Alex Kipman](https://twitter.com/akipman) ab und sahen eine Vorstellung der neusten Microsoft Plattform: [Microsoft Mesh](https://www.microsoft.com/en-us/mesh). Der Kern von Microsoft Mesh ist eine 3D-Digitalisierung des Nutzers für Meetings als Hologramm oder Avatar, die Teilnahme kann über HoloLens 2, VR Headset, Smartphone, Tablet oder am PC stattfinden.

[![Introducing Microsoft Mesh](http://img.youtube.com/vi/Jd2GK0qDtRg/0.jpg)](https://www.youtube.com/watch?v=Jd2GK0qDtRg "Introducing Microsoft Mesh")

© Bereitgestellt von Microsoft

# Power Platform

Um 22 Uhr CET zeigte uns [Charles Lamanna](https://twitter.com/clamanna) (Corporate Vice President, Low Code Platform) die neusten Features und Ankündigungen der Power Platform. Zuerst ein paar allgemeine Zahlen und Fakten:

- Über 500 Millionen mehr Apps werden in den nächsten 5 Jahren gebaut als in den letzten 40 Jahren
- 50% der digitalen Arbeit kann durch heutige Technik automatisiert werden
- 1 Millionen Entwickler fehlen
- 86% der Unternehmen haben Probleme technische Talente einzustellen
- The Great Lockdown: 42% US-Mitarbeiter\*Innen arbeiten remote
- 5,2% Rückgang des globalen BIP

**Teach everyone to code ➔ Turn everyone into a developer with low code**

## Power Platform Fokus Themen

![]({{"assets/img/posts/2021-03-04/Image-2274.png" | relative_url}}) © Microsoft

## Ankündigungen

### Power Automate Desktop

Power Automate Desktop ist nun in Windows 10 enthalten, um lokale Aufgaben und Prozesse automatisiert ausführen zu können. Endanwender\*Innen von Windows 10 erhalten so die Möglichkeit, ohne zusätzliche Kosten, Ihre eigene Produktivität durch die RPA (Robotic Process Automation) Lösung von Microsoft zu erhöhen und diese direkt einzusetzen. Über RPA können manuelle Prozesse, zum Beispiel das Übertragen von Informationen aus einer Excel-Tabelle in ein Online-Formular, ohne Programmierkenntnisse automatisiert werden.

Weitere Informationen:  
Power Automate Blog: [Automate tasks with Power Automate Desktop for Windows 10](https://flow.microsoft.com/en-us/blog/automate-tasks-with-power-automate-desktop-for-windows-10-no-additional-cost/)  
  

Kostenfrei herunterladen und starten: [aka.ms/GetStarted-PAD](https://aka.ms/getstarted-pad)

[![Power Automate Desktop](http://img.youtube.com/vi/lwpAvKkk2Hc/0.jpg)](https://www.youtube.com/watch?v=lwpAvKkk2Hc "Power Automate Desktop")

© Bereitgestellt von Microsoft

### Microsoft Power Fx

Microsoft Power Fx ist das neuste Mitglied der Microsoft Power Platform und ist eine Open Source Programmiersprache für die Power Platform basierend auf Microsoft Excel. Drei Gründe für Power Fx:

- **Power Fx ist open source**  
    Über GitHub soll die Sprache für alle offen bereitgestellt werden, um Innovationen und neue Möglichkeiten zu schaffen
- **Power Fx basiert auf Microsoft Excel**  
    Bereits bekannte Formeln aus Microsoft Excel erleichtern den Einstieg in Power Fx
- **Power Fx ist für Low-Code gebaut**  
    Die Basis für Power Fx ist bereits in Power Apps Canvas Apps enthalten, diese Funktionalitäten werden zukünftig auch in der gesamten Power Platform zur Verfügung stehen: Microsoft Dataverse, Microsoft Power Automate, Microsoft Power Virtual Agents und noch mehr.

Roadmap:  
Juni 2021:

- Formular basierte Model-Driven App Anpassungen
- Formular basierte Dataverse Plugins

Ende 2021:

- Dataverse berechnete Spalten
- AI Builder Datenvorbereitung
- Power Virtual Agents

Weitere Informationen:  
Power Apps Blog: [Introducing Microsoft Power Fx](https://powerapps.microsoft.com/en-us/blog/introducing-microsoft-power-fx-the-low-code-programming-language-for-everyone/)  
Power Apps Blog: [What is Power Fx?](https://powerapps.microsoft.com/en-us/blog/what-is-microsoft-power-fx/)  
Microsoft Docs: [Microsoft Power Fx overview](https://docs.microsoft.com/en-us/power-platform/power-fx/overview)

![]({{"assets/img/posts/2021-03-04/Image-2272.png" | relative_url}}) © Microsoft

### Power BI Premium Per User Lizenz

Zum 2. April 2021 wird die Power BI Premium Per User Lizenz für 20$ / User / Monat für alle verfügbar sein und für Kunden, die bereits Power BI Pro einsetzen, entweder als Standalone oder über E5, wird der Preis nur $10 / User / Monat betragen!

Die Power BI Premium Per User Lizenz wurde bereits auf der letzten Microsoft Ignite im Oktober 2020 angekündigt und war zuletzt in der Private, sowie Public Preview. Die Premium Per User Lizenz beinhaltet dabei alle Power BI Pro Funktionalitäten und noch weitere Funktionen wie automatisches Machine Learning, Cognitive Services, Deployment Pipelines, Advanced Security und vieles mehr.

![]({{"assets/img/posts/2021-03-04/PremiumFeatures-forGIF_White_520x360_REV.gif" | relative_url}})

### Direct Query support for Dataverse in Power BI

Neben Import, wobei eine Kopie der Daten in Power BI geladen wird, können Daten aus Dataverse nun auch direkt über Direct Query angebunden werden.

Vorteile von Direct Query:

- Visualisierung über sehr große Datensätze
- Immer Nutzung von den aktuellen Daten, keine Datenaktualisierung erforderlich
- Kein 1 GB Datenlimit

![]({{"assets/img/posts/2021-03-04/Image-2273.png" | relative_url}}) © Microsoft

### Endpoint Filtering

anwendbar über DLP (Data Loss Prevention) Policies im Power Platform Admin Center. Für einzelne Konnektoren können nun Endpunkte (IP-Adresse oder FQDN) konfiguriert werden, über die auf den Konnektor zugegriffen werden darf oder geblockt wird. 

![]({{"assets/img/posts/2021-03-04/Image-2264.png" | relative_url}}) © Microsoft

### Connector action controls

Es müssen nun nicht mehr Konnektoren komplett blockiert werden, sondern es können einzelne Aktionen der Konnektoren blockiert und erlaubt werden. Zum Beispiel für den Twitter-Konnektor können alle "lesen"-Aktionen freigegeben werden, aber alle "schreiben"-Aktionen blockiert werden.

![]({{"assets/img/posts/2021-03-04/Image-2265.png" | relative_url}}) © Microsoft

### Tenant Isolation

Über Regeln kann definiert werden, ob Verbindungen zwischen externen Azure ADs blockiert oder erlaubt werden. Dies können eingehende und ausgehende Verbindungen sein, sodass ein Tenant komplett isoliert oder nur für ausgewählte andere Tenants freigegeben werden kann.

![]({{"assets/img/posts/2021-03-04/Image-2266.png" | relative_url}}) © Microsoft

### Tenant wide analytics

Über das Power Platform Admin Center können nun neue Berichte eingesehen werden, die über die gesamte Power Platform gehen und so jede App, jeden Flow und jeden Bericht sehen, die im Tenant erstellt wurden, welche Personen damit arbeiten, welche Konnektoren genutzt werden und potenzielle Risiken über alle Umgebungen.

![]({{"assets/img/posts/2021-03-04/Image-2267.png" | relative_url}}) © Microsoft

### Microsoft Information Protection support

(Later this year)

MIP (Microsoft Information Protection) wird auch für Dataverse zur Verfügung stehen, sodass Daten mit Ihrer entsprechenden Sensibilität gekennzeichnet werden können. Dieses Label ist dann direkt dem Eintrag zugeordnet, egal wo es in der Power Platform genutzt wird.

![]({{"assets/img/posts/2021-03-04/Image-2268.png" | relative_url}}) © Microsoft

### Pro Developers + Power Platform = No Limits

![]({{"assets/img/posts/2021-03-03/Image-2269.png" | relative_url}}) © Microsoft

### Azure Networking Connectivity

(Later this year)

Aus der Power Platform können direkt Verbindungen zu Azure Virtual Network aufgebaut werden.

![]({{"assets/img/posts/2021-03-04/Image-2270.png" | relative_url}}) © Microsoft

### Customer managed key

(Later this year)

Eigene Keys aus Azure Key Vault können erstellt werden, um Daten in Dataverse direkt zu verschlüsseln.

![]({{"assets/img/posts/2021-03-04/Image-2271.png" | relative_url}}) © Microsoft

... und viele weitere Ankündigungen zu anderen Microsoft 365, Dynamics 365 und Azure Themen!
