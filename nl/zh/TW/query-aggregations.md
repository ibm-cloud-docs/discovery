---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-09"

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

# 查詢聚集
{: #query-aggregations}

聚集傳回一組資料值。如需可用聚集的完整清單，請參閱[查詢參照](/docs/services/discovery/query-reference.html#aggregations)。

## term
{: #term}

傳回所選取強化的前幾個值（依評分和依頻率）。所有強化都是有效值。您可以選擇性地使用 `count` 來指定要傳回的詞彙數。此範例會傳回含有概念強化的前幾個值的全文和強化，並指定傳回 10 個詞彙。

例如：
```bash
term(enriched_text.concepts.text,count:10)
```
{: codeblock}

## filter
{: #filter}

一個修飾元，它會縮減其後的聚集查詢的文件集。此範例會過濾成包含「雲端運算」概念的文件集。

例如：
```bash
filter(enriched_text.concepts.text:cloud computing)
```
{: codeblock}

## nested
{: #nested}

在聚集查詢之前套用巢狀，會將聚集限制為所指定結果的區域。例如：`nested(enriched_text.entities)` 表示只會使用任何結果的 `enriched_text.entities` 元件來進行聚集。

例如：
```bash
nested(enriched_text.entities)
```
{: codeblock}

## histogram
{: #histogram}

建立數值間隔區段來分類文件。請使用單一數值欄位中的欄位值來說明該種類。用來建立直方圖的欄位必須是數字（`integer`、`float`、`double` 或 `date`）類型。不支援非數字類型，例如 `string`。例如，"price": 1.30 是有效的數字值，"price": "1.30" 是字串，因此它無效。請利用 `interval` 引數來定義結果要分割成的區段大小。間隔值必須是整數且非負數，並設定為合理值，以便將可能的欄位值分段。例如，如果您的資料集包含數個項目的價格，例如："price" : 1.30、"price" : 1.99 及 "price" : 2.99，您可以使用間隔 1，這樣您會看到一切都是在 1 與 2 及 2 與 3 之間分組。您可能不會使用間隔 100，因為所有資料最後都會在同一個區段。直方圖可以處理小數值，但間隔必須為整數。語法是 `histogram(<field>,<interval>)`，如下列範例所示。

例如：
```bash
histogram(product.price,interval:1)
```
{: codeblock}

## timeslice
{: #timeslice}

使用日期來建立間隔區段的特殊化直方圖。有效的日期間隔值為 `second/seconds`、`minute/minutes`、`hour/hours`、`day/days`、`week/weeks`、`month/months` 及 `year/years`。語法是 `timeslice(<field>,<interval>,<time_zone>)`。若要使用 `timeslice`，則文件中的時間欄位必須是 `date` 資料類型，且格式為 [UNIX 時間 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://en.wikipedia.org/wiki/Unix_time){: new_window}。除非這兩項需求都符合，否則 `timeslice` 參數無法正確運作。如果文件包含 `date` 欄位（含有諸如 `1496228512` 之類的值），則您可以建立時間片段。此值必須是數字格式（例如，`float` 或 `double`），而且不以引號括住。該服務會將文字中的日期和 ISO 8601 格式的日期視為資料類型 `string`，而不是資料類型 `date`。您可以在時間片段聚集中偵測到異常點。如需相關資訊，請參閱[時間片段異常偵測](#anomaly-detection)。本範例傳回紐約市時區間隔 2 天的「銷售」("product.sales") 值。

例如：
```bash
timeslice(product.sales,2day,America/New York)
```
{: codeblock}

### 時間片段異常偵測
{: #anomaly-detection}

您可以選擇性地將異常偵測套用至 `timeliice` 聚集的結果。異常偵測可用來尋找時間序列內的異常資料點，並標示它們以進一步檢閱。異常偵測的範例用途包括識別信用卡使用情形中的突增，以及搜尋 Watson Discovery News 中有關特定主題的文章群。

若要套用異常偵測，請在聚集中使用下列語法：

```bash
timeslice(field:<date>,interval:<interval>,anomaly:true)`
```
{: codeblock}

如果您在 `timeslice` 聚集中指定 `anomaly:true`，則輸出包括下列兩個其他欄位，如範例中所示。

  - `"anomaly": true`，指出已執行異常偵測
  - 在輸出結果陣列中異常之點的 `anomaly` 欄位。anomaly 欄位具有 `float` 資料類型的值，指出異常行為的強度。anomaly 欄位值越接近 `1`，結果越可能異常。

  - `results` 陣列中每一個物件的 `key` 和 `key_as_string` 都對應於 UNIX 時間戳記（以秒為單位）。
  - 異常評分與一項查詢相關，而不是跨不同查詢。

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

#### 異常偵測的限制

- 「異常偵測」目前只適用於最上層 `timellu` 聚集。它無法使用於低階（巢狀）聚集。
- 任何給定的 `timeslice` 聚集中，可由異常偵測處理的點數目上限為 `1500`。
- 可由異常偵測處理的最上層時間片段聚集數目上限為 `20`。

<!--
#### Anomaly detection workflow

The following example workflow detects an anomaly for the text entity `London` and retrieves additional information about the anomalous datapoint.

  1. Timeslice aggregation: `query=entities.text:London&count=0&aggregation=timeslice(blekko.last_crawled,1day,anomaly:true)`
  1. Term aggregation to retrieve top keywords: `query=entities.text:London&count=0&aggregation=term(keywords.text,count:5)&filter=blekko.last_crawled>=1490140800,<=1490227200`
  1. Query to retrieve top enriched title: `query=entities.text:London,keywords.text:Westminster Bridge|police officer|people|Prime Minister Theresa|parliament&count=1&filter=blekko.last_crawled>=1490140800,<=1490227200&return=enrichedTitle.text`
  -->

## top_hits
{: #top_hits}

傳回依查詢或強化的評分來分級的文件。可以與任何查詢參數或聚集搭配使用。此範例會傳回詞彙聚集的前 10 個相符數。

例如：
```bash
term(enriched_text.concepts.text).top_hits(10)
```
{: codeblock}

## unique_count
{: #unique_count}

傳回集合中所指定欄位的唯一實例計數。

範例：
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

傳回所有相符文件之間所指定欄位中的最高值。

例如：
```bash
max(product.price)
```
{: codeblock}

## min
{: #min}

傳回所有相符文件之間所指定欄位中的最低值。

例如：
```bash
min(product.price)
```
{: codeblock}

## average
{: #average}

傳回所有相符文件之間所指定欄位的平均值。

例如：
```bash
average(product.price)
```
{: codeblock}

## sum
{: #sum}

將所有相符文件之間所指定欄位的值相加。

例如：
```bash
sum(product.price)
```
{: codeblock}
