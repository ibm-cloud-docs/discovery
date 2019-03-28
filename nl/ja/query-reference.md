---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-04"

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

# 照会リファレンス
{: #query-reference}

{{site.data.keyword.discoveryfull}} サービスは、照会を介して強力なコンテンツ検索機能を提供します。 コンテンツがアップロードされ、{{site.data.keyword.discoveryshort}} サービスによってエンリッチされた後は、照会を作成したり、{{site.data.keyword.discoveryshort}} を独自プロジェクトに統合したり、{{site.data.keyword.watson}} Explorer Application Builder を使用してカスタム・アプリケーションを作成したりできます。
{: shortdesc}

照会の作成について詳しくは、以下を参照してください。
- [照会入門](/docs/services/discovery?topic=discovery-getting-started-with-querying#getting-started-with-querying)
- [照会の概念](/docs/services/discovery?topic=discovery-query-concepts#query-concepts)

## パラメーターの説明
{: #parameter-descriptions}

照会パラメーターにより、コレクションの検索、結果セットの識別、および結果セットの分析を実行できます。


| パラメーター | 説明 | 例 |
|:-------------------:|------------------------------------------------------------|--------------------------------|
|** 検索パラメーター **|  |  |
| [query](/docs/services/discovery?topic=discovery-query-parameters#query) | ランク付けされる、一致する文書の照会言語検索。 | `query=bees` |
| [filter](/docs/services/discovery?topic=discovery-query-parameters#filter) | ランク付けされない、一致する文書の照会言語検索。 | `filter=bees` |
| [natural_language_query](/docs/services/discovery?topic=discovery-query-parameters#nlq) | ランクされる、一致する文書の自然言語検索 | `natural_language_query="How do bees fly"` |
| [aggregation](/docs/services/discovery?topic=discovery-query-parameters#aggregation) | 結果セットの統計的照会 | `aggregation=term(enriched_text.entities.type)` |
| **構造パラメーター** | | |
| [count](/docs/services/discovery?topic=discovery-query-parameters#count) | 返す `result` 文書の数。 | `count=15` |
| [offset](/docs/services/discovery?topic=discovery-query-parameters#offset) | 結果セットから `result` 文書を返す前に無視する結果の数 | `offset=100` |
| [return](/docs/services/discovery?topic=discovery-query-parameters#return) | 返すフィールドのリスト | `return=title,url` |
| [sort](/docs/services/discovery?topic=discovery-query-parameters#sort) | 結果セットのソート基準となるフィールド | `sort=enriched_text.sentiment.document.score` |
| [bias](/docs/services/discovery?topic=discovery-query-parameters#bias) | 結果セットにバイアスをかけるためのフィールド | `bias=publication_date` |
| [passages.fields](/docs/services/discovery?topic=discovery-query-parameters#passages_fields) | パッセージの抽出元のフィールド | `passages=true&passages.fields=text,abstract,conclusion` |
| [passages.count](/docs/services/discovery?topic=discovery-query-parameters#passages_count) | 返すパッセージの数 | `passages=true&passages.count=6` |
| [passages.characters](/docs/services/discovery?topic=discovery-query-parameters#passages_characters) | パッセージの長さ | `passages=true&passages.characters=144` |
| [highlight](/docs/services/discovery?topic=discovery-query-parameters#highlight) | 照会の一致を強調表示する | `highlight=true` |
| [deduplicate](/docs/services/discovery?topic=discovery-query-parameters#deduplicate) | {{site.data.keyword.discoverynewsfull}} の返された結果を重複排除する | `deduplicate=true` |
| [deduplicate.field](/docs/services/discovery?topic=discovery-query-parameters#deduplicate_field) | フィールドに基づいて、返された結果を重複排除する | `deduplicate.field=title` |
| [collection_ids](/docs/services/discovery?topic=discovery-query-parameters#collection_ids) | 複数のコレクションを照会する | `collection_ids={1},{2},{3}` |
| [similar](/docs/services/discovery?topic=discovery-query-parameters#similar) | 類似文書の検索を可能にする | `similar=true` |
| [similar.document_ids](/docs/services/discovery?topic=discovery-query-parameters#similar_document_ids) | どの文書の類似文書を検索するか | `similar.document_ids={id1},{id2}` |
| [similar.fields](/docs/services/discovery?topic=discovery-query-parameters#similar_fields) | 類似文書の検索時に比較するフィールド | `similar.fields=text,title` |

### 照会に関する制限
{: #query-limitations}

以下を含んでいるフィールド名を照会することはできません。
- フィールド名のサフィックス内に数字 (`0 から 9`) (例: `extracted-content2`)
- `field_name` のプレフィックス内に文字 `_`、`+`、および `-` (例: `+extracted-content`)
- `field_name` 内に文字 `.`、`,`、および `:` (例: `new:extracted-content`)

## 演算子
{: #operators}

演算子は、照会のさまざまな部分の分離文字です。 使用可能な演算子は以下のとおりです。

| 演算子 | 説明 | 例 |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [.](/docs/services/discovery?topic=discovery-query-operators#delimiter) | JSON 区切り文字 | `enriched_text.concepts.text` |
| [:](/docs/services/discovery?topic=discovery-query-operators#includes) | 含む | `text:computer` |
| [::](/docs/services/discovery?topic=discovery-query-operators#match) | 完全一致 | `title::"Query building"` |
| [:!](/docs/services/discovery?topic=discovery-query-operators#notinclude) | 含まない | `text:!computer` |
| [::!](/docs/services/discovery?topic=discovery-query-operators#notamatch) | 完全一致ではない | `text::!winter` |
| [\\](/docs/services/discovery?topic=discovery-query-operators#escape) | エスケープ文字 | `title::"Dorothy said: \"There's no place like home\""` |
| [""](/docs/services/discovery?topic=discovery-query-operators#phrase) | 句照会 | `enriched_text.concepts.text:"IBM Watson"` |
| [(), \[\]](/docs/services/discovery?topic=discovery-query-operators#nestedquery) | ネストされたグループ | `filter-entities:(text:Turkey,type:Location)` |
| [<code>&#124;</code>](/docs/services/discovery?topic=discovery-query-operators#or) | または | <code>query-enriched.entities.text:Google&#124;IBM</code> |
| [,](/docs/services/discovery?topic=discovery-query-operators#and) | および | `query-enriched.entities.text:Google,IBM` |
| [<=, >=, >, <](/docs/services/discovery?topic=discovery-query-operators#comparisons) | 数値比較 |  `enriched_text.sentiment.document.score>0.679`     |
| [^x](/docs/services/discovery?topic=discovery-query-operators#multiplier) | スコア乗数 | `text:IBM^3` |
| [*](/docs/services/discovery?topic=discovery-query-operators#wildcard) | ワイルドカード | `query-enriched_text.concepts.text:pre*` |
| [~n](/docs/services/discovery?topic=discovery-query-operators#variation) | 文字列変化 | `query-enriched_text.entities.text:cat~1` |
| [:*](/docs/services/discovery?topic=discovery-query-operators#exists) | 存在する | `title:*` |
| [!*](/docs/services/discovery?topic=discovery-query-operators#dnexist) | 存在しない | `title!*` |

## 集約
{: #aggregations}

集約は、一連のデータ値を返します。 使用可能な集約は以下のとおりです。

| 集約 | 説明 | 例 |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [term](/docs/services/discovery?topic=discovery-query-aggregations#term) | 同一の値のカウント | `term(enriched_text.concepts.text,count:10)` |
| [filter](/docs/services/discovery?topic=discovery-query-aggregations#aggfilter) | 定義されたパターンに従って結果セットをフィルターに掛ける | `filter(enriched_text.concepts.text:cloud computing)`
| [nested](/docs/services/discovery?topic=discovery-query-aggregations#nested) | 集約を制限する | `nested(enriched_text.entities)` |
| [histogram](/docs/services/discovery?topic=discovery-query-aggregations#histogram) | 区間に基づく分布 | `histogram(product.price,interval:1)` |
| [timeslice](/docs/services/discovery?topic=discovery-query-aggregations#timeslice) | 時間に基づく分布 | `timeslice(last_modified,2day,America/New York)` |
| [top_hits](/docs/services/discovery?topic=discovery-query-aggregations#top_hits) | 現在の集約で上位にランク付けされている結果文書 | `term(enriched_text.concepts.text).top_hits(10)` |
| [unique_count](/docs/services/discovery?topic=discovery-query-aggregations#unique_count) | 集約内のフィールドの固有値の数 | `unique_count(enriched_text.entities.type)` |
| [max](/docs/services/discovery?topic=discovery-query-aggregations#max) | 結果セット内の指定されたフィールドの最大値。 | `max(product.price)` |
| [min](/docs/services/discovery?topic=discovery-query-aggregations#min) | 結果セット内の指定されたフィールドの最小値。 | `min(product.price)` |
| [average](/docs/services/discovery?topic=discovery-query-aggregations#average) |結果セット内の指定されたフィールドの平均値。 | `average(product.price)` |
| [sum](/docs/services/discovery?topic=discovery-query-aggregations#sum) | 結果セット内のすべてのフィールドの合計。 | `sum(product.price)` |
