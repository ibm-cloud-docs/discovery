---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-09"

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

# 照会リファレンス

{{site.data.keyword.discoveryfull}} サービスは、照会を介して強力なコンテンツ検索機能を提供します。コンテンツがアップロードされ、{{site.data.keyword.discoveryshort}} サービスによってエンリッチされた後は、照会を作成したり、{{site.data.keyword.discoveryshort}} を独自プロジェクトに統合したり、{{site.data.keyword.watson}} Explorer Application Builder を使用してカスタム・アプリケーションを作成したりできます。{: shortdesc}

照会の作成について詳しくは、以下を参照してください。
- [照会入門](/docs/services/discovery/getting-started-query.html)
- [照会の概念](/docs/services/discovery/using.html)

## パラメーターの説明
{: #parameter-descriptions}

照会パラメーターにより、コレクションの検索、結果セットの識別、および結果セットの分析を実行できます。


| パラメーター | 説明 | 例 |
|:-------------------:|------------------------------------------------------------|--------------------------------|
|** 検索パラメーター **|  |  |
| [query](/docs/services/discovery/query-parameters.html#query) | ランク付けされる、一致する文書の照会言語検索。| `query=bees` |
| [filter](/docs/services/discovery/query-parameters.html#filter) | ランク付けされない、一致する文書の照会言語検索。| `filter=bees` |
| [natural_language_query](/docs/services/discovery/query-parameters.html#nlq) | ランクされる、一致する文書の自然言語検索 | `natural_language_query="How do bees fly"` |
| [aggregation](/docs/services/discovery/query-parameters.html#aggregation) | 結果セットの統計的照会 | `aggregation=term(enriched_text.entities.type)` |
| **構造パラメーター** | | |
| [count](/docs/services/discovery/query-parameters.html#count) | 返す `result` 文書の数。| `count=15` |
| [offset](/docs/services/discovery/query-parameters.html#offset) | 結果セットから `result` 文書を返す前に無視する結果の数 | `offset=100` |
| [return](/docs/services/discovery/query-parameters.html#return) | 返すフィールドのリスト | `return=title,url` |
| [sort](/docs/services/discovery/query-parameters.html#sort) | 結果セットのソート基準となるフィールド | `sort=enriched_text.sentiment.document.score` |
| [passages.fields](/docs/services/discovery/query-parameters.html#passages_fields) | パッセージの抽出元のフィールド | `passages=true&passages.fields=text,abstract,conclusion` |
| [passages.count](/docs/services/discovery/query-parameters.html#passages_count) | 返すパッセージの数 | `passages=true&passages.count=6` |
| [passages.characters](/docs/services/discovery/query-parameters.html#passages_characters) | パッセージの長さ | `passages=true&passages.characters=144` |
| [highlight](/docs/services/discovery/query-parameters.html#highlight) | 照会の一致を強調表示する | `highlight=true` |
| [deduplicate](/docs/services/discovery/query-parameters.html#deduplicate) | {{site.data.keyword.discoverynewsfull}} の返された結果を重複排除する | `deduplicate=true` |
| [deduplicate.field](/docs/services/discovery/query-parameters.html#deduplicated_field) | フィールドに基づいて、返された結果を重複排除する | `deduplicate.field=title` |
| [collection_ids](/docs/services/discovery/query-parameters.html#collection_ids) | 複数のコレクションを照会する | `collection_ids={1},{2},{3}` |

## 演算子
{: #operators}

演算子は、照会のさまざまな部分の分離文字です。使用可能な演算子は以下のとおりです。

| 演算子| 説明 | 例|
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [.](/docs/services/discovery/query-operators.html#delimiter) | JSON 区切り文字| `enriched_text.concepts.text` |
| [:](/docs/services/discovery/query-operators.html#includes) | 含む | `text:computer` |
| [::](/docs/services/discovery/query-operators.html#match) | 完全一致 | `title::Query building` |
| [:!](/docs/services/discovery/query-operators.html#notinclude) | 含まない | `text:!computer` |
| [::!](/docs/services/discovery/query-operators.html#notamatch) | 完全一致ではない | `title::!Query building` |
| [\\](/docs/services/discovery/query-operators.html#escape) | エスケープ文字 | `enriched_text.entitle.text:Trinidad \& Tobago` |
| [""](/docs/services/discovery/query-operators.html#phrase) | 句照会 | `enriched_text.concepts.text:"IBM Watson"` |
| [(), \[\]](/docs/services/discovery/query-operators.html#nestedquery) | ネストされたグループ| `filter-entities:(text:Turkey,type:Location)` |
| [<code>&#124;</code>](/docs/services/discovery/query-operators.html#or) | または | <code>query-enriched.entities.text:Google&#124;IBM</code> |
| [,](/docs/services/discovery/query-operators.html#and) | および | `query-enriched.entities.text:Google,IBM` |
| [<=, >=, >, <](/docs/services/discovery/query-operators.html#comparisons) | 数値比較 |  `enriched_text.sentiment.document.score>0.679`     |
| [^x](/docs/services/discovery/query-operators.html#multiplier) | スコア乗数 | `text:IBM^3` |
| [*](/docs/services/discovery/query-operators.html#wildcard) | ワイルドカード | `query-enriched_text.concepts.text:pre*` |
| [~n](/docs/services/discovery/query-operators.html#variation) | 文字列変化 | `query-enriched_text.entities.text:cat~1` |

## 集約
{: #aggregations}

集約は、一連のデータ値を返します。使用可能な集約は以下のとおりです。

| 集約 | 説明 | 例 |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [term](/docs/services/discovery/query-aggregations.html#term) | 同一の値のカウント | `term(enriched_text.concepts.text,count:10)` |
| [filter](/docs/services/discovery/query-aggregations.html#filter) | 定義されたパターンに従って結果セットをフィルターに掛ける | `filter(enriched_text.concepts.text:cloud computing)`
| [nested](/docs/services/discovery/query-aggregations.html#nested) | 集約を制限する | `nested(enriched_text.entities)` |
| [histogram](/docs/services/discovery/query-aggregations.html#histogram) | 区間に基づく分布 | `histogram(product.price,interval:1)` |
| [timeslice](/docs/services/discovery/query-aggregations.html#timeslice) | 時間に基づく分布 | `timeslice(last_modified,2day,America/New York)` |
| [top_hits](/docs/services/discovery/query-aggregations.html#top_hits) | 現在の集約で上位にランク付けされている結果文書 | `term(enriched_text.concepts.text).top_hits(10)` |
| [unique_count](/docs/services/discovery/query-aggregations.html#unique_count) | 集約内のフィールドの固有値の数 | `unique_count(enriched_text.entities.type)` |
| [max](/docs/services/discovery/query-aggregations.html#min) | 結果セット内の指定されたフィールドの最大値。 | `max(product.price)` |
| [min](/docs/services/discovery/query-aggregations.html#max) | 結果セット内の指定されたフィールドの最小値。 | `min(product.price)` |
| [average](/docs/services/discovery/query-aggregations.html#average) |結果セット内の指定されたフィールドの平均値。 | `average(product.price)` |
| [sum](/docs/services/discovery/query-aggregations.html#sum) | 結果セット内のすべてのフィールドの合計。| `sum(product.price)` |
