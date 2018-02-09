---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-14"

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

# 相关性培训技巧
{: #relevancy-tips}

 有关培训集合的常见问题的答案，以及常见错误和警告消息的说明。有关改进自然语言查询相关性的更多信息，请参阅[使用工具改进结果相关性](/docs/services/discovery/train-tooling.html)和[使用 API 改进结果相关性](/docs/services/discovery/train.html)。
{: shortdesc}

## 了解培训

有关培训集合的常见问题的答案。

### 如何知道自己的系统是否经过培训？

使用[列出集合详细信息 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/?curl#list-collection-details){: new_window} API 命令来验证系统是否已经过培训。  

```bash
curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07"
```
{: pre}

示例响应：

```json
{
  "training": {
    "total_examples": 54,
    "available": true,
    "processing": false,
    "minimum_queries_added": true,
    "minimum_examples_added": true,
    "sufficient_label_diversity": false,
    "notices": 13,
    "successfully_trained": "2017-02-08T14:18:22.786Z",
    "data_updated": "2017-02-10T14:18:22.786Z"
    }
}
```

为了满足培训需求，以下各项必须全部为 `true`：
- `minimum_queries_added`
- `minimum_examples_added`
- `sufficient_label_diversity`   

在响应中：
- `successfully_trained` 是上次成功完成培训的时间。
- `available: true` 指示已执行培训并且模型可用。
- `processing: true` 指示正在进行培训。
-  如果 `data_updated` 日期晚于 `successfully_trained` 日期，说明自最近一次上传数据以来，尚未对新模型进行过培训。  

### 如何检查错误和警告？

可以使用[查询通知 API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-notices){: new_window} 来查看错误或警告。  

```bash
curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/notices?version=2017-11-07"
```
{: pre}

其他 API 操作列在[执行其他培训数据查询操作](/docs/services/discovery/train.html#training-data-operations)中。

### 如何解释培训后在自然语言查询结果中显示的 `confidence` 分数？

已培训的集合将在自然语言查询的结果中返回 `confidence` 分数。此 `confidence` 数字是根据结果相对于已培训模型的相关性来计算的。`confidence` 分数与 `score` **不同**。请参阅[置信度分数](/docs/services/discovery/train-tooling.html#confidence)以获取更多信息。  

## 解释错误和警告

常见错误和警告消息的说明。

### 警告：`找到的培训数据无效：返回的文档不在给定查询的前 100 个搜索结果中，因此不会用于培训`

导致此警告的原因是培训数据中的 `document_ids` 与针对该集合执行的搜索中的 `document_ids` 不匹配。您应该检查查询，确保返回的要评级的文档的 `document_id` 在该查询的前 100 个结果中。如果不在，您可能要检查以下两项内容：  

- 如果该文档未在前 100 个结果中返回，说明该文档可能不是高质量结果的良好示例，您可能要重新检查选择此文档的原因。  

- 如果根本未返回该文档，那么应该查看未返回该文档的原因，并确定该文档中是否有任何文本与查询的某些部分匹配。  

**注：**此警告指示您可能有一个或多个错误查询，但这并不表示不会执行培训。  

### 错误：`找到的培训数据无效：解析查询时发生语法错误`

- 这意味着实际查询语法存在问题。请验证查询是否返回了结果，并且未引发语法错误。仅当向自然语言查询添加了过滤器时，才会发生此错误。

### 错误：`找到的培训数据无效：提供的查询字符串超出最大长度，请提供较短的查询字符串`

- 最大查询字符串长度为 `X`。您需要缩短特定查询。在查询中包含过滤器是解决此问题的一种方法。  

### 错误：`无法培训此集合：您的套餐不支持对如此多的顶级文本字段进行培训。`

- 仅在 `Lite` 套餐中才会发生此错误。可以对其进行培训的最大顶级文本字段数为 `X`。顶级字段是指未嵌套在其他字段下的字段。培训仅对顶级字段执行，并且对于培训过程中可以使用的字段数有限制。  

### 错误：`不满足培训数据质量标准：您需要具有已标注示例的其他培训查询。（为了符合条件进行培训，每个示例都必须出现在其查询的前 100 个搜索结果中。）`

- 这意味着您需要添加更多培训数据才能成功培训。您至少需要 49 个唯一培训查询，并且每个查询至少需要一个已评级文档。最小值不等于是最佳值；集合的大小和其他因素可能会增加满足最低要求所需的培训示例数。  

### 错误：`不满足培训数据质量标准：唯一培训查询数不充分。至少需要 n 个，但实际只有 m 个。`

- 为了满足最低培训需求，您至少需要 49 个唯一培训查询，并且每个查询至少需要一个已评级文档。如果您拥有超过此数量的查询，但仍然收到此错误消息，那么应该检查通知以了解其他错误。  

### 错误：`不满足培训数据质量标准：找不到具有非零相关性标签的文档。`

- 培训数据需要足够的已标注数据，这些数据用于指定哪些文档的价值比较高。这意味着您需要使用非零值对某些文档评级。如果使用的是 Discovery 工具，那么需要将某些文档评级为“相关”(`10`)；如果使用的是 API，那么需要将某个文档标注为 `1` 或更高值。   

### 错误：`不满足培训数据质量标准：培训示例针对 X 个查询没有相关性标签变化。`

- 培训的其中一个要求是有足够的标签差异性。这意味着，如果要获得经过良好培训的系统，那么不仅应该添加属于最佳相关性匹配的文档，而且还应添加相关性为“好”的文档。换言之，如果量程为 0-4，那么除了拥有评级为 4 的文档之外，还拥有评级为 2 和 3 的文档会很有助益。（如果使用的是 Discovery 工具，那么会将文档评级为相关 (`10`) 或不相关 (`0`)。至少 25% 的问题必须存在一定的标签变化。   
