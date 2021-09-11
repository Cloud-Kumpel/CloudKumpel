---
layout: post
title: "SharePoint \"erstellt von\"- und \"geändert von\"-Felder mit Power Automate und REST API aktualisieren"
date: "2020-06-12"
tags: [Office 365,Power Automate,HowTo,Deutsch,SharePoint Online,REST API]
feature-img: "assets/img/posts/2020-06-12/Image-1280.png"
author: MarvinBangert
excerpt_separator: <!--more-->
---

english version below

Im folgenden Beitrag zeige ich euch, wie Ihr die SharePoint-Felder "Erstellt von", "Geändert von", "Erstellt" und "Geändert" per REST API und Power Automate Flow anpassen könnt.

<!--more-->

Wenn über Power Automate z.B. neue Listenelemente in einer Liste erstellt werden, taucht unter "Erstellt von" oder "Geändert von" der Besitzer des Flows auf bzw. die hinterlegten Verbindungsdaten (z.B. eines Service Accounts).

![]({{"assets/img/posts/2020-06-12/Image-1275.png" | relative_url}})

In unserem Fall möchten wir gerne die SharePoint Standardfelder "Geändert", "Geändert von", "Erstellt" und "Erstellt von" direkt anpassen, sodass wir ohne Hilfsspalte etc. auskommen. In unserem Beispiel haben wir zwei Listen, wenn in Liste A ein Element erstellt wird, soll ein neues Element in Liste B erstellt werden. Dazu verwenden wir den SharePoint Trigger "Wenn ein Element erstellt wird" und die Aktion "Element erstellen".

Als nächsten nutzen wir die SharePoint Aktion "HTTP Anfrage an SharePoint senden". Über den Parameter "ValidateUpdateListItem()" ist es möglich per REST API auf bestimmte Elemente zuzugreifen und ein paar der SharePoint-Felder zu aktualisieren. Hier ist meine Konfiguration, um das neu erstellte Element zu überarbeiten:

![]({{"assets/img/posts/2020-06-12/Image-1276-1.png" | relative_url}})

Führen wir nun unseren Flow erneut aus, erscheint unter "Erstellt von" und "Geändert von" der Account, der auch in der anderen Liste das Element erstellt hat.

![]({{"assets/img/posts/2020-06-12/Image-1277.png" | relative_url}})

Hier ist der gesamte Code:

```R
Site Address: "https://<tenant>.sharepoint.com/sites/<sitename>"

Method: POST

URI: "_api/web/lists/getbytitle('SharePointList')/items('@{body('Create_item')?['ID']}')/ValidateUpdateListItem()"

Headers:
  Accept: application/json;odata=verbose
  Content-Type: application/json;odata=verbose

Body:
  {
    "formValues": [
      {
        "FieldName": "Editor",
        "FieldValue": "[{'Key':'<Benutzername als Claims>'}]"
      },
      {
        "FieldName": "Author",
        "FieldValue": "[{'Key':'<Benutzername als Claims>'}]"
      },
      {
        "FieldName": "Modified",
        "FieldValue": "06/12/2020 07:25 PM"
      },
      {
        "FieldName": "Created",
        "FieldValue": "06/12/2020 07:25 PM"
      }
    ],
    "bNewDocumentUpdate": true
  }
```

Wir haben auch die Möglichkeit das "Geändert" und "Erstellt" Datum anzupassen, dies wird über die Feldnamen "Modified" und "Created" bearbeitet.

In der URI nutzen wir die ID unseres SharePoint Elements, welches wir über "Create item" im vorherigen Schritt erstellt haben. Die Liste geben wir über den Listennamen "SharePointList" an.

Im Body geben wir den Account für "Erstellt von" (Author) und "Geändert von" (Editor) als Claims schreibweise an. Hierzu nutzen wir aus dem Trigger "When an item is created" das Feld "Created by Claims".

### SharePoint Versionen

Eine weitere Frage, die ich mir gestellt hatte: "Was passiert mit den SharePoint Versionen, wenn das Element geändert wird?". Hierzu dient der Parameter am Ende des Body "bNewDocumentUpdate". Ist dieses auf "true" gesetzt, dann wird die bestehende Version überschrieben, also obwohl das Element in Power Automate vorher durch unseren Service Account erstellt wurde, taucht dieser danach im Elementcontext nicht mehr auf, ist der Parameter auf "false" gesetzt, erhalten wir zwei Versionen in SharePoint

\[caption id="attachment\_358" align="alignnone" width="781"\]![]({{"assets/img/posts/2020-06-12/Image-1278.png" | relative_url}}) bNewDocumentUpdate = true\[/caption\] \[caption id="attachment\_359" align="alignnone" width="726"\]![]({{"assets/img/posts/2020-06-12/Image-1279.png" | relative_url}}) bNewDocumentUpdate = false\[/caption\]

Ich hoffe der Beitrag war hilfreich! Vielen Dank fürs lesen!

# Update SharePoint fields "created by" and "modified by" using Power Automate and REST API

If you try to create a new SharePoint list item using Power Automate, you may have noticed that the "created by" and "modified by" fields are always set to the flow owner or the registered connections within the flow (e.g. a service account). At this point, you may consider using a custom column to set the actual user and created or modified date.

![]({{"assets/img/posts/2020-06-12/Image-1275.png" | relative_url}})

In this case, we want to update the SharePoint standard columns "Created", "Created by", "Modified" and "Modified by" to the actual user and date without using a custom column. In this example, we have to lists, if you create an item in list A Power Automate should create an item in list B. We are using the SharePoint Trigger "When an item is created" and the action "create item" to achieve this.

Then we use the action "Send an HTTP request to SharePoint" to send our REST API to SharePoint Online. With the parameter "ValidateUpdateListItem()" within your "URI" you can update a specific SharePoint element within your SharePoint list.  
This is my configuration to update a created item within SharePoint:  
![]({{"assets/img/posts/2020-06-12/Image-1276-1.png" | relative_url}})

When we start our flow again, you will see that we created an item and updated the "Created by" and "Modified by" fields.

![]({{"assets/img/posts/2020-06-12/Image-1277.png" | relative_url}})

This is my whole code:

```
Site Address: "https://<tenant>.sharepoint.com/sites/<sitename>"

Method: POST

URI: "_api/web/lists/getbytitle('SharePointList')/items('@{body('Create_item')?['ID']}')/ValidateUpdateListItem()"

Headers:
  Accept: application/json;odata=verbose
  Content-Type: application/json;odata=verbose

Body:
  {
    "formValues": [
      {
        "FieldName": "Editor",
        "FieldValue": "[{'Key':'<Username in Claims>'}]"
      },
      {
        "FieldName": "Author",
        "FieldValue": "[{'Key':'<Username in Claims>'}]"
      },
      {
        "FieldName": "Modified",
        "FieldValue": "06/12/2020 07:25 PM"
      },
      {
        "FieldName": "Created",
        "FieldValue": "06/12/2020 07:25 PM"
      }
    ],
    "bNewDocumentUpdate": true
  }
```

We are also able to update the "created" and "modified" SharePoint fields by the field names "Modified" and "Created".

Within the URI we use the SharePoint item ID we created in the "Create item" action. The name of the list is "SharePointList".

In the body, we set the account for "created by" (Author) and "modified by" (Editor) as claims (i:0#.f|membership|name@tenant.onmicrosoft.com). We use the dynamic content "Created by Claims" from the trigger "When an item is created".

### SharePoint Versionen

Another question I asked myself was: "What happens to the SharePoint versions if I update the element?". You can use the parameter at the end of the body "bNewDocumentUpdate" to control the SharePoint versions. If you set it to "true", the existing version will be updated too, if you set it to "false" you will create another version within SharePoint:

\[caption id="attachment\_358" align="alignnone" width="781"\]![]({{"assets/img/posts/2020-06-12/Image-1278.png" | relative_url}}) bNewDocumentUpdate = true\[/caption\] \[caption id="attachment\_359" align="alignnone" width="726"\]![]({{"assets/img/posts/2020-06-12/Image-1279.png" | relative_url}}) bNewDocumentUpdate = false\[/caption\]

I hope you find this article helpful! Thanks for reading!

Thanks to Ano mepanis' article: [https://anomepani.github.io/posts/how-to-update-created-by-and-modified-by-field-in-sharepoint-list-using-rest-api/](https://anomepani.github.io/posts/how-to-update-created-by-and-modified-by-field-in-sharepoint-list-using-rest-api/)
