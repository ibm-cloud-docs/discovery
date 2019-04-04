---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-08"

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

# 从 AlchemyData News 迁移
{: #migrate-adn}

新版本的 {{site.data.keyword.discoverynewsfull}} 已在 **2017 年 7 月 31 日**推出。请参阅 [Watson Discovery News](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) 以获取此集合的描述。

AlchemyData News 已引退，其终止服务日期为 **2018 年 3 月 7 日**。

## 服务比较
{: #service-adn}

从 AlchemyData News 移至 {{site.data.keyword.discoveryshort}} 服务中的 {{site.data.keyword.discoverynewsshort}} 时，应注意以下差异。

- {{site.data.keyword.discoveryshort}} 仅按查询对新闻查询收费。对于每个结果，所有字段均可供返回，无需额外成本。
- 每个 {{site.data.keyword.discoveryshort}} 查询最多可返回 50 个结果。`offset` 参数可用，因此可以根据需要的任意结果数对查询分页。
- 此外，{{site.data.keyword.discoveryshort}} 还支持聚集。请参阅 {{site.data.keyword.discoveryshort}} 文档的[聚集](/docs/services/discovery?topic=discovery-query-reference#aggregations)部分以了解更多信息。
- {{site.data.keyword.discoverynewsfull}} 的排名方式与 AlchemyData News 的不同。目前没有用于排名的字段。
- {{site.data.keyword.discoverynewsshort}} 和 AlchemyData News 的查询结构及返回数据的结构不同。了解 JSON 结构的一个好办法是查询 {{site.data.keyword.discoverynewsshort}} 中的单个结果，然后检查结果。
- {{site.data.keyword.discoverynewsshort}} 不支持 XML 输出。
- 去重是 {{site.data.keyword.discoverynewsshort}} 中的 Beta 功能。

## 认证差异
{: #auth-adn}

{{site.data.keyword.discoveryshort}} 服务使用标准 {{site.data.keyword.Bluemix_notm}} `username` 和 `password` 凭证来访问查询。这将替换 AlchemyData News 使用的现有 API 密钥方法。所有 {{site.data.keyword.discoveryshort}} 查询都必须使用由 {{site.data.keyword.discoveryshort}} 服务实例创建的用户名和密码组合来发起。

可以通过在 {{site.data.keyword.Bluemix_notm}} 中查看服务的**服务凭证**选项卡来管理您的服务凭证。

## 配置 Discovery 实例
{: #config-adn}

{{site.data.keyword.discoveryshort}} 服务实例的创建方式与 AlchemyData News 实例的相同。

1. 导航至 [{{site.data.keyword.Bluemix_notm}} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/catalog/services/discovery){: new_window}，登录并从服务目录中选择 {{site.data.keyword.discoveryshort}}。
1. 根据需要选择相应的套餐，然后单击**创建**。

  {{site.data.keyword.discoveryshort}} 服务提供有轻量套餐，每月支持 1000 个可用新闻查询。可以使用此套餐的实例来识别等效查询，而不必为此付费。
  {: tip}

1. 单击**服务凭证**选项卡，然后选择**查看凭证**以识别此实例的 `url`、`username` 和 `password`。

## 查询 Watson Discovery News
{: #querying-adn}

可以使用该 API 或某个 {{site.data.keyword.watson}} SDK 来查询 {{site.data.keyword.discoverynewsfull}}。此外，还可以使用查询构建工具以交互方式构造查询。

要启动 {{site.data.keyword.discoveryshort}} 工具并查询 {{site.data.keyword.discoverynewsshort}}，请执行以下操作：

1. 在**服务**下，针对 {{site.data.keyword.discoveryshort}}，单击**启动工具**。
1. 单击 {{site.data.keyword.discoverynewsshort}} 磁贴以打开**管理数据**屏幕。
1. 单击**查看数据模式**，然后单击**构建查询**以打开查询构建器。

  {{site.data.keyword.discoverynewsfull}} 中查询的构造方式与为专用数据集合编写的查询相同。请参阅[查询概念](/docs/services/discovery?topic=discovery-query-concepts#query-concepts)和[查询参考](/docs/services/discovery?topic=discovery-query-reference#query-reference)。
  {: tip}

不要指望针对 AlchemyData News 和 {{site.data.keyword.discoverynewsfull}} 中的类似查询返回完全相同的结果。搜寻时间、源和扩充项全部组合在一起，会返回不同的结果。
{: note}

## 向应用程序添加 Watson Discovery News 查询
{: #queries-adn}

使用以下其中一种方法向应用程序添加查询。所有这些示例均查询的是 `text` 值为 `IBM` 的 `enriched_text.entities` (`enriched_text.entities.text:IBM`)。

在以下所有示例中，将 `{username}` 和 `{password}` 替换为您服务实例的**服务凭证**页面中列出的用户名和密码。

### 使用对 API 的直接调用
{: #api-adn}

```bash
curl -u "{username}":"{password}"  'https://gateway.watsonplatform.net/discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

### 使用 Java SDK
{: #javasdk-adn}

```java
Discovery discovery = new Discovery("2017-11-07");
discovery.setEndPoint("https://gateway.watsonplatform.net/discovery/api/v1");
discovery.setUsernameAndPassword("{username}", "{password}");  
String environmentId = "system";
  String collectionId = "news";

QueryRequest.Builder queryBuilder = new QueryRequest.Builder(environmentId,collectionId);  
queryBuilder.query("enriched_text.entities.text:IBM");  
QueryResponse queryResponse =  
discovery.query(queryBuilder.build()).execute();
```
{: codeblock}

### 使用 Watson Node.js SDK
{: #nodesdk-adn}

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
```
{: codeblock}

### 使用 Watson Python SDK
{: #pythonsdk-adn}

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
my_query = discovery.query('{environment_id}', '{collection_id}', qopts)
print(json.dumps(my_query, indent=2))
```
{: codeblock}
