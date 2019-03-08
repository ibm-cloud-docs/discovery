---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-23"

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

# 照会の概念
{: #query-concepts}

{{site.data.keyword.discoveryfull}} サービスは、強力なコンテンツ検索機能を提供します。 {{site.data.keyword.discoveryshort}} サービスによってコンテンツがアップロードされ、エンリッチされたら、照会を作成することができます。また、その後、{{site.data.keyword.discoveryshort}} をプロジェクトに統合したり、{{site.data.keyword.watson}} Explorer Application Builder を使用してカスタム・アプリケーションを作成したりできます。
{: shortdesc}

  コレクションのコンテンツはすべて固有であるため、作成する照会はコレクションによって異なります。
  {: tip}

照会またはフィルターを作成すると、{{site.data.keyword.discoveryshort}} は各結果を調べて、定義済みのパスを突き合わせます。 一致があれば、それらが結果セットに追加されます。 照会を作成するときには、あいまいにしたり、具体的にしたり、好きなように作成できます。 照会が具体的であるほど、結果は絞り込まれます。

パッセージ取り出しをオンにするオプションもあります。 パッセージは、照会から返される全文書から抽出される、関連する短い抜粋です。的を絞ったこれらのパッセージは、コレクション内の文書の `text` フィールドから抽出されます。 デフォルトでは、1 つの照会に対して、それぞれ 400 文字ほどの最大 10 個のパッセージが返されます。 1 つの結果から抽出されるのは、最大 3 つまでのパッセージです。 `passages` パラメーターは、プライベート・コレクションにのみ使用可能であり、{{site.data.keyword.discoverynewsshort}} コレクションでは使用できません。 パッセージがどのように識別されるのかについて詳しくは、『[パッセージ](/docs/services/discovery/query-parameters.html#passages)』を参照してください。

  {{site.data.keyword.discoveryshort}} ツールまたは API を使用して、自然言語照会 (例：「IBM Watson partnerships」) を作成できます。
  {: tip}

トレーニングされたコレクションは、自然言語照会の結果で `confidence` スコアを返します。詳しくは、[信頼度スコア](/docs/services/discovery/train-tooling.html#confidence)を参照してください。

{{site.data.keyword.discoveryshort}} では、英語、ドイツ語、フランス語、オランダ語、イタリア語、およびポルトガル語の各言語の特殊文字が含まれる照会結果が返されます。例えば、`aqui` を照会した場合、`aqui` と <code>aqu&iacute;</code> の両方を結果で受け取ります。

複数のフィルターと複雑な集約を含んだ、より長くてより複雑な照会を作成できます。このオプションは API のみで使用可能であり、照会の文字の長さ制限が 10,000 文字に増えます。詳しくは、[長いコレクション照会 (Long collection queries) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query){: new_window} および [長い環境照会 (Long environment queries) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#federated-query){: new_window} を参照してください。

{{site.data.keyword.discoveryfull}} Knowledge Graph は、複数の文書にわたってエンティティーおよび関係を照会するための新しいエンドポイントを提供するベータ版フィーチャーです。これには、コンテキスト・ベースの検索および関連性ランキングが含まれます。 詳しくは、[{{site.data.keyword.discoveryfull}} Knowledge Graph](/docs/services/discovery/building-kg.html) を参照してください。

照会の作成について詳しくは、以下を参照してください。
- [照会入門のチュートリアル](/docs/services/discovery/getting-started-query.html)
- [照会リファレンス](/docs/services/discovery/query-reference.html) ({{site.data.keyword.discoveryshort}} 照会言語で使用可能なパラメーター、演算子、および集約のリストが含まれています)

## Discovery データ・スキーマ
{: #discovery-schema}

まず、{{site.data.keyword.discoveryshort}} JSON について理解してください。 {{site.data.keyword.discoveryshort}} 照会言語を使用して照会を作成する方法を理解するには、{{site.data.keyword.discoveryshort}} がコレクション内の文書をエンリッチした後で生成する JSON についてよく知ることが必要です。 文書のデータ・スキーマを理解すれば、{{site.data.keyword.discoveryshort}} 照会言語で照会を作成するのが簡単になります。 そのためには 3 つの方法があります。

  1. {{site.data.keyword.discoveryshort}} ツールで、**「データの管理 (Manage data)」**画面を開き、{{site.data.keyword.IBM_notm}} プレス・リリースを含んでいるコレクションを選択します。 **「データ・スキーマの表示 (View Data Schema)」**ボタンをクリックします。 **「データ・スキーマの表示 (View data schema)」**画面に、文書別 (**「文書 (Document)」ビュー**) またはフィールド別 (**「コレクション (Collection)」ビュー**) の 2 つの方法のいずれかで、変換された文書中のフィールドと値が表示されます。 **「文書 (Document)」ビュー**には最大 50 の文書が表示されます。 **「コレクション (Collection)」ビュー**には、コレクション全体のフィールドが表示されます。

    **「コレクション (Collection)」ビュー**の `enriched_text` の下で、**Default Configuration** ファイルを使用して適用したエンリッチメントを調べることができます。`categories`、`concepts`、`entities`、および `sentiment` をクリックすると、Watson の洞察によってコレクションがどのようにエンリッチされたのかを確認できます。

  1. 「空の」照会を実行して JSON を表示します。 **「データ・スキーマの表示 (View data schema)」**画面で**「照会の作成 (Build queries)」**ボタンをクリックし、次に、**「照会の実行 (Run Query)」**をクリックします。 結果は、右側にある**「サマリー (Summary)」** (照会結果の概要) および**「JSON」**の 2 つのタブに表示されます。 まず**「JSON」**タブを開きます。

     -  4 つの文書のそれぞれは `id` 番号から始まります。
     -  `enriched_text` フィールドまでスクロールダウンします。 各エンリッチメントを検査して、照会の対象にできる JSON フィールドについて理解してください。

        ![デフォルト構成のフィールド](images/JSON.png)

     -  **entities** - まず `text` フィールドを探し、次に、他のエンリッチメント情報を調べてください。
     -  **sentiment** - まず `label` フィールドを探し、次に、他のエンリッチメント情報を調べてください。
     -  **concepts** - まず `text` フィールドを探し、次に、他のエンリッチメント情報を調べてください。
     -  **categories** - まず `document` フィールドを探し、次に、他のエンリッチメント情報を調べてください。

     最初の文書中の洞察を調べた後、必要であれば他の 3 つの文書も見ることができます。

  1. **ビジュアル照会ビルダー**で、使用可能なフィールドを表示します。 **「照会の作成 (Build queries)」**画面で、**「文書の検索 (Search for documents)」**をクリックし、次に、**「{{site.data.keyword.discoveryshort}} 照会言語の使用 (Use the {{site.data.keyword.discoveryshort}} Query Language)」**をクリックします。 **「フィールド (Field)」**ドロップダウンをクリックして、データ内にあるフィールドを表示します。 {{site.data.keyword.discoveryshort}} 照会言語を使用して照会を手動で作成するには、**「照会言語での編集 (Edit in query language)」**をクリックします。      

### 基本的な照会の組み立て方
{: #structure-basic-query}

お気付きのように、JSON は階層型であるため、照会を作成するときには同じ階層を使用する必要があります。 次のような JSON を想定します。

```json
"enriched_text": {
  "concepts": [
    {
    "text": "Cloud computing",
    "relevance": 0.610029}
    ]
  }
```
{: codeblock}

この場合、照会は次のような構造になります。

![照会の構造例](images/query_structure2.png)

  フィールドを評価する演算子 (`<=`、`>=`、`<`、`>`) は、値として `number` または `date` を必要とします。値を引用符で囲むと、その値は常に `string` になります。したがって、`score>=0.5` は有効な照会ですが、`score>="0.5"` は有効ではありません。演算子の完全なリストについては、[照会演算子](/docs/services/discovery/query-operators.html)を参照してください。
  {: tip}

考慮事項

- どのようなときにエンティティー、コンセプト、キーワードの照会を行えばよいのかがよく分からない場合、『[エンティティー、概念、およびキーワードの違いについて](/docs/services/discovery/building.html#udbeck)』を参照してください。

- **注:** **「照会の実行 (Run query)」**をクリックした後に**「JSON」**タブを開くと、照会の強調表示がデフォルトでオンになっていることがわかります。 これによって、照会結果に `highlight` フィールドが追加されます。 `highlight` フィールド内で、照会に一致する単語は HTML `<em>` (強調表示) タグで囲まれます。 詳しくは、『[照会パラメーター](/docs/services/discovery/query-parameters.html#highlight)』を参照してください。

## 結合された照会の作成
{: #building-combined-queries}

複数の照会パラメーターを結合することで、さらに的を絞った照会を作成できます。 例えば、`filter` パラメーターと `query` パラメーターの両方を一緒に使用できます。 フィルターと照会の違いについて詳しくは、『[filter パラメーターと query パラメーターの相違点](/docs/services/discovery/query-parameters.html#filtervquery)』を参照してください。

## 集約の組み立て方
{: #structure-aggregation}

集約は、データ値の集合 (例えば、上位キーワード、エンティティーのセンチメント全体など) を返します。 集約オプションの完全なリストについては、『[集約](/docs/services/discovery/query-reference.html#aggregations)』を参照してください。

![集約照会の構造の例](images/aggregation_structure.png)

この例の集約では、コレクション内のすべての `concepts` が検出されます。
この照会での区切り文字は `.` であり、演算子は `()` です。{{site.data.keyword.discoveryshort}} 照会言語で使用可能なその他の演算子について詳しくは、[照会演算子](/docs/services/discovery/query-operators.html)を参照してください。

### 集約照会の例
{: #example-aggregations}

{{site.data.keyword.discoverynewsshort}} での結果を集約する方法には、上位値、合計、最小、最大、平均、タイム・スライス、ヒストグラムなど、数種類の方法があります。 フィルターを追加したり、集約をネストしたりもできます。

#### 集約のフィルタリング
{: #filter-aggregations}

次の集約の例は、{{site.data.keyword.discoverynewsshort}} で見つかった Pittsburgh Steelers (フットボール・チーム) に関する記事の数と、それらの結果のうちセンチメントが `positive`、`negative`、または `neutral` である数を返します。

- `filter(enriched_text.entities.text:"Pittsburgh Steelers").term(enriched_text.sentiment.document.label,count:3)`


次の集約の例は、最初に {{site.data.keyword.discoverynewsshort}} 内の記事集合の絞り込み (フィルター) によって Twitter のエンティティー・テキストを含む記事だけにし、次に、それらの記事を文書センチメント・タイプ別に分けます。 最上位の 3 つの文書センチメント・タイプ (`positive`、`negative`、`neutral`) のみが返されます。

- `filter(enriched_text.entities.text:twitter).term(enriched_text.sentiment.document.label,count:3)`

#### ネストされた集約
{: #nested-aggregations}

集約の前に `nested` を追加すると、集約は指定された結果領域に制限されます。 例えば、`nested(enriched_text.entities)` は、結果の `enriched_text.entities` コンポーネントのみが集約に使用されることを意味します。

以下の 2 つの照会の違いを見ると、これがよく分かります。
- `filter(enriched_text.entities.disambiguation.subtype::City)` - この集約は、タイプ `City` の `entity` を 1 つ以上含んでいる*結果* の数をカウントします。
- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City)` - この集約は、タイプ `City` の `entity` のインスタンスの数を結果内でカウントします。  

これに加えて後続の演算があれば、集約に使用できる結果セットはさらに限定されます。以下に例を示します。

- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City)` は、`subtype::City` のエンティティーのみが集約されることを意味します。
- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City).term(enriched_text.entities.text,count:3)` は、サブタイプが `City` の上位 3 つのエンティティーを集約します。
- `filter(enriched_text.entities.disambiguation.subtype::City).term(enriched_text.entities.text,count:3)` は、結果にサブタイプ `City` のエンティティーが 1 つ以上含まれている、上位 3 つのエンティティーを返します。

## Watson Discovery News の照会
{: #querying-news}

{{site.data.keyword.discoveryshort}} には、コグニティブな洞察によって事前にエンリッチされた公開データ・セット、{{site.data.keyword.discoverynewsshort}} も含まれています。このコレクションについて詳しくは、『[Watson Discovery News](/docs/services/discovery/watson-discovery-news.html#watson-discovery-news)』を参照してください。

自然言語照会 (例: 「IBM Watson partnerships」) または {{site.data.keyword.discoveryshort}} 照会言語を使用してこのコレクションを照会できます。 自然言語照会について詳しくは、『[自然言語照会](/docs/services/discovery/query-parameters.html#nlq)』を参照してください。

{{site.data.keyword.discoverynewsshort}} の構成を調整したり、トレーニングを行ったり、{{site.data.keyword.discoverynewsshort}} コレクションに文書を追加したりすることはできません。{{site.data.keyword.discoverynewsshort}} を使用して何を作成できるのかを示すデモを[ここ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://discovery-news-demo.ng.bluemix.net/){: new_window} で見ることができます。

英語、韓国語、ドイツ語、スペイン語、および日本語の {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} コレクションを {{site.data.keyword.discoveryshort}} ツールと API の両方で使用できます。

{{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} ツールのデフォルト言語は、英語です。言語を切り替えるには、まず、![データの管理](/images/icon_yourData.png) アイコンをクリックし、次にドロップダウンから適切な言語を選択します。

API を介したコレクションの照会について詳しくは、[API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection){: new_window} を参照してください。 英語版の Watson {{site.data.keyword.discoverynewsshort}} の `collection_id` は `news-en` です。 以前は、`collection_id` は `news` でした。以前の `collection_id` を使用している場合、引き続き機能しますが、新しいプロジェクト用に新しい `collection_id` に切り替えることをお勧めします。 韓国語コレクションの `collection_id` は `news-ko`、スペイン語の `collection_id` は `news-es`、ドイツ語の `collection_id` は `news-de`、日本語の `collection_id` は `news-ja` です。

{{site.data.keyword.discoverynewsfull}} 照会では、`text` JSON フィールドに各記事の最初の 50 ワードが表示されます。

{{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} の 1 回の照会で返される結果の最大数は `50` です。`50` を超える結果を返すには、追加の照会と `offset` パラメーターを使用してください。

{{site.data.keyword.discoveryshort}} 照会言語を使用する場合、{{site.data.keyword.discoverynewsshort}} 照会に相対日付範囲 (例: `crawl_date>=now-1month`) を組み込むことができます。 有効な日付間隔値は、`second/seconds`、`minute/minutes`、`hour/hours`、`day/days`、`week/weeks`、`month/months`、および `year/years` です。 `now` は `time_zone` パラメーターの影響を受けません。`UTC` タイム・ゾーンがデフォルトです。

以下の例では、特定の日付範囲内でキーワードを照会します。タイム・ゾーン情報は不要です。
- `enriched_text.keywords.text:"olympics", publication_date<=2018-02-15T00:00:00Z, publication_date>=2018-02-01T00:00:00Z`

ニュース記事はいくつかの報道機関に配信される可能性があり、{{site.data.keyword.discoverynewsfull}} はそれらの中から各記事を選出するため、記事が重複することがあります。これは、{{site.data.keyword.discoverynewsfull}} への照会の結果、複数の同じ記事またはほぼ同じ記事が返される可能性があることを意味します。重複排除を使用してこれを管理できます。 このベータ機能について詳しくは、『[照会結果から重複する文書を除外](/docs/services/discovery/query-parameters.html#deduplication)』を参照してください。

## 複数コレクションの照会
{: #multiple-collections}

環境に複数のコレクションがある場合、それらのコレクションにまたがる結果が必要になることがあります。 `environments` レベルで照会メソッド (`query`、`fields`、および `notices`) を使用すると、指定した複数のコレクションを照会することができます。 現在のところ、複数のコレクションにまたがる照会は {{site.data.keyword.discoveryshort}} ツールでは使用できません。

`environments/{environment_id}/query` API メソッドを使用することによって、同じ環境にある複数のコレクションに対して照会を実行できます。 複数のコレクションにまたがって照会するときには、以下を考慮してください。
-  このメソッドを使用するときには `collection_ids` パラメーターを指定する必要があります。 `collection_ids` は、照会する対象の環境内のコレクションをコンマで区切ったリストです。
-  `passages` は、複数のコレクションを照会する場合にサポートされます。
-  `collection_id` は、各結果オブジェクトの一部として返されます。このフィールドは、その結果が見つかったコレクションを指定します。
-  {{site.data.keyword.discoverynewsshort}} は、`system` 環境の一部であり、複数コレクションの照会に含めることはできません。
-  個別のコレクション関連性のトレーニングは、複数のコレクションを照会する際の結果のランキングには影響しません。複数のコレクションを照会するときに返される結果を再ランク付けするには、[Continuous Relevancy Training](/docs/services/discovery/continuous-training.html) を実装してください。
-  複数コレクションの照会では、照会内のすべてのコレクションがトレーニング済みであっても、照会のどの部分でも再ランキングは実行されません。

詳しくは、[複数コレクションの照会に関する API リファレンス![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-multi-collections){: new_window} を参照してください。

`environments/{environment_id}/notices` API メソッドを使用することによって、同じ環境にある複数のコレクションにわたって通知を確認できます。
-  このメソッドを使用するときには `collection_ids` パラメーターを指定する必要があります。 `collection_ids` は、照会する対象の環境内のコレクションをコンマで区切ったリストです。
-  `passages` は、複数のコレクションを照会する場合にサポートされます。

詳しくは、[複数コレクションの通知に関する API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#collections-notices){: new_window} を参照してください。

`environments/{environment_id}/fields` API メソッドを使用することによって、同じ環境にある複数のコレクションにまたがって使用可能なフィールドを確認できます。 詳しくは、[複数コレクションのフィールド照会に関する API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#multi-list-fields){: new_window} を参照してください。

## 照会拡張
{: #query-expansion}

{{site.data.keyword.discoveryshort}} API を使用して照会拡張用語のリストをアップロードすることで、照会の適用範囲を、完全一致を超えた範囲まで拡張できます。例えば、「car」に対する照会を「automobile」や「motor vehicle」まで含めるように拡張できます。照会拡張用語は、通常、一般的な用語の同義語、対義語、または典型的なミススペルです。

以下の 2 つのタイプの拡張を定義できます。
- **両方向** - 各 `expanded_term` が拡張され、拡張されたすべての用語が組み込まれます。例えば、`car` の照会は、`car OR automobile OR (motor AND vehicle`) に拡張されます。
- **単一方向** - 照会内の `input_terms` が `expanded_terms` に置き換えられます。例えば、`ibm` の照会は、`international business machines` と `big blue` に拡張されます。`input_terms` は、結果として生成される照会の一部としては使用されません。前の `ibm` の例では、照会 `IBM` は、`international business machines` または `big blue` に変換され、元の用語は含まれません。

以下のファイルを、照会拡張リストを作成する際の開始点として使用できます。
<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/expansions.json" download>expansions.json <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン" class="style-scope doc-content"></a>。このファイルを変更して、カスタムの照会拡張リストを作成できます。

両方向の例:
```JSON
 {
   "expansions": [
     {
       "expanded_terms": [
         "car",
         "automobile",
         "motor vehicle"
       ]
     }
   ]
 }
```
{: codeblock}

単一方向の例:
```JSON
 {
   "expansions": [
     {
      "input_terms": [
        "ibm"
       ],
      "expanded_terms": [
        "ibm",
        "international business machines",
        "big blue"
       ]
     }
   ]
 }
```
{: codeblock}

照会拡張に関する注意

- 照会拡張は、プライベート・コレクションにのみ使用可能です。使用可能な `expansions` 配列 (両方向と単一方向の配列の合計) および用語 (`input_terms` と `expanded_terms` を加算した合計) の数は、プランによって異なります。詳しくは、[Discovery の料金プラン](/docs/services/discovery/pricing-details.html)を参照してください。**注:** すべての照会用語 (`input_terms` と `expanded_terms` の両方) は、それぞれが 1 つの用語としてカウントされます。この例の場合、`expansions` 配列内に 2 つのオブジェクトと、8 つの用語ストリングが含まれています。

```JSON
 {
   "expansions": [
     {
      "input_terms": [
         "ibm"
       ],
      "expanded_terms": [
         "ibm",
         "international business machines",
         "big blue"
       ]
     },
     {
      "input_terms": [
         "banana"
       ],
      "expanded_terms": [
         "banana",
         "plantain",
         "fruit"
       ]
     }
   ]
 }
```
{: codeblock}

- コレクションごとにアップロードできる照会拡張リストは 1 つのみです。2 番目の拡張リストがアップロードされると、最初のリストは置き換えられます。
- `input_terms` および `expanded_terms` はすべて小文字でなければなりません。小文字の用語は大文字に拡張されます。
- 照会拡張リストは JSON で記述する必要があります。
- 照会拡張を無効にするには、照会拡張リストを削除します。
- 現在、{{site.data.keyword.discoveryshort}} ツールを使用して照会拡張リストをアップロードおよび削除することはできません。その際は、{{site.data.keyword.discoveryshort}} API を使用してください。
- 照会拡張は、`query` メソッドおよび `multiple collection query` メソッドに対して実行されます。照会拡張は、Knowledge Graph 照会では実行されません。
- 拡張の各セットは、1 つのコレクションに関連付けられます。[複数のコレクション](/docs/services/discovery/using.html#multiple-collections)にまたがって照会する場合は、各コレクションが個別に拡張されます。
- 照会拡張は、索引付け時でなく、照会時に適用されます。したがって、文書を再取り込みすることなく、照会拡張リストを更新できます。
- 文書がコレクションに取り込まれるのと同じときに、照会拡張リストをアップロードしたり削除したりしないでください。そうすると、その短い期間、索引が使用不可になる可能性があります。

照会拡張ファイルをアップロードおよび削除するための API コマンドについては、[照会拡張に関する API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-expansion){: new_window} を参照してください。

## カスタムのトークン化辞書

トークン化は、テキストをトークンと呼ばれる単位に分割します。コレクションには標準のトークン化辞書が適用されますが、カスタムのトークン化辞書をアップロードすることで、ドメインまたは言語の検索精度を高めることができます。カスタム辞書は標準辞書をオーバーライドします。辞書は、{{site.data.keyword.discoveryshort}} API を使用してアップロードできます。 

トークン化ファイルをアップロードおよび削除するための API コマンドについては、[トークン化に関する API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#create-tokenization-dictionary){: new_window} を参照してください。 

**注:** 現在、この機能は、日本語コレクションでのみ使用可能です。 

以下の例で、**text** は、検出されたときにトークン化される句で、**tokens** は、**text** が分割された後の単語です。**readings** には、異なる文字セットで表されるトークンのバージョンがリストされ、**part_of_speech** はトークンが表す品詞です。

このカスタム辞書を使用して、`ネコ`というテキストを検索した場合、検索結果には、`ネコ`のみを含んだテキストに加えて、`すしネコ`を含んでいるテキストも組み込まれます。

```
{ "tokenization_rules":
  [
    {
      "text":"すしネコ",
      "tokens":[
        "すし",
        "ネコ"
      ],
      "readings":[
        "寿司",
        "ネコ"
      ],
      "part_of_speech":"カスタム名詞"
    },
    ...
  ]
}
```

単一トークンを含んだルールを作成することもできます。この例の場合、`ibm発見`は単一トークンとしてトークン化され、それ以上小さい単位には分割されません。

```
{ "tokenization_rules":
  [
    {
      "text":"ibm発見",
      "tokens":[  
      "ibm発見"
      ],
      "readings":[  
      "ibm発見"
      ],
      "part_of_speech":"カスタム名詞"
    },
    ...
  ]
}
```

- トークン化は、索引付けと照会時の両方で行われます。 
- 標準トークン化辞書は、すべてのコレクションに使用されます。コレクションが既にその辞書を使用して索引付けされている場合は、カスタムのトークン化辞書をアップロードした後に、そのコレクション内に文書を再取り込みする必要があります。
- コレクションごとにアップロードできるトークン化辞書は 1 つのみです。2 番目のトークン化辞書がアップロードされると、最初の辞書は置き換えられます。そのコレクションに既に文書が含まれていた場合、新しいカスタムのトークン化辞書を適用するためには、それらの文書を再取り込みする必要があります。
- カスタムのトークン化辞書は、JSON で記述する必要があります。サンプル・ファイル名は `custom_tokenization_dictionary.json` です。
- トークン化を無効にするには、トークン化辞書を削除し、文書を再取り込みします。
- 現在、{{site.data.keyword.discoveryshort}} ツールを使用してトークン化辞書をアップロードまたは削除することはできません。その際は、{{site.data.keyword.discoveryshort}} API を使用してください。
- トークン化は、`query` メソッドおよび `multiple collection query` メソッドに対して実行されます。トークン化は、Knowledge Graph 照会では実行されません。
- 各トークン化辞書は、1 つのコレクションに関連付けられます。[複数のコレクション](/docs/services/discovery/using.html#multiple-collections)にまたがって照会する場合は、各コレクションが個別にトークン化されます。
- 文書がコレクションに取り込まれるのと同じときに、トークン化辞書をアップロードしたり削除したりしないでください。 

## 文書類似性
{: #doc-similarity}

文書類似性照会では、現在表示されている文書に似た他の文書が検索されます。例えば、ある製品のマニュアルを表示しているコール・センターのオペレーターが、文書類似性を使用して、似た特徴を持つその他の文書を検索できます。`similar.document_ids` を使用して類似文書を照会でき、オプションで、追加の `similar.fields` を指定することにより類似性を詳細化することができます。

文書類似性は、元の文書から最も関連性の高い 25 の用語を抽出し、類似した関連用語を持つ文書を検索することによって判別されます。

`similar.document_ids` による照会の例を以下に示します (複数の `similar.document_ids` を指定する場合、コンマの後にスペースは入れないでください)。

`curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&similar.document_ids=4107b6f1-5d3f-4bea-bbcf-fb05bbf960b1,6057k6d1-7d7k-6aeh-cfbb-kj98ssf786c2"`

`similar.fields` を追加した照会の例を以下に示します。

`curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&similar.document_ids=4107b6f1-5d3f-4bea-bbcf-fb05bbf960b1&similar.fields=title&return=title&count=100"`

詳しくは、[文書類似性に関する API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query-using-get){: new_window} および[照会パラメーター](/docs/services/discovery/query-parameters.html#similar)を参照してください。
