---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-18"

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

# 查询性能
{: #qp}

{{site.data.keyword.discoveryshort}} 中的查询性能取决于多个因素。 

## 评估性能 
{: #qp-evaluate}

如果预期应用程序上的同时负载较高，那么评估 {{site.data.keyword.discoveryshort}} 应用程序的性能很重要。常用于度量性能的几个维度如下所示：
1.  **响应等待时间** - {{site.data.keyword.discoveryshort}} 返回查询结果所耗用的时间。 
    - 等待时间可能会因多个因素而有所不同，请参阅[影响性能的因素](/docs/services/discovery?topic=discovery-qp#perffactors)以获取更多信息。 
    - 请务必在生产环境中使用一组具有代表性的查询来运行测试，从而确定平均等待时间。 
1.   **查询比率** - 给定时间内可处理的请求数，通常以“每秒查询数”(QPS) 进行度量。此度量在您预期应用程序上的同时负载较高时最重要。  
     - 可达到的比率会因等待时间等许多相同的因素而有所不同。 
     - 查询比率也应使用具有代表性的查询以及您预期会出现的负载进行评估。请务必计入测试期间的峰值负载。

## 影响性能的因素
{: #perffactors}

{{site.data.keyword.discoveryshort}} 中的查询性能将会因多个因素而有所不同，包括套餐大小、查询复杂性、使用的功能以及集合大小和复杂性。

### 套餐大小
{: #qp-plansize}

{{site.data.keyword.discoveryshort}} 价格套餐限制了可用的文档数，并且还提供不同的功能来处理查询负载。套餐大小越大，可用于处理查询的资源越多。平均速率限制也因套餐大小而有所不同。升级套餐可提高性能。请参阅 [{{site.data.keyword.discoveryshort}} 价格套餐](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)以了解套餐和限制。 

### 查询复杂性
{: #qp-query}

可使用很多方法对 {{site.data.keyword.discoveryshort}} 运行查询，而使用的不同操作会影响性能。这些查询特征会影响性能：

1.   **长度** - 较长时间的查询最有可能产生较差的性能。 
1.   **聚集** - 聚集是更复杂的查询类型，其中嵌套聚集对性能影响最大。 
1.   **运算符** - 通配符和模糊匹配会影响性能。
1.   **计数** - 减少返回的文档数可以提高性能；如果需要翻阅结果，请使用 `offset` 参数。 
1.   **返回字段** - 将返回的字段限制为仅包含应用程序所需的内容会很有用（例如，如果只需要标题和段落，那么不要返回文档全文）。 

请参阅[查询参考](/docs/services/discovery?topic=discovery-query-reference#query-reference)以获取详细信息。

### 使用的功能
{: #qp-features}

可使用多种功能来增强查询结果。以下功能会影响性能：
 
1.   **段落检索** - 段落检索会在文档内搜索，以查找查询的相关文本片段。您可以使用 `passages.fields` 参数调整段落检索所搜索文档中的字段；如果内容具有很多字段，这有助于减少段落检索的等待时间。请参阅[段落](/docs/services/discovery?topic=discovery-query-parameters#passages)以获取有关段落检索的更多信息。
1.   **相关性训练** - 相关性训练会计算集合中每个顶级文本字段（与 JSON 中 `document_id` 处于相同级别的字段）的功能。如果有很多顶级字段，那么在使用训练时，`natural_language_query` 的性能会受到影响。减少顶级字段数可提高性能。为此，您可以使用规范化，或手动编辑 JSON 来放入对查找嵌套结构中的相关内容并无帮助的字段。更改训练所使用的字段也会影响模型，因此在进行此更改时，您需要同时考虑对性能的影响以及结果的准确性。请参阅[改进结果相关性](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling)，以获取有关相关性训练的更多信息。
1.  **Continuous Relevancy Training** - 环境中所有集合的 Continuous Relevancy Training 搜索。环境中的集合越多，对性能的影响越大。请参阅 [Continuous Relevancy Training](/docs/services/discovery?topic=discovery-crt#crt) 以获取更多信息。

### 集合大小和复杂性
{: #qp-collection} 

专用集合中的文档组成也会影响查询性能：
1.  **文档总数** - 达到高级套餐大小的`文档数`上限时，性能可能会受影响。 
1.  **文档大小** - 对于非常大的文档（大小为若干 MB），每个请求需要移动较大数量的数据，这会对性能造成负面影响，尤其是在使用段落检索和相关性训练时。 
1.  **扩充项数** - 扩充项会添加很大数量的嵌套字段，从而增加文档的复杂性。如果扩充项对您的用例而言并非必要，请考虑在摄入时将其禁用。扩充项不会直接用于 `natural_language_query` 搜索相关性。请参阅[添加扩充项](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)以获取有关扩充项的更多信息。
