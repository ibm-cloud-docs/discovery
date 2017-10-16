---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-16"

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

You also have the option to turn on passage retrieval. Passages are short, relevant excerpts extracted from the full documents returned by your query. These targeted passages are extracted from the `text` fields of the documents in your collection. A maximum of three passages of no more than 2,000 characters each will be returned per relevant document, and no more than 10 passages total will be returned (the number of passages returned cannot be changed). The `passages` parameter is only available for private collections; it is not available in the {{site.data.keyword.discoverynewsshort}} collection. See [Passages](/docs/services/discovery/query-parameters.html#passages) for details.

  You can write natural language queries (such as "IBM Watson partnerships") using the {{site.data.keyword.discoveryshort}} tooling or the API.
  {: tip}

For more information about writing queries, see:
- [Getting started with querying tutorial](/docs/services/discovery/getting-started-query.html)
- [Query reference](/docs/services/discovery/query-reference.html) (includes the list of parameters, operators, and aggregations available in the {{site.data.keyword.discoveryshort}} Query Language)

## The Discovery data schema
{: #discovery-schema}

Start out by getting to know the {{site.data.keyword.discoveryshort}} JSON. To understand how to build a query using the {{site.data.keyword.discoveryshort}} Query Language, you need to be familiar with the JSON produced by {{site.data.keyword.discoveryshort}} after it enriches the documents in your collection. Once you are familiar with the data schema of your documents, it will be easier to write queries in the {{site.data.keyword.discoveryshort}} Query Language. There are three ways to do this.

  1. In the {{site.data.keyword.discoveryshort}} Tooling, open the **Manage data** screen, choose the collection that contains the {{site.data.keyword.IBM_notm}} Press Releases. Click the **View Data Schema** button. The **View data schema** screen displays the fields and values in your transformed documents two ways: by document (**Document view**), or by field (**Collection view**). A maximum of 50 documents will display in **Document view**. **Collection view** will display the fields in the entire collection.

    In the **Collection view**, under `enriched_text`, you can examine the enrichments you applied with the **Default Configuration** file. Click on `categories`, `concepts`, `entities`, and `sentiment` to see how your collection was enriched with Watson insights.

  1. Run an "empty" query to view the JSON. On the **View data schema** screen, click the **Build queries** button, then **Run Query**. The results display on the right, under two tabs, **Summary** (an overview of the query results) and **JSON**. Start by opening the **JSON** tab.

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

- `filter(text:"Pittsburgh Steelers").term(enriched_text.sentiment.document.label,count:3)`


This example aggregation will first narrow down (filter) a set of articles in {{site.data.keyword.discoverynewsshort}} to only the ones that include the entities text of twitter, then divide those articles by the document sentiment types. Only the top 3 document sentiment types (`positive`, `negative`, `neutral`) will be returned.

- `filter(enriched_text.entities.text:twitter).term(enriched_text.sentiment.document.label,count:3)`

#### Nested aggregations
{: #nested-aggregations}

Adding `nested` before an aggregation restricts the aggregation to the area of the results specified. For example: `nested(text.entities)` means that only the `text.entities` components of any result are used to aggregate against.

This can be seen easily by looking at the differences between the following two queries:
- `filter(text.entities.type::City)` - the aggregation counts the number of *Results* that contain one or more `entity` with the type `City`
- `nested(text.entities).filter(text.entities.type::City)` - the aggregation counts the number of instances of an `entity` with the type `City` in the results.  

Additionally, any subsequent operation will further restrict the result set that can be aggregated against. For example:

- `nested(text.entities).filter(text.entities.type::City)` means that only entities of `type::City` will be aggregated.
- `nested(text.entities).filter(text.entities.type::City).term(text.entities.text,count:3)` will aggregate the top 3 entities of type `City`
- `filter(text.entities.type::City).term(text.entities.text,count:3)` will return the top 3 entities where the result contains at least one entity of type `City`.

## Querying Watson Discovery News
{: #querying-news}

{{site.data.keyword.discoverynewsshort}}, a public data set that has been pre-enriched with cognitive insights, is also included with {{site.data.keyword.discoveryshort}}. See [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html#watson-discovery-news) for more information about this collection.

You can query this collection using natural language queries, for example "IBM Watson partnerships", or the {{site.data.keyword.discoveryshort}} Query Language. To learn more about natural language queries, see the [Natural language query](/docs/services/discovery/query-parameters.html#nlq).

You cannot adjust the {{site.data.keyword.discoverynewsshort}} configuration, train, or add documents to {{site.data.keyword.discoverynewsshort}} collection. See a demo of what you can build with {{site.data.keyword.discoverynewsshort}} [here ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://discovery-news-demo.mybluemix.net/){: new_window}.

**Note:** The maximum number of results returned for a Watson Discovery News query is `50`. Use additional queries and the `offset` parameter to return more than `50` results.

News articles may be syndicated to several news outlets and {{site.data.keyword.discoverynewsfull}} will pick up each of them, resulting in duplicate articles. This means that a query to {{site.data.keyword.discoverynewsfull}} may potentially return several identical or nearly identical articles in query results. You can manage this using deduplication. To learn more about this beta capability, see [Excluding duplicate documents from query results](/docs/services/discovery/query-parameters.html#deduplication).

## Querying multiple collections
{: #multiple-collections}

If you have multiple collections in your environment, you might want to view results across those collections. The query methods (`query`, `fields`, and `notices`) at the `environments` level allow you to query multiple specified collections. Querying across collections is not currently available in the {{site.data.keyword.discoveryshort}} tooling.

You can query multiple collections in the same environment by using the `environments/{environment_id}/query` API method. When querying across multiple collections, take into consideration the following items.
-  The `collection_ids` parameter must be specified when using this method. `collection_ids` is a comma-separated list of collections in the environment to query.
-  `passages` and all sub parameters are not supported when querying multiple collections.
-  A new field, `collection_id` is returned as part of each result object. This field specifies the collection where the result was found.
-  The {{site.data.keyword.discoverynewsshort}} is part of the `system` environment and cannot be included in multiple collection queries.
-  Re-ranking is not performed on any part of a multiple collection query, even if all collections in the query have been trained.

See the [multiple collection query API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-multi-collections){: new_window} for more information.

You can view notices across multiple collections in the same environment by using the `environments/{environment_id}/notices` API method.
-  The `collection_ids` parameter must be specified when using this method. `collection_ids` is a comma-separated list of collections in the environment to query.
-  `passages` and all sub parameters are not supported when querying multiple collections.

See the [multiple collection notices API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#collections-notices){: new_window} for more information.

You can view the fields available across collections in the same environment by using the `environments/{environment_id}/fields` API method. See the [multiple collection field query API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#multi-list-fields){: new_window} for more information.
