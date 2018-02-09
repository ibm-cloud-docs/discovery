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

# AlchemyData News からのマイグレーション

{{site.data.keyword.discoverynewsfull}} の新しいバージョンが **2017 年 7 月 31 日**に公開されました。このコレクションの説明については、[Watson Discovery News](/docs/services/discovery/watson-discovery-news.html) を参照してください。

AlchemyData News は、**2018 年 3 月 7 日**のサービスからの削除によって廃止されます。

## サービスの比較
{: shortdesc}

AlchemyData News から {{site.data.keyword.discoveryshort}} サービスの {{site.data.keyword.discoverynewsshort}} に移動する際は、以下の相違点に注意してください。

- {{site.data.keyword.discoveryshort}} は、照会のみによるニュース照会に対して料金を請求します。各結果ですべてのフィールドは、追加コストなしで返すことができます。
- 各 {{site.data.keyword.discoveryshort}} 照会は、最大 50 個の結果を返すことができます。`offset` パラメーターが使用可能なため、必要な結果数に関係なく照会をページ送りできます。
- {{site.data.keyword.discoveryshort}} は、追加で集約をサポートします。詳しくは、{{site.data.keyword.discoveryshort}} 資料の『[集約](/docs/services/discovery/query-reference.html#aggregations)』セクションを参照してください。
- {{site.data.keyword.discoverynewsfull}} は、AlchemyData News と同じ方法でランク付けを行いません。現在、ランキング用のフィールドはありません。
- 照会の構造と、返されるデータの構造は、{{site.data.keyword.discoverynewsshort}} と AlchemyData News で異なります。JSON 構造を理解するための良い方法は、{{site.data.keyword.discoverynewsshort}} で単一結果を照会し、その結果を検査するというものです。
- {{site.data.keyword.discoverynewsshort}} では XML 出力はサポートされません。
- 重複排除は、{{site.data.keyword.discoverynewsshort}} のベータ版フィーチャーです。

## 認証の相違点

{{site.data.keyword.discoveryshort}} サービスは、標準の {{site.data.keyword.Bluemix_notm}} の `username` と `password` の資格情報を使用して照会にアクセスします。この方式は、AlchemyData News で使用されていた、既存の API 鍵方式に代わるものです。すべての {{site.data.keyword.discoveryshort}} 照会は、{{site.data.keyword.discoveryshort}} サービス・インスタンスによって作成された username と password の組み合わせを使用して行う必要があります。

サービス資格情報は、{{site.data.keyword.Bluemix_notm}} 内のサービスの**「サービス資格情報」**タブを表示することによって管理できます。

## Discovery インスタンスの構成

{{site.data.keyword.discoveryshort}} サービス・インスタンスは、AlchemyData News インスタンスと同じ方法で作成されます。

1. [{{site.data.keyword.Bluemix_notm}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window} にナビゲートし、ログインし、サービス・カタログから「{{site.data.keyword.discoveryshort}}」を選択します。
1. 自分のニーズに適切なプランを選択し、**「作成」**をクリックします。

  {{site.data.keyword.discoveryshort}} サービスには、1 カ月当たり 1,000 個のニュース照会が使用可能なライト・プランが用意されています。このプランのインスタンスを使用すれば、無料で同等の照会を識別できます。
  {: tip}

1. **「サービス資格情報」**タブをクリックし、**「資格情報の表示」**を選択して、このインスタンスの `url`、`username`、および `password` を識別します。

## Watson Discovery News の照会

API、またはいずれかの {{site.data.keyword.watson}} SDK を使用して、{{site.data.keyword.discoverynewsfull}} を照会することができます。さらに、照会作成ツールを使用して、対話式に照会を作成することもできます。

{{site.data.keyword.discoveryshort}} ツールを起動し、{{site.data.keyword.discoverynewsshort}} を照会するには、以下のようにします。

1. **「サービス」**の下で、{{site.data.keyword.discoveryshort}} の**「ツールの起動 (Launch Tool)」**をクリックします。
1. {{site.data.keyword.discoverynewsshort}} タイルをクリックして、**「データの管理 (Manage data)」**画面を開きます。
1. **「データ・スキーマの表示 (View data schema)」**をクリックし、次に**「照会の作成 (Build queries)」**をクリックして照会ビルダーを開きます。

  {{site.data.keyword.discoverynewsfull}} の照会は、プライベート・データ・コレクション用に作成された照会と同じ方法で構造化されます。[照会の概念](/docs/services/discovery/using.html)および[照会リファレンス](/docs/services/discovery/query-reference.html)を参照してください。
  {: tip}

**注**: AlchemyData News と {{site.data.keyword.discoverynewsfull}} で、同様の照会について、まったく同じ結果が返されることを期待しないでください。クロール時間、ソース、およびエンリッチメントのすべてが組み合わされて、異なる結果が返されます。

## アプリケーションへの Watson Discovery News 照会の追加

照会をアプリケーションに追加するには、以下のいずれかの方式を使用します。これらの例はすべて、`IBM` の `text` 値で `enriched_text.entities` を照会します (`enriched_text.entities.text:IBM`)。

以下のすべての例で、`{username}` と `{password}` は、ご自分のサービス・インスタンスの**「サービス資格情報」**ページにリストされている username と password に置き換えてください。

### API への直接呼び出しを使用

```bash
curl -u "{username}":"{password}"  'https://gateway.watsonplatform.net/discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

### Java SDK を使用

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

### Watson Node.js SDK を使用

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

### Watson Python SDK を使用

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
