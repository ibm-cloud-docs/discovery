---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-14"

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

# 関連性トレーニングのヒント
{: #relevancy-tips}

 コレクションのトレーニングに関する一般的質問に対する回答と、一般的なエラー・メッセージおよび警告メッセージの説明を示します。自然言語照会の関連性の改善について詳しくは、[ツールを使用した結果関連性の改善](/docs/services/discovery/train-tooling.html)および [API を使用した結果関連性の改善](/docs/services/discovery/train.html)を参照してください。
{: shortdesc}

## トレーニングについて

コレクションのトレーニングに関する一般的質問に対する回答は次のとおりです。

### システムがトレーニング済みであることを確認する方法は?

システムがトレーニング済みであることを検証するには、[List collection details ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/?curl#list-collection-details){: new_window} API コマンドを使用します。  

```bash
curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07"
```
{: pre}

応答の例:

```json
{
  "training": {
    "total_examples": 54,
    "available": true,
    "processing": false,
    "minimum_queries_added": true,
    "minimum_examples_added": true,
    "sufficient_label_diversity": false,
    "notices": 13,
    "successfully_trained": "2017-02-08T14:18:22.786Z",
    "data_updated": "2017-02-10T14:18:22.786Z"
    }
}
```

トレーニングの要件を満たすには、以下のすべてが `true` でなければなりません。
- `minimum_queries_added`
- `minimum_examples_added`
- `sufficient_label_diversity`   

応答内の項目の意味は次のとおりです。
- `successfully_trained` は、トレーニングが最後に正常に完了した時刻です。
- `available: true` は、トレーニングが発生したこと、および、使用可能なモデルがあることを示します。
- `processing: true` は、トレーニングが進行中であることを示します。
-  `data_updated` 日付が `successfully_trained` 日付より後の場合、最新のデータ・アップロード以降にトレーニングされた新しいモデルはありません。  

### エラーと警告をどのようにチェックすればいいですか?

[通知照会 API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-notices){: new_window} を使用して、エラーおよび警告を確認できます。  

```bash
curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/notices?version=2017-11-07"
```
{: pre}

その他の API 操作は『[その他のトレーニング・データ照会操作の実行](/docs/services/discovery/train.html#training-data-operations)』にリストされています。

### トレーニングの後に自然言語照会結果に含まれる `confidence` スコアをどのように解釈すればよいですか?

トレーニングされたコレクションは、自然言語照会の結果に `confidence` スコアを入れて返すようになります。この `confidence` 数値は、トレーニングされたモデルに比べて、結果がどのくらい関連しているのかに基づいて計算されます。`confidence` スコアは `score` と同じでは**ありません**。詳しくは、『[信頼度スコア](/docs/services/discovery/train-tooling.html#confidence)』を参照してください。  

## エラーと警告の解釈

一般的なエラー・メッセージおよび警告メッセージの説明は次のとおりです。

### 警告: `Invalid training data found: The document was not returned in the top 100 search results for the given query, and will not be used for training` (無効なトレーニング・データが見つかりました。文書は照会の上位 100 の検索結果では返されなかったため、トレーニングには使用されません)

この警告の原因は、トレーニング・データ内の `document_id` が、コレクションに対して実行された検索内の `document_id` と一致していないことです。照会を検査して、評価しようとしている文書の `document_id` がその照会の上位 100 の結果に入って返されることを確認する必要があります。そのような結果にならない場合、次の 2 つのことを調べてください。  

- この文書が上位 100 では返されない場合、高品質結果の良い例ではないと考えられます。この文書が選ばれた理由を再検討してください。  

- この文書がまったく返されない場合、なぜ返されないのかを検討し、照会のどこかの部分に一致するテキストが文書中にあるかどうかを確認してください。  

**注:** この警告は、1 つ以上の不良照会がある可能性を示しており、トレーニングが行われないことを示しているのではありません。  

### エラー: `Invalid training data found: Syntax error when parsing query` (無効なトレーニング・データが見つかりました。照会の構文解析で構文エラー)

- これは、実際の照会構文に問題があることを意味します。照会が結果を返すことを検証して、構文エラーが発生しないようにしてください。これが発生する可能性があるのは、自然言語照会にフィルターを追加した場合のみです。

### エラー: `Invalid training data found: The query string provided exceeds the maximum length, please provide a shorter one` (無効なトレーニング・データが見つかりました。指定された照会ストリングが最大長を超えています。もっと短いものを指定してください)

- 照会ストリングの最大長は `X` です。この特定の照会を短くする必要があります。これを回避する方法の 1 つは、照会にフィルターを含めることです。  

### エラー: `This collection cannot be trained: your plan does not support training on this many top-level text fields.` (このコレクションをトレーニングできません。ご使用のプランでは、これだけ多くの最上位テキスト・フィールドでのトレーニングはサポートされていません) 

- このエラーは、`ライト`・プランでのみ発生します。トレーニング可能な最上位テキスト・フィールドの最大数は `X` です。最上位フィールドとは、別のフィールドの下にネストされていないフィールドのことです。トレーニングは最上位フィールドでのみ行われ、トレーニング処理で使用できるフィールド数には制限があります。  

### エラー: `Training data quality standards not met: You will need additional training queries with labeled examples. (To be considered for training, each example must appear in the top 100 search results for its query.)` (トレーニング・データ品質基準が満たされていません。ラベル付きの例を含む追加トレーニング照会が必要です (トレーニングが考慮されるためには、各例がその照会の上位 100 の検索結果に入っている必要があります))

- これは、トレーニングを成功させるために、より多くのトレーニング・データを追加する必要があることを意味します。少なくとも 49 個の固有のトレーニング照会が最低限必要であり、それぞれが少なくとも 1 つの評価済み文書を必要とします。最小は最適と等価ではありません。コレクションのサイズやその他の要因のために、最小限を満たすために必要なトレーニング例の数が増えることがあります。  

### エラー: `Training data quality standards not met: Insufficient number of unique training queries. Expected at least n, but found m.` (トレーニング・データ品質標準が満たされていません。固有トレーニング照会の数が不十分です。少なくとも n が予期されていましたが、見つかったのは m です) 

- 最小のトレーニング要件を満たすためには、少なくとも 49 個の固有のトレーニング照会が最低限必要であり、それぞれが少なくとも 1 つの評価済み文書を必要とします。それを超える数があり、それでもこのエラー・メッセージが出される場合、他にエラーがないか通知を調べる必要があります。  

### エラー: `Training data quality standards not met: No documents found with non-zero relevance labels.` (トレーニング・データ品質標準が満たされていません。ゼロ以外の関連性ラベルの付いた文書が見つかりませんでした) 

- トレーニング・データは、どの文書が高い値なのかを指定するラベル付きデータが十分にあることを必要とします。これは、いくつかの文書をゼロ以外の値で評価する必要があることを意味します。Discovery ツールを使用している場合、いくつかの文書を「関連性あり (Relevant)」(`10`) と評価する必要があります。 API を使用している場合、いくつかの文書に `1` 以上のラベルを付ける必要があります。   

### エラー: `Training data quality standards not met: Training examples have no relevance label variety for X queries.` (トレーニング・データ品質標準が満たされていません。X 照会でトレーニング例の信頼性ラベルが多様ではありません)

- トレーニングの要件の 1 つは、十分に多様なラベル付けがなされていることです。これは、システムを適切にトレーニングさせたい場合は、関連性一致が最高である文書だけでなく、関連性が「良好」な文書も追加する必要があることを意味します。言い換えると、スケールが 0 から 4 の場合、文書が 4 と評価されるのに加えて、2 および 3 と評価されるのに役立ちます。(Discovery ツールを使用している場合、文書は「関連性あり (Relevant)」(`10`) または「関連性なし (Not relevant)」(`0`)) のいずれかに評価されます。少なくとも質問のうち 25% で、ラベルがいくらか多様である必要です。   
