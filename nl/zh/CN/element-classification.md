---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-23"

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

# 元素分类
{: #element-classification}

借助“元素分类”，可以通过管理文档快速进行解析，以转换、识别和分类重要元素。使用最新的自然语言处理时，将从文档的元素中抽取 party（所指对象）、nature（元素类型）和 category（特定类）。

“元素分类”旨在提供以下功能：

-  合同的自然语言理解，重点是软件采购合同
-  能够将程序化 PDF 转换为带注释的 JSON
-  识别符合主题专业知识的合法实体和类别

“元素分类”将一组功能丰富的集成、自动化 Watson API 整合在一起，以输入程序化 PDF 来识别：部分、列表（编号和项目符号）、脚注和表，将这些项转换为结构化 HTML 格式。此外，此结构化格式的分类将进行注释并以 JSON 形式输出，含有带标签的元素、类型和类别。

“元素分类”可安全地传输执行了动态和静态加密的数据。有关 IBM Cloud 安全性的信息，请参阅 [{{site.data.keyword.Bluemix_notm}} 服务描述 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=%28IBM+Cloud+Service+description%29){: new_window}。

“元素分类”会返回包含以下内容的 JSON 对象：

-  `documents` 对象，包含输入文档的标题、HTML 版本的输入文档和输入文档的 MD5 散列。
-  有关用于对输入文档进行分类的模型的信息。  
-  `elements` 数组，详细描述了在输入文档中识别到的语义元素。
-  `tables` 数组，用于对在输入文档中识别到的表进行细分。
-  `document_structure` 对象，用于列出在输入文档中识别到的节标题和主题句。
-  `parties` 数组，用于列出在输入文档中识别到的参与方以及参与方的角色、地址和联系人。
-  用于定义 `effective_dates` 和 `contract_amounts` 的数组。

此功能当前仅支持英语版本，请参阅[语言支持](/docs/services/discovery/language-support.html#feature-support)以获取详细信息。


## 分类需求
{: #element-class}

要使用“元素分类”对文档进行分类，配置和源文档必须满足以下需求：

-  要分析的文件为 PDF 格式。
-  PDF 内容以文本格式显示。无法解析扫描的文档，即使扫描内容已通过 OCR 进行处理。**注：**您可以通过在 PDF 查看器中打开文档并使用**文本选择**工具选择单字，以识别文本格式的 PDF。如果无法在文档中选择单字，说明无法解析该文件。
-  文件大小不超过 50 MB。
-  无法解析安全 PDF（使用密码才可打开）和限制编辑的 PDF（使用密码才可编辑）。
-  {{site.data.keyword.discoveryshort}} 工具包含名为 **Default Contract Configuration** 的配置，可用于扩充 PDF 文档集合。您还可以选择用于创建包含 `elements` 扩充项的定制配置。请参阅[集合需求](/docs/services/discovery/element-classification.html#element-collection)以获取详细信息。
-  **轻量**套餐每月最多可以处理 500 个页面。
-  在**专用**环境中不可用。
-  使用“元素分类”时无法执行扩充后规范化。

**注：****Default Contract Configuration** 文件已于 2018 年 9 月 25 日更新。如果在此日期之前已将此配置应用于集合，请参阅[发行说明](/docs/services/discovery/release-notes.html#25sept)以获取有关更新集合的信息。

## 集合需求
{: #element-collection}

要使用“元素分类”，必须对集合进行配置以满足特定需求。

{{site.data.keyword.discoveryshort}} 工具包含名为 **Default Contract Configuration** 的配置，此配置已预配置为通过**元素分类**扩充项和其他必需的选项来扩充 PDF 文档。您可以在创建集合时选择此配置。此配置的 JSON 如下：

```json
 {
   "name": "Default Contract Configuration",
   "description": "Extract party, nature, and category from elements in PDFs.",
  "conversions": {
    "html": {
  "exclude_tags_completely": [],
       "exclude_tags_keep_content": []
     }
   },
   "enrichments": [
     {
       "source_field": "html",
       "destination_field": "enriched_html_elements",
       "enrichment": "elements",
       "options": {
         "model": "contract"
    }
  }
   ]
 }
```
{: codeblock}

如果要创建定制配置文件，请配置集合以满足以下需求：  

-  将忽略指定的 `PDF` 转换设置。
-  可以省略 `WORD` 转换设置，因为在指定“元素分类”时，无法摄入 Microsoft Word 文件。
-  将忽略指定的 `html` 规范化设置。
-  指定了 `elements` 扩充项时，不支持文档分段。
-  在 {{site.data.keyword.discoveryshort}} 配置中，`html` 字段必须通过 `elements` 扩充项进行扩充，并且将 `model` 指定为 `contract`。在以下示例中，`destination_field` 为 `enriched_html`，但也可以使用任何有效名称：

```json
"enrichments": [
   {
     "source_field": "html",
    "destination_field": "enriched_html",
    "enrichment": "elements",
    "options": {
      "model": "contract"
    }
  }
 ]
```
{: codeblock}

选择工具中的 `Default Contract Configuration` 后，可以上传文档。如果您不熟悉如何创建集合和上传文档，请参阅[工具入门](/docs/services/discovery/getting-started-tool.html)。

## 分类的元素

一旦使用“元素分类”对文档建立了索引，即会将 `elements` 数组作为该可搜索文档的一部分来返回该文档。

`elements` 数组中的每个对象描述 {{site.data.keyword.discoveryshort}} 识别到的一个合同元素。以下代码表示典型元素：

```json
 {
    "location" : {
     "begin" : 134323,
     "end" : 135109
    },
    "text" : "9. In the event that the Participant's total vested account balance is determined to be less than or equal to $2,000.00 as of the date that the Order is received, the parties will be informed in writing that the QDRO determination fee may potentially liquidate the account.",
   "types" : [ {
     "label" : {
       "nature" : "Obligation",
        "party" : "All Parties"
      },
      "provenance_ids" : ["Nlu0ogWAEGms4vjhhzpMv3iXhm8b8fBqMBNtT/bXH8JI=", "PlyERkjg5is36RpFjVUFXp69eDmGmCxLCXRs1sDMDUCo="
      ]
    } ],
   "categories" : [ {
     "label" : "Communication",
      "provenance_ids" : [ "Cs38YyU6VBFtJK1/bgtEJBlqqWmX5F6OYUciRxQXf7HrN5TOCPuI7QXbkbj4LRXoxVuB3/i9H15q5TU+vFxorhUBeWFfF998OYQiPYViD2yI="
      ]
    } ],
    "attributes" : [ {
      "type" : "Currency",
      "text" : "$2,000.00",
      "location" : {
        "begin" : 134780,
        "end" : 134789
      }
    } ]
 }
 ```
{: codeblock}

每个元素具有五个重要部分：
-  `location`：`begin` 和 `end` 索引，用于指示元素在输入文档中的位置。
-  `text`：已分类元素的文本。
-  `types`：一个数组，包含零个或更多个 `label` 对象。每个 `label` 对象都包含 `nature` 字段和 `party` 字段；nature 字段用于列出元素对所识别到的参与方的影响（例如，`Right` 或 `Exclusion`），party 字段用于标识该元素影响的参与方。请参阅[了解合同解析](/docs/services/discovery/parsing.html#contract_parsing)中的[类型](/docs/services/discovery/parsing.html#contract_types)以获取其他信息。
-  `categories`：一个数组，包含零个或更多个 `label` 对象。每个 `label` 对象的值列出了识别到的元素所属的功能类别。请参阅[了解合同解析](/docs/services/discovery/parsing.html#contract_parsing)中的[类别](/docs/services/discovery/parsing.html#contract_categories)以获取其他信息。
-  `attributes`：一个数组，用于列出定义元素属性的零个或更多个对象。当前支持的属性类型包括 `Location`（元素引用的地理位置或区域）、`DateTime`（元素指定的日期、时间、日期范围或时间范围）和 `Currency`（货币值和单位）。`attributes` 数组中的每个对象还包含所识别到的元素的文本和位置；位置由输入文档中的文本的 `begin` 和 `end` 索引定义。请参阅[了解合同解析](/docs/services/discovery/parsing.html#contract_parsing)中的[属性](/docs/services/discovery/parsing.html#attributes)以获取其他信息。

此外，`types` 和 `categories` 数组中的每个对象都包含一个 `provenance_ids` 对象。`provenance_ids` 数组中列出的值是散列值，您可以将其发送给 IBM 来提供有关与该元素关联的分析部分的反馈或接收与此相关的支持。

**注**：某些语句不属于任何类型或类别，在这种情况下，服务会将 `types` 和 `categories` 数组作为空对象返回。

**注**：某些语句涵盖多个主题，在这种情况下，服务会返回多组 `types` 和 `categories` 对象。

**注**：某些语句不包含任何可识别的属性，在这种情况下，服务会将 `attributes` 数组作为空对象返回。
