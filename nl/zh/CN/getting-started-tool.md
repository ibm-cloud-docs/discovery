---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-18"

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
{:download: .download}

# 入门

在此简短教程中，我们将介绍 {{site.data.keyword.discoveryshort}} 工具，然后完成创建专用数据集合并对其进行搜索的过程。
{: shortdesc}

如果您倾向于使用 API，请参阅 [API 入门](/docs/services/discovery/getting-started.html)。
{: tip}

## 开始之前
{: #before-you-begin}

您首先需要一个服务实例。

<!-- Remove the text marked `download` after there's no g-s tab in the catalog dashboard -->


您已创建服务实例。单击**管理**，然后单击**打开工具**。请转至[步骤 2](/docs/services/discovery/getting-started-tooling.html#create-a-collection)。
{: download tip}

如果已创建 {{site.data.keyword.discoveryshort}} 服务实例，说明这些先决条件已全部准备就绪。请转至[步骤 1](/docs/services/discovery/getting-started-tool.html#launch-the-tooling)。

1.  转至 {{site.data.keyword.Bluemix_notm}}“目录”中的 [{{site.data.keyword.discoveryshort}} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.{DomainName}/catalog/services/discovery){: new_window} 页面。
1.  注册免费的 {{site.data.keyword.Bluemix_notm}} 帐户或登录。
1.  单击**创建**。


## 步骤 1：启动工具
{: #launch-the-tooling}

创建 {{site.data.keyword.discoveryshort}} 服务的实例后，您将登录到 [{{site.data.keyword.Bluemix_notm}} 仪表板](https://console.{DomainName}/dashboard)。单击 {{site.data.keyword.discoveryshort}} 服务实例以转至 {{site.data.keyword.discoveryshort}} 服务仪表板。

在**管理**页面上，单击**打开工具**。

<!-- To do: Add screenshot for developer console -->

如果系统提示您登录到工具，请提供您的 {{site.data.keyword.Bluemix_notm}} 凭证。

如果您不在 {{site.data.keyword.discoveryshort}} 服务的项目详细信息页面上，请转至 {{site.data.keyword.watson}} 开发者控制台[项目 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.{DomainName}/developer/watson/projects) 页面，然后选择相应项目。
{: tip}

<!-- Remove this text after dedicated instances have the Developer Console: begin -->

{{site.data.keyword.Bluemix_dedicated_notm}}：在“仪表板”中选择服务实例以启动工具。

<!-- Remove this text after dedicated instances have the Developer Console: end -->

## 步骤 2：创建集合
{: #create-a-collection}

在 {{site.data.keyword.discoveryshort}} 工具中执行的第一步是创建数据集合。

集合是一组文档。*为什么需要多个集合？*原因有多种：

- 您可能需要多个集合来针对不同的受众隔离结果。
- 数据可能差异太大，因而同时对所有数据进行查询没有任何意义。

此外，还有预扩充的公共 {{site.data.keyword.discoverynewsshort}} 数据集合供您使用。这是可随时查询的集合，您可以立即开始创建对该集合的查询。不能调整此集合的配置，也不能向 {{site.data.keyword.discoverynewsshort}} 添加文档。

1.  单击 ![齿轮](images/icon_settings.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->，然后选择**创建环境**。
1.  环境就绪后，请单击**上传您自己的数据**按钮，然后可以**命名新集合**。命名集合并从**选择要应用的配置**中选择**缺省配置**（日后可以更改此配置）。

另外还提供了一个名为 **Default Contract Configuration** 的配置，此配置支持“元素分类”，后者可用于从 PDF 内的元素中抽取参与方、性质和类别。请参阅[元素分类](/docs/services/discovery/element-classification.html#element-collection)以获取详细信息。

您还可以使用 {{site.data.keyword.discoveryshort}} 工具来搜寻 Box、Salesforce 和 Microsoft SharePoint Online 数据源。单击**连接数据源**按钮，然后请参阅[连接到数据源](/docs/services/discovery/connect.html)以获取更多信息。
{: tip}

## 步骤 3：创建定制配置
{: create-custom-configuration}

创建集合后，可以立即使用上传区域开始上传内容，但我们希望创建和测试定制配置。

1.  单击集合名称旁边的**切换**，然后选择**新建配置**。命名配置，然后单击**创建**。
1.  创建配置后，可以对其进行定制：
    1.  下载 <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>testdoc1.html <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标" class="style-scope doc-content"></a> 样本文档。
    1.  使用**上传样本文档**面板来上传样本文档。上传后，可以单击文档名称链接来查看变换。
1.  现在来调整配置。对于此任务，您将更改应用于每个文档的扩充项：
    1.  单击配置的**扩充**部分。在屏幕右侧查看生成的 JSON。向下滚动到 *enriched_text* 部分，请注意，此部分包含多个 *concepts*。
    1.  接下来，通过单击名为 *concepts* 的文本扩充项旁边的 **X** 来除去该扩充项，然后单击**应用并保存**。
    1.  最后，再次查看 JSON。请注意，输出已经发生变化，不再包含 *concepts*。

## 步骤 4：上传文档
{: #upload-your-documents}

对样本文档的定制转换感到满意后，现在要将实际内容摄入到集合中。

1. 下载以下三个样本文档：<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>testoc2.html <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标" class="style-scope doc-content"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>testdoc3.html <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标" class="style-scope doc-content"></a> 和 <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标" class="style-scope doc-content"></a>。
1.  单击 ![“文件”图标](images/icon_yourData.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> 并选择您的集合。
1.  确保您创建的定制配置列在**配置**下。如果未列出，请单击配置名称旁边的**切换**，然后选择所需配置。
1.  单击**上传文档**按钮，然后开始上传四个样本文档：test-doc1.html、test-doc2.html、test-doc3.html 和 test-doc4.html。
1.  等待文档上传。文档的状态将显示在**概述**部分中。

## 步骤 5：构建查询
{: #build-a-query}

1.  单击 ![“查询”图标](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> 以打开查询页面。选择您的集合，然后单击**开始使用**。
1.  在**构建查询**屏幕上，单击**搜索文档**，然后单击**使用 {{site.data.keyword.discoveryshort}} Query Language**：
    - 要使用实体名“IBM”搜索结果：
        1.  单击**字段**，然后选择 `enriched_text.entities.text`。对于**运算符**，选择 `contains`，对于**值**，选择 `IBM`。查询 `enriched_text.entities.text:IBM` 将显示在 **Visual Query Builder** 中。
        1.  单击**运行查询**。此查询会返回 4 个结果。
    - 要使用实体名“Watson”搜索结果：
        1.  单击**字段**，然后选择 `enriched_text.entities.text`。对于**运算符**，选择 `contains`，对于**值**，选择 `watson`。查询 `enriched_text.entities.text:watson` 将显示在 **Visual Query Builder** 中。
        1.  单击**运行查询**。此查询会返回 2 个结果。
    - 要同时使用实体名“Watson”和“Slack”搜索结果：
        1.  单击**字段**，然后选择 `enriched_text.entities.text`。对于**运算符**，选择 `contains`，对于**值**，选择 `watson`。单击**添加规则**，然后重复您的选择，但对于**值**，选择 `Slack`。查询 `enriched_text.entities.text:watson,enriched_text.entities.text:Slack` 将显示在 **Visual Query Builder** 中。
        1.  单击**运行查询**。此查询会返回 1 个结果。

    单击**使用查询语言编辑**，以使用 {{site.data.keyword.discoveryshort}} Query Language 来构建查询。要了解有关 {{site.data.keyword.discoveryshort}} Query Language 的更多信息，请参阅[查询参考](/docs/services/discovery/query-reference.html)和[查询概念](/docs/services/discovery/using.html)。
1.  查询结果会显示在**结果**部分中：
    - **摘要**选项卡提供查询结果的概述。
    - **JSON** 选项卡显示完整的 JSON 结果。

    对于所列出的查询，**摘要**首先显示文档段落（按相关性顺序），后跟找到的文档的名称，然后按扩充项显示结果。**段落**是从查询返回的完整文档中抽取的简短相关摘录。

    在 **JSON** 和**摘要**选项卡下提供的**查询 URL** 链接在应用程序中随时可用。

    您还可以单击**使用自然语言**并编写自然语言查询，例如“IBM Watson 伙伴关系”。要了解有关自然语言查询的更多信息，请参阅[自然语言查询](/docs/services/discovery/query-parameters.html#nlq)。

    可以对 Watson 进行训练以改进自然语言查询的结果，请参阅[使用工具改进结果相关性](/docs/services/discovery/train-tooling.html)。

    其他资源：
    - 要了解有关文档数据模式的更多信息，请单击**查看数据模式**图标或单击 **JSON** 选项卡。请参阅 [Discovery 数据模式](/docs/services/discovery/using.html#discovery-schema)以获取详细信息。
    - 如果是在 {{site.data.keyword.discoveryshort}} Query Language 中进行编辑，请单击任意**在此输入查询**字段旁边的 **?** 以获取更多示例。

## 后续步骤
{: #next-steps}

您现在有一个正常运行且已填充的 {{site.data.keyword.discoveryshort}} 服务实例。现在，可以开始通过添加更多文档和扩充项以及定制转换设置来定制集合。
