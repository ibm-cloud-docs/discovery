---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-17"

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

# 使用情况监视
{: #usage}

您可以监视和跟踪 {{site.data.keyword.discoveryshort}} 实例的使用情况，并使用这些数据来帮助您了解和改进应用程序。[事件 API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#events-and-feedback-api){: new_window} 可用于创建与特定自然语言查询和操作相关联的日志条目。例如，可以记录用户“已单击”结果集内的哪些文档，以及单击发生的时间。

**注：**仅对于针对专用数据集合的自然语言查询，才会监视日志和事件。在 {{site.data.keyword.discoverynewsfull}} 上不会收集任何日志。

{{site.data.keyword.discoveryshort}} 可以记录以下信息：
- **查询** - 针对环境中的集合运行的自然语言查询 
- **印记**（或**结果**）- 针对特定查询返回的结果，通常是文档或段落 
- **事件** - 用户对 {{site.data.keyword.discoveryshort}} 中的某个结果或结果集执行的交互（例如，单击文档结果）

**查询**和**印记**会自动进行记录；**事件**日志记录可以通过 API 集成到应用程序中。

## 查看日志
{: #viewlogs}

您可以搜索查询和事件日志，以查找与指定条件相匹配的查询会话。搜索 `logs` 端点可将标准 {{site.data.keyword.discoveryshort}} 查询语法用于支持的参数。该端点提供了用于查看和搜索所记录数据的基本查询功能。  

`/api/v1/logs` 端点支持以下 {{site.data.keyword.discoveryshort}} 查询参数。
- query 
- filter
- sort
- count 
- offset
- version

有关参数的函数和语法的其他详细信息，请参阅[查询参数](/docs/services/discovery/query-parameters.html)。

以下示例在日志中搜索包含术语“train”的自然语言查询：

`https://gateway.watsonplatform.net/discovery/api/v1/logs?version=2018-03-28&query=train`

`logs` 查询的响应包含的结果类似于 {{site.data.keyword.discoveryshort}} 文档结果。每个结果将为 query 或 event，这在文档的 `type` 字段中指定。  

示例查询日志：

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

通过查询日志，您可以调查返回给最终用户的结果类型，并调查使用 {{site.data.keyword.discoveryshort}} 中提供的方法来改进结果质量的途径。例如： 
- 相关性训练，请参阅[使用 API 改进结果相关性](/docs/services/discovery/train.html)和[使用工具改进结果相关性](/docs/services/discovery/train-tooling.html)
- [查询运算符](/docs/services/discovery/query-operators.html)
- [查询扩展](/docs/services/discovery/using.html#query-expansion)
- 定制配置，请参阅[配置参考](/docs/services/discovery/custom-config.html)

## 创建事件日志
{: #eventlogs}

事件日志用于跟踪应用程序中用户的交互。事件日志可以帮助您了解应用程序的执行情况，以及识别您可能需要重点关注的区域，以改进结果。{{site.data.keyword.discoveryshort}} 提供了可嵌入到应用程序中以跟踪事件的 API。用户执行操作时，使用相应的信息调用此 API 可向 {{site.data.keyword.discoveryshort}} 发回信号，然后可以在日志中查看该信号。 

事件可以帮助收集有关计算度量值的信息（如点击率），以度量应用程序在帮助最终用户查找相关信息方面的有效程度，或者可用于通过复查查询和单击来帮助进行种子训练，以开始构建参考标准。 

您可以在用户与结果进行交互的任何位置添加此 API。例如，在搜索 UI 中，您可能希望在用户单击文档链接时添加此 API，或者在聊天机器人界面中，您可能希望使用此 API 在用户单击**展开**或**更多详细信息**按钮时进行跟踪。

{{site.data.keyword.discoveryshort}} 结果将返回可用于跟踪事件（包括会话令牌）的其他信息。 

`"matching_results": 179,`
`"session_token": "1_LKczxWGEWx59fYD0_VV8HFUpb6"`

要记录事件，请对 `/api/v1/events` 端点执行 POST 操作。请参阅[事件 API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#events-and-feedback-api){: new_window} 以获取详细信息。

记录事件后，即可以使用 `/api/v1/logs` 端点回读该事件。使用 `session_token` 将事件连接到关联的查询。
