---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-08"

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

# Migrating from AlchemyData News

A new version of {{site.data.keyword.discoverynewsfull}} debuted on **31, July 2017**. See [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html) for a description of this collection.

AlchemyData News has been retired with a removal from service date of **7, March 2018**

## Service comparison
{: shortdesc}

The following differences are of note when moving from AlchemyData News to {{site.data.keyword.discoverynewsshort}} in the {{site.data.keyword.discoveryshort}} service.

- {{site.data.keyword.discoveryshort}} charges for news queries by the query only. All fields are available for return with each result at no additional cost.
- Each {{site.data.keyword.discoveryshort}} query can return up to a maximum of 50 results. An `offset` parameter is available so that you can page queries to whatever number of results you require.
- {{site.data.keyword.discoveryshort}} additionally supports aggregations. See the [aggregations](/docs/services/discovery/query-reference.html#aggregations) section of the {{site.data.keyword.discoveryshort}} documentation for more information.
- {{site.data.keyword.discoverynewsfull}} doesn't rank in the same way that AlchemyData News does. There is currently no field for ranking.
- The query structure and the structure of data returned is different between {{site.data.keyword.discoverynewsshort}} and AlchemyData News. A good way to understand the JSON structure is to query for a single result in {{site.data.keyword.discoverynewsshort}} and inspect the result.
- {{site.data.keyword.discoverynewsshort}} does not support XML output.
- Deduplication is a beta feature in {{site.data.keyword.discoverynewsshort}}.

## Authentication differences

The {{site.data.keyword.discoveryshort}} service uses the standard {{site.data.keyword.Bluemix_notm}} `username` and `password` credentials to access queries. This replaces the existing API key method that AlchemyData News used. All {{site.data.keyword.discoveryshort}} queries must be made with a username and password combination created by {{site.data.keyword.discoveryshort}} service instance.

Your service credentials can be managed by viewing the **Service Credentials** tab of your service within {{site.data.keyword.Bluemix_notm}}.

## Configuring a Discovery instance

A {{site.data.keyword.discoveryshort}} service instance is created in the same way that you created your AlchemyData News instance.

1. Navigate to [{{site.data.keyword.Bluemix_notm}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/catalog/services/discovery){: new_window}, login, and select {{site.data.keyword.discoveryshort}} from the service catalog.
1. Select the appropriate plan for your needs and click **Create**.

  The {{site.data.keyword.discoveryshort}} service offers a Lite plan with 1000 available news queries per month. You can use an instance of this plan to identify equivalent queries without having to pay for them.
  {: tip}

1. Click on the **Service Credentials** tab and select **View Credentials** to identify the `url`, `username`, and `password` for this instance.

## Querying Watson Discovery News

You can query {{site.data.keyword.discoverynewsfull}} by using the API or one of the {{site.data.keyword.watson}} SDKs. Additionally, you can use the query building tooling to construct queries interactively.

To launch the {{site.data.keyword.discoveryshort}} tooling and query {{site.data.keyword.discoverynewsshort}}:

1. Click **Launch Tool** for {{site.data.keyword.discoveryshort}} under **Services**.
1. Click on the {{site.data.keyword.discoverynewsshort}} tile to open the **Manage data** screen.
1. Click **View data schema**, then **Build queries** to open the query builder.

  Queries in {{site.data.keyword.discoverynewsfull}} are structured the same way as queries written for private data collections. See [Query concepts](/docs/services/discovery/using.html) and [Query reference](/docs/services/discovery/query-reference.html).
  {: tip}

Do not expect identical results to be returned for similar queries in AlchemyData News and {{site.data.keyword.discoverynewsfull}}. Crawl time, sources, and enrichments all combine to return different results.
{: note}

## Adding Watson Discovery News queries to your application

Use one of the following methods to add queries to your application. All of these examples query for `enriched_text.entities` with a `text` value of `IBM` (`enriched_text.entities.text:IBM`).

In all of the following examples, replace `{username}` and `{password}` with the username and password that are listed in the **Service Credentials** page of your service instance.

### Using direct calls to the API

```bash
curl -u "{username}":"{password}"  'https://gateway.watsonplatform.net/discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

### Using the Java SDK

```java
Discovery discovery = new Discovery("2017-11-07");
discovery.setEndPoint("https://gateway.watsonplatform.net/discovery/api/v1");
discovery.setUsernameAndPassword("{username}", "{password}");  
String environmentId = "system";
  String collectionId = "news";

QueryRequest.Builder queryBuilder = new QueryRequest.Builder(environmentId,collectionId);  
queryBuilder.query("enriched_text.entities.text:IBM");  
QueryResponse queryResponse =  
discovery.query(queryBuilder.build()).execute();
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
my_query = discovery.query('{environment_id}', '{collection_id}', qopts)
print(json.dumps(my_query, indent=2))
```
{: codeblock}
