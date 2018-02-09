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

# Watson Discovery News Original からのマイグレーション

{{site.data.keyword.discoverynewsshort}} の新しいバージョンが **2017 年 7 月 31 日**に公開されました。元のバージョンは、{{site.data.keyword.discoverynewsshort}} Original と名前変更され、**2018 年 1 月 15 日**のサービスからの削除によって廃止されました。  
{: shortdesc}

{{site.data.keyword.discoverynewsshort}} Original から新しいバージョンにマイグレーションするには、{{site.data.keyword.discoverynewsshort}} Original 用に作成されたすべての照会の更新を含め、いくつかの変更を行う必要があります。

  **注:** {{site.data.keyword.discoveryshort}} の新規インスタンスを作成した場合は、{{site.data.keyword.discoverynewsshort}} の新しいバージョンにしかアクセスできません。新しい {{site.data.keyword.discoverynewsshort}} と {{site.data.keyword.discoverynewsshort}} Original の両方へのアクセスは、**2017 年 7 月 31 日**より前に作成された {{site.data.keyword.discoveryshort}} のインスタンスでのみ可能です。

このコレクションの説明については、[Watson Discovery News](/docs/services/discovery/watson-discovery-news.html) を参照してください。

{{site.data.keyword.discoverynewsshort}} Original の照会に関する説明と情報については、[Watson Discovery News Original](/docs/services/discovery/discovery-auxiliary.html#watson-discovery-news-original) を参照してください。

## サービスの比較

| {{site.data.keyword.discoverynewsshort}} Original         | {{site.data.keyword.discoverynewsshort}}           |
|----------------------------------------|---------------------------------|
| **{{site.data.keyword.discoverynewsshort}} Original** は、Alchemy Language エンリッチメント (キーワード抽出、エンティティー抽出、概念のタグ付け、関係抽出、センチメント分析、およびタクソノミー分類) によって事前にエンリッチされています。また、クロール日、公開日、URL ランキング、ホスト・ランク、アンカー・テキストのメタデータも追加されます。| **{{site.data.keyword.discoverynewsshort}}** は、{{site.data.keyword.nlushort}} (NLU) エンリッチメント (キーワード抽出、エンティティー抽出、意味役割抽出、センチメント分析、関係、およびカテゴリー分類) によって事前にエンリッチされています。クロール日付および公開日付もメタデータとして追加されます。NLU エンリッチメントの詳細については、[エンリッチメントの追加](/docs/services/discovery/building.html#adding-enrichments)を参照してください。                         |
| **{{site.data.keyword.discoverynewsshort}} Original** は、サービス・インスタンス固有の環境からアクセス可能でした。| **{{site.data.keyword.discoverynewsshort}}** を使用する場合、すべてのユーザーは同じ環境とコレクションを照会します。つまり、ご使用の環境とコレクションのすべての参照を変更する必要があります。|
| **{{site.data.keyword.discoverynewsshort}} Original** では、API を介して環境を取得するときに、コレクション・サイズ、文書数、その他の情報を受け取ります。| **{{site.data.keyword.discoverynewsshort}}** API はこの情報を返しません                          |

**{{site.data.keyword.discoverynewsshort}}** では以下の新規フィールドが使用可能です。

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

多くのフィールド (例えば、`blekko.hostrank`、`duplicate_url`、`domain` など) も削除されました。完全リストについては、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/News_migration_v_1.01.xlsx" download>ここ <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン" class="style-scope doc-content"></a> を参照してください。

## 新しい Watson Discovery News への照会の移動

{{site.data.keyword.discoverynewsshort}} Original から新しい {{site.data.keyword.discoverynewsshort}} に照会を移動するには、以下のようにしてすべての既存の照会を変更する必要があります。  

- 照会が呼び出す環境 ID を変更します。ニュースの環境名は、すべての {{site.data.keyword.discoveryshort}} サービス・インスタンスで以下のように標準化されました。

  `system`  

- 照会が呼び出すコレクション ID を変更します。ニュースのコレクション名は、すべての {{site.data.keyword.discoveryshort}} サービス・インスタンスで以下のように標準化されました。

  `news`

- 新しい {{site.data.keyword.discoverynewsshort}} 用の新しい JSON パス構造を使用するように照会を変更します。ほとんどのフィールドがパスを変更し、複数のフィールドが追加され、価値の低い、選択されたフィールドが削除されました。詳細については、フィールド・マイグレーション・スプレッドシート (<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/News_migration_v_1.01.xlsx" download>ここ <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン" class="style-scope doc-content"></a>) を参照してください。例えば、以下の照会をご覧ください。

  `discovery/api/v1/environments/ae5790c2-592f-432a-804a-ee16de7154d7/collections/3edcd8f1-e25a-4f44-a069-58332ad17651/query?version=2017-11-07&query=entities.type:"Company"`

  この照会は、次のように変更する必要があります。

  `discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.type:"Company"`  

## Watson Discovery News の照会

API、またはいずれかの {{site.data.keyword.watson}} SDK を使用して {{site.data.keyword.discoverynewsshort}} を照会することができます。さらに、照会作成ツールを使用して、対話式に照会を作成することもできます。

**{{site.data.keyword.discoveryshort}} ツールを起動し、{{site.data.keyword.discoverynewsshort}} を照会するには、以下のようにします。**

1. **「サービス」**の下で、{{site.data.keyword.discoveryshort}} の**「ツールの起動 (Launch Tool)」**をクリックします。
1. {{site.data.keyword.discoverynewsshort}} タイルをクリックして、**「データの管理 (Manage data)」**画面を開きます。
1. **「データ・スキーマの表示 (View data schema)」**をクリックし、次に**「照会の作成 (Build queries)」**をクリックして照会ビルダーを開きます。

  {{site.data.keyword.discoverynewsshort}} の照会は、プライベート・データ・コレクション用に作成された照会と同じ方法で構造化されます。[照会の概念](/docs/services/discovery/using.html)および[照会リファレンス](/docs/services/discovery/query-reference.html)を参照してください。
  {: tip}

**注:** {{site.data.keyword.discoverynewsshort}} Original と {{site.data.keyword.discoverynewsshort}} で、同様の照会についてまったく同じ結果が返されることを期待しないでください。クロール時間、ソース、およびエンリッチメントのすべてが組み合わされて、異なる結果が返されます。

## アプリケーションへの Watson Discovery News 照会の追加

照会をアプリケーションに追加するには、以下のいずれかの方式を使用します。これらの例はすべて、`IBM` の `text` 値で `enriched_text.entities` を照会します (`enriched_text.entities.text:IBM`)。

以下のすべての例で、`{username}` と `{password}` は、ご自分のサービス・インスタンスの**「サービス資格情報」**ページにリストされている username と password に置き換えてください。

### API への直接呼び出しを使用

```bash
curl -u "{username}":"{password}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

### Watson Java SDK を使用

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
  }
);
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
my_query = discovery.query('system', 'news', qopts)  
print(json.dumps(my_query, indent=2))  
```
{: codeblock}
