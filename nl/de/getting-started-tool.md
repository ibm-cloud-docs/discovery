---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}

# Einführung

In diesem kurzen Lernprogramm werden die {{site.data.keyword.discoveryshort}}-Tools vorgestellt. Sie werden durch den Prozess für die Erstellung einer privaten Datensammlung geführt und erfahren, wie Sie diese durchsuchen können.
{: shortdesc}

Wenn Sie lieber mit der API arbeiten, lesen Sie den Abschnitt [Einführung in die API](/docs/services/discovery/getting-started.html).
{: tip}

## Vorbereitende Schritte
{: #before-you-begin}

Sie benötigen eine Serviceinstanz.

<!-- Remove the text marked `download` after there's no g-s tab in the catalog dashboard -->


Sie haben Ihre Serviceinstanz erstellt. Klicken Sie auf **Verwalten** und dann auf **Tool öffnen**. Fahren Sie mit [Schritt 2](/docs/services/discovery/getting-started-tooling.html#create-a-collection) fort.
{: download tip}

Wenn Sie eine {{site.data.keyword.discoveryshort}}-Serviceinstanz erstellt haben, sind alle diese Voraussetzungen bereits eingerichtet. Fahren Sie mit [Schritt 1](/docs/services/discovery/getting-started-tool.html#launch-the-tooling) fort.

1.  Rufen Sie die [{{site.data.keyword.discoveryshort}}-Seite ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.{DomainName}/catalog/services/discovery){: new_window} im {{site.data.keyword.Bluemix_notm}}-Katalog auf.
1.  Registrieren Sie sich entweder für ein kostenloses {{site.data.keyword.Bluemix_notm}}-Konto oder melden Sie sich an.
1.  Klicken Sie auf **Erstellen**.


## Schritt 1: Tools starten
{: #launch-the-tooling}

Nachdem Sie eine Instanz des {{site.data.keyword.discoveryshort}}-Service erstellt haben, landen Sie im [{{site.data.keyword.Bluemix_notm}}-Dashboard](https://console.{DomainName}/dashboard). Klicken Sie auf die {{site.data.keyword.discoveryshort}}-Serviceinstanz, um die Dashboardseite des {{site.data.keyword.discoveryshort}}-Service aufzurufen.

Klicken Sie auf der Seite **Verwalten** auf **Tool öffnen**.

<!-- To do: Add screenshot for developer console -->

Falls Sie aufgefordert werden, sich bei den Tools anzumelden, geben Sie Ihre {{site.data.keyword.Bluemix_notm}}-Berechtigungsnachweise an.

Wenn keine Seite mit Projektdetails für den {{site.data.keyword.discoveryshort}}-Service angezeigt wird, wechseln Sie auf die {{site.data.keyword.watson}} Developer Console-Seite [Projekte ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.{DomainName}/developer/watson/projects) und wählen Sie das Projekt aus.
{: tip}

<!-- Remove this text after dedicated instances have the Developer Console: begin -->

{{site.data.keyword.Bluemix_dedicated_notm}}: Wählen Sie Ihre Serviceinstanz im Dashboard aus, um die Tools zu starten.

<!-- Remove this text after dedicated instances have the Developer Console: end -->

## Schritt 2: Sammlung erstellen
{: #create-a-collection}

Ihr erster Schritt in den {{site.data.keyword.discoveryshort}}-Tools ist die Erstellung einer Datensammlung.

Eine Sammlung ist eine Gruppe von Dokumenten. *Es kann sinnvoll sein, mehrere Sammlungen zu verwenden.* Hierfür gibt es unter anderem die folgenden Gründe:

- Mit mehreren Sammlungen können Sie Ergebnisse für unterschiedliche Zielgruppen zusammenstellen.
- Die Daten sind unter Umständen so unterschiedlich, dass die gleichzeitige Abfrage aller Daten nicht zweckdienlich ist.

Die allgemein zugängliche und bereits aufbereitete {{site.data.keyword.discoverynewsshort}}-Datensammlung steht Ihnen ebenfalls zur Verfügung. Sie kann sofort abgefragt werden und Sie können umgehend mit der Erstellung von Abfragen für diese Sammlung beginnen. Ihre Konfiguration kann jedoch nicht angepasst werden; auch das Hinzufügen von Dokumenten zu {{site.data.keyword.discoverynewsshort}} ist nicht möglich.

1.  Klicken Sie auf ![Cog](images/icon_settings.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> und wählen Sie **Umgebung erstellen** aus.
1.  Sobald Ihre Umgebung bereit ist, klicken Sie auf die Schaltfläche **Eigene Daten hochladen**. Anschließend können Sie Ihre neue **Datensammlung benennen**. Vergeben Sie einen Namen für Ihre Sammlung und wählen Sie bei **Anzuwendende Konfiguration auswählen** die Option **Standardkonfiguration** aus (Sie können die Konfiguration später ändern).

Es ist eine weitere Konfiguration mit dem Namen **Standardvertragskonfiguration** verfügbar, die die Elementklassifizierung unterstützt, mit der Partei-, Natur- und Kategorienelemente aus Elementen in PDFs extrahiert werden können. Details finden Sie unter [Elementklassifizierung](/docs/services/discovery/element-classification.html#element-collection).

Sie können auch Box-, Salesforce- und Microsoft SharePoint Online-Datenquellen mit den {{site.data.keyword.discoveryshort}}-Tools durchsuchen. Klicken Sie auf die Schaltfläche **Datenquelle verbinden**; weitere Informationen hierzu finden Sie unter [Verbindung zu Datenquellen herstellen](/docs/services/discovery/connect.html).
{: tip}

## Schritt 3: Angepasste Konfiguration erstellen
{: create-custom-configuration}

Nachdem Ihre Sammlung erstellt wurde, können Sie im Uploadbereich sofort mit dem Hochladen von Inhalt beginnen. Jetzt sollen Sie jedoch eine angepasste Konfiguration erstellen und testen.

1.  Klicken Sie neben dem Namen der Sammlung auf **Wechseln** und wählen Sie die Option **Neue Konfiguration erstellen** aus. Vergeben Sie einen Namen für die Konfiguration und klicken Sie auf **Erstellen**.
1.  Nachdem Sie Ihre Konfiguration erstellt haben, können Sie sie anpassen:
    1.  Laden Sie das Beispieldokument <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link" class="style-scope doc-content"></a> herunter.
    1.  Laden Sie das Beispieldokument in der Anzeige **Beispieldokumente hochladen** hoch. Nachdem es hochgeladen wurde, können Sie auf den Dokumentnamen klicken, um die Konvertierung anzuzeigen.
1.  Jetzt ist der richtige Zeitpunkt, um die Konfiguration anzupassen. Bei dieser Task ändern Sie die Aufbereitungen, die auf jedes Dokument angewendet werden:
    1.  Klicken Sie auf den Abschnitt **Aufbereiten** der Konfiguration. Sehen Sie sich rechts in der Anzeige den generierten JSON-Code an. Blättern Sie bis zum Abschnitt *enriched_text* vor. Sie können feststellen, dass er viele Einträge *concepts* enthält.
    1.  Entfernen Sie nun die Textaufbereitung namens *concepts*, indem Sie auf das **X** neben ihr klicken, und klicken Sie dann auf **Anwenden & speichern**.
    1.  Sehen Sie sich jetzt erneut den JSON-Code an. Sie können feststellen, dass die Ausgabe geändert wurde und *concepts* nicht mehr enthält.

## Schritt 4: Dokumente hochladen
{: #upload-your-documents}

Sobald Sie mit der angepassten Konvertierung für das Beispieldokument zufrieden sind, können Sie den echten Inhalt in Ihre Sammlung einpflegen.

1. Laden Sie die drei folgenden Beispieldokumente herunter: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link" class="style-scope doc-content"></a> und <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link" class="style-scope doc-content"></a>.
1.  Klicken Sie auf ![Dateisymbol](images/icon_yourData.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> und wählen Sie Ihre Sammlung aus.
1.  Vergewissern Sie sich, dass die von Ihnen erstellte angepasste Konfiguration unter **Konfiguration** aufgeführt ist. Klicken Sie andernfalls neben dem Konfigurationsnamen auf **Wechseln** und wählen Sie Ihre angepasste Konfiguration aus.
1.  Klicken Sie auf die Schaltfläche **Dokumente hochladen** und starten Sie den Upload für die vier Beispieldokumente (test-doc1.html, test-doc2.html, test-doc3.html, test-doc4.html).
1.  Warten Sie, bis die Dokumente hochgeladen worden sind. Der Status der Dokumente wird im Abschnitt **Übersicht** angezeigt.

## Schritt 5: Abfrage erstellen
{: #build-a-query}

1.  Klicken Sie auf ![Abfragesymbol](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->, um die Abfrageseite zu öffnen. Wählen Sie Ihre Sammlung aus und klicken Sie auf **Los geht's!**
1.  Klicken Sie in der Anzeige **Abfragen erstellen** auf **Dokumente suchen** und dann auf **{{site.data.keyword.discoveryshort}}-Abfragesprache verwenden**:
    - Führen Sie Folgendes aus, um nach Ergebnissen mit Entitäten namens 'IBM' zu suchen:
        1.  Klicken Sie auf **Feld** und wählen Sie `enriched_text.entities.text` aus. Wählen Sie `enthält` als **Operator** und `IBM` als **Wert** aus. Die Abfrage `enriched_text.entities.text:IBM` wird in **Visual Query Builder** angezeigt.
        1.  Klicken Sie auf **Abfrage ausführen**. Die Abfrage gibt 4 Ergebnisse zurück.
    - Führen Sie Folgendes aus, um nach Ergebnissen mit Entitäten namens 'Watson' zu suchen:
        1.  Klicken Sie auf **Feld** und wählen Sie `enriched_text.entities.text` aus. Wählen Sie `enthält` als **Operator** und `watson` als **Wert** aus. Die Abfrage `enriched_text.entities.text:watson` wird in **Visual Query Builder** angezeigt.
        1.  Klicken Sie auf **Abfrage ausführen**. Die Abfrage gibt 2 Ergebnisse zurück.
    - Führen Sie Folgendes aus, um nach Ergebnissen mit beiden Entitäten namens 'Watson' und 'Slack' zu suchen:
        1.  Klicken Sie auf **Feld** und wählen Sie `enriched_text.entities.text` aus. Wählen Sie `enthält` als **Operator** und `watson` als **Wert** aus. Klicken Sie auf **Regel hinzufügen** und wiederholen Sie den Auswahlprozess. Wählen Sie jetzt jedoch als **Wert** die Angabe `Slack` aus. Die Abfrage `enriched_text.entities.text:watson,enriched_text.entities.text:Slack` wird in **Visual Query Builder** angezeigt.
        1.  Klicken Sie auf **Abfrage ausführen**. Die Abfrage gibt 1 Ergebnis zurück.

    Klicken Sie auf **In Abfragesprache bearbeiten**, um Abfragen unter Verwendung der {{site.data.keyword.discoveryshort}}-Abfragesprache zu erstellen. Weitere Informationen zur {{site.data.keyword.discoveryshort}}-Abfragesprache finden Sie unter [Abfragereferenz](/docs/services/discovery/query-reference.html) und [Abfragekonzepte](/docs/services/discovery/using.html).
1.  Die Ergebnisse Ihrer Abfrage werden im Abschnitt **Ergebnisse** angezeigt:
    - Die Registerkarte **Zusammenfassung** vermittelt Ihnen einen Überblick über die Abfrageergebnisse.
    - Auf der Registerkarte **JSON** werden die vollständigen JSON-Ergebnisse angezeigt.

    Für die aufgelisteten Abfragen werden auf der Registerkarte **Zusammenfassung** zunächst die (nach Relevanz sortierten) Dokumentpassagen angezeigt, gefolgt von den Namen der gefundenen Dokumente und den Ergebnissen nach Aufbereitung. **Passagen** sind kurze, relevante und aus den vollständigen Dokumenten, die von Ihrer Abfrage zurückgegeben wurden, extrahierte Auszüge.

    Den Link **Abfrage-URL**, der auf beiden Registerkarten **JSON** und **Zusammenfassung** bereitgestellt wird, können Sie sofort in Ihrer Anwendung einsetzen.

    Sie können auch auf **Natürliche Sprache verwenden** klicken und eine Abfrage in natürlicher Sprache schreiben, beispielsweise 'Partnerschaften von IBM Watson'. Weitere Informationen zu Abfragen in natürlicher Sprache finden Sie unter [Abfrage in natürlicher Sprache](/docs/services/discovery/query-parameters.html#nlq).

    Watson kann trainiert werden, um die Ergebnisse von Abfragen in natürlicher Sprache zu verbessern. Entsprechende Informationen enthält der Abschnitt [Ergebnisrelevanz mithilfe der Tools verbessern](/docs/services/discovery/train-tooling.html).

    Zusätzliche Ressourcen:
    - Weitere Informationen zum Datenschema Ihrer Dokumente werden angezeigt, wenn Sie auf das Symbol **Datenschema anzeigen** oder auf die Registerkarte **JSON** klicken. Details finden Sie unter [Discovery-Datenschema](/docs/services/discovery/using.html#discovery-schema).
    - Bei einer Bearbeitung in der {{site.data.keyword.discoveryshort}}-Abfragesprache können Sie durch Klicken auf das Symbol **?** neben einem Feld **Abfrage hier eingeben** weitere Beispiele anzeigen.

## Nächste Schritte
{: #next-steps}

Sie besitzen nun eine funktionsfähige und mit Daten bestückte {{site.data.keyword.discoveryshort}}-Serviceinstanz. Jetzt können Sie mit der Anpassung Ihrer Sammlung beginnen, indem Sie weitere Dokumente und Aufbereitungen hinzufügen sowie Konvertierungseinstellungen anpassen.
