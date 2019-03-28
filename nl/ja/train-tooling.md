---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-11"

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

# ツールを使用した結果関連性の改善
{: #improving-result-relevance-with-the-tooling}

{{site.data.keyword.discoveryfull}} サービスでトレーニングを使用して、自然言語照会の関連性を改善することができます。 {{site.data.keyword.discoveryshort}} ツールまたは {{site.data.keyword.discoveryshort}} API のいずれかを使用して、プライベート・コレクションをトレーニングすることができます。 API を使用したい場合は、[API を使用した照会結果関連性の改善](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api)を参照してください。
{: shortdesc}

関連性トレーニングはオプションです。照会の結果がニーズを満たしている場合は、それ以上のトレーニングは不要です。 トレーニング用のユース・ケース作成の概要については、ブログ投稿 [How to get the most out of Relevancy Training ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window} を参照してください。

Watson をトレーニングするためには、以下を行う必要があります。

  -   ユーザーが入力する照会を代表するような照会例を用意する
  -   各照会の結果のどれが関連していて、どれが関連していないのかを示す評価を用意する

Watson のトレーニング入力が十分になれば、各照会のどの結果が良でどの結果が不良なのかに関して用意した情報が、コレクションについて学習するために使用されるようになります。 Watson は、単に記憶するのではなく、個々の照会に関する具体的な情報から学習し、検出したパターンをすべての新規照会に適用します。 これは、コンテンツと質問の中にあるシグナルを検出する Watson 機械学習手法によって行われます。 トレーニングが適用された後、{{site.data.keyword.discoveryshort}} は照会結果を並べ替えて、最も関連性の高い結果を上位に表示します。 さらに多くのトレーニング・データを追加するにしたがって、{{site.data.keyword.discoveryshort}} による照会結果の順序付けが正確になっていくはずです。

**注:** 現在のところ、関連性トレーニングは、プライベート・コレクションにおける自然言語照会にのみ適用され、構造化された {{site.data.keyword.discoveryshort}} 照会言語の照会での使用はその対象にはなっていません。 {{site.data.keyword.discoveryshort}} 照会言語について詳しくは、[照会の概念](/docs/services/discovery?topic=discovery-query-concepts#query-concepts)を参照してください。

すべてのプライベート・コレクションは、ほとんどの場合、`confidence` スコアを照会結果に含めて返します。詳しくは、[信頼度スコア](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence)を参照してください。

カスタム・ストップワード・リストを追加すると、自然言語照会の結果の関連性を改善できる可能性があります。詳しくは、[ストップワードの定義](/docs/services/discovery?topic=discovery-query-concepts#stopwords)を参照してください。

トレーニングの最小要件とトレーニングの制限については、[トレーニング・データ要件](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#reqs)を参照してください。

使用状況の追跡や、このデータをアプリケーションの理解と改善に役立てる方法について詳しくは、[使用状況のモニター](/docs/services/discovery?topic=discovery-usage#usage)を参照してください。

## 照会の追加および結果の関連性の評価
{: #results}

トレーニングは、自然言語照会、照会結果、それらの結果に適用する評価という 3 つのパーツからなります。

1.  {{site.data.keyword.discoveryshort}} ツールのトレーニング・ページにアクセスする方法は、以下のように 2 とおりあります。
    - 個々のコレクションに対しては、**「照会の作成 (Build queries)」**画面で、右上にある**「結果を改善するために Watson をトレーニングする (Train Watson to improve results)」**をクリックします。 トレーニングを開始するために**「照会の作成 (Build queries)」**画面で照会を入力する必要はありません。 
    - パフォーマンス・ダッシュボードで、 左側にある**「データ・メトリックの表示 (View data metrics)」**アイコンをクリックして、ダッシュボードを開きます。 トレーニングするコレクションを選択するように求められます。
1.  **「Watson のトレーニング (Train Watson)」**画面で、**「自然言語照会の追加 (Add a natural language query)」**をクリックします。例えば「IBM Watson in healthcare」を追加します。 ユーザーが質問すると予想される照会を作成してください。 また、トレーニング照会は、照会と望ましい回答とでいくつかの用語が重なるように作成する必要があります。 これによって、自然言語照会が実行されたときの最初の結果が改善されます。 関連性トレーニングでは自然言語照会のみが使用されます。{{site.data.keyword.discoveryshort}} 照会言語で作成された照会を入力しないでください。
1.  照会の結果を表示するため、その横にある**「結果の評価 (Rate Results)」**ボタンをクリックします。 十分な数の結果がないと思う場合は、照会を書き直すか、または、**「データの管理 (Manage data)」**画面でこのコレクションにさらに文書を追加してみてください。
1.  `Relevant` または `Not relevant` のいずれかとして結果の評価を開始します。 完了したら、**「照会に戻る (Back to queries)」**をクリックします。 {{site.data.keyword.discoveryshort}} ツールでは、`Relevant` はスコア `10` であり、`Not relevant` はスコア `0` です。このコレクションの結果レーティングを API を使用して既に開始し、かつ、異なるスコアリング・スケールを使用した場合、警告が表示され、問題を修正するためのオプションが示されます。
    画面の最上部で、Watson によってトレーニング状況がずっと追跡され、結果を改善するためにできることに関するヒントが示されます。 「Add more variety to your ratings (レーティングにもっと多様性を追加)」は、`Relevant` と `Not relevant` の両方の評価を使用するべきであることを意味します。 要件を満たすと、トレーニングは定期的な更新を開始します。 これは開始してから完了するまで 30 分もかからず、Watson が更新している間も作業を続けることができます。
1.  照会の追加および結果のレーティングを続けます。

左上にある**「照会の作成 (Build queries)」**をクリックすると、いつでも**「照会の作成 (Build queries)」**メイン画面に戻ることができます。
{: tip}
**「データの管理 (Manage data)」**画面に戻るには、右上にあるコレクション名をクリックします。
{: tip}

コレクション内のすべてのトレーニング・データを一度に削除したい場合は、API を使用して行う必要があります。 詳しくは、[Delete all training data for a collection ](https://{DomainName}/apidocs/discovery#delete-all-training-data)を参照してください。 API を使用したトレーニングについて詳しくは、[API を使用した照会結果関連性の改善](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api)を参照してください。

## 結果の関連性についてのテストおよび反復
{: #testing-results}

結果の評価を完了し、Watson がトレーニングを適用した後、照会結果が改善されたかどうかを確認するためにテストを行う必要があります。 そのためには、トレーニング照会に関連した (ただし同一ではない) テスト照会を実行します。 テスト照会の結果が改善されたかどうかを確認します。

テスト後にさらに結果を改善したい場合は、以下を行うことができます。
- コレクションにさらに文書を追加する。
- さらにトレーニング照会を追加する。
- `Relevant` と `Not relevant` の両方の評価を必ず使用して、より多くの結果を評価する。

トレーニングに関する追加ガイダンスについては、『[関連性トレーニングのヒント](/docs/services/discovery?topic=discovery-relevancy-tips#relevancy-tips)』を参照してください。

## 信頼度スコア
{: #confidence}

自然言語照会でも、{{site.data.keyword.discoveryshort}} 照会言語で書かれた照会でも、{{site.data.keyword.discoveryshort}} は `confidence` スコアを返します。

トレーニングされたプライベート・コレクションでも、トレーニングされていないプライベート・コレクションでも (トレーニングされていないコレクションのフィルターのみの照会を除く)、`confidence` スコアは返されます。また、{{site.data.keyword.discoveryshort}} は、次に示す `confidence` スコアのソースを表す `document_retrieval_strategy` フィールドも返します。 
-  `untrained`
-  `relevancy_training`、または
-  `continuous_relevancy_training`

`document_retrieval_strategy` と `confidence` スコアを一緒に使用することで、返された結果をどのように使用すべきかを判断できます。負荷が大きいと、トレーニングされたコレクションでも、`untrained` の `document_retrieval_strategy` が返されることがあります。

`confidence` の範囲は 0.0 から 1.0 までです。 この数値が大きいほど、文書の関連度が高くなります。

`confidence` スコアは、各文書の照会結果の `result_metadata` の下にあります。  `document_retrieval_strategy` は `retrieval_details` の下にリストされます。

```json
{
  "matching_results": 4,
  "session_token": "1_2gYuWJyaWx792Ni4_DQ4C5cbnW",
  "retrieval_details" : {
    "document_retrieval_strategy" : "relevancy_training",
  },
  "results": [
    {
      "id": "eea16dfd5fe6139a25324e7481a32f89_13",
            "result_metadata": {
        "confidence": 0.5893963975910735,
        "score": 0.5006834
      }
    }
  ]
}
```
{: codeblock}

トレーニングされたコレクションでは、トレーニングされたモデルと比較して結果関連性が見積もられ、その見積もり値に基づいて、`confidence` 数値が計算されます。トレーニングされたコレクションの `confidence` スコアが計算されるのは、自然言語照会の場合のみです。トレーニングされたコレクションを {{site.data.keyword.discoveryshort}} 照会言語を使用して照会した場合、またはトレーニングされたモデルが一時的に使用不可だった場合、返される `confidence` 数値の `document_retrieval_strategy` は `untrained` になります。`document_retrieval_strategy` が `untrained` である結果の `confidence` スコアは、照会に対する文書結果の関連性について教師なしで見積もられた値です。このようなスコアは、トレーニングされたコレクションの場合に返されるスコアと同等のものではありません。トレーニングされたコレクションは、トレーニングされていないコレクションよりも、自然言語照会で適切な回答を返すことができます。

`confidence` (信頼度) スコアは `score` と同じ**ではない**ということに注意してください。信頼度スコアのしきい値の決定について詳しくは、[How to select a threshold for acting using confidence scores ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.ibm.com/watson/blog/2016/06/23/how-to-select-a-threshold-for-acting-using-confidence-scores/) を参照してください。 `score` は、相対的な計算であるため、絶対しきい値の設定に使用するべきではありません。 代わりに、`confidence` フィールドを含んでいないすべての結果に対して、アプリケーションでは常に同じ動作を実行することをお勧めします。 例えば、アプリケーションでは、`confidence` フィールドのない結果をすべて表示するか、`confidence` フィールドのない結果をすべて非表示にすることはかまいませんが、`score` の値を使用して、一部を表示し、他は非表示にすることはすべきでありません。 `confidence` の計算方法は取得方式によって異なるため、しきい値を設定する際は `document_retrieval_strategy` を考慮に入れ、トレーニングの前後に値を確認する必要があります。

照会について詳しくは、[照会入門](/docs/services/discovery?topic=discovery-getting-started-with-querying#getting-started-with-querying)を参照してください。

教師ありのトレーニング方式について詳しくは、以下を参照してください。
-  [関連性トレーニング](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling) および
-  [Continuous Relevancy Training](/docs/services/discovery?topic=discovery-crt#crt)
