---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-08"

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

# Aus AlchemyData News migrieren
{: #migrate-adn}

Eine neue Version von {{site.data.keyword.discoverynewsfull}} ist seit dem **31. Juli 2017** verfügbar. Eine Beschreibung dieser Sammlung finden Sie unter [Watson Discovery News](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news).

AlchemyData News wurde mit dem Servicedatum **7. März 2018** zurückgezogen.

## Servicevergleich
{: #service-adn}

Bei einem Umstieg von AlchemyData News auf {{site.data.keyword.discoverynewsshort}} im {{site.data.keyword.discoveryshort}}-Service sind die folgenden Unterschiede zu beachten.

- {{site.data.keyword.discoveryshort}} berechnet neue Abfragen nur nach der Abfrage. Bei jedem Ergebnis sind alle Felder ohne gesonderte Berechnung für die Rückgabe verfügbar.
- Jede {{site.data.keyword.discoveryshort}}-Abfrage kann maximal 50 Ergebnisse zurückgeben. Mit dem Parameter `offset` können Sie Abfragen für jede gewünschte Anzahl von Ergebnissen definieren.
- {{site.data.keyword.discoveryshort}} unterstützt zusätzlich Aggregationen. Weitere Informationen enthält der Abschnitt [Aggregationen](/docs/services/discovery?topic=discovery-query-reference#aggregations) in der {{site.data.keyword.discoveryshort}}-Dokumentation.
- {{site.data.keyword.discoverynewsfull}} nimmt die Einstufung nicht wie AlchemyData News vor. Gegenwärtig gibt es kein Feld für die Einstufung.
- Die Abfragestruktur und die Struktur der zurückgegebenen Daten sind bei {{site.data.keyword.discoverynewsshort}} und AlchemyData News unterschiedlich. Ein gutes Verfahren, sich über die JSON-Struktur zu informieren, besteht im Abfragen und Untersuchen eines einzelnen Ergebnisses in {{site.data.keyword.discoverynewsshort}}.
- XML-Ausgabe wird von {{site.data.keyword.discoverynewsshort}} nicht unterstützt.
- Die Deduplizierung ist in {{site.data.keyword.discoverynewsshort}} als Betaversionsfeature verfügbar.

## Unterschiede bei der Authentifizierung
{: #auth-adn}

Der {{site.data.keyword.discoveryshort}}-Service verwendet die {{site.data.keyword.Bluemix_notm}}-Standardberechtigungsnachweise für `Benutzername` und `Kennwort`, um auf Abfragen zuzugreifen. Dies ersetzt das bestehende, von AlchemyData News verwendete Verfahren mit API-Schlüsseln. Alle {{site.data.keyword.discoveryshort}}-Abfragen müssen mit einer durch die {{site.data.keyword.discoveryshort}}-Serviceinstanz erstellten Kombination aus Benutzername und Kennwort ausgeführt werden.

Ihre Serviceberechtigungsnachweise können Sie verwalten, indem Sie die Registerkarte **Serviceberechtigungsnachweise** Ihres Service in {{site.data.keyword.Bluemix_notm}} anzeigen.

## Discovery-Instanz konfigurieren
{: #config-adn}

Eine {{site.data.keyword.discoveryshort}}-Serviceinstanz wird auf dieselbe Weise wie die AlchemyData News-Instanz erstellt.

1. Navigieren Sie zu [{{site.data.keyword.Bluemix_notm}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/catalog/services/discovery){: new_window}, melden Sie sich an und wählen Sie {{site.data.keyword.discoveryshort}} im Servicekatalog aus.
1. Wählen Sie den entsprechenden Plan für Ihren Bedarf aus und klicken Sie auf **Erstellen**.

  Der {{site.data.keyword.discoveryshort}}-Service bietet einen Lite-Plan mit 1000 verfügbaren Abfragen für Nachrichten pro Monat. Mit einer Instanz dieses Plans können Sie funktional entsprechende Abfragen ermitteln, ohne dass dafür Kosten anfallen.
  {: tip}

1. Klicken Sie auf die Registerkarte **Serviceberechtigungsnachweise** und wählen Sie **Berechtigungsnachweise anzeigen** aus, um die `URL`, den `Benutzernamen` und das `Kennwort` für diese Instanz zu ermitteln.

## Watson Discovery News abfragen
{: #querying-adn}

Sie können {{site.data.keyword.discoverynewsfull}} mithilfe der API oder mit einem der {{site.data.keyword.watson}}-SDKs abfragen. Außerdem können Sie mit den Abfrageerstellungstools Abfragen interaktiv erstellen.

So können Sie die {{site.data.keyword.discoveryshort}}-Tools starten und {{site.data.keyword.discoverynewsshort}} abfragen:

1. Klicken Sie unter **Services** für {{site.data.keyword.discoveryshort}} auf **Tool starten**.
1. Klicken Sie auf die Kachel '{{site.data.keyword.discoverynewsshort}}', um die Anzeige **Daten verwalten** zu öffnen.
1. Klicken Sie auf **Datenschema anzeigen** und dann auf **Abfragen erstellen**, um den Abfragebuilder zu öffnen.

  Abfragen in {{site.data.keyword.discoverynewsfull}} sind genauso strukturiert wie Abfragen, die für private Datensammlungen geschrieben sind. Weitere Informationen finden Sie unter [Abfragekonzepte](/docs/services/discovery?topic=discovery-query-concepts#query-concepts) und [Abfragereferenz](/docs/services/discovery?topic=discovery-query-reference#query-reference).
  {: tip}

Erwarten Sie nicht, dass für ähnliche Abfragen in AlchemyData News und {{site.data.keyword.discoverynewsfull}} identische Ergebnisse zurückgegeben werden. Die Kombination aus Zeitpunkt der Crawlersuche, Quellen und Aufbereitungen führt jeweils zu unterschiedlichen Ergebnissen.
{: note}

## Watson Discovery News-Abfragen zur Anwendung hinzufügen
{: #queries-adn}

Verwenden Sie eines der folgenden Verfahren, um Abfragen zu Ihrer Anwendung hinzuzufügen. Alle Beispiele fragen `enriched_text.entities` mit dem Wert `IBM` für `text` (`enriched_text.entities.text:IBM`) ab.

Ersetzen Sie in allen Beispielen `{benutzername}` und `{kennwort}` durch den Benutzernamen und das Kennwort, die auf der Seite **Serviceberechtigungsnachweise** für Ihre Serviceinstanz aufgeführt sind.

### Direkte Aufrufe der API verwenden
{: #api-adn}

```bash
curl -u "{benutzername}":"{kennwort}"  'https://gateway.watsonplatform.net/discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

### Java-SDK verwenden
{: #javasdk-adn}

```java
Discovery discovery = new Discovery("2017-11-07");
discovery.setEndPoint("https://gateway.watsonplatform.net/discovery/api/v1");
discovery.setUsernameAndPassword("{benutzername}", "{kennwort}");
String environmentId = "system";
  String collectionId = "news";

QueryRequest.Builder queryBuilder = new QueryRequest.Builder(environmentId,collectionId);  
queryBuilder.query("enriched_text.entities.text:IBM");  
QueryResponse queryResponse =  
discovery.query(queryBuilder.build()).execute();
```
{: codeblock}

### Watson-Node.js-SDK verwenden
{: #nodesdk-adn}

```javascript
var watson = require('watson-developer-cloud');

var discovery = new DiscoveryV1({  
  username: '{benutzername}',
  password: '{kennwort}',
  version_date: '2017-11-07'
});  

discovery.query(('system', 'news', 'enriched_text.entities.text:IBM'),  
  function(error, data) {  
  console.log(JSON.stringify(data, null, 2));  
```
{: codeblock}

### Watson-Python-SDK verwenden
{: #pythonsdk-adn}

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

qopts = {'query': 'enriched_text.entities.text:IBM'}
my_query = discovery.query('{umgebungs-id}', '{sammlungs-id}', qopts)
print(json.dumps(my_query, indent=2))
```
{: codeblock}
