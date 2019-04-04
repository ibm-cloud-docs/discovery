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
{:gif: data-image-type='gif'}

# 智能文档理解
{: #sdu}

“智能文档理解”(SDU) 是用于训练 {{site.data.keyword.discoveryfull}} 以抽取文档中的定制字段的新方法。定制在 {{site.data.keyword.discoveryshort}} 中对文档建立索引的方式将改进应用程序返回的答案。

使用 SDU，您将注释文档内的字段，以训练定制转换模型。在您注释时，Watson 即会进行学习并开始预测注释。SDU 模型可导出并用于其他集合。 

## 支持的文档类型和浏览器
{: #doctypes}

智能文档理解支持的文档类型： 
-  轻量套餐：PDF、Word、PowerPoint、Excel、JSON\* 和 HTML\* 
-  高级套餐：PDF、Word、PowerPoint、Excel、PNG\*\*、TIFF\*\*、JPG\*\*、JSON\* 和 HTML\*  

\* {{site.data.keyword.discoveryfull}} 支持 JSON 和 HTML 文档，但无法使用 SDU 编辑器编辑这些文档。要更改 HTML 和 JSON 文档的配置，您需要使用 API。有关更多信息，请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/discovery/){: new_window}。

\*\* 将扫描各个图像文件（PNG、TIFF 和 JPG），并抽取文本（如果有）。此外，还将扫描 PDF、Word、PowerPoint 和 Excel 文件中嵌入的 PNG、TIFF 和 JPEG 图像，并抽取文本（如果有）。

支持的浏览器：Chrome 和 Firefox。

## 使用智能文档理解编辑器
{: #annotate}

SDU 编辑器仅可用于包含受支持文档类型且未应用“元素分类”扩充项的新集合。现有专用集合将使用原始配置方法。如果要对现有集合使用 SDU 编辑器，您将需要创建新的集合并将这些文档上传到其中。如果不想使用 SDU 编辑器，您可以使用 API 设置您的配置，请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/discovery/){: new_window}。
{: important}

SDU 编辑器功能仅可用于 {{site.data.keyword.discoveryshort}} 工具，在 API 中不可用。
{: note}

在“智能文档理解”编辑器中导航：

如果尚未创建 {{site.data.keyword.discoveryshort}} 实例和环境，请参阅[入门](/docs/services/discovery?topic=discovery-getting-started#getting-started)以获取指示信息。
{: tip}

1. 在**管理数据**屏幕上，单击**上传您自己的数据**按钮，并在 {{site.data.keyword.discoveryshort}} 中创建新的专用集合。
1. 如有需要，您可以将文档拖放到您的集合，或者也可以单击**从计算机浏览**来上传文档。上传完成后，将显示以下信息：
   -  从文档中识别的字段。
   -  对文档应用的扩充项。{{site.data.keyword.discoveryshort}} 会将“实体抽取”、“观点分析”、“类别分类”和“概念标记”扩充项自动应用到 `text` 字段（除非您使用连接器导入文档）。您可以将其他扩充项添加到 `text` 字段，或将其除去。
   -  您可以立即运行的预构建查询。
1. 单击右上角的**配置数据**。 
1. 在**配置数据**屏幕上，将有三个选项卡：**识别字段**、**管理字段**和**扩充字段**。

   - **识别字段**包含 SDU 编辑器。此选项卡将替换原始 {{site.data.keyword.discoveryshort}} 屏幕上的**转换**和**规范化**选项卡。 
   - **管理字段**列出所有建立索引的字段（缺省情况下，所有字段都将建立索引）。请关闭不想建立索引的任何字段。例如，您的 PDF 中正在使用的页眉或页脚可能并不包含有用信息，所以您可以将这些字段从索引中排除。此外，您还可以在此处根据字段拆分文档，请参阅[拆分文档](/docs/services/discovery?topic=discovery-sdu#splitting)。
   - **扩充字段**与原始屏幕上的**扩充**选项卡完全相同。有关扩充项的更多信息，请参阅[添加扩充项](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)。**上传样本文档**选项不可用于 SDU 集合。

   如果先前未上传任何文档，可单击左上角的集合名称以返回到**概述**屏幕，或单击 ![管理数据](/images/icon_yourData.png) 图标并选择集合。将文档拖放到您的集合，或单击**从计算机浏览**。完成初始上传后，**上传文档**按钮将在右上角显示。
   {: important}

   使用“智能文档理解”时，仅可扩充 `text` 字段。不要尝试扩充任何其他字段。
   {: important}

1. 打开**识别字段**选项卡。集合中的最多二十 (20) 个文档将自动装入到“智能文档理解”编辑器中。

通过顶部的工具栏，您可以执行以下操作：
- 选择要注释的文档
- 浏览显示的文档
- 调整页面视图（`单页面视图`、`放大`和`缩小`）、`清除更改`以及`导出/导入模型`。单击`单页面视图`可切换显示 - 您可以单独或一起查看您的注释和文档。

您还可以搜寻 Box、Salesforce、Microsoft SharePoint Online、IBM Cloud Object Storage 和 Microsoft SharePoint 2016 数据源，或使用 {{site.data.keyword.discoveryshort}} 工具执行 Web 搜寻。单击**连接数据源**按钮，然后请参阅[连接到数据源](/docs/services/discovery?topic=discovery-sources#sources)以获取更多信息。
如果使用此方法创建集合，将不会自动应用任何扩充项。
{: tip}

## 如何注释文档
{: #documents}

**注：**将在单独的步骤中对表进行注释。

开始注释之前，请参阅[注释文档和表的最佳实践](/docs/services/discovery?topic=discovery-sdu#bestpractices)。

1. 缺省字段集将显示在文档右侧。可用字段为 `answer`、`author`、`footer`、`header`、`question`、`subtitle`、`table_of_contents`、`text` 和 `title`。如果要创建一个或多个新的定制字段标签，请单击**新建**。您可以使用的定制标签数有如下限制：轻量套餐 - `0`，高级套餐 - `5`，高端套餐 - `20`。
1. 单击右侧的字段标签以将其激活。
1. 单击 SDU 编辑器中表示该字段的内容。该内容将突出显示。 
   - 或者，可以选择右侧的字段标签，然后将其拖动到 SDU 编辑器中的内容中。 
   - 要清除更改，请单击工具栏上的**清除更改**按钮。
1. 单击**提交**。
   **注：**在您注释时，Watson 即会进行学习并开始预测注释。继续进行注释，直至 Watson 能正确、一致地识别字段。
1. 完成注释后，单击**将更改应用于集合**。这将打开**上传文档**屏幕。将文档重新上传到您的集合。上传完成后，会将您重定向到**管理数据**屏幕。

字段|定义
------ | ------ 
answer|问答对中（通常在常见问题中）针对问题的答案。
author|作者的姓名。
footer|使用此标记来表示显示在页面底部的有关文档的元信息（例如，页码或参考）。
header|使用此标记来表示显示在页面顶部的有关文档的元信息。
question|问答对中（通常在常见问题中）的问题。
subtitle|正在注释的文档的副标题。
table_of_contents |对文档目录中的列表使用此标记。
text    |将此标记用于标准复制文本，包括段、定义，或者不是标题、表的一部分、答案、作者、子标题、页眉或页脚的任何一组文字。
title    |正在注释的文档的主标题。

## 如何注释表
{: #tables}

表注释为 Beta 发行版。可以在[此处](/docs/services/discovery?topic=discovery-release-notes#beta-features)找到说明 Beta 功能的陈述。
{: important}

开始注释之前，请参阅[注释文档和表的最佳实践](/docs/services/discovery?topic=discovery-sdu#bestpractices)。

1. 选择 SDU 编辑器右侧的 `table` 字段，然后在文档中选择该表。 
1. 将鼠标悬停在该表上可显示**注释表**按钮。单击该按钮以打开表编辑器。
1. 首先，设置该表的框线：
   - 选择 `column` 字段。
   - 单击表中的列以将其激活。
   - 选择 `row` 字段。
   - 单击表中的行以将其激活。

   左侧的表预览中将显示表的框线。

   **注：**在您注释表时，Watson 即会进行学习并开始预测注释。
1. 然后，标注该表中的内容。
1. 完成对表的注释后，单击**完成注释**。
1. 单击**将更改应用于集合**。这将打开**上传文档**屏幕。将文档重新上传到您的集合。上传完成后，会将您重定向到**管理数据**屏幕。

使用此视频作为指导 ![表注释视频](images/SDU_table_demo.gif){: gif}

字段|定义
------ | ------ 
body |包含信息的任何非头单元格
column header|表中每列的标题单元格（如果存在）
multi-column header|跨多列的任何标题单元格
row title |行标题列的列标题（如果存在）
row header|表中每行的行标签（如果存在）
multi-row header|跨多行的任何行标签

## 拆分文档
{: #splitting}

**管理字段**选项卡包含**拆分文档以改进查询结果**选项。使用此选项，可根据字段名称将文档拆分为分段。拆分后，每个分段都是一个单独的文档，将进行扩充、建立索引以及作为单独查询结果返回。 

文档根据单个字段名称进行拆分，例如：`title`、`author` 和 `question`。 

注意事项：

  - 每个文档的分段数限制为 `250` 个。超过 `249` 个分段之后剩余的任何文档内容都将存储在第 `250` 个分段中。

  - 每个分段都会计入套餐的文档限制。{{site.data.keyword.discoveryshort}} 将对分段建立索引，直到达到套餐限制。请参阅 [Discovery 价格套餐](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)以了解文档限制。

  - 将抽取 PDF 和 Word 元数据以及任何定制元数据，并包含在每个分段的索引中。文档的每个分段将包含完全相同的元数据。

  - 如果更新了已拆分的文档，并且需要重新上传该文档，那么应使用[更新文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/discovery#update-a-document){: new_window} 方法来替换该文档。应使用 `/environments/{environment_id}/collections/{collection_id}/documents/{document_id}` API 的 POST 方法来上传该文档，并将当前某个分段的 `parent_id` 字段的内容指定为 `{document_id}` 路径变量。将覆盖所有分段，除非更新后的文档版本的总部分数少于原始版本。这些较旧的分段会保留在索引中，并且可以使用 API 单独删除这些分段。请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/discovery#delete-a-document){: new_window} 以获取详细信息。 

## 导入和导出模型
{: #import}

使用 SDU 编辑器定义模型后，您可以将其保存并在其他集合上复用。

可以使用编辑器顶部的工具栏导入或导出完成的 SDU 模型。单击最后一个图标，并选择`导入模型`或`导出模型`。

导出的模型的文件扩展名为 `.sdumodel`。 

导入的模型旨在直接使用，而不进行任何进一步注释。如果在导入模型后继续注释，模型将被完全覆盖。如果计划将模型导入新集合，最佳实践是创建仅包含 1 个文档的新集合，导入模型，然后上传其余文档。

## 注释文档和表的最佳实践
{: #bestpractices}

表注释为 Beta 发行版。可以在[此处](/docs/services/discovery?topic=discovery-release-notes#beta-features)找到说明 Beta 功能的陈述。
{: important}

- 遵循所有准则并对所有文档使用一致的标注
- 不标注空格
- 在图像和图上使用 `image` 标签
- 不要以不同方式处理**粗体**、_斜体_或带下划线的文本。基于上下文而非样式进行标注。 
- 标注文档时，请从第一页开始，一直标注到最后一页。
- 如果不正确地标注了某项，请为该项选择其他标签以覆盖先前的标签。
- 可以随时提交页面。在提交之前，请确保所有相应的标注都已完成。
- 如果文档和表显示有叠加在其他文本上的文本，那么这些文档和表会视为“双重叠加”，因此无法对其进行注释。请向管理员报告这些文档。
- 不能对在单个页面上包含多个文本列的文档和表进行注释。请向管理员报告这些文档。
- 仅当脚注显示在页面底部，并在文档的正文文本中引用时，才应对其进行标注。
- 显示在节或列表内的注释（例如，明确标注为“注释”）应标注为 `text`。
- 如果您不确定表是否已正确标注，并且预览窗格变为无响应，那么应在浏览器中重新装入该页面，并重新标注该表，以确保正确性。

