---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-16"

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

# 查询入门

在本教程中，我们将学习如何在 {{site.data.keyword.discoveryshort}} 中编写几种不同类型的查询。
{: shortdesc}

有关编写查询的更多信息，请参阅：
- [查询概念](/docs/services/discovery/using.html)
- [查询参考](/docs/services/discovery/query-reference.html)（包括 {{site.data.keyword.discoveryshort}} Query Language 中可用的参数、运算符和聚集的列表）

这些示例查询是使用 {{site.data.keyword.discoveryshort}} 工具构建的。如果要改为使用 API，请将查询参数添加到 API 调用。有关更多信息和示例，请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection){: new_window} 中的“查询”部分。

您还可以使用 {{site.data.keyword.discoveryshort}} 工具来编写自然语言查询（例如“IBM Watson 伙伴关系”）。本教程主要讨论如何使用 {{site.data.keyword.discoveryshort}} Query Language 编写查询，因为您的需求可能要求使用结构化查询，而且过滤器和聚集必须用 {{site.data.keyword.discoveryshort}} Query Language 进行编写。
{: tip}

## 开始之前

**完成[入门](/docs/services/discovery/getting-started-tool.html)中的步骤。**如果尚未完成**入门**，请转至**管理数据**屏幕，创建名为 {{site.data.keyword.IBM_notm}} Press Releases 的新集合，并将以下四个文档添加到该集合（使用 **Default Configuration**）：<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>testoc1.html <img src="../../icons/launch-glyph.svg" alt=" 外部链接图标" title="外部链接图标" class="style-scope doc-content"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>testoc2.html <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标" class="style-scope doc-content"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>testdoc3.html <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标" class="style-scope doc-content"></a> 和 <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标" class="style-scope doc-content"></a>

## 步骤 1：Discovery 数据模式快速导览

首先来了解 {{site.data.keyword.discoveryshort}} JSON。要了解如何使用 {{site.data.keyword.discoveryshort}} Query Language 来构建查询，熟悉 {{site.data.keyword.discoveryshort}} 在扩充集合中的文档后生成的 JSON 会很有帮助。

1.  [启动 {{site.data.keyword.discoveryshort}} 工具](/docs/services/discovery/getting-started-tool.html#launch-the-tooling)。在**管理数据**屏幕上，选择 {{site.data.keyword.IBM_notm}} Press Releases 集合。

1.  查看 Watson 在扩充的文档中发现的见解。

    -  **总体观点**显示“观点分析”扩充项发现的标记为 positive、neutral 和 negative 的文档分别所占百分比。
    -  **排名靠前的实体**显示“实体抽取”扩充项在文档中发现的人员、场所和组织。
    -  **内容层次结构**显示“类别分类”扩充项在文档中发现的分层分类法。
    -  **相关概念**显示“概念标记”扩充项在文档中发现的概念。

         单击任意卡上的**在模式中查看**以查看构成这些结果的扩充项。
         {: tip}

1.  为了熟悉文档的数据模式，我们来浏览**查看数据模式**屏幕。此屏幕通过两种方式显示已变换文档中的字段和值：按文档（**文档视图**）或按字段（**集合视图**）。**集合视图**将显示集合中的所有字段。

    单击**查看数据模式**按钮。在**集合视图**中的 `enriched_text` 下，可以检查通过 **Default Configuration** 文件应用的扩充项。单击 `categories`、`concepts`、`entities` 和 `sentiment` 可查看集合是如何通过 Watson 见解扩充的。

如果查询未返回任何匹配的结果，而您认为应该返回匹配结果，请尝试将查询使用的字段/值改换为可以在数据模式中验证的字段/值。
{: tip}    

## 步骤 2：构建基本查询

首先编写一个查询，用于在集合中查找 `Cloud computing` 概念：

1.  单击“构建查询”图标 ![“查询”图标](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> 以打开查询页面。选择包含 {{site.data.keyword.IBM_notm}} Press Releases 的集合，然后单击**开始使用**。
1.  在**构建查询**屏幕上，单击**搜索文档**，单击**使用 {{site.data.keyword.discoveryshort}} Query Language**，然后执行以下操作：
    - 单击**字段**下拉列表并选择 `enriched_text.concepts.text`，对于**运算符**，选择 `contains`，然后输入**值** `Cloud computing`。查询 `enriched_text.concepts.text:Cloud computing` 将显示在 **Visual Query Builder** 下。

    - 或者，可以单击**使用查询语言编辑**，然后单击**使用 {{site.data.keyword.discoveryshort}} Query Language**。在**在此输入查询**字段中，输入 `enriched_text.concepts.text:Cloud computing`。

1.  单击**运行查询**。应该会有一个匹配项 (`"matching_results": 1`)。复制**摘要**或 **JSON** 选项卡项部的**查询 URL**，以便在应用程序中使用。

**额外功能：**在**更多选项**下，可以选择使用**包含相关段落**单选按钮来开启段落检索。段落是查询返回的完整文档中的简短相关摘录。这些目标段落是从集合中文档的 `text` 字段中抽取的。请参阅[段落](/docs/services/discovery/query-parameters.html#passages)以获取更多信息。段落检索不可用于 {{site.data.keyword.discoveryshort}} News 集合。

如果要检出一些预构建的查询，请单击**使用样本查询**按钮。
{: tip}

## 步骤 3：试用不同的查询

尝试以下查询：

要返回具有 `positive` 观点的所有文档：单击**搜索文档**，单击**使用 {{site.data.keyword.discoveryshort}} Query Language**，然后执行以下操作：
-  单击**字段**下拉列表并选择 `enriched_text.sentiment.document.label`，对于**运算符**，选择 `contains`，然后输入**值** `positive`。  

   查询 `enriched_text.sentiment.document.label:positive` 将显示在 **Visual Query Builder** 下。

要返回 `health and fitness` 类别的所有文档：单击**搜索文档**，单击**使用 {{site.data.keyword.discoveryshort}} Query Language**，然后执行以下操作：
-  单击**字段**下拉列表并选择 `enriched_text.categories.label`，对于**运算符**，选择 `is`，然后输入**值** `"health and fitness"`。

   查询 `enriched_text.categories.label::"health and fitness"` 将显示在 **Visual Query Builder** 下。运算符 `::` 表示完全匹配。

要返回包含实体 `IBM` 而不包含实体 `Watson` 的所有文档：单击**搜索文档**，单击**使用 {{site.data.keyword.discoveryshort}} Query Language**，然后执行以下操作：
-  单击**字段**下拉列表并选择 `enriched_text.entities.text`，对于**运算符**，选择 `contains`，然后输入**值** `IBM`。单击**添加规则**，接着对于**字段**，选择 `enriched_text.entities.text`，对于**运算符**，选择 `does not contain`，然后输入**值** `Watson`。

   查询 `enriched_text.entities.text:IBM,enriched_text.entities.text:!Watson` 将显示在 **Visual Query Builder** 下。运算符 `:!` 表示“不包含”。

## 步骤 4：构建组合查询

可以将查询参数组合在一起，以构建更有针对性的查询。下面我们尝试使用 `filter` 和 `query` 参数来返回有关 {{site.data.keyword.IBM_notm}} acquisitions 的文档。filter 参数可将结果范围缩小为仅那些提及 `IBM` 的文档，然后 query 参数将按相关性顺序返回有关 `acquisitions` 的所有结果。

1.  单击“构建查询”图标 ![“查询”图标](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> 以打开查询页面。选择包含 {{site.data.keyword.IBM_notm}} Press Releases 的集合，然后单击**开始使用**。

1.  在**过滤查询的文档**下：
    -  单击**字段**下拉列表并选择 `enriched_text.entities.text`，对于**运算符**，选择 `contains`，然后输入**值** `IBM`。

       查询 `enriched_text.entities.text:IBM` 将文档范围缩小为仅那些提及实体 `IBM` 的文档。

1.  在**搜索文档**下，单击**使用 {{site.data.keyword.discoveryshort}} Query Language**，然后执行以下操作：
    -  单击**字段**下拉列表并选择 `enriched_text.concepts.text`，对于**运算符**，选择 `contains`，然后输入**值** `world wide web`。

       查询 `enriched_text.concepts.text:world wide web` 将返回包含 `world wide web` 概念的所有文档，并且这些文档将按相关性顺序排名。

1.  单击**更多选项**，单击**要返回的字段**，然后选择**指定**。选择 `text`。这会将响应限制为相关文章的文本，而排除所有其他内容。

1.  单击**运行查询**。将有一个匹配的文档：`"matching_results": 1`

## 步骤 5：构建聚集

聚集会返回一组数据值；例如，排名靠前的关键字、实体的总体观点等。

尝试构建这样一个聚集 - 将返回 {{site.data.keyword.IBM_notm}} Press Releases 集合中的前 10 个概念。

1.  单击“构建查询”图标 ![“查询”图标](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> 以打开查询页面。选择包含 {{site.data.keyword.IBM_notm}} Press Releases 的集合，然后单击**开始使用**。

1.  在**包含对结果的分析**下：
    -  单击**输出**下拉列表并选择`排名靠前的值`，对于**字段**，选择 `enriched_text.concepts.text`，然后为**计数**输入 `10`。

       `Term` 将返回 `concepts` `text` 字段的最常见值。**计数**指定要返回的结果数。查询 `term(enriched_text.concepts.text,count:10)` 将显示在 **Visual Query Builder** 下。   

1.  单击**更多选项**，然后在**要返回的文档数**字段中输入 `0`。

1.  单击**运行查询**。这将同时在**摘要**和 **JSON** 选项卡中显示前 10 个概念。下面是“摘要”的示例：

## 步骤 6：在 Watson Discovery News 中构建查询

{{site.data.keyword.discoverynewsshort}} 是已使用认知见解进行预扩充的公共数据集。它随附于 {{site.data.keyword.discoveryshort}}。请参阅 [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html#watson-discovery-news) 以获取有关此集合的更多信息。

不能调整 {{site.data.keyword.discoverynewsshort}} 配置，也不能培训 {{site.data.keyword.discoverynewsshort}} 集合或向其中添加文档。请在[此处 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://discovery-news-demo.mybluemix.net/){: new_window} 查看可以使用 {{site.data.keyword.discoverynewsshort}} 构建的内容的演示。

以下示例查询返回 {{site.data.keyword.discoverynewsfull}} 中有关 Pittsburgh Steelers 的具有正面观点的前 10 篇文章。

1.  单击“构建查询”图标 ![“查询”图标](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> 以打开查询页面。选择 {{site.data.keyword.discoverynewsshort}} 集合，然后单击**开始使用**。

1.  在**搜索文档**下，单击**使用 {{site.data.keyword.discoveryshort}} Query Language**，然后执行以下操作：
    -  单击**字段**下拉列表并选择 `text`，对于**运算符**，选择 `contains`，然后输入**值** `Pittsburgh Steelers`。单击**添加规则**，然后单击**字段**下拉列表并选择 `enriched_text.sentiment.document.label`，对于**运算符**，选择 `contains`，然后输入**值** `positive`。

       查询 `text:Pittsburgh Steelers, enriched_text.sentiment.document.label:positive` 将显示在 **Visual Query Builder** 下。

1.  单击**更多选项**，然后在**要返回的文档数**中输入 `0`（这是缺省值）。

1.  单击**运行查询**。这将显示有关 Pittsburgh Steelers 的具有正面观点的前 10 篇文章。

**注：**针对 Watson Discovery News 查询返回的最大结果数为 `50`。

新闻文章可能会联合到多家新闻媒体，{{site.data.keyword.discoverynewsfull}} 会选取其中每家新闻媒体，因而会生成重复的文章。这意味着对 {{site.data.keyword.discoverynewsfull}} 的查询可能会在查询结果中返回多个完全相同或几乎完全相同的文章。要启用去重，请在**更多选项**下选择**排除重复结果**。要了解有关此 Beta 功能的更多信息，请参阅[从查询结果中排除重复文档](/docs/services/discovery/query-parameters.html#deduplication)。
