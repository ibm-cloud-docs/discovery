---

copyright:
  years: 2015, 2018
lastupdated: "2018-01-16"

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

# Von Watson Discovery News Original migrieren

Eine neue Version von {{site.data.keyword.discoverynewsshort}} ist seit dem **31. Juli 2017** verfügbar. Die ursprüngliche Version wurde in {{site.data.keyword.discoverynewsshort}} Original umbenannt und wurde mit dem Servicedatum **15. Januar 2018** zurückgezogen. Wenn Sie versuchen, auf {{site.data.keyword.discoverynewsshort}} Original zuzugreifen, erhalten Sie die Nachricht `410 GONE`.
{: shortdesc}

Zur Migration von {{site.data.keyword.discoverynewsshort}} Original auf die neue Version müssen Sie einige Änderungen vornehmen, zu denen auch die Aktualisierung aller Abfragen gehört, die für {{site.data.keyword.discoverynewsshort}} Original erstellt wurden.

  **Hinweis:** {{site.data.keyword.discoverynewsshort}} Original war nur in Instanzen von {{site.data.keyword.discoveryshort}} verfügbar, die vor dem **31. Juli 2017** erstellt wurden und mit dem Servicedatum **15. Januar 2018** zurückgezogen wurden.

Eine Beschreibung dieser Sammlung finden Sie unter [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html).

Eine Beschreibung sowie Informationen zur Abfrage von {{site.data.keyword.discoverynewsshort}} Original enthält der Abschnitt [Watson Discovery News Original](/docs/services/discovery/discovery-auxiliary.html#watson-discovery-news-original).

## Servicevergleich

| {{site.data.keyword.discoverynewsshort}} Original         | {{site.data.keyword.discoverynewsshort}}           |
|----------------------------------------|---------------------------------|
| **{{site.data.keyword.discoverynewsshort}} Original** wurde vorab mit den folgenden Alchemy Language-Aufbereitungen aufbereitet: Schlüsselwortextraktion, Entitätsextraktion, Konzepttagging, Beziehungsextraktion, Stimmungsanalyse und Taxonomieklassifizierung. Auch die folgenden zusätzlichen Metadaten wurden hinzugefügt: Suchlaufdatum, Veröffentlichungsdatum, URL-Einstufung, Hosteinstufung und Ankertext. | **{{site.data.keyword.discoverynewsshort}}** ist vorab mit den folgenden Aufbereitungen von {{site.data.keyword.nlushort}} (NLU) aufbereitet: Schlüsselwortextraktion, Entitätsextraktion, Semantikrollenextraktion, Stimmungsanalyse, Beziehungen und Kategorieklassifizierung. Auch die folgenden zusätzlichen Metadaten werden hinzugefügt: Suchlaufdatum und Veröffentlichungsdatum. Weitere Informationen zu NLU-Aufbereitungen finden Sie unter [Aufbereitungen hinzufügen](/docs/services/discovery/building.html#adding-enrichments).                         |
| **{{site.data.keyword.discoverynewsshort}} Original** war über eine Umgebung zugänglich, die für die Serviceinstanz eindeutig war.                       | Bei Verwendung von **{{site.data.keyword.discoverynewsshort}}** fragen alle Benutzer dieselbe Umgebung und Sammlung ab. Dies bedeutet, dass alle Verweise auf Ihre Umgebung und Sammlung geändert werden müssen.      |
| In ** {{site.data.keyword.discoverynewsshort}} Original** wurden Informationen wie Sammlungsgröße, Anzahl der Dokumente usw. beim Abrufen der Umgebung über die API empfangen.  | **Die {{site.data.keyword.discoverynewsshort}}**-API gibt diese Informationen nicht zurück.                          |

In **{{site.data.keyword.discoverynewsshort}}** sind die folgenden Felder verfügbar:

`enriched_text.relations.arguments.text`  
`enriched_text.relations.score`  
`enriched_text.relations.sentence`  
`enriched_text.relations.type`  
`enriched_title.relations`  
`enriched_title.relations.arguments`  
`enriched_title.relations.arguments.entities`<br/>
`enriched_title.relations.arguments.entities.text`  
`enriched_title.relations.arguments.entities.type`  
`enriched_title.relations.arguments.text`  
`enriched_title.relations.score`  
`enriched_title.relations.sentence`  
`enriched_title.relations.type`  
`external_links`  
`extracted_metadata`  
`extracted_metadata.file_type`  
`extracted_metadata.filename`  
`extracted_metadata.sha1`  
`forum_title`  
`main_image_url`

Viele Felder wurden auch entfernt, z. B. `blekko.hostrank`, `duplicate_url`, `domain` und weitere. Eine vollständige Liste finden Sie <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/News_migration_v_1.01.xlsx" download>hier <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link" class="style-scope doc-content"></a>.

## Abfragen auf Watson Discovery News umstellen

Um Ihre Abfragen von {{site.data.keyword.discoverynewsshort}} Original auf das neue {{site.data.keyword.discoverynewsshort}} umzustellen, müssen Sie alle vorhandenen Abfragen wie folgt ändern:  

- Ändern Sie die Umgebungs-ID, die von der Abfrage aufgerufen wird. Der Name für die Nachrichtenumgebung wurde für alle {{site.data.keyword.discoveryshort}}-Serviceinstanzen wie folgt standardisiert:

  `system`  

- Ändern Sie die Sammlungs-ID, die von der Abfrage aufgerufen wird. Der Name für die Nachrichtensammlung wurde für alle {{site.data.keyword.discoveryshort}}-Serviceinstanzen wie folgt standardisiert:

  `news`

- Ändern Sie die Abfrage so, dass die neue JSON-Pfadstruktur für das neue {{site.data.keyword.discoverynewsshort}} verwendet wird. Bei den meisten Feldern wurden die Pfade geändert. Außerdem wurden mehrere Felder hinzugefügt und eine ausgewählte Gruppe von Feldern mit geringem Wert wurde entfernt. Vollständige Details enthält das Arbeitsblatt für die Feldmigration, das Sie <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/News_migration_v_1.01.xlsx" download>hier <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link" class="style-scope doc-content"></a> finden. Beispielsweise sollte die Abfrage

  `discovery/api/v1/environments/ae5790c2-592f-432a-804a-ee16de7154d7/collections/3edcd8f1-e25a-4f44-a069-58332ad17651/query?version=2017-11-07&query=entities.type:"Company"`

  geändert werden in

  `discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.type:"Company"`  

## Watson Discovery News abfragen

Sie können {{site.data.keyword.discoverynewsshort}} mithilfe der API oder mit einem der {{site.data.keyword.watson}}-SDKs abfragen. Außerdem können Sie mit den Abfrageerstellungstools Abfragen interaktiv erstellen.

**So können Sie die {{site.data.keyword.discoveryshort}}-Tools starten und {{site.data.keyword.discoverynewsshort}} abfragen:**

1. Klicken Sie unter **Services** für {{site.data.keyword.discoveryshort}} auf **Tool starten**.
1. Klicken Sie auf die Kachel '{{site.data.keyword.discoverynewsshort}}', um die Anzeige **Daten verwalten** zu öffnen.
1. Klicken Sie auf **Datenschema anzeigen** und dann auf **Abfragen erstellen**, um den Abfragebuilder zu öffnen.

  Abfragen in {{site.data.keyword.discoverynewsshort}} sind genauso strukturiert wie Abfragen, die für private Datensammlungen geschrieben sind. Weitere Informationen finden Sie unter [Abfragekonzepte](/docs/services/discovery/using.html) und [Abfragereferenz](/docs/services/discovery/query-reference.html).
  {: tip}

**Hinweis**: Erwarten Sie nicht, dass für ähnliche Abfragen in {{site.data.keyword.discoverynewsshort}} Original und {{site.data.keyword.discoverynewsshort}} identische Ergebnisse zurückgegeben werden. Die Kombination aus Zeitpunkt der Crawlersuche, Quellen und Aufbereitungen führt jeweils zu unterschiedlichen Ergebnissen.

## Watson Discovery News-Abfragen zur Anwendung hinzufügen

Verwenden Sie eines der folgenden Verfahren, um Abfragen zu Ihrer Anwendung hinzuzufügen. Alle Beispiele fragen `enriched_text.entities` mit dem Wert `IBM` für `text` (`enriched_text.entities.text:IBM`) ab.

Ersetzen Sie in allen Beispielen `{benutzername}` und `{kennwort}` durch den Benutzernamen und das Kennwort, die auf der Seite **Serviceberechtigungsnachweise** für Ihre Serviceinstanz aufgeführt sind.

### Direkte Aufrufe der API verwenden

```bash
curl -u "{benutzername}":"{kennwort}"  'https://gateway.watsonplatform.net/discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

### Watson-Java-SDK verwenden

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
  }
);
```
{: codeblock}

### Watson-Python-SDK verwenden

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
my_query = discovery.query('system', 'news', qopts)  
print(json.dumps(my_query, indent=2))  
```
{: codeblock}
