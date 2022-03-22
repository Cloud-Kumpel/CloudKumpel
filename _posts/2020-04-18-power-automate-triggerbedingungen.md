---
layout: post
title: "Power Automate: Triggerbedingungen"
date: "2020-04-18"
tags: [Power Automate,HowTo,Deutsch]
feature-img: "assets/img/posts/2020-04-18/Image-946.png"
author: MarvinBangert
excerpt_separator: <!--more-->
---

In Microsoft Power Automate werden Flow ausgeführt, sobald der Trigger erfüllt wird, z.B. ein Element wird in SharePoint erstellt oder bearbeitet, eine neue Microsoft Forms Umfrage wurde ausgefüllt oder eine E-Mail ist eingegangen. Doch manchmal soll der Flow nur starten, wenn eine bestimmte Bedingung erfüllt ist, etwa der SharePoint Listenwert weißt einen bestimmten Wert auf. Hierzu gibt es die Triggerbedingungen in Power Automate, auf die ich im weiteren genauer eingehen möchte.

<!--more-->

Nehmen wir das Beispiel, dass wir eine E-Mail Benachrichtigung erhalten möchten, sobald ein SharePoint Listenelement auf "Abgeschlossen" gesetzt wurde. Hierzu könnte man den SharePoint Trigger "Wenn ein Element erstell oder geändert wird" nutzen, dann eine Bedingung hinzufügen "Wenn Abgeschlossen ist gleich True" (Voraussetzung es handelt sich bei dem Feld "Abgeschlossen" um ein "Ja/Nein"-Feld) und "Wenn ja", wird eine E-Mail gesendet.

![]({{"assets/img/posts/2020-04-18/Image-944-1024x452.png" | relative_url}})

Üblicher Aufbau einer Bedingung in Power Automate

Dies hat allerdings zur Folge, dass unser Flow immer getriggert wird, sobald ein neues Element in unserer Liste erstellt oder bearbeitet wird, ganz egal, ob unser Feld Abgeschlossen gleich True oder False ist, die Überprüfung findet dann erst im Flow selbst statt. Betrachten wir allerdings die Anzahl der API-Anforderungen, die ein Benutzer durch seine Lizenz in 24 Stunden ausführen kann, könnte es bei einer hohen Bearbeitung in der SharePoint-Liste zu Problemen kommen:

| Benutzerlizenzen                                | Anzahl API-Anforderungen / 24 Stunden |
|-------------------------------------------------|---------------------------------------|
| Dynamics 365 Enterprise-Anwendungen             | 20.000                                |
| Dynamics 365 Professional                       | 10.000                                |
| Dynamics 365-Teammitglieder                     | 5.000                                 |
| Power Apps pro Benutzerplan                     | 5.000                                 |
| Power Automate pro Benutzerplan                 | 5.000                                 |
| Office-Lizenzen (mit Power Apps/Power Automate) | 2.000                                 |

(Quelle: [https://docs.microsoft.com/de-de/power-platform/admin/api-request-limits-allocations](https://docs.microsoft.com/de-de/power-platform/admin/api-request-limits-allocations#microsoft-power-platform-requests-allocations-based-on-licenses) Stand: 18.04.2020; Einschränkungen in den Lizenzen bitten dem Docs-Artikel entnehmen)

### Was ist eine Microsoft Power Platform-Anforderung?

Anforderungen bestehen aus verschiedenen Aktionen, die ein Benutzer für verschiedene Produkte ausführt. Auf einer allgemeinen Ebene ist unten aufgeführt, was einen API-Aufruf ausmacht:

- Konnektoren - Alle API-Anforderungen an Konnektoren von Power Apps oder Power Automate
- Microsoft Power Automate - Alle schrittweisen Power Automate-Aktionen
- Common Data Service - CRUD-Vorgänge (Create, Read, Update, Delete) sowie alle Spezialvorgänge wie "Teilen" oder "Zuweisen".

Achten Sie darauf, dass es für Common Data Service eine kleine Auswahl an systeminternen Vorgängen gibt, die ausgeschlossen sind, wie Anmelden, Abmelden und Systemmetadaten-Vorgänge wie getClientMetadata

(Quelle: [https://docs.microsoft.com/de-de/power-platform/admin/api-request-limits-allocations#what-is-a-microsoft-power-platform-request](https://docs.microsoft.com/de-de/power-platform/admin/api-request-limits-allocations#what-is-a-microsoft-power-platform-request) Stand: 18.04.2020)

Wir führen also immer wieder (unnötige) Anforderungen aus, obwohl unser Element noch gar nicht abgeschlossen ist.

### Wie können wir dies verhindern?

Microsoft hat hier für Microsoft Power Automate eine Funktion in die Triggereinstellungen eingebaut, mit der wir bereits im Trigger eine Bedingung integrieren können, sodass unser Flow nur startet, wenn diese Bedingung erfüllt wurde. Um diese zu finden, klicken wir auf die drei Punkte unseres Triggers und wählen "Einstellungen"

![]({{"assets/img/posts/2020-04-18/Image-945.png" | relative_url}})


![]({{"assets/img/posts/2020-04-18/Image-946.png" | relative_url}})


Am Ende der Einstellungen finden wir die Funktion "Triggerbedingungen", mit der wir einen Ausdruck definieren können, der den Wert TRUE aufweisen muss, damit unser Trigger und damit unser Flow gestartet wird. Wir können hier bis zu zehn Triggerbedingungen festlegen.

### Wie gebe Ich eine neue Triggerbedingung an?

Klicken wir auf "Hinzufügen", öffnet sich ein Feld, in dem wir unsere Triggerbedingung hinzufügen müssen. Doch was geben wir hier nun an?

Hier müssen wir mit Ausdrücken arbeiten, die wir bereits aus unserem Dynamischen Inhalt kennen:

![]({{"assets/img/posts/2020-04-18/Image-947.png" | relative_url}})


Um unseren Ausdruck zu schreiben, kann uns auch die "Aktion" Verfassen helfen, falls wir unseren Ausdruck überprüfen möchten:

![]({{"assets/img/posts/2020-04-18/Image-948.png" | relative_url}})


Da unser Flow nur starten soll, wenn unsere SharePoint Spalte "Abgeschlossen" gleich Ja/TRUE ist, nutzen wir den folgenden Ausdruck "equals":

```JavaScript
equals(triggerBody()?['Abgeschlossen'],true)
```

Durch "equals" werden werden zwei Werte miteinander verglichen und uns wird "true", wenn die Werte gleich sind, oder "false", wenn die Werte ungleich sind, zurückgegeben. Dabei ist darauf zu achten, dass in unserem "equals" true als boolischer Wert angegeben wird und nicht als Text.

Führen wir unseren Flow noch ohne Triggerbedingung aus, erhalten wir folgende Ergebnisse für "Verfassen":

![]({{"assets/img/posts/2020-04-18/Image-950.png" | relative_url}})


Ist "Abgeschlossen" gleich Ja? = true

![]({{"assets/img/posts/2020-04-18/Image-951.png" | relative_url}})


Ist "Abgeschlossen" gleich Ja? = false

Haben wir unseren Ausdruck gefunden, der die richtigen Ergebnisse liefert, kopieren wir diesen Ausdruck einfach in unsere Triggerbedingung. Wichtig dabei ist, dass vor dem Ausdruck ein @-Symbol hinzugefügt wird.

![]({{"assets/img/posts/2020-04-18/Image-952.png" | relative_url}})


Außerdem können wir unsere Bedingung entfernen:

![]({{"assets/img/posts/2020-04-18/Image-953.png" | relative_url}})


Zum Test erstellen wir in unserer SharePoint-Liste nun zwei Elemente, ein Element mit "Abgeschlossen" = Ja und ein Element mit "Abgeschlossen" = Nein. Wenn unser Ausdruck richtig ist, sollte nur ein Flow ausgeführt werden:

![]({{"assets/img/posts/2020-04-18/Image-954.png" | relative_url}})


Wir erstellen direkt nacheinander zwei SharePoint Elemente

![]({{"assets/img/posts/2020-04-18/Image-955.png" | relative_url}})


In unseren Ausführungen sehen wir nur eine Ausführung (die vor 9 Minuten ist von unserem Test mit Verfassen)

![]({{"assets/img/posts/2020-04-18/Image-957.png" | relative_url}})

Und auch wenn wir unseren Flow überprüfen, sehen wir, dass der Flow nur für das Element "Test Ja" ausgeführt wurde, wo der Wert für Abgeschlossen auf true steht.

Ich hoffe euch hat der Beitrag weitergeholfen und viel Erfolg bei der Nutzung von Triggerbedingungen in Power Automate :-)

Gruß Marvin
