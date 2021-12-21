---

copyright:
  years: 2015, 2021
lastupdated: "2021-10-20"

subcollection: discovery

---

{{site.data.keyword.attribute-definition-list}}

# Query reference
{: #query-reference}

{{site.data.keyword.discoveryfull}} offers powerful content search capabilities through queries. After your content is uploaded and enriched by {{site.data.keyword.discoveryshort}}, you can build queries, integrate {{site.data.keyword.discoveryshort}} into your own projects, or create a custom application by using the {{site.data.keyword.watson}} Explorer Application Builder.
{: shortdesc}

For more information about writing queries, see:
- [Getting started with querying](/docs/discovery?topic=discovery-getting-started-with-querying)
- [Query concepts](/docs/discovery?topic=discovery-query-concepts)

## Parameters descriptions
{: #parameter-descriptions}

Query parameters enable you to search your collection, identify a result set, and perform analysis on the result set.


| Parameter | Description | Example |
|:-------------------:|------------------------------------------------------------|--------------------------------|
|** Search parameters **|  |  |
| [query](/docs/discovery?topic=discovery-query-parameters#query) | A ranked query language search for matching documents. | `query=bees` |
| [filter](/docs/discovery?topic=discovery-query-parameters#filter) | An unranked query language search for matching documents. | `filter=bees` |
| [natural_language_query](/docs/discovery?topic=discovery-query-parameters#nlq) | A ranked natural language search for matching documents | `natural_language_query="How do bees fly"` |
| [aggregation](/docs/discovery?topic=discovery-query-parameters#aggregation) | A statistical query of the results set | `aggregation=term(enriched_text.entities.type)` |
| **Structure parameters** | | |
| [count](/docs/discovery?topic=discovery-query-parameters#count) | The number of `result` documents to return. | `count=15` |
| [offset](/docs/discovery?topic=discovery-query-parameters#offset) | The number of results to ignore before returning `result` documents from the results set | `offset=100` |
| [return](/docs/discovery?topic=discovery-query-parameters#return) | List of fields to return | `return=title,url` |
| [sort](/docs/discovery?topic=discovery-query-parameters#sort) | Field to sort results set by | `sort=enriched_text.sentiment.document.score` |
| [bias](/docs/discovery?topic=discovery-query-parameters#bias) | Field to bias results set by | `bias=publication_date` |
| [passages.fields](/docs/discovery?topic=discovery-query-parameters#passages_fields) | Fields to extract passages from | `passages=true&passages.fields=text,abstract,conclusion` |
| [passages.count](/docs/discovery?topic=discovery-query-parameters#passages_count) | Number of passages to return | `passages=true&passages.count=6` |
| [passages.characters](/docs/discovery?topic=discovery-query-parameters#passages_characters) | Length of passages | `passages=true&passages.characters=144` |
| [highlight](/docs/discovery?topic=discovery-query-parameters#highlight) | Highlight query matches | `highlight=true` |
| [deduplicate](/docs/discovery?topic=discovery-query-parameters#deduplicate) | Deduplicate {{site.data.keyword.discoverynewsfull}} returned results | `deduplicate=true` |
| [deduplicate.field](/docs/discovery?topic=discovery-query-parameters#deduplicate_field) | Deduplicate returned results based on field | `deduplicate.field=title` |
| [collection_ids](/docs/discovery?topic=discovery-query-parameters#collection_ids) | Query multiple collections | `collection_ids={1},{2},{3}` |
| [similar](/docs/discovery?topic=discovery-query-parameters#similar) | Enables the similar document finding | `similar=true` |
| [similar.document_ids](/docs/discovery?topic=discovery-query-parameters#similar_document_ids) | Which documents to find similar documents to | `similar.document_ids={id1},{id2}` |
| [similar.fields](/docs/discovery?topic=discovery-query-parameters#similar_fields) | Which fields to compare when finding similar documents | `similar.fields=text,title` |

### Query limitations
{: #query-limitations}

You cannot query on field names that contain the following:
- Numerical characters (`0 - 9`) in the suffix of the field name (for example `extracted-content2`).
- The characters `_`, `+`, and `-` in the prefix of the `field_name` (for example `+extracted-content`).
- The characters `.`, `,`, and `:` in the `field_name` (for example `new:extracted-content`)

## Operators
{: #operators}

<!-- Learn more topic WDS -->
Operators are the separators between different parts of a query. These are the available operators:

| Operator | Description | Example |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [.](/docs/discovery?topic=discovery-query-operators#delimiter) | JSON delimiter | `enriched_text.concepts.text` |
| [:](/docs/discovery?topic=discovery-query-operators#includes) | Includes | `text:computer` |
| [::](/docs/discovery?topic=discovery-query-operators#match) | Exact match | `title::"Query building"` |
| [:!](/docs/discovery?topic=discovery-query-operators#notinclude) | Does not include | `text:!computer` |
| [::!](/docs/discovery?topic=discovery-query-operators#notamatch) | Not an exact match | `text::!winter` |
| [\\](/docs/discovery?topic=discovery-query-operators#escape) | Escape character | `title::"Dorothy said: \"There's no place like home\""` |
| [""](/docs/discovery?topic=discovery-query-operators#phrase) | Phrase query | `enriched_text.concepts.text:"IBM Watson"` |
| [(), \[\]](/docs/discovery?topic=discovery-query-operators#nestedquery) | Nested grouping | `filter-entities:(text:Turkey,type:Location)` |
| [<code>&#124;</code>](/docs/discovery?topic=discovery-query-operators#or) | or | <code>query-enriched.entities.text:Google&#124;IBM</code> |
| [,](/docs/discovery?topic=discovery-query-operators#and) | and | `query-enriched.entities.text:Google,IBM` |
| [<=, >=, >, <](/docs/discovery?topic=discovery-query-operators#comparisons) | Numerical comparisons |  `enriched_text.sentiment.document.score>0.679`     |
| [^x](/docs/discovery?topic=discovery-query-operators#multiplier) | Score multiplier | `text:IBM^3` |
| [*](/docs/discovery?topic=discovery-query-operators#wildcard) | Wildcard | `query-enriched_text.concepts.text:pre*` |
| [~n](/docs/discovery?topic=discovery-query-operators#variation) | String variation | `query-enriched_text.entities.text:cat~1` |
| [:*](/docs/discovery?topic=discovery-query-operators#exists) | Exists | `title:*` |
| [!*](/docs/discovery?topic=discovery-query-operators#dnexist) | Does not exist | `title:!*` |

## Aggregations
{: #aggregations}

Aggregations return a set of data values. These are the available aggregations:

| Aggregation | Description | Example |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [term](/docs/discovery?topic=discovery-query-aggregations#term) | Count of identical values | `term(enriched_text.concepts.text,count:10)` |
| [filter](/docs/discovery?topic=discovery-query-aggregations#aggfilter) | Filter results set to defined pattern | `filter(enriched_text.concepts.text:cloud computing)`
| [nested](/docs/discovery?topic=discovery-query-aggregations#nested) | Restrict aggregation | `nested(enriched_text.entities)` |
| [histogram](/docs/discovery?topic=discovery-query-aggregations#histogram) | Interval based distribution | `histogram(product.price,interval:1)` |
| [timeslice](/docs/discovery?topic=discovery-query-aggregations#timeslice) | Time base distribution | `timeslice(last_modified,2day,America/New York)` |
| [top_hits](/docs/discovery?topic=discovery-query-aggregations#top_hits) | Top ranked results documents for the current aggregation | `term(enriched_text.concepts.text).top_hits(10)` |
| [unique_count](/docs/discovery?topic=discovery-query-aggregations#unique_count) | Count of unique values for a field within an aggregation | `unique_count(enriched_text.entities.type)` |
| [max](/docs/discovery?topic=discovery-query-aggregations#max) | Maximum value for the specified field in the results set. | `max(product.price)` |
| [min](/docs/discovery?topic=discovery-query-aggregations#min) | Minimum value for the specified field in the results set. | `min(product.price)` |
| [average](/docs/discovery?topic=discovery-query-aggregations#average) |Mean value for the specified field in the results set. | `average(product.price)` |
| [sum](/docs/discovery?topic=discovery-query-aggregations#sum) | Sum of all fields in the results set. | `sum(product.price)` |
