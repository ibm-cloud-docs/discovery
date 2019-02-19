---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-15"

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

# 添加内容

如何确定要使用哪种文档上传方法？
{: shortdesc}

-   如果要将内容上传与现有应用程序相集成，或者创建您自己的定制上传机制，请使用 [API](/docs/services/discovery/getting-started.html)。
-   如果要快速上传可本地访问的文件，请使用 [{{site.data.keyword.discoveryshort}} 工具](/docs/services/discovery/getting-started-tool.html)。使用 {{site.data.keyword.discoveryshort}} 工具上传文档时，所有文档都应具有唯一的文件名。如果两个文件具有相同名称，那么在上传较新版本时，将覆盖原始版本。如果希望具有相同文件名的文档在集合中共存，那么需要指定“文档标识”。使用 API 或 Data Crawler 上传文档时，可以指定“文档标识”。
-   使用 {{site.data.keyword.discoveryshort}} 工具或 API 来连接到 Box、Salesforce 和 Microsoft SharePoint Online 数据源。请参阅[连接到数据源](/docs/services/discovery/connect.html)以获取更多信息。

-   如果要对大量文件进行受管上传，或者要从支持的存储库（例如，Db2 数据库）中抽取内容，请使用 [Data Crawler](/docs/services/discovery/data-crawler.html)。

## 使用 API 或工具添加内容

准备好向集合添加文档时，请考虑以下内容：

-   可以上传到 {{site.data.keyword.discoveryshort}} 服务的最大文件大小为 50 MB。
-   样本文档不会自动添加到集合中。如果需要将样本文档作为集合的一部分，您必须添加这些文档。
-   将仅扩充选择用于扩充的每个 JSON 字段的前 50,000 个字符。
-   创建集合时，可选择文档语言（缺省值为英语）。请参阅[语言支持](/docs/services/discovery/language-support.html)以获取语言列表。您的文档将以所选语言进行扩充。不要在同一集合中混用语言。
-   可以向集合添加 Microsoft Word、PDF、HTML 和 JSON 文档。**注：**无法转换和扩充属于已扫描图像文件的 PDF。
-   除非选择其他配置文件，否则将使用提供的配置文件（名为 Default Configuration）来转换集合中的文档。有关创建配置文件的信息，请参阅[定制配置](/docs/services/discovery/building.html#custom-configuration)。
-   将文档上传到数据集合后，将使用为该集合选择的配置文件对这些文档进行转换和扩充。如果您日后决定要将集合切换到其他配置文件，您可以执行此操作，但已上传的文档仍然通过原始配置文件进行转换。切换配置文件后上传的所有文档都将使用新的配置文件。如果您希望**整个**集合使用新配置，那么需要创建新的集合，选择该新的配置文件，然后重新上传所有文档。
-   不能指定字段的`数据类型`（例如：`text` 或 `date`）。在文档摄入期间，如果检测到索引中尚不存在某个字段，那么 {{site.data.keyword.discoveryshort}} 将根据已建立索引的第一个文档的相应字段值自动检测该字段的`数据类型`。
-   可能由于当前文档中的数据与先前摄入文档中的类似数据之间的类型不匹配，导致文档摄入失败。例如，某个字段可能在一个文档中的类型为 `date`，而在后续文档中的类型为 `string`，这会使该后续文档无法正确建立索引。
-   如果计划使用定制记号化（目前在使用 {{site.data.keyword.discoveryshort}} API 时仅可用于日语集合），那么必须在上传文档之前添加集合的记号化字典。

上传文档时存在以下限制：

-   **轻量**套餐：21 个未完成的文档
-   **高级**套餐：105 个未完成的文档（超小高级套餐除外，此类套餐限制为 50 个未完成的文档）
-   **高端**套餐：210 个未完成的文档

这些限制可能会更改。 

使用 Discovery 服务时，未完成的上传表示正在上传并处理文档，完成后会将文档添加到集合。如果达到未完成文档数的限制，那么应该降低摄入的速度。一个选项是为重试添加自动退避机制。

## 使用 Discovery 工具上传文档

1.  创建集合。请参阅[准备服务以用于处理文档](/docs/services/discovery/building.html#preparing-the-service-for-your-documents)。
1.  单击该集合以将其打开。
1.  单击**上传文档**按钮，然后通过拖放或浏览操作开始上传文档。

现在文档已排队等待转换和扩充。所花时间取决于集合的大小。对集合建立索引并扩充后，该集合的详细信息将显示在**概述**部分中。

-   **创建日期**和**上次更新日期**（单击**在 API 中使用此集合**可查看 `collection_id`、`configuration_id` 和 `environment_id`。）
-   集合中的**文档数**
-   **配置** - 用于转换此集合的配置文件的名称
-   **错误和警告**

有关如何使用 {{site.data.keyword.discoveryshort}} 工具连接到 Box、Salesforce 和 Microsoft SharePoint Online 数据源的信息，请参阅[连接到数据源](/docs/services/discovery/connect.html)。


## 使用 API 上传文档

请参阅 [{{site.data.keyword.discoveryshort}} API 入门](/docs/services/discovery/getting-started.html)以获取逐步教程。

有关该 API 的更多信息，请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}。

1.  使用 `POST /v1/environments/{environment_id}/collections` 方法来创建集合。
1.  然后，使用 `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` 方法向集合添加文档。

## 搜寻 URL

可以使用 {{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} {{site.data.keyword.discoveryshort}} Service [Indexing plugin for Apache Nutch ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/IBM-Watson/nutch-indexer-discovery) 来搜寻 URL 并对其建立索引。搜寻不会自动更新，因此需要定期重复执行此过程，以使索引保持最新状态。
