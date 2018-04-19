---

copyright:
  years: 2015, 2018
lastupdated: "2018-04-13"

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

# Query reference

The {{site.data.keyword.discoveryfull}} service offers powerful content search capabilities through queries. After your content is uploaded and enriched by the {{site.data.keyword.discoveryshort}} service, you can build queries, integrate {{site.data.keyword.discoveryshort}} into your own projects, or create a custom application by using the {{site.data.keyword.watson}} Explorer Application Builder.
{: shortdesc}

For more information about writing queries, see:
- [Getting started with querying](/docs/services/discovery/getting-started-query.html)
- [Query concepts](/docs/services/discovery/using.html)

## Parameters descriptions
{: #parameter-descriptions}

Query parameters enable you to search your collection, identify a result set, and perform analysis on the result set.


| Parameter | Description | Example |
|:-------------------:|------------------------------------------------------------|--------------------------------|
|** Search parameters **|  |  |
| [query](/docs/services/discovery/query-parameters.html#query) | A ranked query language search for matching documents. | `query=bees` |
| [filter](/docs/services/discovery/query-parameters.html#filter) | An unranked query language search for matching documents. | `filter=bees` |
| [natural_language_query](/docs/services/discovery/query-parameters.html#nlq) | A ranked natural language search for matching documents | `natural_language_query="How do bees fly"` |
| [aggregation](/docs/services/discovery/query-parameters.html#aggregation) | A statistical query of the results set | `aggregation=term(enriched_text.entities.type)` |
| **Structure parameters** | | |
| [count](/docs/services/discovery/query-parameters.html#count) | The number of `result` documents to return. | `count=15` |
| [offset](/docs/services/discovery/query-parameters.html#offset) | The number of results to ignore before returning `result` documents from the results set | `offset=100` |
| [return](/docs/services/discovery/query-parameters.html#return) | List of fields to return | `return=title,url` |
| [sort](/docs/services/discovery/query-parameters.html#sort) | Field to sort results set by | `sort=enriched_text.sentiment.document.score` |
| [passages.fields](/docs/services/discovery/query-parameters.html#passages_fields) | Fields to extract passages from | `passages=true&passages.fields=text,abstract,conclusion` |
| [passages.count](/docs/services/discovery/query-parameters.html#passages_count) | Number of passages to return | `passages=true&passages.count=6` |
| [passages.characters](/docs/services/discovery/query-parameters.html#passages_characters) | Length of passages | `passages=true&passages.characters=144` |
| [highlight](/docs/services/discovery/query-parameters.html#highlight) | Highlight query matches | `highlight=true` |
| [deduplicate](/docs/services/discovery/query-parameters.html#deduplicate) | Deduplicate {{site.data.keyword.discoverynewsfull}} returned results | `deduplicate=true` |
| [deduplicate.field](/docs/services/discovery/query-parameters.html#deduplicated_field) | Deduplicate returned results based on field | `deduplicate.field=title` |
| [collection_ids](/docs/services/discovery/query-parameters.html#collection_ids) | Query multiple collections | `collection_ids={1},{2},{3}` |
| [similar](/docs/services/discovery/query-parameters.html#similar) | Enables the similar document finding | `similar=true` |
| [similar.document_ids](/docs/services/discovery/query-parameters.html#similar_document_ids) | Which documents to find similar documents to | `similar.document_ids={id1},{id2}` |
| [similar.fields](/docs/services/discovery/query-parameters.html#similar_fields) | Which fields to compare when finding similar documents | `similar.fields=text,title` |

### Query limitations

You cannot query on field names that contain the following:
- Numerical characters (`0 - 9`) in the suffix of the field name (for example `extracted-content2`).
- The characters `_`, `+`, and `-` in the prefix of the `field_name` (for example `+extracted-content`).
- The characters `.`, `,`, and `:` in the `field_name` (for example `new:extracted-content`)

## Operators
{: #operators}

Operators are the separators between different parts of a query. These are the available operators:

| Operator | Description | Example |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [.](/docs/services/discovery/query-operators.html#delimiter) | JSON delimiter | `enriched_text.concepts.text` |
| [:](/docs/services/discovery/query-operators.html#includes) | Includes | `text:computer` |
| [::](/docs/services/discovery/query-operators.html#match) | Exact match | `title::"Query building"` |
| [:!](/docs/services/discovery/query-operators.html#notinclude) | Does not include | `text:!computer` |
| [::!](/docs/services/discovery/query-operators.html#notamatch) | Not an exact match | `text::!winter` |
| [\\](/docs/services/discovery/query-operators.html#escape) | Escape character | `title::"Dorothy said: \"There's no place like home\""` |
| [""](/docs/services/discovery/query-operators.html#phrase) | Phrase query | `enriched_text.concepts.text:"IBM Watson"` |
| [(), \[\]](/docs/services/discovery/query-operators.html#nestedquery) | Nested grouping | `filter-entities:(text:Turkey,type:Location)` |
| [<code>&#124;</code>](/docs/services/discovery/query-operators.html#or) | or | <code>query-enriched.entities.text:Google&#124;IBM</code> |
| [,](/docs/services/discovery/query-operators.html#and) | and | `query-enriched.entities.text:Google,IBM` |
| [<=, >=, >, <](/docs/services/discovery/query-operators.html#comparisons) | Numerical comparisons |  `enriched_text.sentiment.document.score>0.679`     |
| [^x](/docs/services/discovery/query-operators.html#multiplier) | Score multiplier | `text:IBM^3` |
| [*](/docs/services/discovery/query-operators.html#wildcard) | Wildcard | `query-enriched_text.concepts.text:pre*` |
| [~n](/docs/services/discovery/query-operators.html#variation) | String variation | `query-enriched_text.entities.text:cat~1` |

## Aggregations
{: #aggregations}

Aggregations return a set of data values. These are the available aggregations:

| Aggregation | Description | Example |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [term](/docs/services/discovery/query-aggregations.html#term) | Count of identical values | `term(enriched_text.concepts.text,count:10)` |
| [filter](/docs/services/discovery/query-aggregations.html#filter) | Filter results set to defined pattern | `filter(enriched_text.concepts.text:cloud computing)`
| [nested](/docs/services/discovery/query-aggregations.html#nested) | Restrict aggregation | `nested(enriched_text.entities)` |
| [histogram](/docs/services/discovery/query-aggregations.html#histogram) | Interval based distribution | `histogram(product.price,interval:1)` |
| [timeslice](/docs/services/discovery/query-aggregations.html#timeslice) | Time base distribution | `timeslice(last_modified,2day,America/New York)` |
| [top_hits](/docs/services/discovery/query-aggregations.html#top_hits) | Top ranked results documents for the current aggregation | `term(enriched_text.concepts.text).top_hits(10)` |
| [unique_count](/docs/services/discovery/query-aggregations.html#unique_count) | Count of unique values for a field within an aggregation | `unique_count(enriched_text.entities.type)` |
| [max](/docs/services/discovery/query-aggregations.html#min) | Maximum value for the specified field in the results set. | `max(product.price)` |
| [min](/docs/services/discovery/query-aggregations.html#max) | Minimum value for the specified field in the results set. | `min(product.price)` |
| [average](/docs/services/discovery/query-aggregations.html#average) |Mean value for the specified field in the results set. | `average(product.price)` |
| [sum](/docs/services/discovery/query-aggregations.html#sum) | Sum of all fields in the results set. | `sum(product.price)` |
