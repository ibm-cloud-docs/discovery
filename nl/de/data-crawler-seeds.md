---

copyright:
  years: 2015, 2017, 2019
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

# Connector und Seedoptionen konfigurieren
{: #configuring-connector-and-seed-options}

Bei einer Crawlersuche in den Daten ermittelt der Crawler zuerst den Typ des Datenrepositorys (also den Connector) und die benutzerdefinierte Startposition (den Seed), bevor er mit dem Herunterladen von Informationen beginnt.
{: shortdesc}

Data Crawler sollte nur zum Durchsuchen von Dateifreigaben oder Datenbanken verwendet werden, in allen anderen Fällen sollten Sie den entsprechenden {{site.data.keyword.discoveryshort}}-Connector verwenden. Weitere Informationen finden Sie unter [Verbindung zu Datenquellen herstellen](/docs/services/discovery?topic=discovery-sources#sources). Data Crawler wird nicht mehr unterstützt, falls Sie ihn mit einer Datenquelle verwenden, die von den {{site.data.keyword.discoveryshort}}-Connectoren unterstützt wird.
{: important}

**Wichtig:** Bei Verwendung von Data Crawler werden Sicherheitseinstellungen für das Datenrepository ignoriert.

Seeds sind der Ausgangspunkt einer Crawlersuche und werden von Data Crawler verwendet, um Daten aus der Ressource abzurufen, die durch den Connector angegeben ist. Seeds konfigurieren normalerweise URLs für den Zugriff auf protokollbasierte Ressourcen wie Dateifreigaben, SMB-Freigaben, Datenbanken und andere Datenrepositorys, die für verschiedene Protokolle zugänglich sind. Unterschiedliche Seed-URLs können darüber hinaus unterschiedliche Leistungsmerkmale aufweisen. Seeds können ebenfalls repositoryspezifisch sein, was eine Crawlersuche in bestimmten Anwendungen anderer Anbieter (z. B. Systemen für das Customer-Relationship-Management, Systemen für das Produktlebenszyklusmanagement, Content-Management-Systemen, cloudbasierten Anwendungen und Webdatenbankanwendungen) ermöglicht.

Damit die Crawlersuche für Ihre Daten korrekt ausgeführt wird, müssen Sie sicherstellen, dass der Crawler für das Lesen Ihres Datenrepositorys ordnungsgemäß konfiguriert wurde. Data Crawler stellt Connectors bereit, damit die Datensammlung aus den folgenden Repositorys unterstützt wird:

-   [Dateisystem](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-filesystem-crawl-options)
-   [Datenbanken (über JDBC)](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-database-crawl-options)
-   [CMIS (Content Management Interoperability Services)](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-cmis-crawl-options)
-   [SMB- (Server Message Block), CIFS- (Common Internet Filesystem) oder Samba-Dateifreigaben](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#smb-cifs-samba-crawl-options)

Es gibt außerdem eine Connectorkonfigurationsvorlage, mit deren Hilfe Sie einen Connector anpassen können.

So konfigurieren Sie Ihren Connector:

1.  Öffnen Sie in einem Texteditor die Datei im Verzeichnis `connectors`, das dem Repository entspricht, zu dem Sie eine Verbindung herstellen wollen (beispielsweise ist `filesystem.conf` die Konfigurationsdatei für den Dateisystemconnector).

1.  Ändern Sie die entsprechenden Werte für Ihr Repository:

    -   [Dateisystem](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#filesystem-crawl-options)
    -   [Datenbanken (über JDBC)](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#database-crawl-seed)
    -   [CMIS (Content Management Interoperability Services)](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#cmis-crawl-options)
    -   [SMB- (Server Message Block), CIFS- (Common Internet Filesystem) oder Samba-Dateifreigaben](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#smb-cifs-samba-crawl-options)
1.  Speichern und schließen Sie die Datei.
1.  Wiederholen Sie die Schritte in einem Texteditor für die Datei `-seed.conf` in dem Verzeichnis `connectors/seeds`, das dem zu verbindenden Repository entspricht (beispielsweise ist `filesystem-seed.conf` die Konfigurationsdatei für den Seed, also das Ziel der Verbindung, für den Dateisystemconnector).
1.  Fahren Sie mit dem [Konfigurieren von Data Crawler für die Verbindung zu {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-the-data-crawler) fort.

Um auf das produktinterne Handbuch für die Connector- und Seedkonfigurationsdateien zuzugreifen, das die neuesten Informationen enthält, geben Sie die folgenden Befehle im Installationsverzeichnis des Crawlers ein:
-   Zum Aufrufen von Informationen zu den Connectorkonfigurationsoptionen:
    ```bash
    man crawler-options.conf
    ```
    {: pre}
-   Zum Aufrufen von Informationen zu den Konfigurationsoptionen für den Seed der Crawlersuche:
    ```bash
    man crawler-seed.conf
    ```
    {: pre}


## Optionen für die Crawlersuche in Dateisystemen konfigurieren
{: #filesystem-crawl-options}

Mit dem Dateisystemconnector können Sie Dateien durchsuchen, die sich an einer aus Sicht der Data Crawler-Installation lokalen Position befinden.

Eine weitere Option zum Hochladen einer großen Anzahl von Dateien in {{site.data.keyword.discoveryshort}} ist [discovery-files ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/IBM/discovery-files){: new_window} auf GitHub.
{: note}

### Dateisystemconnector konfigurieren
{: #filesystem-connector}

Für die Verwendung des Dateisystemconnectors werden die folgenden Basiskonfigurationsoptionen benötigt. Zum Festlegen dieser Werte öffnen Sie die Datei `config/connectors/filesystem.conf` und ändern Sie die folgenden Werte Ihren Anwendungsfällen entsprechend:

-   **`protocol`**: Der Name des Connectorprotokolls, das für die Crawlersuche verwendet wird. Verwenden Sie für diesen Connector den Wert `sdk-fs`.
-   **`collection`**: Dieses Attribut wird zum Entpacken von temporären Dateien verwendet. Der Standardwert ist `crawler-fs`.
-   **`logging-config`**: Gibt die Datei an, die zum Konfigurieren der Protokollierungsoptionen verwendet wird; der Wert muss als XML-Zeichenfolge gemäß `log4j` formatiert sein.
-   **`classname`**: Der Java-Klassenname für den Connector. Für diesen Connector muss der Wert `plugin:filesystem.plugin@filesystem` verwendet werden.

### Seed für Crawlersuche in Dateisystemen konfigurieren
{: #filesystem-crawl-seed}

Die folgenden Werte können in der Datei konfiguriert werden, die den Seed für die Crawlersuche in Dateisystemen definiert. Zum Festlegen dieser Werte öffnen Sie die Datei `config/seeds/filesystem-seed.conf` und geben Sie die folgenden Werte Ihren Anwendungsfällen entsprechend an:

-   **`url`**: Eine durch Zeilenumbrüche getrennte Liste von Dateien und Ordnern, für die eine Crawlersuche ausgeführt werden soll. UNIX-Benutzer können einen Pfad wie z. B. `/usr/local/` verwenden.

    **Hinweis:** Die URLs müssen mit der Zeichenfolge `sdk-fs://` beginnen. Um beispielsweise `/home/watson/mydocs` zu durchsuchen, muss als Wert dieser URL daher `sdk-fs:///home/watson/mydocs` angegeben werden. Der dritte Schrägstrich ist unbedingt erforderlich!

    Die von Linux-, UNIX- und UNIX-ähnlichen Computersystemen verwendeten Dateisysteme können besondere Dateitypen enthalten, beispielsweise Block-  und Zeicheneinheitenknoten und Dateien, die benannte Pipes darstellen. Diese Dateien können nicht durchsucht werden, weil sie keine Daten enthalten, sondern als Zugriffspunkte für Einheiten oder Ein-/Ausgabe dienen. Der Versuch, solche Dateien zu durchsuchen, verursacht Fehler bei der Crawlersuche. Zur Vermeidung derartiger Fehler sollten Sie das Verzeichnis `/dev` bei jeder übergeordneten Crawlersuche in einem Linux-, UNIX- oder UNIX-ähnlichen Dateisystem ausschließen. Falls das System, in dem Sie die Crawlersuche ausführen, temporäre Systemverzeichnisse wie z. B. `/proc`, `/sys` und `/tmp` vorhanden sind, die temporäre Dateien und Systeminformationen enthalten, sollten Sie diese Verzeichnisse ebenfalls ausschließen.   **`hops`**: Nur zur internen Verwendung.   **`default-allow`**: Nur zur internen Verwendung.
    {: tip}

## Optionen für die Crawlersuche in Datenbanken konfigurieren
{: #database-crawl}

Mit dem Datenbankconnector können Sie eine Datenbank durchsuchen, indem Sie einen angepassten SQL-Befehl ausführen und ein Dokument pro Zeile (Datensatz) sowie ein Inhaltselement pro Spalte (Feld) erstellen. Sie können eine als eindeutigen Schlüssel zu verwendende Spalte sowie eine Spalte mit einer Zeitmarke angeben, die das letzte Änderungsdatum für jeden Datensatz angibt. Der Connector ruft alle Datensätze aus der angegebenen Datenbank ab und kann in der SQL-Anweisung auch auf bestimmte Tabellen, Verknüpfungen usw. beschränkt werden.

Mit dem Datenbankconnector können Sie die folgenden Datenbanken durchsuchen:

-   {{site.data.keyword.IBM}} DB2
-   MySQL
-   Oracle PostgreSQL
-   Microsoft SQL Server
-   Sybase
-   Andere SQL-konforme Datenbanken über einen mit JDBC 3.0 konformen Treiber

Der Connector ruft alle Datensätze aus der angegebenen Datenbank und Tabelle ab.

***JDBC-Treiber***: Der Datenbankconnector wird mit der Treiberversion 1.5 von Oracle JDBC (Java Database Connectivity) ausgeliefert. Alle mit Data Crawler ausgelieferten JDBC-Treiber anderer Anbieter befinden sich im Verzeichnis `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` der Data Crawler-Installation. Dort können Sie die Treiber bei Bedarf hinzufügen, entfernen und ändern. Mit der Einstellung `extra_jars_dir` in der Datei `crawler.conf` können Sie außerdem eine andere Position angeben.

***Db2-JDBC-Treiber***: Data Crawler wird aufgrund von Lizenzierungsproblemen nicht mit den JDBC-Treibern für DB2 ausgeliefert. Alle Db2-Installationen, in denen die JDBC-Unterstützung installiert ist, enthalten jedoch die JAR-Dateien, die Data Crawler benötigt, um eine Db2-Installation zu durchsuchen. Um eine Crawlersuche für eine Db2-Instanz durchzuführen, müssen Sie diese Dateien in das entsprechende Verzeichnis der Data Crawler-Installation kopieren, damit sie vom Datenbankconnector verwendet werden können. Um eine Crawlersuche von Data Crawler in einer Db2-Installation zu aktivieren, suchen Sie nach der JAR-Datei `db2jcc.jar` und der JAR-Datei für die Lizenz (normalerweise `db2jcc_license_cu.jar`) in Ihrer Db2-Installation und kopieren Sie diese Dateien in das Unterverzeichnis `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` des Data Crawler-Installationsverzeichnisses. Alternativ können Sie auch mit der Einstellung `extra_jars_dir` in der Datei `crawler.conf` eine andere Position angeben.

***MySQL-JDBC-Treiber***: Data Crawler wird nicht mit den JDBC-Treibern für MySQL ausgeliefert, weil bei deren Lieferung im Rahmen des Produkts Lizenzprobleme bestehen könnten. Die JAR-Datei, die die MySQL-JDBC-Treiber enthält, können Sie jedoch ganz leicht herunterladen und in Ihre Data Crawler-Installation integrieren:

1.  Rufen Sie in einem Web-Browser die MySQL-Download-Site auf und suchen Sie nach der Quelle und dem Binär-Download-Link für das Archivformat, das Sie verwenden wollen (bei Microsoft Windows-Systemen normalerweise 'zip' bzw. bei Linux-Systemen mit 'gzip' komprimierte TAR-Datei). Klicken Sie auf diesen Link, um den Downloadprozess zu starten. Möglicherweise ist eine Registrierung erforderlich.
1.  Verwenden Sie den entsprechenden Befehl 'unzip archivdateiname' bzw. 'tar zxf archivdateiname' für den Typ und den Namen der heruntergeladenen Archivdatei, um den Inhalt dieser Archivdatei zu extrahieren.
1.  Wechseln Sie in das Verzeichnis, das aus der Archivdatei extrahiert wurde, und kopieren Sie die JAR-Datei aus diesem Verzeichnis in das Unterverzeichnis `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` Ihres Data Crawler-Installationsverzeichnisses. Alternativ können Sie mit der Einstellung `extra_jars_dir` in der Datei `crawler.conf` auch eine andere Position angeben.

### Datenbankconnector konfigurieren
{: #database-connector}

Für die Verwendung des Datenbankconnectors werden die folgenden Basiskonfigurationsoptionen benötigt. Zum Festlegen dieser Werte öffnen Sie die Datei `config/connectors/database.conf` und ändern Sie die folgenden Werte Ihren Anwendungsfällen entsprechend:

-   **`protocol`**: Der Name des Connectorprotokolls, das für die Crawlersuche verwendet wird. Der Wert für diesen Connector richtet sich nach dem Datenbanksystem, auf das zugegriffen werden soll.
-   **`collection`**: Dieses Attribut wird zum Entpacken von temporären Dateien verwendet.
-   **`classname`**: Der Java-Klassenname für den Connector. Für diesen Connector muss der Wert `plugin:database.plugin@database` verwendet werden.
-   **`logging-config`**: Gibt die Datei an, die zum Konfigurieren der Protokollierungsoptionen verwendet wird; der Wert muss als XML-Zeichenfolge gemäß `log4j` formatiert sein.

### Seed für Crawlersuche in Datenbanken konfigurieren
{: #database-crawl-seed}

Die folgenden Werte können in der Datei konfiguriert werden, die den Seed für die Crawlersuche in Datenbanken definiert. Zum Festlegen dieser Werte öffnen Sie die Datei `config/seeds/database-seed.conf` und geben Sie die folgenden Werte Ihren Anwendungsfällen entsprechend an:

-   **`url`**: Die URL der abzurufenden Tabelle oder Sicht. Definiert Ihre angepasste Seed-URL für die SQL-Datenbank. Die Struktur lautet:

    -   `datenbanksystem://host:port/datenbank?[per=num]&[sql=SQL]`

    Beim Testen einer Seed-URL werden alle eingereihten URLs angezeigt. Beispiel: Die folgende URL wird für eine Datenbank mit 200 Datensätzen getestet:
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?per=100&sql=select%20*%20from%20vessel&`

    Daraufhin werden die folgenden eingereihten URLs angezeigt:
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=0&`
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=100&`
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=200&`

    Beim Testen der folgenden URL werden hingegen die aus Zeile 43 abgerufenen Daten angezeigt:
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?per-1&key-val=43`
-   **`hops`**: Nur zur internen Verwendung.
-   **`default-allow`**: Nur zur internen Verwendung.
-   **`user-password`**: Berechtigungsnachweise für das Datenbanksystem. Der Benutzername und das Kennwort müssen durch einen Doppelpunkt (`:`) voneinander abgegrenzt werden und das Kennwort muss mit dem Programm 'vcrypt', das mit Data Crawler ausgeliefert wird, verschlüsselt werden. Beispiel: `benutzername:[[vcrypt/3]]kennwortzeichenfolge`
-   **`max-data-size`**: Die maximale Größe der Daten für ein Dokument. Dies ist der größte Hauptspeicherblock, der jeweils geladen wird. Setzen Sie diesen Grenzwert nur herauf, wenn auf Ihrem Computer ausreichend Hauptspeicher verfügbar ist.
-   **`filter-exact-duplicates`**: Nur zur internen Verwendung.
-   **`timeout`**: Nur zur internen Verwendung.
-   **`jdbc-class`** (Extender-Option): Bei Angabe dieser Option überschreibt diese Zeichenfolge die vom Connector verwendete JDBC-Klasse, wenn `(other)` als Wert für das Datenbanksystem ausgewählt ist.
-   **`connection-string`** (Extender-Option): Bei Angabe dieser Option überschreibt diese Zeichenfolge die automatisch generierte JDBC-Verbindungszeichenfolge. Auf diese Weise können Sie eine detailliertere Konfiguration für die Datenbankverbindung angeben, z. B. einen Lastausgleich oder SSL-Verbindungen. Beispiel: `jdbc:netezza://127.0.0.1:5480/datenbankname`.
-   **`save-frequency-for-resume`** (Extender-Option): Gibt den Namen einer Spalte oder zugeordneten Kennzeichnung an, damit eine Crawlersuche wiederaufgenommen oder eine Teilaktualisierung ausgeführt werden kann. Der Seed speichert den Namen dieser Spalte in regelmäßigen Abständen, wenn er die Crawlersuche weiter ausführt, und erneut, sobald die letzte Zeile der Datenbank durchsucht wurde. Wenn die Crawlersuche wiederaufgenommen oder aktualisiert wird, beginnt die Crawlersuche bei der Zeile, die im gespeicherten Wert für dieses Feld angegeben ist.

## Optionen für die Crawlersuche in CMIS konfigurieren
{: #cmis-crawl-options}

Mit dem Connector für CMIS (Content Management Interoperability Services) können Sie CMIS-fähige Repositorys von Content-Management-Systemen (CMS-Repositorys) durchsuchen (z. B. Alfresco, Documentum oder {{site.data.keyword.IBM}} Content Manager) und die in ihnen enthaltenen Daten indexieren.

### CMIS-Connector konfigurieren
{: #cmis-connector}

Für die Verwendung des CMIS-Connectors werden die folgenden Basiskonfigurationsoptionen benötigt. Zum Festlegen dieser Werte öffnen Sie die Datei `config/connectors/cmis.conf` und geben Sie die folgenden Werte Ihren Anwendungsfällen entsprechend an:

-   **`protocol`**: Der Name des Connectorprotokolls, das für die Crawlersuche verwendet wird. Für diesen Connector muss der Wert `cmis` verwendet werden.
-   **`collection`**: Dieses Attribut wird zum Entpacken von temporären Dateien verwendet.
-   **`dns`**: Nicht verwendete Option.
-   **`classname`**: Der Java-Klassenname für den Connector. Verwenden Sie für diesen Connector den Wert `plugin:cmis-v1.1.plugin@connector`.
-   **`logging-config`**: Gibt die Datei an, die zum Konfigurieren der Protokollierungsoptionen verwendet wird; der Wert muss als XML-Zeichenfolge gemäß `log4j` formatiert sein.
-   **`endpoint`**: Die Serviceendpunkt-URL eines CMIS-konformen Repositorys. 
-   **`username`**: Der Benutzername des CMIS-Repositorybenutzers, mit dem auf den Inhalt zugegriffen wird. Dieser Benutzer muss Zugriff auf alle Zielordner und -dokumente besitzen, die durchsucht und indexiert werden sollen.
-   **`password`**: Das Kennwort des CMIS-Repositorys, das für den Zugriff auf den Inhalt verwendet wird. Das Kennwort darf NICHT verschlüsselt sein und sollte als einfacher Text angegeben werden.
-   **`repositoryid`**: Die ID des CMIS-Repositorys, die für den Zugriff auf den Inhalt in diesem speziellen Repository verwendet wird.
-   **`bindingtype`**: Gibt an, welcher Bindungstyp für das Herstellen einer Verbindung zu einem CMIS-Repository verwendet werden soll. Der Wert ist entweder 'AtomPub' oder 'WebServices'.
-   **`authentication`**: Gibt an, welcher Typ für das Authentifizierungsverfahren verwendet werden soll, wenn eine Verbindung zu einem CMIS-konformen Repository hergestellt wird (HTTP-Basisauthentifizierung, NTML oder WS-Security (Benutzernamenstoken)).
-   **`enable-acl`**: Ermöglicht den Abruf von ACLs für durchsuchte Daten. Wenn die Sicherheit für die Dokumente in dieser Sammlung unproblematisch ist, verbessert die Inaktivierung dieser Option die Leistung, da diese Informationen nicht mit dem Dokument angefordert, nicht abgerufen und nicht verschlüsselt werden. Der Wert ist entweder 'true' oder 'false'.
-   **`user-agent`**: Ein Header, der beim Durchsuchen von Dokumenten an den Server gesendet wird.
-   **`method`**: Die Methode (GET oder POST), mit der Parameter übergeben werden.
-   **`url-logging`**: Der Umfang für die Protokollierung der durchsuchten URLs. Mögliche Werte:

    -   `full-logging`: Alle Informationen zur URL werden protokolliert.
    -   `refined-logging`: Nur die Informationen, die zum Durchsuchen des Crawlerprotokolls und für eine ordnungsgemäße Funktion des Connectors erforderlich sind, werden protokolliert. Dies ist der Standardwert.
    -   `minimal-logging`: Nur ein Minimum der Informationen, die für die ordnungsgemäße Funktion des Connectors erforderlich sind, werden konfiguriert.

    Wenn Sie für diese Option den Wert `minimal-logging` festlegen, verringert sich die Größe der Protokolle und Sie erzielen eine leichte Leistungsverbesserung, da durch die Reduzierung der protokollierten Datenmenge weniger Ein-/Ausgabeoperationen erfoderlich sind.
-   **`ssl-version`**: Gibt eine für HTTPS-Verbindungen zu verwendende SSL-Version an. Standardmäßig wird das strengste verfügbare Protokoll verwendet.

### Seed für CMIS-Crawlersuche konfigurieren
{: #cmis-crawl-seed}

Die folgenden Werte können in der Datei konfiguriert werden, die den Seed für die CMIS-Crawlersuche definiert. Zum Festlegen dieser Werte öffnen Sie die Datei `config/seeds/cmis-seed.conf` und ändern Sie die folgenden Werte Ihren Anwendungsfällen entsprechend:

-   **`url`**: Die URL eines Ordners aus dem CMIS-Repository, der als Ausgangspunkt der Crawlersuche verwendet werden soll (z. B. `cmis://alfresco.test.com:8080/alfresco/cmisatom?folderToProcess-workspace://SpacesStore/guid`).

    Um die Crawlersuche beim Stammordner beginnen zu lassen, müssen Sie die URL wie folgt angeben: `cmis://alfresco.test.com:8080/alfresco/cmisatom?folderToProcess-`.
-   **`at`**: Nicht verwendete Option.
-   **`default-allow`**: Nur zur internen Verwendung.

## Optionen für die Crawlersuche in SMB/CIFS/Samba konfigurieren
{: #smb-cifs-samba-crawl-options}

Mit dem Samba-Connector können Sie Dateifreigaben von Server Message Block (SMB) und Common Internet Filesystem (CIFS) durchsuchen. Dieser Dateifreigabetyp ist in Windows-Netzen gängig und wird auch durch das Open-Source-Projekt 'Samba' bereitgestellt.

### Samba-Connector konfigurieren
{: #smb-cifs-samba-crawl-connector}

Für die Verwendung des Samba-Connectors werden die folgenden Basiskonfigurationsoptionen benötigt. Zum Festlegen dieser Werte öffnen Sie die Datei `config/connectors/samba.conf` und geben Sie die folgenden Werte Ihren Anwendungsfällen entsprechend an:

-   **`protocol`**: Der Name des Connectorprotokolls, das für die Crawlersuche verwendet wird. Für diesen Connector muss der Wert `smb` verwendet werden.
-   **`collection`**: Dieses Attribut wird zum Entpacken von temporären Dateien verwendet.
-   **`classname`**: Der Java-Klassenname für den Connector. Für diesen Connector muss der Wert `plugin:smb.plugin@connector` verwendet werden.
-   **`logging-config`**: Gibt die Datei an, die zum Konfigurieren der Protokollierungsoptionen verwendet wird; der Wert muss als XML-Zeichenfolge gemäß `log4j` formatiert sein.
-   **`username`**: Der Samba-Benutzername für die Authentifizierung. Wenn er angegeben wird, müssen auch die Domäne und das Kennwort angegeben werden. Ist er nicht angegeben, wird das Gastkonto verwendet.
-   **`password`**: Das Samba-Kennwort für die Authentifizierung. Falls der Benutzername angegeben ist, ist dieser Wert erforderlich. Das Kennwort muss mit dem Programm 'vcrypt', das mit Data Crawler ausgeliefert wird, verschlüsselt werden.
-   **`archive`**: Ermöglicht dem Samba-Connector das Durchsuchen und Indexieren von Datenen, die innerhalb von Archivdateien komprimiert sind. Der Wert ist entweder 'true' oder 'false'; Standardwert ist 'false'.
-   **`max-policies-per-handle`**: Gibt die maximale Anzahl von LSA-Richtlinien (LSA = Local Security Authority, lokale Sicherheitsautorität) an, die für eine einzelne RPC-Kennung geöffnet werden können. Diese Richtlinien definieren die Zugriffsberechtigungen, die zum Abfragen oder Ändern eines bestimmten Systems unter verschiedenen Bedingungen erforderlich sind. Der Standardwert für diese Option ist 255.
-   **`crawl-fs-metadata`**: Bei Aktivierung dieser Option fügt Data Crawler ein VXML-Dokument hinzu, das die verfügbaren Dateisystemmetadaten über die Datei (Erstellungsdatum, Datum der letzten Änderung, Dateiattribute usw.) enthält.
-   **`enable-arc-connector`**: Nicht verwendete Option.
-   **`disable-indexes`**: Eine durch Zeilenumbrüche getrennte Liste von Indizes, die inaktiviert werden sollen, was eine Crawlersuche beschleunigen kann. Beispiel:

    -   `disable-url-index`
    -   `disable-error-state-index`
    -   `disable-crawl-time-index`
-   **`exact-duplicates-hash-size`**: Legt die Größe der Hashtabelle fest, die zur Auflösung von identischen Duplikaten verwendet wird. Gehen Sie bei einer Änderung dieses Wertes äußerst umsichtig vor. Der von Ihnen ausgewählte Wert sollte eine Primzahl sein. Höhere Größen können schnellere Suchvorgänge ermöglichen, benötigen jedoch mehr Hauptspeicher, während kleinere Größen die Suchvorgänge verlangsamen können, die Hauptspeichernutzung jedoch wesentlich reduzieren.
-   **`user-agent`**: Nicht verwendete Option.
-   **`timeout`**: Nur zur internen Verwendung.
-   **`n-concurrent-requests`**: Die Anzahl der Anforderungen, die parallel an eine einzelne IP-Adresse gesendet werden. Der Standardwert ist `1`.
-   **`enqueue-persistence`**: Nicht verwendete Option.

### Seed für Samba-Crawlersuche konfigurieren
{: #smb-cifs-samba-crawl-seed}

Die folgenden Werte können in der Datei konfiguriert werden, die den Seed für die Samba-Crawlersuche definiert. Zum Festlegen dieser Werte öffnen Sie die Datei `config/seeds/samba-seed.conf` und geben Sie die folgenden Werte Ihren Anwendungsfällen entsprechend an:

-   **`url`**: Eine durch Zeilenumbrüche getrennte Liste von zu durchsuchenden Freigaben. Beispiel:

    ```
    smb://share.test.com/office
    smb://share.test.com/cash/money/change
    smb://share.test.com/C$/Program Files
    ```
    {: codeblock}

-   **`hops`**: Nur zur internen Verwendung.
-   **`default-allow`**: Nur zur internen Verwendung.
