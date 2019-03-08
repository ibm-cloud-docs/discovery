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

# 從 Watson Discovery News Original 移轉
{: #migrate-bwdn}

新版本的 {{site.data.keyword.discoverynewsshort}} 在 **2017 年 7 月 31 日**初次亮相。原始版本已重新命名為 {{site.data.keyword.discoverynewsshort}} Original，並且在 **2018 年 1 月 15 日**已從服務下架。如果您嘗試存取 {{site.data.keyword.discoverynewsshort}} Origianl，您會收到 `410 GONE` 訊息。
{: shortdesc}

若要從 {{site.data.keyword.discoverynewsshort}} Original 移轉至新版本，您需要進行一些變更，包括更新已對 {{site.data.keyword.discoverynewsshort}} Original 建立的任何查詢。

  **附註：**{{site.data.keyword.discoverynewsshort}} Original 僅適用於 **2017 年 7 月 31 日**之前建立的 {{site.data.keyword.discoveryshort}} 實例，並且在 **2018 年 1 月 15 日**已從服務下架。

如需此集合的說明，請參閱 [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html)。

如需查詢 {{site.data.keyword.discoverynewsshort}} Original 的說明及相關資訊，請參閱 [Watson Discovery News Original](/docs/services/discovery/discovery-auxiliary.html#watson-discovery-news-original)。

## 服務比較

|{{site.data.keyword.discoverynewsshort}} Original         | {{site.data.keyword.discoverynewsshort}}           |
|----------------------------------------|---------------------------------|
| **{{site.data.keyword.discoverynewsshort}} Original** 已使用下列「Alchemy 語言」強化進行預先強化：「關鍵字擷取」、「實體擷取」、「概念標記」、「關係擷取」、「觀感分析」及「分類架構分類」。也新增了下列其他 meta 資料：搜索日期、發佈日期、URL 分級、主機分級及錨點文字。|**{{site.data.keyword.discoverynewsshort}}** 已使用下列 {{site.data.keyword.nlushort}} (NLU) 強化進行預先強化：「關鍵字擷取」、「實體擷取」、「語意角色擷取」、「觀感分析」、「關係」及「種類分類」。也新增了下列其他 meta 資料：搜索日期和發佈日期。若要進一步瞭解 NLU 強化，請參閱[新增強化](/docs/services/discovery/building.html#adding-enrichments)。|
|可透過對服務實例而言是唯一的環境來存取 **{{site.data.keyword.discoverynewsshort}} Original**。|使用 **{{site.data.keyword.discoverynewsshort}}** 時，所有使用者會查詢相同的環境和集合。這表示需要變更環境和集合的所有參照。|
|在 **{{site.data.keyword.discoverynewsshort}} Original** 中，透過 API 擷取環境時，您會收到集合大小、文件數等資訊。|**{{site.data.keyword.discoverynewsshort}}** API 不會傳回此資訊。|

以下是 **{{site.data.keyword.discoverynewsshort}}** 可用的新欄位：

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

已移除了許多欄位，例如 `blaekko.hostrank`、`duplicate_url`、`domain` 等等。如需完整清單，請參閱<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/News_migration_v_1.01.xlsx" download>這裡 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示" title="外部鏈結圖示" class="style-scope doc-content"></a>。

## 將查詢移至新的 Watson Discovery News

若要將查詢從 {{site.data.keyword.discoverynewsshort}} Original 移至新的 {{site.data.keyword.discoverynewsshort}}，您需要以下列方式修改所有現有的查詢：  

- 變更該查詢呼叫的環境 ID。在所有 {{site.data.keyword.discoveryshort}} 服務實例之間，新聞環境名稱已標準化為：

  `system`  

- 變更該查詢呼叫的集合 ID。在所有 {{site.data.keyword.discoveryshort}} 服務實例之間，新聞集合名稱已標準化為：

  `news`

- 修改查詢，以使用新的 {{site.data.keyword.discoverynewsshort}} 的新 JSON 路徑結構。大部分欄位已變更路徑、已新增多個欄位，而且已移除所選取的低值欄位群組。請參閱<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/News_migration_v_1.01.xlsx" download>這裡 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示" title="外部鏈結圖示" class="style-scope doc-content"></a>的欄位移轉試算表，以取得完整資料。例如，下列查詢：

  `discovery/api/v1/environments/ae5790c2-592f-432a-804a-ee16de7154d7/collections/3edcd8f1-e25a-4f44-a069-58332ad17651/query?version=2017-11-07&query=entities.type:"Company"`

  應變更為：

  `discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.type:"Company"`  

## 查詢 Watson Discovery News

您可以利用 API 或其中一個 {{site.data.keyword.watson}} SDK 來查詢 {{site.data.keyword.discoverynewsshort}}。此外，您可以使用查詢建置工具，以互動方式建構查詢。

**若要啟動 {{site.data.keyword.discoveryshort}} 工具及查詢 {{site.data.keyword.discoverynewsshort}}，請執行下列動作：**

1. 在**服務**下，對 {{site.data.keyword.discoveryshort}} 按一下**啟動工具**。
1. 按一下 {{site.data.keyword.discoverynewsshort}} 磚，以開啟**管理資料**畫面。
1. 按一下**檢視資料綱目**，然後按一下**建置查詢**來開啟查詢建置器。

  {{site.data.keyword.discoverynewsshort}} 中查詢的建構方式與針對專用資料集合撰寫的查詢相同。請參閱[查詢概念](/docs/services/discovery/using.html)及[查詢參考資料](/docs/services/discovery/query-reference.html)。
  {: tip}

**附註：**請不要預期 {{site.data.keyword.discoverynewsshort}} Original 和 {{site.data.keyword.discoverynewsshort}} 會針對類似查詢傳回相同的結果。搜索時間、來源及強化全都會結合而傳回不同的結果。

## 將 Watson Discovery News 查詢新增至應用程式

使用下列其中一種方法，可將查詢新增至應用程式。所有這些範例使用 `text` 值 `IBM` 來查詢 `enriched_text.entities` (`enriched_text.entities.text:IBM`)。

在所有下列範例中，將 `{username}` 和 `{password}` 取代為服務實例的**服務認證**頁面中列出的使用者名稱和密碼。

### 對 API 使用直接呼叫

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
