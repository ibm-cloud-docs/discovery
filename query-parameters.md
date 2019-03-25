---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-03-25"

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

# Query parameters
{: #query-parameters}

The {{site.data.keyword.discoveryfull}} service offers powerful content search capabilities through queries. After your content is uploaded and enriched by the {{site.data.keyword.discoveryshort}} service, you can build queries, integrate {{site.data.keyword.discoveryshort}} into your own projects, or create a custom application by using the {{site.data.keyword.watson}} Explorer Application Builder. To get started with queries, see [Query concepts](/docs/services/discovery?topic=discovery-query-concepts#query-concepts). For the complete list of parameters, see the [Query reference](/docs/services/discovery?topic=discovery-query-reference#parameter-descriptions).
{: shortdesc}

**Search parameters**

Search parameters enable you to search your collection, identify a result set, and perform analysis on the result set.

The **results set** is the group of documents identified by the combined searches of the search parameters. The results set may be significantly larger than the returned results. If an empty query is performed, the results set is equal to all the documents in the collection.

## query
{: #query}

A query search returns all documents in your data set with full enrichments and full text in order of relevance. A query also excludes any documents that don't mention the query content. These queries are written using the [{{site.data.keyword.discoveryshort}} Query Language](/docs/services/discovery?topic=discovery-query-operators#query-operators).

## filter
{: #filter}

A cacheable query that excludes any documents that don't mention the query content. Filter search results are **not** returned in order of relevance. These queries are written using the [{{site.data.keyword.discoveryshort}} Query Language](/docs/services/discovery?topic=discovery-query-operators#query-operators)

### Differences between the filter and query parameters
{: #filtervquery}

If you test the same search term on a small data set, you might find that the `filter` and `query` parameters return very similar (if not identical) results. However, there is a difference between the two parameters.

- Using a filter parameter alone will return search results in no specific order.
- Using a query parameter alone will return search results in order of relevance.

In large data sets, if you need results returned in order of relevance, you should combine the `filter` and `query` parameters, because using them together will improve performance. This is because the `filter` parameter will run first and cache results, then the `query` parameter will rank them. For an example of using filters and queries together, see [Building combined queries](/docs/services/discovery?topic=discovery-query-concepts#building-combined-queries). Filters can also be used in aggregations.

When you write a query that includes both a `filter`, and an `aggregation`, `query`, or `natural_language_query` parameter; the `filter` parameters run first, after which any `aggregation`, `query`, or `natural_language_query` parameters run in parallel.

With a simple query, especially on a small data set, `filter` and `query` often return the exact same (or similar) results. If a `filter` and `query` call return similar results, and getting a response in order of relevance does not matter, it is better to use filter because filter calls are faster and are cached. Caching means that the next time you make that call, you get a much quicker response, particularly in a big data set.

## aggregation
{: #aggregation}

Aggregation queries return a count of documents matching a set of data values; for example, top keywords, overall sentiment of entities, and more. For the full list of aggregation options, see the [Aggregations table](/docs/services/discovery?topic=discovery-query-aggregations#query-aggregations). These aggregations are written using the [{{site.data.keyword.discoveryshort}} Query Language](/docs/services/discovery?topic=discovery-query-operators#query-operators)

## natural_language_query
{: #nlq}

A natural language query enables you to perform queries expressed in natural language, as might be received from an end user in a conversational or free-text interface - for example: "IBM Watson in healthcare". The parameter uses the entire input as the query text. It does **not** recognize operators. The `natural_language_query` parameter enables capabilities such as passage search and relevancy training. All private collections will return a `confidence` score in the query results in most cases. See [Confidence scores](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence) for details. The maximum query string length for a natural language query is `2048`.

**Structure parameters**

Structure parameters define the content and organization of the documents in the returned JSON. This includes the number of results retuned, where in the results set to start returning documents, how the result set is sorted, which fields to return for each documents, if duplicate documents should be removed, and if relevant passages should be extracted from the results set. Structure parameters don't affect which documents are part of the entire results set.

## count
{: #count}

The number of documents that you want returned in the response. The default is `10`. The maximum for the `count` and `offset` values together in any one query is `10000`.

## offset
{: #offset}

The number of query results to skip at the beginning. For example, if the total number of results that are returned is 10, and the offset is 8, it returns the last two results. The default is `0`. The maximum for the `count` and `offset` values together in any one query is `10000`.

## return
{: #return}

A comma-separated list of the portion of the document hierarchy to return. Any of the document hierarchy are valid values.

## sort
{: #sort}

A comma-separated list of fields in the document to sort on. You can optionally specify a sort direction by prefixing the field with `-` for descending order or `+` for ascending order. Ascending order is the default sort direction.

The `sort` parameter is currently available for use only with the API; it is not available through the tooling.

## bias
{: #bias}

Adjusts search results to bias towards certain results, for example, documents that were published most recently. `bias` must be set to either a `date` type field or a `number` type field, for example `bias=publication_date` or `bias=field_1`.  When a `date` type field is specified, returned results will be biased towards field values closer to the current date. When a `number` type field is specified, returned results will be biased towards higher field values. This parameter cannot be used in the same query as the `sort` parameter.

The `bias` parameter is currently available for use only with the API; it is not available through the tooling.

## passages
{: #passages}

A boolean that specifies whether the service returns a set of the most relevant passages from the documents returned by a query that uses the `natural_language_query` parameter. The passages are generated by sophisticated Watson algorithms to determine the best passages of text from all of the documents returned by the query. The default is `false`.

The `passages` parameter can only be used on private collections. It cannot be used on the {{site.data.keyword.discoverynewsfull}} collection.
{: tip}

{{site.data.keyword.discoveryshort}} attempts to return passages that start at the beginning of a sentence and stop at the end using sentence boundary detection. To do so, it first searches for passages approximately the length specified in the [`passages.characters` parameter](/docs/services/discovery?topic=discovery-query-parameters#passages_characters) (default `400`). It then expands each passage to the limit of twice the specified length in order to return full sentences. If your `passages.characters` parameter is short and/or the sentences in your documents are very long there may be no sentence boundaries close enough to return the full sentence without going over twice the requested length. In that case, {{site.data.keyword.discoveryshort}} stays within the limit of twice the `passages.characters` parameter, so the passage returned will not include the entire sentence and omit the beginning, end, or both.

Since sentence boundary adjustments expand passage size, you will see a substantial increase in average passage length. If your application has limited screen space, you may want to set a smaller value for `passages.characters` and/or truncate the passages that are returned by {{site.data.keyword.discoveryshort}}. Sentence boundary detection works for all supported languages and uses language-specific logic.

You can adjust the fields in the documents over which passage retrieval searches with the [`passages.fields`](/docs/services/discovery?topic=discovery-query-parameters#passages_fields) parameter.

The `passages` parameter returns matching passages (`passage_text`), as well as the `score`, `document_id`, the name of the field the passage was extracted from (`field`), and the starting and ending characters of the passage text within the field (`start_offset` and `end_offset`), as shown in the following example. The query is shown at the top of the example.

```bash
 curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-06-25&natural_language_query='Hybrid%20cloud%20companies'&passages=true"
```
{: pre}

The JSON that is returned will be of the following format:

```json
 {
   "matching_results":2,
   "passages":[
     {
       "document_id":"ab7be56bcc9476493516b511169739f0",
       "passage_score":15.230205287402338,
       "passage_text":"a privately held company that provides hybrid cloud recovery, cloud migration and business continuity software for enterprise data centers and cloud infrastructure."
       "start_offset":120
       "end_offset":300
       "field":"text"       
     },
     {
       "passage_text":"Disaster Recovery Services for Hybrid Cloud</title></head>\n<body>\n\n\n<p>Published: Thu, 27 Oct 2016 07:01:21 GMT</p>\n"
       "passage_score":10.153470191601558,
       "document_id":"fbb5dcb4d8a6a29f572ebdeb6fbed20e",              
       "start_offset":70
       "end_offset":120
       "field":"html"
     },
  ...
```
{: codeblock}                        

### passages.fields
{: #passages_fields}

A comma-separated list of fields in the index that passages will be drawn from. If this parameter not specified then all top level field are included.

### passages.count
{: #passages_count}

The maximum number of passages to return. The search will return fewer passages if that is the total number found. The default is `10`. The maximum is `100`.

### passages.characters
{: #passages_characters}

The approximate number of characters that any one passage should have. The default is `400`. The minimum is `50`. The maximum is `2000`. Passages returned may be up to twice the requested length (if necessary) to get them to begin and end at sentence boundaries.

## highlight
{: #highlight}

A boolean that specifies whether the returned output includes a `highlight` object in which the keys are field names and the values are arrays that contain segments of query-matching text highlighted by the HTML `*` tag.

The output lists the `highlight` object after the `enriched_text` object, as shown in the following example.

```bash
curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-06-25&natural_language_query=Hybrid%20cloud%20companies&highlight=true"
```
{: pre}

The JSON that is returned will be of the following format:

```json
{
   "highlight": {
     "extracted_metadata.title": [
       "IBM to Acquire Sanovi Technologies to Expand Disaster Recovery Services for <em>Hybrid</em> <em>Cloud</em>"
       ],
     "enriched_text.concepts.text": [
       "Privately held <em>company</em>",
       "<em>Cloud</em> computing"
       ],
     "text": [
       " Sanovi Technologies, a privately held <em>company</em> that provides <em>hybrid</em> <em>cloud</em> recovery, <em>cloud</em> migration",
       "IBM to Acquire Sanovi Technologies to Expand Disaster Recovery Services for <em>Hybrid</em> <em>Cloud</em>\n\nPublished",
       " undergoing digital and <em>hybrid</em> <em>cloud</em> transformation.\n\nURL: http://www.ibm.com/press/us/en/pressrelease/50837.wss",
       " and business continuity software for enterprise data centers and <em>cloud</em> infrastructure. Adding"
       ],
     "enriched_text.categories.label": [
       "/business and industrial/<em>company</em>/bankruptcy"
       ],
     "enriched_text.entities.type": [
       "<em>Company</em>"
       ],
     "html": [
       " Technologies, a privately held <em>company</em> that provides <em>hybrid</em> <em>cloud</em>\n recovery, <em>cloud</em> migration and business",
       " Disaster Recovery Services for <em>Hybrid</em> <em>Cloud</em></title></head>\n<body>\n\n\n<p>Published: Thu, 27 Oct 2016 07:01",
       " digital and <em>hybrid</em> <em>cloud</em> transformation.</p>\n<p>URL: http://www.ibm.com/press/us/en/pressrelease/50837.wss</p>\n\n\n\n</body></html>",
       " continuity software for \nenterprise data centers and <em>cloud</em> infrastructure. Adding these \ncapabilities"
       ]
   }
}
```
{: codeblock}

## deduplicate
{: #deduplicate}

 A beta capability that excludes duplicate documents from {{site.data.keyword.discoverynewsfull}} collection query results based on the `title` field. See [Excluding duplicate documents from query results](/docs/services/discovery?topic=discovery-query-parameters#deduplication).

### deduplicate.field
{: #deduplicate_field}

A beta capability that excludes duplicate documents from your query results based on the specified `{field}`. See [Excluding duplicate documents from query results](/docs/services/discovery?topic=discovery-query-parameters#deduplication).

### Excluding duplicate documents from query results
{: #deduplication}

If you are querying the {{site.data.keyword.discoverynewsfull}} collection, or your private data collection contains multiple identical (or near-identical) documents, you can exclude most of them from your query results using document deduplication.

**Note:** Document deduplication is currently supported only as a beta capability. See [Beta features](/docs/services/discovery?topic=discovery-release-notes#beta-features) in the Release notes for more information. This beta feature is currently supported in English only, see [Language support](/docs/services/discovery?topic=discovery-language-support#feature-support) for details.

**Note:**  Each query is deduplicated independently, so deduplication across offsets is not supported.

Deduplication is performed after `passages` are extracted and aggregations are calculated, so if you include the `passages` parameter in your query, passages will be returned from all documents in the query results, before deduplication. If you run an aggregation and query together, the aggregation results will include data from all documents returned, before deduplication.

Deduplication is performed on returned fields only. If you choose to specify the `return=` in your query, include the field you are deduplicating on.

To apply deduplication, use the following syntax in your query.  Replace `{field}` with the name of the field you wish to deduplicate on. The specified `{field}` must be a string, such as `title`.

```
&deduplicate.field={field}
```
{: codeblock}

When deduplicating, the JSON response includes `"duplicates_removed": x`, where `x` is the number of documents removed from the results.

#### Deduplicating documents in Watson Discovery News
{: #deduplicatewds}

News articles may be syndicated to several news outlets and {{site.data.keyword.discoverynewsfull}} will pick up each of them, resulting in duplicate articles. This means that a query to {{site.data.keyword.discoverynewsfull}} may potentially return several identical or nearly identical articles in query results. Using deduplication will remove most duplicate articles from your search queries.

{{site.data.keyword.discoveryshort}} deduplicates by using approximate matching on the `title` field and therefore a field doesn't need to be specified.

To apply deduplication, use the following parameter in your query. This query automatically deduplicates on the `title` field in {{site.data.keyword.discoverynewsfull}}.

```bash
&deduplicate=true
```
{: codeblock}

If you prefer to deduplicate on a field other than `title`, use the following syntax in your query. Replace `{field}` with the name of the field you wish to deduplicate on. The specified `{field}` must be a string.

```bash
&deduplicate.field={field}
```
{: codeblock}

## collection_ids
{: #collection_ids}

A comma-separated list of collections in the same environment that will be queried. This parameter is only valid when using the `environments/{environment_id}/query?` method. See [Querying multiple collections](/docs/services/discovery?topic=discovery-query-concepts#multiple-collections) for more information.

```bash
&collection_ids={id1},{id2}
```
{: codeblock}

## similar
{: #similar}

Document similarity identifies documents that are similar to the documents listed in the `similar.document_ids` parameters. This can be further refined by specifing which fields will be considered for comparison using the `similar.fields` parameters. The default is `false`. See [Document similarity](/docs/services/discovery?topic=discovery-query-concepts#doc-similarity) for more information.

```bash
&similar=true
```
{: codeblock}

### similar.document_ids
{: #similar_document_ids}

A comma-separated list of document IDs that will be used as a basis for finding similar documents as results. This parameter is required if the `similar` parameter is set to `true`.

```bash
&similar.document_ids={id1},{id2}
```
{: codeblock}

### similar.fields
{: #similar_fields}

An optional, comma-separated list of fields that will be used to compare documents to find similar documents. This parameter can only be used in conjunction with the `similar.document_ids` parameter.

```bash
&similar.fields={field1},{field2}
```
{: codeblock}
