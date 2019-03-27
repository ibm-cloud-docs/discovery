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

# Verbindung zu Datenquellen herstellen
{: #sources}

Mit dem {{site.data.keyword.discoveryshort}}-Service können Sie eine Verbindung zu Dokumenten aus fernen Quellen herstellen und diese durchsuchen.
{: shortdesc}

Sie können eine Verbindung zu einer Datenquelle herstellen und Dokumente nach einem Zeitplan (falls gewünscht) in den {{site.data.keyword.discoveryshort}}-Service extrahieren, indem Sie eine Sammlung konfigurieren, die dieser Quelle zugeordnet werden soll. Wenn Sie die {{site.data.keyword.discoveryshort}}-Tools verwenden, kann jede Sammlung mit genau einer Datenquelle konfiguriert werden. Wenn Sie die API verwenden, können Sie Dokumente aus mehreren Datenquellen an eine einzige Sammlung senden. Der {{site.data.keyword.discoveryshort}}-Service extrahiert Dokumente aus der Datenquelle mit einem Prozess, der als Crawlersuche bezeichnet wird. Die Crawlersuche ist der Prozess, mit dem Dokumente systematisch von der angegebenen Startposition aus durchsucht und abgerufen werden. Nur Elemente, die explizit von Ihnen angegeben wurden, werden durch den {{site.data.keyword.discoveryshort}}-Service durchsucht. Die folgenden Typen von Datenquellen können durchsucht werden:

-  [Box](/docs/services/discovery?topic=discovery-sources#connectbox)
-  [Salesforce](/docs/services/discovery?topic=discovery-sources#connectsf)
-  [Microsoft SharePoint Online](/docs/services/discovery?topic=discovery-sources#connectsp)
-  [Microsoft SharePoint 2016 On-Premise](/docs/services/discovery?topic=discovery-sources#connectsp_op)
-  [Web-Crawler-Suche](/docs/services/discovery?topic=discovery-sources#connectwebcrawl) (Betaversion)
-  [IBM Cloud Object Storage](/docs/services/discovery?topic=discovery-sources#connectcos)

Die Verbindung zu einer Datenquelle kann mit den {{site.data.keyword.discoveryshort}}-Tools oder über die API hergestellt werden. Die {{site.data.keyword.discoveryshort}}-Tools bieten eine vereinfachte Verbindungsmethode, die weniger Kenntnisse über die Quellensysteme erfordert, während die API eine differenzierte und extrem konfigurierbare Schnittstelle darstellt, die ein besseres Verständnis der Quelle erfordert, zu der Sie eine Verbindung herstellen. Anhand der folgenden Prozessübersicht können Sie sehen, welche Abschnitte dieses Dokuments Sie als Nächstes lesen sollten:

1.  Lesen Sie sich die [allgemeinen Quellenanforderungen](/docs/services/discovery?topic=discovery-sources#gen_req) durch, um ein allgemeines Verständnis darüber zu erhalten, was benötigt wird.
2.  Lesen Sie sich die für Ihr Quellensystem spezifischen Anforderungen durch:
    -  [Box](/docs/services/discovery?topic=discovery-sources#connectbox)
    -  [Salesforce](/docs/services/discovery?topic=discovery-sources#connectsf)
    -  [Microsoft SharePoint Online](/docs/services/discovery?topic=discovery-sources#connectsp)
    -  [Microsoft SharePoint 2016 On-Premise](/docs/services/discovery?topic=discovery-sources#connectsp_op)
    -  [Web-Crawler-Suche](/docs/services/discovery?topic=discovery-sources#connectwebcrawl) (Betaversion)
    -  [IBM Cloud Object Storage](/docs/services/discovery?topic=discovery-sources#connectcos)
3.  Lesen Sie die Anweisungen für die Quellenkonfiguration auf der Basis Ihrer Konfigurationsauswahl:
    -  [Tools verwenden](/docs/services/discovery?topic=discovery-sources#source_tooling)
    -  [API verwenden](/docs/services/discovery?topic=discovery-sources#source_api)

Wenn Sie eine lokale Datenquelle auswählen, müssen Sie zunächst IBM Secure Gateway installieren und konfigurieren. Weitere Informationen finden Sie unter [IBM Secure Gateway für lokale Daten installieren](/docs/services/discovery?topic=discovery-sources#gateway).

## Allgemeine Quellenanforderungen
{: #gen_req}

Für alle Datenquellen gelten die folgenden allgemeinen Voraussetzungen:

-  Die Größenbegrenzung für einzelne Dokumentdateien für Box, Salesforce, SharePoint Online, SharePoint 2016, IBM Cloud Object Storage und die Web-Crawler-Suche beträgt 10 MB.
-  Sie benötigen die Berechtigungsnachweise und Dateiadressen (oder URLs) für jede Datenquelle. Diese werden in der Regel von einem Entwickler/Systemadministrator der Datenquelle bereitgestellt.
-  Sie müssen wissen, welche Ressourcen der Datenquelle durchsucht werden sollen. Diese Information kann vom Quellenadministrator bereitgestellt werden. Bei der Crawlersuche in Box oder Salesforce wird eine Liste der verfügbaren Ressourcen angezeigt, wenn eine Quelle mit den {{site.data.keyword.discoveryshort}}-Tools konfiguriert wird.
-  Wenn Sie die {{site.data.keyword.discoveryshort}}-Tools verwenden, kann eine Sammlung mit einer einzigen Datenquelle konfiguriert werden. Wenn Sie die API verwenden, können Dokumente aus mehreren Datenquellen an eine einzige Sammlung gesendet werden.
-  Die Crawlersuche für eine Datenquelle verwendet Ressourcen (API-Aufrufe) für die Datenquelle. Die Anzahl der API-Aufrufe ist von der Anzahl der Dokumente abhängig, die durchsucht werden müssen. Es muss eine entsprechende Stufe der Servicelizenz (z. B. Enterprise) für die Datenquelle erworben und der Administrator des Quellensystems zu Rate gezogen werden.
-  Bei Crawlersuchen in {{site.data.keyword.discoveryshort}}-Quellen werden keine Dokumente gelöscht, die in einer Sammlung gespeichert sind. Wenn eine Quelle erneut durchsucht wird, werden neue Dokumente hinzugefügt, das aktualisierte Dokument wird in die aktuelle Version geändert und gelöschte Dokumente bleiben als letzte gespeicherte Version erhalten.
-  Folgende Dateitypen können von {{site.data.keyword.discoveryshort}} eingepflegt werden; alle anderen Dokumenttypen werden ignoriert:

Sammlung | Lite-Pläne | Advanced-Pläne 
---------------- | ------------------------------ | ------------------------------------------- 
Vorhandene Sammlungen, die vor dem Release von [Smart Document Understanding (SDU)](/docs/services/discovery?topic=discovery-release-notes#22jan19) speziell für {{site.data.keyword.discoveryfull}} erstellt wurden | Microsoft Word, PDF, HTML, JSON | Microsoft Word, PDF, HTML, JSON 
Sammlungen, die nach dem Release von [SDU](/docs/services/discovery?topic=discovery-sdu#sdu) erstellt wurden | PDF, Word, PowerPoint, Excel, JSON\*, HTML\* | PDF, Word, PowerPoint, Excel, PNG\*\*, TIFF\*\*, JPG\*\*, JSON\*, HTML\* 
    
\* JSON- und HTML-Dokumente werden von {{site.data.keyword.discoveryfull}} unterstützt, können aber mit dem SDU-Editor nicht bearbeitet werden. Zum Ändern der Konfiguration von HTML- und JSON-Dokumenten benötigen Sie die API. Weitere Informationen finden Sie in der [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/discovery/){: new_window}.

\*\* Einzelne Bilddateien (PNG, TIFF, JPG) werden gescannt und Text, sofern vorhanden, extrahiert. PNG-, TIFF- und JPEG-Bilder, die in PDF-, Word-, PowerPoint- und Excel-Dateien eingebettet sind, werden ebenfalls gescannt und Text, sofern vorhanden, extrahiert.

## Box
{: #connectbox}

Sie müssen eine angepasste Box-Anwendung erstellen, um eine Verbindung zu {{site.data.keyword.discoveryfull}} herstellen zu können. Für die Box-Anwendung, die Sie erstellen, ist Zugriff entweder auf Unternehmensebene oder auf Anwendungsebene erforderlich.

-  Wenn Sie nicht der Box-Administrator für Ihre Organisation sind, wird der Zugriff auf [**Anwendungsebene**](/docs/services/discovery?topic=discovery-sources#applevelbox) empfohlen. Die Anwendung muss von einem Administrator freigegeben werden.
-  Wenn Sie der Box-Administrator für Ihre Organisation sind, wird der Zugriff auf [**Unternehmensebene**](/docs/services/discovery?topic=discovery-sources#entlevelbox) empfohlen.

Die Schritte zum Einrichten des Box-Zugriffs können sich ändern, wenn eine Box-Aktualisierung vorhanden ist. Bezüglich Aktualisierungen ziehen Sie die [Dokumentation für Box-Entwickler ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.box.com/){: new_window} zu Rate.
{: note}

### Zugriff auf Anwendungsebene einrichten
{: #applevelbox}

1.   Navigieren Sie zu `https://app.box.com/developers/console` (verwenden Sie dazu die Box-URL Ihres Unternehmens) und klicken Sie auf **Neue App erstellen**.
1.   Wählen Sie in der Anzeige **Neue App erstellen** die Option **Enterprise Integration** und klicken Sie auf **Weiter**.
1.   Wählen Sie in der Anzeige **Authentifizierungsmethode** die Option **OAuth 2.0 mit JWT (Serverauthentifizierung)** und klicken Sie auf **Weiter**.
1.   Benennen Sie Ihre App und klicken Sie auf die Schaltfläche **App erstellen**. Nachdem Ihre Box-App erstellt wurde, klicken Sie auf **App anzeigen**.
1.   Wenn Ihre App angezeigt wird, wählen Sie als **Anwendung** die Option **Anwendungszugriff**. Sie können weiterhin Ihre vorhandenen verwalteten Benutzer verwenden. Es müssen keine neuen verwalteten Benutzer erstellt werden.
1.   Blättern Sie zum Abschnitt **Anwendungsbereiche** der Seite und aktivieren Sie die folgenden Kontrollkästchen: 
     - `Alle in Box gespeicherten Ordner lesen und schreiben`
     - `Benutzer verwalten`
1.   Blättern Sie abwärts zum Abschnitt **Erweiterte Features** und aktivieren Sie die folgenden Umschaltfunktionen:
     - `Aktionen als Benutzer ausführen`
     - `Benutzerzugriffstokens generieren` 
1.  Klicken Sie auf die Schaltfläche **Änderungen speichern**.

Für die nächsten Schritte ist Unterstützung durch den Administrator für das Box-Konto Ihres Unternehmens erforderlich. Wenn Sie nicht der Box-Administrator Ihrer Organisation sind, können Sie den Administrator ermitteln, indem Sie die Konsole des Box-Entwicklers öffnen und unter **Kontoeinstellungen** > **Kontodetails** > **Einstellungen** nachsehen.

1.  [Administratorschritt] Berechtigen Sie Ihre Anwendungsclient-ID unter `https://app.box.com/master/settings/openbox`, indem Sie auf die Schaltfläche **Neue App berechtigen** klicken.
1.  [Administratorschritt] Geben Sie die **Client-ID** aus `https://app.box.com/developers/console` in das Feld **API-Schlüssel** ein und klicken Sie anschließend auf die Schaltfläche **Berechtigen**.
1.  [Administratorschritt] Rufen Sie ein Entwicklertoken für die Anwendung ab. Navigieren Sie dazu zu `https://app.box.com/developers/console`, blättern Sie bis zum Abschnitt **Entwicklertoken** und generieren Sie Ihr Token.
1.  Nachdem die Anwendung vom Administrator berechtigt wurde, navigieren Sie zu `https://developer.box.com/reference#page-create-an-enterprise-user` und erstellen Sie über die Seite der API-Referenz einen App-Benutzer.

   cURL-Beispiel für die Erstellung eines App-Benutzers:

   ```bash
    curl https://api.box.com/2.0/users -H "Authorization: Bearer ACCESS_TOKEN" -d '{"name": "NedStark", "is_platform_access_only": true}' -X POST
   ```
   {: pre}

1.  Kopieren Sie die neu generierten Inhalte des **id**-Felds und stellen Sie sie dem Benutzer ohne Administratorberechtigung zur Verfügung, der die Box-Anwendung mit {{site.data.keyword.discoveryfull}} verbindet.
1.  Nachdem die App erstellt ist, müssen die zu durchsuchenden Ordner für den App-Benutzer freigegeben werden, der für diese Ordner `anzeigeberechtigt` sein muss. Dazu ist der Anmeldename des App-Benutzers aus der obigen cURL-Befehlsantwort erforderlich. Beispiel: `"login":"AppUser_737729_jmUo@boxdevedition.com"`.
1.  Kehren Sie zur Box-Entwicklerkonsole `https://app.box.com/developers/console` zurück und blättern Sie zum Abschnitt **Öffentliche Schlüssel hinzufügen und verwalten**. Klicken Sie auf das Symbol **public/private keypair generieren** und laden Sie die Schlüsselpaardatei herunter. Öffnen Sie die Datei.
1.  Schneiden Sie aus der Schlüsselpaardatei die folgenden Felder aus und fügen Sie sie in die {{site.data.keyword.discoveryshort}}-Tools ein.
    -  `client_id`
    -  `enterprise_id`
    -  `client_secret` 
    -  `public_key_id` 
    -  `private_key` 
    -  `passphrase` 

### Zugriff auf Unternehmensebene einrichten
{: #entlevelbox}

1.  Navigieren Sie zu `https://app.box.com/developers/console` (verwenden Sie dazu die Box-URL Ihres Unternehmens) und klicken Sie auf **Neue App erstellen**.
1.  Wählen Sie in der Anzeige **Neue App erstellen** die Option **Enterprise Integration** und klicken Sie auf **Weiter**.
1.  Wählen Sie in der Anzeige **Authentifizierungsmethode** die Option **OAuth 2.0 mit JWT (Serverauthentifizierung)** und klicken Sie auf **Weiter**.
1.  Benennen Sie Ihre App und klicken Sie auf die Schaltfläche **App erstellen**. Nachdem Ihre Box-App erstellt wurde, klicken Sie auf **App anzeigen**.
1.  Wenn Ihre App angezeigt wird, wählen Sie als **Anwendungszugriff** die Option **Unternehmen** aus. Sie können weiterhin Ihre vorhandenen verwalteten Benutzer verwenden. Es müssen keine neuen verwalteten Benutzer erstellt werden.
1.  Blättern Sie zum Abschnitt **Anwendungsbereiche** der Seite und aktivieren Sie die folgenden Kontrollkästchen: 
    - `Alle in Box gespeicherten Ordner lesen und schreiben`
    - `Benutzer verwalten`
    - `Unternehmenseigenschaften verwalten`
1.  Blättern Sie abwärts zum Abschnitt **Erweiterte Features** und aktivieren Sie die folgenden Umschaltfunktionen:
    - `Aktionen als Benutzer ausführen`
    - `Benutzerzugriffstokens generieren` 
1.  Klicken Sie auf die Schaltfläche **Änderungen speichern**.

Die Option `Aktualisieren` wird nur bei Zugriff auf Unternehmensebene unterstützt.
{: note}

Wenn Sie Ihre Box-App-Einstellungen ändern, `autorisieren Sie Ihre App erneut`, damit die Änderungen wirksam werden.
{: tip}

Für die nächsten Schritte ist Unterstützung durch den Administrator für das Box-Konto Ihres Unternehmens erforderlich. Wenn Sie nicht der Box-Administrator Ihrer Organisation sind, können Sie den Administrator ermitteln, indem Sie die Konsole des Box-Entwicklers öffnen und unter **Kontoeinstellungen** > **Kontodetails** > **Einstellungen** nachsehen.

1.  [Administratorschritt] Berechtigen Sie Ihre Anwendungsclient-ID, indem Sie zu **Administratorkonsole** > **Unternehmenseinstellungen** > **Apps** navigieren und dann zu `Angepasste Anwendungen` blättern. Beispiel-URL: `https://app.box.com/master/settings/openbox`.
1.  [Administratorschritt] Geben Sie die **Client-ID** aus `https://app.box.com/developers/console` in das Feld **API-Schlüssel** ein und klicken Sie anschließend auf die Schaltfläche **Berechtigen**.
1.  Kehren Sie zur Box-Entwicklerkonsole `https://app.box.com/developers/console` zurück und blättern Sie zum Abschnitt **Öffentliche Schlüssel hinzufügen und verwalten**. Klicken Sie auf das Symbol **public/private keypair generieren** und laden Sie die Schlüsselpaardatei herunter. Öffnen Sie die Datei.
1.  Schneiden Sie aus der Schlüsselpaardatei die folgenden Felder aus und fügen Sie sie in die {{site.data.keyword.discoveryshort}}-Tools ein.
    -  `client_id`
    -  `enterprise_id`
    -  `client_secret` 
    -  `public_key_id` 
    -  `private_key` 
    -  `passphrase` 

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
-  `site_collection_path` - Der `Siteerfassungspfad` der Quelle, mit der diese Berechtigungsnachweise verbunden werden.
-  `username`: Die `Client-ID` der Quelle, zu der diese Berechtigungsnachweise eine Verbindung herstellen. Dieser Benutzer muss Zugriff auf alle Sites und Listen haben, die durchsucht und indexiert werden müssen.
-  `password`: Das `Kennwort` der Quelle, zu der diese Berechtigungsnachweise eine Verbindung herstellen. Dieser Wert wird nie zurückgegeben und wird nur verwendet, wenn Berechtigungsnachweise erstellt oder geändert werden.

Wenn Sie die Berechtigungsnachweise angeben, kann es sinnvoll sein, die [Dokumentation für Microsoft SharePoint-Entwickler ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.microsoft.com/en-us/sharepoint/dev/){: new_window} zu Rate zu ziehen.

Weitere Punkte, die beim Durchsuchen von Microsoft SharePoint Online zu beachten sind:

-  Zum Durchsuchen von SharePoint muss das Konto `Benutzer der Crawlersuche` über die Berechtigung `SiteCollection-Administrator` verfügen.
-  Zum Durchsuchen von SharePoint benötigen Sie eine Liste der SharePoint-Siteerfassungspfade, die Sie durchsuchen möchten. {{site.data.keyword.discoveryshort}} unterstützt keine Ordnerpfade als Eingabe.

## Web-Crawler-Suche
{: #connectwebcrawl}

Diese Beta-Funktionalität kann verwendet werden, um öffentliche Websites zu durchsuchen, für die kein Kennwort erforderlich ist. Sie können auswählen, wie oft {{site.data.keyword.discoveryshort}} mit den Websites, der Sprache und der Anzahl von Hops synchronisiert werden soll.

-  `Eigene Daten synchronisieren`: Sie können eine Synchronisation alle 5 Minuten, stündlich, täglich, wöchentlich oder monatlich auswählen. 
-  `Sprache auswählen`: Sie können die Sprache der Websites aus der Liste der unterstützten Sprachen auswählen. Eine Liste der von {{site.data.keyword.discoveryshort}} unterstützten Sprachen finden Sie unter [Sprachunterstützung](/docs/services/discovery?topic=discovery-language-support#supported-languages). Es wird empfohlen, für jede Sprache eine separate Sammlung zu erstellen.
-  `Zu synchronisierende URL-Gruppe`: Geben Sie Ihre URL ein und klicken Sie auf das Pluszeichen, um sie zur URL-Gruppe hinzuzufügen. Um die **Crawlereinstellungen** für die URL-Gruppe anzugeben, klicken Sie auf das Symbol ![Cog](images/icon_settings.png). Sie können den Wert für **Maximale Anzahl Hops** festlegen. Dies ist die Anzahl der aufeinanderfolgenden Links, denen ab der Start-URL gefolgt werden soll (die Start-URL ist `0`). Die Standardanzahl an Hops ist `2`, das Maximum `20` (wenn die API verwendet wird, beträgt das Maximum `1000`). 

Für diese Betaversion ist die Anzahl der durchsuchten Webseiten begrenzt, weshalb der Web-Crawler möglicherweise nicht alle angegebenen Webseiten durchsucht und die maximale Anzahl für Hops nicht erreicht.
{: note}

Wenn Sie für andere URLs unterschiedliche **Crawlereinstellungen** benötigen, klicken Sie auf **URL-Gruppe hinzufügen** und erstellen Sie eine neue Gruppe. Sie können so viele URL-Gruppen erstellen wie benötigt.
{: tip}

## SharePoint 2016 On-Premise
{: #connectsp_op}

Microsoft SharePoint 2016 (auch als SharePoint Server 2016 bezeichnet) ist eine lokale Datenquelle. Für eine Verbindung zu dieser Datenquelle müssen Sie zunächst IBM Secure Gateway installieren und konfigurieren. Weitere Informationen finden Sie unter [IBM Secure Gateway für lokale Daten installieren](/docs/services/discovery?topic=discovery-sources#gateway).{: note}

Die folgenden Berechtigungsnachweise sind erforderlich, um eine Verbindung zu einer SharePoint 2016-Quelle herzustellen. Sie sollten sie bei Ihrem SharePoint Online-Administrator anfragen:

-  `username`: Die `Client-ID` der Quelle, zu der diese Berechtigungsnachweise eine Verbindung herstellen. Dieser Benutzer muss Zugriff auf alle Sites und Listen haben, die durchsucht und indexiert werden müssen.
-  `password`: Das `Kennwort` der Quelle, zu der diese Berechtigungsnachweise eine Verbindung herstellen. Dieser Wert wird nie zurückgegeben und wird nur verwendet, wenn Berechtigungsnachweise erstellt oder geändert werden.
-  `web_application_url`: Die `Webanwendungs-URL` von SharePoint 2016, z. B. https://sharepointwebapp.com:8443. Wird der Port nicht angegeben, wird standardmäßig Port `80` für HTTP und Port `443` für HTTPS verwendet.
-  `domain`: Die `Domäne` des SharePoint 2016-Kontos.

Wenn Sie die Berechtigungsnachweise angeben, kann es sinnvoll sein, die [Dokumentation für Microsoft SharePoint-Entwickler ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.microsoft.com/en-us/sharepoint/dev/){: new_window} zu Rate zu ziehen.

Weitere Punkte, die beim Durchsuchen von Microsoft SharePoint 2016 zu beachten sind:

-  Zum Durchsuchen von SharePoint 2016 muss das Konto `Benutzer der Crawlersuche` über die Berechtigung `SiteCollection-Administrator` verfügen.
-  Zum Durchsuchen von SharePoint benötigen Sie eine Liste der SharePoint-Siteerfassungspfade, die Sie durchsuchen möchten. {{site.data.keyword.discoveryshort}} unterstützt keine Ordnerpfade als Eingabe.

## IBM Cloud Object Storage
{: #connectcos}

Wenn eine Verbindung zu einer IBM Cloud Object Storage-Quelle hergestellt wird, sind die folgenden Berechtigungsnachweise erforderlich. Sie sollten von Ihrem IBM Cloud Object Storage-Administrator angefordert werden:

-  `endpoint`: Der `Endpunkt` für die Interaktion mit IBM Cloud Object Storage-Daten.
-  `access_key_id`: Die `Zugangsschlüssel-ID`, die bei der Erstellung der IBM Cloud Object Storage-Instanz erhalten wurde.
-  `secret_access_key`: Der `geheime Zugangsschlüssel` für die Unterzeichnung von Anforderungen, der bei der Erstellung der IBM Cloud Object Storage-Instanz erhalten wurde.

Nachdem diese Informationen eingegeben wurden, können Sie auswählen, wie oft Ihre Daten synchronisiert werden sollen, und die Buckets auswählen, mit denen synchronisiert werden soll.

Weitere Punkte, die beim Durchsuchen von IBM Cloud Object Storage zu beachten sind:

-  Dieser Connector bietet keine Unterstützung für die Crawlersuche durch private Endpunkte.
-  Wenn alle Buckets ausgewählt sind, ist die Leistung geringfügig beeinträchtigt. In diesem Fall kann die Indexierung der Dokumente längere Zeit in Anspruch nehmen.

## Tools verwenden
{: #source_tooling}

Mit den {{site.data.keyword.discoveryshort}}-Tools können Sie eine Verbindung zu einer Datenquelle herstellen, indem Sie speziell für Ihre Quelle eine Sammlung erstellen. Führen Sie die folgenden Schritte aus, um eine Quellensammlung zu erstellen und zu durchsuchen:

1.  Wählen Sie auf der Seite **Daten verwalten** der {{site.data.keyword.discoveryshort}}-Tools die Option **Datenquelle verbinden** aus.
2.  Wählen Sie die Datenquelle aus, zu der eine Verbindung hergestellt werden soll. Wenn Sie eine lokale Datenquelle ausgewählt haben, müssen Sie zunächst IBM Secure Gateway installieren; siehe dazu [IBM Secure Gateway für lokale Daten installieren](/docs/services/discovery?topic=discovery-sources#gateway). 
3.  Geben Sie Ihre Quellenberechtigungsnachweise ein und klicken Sie auf 'Verbinden'. Sie erhalten Ihre Quellenberechtigungsnachweise von Ihrem Quellensystemadministator.
4.  Wählen Sie aus, welche Daten Sie durchsuchen und wie oft Sie die Crawlersuche synchronisieren möchten. Synchronisationsoptionen:
    -  Alle fünf Minuten: Ausführung alle fünf Minuten.
    -  Stündlich: Ausführung einmal pro Stunde.
    -  Täglich: Ausführung täglich zwischen 00:00 und 06:00 Uhr in der angegebenen Zeitzone.
    -  Wöchentlich: Ausführung jeden Sonntag zwischen 00:00 und 06:00 Uhr in der angegebenen Zeitzone.
    -  Monatlich: Ausführung an jedem ersten Sonntag im Monat zwischen 00:00 und 06:00 Uhr in der angegebenen Zeitzone.
    
    Beispiel für einen Crawlerstatus:
    
    ```json
    "crawl_status" : {
    "source_crawl" : {
      "status" : "completed",
      "next_crawl" : "2019-02-10T05:00:00-05:00"
    }
    ```
5.  Klicken Sie auf **Speichern & Objekte synchronisieren**, um die Crawlersuche für die Datenquelle zu starten. Sie werden dann an die Anzeige mit dem Sammlungsstatus umgeleitet, die aktualisiert wird, wenn Dokumente der Sammlung hinzugefügt werden.

Die Crawlersuche synchronisiert die Daten zunächst und dann anhand der Häufigkeit, die Sie angegeben haben.
**Hinweis:** Wenn Sie Änderungen in der Anzeige **Synchronisationseinstellung** ändern und dann auf **Objekte speichern und synchronisieren** klicken, wird eine Crawlersuche gestartet (oder erneut gestartet, falls zu diesem Zeitpunkt bereits eine Crawlersuche ausgeführt wird).

## API verwenden
{: #source_api}

Verwenden Sie den folgenden Prozess, um eine Sammlung zu erstellen, die über die API mit einer Datenquelle verbunden ist.

Wenn Sie vorhaben, eine lokale Datenquelle anzubinden, müssen Sie zunächst IBM Secure Gateway installieren; siehe dazu [IBM Secure Gateway für lokale Daten installieren](/docs/services/discovery?topic=discovery-sources#gateway). 

Im folgenden Beispiel wird die SharePoint-Datenquelle verwendet.

1.  Erstellen Sie Berechtigungsnachweise für die Quelle, zu der Sie eine Verbindung herstellen wollen, indem Sie die [API für Quellenberechtigungsnachweise ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/discovery#create-credentials){: new_window} verwenden. Notieren Sie die zurückgegebene Berechtigungsnachweis-ID (**credential_id**) der neu erstellten Berechtigungsnachweise.
2.  Erstellen Sie mit der [Konfigurations-API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/discovery#add-configuration){: new_window} eine neue Konfiguration. Diese Konfiguration muss ein Objekt des Typs **source** enthalten, das die Crawlersuche definiert. Das Objekt **source** muss die **credential_id** enthalten, die Sie zuvor notiert haben.
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
3.  Erstellen Sie mithilfe der [Sammlungs-API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/discovery#create-a-collection){: new_window} eine neue Sammlung. Das Objekt, das die Sammlung definiert, muss die **configuration-id** enthalten, die Sie zuvor vermerkt haben.

Die Crawlersuche für die Quelle beginnt, sobald die Sammlung erstellt wurde, und wird anschließend wieder mit der von Ihnen angegebenen Häufigkeit durchgeführt.
**Hinweis:** Wenn Sie Änderungen im Objekt **source** der Konfiguration ändern, wird zu diesem Zeitpunkt eine neue Crawlersuche gestartet (oder erneut gestartet, falls bereits eine Crawlersuche ausgeführt wird).

### Kunden-ID`` angeben
{: #source_customer_id}

Das Feld `customer_id` in einem eingepflegten {{site.data.keyword.discoveryshort}}-Dokument kann verwendet werden, um Inhalt basierend auf der Kunden-ID (`customer_id`) mithilfe der Methode **user-data** in der API zu löschen. Eingehenden Dokumente aus einer Datenquelle wird beim Einpflegen nicht automatisch eine `customer_id` zugewiesen. Falls für Ihre Anwendung eine `customer_id` definiert sein muss, können Sie eine (oder mehrere) der eingehenden Felder aus dem Quellensystem angeben, die kopiert und als `customer_id` verwendet werden sollen. Dazu müssen Sie die Konfiguration ändern, die für die Herstellung der Verbindung zur Quelle verwendet wird.

1.  Führen Sie eine Beispielabfrage aus und geben Sie an, welches Feld als `customer_id` verwendet werden soll.
2.  Ändern Sie die Konfiguration. Sie müssen einen **Normalization**-Abschnitt hinzufügen, um das Feld `customer_id` zu erstellen.
    -  Navigieren Sie in den Tools zu Ihrer Sammlung und klicken Sie auf den Link **Bearbeiten** im Konfigurationsabschnitt. Klicken Sie anschließend auf die Registerkarte **Normalisierung** und fügen Sie die Normalisierung **copy** hinzu, um das Feld `customer_id` zu erstellen. Klicken Sie dann auf **Anwenden & speichern**.
    ![Copy normalization](images/norm_copy.png)
    -  Wenn Sie die API verwenden, fügen Sie das folgende Objekt zum Array **normalizations** hinzu:
       ```json
       {
         "operation" : "copy",
         "source_field" : "{ursprünglicher_feldname}",
         "destination_field" : "customer_id"
       }
       ```
       {: codeblock}
3.  Bei der nächsten geplanten Crawlersuche wird das Feld `customer_id` zu allen Dokumenten hinzugefügt. Wenn eine Crawlersuche sofort gestartet werden soll, ändern Sie die Quellenkonfiguration (**Synchronisationseinstellungen** in den Tools).

Weitere Informationen, auch zum Löschen auf Basis der `customer_id`, finden Sie im Abschnitt [Informationssicherheit](/docs/services/discovery?topic=discovery-information-security#information-security).

## IBM Secure Gateway für lokale Daten installieren 
{: #gateway}

Für die Verbindung mit einer lokalen Datenquelle müssen Sie zunächst IBM Secure Gateway herunterladen, installieren und konfigurieren. Nachdem Sie IBM Secure Gateway für Ihre erste lokale Datenquelle installiert haben, müssen Sie diesen Prozess nicht wiederholen.

1.  Wählen Sie auf der Seite **Daten verwalten** der {{site.data.keyword.discoveryshort}}-Tools die Option **Datenquelle verbinden** aus.
1.  Wählen Sie die Datenquelle aus, zu der eine Verbindung hergestellt werden soll. Wenn Sie eine lokale Datenquelle auswählen, rufen Sie den Abschnitt **Verbindung zum lokalen Netz herstellen** auf und klicken Sie auf die Schaltfläche **Verbindung herstellen**.
1.  Laden Sie über die Anzeige **Secure Gateway Client herunterladen und installieren** die entsprechende Version von IBM Secure Gateway herunter.
1.  Nach dem Abschluss des Downloads klicken Sie auf die Schaltfläche **Secure Gateway herunterladen und fortfahren**. Während der Installation benötigen Sie auf Aufforderung von Secure Gateway Client die **Gateway-ID** und das **Token**. Beides ist in der Anzeige angegeben. Installationsanweisungen finden Sie unter [Client installieren![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/docs/services/SecureGateway/securegateway_install.html#installing-the-client){: new_window} in der Dokumentation zu Secure Gateway.
1.  Öffnen Sie auf der Maschine, auf der Secure Gateway Client ausgeführt wird, das Secure Gateway-Dashboard unter http://localhost: 9003.
1.  Klicken Sie im Dashboard auf **ACL hinzufügen**. Fügen Sie der Liste **Zugriff zulassen** die Endpunkt-URL der einzelnen SharePoint-Sammlungen hinzu. Zum Beispiel den Hostnamen `mycompany.sharepoint.com` und den Port `80`.
1.  Kehren Sie zu den {{site.data.keyword.discoveryshort}}-Tools zurück und klicken Sie auf **Weiter**. Wenn die Verbindung erfolgreich ist, wird die Nachricht `Verbindung erfolgreich` angezeigt. Wenn die Verbindung nicht erfolgreich war, öffnen Sie das Secure Gateway-Dashboard und vergewissern Sie sich, dass die Endpunkte in der Liste **Zugriff zulassen** korrekt sind.

Nachdem die Verbindung erfolgreich hergestellt wurde, können Sie mit der Eingabe der Berechtigungsnachweise für Ihre lokale Datenquelle beginnen.

## Datenquellenverbindung und Datenisolation
{: #source_isolation}

Die Option [Verbindung zu externen Datenquellen herstellen](/docs/services/discovery?topic=discovery-sources#sources) reduziert die Datenisolation Ihrer Serviceinstanz, da die Daten im Transit zwischen der Quelle und dem Service nicht isoliert werden können. Die gesamte andere Isolation (ruhend, Administration, Abfrage) bleibt vollständig erhalten. Die gesamte Inflight-Kommunikation zwischen und innerhalb der Services und Datenquellen wird mit TLS V1.2 verschlüsselt. Die privaten Schlüssel für die TLS-Zertifikate werden ruhend mittels AES-256-GCM verschlüsselt, die Servicezertifikate laufen nach jeweils drei Jahren ab und die Zertifikatswiderrufslisten werden monatlich aktualisiert. Alle Berechtigungsnachweise werden mittels TLS V1.2 über eine verschlüsselte Verbindung gesendet und ruhend mittels AES-256 verschlüsselt. Verbindungen zu diesen Datenquellen verwenden die jeweiligen von diesen Datenquellen unterstützten Sicherheitsprotokolle.
