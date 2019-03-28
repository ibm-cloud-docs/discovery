---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-09"

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

# 照会の集約
{: #query-aggregations}

集約は、一連のデータ値を返します。 使用可能な集約の完全リストについては、[照会リファレンス](/docs/services/discovery?topic=discovery-query-reference#aggregations)を参照してください。

## term
{: #term}

選択したエンリッチメントの上位の値を (スコア順および頻度順に) 返します。 すべてのエンリッチメントは有効な値です。 オプションで、`count` を使用して、返す用語の数を指定できます。 `count` パラメーターのデフォルト値は 10 です。 以下の例は、概念エンリッチメントでの最上位の値のフルテキストとエンリッチメントを返し、10 個の用語を返すことを指定します。

以下に例を示します。
```bash
term(enriched_text.concepts.text,count:10)
```
{: codeblock}

## filter
{: #aggfilter}

この修飾子が前に付いた集約照会の文書セットを絞り込みます。 以下の例は、フィルタリングでクラウド・コンピューティングの概念を含む文書セットを検出します。

以下に例を示します。
```bash
filter(enriched_text.concepts.text:"cloud computing")
```
{: codeblock}

## nested
{: #nested}

集約照会の前に nested を適用すると、集約は、指定された結果の領域に制限されます。 例えば、`nested(enriched_text.entities)` は、結果の `enriched_text.entities` コンポーネントのみが集約に使用されることを意味します。

以下に例を示します。
```bash
nested(enriched_text.entities)
```
{: codeblock}

## histogram
{: #histogram}

文書を分類するための数値区間セグメントを作成します。 単一の数値フィールドのフィールド値を使用して、カテゴリーを記述します。 ヒストグラムの作成に使用するフィールドは、数値型 (`integer`、`float`、`double`、または `date`) でなければなりません。 `string` などの非数値型はサポートされません。 例えば、"price": 1.30 は数値なので機能しますが、"price": "1.30" はストリングなので機能しません。 結果を分割するセクションのサイズを定義するには、`interval` 引数を使用します。 interval の値は、非負の整数でなければなりません。また、考えられるフィールド値をセグメント化する際に意味をなすように設定する必要があります。 例えば、データ・セットに複数のアイテムの価格 (例えば、“price”: 1.30、“price”: 1.99、および“price”: 2.99) が含まれている場合は、1 の interval を使用できます。こうすると、1 と 2 の間、および 2 と 3 の間にグループ化されているすべてが表示されます。100 の interval を使用することはおそらくありません。なぜなら、その場合は、すべてのデータが同じセグメントに入ることになるからです。 ヒストグラムは 10 進数の値を処理できますが、interval は整数でなければなりません。 以下の例に示すように、構文は `histogram(<field>,<interval>)` になります。

以下に例を示します。
```bash
histogram(product.price,interval:1)
```
{: codeblock}

## timeslice
{: #timeslice}

日付を使用して区間セグメントを作成する特殊なヒストグラム。 有効な日付間隔値は、`second/seconds`、`minute/minutes`、`hour/hours`、`day/days`、`week/weeks`、`month/months`、および `year/years` です。 構文は `timeslice(<field>,<interval>,<time_zone>)` です。 `timeslice` を使用するには、文書内の時間フィールドは `date` データ型で、[UNIX 時間 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://en.wikipedia.org/wiki/Unix_time){: new_window} フォーマットでなければなりません。 これらの両方の要件が満たされていない限り、`timeslice` パラメーターは正しく機能しません。 文書に、`1496228512` などの値を含む `date` フィールドが含まれている場合、タイム・スライスを作成できます。 値は、数値フォーマット (例えば、`float` や `double`) でなければならず、引用符で囲まれていてはなりません。 サービスは、テキスト内の日付と ISO 8601 フォーマットの日付を、`date` のデータ型ではなく、`string` のデータ型として処理します。 timeslice 集約で変則的な点を検出することができます。 追加情報については、[タイム・スライスの異常検出](#anomaly-detection)を参照してください。 以下の例は、"sales" ("product.sales") の値を、New York City タイム・ゾーンで 2 日間の間隔で返します。

以下に例を示します。
```bash
timeslice(product.sales,2day,America/New York)
```
{: codeblock}

### タイム・スライスの異常検出
{: #anomaly-detection}

オプションで、`timeslice` 集約の結果に異常検出を適用できます。 異常検出は、時系列の中で、通常と異なるデータ・ポイントを見つけ、後で検討するためにそれらにフラグを立てるために使用されます。 異常検出の使用例としては、クレジット・カード使用の急増の識別や、Watson Discovery News での特定のトピックに関する記事群の検索などがあります。

異常検出を適用するには、集約で以下の構文を使用します。

```bash
timeslice(field:<date>,interval:<interval>,anomaly:true)`
```
{: codeblock}

`timeslice` 集約で `anomaly:true` を指定すると、以下の 2 つの追加フィールド (例に示されている) が出力に含まれます。

  - 異常検出が実行されたことを示す `"anomaly": true`
  - 出力の結果配列で変則的なポイント内の `anomaly` フィールド。 anomaly フィールドには、変則的な動作の大きさを示す `float` データ型の値が含まれます。 anomaly フィールドの値が `1` に近づけば近づくほど、結果が変則的である可能性が高くなります。

  - `results` 配列内の各オブジェクトの `key` と `key_as_string` は、UNIX タイム・スタンプ (秒単位) に対応しています。
  - anomaly スコアは、元の照会にのみ関連しています。

```json
"type": "timeslice",
"field": "blekko.chrondate",
"interval": "1d",
"anomaly": true,
"results": [
  {
    "matching_results": 2933,
    "anomaly": 1,
    "key_as_string": "1496880000",
    "key": 1496880000000
  },
  {
    "matching_results": 3435,
    "anomaly": 1,
    "key_as_string": "1496966400",
    "key": 1496966400000
  },
  {
    "matching_results": 3692,
    "anomaly": 0.598226,
    "key_as_string": "1496016000",
    "key": 1496016000000
  },
  {
    "matching_results": 4551,
    "anomaly": 0.828498,
    "key_as_string": "1495411200",
    "key": 1495411200000
  },
  {
    "matching_results": 947,
    "key_as_string": "1489968000",
    "key": 1489968000000
  },
 ...
]
...
```
{: codeblock}

#### 異常検出の制限
{: #anomaly-limitations}

- 異常検出は、現在、最上位の `timeslice` 集約でのみ使用可能です。 下位 (ネストされた) 集約では使用できません。
- ある特定の `timeslice` 集約で、異常検出によって処理できるポイントの最大数は `1500` です。
- 異常検出によって処理できる最上位 timeslice 集約の最大数は `20` です。

<!--
#### Anomaly detection workflow

The following example workflow detects an anomaly for the text entity `London` and retrieves additional information about the anomalous datapoint.

  1. Timeslice aggregation: `query=entities.text:London&count=0&aggregation=timeslice(blekko.last_crawled,1day,anomaly:true)`
  1. Term aggregation to retrieve top keywords: `query=entities.text:London&count=0&aggregation=term(keywords.text,count:5)&filter=blekko.last_crawled>=1490140800,<=1490227200`
  1. Query to retrieve top enriched title: `query=entities.text:London,keywords.text:Westminster Bridge|police officer|people|Prime Minister Theresa|parliament&count=1&filter=blekko.last_crawled>=1490140800,<=1490227200&return=enrichedTitle.text`
  -->

## top_hits
{: #top_hits}

照会またはエンリッチメントのスコアによってランク付けされた文書を返します。 どの照会パラメーターまたは集約でも使用できます。 以下の例は、term 集約で上位 10 個のヒットを返します。

以下に例を示します。
```bash
term(enriched_text.concepts.text).top_hits(10)
```
{: codeblock}

## unique_count
{: #unique_count}

コレクション内の指定されたフィールドの固有インスタンスのカウントを返します。

例:
```bash
unique_count(enriched_text.keyword.text)
```
{: codeblock}

```bash
nested(enriched_text.entities).term(enriched_text.entities.text,count:3).unique_count(enriched_text.entities.type)
```
{: codeblock}

## max
{: #max}

一致するすべての文書において、指定されたフィールドの最高値を返します。

以下に例を示します。
```bash
max(product.price)
```
{: codeblock}

## min
{: #min}

一致するすべての文書において、指定されたフィールドの最低値を返します。

以下に例を示します。
```bash
min(product.price)
```
{: codeblock}

## average
{: #average}

一致するすべての文書において、指定されたフィールドの平均値を返します。

以下に例を示します。
```bash
average(product.price)
```
{: codeblock}

## sum
{: #sum}

一致するすべての文書において、指定されたフィールドの値を合計します。

以下に例を示します。
```bash
sum(product.price)
```
{: codeblock}
