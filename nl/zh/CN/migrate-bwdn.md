---

copyright:
  years: 2015, 2018
lastupdated: "2018-01-16"

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

# 从 Watson Discovery News Original 迁移
{: #migrate-bwdn}

新版本的 {{site.data.keyword.discoverynewsshort}} 已在 **2017 年 7 月 31 日**推出。原始版本已重命名为 {{site.data.keyword.discoverynewsshort}} Original，并且已于 **2018 年 1 月 15 日**引退不用。如果您尝试访问 {{site.data.keyword.discoverynewsshort}} Original，那么会收到消息：`410 GONE`。
{: shortdesc}

要从 {{site.data.keyword.discoverynewsshort}} Original 迁移到新版本，您需要执行多项更改，包括更新为 {{site.data.keyword.discoverynewsshort}} Original 创建的所有查询。

  **注：**{{site.data.keyword.discoverynewsshort}} Original 仅在 **2017 年 7 月 31 日之前创建**的 {{site.data.keyword.discoveryshort}} 实例中可用，并且已于 **2018 年 1 月 15 日**引退不用。

请参阅 [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html) 以获取此集合的描述。

有关查询 {{site.data.keyword.discoverynewsshort}} Original 的描述和信息，请参阅 [Watson Discovery News Original](/docs/services/discovery/discovery-auxiliary.html#watson-discovery-news-original)。

## 服务比较

|{{site.data.keyword.discoverynewsshort}} Original         | {{site.data.keyword.discoverynewsshort}}           |
|----------------------------------------|---------------------------------|
|**{{site.data.keyword.discoverynewsshort}} Original** 已使用以下 Alchemy Language 扩充项进行预扩充：“关键字抽取”、“实体抽取”、“概念标记”、“关系抽取”、“观点分析”和“分类法分类”。此外，还添加了以下其他元数据：搜寻日期、发布日期、URL 排名、主机排名和锚点文本。|**{{site.data.keyword.discoverynewsshort}}** 已使用以下 {{site.data.keyword.nlushort}} (NLU) 扩充项进行预扩充：“关键字抽取”、“实体抽取”、“语义角色抽取”、“观点分析”、“关系”和“类别分类”。此外，还添加了以下其他元数据：搜寻日期和发布日期。要了解有关 NLU 扩充项的更多信息，请参阅[添加扩充项](/docs/services/discovery/building.html#adding-enrichments)。|
|**{{site.data.keyword.discoverynewsshort}} Original** 可通过对服务实例唯一的环境进行访问。|使用 **{{site.data.keyword.discoverynewsshort}}** 时，所有用户都将查询相同的环境和集合。这意味着需要更改对环境和集合的所有引用。|
|在 **{{site.data.keyword.discoverynewsshort}} Original** 中，通过 API 检索环境时，您会收到集合大小、文档数等信息。|**{{site.data.keyword.discoverynewsshort}}** API 不会返回这些信息。|

**{{site.data.keyword.discoverynewsshort}}** 中提供了以下新字段：

`enriched_text.relations.arguments.text`  
`enriched_text.relations.score`  
`enriched_text.relations.sentence`  
`enriched_text.relations.type`  
`enriched_title.relations`  
`enriched_title.relations.arguments`  
`enriched_title.relations.arguments.entities`<br/>
`enriched_title.relations.arguments.entities.text`  
`enriched_title.relations.arguments.entities.type`  
`enriched_title.relations.arguments.text`  
`enriched_title.relations.score`  
`enriched_title.relations.sentence`  
`enriched_title.relations.type`  
`external_links`  
`extracted_metadata`  
`extracted_metadata.file_type`  
`extracted_metadata.filename`  
`extracted_metadata.sha1`  
`forum_title`  
`main_image_url`

另外还除去了很多字段，例如 `blekko.hostrank`、`duplicate_url`、`domain` 等。请参阅<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/News_migration_v_1.01.xlsx" download>此处 <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标" class="style-scope doc-content"></a> 以获取完整列表。

## 将查询移至新的 Watson Discovery News

要将查询从 {{site.data.keyword.discoverynewsshort}} Original 移至新版本 {{site.data.keyword.discoverynewsshort}}，需要按以下方式修改所有现有查询：  

- 更改查询调用的环境标识。所有 {{site.data.keyword.discoveryshort}} 服务实例上的新闻环境名称均已标准化为：

  `system`  

- 更改查询调用的集合标识。所有 {{site.data.keyword.discoveryshort}} 服务实例上的新闻集合名称均已标准化为：

  `news`

- 修改查询以使用新版本 {{site.data.keyword.discoverynewsshort}} 的新 JSON 路径结构。大多数字段的路径都已更改，添加了多个字段，并且除去了一组所选的低值字段。请参阅字段迁移电子表格以获取完整的详细信息（<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/News_migration_v_1.01.xlsx" download>此处 <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标" class="style-scope doc-content"></a>）。例如，以下查询：

  `discovery/api/v1/environments/ae5790c2-592f-432a-804a-ee16de7154d7/collections/3edcd8f1-e25a-4f44-a069-58332ad17651/query?version=2017-11-07&query=entities.type:"Company"`

  应该更改为：

  `discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.type:"Company"`  

## 查询 Watson Discovery News

可以使用该 API 或某个 {{site.data.keyword.watson}} SDK 来查询 {{site.data.keyword.discoverynewsshort}}。此外，还可以使用查询构建工具以交互方式构造查询。

**要启动 {{site.data.keyword.discoveryshort}} 工具并查询 {{site.data.keyword.discoverynewsshort}}**，请执行以下操作：

1. 在**服务**下，针对 {{site.data.keyword.discoveryshort}}，单击**启动工具**。
1. 单击 {{site.data.keyword.discoverynewsshort}} 磁贴以打开**管理数据**屏幕。
1. 单击**查看数据模式**，然后单击**构建查询**以打开查询构建器。

  {{site.data.keyword.discoverynewsshort}} 中查询的构造方式与为专用数据集合编写的查询相同。请参阅[查询概念](/docs/services/discovery/using.html)和[查询参考](/docs/services/discovery/query-reference.html)。
  {: tip}

**注：**不要指望 {{site.data.keyword.discoverynewsshort}} Original 和 {{site.data.keyword.discoverynewsshort}} 中的类似查询返回完全相同的结果。搜寻时间、源和扩充项全部组合在一起，会返回不同的结果。

## 向应用程序添加 Watson Discovery News 查询

使用以下其中一种方法向应用程序添加查询。所有这些示例均查询的是 `text` 值为 `IBM` 的 `enriched_text.entities` (`enriched_text.entities.text:IBM`)。

在以下所有示例中，将 `{username}` 和 `{password}` 替换为您服务实例的**服务凭证**页面中列出的用户名和密码。

### 使用对 API 的直接调用

```bash
curl -u "{username}":"{password}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

### 使用 Watson Java SDK

```java
Discovery discovery = new Discovery("2017-11-07");  
discovery.setEndPoint("https://gateway.watsonplatform.net/discovery/api/v1");
discovery.setUsernameAndPassword("{username}", "{password}");  
String environmentId = "system";
String collectionId = "news";

QueryRequest.Builder queryBuilder = new QueryRequest.Builder(environmentId, collectionId);  
queryBuilder.query("enriched_text.entities.text:IBM");  
QueryResponse queryResponse = discovery.query(queryBuilder.build()).execute();
```
{: codeblock}

### 使用 Watson Node.js SDK

```javascript
var watson = require('watson-developer-cloud');  

var discovery = new DiscoveryV1({  
  username: '{username}',  
  password: '{password}',  
  version_date: '2017-11-07'  
});  

discovery.query(('system', 'news', 'enriched_text.entities.text:IBM'),  
  function(error, data) {  
    console.log(JSON.stringify(data, null, 2));  
  }
);
```
{: codeblock}

### 使用 Watson Python SDK

```python
import sys  
import os  
import json  
from watson_developer_cloud import DiscoveryV1  

discovery = DiscoveryV1(  
  username="{username}",  
  password="{password}",  
  version="2017-11-07"  
)  

qopts = {'query': 'enriched_text.entities.text:IBM'}  
my_query = discovery.query('system', 'news', qopts)  
print(json.dumps(my_query, indent=2))  
```
{: codeblock}
