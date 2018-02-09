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


# チュートリアル: Retrieve and Rank からのマイグレーション

{{site.data.keyword.retrieveandrankshort}} から {{site.data.keyword.discoveryfull}} サービスへのマイグレーション。Cranfield 入門チュートリアルの続き。

## 概説
{: #overview}
このチュートリアルでは、サンプル・データを使用して {{site.data.keyword.discoveryfull}} サービスの作成とトレーニングのプロセスについてご案内します。このチュートリアルでは、[{{site.data.keyword.retrieveandrankshort}} 入門チュートリアル](/docs/services/retrieve-and-rank/getting-started.html)で使用されたのと同じデータ・セットを使用しますが、同じ方法を使用して、独自のデータを使用するサービス・インスタンスを作成できます。

{{site.data.keyword.retrieveandrankshort}} から {{site.data.keyword.discoveryshort}} にデータをマイグレーションするユーザーのプロセスは、以下の 2 つの主なステップで構成されています。

1. コレクション・データをマイグレーションする。
2. トレーニング・データをマイグレーションする。

トレーニングしたコレクション・データをマイグレーションするときに**最も**重要なことは、_文書 ID を同一に保つ_ ことです。この理由は、トレーニング・データはそれらの ID を使用してグラウンド・トゥルースを参照するため、{{site.data.keyword.retrieveandrankshort}} から {{site.data.keyword.discoveryshort}} への移動の際にそれらの ID が変更されると、ランキングが完全にオフになる (またはトレーニングが開始さえされない可能性がある) からです。{{site.data.keyword.discoveryshort}} では、API アップロード・プロセスで文書 ID を指定できるため、この問題は本資料のガイドラインに従うことによって回避できます。{{site.data.keyword.retrieveandrankshort}} トレーニング・データは、通常、`csv` ファイルに保管されます。このチュートリアルでは、この `csv` ファイルを使用して、サンプル・トレーニング・データを {{site.data.keyword.discoveryshort}} にアップロードします。{{site.data.keyword.retrieveandrankshort}} ツールからエクスポートされたトレーニング・データのマイグレーションについては、[サービスからのトレーニング・データのマイグレーション](/docs/services/discovery/migrate-dcs-rr.html#extract-train)を参照してください。

このチュートリアルでは、{{site.data.keyword.retrieveandrankshort}} は、[{{site.data.keyword.retrieveandrankshort}} 入門チュートリアル](/docs/services/retrieve-and-rank/getting-started.html)と同様にセットアップされたものと想定し、[ここ](/docs/services/discovery/migrate-dcs-rr.html#source)に記載されているソース・パスからのマイグレーションを使用しています。その他のマイグレーション・オプションについては、[Watson Discovery サービスへのマイグレーション・パスの評価](/docs/services/discovery/migrate-dcs-rr.html#evaluate)を参照してください。

このチュートリアルを実行するには、以下が必要です。

-  **cURL**。ご使用のオペレーティング・システム用の cURL のバージョン は、[haxx.se ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://curl.haxx.se/){: new_window} からインストールできます。Secure Sockets Layer (SSL) プロトコルがサポートされているバージョンをインストールをする必要があります。インストールされたバイナリー・ファイルを必ず PATH 環境変数に含めてください。
-  サンプル Cranfield データ。このチュートリアルでは、{{site.data.keyword.retrieveandrankshort}} 入門チュートリアルのサンプル・コレクション・データ ([cranfield json data ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-data.json){: new_window} を使用しています。
-  **サンプル・データのグラウンド・トゥルース**。このチュートリアルでは、{{site.data.keyword.retrieveandrankshort}} 入門チュートリアルのサンプル Cranfield グラウンド・トゥルース ([cranfield ground truth csv![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-gt.csv){: new_window}) を使用しています。
-  **Python バージョン 2**。Python がインストール済みかどうかを確認するには、コマンド・プロンプトに `python --version` と入力し、バージョン番号が 2 で始まっていることを確認してください。Python をインストールする必要がある場合は、[Downloading Python ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://wiki.python.org/moin/BeginnersGuide/Download){: new_window} を参照してください。
-  データのアップロード・スクリプト: [Discovery document uploader ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-upload.py){: new_window}
-  トレーニング・データのアップロード・スクリプト: [Discovery training uploader ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-train.py){: new_window}

このチュートリアルを開始する前に、以下の前提条件が必要です。

-  このチュートリアルでは、{{site.data.keyword.discoveryshort}} インスタンスが既に作成済みであると想定しています。{{site.data.keyword.discoveryshort}} インスタンスの作成方法の指示が必要な場合は、[次のチュートリアル](/docs/services/discovery/getting-started.html)を参照してください。

-  このチュートリアルでは、ユーザーがサービス資格情報を持っていると想定しています。
   -  {{site.data.keyword.Bluemix_notm}} の Watson {{site.data.keyword.discoveryshort}} サービスを開始したら、**「サービス資格情報」**をクリックします。
   -  「アクション」の下の**「資格情報の表示」**をクリックします。
   -  `username` と `password` の値をコピーし、`url` の値が以下の例の値に一致していることを確認します。一致しない場合は、それも置き換えてください。

## Discovery への Cranfield データの追加

1.  環境を作成します。

    ```bash
    curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{ "name": "my_environment", "description": "My environment" }' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    返された JSON にリストされている `environment-id` をコピーします。

1. コレクションを作成します。

    ```bash
    curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{ "name": "test_collection", "description": "My test collection", "configuration_id": "{configuration_id}", "language_code": "en" }' "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07"
    ```
    {: pre}

    返された JSON にリストされている `collection-id` をコピーします。

1.  検索対象の文書を追加します。
    1.  [cranfield-data.json ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-data.json){: new_window} ファイルをまだダウンロードしていない場合は、ダウンロードします。これは、{{site.data.keyword.retrieveandrankshort}} で使用されている文書のソースです。Cranfield コレクション文書は、JSON フォーマットです。これは、{{site.data.keyword.retrieveandrankshort}} が受け入れ、Watson {{site.data.keyword.discoveryshort}} でも適切に機能するフォーマットです。
        **注:** {{site.data.keyword.discoveryshort}} では、Solr スキーマのアップロードは必要ありません。この理由は、{{site.data.keyword.discoveryshort}} が、JSON 構造から自動的にスキーマを推測するからです。
    1.  データのアップロード・スクリプトを[ここ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-upload.py){: new_window} からダウンロードします。このスクリプトは、Cranfield json を {{site.data.keyword.discoveryshort}} にアップロードします。
        このスクリプトは JSON ファイルを読み取り、{{site.data.keyword.discoveryshort}} のデフォルト構成を使用して個々の JSON 文書を {{site.data.keyword.discoveryshort}} サービスに送信します。
        **注:** {{site.data.keyword.discoveryshort}} のデフォルト構成は、{{site.data.keyword.retrieveandrankshort}} のデフォルト Solr 構成と同様の設定を提供します。
    1.  以下のコマンドを発行して、`cranfield-data-json` データを `cranfield_collection` コレクションにアップロードします。`{username}`、`{password}`、`{path_to_file}`、`{environment_id}`、`{collection_id}` は、ご自身の情報に置き換えてください。追加オプション (デバッグを示す -d と curl からの詳細出力を示す –v) があることに注意してください。

        ```bash
        python ./disco-upload.py -u {username}:{password} -i {path_to_file}/cranfield-data.json –e {environment_id} -c {collection_id}
        ```
        {: pre}

1.  アップロード・プロセスが完了したら、以下のコマンドを発行してコレクションの詳細を表示することにより、文書がそこにあることを確認できます。

    ```bash
    curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07"
    ```
    {: pre}

    出力は、以下のようなものになります。

    ```json
    {
      "collection_id": "f1360220-ea2d-4271-9d62-89a910b13c37",
      "name": "democollection",
      "description": "this is a demo collection",
      "created": "2015-08-24T18:42:25.324Z",
      "updated": "2015-08-24T18:42:25.324Z",
      "status": "available",
      "configuration_id": "6963be41-2dea-4f79-8f52-127c63c479b0",
      "language": "en",
      "document_counts": {
        "available": 1000,
        "processing": 20,
        "failed": 180
      },
      "disk_usage": {
        "used_bytes": 260
      },
      "training": {
        "total_examples": 0,
        "available": false,
        "processing": false,
        "minimum_queries_added": false,
        "minimum_examples_added": true,
        "sufficient_label_diversity": false,
        "notices": 0,
        "successfully_trained": null,
        "data_updated": null
      }
    }
    ```
    {: codeblock}

`document_counts` セクションを参照して、正常にアップロードされた文書の数を確認します。このサンプル・データ・セットでは、文書の失敗は予期していません。しかし、他のデータ・セットでは、失敗した文書数が表示されることがあります。失敗した文書数がある場合は、通知 API を表示してエラー・メッセージを確認することができます。通知 API コマンドを確認するには、[ここ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-notices){: new_window} のセクションを参照してください。

返された値の `training` セクションは、トレーニングに関する情報を提供します。そのセクションは、トレーニング・データをアップロードした後に確認します。

## Discovery へのトレーニング・データの追加

Watson {{site.data.keyword.discoveryshort}} サービスは、機械学習モデルを使用して文書を再ランク付けします。そのためには、モデルをトレーニングする必要があります。トレーニングは、適切に評価された文書とともに十分な数の照会をロードした後に行われます。十分な差異がある十分な数の例を Watson {{site.data.keyword.discoveryshort}} にロードすることにより、「有効な」文書とは何かを教えます。このステップでは、{{site.data.keyword.retrieveandrankshort}} で使用されている、既存の Cranfield の「グラウンド・トゥルース」を使用して Watson {{site.data.keyword.discoveryshort}} をトレーニングします。

1.  サンプルの [Cranfield ground truth csv ファイル ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-gt.csv){: new_window} をまだダウンロードしていない場合は、{{site.data.keyword.retrieveandrankshort}} チュートリアルからダウンロードします。

   このファイルは、ユーザーが文書について尋ねる可能性のある一連の質問です。このファイルには、質問および関連する回答について、{{site.data.keyword.retrieveandrankshort}} および {{site.data.keyword.discoveryshort}} の関連性トレーニングでランカーをトレーニングするためのサンプル情報が記載されています。

   それぞれの質問について、回答への ID (文書 ID) が少なくとも 1 つあります。各文書 ID には、その回答が質問に対してどのくらい関連しているかを示す数字が含まれています。文書 ID は、前のステップで {{site.data.keyword.discoveryshort}} にアップロードした `cranfield-data.json` ファイル内の回答を指します。

1.  トレーニング・データのアップロード・スクリプトをダウンロードします。このスクリプトを使用して、トレーニング・データを {{site.data.keyword.discoveryshort}} にアップロードします。このスクリプトは、`csv` ファイルを JSON 照会と例のセットに変換し、[トレーニング・データ API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#training-data){: new_window} を使用してそれらを {{site.data.keyword.discoveryshort}} サービスに送信します。
    **注:** {{site.data.keyword.discoveryshort}} は、サービス内でトレーニング・データを管理します。つまり、新しい例とトレーニング照会を生成するとき、それらは、維持する必要がある別個の CSV ファイルの一部としてではなく、{{site.data.keyword.discoveryshort}} 自体に保管することができます。
1.  トレーニングのアップロード・スクリプトを実行して、トレーニング・データを {{site.data.keyword.discoveryshort}} にアップロードします。`{username}`、`{password}`、`{path_to_file}`、`{environment_id}`、`{collection_id}` は、ご自身の情報に置き換えてください。追加オプション (debug を示す `-d` と curl からの詳細出力を示す `–v`) があることに注意してください。

    ```bash
    python ./disco-train.py -u {username}:{password} -i {path_to_file}/cranfield-gt.csv –e {environment_id} -c {collection_id}
    ```
    {: pre}

1.  データがロードされたら、前のセクションで示されたコレクション詳細コマンドを使用して、トレーニングの状況を確認することができます。{{site.data.keyword.discoveryshort}} は、1 時間に 1 回、新しいデータがあるかどうかを確認し、あった場合は、そのデータの処理を開始し、それを機械学習モデルに変換します。モデルのトレーニング中、training セクションの状態が `"processing": false` から `"processing": true` に変化するのを確認できます。モデルのトレーニングが完了すると、training セクションの状態は `"available": false` から `"available": true` に変わります。また、`"successfully_trained"` 値の日付の変更も確認できます。エラーがある場合は、前のセクションで述べたように、**通知 API** を表示して確認できます。

## 文書の検索 (Search for documents)
{: search}

{{site.data.keyword.discoveryshort}} サービスは、トレーニングされたモデルがある場合、自動的にそれを使用して検索結果を再ランク付けします。[API 呼び出し![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection){: new_window} が、`query` ではなく、`natural_language_query` を使用して行われると、使用可能なモデルがあるかどうかを確認するためのチェックが行われます。モデルが使用可能な場合、{{site.data.keyword.discoveryshort}} はそのモデルを使用して結果の再ランク付けを行います。まずランク付けされていない文書で検索を行い、次に、ランキング・モデルを使用して検索を行います。

1.  cURL コマンドを使用して、コレクション内の文書を検索することができます。照会 API 呼び出しを使用して照会を実行し、ランク付けされていない結果を表示します。`{username}`、`{password}`、`{environment_id}`、`{collection_id}` は、ご自身の値に置き換えてください。返される結果は、ランク付けされていない結果となり、{{site.data.keyword.discoveryshort}} のデフォルトのランキング式を使用します。トレーニング・データの `csv` ファイルを開き、最初の列の値を照会パラメーターにコピーすることにより、他の照会を試行できます。

    ```bash
    curl -u "{username}":"{password}""https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query=what is the basic mechanism of the transonic aileron buzz"
    ```
    {: pre}

1.  次に、`natural_language_query` パラメーターを設定して、モデルを使用した検索を実行します。それを実行する前に、前のセクションで説明した、トレーニングされたモデルがあることを確認します。コンソールに以下のコードを貼り付けます。`{username}`、`{password}`、`{environment_id}`、`{collection_id}` は、ご自身の値に置き換えてください。

    ```bash
    curl -u "{username}":"{password}""https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&natural_language_query=what is the basic mechanism of the transonic aileron buzz"
    ```
    {: pre}

    このコマンドは、前にトレーニングしたモデルを使用して再ランク付けされた結果を返します。この検索の結果、および前に試行した他のいくつかの検索の結果を比較してください。{{site.data.keyword.retrieveandrankshort}} で表示されるものと比べて、結果にいくつかの相違点があることを確認できる可能性があります。この理由は、検索に使用されたいくつかの手法が、経験を単純化して、結果を向上させるように変更されたためです。ただし、全体的な結果の品質は同様です。

再ランク付けされた検索結果を評価したら、トレーニング・データを追加のトレーニング照会および例とともにアップロードするステップを繰り返し、検索結果を表示することによって、{{site.data.keyword.discoveryshort}} でそれらを詳細化できます。また、最初のステップで説明したように、新しい文書を追加して検索の適用範囲を広げることもできます。{{site.data.keyword.retrieveandrankshort}} と同様に、トレーニングによる結果の改善は反復プロセスです。
