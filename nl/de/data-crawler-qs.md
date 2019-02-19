---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-03"

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

# Einführung in Data Crawler

In diesem Abschnitt wird erläutert, wie Sie mit Data Crawler Dateien aus Ihrem lokalen Dateisystem einpflegen können, um sie mit dem {{site.data.keyword.discoveryfull}}-Service zu verwenden.
{: shortdesc}

Erstellen Sie vor dem Ausführen dieser Task eine Instanz des {{site.data.keyword.discoveryshort}}-Service in {{site.data.keyword.Bluemix}}. Damit Sie diese Anleitung durcharbeiten können, müssen Sie die Berechtigungsnachweise verwenden, die der erstellten Instanz des Service zugeordnet sind.

Sie können die {{site.data.keyword.discoveryshort}}-Tools oder die API für die Crawlersuche in Box-, Salesforce- und Microsoft SharePoint Online-Datenquellen verwenden. Weitere Informationen finden Sie unter [Verbindung zu Datenquellen herstellen](/docs/services/discovery/connect.html).
{: tip}

## Umgebung erstellen

Verwenden Sie die Bash-Methode 'POST /v1/environments', um eine Umgebung zu erstellen. Eine Umgebung ist hier mit einer Art Data-Warehouse vergleichbar, in dem Sie alle Ihre Behälter für Dokumente speichern. Im folgenden Beispiel wird eine Umgebung namens `my-first-environment` erstellt:

Ersetzen Sie `{benutzername}` und `{kennwort}` durch Ihre Serviceberechtigungsnachweise.

```bash
curl -X POST -u "{benutzername}":"{kennwort}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
```
{: pre}

Die API gibt eine Antwort zurück, die Informationen wie Ihre Umgebungs-ID, den Umgebungsstatus sowie den Umfang des durch die Umgebung verwendeten Speichers enthält. Fahren Sie erst dann mit dem nächsten Schritt fort, wenn der Umgebungsstatus `ready` lautet. Wenn beim Erstellen der Umgebung der Status `status:pending` zurückgegeben wird, können Sie mit der Methode `GET /v1/environments/{umgebungs-id}` den Status überprüfen, bis die Umgebung bereit ist ('ready'). Ersetzen Sie in diesem Beispiel `{benutzername}` und `{kennwort}` durch Ihre Serviceberechtigungsnachweise und `{umgebungs-id}` durch die Umgebungs-ID, die beim Erstellen der Umgebung zurückgegeben wurde.

```bash
curl -u "{benutzername}":"{kennwort}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}?version=2017-11-07
```
{: pre}

## Sammlung erstellen

Erstellen Sie als Nächstes mit der Methode `POST /v1/environments/{umgebungs-id}/collections` eine Sammlung. Eine Sammlung ist mit einem Behälter vergleichbar, in dem Ihre Dokumente in der Umgebung gespeichert werden. Mit diesem Beispiel wird eine Sammlung namens `my-first-collection` in der Umgebung erstellt, die Sie im vorherigen Schritt erstellt haben. Die Sammlung verwendet die folgende Standardkonfiguration:

-   Ersetzen Sie `{benutzername}` und `{kennwort}` durch Ihre Serviceberechtigungsnachweise.
-   Ersetzen Sie `{umgebungs-id}` durch die ID der Umgebung, die Sie in Schritt 1 erstellt haben.

Bevor Sie eine Sammlung erstellen, müssen Sie die ID Ihrer Standardkonfiguration abrufen. Um den Standardwert für `configuration_id` zu ermitteln, verwenden Sie die Methode `GET /v1/environments/{umgebungs-id}/configurations`:

```bash
curl -u "{benutzername}":"{kennwort}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/configurations?version=2017-11-07
```
{: pre}

Nachdem Sie die Standardkonfigurations-ID ermittelt haben, verwenden Sie sie bei der Erstellung Ihrer Sammlung. Ersetzen Sie `{konfigurations-id}` durch die Standardkonfigurations-ID für Ihre Umgebung.

```bash
curl -X POST -u "{benutzername}":"{kennwort}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{konfigurations-id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/collections?version=2017-11-07
```
{: pre}

Die API gibt eine Antwort zurück, die Informationen wie die ID Ihrer Sammlung, den Sammlungsstatus sowie den Umfang des durch die Sammlung verwendeten Speichers enthält. Fahren Sie erst dann mit dem nächsten Schritt fort, wenn der Sammlungsstatus `online` lautet. Wenn beim Erstellen der Sammlung der Status `status:pending` zurückgegeben wird, können Sie mit der Methode `GET /v1/environments/{umgebungs-id}/collections/{sammlungs-id}` den Status überprüfen, bis die Sammlung online ist. Ersetzen Sie in diesem Beispiel `{benutzername}` und `{kennwort}` durch Ihre Serviceberechtigungsnachweise, ersetzen Sie `{umgebungs-id}` durch Ihre Umgebungs-ID und ersetzen Sie `{sammlungs-id}` durch die Sammlungs-ID, die zuvor in diesem Schritt zurückgegeben wurde.

```bash
curl -u "{benutzername}":"{kennwort}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/collections/{sammlungs-id}?version=2017-11-07
```
{: pre}

## Beispieldokumente herunterladen
Laden Sie die folgenden Dokumente herunter:

-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link" class="style-scope doc-content"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link" class="style-scope doc-content"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link" class="style-scope doc-content"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link" class="style-scope doc-content"></a>

## Data Crawler herunterladen und installieren

1.  Prüfen Sie, ob Ihr System die folgenden Voraussetzungen erfüllt:

    -   Java Runtime Environment Version 8 oder höher

        **Hinweis:** Die Umgebungsvariable `JAVA_HOME` muss korrekt festgelegt sein oder darf andernfalls nicht festgelegt sein, damit der Crawler ausgeführt werden kann.
    -   Red Hat Enterprise Linux 6 oder 7 bzw. Ubuntu Linux 15 oder 16. Eine optimale Leistung wird erzielt, wenn Data Crawler in einer eigenen Linux-Instanz ausgeführt wird. Hierbei kann es sich um eine virtuelle Maschine, einen Container oder um Hardware handeln.
    -   Mindestens 2 GB Hauptspeicher auf dem Linux-System

1.  Öffnen Sie einen Browser und melden Sie sich bei Ihrem [{{site.data.keyword.Bluemix_notm}}-Konto ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net){: new_window} an.
1.  Wählen Sie in Ihrem {{site.data.keyword.Bluemix_notm}}-Dashboard den {{site.data.keyword.discoveryshort}}-Service aus, den Sie zuvor erstellt haben.
1.  Wählen Sie unter **Upload von Inhalt in den Discovery-Service automatisieren** den entsprechenden Download-Link für Ihr System (DEB, RPM oder ZIP) aus, um Data Crawler herunterzuladen.
1.  Führen Sie als Administrator die folgenden Befehle aus, um die heruntergeladene Archivdatei zu installieren:

    -   Verwenden Sie auf Systemen wie Red Hat und CentOS, die RPM-Pakete verwenden, einen Befehl wie etwa den Folgenden: `rpm -i /full/path/to/rpm/package/rpm-dateiname`
    -   Verwenden Sie auf Systemen wie Ubuntu und Debian, die DEB-Pakete verwenden, einen Befehl wie etwa den Folgenden: `dpkg -i /full/path/to/deb/package/deb-dateiname`
    -   Die Crawler-Scripts werden an der Position `{installationsverzeichnis}/bin` installiert (z. B. `/opt/ibm/crawler/bin`). Stellen Sie sicher, dass `{installationsverzeichnis}/bin` in Ihrer Umgebungsvariablen `PATH` angegeben ist.

    Crawler-Scripts werden auch an der Position `/usr/local/bin` installiert, weshalb diese Position ebenfalls zur Umgebungsvariablen `PATH` hinzugefügt werden kann.
    {: tip}

## Arbeitsverzeichnis erstellen

Kopieren Sie den Inhalt des Verzeichnisses `{installationsverzeichnis}/share/examples/config` in ein Arbeitsverzeichnis auf Ihrem System (z. B. `/home/config`).

**Achtung:** Nehmen Sie keine direkten Änderungen an den Konfigurationsbeispieldateien vor. Kopieren Sie die Dateien und bearbeiten Sie die Kopie. Falls Sie die Beispieldateien direkt bearbeiten, wird Ihre Konfiguration möglicherweise bei einem Update von Data Crawler überschrieben oder bei der Deinstallation dieses Dienstprogramms entfernt.

**Hinweis:** In diesen Anleitungen beziehen sich Verweise auf Dateien im Verzeichnis `config` (z. B. `config/crawler.conf`) auf diese Datei in Ihrem Arbeitsverzeichnis und NICHT im installierten Verzeichnis `{installationsverzeichnis}/share/examples/config`.

## Optionen für die Crawlersuche konfigurieren

Um Data Crawler für die Crawlersuche in Ihrem Repository zu konfigurieren, müssen Sie angeben, für welche Dateien im lokalen System die Crawlersuche durchgeführt werden soll und an welchen {{site.data.keyword.discoveryshort}}-Service die Sammlung der durchsuchten Dateien gesendet werden soll, nachdem die Crawlersuche abgeschlossen ist.

1.  **`filesystem-seed.conf`**: Öffnen Sie die Datei `seeds/filesystem-seed.con` in einem Texteditor. Ändern Sie das Attribut `value`, das sich direkt unter dem Attribut `name-"url"` befindet, in den Dateipfad, für den die Crawlersuche ausgeführt werden soll. Beispiel: `value-"sdk-fs:///TMP/MY_TEST_DATA/"`.

    **Hinweis:** Die URLs müssen mit der Zeichenfolge `sdk-fs://` beginnen. Um beispielsweise `/home/watson/mydocs` zu durchsuchen, muss als Wert dieser URL daher `sdk-fs:///home/watson/mydocs` angegeben werden. Der dritte Schrägstrich ist unbedingt erforderlich!

    Speichern und schließen Sie die Datei.

1.  **`discovery_service.conf`**: Öffnen Sie die Datei `discovery/discovery_service.conf` in einem Texteditor. Ändern Sie die folgenden Werte für den entsprechenden {{site.data.keyword.discoveryshort}}-Service, den Sie zuvor in {{site.data.keyword.Bluemix_notm}} erstellt haben:

    -   `environment_id`: Geben Sie die Umgebungs-ID für Ihren {{site.data.keyword.discoveryshort}}-Service an.
    -   `collection_id`: Geben Sie die Sammlungs-ID für Ihren {{site.data.keyword.discoveryshort}}-Service an.
    -   `configuration_id`: Geben Sie die Konfigurations-ID für Ihren {{site.data.keyword.discoveryshort}}-Service an.
    -   `configuration`: Geben Sie den vollständigen Pfad dieser Datei `discovery_service.conf` an, z. B. `/home/config/discovery/discovery_service.conf`.
    -   `username`: Geben Sie den Benutzernamen des Berechtigungsnachweises für Ihren {{site.data.keyword.discoveryshort}}-Service an.
    -   `password`: Geben Sie das Kennwort des Berechtigungsnachweises für Ihren {{site.data.keyword.discoveryshort}}-Service an.
1.  **`crawler.conf`**: Öffnen Sie die Datei `config/crawler.conf` in einem Texteditor.

    -   Legen Sie die Optionen `output_adapter`, `class` und `config` für den {{site.data.keyword.discoveryshort}}-Service wie folgt fest:

        ```bash
        class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

        config - "discovery_service"

        discovery_service {
          include "discovery/discovery_service.conf"
        }
        ```
        {: pre}

1.  Nachdem Sie diese Dateien geändert haben, können Sie eine Crawlersuche für Ihre Daten ausführen.

## Crawlersuche für Daten ausführen

Führen Sie den folgenden Befehl aus: `crawler crawl --config [config/crawler.conf]`

Hierdurch wird eine Crawlersuche mit der Konfigurationsdatei `crawler.conf` ausgeführt.

**Hinweis:** Der Pfad zur Konfigurationsdatei, der in der Option `--config` übergeben wird, muss ein qualifizierter Pfad sein. Er muss somit in relativen Formaten angegeben werden, z. B. `config/crawler.conf` oder `./crawler.conf`, bzw. als absoluter Pfad wie `/path/to/config/crawler.conf`.

## Dokumente durchsuchen

Verwenden Sie abschließend die Methode `GET /v1/environments/{umgebungs-id}/collections/{sammlungs-id}/query`, um Ihre Dokumentensammlung zu durchsuchen. Beim folgenden Beispiel werden alle Entitäten namens `IBM` zurückgegeben:

-   Ersetzen Sie `{benutzername}` und `{kennwort}` durch Ihre Serviceberechtigungsnachweise.
-   Ersetzen Sie `{umgebungs-id}` durch die ID der Umgebung, die Sie in Schritt 1 erstellt haben.
-   Ersetzen Sie `{sammlungs-id}` durch die ID der Sammlung, die Sie in Schritt 2 erstellt haben.

```bash
curl -u "{benutzername}":"{kennwort}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/collections/{sammlungs-id}/query?version=2017-11-07&query-enriched_text.entities.text:IBM'
```
{: pre}

## Ergebnisse

Sie haben Dokumente in der von Ihnen erstellten Umgebung und Sammlung erfolgreich abgefragt. Jetzt können Sie mit der Anpassung beginnen, indem Sie weitere Dokumente zur Sammlung hinzufügen.
