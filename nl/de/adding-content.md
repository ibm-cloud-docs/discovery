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

# Inhalt hinzufügen
{: #addcontent}

Wie entscheide ich mich für das zu nutzende Dokumentuploadverfahren?
{: shortdesc}

-   Verwenden Sie die [API](/docs/services/discovery?topic=discovery-gs-api#gs-api), wenn der Upload von Inhalt mit einer vorhandenen Anwendung integriert werden soll oder Sie ein eigenes angepasstes Uploadverfahren erstellen.
-   Verwenden Sie die [{{site.data.keyword.discoveryshort}}-Tools](/docs/services/discovery?topic=discovery-getting-started#getting-started) wenn Sie zugängliche Dateien schnell hochladen möchten.
    Beim Hochladen von Dokumenten mit den {{site.data.keyword.discoveryshort}}-Tools sollten alle Dokumente einen eindeutigen Dateinamen besitzen. Falls zwei Dateien denselben Namen tragen, wird das Original beim Hochladen der neueren Version überschrieben. Falls in Ihrer Sammlung jedoch Dokumente desselben Dateinamens koexistieren sollen, muss die Dokument-ID angegeben werden. Sie können die Dokument-ID angeben, wenn Sie für den Dokumentupload die API oder Data Crawler verwenden.
-   Mit den {{site.data.keyword.discoveryshort}}-Tools oder der zugehörigen API können Sie Verbindungen zu Box-, Salesforce-, Microsoft SharePoint Online-, IBM Cloud Object Storage- und Microsoft SharePoint 2016-Datenquellen herstellen oder eine Web-Crawler-Suche durchführen. Weitere Informationen finden Sie unter [Verbindung zu Datenquellen herstellen](/docs/services/discovery?topic=discovery-sources#sources).
-   Verwenden Sie [Data Crawler](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler), falls Sie ein verwaltetes Upload für eine erhebliche Anzahl von Dateien durchführen möchten oder wenn Sie Inhalt aus einem unterstützten Repository (z. B. einer Db2-Datenbank) extrahieren wollen.

## Inhalt mit der API oder den Tools hinzufügen
{: #adding-content-with-the-api-or-tooling}

Berücksichtigen Sie die folgenden Punkte, bevor Sie Dokumente zu Ihrer Sammlung hinzufügen:

-   Die maximale Größe von Dateien, die in den {{site.data.keyword.discoveryshort}}-Service hochgeladen werden können, beträgt 50 MB.
-   Die Beispieldokumente werden nicht automatisch zur Sammlung hinzugefügt. Sie müssen sie selbst hinzufügen, wenn Sie sie im Rahmen Ihrer Sammlung verwenden wollen. (Gilt nur für Sammlungen, die vor dem Release von [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu) erstellt wurden.)
-   Nur die ersten 50.000 Zeichen jedes JSON-Feldes, das für die Aufbereitung ausgewählt ist, werden aufbereitet.
-   Beim Erstellen einer Sammlung wählen Sie die Dokumentsprache aus (Standardeinstellung ist Englisch). Eine Liste der Sprachen finden Sie unter [Sprachunterstützung](/docs/services/discovery?topic=discovery-language-support#language-support). Ihre Dokumente werden in der ausgewählten Sprache aufbereitet. Verwenden Sie in einer Sammlung jeweils nur eine einzige Sprache.
-   Folgende Dateitypen können von {{site.data.keyword.discoveryshort}} eingepflegt werden; alle anderen Dokumenttypen werden ignoriert:

Sammlung | Lite-Pläne | Advanced-Pläne 
---------------- | ------------------------------ | ------------------------------------------- 
Vorhandene Sammlungen, die vor dem Release von [Smart Document Understanding (SDU)](/docs/services/discovery?topic=discovery-release-notes#22jan19) speziell für {{site.data.keyword.discoveryfull}} erstellt wurden | Microsoft Word, PDF, HTML, JSON | Microsoft Word, PDF, HTML, JSON 
Sammlungen, die nach dem Release von [SDU](/docs/services/discovery?topic=discovery-sdu#sdu) erstellt wurden | PDF, Word, PowerPoint, Excel, JSON\*, HTML\* | PDF, Word, PowerPoint, Excel, PNG\*\*, TIFF\*\*, JPG\*\*, JSON\*, HTML\* 
    
\* JSON- und HTML-Dokumente werden von {{site.data.keyword.discoveryfull}} unterstützt, können aber mit dem SDU-Editor nicht bearbeitet werden. Zum Ändern der Konfiguration von HTML- und JSON-Dokumenten benötigen Sie die API. Weitere Informationen finden Sie in der [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/discovery/){: new_window}.

\*\* Einzelne Bilddateien (PNG, TIFF, JPG) werden gescannt und Text, sofern vorhanden, extrahiert. PNG-, TIFF- und JPEG-Bilder, die in PDF-, Word-, PowerPoint- und Excel-Dateien eingebettet sind, werden ebenfalls gescannt und Text, sofern vorhanden, extrahiert.
-   Die Dokumente in Ihrer Sammlung werden unter Verwendung der angegebenen Konfigurationsdatei konvertiert, sofern Sie keine andere Konfigurationsdatei auswählen. Informationen zum Erstellen einer Konfigurationsdatei finden Sie unter [Angepasste Konfiguration](/docs/services/discovery?topic=discovery-configservice#custom-configuration). (Gilt nur für Sammlungen, die vor dem Release von [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu) erstellt wurden.)
-   Sobald Dokumente in eine Datensammlung hochgeladen werden, werden sie unter Verwendung der für diese Sammlung ausgewählten Konfigurationsdatei konvertiert und aufbereitet. Falls Sie später bei einer Sammlung zu einer anderen Konfigurationsdatei wechseln wollen, ist dies möglich. Die Dokumente, die bereits hochgeladen wurden, bleiben jedoch gemäß der ursprünglichen Konfigurationsdatei konvertiert. Alle Dokumente, die nach dem Wechsel der Konfigurationsdatei hochgeladen werden, verwenden die neue Konfigurationsdatei. Wenn Sie die neue Konfiguration für die **gesamte** Sammlung verwenden wollen, müssen Sie eine neue Sammlung erstellen, die neue Konfigurationsdatei auswählen und alle Dokumente erneut hochladen. (Wenn Sie [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu) verwenden, werden Sie aufgefordert, Ihre Dokumente erneut hochzuladen, nachdem Sie auf die Schaltfläche **Änderungen auf Sammlung anwenden** geklickt haben.)
-   Der `Datentyp` (z. B. `text` oder `date`) von Feldern kann nicht angegeben werden. Wenn während der Dokumenteinpflegung ein Feld erkannt wird, das noch nicht im Index vorhanden ist, erkennt {{site.data.keyword.discoveryshort}} automatisch den `Datentyp` dieses Feldes, basierend auf dem Wert des Feldes für das erste indexierte Dokument.
-   Das Einpflegen eines Dokuments kann fehlschlagen, weil keine Typübereinstimmung zwischen Daten im aktuellen Dokument und ähnlichen Daten in einem zuvor eingepflegten Dokument besteht. Beispielsweise kann ein Feld in einem Dokument den Typ `date` und in einem nachfolgenden Dokument den Typ `string` besitzen.
-   Wenn Sie die angepasste Zerlegung in Tokens verwenden möchten (derzeit nur für japanische Sammlungen verfügbar, wenn die {{site.data.keyword.discoveryshort}}-API verwendet wird), muss das entsprechende Wörterverzeichnis für Ihre Sammlung vor dem Hochladen von Dokumenten hinzugefügt werden.

## Dokumente mit den Discovery-Tools hochladen
{: #upload_tooling}

1.  Erstellen Sie eine Sammlung. Weitere Informationen finden Sie unter [Service für Dokumente vorbereiten](/docs/services/discovery?topic=discovery-configservice#preparing-the-service-for-your-documents).
1.  Klicken Sie auf die Sammlung, um sie zu öffnen.
1.  Klicken Sie auf die Schaltfläche **Dokumente hochladen** und starten Sie das Upload Ihrer Dokumente durch Ziehen und Ablegen oder durch Navigieren und Auswählen.

Ihre Dokumente werden jetzt für die Konvertierung und Aufbereitung eingereiht. Die hierfür benötigte Zeit ist von der Größe Ihrer Sammlung abhängig. Nach der Indexierung und Aufbereitung werden die Details der Sammlung im Abschnitt **Übersicht** angezeigt.

-   **Identifizierte Felder** in Ihrer Sammlung (nur Smart Document Understanding.)
-   Datumsangaben für **Erstellt** und **Zuletzt aktualisiert** (klicken Sie auf **Sammlung in API verwenden**, um die Werte für die `Sammlungs-ID`, die `Konfigurations-ID` und die `Umgebungs-ID` anzuzeigen).
-   **Anzahl der Dokumente** in Ihrer Sammlung.
-   **Konfiguration**: Der Name der Konfigurationsdatei, die zum Konvertieren dieser Sammlung verwendet wird (nur bei Sammlungen, die vor dem Release von [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu) erstellt wurden).
-   **Fehler und Warnungen**

Informationen zum Herstellen von Verbindungen zu Box-, Salesforce-, Microsoft SharePoint Online-, IBM Cloud Object Storage- und Microsoft SharePoint 2016-Datenquellen oder zur Durchführung einer Web-Crawler-Suche mit den {{site.data.keyword.discoveryshort}}-Tools finden Sie im Abschnitt [Verbindung zu Datenquellen herstellen](/docs/services/discovery?topic=discovery-sources#sources).


## Dokumente mit der API hochladen
{: #upload_api}

Unter [Einführung in die {{site.data.keyword.discoveryshort}}-API](/docs/services/discovery?topic=discovery-gs-api#gs-api) finden Sie ein schrittweises Lernprogramm.

Weitere Informationen zur API enthält die [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/discovery/){: new_window}.

1.  Erstellen Sie mit der Methode `POST /v1/environments/{umgebungs-id}/collections` eine Sammlung.
1.  Verwenden Sie anschließend die Methode `POST /v1/environments/{umgebungs-id}/collections/{sammlungs-id}/documents`, um Dokumente zu Ihrer Sammlung hinzuzufügen.

## Crawlersuche für URLs durchführen
{: #crawl_urls}

Mit dem {{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} {{site.data.keyword.discoveryshort}}-Service können Sie eine Crawlersuche für URLs durchführen und die URLs indexieren. Weitere Informationen finden Sie unter [Indexierungs-Plug-in für Apache Nutch ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/IBM-Watson/nutch-indexer-discovery). Die Crawlersuche wird nicht automatisch aktualisiert. Daher muss die Prozedur regelmäßig wiederholt werden, damit der Index aktuell bleibt. 

Außerdem haben Sie die Möglichkeit, den Connector der Betaversion für die Web-Crawler-Suche zu verwenden. Weitere Informationen finden Sie unter [Verbindung zu Datenquellen herstellen](/docs/services/discovery?topic=discovery-sources#connectwebcrawl). 
