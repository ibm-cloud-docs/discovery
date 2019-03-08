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

# 查询概念
{: #query-concepts}

{{site.data.keyword.discoveryfull}} 服务提供了强大的内容搜索功能。通过 {{site.data.keyword.discoveryshort}} 服务上传并扩充内容后，随即可以构建查询，然后将 {{site.data.keyword.discoveryshort}} 集成到您自己的项目中，或者使用 {{site.data.keyword.watson}} Explorer Application Builder 来创建定制应用程序。
{: shortdesc}

  您编写的查询将因集合而有所不同，因为所有集合都包含唯一的内容。
  {: tip}

创建查询或过滤器时，{{site.data.keyword.discoveryshort}} 会查看每个结果并尝试与已定义的路径相匹配。如果匹配，即会将其添加到结果集。创建查询时，可以根据需要使其尽量模糊或尽量具体。查询越具体，结果越有针对性。

您还可以选择开启段落检索。段落是查询返回的完整文档中的简短相关摘录。这些目标段落是从集合中文档的 `text` 字段中抽取的。缺省情况下，一个查询最多可以返回 10 个段落，每个段落大约 400 个字符。从单个结果中最多抽取三个段落。`passages` 参数仅可用于专用集合；此参数在 {{site.data.keyword.discoverynewsshort}} 集合中不可用。请参阅[段落](/docs/services/discovery/query-parameters.html#passages)，以获取有关如何识别段落的更多信息。

  您可以使用 {{site.data.keyword.discoveryshort}} 工具或 API 来编写自然语言查询（例如“IBM Watson partnerships”）。
  {: tip}

已训练的集合将在自然语言查询的结果中返回 `confidence` 分数。请参阅[置信度分数](/docs/services/discovery/train-tooling.html#confidence)以获取详细信息。

对于以下语言，{{site.data.keyword.discoveryshort}} 会返回包含特殊字符的查询结果：英语、德语、法语、荷兰语、意大利语和葡萄牙语。例如，如果查询 `aqui`，现在将收到包含 `aqui` 的结果和包含 <code>aqu&iacute;</code> 的结果。

您可以创建更长、更复杂的查询，其中包含多个过滤器和复杂聚集。此选项仅在 API 中可用，并且将查询的字符限制增加到 10,000 个字符。请参阅[集合长查询 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query){: new_window} 和[环境长查询 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#federated-query){: new_window}，以获取详细信息。

{{site.data.keyword.discoveryfull}} Knowledge Graph 是一个 Beta 功能，提供用于跨文档查询实体和关系的新端点。这包括基于上下文的搜索和相关性排名。请参阅 [{{site.data.keyword.discoveryfull}} Knowledge Graph](/docs/services/discovery/building-kg.html) 以获取更多信息。

有关编写查询的更多信息，请参阅：
- [查询入门教程](/docs/services/discovery/getting-started-query.html)
- [查询参考](/docs/services/discovery/query-reference.html)（包括 {{site.data.keyword.discoveryshort}} Query Language 中可用的参数、运算符和聚集的列表）

## Discovery 数据模式
{: #discovery-schema}

首先来了解 {{site.data.keyword.discoveryshort}} JSON。要了解如何使用 {{site.data.keyword.discoveryshort}} Query Language 来构建查询，您需要熟悉在 {{site.data.keyword.discoveryshort}} 扩充集合中的文档后生成的 JSON。熟悉文档的数据模式后，在 {{site.data.keyword.discoveryshort}} Query Language 中编写查询会更容易。有三种方法可执行此操作。

  1. 在 {{site.data.keyword.discoveryshort}} 工具中，打开**管理数据**屏幕，然后选择包含 {{site.data.keyword.IBM_notm}} Press Releases 的集合。单击**查看数据模式**按钮。**查看数据模式**屏幕通过两种方式显示已变换文档中的字段和值：按文档（**文档视图**）或按字段（**集合视图**）。**文档视图**中将最多显示 50 个文档。**集合视图**将显示整个集合中的字段。

    在**集合视图**中的 `enriched_text` 下，可以检查通过 **Default Configuration** 文件应用的扩充项。单击 `categories`、`concepts`、`entities` 和 `sentiment` 可查看集合是如何通过 Watson 洞察扩充的。

  1. 运行“空”查询来查看 JSON。在**查看数据模式**屏幕上，单击**构建查询**按钮，然后单击**运行查询**。结果会显示在右侧的两个选项卡下：**摘要**（查询结果的概述）和 **JSON**。首先打开 **JSON** 选项卡。

     -  这四个文档前面各自有一个 `id` 号。
     -  向下滚动到 `enriched_text` 字段。检查每个扩充项，以了解可以查询的 JSON 字段。

        ![缺省配置字段](images/JSON.png)

     -  **entities** - 首先找到 `text` 字段，然后检查其他扩充项信息。
     -  **sentiment** - 首先找到 `label` 字段，然后检查其他扩充项信息。
     -  **concepts** - 首先找到 `text` 字段，然后检查其他扩充项信息。
     -  **categories** - 首先找到 `document` 字段，然后检查其他扩充项信息。

     检查了第一个文档中的洞察后，可以根据需要查看其他三个文档。

  1. 查看 **Visual Query Builder** 中的可用字段。在**构建查询**屏幕上，单击**搜索文档**，然后单击**使用 {{site.data.keyword.discoveryshort}} Query Language**。单击**字段**下拉列表以查看数据中可用的字段。单击**使用查询语言编辑**，以使用 {{site.data.keyword.discoveryshort}} Query Language 来手动构建查询。      

### 如何构造基本查询
{: #structure-basic-query}

如前所述，JSON 为分层结构，因此查询需要使用相同的层次结构进行编写。所以，如果 JSON 类似于以下内容：

```json
"enriched_text": {
  "concepts": [
    {
    "text": "Cloud computing",
    "relevance": 0.610029}
    ]
  }
```
{: codeblock}

那么查询的结构将如下所示：

![示例查询结构](images/query_structure2.png)

  对字段求值的运算符（`<=`、`>=`、`<` 和 `>`）需要将 `number` 或 `date` 作为值。将值用引号括起会使该值始终为 `string`。因此，`score>=0.5` 是有效查询，而 `score>="0.5"` 不是有效查询。请参阅[查询运算符](/docs/services/discovery/query-operators.html)以获取运算符的完整列表。
  {: tip}

注意事项：

- 不确定何时查询实体、概念或关键字？请参阅[了解实体、概念和关键字之间的差异](/docs/services/discovery/building.html#udbeck)。

- **注：**单击**运行查询**并打开 **JSON** 选项卡后，您将注意到缺省情况下查询突出显示已开启。这将向查询结果添加 `highlight` 字段。在 `highlight` 字段中，与查询匹配的字词将用 HTML`<em>`（强调）标记打包。请参阅[查询参数](/docs/services/discovery/query-parameters.html#highlight)以获取详细信息。

## 构建组合查询
{: #building-combined-queries}

可以将查询参数组合在一起，以构建更有针对性的查询。例如：可以将 `filter` 和 `query` 参数一起使用。有关过滤和查询的更多信息，请参阅 [filter 与 query 参数的差异](/docs/services/discovery/query-parameters.html#filtervquery)。

## 如何构造聚集
{: #structure-aggregation}

聚集会返回一组数据值；例如，排名靠前的关键字、实体的总体观点等。要获取聚集选项的完整列表，请参阅[聚集](/docs/services/discovery/query-reference.html#aggregations)。

![示例聚集查询结构](images/aggregation_structure.png)

此示例聚集将在集合中查找所有 `concepts`。
此查询中的定界符为 `.`，运算符为 `()`；请参阅[查询运算符](/docs/services/discovery/query-operators.html)，以了解有关 {{site.data.keyword.discoveryshort}} Query Language 中可用的其他运算符的信息。

### 示例聚集查询
{: #example-aggregations}

有若干种方法可以通过 {{site.data.keyword.discoverynewsshort}} 来聚集结果，包括排名靠前的值、总和、最小值、最大值、平均值、时间片和直方图。您还可以添加过滤器和嵌套聚集。

#### 过滤器聚集
{: #filter-aggregations}

此示例聚集将返回在 {{site.data.keyword.discoverynewsshort}} 中找到的有关 Pittsburgh Steelers 的文章数，以及这些结果中有多少具有 `positive`、`negative` 或 `neutral` 观点。

- `filter(enriched_text.entities.text:"Pittsburgh Steelers").term(enriched_text.sentiment.document.label,count:3)`


此示例聚集会先将 {{site.data.keyword.discoverynewsshort}} 中一组文章的范围缩小（过滤）为仅包含推特实体文本的文章，然后按文档观点类型划分这些文章。仅返回前 3 种文档观点类型（`positive`、`negative` 和 `neutral`）。

- `filter(enriched_text.entities.text:twitter).term(enriched_text.sentiment.document.label,count:3)`

#### 嵌套聚集
{: #nested-aggregations}

在聚集前面添加 `nested` 可将聚集限制为指定的结果区域。例如：`nested(enriched_text.entities)` 表示仅对任何结果的 `enriched_text.entities` 组成部分进行聚集。

通过查看以下两个查询之间的差异，可以轻松看到这一情况：
- `filter(enriched_text.entities.disambiguation.subtype::City)` - 聚集统计包含一个或多个类型为 `City` 的 `entity` 的 *Results* 数
- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City)` - 聚集统计结果中类型为 `City` 的 `entity` 实例数。  

此外，任何后续操作都将进一步限制可对其进行聚集的结果集。例如：

- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City)` 表示将仅聚集 `subtype::City` 的实体。
- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City).term(enriched_text.entities.text,count:3)` 将聚集子类型为 `City` 的前 3 个实体。
- `filter(enriched_text.entities.disambiguation.subtype::City).term(enriched_text.entities.text,count:3)` 将返回其中结果至少包含一个子类型为 `City` 的实体的前 3 个实体。

## 查询 Watson Discovery News
{: #querying-news}

{{site.data.keyword.discoverynewsshort}} 是已使用认知洞察进行预扩充的公共数据集，并且随附于 {{site.data.keyword.discoveryshort}} 中。请参阅 [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html#watson-discovery-news) 以获取有关此集合的更多信息。

您可以使用自然语言查询（例如“IBM Watson partnerships”）或 {{site.data.keyword.discoveryshort}} Query Language 来查询此集合。要了解有关自然语言查询的更多信息，请参阅[自然语言查询](/docs/services/discovery/query-parameters.html#nlq)。

不能调整 {{site.data.keyword.discoverynewsshort}} 配置，也不能训练 {{site.data.keyword.discoverynewsshort}} 集合或向其中添加文档。请在[此处 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://discovery-news-demo.ng.bluemix.net/){: new_window} 查看可以使用 {{site.data.keyword.discoverynewsshort}} 构建的内容的演示。

{{site.data.keyword.discoveryshort}} 工具和 API 都提供了英语、韩语、德语、西班牙语和日语语言版本的 {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} 集合。

工具中 {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} 的缺省语言是英语。要切换语言，请单击 ![管理数据](/images/icon_yourData.png) 图标，然后从下拉列表中选择相应的语言。

有关通过 API 查询集合的信息，请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection){: new_window}。Watson {{site.data.keyword.discoverynewsshort}} 英语语言版本的 `collection_id` 为 `news-en`。原先，`collection_id` 为 `news` - 如果您一直在使用先前的 `collection_id`，那么它将继续有效，但是，对于新项目，您可能希望切换到新的 `collection_id`。韩语集合的 `collection_id` 为 `news-ko`，西班牙语的 `collection_id` 为 `news-es`，德语的 `collection_id` 为 `news-de`，日语的 `collection_id` 为 `news-ja`。

{{site.data.keyword.discoverynewsfull}} 查询将在 `text` JSON 字段中显示每篇文章的前 50 个字。

针对 {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} 查询返回的最大结果数为 `50`。使用其他查询和 `offset` 参数可返回 `50` 个以上的结果。

如果使用 {{site.data.keyword.discoveryshort}} Query Language，那么可以在 {{site.data.keyword.discoverynewsshort}} 查询中包含相对日期范围，例如：`crawl_date>=now-1month`。有效的日期时间间隔值为 `second/seconds`、`minute/minutes`、`hour/hours`、`day/days`、`week/weeks`、`month/months` 和 `year/years`。`now` 不受 `time_zone` 参数的影响；`UTC` 时区为缺省值。

以下示例将查询特定日期范围内的关键字。时区信息不是必需的：
- `enriched_text.keywords.text:"olympics", publication_date<=2018-02-15T00:00:00Z, publication_date>=2018-02-01T00:00:00Z`

新闻文章可能会联合到多家新闻媒体，{{site.data.keyword.discoverynewsfull}} 会选取其中每家新闻媒体，因而会生成重复的文章。这意味着对 {{site.data.keyword.discoverynewsfull}} 的查询可能会在查询结果中返回多个完全相同或几乎完全相同的文章。您可以使用去重功能来管理此问题。要了解有关此 Beta 功能的更多信息，请参阅[从查询结果中排除重复文档](/docs/services/discovery/query-parameters.html#deduplication)。

## 查询多个集合
{: #multiple-collections}

如果环境中有多个集合，那么您可能要查看跨这些集合的结果。`environments` 级别的查询方法（`query`、`fields` 和 `notices`）允许您查询多个指定的集合。目前，{{site.data.keyword.discoveryshort}} 工具中未提供跨集合查询。

可以使用 `environments/{environment_id}/query` API 方法在相同环境中查询多个集合。跨多个集合查询时，请考虑以下各项。
-  使用此方法时，必须指定 `collection_ids` 参数。`collection_ids` 是环境中要查询的集合的逗号分隔列表。
-  查询多个集合时，支持 `passages`。
-  `collection_id` 会作为每个结果对象的一部分返回。此字段指定在其中找到结果的集合。
-  {{site.data.keyword.discoverynewsshort}} 是 `system` 环境的一部分，因此不能包含在多集合查询中。
-  查询多个集合时，单个集合相关性训练不会影响结果的排名。要在查询多个集合时对返回的结果重新排名，请实施 [Continuous Relevancy Training](/docs/services/discovery/continuous-training.html)。
-  即便已对查询中的所有集合进行训练，也不会对多集合查询的任何部分执行重新排名。

请参阅[多集合查询 API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-multi-collections){: new_window} 以获取更多信息。

可以使用 `environments/{environment_id}/notices` API 方法来查看相同环境中跨多个集合的通知。
-  使用此方法时，必须指定 `collection_ids` 参数。`collection_ids` 是环境中要查询的集合的逗号分隔列表。
-  查询多个集合时，支持 `passages`。

请参阅[多集合通知 API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#collections-notices){: new_window} 以获取更多信息。

可以使用 `environments/{environment_id}/fields` API 方法来查看相同环境中跨多个集合可用的字段。请参阅[多集合字段查询 API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#multi-list-fields){: new_window} 以获取更多信息。

## 查询扩展
{: #query-expansion}

通过使用 {{site.data.keyword.discoveryshort}} API 来上传查询扩展术语列表，可以将查询范围扩展到完全匹配之外 - 例如，您可以将对“car”的查询扩展为包含“automobile”和“motor vehicle”。查询扩展术语通常是同义词、反义词或常见术语的典型拼写错误。

可以定义两种类型的扩展：
- **双向** - 每个 `expanded_term` 都将扩展为包含所有扩展的术语。例如，对 `car` 的查询将扩展到 `car OR automobile OR (motor AND vehicle)`。
- **单向** - 查询中的 `input_terms` 将替换为 `expanded_terms`。例如，对 `ibm` 的查询可扩展到 `international business machines` 和 `big blue`。`input_terms` 不用作生成的查询的一部分。在先前的 `ibm` 示例中，查询 `IBM` 将转换为 `international business machines` 或 `big blue`，而不包含原始术语。

以下文件可用作构建查询扩展列表时的起点：
<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/expansions.json" download>expansions.json <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标" class="style-scope doc-content"></a>。可以修改此文件以创建定制查询扩展列表。

双向示例：
```JSON
 {
   "expansions": [
     {
       "expanded_terms": [
         "car",
         "automobile",
         "motor vehicle"
       ]
     }
   ]
 }
```
{: codeblock}

单向示例：
```JSON
 {
   "expansions": [
     {
      "input_terms": [
        "ibm"
       ],
      "expanded_terms": [
        "ibm",
        "international business machines",
        "big blue"
       ]
     }
   ]
 }
```
{: codeblock}

有关查询扩展的说明：

- 查询扩展仅可用于专用集合。可用 `expansions` 数组的数量（双向数组和单向数组的总数）和术语数（`input_terms` 加上 `expanded_terms` 的总数）因套餐而有所不同。请参阅 [Discovery 价格套餐](/docs/services/discovery/pricing-details.html)以获取详细信息。**注：**对于所有查询术语（`input_terms` 和 `expanded_terms`），每个计为一个术语。以下示例包含 `expansions` 数组中的 2 个对象以及 8 个术语字符串。

```JSON
 {
   "expansions": [
     {
      "input_terms": [
         "ibm"
       ],
      "expanded_terms": [
         "ibm",
         "international business machines",
         "big blue"
       ]
     },
     {
      "input_terms": [
         "banana"
       ],
      "expanded_terms": [
         "banana",
         "plantain",
         "fruit"
       ]
     }
   ]
 }
```
{: codeblock}

- 对于每个集合，只能上传一个查询扩展列表；如果上传了第二个扩展列表，那么此列表将替换第一个扩展列表。
- 所有 `input_terms` 和 `expanded_terms` 都应该为小写。小写术语将扩展到大写。
- 查询扩展列表必须以 JSON 格式编写。
- 要禁用查询扩展，请删除查询扩展列表。
- 目前无法使用 {{site.data.keyword.discoveryshort}} 工具来上传或删除查询扩展列表；必须使用 {{site.data.keyword.discoveryshort}} API 来执行此操作。
- 查询扩展是对`查询`和`多集合查询`方法执行的。不会对知识图查询执行查询扩展。
- 每组扩展都与一个集合相关联。在[多个集合](/docs/services/discovery/using.html#multiple-collections)中进行查询时，将分别扩展每个集合。
- 查询扩展在查询时应用，而不是在建立索引期间应用，因此可以更新查询扩展列表，而无需重新摄入文档。
- 不要在将文档摄入到集合期间上传或删除查询扩展列表。这可能会导致索引在该短时间内不可用。

请参阅[查询扩展 API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-expansion){: new_window}，以了解用于上传和删除查询扩展文件的 API 命令。

## 定制记号化字典

记号化用于将文本分解成单元，此单元称为记号。标准记号化字典会应用于集合，但您可以通过上传定制记号化字典来提高域或语言的搜索准确性。定制字典将覆盖标准字典。您可以使用 {{site.data.keyword.discoveryshort}} API 来上传字典。 

请参阅[记号化 API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#create-tokenization-dictionary){: new_window}，以了解用于上传和删除记号化文件的 API 命令。 

**注：**此功能当前仅可用于日语集合。 

在以下示例中，**text** 是遇到时将进行记号化的短语，**tokens** 是 **text** 将拆分成的字。**Readings** 列出了由不同字符集表示的记号的版本，**part_of_speech** 是记号表示的词性。

对于此定制字典，如果搜索文本 `ネコ`，那么搜索结果将包括含有 `すしネコ` 的文本，以及仅含有 `ネコ` 的文本。

```
{ "tokenization_rules":
  [
    {
      "text":"すしネコ",
      "tokens":[
        "すし",
        "ネコ"
      ],
      "readings":[
        "寿司",
        "ネコ"
      ],
      "part_of_speech":"カスタム名詞"
    },
    ...
  ]
}
```

您还可以创建包含单个记号的规则。在以下示例中，`ibm発見` 将记号化为单个记号，因此不会分解为更小的单元。

```
{ "tokenization_rules":
  [
    {
      "text":"ibm発見",
      "tokens":[  
      "ibm発見"
      ],
      "readings":[  
      "ibm発見"
      ],
      "part_of_speech":"カスタム名 詞"
    },
    ...
  ]
}
```

- 记号化可在索引和查询时执行。 
- 标准记号化字典用于所有集合。如果集合已使用该字典建立了索引，那么在上传定制记号化字典之后，必须重新摄入该集合中的文档。
- 对于每个集合，只能上传一个记号化字典；如果上传了第二个记号化字典，那么此字典将替换第一个记号化字典。如果该集合已包含文档，那么必须重新摄入这些文档，才能应用新的定制记号化字典。
- 定制记号化字典必须以 JSON 格式编写，示例文件名：`custom_tokenization_dictionary.json`。
- 要禁用记号化，请删除记号化字典并重新摄入文档。
- 目前无法使用 {{site.data.keyword.discoveryshort}} 工具来上传或删除记号化字典；必须使用 {{site.data.keyword.discoveryshort}} API 来执行此操作。
- 记号化是对`查询`和`多集合查询`方法执行的。不会对知识图查询执行记号化。
- 每个记号化字典都与一个集合相关联。在[多个集合](/docs/services/discovery/using.html#multiple-collections)中进行查询时，将分别对每个集合进行记号化。
- 不要在将文档摄入到集合期间上传或删除记号化字典。 

## 文档相似度
{: #doc-similarity}

文档相似度查询将查找类似于当前所查看文档的其他文档，例如，呼叫中心操作员可能在查看产品手册，并使用文档相似度来查找具有类似特征的其他文档。您可以通过 `similar.document_ids` 来查询类似文档，并可以选择通过指定其他 `similar.fields` 来优化相似度。

文档相似度的确定方法是从原始文档中抽取 25 个最相关的术语，然后搜索具有类似相关术语的文档。

通过 `similar.document_ids` 执行的示例查询（如果指定多个 `similar.document_ids`，逗号后面不应有空格）：

`curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&similar.document_ids=4107b6f1-5d3f-4bea-bbcf-fb05bbf960b1,6057k6d1-7d7k-6aeh-cfbb-kj98ssf786c2"`

添加了 `similar.fields` 的示例查询：

`curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&similar.document_ids=4107b6f1-5d3f-4bea-bbcf-fb05bbf960b1&similar.fields=title&return=title&count=100"`

请参阅[文档相似度 API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query-using-get){: new_window} 和[查询参数](/docs/services/discovery/query-parameters.html#similar)，以获取更多信息。
