---
layout: post
title: Lenovo ThinkVision m14t an Desktop PC nutzen
tags: [Hardware, Touch Display, Thunderbolt]
author: get-adr
excerpt_separator: <!--more-->
---
Heute von mir mal ein wahrscheinlich etwas nieschiger Post :)
Seit längerem habe ich mit dem Gedanken gespielt einen mobilen Monitor anzuschaffen, sozusagen als Dua-Display im mobile Office.
Mittlerweile findet man eine breite Auswahl in einer eben so breiten Preisspanne. 
Aufgrund des Touchdisplays mit der gleichen Digitizer Technologie wie bei meinem Notebook und dem Anschluss über ein USB-C Kabel fiehl die Wahl auf das ThinkVision m14t Display.
Würde es in dem Artikel nur um den Betrieb am Notebook gehen, könnte der Artikel hier schon zu ende sein. Kurz gesagt es funktioniert einfach.
Nun dachte ich mir aber, es wäre ja schön das Display auch an meinen Desktop PC anschließen zu können.
Worauf es dabei ankommt möchte ich hier kurz festhalten.
<!--more-->
## Die technischen Anforderungen
Das Lenovo Display verwendet wie schon geschrieben UBS-C als einzigen Anschluss.
Was bei den aktuellen Notebooks kein Problem darstellt, ist bei Desktop PCs zwar als Anschluss mittlerweile ebenfalls selbstverständlich, doch wie so oft steckt die Tücke im Detail. Neben USB Daten werden im Fall des ThinkVision Displays eben auch Display Port Signal und Strom übertragen.
Da hörte es bei meinem Desktop auch schon auf, also musste eine Lösung her, die die folgenden Funktionen nachrüstet:
- USB-C Anschluss
- Unterstützung für [USB-C dp Alt Mode](https://www.club-3d.com/de/technology/15/usb_c_over_alt_mode/)
- 10W Power Delivery, damit kein zusätzliches Netzteil für das Display nötig ist.

## Die technische Lösung
Also erst mal etwas recherchiert, welche Optionen es da überhaupt gibt. Schnell bin ich auf den Link Plus Adapter von Wacom gestoßen, dieser überführt Strom, USB und DisplayPort bzw. HDMI in ein USB-C Kabel und soll auch mit dem ThinkVision Display funktionieren. Die Aussicht auf so viele Kabel an einem Adapter fand ich nicht so gut und habe erst mal weiter gesucht.

Eine ziemlich universelle Lösung scheint die PCIe Karte UPD2018 von Sunix zu sein. Sie Liefert USB-C 3.1 mit dpAlt Mode. Das DisplayPort Signal wird hier über ein kurzes DP Kabel direkt von der Grafikkarte eingespeist. Ein Blick in das Datenblatt zeigte allerdings das nur 7,5W Leistung über USB-C abgegeben werden können. Also würde das ThinkVision Display ein zusätzliches Stromkabel benötigen, was ich gerne vermeiden wollte.

Bei der weiteren Suche bin ich darauf gestoßen, dass es für verschiedene Mainboards Thunderbolt Karten zum Nachrüsten gibt. Glücklicherweise auch für mein schon etwas älteres Gigabyte Board. Die passende Karte ist [Gigabyte GC Titan Ridge 2.0](https://www.gigabyte.com/de/Motherboard/GC-TITAN-RIDGE-rev-20). Im Gegensatz zur Sunix Karte unterstützt die Karte Power Delivery 3.0 und somit bis zu 100W Leistung über USB-C. Das DisplayPort Signal wird ebenfalls von der Grafikkarte eingespeist, hier über ein Mini Display Port Anschluss.

Somit hatte ich meine technische Lösung gefunden.

## Umsetzung
Die PCIe 4x Karte wird mit allen benötigten Kabeln geliefert:
![]({{"assets/img/posts/2022-02-20/gc1.jpg" | relative_url}})
![]({{"assets/img/posts/2022-02-20/gc1a.jpg" | relative_url}})

Die Karte hat die folgenden Anschlüsse:
- 2x UBS-C (Thunderbolt 3)
- 2x Mini Display Port In
- 1x Display Port

![]({{"assets/img/posts/2022-02-20/gc2.jpg" | relative_url}})

Je nach Mainboard muss das passende Thunderbolt-Header Kabel für das Mainboard, in meinem Fall das 5-Polige, sowie das USB-Kabel angeschlossen werden.

![]({{"assets/img/posts/2022-02-20/gc3.jpg" | relative_url}})

Um die Power Delivery 3.0 entsprechende Leistung abgeben zu können, muss nach dem Einbau auch noch das PCIe Stromkabel (6-Pol) angeschlossen werden. Für die vollen 100W sogar zwei mal..

![]({{"assets/img/posts/2022-02-20/gc4.jpg" | relative_url}})

Sind alle Kabel verbunden, natürlich auch das DisplayPort Kabel von der Grafikkarte mit dem Mini DisplayPort Eeingang der Thunderbolt karte, habe ich im BIOS die Thunderbolt Unterstützung aktiviert.

## Troubelshooting

Nach der Installation der Treiber eine kurze Schrecksekunde, das Display wurde zwar per USB Erkannt (Touch/Digitizer HID Device), aber es gab keine Display Anzeige. Ein kurzer Check der Verkabelung löste das Problem jedoch schnell. Für die Nutzung von USB-C dp Alt Mode muss der erste USB-C Anschluss verwendet werden.

Sollte danach die Touch / Digitizer Eingabe auf dem falschen Bildschirm angezeigt werden, hilft es das Tablet Setup über die Systemsteuerung auszuführen. 

![]({{"assets/img/posts/2022-02-20/win1.jpg" | relative_url}})

Zunächst wird das Setup gestartet und so lange "Enter" gedrückt, bis die Anzeige auf dem ThinkVision Display erscheint.

![]({{"assets/img/posts/2022-02-20/win2.jpg" | relative_url}})

Durch Berührung wird das Display dann als Touch Display identifiziert. Danach hat bei mir das Lenovo ThinkVision m14t vollständig wie erwartet funktioniert.

Vielleicht helfen meine Erfahrungen wenn ihr vor der gleichen Anforderung steht.

[Glück auf](https://en.wikipedia.org/wiki/Gl%C3%BCck_auf)

Adrian