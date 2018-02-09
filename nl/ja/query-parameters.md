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

# 照会パラメーター
{: #query-parameters}

{{site.data.keyword.discoveryfull}} サービスは、照会を介して強力なコンテンツ検索機能を提供します。コンテンツがアップロードされ、{{site.data.keyword.discoveryshort}} サービスによってエンリッチされた後は、照会を作成したり、{{site.data.keyword.discoveryshort}} を独自プロジェクトに統合したり、{{site.data.keyword.watson}} Explorer Application Builder を使用してカスタム・アプリケーションを作成したりできます。照会を開始するには、[照会の概念](/docs/services/discovery/using.html)を参照してください。パラメーターの完全リストについては、[照会リファレンス](/docs/services/discovery/query-reference.html#parameter-descriptions)を参照してください。
{: shortdesc}

**検索パラメーター **

検索パラメーターにより、コレクションの検索、結果セットの識別、および結果セットの分析を行うことができます。

**結果セット**とは、検索パラメーターの組み合わせ検索によって識別される文書のグループです。結果セットは、返された結果より大幅に大きい可能性があります。空の照会が実行された場合、結果セットは、コレクション内のすべての文書と等しくなります。

## query
{: #query}

照会検索は、データ・セット内のすべての文書を、すべてのエンリッチメントとフルテキストを含めて、関連性の高い順に返します。また、照会では、照会コンテンツに言及していない文書はすべて除外されます。これらの照会は、[{{site.data.keyword.discoveryshort}} Query Language](/docs/services/discovery/query-operators.html) を使用して作成されます。

## filter
{: #filter}

照会コンテンツに言及していないすべての文書を除外する、キャッシュ可能な照会。フィルター検索結果は、関連性の高い順に**返されません**。これらの照会は、[{{site.data.keyword.discoveryshort}} Query Language](/docs/services/discovery/query-operators.html) を使用して作成されます。

### filter パラメーターと query パラメーターの相違点
{: #filtervquery}

小規模なデータ・セットで同じ検索語をテストすると、`filter` パラメーターと `query` パラメーターが、(同一ではないとしても) 非常によく似た結果を返すことに気付く場合があります。しかし、これらの 2 つのパラメーターには相違点があります。

- filter パラメーターを単独で使用すると、検索結果は順不同で返されます。
- query パラメーターを単独で使用すると、検索結果は関連性の高い順に返されます。

大規模なデータ・セットでは、関連性の高い順に結果を返す必要がある場合は、`filter` パラメーターと `query` パラメーターを組み合わせてください。なぜなら、それらを一緒に使用するとパフォーマンスが向上するからです。この理由は、最初に `filter` パラメーターが実行されて結果をキャッシュに入れ、次に `query` パラメーターがそれらをランク付けするためです。filter と query を一緒に使用する例については、[結合された照会の作成](/docs/services/discovery/using.html#building-combined-queries)を参照してください。filter は集約でも使用できます。

`filter` パラメーターと、`aggregation` パラメーター、`query` パラメーター、または `natural_language_query` パラメーターの両方を含む照会を作成すると、`filter` パラメーターが最初に実行され、その後、`aggregation`、`query`、または `natural_language_query` のいずれかのパラメーターが並行して実行されます。

シンプルな照会、特に小規模なデータ・セットでの照会では、`filter` と `query` は、完全に同じ (または類似する) 結果を返すことがよくあります。`filter` 呼び出しと `query` 呼び出しが類似する結果を返し、応答が関連性の高い順に返されるかどうかは問題でない場合は、filter 呼び出しの方が速く、キャッシュに入れられるので、filter 呼び出しを使用することをお勧めします。キャッシングは、次回呼び出しを行ったときに、特に大規模なデータ・セットで、より速く応答を得られることを意味します。

## aggregation
{: #aggregation}

集約照会は、一連のデータ値 (例えば、上位のキーワードやエンティティーの全体的なセンチメントなど) に一致する文書数を返します。集約オプションの完全リストについては、[集約表](/docs/services/discovery/query-aggregations.html)を参照してください。これらの集約は、[{{site.data.keyword.discoveryshort}} Query Language](/docs/services/discovery/query-operators.html) を使用して作成されます。

## natural_language_query
{: #nlq}

自然言語照会は、会話型またはフリー・テキストのインターフェース (例えば、「IBM Watson in healthcare」など) でエンド・ユーザーから受け取ったかのように、自然言語で表された照会の実行を可能にします。このパラメーターは、入力全体を照会テキストとして使用します。演算子は認識**されません**。`natural_language_query` パラメーターは、パッセージ検索や関連性トレーニングなどの機能を可能にします。トレーニングされたコレクションは、自然言語照会の結果で `confidence` スコアを返します。詳しくは、[信頼度スコア](/docs/services/discovery/train-tooling.html#confidence)を参照してください。

**構造パラメーター**

構造パラメーターは、返される JSON 内の文書のコンテンツと編成を定義します。これには、返される結果の数、結果セット内のどこから文書の返却を開始するか、結果セットのソート方法、各文書でどのフィールドを返すか、重複する文書を削除するかどうか、および関連するパッセージを結果セットから抽出するかどうかが含まれます。構造パラメーターは、どの文書が結果セット全体の一部かということには影響を与えません。

## count
{: #count}

応答で返す文書の数。デフォルトは `10` です。1 つの任意の照会で `count` 値と `offset` 値を合わせた場合の最大値は `10000` です。

## offset
{: #offset}

最初にスキップする照会結果の数。例えば、返される結果の総数が 10 で、オフセットが 8 の場合は、最後の 2 つの結果が返されます。デフォルトは `0` です。1 つの任意の照会で `count` 値と `offset` 値を合わせた場合の最大値は `10000` です。

## return
{: #return}

返す文書階層の部分のコンマ区切りリスト。いずれの文書階層も有効な値です。

## sort
{: #sort}

文書内のソート対象フィールドのコンマ区切りリスト。オプションで、 フィールドに `-` (降順) または `+` (昇順) の接頭部を付けてソート方向を指定できます。昇順がデフォルトのソート方向です。

`sort` パラメーターは、現在、API でのみ使用可能です。ツールからは使用できません。

## passages
{: #passages}

サービスが、`natural_language_query` パラメーターを使用する照会によって返された文書から、最も関連性の高い一連のパッセージを返すかどうかを指定するブール値。パッセージは、照会によって返されたすべての文書から最適のテキスト・パッセージを判別する、高度な Watson アルゴリズムによって生成されます。デフォルトは、`false` です。

`passages` パラメーターは、プライベート・コレクションでのみ使用できます。{{site.data.keyword.discoverynewsfull}} コレクションでは使用できません。
{: tip}

{{site.data.keyword.discoveryshort}} は、文境界検出を使用して、文の先頭から始まり、末尾で終了するパッセージを返そうとします。このために、まず [`passages.characters` パラメーター](/docs/services/discovery/query-parameters.html#passages_characters) (デフォルトは `400`) で指定された大体の長さのパッセージを検索します。次に、完全な文を返すために、指定された長さの 2 倍の制限まで各パッセージを拡大します。`passages.characters` パラメーターが短いか、文書内の文が非常に長い場合、またはその両方の場合は、要求された長さの 2 倍を超えないと、完全な文を返すために十分近い文境界がない可能性があります。その場合、{{site.data.keyword.discoveryshort}} は `passages.characters` パラメーターの 2 倍の制限内に留まるため、返されるパッセージには文全体が含まれず、文の先頭、末尾、またはその両方が省略されることになります。

文境界の調整ではパッセージ・サイズが拡大されるため、平均パッセージ長さが大幅に増大されます。アプリケーションの画面スペースが限られている場合は、`passages.characters` に設定する値を小さくするか、{{site.data.keyword.discoveryshort}} によって返されるパッセージを切り捨てるか、またはその両方を実行できます。文境界検出は、サポートされるすべての言語で機能し、言語固有のロジックを使用します。

`passages` パラメーターは、以下の例に示すように、一致するパッセージ (`passage_text`) のほか、`score`、`document_id`、パッセージの抽出元フィールドの名前 (`field`)、およびフィールド内のパッセージ・テキストの先頭文字数と終了文字数 (`start_offset` と `end_offset`) を返します。この例の先頭には照会が示されています。

```bash
 curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-06-25&natural_language_query='Hybrid%20cloud%20companies'&passages=true"
```
{: pre}

返される JSON は、以下のフォーマットになります。

```json
 {
   "matching_results":2,
   "passages":[
     {
       "document_id":"ab7be56bcc9476493516b511169739f0",
       "passage_score":15.230205287402338,
       "passage_text":"a privately held company that provides hybrid cloud recovery, cloud migration and business continuity software for enterprise data centers and cloud infrastructure."
       "start_offset":120
       "end_offset":300
       "field":"text"       
     },
     {
       "passage_text":"Disaster Recovery Services for Hybrid Cloud</title></head>\n<body>\n\n\n<p>Published: Thu, 27 Oct 2016 07:01:21 GMT</p>\n"
       "passage_score":10.153470191601558,
       "document_id":"fbb5dcb4d8a6a29f572ebdeb6fbed20e",              
       "start_offset":70
       "end_offset":120
       "field":"html"
     },
  ...
```
{: codeblock}                        

### passages.fields
{: #passages_fields}

パッセージが抽出される索引内のフィールドのコンマ区切りリスト。このパラメーターが指定されていない場合は、すべての最上位フィールドが含まれます。

### passages.count
{: #passages_fields}

返されるパッセージの最大数。それが検出された総数の場合、検索で返される数はこれより少なくなります。デフォルトは `10` です。最大は `100` です。

### passages.characters
{: #passages_characters}

1 つの任意のパッセージの概算文字数。デフォルトは `400` です。最小は `50` です。最大は `2000` です。パッセージを文境界で開始して終了するために、返されるパッセージは、要求された長さの最大 2 倍 になる可能性があります (必要な場合)。

## highlight
{: #highlight}

返される出力が、`highlight` オブジェクトを含むかどうかを指定するブール値。このオブジェクトでは、キーはフィールド名で、値は、HTML の `*` タグで強調表示された照会一致テキストのセグメントを含む配列です。

以下の例に示すように、出力は、`highlight` オブジェクトを `enriched_text` オブジェクトの後にリストします。

```bash
curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-06-25&natural_language_query=Hybrid%20cloud%20companies&highlight=true"
```
{: pre}

返される JSON は、以下のフォーマットになります。

```json
{
   "highlight": {
     "extracted_metadata.title": [
       "IBM to Acquire Sanovi Technologies to Expand Disaster Recovery Services for <em>Hybrid</em> <em>Cloud</em>"
       ],
     "enriched_text.concepts.text": [
       "Privately held <em>company</em>",
       "<em>Cloud</em> computing"
       ],
     "text": [
       " Sanovi Technologies, a privately held <em>company</em> that provides <em>hybrid</em> <em>cloud</em> recovery, <em>cloud</em> migration",
       "IBM to Acquire Sanovi Technologies to Expand Disaster Recovery Services for <em>Hybrid</em> <em>Cloud</em>\n\nPublished",
       " undergoing digital and <em>hybrid</em> <em>cloud</em> transformation.\n\nURL: http://www.ibm.com/press/us/en/pressrelease/50837.wss",
       " and business continuity software for enterprise data centers and <em>cloud</em> infrastructure. Adding"
       ],
     "enriched_text.categories.label": [
       "/business and industrial/<em>company</em>/bankruptcy"
       ],
     "enriched_text.entities.type": [
       "<em>Company</em>"
       ],
     "html": [
       " Technologies, a privately held <em>company</em> that provides <em>hybrid</em> <em>cloud</em>\n recovery, <em>cloud</em> migration and business",
       " Disaster Recovery Services for <em>Hybrid</em> <em>Cloud</em></title></head>\n<body>\n\n\n<p>Published: Thu, 27 Oct 2016 07:01",
       " digital and <em>hybrid</em> <em>cloud</em> transformation.</p>\n<p>URL: http://www.ibm.com/press/us/en/pressrelease/50837.wss</p>\n\n\n\n</body></html>",
       " continuity software for \nenterprise data centers and <em>cloud</em> infrastructure. Adding these \ncapabilities"
       ]
   }
}
```
{: codeblock}

## deduplicate
{: #deduplicate_field}

 `title` フィールドに基づいて、重複する文書を {{site.data.keyword.discoverynewsfull}} コレクション照会結果から除外するベータ機能。[照会結果から重複する文書を除外](/docs/services/discovery/query-parameters.html#deduplication)を参照してください。

### deduplicate.field
{: #deduplicate_field}

指定された `{field}` に基づいて、重複する文書を照会結果から除外するベータ機能。[照会結果から重複する文書を除外](/docs/services/discovery/query-parameters.html#deduplication)を参照してください。

### 照会結果から重複する文書を除外
{: #deduplication}

{{site.data.keyword.discoverynewsfull}} コレクションを照会している場合、またはプライベート・データ・コレクションに複数のまったく同じ (またはほぼ同一の) 文書が含まれている場合は、文書の重複排除を使用してそれらのほとんどを照会結果から除外できます。

**注:** 文書の重複排除は、現在、ベータ機能としてのみサポートされています。詳細情報については、リリース・ノートの「[ベータ版フィーチャー](/docs/services/discovery/release-notes.html#beta-features)」を参照してください。

**注:** 各照会は個別に重複排除されるため、複数のオフセットでの重複排除はサポートされていません。

重複排除は、`passages` が抽出され、集約が計算された後に実行されます。したがって、`passages` パラメーターを照会に含めると、重複排除の前に、照会結果内のすべての文書からパッセージが返されます。集約と照会を一緒に実行すると、重複排除の前に、返されたすべての文書のデータが集約結果に含まれます。

重複排除は、返されたフィールドでのみ実行されます。`return=` を照会に指定することを選択する場合は、重複排除を実行するフィールドを含めてください。

重複排除を適用するには、照会で以下の構文を使用します。`{field}` は、重複排除を行うフィールドの名前に置き換えてください。指定する `{field}` は、`title` などのストリングでなければなりません。

```
&deduplicate.field={field}
```
{: codeblock}

重複排除を実行するとき、JSON 応答には `"duplicates_removed": x` が含まれます。ここで、`x` は、結果から削除する文書の数です。

#### Watson Discovery News での文書の重複排除

ニュース記事は複数の報道機関に配信されている可能性があり、{{site.data.keyword.discoverynewsfull}} はそのそれぞれを取得するため、記事が重複します。つまり、{{site.data.keyword.discoverynewsfull}} への照会で、照会結果に複数の同一またはほぼ同一の記事が返される可能性があります。重複排除を使用すると、ほとんどの重複する記事が検索照会から削除されます。

{{site.data.keyword.discoveryshort}} は、`title` フィールドで近似照合を使用して重複排除を行うため、フィールドを指定する必要はありません。

重複排除を適用するには、照会で以下のパラメーターを使用します。この照会は、自動的に {{site.data.keyword.discoverynewsfull}} 内の `title` フィールドで重複排除を行います。

```bash
&deduplicate=true
```
{: codeblock}

`title` 以外のフィールドで重複排除を行いたい場合は、照会で以下の構文を使用します。`{field}` は、重複排除を行うフィールドの名前に置き換えてください。指定する `{field}` はストリングでなければなりません。

```bash
&deduplicate.field={field}
```
{: codeblock}

## collection_ids
{: #collection_ids}

照会される同じ環境内のコレクションのコンマ区切りリスト。このパラメーターは、`environments/{environment_id}/query?` メソッドを使用しているときにのみ有効です。詳しくは、[複数コレクションの照会](/docs/services/discovery/using.html#multiple-collections)を参照してください。

```bash
&collection_ids={id1},{id2}
```
{: codeblock}
