---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-08"

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

# 從 AlchemyData News 移轉

新版本的 {{site.data.keyword.discoverynewsfull}} 在 **2017 年 7 月 31 日**初次亮相。如需此集合的說明，請參閱 [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html)。

AlchemyData News 已下架，在 **2018 年 3 月 7 日**已從服務移除。

## 服務比較
{: shortdesc}

從 AlchemyData News 移至 {{site.data.keyword.discoveryshort}} 服務中的 {{site.data.keyword.discoverynewsshort}} 時，下列差異值得注意。

- {{site.data.keyword.discoveryshort}} 僅針對該查詢的新聞查詢收費。所有欄位都可用來隨每一個結果傳回，而不需要額外成本。
- 每一個 {{site.data.keyword.discoveryshort}} 查詢最多可傳回 50 個結果。您可以使用 `offset` 參數，以便將查詢分頁為您需要的任意數目結果。
- {{site.data.keyword.discoveryshort}} 另外支援聚集。如需相關資訊，請參閱 {{site.data.keyword.discoveryshort}} 文件的[聚集](/docs/services/discovery/query-reference.html#aggregations)小節。
- {{site.data.keyword.discoverynewsfull}} 不會使用與 AlchemyData News 相同的方式進行分級。目前沒有用於分級的欄位。
- {{site.data.keyword.discoverynewsshort}} 與 AlchemyData News 之間的查詢結構及傳回的資料結構不同。瞭解 JSON 結構的良好方法是查詢 {{site.data.keyword.discoverynewsshort}} 中的單一結果，並檢查結果。
- {{site.data.keyword.discoverynewsshort}} 不支援 XML 輸出。
- 刪除重複是 {{site.data.keyword.discoverynewsshort}} 中的一項測試版特性。

## 鑑別差異

{{site.data.keyword.discoveryshort}} 服務使用標準 {{site.data.keyword.Bluemix_notm}} `username` 和 `password` 認證來存取查詢。這會取代 AlchemyData News 所使用的現有 API 金鑰方法。所有 {{site.data.keyword.discoveryshort}} 查詢都必須使用 {{site.data.keyword.discoveryshort}} 服務實例所建立的使用者名稱和密碼組合來進行。

您可以在 {{site.data.keyword.Bluemix_notm}} 內檢視服務的**服務認證**標籤，來管理您的服務認證。

## 配置 Discovery 實例

建立 {{site.data.keyword.discoveryshort}} 服務實例的方式與您建立 AlchemyData News 實例的方式相同。

1. 導覽至 [{{site.data.keyword.Bluemix_notm}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window}，登入並從服務型錄中選取 {{site.data.keyword.discoveryshort}}。
1. 選取符合您的需求的適當方案，然後按一下**建立**。

  {{site.data.keyword.discoveryshort}} 服務提供的「精簡」方案每月有 1000 個新聞查詢可用。您可以使用此方案的實例來識別同等的查詢，而不必支付它們的費用。
  {: tip}

1. 按一下**服務認證**標籤，並選取**檢視認證**，以識別此實例的 `url`、`username` 及 `password`。

## 查詢 Watson Discovery News

您可以利用 API 或其中一個 {{site.data.keyword.watson}} SDK 來查詢 {{site.data.keyword.discoverynewsfull}}。此外，您可以使用查詢建置工具，以互動方式建構查詢。

若要啟動 {{site.data.keyword.discoveryshort}} 工具及查詢 {{site.data.keyword.discoverynewsshort}}，請執行下列動作：

1. 在**服務**下，對 {{site.data.keyword.discoveryshort}} 按一下**啟動工具**。
1. 按一下 {{site.data.keyword.discoverynewsshort}} 磚，以開啟**管理資料**畫面。
1. 按一下**檢視資料綱目**，然後按一下**建置查詢**來開啟查詢建置器。

  {{site.data.keyword.discoverynewsfull}} 中查詢的建構方式與針對專用資料集合撰寫的查詢相同。請參閱[查詢概念](/docs/services/discovery/using.html)及[查詢參考資料](/docs/services/discovery/query-reference.html)。
  {: tip}

**附註**：請不要預期 AlchemyData News 及 {{site.data.keyword.discoverynewsfull}} 會針對類似查詢傳回相同的結果。搜索時間、來源及強化全都會結合而傳回不同的結果。

## 將 Watson Discovery News 查詢新增至應用程式

使用下列其中一種方法，可將查詢新增至應用程式。所有這些範例使用 `text` 值 `IBM` 來查詢 `enriched_text.entities` (`enriched_text.entities.text:IBM`)。

在所有下列範例中，將 `{username}` 和 `{password}` 取代為服務實例的**服務認證**頁面中列出的使用者名稱和密碼。

### 對 API 使用直接呼叫

```bash
curl -u "{username}":"{password}"  'https://gateway.watsonplatform.net/discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

### 使用 Java SDK

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
