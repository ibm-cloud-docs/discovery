---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-01-28"

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

# Data Crawler herunterladen und installieren
{: #downloading-and-installing-the-data-crawler}

Data Crawler erfasst Rohdaten, die später dann zur Bildung von Suchergebnissen für den {{site.data.keyword.discoveryshort}}-Service verwendet werden. Bei einer Crawlersuche in Datenrepositorys lädt der Crawler ausgehend von einer benutzerdefinierten Seed-URL Dokumente und Metadaten herunter. Der Crawler erkennt Dokumente in einer Hierarchie oder auf andere Weise mit der Seed-URL verbundene Dokumente und reiht sie zum Abruf ein.
{: shortdesc}

Data Crawler sollte nur zum Durchsuchen von Dateifreigaben oder Datenbanken verwendet werden, in allen anderen Fällen sollten Sie den entsprechenden {{site.data.keyword.discoveryshort}}-Connector verwenden. Weitere Informationen finden Sie unter [Verbindung zu Datenquellen herstellen](/docs/services/discovery?topic=discovery-sources#sources). Data Crawler wird nicht mehr unterstützt, falls Sie ihn mit einer Datenquelle verwenden, die von den {{site.data.keyword.discoveryshort}}-Connectoren unterstützt wird.
{: important}

## Voraussetzungen
{: #dc-prerequisites}

-   Java Runtime Environment Version 8 oder höher

    Die Umgebungsvariable `JAVA_HOME` muss korrekt festgelegt sein oder darf andernfalls nicht festgelegt sein, damit der Crawler ausgeführt werden kann.
    {: tip}
-   Red Hat Enterprise Linux 6 oder 7 bzw. Ubuntu Linux 15 oder 16. Eine optimale Leistung wird erzielt, wenn Data Crawler in einer eigenen Linux-Instanz ausgeführt wird. Hierbei kann es sich um eine virtuelle Maschine, einen Container oder um Hardware handeln.

-   Mindestens 2 GB Hauptspeicher auf dem Linux-System

## Data Crawler herunterladen und installieren
{: #dc-download-install}

1.  Öffnen Sie einen Browser und melden Sie sich bei Ihrem [{{site.data.keyword.Bluemix}}-Konto ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/){: new_window} an.

1.  Wählen Sie in Ihrem {{site.data.keyword.Bluemix_notm}}-Dashboard den {{site.data.keyword.discoveryshort}}-Service aus, den Sie zuvor erstellt haben.

1.  Klicken Sie im Abschnitt **Upload von Inhalt in den Discovery-Service automatisieren** auf den entsprechenden Link, um den Data Crawler für Linux in DEB-, RPM- und ZIP-Formaten herunterzuladen.

1.  Vergewissern Sie sich, dass Java Runtime Environment Version 8 oder höher ausgeführt wird. Führen Sie den Befehl `java -version` aus und suchen Sie nach **1.8**. Falls eine frühere Version als **1.8** angegeben ist, müssen Sie für Java ein Upgrade durchführen, indem Sie Java Developer Kit (JDK) 8 aus Ihrem Paketmanagementsystem, von der Website [IBM JDK ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/developerworks/java/jdk/){: new_window} oder über [java.com ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.java.com){: new_window} installieren.

    Die Umgebungsvariable `JAVA_HOME` muss korrekt festgelegt sein oder darf andernfalls nicht festgelegt sein, damit der Crawler ausgeführt werden kann.
    {: tip}

1.  Führen Sie als Administrator die folgenden Befehle aus, um die heruntergeladene Archivdatei zu installieren:

    -   Verwenden Sie auf Systemen wie Red Hat und CentOS, die RPM-Pakete verwenden, einen Befehl wie etwa den Folgenden: `rpm -i /full/path/to/rpm/package/rpm-dateiname`
    -   Verwenden Sie auf Systemen wie Ubuntu und Debian, die DEB-Pakete verwenden, einen Befehl wie etwa den Folgenden: `dpkg -i /full/path/to/deb/package/deb-dateiname`
    -   Die Crawler-Scripts werden an der Position `{installationsverzeichnis}/bin` installiert (z. B. `/opt/ibm/crawler/bin`). Stellen Sie sicher, dass `{installationsverzeichnis}/bin` in Ihrer Umgebungsvariablen `PATH` angegeben ist.

    Crawler-Scripts werden auch an der Position `/usr/local/bin` installiert, weshalb diese Position ebenfalls zur Umgebungsvariablen `PATH` hinzugefügt werden kann.
    {: tip}
1.  Erstellen Sie Ihr Arbeitsverzeichnis, indem Sie den Inhalt des Verzeichnisses `{installationsverzeichnis}/share/examples/config` in ein Arbeitsverzeichnis auf Ihrem System (z. B. `/home/config`) kopieren.

    **Achtung:** Nehmen Sie keine direkten Änderungen an den Konfigurationsbeispieldateien vor. Kopieren Sie die Dateien und bearbeiten Sie die Kopie. Falls Sie die Beispieldateien direkt bearbeiten, wird Ihre Konfiguration möglicherweise bei einem Update von Data Crawler überschrieben oder bei der Deinstallation dieses Dienstprogramms entfernt.

    **Hinweis:** In diesen Anleitungen beziehen sich Verweise auf Dateien im Verzeichnis `config` (z. B. `config/crawler.conf`) auf diese Datei in Ihrem Arbeitsverzeichnis und NICHT im installierten Verzeichnis `{installationsverzeichnis}/share/examples/config`.

1.  Jetzt können Sie [Data Crawler für die Verbindung zu Ihrem Repository konfigurieren](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-connector-and-seed-options).

## Struktur von Data Crawler
{: #dc-structure}

Beim Download von Data Crawler werden die folgenden Ordner in Ihrem System abgelegt:

-   `doc`: Enthält Dateien mit Copyright- und Lizenzinformationen.
-   `bin`: Enthält die Scriptdateien für die Ausführung des Crawlers.
-   `connectorFramework`: Die Dateien in diesem Verzeichnis ermöglichen Aktionen für die Daten, bei denen es sich um interne Daten des Unternehmens oder um externe Daten im Web oder in der Cloud handeln kann.
-   `lib`: Enthält die vom Crawler verwendeten Bibliotheksdateien.
-   `share`
    -   `doc`: Stellt sowohl in HTML als auch in Markdown formatierte Dokumentationsdateien bereit.
    -   `examples/config`: Mit den Dateien in diesem Verzeichnis können Sie für den Crawler angeben, welche Daten für die Crawlersuche verwendet werden sollen und wohin die Sammlung der durchsuchten Daten nach Abschluss der Crawlersuche gesendet werden sollen, sowie außerdem weitere Optionen für die Verwaltung der Crawlersuche festlegen.
    -   `man`: Enthält die produktinternen Handbuchseiten mit der Dokumentation für den Crawler.

## Bekannte Einschränkungen in diesem Release
{: #dc-limitations}

-   Data Crawler wird möglicherweise blockiert, wenn der Dateisystemconnector mit einer ungültigen oder fehlenden URL ausgeführt wird.
-   Konfigurieren Sie den Wert für `urls_to_filter` in der Datei `crawler.conf` so, dass alle Whitelist-URLs oder regulären Ausdrücke in einem einzigen RegEx-Ausdruck enthalten sind. Weitere Informationen finden Sie unter [Optionen für Crawlersuche konfigurieren](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-crawl-options).
-   Der Pfad zur Konfigurationsdatei, der in der Option `--config -c` übergeben wird, muss ein qualifizierter Pfad sein. Er muss somit in den relativen Formaten `config/crawler.conf` oder `./crawler.conf` bzw. als absoluter Pfad wie `/path/to/config/crawler.conf` angegeben werden. Die Angabe von lediglich `crawler.conf` ist nur dann möglich, wenn die Datei `orchestration_service.conf` integriert ist, statt mit `include` in der `crawler.conf` Datei referenziert zu sein.
