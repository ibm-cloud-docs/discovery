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

# Data Crawler konfigurieren
{: #configuring-the-data-crawler}

Um Data Crawler für die Crawlersuche in Ihrem Repository zu konfigurieren, müssen Sie den geeigneten Eingabeadapter in der Datei `crawler.conf` angeben und anschließend repositoryspezifische Informationen in den Konfigurationsdateien für den Eingabeadapter konfigurieren.
{: shortdesc}

Sie können die {{site.data.keyword.discoveryshort}}-Tools oder die API für die Crawlersuche in Box-, Salesforce- und Microsoft SharePoint Online-Datenquellen verwenden. Weitere Informationen finden Sie unter [Verbindung zu Datenquellen herstellen](/docs/services/discovery/connect.html).
{: tip}

Bevor Sie die in den folgenden Schritten aufgeführten Änderungen vornehmen, müssen Sie sicherstellen, dass Sie Ihr Arbeitsverzeichnis erstellt haben, indem Sie den Inhalt des Verzeichnisses `{installationsverzeichnis}/share/examples/config` in ein Arbeitsverzeichnis auf Ihrem System kopiert haben (z. B. `/home/config`).

**Wichtig:** Nehmen Sie keine direkten Änderungen an den Konfigurationsbeispieldateien vor. Kopieren Sie die Dateien und bearbeiten Sie die Kopie. Falls Sie die Beispieldateien direkt bearbeiten, wird Ihre Konfiguration möglicherweise bei einem Update von Data Crawler überschrieben oder bei der Deinstallation dieses Dienstprogramms entfernt.

**Hinweis:** In diesen Anleitungen beziehen sich Verweise auf Dateien im Verzeichnis `config` (z. B. `config/crawler.conf`) auf diese Datei in Ihrem Arbeitsverzeichnis und NICHT im installierten Verzeichnis `{installationsverzeichnis}/share/examples/config`.

Die angegebenen Werte sind die Standardwerte in `config/crawler.conf` und konfigurieren den Dateisystemconnector:

1.  Öffnen Sie die Datei `config/crawler.conf` in einem Texteditor.

    -   Legen Sie für die Option `crawl_config_file` die Datei `.conf` fest, die Sie zuvor geändert haben (z. B. `connectors/filesystem.conf`).
    -   Legen Sie für die Option `crawl_seed_file` die Datei `-seed.conf` fest, die Sie zuvor geändert haben (z. B. `seeds/filesystem-seed.conf`).
    -   Legen Sie die Optionen `output_adapter`, `class` und `config` für den {{site.data.keyword.discoveryshort}}-Service wie folgt fest:

        ```
        class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

        config - "discovery_service"

        discovery_service {
          include "discovery/discovery_service.conf"
        }
        ```
        {: codeblock}

    In dieser Datei gibt es weitere, optionale Einstellungen, die gemäß Ihrer Umgebung festgelegt werden können. Ausführliche Informationen zum Festlegen dieser Werte finden Sie unter [Optionen für die Crawlersuche konfigurieren](/docs/services/discovery/data-crawler-discovery.html#configuring-crawl-options), [Eingabeadapter konfigurieren](/docs/services/discovery/data-crawler-discovery.html#input-adapter), [Ausgabeadapter konfigurieren](/docs/services/discovery/data-crawler-discovery.html#output-adapter) und [Zusätzliche Optionen für die Verwaltung der Crawlersuche](/docs/services/discovery/data-crawler-discovery.html#additional-crawl-management-options).

1.  Öffnen Sie die Datei `discovery/discovery_service.conf` in einem Texteditor. Ändern Sie die folgenden Werte für den entsprechenden {{site.data.keyword.discoveryshort}}-Service, den Sie zuvor in {{site.data.keyword.Bluemix}} erstellt haben:

    -   `environment_id`: Geben Sie die Umgebungs-ID für Ihren {{site.data.keyword.discoveryshort}}-Service an.
    -   `collection_id`: Geben Sie die Sammlungs-ID für Ihren {{site.data.keyword.discoveryshort}}-Service an.
    -   `configuration_id`: Geben Sie die Konfigurations-ID für Ihren {{site.data.keyword.discoveryshort}}-Service an.
    -   `configuration`: Geben Sie den vollständigen Pfad dieser Datei `discovery_service.conf` an, z. B. `/home/config/discovery/discovery_service.conf`.
    -   `username`: Geben Sie den Benutzernamen des Berechtigungsnachweises für Ihren {{site.data.keyword.discoveryshort}}-Service an.
    -   `password`: Geben Sie das Kennwort des Berechtigungsnachweises für Ihren {{site.data.keyword.discoveryshort}}-Service an.

    Diese Datei enthält weitere, optionale Einstellungen, die Sie gemäß Ihrer Umgebung festlegen können. Detaillierte Informationen zum Festlegen dieser Werte finden Sie unter [Serviceoptionen konfigurieren](/docs/services/discovery/data-crawler-discovery.html#configuring-service-options).

1.  Nachdem Sie diese Dateien geändert haben, können Sie eine Crawlersuche für Ihre Daten ausführen. Fahren Sie mit dem Abschnitt [Crawlersuche für Datenrepository ausführen](/docs/services/discovery/data-crawler-run.html#crawling-your-data-repository) fort.

## Optionen für die Crawlersuche konfigurieren
{: #configuring-crawl-options}

Die Informationen in der Datei `config/crawler.conf` teilen Data Crawler mit, welche Dateien für die Crawlersuche verwendet werden sollen (Eingabeadapter) und wohin die Sammlung der durchsuchten Dateien nach Abschluss der Crawlersuche gesendet werden soll (Ausgabeadapter). Außerdem enthält diese Datei weitere Optionen für die Verwaltung der Crawlersuche.

**Hinweis:** Sofern nichts anderes angegeben ist, sind alle Dateipfade relativ zum Verzeichnis `config`.

Um auf das produktinterne Handbuch für die Datei `crawler.conf` zuzugreifen, das die neuesten Informationen enthält, geben Sie den Befehl  `man crawler.conf` im Installationsverzeichnis des Crawlers ein.
{: tip}

In dieser Datei können die folgenden Optionen festgelegt werden:

### Eingabeadapter
{: #input-adapter}

-   **`class`**: Nur zur internen Verwendung. Definiert die Klasse des Eingabeadapters für Data Crawler. Der Standardwert ist `com.ibm.watson.crawler.connectorframeworkinputadapter.Crawl`.
-   **`config`**: Nur zur internen Verwendung. Definiert die Konfiguration des Connector-Frameworks. Der Standardkonfigurationsschlüssel in diesem Block, der an den ausgewählten Eingabeadapter übergeben werden muss, ist `connector_framework`.

    Das Connector-Framework ist das Element, das Ihnen den Kontakt mit Ihren Daten ermöglicht. Hierbei kann es sich um interne Daten des Unternehmens oder um externe Daten im Web oder in der Cloud handeln. Die Connectors ermöglichen den Zugriff auf eine Reihe unterschiedlicher Datenquellen, das Herstellen der Verbindung wird jedoch eigentlich durch den Crawlersuchprozess gesteuert.

    **Wichtig:** Vom Eingabeadapter im Connector-Framework abgerufene Daten werden lokal zwischengespeichert. Sie werden unverschlüsselt gespeichert. Die Daten werden standardmäßig in einem temporären Verzeichnis zwischengespeichert, dessen Inhalt bei einem Warmstart gelöscht wird und das nur für den Benutzer lesbar sein sollte, der den Crawlerbefehl ausgeführt hat.

    Es besteht die Möglichkeit, dass dieses Verzeichnis länger als der Crawler aktiv ist, falls das Connector-Framework beendet wurde, bevor es eine Bereinigung vornehmen konnte. Überlegen Sie genau, an welcher Position Sie die Daten zwischenspeichern wollen. Sie können hierzu zwar ein verschlüsseltes Dateisystem verwenden, müssen sich jedoch der Auswirkungen auf die Leistung bewusst sein. Welches Verhältnis zwischen Geschwindigkeit und Sicherheit für Ihre Crawlersuchen angemessen ist, können nur Sie selbst entscheiden.
-   **`crawl_config_file`**: Die für die Crawlersuche zu verwendende Konfigurationsdatei. Der Standardwert ist `connectors/filesystem.conf`.
-   **`crawl_seed_file`**: Die für die Crawlersuche zu verwendende Seeddatei. Der Standardwert ist `seeds/filesystem-seed.conf`.
-   **`id_vcrypt_file`**: Die Schlüsseldatei, die für die Datenverschlüsselung durch den Crawler verwendet wird; der im Crawler enthaltene Standardschlüssel ist `id_vcrypt`. Verwenden Sie das Script 'vcrypt' im Ordner `bin`, falls Sie eine neue Datei `id_vcrypt` generieren müssen.
-   **`crawler_temp_dir`**: Der temporäre Ordner des Crawlers für Connectorprotokolle. Ein Ordner `tmp` wird standardmäßig bereitgestellt. Falls der Ordner `tmp` noch nicht vorhanden ist, wird er im aktuellen Arbeitsverzeichnis erstellt.
-   **`extra_jars_dir`**: Fügt ein Verzeichnis mit zusätzlichen JAR-Dateien zum Klassenpfad des Connector-Frameworks hinzu.

    **Hinweis:** Diese Angabe ist relativ zum Verzeichnis `lib/java` des Connector-Frameworks.

    -   Dieser Wert muss bei Verwendung des SharePoint-Connectors `oakland` lauten.
    -   Dieser Wert muss bei Verwendung des Datenbankconnectors `database` lauten.

    Bei Verwendung anderer Connectors können Sie diesen Wert leer lassen (also die leere Zeichenfolge "" verwenden).

-   **`urls_to_filter`**: Eine Blacklist der nicht zu durchsuchenden URLs (jeweils angegeben im Format eines regulären Ausdrucks). Data Crawler durchsucht keine URLs, die nicht den bereitgestellten regulären Ausdrücken entsprechen.

    Die Domänenliste (`domain list`) enthält die Domänen, die nicht durchsucht werden können. Sie können bei Bedarf Domänen zur Liste hinzufügen.

    Die Dateitypliste (`filetype list`) enthält die Dateierweiterungen, die der Orchestrierungsservice nicht unterstützt.

    Entfernen Sie alle unterstützten Dateitypen aus den regulären Ausdrücken.

    Stellen Sie sicher, dass die Domäne für Ihre Seed-URLs durch den Filter zugelassen wird. Verwenden Sie einen leeren Filter für das Verhalten von `Alles zulassen`.

    Stellen Sie sicher, dass Ihre Seed-URL nicht durch einen Filter ausgeschlossen wird, da der Crawler andernfalls blockieren kann.

-   **`max_text_size`**: Die maximale Größe in Byte, die ein Dokument erreichen kann, bevor es durch das Connector-Framework auf Platte geschrieben wird. Eine Erhöhung dieses Wertes verringert die Menge der Dokumente, die auf Platte geschrieben werden, vergrößert jedoch den Speicherbedarf. Der Standardwert ist `1048576`.
-   **`extra_vm_params`**: Ermöglicht das Hinzufügen weiterer Java-Parameter zu dem Befehl, mit dem das Connector-Framework gestartet wird.

-   **`bootstrap_logging`**: Schreibt das Protokoll für den Start des Connector-Frameworks; ist lediglich beim erweiterten Debug von Nutzen. Mögliche Werte sind `true` oder `false`. Die Protokolldatei wird an der Position `crawler_temp_dir` geschrieben.

-   **`read-timeout`**: Legt fest, wie viele Sekunden der Crawler auf eine Antwort vom Connector-Framework wartet. Der Standardwert ist 5 Sekunden.

### Ausgabeadapter
{: #output-adapter}

-   **`class`**: Definiert die Klasse des Ausgabeadapters für Data Crawler.
-   **`config`**: Definiert, welcher Konfigurationsschlüssel an den Ausgabeadapter übergeben werden soll. Die Zeichenfolge muss einem Schlüssel in diesem Konfigurationsobjekt entsprechen. Codebeispiel:

    ```
    class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

    config - "discovery_service"

    discovery_service {
        include "discovery/discovery_service.conf"
      }
    ```
    {: codeblock}

    In diesem Beispiel ist `discovery_service` der Konfigurationsschlüssel.

Sie müssen einen Ausgabeadapter auswählen, indem Sie seinen Parameter `class` und seinen Schlüssel für `config` angeben.

-   **Ausgabeadapter für {{site.data.keyword.discoveryshort}}-Service**: Lädt durchsuchte Dokumente in den {{site.data.keyword.discoveryfull}}-Service hoch. Wählen Sie diesen Adapter aus, indem Sie den Parameter `class` und den Schlüssel für `config` wie folgt festlegen.

```
class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

config - "discovery_service"

discovery_service {
            include "discovery/discovery_service.conf"
          }
```
{: codeblock}

-   **Testausgabeadapter**: Der Testausgabeadapter schreibt eine Darstellung der durchsuchten Dateien an einer angegebenen Position. Wählen Sie diesen Adapter aus, indem Sie den Parameter `class` und den Schlüssel für `config` wie folgt festlegen.

    Mit dem zusätzlichen Parameter `output_directory` wird das Verzeichnis ausgewählt, in das die Darstellung der durchsuchten Daten geschrieben werden soll.

```
class - "com.ibm.watson.crawler.testoutputadapter.TestOutputAdapter"

config - "test"

output_directory - "/tmp/crawler-test-output"`
```
{: codeblock}

-   **`retry`**: Gibt die Optionen für die Wiederholung bei fehlgeschlagenen Versuchen an, Daten an den Ausgabeadapter mit einer Push-Operation zu übertragen.

    -   `max_attempts`: Die maximale Anzahl der Wiederholungsversuche. Der Standardwert ist `10`.
    -   `delay`: Die Mindestverzögerung zwischen den Versuchen in Sekunden. Der Standardwert ist `2`.
    -   `exponent_base`: Der Faktor, der den Zuwachs der Verzögerungszeit bei jedem fehlgeschlagenen Versuch bestimmt. Der Standardwert ist `2`.

    Die Formel lautet:

        **`d(nte_wiederholung) - delay * (wert_für_exponent_base ^ nte_wiederholung)`**

    Beispiel: Die Standardeinstellungen mit einer Verzögerung von 1 Sekunde und einer Exponentenbasis von 2 bewirken, dass die zweite Wiederholung (also der dritte Versuch) 2 Sekunden anstelle von 1 Sekunde und die nächste Wiederholung 4 Sekunden verzögert wird.

        `d(0) - 1 * (2 ^ 0)` = 1 Sekunde
        `d(1) - 1 * (2 ^ 1)` = 2 Sekunden
        `d(2) - 1 * (2 ^ 2)` = 4 Sekunden

    Bei Verwendung der Standardeinstellungen gibt es somit bis zu 10 Übergabeversuche, bei denen bis zu ca. 1022 Sekunden (also etwas mehr als 17 Minuten) gewartet wird. Diese Dauer ist ein Näherungswert, weil zusätzliche Zeit hinzugefügt wird, um die gleichzeitige Ausführung mehrerer erneuter Übergaben zu verhindern. Diese zeitliche 'Unschärfe' beträgt möglicherweise bis zu 10%, daher könnte sich die letzte Verzögerung im vorherigen Beispiel um bis zu 7,7 Sekunden verzögern. Die Wartezeit beinhaltet nicht die Zeit, die für das Herstellen der Verbindung zum Service, das Hochladen der Daten oder das Warten auf eine Antwort benötigt wird.

    Der Wert von `output_timeout` hat hier Vorrang vor der Wartezeit; falls die gesamte Wartezeit für Wiederholungen seine Einstellung überschreitet, schlägt die Übergabe auch dann fehl, wenn ein Versuch erfolgen sollte.
    {: tip}

### Zusätzliche Optionen für die Verwaltung der Crawlersuche
{: #additional-crawl-management-options}

-   **`full_node_debugging`**: Aktiviert den Debugmodus. Mögliche Werte sind `true` oder `false`.

    **Wichtig:** Bei dieser Option werden die vollständigen Daten jedes durchsuchten Dokuments in die Protokolle aufgenommen.   

-   **`logging.log4j.configuration_file`***: Die Konfigurationsdatei, die für die Protokollierung zu verwenden ist. In der Beispieldatei `crawler.conf` ist diese Option in `logging.log4j` definiert und ihr Standardwert lautet `log4j_custom.properties`. Diese Option muss unabhängig davon, ob eine Datei `.properties` oder `.conf` verwendet wird, ähnlich definiert werden.   
-   **`shutdown_timeout`**: Gibt in Minuten den Zeitlimitwert an, bevor die Anwendung beendet wird. Der Standardwert ist `10`.   
-   **`output_limit`**: Die höchste Anzahl von indexierbaren Elementen, die der Crawler gleichzeitig versucht, an den Ausgabeadapter zu senden. Dies kann durch die Anzahl der verfügbaren Kerne für die Ausführung der Arbeit weiter eingeschränkt werden. Der Wert besagt, dass an einem bestimmten Punkt nicht mehr als 'x' indexierbare Elemente an den Ausgabeadapter gesendet werden, während auf die Rückgabe gewartet wird. Der Standardwert ist `10`.   
-   **`input_limit`**: Begrenzt die Anzahl der URLs, die gleichzeitig aus dem Eingabeadapter angefordert werden können. Der Standardwert ist `30`.   
-   **`output_timeout`**: Gibt an, nach wie vielen Sekunden Data Crawler eine Anforderung an den Ausgabeadapter aufgibt und das Element anschließend aus der Warteschlange für den Ausgabeadapter entfernt, um eine weitere Verarbeitung zu ermöglichen. Der Standardwert ist `1200`.

    Die durch den Ausgabeadapter vorgegebenen Einschränkungen müssen berücksichtigt werden, da sich diese Einschränkungen auf die hier definierten Grenzwerte auswirken können. Der definierte Wert für `output_limit` bezieht sich lediglich darauf, wie viele indexierbare Objekte gleichzeitig an den Ausgabeadapter gesendet werden können. Sobald ein indexierbares Objekt an den Ausgabeadapter gesendet wurde, wird es bei der Zählung berücksichtigt, die durch die Variable `output_timeout` definiert wird. Es kann sein, dass der Ausgabeadapter selbst eine Drosselung vornimmt, die verhindert, dass er so viele Eingaben verarbeiten kann, wie er empfängt. Beispielsweise kann der Ausgabeadapter für die Orchestrierung einen Verbindungspool besitzen, der für HTTP-Verbindungen zum Service konfigurierbar ist. Falls er beispielsweise den Standardwert 8 verwendet und Sie für `output_limit` einen größeren Wert als 8 festlegen, gibt es Prozesse, die bei der Zählung berücksichtigt wurden und deren Verarbeitung aussteht. In einem solchen Fall kann es zu Zeitlimitüberschreitungen kommen.   
-   **`num_threads`**: Die Anzahl von parallelen Threads, die gleichzeitig aktiv sein können. Dieser Wert kann entweder eine ganze Zahl sein, die die Anzahl der parallelen Threads direkt angibt, oder aber eine Zeichenfolge im Format `"xNUM"`, die den Multiplikationsfaktor für die Anzahl verfügbarer Prozessoren angibt, z. B. `"x1.5"`. Der Standardwert ist `"30"`.

## Serviceoptionen konfigurieren
{: #configuring-service-options}

Der {{site.data.keyword.discoveryshort}}-Service weist den Crawler an, wie durchsuchte Dateien unter Verwendung des {{site.data.keyword.discoveryfull}}-Service zu verwalten sind.

Um auf das produktinterne Handbuch für die Datei `discovery-service.conf` zuzugreifen, das die neuesten Informationen enthält, geben Sie den folgenden Befehl im Installationsverzeichnis des Crawlers ein:

  ```bash
  man discovery_service.conf
  ```
  {: pre}
{: tip}

Standardoptionen können Sie direkt ändern, indem Sie die Datei `config/discovery/discovery_service.conf` öffnen und die folgenden Werte Ihrem Anwendungsfall entsprechend angeben:

-   **`http_timeout`**: Das Zeitlimit in Sekunden für die Operation zum Lesen/Indexieren von Dokumenten. Der Standardwert ist `125`.
-   **`proxy_host_port`** (optional): Wenn Data Crawler hinter einer Firewall ausgeführt wird, müssen Sie möglicherweise den Proxy-Hostnamen und die Proxy-Portnummer festlegen, damit Data Crawler mit dem {{site.data.keyword.discoveryshort}}-Service kommunizieren kann. Der Standardwert für diese Option ist eine leere Zeichenfolge. Falls Sie den Wert ändern müssen, sollte er das Format `"<host>:<port>"`.
-   **`concurrent_upload_connection_limit`**: Die zulässige Anzahl gleichzeitiger Verbindung für das Hochladen von Dokumenten. Der Standardwert ist `2`.

    **Hinweis:** Bei Verwendung des Ausgabeadapters für den Orchestrierungsservice sollte dieser Wert größer-gleich dem Wert für `output_limit` sein, der beim Konfigurieren der Optionen für die Crawlersuche festgelegt wurde.   

-   **`base_url`**: Die URL, an die Ihre durchsuchten Dokumente gesendet werden. Beim aktuellen Release des {{site.data.keyword.discoveryshort}}-Service lautet sie `https://gateway.watsonplatform.net/discovery/api`.   
-   **`environment_id`**: Die Position Ihrer durchsuchten Dokumentsammlung bei der Basis-URL.   
-   **`collection_id`**: Der Name der Dokumentsammlung, den Sie im {{site.data.keyword.discoveryshort}}-Service festgelegt haben.
-   **`api_version`**: Nur zur internen Verwendung. Das Datum für die letzte Änderung der API-Version.   
-   **`configuration_id`**: Der Dateiname der Konfigurations-ID, die vom {{site.data.keyword.discoveryshort}}-Service verwendet wird.
-   **`username`**: Der Benutzername für die Authentifizierung bei der Position Ihrer durchsuchten Dokumentsammlung.   
-   **`password`**: Das Kennwort für die Authentifizierung bei der Position Ihrer durchsuchten Dokumentsammlung.

Der Ausgabeadapter für den {{site.data.keyword.discoveryshort}}-Service kann Statistikdaten senden, damit {{site.data.keyword.IBM}} durch die Erzielung von weiteren Erkenntnissen einen besseren Service für die Benutzer bereitstellen kann. Die folgenden Optionen können für die Variable `send_stats` festgelegt werden:

-   **`jvm`**: Zu den über Java Virtual Machine (JVM) gesendeten Statistikdaten gehören der Java-Anbieter und die Java-Version, die von der JVM gemeldet wurden, mit der Data Crawler ausgeführt wird. Der Wert ist entweder `true` oder `false`. Der Standardwert ist `true`.
-   **`os`**: Zu den über das Betriebssystem gesendeten Statistikdaten gehören der Name, die Version und die Architektur des Betriebssystems, die von der JVM gemeldet wurden, mit der Data Crawler ausgeführt wird. Der Wert ist entweder `true` oder `false`. Der Standardwert ist `true`.
