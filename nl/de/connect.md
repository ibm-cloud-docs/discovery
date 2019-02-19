---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-14"

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

# Verbindung zu Datenquellen herstellen
{: #sources}

Mit dem {{site.data.keyword.discoveryshort}}-Service können Sie eine Verbindung zu Dokumenten aus fernen Quellen herstellen und diese durchsuchen.
{: shortdesc}

Sie können eine Verbindung zu einer Datenquelle herstellen und Dokumente nach einem Zeitplan (falls gewünscht) in den {{site.data.keyword.discoveryshort}}-Service extrahieren, indem Sie eine Sammlung konfigurieren, die dieser Quelle zugeordnet werden soll. Jede Sammlung kann mit einer Datenquelle konfiguriert werden. Der {{site.data.keyword.discoveryshort}}-Service extrahiert Dokumente aus der Datenquelle mit einem Prozess, der als Crawlersuche bezeichnet wird. Die Crawlersuche ist der Prozess, mit dem Dokumente systematisch von der angegebenen Startposition aus durchsucht und abgerufen werden. Nur Elemente, die explizit von Ihnen angegeben wurden, werden durch den {{site.data.keyword.discoveryshort}}-Service durchsucht. Die folgenden Typen von Datenquellen können durchsucht werden:

-  [Box](/docs/services/discovery/connect.html#connectbox)
-  [Salesforce](/docs/services/discovery/connect.html#connectsf)
-  [Microsoft SharePoint Online](/docs/services/discovery/connect.html#connectsp)

Die Verbindung zu einer Datenquelle kann mit den {{site.data.keyword.discoveryshort}}-Tools oder über die API hergestellt werden. Die {{site.data.keyword.discoveryshort}}-Tools bieten eine vereinfachte Verbindungsmethode, die weniger Kenntnisse über die Quellensysteme erfordert, während die API eine differenzierte und extrem konfigurierbare Schnittstelle darstellt, die ein besseres Verständnis der Quelle erfordert, zu der Sie eine Verbindung herstellen. Anhand der folgenden Prozessübersicht können Sie sehen, welche Abschnitte dieses Dokuments Sie als Nächstes lesen sollten:

1.  Lesen Sie sich die [allgemeinen Quellenanforderungen](/docs/services/discovery/connect.html#gen_req) durch, um ein allgemeines Verständnis darüber zu erhalten, was benötigt wird.
2.  Lesen Sie sich die für Ihr Quellensystem spezifischen Anforderungen durch:
    -  [Box](/docs/services/discovery/connect.html#connectbox)
    -  [Salesforce](/docs/services/discovery/connect.html#connectsf)
    -  [Microsoft SharePoint Online](/docs/services/discovery/connect.html#connectsp)
3.  Lesen Sie die Anweisungen für die Quellenkonfiguration auf der Basis Ihrer Konfigurationsauswahl:
    -  [Tools verwenden](/docs/services/discovery/connect.html#source_tooling)
    -  [API verwenden](/docs/services/discovery/connect.html#source_api)

## Allgemeine Quellenanforderungen
{: #gen_req}

Für alle Datenquellen gelten die folgenden allgemeinen Voraussetzungen:

-  Die Größenbegrenzung für einzelne Dokumentdateien für Box, Salesforce und SharePoint Online ist 10 MB.
-  Sie benötigen die Berechtigungsnachweise und Dateiadressen (oder URLs) für jede Datenquelle. Diese werden in der Regel von einem Entwickler/Systemadministrator der Datenquelle bereitgestellt.
-  Sie müssen wissen, welche Ressourcen der Datenquelle durchsucht werden sollen. Diese Information kann vom Quellenadministrator bereitgestellt werden. Bei der Crawlersuche in Box oder Salesforce wird eine Liste der verfügbaren Ressourcen angezeigt, wenn eine Quelle mit den {{site.data.keyword.discoveryshort}}-Tools konfiguriert wird.
-  Die Crawlersuche für eine Datenquelle verwendet Ressourcen (API-Aufrufe) für die Datenquelle. Die Anzahl der Aufrufe hängt von der Anzahl durchsuchter Dokumente ab. Ein entsprechendes Service-Level (z. B. Enterprise) muss für die Datenquelle abgerufen und der Administrator des Quellensystems zu Rate gezogen werden.
-  Die folgenden Dateitypen können von {{site.data.keyword.discoveryshort}} eingepflegt werden; alle anderen Dokumenttypen werden ignoriert:
   -  Microsoft Word
   -  PDF
   -  HTML
   -  JSON
-  Bei Crawlersuchen in {{site.data.keyword.discoveryshort}}-Quellen werden keine Dokumente gelöscht, die in einer Sammlung gespeichert sind. Wenn eine Quelle erneut durchsucht wird, werden neue Dokumente hinzugefügt, das aktualisierte Dokument wird in die aktuelle Version geändert und gelöschte Dokumente bleiben als letzte gespeicherte Version erhalten.

## Box
{: #connectbox}

Wenn Sie eine Verbindung zu einer Box-Quelle herstellen, stellen Sie sicher, dass die Instanz, zu der Sie eine Verbindung herstellen wollen, ein Enterprise-Plan oder höher ist.

So richten Sie ein Box-Konto für die Verwendung mit {{site.data.keyword.discoveryshort}} ein:

1.  Erstellen Sie eine neue angepasste Box-Anwendung unter `https://app.box.com/developers/console` (verwenden Sie die Box-URL Ihres Unternehmens).
1.  Führen Sie anschließend einen der folgenden Schritte aus:
    - Wählen Sie als **Anwendungszugriff** die Option `Enterprise` aus und verwenden Sie anschließend vorhandene verwaltete Benutzer.
      ODER
    - Wählen Sie als **Anwendungszugriff** die Option `Anwendung` aus und erstellen Sie anschließend mithilfe der [Box-API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.box.com/reference#create-app-user){: new_window} einen `Anwendungsbenutzer` mit der neu erstellen Anwendung.
1.  Aktivieren Sie die folgenden **Anwendungsbereiche**:
    - `Alle in Box gespeicherten Ordner lesen und schreiben`
    - `Benutzer verwalten`
1.  Aktivieren Sie die folgenden **erweiterten Features**:
    - `Aktionen als Benutzer ausführen`
    - `Benutzerzugriffstokens generieren`
1.  Lassen Sie den Administrator Ihre Anwendungsclient-ID `https://app.box.com/master/settings/openbox` autorisieren, indem Sie die `Client-ID` von `https://app.box.com/developers/console` in das Feld `API-Schlüssel` eingeben.
1.  Generieren Sie das `öffentliche/private Schlüsselpaar` (wird auf Ihren Computer heruntergeladen).
1.  Öffnen Sie die heruntergeladene Datei und kopieren/fügen Sie die Felder in {{site.data.keyword.discoveryshort}} ein. Entfernen Sie beim Kopieren in {{site.data.keyword.discoveryshort}} den abschließenden Zeilenumbruch `\n` am Ende des privaten Schlüssels (`privateKey`).

**Hinweis:** {{site.data.keyword.discoveryshort}} unterstützt die Crawlersuche für angepasste Anwendungen nicht als sich selbst (Sie können nicht die eigene Identität vortäuschen). 

Die folgenden Berechtigungsnachweise sind erforderlich, um eine Verbindung zu einer Box-Quelle herzustellen; Sie sollten sie bei Ihrem Box-Administrator anfragen (es sei denn, Sie haben sie bereits erhalten, indem Sie mit den vorherigen Schritten eine angepasste Box-Anwendung einrichten):

-  `client_id`: Die `Kunden-ID` der Quelle, zu der diese Berechtigungsnachweise eine Verbindung herstellen.    
-  `enterprise_id`: Die `Unternehmens-ID` der Box-Site, zu der diese Berechtigungsnachweise eine Verbindung herstellen.
-  `client_secret`: Der `geheime Clientschlüssel` der Quelle, zu der diese Berechtigungsnachweise eine Verbindung herstellen. Dieser Wert wird nie zurückgegeben und wird nur verwendet, wenn Berechtigungsnachweise erstellt oder geändert werden.
-  `public_key_id`: Die `ID des öffentlichen Schlüssels` der Quelle, zu der diese Berechtigungsnachweise eine Verbindung herstellen. Dieser Wert wird nie zurückgegeben und wird nur verwendet, wenn Berechtigungsnachweise erstellt oder geändert werden.
-  `private_key`: Der `private Schlüssel` der Quelle, zu der diese Berechtigungsnachweise eine Verbindung herstellen. Dieser Wert wird nie zurückgegeben und wird nur verwendet, wenn Berechtigungsnachweise erstellt oder geändert werden.
-  `passphrase`: Die `Kennphrase` der Quelle, zu der diese Berechtigungsnachweise eine Verbindung herstellen. Dieser Wert wird nie zurückgegeben und wird nur verwendet, wenn Berechtigungsnachweise erstellt oder geändert werden.

Wenn Sie die Berechtigungsnachweise angeben, kann es sinnvoll sein, die [Dokumentation für Box-Entwickler ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.box.com/){: new_window} zu Rate zu ziehen.

Weitere Punkte, die bei der Crawlersuche in Box berücksichtigt werden sollten:

-  Box-Notizen werden im JSON-Format gespeichert. Alle Box-Notizen in den angegebenen Ordnern werden so von {{site.data.keyword.discoveryshort}} eingepflegt.
-  Bei der Verwendung der API benötigen Sie eine Liste der Ordner-IDs und der zugehörigen Eigner-IDs für jeden Ordner, den Sie durchsuchen möchten. Mit den {{site.data.keyword.discoveryshort}}-Tools können Sie Inhalte durchsuchen und auswählen, welche Inhalte durchsucht werden sollen.

## Salesforce
{: #connectsf}

Wenn Sie eine Verbindung zu einer Salesforce-Quelle herstellen, stellen Sie sicher, dass die Instanz, zu der Sie eine Verbindung herstellen wollen, ein Enterprise-Plan oder höher ist.

Die folgenden Berechtigungsnachweise sind erforderlich, um eine Verbindung zu einer Salesforce-Quelle herzustellen. Sie sollten sie bei Ihrem Salesforce-Administrator anfragen:
-  `url`: Die `URL` der Quelle, zu der diese Berechtigungsnachweise eine Verbindung herstellen.
-  `username`: Der `Benutzername` der Quelle, zu der diese Berechtigungsnachweise eine Verbindung herstellen.
-  `password`: Das `Kennwort` setzt sich aus dem Salesforce-Kennwort und einem gültigen Salesforce-Sicherheitstoken zusammen, die verkettet sind. Dieser Wert wird nie zurückgegeben und wird nur verwendet, wenn Berechtigungsnachweise erstellt oder geändert werden.

Wenn Sie die Berechtigungsnachweise angeben, kann es sinnvoll sein, die [Dokumentation für Salesforce-Entwickler ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.salesforce.com/docs/){: new_window} zu Rate zu ziehen.

Weitere Punkte, die bei der Crawlersuche in Salesforce berücksichtigt werden sollten:

-  Wissensartikel werden nur durchsucht, wenn ihre **Version** den Status `published` aufweist und ihre Sprache `en-us` ist.
-  Bei der Verwendung der API benötigen Sie eine Liste der Salesforce-Objekte, die Sie durchsuchen möchten. Mit den {{site.data.keyword.discoveryshort}}-Tools können Sie Inhalte durchsuchen und auswählen, welche Inhalte durchsucht werden sollen.


## SharePoint Online
{: #connectsp}

Wenn Sie eine Verbindung zu einer Microsoft SharePoint Online-Quelle herstellen, stellen Sie sicher, dass die Instanz, zu der Sie eine Verbindung herstellen wollen, ein Enterprise (E1)-Plan oder höher ist.

Die folgenden Berechtigungsnachweise sind erforderlich, um eine Verbindung zu einer SharePoint Online-Quelle herzustellen. Sie sollten sie bei Ihrem SharePoint Online-Administrator anfragen:

-  `organization_url`: Die `Unternehmens-URL` der Quelle, zu der diese Berechtigungsnachweise eine Verbindung herstellen.
-  `site_collection.path`: Der `Pfad für die Siteerfassung` der Quelle, zu der diese Berechtigungsnachweise eine Verbindung herstellen.
-  `username`: Die `Client-ID` der Quelle, zu der diese Berechtigungsnachweise eine Verbindung herstellen.
-  `password`: Das `Kennwort` der Quelle, zu der diese Berechtigungsnachweise eine Verbindung herstellen. Dieser Wert wird nie zurückgegeben und wird nur verwendet, wenn Berechtigungsnachweise erstellt oder geändert werden.

Wenn Sie die Berechtigungsnachweise angeben, kann es sinnvoll sein, die [Dokumentation für Microsoft SharePoint-Entwickler ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.microsoft.com/en-us/sharepoint/dev/){: new_window} zu Rate zu ziehen.

Weitere Punkte, die beim Durchsuchen von Microsoft SharePoint Online zu beachten sind:

-  Beim Durchsuchen von SharePoint benötigen Sie eine Liste der SharePoint-Siteerfassungspfade, die Sie durchsuchen möchten. Mit den {{site.data.keyword.discoveryshort}}-Tools können Sie Inhalte durchsuchen und auswählen, welche Inhalte durchsucht werden sollen. Wenn Sie Ihre gesamte SharePoint Online-Site durchsuchen wollen, wählen Sie in diesem Feld keine Mehrfachpfade (URLs) aus. Geben Sie in diesem Szenario ein `/` im Feld `site_collection.path` ein.

## Tools verwenden
{: #source_tooling}

Mit den {{site.data.keyword.discoveryshort}}-Tools können Sie eine Verbindung zu einer Datenquelle herstellen, indem Sie speziell für Ihre Quelle eine Sammlung erstellen. Führen Sie die folgenden Schritte aus, um eine Quellensammlung zu erstellen und zu durchsuchen:

1.  Wählen Sie auf der Seite **Daten verwalten** der {{site.data.keyword.discoveryshort}}-Tools die Option **Datenquelle verbinden** aus.
2.  Wählen Sie die Datenquelle aus, zu der eine Verbindung hergestellt werden soll.
3.  Geben Sie Ihre Quellenberechtigungsnachweise ein und klicken Sie auf 'Verbinden'. Sie erhalten Ihre Quellenberechtigungsnachweise von Ihrem Quellensystemadministator.
4.  Wählen Sie aus, welche Daten Sie durchsuchen und wie oft Sie die Crawlersuche synchronisieren möchten.
5.  Klicken Sie auf **Speichern & Objekte synchronisieren**, um die Crawlersuche für die Datenquelle zu starten. Sie werden dann an die Anzeige mit dem Sammlungsstatus umgeleitet, die aktualisiert wird, wenn Dokumente der Sammlung hinzugefügt werden.

Die Crawlersuche synchronisiert die Daten zunächst und dann anhand der Häufigkeit, die Sie angegeben haben.
**Hinweis:** Wenn Sie Änderungen in der Anzeige **Synchronisationseinstellung** ändern und dann auf **Objekte speichern und synchronisieren** klicken, wird eine Crawlersuche gestartet (oder erneut gestartet, falls zu diesem Zeitpunkt bereits eine Crawlersuche ausgeführt wird).

## API verwenden
{: #source_api}

Verwenden Sie den folgenden Prozess, um eine Sammlung zu erstellen, die über die API mit einer Datenquelle verbunden ist.
1.  Erstellen Sie Berechtigungsnachweise für die Quelle, zu der Sie eine Verbindung herstellen wollen, indem Sie die [API für Quellenberechtigungsnachweise ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#credentials-api){: new_window} verwenden. Notieren Sie die zurückgegebene Berechtigungsnachweis-ID (**credential_id**) der neu erstellten Berechtigungsnachweise.
2.  Erstellen Sie mit der [Konfigurations-API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#configurations-api){: new_window} eine neue Konfiguration. Diese Konfiguration muss ein Objekt des Typs **source** enthalten, das die Crawlersuche definiert. Das Objekt **source** muss die **credential_id** enthalten, die Sie zuvor notiert haben.
    ```json
    "source" : {
      "type" : "salesforce",
      "credential_id" : "{berechtigungs-id}",
      "schedule" : {
        "enabled" : true,
        "time_zone" : "America/New_York",
        "frequency" : "weekly"
      },
      "options" : {
         "site_collections" : [ {
         "site_collection_path" : "/sites/TestSiteA",
         "limit" : 10
         } ]
      }
    }
    ```
    {: codeblock}
    Notieren Sie die zurückgegebene Konfigurations-ID (**configuration_id**) der neu erstellten Konfiguration.
3.  Erstellen Sie mithilfe der [Sammlungs-API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#configurations-api){: new_window} eine neue Sammlung. Das Objekt, das die Sammlung definiert, muss die **configuration-id** enthalten, die Sie zuvor notiert haben.

Die Crawlersuche für die Quelle beginnt, sobald die Sammlung erstellt wurde, und wird anschließend wieder mit der von Ihnen angegebenen Häufigkeit durchgeführt.
**Hinweis:** Wenn Sie Änderungen im Objekt **source** der Konfiguration ändern, wird zu diesem Zeitpunkt eine neue Crawlersuche gestartet (oder erneut gestartet, falls bereits eine Crawlersuche ausgeführt wird).

## Kunden-ID`` angeben
{:# source_customer_id}

Das Feld `customer_id` in einem eingepflegten {{site.data.keyword.discoveryshort}}-Dokument kann verwendet werden, um Inhalt basierend auf der Kunden-ID (`customer_id`) mithilfe der Methode **user-data** in der API zu löschen. Eingehenden Dokumente aus einer Datenquelle wird beim Einpflegen nicht automatisch eine `customer_id` zugewiesen. Falls für Ihre Anwendung eine `customer_id` definiert sein muss, können Sie eine (oder mehrere) der eingehenden Felder aus dem Quellensystem angeben, die kopiert und als `customer_id` verwendet werden sollen. Dazu müssen Sie die Konfiguration ändern, die für die Herstellung der Verbindung zur Quelle verwendet wird.

1.  Führen Sie eine Beispielabfrage aus und geben Sie an, welches Feld als `customer_id` verwendet werden soll.
2.  Ändern Sie die Konfiguration. Sie müssen einen **Normalization**-Abschnitt hinzufügen, um das Feld `customer_id` zu erstellen.
    -  Navigieren Sie in den Tools zu Ihrer Sammlung und klicken Sie auf den Link **Bearbeiten** im Konfigurationsabschnitt. Klicken Sie anschließend auf die Registerkarte **Normalisierung** und fügen Sie die Normalisierung **copy** hinzu, um das Feld `customer_id` zu erstellen. Klicken Sie dann auf **Anwenden & speichern**.
    ![Copy normalization](images/norm_copy.png)
    -  Wenn Sie die API verwenden, fügen Sie das folgende Objekt zum Array **noramizations** hinzu."
       ```json
       {
         "operation" : "copy",
         "source_field" : "{ursprünglicher_feldname}",
         "destination_field" : "customer_id"
       }
       ```
       {: codeblock}
3.  Bei der nächsten geplanten Crawlersuche wird das Feld `customer_id` zu allen Dokumenten hinzugefügt. Wenn eine Crawlersuche sofort gestartet werden soll, ändern Sie die Quellenkonfiguation (**Synchronisationseinstellungen** in den Tools).

Weitere Informationen sowie Informationen zu Löschvorgängen, die auf der `customer_id` basieren, finden Sie unter [Informationssicherheit ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.bluemix.net/docs/services/discovery/information-security.html){: new_window}.
