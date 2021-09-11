---
layout: post
title: "Power Automate: \"Ausführen nach\" konfigurieren"
date: "2020-03-08"
tags: [Office 365,Power Automate,HowTo]
feature-img: "assets/img/posts/2020-03-08/Image-306.png"
author: MarvinBangert
excerpt_separator: <!--more-->
---

In Power Automate können immer wieder unvorhergesehene Ereignisse geschehen, zum Beispiel eine Genehmigung ist in einen Timeout gelaufen oder eine E-Mail konnte nicht versendet werden. Um auf diese Fehler zu reagieren, können wir in Power Automate die "Ausführen nach" Funktionalität nutzen, sodass der Besitzer benachrichtigt wird. "Ausführen nach" ist eine Funktion, um zu definieren, was soll passieren, wenn eine Aktion "erfolgreich", "fehlerhaft", "übersprungen" oder "einen Timeout" verursacht hat. "Ausführen nach" bezieht sich dabei immer auf die vorangegangene Aktion und muss auf der direkt nachfolgenden Aktion definiert werden.
<!--more-->

> "Ausführen nach" kann nicht für eine Aktion konfiguriert werden, die direkt auf einen Trigger folgt.

![]({{"assets/img/posts/2020-03-08/Image-307.png" | relative_url}})

Hier sehen wir einen sehr einfachen Flow, der mit einem manuellen Trigger startet, eine Genehmigung einfordert und dann eine E-Mail Benachrichtigung sendet. Jetzt wollen wir "was passiert, wenn die Genehmigung in einen Timeout läuft?" konfigurieren. Dazu klicken wir auf die drei Punkte der Aktion "Sende mir eine E-Mail Benachrichtigung" und wählen "Ausführen nach konfigurieren" aus.

![]({{"assets/img/posts/2020-03-08/Image-305.png" | relative_url}})

![]({{"assets/img/posts/2020-03-08/Image-306.png" | relative_url}})

Nun können wir definieren was soll passieren, wenn die Aktion "Starten und auf Genehmigung warten" den Status ändert. Standardmäßig ist immer "ist erfolgreich" ausgewählt, wenn wir also keinen Fehler haben, wird jede Aktion ausgeführt und der Flow erfolgreich abgeschlossen. Aber wir können auch definieren, was soll passieren, wenn eine Aktion nicht abgeschlossen werden kann.  
Um dies ein bisschen besser zu verdeutlichen, erstellen wir einen parallelen Branch. 

![]({{"assets/img/posts/2020-03-08/Image-308.png" | relative_url}})

Klick auf das Plus-Symbol zwischen "Sende mir eine E-Mail Benachrichtigung" und "Starten und auf Genehmigung warten", um einen parallelen Branch hinzuzufügen

![]({{"assets/img/posts/2020-03-08/Image-309-1024x193.png" | relative_url}})

![]({{"assets/img/posts/2020-03-08/Image-310-1024x306.png" | relative_url}})

![]({{"assets/img/posts/2020-03-08/Image-311-1024x187.png" | relative_url}})

Nach unserer Änderung sehen wir, dass sich der Pfeil auf der linken Branchseite geändert hat. Klicken wir auf das kleine Informationssymbol daneben, erhalten wir den Hinweis "_Ansicht, wenn "Sende mir eine E-Mail Benachrichtigung bei Timeout" unter "'Ausführen nach' konfigurieren" ausgeführt wird_". Dieser Branch wird also ausgeführt, wenn die Bedingung unter "Ausführen nach" erfüllt wird.

Hier das Ergebnis, wenn wir unseren Flow testen:

![]({{"assets/img/posts/2020-03-08/Image-314-1024x253.png" | relative_url}})

In der Fehlermeldung für "Starten und auf Genehmigung warten" sehen wir, dass die Aktion in einen Timeout gelaufen ist (keine Rückmeldung kam) und der Flow in den linken Branch gelaufen ist.

![]({{"assets/img/posts/2020-03-08/Image-312-1024x205.png" | relative_url}})

Hier gab es rechtzeitig eine Antwort auf die Genehmigung, sodass der Flow normal weiter läuft
