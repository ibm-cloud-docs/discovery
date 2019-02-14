---

copyright:
years: 2018
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

# 出力スキーマについて
{: #output_schema}

「要素の分類」を使用して文書が取り込まれると、バージョン日付 `2018-10-15` 以降の場合、本サービスは以下のスキーマの JSON 出力を提供します。出力は、`enriched_html_elements` オブジェクト内に組み込まれます。 

```
{
  "document": {
    "title": string,
    "html": string,
    "hash": string
  },
  "model_id" : string,
  "model_version" : string,  
  "elements": [
    {
      "location": { 
        "begin": int,
        "end": int
      },
      "text": string,
      "types": [
        {
          "label": { "nature": string, "party": string },
          "provenance_ids": [string, string, ...]
            ...
          ]
        }
        ...
      ],
      "categories": [
        {
          "label": string,
          "provenance_ids": [string, string, ...]
        }
        ...
      ],
      "attributes": [
        {
      	  "type": string,
          "text": string,
          "location": { "begin": int, "end": int }
         }
      ]
    }
    ...
  ],
  "tables": [
    {
      "location" : {
        "begin" : int,
        "end" : int
      },
      "text": string,
      "section_title": {
        "text": string,
        "location": {
          "begin" : int,
          "end" : int
        }
      },
      "table_headers" : [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int
        },
        ...
      ],
      "column_headers" : [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "text_normalized" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int
        },
        ...
      ],
      "row_headers" : [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "text_normalized" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int
        },
        ...
      ],
      "body_cells" : [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int,
          "row_header_ids": [ string ],
          "row_header_texts": [ string ],
          "row_header_texts_normalized": [ string ],
          "column_header_ids": [ string ],
          "column_header_texts": [ string ],
          "column_header_texts_normalized": [ string ]
        },
        ...
      ]
    },
    ...
  ],
  "document_structure": {
    "section_titles": [
      {
        "text": string,
        "location": {
          "begin": int,
          "end": int
        },
        "level": int
        "element_locations": [
          {
            "begin": int,
            "end": int
          },
          ...
        ]
      },
      ...
    ],
    "leading_sentences": [
      {
        "text": string,
        "location": {
          "begin": int,
          "end": int
        },
        "element_locations": [
          {
            "begin": int,
            "end": int
          },
          ...
        ]
      },
      ...
    ]
  },
  "parties": [
    {
      "party": string,
      "role": string,
      "addresses": [
        {
          "text": string,
          "location": {
            "begin": int,
            "end": int
          }
        },
        ...
      ],
      "contacts": [
        {
          "name": string,
          "role": string 
        },
        ...
      ]
    },
    ...
  ],
  "effective_dates": [
    {
      "text": string,
      "location": { "begin": int, "end": int }
     },
     ...
  ],
  "contract_amounts": [
    {
      "text": string,
      "location": { "begin": int, "end": int }
    },
    ...
  ]
}
```

スキーマは次のように配置されます。

  - `document`: 文書に関する以下の基本情報をリストしたオブジェクト。
    - `title`: 文書のタイトル (検出された場合)。
    - `html`: HTML 形式で表される、入力文書のフルテキスト。
    - `hash`: 入力文書の MD5 ハッシュ。
  - `model_id`: 文書の分類に使用される分析モデル。デフォルトは、`contracts` です。 
  - `model_version`: `model_id` パラメーターの値によって指定される分析モデルのバージョン。
  - `elements`: 本サービスによって検出された文書要素の配列。
    - `location`: 要素の `begin` 索引と `end` 索引によって定義される要素の位置。
    - `text`: 要素のテキスト。
    - `types`: 要素の種類とその影響を受ける対象者を記述した配列。
      - `label`: 以下の要素のペアを使用してタイプを定義するオブジェクト。
        - `nature`: センテンスに必要なアクションのタイプ。現行値は、`Definition`、`Disclaimer`、`Exclusion`、`Obligation`、および `Right` です。
        - `party`: センテンスが適用されるパーティーを識別するストリング。
      - `provenance_ids`: フィードバックを提供したりサポートを受けたりするために IBM に送信できる 1 つ以上のハッシュ値の配列。
    - `categories`: 要素が分類される機能カテゴリー、つまり要素の主題をリストした配列。
      - `label`: 識別されたカテゴリーをリストしたストリング。[categories](/docs/services/discovery/parsing.html#contract_categories) のリストは、[契約の解析](/docs/services/discovery/parsing.html#contract_parsing)にあります。
      - `provenance_ids`: フィードバックを提供したりサポートを受けたりするために IBM に送信できる 1 つ以上のハッシュ値の配列。
    - `attributes`: 文書の属性を識別する配列。配列内の各オブジェクトは、以下の 3 つの要素で構成されます。
      - `type`: 属性のタイプ。可能な値は、`Location`、`DateTime`、および `Currency` です。
      - `text`: 属性と関連付けられているテキスト。
      - `location`: 属性の `begin` 索引と `end` 索引によって定義される属性の位置。
  - `tables`\*: 入力文書内で識別された表を定義する配列。
    - `location`: 入力文書内の表の `begin` 索引と `end` 索引によって定義される現行表の位置。
    - `text`: 関連付けられたマークアップ・コンテンツなしの、入力文書にある現行表のテキスト・コンテンツ。
    - `section_title`: 識別された場合、現行表を含んでいるセクション・タイトルの位置。セクション・タイトルが識別されない場合は空です。
      - `text`: 識別されたセクション・タイトルのテキスト。
      - `location`: セクション・タイトルの `begin` 索引と `end` 索引によって定義される、入力文書内でのセクション・タイトルの位置。
    - `table_headers`: 現行表の他のすべてのセルにヘッダーとして適用可能な表レベルのセルの配列。それぞれの表ヘッダーは次の要素の集合として定義されます。
      - `cell_id`: `tableHeader-x-y` という形式のストリング値。ここで `x` および `y` は元の入力文書内のセル値の開始オフセットと終了オフセットです。
      - `location`: セルの `begin` 索引と `end` 索引によって定義される、入力文書内でのセルの位置。
      - `text`: 関連付けられたマークアップ・コンテンツなしの、入力文書にあるセルのテキスト・コンテンツ。
      - `row_index_begin`: 現行表におけるセルの `row` 位置の `begin` 索引。
      - `row_index_end`: 現行表におけるセルの `row` 位置の `end` 索引。
      - `column_index_begin`: 現行表におけるセルの `column` 位置の `begin` 索引。
      - `column_index_end`: 現行表におけるセルの `column` 位置の `end` 索引。
    - `column_headers`: 同じ列の他のセルにヘッダーとして適用可能な、 現行表の列レベルのセルの配列。それぞれの列ヘッダーは以下の集合として定義されます。
      - `cell_id`: `columnHeader-x-y` という形式のストリング値。ここで、`x` および `y` は、入力文書のこの列ヘッダー・セルの開始オフセットと終了オフセットです。
      - `location`: セルの `begin` 索引と `end` 索引によって定義される、入力文書内でのセルの位置。
      - `text`: 関連付けられたマークアップ・コンテンツなしの、入力文書にあるセルのテキスト・コンテンツ。
      - `text_normalized`: カスタマイズ入力を指定した場合は、カスタマイズに従って正規化されたバージョンのセル・テキスト。そうでない場合は、`text` と同じ値。 
      - `row_index_begin`: 現行表におけるセルの `row` 位置の `begin` 索引。
      - `row_index_end`: 現行表におけるセルの `row` 位置の `end` 索引。
      - `column_index_begin`: 現行表におけるセルの `column` 位置の `begin` 索引。
      - `column_index_end`: 現行表におけるセルの `column` 位置の `end` 索引。
    - `row_headers`: 同じ行の他のセルにヘッダーとして適用可能な、現行表の行レベルのセルの配列。それぞれの行ヘッダーは以下の集合として定義されます。
      - `cell_id`: `rowHeader-x-y` という形式のストリング値。ここで、`x` および `y` は、入力文書のこの行ヘッダー・セルの開始オフセットと終了オフセットです。
      - `location`: セルの `begin` 索引と `end` 索引によって定義される、入力文書内でのセルの位置。
      - `text`: 関連付けられたマークアップ・コンテンツなしの、入力文書にあるセルのテキスト・コンテンツ。
      - `text_normalized`: カスタマイズ入力を指定した場合は、カスタマイズに従って正規化されたバージョンのセル・テキスト。そうでない場合は、`text` と同じ値。 
      - `row_index_begin`: 現行表におけるセルの `row` 位置の `begin` 索引。
      - `row_index_end`: 現行表におけるセルの `row` 位置の `end` 索引。
      - `column_index_begin`: 現行表におけるセルの `column` 位置の `begin` 索引。
      - `column_index_end`: 現行表におけるセルの `column` 位置の `end` 索引。
    - `body_cells`: 対応する行ヘッダーと列ヘッダーが関連付けられている、表ヘッダー・セルでも列ヘッダー・セルでも行ヘッダー・セルでもない現行表のセルの配列。それぞれの本文セルは、次の要素の集合として定義されます。
      - `cell_id`: `bodyCell-x-y` という形式のストリング値。ここで `x` および `y` は、入力文書内のこの本文セルの開始オフセットと終了オフセットです。
      - `location`: セルの `begin` 索引と `end` 索引によって定義される、入力文書内でのセルの位置。
      - `text`: 関連付けられたマークアップ・コンテンツなしの、入力文書にあるセルのテキスト・コンテンツ。
      - `row_index_begin`: 現行表におけるこのセルの `row` 位置の `begin` 索引。
      - `row_index_end`: 現行表におけるこのセルの `row` 位置の `end` 索引。
      - `column_index_begin`: 現行表におけるこのセルの `column` 位置の `begin` 索引。
      - `column_index_end`: 現行表におけるこのセルの `column` 位置の `end` 索引。
      - `row_header_ids`: この本文セルに適用可能な行ヘッダーの `cell_id` 値の配列。
      - `row_header_texts`: この本文セルに適用可能な行ヘッダーの `text` 値の配列。
      - `row_header_texts_normalized`: カスタマイズ入力を指定した場合は、カスタマイズに従って正規化されたバージョンの行ヘッダー・テキスト。そうでない場合は、`row_header_texts` と同じ値。 
      - `column_header_ids`: この本文セルに適用可能な列ヘッダーの `cell_id` 値の配列。
      - `column_header_texts`: この本文セルに適用可能な列ヘッダーの `text` 値の配列。
      - `column_header_texts_normalized`: カスタマイズ入力を指定した場合は、カスタマイズに従って正規化されたバージョンの列ヘッダー・テキスト。そうでない場合は、`column_header_texts` と同じ値。
  - `document_structure`: 入力文書の構造を記述したオブジェクト。
    - `section_titles`: 入力文書内で検出されたセクションまたはサブセクションごとに 1 つのオブジェクトを含んだ配列。セクションおよびサブセクションはネストされずにフラット化され、要素の `begin` と `end` の値およびセクションの `level` 値を使用して元の状態に戻すことができます。
      - `text`: セクション・タイトルをリストしたストリング (検出された場合)。
      - `location`: タイトルの `begin` 索引と `end` 索引によって定義される、入力文書内でのタイトルの位置。
      - `level`: 入力文書内でセクションが配置されていたレベルを示す整数。例えば、`1` はトップレベル・セクションを表し、`2` は、レベル `1` セクション内のサブセクションを表します。
      - `element_locations`: セクション内のセンテンスの `begin` 値と `end` 値を指定するオブジェクトを含んだ配列。
    - `leading_sentences`: 対応するセクションまたはサブセクション内のリード文を詳述した配列であり、`section_titles` 配列と並列に配置され、セクションまたはサブセクションごとに 1 つのオブジェクトを含んだ配列。`section_titles` 配列と同様に、オブジェクトはネストされずにフラット化され、要素の `begin` と `end` の値または入力文書内の任意のレベル・マーカーを使用して元の状態に戻すことができます。
      - `text`: リード文をリストしたストリング (検出された場合)。
      - `location`: リード文の `begin` 索引と `end` 索引によって定義される、入力文書内でのリード文の位置。
      - `element_locations`: セクション内のリード文の `begin` 値と `end` 値を指定するオブジェクトを含んだ配列。
  - `parties`: 本サービスによって識別されたパーティーを定義する配列。
    - `party`: パーティーを識別するストリング値。
    - `role`: パーティーの役割を識別するストリング値。
    - `addresses`: アドレスを識別するオブジェクトの配列。
      - `text`: アドレスを含んだストリング。
      - `location`: アドレスの `begin` 索引と `end` 索引によって定義されるアドレスの位置。
    - `contacts`: 入力文書内で識別された連絡先の名前と役割を定義する配列。
      - `name`: 識別された連絡先の名前をリストしたストリング。
      - `role`: 識別された連絡先の役割をリストしたストリング。  
  - `effective_dates`: 文書の発効日を識別する配列。
    - `text`: ストリングとしてリストされる発効日。
    - `location`: 日付の `begin` 索引と `end` 索引によって定義される日付の位置。
  - `contract_amounts`: 文書内で識別された金額を識別する配列。
    - `text`: ストリングとしてリストされる契約金額。
    - `location`: 金額の `begin` 索引と `end` 索引によって定義される金額の位置。

**\*表に関する注記:**
  - セルごとの行および列の索引値はゼロベースであり、`0` で始まります。
  - `row_header_ids` 要素と `row_header_texts` 要素の配列内の複数の値は、行ヘッダーの階層を示しています。
  - `column_header_ids` 要素と `column_header_texts` 要素の配列内の複数の値は、列ヘッダーの階層を示しています。
