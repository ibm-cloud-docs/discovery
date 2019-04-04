---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-25"

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

# Continuous Relevancy Training
{: #crt}

{{site.data.keyword.discoveryshort}} Continuous Relevancy Training 可以自动从用户行为中学习，从而显著减少提高结果相关性排名所需的工作量。Continuous Relevancy Training 使用来自用户的交互来学习如何使最相关的结果浮现。它可以从交互（如单击）中学习，以确定哪些结果对于用户最有价值，并揭示未来查询的最重要信号。Continuous Relevancy Training 将对文档重新排名，以使最相关的信息浮现在结果顶部。Continuous Relevancy Training 可用于：

- 根据支持座席单击的结果，帮助改进支持座席的结果相关性
- 在客户聊天机器人中，根据所选的长尾结果，显示更相关的结果 
- 根据专家探索的结果，向专家提供更相关的响应

要设置 Continuous Relevance Training，请执行以下操作：

- Continuous Relevancy Training 只能在环境级别启用。查询必须使用 `/api/v1/environment/{environment_id}/query` 和 `/api/v1/environments/{environment_id}/query` 端点来查询一个或多个集合。
- 由于要使用 {{site.data.keyword.discoveryshort}} `事件`（单击）来创建所需的训练数据，因此请首先集成事件跟踪。请参阅[监视使用情况](/docs/services/discovery?topic=discovery-usage#usage)以获取详细信息。

- 要启动 Continuous Relevancy Training，最少需要 1000 个具有关联单击事件的自然语言查询。事件和日志将在实例中保留 30 天，因此必须在该时间段内收集 1000 次单击。
- Continuous Relevancy Training 可用于大小为 `S 号`或更大大小的高级套餐以及高端套餐。不可用于`轻量`套餐。
- Continuous Relevancy Training 的集合数限制为 `5` 个。由于 Continuous Relevancy Training 可跨多个集合工作，因此查询和训练时间均可能延长。
- Continuous Relevancy Training 仅对顶级字段执行，并且对于训练过程中可以使用的字段数有限制。如果顶级字段数超过 `10` 个，那么训练遇到错误的可能性更高。 

要使用 Continuous Relevance Training，请执行以下操作：

经过训练后，Continuous Relevancy Training 用于在使用环境级别的查询时，影响 `natural_language_query` 的结果。 

在查询时，可以通过对环境中的所有集合运行多集合 `nual_language_query` 来使用 Continuous Relevancy Training。请参阅[查询多个集合](/docs/services/discovery?topic=discovery-query-concepts#multiple-collections)以获取相关指示信息。 

**注：**Continuous Relevancy Training 不会影响对已训练或未训练集合级别 (`/v1/environments/{environment_id}/collections/{collection_id}/query`) 的查询调用所做的查询。 

跟踪状态：

可以通过 `/api/v1/environments` 端点查看 Continuous Relevancy Training 的状态。请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/discovery#get-environment-info){: new_window}。`状态`将提供有关训练操作状态的信息，并将在 Continuous Relevancy Training 处于活动状态时通知您：

```
"search_status" : [
        {
            "scope" : "environment",
            "status" : "NO_DATA",
            "status_description" : "Discovery is employing a default strategy for document search natural_language_query. Enable query and event logging so we can initiate relevancy training to improve search accuracy.”
        }
    ]
```
