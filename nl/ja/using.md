---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-15"

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

{{site.data.keyword.discoveryfull}} サービスは、強力なコンテンツ検索機能を提供します。{{site.data.keyword.discoveryshort}} サービスによってコンテンツがアップロードされ、エンリッチされたら、照会を作成することができます。また、その後、{{site.data.keyword.discoveryshort}} をプロジェクトに統合したり、{{site.data.keyword.watson}} Explorer Application Builder を使用してカスタム・アプリケーションを作成したりできます。
{: shortdesc}

  コレクションのコンテンツはすべて固有であるため、作成する照会はコレクションによって異なります。
  {: tip}

照会またはフィルターを作成すると、{{site.data.keyword.discoveryshort}} は各結果を調べて、定義済みのパスを突き合わせます。一致があれば、それらが結果セットに追加されます。照会を作成するときには、あいまいにしたり、具体的にしたり、好きなように作成できます。照会が具体的であるほど、結果は絞り込まれます。

パッセージ取り出しをオンにするオプションもあります。パッセージは、照会から返される全文書から抽出される、関連する短い抜粋です。的を絞ったこれらのパッセージは、コレクション内の文書の `text` フィールドから抽出されます。デフォルトでは、1 つの照会に対して、それぞれ 400 文字ほどの最大 10 個のパッセージが返されます。1 つの結果から抽出されるのは、最大 3 つまでのパッセージです。`passages` パラメーターは、プライベート・コレクションにのみ使用可能であり、{{site.data.keyword.discoverynewsshort}} コレクションでは使用できません。パッセージがどのように識別されるのかについて詳しくは、『[パッセージ](/docs/services/discovery/query-parameters.html#passages)』を参照してください。

  {{site.data.keyword.discoveryshort}} ツールまたは API を使用して、自然言語照会 (例：「IBM Watson partnerships」) を作成できます。
  {: tip}

トレーニングされたコレクションは、自然言語照会の結果に `confidence` スコアを入れて返すようになります。詳しくは、『[信頼度スコア](/docs/services/discovery/train-tooling.html#confidence)』を参照してください。

{{site.data.keyword.discoveryfull}} Visual Insights は、試験的フィーチャーであり、これを使用すると、セマンティック・エレメント、関係、コンセプトなどを {{site.data.keyword.discoveryshort}} が理解することによって識別される関連を視覚的に探索できます。詳しくは、[{{site.data.keyword.discoveryfull}} Visual Insights](/docs/services/discovery/visual-insights.html) を参照してください。

{{site.data.keyword.discoveryfull}} Knowledge Graph は、複数の文書にわたってエンティティーおよび関連を照会するための新しいエンドポイントを提供するベータ版フィーチャーです。これには、コンテキスト・ベースの検索および関連性ランキングが含まれます。詳しくは、[{{site.data.keyword.discoveryfull}} Knowledge Graph](/docs/services/discovery/building-kg.html) を参照してください。

照会の作成について詳しくは、以下を参照してください。
- [照会入門のチュートリアル](/docs/services/discovery/getting-started-query.html)
- [照会リファレンス](/docs/services/discovery/query-reference.html) ({{site.data.keyword.discoveryshort}} 照会言語で使用可能なパラメーター、演算子、および集約のリストが含まれています)

## Discovery データ・スキーマ
{: #discovery-schema}

まず、{{site.data.keyword.discoveryshort}} JSON について理解してください。{{site.data.keyword.discoveryshort}} 照会言語を使用して照会を作成する方法を理解するには、{{site.data.keyword.discoveryshort}} がコレクション内の文書をエンリッチした後で生成する JSON についてよく知ることが必要です。文書のデータ・スキーマを理解すれば、{{site.data.keyword.discoveryshort}} 照会言語で照会を作成するのが簡単になります。そのためには 3 つの方法があります。

  1. {{site.data.keyword.discoveryshort}} ツールで、**「データの管理 (Manage data)」**画面を開き、{{site.data.keyword.IBM_notm}} プレス・リリースを含んでいるコレクションを選択します。**「データ・スキーマの表示 (View Data Schema)」**ボタンをクリックします。**「データ・スキーマの表示 (View data schema)」**画面に、文書別 (**「文書 (Document)」ビュー**) またはフィールド別 (**「コレクション (Collection)」ビュー**) の 2 つの方法のいずれかで、変換された文書中のフィールドと値が表示されます。**「文書 (Document)」ビュー**には最大 50 の文書が表示されます。**「コレクション (Collection)」ビュー**には、コレクション全体のフィールドが表示されます。

    **「コレクション (Collection)」ビュー**の `enriched_text` の下で、**デフォルト構成**ファイルを使用して適用したエンリッチメントを調べることができます。`categories`、`concepts`、`entities`、および `sentiment` をクリックすると、Watson の洞察によってコレクションがどのようにエンリッチされたのかを確認できます。

  1. 「空の」照会を実行して JSON を表示します。**「データ・スキーマの表示 (View data schema)」**画面で**「照会の作成 (Build queries)」**ボタンをクリックし、次に、**「照会の実行 (Run Query)」**をクリックします。結果は、右側にある**「サマリー (Summary)」** (照会結果の概要) および**「JSON」**の 2 つのタブに表示されます。まず**「JSON」**タブを開きます。

     -  4 つの文書のそれぞれは `id` 番号から始まります。
     -  `enriched_text` フィールドまでスクロールダウンします。各エンリッチメントを検査して、照会の対象にできる JSON フィールドについて理解してください。

        ![デフォルト構成のフィールド](images/JSON.png)

     -  **entities** - まず `text` フィールドを探し、次に、他のエンリッチメント情報を調べてください。
     -  **sentiment** - まず `label` フィールドを探し、次に、他のエンリッチメント情報を調べてください。
     -  **concepts** - まず `text` フィールドを探し、次に、他のエンリッチメント情報を調べてください。
     -  **categories** - まず `document` フィールドを探し、次に、他のエンリッチメント情報を調べてください。

     最初の文書中の洞察を調べた後、必要であれば他の 3 つの文書も見ることができます。

  1. **ビジュアル照会ビルダー**で、使用可能なフィールドを表示します。**「照会の作成 (Build queries)」**画面で、**「文書の検索 (Search for documents)」**をクリックし、次に、**「{{site.data.keyword.discoveryshort}} 照会言語の使用 (Use the {{site.data.keyword.discoveryshort}} Query Language)」**をクリックします。**「フィールド (Field)」**ドロップダウンをクリックして、データ内にあるフィールドを表示します。{{site.data.keyword.discoveryshort}} 照会言語を使用して照会を手動で作成するには、**「照会言語での編集 (Edit in query language)」**をクリックします。      

### 基本的な照会の組み立て方
{: #structure-basic-query}

お気付きのように、JSON は階層型であるため、照会を作成するときには同じ階層を使用する必要があります。次のような JSON を想定します。

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


考慮事項:

- どのようなときにエンティティー、コンセプト、キーワードの照会を行えばよいのかがよく分からない場合、『[エンティティー、概念、およびキーワードの違いについて](/docs/services/discovery/building.html#udbeck)』を参照してください。

- **注:** **「照会の実行 (Run query)」**をクリックした後に**「JSON」**タブを開くと、照会の強調表示がデフォルトでオンになっていることがわかります。これによって、照会結果に `highlight` フィールドが追加されます。`highlight` フィールド内で、照会に一致する単語は HTML `<em>` (強調表示) タグで囲まれます。詳しくは、『[照会パラメーター](/docs/services/discovery/query-parameters.html#highlight)』を参照してください。

## 結合された照会の作成
{: #building-combined-queries}

複数の照会パラメーターを結合することで、さらに的を絞った照会を作成できます。例えば、`filter` パラメーターと `query` パラメーターの両方を一緒に使用できます。フィルターと照会の違いについて詳しくは、『[filter パラメーターと query パラメーターの相違点](/docs/services/discovery/query-parameters.html#filtervquery)』を参照してください。

## 集約の組み立て方
{: #structure-aggregation}

集約は、データ値の集合 (例えば、上位キーワード、エンティティーのセンチメント全体など) を返します。集約オプションの完全なリストについては、『[集約](/docs/services/discovery/query-reference.html#aggregations)』を参照してください。

![集約照会の構造の例](images/aggregation_structure.png)

この例の集約では、コレクション内のすべての `concepts` が検出されます。
この照会での区切り文字は `.` であり、演算子は `()` です。{{site.data.keyword.discoveryshort}} 照会言語で使用可能なその他の演算子について詳しくは、[照会演算子](/docs/services/discovery/query-operators.html)を参照してください。

### 集約照会の例
{: #example-aggregations}

{{site.data.keyword.discoverynewsshort}} での結果を集約する方法には、上位値、合計、最小、最大、平均、タイム・スライス、ヒストグラムなど、数種類の方法があります。フィルターを追加したり、集約をネストしたりもできます。

#### 集約のフィルタリング
{: #filter-aggregations}

次の集約の例は、{{site.data.keyword.discoverynewsshort}} で見つかった Pittsburgh Steelers (フットボール・チーム) に関する記事の数と、それらの結果のうちセンチメントが `positive`、`negative`、または `neutral` である数を返します。

- `filter(enriched_text.entities.text:"Pittsburgh Steelers").term(enriched_text.sentiment.document.label,count:3)`


次の集約の例は、最初に {{site.data.keyword.discoverynewsshort}} 内の記事集合の絞り込み (フィルター) によって Twitter のエンティティー・テキストを含む記事だけにし、次に、それらの記事を文書センチメント・タイプ別に分けます。最上位の 3 つの文書センチメント・タイプ (`positive`、`negative`、`neutral`) のみが返されます。

- `filter(enriched_text.entities.text:twitter).term(enriched_text.sentiment.document.label,count:3)`

#### ネストされた集約
{: #nested-aggregations}

集約の前に `nested` を追加すると、集約は指定された結果領域に制限されます。例えば、`nested(enriched_text.entities)` は、結果の `enriched_text.entities` コンポーネントのみが集約に使用されることを意味します。

以下の 2 つの照会の違いを見ると、これがよく分かります。
- `filter(enriched_text.entities.disambiguation.subtype::City)` - この集約は、タイプ `City` の `entity` を 1 つ以上含んでいる*結果* の数をカウントします。 
- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City)` - この集約は、タイプ `City` の `entity` のインスタンスの数を結果内でカウントします。  

これに加えて後続の演算があれば、集約に使用できる結果セットはさらに限定されます。以下に例を示します。

- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City)` は、`subtype::City` のエンティティーのみが集約されることを意味します。
- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City).term(enriched_text.entities.text,count:3)` は、サブタイプが `City` の上位 3 つのエンティティーを集約します。
- `filter(enriched_text.entities.disambiguation.subtype::City).term(enriched_text.entities.text,count:3)` は、結果にサブタイプ `City` のエンティティーが 1 つ以上含まれている、上位 3 つのエンティティーを返します。

## Watson Discovery News の照会
{: #querying-news}

{{site.data.keyword.discoverynewsshort}} は、コグニティブな洞察で事前にエンリッチされている公開データ・セットであり、{{site.data.keyword.discoveryshort}} にも組み込まれています。このコレクションについて詳しくは、『[Watson Discovery News](/docs/services/discovery/watson-discovery-news.html#watson-discovery-news)』を参照してください。

自然言語照会 (例: 「IBM Watson partnerships」) または {{site.data.keyword.discoveryshort}} 照会言語を使用してこのコレクションを照会できます。自然言語照会について詳しくは、『[自然言語照会](/docs/services/discovery/query-parameters.html#nlq)』を参照してください。

{{site.data.keyword.discoverynewsshort}} 構成の調整、トレーニング、{{site.data.keyword.discoverynewsshort}} コレクションへの文書の追加を行うことはできません。{{site.data.keyword.discoverynewsshort}} を使用して何を作成できるのかを示すデモを[ここ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://discovery-news-demo.mybluemix.net/){: new_window} で見ることができます。

英語版の Watson {{site.data.keyword.discoverynewsshort}} は {{site.data.keyword.discoveryshort}} ツールおよび API を介して使用できます。韓国語 (`collection_id`: `news-ko`) およびスペイン語 (`collection_id`: `news-es`) 版は、API を介してのみ使用できます。API を介したコレクションの照会について詳しくは、[API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection){: new_window} を参照してください。英語版の Watson {{site.data.keyword.discoverynewsshort}} の `collection_id` は `news-en` です。以前は、`collection_id` は `news` でした。以前の `collection_id` を使用している場合、引き続き機能しますが、新しいプロジェクト用に新しい `collection_id` に切り替えることをお勧めします。

**注:** Watson Discovery News の 1 回の照会で返される結果の最大数は `50` です。`50` を超える結果を返すには、追加の照会と `offset` パラメーターを使用してください。

{{site.data.keyword.discoveryshort}} 照会言語を使用する場合、{{site.data.keyword.discoverynewsshort}} 照会に相対日付範囲 (例: `crawl_date>=now-1month`) を組み込むことができます。有効な日付間隔値は、`second/seconds`、`minute/minutes`、`hour/hours`、`day/days`、`week/weeks`、`month/months`、および `year/years` です。`now` は `time_zone` パラメーターの影響を受けません。`UTC` タイム・ゾーンがデフォルトです。

ニュース記事はいくつかの報道機関に配信される可能性があり、{{site.data.keyword.discoverynewsfull}} はそれらの中から各記事を選出するため、記事が重複することがあります。これは、{{site.data.keyword.discoverynewsfull}} への照会の結果、複数の同じ記事またはほぼ同じ記事が返される可能性があることを意味します。重複排除を使用してこれを管理できます。このベータ機能について詳しくは、『[照会結果から重複する文書を除外](/docs/services/discovery/query-parameters.html#deduplication)』を参照してください。

## 複数コレクションの照会
{: #multiple-collections}

環境に複数のコレクションがある場合、それらのコレクションにまたがる結果が必要になることがあります。`environments` レベルで照会メソッド (`query`、`fields`、および `notices`) を使用すると、指定した複数のコレクションを照会することができます。現在のところ、複数のコレクションにまたがる照会は {{site.data.keyword.discoveryshort}} ツールでは使用できません。

`environments/{environment_id}/query` API メソッドを使用することによって、同じ環境にある複数のコレクションに対して照会を実行できます。複数のコレクションにまたがって照会するときには、以下を考慮してください。
-  このメソッドを使用するときには `collection_ids` パラメーターを指定する必要があります。`collection_ids` は、照会する対象の環境内のコレクションをコンマで区切ったリストです。
-  複数のコレクションを照会するときには、`passages` およびすべてのサブパラメーターはサポートされません。
-  各結果オブジェクトの一部として、新しいフィールド `collection_id` が返されます。このフィールドは、その結果が見つかったコレクションを指定します。
-  {{site.data.keyword.discoverynewsshort}} は、`system` 環境の一部であり、複数コレクションの照会に含めることはできません。
-  複数コレクションの照会では、照会内のすべてのコレクションがトレーニング済みであっても、照会のどの部分でも再ランキングは実行されません。

詳しくは、[複数コレクションの照会に関する API リファレンス![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-multi-collections){: new_window} を参照してください。

`environments/{environment_id}/notices` API メソッドを使用することによって、同じ環境にある複数のコレクションにわたって通知を確認できます。
-  このメソッドを使用するときには `collection_ids` パラメーターを指定する必要があります。`collection_ids` は、照会する対象の環境内のコレクションをコンマで区切ったリストです。
-  複数のコレクションを照会するときには、`passages` およびすべてのサブパラメーターはサポートされません。

詳しくは、[複数コレクションの通知に関する API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#collections-notices){: new_window} を参照してください。

`environments/{environment_id}/fields` API メソッドを使用することによって、同じ環境にある複数のコレクションにまたがって使用可能なフィールドを確認できます。詳しくは、[複数コレクションのフィールド照会に関する API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#multi-list-fields){: new_window} を参照してください。
