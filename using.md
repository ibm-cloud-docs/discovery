---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-25"

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

# Query concepts

The {{site.data.keyword.discoveryfull}} service offers powerful content search capabilities. Once your content is uploaded and enriched by the {{site.data.keyword.discoveryshort}} service, you can build queries, then integrate {{site.data.keyword.discoveryshort}} into your own projects, or create a custom application by using the {{site.data.keyword.watson}} Explorer Application Builder.
{: shortdesc}

  The queries you write will vary by collection, because all collections contain unique content.
  {: tip}

When you create a query or filter, {{site.data.keyword.discoveryshort}} looks at each result and tries to match the paths you have defined. When matches occur, they are added to the results set. When creating a query, you can be as vague or as specific as you want. The more specific the query, the more targeted the results.

You also have the option to turn on passage retrieval. Passages are short, relevant excerpts extracted from the full documents returned by your query. These targeted passages are extracted from the `text` fields of the documents in your collection. By default, up to 10 passages of around 400 characters each will be returned for a query. A maximum of three passages are extracted from a single result. The `passages` parameter is only available for private collections; it is not available in the {{site.data.keyword.discoverynewsshort}} collection. See [Passages](/docs/services/discovery/query-parameters.html#passages) for more information on how passages are identified.

  You can write natural language queries (such as "IBM Watson partnerships") using the {{site.data.keyword.discoveryshort}} tooling or the API.
  {: tip}

Trained collections will return a `confidence` score in the result of a natural language query. See [Confidence scores](/docs/services/discovery/train-tooling.html#confidence) for details.

{{site.data.keyword.discoveryshort}} returns query results that include special characters for the following languages: English, German, French, Dutch, Italian, and Portuguese. For example, if you query for `aqui`, you will now receive results for both for `aqui` and <code>aqu&iacute;</code>.

You can create longer, more complex queries that include multiple filters and complex aggregations. This option is available in the API-only, and will increase the character limit of a query to 10,000 characters. See [Long collection queries ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query){: new_window} and [Long environment queries ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#federated-query){: new_window} for details.

{{site.data.keyword.discoveryfull}} Knowledge Graph is a beta feature which provides new end-points for querying entities and relations across documents. This includes context-based searches and relevance ranking. See [{{site.data.keyword.discoveryfull}} Knowledge Graph](/docs/services/discovery/building-kg.html) for more information.

For more information about writing queries, see:
- [Getting started with querying tutorial](/docs/services/discovery/getting-started-query.html)
- [Query reference](/docs/services/discovery/query-reference.html) (includes the list of parameters, operators, and aggregations available in the {{site.data.keyword.discoveryshort}} Query Language)

## The Discovery data schema
{: #discovery-schema}

Start out by getting to know the {{site.data.keyword.discoveryshort}} JSON. To understand how to build a query using the {{site.data.keyword.discoveryshort}} Query Language, you need to be familiar with the JSON produced by {{site.data.keyword.discoveryshort}} after it enriches the documents in your collection. Once you are familiar with the data schema of your documents, it will be easier to write queries in the {{site.data.keyword.discoveryshort}} Query Language. There are three ways to do this.

  1. In the {{site.data.keyword.discoveryshort}} Tooling, open the **Manage data** screen, choose the collection that contains the {{site.data.keyword.IBM_notm}} Press Releases. Click the **View Data Schema** button. The **View data schema** screen displays the fields and values in your transformed documents two ways: by document (**Document view**), or by field (**Collection view**). A maximum of 50 documents will display in **Document view**. **Collection view** will display the fields in the entire collection.

    In the **Collection view**, under `enriched_text`, you can examine the enrichments you applied with the **Default Configuration** file. Click on `categories`, `concepts`, `entities`, and `sentiment` to see how your collection was enriched with Watson insights.

  1. Run an "empty" query to view the JSON. On the **View data schema** screen, click the **Build queries** button, then click **Run Query**. The results display on the right, under two tabs, **Summary** (an overview of the query results) and **JSON**. Start by opening the **JSON** tab.

     -  Each of the four documents will be proceeded by an `id` number.
     -  Scroll down to the `enriched_text` field. Examine each enrichment to learn about the JSON fields you can query on.

        ![Default configuration fields](images/JSON.png)

     -  **entities** - Start by finding the `text` field, and examine the other enrichment information.
     -  **sentiment** - Start by finding the `label` field, and examine the other enrichment information.
     -  **concepts** - Start by finding the `text` field, and examine the other enrichment information.
     -  **categories** - Start by finding the `document` field, and examine the other enrichment information.

     After you have examined the insights in the first document, you can look at the other three documents if you wish.

  1. View the available fields in the **Visual Query Builder**. On the **Build queries** screen, click **Search for documents**, then **Use the {{site.data.keyword.discoveryshort}} Query Language**. Click the **Field** drop-down to view the fields available in your data. Click **Edit in query language** to build queries manually using the {{site.data.keyword.discoveryshort}} Query Language.      

### How to structure a basic query
{: #structure-basic-query}

As you have noticed, the JSON is hierarchical, so queries need to be written using that same hierarchy. So if your JSON looks like this:

```json
"enriched_text": {
  "concepts": [
    {
    "text": "Cloud computing",
    "relevance": 0.610029}
    ]
  }
```
{: codeblock}

Your query would be structured like this:

![Example query structure](images/query_structure2.png)

  Operators that evaluate a field (`<=` , `>=`, `<`, `>`) require a `number` or `date` as the value. Using quotations around a value always makes it a `string`. Therefore `score>=0.5` is a valid query and `score>="0.5"` is not. See [Query operators](/docs/services/discovery/query-operators.html) for a complete list of operators.
  {: tip}

Considerations:

- Not sure when to query on an entity, concept, or keyword? See [Understanding the difference between Entities, Concepts, and Keywords](/docs/services/discovery/building.html#udbeck).

- **Note:**  After you click **Run query** and open the **JSON** tab, you will notice that query highlighting is turned on by default. This will add a `highlight` field to your query results. Within the `highlight` field, the words that match your query will be wrapped in HTML `<em>` (emphasis) tags. See the [Query parameters](/docs/services/discovery/query-parameters.html#highlight) for details.

## Building combined queries
{: #building-combined-queries}

You can combine query parameters together to build more targeted queries. For example. you can use the both the `filter` and `query` parameters together. For more information about filtering vs. querying, see [Differences between the filter and query parameters](/docs/services/discovery/query-parameters.html#filtervquery).

## How to structure an aggregation
{: #structure-aggregation}

Aggregations return a set of data values; for example, top keywords, overall sentiment of entities, and more. For the full list of aggregation options, see [Aggregations](/docs/services/discovery/query-reference.html#aggregations).

![Example aggregation query structure](images/aggregation_structure.png)

This example aggregation will find all of the `concepts` in your collection.
The delimiter in this query is `.` and the operator is `()`, see [Query operators](/docs/services/discovery/query-operators.html) to learn about other operators available in the {{site.data.keyword.discoveryshort}} Query Language.

### Example aggregation queries
{: #example-aggregations}

There are several types of ways you can aggregate results with {{site.data.keyword.discoverynewsshort}}, including top values, sum, min, max, average, timeslice, and histogram. You can also add filters and nest aggregations.

#### Filter aggregations
{: #filter-aggregations}

This example aggregation returns the number of articles found in {{site.data.keyword.discoverynewsshort}} about the Pittsburgh Steelers and how many of those results have a `positive`, `negative`, or `neutral` sentiment.

- `filter(enriched_text.entities.text:"Pittsburgh Steelers").term(enriched_text.sentiment.document.label,count:3)`


This example aggregation will first narrow down (filter) a set of articles in {{site.data.keyword.discoverynewsshort}} to only the ones that include the entities text of twitter, then divide those articles by the document sentiment types. Only the top 3 document sentiment types (`positive`, `negative`, `neutral`) will be returned.

- `filter(enriched_text.entities.text:twitter).term(enriched_text.sentiment.document.label,count:3)`

#### Nested aggregations
{: #nested-aggregations}

Adding `nested` before an aggregation restricts the aggregation to the area of the results specified. For example: `nested(enriched_text.entities)` means that only the `enriched_text.entities` components of any result are used to aggregate against.

This can be seen easily by looking at the differences between the following two queries:
- `filter(enriched_text.entities.disambiguation.subtype::City)` - the aggregation counts the number of *Results* that contain one or more `entity` with the type `City`
- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City)` - the aggregation counts the number of instances of an `entity` with the type `City` in the results.  

Additionally, any subsequent operation will further restrict the result set that can be aggregated against. For example:

- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City)` means that only entities of `subtype::City` will be aggregated.
- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City).term(enriched_text.entities.text,count:3)` will aggregate the top 3 entities of subtype `City`
- `filter(enriched_text.entities.disambiguation.subtype::City).term(enriched_text.entities.text,count:3)` will return the top 3 entities where the result contains at least one entity of subtype `City`.

## Querying Watson Discovery News
{: #querying-news}

{{site.data.keyword.discoverynewsshort}}, a public data set that has been pre-enriched with cognitive insights, is also included with {{site.data.keyword.discoveryshort}}. See [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html#watson-discovery-news) for more information about this collection.

You can query this collection using natural language queries, for example "IBM Watson partnerships", or the {{site.data.keyword.discoveryshort}} Query Language. To learn more about natural language queries, see the [Natural language query](/docs/services/discovery/query-parameters.html#nlq).

You cannot adjust the {{site.data.keyword.discoverynewsshort}} configuration, train, or add documents to {{site.data.keyword.discoverynewsshort}} collection. See a demo of what you can build with {{site.data.keyword.discoverynewsshort}} [here ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://discovery-news-demo.ng.bluemix.net/){: new_window}.

The English, Korean, German, Spanish, and Japanese language {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} collections are available from both the {{site.data.keyword.discoveryshort}} tooling and the API.

The default language of {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} in the tooling is English. To switch the language, you must first click the ![Manage Data](/images/icon_yourData.png) icon, then choose the appropriate language from the drop-down.

For information about querying a collection via the API, see [API Reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection){: new_window}. The `collection_id` of the English language version of Watson {{site.data.keyword.discoverynewsshort}} is `news-en`. Formerly, the `collection_id` was `news` - if you have been using the former `collection_id`, it will continue to work, however, you may want to switch to the new `collection_id` for new projects. The `collection_id` of the Korean collection is `news-ko`, the Spanish `collection_id` is `news-es`, the German `collection_id` is `news-de`, the Japanese `collection_id` is `news-ja`.

{{site.data.keyword.discoverynewsfull}} queries display the first 50 words of each article in the `text` JSON field.

The maximum number of results returned for a {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} query is `50`. Use additional queries and the `offset` parameter to return more than `50` results.

If using the {{site.data.keyword.discoveryshort}} Query Language, you can include a relative date range in your {{site.data.keyword.discoverynewsshort}} queries, for example: `crawl_date>=now-1month`. Valid date interval values are `second/seconds` `minute/minutes`, `hour/hours`, `day/days`, `week/weeks`, `month/months`, and `year/years`. `now` is not affected by the `time_zone` parameter; the `UTC` time zone is the default.

This example will query for a keyword within a specific date range. The time zone information is not required:
- `enriched_text.keywords.text:"olympics", publication_date<=2018-02-15T00:00:00Z, publication_date>=2018-02-01T00:00:00Z`

News articles may be syndicated to several news outlets and {{site.data.keyword.discoverynewsfull}} will pick up each of them, resulting in duplicate articles. This means that a query to {{site.data.keyword.discoverynewsfull}} may potentially return several identical or nearly identical articles in query results. You can manage this using deduplication. To learn more about this beta capability, see [Excluding duplicate documents from query results](/docs/services/discovery/query-parameters.html#deduplication).

## Querying multiple collections
{: #multiple-collections}

If you have multiple collections in your environment, you might want to view results across those collections. The query methods (`query`, `fields`, and `notices`) at the `environments` level allow you to query multiple specified collections. Querying across collections is not currently available in the {{site.data.keyword.discoveryshort}} tooling.

You can query multiple collections in the same environment by using the `environments/{environment_id}/query` API method. When querying across multiple collections, take into consideration the following items.
-  The `collection_ids` parameter must be specified when using this method. `collection_ids` is a comma-separated list of collections in the environment to query.
-  `passages` are supported when querying multiple collections.
-  `collection_id` is returned as part of each result object. This field specifies the collection where the result was found.
-  The {{site.data.keyword.discoverynewsshort}} is part of the `system` environment and cannot be included in multiple collection queries.
-  Individual collection relevancy training does not affect ranking of results when querying multiple collections. To rerank results returned when querying multiple collections implement [Continuous Relevancy Training](/docs/services/discovery/continuous-training.html).
- Re-ranking is not performed on any part of a multiple collection query, even if all collections in the query have been trained.

See the [multiple collection query API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-multi-collections){: new_window} for more information.

You can view notices across multiple collections in the same environment by using the `environments/{environment_id}/notices` API method.
-  The `collection_ids` parameter must be specified when using this method. `collection_ids` is a comma-separated list of collections in the environment to query.
-  `passages` are supported when querying multiple collections.

See the [multiple collection notices API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#collections-notices){: new_window} for more information.

You can view the fields available across collections in the same environment by using the `environments/{environment_id}/fields` API method. See the [multiple collection field query API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#multi-list-fields){: new_window} for more information.

## Query expansion
{: #query-expansion}

You can expand the scope of a query beyond exact matches - for example, you can expand a query for "car" to include "automobile" and "motor vehicle" - by uploading a list of query expansion terms using the {{site.data.keyword.discoveryshort}} API. Query expansion terms are usually synonyms, antonyms, or typical misspellings for common terms.

You can define two types of expansions:
- **bidirectional** - each `expanded_term` will expand to include all expanded terms. For example, a query for `car` would expand to `car OR automobile OR (motor AND vehicle`).
- **unidirectional** - the `input_terms` in the query will be replaced by the `expanded_terms`. For example, a query for `ibm` could expand to `international business machines` and `big blue`. `input_terms` are not used as part of the resulting query. In the previous `ibm` example, the query `IBM` would be converted to `international business machines` OR `big blue` and not contain the original term.

This file can be used as a starting point when building a query expansion list:
<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/expansions.json" download>expansions.json <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>. You can modify this file to create your custom query expansion list.

Bidirectional example:
```JSON
 {
   "expansions": [
     {
       "expanded_terms": [
         "car",
         "automobile",
         "motor vehicle"
       ]
     }
   ]
 }
```
{: codeblock}

Unidirectional example:
```JSON
 {
   "expansions": [
     {
      "input_terms": [
        "ibm"
       ],
      "expanded_terms": [
        "ibm",
        "international business machines",
        "big blue"
       ]
     }
   ]
 }
```
{: codeblock}

Notes about query expansion:

- Query expansion is only available for private collections. The number of available `expansions` arrays (total bidirectional and unidirectional arrays) and terms (the total `input_terms` plus `expanded_terms`) varies by plan. See [Discovery pricing plans](/docs/services/discovery/pricing-details.html) for details. **Note:** All query terms (both `input_terms` and `expanded_terms`) each count as one term. This example contains two objects in the `expansions` array and eight term strings.

```JSON
 {
   "expansions": [
     {
      "input_terms": [
         "ibm"
       ],
      "expanded_terms": [
         "ibm",
         "international business machines",
         "big blue"
       ]
     },
     {
      "input_terms": [
         "banana"
       ],
      "expanded_terms": [
         "banana",
         "plantain",
         "fruit"
       ]
     }
   ]
 }
```
{: codeblock}

- Only one query expansion list can be uploaded per collection; if a second expansion list is uploaded, it will replace the first.
- All `input_terms` and `expanded_terms` should be lowercase. Lowercase terms will expand to uppercase.
- The query expansion list must be written in JSON.
- To disable query expansion, delete the query expansion list.
- You cannot currently upload or delete a query expansion list using the {{site.data.keyword.discoveryshort}} tooling; it must be done using the {{site.data.keyword.discoveryshort}} API.
- Query expansion is performed on the `query` and `multiple collection query` methods. Query expansion is not performed on Knowledge Graph queries.
- Each set of expansions is associated with a collection. When querying across [multiple collections](/docs/services/discovery/using.html#multiple-collections), each collection is expanded individually.
- Query expansions are applied at query time, not during indexing, so the query expansion list can be updated without the need to re-ingest your documents.
- Do not upload or delete a query expansion list at the same time documents are being ingested into your collection. This could cause the index to be unavailable for that brief period.

See the [query expansion API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-expansion){: new_window} for the API commands to upload and delete query expansion files.

## Document similarity
{: #doc-similarity}

A document similarity query will find other documents similar to the currently viewed document, for example, a call center operator could be viewing the manuals for a product and use document similarity to find other documents with similar characteristics. You can query for similar documents by `similar.document_ids`, and can optionally refine the similarity by specifying additional `similar.fields`. 

Document similarity is determined by extracting the 25 most relevant terms from the original document and then searching for documents with similar relevant terms.

Example query by `similar.document_ids` (there should be no space after the comma if specifying multiple `similar.document_ids`):

`curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&similar.document_ids=4107b6f1-5d3f-4bea-bbcf-fb05bbf960b1,6057k6d1-7d7k-6aeh-cfbb-kj98ssf786c2"`

Example query with `similar.fields` added:

`curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&similar.document_ids=4107b6f1-5d3f-4bea-bbcf-fb05bbf960b1&similar.fields=title&return=title&count=100"`

See the [document similarity API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query-using-get){: new_window} and [query parameters](/docs/services/discovery/query-parameters.html#similar) for more information.
