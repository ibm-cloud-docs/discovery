---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-06"

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

# API を使用した結果関連性の改善

{{site.data.keyword.discoveryshort}} サービスをトレーニングして、特定の組織またはサブジェクト・エリアの照会結果の関連性を改善することができます。 {{site.data.keyword.discoveryshort}} インスタンスに*トレーニング・データ* を提供すると、本サービスは Watson の機械学習技法を使用して、コンテンツおよび質問に含まれるシグナルを検出します。 次に、本サービスは照会結果を並べ替えて、最も関連性の高い結果を先頭に表示します。 さらにトレーニング・データを追加するにしたがって、サービス・インスタンスが返す結果の順序付けがより正確で洗練されたものになります。
{: shortdesc}

関連性トレーニングはオプションです。照会の結果がニーズを満たしている場合は、それ以上のトレーニングは不要です。 トレーニング用のユース・ケース作成の概要については、ブログ投稿 [How to get the most out of Relevancy Training ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window} を参照してください。

トレーニング API に関する包括的な情報については、[API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・リンク")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window} を参照してください。

{{site.data.keyword.discoveryshort}} をトレーニングするために {{site.data.keyword.discoveryshort}} ツールを使用したい場合は、[ツールを使用した結果関連性の改善](/docs/services/discovery/train-tooling.html)を参照してください。

**注:** 現在のところ、関連性トレーニングは、プライベート・コレクションにおける自然言語照会にのみ適用され、構造化された {{site.data.keyword.discoveryshort}} 照会言語の照会での使用はその対象にはなっていません。  {{site.data.keyword.discoveryshort}} 照会言語について詳しくは、[照会の概念](/docs/services/discovery/using.html)を参照してください。

トレーニングされたコレクションは、自然言語照会の結果で `confidence` スコアを返します。詳しくは、[信頼度スコア](/docs/services/discovery/train-tooling.html#confidence)を参照してください。

トレーニングの最小要件とトレーニングの制限については、[トレーニング・データ要件](/docs/services/discovery/train.html#reqs)を参照してください。

使用状況の追跡や、このデータをアプリケーションの理解と改善に役立てる方法について詳しくは、[使用状況のモニター](/docs/services/discovery/feedback.html)を参照してください。

<!-- A trained Discovery service instance is intended primarily for use with natural language queries, but it works equally well with queries that use structured syntax. -->  <!-- See [Query Concepts](/docs/services/discovery/using.html) and the [Query reference](/docs/services/discovery/query-reference.html) for information about structured queries and natural language queries. -->

Discovery インスタンスのトレーニングに必要なコンポーネントは、次のとおりです。

 - **トレーニング・データ**。 これは、本サービスが照会結果を絞り込むために使用する *照会* および*例* のセットです。
 - **照会**。 トレーニング・データ・セットに適用される自然言語照会。
   次の黒丸で説明されているように、各照会に 1 つ以上の*例* が関連付けられています。
   各照会は、トレーニング・データ・セット内で固有でなければなりません。
 - **例**。 これは、関連付けられた照会の見本 (**良または不良**) として機能する、Discovery コレクション内の索引付けられた文書です。 トレーニング・データ照会に例を追加するときには、指定された照会に適用される際の文書の関連性 (または「良」対「不良」) を示す関連性ラベルを組み込んでください。

   例は、索引付き文書 ID によって識別されます。 説明したように、すべての例には、照会に関与する際に文書の「良」または「不良」を示すラベルが含まれている必要があります。

   オプションで、例は相互参照照会を指定できます。 相互参照照会は、例文書のみを返す必要があり、固有 Watson Discovery 文書 ID とは無関係でなければなりません。 相互参照照会は現在は自動的には使用されませんが、取り込みイベント中に新規 ID が 文書に割り当てられた場合にトレーニング・データを修理するために使用されることがあります。

## トレーニング・データ要件
{: #reqs}

Discovery サービスから返される回答の関連性を効果的に向上させるためには、トレーニング・データが以下の**最小**品質基準を満たしている必要があります。 **最小**は**最適**を意味しないことに注意してください。 本サービスは、トレーニング・データを定期的に検査してこれらの要件が満たされているかどうかを判別し、変更内容に基づいてそれ自体を自動的に更新します。

- コレクションのトレーニング・データ・セットは、少なくとも 49 個の固有のトレーニング照会 (つまり、照会と例のセット) を含んでいる必要があります。 コレクションのサイズと複雑さによっては、セット中のトレーニング照会の数が 49 を超えないと、Watson がコレクションに関連性トレーニングを適用できないことがあります。 Watson は、トレーニングのためにより多くの照会が必要な場合、フィードバックを提供します。
- API を使用して関連性スコアを割り当てる場合: 各トレーニング照会の関連性スコアは、負でない整数でなければなりません。例えば、`0` で*関連性なし* を、`1` で*いくらか関連性あり* を、`2` で*高い関連性あり* を表します。ただし、最大の柔軟性を確保するため、本サービスでは、さまざまなスコアリング体系を試している上級ユーザー向けに、`0` から `100` までの範囲の負でない整数が許容されます。 使用する範囲に関わらず、トレーニング照会のセット中の最大の整数が、最大の関連性を表します。
- ツールを使用して関連性の評価を割り当てる場合: {{site.data.keyword.discoveryshort}} ツールは、関連性スコア `0` を使用して*関連性なし* を表し、`10` で*関連性あり* を表します。使用可能な評価 `Relevant` および `Not relevant` の両方を結果に適用する必要があります。 `Relevant` 文書のみを評価すると、必要なデータが提供されません。  {{site.data.keyword.discoveryshort}} ツールと API の両方を使用して文書のスコア付けを行うことを計画しているか、または、API から始めてツールに移行することを計画している場合は、この `0` および `10` の関連性スコアを使用してください。
- トレーニング照会には、対象範囲が広い Discovery サービスの最初の検索で取り出されることができるように、照会と望ましい回答との間で重なる用語がいくつか含まれている必要があります。

**注:** Watson は、トレーニング・データを、パターンを学習するため、および汎用化するために使用し、個々のトレーニング照会を記憶するために使用するのではありません。 したがって、このサービスでは、同じトレーニング照会に対して常に同じ関連性結果が再現されるとは限りません。

トレーニングは、以下の**最大**要件を超えることはできません。
  - 環境ごとに、トレーニングされたコレクションが 24 個を超えることはできません。
  - 単一環境内では、トレーニング照会の数は 10,000 に制限され、照会ごとのサンプル数は最大 100 です。 

## トレーニング・データ・セットへの照会の追加

コレクションのトレーニング・データのセットに照会を追加するには、`POST /v1/environments/{environment_id}/collections/{collection_id}/training_data` メソッドを使用します。 照会は、以下の形式の JSON オブジェクトとして指定されます。

```json
{
  "query_id": "string",
  "natural_language_query": "string",
  "filter": "string",
  "examples": [
    {
      "document_id": "string",
      "cross_reference": "string",
      "relevance": 0
    }
  ]
}
```
{: codeblock}

このオブジェクト内の値は次のとおりです。

- `query_id`: 照会の固有 ID。 このフィールドを指定しないと、サービスによって ID が自動的に生成されます。
- `natural_language_query`: トレーニング・セットに適用される Discovery 自然言語照会。<!-- The `natural_language_query` parameter is preferred. -->
- `filter`: 照会のフィルター (オプション)。『[照会リファレンス](/docs/services/discovery/query-reference.html#parameter-descriptions)』に説明があります。

    **注:** トレーニング・データ照会にフィルターを含める場合、トレーニングされたコレクションで自然言語照会を使用するときには、必ず同じフィルターを使用してください。 フィルタリングされたデータでコレクションをトレーニングするが、コレクションを照会するときに同じタイプのフィルターを使用しない場合、結果は予測不能になる可能性があります。

- `examples`: 以下の値を含む配列。

   - `document_id`: トレーニング・セットに適用される文書の固有 ID。 これは前述の*例* です。
   - `cross_reference`: オプション・ラベル。これは、通常、参照される文書中の、文書を「ピン留め」する 1 つのフィールドと、文書の ID が変更されたとき (例えば、新しく取り込まれた文書に同じ ID が割り当てられる場合など) に使われるそのフィールドの情報からなります。 `cross-reference` に値を指定することで、文書間にリンクが生成されるわけでは**ありません**。そうではなく、文書が名前変更または上書きされたときに、文書の関連情報をこのサービスが確実に保持されるようにします。
   - `relevance`: 照会とトレーニング・データとの相対的な関連性を示す、`0` から `100` までの範囲の整数。 値が大きいほど、関連性が高くなります。 値 `0` は照会への関連性がないことを示し、値 `100` は照会への絶対的な関連性を示します。

   **注:** `relevance` パラメーターの範囲は、最大の柔軟性を確保にするために `0` から `100` になっていますが、例のスコアリングを単純化するためにもっと小さい範囲を使用できます。 `0` から `4` までを標準範囲にしたり、範囲全体を使用するものの 20 ずつの増分 (`0`、`20`、`40`、`60`、`80`、および `100`) のみを使用するようにしたりできます。 {{site.data.keyword.discoveryshort}} ツールは、関連性スコア `0` を使用して*関連性なし* を表し、`10` で*関連性あり* を表します。 {{site.data.keyword.discoveryshort}} ツールと API の両方を使用して文書のスコア付けを行うことを計画しているか、または、API から始めてツールに移行することを計画している場合は、この `0` および `10` の関連性スコアを使用してください。

以下のオブジェクトは、値が設定されたトレーニング・データ照会を示しています。

```json
{
  "natural_language_query": "why is the sky blue",
  "filter": "text:meteorology",
  "examples": [
    {
      "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
      "relevance": 0
    },
    {
      "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
      "relevance": 1
    },
    {
      "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
      "cross_reference": "my_id_field:1463",
      "relevance": 4
    }
  ]
}
```
{: codeblock}

以下のコマンド例は、上のトレーニング・データ照会を、`a56dd9b4-040b-4ea3-a736-c1e7a467e191` という名前の環境内の `99040100-fe6a-4782-a4f5-28f9eee30850` という名前のコレクションに追加します。

```bash
curl -X POST -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" -H "Content-Type: application/json" -d
'{
  "natural_language_query": "why is the sky blue",
  "filter": "text:meteorology",
  "examples": [
    {
    "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
    "relevance": 0
    },
    {
      "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
      "relevance": 1
    },
    {
      "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
      "cross_reference": "my_id_field:1463",
      "relevance": 4
    }
  ]
}'
"https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
```
{: pre}

## トレーニング・データ照会への例の追加

トレーニング・データ照会を作成した後、引き続き例を追加して、トレーニングの正確度を向上させることができます。 既存のトレーニング・データ照会に例を追加するには、`POST /v1/environments/{environment_id}/collections/{collection_id}/training_data/{query_id}` を使用します。

トレーニング・データ照会に例を追加するには、以下のステップを実行します。

1. [コレクションのトレーニング・データ照会のリスト表示 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#get-training-data){: new_window} によって、新しい例を追加する先のトレーニング・データ照会の照会 ID を取得します。

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
   ```
   {: pre}

   返される JSON は、以下のフォーマットになります。

   ```json
    {
      "query_id": "484baad4-d440-44b7-a0dd-70bb2ac77baa",
      "natural_language_query": "why is the sky blue",
      "filter": "text:meteorology",
      "examples": [
        {
          "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
          "relevance": 0
        },
        {
          "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
          "relevance": 1
        },
        {
          "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
          "cross_reference": "my_id_field:1463",
          "relevance": 4
        }
      ]
    }
   ```
   {: codeblock}

1. 新規トレーニング・データ照会の作成時に例を定義するために使用するのと同じ構文を使用して、新しい例を追加します。 以下のコマンド例は、相互参照を含んでいません。

   ```bash
    curl -u -X POST -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" -H "Content-Type: application/json" -d
    '{
      "document_id": "46b52fdc-3a72-4700-9849-ac217532b373",
      "relevance": 3
    }' "https://gateway.watsonplatform.net/discovery/api/v1/environments//a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data/484baad4-d440-44b7-a0dd-70bb2ac77baa?version=2016-12-01"
   ```
   {: pre}

1. もう一度[コレクションのトレーニング・データ照会のリスト表示 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#get-training-data){: new_window} を行うことによって、新しい例がトレーニング・データ照会に追加されたことを検証します。

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
   ```
   {: pre}

   返される JSON は、以下のフォーマットになります。

   ```json
    {
      "query_id": "484baad4-d440-44b7-a0dd-70bb2ac77baa",
      "natural_language_query": "why is the sky blue",
      "filter": "text:meteorology",
      "examples": [
        {
          "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
          "relevance": 0
        },
        {
          "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
          "relevance": 1
        },
        {
          "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
          "cross_reference": "my_id_field:1463",
          "relevance": 4
        },
        {
          "document_id": "46b52fdc-3a72-4700-9849-ac217532b373",
          "relevance": 3
        }
      ]
    }
   ```
   {: codeblock}

1. [コレクション詳細のリスト表示 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#list-collection-details){: new_window} メソッドを使用し、`"training"`/`"available"` フィールドの値を調べて、トレーニングの状況を確認します。 トレーニング要求を満たすための十分な照会および例を追加した場合、このフィールドの値として `true` が返され、本サービスは自動的にこのトレーニング・データの使用を開始します。

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850?version=2016-12-01"
   ```
   {: pre}

   返される JSON は、以下のフォーマットになります。

   ```json
    {
      "collection_id": "99040100-fe6a-4782-a4f5-28f9eee30850",
      "name": "democollection",
      "configuration_id": "def9bd08-8472-470f-ab5a-e377f77e9300",
      "language": "en_us",
      "status": "available",
      "description": "this is a demo collection",
      "created": "2015-08-24T18:42:25.324Z",
      "updated": "2015-08-24T18:42:25.324Z",
      "document_counts": {
        "available": 1000,
        "processing": 20,
        "failed": 180
      },
      "disk_usage": {
        "used_bytes": 895111
      },
      "training_status": {
        "data_updated": "2017-02-10T14:18:22.786Z",
        "total_examples": 54,
        "sufficient_label_diversity": false,
        "processing": false,
        "minimum_examples_added": true,
        "successfully_trained": "2017-02-08T14:18:22.786Z",
        "available": true,
        "notices": 13,
        "minimum_queries_added": true
      }
    }
   ```
   {: codeblock}

1. 前のステップで以下のフィールドがすべて `true` と返される場合、いくつかのサンプル照会を実行して、本サービスがより関連性の高い結果を返すかどうかを確認します。

   - `minimum_queries_added`
   - `minimum_examples_added`
   - `sufficient_label_diversity`

   結果の関連性が改善されない場合は、要件を満たす結果が得られるまで、さらにトレーニング照会を追加してください。

トレーニングに関する追加ガイダンスについては、『[関連性トレーニングのヒント](/docs/services/discovery/train-tips.html#relevancy-tips)』を参照してください。   

## その他のトレーニング・データ照会操作の実行
{: #training-data-operations}

[API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window} に記述されているように、他の API メソッドを使用して、トレーニング・データ照会の管理および保守を行うことができます。

 - [ for a collection ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#get-training-data){: new_window}
 - [Delete all training data for a collection ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-all-training-data){: new_window}
 - [Display the contents of a specified training-data query  ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#show-td-query){: new_window}
 - [Delete a training-data query from the collection ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1#delete-td-query-example){: new_window}
 - [Change a training-data query example's relevance label or cross reference ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#update-example){: new_window}
 - [Delete an example document from a training-data query  ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-example){: new_window}

 **エラーのモニター:** トレーニング・データのエラーは通知に含まれます。通知は、[通知照会 API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-notices){: new_window} (`GET /v1/environments/{environment_id}/collections/{collection_id}/notices`) を使用してモニターできます。
