---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-25"

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

# 发行说明

发行说明提供有关 {{site.data.keyword.discoveryfull}} 服务自前发行版以来所做更改的信息。
{: shortdesc}

## 服务 API 版本控制
{: shortdesc}

API 请求需要用于获取 `version=YYYY-MM-DD` 格式日期的 version 参数。只要我们以向后不兼容的方式更改了 API，就会发布 API 的一个新的次版本。

随每个 API 请求一起发送 version 参数。服务会使用您指定日期的 API 版本，或该日期之前的最新版本。不要缺省使用当前日期。而是改为指定与兼容您应用程序的版本相匹配的日期，并使其保持不变，直到应用程序准备好用于更高版本。

当前版本为 `2018-10-15`。

## Beta 功能
{: #beta-features}

IBM 将发布分类为 Beta 或试验性的服务、功能和语言支持。这些内容可能不稳定，可能会频繁更改，并且可能随时停止使用。提供这些内容是为了供您评估其功能。Beta 或试验性功能提供的性能级别或兼容性可能与一般发布功能所提供的不同。这些功能并非旨在用于生产环境，任何此类用途由您自行承担风险。


## 更改
{: #change-log}

提供了以下新功能和对服务的更改。

## 2018 年 10 月 25 日
{: #25oct}

更改了[元素分类](/docs/services/discovery/element-classification.html)扩充项的模式。如果要使用更新的模式，您必须使用版本日期为 `2018-10-15` 或更高版本的 API 来摄入文档。{{site.data.keyword.discoveryshort}} 工具尚未使用此 API 版本（它当前使用的是 `2018-08-01`），因此使用 {{site.data.keyword.discoveryshort}} 工具摄入的文档将使用原始模式进行扩充。

## 2018 年 9 月 25 日
{: #25sept}

- 发布了 Continuous Relevancy Training，此功能使用来自用户的交互来学习如何使最相关的结果浮现。它可以自动从用户行为中学习，显著减少了提高结果相关性排名所需的工作量。请参阅 [Continuous Relevancy Training](/docs/services/discovery/continuous-training.html#crt) 以获取详细信息。

- 添加了对执行更长查询的 API 支持。这使得字符限制增加到 10,000 个字符，并且可以增加查询中的过滤器数并执行更复杂的聚集。请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query){: new_window} 和 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#federated-query){: new_window} 中的 POST 查询，以获取详细信息。

- 现在，您可以使用 API 来升级高级套餐。请参阅[升级套餐](/docs/services/discovery/upgrading.html#advanced)以获取详细信息。 

- “元素分类”扩充项更新了分类元素、合同元素以及识别到的参与方和表。请参阅[元素分类](https://console.bluemix.net/docs/services/discovery/element-classification.html)以获取更新。

- 添加了对巴西葡萄牙语的完全支持。有关更多信息，请参阅[语言支持](/docs/services/discovery/language-support.html)。

- 现在，查询 API (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`) 支持 `bias` 参数，这允许您偏向于特定结果，例如最近发布的文档。请参阅“API 参考”中的[查询集合 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query-using-get){: new_window} 方法以获取相关信息。

- 对于提供用于扩充[元素分类](/docs/services/discovery/element-classification.html#element-collection)集合的 **Default Contract Configuration** 文件，发现该文件存在 HTML 规范化方面的问题。因此，此发行版随附新的 **Default Contract Configuration**。请遵循以下步骤将新的 **Default Contract Configuration** 应用于集合。

     1. 确定哪些集合使用的是 **Default Contract Configuration** 配置文件，哪些使用的是基于 **Default Contract Configuration** 的定制配置。
     1. 记下对基于 **Default Contract Configuration** 的任何定制配置所做的更改。
     1. 由于在使用新的 **Default Contract Configuration** 文件之前，需要先从环境中删除相应的旧文件，所以请使用[删除配置 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#delete-configuration){: new_window} API 来删除与任何集合相关联的当前 **Default Contract Configuration**。此外，还请删除任何基于旧 **Default Contract Configuration** 的配置。
     1. 现在，您可以使用新的 **Default Contract Configuration** 文件。对于使用其中某个配置的每个集合，请创建一个新集合。应用新的 **Default Contract Configuration**，或者使用您在步骤 2 中所做的记录，创建基于新 **Default Contract Configuration** 的新定制配置。
     1. 将先前摄入的文件上传到原始集合。
     1. 删除旧集合。

## 2018 年 8 月 15 日
{: #15aug}

- 提供了两个新的查询运算符。`Exists` (`:*`) 可用于返回包含指定 `field` 的所有结果。`Does not exist` (`!*`) 可用于返回不包含指定 `field` 的所有结果。请参阅[查询运算符](/docs/services/discovery/query-operators.html)以获取更多信息。 

## 2018 年 8 月 2 日
{: #2aug}

- 现在，{{site.data.keyword.discoveryfull}} 使用 {{site.data.keyword.discoveryshort}} 工具连接和同步到 Box、Salesforce 和 SharePoint Online 时，支持英语、西班牙语、德语、意大利语、葡萄牙语、法语、阿拉伯语、韩语和日语集合。 

## 2018 年 7 月 31 日
 
 - 从 **2018 年 8 月 1 日**开始，{{site.data.keyword.discoveryfull}} 将采用全新的定价结构。此结构的特点是针对 {{site.data.keyword.discoverynewsfull}} 查询采用更简单的定价模型（计算中不再包含文档小时数）和分层定价。此外，标准套餐已引退，轻量套餐降低了文档和 {{site.data.keyword.discoverynewsshort}} 查询限制。定价变更无需当前的 {{site.data.keyword.discoverynewsshort}} 用户执行任何操作。请参阅 [{{site.data.keyword.discoveryshort}} 价格套餐](/docs/services/discovery/pricing-details.html)以获取详细信息。
 
**注：**API 的版本日期已更新为 `2018-08-01`。要利用新的环境大小选项（`LT`、`XS`、`S`、`MS`、`M`、`ML`、`L`、`XL`、`XXL` 和 `XXXL`），必须在使用 API 创建环境时使用此版本日期。现在，环境大小的类型为 `string`（先前类型为 `integer`）。

## 2018 年 7 月 27 日

- 发布的 [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery/watson-discovery-news.html) 新增一种语言版本：日语 (`collection_id`:`news-ja`)。{{site.data.keyword.discoverynewsfull}} 还提供了英语、西班牙语、德语和韩语版本。

## 2018 年 6 月 25 日

- 添加了用于与 Salesforce、Microsoft SharePoint Online 和 Box 数据源连接并同步的选项。这些数据源在高端环境中不可用。针对这些数据源发布了[源凭证 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#credentials-api){: new_window} 和 [配置 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#configurations-api){: new_window} API。 
  - {{site.data.keyword.discoveryfull}} 使用 {{site.data.keyword.discoveryshort}} 工具连接并同步到 Box、Salesforce 和 SharePoint Online 时，仅支持英语语言集合。[已解决](/docs/services/discovery/release-notes.html#2aug)
  - Box、Salesforce 和 SharePoint Online 的单个文档文件大小限制为 10 MB。
- 在 {{site.data.keyword.discoveryshort}} 工具中添加了新的性能仪表板。请参阅[使用性能仪表板查看度量值和改进查询结果](/docs/services/discovery/dashboard.html)。新仪表板在高端或专用环境中不可用。
- 添加了对日语的完全支持。有关更多信息，请参阅[语言支持](/docs/services/discovery/language-support.html)。

## 2018 年 6 月 22 日

- 发布了事件和反馈 API。请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#events-and-feedback-api){: new_window} 以获取更多信息。

## 2018 年 6 月 11 日

-  对于在华盛顿（美国东部）托管的应用程序，服务现在支持基于令牌的 Identity and Access Management (IAM) 认证。IAM 使用访问令牌（而不是服务凭证）向服务进行认证。有关将 IAM 令牌用于现有应用程序和新应用程序的更多信息，请参阅 [2018 年 5 月 17 日](#17May2018)发布更新。
-  现在，“元素分类”中新增一个支持的合同元素：`安全与保障`。请参阅[了解合同元素](/docs/services/discovery/element-classification.html#contract-elements)以获取详细信息。

## 2018 年 6 月 6 日

- 现在，{{site.data.keyword.discoverynewsfull}} 查询将在 `text` JSON 字段中显示每篇文章的前 50 个字。

## 2018 年 6 月 5 日
{: #5jun}

- 现在，“元素分类”可供预订高端套餐的用户使用。
- `assurance` 评级 `Low` 不再可用于“元素分类”。

## 2018 年 5 月 31 日

- 添加了对法语的完全支持。有关更多信息，请参阅[语言支持](/docs/services/discovery/language-support.html)。

## 2018 年 5 月 30 日

- 解决了 {{site.data.keyword.discoverynewsfull}} 中的已知问题。先前，查询 {{site.data.keyword.discoverynewsshort}} 时，可能会收到不正确的文档计数，因为其他语言的文档会与您所请求语言的文档一起计数。如今此问题已不复存在。
- 现在，查询 `2018 年 5 月 22 日`及之后创建的集合时，对于以下语言，{{site.data.keyword.discoveryshort}} 会返回包含特殊字符的查询结果：英语、德语、法语、荷兰语、意大利语和葡萄牙语。例如，如果查询 `aqui`，现在将收到包含 `aqui` 的结果和包含 <code>aqu&iacute;</code> 的结果。

## 2018 年 5 月 21 日

- 发布的 [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery/watson-discovery-news.html) 新增一种语言版本：德语 (`collection_id`:`news-de`)。{{site.data.keyword.discoverynewsfull}} 还提供了英语、西班牙语和韩语版本。

## 2018 年 5 月 17 日
{: #17May2018}

- 现在，{{site.data.keyword.discoverynewsfull}} 查询在 `text` JSON 字段中仅显示每篇文章的前 20 个字。

-   自 2018 年 5 月 15 日开始，服务现在支持新的 API 认证过程用于在悉尼 (**au-syd**) 托管的应用程序的服务实例。对于在其他区域中托管的应用程序，很快将启用此功能。{{site.data.keyword.Bluemix}} 正在迁移到基于令牌的 Identity and Access Management (IAM) 认证。IAM 使用访问令牌（而不是服务凭证）向服务进行认证。

   在悉尼区域中，对于以下实例，可将 IAM 访问令牌用于 {{site.data.keyword.discoveryshort}} 服务：

    -   5 月 15 日之后创建的*新服务实例*。有关更多信息，请参阅[使用 IAM 令牌进行认证](/docs/services/watson/getting-started-iam.html)。
    -   从 Cloud Foundry 迁移到由资源控制器 (RC) 管理的资源组的*现有服务实例*。5 月 15 之前创建的服务实例将继续使用服务凭证进行认证，直到您迁移这些实例。有关更多信息，请参阅[将 Cloud Foundry 服务实例迁移到资源组](/docs/resources/instance_migration.html)。

    其他区域中的所有新服务实例和现有服务实例将继续使用服务凭证 (`apikey:{apikey_value}`) 进行认证。

### 使用 IAM 访问令牌进行认证

使用 IAM 访问令牌时，您在向 {{site.data.keyword.discoveryshort}} 服务发送请求之前须进行认证。

1.  从 IBM Cloud 中获取 API 密钥。使用该密钥来生成 IAM 访问令牌。有关更多信息，请参阅[如何使用 {{site.data.keyword.watson}} 服务 API 密钥来获取 IAM 令牌](/docs/services/watson/getting-started-iam.html#iamtoken)。
1.  使用 `Authorization` 头将 IAM 访问令牌传递到 {{site.data.keyword.discoveryshort}} 服务。在该头中，通过指定 `Authorization: Bearer {access_token}` 来指示访问令牌是 `Bearer` 令牌。

    下面是使用访问令牌的简单 cURL 示例：

    ```bash
    curl -X GET
    --header "Authorization: Bearer eyJhbGciOiJIUz......sgrKIi8hdFs"
    "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    有关更多信息，请参阅[使用令牌进行认证](/docs/services/watson/getting-started-iam.html#use_token)。

### 刷新 IAM 访问令牌

生成的 IAM 访问令牌具有以下结构。可以使用 `access_token` 字段的值向服务发出经过认证的请求。

```javascript
{
  "access_token": "eyJhbGciOiJIUz......sgrKIi8hdFs",
  "refresh_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353
}
```
{: codeblock}

访问令牌的生存时间有限。`expires_in` 字段指示令牌可持续多长时间，在本例中为 1 小时。`expiration` 字段显示令牌到期的时间，格式为 UNIX 时间戳记，即指定自 1970 年 1 月 1 日（午夜 UTC/GMT）以来的秒数。

在应用程序中，使用访问令牌来发出已认证的请求之前，请检查该访问令牌的到期时间。如果该令牌已到期，那么必须先刷新访问令牌，然后才能使用。使用 `refresh_token` 字段的值可刷新访问令牌。有关更多信息，请参阅[刷新令牌](/docs/services/watson/getting-started-iam.html#refresh_token)。


## 2018 年 5 月 11 日

- 可在以下位置找到有关信息安全的详细信息：[信息安全](/docs/services/discovery/information-security.html)。
- 使用 `2018-05-04` API 版本更新解决了以下 {{site.data.keyword.discoveryfull}} Knowledge Graph `query_entities` 已知问题。仅当在 `2018-05-04` 之后摄入或替换了实体时，此修订才适用。实体可通过重新摄入旧文档或通过摄入包含这些实体的新文档来进行替换。如果未替换旧实体，那么对于 `2018-05-04` API 版本，`query_entities` 将以全部大写的形式返回。
  - 在 `query_entities` 中，先前所有实体名称都会转换为驼峰大小写。例如，实体名称“IBM Corporation”会转换为“Ibm Corporation”。如今此问题已不复存在。

## 2018 年 5 月 9 日

- 现在，样本文档会本地存储在浏览器的本地漫游数据文件夹中。有关样本文档的更多信息，请参阅[上传样本文档](/docs/services/discovery/building.html#uploading-sample-documents)。

## 2018 年 5 月 4 日

- 现在，“元素分类”中新增两个支持的合同元素：属性和起源。请参阅[了解合同元素](/docs/services/discovery/element-classification.html#contract-elements)以获取详细信息。

## 2018 年 4 月 26 日

- 解决了以下摄入问题：对于指定了扩充后 `json_normalizations` 和/或 `normalizations` 的某些情况，规范化可能会以不正确的顺序进行应用。这可能会导致使用意外的字段值对文档建立索引。如今此问题已不复存在。
- 现在，样本文档的最大文件大小为 1 MB。最大文件大小先前为 5 MB。

## 2018 年 4 月 12 日

- 现在，知识图[证据](/docs/services/discovery/building-kg.html#evidence)以及[规范化和过滤](/docs/services/discovery/building-kg.html#canonicalization)在所有集合中都可用。在 `03-05-2018` 之前创建的任何集合中，都需要重新摄入文档才能使用这两个功能。先前，您需要创建新的集合并重新摄入文档。

## 2018 年 4 月 11 日

- 现在，“元素分类”中新增两个支持的类别：`资产使用`和`通信`。请参阅[了解合同元素](/docs/services/discovery/element-classification.html#contract-elements)以获取详细信息。

## 2018 年 4 月 2 日

- 现在，样本文档将在 24 小时后自动删除，而不是在 1 个月后删除。

## 2018 年 3 月 16 日

- 添加了对德语的完全支持。有关更多信息，请参阅[语言支持](/docs/services/discovery/language-support.html)。

{{site.data.keyword.discoveryshort}} 工具：
- 添加了名为 **Default Contract Configuration** 的新配置以支持“元素分类”，可用于从 PDF 内的元素中抽取参与方、性质和类别。请参阅[元素分类](/docs/services/discovery/element-classification.html#element-collection)以获取详细信息。

更新到一般可用性：
- 文档分段已从 Beta 状态移至 GA 状态。分段限制增加到了 250 个分段。每个文档的分段数不再限于 50 个。请参阅[文档分段](/docs/services/discovery/building.html#doc-segmentation)以获取详细信息。

已知问题：
- 通配符对于包含大写字母的查询无效。例如，对于键/字段对 `{"borrower": "GOVERNMENT OF INDIA"}`，`query-borrower:*ndia` 会返回结果，但 `query-borrower:*NDIA` 不会返回结果。

## 2018 年 3 月 8 日
{: #8mar}

- Beta 版本的 {{site.data.keyword.discoveryfull}} Knowledge Graph 添加了若干功能。在 Beta 发布期间，[知识图](/docs/services/discovery/building-kg.html)功能及其关联的方法仅可用于预订**高级**套餐、**高端**套餐和所有**专用**环境的服务实例。新功能包括：
  - [实体相似度](/docs/services/discovery/building-kg.html#similarity)
  - [证据](/docs/services/discovery/building-kg.html#evidence)
  - [规范化和过滤](/docs/services/discovery/building-kg.html#canonicalization)

## 2018 年 3 月 7 日

- 解决了以下摄入已知问题：在 2 月 28 日到 3 月 6 日之间，仅使用 `id` 和 `extracted_metadata` 字段对文档的一小部分建立了索引（未对其他文档内容建立索引）。该底层问题已得到解决，但是您需要重新提交任何受影响的文档以进行摄入。没有简单的方法可识别受影响的文档。

## 2018 年 3 月 5 日
{: #5mar}

- 使用 `2018-03-05` API 版本更新解决了以下 {{site.data.keyword.discoveryfull}} Knowledge Graph 已知问题。此修订仅适用于使用 `2018-03-05` 版本更新的新创建的集合。  
  - 先前，在摄入期间，所有实体类型名称和关系类型名称都会转换为大写。例如，实体“GeoPoliticalEntity”会转换为“GEOPOLITICALENTITY”，关系“partOf”会转换为“PARTOF”。如今此问题已不复存在。

## 2018 年 3 月 1 日

- 对于高级和高端套餐，[查询扩展](/docs/services/discovery/using.html#query-expansion)限制已增加到 5,000 个查询扩展以及共 25,000 个术语。请参阅 [Discovery 价格套餐](/docs/services/discovery/pricing-details.html)以获取详细信息。

## 2018 年 2 月 28 日

- {{site.data.keyword.alchemylanguageshort}} 扩充项已于 **2018 年 3 月 1 日**废弃。
有关迁移利用 {{site.data.keyword.alchemylanguageshort}} 扩充项的现有集合和配置文件的信息，请参阅[将扩充项迁移到 {{site.data.keyword.nlushort}}](/docs/services/discovery/migrate-nlu.html)。

## 2018 年 2 月 23 日

- 添加了按文档相似度进行查询的功能。您可以通过文档标识来查询类似文档，并且可以选择通过指定字段来进一步优化相似度。请参阅[文档相似度](/docs/services/discovery/using.html#doc-similarity)以获取更多信息。

- 增强了查询结果中的 [ `highlight` 参数](/docs/services/discovery/query-parameters.html#highlight)的功能。查询结果将返回完整的语句，并按其 `score` 排序。

## 2018 年 2 月 21 日
{: #21feb}

- 先前，摄入 PDF 文档时，如果通过文档详细信息 API 在 `extracted_metadata` 对象中查询摄入通知，返回的 `file_type` 为 `html`。如今此问题已不复存在。现在返回的 `file_type` 将为 `pdf`。 

## 2018 年 1 月 26 日
{: #26jan}

{{site.data.keyword.discoveryshort}} 工具：

- 添加了通过工具中的 [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery/watson-discovery-news.html) 磁贴访问韩语和西班牙语集合的功能。先前，只能通过 API 来查询这些集合。

## 2018 年 1 月 23 日

- 添加了扩展查询范围的功能 - 例如，您可以将对“car”的查询扩展为包含“automobile”和“motor vehicle”。此外，可以替换经常拼错的术语，例如，可以将对“seabizcuit”的查询替换为“seabiscuit”。查询扩展通过 {{site.data.keyword.discoveryshort}} API 来实现。请参阅[查询扩展](/docs/services/discovery/using.html#query-expansion)以获取详细信息。  

## 2018 年 1 月 15 日

- {{site.data.keyword.discoverynewsfull}} Original 已引退不用。自 2017 年 7 月 31 日开始，该版本替换为名为 {{site.data.keyword.discoverynewsfull}} 的新版本。有关从 {{site.data.keyword.discoverynewsfull}} Original 迁移到新版本的指示信息，请参阅[从 Watson Discovery News Original 迁移](/docs/services/discovery/migrate-bwdn.html)。

## 2018 年 1 月 11 日

- 添加了对韩语的完整支持。有关更多信息，请参阅[语言支持](/docs/services/discovery/language-support.html)。

## 2017 年 12 月 15 日

- 发布了**元素分类**扩充项，用于对管理文档中的元素（语句、列表和表）进行解析，以对重要类别和类型进行分类。请参阅[元素分类](/docs/services/discovery/element-classification.html)以获取更多信息。“元素分类”不可用于预订**高端**套餐的服务实例。[已解决](/docs/services/discovery/release-notes.html#5jun)
- 添加了对简体中文和荷兰语的基本语言支持。请参阅[语言支持](/docs/services/discovery/language-support.html)以获取更多信息。目前，必须使用 API 来创建简体中文和荷兰语集合。
- 为 Data Crawler 添加了两个新参数：`proxy_host_port` 和 `read-timeout`。请参阅[配置 Data Crawler](/docs/services/discovery/data-crawler-discovery.html) 以获取详细信息。
- 摄入 PDF 文档时，可能会看到以下问题：[已解决](/docs/services/discovery/release-notes.html#21feb)
  - 查询摄入通知时，PDF 文档的 `file_type` 字段会返回为 `html`。
  - PDF 文档结果的 `extracted_metadata` 对象中的 `file_type` 字段设置为 `html`。
  - 文档详细信息 API 还会将 PDF 文档的 `file_type` 字段返回为 `html`。
- 如果摄入的是 JSON，那么不支持混合类型的数组。  

{{site.data.keyword.discoveryshort}} 工具：

- 为 Beta 版本的 {{site.data.keyword.discoveryfull}} Knowledge Graph 添加了 Visual Query Builder。请参阅[使用 {{site.data.keyword.discoveryshort}} 工具查询知识图](/docs/services/discovery/building-kg.html#querying-kg)

## 2017 年 11 月 30 日

- 发布了 Beta 版本的 {{site.data.keyword.discoveryfull}} Knowledge Graph，提供用于跨文档查询实体和关系的新端点。这包括基于上下文的搜索和相关性排名。此 Beta 功能仅可供**高级**套餐用户使用。在**专用**环境中不可用。[已解决](/docs/services/discovery/release-notes.html#8mar)。请参阅 [{{site.data.keyword.discoveryfull}} Knowledge Graph](/docs/services/discovery/building-kg.html) 以获取更多信息。可以在[此处](/docs/services/discovery/release-notes.html#beta-features)找到说明 Beta 功能的陈述。
  - {{site.data.keyword.discoveryfull}} Knowledge Graph 中的已知问题：在摄入期间，所有实体类型名称和关系类型名称都会转换为大写。例如，实体“GeoPoliticalEntity”会转换为“GEOPOLITICALENTITY”，关系“partOf”会转换为“PARTOF”。[已解决](/docs/services/discovery/release-notes.html#5mar)
- 另外发布了两种语言的 [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery/watson-discovery-news.html)：韩语 (`collection_id`:`news-ko`) 和西班牙语 (`collection_id`:`news-es`)。{{site.data.keyword.discoverynewsfull}} 韩语和西班牙语仅可通过 API 使用；有关通过 API 来查询集合的信息，请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")][Resolved] (/docs/services/discovery/release-notes.html#26jan)(https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection){: new_window}. 现在，{{site.data.keyword.discoverynewsfull}} 英语的 `collection_id` 为 `news-en`。原先，`collection_id` 为 `news` - 如果您一直在使用先前的 `collection_id`，那么它将继续有效，但是，对于新项目，您可能希望切换到新的 `collection_id`。
- 查询结果会返回 `score` 值，用于指示查询结果之间的相对相关性。从 2017 年 11 月 30 日开始，`score` 的计算方式已更改。`score` 值应该仅用于对单个搜索（而不是跨搜索或会话）中的文档进行排名。如果您已训练集合，那么会在自然语言查询的结果中返回 `score` 值。由于 `score` 指示的是查询结果之间的相对相关性，因此不应将其用作阈值。请改为使用 `confidence` 来设置阈值；confidence 指示结果相对于已训练模型的相关性。请参阅[置信度分数](/docs/services/discovery/train-tooling.html#confidence)，以获取有关设置阈值的更多信息。
- 从本发行版开始，段落检索会检测语句边界 - 它会尝试返回从语句起始处开始并在语句结尾处停止的段落。先前，许多段落会在语句中间的某个位置开始或结束。请参阅[段落](/docs/services/discovery/query-parameters.html#passages)以获取有关段落检索的更多信息。

## 2017 年 11 月 15 日
{: #15nov}

{{site.data.keyword.discoveryshort}} 工具：

- 添加了[关系抽取](/docs/services/discovery/building.html#relation-extraction)扩充项，其中包含用于合并使用 {{site.data.keyword.knowledgestudiofull}} 创建的定制关系模型的选项。
- 现在，{{site.data.keyword.discoveryshort}} 工具的[实体抽取](/docs/services/discovery/building.html#entity-extraction)扩充项包含用于合并使用 {{site.data.keyword.knowledgestudiofull}} 创建的定制实体模型的选项。
- 从 {{site.data.keyword.discoveryshort}} 工具中除去了用于创建日语集合的选项，但是保留了用于使用 {{site.data.keyword.discoveryshort}} API 来创建日语集合的选项。
- 现在，{{site.data.keyword.discoveryshort}} 工具支持联合环境。

## 2017 年 11 月 10 日

{{site.data.keyword.discoveryshort}} 工具：

- 向 {{site.data.keyword.discoveryshort}} 工具添加了用于段落检索的更多选项。现在，查询时可以指定要从中返回段落的字段、要返回的段落数以及每个段落的最大字符数。请参阅[段落](/docs/services/discovery/query-parameters.html#passages)，以获取限制、最小值和最大值的信息。

## 2017 年 11 月 8 日
{: #8nov}

所有 API 调用的版本字符串均已从 `2017-10-16` 更改为 `2017-11-07`。此版本进行了如下更改：
- 将每个查询结果中的 `score` 移至名为 `result_metadata` 的新对象。
- 如果已对查询的集合进行训练，并且该查询是自然语言查询，那么 `result_metadata` 将包含用于显示该结果的置信度分数的 `confidence` 字段。请参阅[置信度分数](/docs/services/discovery/train-tooling.html#confidence)以获取详细信息。
- 包含空格的字段（例如：`body.additional reading`）在摄入期间会被过滤掉。`notices` 描述将为 `The field 'additional reading' is invalid: whitespace, '.', '#' and ',' are invalid in a field name`。
- `result_metadata` 字段在摄入期间会被过滤掉。

## 2017 年 10 月 16 日

- 所有 API 调用的版本字符串均已从 `2017-09-01` 更改为 `2017-10-16`。此版本放弃支持将新文档上传到通过 {{site.data.keyword.alchemylanguageshort}} 扩充项扩充的现有集合，并且放弃支持创建新集合并通过 {{site.data.keyword.alchemylanguageshort}} 扩充项来扩充这些集合。使用 {{site.data.keyword.alchemylanguageshort}} 扩充的现有集合应该尽快迁移到 {{site.data.keyword.nlushort}} 扩充项。请参阅[将扩充项迁移到 {{site.data.keyword.nlushort}}](/docs/services/discovery/migrate-nlu.html#migrating-enrichments-to-natural-language-understanding) 以获取详细信息。{{site.data.keyword.discoveryshort}} 工具还会使用 `2017-10-16` 版本，请参阅下文以获取更多信息。

{{site.data.keyword.discoveryshort}} 工具：

- {{site.data.keyword.discoveryshort}} 工具将使用 `2017-10-16` API 版本字符串，因此，如果您正在使用该工具，那么无法再将文档上传到现有 {{site.data.keyword.alchemylanguageshort}} 集合，也无法在 `2017-10-16` 之后创建通过 {{site.data.keyword.alchemylanguageshort}} 扩充项扩充的新集合。如果要继续使用 {{site.data.keyword.discoveryshort}} 工具来扩充集合，请先将集合迁移到 {{site.data.keyword.nlushort}}。请参阅[将扩充项迁移到 {{site.data.keyword.nlushort}}](/docs/services/discovery/migrate-nlu.html#migrating-enrichments-to-natural-language-understanding) 以获取详细信息。
- **数据模式资源管理器**会显示 {{site.data.keyword.discoverynewsfull}} 集合中多种扩充项的样本查询。现在，该资源管理器还有**显示更多值**链接，用于显示 {{site.data.keyword.discoverynewsfull}} 中该扩充项的更多示例值。
- 多种生产力增强功能，包括在**管理数据**屏幕上组合集合统计信息、错误和警告以及数据洞察。
- 添加了在文档完成处理后显示警报的消息。

## 2017 年 10 月 9 日

- API 中提供了新的聚集度量值 `unique_count`。它将返回集合中所指定字段的唯一实例计数。请参阅 [unique_count](/docs/services/discovery/query-aggregations.html#unique_count) 以获取更多信息。

{{site.data.keyword.discoveryshort}} 工具：

- 现在，**Visual Query Builder** 中支持 Histogram 和 Timeslice 聚集。您还可以选择对 Timeslice 查询开启异常检测。
- **数据模式资源管理器**会显示所选扩充项的样本查询。现在，该资源管理器还有“**显示更多值”链接，用于显示该扩充项的更多示例值。
- 添加了汉堡包菜单，用于更快地浏览**管理数据**、**查看数据模式**和**构建查询**屏幕。

### 2017 年 10 月 3 日

- 现在，提供了文档分段功能。请参阅[使用文档分段拆分文档](/docs/services/discovery/building.html#doc-segmentation)。

### 2017 年 9 月 29 日

- 2017 年 9 月 29 日，{{site.data.keyword.discoveryshort}} 在`德国`区域推出。为了遵守欧盟的数据法规，此区域中不支持 AlchemyLanguage 扩充项。
- 已知问题：查询字段不能包含空格。在 {{site.data.keyword.discoveryshort}} 中编写查询时，如果任何查询字段包含空格（例如，`body.additional reading`），那么您将收到 `400: Invalid query syntax error`。[已解决](/docs/services/discovery/release-notes.html#8nov)

### 2017 年 9 月 25 日

- 现在提供了高端价格套餐。有关更多信息，请参阅 [{{site.data.keyword.discoveryshort}} 价格套餐](/docs/services/discovery/pricing-details.html)。
- 添加了在同一环境中跨集合查询、列出字段和查询通知的功能。请参阅[查询多个集合](/docs/services/discovery/using.html#multiple-collections)以获取详细信息。
- [语言支持](/docs/services/discovery/language-support.html)上提供了 {{site.data.keyword.discoveryshort}} 的语言支持信息。

{{site.data.keyword.discoveryshort}} 工具：
- Visual Query Builder 已从 Beta 状态移至 GA 状态。目前，Visual Query Builder 不支持 Filter、Timeslice 和 Histogram 聚集。请单击**包含对结果的分析**，然后单击**构建查询**屏幕上的**使用查询语言编辑**来编写这些聚集。
- 添加了对 {{site.data.keyword.discoverynewsfull}} 查询执行去重的 Beta 功能。
- 除了英语、德语和西班牙语语言集合之外，现在还可以创建阿拉伯语、法语、意大利语、韩语、日语和巴西葡萄牙语集合。
- 已知问题：{{site.data.keyword.discoveryshort}} 工具不支持联合环境。[已解决](/docs/services/discovery/release-notes.html#15nov)

### 2017 年 9 月 14 日

{{site.data.keyword.discoveryshort}} 工具：

- 添加了“数据模式资源管理器”，用于显示已变换文档中的字段和值。使用 Discovery Query Language 构建查询之前，可以使用这些信息来了解集合的数据结构。数据模式可以通过两种方式来查看：按文档（“文档”视图）或按字段（“集合”视图）。要访问“数据模式资源管理器”：在**我的数据洞察**屏幕上，单击**查看数据模式**按钮，或单击左侧的**查看数据模式**图标。

### 2017 年 9 月 6 日

- 添加了对查询返回的文档执行去重的 Beta 功能。此 Beta 功能适用于专用集合和 Watson Discovery News 集合。请参阅[从查询结果中排除重复文档](/docs/services/discovery/query-parameters.html#deduplication)以获取详细信息。

目前，文档去重仅作为 Beta 功能受支持。请参阅本文档顶部关于 Beta 功能的陈述以获取更多信息。

### 2017 年 8 月 31 日

- 所有 API 调用的版本字符串均已从 `2017-08-01` 更改为 `2017-09-01`。此版本包含将用于在预览和摄入期间过滤掉以下无效 JSON 字段的更新，以便仅摄入有效的 JSON 字段。请将您的版本字符串更新为 `2017-09-01`，以避免冲突和可能的错误。

   - 顶级的 `id`、`score` 和 `highlight`（您可以继续通过`添加文档`功能使用文档标识将文档添加到集合中）。请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#add-doc){: new_window} 以获取详细信息。
   - 带 `_` 前缀的顶级字段名称（因此，按标识查询文档时，可以查询 `id`，而不是 `_id`。）
   - 字段名称中有 `#` 和 `,`
   - 带 `+` 和 `-` 前缀的字段名称
   - 字段名称中有 `"` `"` 空值

**注：**如果 JSON 文档在字段名称中包含这些字符，或者包含顶级 `id`、`score` 和 `highlight`，那么在将文档添加到集合之前，需要除去这些字符，否则这些字段将为空。您可以先创建定制配置并规范化 JSON，然后将文档添加到集合以避免此问题。请参阅[定制配置](/docs/services/discovery/building.html#custom-configuration)。此外，文件名中包含标点字符 `?`、`:` 或 `#` 的文档将在摄入时导致错误。在摄入名称中包含这些字符的任何文档之前，请先对这些文档重命名。

- 更新了 `natural_language_query` 的检索方法，可通过匹配具有相关语义的字词来提高结果的相关性。此更新仅影响没有进行相关性训练的集合。如果使用的是 `natural_language_query` 并且尚未执行相关性训练，那么您可能会看到返回结果的顺序有所改进。

{{site.data.keyword.discoveryshort}} 工具：

- 更改了查询构建器，使得在 Discovery Query Language 和“自然语言查询”选项之间以及在查询、过滤器和聚集之间切换更容易。


### 2017 年 8 月 25 日

- 现在，`passages` 数组包含 `field`、`start_offset` 和 `end _offset`。`field` 是从中抽取段落的字段的名称。`start_offset` 是字段内段落文本的起始字符。`end_offset` 是字段内段落文本的结束字符。

{{site.data.keyword.discoveryshort}} 工具：可以在**构建查询**屏幕上找到此查询构建增强功能。

-  添加了使用可视构建器在 {{site.data.keyword.discoveryshort}} Query Language 中编写查询的 Beta 功能。单击**搜索文档**和**限制查询的文档**部分中的**以可视方式构建**可试用此功能。以可视方式构建查询时，该查询将显示在其下方的 **{{site.data.keyword.discoveryshort}} Query Language** 中。

   目前，Visual Query Builder 仅作为 Beta 功能受支持。请参阅本文档顶部关于 Beta 功能的陈述以获取更多信息。

### 2017 年 8 月 18 日

{{site.data.keyword.discoveryshort}} 工具：

- 添加了对在 [2017 年 8 月 11 日](/docs/services/discovery/release-notes.html#11aug)引入的 Beta Visual Aggregation Builder 的嵌套聚集和条件的支持。每个聚集行的条件限制为 3 个。

   目前，Visual Aggregation Builder 仅作为 Beta 功能受支持。请参阅本文档顶部关于 Beta 功能的陈述以获取更多信息。

### 2017 年 8 月 11 日
{: #11aug}

{{site.data.keyword.discoveryshort}} 工具：

下面两个功能都是查询构建增强功能，可在**构建查询**屏幕上找到。

- 添加了用于从一组预构建的样本查询和聚集中选择查询的选项。单击右上角的**使用样本查询**可访问该列表。如果要查询专用数据集合，那么样本将使用在集合中找到的 `top entities`、`categories` 等。这些查询可以用作编写您自己查询的起始点。样本查询可用于 {{site.data.keyword.discoverynewsfull}} 集合和专用集合。

-  添加了使用可视构建器编写聚集的 Beta 功能。单击**使用 {{site.data.keyword.discoveryshort}} Query Language 编写聚集查询**字段上方的**以可视方式构建**可试用此功能。以可视方式构建聚集时，查询将显示在其下方的 **{{site.data.keyword.discoveryshort}} Query Language** 中。  

   目前，Visual Aggregation Builder 仅作为 Beta 功能受支持。请参阅本文档顶部关于 Beta 功能的陈述以获取更多信息。

### 2017 年 7 月 31 日

- 发布了新版本的 {{site.data.keyword.discoverynewsfull}}。原始版本已重命名为 {{site.data.keyword.discoverynewsfull}} Original，该版本已引退，其终止服务日期为 **2018 年 1 月 15 日**。请参阅[从 Watson Discovery News Original 迁移](/docs/services/discovery/migrate-bwdn.html)以获取迁移指示信息。
  **注：**如果已创建 {{site.data.keyword.discoveryshort}} 的新实例，那么您只有权访问新版本的 {{site.data.keyword.discoverynewsfull}}。

- 发布了新的 {{site.data.keyword.discoveryfull}} 价格套餐。请参阅 [{{site.data.keyword.discoveryshort}} 价格套餐](/docs/services/discovery/pricing-details.html)以获取详细信息。

- 所有 API 调用的版本字符串均已从 `2017-07-19` 更改为 `2017-08-01`。此版本包含对新价格套餐和新版本 Watson Discovery News 的更新。请更新版本字符串，以避免冲突和可能的错误。

### 2017 年 7 月 19 日

 - 在 2017 年 8 月 1 日公告的价格更改中，当前位于不推荐使用的 **30 天免费试用**套餐的用户将自动迁移到**轻量**套餐。执行此转换后，现有用户可能已达到或超过轻量套餐对文档数_（2000 个）_、存储量 _(200 Mb)_ 或集合数_（2 个）_的限制。如果您已超过**轻量**套餐的限制，那么将无法向服务添加任何额外的内容，但仍可以查询集合。您可以使用 {{site.data.keyword.discoveryshort}} 工具或 API 来查看所有这些限制的当前状态。为了能够继续向 {{site.data.keyword.discoveryshort}} 实例添加内容，您必须执行以下其中一个操作：
   - 除去集合和/或文档，使其数量不超过**轻量**套餐的限制。
    可以使用 [delete-doc](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-doc) 方法通过 API 来逐个删除文档，也可以使用 [delete-collection](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-collection) 方法通过工具或 API 来删除整个集合。
   - 将套餐升级到满足您存储需求的级别。
 - 环境大小为 **`1`**、**`2`** 或 **`3`** 的客户将自动迁移到**高级**套餐。

### 2017 年 7 月 17 日

 - 以下功能已从 Beta 状态移至 GA 状态：

   - 相关性训练
   - 自然语言查询
   - 突出显示

 - 自本发行版开始，{{site.data.keyword.discoveryfull}} 将其扩充项机制从 {{site.data.keyword.alchemylanguageshort}} 更改为 {{site.data.keyword.nlushort}}。{{site.data.keyword.alchemylanguageshort}} 处于不推荐使用的过程中，所以您应该尽快开始使用 {{site.data.keyword.nlushort}}。请参阅[从 {{site.data.keyword.alchemylanguageshort}} 扩充项迁移到 {{site.data.keyword.nlushort}} 扩充项](/docs/services/discovery/migrate-nlu.html)，以获取详细信息。
   **注：**与 Watson Knowledge Studio 集成时，仍必须使用 {{site.data.keyword.alchemylanguageshort}} 扩充项配置。请参阅[与 {{site.data.keyword.knowledgestudiofull}} 集成](/docs/services/discovery/integrate-wks.html)以获取详细信息。

 - 所有 API 调用的版本字符串均已从 `2017-06-25` 更改为 `2017-07-19`。此版本在创建集合时支持 NLU 缺省配置。在先前的版本中，应该仍可以使用 {{site.data.keyword.alchemylanguageshort}} 进行扩充。

    缺省配置已更新为使用 {{site.data.keyword.nlushort}}。您应该尽快更新版本字符串，以避免冲突和可能的错误。

 - Discovery 工具：

    通过 {{site.data.keyword.alchemylanguageshort}} 扩充项扩充的集合的洞察卡不会再自动更新。必须将集合迁移到 {{site.data.keyword.nlushort}} 扩充项才可更新洞察卡。

    如果在 **2017 年 7 月 18 日**之前创建了集合并应用了**缺省配置**，那么该集合已使用 {{site.data.keyword.alchemylanguageshort}} 扩充项扩充。如果在此日期之后将**缺省配置**应用于集合，那么将使用 {{site.data.keyword.nlushort}} 扩充项（在工具中配置名称将切换到 **Default Configuration with NLU**）。由于 {{site.data.keyword.alchemylanguageshort}} 扩充项已不推荐使用，因此不应将其用于新的集合。

### 2017 年 6 月 30 日
{: #30jun}

 -  2017 年 5 月 5 日作为 Beta 功能引入的实体规范化功能已移至 GA 状态。请参阅[创建定制配置以规范化实体](/docs/services/discovery/normalize-entities.html)以获取详细信息。

### 2017 年 6 月 23 日

 - 所有 API 调用的版本字符串均已从 `2016-12-01` 更改为 `2017-06-25`。如果集合的语言设置为德语 (`de`) 或西班牙语 (`es`)，那么新的版本字符串将支持相应语言的扩充项。先前，所有扩充项都以英语执行，而不考虑集合的语言设置。

    如果您未使用非英语语言的扩充项，那么可以继续使用 `2016-12-01` 版本字符串。但是，您应该尽快更新此版本字符串，以避免未来潜在的冲突。

 - 现在，异常检测可作为 GA 功能并以 `timesliice` 聚集的一部分提供。请参阅[时间片异常检测](/docs/services/discovery/query-aggregations.html#anomaly-detection)以获取详细信息。

 - Discovery 工具：

   - 添加了使用 Discovery 工具（相关性工具）提高查询结果相关性的 Beta 功能。请参阅[使用 Discovery 工具改进查询结果的相关性](/docs/services/discovery/train-tooling.html)。

### 2017 年 6 月 19 日

  - Discovery 工具：

    - 添加了用于将新集合中文档的语言指定为英语、西班牙语或德语的选项。要使用此选项，请在**命名新集合**对话框中，选择**选择文档语言**。

    - 向**构建查询**屏幕中添加了**摘要**选项卡。**摘要**选项卡显示现有 **JSON** 选项卡中提供的完整查询结果的概述。**摘要**显示内容将根据查询和扩充项而变化。可以显示的信息包括：文档名称或标识、聚集统计信息、按相关性顺序排列的文档段落以及按扩充项列出的结果。

    - 向**构建查询**屏幕中添加了“自然语言查询”选项。要使用此选项，请单击**搜索文档**部分中的**以简明语言提问**，这将显示一个字段，您可以在其中输入问题。现在，可以通过单击**使用 Discovery Query Language** 按钮来访问原始查询字段（原先名为**输入查询或关键字**）。

    - **构建查询**屏幕已重新设计，但保留了所有字段和选项。下面是字段的旧名称和新名称。

|**旧字段名称**|**新字段或部分名称**|
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
|编写和运行查询|搜索文档|
|缩小查询结果范围（过滤器）|限制查询的文档|
|对查询结果分组（聚集）|包含对结果的分析|
|要显示的字段|名称未更改，但移至新的**定制显示选项**部分。|
|要返回的文档数（计数）|要返回的文档数 [此字段已移至**定制显示选项**部分。]|
|包含匹配的段落|包含相关段落 [此字段已移至**定制显示选项**部分。]|
|要在开头跳过的查询字段数（偏移量）|要在开头跳过的查询结果数 [此字段已移至**定制显示选项**部分。]|

### 2017 年 6 月 5 日

 - 现在，Watson Discovery News 查询在 `text` 和 `alchemyapi_text` JSON 字段中仅显示每篇文章的前 150 个字。`blekko.snippet` 字段将仅显示片段数组的第一个语句。

### 2017 年 5 月 30 日
{: #30may}

 - 查询 API 上的 `passages` 参数已从 Beta 状态移至 GA 状态。

### 2017 年 5 月 25 日

 - Discovery 工具：在本发行版中，添加了查询字段突出显示。此功能将向“结果”窗格的 JSON 中的字段名称添加黄色突出显示。对于每个结果，所有已查询或已过滤的字段都会突出显示，即便字段的内容与查询并不匹配也是如此。在聚集中使用的任何字段也会在查询结果中突出显示，但仅突出显示第一个聚集操作。

### 2017 年 5 月 10 日

 - 现在，`query` 和 `notices` 方法支持 `highlight` 参数。此参数为布尔值。在运行查询并将 `highlight` 指定为 `true` 时，服务将返回包含新 `highlight` 字段的输出，其中与查询匹配的字词将打包在 HTML `*`（强调）标记中。请参阅[查询参数](/docs/services/discovery/query-parameters.html#highlight)以获取详细信息。

 - 删除环境可能仅部分完成，这会导致无法创建新环境的情况发生，因为每个服务实例只允许一个环境。如果您尝试删除环境，然后创建环境，但是看到其中任一操作卡在 `pending` 状态，说明很可能遇到了此问题。要解决此问题，请重新运行删除操作以完成删除，然后再创建新环境。

### 2017 年 5 月 8 日

 - 更新了情绪语气分数模型，以提高情绪分析 (`docEmotion`) 扩充项的精度。扩展了训练数据集，并且变更了特征工程，因此模型在基准数据集上的精度更高。

### 2017 年 5 月 5 日

 - 现在，实体规范化可用于 Discovery 服务，该服务使用 Watson Knowledge Studio 生成的定制模型。实体规范化用于针对源文档中同一人或同一对象的不同引用插入规范化（规范）名称。请参阅[创建定制配置以规范化实体](/docs/services/discovery/normalize-entities.html)以获取详细信息。

     **注：**目前，实体规范化仅作为 Beta 功能受支持。请参阅本文档顶部关于 Beta 功能的陈述以获取更多信息。[已解决](/docs/services/discovery/release-notes.html#30jun)

{{site.data.keyword.discoveryshort}} 工具：

 - 工具错误日志不再限制为最多八 (8) 页结果。如果文档名称不可用，错误日志仍会显示文档标识。

 - 配置名称限制为 50 个字符，并且必须包含字符 `[a-zA-Z0-9-_]`。 

 - 先前仅通过 API 可用的 `passages` 参数现在可通过工具以及 API 使用。

### 2017 年 4 月 25 日

  - 现在，服务支持提供*训练数据*来提高查询结果的准确性。向 Discovery 实例提供训练数据时，服务会使用高级 Watson 算法来确定最相关的结果。添加更多训练数据时，服务实例所返回的结果将变得更准确、更复杂。请参阅[改进查询结果的相关性](/docs/services/discovery/train.html)和 [API 参考](http://www.ibm.com/watson/developercloud/discovery/api/v1/#training-data)以获取相关信息。

  - 现在，在 Beta 发行版中，API 支持 `natural_language_query` 参数。此参数支持以自然语言（而不是 Discovery 服务的查询语言）指定查询。请参阅“API 参考”中的[查询集合](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query-using-get)方法以获取相关信息。

  - 文档更新和勘误表。

### 2017 年 4 月 14 日

向查询 API (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`) 添加了增强功能。请参阅“API 参考”中的[查询集合](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query-using-get)方法以获取相关信息。

  - 现在，查询 API 支持 `passages` 参数。如果此参数设置为 `true`，那么查询将从集合中的文档返回一组最相关的段落。这些段落通过复杂的 Watson 算法生成，用于确定查询所返回的所有文档中最佳的文本段落。这使您能够更精确地找到信息和上下文。请参阅“API 参考”中的[查询集合](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query-using-get)方法以获取相关信息。

    - 在查询中指定 `passages=true` 可能导致性能下降，因为增加了抽取段落的处理。对于较大的环境，对性能的影响较小。

    - 仅专用集合上支持 `passages` 参数。Watson Discovery News 集合中不支持此参数。

    - 目前，`passages` 参数最多返回 10 个结果。无法更改返回的结果数。[更新](/docs/services/discovery/query-parameters.html#passages_count)

    - `passages` 参数从集合中任一给定文档最多返回三 (3) 个段落。如果一个文档包含三个以上的其他相关段落，此参数不会返回这些段落。

### 2017 年 4 月 7 日

- 现在，查询 API (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`) 支持 `sort` 参数，此参数用于指定文档中要排序的字段的逗号分隔列表。请参阅“API 参考”中的[查询集合 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query-using-get){: new_window} 方法以获取相关信息。
- 现在，查询聚集的 `timesliice` 参数可正确处理 UNIX 戳记格式的日期。请参阅[查询参考](/docs/services/discovery/query-reference.html#aggregations)，以获取有关聚集和 `timeslice` 参数的信息。
- 改进了错误消息。
- 更新了服务的 Java SDK。请参阅 [API 参考](http://www.ibm.com/watson/developercloud/discovery/api/v1/?java)以获取详细信息。
- 现在，关于查询中使用通配符的以下限制已得到修正，可正常运作：

  - 在任一给定查询中只能使用一个通配符。例如，`query-month:*ctober` 有效，但 `query-month:*ctobe*` 会生成解析错误。
  - 通配符对于包含大写字母的查询无效。例如，对于键/字段对 `{"borrower": "GOVERNMENT OF INDIA"}`，`query-borrower:*ndia` 会返回结果，但 `query-borrower:*NDIA` 不会返回结果。

**注：**查询中的短语内没必要使用通配符。例如，对于键/字段对 `{"borrower": "GOVERNMENT OF TIMOR"}`，`query-borrower:"GOVERNMENT OF TIMOR"` 会返回结果，但 `query-borrower:"GOVERNMENT OF TI*OR"` 不会返回结果。使用通配符不适用于短语，因为短语的引号 (`"`) 所括起的所有字符都会进行转义。

### 2017 年 3 月 24 日

- 向 Discovery 工具中的“我的数据洞察”屏幕添加了过滤

### 2017 年 3 月 15 日

发现了以下已知问题。

-  从 HTML、PDF 和 Word 文档摄入的所有字段的类型均确定为 **string**。JSON 字段和计算字段（如观点分数）的类型根据定义确定。[更新](/docs/services/discovery/adding-content.html#adding-content-with-the-api-or-tooling)
- 目前，`preview` 操作不会检查提交的 JSON 文档中的嵌套 JSON 数组。服务目前不支持嵌套 JSON 数组，因此具有嵌套数组的文档可以成功通过 `preview` 操作，但会在尝试摄入时失败。请参阅[我可以上传 JSON 数组吗？](/docs/services/discovery/troubleshooting.html#array)
- 如果遇到消息为 `unsupported text language` 的摄入错误，请使用 `"language": "english"` 扩充选项更新配置，以强制将所有文本解释为英语，如以下示例所示。[更新](/docs/services/discovery/migrate-nlu.html)
```json
"enrichments": [
   {
     "enrichment": "alchemy_language",
     "source_field": "author.label",
     "options": {
       "extract": "taxonomy,entity,relation,doc-emotion,doc-sentiment,concept,keyword",
       "sentiment": true,
       "quotations": true,
       "language": "english"
     }
   }
 ]
```
{: codeblock}

修正了以下错误。

- 提高了服务的性能和稳定性。

### 2017 年 3 月 8 日

 - 优化了后端（包括添加新的超时）以提高总体性能。
 - 修正了导致可用（大小为 `0`）的环境报告 `pending` 环境状态（不管实际状态是什么）的错误。
 - 目前，{{site.data.keyword.discoveryshort}} 支持的唯一本地语言是美国英语 (`en_US`)。[更新](/docs/services/discovery/language-support.html)

### 2017 年 3 月 3 日

- 向 Discovery 工具添加了“我的数据洞察”屏幕。

### 2017 年 2 月 26 日

-     改进了 {{site.data.keyword.discoverynewsshort}} 环境的性能。
-  {{site.data.keyword.discoverynewsshort}} 服务一次仅返回 50 个结果。作为变通方法，请在查询中使用 `offset` 参数来逐页浏览结果。
-  可以使用以下命令向单个文档提交新配置：

```bash
curl -X POST -u apikey:{apikey_value} -F "file=@wikipedia-sample.html" -F "configuration=$(cat config.json)" "https://gateway.watsonplatform.net/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2016-12-01"
```
{: pre}
-  服务的 PDF 和 Word 转换器将创建 HTML 作为中间步骤。在最终变换为规范化 JSON 之前，服务可以对中间 HTML 应用其他变换和规范化。

修正了以下错误。

-  改进了错误代码。
-  更正了若干文档错误。

### 2017 年 2 月 16 日

-  现在，您可以使用 CSS 选择器来选择 JSON 字段，然后向这些字段应用扩充项。请参阅[使用 CSS 选择器抽取字段](/docs/services/discovery/building.html#using-css)以获取相关信息。
-  现在，您可以通过将新的 `size:X` 参数传递给 [update-environment 方法](http://www.ibm.com/watson/developercloud/discovery/api/v1/#update_environment)来增大环境的大小，其中 `X` 是 0 到 3 之间的整数。请参阅 [create-environment 方法](http://www.ibm.com/watson/developercloud/discovery/api/v1/#create_environment)，以获取有关环境大小和属性的信息。[更新](/docs/services/discovery/pricing-details.html)

    **注：**不能缩小现有环境的大小。如果要缩小环境的大小，请联系 {{site.data.keyword.IBM}} 支持以获取帮助。

-  提供了新的查询运算符。`::!` 运算符已添加为一元“不等于”运算符。例如，现在可以运行 `query=field::!value`（不等于）。先前，唯一的排除运算符是 `:!`，表示“不包含”运算符（例如，`query=field:!value`）。

修正了以下错误。

-  应用了安全性更新。
-  改进了搜索警报的状态消息。

### 2017 年 2 月 1 日

以下说明专门适用于 Data Crawler 1.3.0 发行版。[更新](/docs/services/discovery/data-crawler.html)

-   Data Crawler 可记录用于上传文档的 `document_id` 值以及上传的状态。转换通知不会在日志以外的位置持久存储。目前不存在与这些数据交互的工具，但如果时间许可，应该会开发此类工具。数据可通过 H2 数据库进行访问，该数据库可能配置为使用远程 DBMS。

### 2017 年 1 月 16 日

以下说明专门适用于 Data Crawler 1.2.5 发行版。[更新](/docs/services/discovery/data-crawler.html)

-  Data Crawler 可以选择在上传文件后立即轮询文档状态。此检查是搜寻器“上传文档”概念的一部分，所以在启用此检查后，搜寻器同时上传的文档数几乎不可能多于 {{site.data.keyword.discoveryshort}} 服务可以为用户同时处理的文档数。

    `check_for_completion` 功能的副作用是，在文档失败时，搜寻器还可以向用户显示文档失败的原因。附加到已成功上传但处理失败的文档的任何通知都会显示在搜寻器日志中。这些通知不会导出到可处理的文件，但如果您建议提供这种功能，IBM 会积极考虑。

### 2017 年 1 月 5 日

以下说明描述了在 2016 年 12 月 15 日 GA 发行版之后确定的问题。

[更新：API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}

-   如果使用 `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` 或 `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]` 调用来添加文档，那么该调用会返回文档标识和 **processing** 状态。如果随后使用 `GET /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]` 调用查询文档，那么状态将保持为 **processing**，直到完成摄入，此时状态将更改为 **available**。

    如果使用 `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]` 调用来**更新**现有文档，那么对应的 **GET** 调用将返回 `available` 状态，即便服务尚未完全处理更新的文档。`available` 状态可以指原始文档或更新的文档。除非更新操作返回错误，否则目前无法确定已更新文档的状态。

        您可以在提交文档更新后但尝试查询更新的内容之前最长等待 10 分钟，从而解决此问题。


### 2016 年 12 月 15 日的一般可用性发行版

以下说明适用于 {{site.data.keyword.discoveryfull}} 服务的一般可用性 (GA) 发行版。

#### 一般说明
[更新：添加内容](/docs/services/discovery/adding-content.html)

请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window} 以了解当前 API 版本。

[更新：与 {{site.data.keyword.knowledgestudiofull}} 集成](/docs/services/discovery/integrate-wks.html)。

-   目前，无法指定字段的数据类型。所有字段都作为文本（数据类型为 **string**）建立索引。 
-   如果使用 API 来处理服务，那么必须为每个调用指定 API 版本。当前 API 版本为 **2016-12-01**。 

    **注：**在 GA 发行版中未强制实施特定版本，但仍必须列出此版本，以支持与未来发行版兼容。

-   可以将服务与使用 {{site.data.keyword.knowledgestudiofull}} 创建的定制模型配合使用。定制模型可用于扩充摄入的文档。必须使用 API 将定制模型与 {{site.data.keyword.discoveryshort}} 服务集成；无法使用工具来执行此集成。

#### 数据管理
[更新](/docs/services/discovery/pricing-details.html)

-   搜索索引未加密。
-   用户无法控制备份和复原功能。

#### 环境
[更新](/docs/services/discovery/pricing-details.html)

-   每个服务实例仅可创建一个环境，以上传您自己的数据。
-   {{site.data.keyword.discoveryshort}} 服务位于单个可用性区域（美国南部）。
-   目前，专用和高端套餐不可用。

#### 环境大小调整
[更新](/docs/services/discovery/pricing-details.html)

-   仅当创建新环境时，才能选择环境大小。目前，用户无法调整环境的大小。
-   选择有更多 RAM 的环境大小可提高性能。
-   目前，没有可用于特定用例的规定性大小调整建议。
-   {{site.data.keyword.knowledgestudiofull}} 模型的定制大小调整不是自助服务。请联系 {{site.data.keyword.IBM}} 代表以获取更多信息。

#### 摄入限制
[更新](/docs/services/discovery/pricing-details.html)

-   目前，摄入速率限制为 100 个并发文档摄入操作。用于将文档提交给服务供摄入的应用程序需要考虑 HTTP 429 错误，并相应地调低摄入请求速率。
-   {{site.data.keyword.alchemylanguageshort}} 扩充项限制为每个字段的前 50 KB。
-   {{site.data.keyword.knowledgestudiofull}} 定制模型中的扩充项不受限制，但会将文档拆分成 10 KB 的区块。不会跨区块边界对关系进行注释。

#### 查询限制
[更新](/docs/services/discovery/using.html#query-concepts)

-   过多查询负载可能会导致搜索索引过程自动重新启动。
-   发出查询的应用程序必须对并发查询数强制实施合理的限制。

### 已知问题
[更新：API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}

[更新：工具](/docs/services/discovery/getting-started-tool.html)

[更新：Data Crawler](/docs/services/discovery/data-crawler.html)

[更新：扩充项](/docs/services/discovery/building.html#adding-enrichments)

[更新：添加内容](/docs/services/discovery/adding-content.html)

-   无法使用工具来删除文档。如果需要删除文档，必须使用 API 的[删除文档](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-doc)方法，如“API 参考”中所述。

-   目前，API 不支持获取文档摄入期间所生成通知（警告和错误）的列表。因此，工具无法显示摄入通知列表，也无法轻松确定 Data Crawler 搜寻到的哪些文档（如果有）未能摄入。 
-   文档状态信息不一定准确。
    -   如果摄入操作所用时间超过配置的超时（10 分钟），那么在摄入操作完成之前，服务会报告文档对于服务未知。操作完成后，文档状态可用且准确。
    -   对于已成功建立索引但生成了错误的文档，在文档完全落实到索引之前，其状态可能在短时间内为**失败**。文档落实到索引后，列出的状态是准确的。
-   无法使用工具来替换特定文档。如果您尝试这样做，那么第二个文档将作为单独的文档上传。如果您使用的是 API 并且知道要替换的文档的标识，那么可以执行此操作；请参阅“API 参考”中的[更新文档](http://www.ibm.com/watson/developercloud/discovery/api/v1/#update-doc)。如果您使用的是 Data Crawler，那么通过与先前文档相同的 URL 来上传更新后的文档将替换原始文档。
-   如果是使用工具来编辑配置中的扩充项，那么只能编辑用于抽取的扩充项。如果要添加或编辑其他扩充项（例如，{{site.data.keyword.knowledgestudiofull}} 模型中的定制扩充项），那么必须使用 API。请参阅“API 参考”中的[更新配置](http://www.ibm.com/watson/developercloud/discovery/api/v1/#replace_configuration)方法以获取相关信息。
-   以下说明专门适用于 Data Crawler。 
    -   如果 Data Crawler 遇到上传失败，它会重试上传。
    -   对于已成功上传但无法转换或建立索引的文档，Data Crawler 无法重试上传。
    -   Data Crawler 没有功能用于检查下游状态并尝试重新上传在下游失败的 URL。
    -   无法轻松确定 Data Crawler 已摄入哪些文档。例如，如果针对 500 个文档的集合运行 Data Crawler，那么 Data Crawler 可能会报告 65 个文档提交失败，共收集 212 个文档。其余 223 个文档的状态不确定。

        提供了变通方法，但此方法比较复杂，涉及直接调用 API。请联系 {{site.data.keyword.IBM}} 支持以获取帮助。
-   用于 {{site.data.keyword.discoveryshort}} 的 Java、Python 和 Node.js SDK 未提供缺省 REST (cURL) API 提供的所有功能。并非所有 cURL 方法都在非 cURL SDK 中具有等效方法，也并非所有非 cURL 方法都提供其 cURL 等效项具有的所有相同功能。换言之，目前 Java、Python 和 Node.js SDK 仅提供 cURL API 的一部分功能。
-   如果使用 Word 转换器，那么使用 `style` 键来匹配标题要比使用 `level` 键准确、高效得多。
