---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-09"

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

# 查询聚集
{: #query-aggregations}

聚集用于返回一组数据值。有关可用聚集的完整列表，请参阅[查询参考](/docs/services/discovery?topic=discovery-query-reference#aggregations)。

## term
{: #term}

返回所选扩充项的排名靠前的值（按分数和按频率）。所有扩充项都是有效值。您可以选择使用 `count` 来指定要返回的 term 数。`count` 参数的缺省值为 10。以下示例会返回包含概念扩充项的排名靠前的值的完整文本和扩充项，并指定返回 10 个 term。

例如：
```bash
term(enriched_text.concepts.text,count:10)
```
{: codeblock}

## filter
{: #aggfilter}

一种修饰符，用于缩小位于其后面的聚集查询的文档集范围。以下示例会将过滤结果范围缩小至包含 Cloud computing 概念的一组文档。

例如：
```bash
filter(enriched_text.concepts.text:"cloud computing")
```
{: codeblock}

## nested
{: #nested}

在聚集查询之前应用 nested，可将聚集限制为指定的结果区域。例如：`nested(enriched_text.entities)` 表示仅对任何结果的 `enriched_text.entities` 组成部分进行聚集。

例如：
```bash
nested(enriched_text.entities)
```
{: codeblock}

## histogram
{: #histogram}

创建数字间隔分段来对文档进行分类。使用单个数字字段中的字段值来描述类别。用于创建 histogram 的字段必须是数字（`integer`、`float`、`double` 或 `date`）类型。不支持非数字类型，如 `string`。例如，"price": 1.30 是有效的数字值，而 "price": "1.30" 是字符串，所以此值无效。`interval` 自变量用于定义将结果拆分成的部分的大小。interval 值必须为非负整数，并且应设置为适当的值，以便可以对可能的字段值进行分段。例如，如果您的数据集包含若干商品的价格，如："price": 1.30、"price": 1.99 和 "price": 2.99，那么可以将 interval 设置为 1，这样所有价格就都能划分到 1 与 2 和 2 与 3 的分段中。您可能不会将 interval 设置为 100，因为这样所有数据就都会位于同一个分段中。histogram 可以处理小数值，但 interval 必须为整数。语法为 `histogram(<field>,<interval>)`，如以下示例所示。

例如：
```bash
histogram(product.price,interval:1)
```
{: codeblock}

## timeslice
{: #timeslice}

一种使用日期创建间隔分段的专用 histogram。有效的日期时间间隔值为 `second/seconds`、`minute/minutes`、`hour/hours`、`day/days`、`week/weeks`、`month/months` 和 `year/years`。语法为 `timeslice(<field>,<interval>,<time_zone>)`. 要使用 `timeslice`，文档中的时间字段必须为 `date` 数据类型和 [UNIX 时间 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://en.wikipedia.org/wiki/Unix_time){: new_window} 格式。除非同时满足这两个需求，否则 `timeslice` 参数无法正常运行。如果文档中包含的 `date` 字段具有诸如 `1496228512` 之类的值，那么可以创建 timeslice。该值必须是数字格式（例如，`float` 或 `double`），并且不能用引号括住。服务会将文本格式的日期和 ISO 8601 格式的日期视为 `string` 数据类型，而不是 `date` 数据类型。您可以在 timeslice 聚集中检测异常点。有关其他信息，请参阅 [timeslice 异常检测](#anomaly-detection)。以下示例会返回纽约市时区中时间间隔为 2 天的“sales”（“product.sales”）的值。

例如：
```bash
timeslice(product.sales,2day,America/New York)
```
{: codeblock}

### timeslice 异常检测
{: #anomaly-detection}

您可以选择将异常检测应用于 `timeslice` 聚集的结果。异常检测用于查找时间系列中的异常数据点，并标记它们以供进一步检查。异常检测的示例应用场景包括识别信用卡使用量的峰值，以及在 Watson Discovery News 中搜索有关特定主题的文章集群。

要应用异常检测，请在聚集中使用以下语法：

```bash
timeslice(field:<date>,interval:<interval>,anomaly:true)`
```
{: codeblock}

如果对 `timeslice` 聚集指定 `anomaly:true`，那么输出将额外包含以下两个字段，如示例中所示。

  - `"anomaly": true`，用于指示已执行异常检测
  - `anomaly` 字段，位于输出结果数组中显示为异常的数据点中。anomaly 字段的值为 `float` 数据类型，用于指示异常行为的量级。anomaly 字段的值越接近 `1`，结果为异常的可能性就越大。

  - `results` 数组中每个对象的 `key` 和 `key_as_string` 都对应于 UNIX 时间戳记（以秒计）。
  - 异常分数仅相对于原始查询。

```json
"type": "timeslice",
"field": "blekko.chrondate",
"interval": "1d",
"anomaly": true,
"results": [
  {
    "matching_results": 2933,
    "anomaly": 1,
    "key_as_string": "1496880000",
    "key": 1496880000000
  },
  {
    "matching_results": 3435,
    "anomaly": 1,
    "key_as_string": "1496966400",
    "key": 1496966400000
  },
  {
    "matching_results": 3692,
    "anomaly": 0.598226,
    "key_as_string": "1496016000",
    "key": 1496016000000
  },
  {
    "matching_results": 4551,
    "anomaly": 0.828498,
    "key_as_string": "1495411200",
    "key": 1495411200000
  },
  {
    "matching_results": 947,
    "key_as_string": "1489968000",
    "key": 1489968000000
  },
 ...
]
...
```
{: codeblock}

#### 异常检测的限制
{: #anomaly-limitations}

- 目前，异常检测仅在顶级 `timeslice` 聚集上可用，而在较低级别 (nested) 聚集上不可用。
- 在任何给定的 `timeslice` 聚集中，异常检测可处理的最大点数为 `1500`。
- 异常检测可处理的最大顶级 timeslice 聚集数为 `20`。

<!--
#### Anomaly detection workflow

The following example workflow detects an anomaly for the text entity `London` and retrieves additional information about the anomalous datapoint.

  1. Timeslice aggregation: `query=entities.text:London&count=0&aggregation=timeslice(blekko.last_crawled,1day,anomaly:true)`
  1. Term aggregation to retrieve top keywords: `query=entities.text:London&count=0&aggregation=term(keywords.text,count:5)&filter=blekko.last_crawled>=1490140800,<=1490227200`
  1. Query to retrieve top enriched title: `query=entities.text:London,keywords.text:Westminster Bridge|police officer|people|Prime Minister Theresa|parliament&count=1&filter=blekko.last_crawled>=1490140800,<=1490227200&return=enrichedTitle.text`
  -->

## top_hits
{: #top_hits}

返回按查询或扩充项分数排名的文档。可与任何查询参数或聚集配合使用。以下示例会返回 term 聚集的前 10 个匹配项。

例如：
```bash
term(enriched_text.concepts.text).top_hits(10)
```
{: codeblock}

## unique_count
{: #unique_count}

返回集合中指定字段的唯一实例计数。

示例：
```bash
unique_count(enriched_text.keyword.text)
```
{: codeblock}

```bash
nested(enriched_text.entities).term(enriched_text.entities.text,count:3).unique_count(enriched_text.entities.type)
```
{: codeblock}

## max
{: #max}

返回所有匹配文档中指定字段的最大值。

例如：
```bash
max(product.price)
```
{: codeblock}

## min
{: #min}

返回所有匹配文档中指定字段的最小值。

例如：
```bash
min(product.price)
```
{: codeblock}

## average
{: #average}

返回所有匹配文档中指定字段的平均值。

例如：
```bash
average(product.price)
```
{: codeblock}

## sum
{: #sum}

将所有匹配文档中指定字段的值加在一起。

例如：
```bash
sum(product.price)
```
{: codeblock}
