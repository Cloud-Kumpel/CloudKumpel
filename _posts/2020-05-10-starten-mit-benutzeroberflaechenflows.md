---
layout: post
title: "Starten mit Benutzeroberflächenflows"
date: "2020-05-10"
tags: [Power Automate,Get Started,Deutsch,UI Flows]
feature-img: "assets/img/posts/2020-05-10/Image-1135.png"
author: MarvinBangert
excerpt_separator: <!--more-->
---

Seit dem 02. April 2020 sind "beaufsichtigte" Benutzeroberflächenflows (engl. attended UI Flows / UI = User Interface) generell verfügbar. Ich nutze heute mal den Tag, um ein paar Einblicke in UI Flows zu geben und den ersten Automatismus zu erstellen.

<!--more-->

### Was genau sind Benutzeroberflächenflows?

Benutzeroberflächenflows in Power Automate ermöglichen die Automatisierung von Prozessen für Anwendungen auf dem Desktop oder im Browser, für die es keine eigenen Schnittstellen (APIs) gibt, um diese über einen Konnektor zu automatisieren. Dazu nutzen Benutzeroberflächenflows die RPA-Funktionen (Robotic Process Automation), die es ermöglichen wiederholende Schritte aufzuzeichnen und automatisiert abzuspielen.

### Was ist der Unterschied zwischen "Beaufsichtigte" und "Unbeaufsichtigte" Benutzeroberflächenflows?

Beaufsichtigte (engl. Attended) Benutzeroberflächenflows werden auf dem jeweiligen Desktop oder im Browser des Benutzers ausgeführt, der Benutzer kann dabei die einzelnen Schritte überwachen, hat in dieser Zeit aber nicht die Möglichkeit etwas anderes auf dem Desktop zu erledigen, da sonst Fehler entstehen könnten. Der Flow übernimmt sozusagen die Steuerung.

Unbeaufsichtigte (engl. Unattended) Benutzeroberflächenflows werden im Hintergrund und hier kann unterbrechungsfrei gearbeitet werden. Aufgrund der aktuellen Situation wurden unbeaufsichtigte Benutzeroberflächenflows nicht, wie anfangs geplant, am 02. April 2020 generell verfügbar, sondern sind für Juni 2020 geplant. Weitere Informationen gibt es in den [Microsoft Docs](https://docs.microsoft.com/en-us/power-platform-release-plan/2020wave1/power-automate/unattended-automation-ui-flows) und in diesem Microsoft [Blog Post](https://cloudblogs.microsoft.com/dynamics365/bdm/2020/03/23/our-commitment-to-customers-to-help-ensure-business-continuity/)

### Welche Voraussetzungen müssen erfüllt sein?

- Microsoft Edge-Browser (Version 80 oder höher) oder Google Chrome-Browser
- Browsererweiterungen
    - UIFlow Browsererweiterung (EXE-Datei wird bei der ersten Nutzung heruntergeladen) für Desktop-Anwendungen
    - Selendium IDE (Open Source) Browsererweiterung für Browser-Anwendungen
- Einen Lizenzplan "Pro Benutzer mit beaufsichtigter RPA" oder optional mit dem Add-On "unbeaufsichtigte RPA"  
    Weitere Informationen und Preise: [https://flow.microsoft.com/de-de/ui-flows/](https://flow.microsoft.com/de-de/ui-flows/)  
    - Common Data Service wird benötigt, dies ist im Plan enthalten

### Benutzeroberflächenflow erstellen

Fangen wir nun an unseren ersten Benutzeroberflächenflow zu erstellen:

1. [Power Automate](https://flow.microsoft.com) öffnen
2. Auf "Meine Flows" und dann auf "Benutzeroberflächenflows"  
    ![]({{"assets/img/posts/2020-05-10/Image-866.png" | relative_url}})
3. Entweder oben auf "Neu" oder auf "Benutzeroberflächenflow erstellen" klicken  
    ![]({{"assets/img/posts/2020-05-10/Image-841.png" | relative_url}})
4. Nun können wir zwischen Desktop-App oder Web-App wählen. Wir wollen eine Desktop-App automatisieren:  
    ![]({{"assets/img/posts/2020-05-10/Image-842.png" | relative_url}})
5. Wir vergeben einen Namen und klicken auf "Weiter"  
    ![]({{"assets/img/posts/2020-05-10/Image-843.png" | relative_url}})
6. Nun müssen wir mindestens eine Bezeichnung erstellen. Je nachdem was wir genau automatisieren möchten, sind hier mehrere Bezeichnungen erforderlich. Diese Bezeichnungen nutzen wir als Platzhalter oder Variablen für unsere Werte. In diesem Beitrag möchten wir zwei einfache Zahlen multiplizieren. Also erstellen wir zwei Bezeichnungen:  
    ![]({{"assets/img/posts/2020-05-10/Image-857.png" | relative_url}})
7. Wenn die UIFlow Erweiterung noch nicht installiert ist, müssen wir dies nun erledigen.  
    ![]({{"assets/img/posts/2020-05-10/Image-845.png" | relative_url}})  
    Sobald die EXE-Datei heruntergeladen ist, diese öffnen  
    ![]({{"assets/img/posts/2020-05-10/Image-846.png" | relative_url}})  
    Hier den Installationspfad und die Checkboxen auswählen:  
    ![]({{"assets/img/posts/2020-05-10/Image-847.png" | relative_url}}) ![]({{"assets/img/posts/2020-05-10/Image-848.png" | relative_url}})  
    Nach Abschluss der Installation muss der Rechner einmal neu gestartet werden.  
    ![]({{"assets/img/posts/2020-05-10/Image-849.png" | relative_url}})  
    Wir können das Fenster schließen und in unserem Benutzeroberflächenflow auf "Speichern" und dann "Schließen" klicken. Danach kann der Rechner neu gestartet werden.  
    ![]({{"assets/img/posts/2020-05-10/Image-850.png" | relative_url}})  
    Sobald der Rechner neu gestartet wurde, muss die UIFlow Erweiterung im Browser aktiviert werden (falls nicht automatisch passiert). Dazu klicken wir im Edge-Browser auf die drei Punkte oben rechts und wählen "Erweiterungen":  
    ![]({{"assets/img/posts/2020-05-10/Image-851-1.png" | relative_url}})  
    Dann aktivieren wir die Erweiterung "Benutzeroberflächenflows in Microsoft Power Automate"  
    ![]({{"assets/img/posts/2020-05-10/Image-852-1.png" | relative_url}})  
    Es öffnet sich ein Pop-up Fenster, dieses müssen wir auch akzeptieren  
    ![]({{"assets/img/posts/2020-05-10/Image-853-1.png" | relative_url}})  
    Ist das erledigt, einmal die Power Automate Seite neu laden, danach zeigt unsere Aktion an, dass wir mit der Aufzeichnung starten können:  
    ![]({{"assets/img/posts/2020-05-10/Image-854.png" | relative_url}})
8. Klicken wir auf "Rekorder starten", öffnet sich ein Hinweisbildschirm und im oberen Bereich der Rekorder. Sobald wir auf "Aufzeichnen" klicken, werden unsere Schritte aufgezeichnet:  
    ![]({{"assets/img/posts/2020-05-10/Image-856.png" | relative_url}})
9. Sobald die Aufzeichnung läuft, drücken wir auf das Windows-Symbol und Suchen nach der Anwendung "Rechner"  
    ![]({{"assets/img/posts/2020-05-10/Image-867.png" | relative_url}})  
    Durch einen roten Rahmen wird erkannt, dass der Fokus auf dieser Anwendung liegt  
    ![]({{"assets/img/posts/2020-05-10/Image-868.png" | relative_url}})  
    Wir klicken im Rekorder auf "Eingabe verwenden" und wählen hier unseren "Wert1":  
    ![]({{"assets/img/posts/2020-05-10/Image-869.png" | relative_url}})  
    Danach klicken wir in der Anwendung "Rechner" auf das Eingabefeld, dies ist hier blau hervorgehoben:  
    ![]({{"assets/img/posts/2020-05-10/Image-870.png" | relative_url}})  
    Unser Beispielwert für Wert1 wird eingefügt. Danach klicken wir auf das "Plus"-Symbol im Rechner und wählen dann im Rekorder über "Eingabe verwenden" unseren Wert2 und klicken wieder in das Eingabefeld:  
    ![]({{"assets/img/posts/2020-05-10/Image-872.png" | relative_url}})  
    Auch unser zweiter Beispielwert aus Wert2 wird eingefügt. Nun klicken wir auf "="-Symbol im Rechner und sehen das Ergebnis unserer Multiplikation. Das Ergebnis möchten wir nun Speichern und später im Flow angezeigt bekommen. Dazu klicken wir im Rekorder auf "Ausgabe abrufen" und geben einen Namen und eine Beschreibung ein:  
    ![](images/Image-873-300x261.png" | relative_url}})  
    Mit "Speichern" wird diese Bezeichnung gespeichert. Danach klicken wir auf "Fertig", um den Rekorder zu beenden. In unserer Aktion wird nun ein neuer Bereich "Rechner Skript ausführen" erstellt:  
    ![]({{"assets/img/posts/2020-05-10/Image-858.png" | relative_url}})  
    Nun klicken wir auf "Weiter" und überprüfen unsere Ausgabe. Hier haben wir eine eigene Bezeichnung "Ergebnis" erstellt:  
    ![]({{"assets/img/posts/2020-05-10/Image-874.png" | relative_url}})  
    Wir klicken wieder auf "Weiter" und können unseren Benutzeroberflächenflow nun testen. Dazu geben wir zwei Zahlen für "Wert1" und "Wert2" an und klicken auf "Jetzt testen". Es erscheint eine Meldung, dass wir während der Ausführung nicht eingreifen, da sonst Fehler auftreten können:  
    ![]({{"assets/img/posts/2020-05-10/Image-859.png" | relative_url}}) ![]({{"assets/img/posts/2020-05-10/Image-860.png" | relative_url}})  
    Unser Flow führt nun automatisiert alle aufgezeichneten Schritte aus. Sobald der Flow abgeschlossen ist, sehen wir den "Erfolgreich"-Status in der Übersicht und können unseren Flow "Speichern und Schließen".

Wir können nun unseren Benutzeroberflächenflow in unseren Flows hinzufügen. Dazu ist noch ein Data Gateway erforderlich, damit wir unsere Desktop-App auch ansprechen können.

Viel Spaß beim Testen von Power Automate UI Flows.
