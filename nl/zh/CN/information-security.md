---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-01-10"

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

# 信息安全
{: #information-security}

IBM 致力于为客户和合作伙伴提供创新的数据隐私、安全性和监管解决方案。
{: shortdesc}

**声明：**
客户应负责确保自身遵守各种法律和法规，包括《欧盟一般数据保护条例》。确定和诠释可能影响客户业务的任何相关法律和法规，以及客户为遵守此类法律和法规所需执行的任何操作，均由客户全权负责向合格的法律顾问咨询建议。


此处描述的产品、服务和其他功能并不适用于所有客户情形，并且在可用性方面可能有限制。IBM 不会提供法律、会计或审计建议，也不会表述或保证其服务或产品将确保客户遵守任何法律或法规。

如果需要为创建的 {{site.data.keyword.cloud}}{{site.data.keyword.watson}} 资源请求 GDPR 支持

-   在欧盟 (EU)，请参阅[请求对欧盟内创建的 IBM Cloud Watson 资源的支持](/docs/services/watson/getting-started-gdpr-sar.html#request-EU)。
-   在欧盟以外的地区，请参阅[请求对欧盟以外的资源的支持](/docs/services/watson/getting-started-gdpr-sar.html#request-non-EU)。

## 欧盟一般数据保护条例 (GDPR)
{: #gdpr}

IBM 致力于为客户和合作伙伴提供创新的数据隐私、安全性和监管解决方案，以帮助他们实现 GDPR 合规性。

在[此处 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/gdpr) 了解有关 IBM 自己的 GDPR 准备旅程以及支持您合规旅程的 GDPR 功能和产品的更多信息。{: new_window}.

## 标注和删除 {{site.data.keyword.discoveryshort}} 中的数据
{: #gdpr-discovery}

{{site.data.keyword.discoveryshort}} 服务包含用于标注每个调用的数据的 API。

通过此 API，您可以：

- 使用客户标识来标注数据。
- 删除特定客户标识的所有数据，包括相关通知。

通过向可选的 `X-Watson-Metadata` 头添加您选择的 `customer_id`（请参阅[如何标注数据](/docs/services/discovery?topic=discovery-information-security#labeling)）来标注数据。然后，{{site.data.keyword.discoveryshort}} 可以通过 `customer_id` 来删除这些数据。

在任何 REST 调用上，都可以发送包含分号分隔的 `field=value` 对的可选头 `X-Watson-Metadata`，其中当前仅持久存储 `customer_id`。通过在 `X-Watson-Metadata` 头中添加该 `customer_id`，请求指示其中包含属于此 `customer_id` 的数据。

`customer_id` 在单个 {{site.data.keyword.discoveryshort}} 服务实例中唯一。但对于每个环境或集合并不唯一。customer_id 不应包含个人数据。

**注：**试验性和 Beta 功能不适用于生产环境，因此在标注和删除数据时，不保证能按预期起作用。在实现需要标注和删除数据的解决方案时，不应使用试验性和 Beta 功能。

## 支持标注数据的方法
{: #pi_methods}

以下存储的信息可以使用 `customer_id` 来删除，只要在通过关联方法初始添加这些信息时已指定此 `customer_id`：

- 查询 (`/v1/environments/{environment_id}/collections/{collection_id}/query`)，仅当与 `passages` 或 `natural_language_query` 参数一起使用时
- 事件 (`/v1/events`)
- 文档 (`/v1/environments/{environment_id}/collections/{collection_id}/documents`)
- 通知 (`/v1/environments/{environment_id}/collections/{collection_id}/notices`)，仅标注摄入`通知`。
- 知识图实体 (`/v1/environments/{environment_id}/collections/{collection_id}/query_entities`)
- 知识图关系 (`/v1/environments/{environment_id}/collections/{collection_id}/query_relations`)
- 训练数据 (`/v1/environments/{environment_id}/collections/{collection_id}/training_data`)

以下存储的信息未明确标注，因此无法通过指定 `customer_id` 来删除。这些字段中不支持个人数据。

以下存储项的任何字符串字段（包括但不限于 `name` 和 `description`）：
- 配置
- 集合
- 环境

## 标注数据
{: #labeling}

摄入文档时，请使用 `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` 或 `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/ID` 操作来包含 `X-Watson-Metadata` 头。`customer_id` 字段会添加到文档的 `extracted_metadata` 中。应用程序应该配置为在执行任何操作时，在 `X-Watson-Metadata` 头中提供 `customer_id`。

（可选）可以在 `metadata` 多部分表单部分中包含 `customer_id` 字段，而不使用 `X-Watson-Metadata` 头。

**注：**如果已摄入文档，那么需要重新摄入这些文档以添加 `X-Watson-Metadata` 头和 `customer_id`。

**注：**如果在 `metadata` 多部分表单部分中指定 `customer_id`，并且同时为同一文档指定了 `X-Watson-Metadata` 头，那么将使用 `X-Watson-Metadata` 头中的 `customer_id`。

限制：

- `X-Watson-Metadata` 头的值不能是超过 4 千字节的文本。
- `X-Watson-Metadata` 头必须包含 `field=value` 对的分号分隔列表。`field` 和 `value` 不能包含分号 (`;`) 或等号 (`=`)。
- `customer_id` 在每个 {{site.data.keyword.discoveryshort}} 实例中唯一。但对于每个环境或集合并不唯一。
- `customer_id` 的长度不能超过 256 个字符。
- 如果 `customer_id` 只包含空格或完全为空，那么会将此情况视为根本未提供 `customer_id`，并且不会返回任何错误消息。

### 使用 Discovery 工具标注数据
{: #labelingtooling}

使用 {{site.data.keyword.discoveryshort}} 工具时，可以通过 `customer_id` 字段来标注数据。单击 ![环境详细信息](images/env_icon.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->，然后在 **GDPR 数据标签**字段中，输入 `customer_id`。设置此字段后，使用此浏览器会话上传的所有数据都将使用指定的 `customer_id` 进行标注，如果关联的客户标识发生更改，那么必须手动更改此字段。

在 **GDPR 数据标签**字段中添加 `customer_id` 后，从添加的这一刻起，即会对该 URL 域中的文档、通知、知识图实体、知识图关系和训练数据进行标注，包括该域下的每个实例。不会对在添加 **GDPR 数据标签**字段之前，在 {{site.data.keyword.discoveryshort}} 工具中执行的任何操作（包括文档上传）进行标注。

**注：**如果在使用 {{site.data.keyword.discoveryshort}} 工具的 **GDPR 数据标签**字段指定 `customer_id` 后，切换了域或浏览器，清空了浏览器高速缓存或启动了无痕浏览会话，那么不会保留 `customer_id`，并且不会再对数据进行标注。如果必须切换域或浏览器，请在 **GDPR 数据标签**字段中重新输入 `customer_id`。

### 使用 Data Crawler 标注文档
{: #labelingdc}

如果已使用 Data Crawler 搜寻了任何文档，那么需要重新搜寻这些文档以添加 `X-Watson-Metadata` 头和 `customer_id`。

1. 更新 {{site.data.keyword.discoveryshort}} Data Crawler 输出适配器配置以包含 `customer_id`。请参阅[配置输出适配器](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#output-adapter)。
1. 安排搜寻。文档会使用 `X-Watson-Metadata` 头提交到 {{site.data.keyword.discoveryshort}}，并且文档会使用配置的 `customer_id` 进行标注。

## 删除标注的数据
{: #deletingdata}

数据必须使用 `customer_id` 进行标注，以便日后将其删除。

1. 使用 `DELETE /v1/user_data` 操作，并提供要删除的数据的 `customer_id`。`DELETE /v1/user_data` 将删除与该服务实例内特定 `customer_id` 关联的所有数据，如[支持标注数据的方法](/docs/services/discovery?topic=discovery-information-security#pi_methods)中所指定。另请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/discovery#delete-labeled-data){: new_window}

删除将以异步方式执行。您无法跟踪删除的进度。

要确保正确除去所有已标注的内容，应在环境中所有集合的 `processing` 和 `pending` 计数返回 `0` 之后运行 `user_delete`。

如果提供不存在的 `customer_id`，那么不会删除任何内容，而是会返回 `200 - OK` 响应。

即使在请求中包含 `X-Watson-Metadata` 头来创建环境或集合，也不会使用 `customer_id` 来标注环境和集合。只会标注环境内集合中的各个文档。因此，删除数据时，不会删除各个环境和集合。

不能使用 {{site.data.keyword.discoveryshort}} 工具来删除标注的数据。
