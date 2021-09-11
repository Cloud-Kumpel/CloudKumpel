---
layout: post
title: "Power BI: SharePoint Online Datum und Uhrzeit korrigieren"
date: "2020-03-13"
tags: [Office 365,Power BI,HowTo,SharePoint Online]
feature-img: "assets/img/posts/2020-03-13/Image-375.png"
author: MarvinBangert
excerpt_separator: <!--more-->
---

Wer in Power BI Daten aus SharePoint Online eingebunden hat und dabei vom UTC Datumsformat abweicht, ist sicherlich schon auf das Problem gestoßen, dass das Datum und die Uhrzeit in Power BI nicht richtig ist. In diesem Beitrag zeige ich, wie ihr den Fehler beheben könnt.
<!--more-->

### Ausgangslage

In SharePoint haben wir eine SharePoint-Liste erstellt und zwei Datums-Spalten hinzugefügt, ohne und mit Uhrzeit zum Vergleich:

![]({{"assets/img/posts/2020-03-13/Image-363.png" | relative_url}})

SharePoint Online Liste mit Datum und Datum und Uhrzeit

![]({{"assets/img/posts/2020-03-13/Image-364.png" | relative_url}})

Importieren der SharePoint Online Liste in Power BI

Der Datumsunterschied beträgt hier eine Stunde, dies ist auf die Zeitzone Mitteleuropäische Zeit (MEZ) zurückzuführen, die eine Stunde vor UTC (Koordinierte Weltzeit) ist. Im Sommer beträgt der Unterschied durch die Zeitumstellung auf die Mitteleuropäische Sommerzeit (MESZ) zwei Stunden vor UTC. Überprüfen wir in SharePoint unsere Regionaleinstellungen, können wir hier auch die Zeitzone festlegen:

![]({{"assets/img/posts/2020-03-13/Image-365.png" | relative_url}})

SharePoint Online Regionaleinstellungen für Deutschland

Wir können natürlich die Zeitzone hier von MEZ / MESZ (UTC +1 / UTC +2) auf UTC umstellen, allerdings ändern sich dadurch auch alle bisherigen Einträge in unserer SharePoint-Liste:

![]({{"assets/img/posts/2020-03-13/Image-366.png" | relative_url}})

Auch hier wurden nun alle Inhalte auf UTC angepasst (z.B. 12.03. statt 13.03)

### Anpassung in Power BI

Warum zeigt uns Power BI Daten in UTC an? Generell werden alle Datumsinhalte von SharePoint Online in UTC gespeichert, über die Regionaleinstellungen können wir die Zeitzonen anpassen, damit diese auch mit unserem Datum und Uhrzeit übereinstimmt. Power BI greift hierbei nur auf die Rohdaten aus SharePoint Online zu und zeigt uns deswegen alle Datums und Uhrzeiten in UTC an.

Um jetzt das Datum in Power BI auch richtig darzustellen, öffnen wir den Power Query Editor und wählen unsere Spalte aus. Wir sehen hier schon, auch für die nur Datumsspalte wird die Uhrzeit gespeichert. Die Uhrzeit wird immer mitgespeichert, im SharePoint ist diese allerdings ausgeblendet und die Uhrzeit wird auf 0 Uhr gesetzt. Dadurch, dass wir unser Datum (13.03.2020) in der Regionalzone "MEZ" gewählt haben, wird im Hintergrund das Datum für UTC als 12.03.2020 23:00:00 gespeichert (MEZ - 1 = UTC).

![]({{"assets/img/posts/2020-03-13/Image-364-1.png" | relative_url}})

Machen wir nun einen Rechtsklick auf den Spaltennamen, erhalten wir unser Menü. Wir wählen hier "Typ ändern" und dann "Datum/Uhrzeit/Zeitzone". Dadurch wird die Zeitzone zu unserer Spalte hinzugefügt (UTC +00:00):

![]({{"assets/img/posts/2020-03-13/Image-367.png" | relative_url}})

![]({{"assets/img/posts/2020-03-13/Image-368.png" | relative_url}})

Dieser Schritt ist sehr wichtig, da wir die Zeitzone in unserer Spalte benötigen, um im nächsten Schritt auf unsere Zeitzone umzustellen.  
Als nächstes klicken wir erneut mit einem Rechtsklick auf unseren Spaltennamen und wählen dieses mal "Typ ändern" - "Mit Gebietsschema"

![]({{"assets/img/posts/2020-03-13/Image-370.png" | relative_url}})

![]({{"assets/img/posts/2020-03-13/Image-371.png" | relative_url}})

Hier müssen wir jetzt für Datentyp "Datum/Uhrzeit" und Gebietsschema "Deutsch (Deutschland)" auswählen. 

![]({{"assets/img/posts/2020-03-13/Image-372.png" | relative_url}})

Durch das Hinzufügen der UTC Zeitzone zur Spalte und das Umwandeln der Spalte mit Gebietsschema, wird der Wert wieder in unsere MEZ umgewandelt. Das Ergebnis ist das gleiche Datum, wie in SharePoint Online:

![]({{"assets/img/posts/2020-03-13/Image-374.png" | relative_url}})

![]({{"assets/img/posts/2020-03-13/Image-363-1.png" | relative_url}})

Natürlich können wir für unsere Datumsspalte in Power BI den Spaltentyp nun auch auf "Datum" ändern, sodass wir lediglich das Datum ohne Uhrzeit angezeigt bekommen.

Ich hoffe dieser Beitrag hat euch beim Umgang mit Datumsformaten zwischen Power BI und SharePoint geholfen :-)
