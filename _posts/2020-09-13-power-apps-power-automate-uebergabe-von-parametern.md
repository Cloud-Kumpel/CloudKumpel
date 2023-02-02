---
title: 'Power Apps & Power Automate: Übergabe von Parametern'
date: 2020-09-13 00:00:00 Z
tags:
- Power Automate
- Power Apps
- HowTo
- Deutsch
layout: post
feature-img: assets/img/posts/2020-09-13/Image-1622.png
author: MarvinBangert
excerpt_separator: "<!--more-->"
---

In einigen Fällen ist es wichtig, dass Informationen zwischen Power Automate und Power Apps ausgetauscht werden. Diese Informationen bzw. Parameter werden meistens in unserer Anwendung in Power Apps ausgewählt und müssen dann zu einem Power Automate Flow gesendet werden. Genauso möchten wir aber auch Informationen oder Parameter zurückerhalten, sobald der Flow ausgeführt wurde.

<!--more-->

Zuerst müssen wir unseren Flow erstellen, der aus Power Apps ausgeführt werden soll. Entweder öffnen wir hierzu Power Automate über [https://flow.microsoft.com](https://flow.microsoft.com) oder wir wählen in unserer Power Apps Anwendung unser Element aus (z.B. eine Schaltfläche/einen Button) und wählen in der Navigation "Aktion" - "Power Automate". Es öffnet sich auf der rechten Seite ein weiteres Fenster.

![]({{"assets/img/posts/2020-09-13/Image-1616.png" | relative_url}})

Dort sehen wir, wenn ein Flow bereits mit dem Element verknüpft ist, welche Flows zur Verfügung stehen (sofern wir schon welche erstellt haben und diese mit dem Trigger "PowerApps" starten) oder wir können einen neuen Flow erstellen.

Zu Beginn sollte die Liste noch leer sein, also wählen wir "Neuen Flow erstellen". Es öffnet sich automatisch die Power Automate Seite und wir erhalten einige Vorlagen, die wir direkt nutzen können. Möchten wir mit einem leeren Flow starten, wählen wir ganz oben links den ersten Eintrag "PowerApps - Schaltfläche" aus. Dort wird nur der Trigger gesetzt, weitere Aktionen müssen wir selbst hinzufügen. Wir konfigurieren also unseren Flow, je nachdem welche Aufgabe dieser übernehmen soll. In diesem Fall erstellen wir einen Termin unserem Kalender. Um die Informationen wie "Betreff", "Startzeit" und "Endzeit" festzulegen und wir diese Informationen in Power Apps auswählen, müssen wir diese Informationen aus Power Apps abfragen. Hierzu gibt es den dynamischen Wert "In Power Apps fragen".

![]({{"assets/img/posts/2020-09-13/Image-1617.png" | relative_url}})

Wählen wir diesen Wert aus, wird automatisch ein neuer dynamischer Inhalt erstellt und in unsere Aktion eingefügt. Der Name dieses dynamischen Inhalts ist <Name der Aktion>\_<Name des Parameters>, also in unserem Fall "Terminerstellen(V4)\_Betreff":

![]({{"assets/img/posts/2020-09-13/Image-1618.png" | relative_url}})

In manchen Fällen kann dieser Name sehr lang oder uneindeutig werden. Es ist zu empfehlen vorher Variablen zu erstellen, die mit einem entsprechenden Namen versehen werden. Dazu nutzen wir die Aktion "Variable initialisieren":

![]({{"assets/img/posts/2020-09-13/Image-1619.png" | relative_url}})

Der Name des dynamischen Inhalts setzt sich dann wie folgt zusammen: <Name der Aktion>\_Wert.

#### Warum ist eine Variable jetzt besser als den dynamischen Inhalt direkt zu setzen?

1. Der Name des dynamischen Inhalts kann sehr lang und unübersichtlich werden
2. Dynamische Inhalte bleiben dauerhaft bestehen, da Sie nicht an dem hinzugefügtem Feld, sondern an der Aktion hängen. Zum Löschen eines Power Apps dynamischen Inhalts müssen wir die gesamte Aktion löschen.

Wenn wir mit Variablen arbeiten, können wir im weiteren Verlauf immer auf die Variable zurückgreifen.

![]({{"assets/img/posts/2020-09-13/Image-1620.png" | relative_url}})

Zum Schluss möchten wir vielleicht in Power Apps mit diesem Kalendereintrag weiterarbeiten. Damit wir diese Veranstaltung auch wiederfinden, geben wir einen eindeutigen Wert an Power Apps. Dazu nutzen wir die Aktion "Auf eine PowerApps oder einen Flow antworten" und geben den dynamischen Inhalt "ID" aus der Aktion "Termin erstellen (V4)" als Text zurück. Hier ist auch einmal unser gesamter Flow:

![]({{"assets/img/posts/2020-09-13/Image-1621.png" | relative_url}})

Wir vergeben noch einen Namen für den Flow, speichern und schließen das Fenster bzw. wechseln zurück in unsere Power Apps Anwendung. Dort sollte nun unser erstellter Flow auftauchen, diesen wählen wir aus. Der Flow wird unserer Schaltfläche hinzugefügt, das Property "OnSelect" wird automatisch gesetzt. Jetzt müssen wir diese Funktion aber noch vervollständigen. Wenn wir keine "In Power Apps fragen" im Flow verwendet haben, dann muss die Funktion ".Run(" nur mit einem ")" geschlossen werden, ansonsten müssen wir nun alle Parameter angeben, die wir übergeben möchten:

![]({{"assets/img/posts/2020-09-13/Image-1622.png" | relative_url}})

![]({{"assets/img/posts/2020-09-13/Image-1624.png" | relative_url}})

**Hinweis**: Damit der Termin erstellt werden kann, muss das Datum in ein anderes Format gebracht werden. Hierzu nutzen wir die Funktion "Text()", um das Datum umzuformatieren von "dd.mm.yyyy" zu "yyyy-mm-dd". Wenn wir dies nicht machen, erhalten wir einen Fehler im Flow.

Unsere Werte kommen aus einem Textfeld und zwei Datumsauswahlfeldern in unserer Power Apps Anwendung. Zum Schluss immer das ".Run()" mit einer Klammer schließen. Wenn wir nun unseren Button/unsere Schaltfläche klicken, wird der Flow im Hintergrund ausgeführt und der Termin in unserem Kalender erstellt.

![]({{"assets/img/posts/2020-09-13/Image-1625.png" | relative_url}})

Jetzt möchten wir aber mit diesem Termin weiterarbeiten. Dazu hatten wir bereits im Flow konfiguriert, dass wir die eindeutige ID erhalten. Diesen Wert möchten wir nun in einer Variable in Power Apps speichern. Dazu wählen wir unsere Schaltfläche/unseren Button aus und fügen um unsere "Starte Flow"-Funktion eine weitere Funktion "Set()"

Set(Variable; Wert)

- Variable: Name der Variable (z.B. varTerminId)
- Wert: Wert, den die Variable erhalten soll (unsere Antwort aus Power Automate)

Damit wir auch nur die TerminId aus dem Flow speichern, geben wir hinter unserem Run() ein ".terminid" an (sobald der Punkt gesetzt wird, sollte Power Apps den Parameter vorschlagen). Diesen Wert speichern wir dann in der Variable "varTerminId":

![]({{"assets/img/posts/2020-09-13/Image-1626.png" | relative_url}})

Wenn nun auf den Button/die Schaltfläche geklickt wird, wird die Variable auf die Termin Id gesetzt und wir können in unserer Power Apps Anwendung mit dieser Information weiterarbeiten. :-)

Ich hoffe der Beitrag hat euch geholfen!
