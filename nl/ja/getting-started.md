---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}

# API 入門
{: #gs-api}

この短いチュートリアルでは、{{site.data.keyword.discoveryshort}} API の概要を説明し、プライベート・データ・コレクションを作成して検索するプロセスをご案内します。
{: shortdesc}

{{site.data.keyword.discoveryshort}} ツールで作業する場合は、[始めに](/docs/services/discovery/getting-started-tool.html)を参照してください。
{: tip}

## 始めに
{: #before-you-begin}

- サービスのインスタンスを作成します。
    1.  {{site.data.keyword.Bluemix_notm}} カタログの[{{site.data.keyword.discoveryshort}} ページ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.{DomainName}/catalog/services/discovery){: new_window}にアクセスします。
    1.  無料の {{site.data.keyword.Bluemix_notm}} アカウントに登録するか、ログインします。
    1.  **「作成」**をクリックします。
- 資格情報をコピーし、以下のようにしてサービス・インスタンスに認証します。
    1. [{{site.data.keyword.Bluemix_notm}} ダッシュボードから](https://console.{DomainName}/dashboard/apps)、{{site.data.keyword.discoveryshort}} サービス・インスタンスをクリックして、{{site.data.keyword.discoveryshort}} サービス・ダッシュボード・ページに移動します。
    1.  **「管理」**ページで、 **「表示」**をクリックして資格情報を表示します。
    1.  `apikey` 値と `url` 値をコピーします。

    場合によっては、基本認証を提供して認証します。資格情報に `username` と `password` がある場合は、このチュートリアルの例で `" apikey":"{apikey_value}"` の代わりにこれらの値を使用してください。
{: tip}

## ステップ 1: 環境の作成
{: #create-an-environment}

`curl` アプリケーションがインストールされている Cygwin などの bash シェルまたは同等の環境で、`POST /v1/environments` メソッドを使用して環境を作成します。環境とは、すべての文書を箱に入れて保管する倉庫のようなものです。

このチュートリアルでは、API 鍵を使用して認証します。実動使用の場合は、必ず API 鍵[ベスト・プラクティス](/docs/services/watson/apikey-bp.html#api-bp)を確認してください。
{: tip}

1.  次のコマンドを発行して、`my-first-environment` という名前の環境を作成します。`{apikey_value}` を先でコピーした API 鍵に置き換えます。

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    この API は、環境 ID、環境の状況、および環境で使用されているストレージの量などの情報を返します。

1.  `active` の状況が表示されるまで、環境の状況を定期的に確認します。
    - `GET /v1/environments/{environment_id}` メソッドへの呼び出しを発行して、環境の状況を取得します。 `{apikey_value}` および `{environment_id}` はご自身の情報に置き換えてください。

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}?version=2017-11-07"
    ```
    {: pre}

    状況が `active` になっていないと、コレクションを作成できません。

## ステップ 2: コレクションの作成
{: #create-a-collection}

これで環境の準備が整ったので、コレクションを作成することができます。 コレクションとは、環境内で資料を保管する箱のようなものです。

1.  まず、デフォルト構成の ID が必要です。 デフォルトの `configuration_id` を見つけるには、`GET /v1/environments/{environment_id}/configurations` メソッドを使用します。 `{apikey_value}` および `{environment_id}` はご自身の情報に置き換えてください。

    ```bash
      curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07
    ```
    {: pre}
1.  `POST /v1/environments/{environment_id}/collections` メソッドを使用して、**my-first-collection** と呼ばれるコレクションを作成します。 `{apikey_value}`、`{environment_id}`、および `{configuration_id}` はご自身の情報に置き換えてください。

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{configuration_id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07
    ```
    {: pre}

    この API は、コレクション ID、コレクションの状況、およびコレクションで使用されているストレージ量などの情報を返します。
1.  `active` の状況が表示されるまで、コレクションの状況を定期的に確認します。
    - `GET /v1/environments/{environment_id}/collections/{collection_id}` メソッドへの呼び出しを発行して、コレクションの状況を取得します。  ここでも、`{apikey_value}`、`{environment_id}`、および `{configuration_id}` は、ご自身の情報に置き換えてください。

    ```bash
    curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07
    ```
    {: pre}

## ステップ 3: サンプル文書のダウンロード
{: #download-sample-documents}

次のサンプル文書をダウンロードします: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン" class="style-scope doc-content"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン" class="style-scope doc-content"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン" class="style-scope doc-content"></a>、および <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン" class="style-scope doc-content"></a>。

**注:** 一部のブラウザーでは、ローカルに保存するのではなく、前のリンクが新しいウィンドウで開きます。これが発生した場合は、ブラウザーの`「ファイル」`メニューで `「名前を付けて保存」`を選択して、ファイルのコピーを保存します。

## ステップ 4: 文書のアップロード
{: #upload-the-documents}

1.  次に、サンプル文書をコレクションに追加します。 この例では、**test-doc1.html** という文書をコレクションにアップロードします。 `{apikey_value}`、`{environment_id}`、および `{configuration_id}` はご自身の情報に置き換えてください。 サンプル文書のロケーションは、保存されている `test-doc1.html` ファイルを指すように変更します。
    - 以下のように、`POST /v1/environments/{environment_id}/collections/{collection_id}/documents` メソッドを使用します。

        ```bash
        curl -X POST -u "apikey":"{apikey_value}" -F "file=@test-doc1.html" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2017-11-07
        ```
        {: pre}

    あるいは、以下のように、[API reference ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window} にリストされているいずれかの SDK を使用します。
    - Java:

      ```java
      Discovery discovery = new Discovery("2017-11-07");
      discovery.setEndPoint("https://gateway.watsonplatform.net/discovery/api/v1");
      IamOptions options = new IamOptions.Builder()
        .apiKey("{apikey_value}")
        .build();
      discovery.setIamCredentials(options);
      String environmentId = "{environment_id}";
      String collectionId = "{collection_id}";
      String documentJson = "{\"field\":\"value\"}";
      InputStream documentStream = new ByteArrayInputStream(documentJson.getBytes());

      CreateDocumentRequest.Builder builder = new CreateDocumentRequest.Builder(environmentId, collectionId);
      builder.inputStream(documentStream, HttpMediaType.APPLICATION_JSON);
      CreateDocumentResponse createResponse = discovery.createDocument(builder.build()).execute();
      ```
      {: codeblock}

    - Python:

      ```python
      import sys
      import os
      import json
      from watson_developer_cloud import DiscoveryV1

      discovery = DiscoveryV1(
        version='2017-11-07',
        api_key='{apikey_value}'
      )

      with open((os.path.join(os.getcwd(), '{path_element}', '{filename}' as fileinfo:
        add_doc = discovery.add_document('{environment_id}', '{collection_id}', file_info=fileinfo)
      print(json.dumps(add_doc, indent=2))
      ```
      {: codeblock}

    - Node.js:

      ```javascript
      var DiscoveryV1 = require('watson-developer-cloud/discovery/v1');
      var fs = require('fs');

      var discovery = new DiscoveryV1({
        version_date: '2017-11-07',
        iam_apikey: '{apikey_value}',
      });

      var file = fs.readFileSync('{/path/to/file}');

      discovery.addDocument({ environment_id: '{environment_id}', collection_id: '{collection_id}', file: file },
      function(error, data) {
        console.log(JSON.stringify(data, null, 2));
        }
      );
      ```
      {: codeblock}

1.  他の 3 つのサンプル・ファイルでこのプロセスを繰り返します。

## ステップ 5: コレクションの照会
{: #query-your-collection}

最後に、`GET /v1/environments/{environment_id}/collections/{collection_id}/query` メソッドを使用して、文書のコレクションを検索します。

以下の例は、**IBM** と呼ばれるすべてのエンティティーを返します。 `{apikey_value}`、`{environment_id}`、および `{configuration_id}` はご自身の情報に置き換えてください。

```bash
curl -u "apikey":"{apikey_value}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

## 次のステップ
{: #next-steps}

作成した環境およびコレクション内の文書が正常に照会されました。次に、さらに文書およびエンリッチメントを追加し、変換設定をカスタマイズして、コレクションのカスタマイズを開始できます。

- [API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window} で、API に関する説明を読みます。
- サービスの[構成](/docs/services/discovery/building.html)
- [IAMによる認証](/docs/services/watson/getting-started-iam.html)についての理解
