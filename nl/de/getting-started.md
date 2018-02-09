---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-30"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}

# Einführung in die API

In diesem kurzen Lernprogramm wird die {{site.data.keyword.discoveryshort}}-API vorgestellt. Sie werden durch den Prozess für die Erstellung einer privaten Datensammlung geführt und erfahren, wie Sie diese durchsuchen können.
{: shortdesc}

## Vorbereitende Schritte
{: #before-you-begin}

- Erstellen Sie eine Instanz des Service:
    - {: download} Wenn diese Anzeige ausgegeben wird, haben Sie Ihre Serviceinstanz erstellt. Rufen Sie nun Ihre Berechtigungsnachweise ab.
    - Erstellen Sie ein Projekt aus einem Service:
        1.  Wechseln Sie zur {{site.data.keyword.watson}} Developer Console-Seite [Services ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.{DomainName}/developer/watson/services){: new_window}.
        1.  Wählen Sie {{site.data.keyword.discoveryshort}} aus, klicken Sie auf **Services hinzufügen** und registrieren Sie sich entweder für ein kostenloses {{site.data.keyword.Bluemix_notm}}-Konto oder melden Sie sich an.
        1.  Geben Sie `discovery-tutorial` als Projektnamen ein und klicken Sie auf **Projekt erstellen**.
- Kopieren Sie die Berechtigungsnachweise für die Authentifizierung bei Ihrer Serviceinstanz:
    - {: download} Führen Sie Folgendes im (gerade angezeigten) Servicedashboard aus:
        1.  Klicken Sie auf die Registerkarte **Serviceberechtigungsnachweise**.
        1.  Klicken Sie unter **Aktionen** auf **Berechtigungsnachweise anzeigen**.
        1.  Kopieren Sie die Werte für `username`, `password` und `url`.
        {: download}
    - Kopieren Sie in Ihrem Projekt **discovery-tutorial** in Developer Console die Werte von `username`, `password` und `url` für `"discovery"` aus dem Abschnitt **Berechtigungsnachweise**.

<!-- Remove this text after dedicated instances have the Developer Console: begin -->

Falls Sie {{site.data.keyword.Bluemix_dedicated_notm}} verwenden, erstellen Sie Ihre Serviceinstanz über die Seite [{{site.data.keyword.discoveryshort}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.{DomainName}/catalog/services/discovery/){: new_window} im Katalog. Detailinformationen zur Suche nach Ihren Serviceberechtigungsnachweisen finden Sie unter [Serviceberechtigungsnachweise für Watson-Services ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/watson/getting-started-credentials.html#getting-credentials-manually){: new_window}.

<!-- Remove this text after dedicated instances have the Developer Console: end -->

## Schritt 1: Umgebung erstellen
{: #create-an-environment}

Erstellen Sie in einer Bash-Shell oder einer funktional entsprechenden Umgebung wie Cygwin mit der Methode `POST /v1/environments` eine Umgebung. Eine Umgebung ist hier mit einer Art Data-Warehouse vergleichbar, in dem Sie alle Ihre Behälter für Dokumente speichern.

1.  Geben Sie den folgenden Befehl aus, um eine Umgebung namens `my-first-environment` zu erstellen. Ersetzen Sie hierbei `{benutzername}` und `{kennwort}` durch die Serviceberechtigungsnachweise, die Sie zuvor kopiert haben:

    ```bash
    curl -X POST -u "{benutzername}":"{kennwort}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    Die API gibt daraufhin Informationen wie Ihre Umgebungs-ID, den Umgebungsstatus und den Umfang des durch die Umgebung verwendeten Speichers zurück.

1.  Überprüfen Sie laufend den Umgebungsstatus, bis der Status `ready` angezeigt wird.
    - Geben Sie einen Aufruf der Methode `GET /v1/environments/{umgebungs-id}` aus, um den Status Ihrer Umgebung abzurufen. Ersetzen Sie hierbei`{benutzername}`, `{kennwort}` und `{umgebungs-id}` durch die für Sie geltenden Informationen:

    ```bash
    curl -u "{benutzername}":"{kennwort}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}?version=2017-11-07
    ```
    {: pre}

    Der Status muss `ready` lauten, damit Sie eine Sammlung erstellen können.

## Schritt 2: Sammlung erstellen
{: #create-a-collection}

Da die Umgebung jetzt bereit ist, können Sie eine Sammlung erstellen. Eine Sammlung ist mit einem Behälter vergleichbar, in dem Ihre Dokumente in der Umgebung gespeichert werden.

1.  Zunächst benötigen Sie die ID Ihrer Standardkonfiguration. Um den Standardwert für `configuration_id` zu ermitteln, verwenden Sie die Methode `GET /v1/environments/{umgebungs-id}/configurations`. Ersetzen Sie hierbei`{benutzername}`, `{kennwort}` und `{umgebungs-id}` durch die für Sie geltenden Informationen:

    ```bash
      curl -u "{benutzername}":"{kennwort}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/configurations?version=2017-11-07
    ```
    {: pre}
1.  Erstellen Sie mit der Methode `POST /v1/environments/{umgebungs-id}/collections` eine Sammlung namens **my-first-collection**. Ersetzen Sie hierbei `{benutzername}`, `{kennwort}`, `{umgebungs-id}` und `{konfigurations-id}` durch die für Sie geltenden Angaben:

    ```bash
    curl -X POST -u "{benutzername}":"{kennwort}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{konfigurations-id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/collections?version=2017-11-07
    ```
    {: pre}

    Die API gibt daraufhin Informationen wie Ihre Sammlungs-ID, den Sammlungsstatus sowie den durch die Sammlung verwendeten Speicher zurück.
1.  Überprüfen Sie laufend den Sammlungsstatus, bis der Status `online` angezeigt wird.
    - Geben Sie einen Aufruf der Methode `GET /v1/environments/{umgebungs-id}/collections/{sammlungs-id}` aus, um den Status Ihrer Sammlung abzurufen. Ersetzen Sie auch hier wieder `{benutzername}`, `{kennwort}`, `{umgebungs-id}` und `{konfigurations-id}` durch die für Sie geltenden Angaben:

    ```bash
    curl -u "{benutzername}":"{kennwort}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/collections/{sammlungs-id}?version=2017-11-07
    ```
    {: pre}

## Schritt 3: Beispieldokumente herunterladen
{: #download-sample-documents}

Laden Sie die folgenden Beispieldokumente herunter: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link" class="style-scope doc-content"></a> und <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link" class="style-scope doc-content"></a>.

## Schritt 4: Dokumente hochladen
{: #upload-the-documents}

1.  Fügen Sie nun die Beispieldokumente zu Ihrer Sammlung hinzu. Im folgenden Beispiel wird das Dokument **test-doc1.html** in Ihre Sammlung hochgeladen. Ersetzen Sie hierbei `{benutzername}`, `{kennwort}`, `{umgebungs-id}` und `{konfigurations-id}` durch die für Sie geltenden Angaben. Ändern Sie die Position des Beispieldokuments so, dass auf die Position verwiesen wird, an der Sie die Datei `test-doc1.html` gespeichert haben.
    - Verwenden Sie die Methode `POST /v1/environments/{umgebungs-id}/collections/{sammlungs-id}/documents`:

        ```bash
        curl -X POST -u "{benutzername}":"{kennwort}" -F "file=@test-doc1.html" https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/collections/{sammlungs-id}/documents?version=2017-11-07
        ```
        {: pre}

    Alternativ können Sie auch eines der in der [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window} aufgelisteten SDKs verwenden:
    - Java:

      ```java
      Discovery discovery = new Discovery("2017-11-07");
      discovery.setEndPoint("https://gateway.watsonplatform.net/discovery/api/v1");
      discovery.setUsernameAndPassword("{benutzername}", "{kennwort}");
      String environmentId = "{umgebungs-id}";
      String collectionId = "{sammlungs-id}";
      String documentJson = "{\"feld\":\"wert\"}";
      InputStream documentStream = new ByteArrayInputStream(documentJson.getBytes());

      CreateDocumentRequest.Builder builder = new CreateDocumentRequest.Builder(environmentId, collectionId);
      builder.inputStream(documentStream, HttpMediaType.APPLICATION_JSON);
      CreateDocumentResponse createResponse = discovery.createDocument(builder.build()).execute();
      ```
      {: codeblock}

    - Python:

      ```python
      import sys
      import os
      import json
      from watson_developer_cloud import DiscoveryV1

      discovery = DiscoveryV1(
        username="{benutzername}",
        password="{kennwort}",
        version="2017-11-07"
      )

      with open((os.path.join(os.getcwd(), '{pfadelement}', '{dateiname}' as fileinfo:
        add_doc = discovery.add_document('{umgebungs-id}', '{sammlungs-id}', file_info=fileinfo)
      print(json.dumps(add_doc, indent=2))
      ```
      {: codeblock}

    - Node.js:

      ```javascript
      var DiscoveryV1 = require('watson-developer-cloud/discovery/v1');
      var fs = require('fs');

      var discovery = new DiscoveryV1({
        username: '{benutzername}',
        password: '{kennwort}',
        version_date: '2017-11-07'
      });

      var file = fs.readFileSync('{/pfad_zur_datei}');

      discovery.addDocument(('{umgebungs-id}', '{sammlungs-id}', file),
      function(error, data) {
        console.log(JSON.stringify(data, null, 2));
        }
      );
      ```
      {: codeblock}

1.  Wiederholen Sie diesen Prozess für die drei anderen Beispieldateien.

## Schritt 5: Sammlung abfragen
{: #query-your-collection}

Verwenden Sie abschließend die Methode `GET /v1/environments/{umgebungs-id}/collections/{sammlungs-id}/query`, um Ihre Dokumentensammlung zu durchsuchen.

Beim folgenden Beispiel werden alle Entitäten namens **IBM** zurückgegeben. Ersetzen Sie hierbei `{benutzername}`, `{kennwort}`, `{umgebungs-id}` und `{konfigurations-id}` durch die für Sie geltenden Angaben:

```bash
curl -u "{benutzername}":"{kennwort}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/collections/{sammlungs-id}*/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

## Nächste Schritte
{: #next-steps}

Sie haben Dokumente in der von Ihnen erstellten Umgebung und Sammlung erfolgreich abgefragt. Jetzt können Sie mit der Anpassung Ihrer Sammlung beginnen, indem Sie weitere Dokumente und Aufbereitungen hinzufügen sowie Konvertierungseinstellungen anpassen. Weitere Informationen zur API enthält die [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}.
