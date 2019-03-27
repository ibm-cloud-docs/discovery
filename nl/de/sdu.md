---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-03-07"

subcollection: discovery

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:pre: .pre}
{:important: .important}
{:deprecated: .deprecated}
{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:hide-dashboard: .hide-dashboard}
{:apikey: data-credential-placeholder='apikey'} 
{:url: data-credential-placeholder='url'}
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}
{:gif: data-image-type='gif'}

# Smart Document Understanding
{: #sdu}

Smart Document Understanding (SDU) ist eine neue Methode zum Trainieren von {{site.data.keyword.discoveryfull}} für die Extraktion von angepassten Feldern in Ihren Dokumenten. Das Anpassen der Art und Weise, wie Ihre Dokumente in {{site.data.keyword.discoveryshort}} indexiert werden, verbessert die Antworten, die von Ihrer Anwendung zurückgegeben werden.

Mit SDU annotieren Sie Felder in Ihren Dokumenten, um angepasste Konvertierungsmodelle zu trainieren. Während Sie annotieren, lernt Watson und beginnt mit der Vorhersage von Annotationen. SDU-Modelle können exportiert und für andere Sammlungen verwendet werden. 

## Unterstützte Dokumenttypen und Browser
{: #doctypes}

Unterstützte Dokumenttypen für Smart Document Understanding: 
-  Lite-Pläne: PDF, Word, PowerPoint, Excel, JSON\*, HTML\*
-  Advanced-Pläne: PDF, Word, PowerPoint, Excel, PNG\*\*, TIFF\*\*, JPG\*\*, JSON\*, HTML\* 

\* JSON- und HTML-Dokumente werden von {{site.data.keyword.discoveryfull}} unterstützt, können aber mit dem SDU-Editor nicht bearbeitet werden. Zum Ändern der Konfiguration von HTML- und JSON-Dokumenten benötigen Sie die API. Weitere Informationen finden Sie in der [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/discovery/){: new_window}.

\*\* Einzelne Bilddateien (PNG, TIFF, JPG) werden gescannt und Text, sofern vorhanden, extrahiert. PNG-, TIFF- und JPEG-Bilder, die in PDF-, Word-, PowerPoint- und Excel-Dateien eingebettet sind, werden ebenfalls gescannt und Text, sofern vorhanden, extrahiert.

Unterstützte Browser: Chrome und Firefox.

## Smart Document Understanding-Editor verwenden
{: #annotate}

Der SDU-Editor ist nur für neue Sammlungen verfügbar, die unterstützte Dokumenttypen enthalten und auf die die Aufbereitung 'Elementklassifizierung' nicht angewendet wurde. Vorhandene private Sammlungen verwenden die ursprüngliche Konfigurationsmethode. Wenn Sie den SDU-Editor für eine vorhandene Sammlung verwenden möchten, müssen Sie eine neue Sammlung erstellen und diese Dokumente in diese Sammlung hochladen. Wenn Sie den SDU-Editor nicht verwenden möchten, können Sie Ihre Konfiguration mit der API einrichten. Weitere Informationen finden Sie in der [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{/apidocs/discovery/){: new_window}.{: important}

Die Funktionen des SDU-Editors sind nur in den {{site.data.keyword.discoveryshort}}-Tools verfügbar, nicht in der API.
{: note}

So navigieren Sie im Smart Document Understanding-Editor:

Wenn Sie noch keine {{site.data.keyword.discoveryshort}}-Instanz und -Umgebung erstellt haben, finden Sie Anweisungen unter [Einführung](/docs/services/discovery?topic=discovery-getting-started#getting-started).{: tip}

1. Klicken Sie in der Anzeige **Daten verwalten** auf die Schaltfläche **Eigene Daten hochladen** und erstellen Sie eine neue private Sammlung in {{site.data.keyword.discoveryshort}}.
1. Bei Bedarf ziehen Sie Dokumente in Ihre Sammluing oder klicken Sie auf die Option zum **Von Computer aus durchsuchen**, um Dokumente hochzuladen. Nachdem der Upload abgeschlossen ist, werden die folgenden Informationen angezeigt:
   -  Die Felder, die aus Ihren Dokumenten identifiziert wurden.
   -  Aufbereitungen, die auf Ihre Dokumente angewendet wurden. Die Aufbereitungen Entitätsextraktion, Stimmungsanalyse, Kategorieklassifizierung und Konzepttagging werden von {{site.data.keyword.discoveryshort}} automatisch auf das Feld `text` angewendet (es sei denn, Sie importieren Dokumente mithilfe eines Connectors). Sie können zusätzliche Aufbereitungen zum Feld `text` hinzufügen oder daraus entfernen.
   -  Vordefinierte Abfragen können sofort ausgeführt werden.
1. Klicken Sie auf die Schaltfläche **Daten konfigurieren** in der rechten oberen Ecke. 
1. Die Anzeige **Daten konfigurieren** enthält drei Registerkarten: **Felder identifizieren**, **Felder verwalten** und **Felder aufbereiten**.

   - **Felder identifizieren** enthält den SDU-Editor. Diese Registerkarte ersetzt die Registerkarten **Konvertieren** und **Normalisieren** der ursprünglichen {{site.data.keyword.discoveryshort}}-Anzeige. 
   - **Felder verwalten** listet alle indexierten Felder auf (standardmäßig sind alle Felder indexiert). Schalten Sie alle Felder aus, die nicht indexiert werden sollen. Beispielsweise können Ihre PDFs eine laufende Kopf- oder Fußzeile enthalten, die keine nützlichen Informationen enthält, sodass Sie diese Felder aus dem Index ausschließen können. Sie können hier auch basierend auf Feldern Dokumente aufteilen. Weitere Informationen finden Sie unter [Dokumente teilen](/docs/services/discovery?topic=discovery-sdu#splitting).
   - **Felder aufbereiten** ist identisch mit der Registerkarte **Aufbereiten** in der ursprünglichen Anzeige. Weitere Informationen zu Aufbereitungen finden Sie unter [Aufbereitungen hinzufügen](/docs/services/discovery?topic=discovery-configservice#adding-enrichments). Die Option **Beispieldokumente hochladen** ist bei SDU-Sammlungen nicht verfügbar.

   Falls Sie zuvor keine Dokumente hochgeladen haben, kehren Sie zur Anzeige **Übersicht** zurück, indem Sie in der linken oberen Ecke auf den Namen Ihrer Sammlung klicken. Alternativ klicken Sie auf das Symbol ![Daten verwalten](/images/icon_yourData.png) und wählen Sie Ihre Sammlung aus. Ziehen Sie Dokumente in Ihre Sammlung oder klicken Sie auf **Von Computer aus durchsuchen**. Nach einem ersten Upload wird in der rechten oberen Ecke die Schaltfläche **Dokumente hochladen** angezeigt.
   {: important}

   Wenn Sie Smart Document Understanding verwenden, kann nur das Feld `text` aufbereitet werden. Versuchen Sie nicht, andere Felder aufzubereiten.
   {: important}

1. Öffnen Sie die Registerkarte **Felder identifizieren**. Es werden maximal zwanzig (20) Dokumente aus Ihrer Sammlung automatisch in den Smart Document Understanding-Editor geladen.

Über die Symbolleiste am oberen Rand können Sie folgende Aktionen durchführen:
- Dokument zum Annotieren auswählen
- In dem angezeigten Dokument navigieren
- Die Seitenansicht (`Einzelseitenansicht`, `Vergrößern`, `Verkleinern`), `Änderungen löschen` und `Modells importieren/exportieren`) anpassen. Klicken Sie auf `Einzelseitenansicht`, um die Anzeige umzuschalten. Sie können Ihre Annotationen und das Dokument einzeln oder zusammen anzeigen.

Sie können mit den {{site.data.keyword.discoveryshort}}-Tools auch Box-, Salesforce-, Microsoft SharePoint Online-, IBM Cloud Object Storage- und Microsoft SharePoint 2016-Datenquellen durchsuchen oder eine Web-Crawler-Suche durchführen. Klicken Sie auf die Schaltfläche **Datenquelle verbinden**; weitere Informationen hierzu finden Sie unter [Verbindung zu Datenquellen herstellen](/docs/services/discovery?topic=discovery-sources#sources). Wenn Sie mit dieser Methode eine Sammlung erstellen, werden keine Aufbereitungen automatisch angewendet.
{: tip}

## Vorgehensweise zum Annotieren eines Dokuments
{: #documents}

**Hinweis:** Tabellen werden in einem separaten Schritt annotiert.

Bevor Sie mit dem Annotieren beginnen, lesen Sie den Abschnitt [Bewährte Verfahren zum Annotieren von Dokumenten und Tabellen](/docs/services/discovery?topic=discovery-sdu#bestpractices).

1. Rechts von Ihrem Dokument wird eine Standardgruppe von Feldern angezeigt. Die verfügbaren Felder sind `answer`, `author`, `footer`, `header`, `question`, `subtitle`, `table_of_contents`, `text` und `title`. Wenn Sie eine oder mehrere neue angepasste Feldbezeichnungen erstellen möchten, klicken Sie auf **Neu erstellen**. Sie sind auf die folgende Anzahl angepasster Bezeichnungen beschränkt: Lite-Pläne - `0`, Advanced-Pläne - `5`, Premium-Pläne - `20`.
1. Klicken Sie auf der rechten Seite auf eine Feldbezeichnung, um sie zu aktivieren.
1. Klicken Sie auf den Inhalt, der dieses Feld im SDU-Editor darstellt. Das Feld wird hervorgehoben. 
   - Alternativ können Sie eine Feldbezeichnung rechts auswählen und sie in den Inhalt im SDU-Editor ziehen. 
   - Wenn Sie eine Änderung löschen möchten, klicken Sie in der Symbolleiste auf die Schaltfläche **Änderung löschen**.
1. Klicken Sie auf **Übergeben**.
   **Hinweis:** Wenn Sie annotieren, lernt Watson dabei und beginnt mit der Vorhersage von Annotationen. Fahren Sie mit dem Annotieren so lange fort, bis Watson Felder korrekt und konsistent angibt.
1. Wenn Sie mit dem Annotieren fertig sind, klicken Sie auf **Änderungen auf Sammlung anwenden**. Die Anzeige **Dokumente hochladen** wird geöffnet. Laden Sie die Dokumente erneut in Ihre Sammlung hoch. Nachdem das Hochladen abgeschlossen ist, werden Sie zur Anzeige **Daten verwalten** weitergeleitet.

Feld | Definition  
------ | ------ 
answer | In einem Frage/Antwort-Paar (oft in einer häufig gestellten Frage) ist dies die Antwort auf die Frage.
author | Der Name des Autors (oder der Autoren).
footer | Verwenden Sie diesen Tag, um Metainformationen über das Dokument (z. B. die Seitenzahl oder die Verweise) zu bezeichnen, die am Ende der Seite angezeigt werden.
header | Verwenden Sie diesen Tag, um Metainformationen über das Dokument zu bezeichnen, das oben auf der Seite angezeigt wird.
question | In einem Frage/Antwort-Paar (oft in einer häufig gestellten Frage) ist dies die Frage.
subtitle | Der sekundäre Titel des Dokuments, das annotiert wird. 
table_of_contents | Verwenden Sie diesen Tag für Listen im Inhaltsverzeichnis des Dokuments.
text | Verwenden Sie diesen Tag für Standardkopiertexte, einschließlich Absätze, Definitionen oder eine Gruppe von Wörtern, die kein Titel, Teil einer Tabelle, eine Antwort, ein Autor, ein Untertitel, eine Kopfzeile oder eine Fußzeile ist. 
title | Der Haupttitel des Dokuments, das annotiert wird.

## Vorgehensweise zum Annotieren einer Tabelle
{: #tables}

Die Tabellenannotation gibt es in der Betaversion. Eine Aussage zu Features als Betaversion finden Sie [hier](/docs/services/discovery?topic=discovery-release-notes#beta-features).
{: important}

Bevor Sie mit dem Annotieren beginnen, lesen Sie den Abschnitt [Bewährte Verfahren zum Annotieren von Dokumenten und Tabellen](/docs/services/discovery?topic=discovery-sdu#bestpractices).

1. Wählen Sie das Feld `table` auf der rechten Seite des SDU-Editors und anschließend die Tabelle im Dokument aus. 
1. Bewegen Sie den Mauszeiger über die Tabelle, um die Schaltfläche **Tabelle annotieren** anzuzeigen. Klicken Sie auf die Schaltfläche, um den Tabelleneditor zu öffnen.
1. Entwerfen Sie zunächst die Tabelle:
   - Wählen Sie das Feld `column` aus.
   - Klicken Sie auf eine Spalte in der Tabelle, um sie zu aktivieren.
   - Wählen Sie das Feld `row` aus.
   - Klicken Sie auf eine Zeile in der Tabelle, um sie zu aktivieren.

   Der Entwurf der Tabelle wird in der Tabellenvorschau auf der linken Seite angezeigt.

   **Hinweis:** Während Sie annotieren, lernt Watson und beginnt mit der Vorhersage von Annotationen.
1. Kennzeichnen Sie als Nächstes den Inhalt in der Tabelle.
1. Nachdem Sie die Tabelle mit Annotationen versehen haben, klicken Sie auf **Fertig mit Annotieren**.
1. Klicken Sie auf **Änderungen auf Sammlung anwenden**. Die Anzeige **Dokumente hochladen** wird geöffnet. Laden Sie die Dokumente erneut in Ihre Sammlung hoch. Nachdem das Hochladen abgeschlossen ist, werden Sie zur Anzeige **Daten verwalten** weitergeleitet.

Verwenden Sie dieses Video als Leitfaden: ![Video zur Tabellenannotation](images/SDU_table_demo.gif){: gif}

Feld | Definition  
------ | ------ 
body | Eine Zelle, die keine Kopfzeile ist und Informationen enthält
column header | Die Kopfzeilenzelle (falls vorhanden) für jede Spalte in der Tabelle 
multi-column header | Alle Kopfzeilenzellen, die sich über mehr als eine Spalte erstrecken
row title | Die Spaltenüberschrift für die Spalte der Zeilenüberschriften (falls vorhanden)
row header | Die Zeilenbeschriftung (falls vorhanden) für jede Zeile in der Tabelle
multi-row header | Alle Zeilenbeschriftungen, die sich über mehr als eine Zeile erstrecken

## Dokumente teilen
{: #splitting}

Die Registerkarte **Felder verwalten** enthält die Option zum **Verbessern der Abfrageergebnisse durch das Teilen Ihrer Dokumente**. Mit dieser Option können Sie Ihre Dokumente basierend auf einem Feldnamen in Segmente teilen. Nachdem ein Dokument geteilt wurde, bildet jedes Segment ein separates Dokument, das aufbereitet, indexiert und als separates Abfrageergebnis zurückgegeben wird.  

Dokumente werden basierend auf einem einzelnen Feldnamen, z. B. `title`, `author`, `question`, geteilt. 

Hinweise:

  - Die Anzahl der Segmente pro Dokument ist auf `250` begrenzt. Der gesamte verbleibende Dokumentinhalt nach dem Erreichen von `249` Segmenten wird im Segment `250` gespeichert.

  - Jedes Segment wird bei der Zählung für den Dokumentgrenzwert Ihres Plans berücksichtigt. {{site.data.keyword.discoveryshort}} indexiert so lange Segmente, bis der Plangrenzwert erreicht ist. Dokumentbegrenzungen finden Sie unter [Preisstrukturpläne für Discovery](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans).

  - PDF- und Word-Metadaten sowie alle benutzerdefinierten Metadaten werden extrahiert und mit jedem Segment in den Index aufgenommen. Jedes Segment eines Dokuments enthält identische Metadaten.

  - Wenn ein geteiltes Dokument aktualisiert wurde und erneut hochgeladen werden muss, kann es mit der Methode [Update document ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/discovery#update-a-document){: new_window} ersetzt werden. Das Dokument sollte unter Verwendung der POST-Methode der API `/environments/{umgebungs-id}/collections/{sammlungs-id}/documents/{dokument-id}` hochgeladen werden. Geben Sie dabei den Inhalt des Feldes `parent_id` eines der aktuellen Segmente als Pfadvariable `{dokument-id}` an. Alle Segmente werden überschrieben, es sei denn, die aktualisierte Version des Dokuments enthält weniger Gesamtabschnitte als das Original. Diese älteren Segmente bleiben im Index und können mit der API einzeln gelöscht werden. Details enthält die [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/discovery#delete-a-document){: new_window}. 

## Modelle importieren und exportieren
{: #import}

Nachdem Sie ein Modell mit dem SDU-Editor definiert haben, können Sie es speichern und in anderen Sammlungen wiederverwenden.

Sie können das fertige SDU-Modell mit der Symbolleiste oben im Editor importieren oder exportieren. Klicken Sie auf das letzte Symbol und wählen Sie `Modell importieren` bzw. `Modell exportieren` aus.

Exportierte Modelle haben die Dateierweiterung `.sdumodel`. 

Ein importiertes Modell soll ohne weitere Annotationen verwendet werden. Wenn Sie das Modell nach dem Import weiterhin mit Annotationen versehen, wird es vollständig überschrieben. Wenn Sie ein Modell in eine neue Sammlung importieren wollen, ist es ein bewährtes Verfahren, eine neue Sammlung zu erstellen, die nur ein Dokument enthält, das Modell zu importieren und anschließend die restlichen Dokumente hochzuladen.

## Bewährte Verfahren zum Annotieren von Dokumenten und Tabellen
{: #bestpractices}

Die Tabellenannotation gibt es in der Betaversion. Eine Aussage zu Features als Betaversion finden Sie [hier](/docs/services/discovery?topic=discovery-release-notes#beta-features).
{: important}

- Befolgen Sie alle Richtlinien und verwenden Sie konsistente Beschriftungen für alle Dokumente.
- Beschriften Sie keine Leerräume.
- Verwenden Sie die `image`-Bezeichnungen für Bilder und Diagramme.
- Text wird immer gleich behandelt, ob **fett** oder _kursiv_ gedruckt oder unterstrichen. Die Bezeichnungen basieren auf dem Kontext, nicht dem Stil. 
- Arbeiten Sie beim Beschriften eines Dokuments dieses von der ersten bis zur letzten Seite durch.
- Wenn Sie ein Element fälschlicherweise beschriften, wählen Sie eine andere Beschriftung für das Element aus, um das erste Element zu überschreiben.
- Seiten können jederzeit übergeben werden. Stellen Sie sicher, dass alle erforderlichen Beschriftungen vor der Übergabe abgeschlossen sind.
- Dokumente und Tabellen, bei denen es so scheint, als ob Text anderen Text überlagert, gelten als 'doppelt überlagert' und können nicht annotiert werden. Melden Sie diese Dokumente Ihrem Administrator.
- Dokumente und Tabellen, die mehrere Spalten mit Text auf einer einzelnen Seite enthalten, können nicht annotiert werden. Melden Sie diese Dokumente Ihrem Administrator.
- Fußnoten sollten nur dann gekennzeichnet sein, wenn sie am unteren Rand der Seite erscheinen und im Hauptteil des Textes im Dokument referenziert werden.
- Hinweise, die in Abschnitten oder Listen enthalten sind (z. B. explizit als 'Notizen' bezeichnet sind), sollten als `text` gekennzeichnet sein.
- Wenn Sie nicht sicher sind, dass die Tabelle korrekt bezeichnet wurde und das Vorschaufenster nicht mehr antwortet, sollte die Seite in Ihrem Browser neu geladen und die Tabelle erneut beschriftet werden, damit die Richtigkeit gewährleistet ist.

