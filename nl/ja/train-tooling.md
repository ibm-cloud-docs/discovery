---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-05"

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

# ツールを使用した結果関連性の改善

{{site.data.keyword.discoveryfull}} サービスでトレーニングを使用して、自然言語照会の関連性を改善することができます。{{site.data.keyword.discoveryshort}} ツールまたは {{site.data.keyword.discoveryshort}} API のいずれかを使用して、プライベート・コレクションをトレーニングすることができます。API を使用したい場合は、[API を使用した照会結果関連性の改善](/docs/services/discovery/train.html)を参照してください。
{: shortdesc}

関連性トレーニングはオプションです。照会の結果がニーズを満たしている場合は、それ以上のトレーニングは不要です。トレーニング用のユース・ケース作成の概要については、ブログ投稿 [How to get the most out of Relevancy Training ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window} を参照してください。

Watson をトレーニングするためには、以下を行う必要があります。

  -   ユーザーが入力する照会を代表するような照会例を用意する
  -   各照会の結果のどれが関連していて、どれが関連していないのかを示す評価を用意する

Watson のトレーニング入力が十分になれば、各照会のどの結果が良でどの結果が不良なのかに関して用意した情報が、コレクションについて学習するために使用されるようになります。Watson は、単に記憶するのではなく、個々の照会に関する具体的な情報から学習し、検出したパターンをすべての新規照会に適用します。これは、コンテンツと質問の中にあるシグナルを検出する Watson 機械学習手法によって行われます。トレーニングが適用された後、{{site.data.keyword.discoveryshort}} は照会結果を並べ替えて、最も関連性の高い結果を上位に表示します。さらに多くのトレーニング・データを追加するにしたがって、{{site.data.keyword.discoveryshort}} による照会結果の順序付けが正確になっていくはずです。

{{site.data.keyword.discoveryshort}} が評価の適用を開始するためには、トレーニングが以下の**最小**要件を満たす必要があります。

  - 最低限 49 個、できればもっと多くの照会をトレーニングする必要があります。Watson は、トレーニングのためにもっと多くの照会が必要な場合、フィードバックで知らせます。
  - 使用可能な評価 `Relevant` および `Not relevant` の両方を結果に適用する必要があります。`Relevant` 文書のみを評価すると、必要なデータが提供されません。

**注:** 関連性トレーニングの効果が出るには、その前にトレーニング・データについてのいくつかの要件が満たされる必要があります。本サービスは、トレーニング・データを定期的に検査してこれらの要件が満たされているかどうかを判別し、変更内容に基づいてそれ自体を自動的に更新します。

**注:** 現在のところ、関連性トレーニングは、プライベート・コレクションにおける自然言語照会にのみ適用され、構造化された {{site.data.keyword.discoveryshort}} 照会言語の照会での使用はその対象にはなっていません。{{site.data.keyword.discoveryshort}} 照会言語について詳しくは、[照会の概念](/docs/services/discovery/using.html)を参照してください。

**注:** トレーニングされたコレクションは、環境当たり最大 4 つあります。  

## 照会の追加および結果の関連性の評価

トレーニングは、自然言語照会、照会結果、それらの結果に適用する評価という 3 つのパーツからなります。

1.  {{site.data.keyword.discoveryshort}} ツールでは、**「照会の作成 (Build queries)」**画面からコレクションのトレーニング・ページにアクセスできます。右上にある**「結果を改善するために Watson をトレーニングする (Train Watson to improve results)」**をクリックします。トレーニングを開始するために**「照会の作成 (Build queries)」**画面で照会を入力する必要はありません。
1.  **「Watson のトレーニング (Train Watson)」**画面で、**「自然言語照会の追加 (Add a natural language query)」**をクリックします。例えば「IBM Watson in healthcare」を追加します。ユーザーが質問すると予想される照会を作成してください。また、トレーニング照会は、照会と望ましい回答とでいくつかの用語が重なるように作成する必要があります。これによって、自然言語照会が実行されたときの最初の結果が改善されます。関連性トレーニングでは自然言語照会のみが使用されます。{{site.data.keyword.discoveryshort}} 照会言語で作成された照会を入力しないでください。
1.  照会の結果を表示するため、その横にある**「結果の評価 (Rate Results)」**ボタンをクリックします。十分な数の結果がないと思う場合は、照会を書き直すか、または、**「データの管理 (Manage data)」**画面でこのコレクションにさらに文書を追加してみてください。
1.  `Relevant` または `Not relevant` のいずれかとして結果の評価を開始します。完了したら、**「照会に戻る (Back to queries)」**をクリックします。{{site.data.keyword.discoveryshort}} ツールでは、`Relevant` はスコア `10` であり、`Not relevant` はスコア `0` です。このコレクションの結果レーティングを API を使用して既に開始し、かつ、異なるスコアリング・スケールを使用した場合、警告が表示され、問題を修正するためのオプションが示されます。
    画面の最上部で、Watson によってトレーニング状況がずっと追跡され、結果を改善するためにできることに関するヒントが示されます。「Add more variety to your ratings (レーティングにもっと多様性を追加)」は、`Relevant` と `Not relevant` の両方の評価を使用するべきであることを意味します。要件を満たすと、トレーニングは定期的な更新を開始します。これは開始してから完了するまで 30 分もかからず、Watson が更新している間も作業を続けることができます。
1.  照会の追加および結果のレーティングを続けます。

左上にある**「照会の作成 (Build queries)」**をクリックすると、いつでも**「照会の作成 (Build queries)」**メイン画面に戻ることができます。
{: tip}
**「データの管理 (Manage data)」**画面に戻るには、右上にあるコレクション名をクリックします。
{: tip}

コレクション内のすべてのトレーニング・データを一度に削除したい場合は、API を使用して行う必要があります。詳しくは、[Delete all training data for a collection ](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-all-training-data)を参照してください。API を使用したトレーニングについて詳しくは、[API を使用した照会結果関連性の改善](/docs/services/discovery/train.html)を参照してください。

## 結果の関連性についてのテストおよび反復

結果の評価を完了し、Watson がトレーニングを適用した後、照会結果が改善されたかどうかを確認するためにテストを行う必要があります。そのためには、トレーニング照会に関連した (ただし同一ではない) テスト照会を実行します。テスト照会の結果が改善されたかどうかを確認します。

テスト後にさらに結果を改善したい場合は、以下を行うことができます。
- コレクションにさらに文書を追加する。
- さらにトレーニング照会を追加する。
- `Relevant` と `Not relevant` の両方の評価を必ず使用して、より多くの結果を評価する。

トレーニングに関する追加ガイダンスについては、『[関連性トレーニングのヒント](/docs/services/discovery/train-tips.html#relevancy-tips)』を参照してください。

## 信頼度スコア
{: #confidence}

トレーニングされたコレクションは、自然言語照会の結果に `confidence` スコアを入れて返すようになります。この `confidence` 数値は、トレーニングされたモデルと比較して見積もられる、結果の関連性の度合いに基づいて計算されます。`confidence` スコアは `score` と同じでは**ありません**。信頼度スコアのしきい値の決定について詳しくは、[How to select a threshold for acting using confidence scores ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.ibm.com/watson/blog/2016/06/23/how-to-select-a-threshold-for-acting-using-confidence-scores/) を参照してください。`score` は、相対的な計算であるため、絶対しきい値の設定に使用するべきではありません。

`confidence` の範囲は 0.0 から 1.0 までです。この数値が大きいほど、文書の関連度が高くなります。

`confidence` スコアは、各文書の照会結果の `result_metadata` の下にあります。以下に例を示します。

```json
    "results": [
        {
            "id": "eea16dfd5fe6139a25324e7481a32f89_13",
            "result_metadata": {
                "confidence": 0.5893963975910735,
                "score": 0.5006834
            },
```
