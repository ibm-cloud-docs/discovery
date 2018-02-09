---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-15"

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

- 合同的自然语言理解，重点是软件采购合同和法规文档
- 能够将程序化 PDF 转换为带注释的 JSON
- 识别符合主题专业知识的合法实体和类别

“元素分类”将一组功能丰富的集成、自动化 Watson API 整合在一起，以输入程序化 PDF 来识别：部分、列表（编号和项目符号）、脚注和表，将这些项转换为结构化 HTML 格式。此外，此结构化格式的分类将进行注释并以 JSON 形式输出，含有带标签的元素、类型和类别。

“元素分类”可安全地传输执行了动态和静态加密的数据。有关 IBM Cloud 安全性的信息，请参阅 [IBM Cloud 服务描述 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=IBM+Bluemix+Service+Description){: new_window}。

## 分类需求

要使用“元素分类”对文档进行分类，配置和源文档必须满足以下需求：

- 要分析的文件为 PDF 格式。
- PDF 内容为文本格式（无法解析已扫描而未执行 OCR 的文档）

  **注：**您可以通过在 PDF 查看器中打开文档并使用**文本选择**工具选择单字，以识别文本格式的 PDF。如果无法在文档中选择单字，说明无法解析该文件。

- 文件大小不超过 50 MB。
- 无法解析安全 PDF（使用密码才可打开）和限制编辑的 PDF（使用密码才可编辑）。
- 必须创建包含 `elements` 扩充项的定制 {{site.data.keyword.discoveryshort}} 配置。此配置只能用于摄入 PDF 文档。
- **Lite** 和**标准**套餐每月最多可以处理 500 个页面。
- 不可用于预订**高级**套餐的服务实例。

## 集合需求

要使用“元素分类”，必须对集合进行配置以满足特定需求，如下所示：

- 将忽略指定的 `PDF` 转换设置。
- 可以省略 `WORD` 转换设置，因为在指定“元素分类”时，无法摄入 Microsoft Word 文件。
- 将忽略指定的 `html` 规范化设置。
- 指定了 `elements` 扩充项时，不支持文档拆分。
- 在 {{site.data.keyword.discoveryshort}} 配置中，`html` 字段必须通过 `elements` 扩充项进行扩充，并且将 `model` 指定为 `contract`。在以下示例中，`destination_field` 为 `enriched_html`，但也可以使用任何有效名称：

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

可以使用 {{site.data.keyword.discoveryshort}} 工具来添加这些选项，创建定制配置，并将**元素分类**扩充项添加到 `html` 字段。

**注：**使用该工具添加**元素分类**时，`destination_field` 会设置为 `enriched_html_elements`。

定制配置创建后，可以在任何集合中使用，只要指定该定制配置，就可以使用任何方法来上传文档。如果您不熟悉如何创建集合和上传文档，请参阅[工具入门](/docs/services/discovery/getting-started-tool.html)。

## 分类的元素

一旦使用“元素分类”对文档建立了索引，即会将 `elements` 数组作为该可搜索文档的一部分来返回该文档。

`elements` 数组中的每个对象描述“元素分类”识别到的一个合同元素。以下代码表示典型元素：

```
{
   "sentence" : {
     "begin" : 34941,
     "end" : 35307
   },
   "sentence_text" : "A buyer must buy from the supplier.",
   "types" : [ {
     "label" : {
       "nature" : "Obligation",
       "party" : "Supplier"
     },
     "assurance" : "High"
   } ],
   "categories" : [ {
     "label : "Responsibilities",
     "assurance : "High"
     }
   ]
}
```

该元素有四个重要部分：

- `sentence_text` - 已分析的文本。
- `sentence` - 此对象描述在转换的 HTML 中找到该元素的位置，包含起始字符值和结束字符值。
- `types` - 此数组描述元素的内容及其影响的当事方，由一组或多组 `party`（语句所影响的当事方）和 `nature`（语句对识别到的当事方的影响）组成
- `categories` - 此数组列出识别到的语句所属的功能类别。语句的主题。

**注**：某些语句不属于任何类型或类别，在这种情况下，返回的 `types` 和 `categories` 数组为空。

**注**：某些语句涵盖多个主题，因此在返回这些语句时会列出多个 `types` 和 `categories` 项。

此外，还在 parties 数组中定义了识别到的任何当事方：

```
  "parties" : [ {
    "party" : "Customer",
    "role" : "Buyer"
  } ]
```

对于 parties 数组的每个元素，有两个重要部分：

- `party` - 在文档内识别为当事方的文本。
- `role` - 识别到的当事方的角色。角色根据子域而变化，请参阅有关指定子域的信息以获取可能角色的列表。无法识别到特定角色的当事方会标记为“未知”。


## 了解合同元素

通过“元素分类”解析的合同会在分析识别到的每个元素后返回。

以下各部分描述返回的 JSON 如何描述分析。

### Type

元素 `types` 信息是一个对象数组，其中每个对象包含识别为此元素一对值的 nature 和 party。以下各表描述了可以识别到的可能的 `nature` 和 `party`。

Nature 是语句需要的操作类型。

| **Nature** | **描述**|
| --- | --- |
| Definition | 此元素向术语/关系/等内容添加澄清。无需操作来实现此元素，也不会影响任何当事方。|
| Disclaimer | 此元素中的当事方没有义务履行此元素中的特定条款，但并未禁止其履行这些条款。|
| Exclusion | 此元素中的当事方不会履行此元素中规定的特定条款。|
| Obligation | 此元素中的当事方必须履行此元素中的条款。|
| Right | 此元素中的当事方一定会收到此元素中的条款。|

### Parties

对于识别到的每个条款，会按名称识别受影响当事方。然后，按 `role` 对识别到的每个当事方进行分类。当事方是合同的参与者。可以识别的合同角色如下所示：

| **Role** | **描述**|
| --- | --- |
| `Buyer` | 负责付款购买货物/服务的当事方。|
| `End User` | 将与实际货物/服务进行交互的当事方，明确区别于 Buyer。|
| `None` | 未识别到此元素的任何当事方，始终与 Definition 性质成对使用。|
| `Supplier` | 负责提供货物/服务的当事方。|

### Categories

Categories 定义语句的主题。可以识别到以下类别。

| **Categories** | **描述**|
| --- | --- |
| `Amendments` | 对原始合同的修改，用于规定更改条款的条件。|
| `Asset Use` | 协议中任何一方将使用的任何资产的详细信息。|
| `Assignments` | 将一方持有的权利转让给另一方。|
| `Audits` | 此条款允许买方检查或检验供应商所提供的服务。|
| `Communication` | 描述可接受的通信方法和联系人信息。|
| `Confidentiality` | 描述将如何处理保密信息或私有信息，例如谁可以共享哪些内容以及如何共享。|
| `Business Continuity` | 描述在发生破坏性事件的情况下，组织将如何在预定义级别继续交付工作。|
| `Definitions` | 用于定义文档中所用术语的部分。|
| `Deliverables` | 在某项工作结束时要交付的项或服务。|
| `Delivery` | 用于完成项目的特定日程安排或过程。|
| `Dispute Resolution` | 规定合同方之间出现任何争议时如何处理。|
| `Force Majeure` | 此条款用于免除在发生破坏性事件时双方的责任。|
| `Indemnification` | 描述违反条款时的补救措施或后果。|
| `Insurance` | 描述供应商必须承保的范围。|
| `Intellectual Property` | 与专利、版权和商标相关的条款。可能更普遍地与发明、著作或专有技术相关。|
| `Liability` | 描述有关各方的义务和责任限制。|
| `Miscellaneous` | 不适合放入其他类别的相关部分。|
| `Payment Terms & Billing` | 描述应付款项以及付款安排。|
| `Pricing & Taxes` | 描述价格构成以及如何承担税费|
| `Privacy` | 描述适用的隐私规定。|
| `Responsibilities` | 描述各方的责任。|
| `Safety and Security` | 描述如何预防当事方受伤。包括人员和实物资产安全。|
| `Scope of Work` | 描述工作说明书中详述的将由各方实现的目标。|
| `Subcontracts` | 与参与履行需求的任何第三方相关。|
| `Term & Termination` | 履行某些内容的时间以及可能导致合同终止的条件。|
| `Warranties` | 供应商保证产品的功能。|

### Assurance

对于“元素分类”识别到的每项（type 或 category），都会给予 `assurance` 评级。assurance 的可能值如下所述：

| **Assurance** | **描述**|
| --- | --- |
| `High` | 有明显的证据证明给出的分类能够代表内容。|
| `Low` | 有一些证据支持该分类，但可能需要进一步复查以进行确认。|
