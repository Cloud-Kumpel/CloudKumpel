---
layout: post
title: "Power Automate: SharePoint Liste durch HTTP-Anforderung aktualisieren"
date: "2020-03-09"
tags: [Office 365,Power Automate,HowTo,REST API]
feature-img: "assets/img/posts/2020-03-09/Image-315.png"
author: MarvinBangert
excerpt_separator: <!--more-->
---

In Power Automate können wir auch direkt per REST API Änderungen in SharePoint vornehmen. So können wir eine bestehenden Listeneintrag aktualisieren oder auch eine komplett neue SharePoint Site Collection erstellen. In diesem Beitrag werden wir einen bestehenden Listeneintrag in einer SharePoint Liste aktualisieren.
<!--more-->

Wenn ihr noch wenig Erfahrung im Umgang mit SharePoint REST-Diensten habt, kann ich den Microsoft Docs Artikel "Grundlegendes zum SharePoint REST-Dienst" empfehlen: [https://docs.microsoft.com/de-de/sharepoint/dev/sp-add-ins/get-to-know-the-sharepoint-rest-service](https://docs.microsoft.com/de-de/sharepoint/dev/sp-add-ins/get-to-know-the-sharepoint-rest-service)

![]({{"assets/img/posts/2020-03-09/Image-316.png" | relative_url}})

Zuerst geben wir die SharePoint Seiten URL an, auf der wir unsere Liste finden

Nun wählen wir die Methode aus. Hier können wir zwischen folgenden Methoden wählen:

GET - Lesen einer Ressource  
PUT - Erstellen oder Aktualisieren einer Ressource  
POST - Aktualisieren oder Hinzufügen einer Ressource  
PATCH - Aktualisieren einzelner Eigenschaften einer Ressource  
DELETE - Löschen einer Ressource

Wir wählen hier die "POST"-Methode.  
Unter URI wählen wir nun den Pfad zu unserem Listenelement (ID) in unserer Liste an: "\_api/web/lists/getbytitle('Liste')/items('@{triggerBody()\['number'\]}')"

"@{triggerBody()\['number'\]}" steht hierbei für die Eingabe aus unserem Trigger

![]({{"assets/img/posts/2020-03-09/Image-324.png" | relative_url}})

Um zu Überprüfen, ob wir unseren URI-Pfad richtig angegeben haben, können wir diesen direkt im Browser eingeben. Hier sollten wir ein XML erhalten mit allen Informationen zu unserem Listeneintrag (mindestens ein Listenelement muss in der Liste existieren, ansonsten erhält man keine vollständige Informationen zurück):

![]({{"assets/img/posts/2020-03-09/images/Image-321.png" | relative_url}})

Wir benötigen später auch noch Informationen aus diesem XML.

Da das XML im Browser sehr unübersichtlich ist, nutze ich gerne Visual Studio Code, um das Ergebnis aufzubereiten. Wir fügen den gesamten XML-Code in ein leeres Editorfenster in VS Code ein und können dann über die Tastenkombination "STRG+K" + "M" (bitte nacheinander drücken) den Sprachenmodus auswählen (XML). Danach sollten bereits einzelne Abschnitte farblich hervorgehoben werden.

Zur übersichtlichen Formatierung drücken wir jetzt noch "ALT+Shift+F". Schon erhalten wir eine gut leserlich formatierte XML Struktur (ich nutze hierbei die Erweiterung "XML Tools" von Josh Johnson):

![]({{"assets/img/posts/2020-03-09/Image-320.png" | relative_url}})

Zurück zu unserer Power Automate Aktion. Als nächstes müssen wir verschiedene Header angeben:

<table><tbody><tr><td>Accept</td><td>Application/json;odata=verbose</td></tr><tr><td>Content-Type</td><td>Application/json;odata=verbose</td></tr><tr><td>X-HTTP-Method</td><td>MERGE</td></tr><tr><td>IF-MATCH</td><td>*</td></tr></tbody></table>

Unter Text müssen wir nun noch folgenden Text eingeben, um zu definieren welche Informationen aktualisiert werden sollen:

```JSON
{"__metadata": 
    {"type": "SP.Data.<Listenname>ListItem"},
    "<interner Spaltenname>": "<Wert>"
}
```

> Die Textstruktur erhalten wir auch, wenn wir einmal die Aktion über die Methode "GET" ausführen, das zurückgegebene JSON können wir dann anpassen.

Den Wert für <Listenname> in "SP.Data.<Listenname>ListItem" erhalten wir aus dem XML-Code unter "category term".

Dann geben wir die internen SharePoint-Spaltennamen ein, sowie den Wert, den wir eintragen möchten. Den internen Namen erhalten wir auch jeweils aus dem XML unter "content"-"m:properties"-"d:<interner Spaltenname>".  
Hier ein Beispiel:

```JSON
{"__metadata": 
    {"type": "SP.Data.ListeListItem"},
    "Title": "FlowTest",
    "Number": "5"
}
```

![]({{"assets/img/posts/2020-03-09/Image-328.png" | relative_url}})

Hier noch das Ergebnis unseres ersten Tests:

![]({{"assets/img/posts/2020-03-09/Image-326.png" | relative_url}})

![]({{"assets/img/posts/2020-03-09/Image-327.png" | relative_url}})
