---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-17"

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

# 监视使用情况
{: #usage}

您可以监视和跟踪 {{site.data.keyword.discoveryshort}} 实例的使用情况，并通过此使用情况数据更好地了解和改进您的应用程序。[事件 API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/discovery#create-event){: new_window} 可用于创建与特定自然语言查询和操作相关联的日志条目。例如，您可以记录用户“单击了”结果集中的哪些文档，以及是在何时单击的。

**注：**仅会为专用数据集合的自然语言查询监视日志和事件。在 {{site.data.keyword.discoverynewsfull}} 上不会收集任何日志。

{{site.data.keyword.discoveryshort}} 可以记录以下信息：
- **查询** - 针对环境中的集合运行的自然语言查询 
- **印记**（或**结果**）- 针对特定查询返回的结果，通常为文档或段落 
- **事件** - 用户与 {{site.data.keyword.discoveryshort}} 中的单个结果或结果集进行的交互（例如，单击文档结果）

**查询**和**印记**是自动记录的；**事件**日志记录可通过 API 集成到应用程序中。

## 查看日志
{: #viewlogs}

您可以搜索查询和事件日志，以查找与指定条件相匹配的查询会话。搜索 `logs` 端点时，会对受支持参数使用标准 {{site.data.keyword.discoveryshort}} 查询语法。该端点提供了用于查看和搜索所记录数据的基本查询功能。  

`/api/v1/logs` 端点支持以下 {{site.data.keyword.discoveryshort}} 查询参数。
- query 
- filter
- sort
- count 
- offset
- version

有关这些参数的函数和语法的其他详细信息，请参阅[查询参数](/docs/services/discovery?topic=discovery-query-parameters#query-parameters)。

下面是包含词汇“train”的自然语言查询的日志搜索示例：

`https://gateway.watsonplatform.net/discovery/api/v1/logs?version=2018-03-28&query=train`

`logs` 查询的响应包含的结果类似于 {{site.data.keyword.discoveryshort}} 文档结果。每个结果都将是一个查询或事件，如文档 `type` 字段中所指定。  

查询日志示例：

```
{
            "customer_id": "",
            "environment_id": "252e6e82-c2d2-450e-9670-0008b0a3a99c",
            "natural_language_query": "how do i get from the airport to the city",
            "query_id": "_Qs35yOoa7",
            "document_results": {
                "count": 2,
                "results": [
                    {
                        "collection_id": "af9e1f41-6114-4d77-bca6-c9b99b2601b1",
                        "score": 6.724753491503856,
                        "position": 1,
                        "document_id": "4193eaa727d79b0f74597356dbcbb9a7"
                    },
                    {
                        "collection_id": "af9e1f41-6114-4d77-bca6-c9b99b2601b1",
                        "score": 5.791631414211986,
                        "position": 2,
                        "document_id": "bdcd6a9cc1438a3faa8c925f6a8d9429"
                    }
                ]
            },
            "event_type": "query",
            "session_token": "1_LKczxWGEWx5TJAi1_Qs35yOoa7",
            "created_timestamp": "2018-09-12T05:20:07.469Z"
        }
```

使用查询日志，您可以调查返回给最终用户的结果类型，并研究如何使用 {{site.data.keyword.discoveryshort}} 中提供的方法来提高结果质量。例如： 
- 相关性训练。请参阅[使用 API 改进结果相关性](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api)和[使用工具改进结果相关性](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling)
- [查询运算符](/docs/services/discovery?topic=discovery-query-operators#query-operators)
- [查询扩展](/docs/services/discovery?topic=discovery-query-concepts#query-expansion)
- 定制配置。请参阅[配置参考](/docs/services/discovery?topic=discovery-configref#configref)

## 创建事件日志
{: #eventlogs}

事件日志用于跟踪应用程序中的用户交互。事件日志可以帮助您了解应用程序的运行情况，以及发现可能需要重点关注的区域，从而改进结果。{{site.data.keyword.discoveryshort}} 提供了可嵌入到应用程序中来跟踪事件的 API。在用户执行操作时使用适当的信息来调用此 API，可将信号发送回 {{site.data.keyword.discoveryshort}}，然后您可以在日志中查看该信号。 

事件可以帮助收集有关计算度量值的信息（如点击率），以衡量应用程序在帮助最终用户查找相关信息方面的效果，也可用于通过查看查询数和单击数来帮助进行种子训练，从而开始构建参考标准。 

您可以在用户与结果进行交互的任何位置添加此 API。例如，在搜索 UI 中，您可能想要在用户单击文档链接时添加此 API，或者在聊天机器人界面中，您可能想要使用此 API 来跟踪用户何时单击**展开**或**更多详细信息**按钮。

{{site.data.keyword.discoveryshort}} 结果会返回可用于跟踪事件的其他信息，包括会话令牌。 

`"matching_results": 179,`
`"session_token": "1_LKczxWGEWx59fYD0_VV8HFUpb6"`

要记录事件，请对 `/api/v1/events` 端点执行 POST 操作。有关详细信息，请参阅[事件 API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/discovery#create-event){: new_window}。

记录的事件可通过 `/api/v1/logs` 端点将其读回。使用 `session_token` 可将事件与关联的查询相连接。
