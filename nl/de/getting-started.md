---
copyright:
  years: 2015, 2018
lastupdated: "2018-12-19"

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

# Einführung in die API
{: #gs-api}

In diesem kurzen Lernprogramm wird die {{site.data.keyword.discoveryshort}}-API vorgestellt. Sie werden durch den Prozess für die Erstellung einer privaten Datensammlung geführt und erfahren, wie Sie diese durchsuchen können.
{: shortdesc}

Wenn Sie lieber mit den {{site.data.keyword.discoveryshort}}-Tools arbeiten, lesen Sie den Abschnitt [Einführung](/docs/services/discovery?topic=discovery-getting-started#getting-started).
{: tip}

## Vorbereitende Schritte
{: #before-you-begin-api}

- Erstellen Sie eine Instanz des Service:
    1.  Rufen Sie die [{{site.data.keyword.discoveryshort}}-Seite ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/catalog/services/discovery) im {{site.data.keyword.cloud_notm}}-Katalog auf.
        Die Serviceinstanz wird in der Ressourcengruppe **default** erstellt, wenn Sie keine andere auswählen, und kann später *nicht* mehr geändert werden. Diese Gruppe reicht aus, um den Service auszuprobieren.
        Wenn Sie eine Instanz für anspruchsvollere Anwendungen erstellen müssen, lesen Sie dazu die Informationen im Abschnitt [Ressourcengruppen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/docs/resources/bestpractice_rgs.html#bp_resourcegroups){: new_window}.
    1.  Registrieren Sie sich entweder für ein kostenloses {{site.data.keyword.cloud_notm}}-Konto oder melden Sie sich an.
    1.  Klicken Sie auf **Erstellen**. Nachdem Sie eine Instanz des {{site.data.keyword.discoveryshort}}-Service erstellt haben, werden Sie zu Ihrer Serviceliste geführt.
- Kopieren Sie die Berechtigungsnachweise für die Authentifizierung bei Ihrer Serviceinstanz:
    1.  Klicken Sie in der [Ressourcenliste](https://{DomainName}/dashboard/) auf Ihre {{site.data.keyword.discoveryshort}}-Serviceinstanz, um zur Dashboardseite des {{site.data.keyword.discoveryshort}}-Service zu wechseln.
    1.  Klicken Sie auf der Seite **Verwalten** auf **Berechtigungsnachweise anzeigen**, um Ihre Berechtigungsnachweise anzuzeigen.
    1.  Kopieren Sie die Werte für den `API-Schlüssel` und die `URL`.

        In einigen Fällen authentifizieren Sie sich durch die Bereitstellung einer Basisauthentifizierung. Wenn Ihnen in den Berechtigungsnachweise Werte für `username` und `password` angezeigt werden, verwenden Sie diese anstelle von `"apikey:{apikey}"` in den Beispielen dieses Lernprogramms.
        {: tip}

## Schritt 1: Umgebung erstellen
{: #create-an-environment}

Verwenden Sie in einer Bash-Shell oder einer funktional entsprechenden Umgebung wie Cygwin mit einer installierten `curl`-Anwendung die Methode `POST /v1/environments`, um eine Umgebung zu erstellen. Eine Umgebung ist hier mit einer Art Data-Warehouse vergleichbar, in dem Sie alle Ihre Behälter für Dokumente speichern.

In diesem Lernprogramm wird ein API-Schlüssel für die Authentifizierung verwendet. Wenn Sie in einer Produktionsumgebung arbeiten, stellen Sie sicher, dass Sie die [Best Practices](/docs/services/watson/apikey-bp.html#api-bp) für den API-Schlüssel überprüfen.
{: important}

1.  Geben Sie den folgenden Befehl aus, um eine Umgebung namens `my-first-environment` zu erstellen. Ersetzen Sie die Werte für `{apikey}` und `{url}` durch die zuvor kopierten Werte:

    ```bash
    curl -X POST -u "apikey:{apikey}" -H "Content-Type: application/json" -d "{\"name\":\"my-first-environment\", \"description\":\"exploring environments\"}" "{url}/v1/environments?version=2018-12-03"
    ```
    {: pre}

    Die API gibt daraufhin Informationen wie Ihre Umgebungs-ID, den Umgebungsstatus und den Umfang des durch die Umgebung verwendeten Speichers zurück.

1.  Überprüfen Sie den Umgebungsstatus in regelmäßigen Abständen, bis der Status `active` angezeigt wird.

    Geben Sie einen Aufruf der Methode `GET /v1/environments/{umgebungs-id}` aus, um den Status Ihrer Umgebung abzurufen. Ersetzen Sie die Werte für `{apikey}`, `{url}` und `{environment_id}` durch eigene Angaben:

    ```bash
    curl -u "apikey:{apikey}" "{url}/v1/environments/{environment_id}?version=2018-12-03"
    ```
    {: pre}

    Der Status muss `active` lauten, damit Sie eine Sammlung erstellen können.

## Schritt 2: Sammlung erstellen
{: #create-a-collection-api}

Da die Umgebung jetzt bereit ist, können Sie eine Sammlung erstellen. Eine Sammlung ist mit einem Behälter vergleichbar, in dem Ihre Dokumente in der Umgebung gespeichert werden.

1.  Zunächst benötigen Sie die ID Ihrer Standardkonfiguration. Um den Standardwert für `configuration_id` zu ermitteln, verwenden Sie die Methode `GET /v1/environments/{umgebungs-id}/configurations`. Ersetzen Sie die Werte für `{apikey}`, `{url}` und `{environment_id}` durch eigene Angaben:
    ```bash
      curl -u "apikey:{apikey}" "{url}/v1/environments/{environment_id}/configurations?version=2018-12-03"
    ```
    {: pre}
1.  Erstellen Sie mit der Methode `POST /v1/environments/{umgebungs-id}/collections` eine Sammlung namens **my-first-collection**. Ersetzen Sie `{apikey}`, `{url}`, `{environment_id}` und `{configuration_id}` durch eigene Angaben:
    ```bash
    curl -X POST -u "apikey:{apikey}" -H "Content-Type: application/json" -d "{\"name\": \"my-first-collection\", \"description\": \"exploring collections\", \"configuration_id\":\"{configuration_id}\" , \"language": \"en_us\"}" "{url}/v1/environments/{environment_id}/collections?version=2018-12-03"
    ```
    {: pre}
    Die API gibt daraufhin Informationen wie Ihre Sammlungs-ID, den Sammlungsstatus sowie den durch die Sammlung verwendeten Speicher zurück.
1.  Überprüfen Sie den Sammlungsstatus in regelmäßigen Abständen, bis der Status `active` angezeigt wird.

    Geben Sie einen Aufruf der Methode `GET /v1/environments/{umgebungs-id}/collections/{sammlungs-id}` aus, um den Status Ihrer Sammlung abzurufen.  Ersetzen Sie nochmals die Werte für `{apikey}`, `{url}`, `{environment_id}` und `{configuration_id}` durch eigene Angaben:

    ```bash
    curl -u "apikey:{apikey}" "{url}/v1/environments/{environment_id}/collections/{collection_id}?version=2018-12-03"
    ```
    {: pre}

## Schritt 3: Beispieldokumente herunterladen
{: #download-sample-documents}

Laden Sie die folgenden Beispieldokumente herunter: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link"></a> und <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link"></a>.

In einigen Browsern werden die vorangehenden Links in einem neuen Fenster geöffnet, anstatt lokal gespeichert zu werden. Falls dies der Fall ist, wählen Sie im Menü `Datei` des Browsers die Option `Speichern unter` aus, um eine Kopie der Datei zu speichern.
{: tip}

## Schritt 4: Dokumente hochladen
{: #upload-the-documents}

1.  Fügen Sie nun die Beispieldokumente zu Ihrer Sammlung hinzu. Im folgenden Beispiel wird das Dokument **test-doc1.html** in Ihre Sammlung hochgeladen. Ersetzen Sie die Werte für `{apikey}`, `{url}`, `{environment_id}` und `{collection_id}` durch eigene Angaben. Ändern Sie die Position des Beispieldokuments so, dass auf die Position verwiesen wird, an der Sie die Datei `test-doc1.html` gespeichert haben.
    - Verwenden Sie die Methode `POST /v1/environments/{umgebungs-id}/collections/{sammlungs-id}/documents`:

        ```bash
        curl -X POST -u "apikey:{apikey}" -F "file=@test-doc1.html" "{url}/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2018-12-03"
        ```
        {: pre}

        Alternativ können Sie auch eines der in der [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/discovery){: new_window} aufgelisteten SDKs verwenden:
    - Java:
      ```java
      Discovery discovery = new Discovery("2018-12-03");
      discovery.setEndPoint("{url}");

      IamOptions options = new IamOptions.Builder()
        .apiKey("{apikey}")
        .build();
      discovery.setIamCredentials(options);

      String environmentId = "{environment_id}";
      String collectionId = "{collection_id}";
      String documentJson = "{\"field\":\"value\"}";
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
          version='2018-12-03',
          iam_apikey='{apikey}',
          url='{url}'
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
        version_date: '2018-12-03',
        iam_apikey: '{apikey}',
        url: '{url}'
      });

      var file = fs.readFileSync('{/pfad_zur_datei}');

      discovery.addDocument({ environment_id: '{umgebungs-id}', collection_id: '{sammlungs-id}', file: file },
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

Beim folgenden Beispiel werden alle Entitäten namens **IBM** zurückgegeben. Ersetzen Sie die Werte für `{apikey}`, `{environment_id}` und `{collection_id}` durch eigene Angaben:

```bash
curl -u "apikey:{apikey}" "{url}/v1/environments/{environment_id}/collections/{collection_id}/query?version=2018-12-03&query=enriched_text.entities.text:IBM"
```
{: pre}

## Nächste Schritte
{: #next-steps-api}

Sie haben Dokumente in der von Ihnen erstellten Umgebung und Sammlung erfolgreich abgefragt. Jetzt können Sie mit der Anpassung Ihrer Sammlung beginnen, indem Sie weitere Dokumente und Aufbereitungen hinzufügen sowie Konvertierungseinstellungen anpassen.

- Lesen Sie sich die Informationen zur API in der [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/discovery){: new_window} durch.
- [Konfigurieren Sie](/docs/services/discovery?topic=discovery-configservice#configservice) Ihren Service.
- Erfahren Sie mehr über die [Authentifizierung mit IAM ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/docs/services/watson/getting-started-iam.html#iam){: new_window}
