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

# 查询概念

{{site.data.keyword.discoveryfull}} 服务提供了强大的内容搜索功能。通过 {{site.data.keyword.discoveryshort}} 服务上传并扩充内容后，随即可以构建查询，然后将 {{site.data.keyword.discoveryshort}} 集成到您自己的项目中，或者使用 {{site.data.keyword.watson}} Explorer Application Builder 来创建定制应用程序。
{: shortdesc}

  您编写的查询将因集合而有所不同，因为所有集合都包含唯一的内容。
  {: tip}

创建查询或过滤器时，{{site.data.keyword.discoveryshort}} 会查看每个结果并尝试与已定义的路径相匹配。如果匹配，即会将其添加到结果集。创建查询时，可以根据需要使其尽量模糊或尽量具体。查询越具体，结果越有针对性。

您还可以选择开启段落检索。段落是查询返回的完整文档中的简短相关摘录。这些目标段落是从集合中文档的 `text` 字段中抽取的。缺省情况下，一个查询最多可以返回 10 个段落，每个段落大约 400 个字符。从单个结果中最多抽取三个段落。`passages` 参数仅可用于专用集合；此参数在 {{site.data.keyword.discoverynewsshort}} 集合中不可用。请参阅[段落](/docs/services/discovery/query-parameters.html#passages)，以获取有关如何识别段落的更多信息。

  您可以使用 {{site.data.keyword.discoveryshort}} 工具或 API 来编写自然语言查询（例如“IBM Watson partnerships”）。
  {: tip}

已培训的集合将在自然语言查询的结果中返回 `confidence` 分数。请参阅[置信度分数](/docs/services/discovery/train-tooling.html#confidence)以获取详细信息。

{{site.data.keyword.discoveryfull}} Visual Insights 是一个试验性功能，可以用于直观地浏览根据 {{site.data.keyword.discoveryshort}} 对语义元素、关系和概念等的理解而识别到的连接。有关更多信息，请参阅 [{{site.data.keyword.discoveryfull}} Visual Insights](/docs/services/discovery/visual-insights.html)。

{{site.data.keyword.discoveryfull}} Knowledge Graph 是一个 Beta 功能，提供用于跨文档查询实体和关系的新端点。这包括基于上下文的搜索和相关性排名。请参阅 [{{site.data.keyword.discoveryfull}} Knowledge Graph](/docs/services/discovery/building-kg.html) 以获取更多信息。

有关编写查询的更多信息，请参阅：
- [查询入门教程](/docs/services/discovery/getting-started-query.html)
- [查询参考](/docs/services/discovery/query-reference.html)（包括 {{site.data.keyword.discoveryshort}} Query Language 中可用的参数、运算符和聚集的列表）

## Discovery 数据模式
{: #discovery-schema}

首先来了解 {{site.data.keyword.discoveryshort}} JSON。要了解如何使用 {{site.data.keyword.discoveryshort}} Query Language 来构建查询，您需要熟悉在 {{site.data.keyword.discoveryshort}} 扩充集合中的文档后生成的 JSON。熟悉文档的数据模式后，在 {{site.data.keyword.discoveryshort}} Query Language 中编写查询会更容易。有三种方法可执行此操作。

  1. 在 {{site.data.keyword.discoveryshort}} 工具中，打开**管理数据**屏幕，然后选择包含 {{site.data.keyword.IBM_notm}} Press Releases 的集合。单击**查看数据模式**按钮。**查看数据模式**屏幕通过两种方式显示已变换文档中的字段和值：按文档（**文档视图**）或按字段（**集合视图**）。**文档视图**中将最多显示 50 个文档。**集合视图**将显示整个集合中的字段。

    在**集合视图**中的 `enriched_text` 下，可以检查通过 **Default Configuration** 文件应用的扩充项。单击 `categories`、`concepts`、`entities` 和 `sentiment` 可查看集合是如何通过 Watson 见解扩充的。

  1. 运行“空”查询来查看 JSON。在**查看数据模式**屏幕上，单击**构建查询**按钮，然后单击**运行查询**。结果会显示在右侧的两个选项卡下：**摘要**（查询结果的概述）和 **JSON**。首先打开 **JSON** 选项卡。

     -  这四个文档前面各自有一个 `id` 号。
     -  向下滚动到 `enriched_text` 字段。检查每个扩充项，以了解可以查询的 JSON 字段。

        ![缺省配置字段](images/JSON.png)

     -  **entities** - 首先找到 `text` 字段，然后检查其他扩充项信息。
     -  **sentiment** - 首先找到 `label` 字段，然后检查其他扩充项信息。
     -  **concepts** - 首先找到 `text` 字段，然后检查其他扩充项信息。
     -  **categories** - 首先找到 `document` 字段，然后检查其他扩充项信息。

     检查了第一个文档中的见解后，可以根据需要查看其他三个文档。

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

{{site.data.keyword.discoverynewsshort}} 是已使用认知见解进行预扩充的公共数据集，并且随附于 {{site.data.keyword.discoveryshort}} 中。请参阅 [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html#watson-discovery-news) 以获取有关此集合的更多信息。

您可以使用自然语言查询（例如“IBM Watson partnerships”）或 {{site.data.keyword.discoveryshort}} Query Language 来查询此集合。要了解有关自然语言查询的更多信息，请参阅[自然语言查询](/docs/services/discovery/query-parameters.html#nlq)。

不能调整 {{site.data.keyword.discoverynewsshort}} 配置，也不能培训 {{site.data.keyword.discoverynewsshort}} 集合或向其中添加文档。请在[此处 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://discovery-news-demo.mybluemix.net/){: new_window} 查看可以使用 {{site.data.keyword.discoverynewsshort}} 构建的内容的演示。

Watson {{site.data.keyword.discoverynewsshort}} 英语语言版本通过 {{site.data.keyword.discoveryshort}} 工具和 API 使用。韩语 (`collection_id`: `news-ko`) 和西班牙语 (`collection_id`: `news-es`) 语言版本仅可通过 API 使用。有关通过 API 查询集合的信息，请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection){: new_window}。Watson {{site.data.keyword.discoverynewsshort}} 英语语言版本的 `collection_id` 为 `news-en`。原先，`collection_id` 为 `news` - 如果您一直在使用先前的 `collection_id`，那么它将继续有效，但是，对于新项目，您可能希望切换到新的 `collection_id`。

**注：**针对 Watson Discovery News 查询返回的最大结果数为 `50`。使用其他查询和 `offset` 参数可返回 `50` 个以上的结果。

如果使用 {{site.data.keyword.discoveryshort}} Query Language，那么可以在 {{site.data.keyword.discoverynewsshort}} 查询中包含相对日期范围，例如：`crawl_date>=now-1month`。有效的日期时间间隔值为 `second/seconds`、`minute/minutes`、`hour/hours`、`day/days`、`week/weeks`、`month/months` 和 `year/years`。`now` 不受 `time_zone` 参数的影响；`UTC` 时区为缺省值。

新闻文章可能会联合到多家新闻媒体，{{site.data.keyword.discoverynewsfull}} 会选取其中每家新闻媒体，因而会生成重复的文章。这意味着对 {{site.data.keyword.discoverynewsfull}} 的查询可能会在查询结果中返回多个完全相同或几乎完全相同的文章。您可以使用去重功能来管理此问题。要了解有关此 Beta 功能的更多信息，请参阅[从查询结果中排除重复文档](/docs/services/discovery/query-parameters.html#deduplication)。

## 查询多个集合
{: #multiple-collections}

如果环境中有多个集合，那么您可能要查看跨这些集合的结果。`environments` 级别的查询方法（`query`、`fields` 和 `notices`）允许您查询多个指定的集合。目前，{{site.data.keyword.discoveryshort}} 工具中未提供跨集合查询。

可以使用 `environments/{environment_id}/query` API 方法在相同环境中查询多个集合。跨多个集合查询时，请考虑以下各项。
-  使用此方法时，必须指定 `collection_ids` 参数。`collection_ids` 是环境中要查询的集合的逗号分隔列表。
-  查询多个集合时，不支持 `passages` 和所有子参数。
-  新字段 `collection_id` 会作为每个结果对象的一部分返回。此字段指定在其中找到结果的集合。
-  {{site.data.keyword.discoverynewsshort}} 是 `system` 环境的一部分，因此不能包含在多集合查询中。
-  即便已对查询中的所有集合进行培训，也不会对多集合查询的任何部分执行重新排名。

请参阅[多集合查询 API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-multi-collections){: new_window} 以获取更多信息。

可以使用 `environments/{environment_id}/notices` API 方法来查看相同环境中跨多个集合的通知。
-  使用此方法时，必须指定 `collection_ids` 参数。`collection_ids` 是环境中要查询的集合的逗号分隔列表。
-  查询多个集合时，不支持 `passages` 和所有子参数。

请参阅[多集合通知 API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#collections-notices){: new_window} 以获取更多信息。

可以使用 `environments/{environment_id}/fields` API 方法来查看相同环境中跨多个集合可用的字段。请参阅[多集合字段查询 API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#multi-list-fields){: new_window} 以获取更多信息。
