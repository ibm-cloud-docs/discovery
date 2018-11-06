---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-21"

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

# Getting started with querying

In this tutorial, we will learn how to write a few different types of queries in {{site.data.keyword.discoveryshort}}.
{: shortdesc}

For more information about writing queries, see:
- [Query concepts](/docs/services/discovery/using.html)
- [Query reference](/docs/services/discovery/query-reference.html) (includes the list of parameters, operators, and aggregations available in the {{site.data.keyword.discoveryshort}} Query Language)

These example queries are built using the {{site.data.keyword.discoveryshort}} tooling. If you'd like to use the API instead, add the query parameters to your API call. For more information and examples, see the Queries section of the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/discovery#query-your-collection){: new_window}.

You can also write natural language queries (such as "IBM Watson partnerships") using the {{site.data.keyword.discoveryshort}} tooling. This tutorial primarily focuses on how to write queries with {{site.data.keyword.discoveryshort}} Query Language because your requirements may necessitate a structured query, and filters and aggregations must be written in the {{site.data.keyword.discoveryshort}} Query Language.
{: tip}

## Before you begin

**Complete the steps in [Getting started](/docs/services/discovery/getting-started-tool.html).** If you haven't completed the **Getting started**, go to the **Manage data** screen, create a new collection named {{site.data.keyword.IBM_notm}} Press Releases, and add these four documents to it (use the **Default Configuration**): <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>

## Step 1: Quick tour of the Discovery data schema

Let's start out by getting to know the {{site.data.keyword.discoveryshort}} JSON. To understand how to build a query using the {{site.data.keyword.discoveryshort}} Query Language, it helps to be familiar with the JSON produced by {{site.data.keyword.discoveryshort}} after it enriches the documents in your collection.

1.  [Launch the {{site.data.keyword.discoveryshort}} tooling](/docs/services/discovery/getting-started-tool.html#launch-the-tooling). On the **Manage data** screen, choose the {{site.data.keyword.IBM_notm}} Press Releases collection.

1.  Review the insights Watson discovered in your enriched documents.

    -  **General sentiments** displays the percentage breakdown of documents tagged as positive, neutral, and negative discovered by the Sentiment Analysis enrichment.
    -  **Top entities** displays persons, places, and organizations discovered in your documents by the Entity Extraction enrichment.
    -  **Content hierarchy** displays the hierarchical taxonomies discovered in your documents by the Category Classification enrichment.
    -  **Related concepts** displays the concepts discovered in your documents by the Concept Tagging enrichment.

         Click **View in schema** on any card to see the enrichments that comprise those results.
         {: tip}

1.  To get familiar with the data schema of your documents, let's look at the **View data schema** screen. It displays the fields and values in your transformed documents two ways: by document (**Document view**), or by field (**Collection view**). **Collection view** will display all fields in your collection.

    Click the **View data schema** button. In the **Collection view**, under `enriched_text`, you can examine the enrichments you applied with the **Default Configuration** file. Click on `categories`, `concepts`, `entities`, and `sentiment` to see how your collection was enriched with Watson insights.

If your query does not return any matching results, and you think it should, try swapping out the field/value your query is using for one that you can verify in the data schema.
{: tip}    

## Step 2: Build a basic query

Let's start out by writing a query that will find the concept `Cloud computing` in your collection:

1.  Click on the build queries icon ![Query icon](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> to open the query page. Select the collection that contains the {{site.data.keyword.IBM_notm}} Press Releases and click **Get started**.
1.  On the **Build queries** screen, click **Search for Documents**, then **Use the {{site.data.keyword.discoveryshort}} Query Language** then:
    - Click the **Field** drop-down and choose `enriched_text.concepts.text`, for the **Operator** choose `contains`, then enter the **Value** of `Cloud computing`. The query `enriched_text.concepts.text:Cloud computing` will display under the **Visual Query Builder**.

    - Alternately, you could click **Edit in query language**, then **Use the {{site.data.keyword.discoveryshort}} Query Language**. Enter `enriched_text.concepts.text:"Cloud computing"` into the **Enter query here** field.

1.  Click **Run query**. There should be one match (`"matching_results": 1`). Copy the **Query URL** at the top of the **Summary** or **JSON** tab to use in your application.

**Bonus:** Under **More options**, you have the option to turn on passage retrieval with the **Include relevant passages** radio button. Passages are short, relevant excerpts extracted from the full documents returned by your query. These targeted passages are extracted from the `text` fields of the documents in your collection. See [Passages](/docs/services/discovery/query-parameters.html#passages) for more information. Passage retrieval is not available for the {{site.data.keyword.discoveryshort}} News collection.

If you'd like to check out a few pre-built queries, click the **Use a sample query** button.
{: tip}

## Step 3: Experiment with different queries

Try out these queries:

To return all documents that have a `positive` sentiment: Click **Search for Documents**, **Use the {{site.data.keyword.discoveryshort}} Query Language** then:
-  Click the **Field** drop-down and choose `enriched_text.sentiment.document.label`, for the **Operator** choose `contains`, then enter the **Value** of `positive`.  

   The query `enriched_text.sentiment.document.label:positive` will display under the **Visual Query Builder**.

To return all documents in the `health and fitness` category: Click **Search for Documents**, **Use the {{site.data.keyword.discoveryshort}} Query Language** then:
-  Click the **Field** drop-down and choose `enriched_text.categories.label`, for the **Operator** choose `is`, then enter the **Value** of `"health and fitness"`.

   The query `enriched_text.categories.label::"health and fitness"` will display under the **Visual Query Builder**. The operator `::` specifies an exact match.

To return all documents that contain the entity `IBM`, but not the entity `Watson`: Click **Search for Documents**, **Use the {{site.data.keyword.discoveryshort}} Query Language** then:
-  Click the **Field** drop-down and choose `enriched_text.entities.text`, for the **Operator** choose `contains`, then enter the **Value** of `IBM`. Click **Add rule**, then for the **Field** choose `enriched_text.entities.text`, for the **Operator** choose `does not contain`, then enter the **Value** of `Watson`.

   The query `enriched_text.entities.text:IBM,enriched_text.entities.text:!Watson` will display under the **Visual Query Builder**. The operator `:!` specifies "does not contain".

## Step 4: Build a combined query

You can combine query parameters together to build more targeted queries. Let's try using both the `filter` and `query` parameters to return documents about {{site.data.keyword.IBM_notm}} acquisitions. The filter parameter will narrow down the results to only documents that mention `IBM`, and then the query parameter will return all results about `acquisitions`,in order of relevance.

1.  Click on the build queries icon ![Query icon](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> to open the query page. Select the collection that contains the {{site.data.keyword.IBM_notm}} Press Releases and click **Get started**.

1.  Under **Filter which documents you query**:
    -  Click the **Field** drop-down and choose `enriched_text.entities.text`, for the **Operator** choose `contains`, then enter the **Value** of `IBM`.

       The query `enriched_text.entities.text:IBM` will narrow down the documents to only those that mention the entity `IBM`.

1.  Under **Search for Documents**, click **Use the {{site.data.keyword.discoveryshort}} Query Language**, then:
    -  Click the **Field** drop-down and choose `enriched_text.concepts.text`, for the **Operator** choose `contains`, then enter the **Value** of `world wide web`.

       The query `enriched_text.concepts.text:"world wide web"` will return all documents that include the concept of `world wide web`, and those documents will be ranked in order of relevance.

1.  Click **More options**, then **Fields to return** and choose **Specify**. Select `text`. This will limit the response to the text of the relevant articles and exclude everything else.

1.  Click **Run query**. There will be one matching document: `"matching_results": 1`

## Step 5: Building an aggregation

Aggregations return a set of data values; for example, top keywords, overall sentiment of entities, and more.

Try building this aggregation - it will return the top 10 concepts in the {{site.data.keyword.IBM_notm}} press releases collection.

1.  Click on the build queries icon ![Query icon](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> to open the query page. Select the collection that contains the {{site.data.keyword.IBM_notm}} Press Releases and click **Get started**.

1.  Under **Include analysis of your results**:
    -  Click the **Output** drop-down and choose `Top values`, for the **Field** choose `enriched_text.concepts.text`, then enter the **Count** of `10`.

       `Term` will return the most common values for the `concepts` `text` field. **Count** specifies the number of results that you want returned. The query `term(enriched_text.concepts.text,count:10)` will display under the **Visual Query Builder**.   

1.  Click **More options**, then enter `0` in the **Number of documents to return** field.

1.  Click **Run query**. The top 10 concepts will be displayed in both the **Summary** and **JSON** tabs. Here is an example of the Summary:

## Step 6: Build a query in Watson Discovery News

{{site.data.keyword.discoverynewsshort}}, is a public data set that has been pre-enriched with cognitive insights. It is included with {{site.data.keyword.discoveryshort}}. See [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html#watson-discovery-news) for more information about this collection.

You cannot adjust the {{site.data.keyword.discoverynewsshort}} configuration, train, or add documents to {{site.data.keyword.discoverynewsshort}} collection. See a demo of what you can build with {{site.data.keyword.discoverynewsshort}} [here ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://discovery-news-demo.ng.bluemix.net/){: new_window}.

The following example query returns the top 10 articles in {{site.data.keyword.discoverynewsfull}} about the Pittsburgh Steelers that have a positive sentiment.

1.  Click on the build queries icon ![Query icon](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> to open the query page. Select the {{site.data.keyword.discoverynewsshort}} collection and click **Get started**. (To query the Spanish, German, or Korean {{site.data.keyword.discoverynewsshort}} collections, you must first click the ![Manage Data](/images/icon_yourData.png) icon, then choose the appropriate language from the drop-down.)

1.  Under **Search for documents**, click **Use the {{site.data.keyword.discoveryshort}} Query Language**, then:
    -  Click the **Field** drop-down and choose `text`, for the **Operator** choose `contains`, then enter the **Value** of `Pittsburgh Steelers`. Click **Add rule**, then click the **Field** drop-down and choose `enriched_text.sentiment.document.label`, for the **Operator** choose `contains`, then enter the **Value** of `positive.`

       The query `text:"Pittsburgh Steelers",enriched_text.sentiment.document.label:"positive"` will display under the **Visual Query Builder**.

1.  Click **More options**, then enter `10` (this is the default) in the **Number of documents to return** field.

1.  Click **Run query**. The top 10 articles about the Pittsburgh Steelers with a positive sentiment will be displayed.

**Note:** The maximum number of results returned for a Watson Discovery News query is `50`.

News articles may be syndicated to several news outlets and {{site.data.keyword.discoverynewsfull}} will pick up each of them, resulting in duplicate articles. This means that a query to {{site.data.keyword.discoverynewsfull}} may potentially return several identical or nearly identical articles in query results. To turn on deduplication, under **More options**, choose **Exclude duplicate results**. To learn more about this beta capability, see [Excluding duplicate documents from query results](/docs/services/discovery/query-parameters.html#deduplication).
