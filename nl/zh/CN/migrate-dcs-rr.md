---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-03"

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


# 从 Watson Document Conversion 和 Retrieve and Rank 迁移
{: #migrate-dcs-rr}

{{site.data.keyword.documentconversionfull}} 和 {{site.data.keyword.retrieveandrankfull}} 已不推荐使用，并已替换为 {{site.data.keyword.discoveryfull}}。通常，这两个服务一起用于进行摄入和排名，然后将结果交付给应用程序。提供了本文档以逐步指导您完成从 {{site.data.keyword.documentconversionshort}} 和 {{site.data.keyword.retrieveandrankshort}} 迁移到 {{site.data.keyword.discoveryshort}} 的过程。

{{site.data.keyword.discoveryfull}} 提供了更稳健的查询界面，简化了数据摄入，改进了训练管理，并扩大了规模。{{site.data.keyword.discoveryshort}} 解决了与 {{site.data.keyword.retrieveandrankshort}} 相同的许多核心用例，包括支持代理程序辅助、组织知识库搜索和研究辅助。它在构建时考虑了 {{site.data.keyword.retrieveandrankshort}} 用户面临的许多困难，并解决了其中大量问题。{{site.data.keyword.discoveryshort}} 还提供了 {{site.data.keyword.retrieveandrankshort}} 中不可用的用于检索信息的新功能（包括段落检索和改进的搜索算法），以找到更多相关结果。

**功能比较**
{: #features-dcs-rr}

|功能| {{site.data.keyword.retrieveandrankshort}} | {{site.data.keyword.discoveryshort}} |
|:-------------|:--------------------:|:-------------:|
|自然语言搜索|是|是|
|机器学习相关性训练|是|是|
|用于训练的 UI 工具|是|是|
|JSON 答案单元输入|是|是|
|文档拆分|是|是|
|段落检索|   |是|
|文档 CRUD|是|是|
|批量 JSON 上传|是|   |
|自动文档 NLP 扩充|   |是|
|用于扩充的定制 NLP 模型集成|   |是|
|服务中存储的训练数据|   |是|
|自动化模型生命周期管理|   |是|
|用于在不训练的情况下改进相关性的语义相似度|   |是|
|工具中基于测试集的准确性度量|是|   |
|定制功能向量支持|是|   |
|定制分析器配置|是|已预配置|
|定制非索引字|是|已预配置|
|定制语言字典|是|已预配置|
|定制同义词|是|是|
**注：**此表将随着 {{site.data.keyword.discoveryshort}} 新功能的添加而更新。



在开始执行迁移操作之前，必须先[评估](#evaluate) {{site.data.keyword.retrieveandrankshort}} 服务中存储的数据，并了解如何移动构成当前解决方案的不同组件。

大多数客户将 {{site.data.keyword.documentconversionshort}} 与 {{site.data.keyword.retrieveandrankshort}} 配合使用。如果未使用 {{site.data.keyword.documentconversionshort}} 来转换内容，以使这些内容可以存储在可搜索索引中，请继续查看[用于迁移独立 {{site.data.keyword.documentconversionshort}} 的选项](#dcs)。

如果您最初使用的是 {{site.data.keyword.retrieveandrankshort}} 教程，并且将您自己的服务实例基于该教程，那么可在[此处](/docs/services/discovery?topic=discovery-migrate-rnr#migrate-rnr)找到该教程中说明如何将相同数据摄入到 {{site.data.keyword.discoveryshort}} 中的扩展内容。

**注：**{{site.data.keyword.discoveryshort}} 随附转换和扩充功能。如果您已使用 {{site.data.keyword.documentconversionshort}} 和/或 {{site.data.keyword.nlushort}} 来转换和扩充源 HTML、PDF 或 Microsoft Word 文档，那么这些服务将替换为 {{site.data.keyword.discoveryshort}} 服务中的功能。

## 评估指向 Watson Discovery 服务的迁移路径
{: #evaluate}

有两个实用选项用于从 {{site.data.keyword.retrieveandrankshort}} 进行迁移：从源内容迁移，以及从已建立索引的内容迁移。在确定要使用的选项之前，请先对这两个选项进行评估。

### 从源内容迁移
{: #source}

要从源内容迁移：

-  您需要有权访问从中摄入内容的原始源文件。
-  您需要以编程方式抽取每个文档的标识（结果在建立索引前已具有标识）

如果可以满足所有迁移条件，那么建议您使用此方法来移至 {{site.data.keyword.discoveryshort}} 服务。

要迁移源内容，请根据源数据的详情来修改[迁移教程](/docs/services/discovery?topic=discovery-migrate-rnr#migrate-rnr)中描述的过程。

#### 迁移答案单元
{: #answerunit-dcs-rr}

如果是使用 {{site.data.keyword.documentconversionshort}} 创建的答案单元，请选择以下其中一个选项来迁移该内容：

-  如果您训练了一个排名器并且需要迁移排名，那么应该获取从 {{site.data.keyword.documentconversionshort}} 返回的内容，然后将其摄入到 {{site.data.keyword.discoveryshort}} 中
-  如果没有任何训练数据要迁移，请使用[文档分段功能](/docs/services/discovery?topic=discovery-configservice#doc-segmentation)将原始的源文档摄入到 {{site.data.keyword.discoveryshort}} 中

### 从已建立索引的内容迁移
{: #indexed}

如果您无权访问原始源文档，或者存在以下情况，那么应该从 {{site.data.keyword.retrieveandrankshort}} 中已建立索引的内容进行迁移：

- 已使用自动文档标识生成并已训练了排名器。
- 已在 {{site.data.keyword.documentconversionshort}} 中创建答案单元并对其排名，但未保留由 {{site.data.keyword.documentconversionshort}} 服务生成的答案单元。

**注：**仅当所有必需的内容都存储在 {{site.data.keyword.retrieveandrankshort}} 中的字段中时，才能使用此方法。如果内容只建立了索引，但未存储，那么无法从服务中查询内容，并且必须再次从源中对数据进行转换和拆分。

使用 [/v1/solr_clusters/{solr_cluster_id}/solr/\{collection_name\}/select ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/retrieve-and-rank/api/v1/#index_doc){: new_window} 方法和空白查询 `q=*:*` 从服务中抽取文档。返回的文档数可能大于实际的最大返回计数（对于大多数集合，为 `200`）。如果发生这种情况，应该使用适当的[分页 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://lucene.apache.org/solr/guide/6_6/pagination-of-results.html){: new_window} 来发出多个调用，以收集所有文档。

使用 [/v1/environments/\{environment_id\}/collections/\{collection_id\}/documents/\{document_id\} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/discovery#update-a-document){: new_window} 方法将具有指定**标识**的文档上传到 {{site.data.keyword.discoveryshort}} 服务。每个文档上传都是一个单独的 API 调用。

## 迁移训练数据
{: #trainingdata-dcs-rr}

迁移结果之后，下一步是迁移已为内容创建的所有训练数据。有两个选项可用于迁移训练数据：从源 (`csv`) 迁移，以及从服务迁移。如果您已通过 `csv` 文件上传了训练数据，并仍有权访问该文件，那么应该从源进行迁移。如果您使用的是 {{site.data.keyword.retrieveandrankshort}} 工具或无权访问原始 `csv` 文件，那么应该从服务进行迁移。

### 从源内容迁移训练数据
{: #csv}

要从排名的源内容迁移：

- 您需要有权访问初始用于上传训练信息的原始源 `csv` 文件。
- 您应确保对其建立索引的已训练文档的标识与在 {{site.data.keyword.retrieveandrankshort}} 中对其建立索引的已训练文档的标识一致。

如果可以满足所有迁移条件，那么建议您使用此方法将训练数据移至 {{site.data.keyword.discoveryshort}} 服务。

要迁移训练数据，请根据源数据的详情来修改[迁移教程](/docs/services/discovery?topic=discovery-migrate-rnr#migrate-rnr)中描述的过程。

### 从服务迁移训练数据
{: #extract-train}

要从 {{site.data.keyword.retrieveandrankshort}} 服务迁移训练数据，您需要执行以下操作：使用 {{site.data.keyword.retrieveandrankshort}} API 来抽取训练数据，将 {{site.data.keyword.retrieveandrankshort}} 训练 JSON 转换为 {{site.data.keyword.discoveryshort}} 可使用的格式，最后使用该 API 将训练数据摄入到 {{site.data.keyword.discoveryshort}} 中。

要从 {{site.data.keyword.retrieveandrankshort}} 中抽取训练数据，请使用 {{site.data.keyword.retrieveandrankshort}} 工具中的 `Export` 功能。成功下载完整导出后，解压缩保存的 `.zip` 文件。在该归档内有两个文件。训练数据存储在名为 `export-questions.json` 的文件中。此文件包含 JSON 训练对象的数组。

数组中的每个训练结果都按以下形式表示：

**样本 {{site.data.keyword.retrieveandrankshort}} 训练数据**
```json
{
    "text":"Who was the first royal to attend Wimbledon?",
    "cluster":{
        "id":"f62c11d3-30fa-11e7-8a0c-333f7f431ce8",
        "answers":{
            "f62c11d3-30fa-11e7-8a0c-33":[
                {
                    "id":"dac41335-0e96-40c9-983f-cc3f1c395782",
                    "ranking":1,
                    "source":{
                        "id":"e26a3d20-30fa-11e7-aa5e-d1632b06e0b1",
                        "file":"wimbledon-wikipedia.html",
                        "sequence":17,
                        "strategy":"retrieve"
                    }
                },
                {
                    "id":"661b4c9f-ecdb-4dad-aafc-6ae561a148c0",
                    "ranking":2,
                    "source":{
                        "id":"da1bc620-30fa-11e7-8f90-3305f35a93c9",
                        "file":"generated-otherFactsFigures.docx",
                        "sequence":67,
                        "strategy":"retrieve"
                    }
                },
                {
                    "id":"0053fdb8-c77e-4fcf-b0e0-6a4cd377266a",
                    "ranking":3,
                    "source":{
                        "id":"d9c0add0-30fa-11e7-aa5e-d1632b06e0b1",
                        "file":"generated-allEngland.docx",
                        "sequence":20,
                        "strategy":"retrieve"
                    }
                },
                {
                    "id":"506d3d50-19ed-49c8-b32f-65f848e60e86",
                    "ranking":4,
                    "source":{
                        "id":"da1bc620-30fa-11e7-8f90-3305f35a93c9",
                        "file":"generated-otherFactsFigures.docx",
                        "sequence":63,
                        "strategy":"retrieve"
                    }
                }
            ]
        },
        "flags":{

        }
    }
},
```
{: codeblock}

{{site.data.keyword.discoveryshort}} 并不需要从 {{site.data.keyword.retrieveandrankshort}} 中导出的所有信息。以下片段显示 {{site.data.keyword.discoveryshort}} 训练条目的必需结构。

```json
{
  "natural_language_query": "{natural_language_query}",
  "examples": [
    {
      "document_id": "{document_id_1}",
      "relevance": 0
    },
    {
      "document_id": "{document_id_2}",
      "relevance": 10
    }
  ]
}
```
{: codeblock}

此时，您需要将 {{site.data.keyword.retrieveandrankshort}} 训练信息转换为 {{site.data.keyword.discoveryshort}} 训练信息。转换时请考虑以下几点。

- 在 {{site.data.keyword.discoveryshort}} 中，`relevance` 分数为 `0` 表示**不相关**，而在 {{site.data.keyword.retrieveandrankshort}} 中，`ranking` 为 `1` 才表示“不相关”- 所有 `"ranking": 1` 条目必须转换为 {{site.data.keyword.discoveryshort}} 中的 `"relevance": 0`。
- {{site.data.keyword.discoveryshort}} 工具使用二进制记数法 `0` 和 `10`。如果要对更多结果排名，并使用 {{site.data.keyword.discoveryshort}} 工具，那么必须将所有 `"ranking": 1` 和 `"ranking": 2` 条目转换为 `"relevance": 0`，并将所有 `"ranking": 3` 和 `"ranking": 4` 条目转换为 `"relevance": 10`。如果您未对更多结果进行排名，或者未使用 {{site.data.keyword.discoveryshort}} 工具，那么无需执行此操作。
- {{site.data.keyword.discoveryshort}} 不需要未回答的问题，将手动检查相关性训练的有效性。

![对迁移流排名](images/migrate-ranking.png)

例如，上面列出的**样本 {{site.data.keyword.retrieveandrankshort}} 训练数据**将转换为在 {{site.data.keyword.discoveryshort}} 工具中使用，如下所示：

```json
{
  "natural_language_query": "Who was the first royal to attend Wimbledon?",
  "examples": [
    {
      "document_id": "e26a3d20-30fa-11e7-aa5e-d1632b06e0b1",
      "relevance": 0
    },
    {
      "document_id": "da1bc620-30fa-11e7-8f90-3305f35a93c9",
      "relevance": 0
    },
    {
      "document_id": "d9c0add0-30fa-11e7-aa5e-d1632b06e0b1",
      "relevance": 10
    },
    {
      "document_id": "da1bc620-30fa-11e7-8f90-3305f35a93c9",
      "relevance": 10
    }
  ]
}
```
{: codeblock}

## 语言支持
{: #language}

请参阅 [{{site.data.keyword.discoveryshort}} 的语言支持表](/docs/services/discovery?topic=discovery-language-support#language-support)。{{site.data.keyword.retrieveandrankshort}} 功能主要通过**基本** {{site.data.keyword.discoveryshort}} 语言支持进行支持。

## 迁移查询
{: #queries}

{{site.data.keyword.discoveryfull}} 查询语言与 {{site.data.keyword.retrieveandrankshort}} 使用的 Solr 查询语言不同。现有查询应重新路由到其中一个 {{site.data.keyword.discoveryfull}} 查询方法并转换为使用 {{site.data.keyword.discoveryfull}} 查询语言。下表描述了大多数查询中使用的一些典型运算符：

**从 Solr 查询迁移到 {{site.data.keyword.discoveryshort}} - 典型运算符**

|Solr 运算符|Discovery 运算符|描述|
|:-------------:|--------------------|-------------|
| `.` | `.` |JSON 定界符|
| `:` | `:` |包含|
|  | `::` |完全匹配|
|`-{fieldname}:` | `:!` |不包含|
|  | `::!` |不完全匹配|
| ``\` | ``\` |转义字符|
| `""` | `""` |短语查询|
| `()` | `()`, `[]` |嵌套分组|
|`OR` |[<code>&#124;</code>] |或|
|`AND` | [,] |和|
|`[* TO 100]` | `<=`, `>=`, `>`, `<` |数字比较|
|`^x` |`^x` |分数乘数|
| `*` | `*` |通配符|
|`~`（0 到 1）|[~n] |字符串变体|

请参阅[查询概念](/docs/services/discovery?topic=discovery-query-concepts#query-concepts)和[查询参考](/docs/services/discovery?topic=discovery-query-reference#query-reference)文档，以获取有关 {{site.data.keyword.discoveryfull}} 查询语言的详细信息。


## 独立 Watson Document Conversion 服务迁移
{: #dcs}

如果是使用 {{site.data.keyword.documentconversionshort}} 来帮助将内容摄入到 {{site.data.keyword.retrieveandrankshort}} 中，那么该功能已演变为单一服务 - {{site.data.keyword.discoveryshort}}。通过 {{site.data.keyword.discoveryshort}}，您可以轻松地将 Microsoft Word、PDF、HTML 和 JSON 文档转换、扩充和摄入到可训练且可搜索的索引中。如果您的用例未涉及将转换的内容存储在索引中，那么此部分与您相关。如果要将文档摄入索引中，请参阅[摄入到 {{site.data.keyword.discoveryshort}} 服务](/docs/services/discovery?topic=discovery-configservice#configservice)。

IBM 不再提供专用于单独转换 Microsoft Word、PDF 和 HTML 文档的服务。如果您当前在使用 {{site.data.keyword.documentconversionshort}} 服务，并且未将输出摄入到联机索引服务（例如，{{site.data.keyword.discoveryshort}}），那么建议您考虑迁移到开放式源代码替代方案，例如 [Apache Tika ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://tika.apache.org/){: new_window}。
