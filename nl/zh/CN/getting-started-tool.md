---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-08"

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

# 入门
{: #getting-started}

在此简短教程中，我们将介绍 {{site.data.keyword.discoveryshort}} 工具，然后完成创建专用数据集合并对其进行搜索的过程。
{: shortdesc}

如果您倾向于使用 API，请参阅 [API 入门](/docs/services/discovery?topic=discovery-gs-api#gs-api)。
{: tip}

## 开始之前
{: #before-you-begin-tool}
{: hide-dashboard}

您首先需要一个服务实例。
{: hide-dashboard}

1.  {: hide-dashboard}转至 {{site.data.keyword.cloud_notm}} 目录中的 [{{site.data.keyword.discoveryshort}} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/catalog/services/discovery) 页面。

    服务实例会在 **default** 资源组中创建（如果您未选择其他组），且稍后*无法*更改。此组对于试用服务而言已足够。

    如果您要创建实例来使用更健全的功能，那么请了解有关[资源组 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/docs/resources/bestpractice_rgs.html#bp_resourcegroups){: new_window} 的更多信息。
1.  {: hide-dashboard}注册免费的 {{site.data.keyword.cloud_notm}} 帐户或登录。
1.  {: hide-dashboard}单击**创建**。

## 步骤 1：启动工具
{: #launch-the-tooling}

创建 {{site.data.keyword.discoveryshort}} 服务的实例后，您将进入到服务列表。
{: hide-dashboard}

1.  {: hide-dashboard}单击您创建的 {{site.data.keyword.discoveryshort}} 服务实例以转至服务仪表板。
1.  在**管理**页面上，单击**启动工具**。如果系统提示您登录到工具，请提供您的 {{site.data.keyword.cloud_notm}} 凭证。

<!-- To do: Add screenshot for developer console -->

## 步骤 2：创建集合
{: #create-a-collection-tool}

在 {{site.data.keyword.discoveryshort}} 工具中执行的第一步是创建数据集合。

集合是一组文档。*为什么需要多个集合？*原因有多种：

- 您可能需要多个集合来针对不同的受众隔离结果。
- 数据可能差异太大，因而同时对所有数据进行查询没有任何意义。

此外，还有预扩充的公共 {{site.data.keyword.discoverynewsshort}} 数据集合供您使用。这是可随时查询的集合，您可以立即开始创建对该集合的查询。不能调整此集合的配置，也不能向 {{site.data.keyword.discoverynewsshort}} 添加文档。

1.  单击 ![环境详细信息](images/env_icon.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->，然后选择**创建环境**。
1.  环境就绪后，请单击**上传您自己的数据**按钮，然后可以**命名新集合**。将集合命名为 **InstallDocs**。

    创建集合时，在**高级**下面，您可以选择名为 **Default Contract Configuration** 的配置文件。此配置仅支持“元素分类”扩充项，后者可用于从 PDF 内的元素中抽取当事方、性质和类别。请参阅[元素分类](/docs/services/discovery?topic=discovery-element-classification#element-collection)以获取详细信息。不要对本教程选择此选项。

您还可以搜寻 Box、Salesforce、Microsoft SharePoint Online、IBM Cloud Object Storage 和 Microsoft SharePoint 2016 数据源，或使用 {{site.data.keyword.discoveryshort}} 工具执行 Web 搜寻。单击**连接数据源**按钮，然后请参阅[连接到数据源](/docs/services/discovery?topic=discovery-sources#sources)以获取更多信息。
{: tip}

## 步骤 3：下载样本文档并上传到您的集合
{: create-custom-configuration}

1.  下载此样本 PDF 文档：<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/watsonexplorerinstall.pdf" download>Watson Explorer Installation Guide <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标"></a>。请参阅[支持的文档类型](/docs/services/discovery?topic=discovery-sdu#doctypes)，以获取 {{site.data.keyword.discoveryshort}} 中支持的完整文档类型列表。 

    在某些浏览器中，链接将在新窗口中打开，而不是在本地保存。如果发生这种情况，请选择浏览器的`文件`菜单中的`另存为`，以保存该文件的副本。
    {: tip}

1.  将文档上传到您的集合。您可以将其拖放到您的集合，或者也可以单击**从计算机浏览**来上传文档。上传完成后，将显示以下信息：
    -  文档数 (1)。
    -  从文档中识别的字段。您应看到识别了一个字段，即 `text`。我们很快将识别更多字段。
    -  对文档应用的扩充项。{{site.data.keyword.discoveryshort}} 会将“实体抽取”、“观点分析”、“类别分类”和“概念标记”扩充项自动应用到 `text` 字段。从[此处](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)了解有关扩充项的更多信息。 
    -  您可以立即运行的预构建查询。
1.  让我们试试对级别设置的快速自然语言查询。单击右下角的**构建您自己的查询**。
1.  在**构建查询**屏幕上，单击**搜索文档**，然后单击**使用自然语言**。输入 `What are the minimum hardware requirements`，然后单击**运行查询**按钮。单击右侧的 **JSON** 选择卡。结果并不会特别精确，那么使用“智能文档理解”来改进一下吧。
1.  单击左上角的集合名称 (**InstallDocs**) 以返回到**概述**屏幕。  
 
## 步骤 4：注释文档
{: #upload-your-documents}

有关注释文档的更多信息，请参阅[智能文档理解](/docs/services/discovery?topic=discovery-sdu#sdu)。
{: tip}

1.  单击右上角的**配置数据**。 
1.  在**配置数据**屏幕上，将有三个选项卡：**识别字段**、**管理字段**和**扩充字段**。
1.  此时将显示 `Watson Explorer Installation Guide`，并已准备好在**识别字段**选项卡上进行注释。右侧的**字段标签**列表中会显示所有可用字段（`answer`、`author`、`footer`、`header`、`question`、`subtitle`、`table_of_contents`、`text` 和 `title`）。如果购买高级套餐或高端套餐，您可以创建自己的定制标签。

    由于整个文档当前识别为 `text`，因此右侧标记整体以黄色显示。随着您进行注释（且系统开始预测），颜色会更新。
    {: tip}

1.  单击 `title`，然后选择 `Installation and Integration Guide` 旁边的标记。单击**提交页面**按钮。
1.  在左侧的页面预览中，单击第 3 页。请注意，已预测此页面的 `title`。单击**提交页面**按钮。
1.  在第 4 页，选择 `footer` 标签，并选择页脚旁边的标记。单击**提交页面**按钮。
1.  在第 5 页和第 6 页，使用 `footer` 标签注释页脚。提交每个页面。单击更多页面；您将发现 {{site.data.keyword.discoveryshort}} 已正确预测页脚。注释第 7、9 和 10 页上的 `title`（左对齐）和 `subtitle`（缩进），然后分别提交每个页面。
1.  单击更多页面，并检查预测的标题和子标题。如有任何内容需要更改，请注释这些页面，并单击**提交页面**按钮。
1.  现在，单击**管理字段**选项卡，并在**拆分文档以改进查询结果**下根据 `subtitle` 拆分文档。 
1.  目前这些注释应该足够了。单击右上角的**将更改应用于集合**。此时将显示**上传文档**对话框。浏览至原始 `watsonexplorerinstall.pdf` 文件，并将其上传。这会将所有注释应用到索引中。建立索引完成后，将打开**概述**屏幕。您现在应该会看到 30 多个文档，并且从您的数据中识别了 4 个字段：`footer`、`subtitle`、`text` 和 `title`。（如果更改在几分钟内未显示，请刷新浏览器窗口。）

    您可以排除字段（如 `footer`）而不对其建立索引，方法是打开**管理字段**选项卡，并将该字段切换为 `off`。
    {: tip}

## 步骤 5：进行查询
{: #build-a-query}

1.  单击右下角的**构建您自己的查询**。
1.  在**构建查询**屏幕上，单击**搜索文档**，然后单击**使用自然语言**。输入 `What are the minimum hardware requirements`，然后单击**运行查询**按钮。 
1.  单击右侧的 **JSON** 选择卡。查看 `results` 下的 `text`。针对该查询返回的答案会精确得多。

其他资源：
-  要了解有关文档数据模式的更多信息，请单击最左侧的**查看数据模式**图标或单击 **JSON** 选项卡。请参阅 [Discovery 数据模式](/docs/services/discovery?topic=discovery-query-concepts#discovery-schema)以获取详细信息。
-  单击**使用样本查询**按钮来试用以 {{site.data.keyword.discoveryshort}} 查询语言编写的示例查询。

## 后续步骤
{: #next-steps-tool}

您现在有一个正常运行且已填充的 {{site.data.keyword.discoveryshort}} 服务实例。现在，可以开始通过添加更多文档和扩充项以及注释其他文档来定制集合。请参阅[智能文档理解](/docs/services/discovery?topic=discovery-sdu#sdu)以获取更多信息。
