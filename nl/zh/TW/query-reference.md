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

# 查詢參考資料
{: #query-reference}

{{site.data.keyword.discoveryfull}} 服務透過查詢提供強大的內容搜尋功能。透過 {{site.data.keyword.discoveryshort}} 服務上傳及強化內容之後，您可以建置查詢，將 {{site.data.keyword.discoveryshort}} 整合至您自己的專案，或使用 {{site.data.keyword.watson}} Explorer Application Builder 來建立自訂應用程式。
{: shortdesc}

如需撰寫查詢的相關資訊，請參閱：
- [開始使用查詢](/docs/services/discovery?topic=discovery-getting-started-with-querying#getting-started-with-querying)
- [查詢概念](/docs/services/discovery?topic=discovery-query-concepts#query-concepts)

## 參數說明
{: #parameter-descriptions}

查詢參數可讓您搜尋集合、識別結果集，以及對結果集執行分析。


|參數 |說明|範例 |
|:-------------------:|------------------------------------------------------------|--------------------------------|
|**搜尋參數**|  |  |
|[query](/docs/services/discovery?topic=discovery-query-parameters#query) |針對相符文件進行的分級查詢語言搜尋。|`query=bees` |
|[filter](/docs/services/discovery?topic=discovery-query-parameters#filter) |針對相符文件進行的未分級查詢語言搜尋。|`filter=bees` |
|[natural_language_query](/docs/services/discovery?topic=discovery-query-parameters#nlq) |針對相符文件進行的分級自然語言搜尋。|`natural_language_query="How do bees fly"` |
|[aggregation](/docs/services/discovery?topic=discovery-query-parameters#aggregation) |結果集的統計查詢|`aggregation=term(enriched_text.entities.type)` |
|**結構參數** | | |
|[count](/docs/services/discovery?topic=discovery-query-parameters#count) |要傳回的 `result` 文件數。|`count=15` |
|[offset](/docs/services/discovery?topic=discovery-query-parameters#offset) |從結果集傳回 `result` 文件之前要忽略的結果數|`offset=100` |
|[return](/docs/services/discovery?topic=discovery-query-parameters#return) |要傳回的欄位清單|`return=title,url` |
|[sort](/docs/services/discovery?topic=discovery-query-parameters#sort) |用來排序結果集的欄位|`sort=enriched_text.sentiment.document.score` |
| [bias](/docs/services/discovery?topic=discovery-query-parameters#bias) | 用來偏移結果集的欄位 | `bias=publication_date` |
|[passages.fields](/docs/services/discovery?topic=discovery-query-parameters#passages_fields) |要從中擷取段落的欄位|`passages=true&passages.fields=text,abstract,conclusion` |
|[passages.count](/docs/services/discovery?topic=discovery-query-parameters#passages_count) |要傳回的段落數| `passages=true&passages.count=6` |
|[passages.characters](/docs/services/discovery?topic=discovery-query-parameters#passages_characters) |段落的長度| `passages=true&passages.characters=144` |
|[highlight](/docs/services/discovery?topic=discovery-query-parameters#highlight) |強調顯示查詢相符項|`highlight=true` |
|[deduplicate](/docs/services/discovery?topic=discovery-query-parameters#deduplicate) |刪除 {{site.data.keyword.discoverynewsfull}} 重複傳回的結果 |`deduplicate=true` |
| [deduplicate.field](/docs/services/discovery?topic=discovery-query-parameters#deduplicate_field) |根據欄位刪除重複傳回的結果|`deduplicate.field=title` |
|[collection_ids](/docs/services/discovery?topic=discovery-query-parameters#collection_ids) |查詢多個集合|`collection_ids={1},{2},{3}` |
| [similar](/docs/services/discovery?topic=discovery-query-parameters#similar) | 啟用類似文件尋找 | `similar=true` |
| [similar.document_ids](/docs/services/discovery?topic=discovery-query-parameters#similar_document_ids) | 要尋找其類似文件的文件 | `similar.document_ids={id1},{id2}` |
| [similar.fields](/docs/services/discovery?topic=discovery-query-parameters#similar_fields) | 尋找類似文件時要比較的欄位 | `similar.fields=text,title` |

### 查詢限制
{: #query-limitations}

您無法查詢包含下列項目的欄位名稱：
- 欄位名稱字尾中包含數字字元 (`0 - 9`)（例如 `extracted-content2`）。
- `field_name` 字首中包含 `_`、`+` 及 `-` 字元（例如 `+extracted-content`）。
- `field_name` 中包含 `.`、`,` 及 `:` 字元（例如 `new:extracted-content`）

## 運算子
{: #operators}

運算子是在查詢的不同部分之間的分隔字元。這些是可用的運算子：

|運算子 |說明|範例 |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [.](/docs/services/discovery?topic=discovery-query-operators#delimiter) |JSON 定界字元 |`enriched_text.concepts.text` |
| [:](/docs/services/discovery?topic=discovery-query-operators#includes) |包含 |`text:computer` |
| [::](/docs/services/discovery?topic=discovery-query-operators#match) |完全相符 | `title::"Query building"` |
| [:!](/docs/services/discovery?topic=discovery-query-operators#notinclude) |不包含 |`text:!computer` |
| [::!](/docs/services/discovery?topic=discovery-query-operators#notamatch) |不完全相符 | `text::!winter` |
| [\\](/docs/services/discovery?topic=discovery-query-operators#escape) |跳出字元 | `title::"Dorothy said: \"There's no place like home\""` |
| [""](/docs/services/discovery?topic=discovery-query-operators#phrase) |詞組查詢 |`enriched_text.concepts.text:"IBM Watson"` |
| [(), \[\]](/docs/services/discovery?topic=discovery-query-operators#nestedquery) |巢狀分組 |`filter-entities:(text:Turkey,type:Location)` |
|[<code>&#124;</code>](/docs/services/discovery?topic=discovery-query-operators#or) |或 |<code>query-enriched.entities.text:Google&#124;IBM</code> |
| [,](/docs/services/discovery?topic=discovery-query-operators#and) |及 |`query-enriched.entities.text:Google,IBM` |
| [<=, >=, >, <](/docs/services/discovery?topic=discovery-query-operators#comparisons) |數值比較 |`enriched_text.sentiment.document.score>0.679`     |
| [^x](/docs/services/discovery?topic=discovery-query-operators#multiplier) |評分乘數 |`text:IBM^3` |
| [*](/docs/services/discovery?topic=discovery-query-operators#wildcard) |萬用字元 |`query-enriched_text.concepts.text:pre*` |
|[~n](/docs/services/discovery?topic=discovery-query-operators#variation) |字串變異 |`query-enriched_text.entities.text:cat~1` |
| [:*](/docs/services/discovery?topic=discovery-query-operators#exists) | 存在 | `title:*` |
| [!*](/docs/services/discovery?topic=discovery-query-operators#dnexist) | 不存在 | `title!*` |

## 聚集
{: #aggregations}

聚集傳回一組資料值。這些是可用的聚集：

|聚集 |說明|範例 |
|:-------------------:|------------------------------------------------------------|--------------------------------|
|[term](/docs/services/discovery?topic=discovery-query-aggregations#term) |相同值計數|`term(enriched_text.concepts.text,count:10)` |
|[filter](/docs/services/discovery?topic=discovery-query-aggregations#aggfilter) |依定義的型樣過濾結果集 |`filter(enriched_text.concepts.text:cloud computing)`
|[nested](/docs/services/discovery?topic=discovery-query-aggregations#nested) |限制聚集 |`nested(enriched_text.entities)` |
|[histogram](/docs/services/discovery?topic=discovery-query-aggregations#histogram) |間隔型分佈 |`histogram(product.price,interval:1)` |
|[timeslice](/docs/services/discovery?topic=discovery-query-aggregations#timeslice) |時間型分佈 |`timeslice(last_modified,2day,America/New York)` |
|[top_hits](/docs/services/discovery?topic=discovery-query-aggregations#top_hits) |現行聚集的前幾個分級的結果文件 |`term(enriched_text.concepts.text).top_hits(10)` |
|[unique_count](/docs/services/discovery?topic=discovery-query-aggregations#unique_count) |聚集內欄位的唯一值計數 |`unique_count(enriched_text.entities.type)` |
| [max](/docs/services/discovery?topic=discovery-query-aggregations#max) |結果集內所指定欄位的最大值。 |`max(product.price)` |
| [min](/docs/services/discovery?topic=discovery-query-aggregations#min) |結果集內所指定欄位的最小值。 |`min(product.price)` |
|[average](/docs/services/discovery?topic=discovery-query-aggregations#average) |結果集內所指定欄位的平均值。 |`average(product.price)` |
|[sum](/docs/services/discovery?topic=discovery-query-aggregations#sum) |結果集內所有欄位的總和。 |`sum(product.price)` |
