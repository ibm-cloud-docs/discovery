---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-03"

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

# 相关性训练技巧
{: #relevancy-tips}

 有关训练集合的常见问题的答案，以及常见错误和警告消息的说明。有关改进自然语言查询相关性的更多信息，请参阅[使用工具改进结果相关性](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling)和[使用 API 改进结果相关性](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api)。
{: shortdesc}

## 了解训练
{: #understanding-training}

有关训练集合的常见问题的答案。

### 如何知道自己的系统是否经过训练？
{: #understanding-system}

使用[列出集合详细信息 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/discovery#get-collection-details){: new_window} API 命令来验证系统是否已经过训练。  

```bash
curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07"
```
{: pre}

示例响应：

```json
{
  "training_status": {
    "data_updated": "2017-02-10T14:18:22.786Z",
    "total_examples": 54,
    "sufficient_label_diversity": false,
    "processing": false,
    "minimum_examples_added": true,
    "successfully_trained": "2017-02-08T14:18:22.786Z",
    "available": true,
    "notices": 13,
    "minimum_queries_added": true    
    }
}
```

为了满足训练需求，以下各项必须全部为 `true`：
- `minimum_queries_added`
- `minimum_examples_added`
- `sufficient_label_diversity`   

在响应中：
- `successfully_trained` 是上次成功完成训练的时间。
- `available: true` 指示已执行训练并且模型可用。
- `processing: true` 指示正在进行训练。
-  如果 `data_updated` 日期晚于 `successfully_trained` 日期，说明自最近一次上传数据以来，尚未对新模型进行过训练。  

### 如何检查错误和警告？
{: #understanding-errors}

可以使用[查询通知 API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/discovery#query-system-notices){: new_window} 来查看错误或警告。  

```bash
curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/notices?version=2017-11-07"
```
{: pre}

其他 API 操作列在[执行其他训练数据查询操作](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#training-data-operations)中。

### 如何解释训练后在自然语言查询结果中显示的`置信度`分数？
{: #interpret-confidence}

请参阅[置信度分数](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence)以获取更多信息。  

## 解释错误和警告
{: #interpreting-errors}

常见错误和警告消息的说明。

### 警告：`找到的训练数据无效：返回的文档不在给定查询的前 100 个搜索结果中，因此不会用于训练`
{: #warning-docnotreturned}

导致此警告的原因是训练数据中的 `document_ids` 与针对该集合执行的搜索中的 `document_ids` 不匹配。您应该检查查询，确保返回的要评级的文档的 `document_id` 在该查询的前 100 个结果中。如果不在，您可能要检查以下两项内容：  

- 如果该文档未在前 100 个结果中返回，说明该文档可能不是高质量结果的良好示例，您可能要重新检查选择此文档的原因。  

- 如果根本未返回该文档，那么应该查看未返回该文档的原因，并确定该文档中是否有任何文本与查询的某些部分匹配。  

**注：**此警告指示您可能有一个或多个错误查询，但这并不表示不会执行训练。  

### 错误：`找到的训练数据无效：解析查询时发生语法错误`
{: #error-syntax}

- 这意味着实际查询语法存在问题。请验证查询是否返回了结果，并且未引发语法错误。仅当向自然语言查询添加了过滤器时，才会发生此错误。

### 错误：`找到的训练数据无效：提供的查询字符串超出最大长度，请提供较短的查询字符串`
{: #error-exceedlength}

- 最大查询字符串长度为 `2048`。您需要缩短特定查询的长度。在查询中包含过滤器是解决此问题的一种方法。  

### 错误：`无法训练此集合：您的套餐不支持对如此多的顶级文本字段进行训练。`
{: #error-toplevelfields}

- 仅在`轻量`套餐中才会发生此错误。顶级字段是指未嵌套在其他字段下的字段。训练仅对顶级字段执行，并且对于训练过程中可以使用的字段数有限制。集合中的顶级字段越多，需要的训练数据就越多。此外，如果顶级字段数超过 `10` 个，那么训练遇到错误的可能性更高。 

### 错误：`不满足训练数据质量标准：您需要具有已标注示例的其他训练查询。（为了符合条件进行训练，每个示例都必须出现在其查询的前 100 个搜索结果中。）`
{: #error-labels}

- 这意味着您需要添加更多训练数据才能成功训练。您至少需要 49 个唯一训练查询，并且每个查询至少需要一个已评级文档。最小值不等于是最佳值；集合的大小和其他因素可能会增加满足最低要求所需的训练示例数。  

### 错误：`不满足训练数据质量标准：唯一训练查询数不充分。至少需要 n 个，但实际只有 m 个。`
{: #error-notunique}

- 为了满足最低训练需求，您至少需要 49 个唯一训练查询，并且每个查询至少需要一个已评级文档。如果您拥有超过此数量的查询，但仍然收到此错误消息，那么应该检查通知以了解其他错误。  

### 错误：`不满足训练数据质量标准：找不到具有非零相关性标签的文档。`
{: #error-relevance}

- 训练数据需要足够的已标注数据，这些数据用于指定哪些文档的价值比较高。这意味着您需要使用非零值对某些文档评级。如果使用的是 Discovery 工具，那么需要将某些文档评级为“相关”(`10`)；如果使用的是 API，那么需要将某个文档标注为 `1` 或更高值。   

### 错误：`不满足训练数据质量标准：训练示例针对 X 个查询没有相关性标签变化。`
{: #error-variety}

- 训练的其中一个要求是有足够的标签差异性。这意味着，如果要获得经过良好训练的系统，那么不仅应该添加属于最佳相关性匹配的文档，而且还应添加相关性为“好”的文档。换言之，如果量程为 0-4，那么除了拥有评级为 4 的文档之外，还拥有评级为 2 和 3 的文档会很有助益。（如果使用的是 Discovery 工具，那么会将文档评级为相关 (`10`) 或不相关 (`0`)。至少 25% 的问题必须存在一定的标签变化。   
