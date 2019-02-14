---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-09"

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

# 查询聚集
{: #query-aggregations}

聚集用于返回一组数据值。有关可用聚集的完整列表，请参阅[查询参考](/docs/services/discovery/query-reference.html#aggregations)。

## term
{: #term}

返回所选扩充项的排名靠前的值（按分数和按频率）。所有扩充项都是有效值。您可以选择使用 `count` 来指定要返回的项数。`count` 参数的缺省值为 10。此示例使用概念扩充项返回排名靠前的值的完整文本和扩充项，并指定返回 10 项。

例如：
```bash
term(enriched_text.concepts.text,count:10)
```
{: codeblock}

## filter
{: #filter}

用于缩小位于其前面的聚集查询文档集范围的修饰符。此示例会过滤为包含概念 Cloud computing 的一组文档。

例如：
```bash
filter(enriched_text.concepts.text:"cloud computing")
```
{: codeblock}

## nested
{: #nested}

在聚集查询之前应用嵌套，可将聚集限制为指定结果区域。例如：`nested(enriched_text.entities)` 表示仅对任何结果的 `enriched_text.entities` 组成部分进行聚集。

例如：
```bash
nested(enriched_text.entities)
```
{: codeblock}

## histogram
{: #histogram}

创建数字区间分段以对文档进行分类。使用单个数字字段中的字段值来描述类别。用于创建直方图的字段必须是数字（`integer`、`float`、`double` 或 `date`）类型。不支持非数字类型，如 `string`。例如，"price": 1.30 是有效的数字值，而 "price": "1.30" 是字符串，所以此值无效。使用 `interval` 自变量可定义将结果拆分成的部分的大小。interval 值必须为非负整数，并且设置为适合对可能的字段值进行分段。例如，如果数据集包括若干项的价格，如："price": 1.30、"price": 1.99 和 "price": 2.99，那么可以将 interval 设置为 1，这样就可以查看在 1 和 2 之间以及 2 和 3 之间进行分组的所有内容。您可能不会将 interval 设置为 100，因为这样会使所有数据全部位于同一个分段中。histogram 可以处理小数值，但 interval 必须为整数。语法为 `histogram(<field>,<interval>)`，如以下示例中所示。

例如：
```bash
histogram(product.price,interval:1)
```
{: codeblock}

## timeslice
{: #timeslice}

使用日期来创建时间间隔分段的专用直方图。有效的日期时间间隔值为 `second/seconds`、`minute/minutes`、`hour/hours`、`day/days`、`week/weeks`、`month/months` 和 `year/years`。语法为 `timeslice(<field>,<interval>,<time_zone>)`. 要使用 `timeslice`，文档中的时间字段必须为 `date` 数据类型和 [UNIX 时间 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://en.wikipedia.org/wiki/Unix_time){: new_window} 格式。除非同时满足这两个需求，否则 `timeslice` 参数无法正常工作。如果文档包含带有 `1496228512` 之类值的 `date` 字段，那么可以创建时间片。该值必须是数字格式（例如，`float` 或 `double`），并且不能用引号括起。服务会将文本格式的日期和 ISO 8601 格式的日期视为数据类型 `string`，而不是数据类型 `date`。您可以在 timeslice 聚集中检测异常点。请参阅[时间片异常检测](#anomaly-detection)以获取其他信息。以下示例返回纽约市时区中时间间隔为 2 天的“sales”（“product.sales”）的值。

例如：
```bash
timeslice(product.sales,2day,America/New York)
```
{: codeblock}

### 时间片异常检测
{: #anomaly-detection}

您可以选择将异常检测应用于 `timeslice` 聚集的结果。异常检测用于查找时间系列中的异常数据点，并对其进行标记以供进一步复查。异常检测的示例用例包括确定信用卡使用量峰值，以及在 Watson Discovery News 中搜索有关特定主题的文章聚类。

要应用异常检测，请在聚集中使用以下语法：

```bash
timeslice(field:<date>,interval:<interval>,anomaly:true)`
```
{: codeblock}

如果对 `timeslice` 聚集指定 `anomaly:true`，那么输出将包含以下两个附加字段，如示例中所示。

  - `"anomaly": true` 指示已执行异常检测
  - 位于输出结果数组中异常点的 `anomaly` 字段。anomaly 字段的值为 `float` 数据类型，指示异常行为的量级。anomaly 字段的值越接近 `1`，结果异常的可能性越大。

  - `results` 数组中每个对象的 `key` 和 `key_as_string` 对应于 UNIX 时间戳记（以秒计）。
  - 异常分数相对于某个查询，而不是在不同查询之间比较。

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

- 目前，异常检测仅在顶级 `timeslice` 聚集上可用，在较低级别（嵌套）聚集中不可用。
- 可由任何给定 `timeslice` 聚集中的异常检测进行处理的最大点数为 `1500`。
- 可由异常检测进行处理的最大顶级 timeslice 聚集数为 `20`。

<!--
#### Anomaly detection workflow

The following example workflow detects an anomaly for the text entity `London` and retrieves additional information about the anomalous datapoint.

  1. Timeslice aggregation: `query=entities.text:London&count=0&aggregation=timeslice(blekko.last_crawled,1day,anomaly:true)`
  1. Term aggregation to retrieve top keywords: `query=entities.text:London&count=0&aggregation=term(keywords.text,count:5)&filter=blekko.last_crawled>=1490140800,<=1490227200`
  1. Query to retrieve top enriched title: `query=entities.text:London,keywords.text:Westminster Bridge|police officer|people|Prime Minister Theresa|parliament&count=1&filter=blekko.last_crawled>=1490140800,<=1490227200&return=enrichedTitle.text`
  -->

## top_hits
{: #top_hits}

返回按查询或扩充项分数排名的文档。可以与任何查询参数或聚集一起使用。以下示例返回 term 聚集的前 10 位命中。

例如：
```bash
term(enriched_text.concepts.text).top_hits(10)
```
{: codeblock}

## unique_count
{: #unique_count}

返回集合中所指定字段的唯一实例的计数。

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
