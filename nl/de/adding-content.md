---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-15"

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

# Inhalt hinzufügen
{: #addcontent}

Wie entscheide ich mich für das zu nutzende Dokumentuploadverfahren?
{: shortdesc}

-   Verwenden Sie die [API](/docs/services/discovery/getting-started.html), wenn der Upload von Inhalt mit einer vorhandenen Anwendung integriert werden soll oder Sie ein eigenes angepasstes Uploadverfahren erstellen.
-   Verwenden Sie die [{{site.data.keyword.discoveryshort}}-Tools](/docs/services/discovery/getting-started-tool.html) wenn Sie zugängliche Dateien schnell hochladen möchten.
    Beim Hochladen von Dokumenten mit den {{site.data.keyword.discoveryshort}}-Tools sollten alle Dokumente einen eindeutigen Dateinamen besitzen. Falls zwei Dateien denselben Namen tragen, wird das Original beim Hochladen der neueren Version überschrieben. Falls in Ihrer Sammlung jedoch Dokumente desselben Dateinamens koexistieren sollen, muss die Dokument-ID angegeben werden. Sie können die Dokument-ID angeben, wenn Sie für den Dokumentupload die API oder Data Crawler verwenden.
-   Verwenden Sie die {{site.data.keyword.discoveryshort}}-Tools oder die API, um eine Verbindung zu Box-, Salesforce- und Microsoft SharePoint Online-Datenquellen herzustellen. Weitere Informationen finden Sie unter [Verbindung zu Datenquellen herstellen](/docs/services/discovery/connect.html).

-   Verwenden Sie [Data Crawler](/docs/services/discovery/data-crawler.html), falls Sie ein verwaltetes Upload für eine erhebliche Anzahl von Dateien durchführen möchten oder wenn Sie Inhalt aus einem unterstützten Repository (z. B. einer Db2-Datenbank) extrahieren wollen.

## Inhalt mit der API oder den Tools hinzufügen

Berücksichtigen Sie die folgenden Punkte, bevor Sie Dokumente zu Ihrer Sammlung hinzufügen:

-   Die maximale Größe von Dateien, die in den {{site.data.keyword.discoveryshort}}-Service hochgeladen werden können, beträgt 50 MB.
-   Die Beispieldokumente werden nicht automatisch zur Sammlung hinzugefügt. Sie müssen sie selbst hinzufügen, wenn Sie sie im Rahmen Ihrer Sammlung verwenden wollen.
-   Nur die ersten 50.000 Zeichen jedes JSON-Feldes, das für die Aufbereitung ausgewählt ist, werden aufbereitet.
-   Beim Erstellen einer Sammlung wählen Sie die Dokumentsprache aus (Standardeinstellung ist Englisch). Eine Liste der Sprachen finden Sie unter [Sprachunterstützung](/docs/services/discovery/language-support.html). Ihre Dokumente werden in der ausgewählten Sprache aufbereitet. Verwenden Sie in einer Sammlung jeweils nur eine einzige Sprache.
-   Sie können Microsoft Word-, PDF-, HTML- und JSON-Dokumente zu Ihrer Sammlung hinzufügen. **Hinweis:** PDF-Dokumente, bei denen es sich um gescannte Bilddateien handelt, können nicht konvertiert und aufbereitet werden.
-   Die Dokumente in Ihrer Sammlung werden unter Verwendung der angegebenen Konfigurationsdatei konvertiert, die 'Standardkonfiguration' heißt, sofern Sie keine andere Konfigurationsdatei auswählen. Informationen zum Erstellen einer Konfigurationsdatei finden Sie unter [Angepasste Konfiguration](/docs/services/discovery/building.html#custom-configuration).
-   Sobald Dokumente in eine Datensammlung hochgeladen werden, werden sie unter Verwendung der für diese Sammlung ausgewählten Konfigurationsdatei konvertiert und aufbereitet. Falls Sie später bei einer Sammlung zu einer anderen Konfigurationsdatei wechseln wollen, ist dies möglich. Die Dokumente, die bereits hochgeladen wurden, bleiben jedoch gemäß der ursprünglichen Konfigurationsdatei konvertiert. Alle Dokumente, die nach dem Wechsel der Konfigurationsdatei hochgeladen werden, verwenden die neue Konfigurationsdatei. Wenn Sie die neue Konfiguration für die **gesamte** Sammlung verwenden wollen, müssen Sie eine neue Sammlung erstellen, die neue Konfigurationsdatei auswählen und alle Dokumente erneut hochladen.
-   Der `Datentyp` (z. B. `text` oder `date`) von Feldern kann nicht angegeben werden. Wenn während der Dokumenteinpflegung ein Feld erkannt wird, das noch nicht im Index vorhanden ist, erkennt {{site.data.keyword.discoveryshort}} automatisch den `Datentyp` dieses Feldes, basierend auf dem Wert des Feldes für das erste indexierte Dokument.
-   Das Einpflegen eines Dokuments kann fehlschlagen, weil keine Typübereinstimmung zwischen Daten im aktuellen Dokument und ähnlichen Daten in einem zuvor eingepflegten Dokument besteht. Beispielsweise kann ein Feld in einem Dokument den Typ `date` und in einem nachfolgenden Dokument den Typ `string` besitzen.
-   Wenn Sie die angepasste Zerlegung in Tokens verwenden möchten (derzeit nur für japanische Sammlungen verfügbar, wenn die {{site.data.keyword.discoveryshort}}-API verwendet wird), muss das entsprechende Wörterverzeichnis für Ihre Sammlung vor dem Hochladen von Dokumenten hinzugefügt werden.

Beim Hochladen von Dokumenten gelten die folgenden Einschränkungen:

-   **Lite**-Pläne: 21 Inflight-Dokumente
-   **Advanced**-Pläne: 105 Inflight-Dokumente (außer für X-Small Advanced-Pläne, die eine Begrenzung von 50 Inflight-Dokumenten aufweisen)
-   **Premium**-Pläne: 210 Inflight-Dokumente

Änderungen vorbehalten. 

Wenn Sie den Discovery-Service verwenden, bedeutet der Inflight-Upload, dass das Dokument vor dem Hinzufügen zur Sammlung hochgeladen und verarbeitet wird. Wenn Sie die Inflight-Begrenzung erreichen, sollten Sie die Einpflegerate verlangsamen. Eine Möglichkeit besteht darin, einen automatischen Backoff-Mechanismus mit Wiederholungen hinzuzufügen.

## Dokumente mit den Discovery-Tools hochladen

1.  Erstellen Sie eine Sammlung. Weitere Informationen finden Sie unter [Service für Dokumente vorbereiten](/docs/services/discovery/building.html#preparing-the-service-for-your-documents).
1.  Klicken Sie auf die Sammlung, um sie zu öffnen.
1.  Klicken Sie auf die Schaltfläche **Dokumente hochladen** und starten Sie das Upload Ihrer Dokumente durch Ziehen und Ablegen oder durch Navigieren und Auswählen.

Ihre Dokumente werden jetzt für die Konvertierung und Aufbereitung eingereiht. Die hierfür benötigte Zeit ist von der Größe Ihrer Sammlung abhängig. Nach der Indexierung und Aufbereitung werden die Details der Sammlung im Abschnitt **Übersicht** angezeigt.

-   Datumsangaben für **Erstellt** und **Zuletzt aktualisiert** (klicken Sie auf **Sammlung in API verwenden**, um die Werte für die `Sammlungs-ID`, die `Konfigurations-ID` und die `Umgebungs-ID` anzuzeigen).
-   **Anzahl der Dokumente** in Ihrer Sammlung.
-   **Konfiguration**: Der Name der Konfigurationsdatei, die zum Konvertieren dieser Sammlung verwendet wird.
-   **Fehler und Warnungen**

Informationen zum Herstellen von Verbindungen zu Box-, Salesforce- und Microsoft SharePoint Online-Datenquellen mit den {{site.data.keyword.discoveryshort}}-Tools finden Sie unter [Verbindung zu Datenquellen herstellen](/docs/services/discovery/connect.html).


## Dokumente mit der API hochladen

Unter [Einführung in die {{site.data.keyword.discoveryshort}}-API](/docs/services/discovery/getting-started.html) finden Sie ein schrittweises Lernprogramm.

Weitere Informationen zur API enthält die [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}.

1.  Erstellen Sie mit der Methode `POST /v1/environments/{umgebungs-id}/collections` eine Sammlung.
1.  Verwenden Sie anschließend die Methode `POST /v1/environments/{umgebungs-id}/collections/{sammlungs-id}/documents`, um Dokumente zu Ihrer Sammlung hinzuzufügen.

## Crawlersuche für URLs durchführen

Mit dem {{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} {{site.data.keyword.discoveryshort}}-Service können Sie eine Crawlersuche für URLs durchführen und die URLs indexieren. Weitere Informationen finden Sie unter [Indexierungs-Plug-in für Apache Nutch ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/IBM-Watson/nutch-indexer-discovery). Die Crawlersuche wird nicht automatisch aktualisiert. Daher muss die Prozedur regelmäßig wiederholt werden, damit der Index aktuell bleibt.
