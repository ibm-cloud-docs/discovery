---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-04"

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

# 查询参考
{: #query-reference}

{{site.data.keyword.discoveryfull}} 服务通过查询提供强大的内容搜索功能。通过 {{site.data.keyword.discoveryshort}} 服务上传并扩充内容后，可以构建查询，将 {{site.data.keyword.discoveryshort}} 集成到您自己的项目中，或者使用 {{site.data.keyword.watson}} Explorer Application Builder 来创建定制应用程序。
{: shortdesc}

有关编写查询的更多信息，请参阅：
- [查询入门](/docs/services/discovery/getting-started-query.html)
- [查询概念](/docs/services/discovery/using.html)

## 参数描述
{: #parameter-descriptions}

通过查询参数，可以搜索集合，识别结果集以及对结果集执行分析。


|参数|描述|示例|
|:-------------------:|------------------------------------------------------------|--------------------------------|
|**搜索参数**|  |  |
|[query](/docs/services/discovery/query-parameters.html#query) |用于匹配文档的已排名的查询语言搜索。|`query=bees` |
|[filter](/docs/services/discovery/query-parameters.html#filter) |用于匹配文档的未排名的查询语言搜索。|`filter=bees` |
|[natural_language_query](/docs/services/discovery/query-parameters.html#nlq) |用于匹配文档的已排名的自然语言搜索。|`natural_language_query="How do bees fly"` |
|[aggregation](/docs/services/discovery/query-parameters.html#aggregation) |结果集的统计查询|`aggregation=term(enriched_text.entities.type)` |
|**结构参数**| | |
|[count](/docs/services/discovery/query-parameters.html#count) |要返回的 `result` 文档数。|`count=15` |
|[offset](/docs/services/discovery/query-parameters.html#offset) |从结果集返回 `result` 文档之前要忽略的结果数|`offset=100` |
|[return](/docs/services/discovery/query-parameters.html#return) |要返回的字段列表|`return=title,url` |
|[sort](/docs/services/discovery/query-parameters.html#sort) |要据以对结果集排序的字段|`sort=enriched_text.sentiment.document.score` |
| [bias](/docs/services/discovery/query-parameters.html#bias)|要据以对结果集进行偏差调整的字段|`bias=publication_date`|
|[passages.fields](/docs/services/discovery/query-parameters.html#passages_fields) |要从中抽取段落的字段|`passages=true&passages.fields=text,abstract,conclusion` |
|[passages.count](/docs/services/discovery/query-parameters.html#passages_count) |要返回的段落数|`passages=true&passages.count=6`|
|[passages.characters](/docs/services/discovery/query-parameters.html#passages_characters) |段落长度|`passages=true&passages.characters=144`|
|[highlight](/docs/services/discovery/query-parameters.html#highlight) |突出显示查询匹配项|`highlight=true` |
|[deduplicate](/docs/services/discovery/query-parameters.html#deduplicate) |对 {{site.data.keyword.discoverynewsfull}} 返回的结果执行去重|`deduplicate=true` |
|[deduplicate.field](/docs/services/discovery/query-parameters.html#deduplicate_field)|根据字段对返回的结果执行去重|`deduplicate.field=title` |
|[collection_ids](/docs/services/discovery/query-parameters.html#collection_ids) |查询多个集合|`collection_ids={1},{2},{3}` |
|[similar](/docs/services/discovery/query-parameters.html#similar)|启用类似文档查找|`similar=true`|
|[similar.document_ids](/docs/services/discovery/query-parameters.html#similar_document_ids)|要查找与其类似的文档的文档|`similar.document_ids={id1},{id2}`|
|[similar.fields](/docs/services/discovery/query-parameters.html#similar_fields)|查找类似文档时要比较的字段|`similar.fields=text,title`|

### 查询限制

不能查询包含以下内容的字段名称：
- 后缀中包含数字字符 (`0 - 9`) 的字段名称（例如，`extracted-content2`）。
- 前缀中包含字符 `_`、`+` 和 `-` 的 `field_name`（例如，`+extracted-content`）。
- 包含字符 `.`、`,` 和 `:` 的 `field_name`（例如，`new:extracted-content`）。

## 运算符
{: #operators}

运算符是一个查询中不同部分之间的分隔符。下面是可用的运算符：

|运算符|描述|示例|
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [.](/docs/services/discovery/query-operators.html#delimiter) |JSON 定界符|`enriched_text.concepts.text` |
| [:](/docs/services/discovery/query-operators.html#includes) |包含|`text:computer` |
| [::](/docs/services/discovery/query-operators.html#match) |完全匹配|`title::"Query building"`|
| [:!](/docs/services/discovery/query-operators.html#notinclude) |不包含|`text:!computer` |
| [::!](/docs/services/discovery/query-operators.html#notamatch) |不完全匹配|`text::!winter`|
| [\\](/docs/services/discovery/query-operators.html#escape) |转义字符|`title::"Dorothy said: \"There's no place like home\""`|
| [""](/docs/services/discovery/query-operators.html#phrase) |短语查询|`enriched_text.concepts.text:"IBM Watson"` |
| [(), \[\]](/docs/services/discovery/query-operators.html#nestedquery) |嵌套分组|`filter-entities:(text:Turkey,type:Location)` |
|[<code>&#124;</code>](/docs/services/discovery/query-operators.html#or) |或|<code>query-enriched.entities.text:Google&#124;IBM</code> |
| [,](/docs/services/discovery/query-operators.html#and) |和|`query-enriched.entities.text:Google,IBM` |
| [<=, >=, >, <](/docs/services/discovery/query-operators.html#comparisons) |数字比较|`enriched_text.sentiment.document.score>0.679`     |
| [^x](/docs/services/discovery/query-operators.html#multiplier) |分数乘数|`text:IBM^3` |
| [*](/docs/services/discovery/query-operators.html#wildcard) |通配符|`query-enriched_text.concepts.text:pre*` |
|[~n](/docs/services/discovery/query-operators.html#variation) |字符串变体|`query-enriched_text.entities.text:cat~1` |
| [:*](/docs/services/discovery/query-operators.html#exists) |存在|`title:*`|
| [!*](/docs/services/discovery/query-operators.html#dnexist) |不存在|`title!*`|

## 聚集
{: #aggregations}

聚集用于返回一组数据值。下面是可用的聚集：

|聚集|描述|示例|
|:-------------------:|------------------------------------------------------------|--------------------------------|
|[term](/docs/services/discovery/query-aggregations.html#term) |完全相同值的计数|`term(enriched_text.concepts.text,count:10)` |
|[filter](/docs/services/discovery/query-aggregations.html#filter) |按定义的模式过滤结果集|`filter(enriched_text.concepts.text:cloud computing)`
|[nested](/docs/services/discovery/query-aggregations.html#nested) |限制聚集|`nested(enriched_text.entities)` |
|[histogram](/docs/services/discovery/query-aggregations.html#histogram) |基于区间的分布|`histogram(product.price,interval:1)` |
|[timeslice](/docs/services/discovery/query-aggregations.html#timeslice) |基于时间的分布|`timeslice(last_modified,2day,America/New York)` |
|[top_hits](/docs/services/discovery/query-aggregations.html#top_hits) |当前聚集的排名靠前的结果文档|`term(enriched_text.concepts.text).top_hits(10)` |
|[unique_count](/docs/services/discovery/query-aggregations.html#unique_count) |聚集中字段的唯一值计数|`unique_count(enriched_text.entities.type)` |
|[max](/docs/services/discovery/query-aggregations.html#max)|结果集内指定字段的最大值。|`max(product.price)` |
|[min](/docs/services/discovery/query-aggregations.html#min)|结果集内指定字段的最小值。|`min(product.price)` |
|[average](/docs/services/discovery/query-aggregations.html#average) |结果集内指定字段的平均值。|`average(product.price)` |
|[sum](/docs/services/discovery/query-aggregations.html#sum) |结果集内所有字段之和。|`sum(product.price)` |
