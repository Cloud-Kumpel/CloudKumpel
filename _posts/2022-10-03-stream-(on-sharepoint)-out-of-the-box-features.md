---
layout: post
title: Stream (on SharePoint) Out Of The Box Features
date: 2022-10-03
tags:
  - SharePoint Online
  - Stream
  - Video
feature-img: /assets/img/posts/2022-07-23/header.jpg
author: get-adr
excerpt_separator: <!--more-->
lastmod: 2022-10-03T19:04:26.985Z
---
# Stream (on SharePoint) OOTB Features
Seit dem letzten [Artikel](https://cloudkumpel.de/2022/05/29/Stream-(on-SharePoint)-%C3%9Cbersicht-und-Stream-on-SharePoint-Portal.html) zu Stream (on SharePoint) ist einige Zeit vergangen und Microsoft hat ganz schön Gas gegeben was die Bereitstellung neuer (alter) Funktionen in Stream (on SharePoint) anbelangt. Also höchste Zeit sich mal anzuschauen, was man mittlerweile alles Out-Of-The-Box machen kann.
<!--more-->
## Neues im Stream on SharePoint "Portal" - Neue Aufzeichnung
Seit dem letzten Artikel hat das neue Stream Portal eine Funktion von Stream Classic erhalten,
![]({{"assets/img/posts/2022-09-04/stream-classic-record-screen.png" | relative_url}}) nämlich die Möglichkeit direkt Videos in Stream aufzuzeichnen, sei es per Webcam, Bildschirmaufnahme oder einer Kombination von beiden.
Der Button zur neuen Funktion sticht direkt ins Auge:
![]({{"assets/img/posts/2022-09-04/stream-on-sharepoint-record-button.png" | relative_url}})
Ein Klick startet der Aufnahmedialog:
![]({{"assets/img/posts/2022-09-04/stream-on-sharepoint-record-dialog.png" | relative_url}})
Hier fällt schnell auf, dass die Menüs komplett überarbeitet wurden. Der Dialog startet mit aktiver Webcam und über den ersten Button, lässt sich die Bildschirmaufzeichnung direkt dazuschalten.
Im Optionen Menü verbergen sich die Einstellungen für Audio und Video.
![]({{"assets/img/posts/2022-09-04/Stream-On-SharePoint-Optionen.png" | relative_url}})
Mit Klick auf "Nur Mikro" wird die gerade ausgewählte Kamera deaktiviert und nur Audio aufgezeichnet. So ist also auch die Podcast Aufzeichnung auf diesem Weg machbar. Was "Video Spiegeln" und "Stumm" bewirken dürfte klar sein 🙂 Hinter "Einstellungen" verbirgt sich die Auswahl der gewünschten Kamera und des Mikrofons. Hier wird auch die Aussteuerung angezeigt.
Mit Klick auf Effekte steht eine Auswahl an Filtern bereit, die in Echtzeit auf das Video angewendet werden können.
![]({{"assets/img/posts/2022-09-04/Stream-On-SharePoint-Filter.png" | relative_url}})
EIn weiterer Effekt ist das hinzufügen von Freitext zum Video. Dafür stehen folgende Schriftstile zur Verfügung:
![]({{"assets/img/posts/2022-09-04/Stream-On-SharePoint-Text.png" | relative_url}})
Über die Stift Option kann Freihand im Aufnahmebereich gemalt werden. Die Farbe und Strichbreite lässt sich dafür frei wählen.
![]({{"assets/img/posts/2022-09-04/Stream-On-SharePoint-Stift.png" | relative_url}})
Über die Foto Option kann per Drag&Drop oder per durchsuchen Dialog eine Grafik im jpg oder png Format zum Video als Overlay hinzugefügt werden. Auch das hinzufügen mehrere Grafiken ist möglich. Hinzugefügt Grafiken können skaliert, gedreht und kopiert werden.
> TIP: Transparenz in png Dateien funktioniert auch.

Über den Hintergrund Button stehen Optionen für die Konfiguration des Hintergrundes zur Verfügung. Die meisten davon dürften den Anwendern bereits von Microsoft Teams bekannt vorkommen.
Mit der Option auch nicht nur eigene Fotos als Hintergrund zu verwenden, sondern auch eigene Videos im webm oder mp4 Format auszuwählen kommen wir zu der ersten Neuerung. Außerdem lässt sich die Bildschirmfreigabe als Hintergrund verwenden:
![]({{"assets/img/posts/2022-09-04/Stream-On-SharePoint-Hintergrund.png" | relative_url}})
Ansonsten stehen Hintergrundunschärfe und die bereits bekannten Bilder zur Auswahl.

Sind alle Einstellungen und FIlter / Hintergründe wie gewünscht vorgenommen, kann die Aufnahme gestartet werde. Wie bisher können maximal 15 Minuten aufgezeichnet werden. Effekte können während der Aufnahme noch angepasst werden. So kann man beispielsweise mit dem Freihandeffekt auf die Tafel in einer Hintergrundgrafik schreiben.
![]({{"assets/img/posts/2022-09-04/Stream-On-SharePoint-Hintergrund.png" | relative_url}})
Das eigene Video Bild kann bei Nutzung eines Hintergrundbildes neben Zentriert auch nach recht- und linksunten verschoben werden:
![]({{"assets/img/posts/2022-09-04/Stream-On-SharePoint-aufnahme.png" | relative_url}})
Ist die Aufzeichnung abgeschlossen, kann das Video noch zugeschnitten werden, Also nicht benötigte Teile an Anfang und Ende können entfernt werden.
![]({{"assets/img/posts/2022-09-04/Stream-On-SharePoint-Zuschneiden.png" | relative_url}})

In meinen Tests erfolgte die Webcam Aufzeichnung mit folgenden Video Einstellungen:
- Format [MPEG-4 AVC / h264](https://de.wikipedia.org/wiki/H.264)
- Framerate: 30
- Auflösung: 1280x720px
- Seitenverhältnis: 16:9

Die Audiospur liegt wie folgt vor:
- Format: Opus
- Kanäle: 1 (Mono)
- Frequenz: 48KHz


  
Die Gesamtbitrate lag bei 1,8 MBit
[Mediainfo](https://github.com/MediaArea/MediaInfo) Details (Webcam Aufnahme):
````
General
Complete name                            : Aufzeichnung-20221003_174304.webm
Format                                   : Matroska
Format version                           : Version 4
File size                                : 908 KiB
Duration                                 : 3 s 950 ms
Overall bit rate                         : 1 883 kb/s
Writing application                      : WebRecorder-5.25.3
Writing library                          : WebRecorder-5.25.3
IsTruncated                              : Yes
FileExtension_Invalid                    : mkv mk3d mka mks

Video
ID                                       : 2
Format                                   : AVC
Format/Info                              : Advanced Video Codec
Codec ID                                 : V_MPEG4/ISO/AVC
Duration                                 : 3 s 944 ms
Width                                    : 1 280 pixels
Height                                   : 720 pixels
Display aspect ratio                     : 16:9
Frame rate mode                          : Constant
Frame rate                               : 30.169 FPS
Language                                 : English
Default                                  : Yes
Forced                                   : No

Audio
ID                                       : 1
Format                                   : Opus
Codec ID                                 : A_OPUS
Duration                                 : 3 s 950 ms
Channel(s)                               : 1 channel
Channel layout                           : C
Sampling rate                            : 48.0 kHz
Bit depth                                : 32 bits
Compression mode                         : Lossy
Language                                 : English
Default                                  : Yes
Forced                                   : No
````
Die Bildschirmaufzeichnungen eines einzelnen Browser Tabs erfolgten mit einer höheren Auflösung von:

- 1920x1036px
  
Audio wurde mit zwei Kanälen, also Stereo aufgezeichnet.

[Mediainfo](https://github.com/MediaArea/MediaInfo) Details (Browser Tab Aufnahme):
````
General
Complete name                            : Aufzeichnung-20221003_175444.webm
Format                                   : Matroska
Format version                           : Version 4
File size                                : 4.67 MiB
Duration                                 : 16 s 111 ms
Overall bit rate                         : 2 432 kb/s
Writing application                      : WebRecorder-5.25.3
Writing library                          : WebRecorder-5.25.3
IsTruncated                              : Yes
FileExtension_Invalid                    : mkv mk3d mka mks

Video
ID                                       : 2
Format                                   : AVC
Format/Info                              : Advanced Video Codec
Codec ID                                 : V_MPEG4/ISO/AVC
Duration                                 : 16 s 100 ms
Width                                    : 1 920 pixels
Height                                   : 1 036 pixels
Display aspect ratio                     : 1.85:1
Frame rate mode                          : Constant
Frame rate                               : 30.000 FPS
Language                                 : English
Default                                  : Yes
Forced                                   : No

Audio
ID                                       : 1
Format                                   : Opus
Codec ID                                 : A_OPUS
Duration                                 : 16 s 111 ms
Channel(s)                               : 2 channels
Channel layout                           : L R
Sampling rate                            : 48.0 kHz
Bit depth                                : 32 bits
Compression mode                         : Lossy
Language                                 : English
Default                                  : Yes
Forced                                   : No

````

Bei der Aufzeichnung des gesamten Bildschirms stieg die Auflösung auf:
- 1920x1200

und das Seitenverhältnis auf 16:10.
  
Allerdings reduzierte sich die Framerate auf 
- 15 fps

[Mediainfo](https://github.com/MediaArea/MediaInfo) (Bildschirmaufzeichnung):
````
General
Complete name                            : Aufzeichnung-20221003_175857.webm
Format                                   : Matroska
Format version                           : Version 4
File size                                : 4.27 MiB
Duration                                 : 43 s 693 ms
Overall bit rate                         : 820 kb/s
Writing application                      : WebRecorder-5.25.3
Writing library                          : WebRecorder-5.25.3
IsTruncated                              : Yes
FileExtension_Invalid                    : mkv mk3d mka mks

Video
ID                                       : 2
Format                                   : AVC
Format/Info                              : Advanced Video Codec
Codec ID                                 : V_MPEG4/ISO/AVC
Width                                    : 1 920 pixels
Height                                   : 1 200 pixels
Display aspect ratio                     : 16:10
Frame rate mode                          : Variable
Language                                 : English
Default                                  : Yes
Forced                                   : No

Audio
ID                                       : 1
Format                                   : Opus
Codec ID                                 : A_OPUS
Duration                                 : 43 s 693 ms
Channel(s)                               : 2 channels
Channel layout                           : L R
Sampling rate                            : 48.0 kHz
Bit depth                                : 32 bits
Compression mode                         : Lossy
Language                                 : English
Default                                  : Yes
Forced                                   : No
````
Zum Vergleich:

In Stream Classic erfolgte die Webcam Aufnahme mit 480p.
Als Video Codec wurde noch [VP8](https://de.wikipedia.org/wiki/VP8) verwendet.

Nach Bestätigung der Änderungen hat man die Möglichkeit das Video direkt herunter zu laden, ohne es zu Speichern. Beendet man die Bearbeitung mit "Veröffentlichen" wird die Aufzeichnung im Root des persönlichen OneDrive for Business gespeichert. Zugriff hat somit auch nur die Person, die das Video erstellt hat.

[Glück auf](https://en.wikipedia.org/wiki/Gl%C3%BCck_auf)

Adrian