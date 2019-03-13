---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-01-14"

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

# Improving result relevance with the API
{: #improving-result-relevance-with-the-api}

You can train the {{site.data.keyword.discoveryshort}} service to improve the relevance of query results for your particular organization or subject area. When you provide a {{site.data.keyword.discoveryshort}} instance with *training data*, the service uses machine-learning Watson techniques to find signals in your content and questions. The service then reorders query results to display the most relevant results at the top. As you add more training data, the service instance becomes more accurate and sophisticated in the ordering of results it returns.
{: shortdesc}

Relevancy training is optional; if the results of your queries meet your needs, no further training is necessary. For an overview of building use cases for training, see the blog post [How to get the most out of Relevancy Training ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window}.

For comprehensive information about the training APIs, see the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery){: new_window}.

If you would prefer to use the {{site.data.keyword.discoveryshort}} tooling to train {{site.data.keyword.discoveryshort}}, see [Improving result relevance with the tooling](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling).

**Note:** Relevance training currently applies only to natural language queries in private collections. It is not intended for use with structured, {{site.data.keyword.discoveryshort}} Query Language queries.  For more about the {{site.data.keyword.discoveryshort}} Query Language, see [Query concepts](/docs/services/discovery?topic=discovery-query-concepts#query-concepts).

Trained collections will return a `confidence` score in the result of a natural language query. See [Confidence scores](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence) for details.

Adding a custom stopwords list can improve the relevance of results for natural language queries. See [Defining stopwords](/docs/services/discovery?topic=discovery-query-concepts#stopwords) for more information.

See [Training data requirements](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#reqs) for the minimum requirements for training, as well as the training limits.

See [Usage monitoring](/docs/services/discovery?topic=discovery-usage#usage) for details on tracking usage and using this data to help you understand and improve your applications.

<!-- A trained Discovery service instance is intended primarily for use with natural language queries, but it works equally well with queries that use structured syntax. -->  <!-- See [Query Concepts](/docs/services/discovery?topic=discovery-query-concepts#query-concepts) and the [Query reference](/docs/services/discovery?topic=discovery-query-reference#query-reference) for information about structured queries and natural language queries. -->

The components needed to train a Discovery instance include the following:

 - **Training data**. This is the set of *queries* and *examples* the service uses to refine query results.
 - **Query**. A natural-language query that applies to the training-data set.
   Each query has one or more associated *examples*, as described in the following bullet point.
   Each query must be unique within the training-data set.
 - **Example**. This is a document indexed in a Discovery collection that acts as an exemplar, **good or bad**, for the associated query. When you add an example to a training-data query, you include a relevance label that indicates the relevance (or "goodness" versus "badness") of the document as it applies to the specified query.

   Examples are identified by the indexed document ID. As noted, every example must include a label that indicates the "goodness" or "badness" of the document as it pertains to the query.

   Examples can optionally specify a cross-reference query. The cross-reference query needs to return only the example document and must be independent of the unique Watson Discovery document ID. Cross-reference queries are not currently used automatically but can be used to repair training data in the event that new IDs are assigned to documents during an ingestion event.

## Training data requirements
{: #reqs}

Training data must meet the following **minimal** quality criteria to effectively improve the relevance of answers that are returned by the Discovery service. Note that **minimal** does not mean **optimal**. The service checks the training data periodically to determine if these requirements are met, and automatically updates itself based on any changes.

- The collection's training-data set must contain at least 49 unique training queries (that is, sets of queries and examples). Depending on the size and complexity of your collection, the number of training queries in your set might need to be higher than 49 before Watson is able to apply relevancy training to the collection. Watson will provide feedback if it needs more queries in order to train.
- When assigning relevance scores via the API: The relevance score for each training query must be a non-negative integer, for example `0` to represent *not relevant*, `1` to represent *somewhat relevant*,  and `2` to represent *highly relevant*. However, for maximum flexibility, the service accepts non-negative integers between `0` and `100` for advanced users experimenting with different scoring schemes. Regardless of the range you use, the largest integer in the set of training queries indicates maximum relevance.
- When assigning relevance ratings via the Tooling: The {{site.data.keyword.discoveryshort}} tooling uses the relevance scores of `0` to represent *not relevant*, and `10` to represent *relevant*. You should apply both available ratings to your results: `Relevant` and `Not relevant`. Only rating the `Relevant` documents will not provide the data needed.  If you plan to score your documents using both the {{site.data.keyword.discoveryshort}} tooling and the API, or you plan to begin with the API and move to the tooling, use the `0` and `10` relevancy scores.
- The training queries must include some term overlap between the query and the desired answer so it can be retrieved by the Discovery service's initial search, which is broad in scope.

**Note:** Watson uses training data to learn patterns and to generalize, not to memorize individual training queries. The service therefore might not always reproduce identical relevance results for any given training query.

Training cannot exceed the following **maximum** requirements:
  - You cannot exceed 24 trained collections per environment.
  - Within a single collection, you are limited to 10,000 training queries, with a maximum of 100 examples per query. 

## Adding a query to the training-data set
{: #adding-a-query}

Use the `POST /v1/environments/{environment_id}/collections/{collection_id}/training_data` method to add a query to a collection's set of training data. The query is specified as a JSON object in the following format:

```json
{
  "query_id": "string",
  "natural_language_query": "string",
  "filter": "string",
  "examples": [
    {
      "document_id": "string",
      "cross_reference": "string",
      "relevance": 0
    }
  ]
}
```
{: codeblock}

The values in this object are as follows:

- `query_id`: A unique ID for the query. If you do not specify this field, the service automatically generates an ID.
- `natural_language_query`: A Discovery natural-language query that applies to the training set. <!-- The `natural_language_query` parameter is preferred. -->
- `filter`: An optional filter for the query, as described in the [Query reference](/docs/services/discovery?topic=discovery-query-reference#parameter-descriptions).

    **Note:** If you include filters in your training-data queries, be sure to use the same filters when you use natural language queries in your trained collection. If you train the collection with filtered data but do not use the same types of filters when you query the collection, the results can be unpredictable.

- `examples`: An array that contains the following values:

   - `document_id`: The unique ID of the document that applies to the training set. This is the *example* described previously.
   - `cross_reference`: An optional label, typically consisting of a field in the referenced document, that "pins" the document and the field's information in place in the event the document's ID changes, for example if a newly ingested document is assigned the same ID. Specifying a value for `cross-reference` does **not** link one document to another; rather, it ensures that the service retains the document's pertinent information in case the document gets renamed or overwritten.
   - `relevance`: An integer from `0` to `100`, inclusive, that indicates the relative relevance of the query to the training data. Higher values indicate higher relevance. A value of `0` indicates no relevance to the query, whereas a value of `100` indicates absolute relevance to the query.

   **Note:** Although the range of the `relevance` parameter is `0` to `100` for maximum flexibility, you can use a smaller range to simplify scoring examples. A standard range might be `0` to `4`, or you could use the entire range, but only ever use increments of 20 (`0`,`20`,`40`,`60`,`80`, and `100`). The {{site.data.keyword.discoveryshort}} tooling uses the relevance scores of `0` to represent *not relevant*,  and `10` to represent *relevant*. If you plan to score your documents using both the {{site.data.keyword.discoveryshort}} tooling and the API, or you plan to begin with the API and move to the tooling, use the `0` and `10` relevancy scores.

The following object shows a populated training-data query.

```json
{
  "natural_language_query": "why is the sky blue",
  "filter": "text:meteorology",
  "examples": [
    {
      "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
      "relevance": 0
    },
    {
      "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
      "relevance": 1
    },
    {
      "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
      "cross_reference": "my_id_field:1463",
      "relevance": 4
    }
  ]
}
```
{: codeblock}

The following command example adds the previous training-data query to a collection named `99040100-fe6a-4782-a4f5-28f9eee30850` in an environment named `a56dd9b4-040b-4ea3-a736-c1e7a467e191`:

```bash
curl -X POST -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" -H "Content-Type: application/json" -d
'{
  "natural_language_query": "why is the sky blue",
  "filter": "text:meteorology",
  "examples": [
    {
    "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
    "relevance": 0
    },
    {
      "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
      "relevance": 1
    },
    {
      "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
      "cross_reference": "my_id_field:1463",
      "relevance": 4
    }
  ]
}'
"https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
```
{: pre}

## Adding an example to a training-data query
{: #adding-an-example}

After you create a training-data query, you can continue to add examples to it to improve the accuracy of the training. Use the `POST /v1/environments/{environment_id}/collections/{collection_id}/training_data/{query_id}` to add an example to an existing training-data query.

Perform the following steps to add an example to a training-data query.

1. Get the query ID of the training-data query to which you want to add a new example by [listing the collection's training-data queries ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#list-training-data){: new_window}:

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
   ```
   {: pre}

   The JSON that is returned will be of the following format:

   ```json
    {
      "query_id": "484baad4-d440-44b7-a0dd-70bb2ac77baa",
      "natural_language_query": "why is the sky blue",
      "filter": "text:meteorology",
      "examples": [
        {
          "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
          "relevance": 0
        },
        {
          "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
          "relevance": 1
        },
        {
          "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
          "cross_reference": "my_id_field:1463",
          "relevance": 4
        }
      ]
    }
   ```
   {: codeblock}

1. Add the new example by using the same syntax you use to define examples when creating a new training-data query. The following command example does not include a cross reference.

   ```bash
    curl -u -X POST -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" -H "Content-Type: application/json" -d
    '{
      "document_id": "46b52fdc-3a72-4700-9849-ac217532b373",
      "relevance": 3
    }' "https://gateway.watsonplatform.net/discovery/api/v1/environments//a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data/484baad4-d440-44b7-a0dd-70bb2ac77baa?version=2016-12-01"
   ```
   {: pre}

1. Verify that the new example has been added to the training-data query by again [listing the collection's training-data queries ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#list-training-data){: new_window}:

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
   ```
   {: pre}

   The JSON that is returned will be of the following format:

   ```json
    {
      "query_id": "484baad4-d440-44b7-a0dd-70bb2ac77baa",
      "natural_language_query": "why is the sky blue",
      "filter": "text:meteorology",
      "examples": [
        {
          "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
          "relevance": 0
        },
        {
          "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
          "relevance": 1
        },
        {
          "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
          "cross_reference": "my_id_field:1463",
          "relevance": 4
        },
        {
          "document_id": "46b52fdc-3a72-4700-9849-ac217532b373",
          "relevance": 3
        }
      ]
    }
   ```
   {: codeblock}

1. Check the status of the training by using the [List collection details ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#get-collection-details){: new_window} method and looking at the value of the `"training"`/`"available"` field. When you have added enough queries and examples to meet the training requirements, the value of the field returns as `true` and the service automatically begins to use the training data.

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850?version=2016-12-01"
   ```
   {: pre}

   The JSON that is returned will be of the following format:

   ```json
    {
      "collection_id": "99040100-fe6a-4782-a4f5-28f9eee30850",
      "name": "democollection",
      "configuration_id": "def9bd08-8472-470f-ab5a-e377f77e9300",
      "language": "en_us",
      "status": "available",
      "description": "this is a demo collection",
      "created": "2015-08-24T18:42:25.324Z",
      "updated": "2015-08-24T18:42:25.324Z",
      "document_counts": {
        "available": 1000,
        "processing": 20,
        "failed": 180
      },
      "disk_usage": {
        "used_bytes": 895111
      },
      "training_status": {
        "data_updated": "2017-02-10T14:18:22.786Z",
        "total_examples": 54,
        "sufficient_label_diversity": false,
        "processing": false,
        "minimum_examples_added": true,
        "successfully_trained": "2017-02-08T14:18:22.786Z",
        "available": true,
        "notices": 13,
        "minimum_queries_added": true
      }
    }
   ```
   {: codeblock}

1. When the following fields in the previous step all return `true`, issue some sample queries to see if the service returns more relevant results:

   - `minimum_queries_added`
   - `minimum_examples_added`
   - `sufficient_label_diversity`

   If the relevance of your results has not improved, add more training queries until the results meet your requirements.

For additional training guidance, see [Relevancy training tips](/docs/services/discovery?topic=discovery-relevancy-tips#relevancy-tips).   

## Performing other training-data query operations
{: #training-data-operations}

You can administer and maintain training-data queries by using other API methods as described in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery){: new_window}:

 - [List the training data for a collection ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#list-training-data){: new_window}
 - [Delete all training data for a collection ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#delete-all-training-data){: new_window}
 - [Display the contents of a specified training-data query ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#get-details-about-a-query){: new_window}
 - [Delete a training-data query from the collection ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/watson/developercloud/discovery/api/v1#delete-example-for-training-data-query){: new_window}
 - [Change a training-data query example's relevance label or cross reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#change-label-or-cross-reference-for-example){: new_window}
 - [Delete an example document from a training-data query ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#list-training-data){: new_window}

 **Error monitoring:** Training-data errors appear in the notices, which you can monitor using the [query notices API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#query-system-notices){: new_window}
 (`GET /v1/environments/{environment_id}/collections/{collection_id}/notices`).
