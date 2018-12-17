---

copyright:
  years: 2015, 2018
lastupdated: "2018-01-16"

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

# Migrating from Watson Discovery News Original

A new version of {{site.data.keyword.discoverynewsshort}} debuted on **31, July 2017**. The original version was renamed {{site.data.keyword.discoverynewsshort}} Original and was retired from service **15, January 2018**. If you attempt to access {{site.data.keyword.discoverynewsshort}} Original, you will receive the message `410 GONE`.
{: shortdesc}

To migrate from {{site.data.keyword.discoverynewsshort}} Original to the new version, you need to make several changes, including updating any queries created for {{site.data.keyword.discoverynewsshort}} Original.

  **Note:** {{site.data.keyword.discoverynewsshort}} Original was only available in instances of {{site.data.keyword.discoveryshort}} created before **31, July 2017** and was retired from service **15, January 2018**.

See [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html) for a description of this collection.

For a description and information about querying {{site.data.keyword.discoverynewsshort}} Original, see [Watson Discovery News Original](/docs/services/discovery/discovery-auxiliary.html#watson-discovery-news-original).

## Service comparison

| {{site.data.keyword.discoverynewsshort}} Original         | {{site.data.keyword.discoverynewsshort}}           |
|----------------------------------------|---------------------------------|
| **{{site.data.keyword.discoverynewsshort}} Original** was pre-enriched with the following Alchemy Language enrichments: Keyword Extraction, Entity Extraction, Concept Tagging, Relation Extraction, Sentiment Analysis, and Taxonomy Classification. The following additional metadata was also added: crawl date, publication date, URL ranking, host rank, and anchor text.     | **{{site.data.keyword.discoverynewsshort}}** is pre-enriched with the following {{site.data.keyword.nlushort}}  (NLU) enrichments: Keyword Extraction, Entity Extraction, Semantic Role Extraction, Sentiment Analysis, Relations, and Category Classification. The following additional metadata is also added: crawl date and publication date. To learn more about NLU enrichments, see [Adding enrichments](/docs/services/discovery/building.html#adding-enrichments).                         |
| **{{site.data.keyword.discoverynewsshort}} Original** was accessible through an environment that was unique to your service instance.                       | When using **{{site.data.keyword.discoverynewsshort}}**, all users query the same environment and collection. This means that all references to your environment and collection need to be changed.      |
| In **{{site.data.keyword.discoverynewsshort}} Original**, you received information such as collection size, number of documents, etc. when retrieving the environment via the API.  | **{{site.data.keyword.discoverynewsshort}}** API does not return this information.                          |

The following new fields are available in **{{site.data.keyword.discoverynewsshort}}**:

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

Many fields have been removed as well, for example `blekko.hostrank`, `duplicate_url`, `domain`, and more. See <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/News_migration_v_1.01.xlsx" download>HERE <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a> for a complete list.

## Moving Queries to the new Watson Discovery News

To move your queries from {{site.data.keyword.discoverynewsshort}} Original to the new {{site.data.keyword.discoverynewsshort}}, you need to modify all existing queries in the following ways:  

- Change the environment ID that the query is calling. The news environment name has been standardized across all {{site.data.keyword.discoveryshort}} service instances to:

  `system`  

- Change the collection ID that the query is calling. The news collection name has been standardized across all {{site.data.keyword.discoveryshort}} service instances to:

  `news`

- Modify the query to use the new JSON path structure for the new {{site.data.keyword.discoverynewsshort}}. Most fields have changed paths, multiple fields have been added, and a selected group of low-value fields have been removed. See the field migration spreadsheet for full details <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/News_migration_v_1.01.xlsx" download>HERE <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>). For example, the following query:

  `discovery/api/v1/environments/ae5790c2-592f-432a-804a-ee16de7154d7/collections/3edcd8f1-e25a-4f44-a069-58332ad17651/query?version=2017-11-07&query=entities.type:"Company"`

  Should be changed to:

  `discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.type:"Company"`  

## Querying Watson Discovery News

You can query {{site.data.keyword.discoverynewsshort}} by using the API or one of the {{site.data.keyword.watson}} SDKs. Additionally, you can use the query building tooling to interactively construct queries.

**To launch the {{site.data.keyword.discoveryshort}} tooling and query {{site.data.keyword.discoverynewsshort}}:**

1. Click **Launch Tool** for {{site.data.keyword.discoveryshort}} under **Services**.
1. Click on the {{site.data.keyword.discoverynewsshort}} tile to open the **Manage data** screen.
1. Click **View data schema**, then **Build queries** to open the query builder.

  Queries in {{site.data.keyword.discoverynewsshort}} are structured the same way as queries written for private data collections. See [Query concepts](/docs/services/discovery/using.html) and [Query Reference](/docs/services/discovery/query-reference.html).
  {: tip}

**Note:** Do not expect identical results to be returned for similar queries in {{site.data.keyword.discoverynewsshort}} Original and {{site.data.keyword.discoverynewsshort}}. Crawl time, sources, and enrichments all combine to return different results.

## Adding Watson Discovery News queries to your application

Use one of the following methods to add queries to your application. All of these examples query for `enriched_text.entities` with a `text` value of `IBM` (`enriched_text.entities.text:IBM`).

In all of the following examples, replace `{username}` and `{password}` with the username and password that are listed in the **Service Credentials** page of your service instance.

### Using direct calls to the API

```bash
curl -u "{username}":"{password}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

### Using the Watson Java SDK

```java
Discovery discovery = new Discovery("2017-11-07");  
discovery.setEndPoint("https://gateway.watsonplatform.net/discovery/api/v1");
discovery.setUsernameAndPassword("{username}", "{password}");  
String environmentId = "system";
String collectionId = "news";

QueryRequest.Builder queryBuilder = new QueryRequest.Builder(environmentId, collectionId);  
queryBuilder.query("enriched_text.entities.text:IBM");  
QueryResponse queryResponse = discovery.query(queryBuilder.build()).execute();
```
{: codeblock}

### Using the Watson Node.js SDK

```javascript
var watson = require('watson-developer-cloud');  

var discovery = new DiscoveryV1({  
  username: '{username}',  
  password: '{password}',  
  version_date: '2017-11-07'  
});  

discovery.query(('system', 'news', 'enriched_text.entities.text:IBM'),  
  function(error, data) {  
    console.log(JSON.stringify(data, null, 2));  
  }
);
```
{: codeblock}

### Using the Watson Python SDK

```python
import sys  
import os  
import json  
from watson_developer_cloud import DiscoveryV1  

discovery = DiscoveryV1(  
  username="{username}",  
  password="{password}",  
  version="2017-11-07"  
)  

qopts = {'query': 'enriched_text.entities.text:IBM'}  
my_query = discovery.query('system', 'news', qopts)  
print(json.dumps(my_query, indent=2))  
```
{: codeblock}
