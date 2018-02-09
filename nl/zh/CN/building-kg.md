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

# Watson Discovery 知识图

知识图不仅仅是通过在文档的数据之间建立连接并生成新知识来提供数据和信息。我们提供了 AI 技术来自动根据非结构化数据创建定制知识图，具体方法是抽取实体和关系并对其消歧，使用算法方法扩充关系，然后使用相关性算法对结果排名。知识图可以充当公司的“知识中心”，用于企业搜索、摘要、推荐引擎和其他决策过程 - 例如检测欺诈、浪费或滥用情况。在知识图创建过程中使用定制模型（在 {{site.data.keyword.knowledgestudioshort}} 中创建）可以帮助构建特定于领域的知识图，使这些知识图适用于财务、技术、安全性、情报、医疗卫生等诸多领域。

{{site.data.keyword.discoveryfull}} 中添加了两个新端点，用于在非结构化文档集合中的文档中，搜索已消歧的实体和已扩充的关系。搜索结果可以按相关性或热门程度排名。除了搜索标记之外，API 还可以使用可选的上下文字词或段落，在自动创建的大型知识图中查找更多相关的实体和关系。

 下图显示了知识图如何适应当前的 {{site.data.keyword.discoveryfull}} 管道。{{site.data.keyword.nlushort}} 使用实体扩充文档，并在单个文档级别进行记录。在知识图创建期间，使用隐式（自动）实体解析和图形扩展方法来自动创建文档之间的实体和关系连通图。除了创建知识图之外，知识图分析服务还添加了相关性排名方法来返回结果。

![知识图过程](images/knowledge-graph.png)

此知识连通图和排名方法提供：

-  使用模糊搜索标记、类型信息（可选）和上下文（可选）消歧的实体。示例：在 `Apple` 上下文中搜索 `Steve` 会返回 `Steve Jobs`，而在 `Microsoft` 上下文中搜索 `Steve` 会在顶部返回 `Steve Ballmer`。
-  通过输入模糊搜索标记和上下文（可选），按相关性排名的关系。相关性排名利用图形的全局属性来显示更具体的信息。示例：在 `health` 上下文中搜索 `Obama` 的关系会返回 `Affordable Care Act` 及其他相关实体。
-  通过查询知识连通图中的实体和关系，执行跨文档推断和聚集。此类查询的一些示例为：人员 X 与人员 Y 的关系如何？员工 X 的数据访问模式与标准模式有何不同？人员 X 的影响范围是什么？

## 服务需求

在 Beta 发布期间，与之关联的知识图功能和方法仅可用于预订**高级**套餐的服务实例。

## 集合需求

{{site.data.keyword.discoveryshort}} 使用从摄入的文档中抽取的实体和关系来构成知识图，并允许执行实体和关系查询。

**注：**知识图只能用于专用数据集合，而不可用于 {{site.data.keyword.discoverynewsshort}}。

要使用知识图，必须对集合进行配置以满足特定需求，如下所示：

-  必须为将利用知识图的字段指定 `entities` 和 `relations` 扩充项，并且每个扩充项必须使用相同的定制模型。如果需要公共模型，那么必须以定制模型 `model="en-news"` 的形式指定该公共模型。

-  必须按如下所示指定 `relations` 扩充项：
   ```json
   "relations": {
     "model": "en-news"
   }
   ```
   {: codeblock}

-  必须按如下所示指定 `entities` 扩充项，并且其中还必须指定 `mentions`、`mentions_types` 和 `sentence_locations` 参数：
   ```json
   "entities": {
     "mentions": true,
     "mention_types": true,
     "sentence_locations": true,
     "model": "en-news"
    }
    ```
    {: codeblock}

   还可以根据需要指定其他可选的 `enrichments` 选项（例如 `"sentiment": true`）。

无法使用 {{site.data.keyword.discoveryshort}} 工具来添加这些选项，必须使用 API 上传定制配置。[此处](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/discovery/config-default-kg.json)提供了已修改的缺省配置的副本，扩充了 `text` 字段，以便集合可用于公共模型的知识图。

创建 {{site.data.keyword.discoveryshort}} 服务实例后，按如下所示创建定制配置：

1. 发出以下命令以创建名为 `my-first-environment` 的环境。将 `{username}` 和 `{password}` 替换为您的服务凭证：

   ```bash
   curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "api/v1/environments?version=2017-11-07"
   ```
   {: pre}

   此 API 将返回环境标识、环境状态以及环境正在使用的存储量等信息。

   您将需要返回的 `{environment_id}`。

1. 接下来，创建定制配置。此过程假定您要上传的是在[此处](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/discovery/config-default-kg.json)找到的配置。如果要构建自己的定制配置，请参阅[配置参考信息](/docs/services/discovery/custom-config.html)。

   ```bash
   curl -X PUT -u "{username}":"{password}" -H "Content-Type: application/json" -d config-default-kg.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07"
   ```
   {: pre}

1. 上传定制配置后，可以在您创建的任何集合中进行使用，只要指定该定制配置，就可以使用任何方法来上传文档。如果您不熟悉如何创建集合和上传文档，请参阅[工具入门](/docs/services/discovery/getting-started-tool.html)。执行到[步骤 3](/docs/services/discovery/getting-started-tool.html#create-custom-configuration) 时，请选择`知识图配置`，而不创建新配置。

## 实体查询
{: #entities}

在 Beta 发行版中，知识图实体查询支持基于上下文的实体消歧。根据提供的实体文本和可选的上下文文本，消歧功能可识别唯一实体，并返回基于上下文信息排名的实体列表。通过对 `JSON` 对象执行 `POST` 操作将该对象发布到 `v1/environments/{environment_id}/collections/{collection_id}/query_entities` 端点来执行知识图实体查询。

可以使用 API 或使用 {{site.data.keyword.discoveryshort}} 工具来查询实体。请参阅[使用 Discovery 工具查询知识图](/docs/services/discovery/building-kg.html#querying-kg)以获取工具信息。

知识图实体查询 JSON 对象采用以下格式：

```json
{
  "feature": "disambiguate",
  "entity": {
    "text": "Steve",
    "type": "Person"
  },
  "context": {
    "text": "iphone"
  },
  "count": 10
}
```
{: codeblock}

- `"feature": string` _必需_ - 要使用的实体查询功能，必须为 `disambiguate`。
-  `"entity": {}` _必需_ - 包含要消歧的实体信息的对象。
   -  `"text": string` _必需_ - 将消歧的实体文本。
   -  `"type": string` _可选_ - 要对其消歧的可选实体类型，如果未指定，将包含所有类型。
-  `"context": {}` _可选_ - 包含消歧的上下文需求的可选对象。
   -  `"text": string` _可选_ - 用于为所查询实体提供上下文并基于该关联排名的实体文本。例如，如果要查询位于 England 的城市 London，那么查询将使用上下文 `England` 查找 `London`。输入可以是部分名称，也可以是包含相关实体词汇的大段落。可以同时传递多个词汇。
-  `"count": INT` _可选_ - 要返回的已消歧实体数。缺省值为 `10`。最大值为 `1000`

此查询会返回以下形式的结果：

```json
{
  "entities": [
    {
      "text": "Steve Jobs",
      "type": "PERSON"
    },
    {
      "text": "Steve Wozniak",
      "type": "PERSON"
    }
  ]
}
```
{: codeblock}

如果找不到匹配项，那么将返回以下 JSON 对象：

```json
{
  "entities": []
}
```
{: codeblock}

## 关系查询
{: #relations}

知识图关系查询支持基于输入实体使用隐式实体消歧和基于上下文的关系来查找最相关的关系，还支持按相关性分数和提及计数排序，以及按类型和文档标识进行过滤。

可以使用 API 或使用 {{site.data.keyword.discoveryshort}} 工具来查询关系。请参阅[使用 Discovery 工具查询知识图](/docs/services/discovery/building-kg.html#querying-kg)以获取工具信息。

通过对 `JSON` 对象执行 `POST` 操作将该对象发布到 `v1/environments/{environment_id}/collections/{collection_id}/query_relations` 端点来执行知识图实体查询。知识图关系查询 JSON 对象采用以下格式：

```json
{
  "entities": [
    {
      "text": "Steve Jobs",
      "type": "PERSON",
      "exact": true
    }
  ],
  "context": {
    "text": "iphone"
  },
  "sort": "score",
  "filter": {
    "relation_types": {
      "exclude": ["colocation"],
      "include": ["locatedAt", "employedBy", "managerOf", "founderOf"]
    },
    "entity_types": {
      "exclude": ["EVENT"],
      "include": ["PERSON", "GPE", "ORGANIZATION"]
    },
    "document_ids": ["b95df4c1-d00f-4771-abb2-a52baea0444a", "ad340635-bf3e-47a5-bea5-5e778f600c32"]
  },
  "count": 10
}
```
{: codeblock}

-  `"entities": []` _必需_ - 包含将查询其关系的实体的数组。如果仅定义了一个实体对象，那么将返回所有相邻关系。定义多个实体对象时，将返回相互成对的关系。相互成对的关系会返回输入实体之间的直接关系，而不是与所有实体邻居之间的关系。每个实体对象都包含：
   -  `"text": string` _必需_ - 实体文本。
   -  `"type": string` _可选_ - 可选的实体类型。如果 `"exact"` 为 `true`，那么此字段是必需的。
   -  `"exact": boolean` _可选_ - 如果为 `false`，将执行隐式消歧。隐式消歧将对每个输入实体对象使用排名第一的已消歧实体。缺省值为 `false`。
-  `"context": {}` _可选_ - 包含上下文需求的可选对象。
   -  `"text": string` _可选_ - 用于为所查询实体提供上下文并基于该关联排名的实体文本。例如，如果要查询位于 England 的城市 London，那么查询将使用上下文 `England` 查找 `London`。输入可以是部分名称，也可以是包含相关实体词汇的大段落。可以同时传递多个词汇。
-  `"sort": string` _可选_ - 关系的排序方法，可以为 `score` 或 `frequency`。缺省值为 `score`。`score` 基于关系和邻居与输入实体的相关性以及与上下文的相关性（如果提供了上下文）。`frequency` 是识别到每个关系的唯一次数。
-  `"filter": {}` _可选_ - 包含此查询要据以过滤的关系类型、实体类型和特定文档的对象。缺省情况下，不会排除任何内容。
   -  `"relation_types": {}` _可选_ - 要过滤的关系类型的列表。
      -  `"exclude": []` _可选_ - 要从查询中排除的关系类型的逗号分隔列表。
      -  `"include": []` _可选_ - 要在查询中显式包含的关系类型的逗号分隔列表。如果指定，所有其他类型均被视为已排除。
   -  `"entity_types": {}` _可选_ - 用于过滤邻居的关系类型的列表。不适用于多实体输入，因为不会返回任何新的邻居。
      -  `"exclude": []` _可选_ - 要从查询中排除的实体类型的逗号分隔列表。
      -  `"include": []` _可选_ - 要在查询中显式包含的实体类型的逗号分隔列表。如果指定，所有其他类型均被视为已排除。
   -  `"document_ids": []` _可选_ - 要对其执行关系查询的文档的逗号分隔列表。
-  `"count": INT` _可选_ - 要返回的关系数。缺省值为 `10`。最大值为 `1000`。

此查询会返回以下形式的结果：

```json
{
  "relations": [
    {
      "type": "FOUNDEROF",
      "frequency": 7,
      "arguments": [
        {
          "entities": [
            {
              "type": "PERSON",
              "text": "Steve Jobs"
            }
          ]
        },
        {
          "entities": [
            {
              "type": "ORGANIZATION",
              "text": "Apple"
            }
          ]
        }
      ]
    }
  ]
}
```
{: codeblock}

在关系数组的每个对象中，都会返回包含一对实体数组的自变量数组，第一个实体数组是关系的源或主体，第二个实体数组是关系的目标或受体。

如果找不到匹配项，那么将返回以下 JSON 对象：

```json
{
  "relations": []
}
```
{: codeblock}

## 使用 Discovery 工具查询知识图
{: #querying-kg}

具有预订[**高级**](/docs/services/discovery/building-kg.html#service-requirements)套餐的服务实例的用户可以使用 {{site.data.keyword.discoveryshort}} 工具通过知识图查询专用集合。
要在 {{site.data.keyword.discoveryshort}} 工具中访问知识图查询，请执行以下操作：

1.  单击 ![“查询”图标](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> 以打开查询页面。
1.  选择集合，然后单击**开始使用**。
1.  在**构建查询**屏幕上，选择**知识图**选项卡，然后选择**实体**或**关系**。
