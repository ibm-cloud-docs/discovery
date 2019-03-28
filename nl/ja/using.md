---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-01-22"

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

# 照会の概念
{: #query-concepts}

{{site.data.keyword.discoveryfull}} サービスは、強力なコンテンツ検索機能を提供します。 {{site.data.keyword.discoveryshort}} サービスによってコンテンツがアップロードされ、エンリッチされたら、照会を作成することができます。また、その後、{{site.data.keyword.discoveryshort}} をプロジェクトに統合したり、{{site.data.keyword.watson}} Explorer Application Builder を使用してカスタム・アプリケーションを作成したりできます。
{: shortdesc}

  コレクションのコンテンツはすべて固有であるため、作成する照会はコレクションによって異なります。
  {: tip}

照会またはフィルターを作成すると、{{site.data.keyword.discoveryshort}} は各結果を調べて、定義済みのパスを突き合わせます。 一致があれば、それらが結果セットに追加されます。 照会を作成するときには、あいまいにしたり、具体的にしたり、好きなように作成できます。 照会が具体的であるほど、結果は絞り込まれます。

パッセージ取り出しをオンにするオプションもあります。 パッセージは、照会から返される全文書から抽出される、関連する短い抜粋です。 的を絞ったこれらのパッセージは、コレクション内の文書の `text` フィールドから抽出されます。 デフォルトでは、1 つの照会に対して、それぞれ 400 文字ほどの最大 10 個のパッセージが返されます。 1 つの結果から抽出されるのは、最大 3 つまでのパッセージです。 `passages` パラメーターは、プライベート・コレクションにのみ使用可能であり、{{site.data.keyword.discoverynewsshort}} コレクションでは使用できません。 パッセージがどのように識別されるのかについて詳しくは、『[パッセージ](//docs/services/discovery?topic=discovery-query-parameters#passages)』を参照してください。

  {{site.data.keyword.discoveryshort}} ツールまたは API を使用して、自然言語照会 (例：「IBM Watson partnerships」) を作成できます。
  {: tip}

すべてのプライベート・コレクションは、ほとんどの場合、`confidence` スコアを照会結果に含めて返します。詳しくは、[信頼度スコア](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence)を参照してください。

{{site.data.keyword.discoveryshort}} では、英語、ドイツ語、フランス語、オランダ語、イタリア語、およびポルトガル語の各言語の特殊文字が含まれる照会結果が返されます。 例えば、`aqui` を照会した場合、`aqui` と <code>aqu&iacute;</code> の両方を結果で受け取ります。

複数のフィルターと複雑な集約を含んだ、より長くてより複雑な照会を作成できます。 このオプションは API のみで使用可能であり、照会の文字の長さ制限が 10,000 文字に増えます。 詳しくは、[長いコレクション照会 (Long collection queries) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery#long-collection-queries){: new_window} および [長い環境照会 (Long environment queries) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery#long-environment-queries){: new_window} を参照してください。

{{site.data.keyword.discoveryfull}} Knowledge Graph は、複数の文書にわたってエンティティーおよび関係を照会するための新しいエンドポイントを提供するベータ版フィーチャーです。 これには、コンテキスト・ベースの検索および関連性ランキングが含まれます。 詳しくは、[{{site.data.keyword.discoveryfull}} Knowledge Graph](/docs/services/discovery?topic=discovery-kg#kg) を参照してください。

照会の作成について詳しくは、以下を参照してください。
- [照会入門のチュートリアル](/docs/services/discovery?topic=discovery-getting-started-with-querying#getting-started-with-querying)
- [照会リファレンス](/docs/services/discovery?topic=discovery-query-reference#query-reference) ({{site.data.keyword.discoveryshort}} 照会言語で使用可能なパラメーター、演算子、および集約のリストが記載されています)

## Discovery データ・スキーマ
{: #discovery-schema}

まず、{{site.data.keyword.discoveryshort}} JSON について理解してください。 {{site.data.keyword.discoveryshort}} 照会言語を使用して照会を作成する方法を理解するには、{{site.data.keyword.discoveryshort}} がコレクション内の文書をエンリッチした後で生成する JSON についてよく知ることが必要です。 文書のデータ・スキーマを理解すれば、{{site.data.keyword.discoveryshort}} 照会言語で照会を作成するのが簡単になります。 そのためには 3 つの方法があります。

  1. {{site.data.keyword.discoveryshort}} ツールで、**「データの管理 (Manage data)」**画面を開き、{{site.data.keyword.IBM_notm}} プレス・リリースを含んでいるコレクションを選択します。 **「データ・スキーマの表示 (View Data Schema)」**ボタンをクリックします。 **「データ・スキーマの表示 (View data schema)」**画面に、文書別 (**「文書 (Document)」ビュー**) またはフィールド別 (**「コレクション (Collection)」ビュー**) の 2 つの方法のいずれかで、変換された文書中のフィールドと値が表示されます。 **「文書 (Document)」ビュー**には最大 50 の文書が表示されます。 **「コレクション (Collection)」ビュー**には、コレクション全体のフィールドが表示されます。

    **「コレクション (Collection)」ビュー**の `enriched_text` の下で、コレクションに適用したエンリッチメントを調べることができます。`categories`、`concepts`、`entities`、および `sentiment` をクリックすると、Watson の洞察によってコレクションがどのようにエンリッチされたのかを確認できます。

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

  フィールドを評価する演算子 (`<=`、`>=`、`<`、`>`) は、値として `number` または `date` を必要とします。 値を引用符で囲むと、その値は常に `string` になります。 したがって、`score>=0.5` は有効な照会ですが、`score>="0.5"` は有効ではありません。 演算子の完全なリストについては、[照会演算子](/docs/services/discovery?topic=discovery-query-operators#query-operators)を参照してください。
  {: tip}

考慮事項

- どのようなときにエンティティー、コンセプト、キーワードの照会を行えばよいのかがよく分からない場合、『[エンティティー、概念、およびキーワードの違いについて](/docs/services/discovery?topic=discovery-configservice#udbeck)』を参照してください。

- **注:** **「照会の実行 (Run query)」**をクリックした後に**「JSON」**タブを開くと、照会の強調表示がデフォルトでオンになっていることがわかります。 これによって、照会結果に `highlight` フィールドが追加されます。 `highlight` フィールド内で、照会に一致する単語は HTML `<em>` (強調表示) タグで囲まれます。 詳しくは、『[照会パラメーター](/docs/services/discovery?topic=discovery-query-parameters#highlight)』を参照してください。

## 結合された照会の作成
{: #building-combined-queries}

複数の照会パラメーターを結合することで、さらに的を絞った照会を作成できます。 例えば、`filter` パラメーターと `query` パラメーターの両方を一緒に使用できます。 フィルターと照会の違いについて詳しくは、『[filter パラメーターと query パラメーターの相違点](/docs/services/discovery?topic=discovery-query-parameters#filtervquery)』を参照してください。

## 集約の組み立て方
{: #structure-aggregation}

集約は、データ値の集合 (例えば、上位キーワード、エンティティーのセンチメント全体など) を返します。 集約オプションの完全なリストについては、『[集約](/docs/services/discovery?topic=discovery-query-reference#aggregations)』を参照してください。

![集約照会の構造の例](images/aggregation_structure.png)

この例の集約では、コレクション内のすべての `concepts` が検出されます。
この照会での区切り文字は `.` であり、演算子は `()` です。{{site.data.keyword.discoveryshort}} 照会言語で使用可能なその他の演算子について詳しくは、[照会演算子](/docs/services/discovery?topic=discovery-query-operators#query-operators)を参照してください。

### 集約照会の例
{: #example-aggregations}

{{site.data.keyword.discoverynewsshort}} での結果を集約する方法には、上位値、合計、最小、最大、平均、タイム・スライス、ヒストグラムなど、数種類の方法があります。 フィルターを追加したり、集約をネストしたりもできます。

#### 集約のフィルタリング
{: #filter-aggregations}

次の集約の例は、{{site.data.keyword.discoverynewsshort}} で見つかった Pittsburgh Steelers (フットボール・チーム) に関する記事の数と、それらの結果のうちセンチメントが `positive`、`negative`、または `neutral` である数を返します。

- `filter(enriched_text.entities.text:"Pittsburgh Steelers").term(enriched_text.sentiment.document.label,count:3)`


次の集約の例は、最初に {{site.data.keyword.discoverynewsshort}} 内の記事集合の絞り込み (フィルター) によって `twitter` のエンティティー・テキストを含む記事だけにし、次に、それらの記事を文書センチメント・タイプ別に分けます。 最上位の 3 つの文書センチメント・タイプ (`positive`、`negative`、`neutral`) のみが返されます。

- `filter(enriched_text.entities.text:twitter).term(enriched_text.sentiment.document.label,count:3)`

#### ネストされた集約
{: #nested-aggregations}

集約の前に `nested` を追加すると、集約は指定された結果領域に制限されます。 例えば、`nested(enriched_text.entities)` は、結果の `enriched_text.entities` コンポーネントのみが集約に使用されることを意味します。

以下の 2 つの照会の違いを見ると、これがよく分かります。
- `filter(enriched_text.entities.disambiguation.subtype::City)` - この集約は、タイプ `City` の `entity` を 1 つ以上含んでいる*結果* の数をカウントします。
- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City)` - この集約は、タイプ `City` の `entity` のインスタンスの数を結果内でカウントします。  

これに加えて後続の演算があれば、集約に使用できる結果セットはさらに限定されます。 以下に例を示します。

- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City)` は、`subtype::City` のエンティティーのみが集約されることを意味します。
- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City).term(enriched_text.entities.text,count:3)` は、サブタイプが `City` の上位 3 つのエンティティーを集約します。
- `filter(enriched_text.entities.disambiguation.subtype::City).term(enriched_text.entities.text,count:3)` は、結果にサブタイプ `City` のエンティティーが 1 つ以上含まれている、上位 3 つのエンティティーを返します。

## Watson Discovery News の照会
{: #querying-news}

{{site.data.keyword.discoveryshort}} には、コグニティブな洞察によって事前にエンリッチされた公開データ・セット、{{site.data.keyword.discoverynewsshort}} も含まれています。 このコレクションについて詳しくは、[Watson Discovery News](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) を参照してください。

自然言語照会 (例: 「IBM Watson partnerships」) または {{site.data.keyword.discoveryshort}} 照会言語を使用してこのコレクションを照会できます。 自然言語照会について詳しくは、『[自然言語照会](/docs/services/discovery?topic=discovery-query-parameters#nlq)』を参照してください。

{{site.data.keyword.discoverynewsshort}} の構成を調整したり、トレーニングを行ったり、{{site.data.keyword.discoverynewsshort}} コレクションに文書を追加したりすることはできません。 {{site.data.keyword.discoverynewsshort}} を使用して何を作成できるのかを示すデモを[ここ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://discovery-news-demo.ng.bluemix.net/){: new_window} で見ることができます。

英語、韓国語、ドイツ語、スペイン語、および日本語の {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} コレクションを {{site.data.keyword.discoveryshort}} ツールと API の両方で使用できます。

{{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} ツールのデフォルト言語は、英語です。 言語を切り替えるには、まず、![データの管理](/images/icon_yourData.png) アイコンをクリックし、次にドロップダウンから適切な言語を選択します。

API を介したコレクションの照会について詳しくは、[API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window} を参照してください。 英語版の Watson {{site.data.keyword.discoverynewsshort}} の `collection_id` は `news-en` です。 以前は、`collection_id` は `news` でした。以前の `collection_id` を使用している場合、引き続き機能しますが、新しいプロジェクト用に新しい `collection_id` に切り替えることをお勧めします。 韓国語コレクションの `collection_id` は `news-ko`、スペイン語の `collection_id` は `news-es`、ドイツ語の `collection_id` は `news-de`、日本語の `collection_id` は `news-ja` です。

{{site.data.keyword.discoverynewsfull}} 照会では、`text` JSON フィールドに各記事の最初の 50 ワードが表示されます。

{{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} の 1 回の照会で返される結果の最大数は `50` です。 `50` を超える結果を返すには、追加の照会と `offset` パラメーターを使用してください。

{{site.data.keyword.discoveryshort}} 照会言語を使用する場合、{{site.data.keyword.discoverynewsshort}} 照会に相対日付範囲 (例: `crawl_date>=now-1month`) を組み込むことができます。 有効な日付間隔値は、`second/seconds`、`minute/minutes`、`hour/hours`、`day/days`、`week/weeks`、`month/months`、および `year/years` です。 `now` は `time_zone` パラメーターの影響を受けません。`UTC` タイム・ゾーンがデフォルトです。

以下の例では、特定の日付範囲内でキーワードを照会します。 タイム・ゾーン情報は不要です。
- `enriched_text.keywords.text:"olympics", publication_date<=2018-02-15T00:00:00Z, publication_date>=2018-02-01T00:00:00Z`

ニュース記事はいくつかの報道機関に配信される可能性があり、{{site.data.keyword.discoverynewsfull}} はそれらの中から各記事を選出するため、記事が重複することがあります。 これは、{{site.data.keyword.discoverynewsfull}} への照会の結果、複数の同じ記事またはほぼ同じ記事が返される可能性があることを意味します。 重複排除を使用してこれを管理できます。 このベータ機能について詳しくは、[照会結果から重複する文書を除外](/docs/services/discovery?topic=discovery-query-parameters#deduplication)を参照してください。

## 複数コレクションの照会
{: #multiple-collections}

環境に複数のコレクションがある場合、それらのコレクションにまたがる結果が必要になることがあります。 `environments` レベルで照会メソッド (`query`、`fields`、および `notices`) を使用すると、指定した複数のコレクションを照会することができます。 現在のところ、複数のコレクションにまたがる照会は {{site.data.keyword.discoveryshort}} ツールでは使用できません。

`environments/{environment_id}/query` API メソッドを使用することによって、同じ環境にある複数のコレクションに対して照会を実行できます。 複数のコレクションにまたがって照会するときには、以下を考慮してください。
-  このメソッドを使用するときには `collection_ids` パラメーターを指定する必要があります。 `collection_ids` は、照会する対象の環境内のコレクションをコンマで区切ったリストです。
-  `passages` は、複数のコレクションを照会する場合にサポートされます。
-  `collection_id` は、各結果オブジェクトの一部として返されます。 このフィールドは、その結果が見つかったコレクションを指定します。
-  {{site.data.keyword.discoverynewsshort}} は、`system` 環境の一部であり、複数コレクションの照会に含めることはできません。
-  個別のコレクション関連性のトレーニングは、複数のコレクションを照会する際の結果のランキングには影響しません。 複数のコレクションを照会するときに返される結果を再ランク付けするには、[Continuous Relevancy Training](/docs/services/discovery?topic=discovery-crt#crt) を実装してください。
-  複数コレクションの照会では、照会内のすべてのコレクションがトレーニング済みであっても、照会のどの部分でも再ランキングは実行されません。

詳しくは、[複数コレクションの照会に関する API リファレンス![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery#query-documents-in-multiple-collections){: new_window} を参照してください。

`environments/{environment_id}/notices` API メソッドを使用することによって、同じ環境にある複数のコレクションにわたって通知を確認できます。
-  このメソッドを使用するときには `collection_ids` パラメーターを指定する必要があります。 `collection_ids` は、照会する対象の環境内のコレクションをコンマで区切ったリストです。
-  `passages` は、複数のコレクションを照会する場合にサポートされます。

詳しくは、[複数コレクションの通知に関する API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery#get-collection-details){: new_window} を参照してください。

`environments/{environment_id}/fields` API メソッドを使用することによって、同じ環境にある複数のコレクションにまたがって使用可能なフィールドを確認できます。 詳しくは、[複数コレクションのフィールド照会に関する API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery#list-fields-across-collections){: new_window} を参照してください。

## 照会拡張
{: #query-expansion}

{{site.data.keyword.discoveryshort}} API を使用して照会拡張用語のリストをアップロードすることで、照会の適用範囲を、完全一致を超えた範囲まで拡張できます。例えば、「car」に対する照会を「automobile」や「vehicle」まで含めるように拡張できます。照会拡張用語は、通常、一般的な用語の同義語、対義語、または典型的なミススペルです。

以下の 2 つのタイプの拡張を定義できます。
-  **両方向** - 各 `expanded_term` が拡張され、拡張されたすべての用語が組み込まれます。 例えば、`car` の照会は、`car OR automobile OR vehicle` に拡張されます。
-  **単一方向** - 照会内の `input_terms` が `expanded_terms` に置き換えられます。例えば、`banana` の照会は、`plaintain` と `fruit` に拡張されます。`input_terms` は、結果として生成される照会の一部としては使用されません。 前の `banana` の例では、照会 `banana` は、`plantain` または `fruit` に変換され、元の用語は含まれません。

以下のファイルを、照会拡張リストを作成する際の開始点として使用できます。
<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/expansions.json" download>expansions.json <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン"></a>。 このファイルを変更して、カスタムの照会拡張リストを作成できます。

両方向の例:
```JSON
 {
   "expansions": [
     {
       "expanded_terms": [
         "car",
         "automobile",
         "vehicle"
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

照会拡張に関する注意

-  複数トークンの照会拡張はサポートされていません。
-  照会拡張は、プライベート・コレクションにのみ使用可能です。 使用可能な `expansions` 配列 (両方向と単一方向の配列の合計) および用語 (`input_terms` と `expanded_terms` を加算した合計) の数は、プランによって異なります。 詳しくは、[Discovery の料金プラン](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)を参照してください。 **注:** すべての照会用語 (`input_terms` と `expanded_terms` の両方) は、それぞれが 1 つの用語としてカウントされます。 この例の場合、`expansions` 配列内に 2 つのオブジェクトと、7 つの用語ストリングが含まれています。

```JSON
 {
   "expansions": [
     {
      "input_terms": [
         "ibm"
       ],
      "expanded_terms": [
         "ibm",
         "watson"
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

-  コレクションごとにアップロードできる照会拡張リストは 1 つのみです。2 番目の拡張リストがアップロードされると、最初のリストは置き換えられます。
-  `input_terms` および `expanded_terms` はすべて小文字でなければなりません。 小文字の用語は大文字に拡張されます。
-  照会拡張リストは JSON で記述する必要があります。
-  照会拡張を無効にするには、照会拡張リストを削除します。
-  現在、{{site.data.keyword.discoveryshort}} ツールを使用して照会拡張リストをアップロードおよび削除することはできません。その際は、{{site.data.keyword.discoveryshort}} API を使用してください。
-  照会拡張は、`query` メソッドおよび `multiple collection query` メソッドに対して実行されます。 照会拡張は、Knowledge Graph 照会では実行されません。
-  拡張の各セットは、1 つのコレクションに関連付けられます。 [複数のコレクション](/docs/services/discovery?topic=discovery-query-concepts#multiple-collections)にまたがって照会する場合は、各コレクションが個別に拡張されます。
-  照会拡張は、索引付け時でなく、照会時に適用されます。したがって、文書を再取り込みすることなく、照会拡張リストを更新できます。
-  文書がコレクションに取り込まれるのと同じときに、照会拡張リストをアップロードしたり削除したりしないでください。 そうすると、その短い期間、索引が使用不可になる可能性があります。

照会拡張ファイルをアップロードおよび削除するための API コマンドについては、[照会拡張に関する API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery#get-the-expansion-list){: new_window} を参照してください。

## ストップワードの定義
{: #stopwords}

ストップワードとは、ほとんど意味がないので照会から除外するワードのことです。例えば、`a、an、the` などです。ストップワード・リストに一般的なワードを追加すると、自然言語照会に対する結果の関連性も向上します。 

いくつかの言語では、{{site.data.keyword.discoveryshort}} は照会時にデフォルトのストップワードのリストを適用します。しかし、ストップワードのカスタム・リストを定義してアップロードすれば、デフォルトのリストをオーバーライドできます。{{site.data.keyword.discoveryshort}} は、プライベート・コレクションに指定されている言語に基づいて、デフォルトまたはカスタムの適切なストップワード・リストをそのコレクションに適用します。 

カスタム・ストップワード・リストは、改行で区切られた `txt` ファイルで指定する必要があります。以下は、カスタム・ストップワード・リストの例です。

```
ibm
watson
a
an
the
what
how
when
can
should
```
このリストには、英語のすべてのデフォルト・ストップワードが含まれています (<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/custom_stopwords_en.txt" download>custom_stopwords_en.txt <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン"></a>)。これを、英語のカスタム・ストップワード・リストを作成する際の開始点として使用できます。`a` や `the` などの非常に一般的な用語を含まないカスタム・ストップワード・リストを作成すると、照会のパフォーマンスが低下する可能性があるため、 こうしたワードはカスタム・ストップワード・リストに入れることをお勧めします。以下は、サポートされている他のいくつかの言語のストップワード・リストです。すべてのリストに、その言語のデフォルト・ストップワードが含まれています。

-  オランダ語: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/custom_stopwords_nl.txt" download>custom_stopwords_nl.txt <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン"></a>。
-  フランス語: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/custom_stopwords_fr.txt" download>custom_stopwords_fr.txt <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン"></a>。
-  ドイツ語: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/custom_stopwords_de.txt" download>custom_stopwords_de.txt <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン"></a>。 
-  イタリア語: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/custom_stopwords_it.txt" download>custom_stopwords_it.txt <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン"></a>。
-  日本語: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/custom_stopwords_ja.txt" download>custom_stopwords_ja.txt <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン"></a>。
-  スペイン語: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/custom_stopwords_es.txt" download>custom_stopwords_es.txt <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン"></a>。 

{{site.data.keyword.discoveryshort}} でサポートされている言語のリストについては、[言語サポート](/docs/services/discovery?topic=discovery-language-support#supported-languages)を参照してください。サポートされている言語の中には、デフォルト・ストップワード・リストがないものがあります。

カスタム・ストップワード・リストをアップロードおよび削除するための API コマンドについては、[ストップワード API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery#create-stopword-list){: new_window} を参照してください。

ストップワードに関する注意:

-  現在、{{site.data.keyword.discoveryshort}} ツールを使用してカスタム・ストップワード・リストをアップロードおよび削除することはできません。その際は、{{site.data.keyword.discoveryshort}} API を使用してください。 [ストップワード API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery#create-stopword-list){: new_window} を参照してください。
-  カスタム・ストップワード・リストのアップロードは、`拡張`プランと`プレミアム`・プランのプライベート・コレクションでのみ行えます。
-  カスタム・ストップワード・リスト `txt` ファイルのサイズ制限は 100 万文字です。ただし、多数の用語を含むカスタム・ストップワード・リストをアップロードすると、検索の精度が低下する可能性があります。ワード数は、言語、文書の内容、および選択したワードによって異なります。ベスト・プラクティスとして、リストするストップワード数の合計は `200` ワード未満にすることをお勧めします。 
-  コレクションごとにアップロードできるカスタム・ストップワード・リストは 1 つのみです。2 番目のカスタム・ストップワード・リストがアップロードされると、最初のリストは置き換えられます。
-  ストップワードはすべて小文字でなければなりません。 
-  カスタム・ストップワード・リストを無効にするには、カスタム・ストップワード・リストを削除します。
-  文書がコレクションに取り込まれるのと同じときに、カスタム・ストップワード・リストをアップロードしたり削除したりしないでください。 そうすると、その短い期間、索引が使用不可になる可能性があります。
-  ストップワードは、索引作成時にも照会時にも除外されます。ベスト・プラクティスとして、文書をアップロードする前にカスタム・ストップワード・リストをアップロードすることをお勧めします。
   - デフォルト・ストップワードを使用して文書の索引を既に作成した後にカスタム・ストップワード・リストを追加した場合でも、新しいストップワードが索引に組み込まれます。その場合、それらの新しいストップワードは、照会に含まれていても照会時に除外されます。
   - 過去にストップワードであったけれども、後でカスタム・ストップワード・リストから削除されたワードをユーザーが検索した場合は、元のストップワードと一致する文書は検索されません。そのワードは索引作成時には除外されていたからです。この問題を解決するには、更新したカスタム・ストップワード・リストを使用して索引を作成するために、コレクション内の文書を削除し、すべての文書を再びアップロードしてください。
-  ストップワードの各セットは、1 つのコレクションに関連付けられます。 複数のコレクションにまたがって照会する場合、コレクションごとに、そのコレクションに関連付けられているカスタム・ストップワード・リストが使用されます。
- カスタム・ストップワード・リストを大幅に変更した場合は、更新したカスタム・ストップワード・リストを使用して索引を作成するために、コレクション内の文書を削除し、すべての文書を再びアップロードする必要があります。


## カスタムのトークン化辞書の作成
{: #tokenization}

トークン化は、テキストをトークンと呼ばれる単位に分割します。 コレクションには標準のトークン化辞書が適用されますが、カスタムのトークン化辞書をアップロードすることで、ドメインまたは言語の検索精度を高めることができます。 カスタム辞書は標準辞書をオーバーライドします。 辞書は、{{site.data.keyword.discoveryshort}} API を使用してアップロードできます。 

トークン化ファイルをアップロードおよび削除するための API コマンドについては、[トークン化に関する API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery#create-tokenization-dictionary){: new_window} を参照してください。 

**注:** 現在、この機能は、日本語コレクションでのみ使用可能です。 

以下の例で、**text** は、検出されたときにトークン化される句で、**tokens** は、**text** が分割された後の単語です (それぞれ個別に定義する必要があります)。**readings** には、異なる文字セットで表されるトークンのバージョンがリストされ、**part_of_speech** はトークンが表す品詞です。

このカスタム辞書を使用して、`ネコ`というテキストを検索した場合、検索結果には、`ネコ`のみを含んだテキストに加えて、`すしネコ`を含んでいるテキストも組み込まれます。

```
{ "tokenization_rules":
  [
     {
      "text":"すし",
      "tokens":[
        "すし"
      ],
      "readings":[
        "寿司"
      ],
      "part_of_speech":"カスタム名詞"
    },
    {
      "text":"ネコ",
      "tokens":[
        "ネコ"
      ],
      "readings":[
        "ネコ"
      ],
      "part_of_speech":"カスタム名詞"
    }
```

このカスタム辞書では、単一トークンを含んだルールを作成することができます。この例の場合、`ibm発見`は単一トークンとしてトークン化され、それ以上小さい単位には分割されません。

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

-  トークン化は、索引付けと照会時の両方で行われます。
-  トークンは個別に定義する必要があります。
-  標準トークン化辞書は、すべてのコレクションに使用されます。 コレクションが既にその辞書を使用して索引付けされている場合は、カスタムのトークン化辞書をアップロードした後に、そのコレクション内に文書を再取り込みする必要があります。
-  トークン化辞書のアップロードは、`拡張`プランと`プレミアム`・プランのプライベート・コレクションでのみ行えます。 
-  コレクションごとにアップロードできるトークン化辞書は 1 つのみです。2 番目のトークン化辞書がアップロードされると、最初の辞書は置き換えられます。 そのコレクションに既に文書が含まれていた場合、新しいカスタムのトークン化辞書を適用するためには、それらの文書を再取り込みする必要があります。
-  カスタムのトークン化辞書は、JSON で記述する必要があります。サンプル・ファイル名は `custom_tokenization_dictionary.json` です。
-  カスタムのトークン化辞書はすべて小文字でなければなりません。
-  トークン化を無効にするには、トークン化辞書を削除し、文書を再取り込みします。
-  現在、{{site.data.keyword.discoveryshort}} ツールを使用してトークン化辞書をアップロードまたは削除することはできません。その際は、{{site.data.keyword.discoveryshort}} API を使用してください。
-  トークン化は、`query` メソッドおよび `multiple collection query` メソッドに対して実行されます。 トークン化は、Knowledge Graph 照会では実行されません。
-  各トークン化辞書は、1 つのコレクションに関連付けられます。 [複数のコレクション](/docs/services/discovery?topic=discovery-query-concepts#multiple-collections)にまたがって照会する場合は、各コレクションが個別にトークン化されます。
-  文書がコレクションに取り込まれるのと同じときに、トークン化辞書をアップロードしたり削除したりしないでください。 

## 文書類似性
{: #doc-similarity}

文書類似性照会では、現在表示されている文書に似た他の文書が検索されます。例えば、ある製品のマニュアルを表示しているコール・センターのオペレーターが、文書類似性を使用して、似た特徴を持つその他の文書を検索できます。 `similar.document_ids` を使用して類似文書を照会でき、オプションで、追加の `similar.fields` を指定することにより類似性を詳細化することができます。

文書類似性は、元の文書から最も関連性の高い 25 の用語を抽出し、類似した関連用語を持つ文書を検索することによって判別されます。

`similar.document_ids` による照会の例を以下に示します (複数の `similar.document_ids` を指定する場合、コンマの後にスペースは入れないでください)。

`curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&similar.document_ids=4107b6f1-5d3f-4bea-bbcf-fb05bbf960b1,6057k6d1-7d7k-6aeh-cfbb-kj98ssf786c2"`

`similar.fields` を追加した照会の例を以下に示します。

`curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&similar.document_ids=4107b6f1-5d3f-4bea-bbcf-fb05bbf960b1&similar.fields=title&return=title&count=100"`

詳しくは、[文書類似性に関する API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window} および[照会パラメーター](/docs/services/discovery?topic=discovery-query-parameters#similar)を参照してください。
