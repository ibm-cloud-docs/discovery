---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-04"

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

# 查询参数
{: #query-parameters}

{{site.data.keyword.discoveryfull}} 服务通过查询提供强大的内容搜索功能。通过 {{site.data.keyword.discoveryshort}} 服务上传并扩充内容后，可以构建查询，将 {{site.data.keyword.discoveryshort}} 集成到您自己的项目中，或者使用 {{site.data.keyword.watson}} Explorer Application Builder 来创建定制应用程序。要开始使用查询，请参阅[查询概念](/docs/services/discovery?topic=discovery-query-concepts#query-concepts)。有关参数的完整列表，请参阅[查询参考](/docs/services/discovery?topic=discovery-query-reference#parameter-descriptions)。
{: shortdesc}

**搜索参数**

通过搜索参数，可以搜索集合，识别结果集以及对结果集执行分析。

**结果集**是由搜索参数的组合搜索所识别到的文档组。结果集可能比返回的结果大得多。如果执行空查询，那么结果集将为集合中的所有文档。

## query
{: #query}

查询搜索将按相关性顺序返回数据集内的所有文档，包括完整扩充项和完整文本。查询还会排除未提及查询内容的所有文档。这些查询使用 [{{site.data.keyword.discoveryshort}} Query Language](/docs/services/discovery?topic=discovery-query-operators#query-operators) 进行编写。

## filter
{: #filter}

可高速缓存的查询，用于排除未提及查询内容的所有文档。过滤器搜索结果**不会**按相关性顺序返回。这些查询使用 [{{site.data.keyword.discoveryshort}} Query Language](/docs/services/discovery?topic=discovery-query-operators#query-operators) 进行编写。

### filter 与 query 参数的差异
{: #filtervquery}

如果对小型数据集测试同一搜索项，您可能会发现 `filter` 和 `query` 参数返回的结果非常类似（就算不完全相同）。但是，这两个参数还是有差异的。

- 仅使用 filter 参数将返回无特定顺序的搜索结果。
- 仅使用 query 参数将按相关性顺序返回搜索结果。

在大型数据集内，如果需要按相关性顺序返回结果，那么应该组合使用 `filter` 和 `query` 参数，因为将这两个参数一起使用可提高性能。这是因为 `filter` 参数将首先运行并高速缓存结果，然后 `query` 参数将对结果排名。有关将 filter 和 query 一起使用的示例，请参阅[构建组合查询](/docs/services/discovery?topic=discovery-query-concepts#building-combined-queries)。还可以在 aggregation 中使用 filter。

编写同时包含一个 `filter` 参数和一个 `aggregation`、`query` 或 `natural_language_query` 参数的查询时，`filter` 参数首先运行，在此之后，所有 `aggregation`、`query` 或 `natural_language_query` 参数都以并行方式运行。

对于简单查询，尤其是对小型数据集的查询，`filter` 和 `query` 通常会返回完全相同（或类似）的结果。如果 `filter` 和 `query` 调用返回类似的结果，并且是否按相关性顺序获得响应无关紧要，那么最好使用 filter，因为 filter 调用速度更快，并且会进行高速缓存。高速缓存意味着下次发出该调用时，获得响应的速度要快得多，在大型数据集内尤为明显。

## aggregation
{: #aggregation}

聚集查询会返回与一组数据值相匹配的文档的计数；例如，排名靠前的关键字、实体的总体观点等。要获取聚集选项的完整列表，请参阅[聚集表](/docs/services/discovery?topic=discovery-query-aggregations#query-aggregations)。这些聚集使用 [{{site.data.keyword.discoveryshort}} Query Language](/docs/services/discovery?topic=discovery-query-operators#query-operators) 进行编写。

## natural_language_query
{: #nlq}

自然语言查询支持执行以自然语言表达的查询，这可能是从会话式或自由文本界面中的最终用户那里收到的查询 - 例如："IBM Watson in healthcare"。此参数将整个输入用作查询文本。此参数**不会**识别运算符。`natural_language_query` 参数会启用段落搜索和相关性训练等功能。在大多数情况下，所有专用集合将在查询结果中返回`置信度`分数。请参阅[置信度分数](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence)以获取详细信息。自然语言查询的最大查询字符串长度为 `2048`。

**结构参数**

结构参数用于在返回的 JSON 中定义文档的内容和组织。这包括重新调整的结果数、在结果集内要开始返回文档的位置、结果集的排序方式、对于每个文档要返回的字段、是否应该除去重复文档，以及是否应该从结果集抽取相关段落。结构参数不会影响哪些文档属于整个结果集的一部分。

## count
{: #count}

您希望在响应中返回的文档数。缺省值为 `10`。在任一查询中，`count` 和 `offset` 值加起来的最大值都为 `10000`。

## offset
{: #offset}

要在开头跳过的查询结果数。例如，如果返回的结果总数为 10，而 offset 为 8，那么将返回最后两个结果。缺省值为 `0`。在任一查询中，`count` 和 `offset` 值加起来的最大值都为 `10000`。

## return
{: #return}

要返回的文档层次结构部分的逗号分隔列表。文档层次结构的任何部分都是有效值。

## sort
{: #sort}

文档中要对其排序的字段的逗号分隔列表。您可以选择通过为字段添加 `-`（表示降序）或 `+`（表示升序）前缀来指定排序方向。升序是缺省排序方向。

目前，`sort` 参数仅可用于 API；不可通过工具使用。

## bias
{: #bias}

调整搜索结果以偏向于特定结果，例如最近发布的文档。`bias` 必须设置为 `date` 类型字段或 `number` 类型字段，例如 `bias=publication_date` 或 `bias=field_1`。指定 `date` 类型字段时，返回的结果将偏向于更接近当前日期的字段值。指定 `number` 类型字段时，返回的结果将偏向于更高的字段值。此参数不能与 `sort` 参数在同一查询中使用。

目前，`bias` 参数仅可用于 API；不可通过工具使用。

## passages
{: #passages}

布尔值，用于指定服务是否从使用 `natural_language_query` 参数的查询所返回文档中返回一组最相关的段落。这些段落通过复杂的 Watson 算法生成，用于确定查询所返回的所有文档中最佳的文本段落。缺省值为 `false`。

`passages` 参数只能用于专用集合。不能用于 {{site.data.keyword.discoverynewsfull}} 集合。
{: tip}

{{site.data.keyword.discoveryshort}} 尝试使用语句边界检测来返回从语句起始处开始并在语句结尾处停止的段落。为此，它会首先搜索长度大致为 [`passages.characters` 参数](/docs/services/discovery?topic=discovery-query-parameters#passages_characters)（缺省值为 `400`）中所指定长度的段落。然后，它将每个段落扩展至两倍于指定长度的限制，以便返回完整的语句。当 `passages.characters` 参数指定的长度较短和/或文档中的语句非常长时，如果不扩展至所请求长度的两倍以上，那么可能没有足够接近的语句边界，从而无法返回完整语句。在这种情况下，{{site.data.keyword.discoveryshort}} 会保持在两倍于 `passages.characters` 参数的限制范围内，因此返回的段落不会包含整个语句，并会省略开头和/或结尾。

由于语句边界调整可扩大段落大小，因此您将看到平均段落长度明显增加。如果应用程序限制了屏幕空间，那么您可能要为 `passages.characters` 设置较小的值和/或截断 {{site.data.keyword.discoveryshort}} 返回的段落。语句边界检测适用于所有支持的语言，并使用特定于语言的逻辑。

`passages` 参数会返回匹配的段落 (`passage_text`)，另外还会返回 `score`、`document_id`、从中抽取段落的字段的名称 (`field`)，以及该字段内段落文本的起始和结束字符（`start_offset` 和 `end_offset`），如以下示例中所示。该查询显示在示例的顶部。

```bash
 curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-06-25&natural_language_query='Hybrid%20cloud%20companies'&passages=true"
```
{: pre}

返回的 JSON 格式如下：

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

索引中将从中抽出段落的字段的逗号分隔列表。如果未指定此参数，那么将包含所有顶级字段。

### passages.count
{: #passages_count}

要返回的最大段落数。如果这是找到的段落总数，搜索将返回少于最大值的段落数。缺省值为 `10`。最大值为 `100`。

### passages.characters
{: #passages_characters}

任一段落应该具有的大致字符数。缺省值为 `400`。最小值为 `50`。最大值为 `2000`。返回的段落可能最大为所请求长度的两倍（如果需要），以使其在语句边界开始和结束。

## highlight
{: #highlight}

布尔值，用于指定返回的输出是否包含 `highlight` 对象，其中键是字段名称，值是包含 HTML`*` 标记所突出显示的查询匹配文本分段的数组。

输出将在 `enriched_text` 对象后面列出 `highlight` 对象，如以下示例中所示。

```bash
curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-06-25&natural_language_query=Hybrid%20cloud%20companies&highlight=true"
```
{: pre}

返回的 JSON 格式如下：

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

## 去重
{: #deduplicate}

 这是一个 Beta 功能，用于根据 `title` 字段从 {{site.data.keyword.discoverynewsfull}} 集合查询结果中排除重复文档。请参阅[从查询结果中排除重复文档](/docs/services/discovery?topic=discovery-query-parameters#deduplication)。

### deduplicate.field
{: #deduplicate_field}

这是一个 Beta 功能，用于根据指定的 `{field}` 从查询结果中排除重复文档。请参阅[从查询结果中排除重复文档](/docs/services/discovery?topic=discovery-query-parameters#deduplication)。

### 从查询结果中排除重复文档
{: #deduplication}

如果要查询 {{site.data.keyword.discoverynewsfull}} 集合，或者专用数据集合包含多个完全相同（或接近完全相同）的文档，那么可以使用文档去重功能将其中大部分重复文档排除在查询结果之外。

**注：**目前，文档去重仅作为 Beta 功能受支持。请参阅发行说明中的 [Beta 功能](/docs/services/discovery?topic=discovery-release-notes#beta-features)以获得更多信息。此 Beta 功能当前仅支持英语版本，请参阅[语言支持](/docs/services/discovery?topic=discovery-language-support#feature-support)以获取详细信息。

**注：**将对每个查询独立去重，因此不支持跨偏移量去重。

去重将在抽取 `passages` 并计算聚集之后执行，因此如果在查询中包含 `passages` 参数，那么将在去重之前，从查询结果中的所有文档返回段落。如果同时运行聚集和查询，那么聚集结果将在去重之前包含返回的所有文档中的数据。

去重仅对返回的字段执行。如果选择在查询中指定 `return=`，请包含要对其执行去重的字段。

要应用去重，请在查询中使用以下语法。将 `{field}` 替换为要对其执行去重的字段的名称。指定的 `{field}` 必须是字符串，例如 `title`。

```
&deduplicate.field={field}
```
{: codeblock}

执行去重时，JSON 响应会包含 `"duplicates_removed": x`，其中 `x` 是从结果中除去的文档数。

#### 在 Watson Discovery News 中对文档去重
{: #deduplicatewds}

新闻文章可能会联合到多家新闻媒体，{{site.data.keyword.discoverynewsfull}} 会选取其中每家新闻媒体，因而会生成重复的文章。这意味着对 {{site.data.keyword.discoverynewsfull}} 的查询可能会在查询结果中返回多个完全相同或几乎完全相同的文章。使用去重功能将从搜索查询中除去大部分重复的文章。

{{site.data.keyword.discoveryshort}} 使用近似匹配对 `title` 字段执行去重，因此无需指定字段。

要应用去重，请在查询中使用以下参数。此查询将自动对 {{site.data.keyword.discoverynewsfull}} 中的 `title` 字段执行去重。

```bash
&deduplicate=true
```
{: codeblock}

如果您希望对除 `title` 以外的字段执行去重，请在查询中使用以下语法。将 `{field}` 替换为要对其执行去重的字段的名称。指定的 `{field}` 必须是字符串。

```bash
&deduplicate.field={field}
```
{: codeblock}

## collection_ids
{: #collection_ids}

将查询的同一环境中集合的逗号分隔列表。仅当使用 `environments/{environment_id}/query?` 方法时，此参数才有效。请参阅[查询多个集合](/docs/services/discovery?topic=discovery-query-concepts#multiple-collections)以获取更多信息。

```bash
&collection_ids={id1},{id2}
```
{: codeblock}

## similar
{: #similar}

文档相似度用于识别与 `similar.document_ids` 参数中列出的文档类似的文档。通过使用 `similar.fields` 参数指定将考虑哪些字段用于比较，可以进一步优化此值。缺省值为 `false`。请参阅[文档相似度](/docs/services/discovery?topic=discovery-query-concepts#doc-similarity)以获取更多信息。

```bash
&similar=true
```
{: codeblock}

### similar.document_ids
{: #similar_document_ids}

文档标识的逗号分隔列表，此列表将用作查找与结果类似的文档的基础。如果 `similar` 参数设置为 `true`，那么此参数是必需的。

```bash
&similar.document_ids={id1},{id2}
```
{: codeblock}

### similar.fields
{: #similar_fields}

可选的逗号分隔字段列表，用于比较文档以查找类似文档。此参数只能与 `similar.document_ids` 参数一起使用。

```bash
&similar.fields={field1},{field2}
```
{: codeblock}
