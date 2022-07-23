---
layout: post
title: "Bookings with me (preview)"
date: "2022-07-23"
tags: [Bookings with me,Bookings,Outlook,Deutsch]
feature-img: "/assets/img/posts/2022-07-23/header.webp"
author: get-adr
excerpt_separator: <!--more-->
---
Wie von Microsoft angekündigt befindet sich "Bookings with me" aktuell in der Public Preview für targeted release Tenants. Ab Ende Juli soll der neue Service auch in Standard Release Tenant verfügbar sein.
Aber erst mal einen Schritt zurück, was ist eigentlich "Bookings with me"? Ähnlich wie die Bookings App oder FindTime ist Bookings with me ein Service der bei der Terminfindung bzw. Buchung helfen soll.
Im Gegensatz zu Bookings richtet sich "Bookings with me" an Einzelpersonen und nicht an Gruppen. Der größte Unterschied zu FindTime ist, dass die Terminfindung nicht Konsens basiert ist und zunächst nur 1:1 Meetings angeboten und gebucht werden können.
<!--more-->
"Bookings with me" ist über die Outlook Web App Kalender Ansicht zu erreichen, wenn eine Bookings Lizenz zugewiesen ist (mehr zu administrativen Einstellungen am Ende des Artikels).
![]({{"assets/img/posts/2022-07-23/01-OutlookLink.webp" | relative_url}})

[https://outlook.office.com/bookwithme/me](https://outlook.office.com/bookwithme/me)

Zunächst scheint alles "ausgegraut", was daran liegt, das zunächst ein Terminangebot angelegt werden muss. Ist dies erfolgt, wird die Bookingsseite vorbereitet:
![]({{"assets/img/posts/2022-07-23/02-Preparing.webp" | relative_url}})

Die Einrichtung dauerte bei mir ca. 8 Minuten.

![]({{"assets/img/posts/2022-07-23/03-prepComplete.webp" | relative_url}})

Danach kann der Freigabelink abgerufen oder das Hintergrundbanner aus einer Auswahl eingestellt werden.

![]({{"assets/img/posts/2022-07-23/04-SettingsDropDown.webp" | relative_url}})

Über das Optionenmenü findet der Anwender auch die Möglichkeit seine Booking Seite zu deaktivieren

# Privater oder öffentlicher Termin?
Auf der eigenen "Bookings with me" Seite können sowohl Öffentlich als auch Private Termine angelegt werden. Der Unterschied besteht darin, das nur öffentliche Termine für Besucher der Bookings Seite angezeigt werden. Private Termine können nur über einen direkten Link gebucht werden.

## Erstellen eines öffentlichen Termins:
Für einen Termin können die üblichen Felder gepflegt werden und natürlich lässt sich ein Termin als Teams-Besprechung konfigurieren. Über Kategorien hat man auf die eigenen Outlook Kategorien Zugriff.

![]({{"assets/img/posts/2022-07-23/05-PublicAppointment.webp" | relative_url}})


Das Zeitfenster für Termine lässt sich in 15 Minuten Schritten bis zu einer Stunde oder Benutzerdefiniert auswählen.

Termine können in der Standardkonfiguration während der Regulären Besprechungsstunden gebucht werden. Die Regulären Besprechungsstunden, sind die Zeiten die in Outlook als "Besprechungsstunden" konfiguriert sind:

![]({{"assets/img/posts/2022-07-23/06-OutlookBesprechungszeiten.webp" | relative_url}})


Voraussetzung ist natürlich das kein anderer Termin zur gleichen Zeit stattfindet.

Alternativ können benutzerdefinierte Verfügbarkeitszeiten verwendet werden. Diese Option ermöglicht es auch, "Bookings with me" Termine nur während eines definierten Zeitraums anzubieten.

![]({{"assets/img/posts/2022-07-23/07-CustomTimes.webp" | relative_url}})

### Erweiterte Optionen
In den erweiterten Optionen lassen sich Pufferzeiten vor und nach einem Termin festlegen. Die gewählte Zeit wird vor bzw. nach einem Termin addiert und entsprechend geblockt. Auf der rechten Seite werden die gewählten Pufferzeiten auch in der Terminvorschau angezeigt.

![]({{"assets/img/posts/2022-07-23/08-ErweiterteOptionen.webp" | relative_url}})

Darüber hinaus lässt sich der Terminintervall sowie die minimale und maximale Vorlaufzeit konfigurieren. bei den Vorlaufzeiten ist auch die Eingabe von benutzerdefinierten Werten möglich.

### Termin speichern und teilen

Ist der Termin wie gewünscht konfiguriert kann er gespeichert werden.

![]({{"assets/img/posts/2022-07-23/09-TerminSpeichern.webp" | relative_url}})

Der Teilen Dialog erstellt einen Link genau auf diese Terminart.

![]({{"assets/img/posts/2022-07-23/10-TeileOeffentlichenTermin.webp" | relative_url}})

## Die eigene Bookings Seite teilen
Es gibt mehrere Optionen die "Bookings with me" Seite zu teilen.

Die erste Option ist einfach die Freigabe über den öffentlichen link

![]({{"assets/img/posts/2022-07-23/11-BookingsWithMeSeiteTeilen.webp" | relative_url}})

Teilen per E-Mail öffnet einen Dialog um den Link zur "Bookings with me" Seite zu versenden. 

![]({{"assets/img/posts/2022-07-23/12-BookingSeitePerMailTeilen.webp" | relative_url}})

Die daraus resultierende E-Mail ist eher unspektakulär:

![]({{"assets/img/posts/2022-07-23/13-BookingsEinladungEMail.webp" | relative_url}})

Die dritte Teilen Option öffnet die Signatur Optionen aus der Outlook Web App in einem Dialog um den Link zur eigenen "Bookings with me" Seite der eigenen Outlook Signatur hinzuzufügen. Die ist mit Vorsicht zu genießen insbesondere dann, wenn die E-Mail Signaturen zentral verwaltet werden.

## Termin Buchen
Beim Aufruf der "Bookings with me" Seite, hat man die Wahl, ob man sich mit einem Azure AD Account anmelden, oder anonym als Gast, fortsetzen möchte.

![]({{"assets/img/posts/2022-07-23/14-BookingSite.webp" | relative_url}})

### Als Gast fortfahren
Wählt man die Gast-Option gelangt man zur Auswahl der Terminart und des Zeit Fensters.
Angezeigt werden natürlich nur die öffentlichen Termine.

![]({{"assets/img/posts/2022-07-23/15-BookingTerminGast.webp" | relative_url}})

Nach Auswahl des Datums und der Zeit kann der "Weiter" Button geklickt werden und es öffnet sich der Dialog um Name und E-Mail Adresse anzugeben.

![]({{"assets/img/posts/2022-07-23/16-GastBuchung.webp" | relative_url}})

Mit Klick auf "E-Mail-Prüfcode" wird ein Prüfcode an die angegebene E-Mail Adresse gesendet. Im folgenden Dialog muss dieser Code zur Kontrolle eingegeben werde.

![]({{"assets/img/posts/2022-07-23/16-GastBuchung.webp" | relative_url}})

Mit Klick auf Zeitplan wird der Termin geplant, ohne weitere Interaktion der Person, die den Termin auf seiner "Bookings with me" Seite angeboten hat.

![]({{"assets/img/posts/2022-07-23/17-GastPruefcodeEingabe.webp" | relative_url}})

### Mit M365 Konto anmelden und fortfahren
Setzt man die Terminbuchung als angemeldeter Benutzer fort, hat dies den Vorteil, dass die eigene Verfügbarkeit bei der Auswahl des Termin angezeigt wird:

![]({{"assets/img/posts/2022-07-23/18-BookingsTerminAngemeldet.webp" | relative_url}})

Der Klick auf "Weiter" öffnet den Buchen Dialog. Im Gegensatz zur Buchung als Gast, sind hier E-Mail Adresse und Name schon ausgefüllt. Eine Notiz kann noch hinzugefügt werden. Eine Bestätigung der E-Mail per Prüfcode ist hier natürlich auch nicht erforderlich und so kann der Termin mit Klick auf "Buchen" vereinbart werden.

![]({{"assets/img/posts/2022-07-23/19-AngemeldetBuchen.webp" | relative_url}})

Unmittelbar danach erhält man eine Termineinladung, der Betreff besteht aus der gewählten Terminart und dem Namen der Buchenden Person.

![]({{"assets/img/posts/2022-07-23/20-OutlookTermin.webp" | relative_url}})

Über den "Besprechung verwalten" kann die Besprechung bearbeitet werden. Absage des Termins geht natürlich wie gewohnt auch über den Outlook Termin.

![]({{"assets/img/posts/2022-07-23/21-OutlookTerminBearbeiten.webp" | relative_url}})

## Voraussetzungen für "Bookings with me" / Administrative Einstellungen
Lizenzenzseitig beinhalten folgende Pläne Bookings und damit "Bookings with me". 
- Office 365:  E1, E3, E5, F1, F3
- Microsoft 365: E1, E3, E5, F1, F3
- Microsoft 365:  Business Basic, Business Standard, Business Premium

Bookings und "Bookings with me" sind standardmäßig aktiviert und steht den Anwendern zur Verfügung.

![]({{"assets/img/posts/2022-07-23/22-BookingsLizenz.webp" | relative_url}})

Es gibt im Lizenzplan also keine separate App Service Plan für Bookings und Bookings with me. Eine getrennte Aktivierung / Deaktivierung von Bookings und Bookings with me Preview ist also über die Lizenzzuweisung nicht möglich.

Wenn das Ziel ist, nur bestimmten Personen das Erstellen von Bookings zu ermöglichen, aber allen Anwendern die Nutzung von Bookings with me zu erlauben geht der einfachste Weg über eine neue OWA Mailbox Policy die den Anwendern zugewiesen wird die Bookings Kalender (Mailboxen) erstellen dürfen.

Mit folgenden PowerShell befehlen wird eine neue Policy für die Nutzung von Bookings erstellt:

````powershell
New-OwaMailboxPolicy -Name "BookingsCreators"
````
und dem Anwender "Nikola Tesla" zugewiesen:
````powershell
Set-CASMailbox -Identity Nikola.Tesla@cloudkumpeldev.onmicrosoft.com -OwaMailboxPolicy "BookingsCreators"
````
Damit niemand sonst Bookings erstellen kann, wird für die Policy die allen anderen Anwendern zugewiesen ist, "OwaMailboxPolicy-Default", die Bookings Mailbox Erstellung deaktiviert:
````powershell
Set-OwaMailboxPolicy "OwaMailboxPolicy-Default" -BookingsMailboxCreationEnabled:$false
````
Quelle: [Microsoft Docs Turn Bookings On or Off](https://docs.microsoft.com/en-us/microsoft-365/bookings/turn-bookings-on-or-off?view=o365-worldwide#allow-only-selected-users-to-create-bookings-calendars)

Versucht ein Anwender dennoch eine Bookings Mailbox zu erstellen, wird folgende Fehlermeldung angezeigt:

![]({{"assets/img/posts/2022-07-23/23-NoBookingsCalendarInApp.webp" | relative_url}})

In der Bookings Teams App sieht die Meldung folgendermaßen aus:

![]({{"assets/img/posts/2022-07-23/24-NoBookingsCalendarTeams.webp" | relative_url}})

Alle Anwender können dann, entsprechend der Standardeinstellungen "Booking with me" verwenden.

Weiterführende Links:
- [Bookings with me Roadmap Eintrag](https://www.microsoft.com/en-us/microsoft-365/roadmap?filters=&searchterms=93239%2C)
- [Bookings with me in Microsoft Docs](https://docs.microsoft.com/en-us/microsoft-365/bookings/bookings-in-outlook?view=o365-worldwide)

Viel Spaß beim testen von "Bookings with me"

Danke fürs Lesen & [Glück auf](https://en.wikipedia.org/wiki/Gl%C3%BCck_auf)

  Adrian