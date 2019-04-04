---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-03-07"

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

# 添加内容
{: #addcontent}

如何确定要使用哪种文档上传方法？
{: shortdesc}

-   如果要将内容上传与现有应用程序相集成，或者创建您自己的定制上传机制，请使用 [API](/docs/services/discovery?topic=discovery-gs-api#gs-api)。
-   如果要快速上传可本地访问的文件，请使用 [{{site.data.keyword.discoveryshort}} 工具](/docs/services/discovery?topic=discovery-getting-started#getting-started)。使用 {{site.data.keyword.discoveryshort}} 工具上传文档时，所有文档都应具有唯一的文件名。如果两个文件具有相同名称，那么在上传较新版本时，将覆盖原始版本。如果希望具有相同文件名的文档在集合中共存，那么需要指定“文档标识”。使用 API 或 Data Crawler 上传文档时，可以指定“文档标识”。
-   使用 {{site.data.keyword.discoveryshort}} 工具或 API 来连接到 Box、Salesforce、Microsoft SharePoint Online、IBM Cloud Object Storage 和 Microsoft SharePoint 2016 数据源，或执行 Web 搜寻。请参阅[连接到数据源](/docs/services/discovery?topic=discovery-sources#sources)以获取更多信息。

-   如果要对大量文件进行受管上传，或者要从支持的存储库（例如，Db2 数据库）中抽取内容，请使用 [Data Crawler](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)。

## 使用 API 或工具添加内容
{: #adding-content-with-the-api-or-tooling}

准备好向集合添加文档时，请考虑以下内容：

-   可以上传到 {{site.data.keyword.discoveryshort}} 服务的最大文件大小为 50 MB。
-   样本文档不会自动添加到集合中。如果需要将样本文档作为集合的一部分，您必须添加这些文档。（仅适用于发布[智能文档理解](/docs/services/discovery?topic=discovery-sdu#sdu)之前创建的集合。）
-   将仅扩充选择用于扩充的每个 JSON 字段的前 50,000 个字符。
-   创建集合时，可选择文档语言（缺省值为英语）。请参阅[语言支持](/docs/services/discovery?topic=discovery-language-support#language-support)以获取语言列表。您的文档将以所选语言进行扩充。不要在同一集合中混用语言。
-   {{site.data.keyword.discoveryshort}} 可以摄入以下文件类型，其他所有文档类型都会被忽略：

集合 | 轻量套餐 | 高级套餐 
---------------- | ------------------------------ | ------------------------------------------- 
发布[智能文档理解 (SDU)](/docs/services/discovery?topic=discovery-release-notes#22jan19) 之前专为 {{site.data.keyword.discoveryfull}} 创建的现有集合。| Microsoft Word、PDF、HTML 和 JSON | Microsoft Word、PDF、HTML 和 JSON 
发布 [SDU](/docs/services/discovery?topic=discovery-sdu#sdu) 之后创建的集合 | PDF、Word、PowerPoint、Excel、JSON\* 和 HTML\* | PDF、Word、PowerPoint、Excel、PNG\*\*、TIFF\*\*、JPG\*\*、JSON\* 和 HTML\* 
    
\* {{site.data.keyword.discoveryfull}} 支持 JSON 和 HTML 文档，但无法使用 SDU 编辑器编辑这些文档。要更改 HTML 和 JSON 文档的配置，您需要使用 API。有关更多信息，请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/discovery/){: new_window}。

\*\* 将扫描各个图像文件（PNG、TIFF 和 JPG），并抽取文本（如果有）。此外，还将扫描 PDF、Word、PowerPoint 和 Excel 文件中嵌入的 PNG、TIFF 和 JPEG 图像，并抽取文本（如果有）。
-   除非选择其他配置文件，否则将使用当前配置来转换集合中的文档。有关创建配置文件的信息，请参阅[定制配置](/docs/services/discovery?topic=discovery-configservice#custom-configuration)。（仅适用于发布[智能文档理解](/docs/services/discovery?topic=discovery-sdu#sdu)之前创建的集合。）
-   将文档上传到数据集合后，将使用为该集合选择的配置文件对这些文档进行转换和扩充。如果您日后决定要将集合切换到其他配置文件，您可以执行此操作，但已上传的文档仍然通过原始配置文件进行转换。切换配置文件后上传的所有文档都将使用新的配置文件。如果您希望**整个**集合使用新配置，那么需要创建新的集合，选择该新的配置文件，然后重新上传所有文档。（如果使用[智能文档理解](/docs/services/discovery?topic=discovery-sdu#sdu)，那么在您单击**将更改应用于集合**按钮之后，将提示您重新上传文档。）
-   不能指定字段的`数据类型`（例如：`text` 或 `date`）。在文档摄入期间，如果检测到索引中尚不存在某个字段，那么 {{site.data.keyword.discoveryshort}} 将根据已建立索引的第一个文档的相应字段值自动检测该字段的`数据类型`。
-   可能由于当前文档中的数据与先前摄入文档中的类似数据之间的类型不匹配，导致文档摄入失败。例如，某个字段可能在一个文档中的类型为 `date`，而在后续文档中的类型为 `string`，这会使该后续文档无法正确建立索引。
-   如果计划使用定制记号化（目前在使用 {{site.data.keyword.discoveryshort}} API 时仅可用于日语集合），那么必须在上传文档之前添加集合的记号化字典。

## 使用 Discovery 工具上传文档
{: #upload_tooling}

1.  创建集合。请参阅[准备服务以用于处理文档](/docs/services/discovery?topic=discovery-configservice#preparing-the-service-for-your-documents)。
1.  单击该集合以将其打开。
1.  单击**上传文档**按钮，然后通过拖放或浏览操作开始上传文档。

现在文档已排队等待转换和扩充。所花时间取决于集合的大小。对集合建立索引并扩充后，该集合的详细信息将显示在**概述**部分中。

-   集合中的**已识别字段**（仅限“智能文档理解”。）
-   **创建日期**和**上次更新日期**（单击**在 API 中使用此集合**可查看 `collection_id`、`configuration_id` 和 `environment_id`。）
-   集合中的**文档数**
-   **配置** - 用于转换此集合的配置文件的名称（仅适用于发布[智能文档理解](/docs/services/discovery?topic=discovery-sdu#sdu)之前创建的集合。）
-   **错误和警告**

有关如何连接到 Box、Salesforce、Microsoft SharePoint Online、IBM Cloud Object Storage 和 Microsoft SharePoint 2016 数据源或使用 {{site.data.keyword.discoveryshort}} 工具执行 Web 搜寻的信息，请参阅[连接到数据源](/docs/services/discovery?topic=discovery-sources#sources)。


## 使用 API 上传文档
{: #upload_api}

请参阅 [{{site.data.keyword.discoveryshort}} API 入门](/docs/services/discovery?topic=discovery-gs-api#gs-api)以获取逐步教程。

有关该 API 的更多信息，请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/discovery/){: new_window}。

1.  使用 `POST /v1/environments/{environment_id}/collections` 方法来创建集合。
1.  然后，使用 `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` 方法向集合添加文档。

## 搜寻 URL
{: #crawl_urls}

可以使用 {{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} {{site.data.keyword.discoveryshort}} Service [Indexing plugin for Apache Nutch ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/IBM-Watson/nutch-indexer-discovery) 来搜寻 URL 并对其建立索引。搜寻不会自动更新，因此需要定期重复执行此过程，以使索引保持最新状态。 

您还可以选择使用 beta Web Crawl 连接器。请参阅[连接到数据源](/docs/services/discovery?topic=discovery-sources#connectwebcrawl)。
