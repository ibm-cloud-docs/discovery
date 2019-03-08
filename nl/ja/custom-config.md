---

copyright:
  years: 2015, 2018
lastupdated: "2018-01-23"

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

# 構成リファレンス
{: #configref}

ご使用のデータに、[変換](#conversion)、[エンリッチメント](#enrichment)、[正規化](#normalization) に関する特別なニーズがある場合は、独自の {{site.data.keyword.discoveryshort}} 取り込み構成を JSON で作成できます。
{: shortdesc}

 次のセクションでは、この JSON の構造とそれによって定義できるオブジェクトについて詳しく説明します。

## 構成の構造
{: #structure}

{{site.data.keyword.discoveryshort}} 構成は、次のような構造になっています。

```json
{
  "name": "Configuration Name",
  "description": "Descriptive text about the configuration",
  "conversions": {
    "word": {},
    "pdf": {},
    "html": {},
    "segment": {},
    "json_normalizations": []
  },
  "enrichments": [],
  "normalizations": []
}
```
{: codeblock}

基本 JSON オブジェクトには、次の項目が含まれます。

-  `"name": "Configuration Name"` - 構成の名前。
-  `"description": "Descriptive text about the configuration"` - 構成の説明。

コレクションにアップロードされた文書を変換、エンリッチ、正規化するには、次のオブジェクトと配列を定義する必要があります。

- `"conversions": {}` - 文書をエンリッチ可能な JSON に変換する方法。
- `"enrichments": []` - 適用するエンリッチメントの種類と、適用対象となる JSON の部分。
- `"normalizations": []` - 文書の保存前に必要な、エンリッチメント後のすべての調整。

また、構成が作成または更新されたときに、{{site.data.keyword.discoveryshort}} によって以下の項目が基本オブジェクトに追加されます。

```json
{
  "configuration_id": "4f5b7c7b-ebf4-4963-882e-27eff08f08e3",
  "created": "2017-09-13T14:45:03.575Z",
  "updated": "2017-09-13T14:45:03.575Z"
}
```
{: codeblock}

## 変換
{: #conversion}

文書の変換とは、1 つ以上のステップを使用して元のソース・フォーマットを JSON に変換することです。この JSON は、残りの取り込みプロセスに使用できます。 アップロードされたファイルのタイプに応じて、プロセスは次のようになります。

- **PDF** ファイルは、`pdf` オプションを使用して HTML に変換されます。結果として得られた **HTML** はその後、`html` オプションを使用して JSON に変換され、その結果の **JSON** は最後に `json` オプションを使用して変換されます。

- **Microsoft Word ** ファイルは、`word` オプションを使用して HTML に変換されます。結果として得られた **HTML** はその後、`html` オプションを使用して JSON に変換され、その結果の **JSON** は最後に `json` オプションを使用して変換されます。

- **HTML** ファイルは、`html` オプションを使用して JSON に変換されます。結果として得られた **JSON** は、`json` オプションを使用して変換されます。

- **JSON** ファイルは、`json` オプションを使用して変換されます。

これらのオプションについては、以下のセクションで説明します。 変換の完了後、[エンリッチメント](#enrichment)と[正規化](#normalization)を実行してから、コンテンツを保存します。

### PDF
{: #pdf}

`pdf` 変換オブジェクトは PDF 文書を HTML に変換する方法を定義し、次に示す構造となっています。

```json
"pdf": {
  "heading": {
    "fonts": [
      {
        "level": 1,
        "min_size": 24,
        "max_size": 80,
        "bold": false,
        "italic": true,
        "name": "arial"
      },
      {
        "level": 2,
        "min_size": 18,
        "max_size": 24,
        "bold": true,
        "italic": false,
        "name": "ariel"
      }
    ]
  }
},
```
{: codeblock}

PDF ファイルを変換するとき、各見出しレベルのサイズ、フォント、スタイルを識別することで、ファイルに含まれる見出しを識別して適切な HTML "`h`" タグに変換できます。 すべての関連セクションを正確に識別するために、必要に応じて見出しレベルを複数回指定できます。 HTML 見出しレベルが識別用として重要なのは、CSS セレクターを使用してコンテンツを抽出する場合や、文書の分割を使用して文書を分割する場合です。 `heading` オブジェクトには `fonts` 配列があり、この配列の各項目では、次のパラメーターを使用して見出しレベルを指定します。

- `"level": 整数` - *必須* - これらのパラメーターで識別されたテキストが変換される HTML の `h` レベル。
- `"min_size": 整数` - _オプション_ - この見出しレベルとして識別される最小フォント・サイズ。
- `"max_size": 整数` - _オプション_ - この見出しレベルとして識別される最大フォント・サイズ。
- `"bold": ブール` - _オプション_ - `true` の場合、太字フォントのみがこの見出しレベルとして識別されます。
- `"italic": ブール` - _オプション_ - `true` の場合、イタリック・フォントのみがこの見出しレベルとして識別されます。
- `"name": "ストリング"` - _オプション_ - この見出しレベルとして識別されるフォントの名前。

見出しとして識別されるテキストの領域は、特定の配列項目で定義されたすべてのパラメーターに一致する必要があります。 定義されたパラメーターがあまりにも柔軟な場合は、予想よりも多くの見出しが識別される可能性があります。 不正な一致をなくし、見出しレベルのバリエーションがすべて含まれるように各見出しレベルを複数回厳密に定義することで、より良い結果を得られます。


### Word
{: #word}

`word` 変換オブジェクトは PDF 文書を HTML に変換する方法を定義し、次に示す構造となっています。

```json
"word": {
  "heading": {
    "fonts": [
      {
        "level": 1,
        "min_size": 24,
        "bold": true,
        "italic": false,
        "name": "arial"
      },
      {
        "level": 2,
        "min_size": 18,
        "max_size": 23,
        "bold": true,
        "italic": false
      }
    ],
    "styles": [
      {
        "level": 1,
        "names": [
          "pullout heading",
          "pulloutheading",
          "header"
        ]
      },
      {
        "level": 2,
        "names": [
          "subtitle"
        ]
      }
    ]
  }
},
```
{: codeblock}

Microsoft Word 変換オブジェクトは、PDF 変換オブジェクトと同様の方法で機能します。 ただし、Microsoft Word 文書から見出しを抽出するときに、`heading` オブジェクト内で指定できる配列が 2 つある点が異なっています。 見出し抽出配列の一方または両方を使用して、Microsoft Word 文書から見出しレベル要素を抽出できます。

`fonts` 配列の各項目では、フォントの特性を用いた次のパラメーターを使用して見出しレベルを指定します。

- `"level": 整数` - *必須* - これらのパラメーターで識別されたテキストが変換される HTML の `h` レベル。
- `"min_size": 整数` - _オプション_ - この見出しレベルとして識別される最小フォント・サイズ。
- `"max_size": 整数` - _オプション_ - この見出しレベルとして識別される最大フォント・サイズ。
- `"bold": ブール` - _オプション_ - `true` の場合、太字フォントのみがこの見出しレベルとして識別されます。
- `"italic": ブール` - _オプション_ - `true` の場合、イタリック・フォントのみがこの見出しレベルとして識別されます。
- `"name": "ストリング"` - _オプション_ - この見出しレベルとして識別されるフォントの名前。

`font` 配列で見出しとして識別されるテキストの領域は、特定の配列項目で定義されたすべてのパラメーターに一致する必要があります。 定義されたパラメーターがあまりにも柔軟な場合は、予想よりも多くの見出しが識別される可能性があります。 不正な一致をなくし、見出しレベルのバリエーションがすべて含まれるように各見出しレベルを複数回厳密に定義することで、より良い結果を得られます。

`styles` 配列の各項目では、対象のパラグラフに適用されている Microsoft Word スタイルから見出しレベルを指定します。

- `"level": 整数` - *必須* - これらのパラメーターで識別されたテキストが変換される HTML の `h` レベル。
- `"names": 配列` - *必須* - この見出しレベルとして識別されるスタイル名で構成されるコンマ区切りの配列。

*フォントを使用するケースとスタイルを使用するケース* - 適切なスタイルを用いて各パラグラフが正しくタグ付けされたスタイル・シートに Microsoft Word 文書がうまく適合している場合は、`styles` を使用した見出しの抽出が推奨されます。 ただし、スタイルが手動で上書きされている文書が存在するかもしれません。 このような文書には、`fonts` 抽出方式を使用すると変換効率が良くなる可能性があります。
{: tip}


### HTML
{: #html}

```json
"html": {
  "exclude_tags_completely": [
    "script",
    "sup"
  ],
  "exclude_tags_keep_content": [
    "font",
    "em"
  ],
  "exclude_content": {
    "xpaths": [
      "//*[@id='list-old']",
      "//*[@id='unstable']"
    ]
  },
  "keep_content": {
    "xpaths": [
      "//*[@id='footer']",
      "//*[@id='header']"
    ]
  },
  "exclude_tag_attributes": [
    "EVENT_ACTIONS"
  ],
  "keep_tag_attributes": [
    "id"
  ],
  "extracted_fields": {
    "{field_name}": {
      "css_selector": "{CSS_selector_expression_1}",
      "type": "{field_type}"
    }
  }
},
```
{: codeblock}

#### exclude_tags_completely

`"exclude_tags_completely" : 配列` - 除外される HTML タグの名前の配列。 これには、タグ、コンテンツ、および定義されたすべてのタグ属性が含まれます。

#### exclude_tags_keep_content

`"exclude_tags_keep_content" : 配列` - タグ情報が削除される HTML タグの名前の配列。 これにより、HTML タグとすべてのタグ属性が除去されます。 タグの内容は、指定されない限り、それ以上は除去されません。 例えば、`span` HTML タグに `exclude_tags_keep_content` を指定すると、`<span class="info">Some <strong>Information</strong></span>` はタグが削除されて `Some <strong>Information</strong>` になります。

#### exclude_content

`"xpaths" : 配列` - 削除されるコンテンツを識別する XPath の配列。 この値を設定すると、いずれかの XPath に一致するものがすべて出力から削除されます。

#### keep_content

`"xpaths" : 配列` - 変換されるコンテンツを識別する XPath の配列。 この値を設定すると、いずれかの XPath に一致するものがすべて出力に含められます。 このパラメーターの指定によって含められたものは、`exclude_content` で指定されたすべての処理の後で処理されます。

#### exclude_tag_attributes

`"exclude_tag_attributes" : 配列` - 変換によって削除される HTML 属性の名前の配列。その HTML 属性がどの HTML タグに含まれるのかは問いません。 **注:** 同じ構成内で `exclude_tag_attributes` と `keep_tag_attributes` の両方を指定すると、エラー・メッセージを受け取ります。構成ごとに指定できるのは 1 つのみです。`keep_tag_attributes` がある場合は、構成から完全に削除する必要があります。空の配列として存在することはできません。

#### keep_tag_attributes

`"keep_tag_attributes" : 配列` - 変換によって保持される HTML 属性の名前の配列。 **注:** 同じ構成内で `keep_tag_attributes` と `exclude_tag_attributes` の両方を指定すると、エラー・メッセージを受け取ります。構成ごとに指定できるのは 1 つのみです。`exclude_tag_attributes` がある場合は、構成から完全に削除する必要があります。空の配列として存在することはできません。

#### extracted_fields

このオブジェクトは、変換の一部として別の JSON フィールドに抽出される、HTML ソースの任意のコンテンツを定義します。 コンテンツは、CSS セレクターを使用して識別されます。

作成する各フィールドは、オブジェクトによって次のように定義します。

```json
"{field_name}": {
  "css_selector": "{CSS_selector_expression_1}",
  "type": "{field_type}"
}
```
{: codeblock}

- `"{field_name}"` - 作成するフィールドの名前。

**注:** 構成で定義するフィールド名は、「[フィールド名の要件](#field_reqs)」で定義された制約事項に従う必要があります。

- `"css_selector" : ストリング` *必須* - フィールドに保存されるコンテンツの領域を定義する CSS セレクター式です。
- `"type" : ストリング` *必須* - 作成するフィールドのタイプで、`string` または `date` を指定できます。
詳しくは、「[CSS セレクターを使用したフィールドの抽出](/docs/services/discovery/building.md#using-css)」を参照してください。

### セグメント
{: #segment}

`segment` オブジェクトは、識別された HTML 見出し (`h1`、`h2`) に基づいて、取り込まれた文書を 1 つ以上のセグメントに分割する構成オプションのセットです。

```json
"segment": {
  "enabled": true,
  "selector_tags": ["h1", "h2", "h3", "h4", "h5", "h6"]
}
```
{: codeblock}

- `"enabled": ブール` - *必須* - 文書のセグメンテーションを有効にするために、`true` に設定する必要があります。
- `"selector_tags": 配列` - *必須* - 文書を分割するための HMTL `h` タグのコンマ区切り配列。

概要として、文書セグメンテーションが有効な場合、以下を指定することはできません。

-  `json_normalizations` を構成の一部として指定することはできません。
-  `normalizations` を構成の一部として指定することはできません。
-  `html` 変換の `extracted_fields` オプションを構成の一部として指定することはできません。

詳しくは、「[セグメンテーションの実行](/docs/services/discovery/building.html#performing-segmentation)」を参照してください。


### JSON
{: #json}

`json_normalizations` 配列で `operation` オブジェクトを定義することにより、取り込んだ JSON にエンリッチメント前の正規化を実行できます。

```json
"json_normalizations": [
  {
    "operation": "remove",
    "source_field": "header"
  },
  {
    "operation": "copy",
    "source_field": "title",
    "destination_field": "title_old"
  },
  {
    "operation": "move",
    "destination_field": "content",
    "source_field": "body"
  },
  {
    "operation": "merge",
    "source_field": "synopsis",
    "destination_field": "preamble"
  },
  {
    "operation": "remove_nulls"
  }
]
```
{: codeblock}

#### 操作オブジェクト
{: #operations}

- `"operation": ストリング` - *必須* - JSON に実行される操作であり、以下のいずれかでなければなりません。
  - `remove` - 指定された `source_field` が JSON から削除されます。
  - `copy` - 指定された `source_field` のコンテンツが、`destination_field` の新規インスタンスにコピーされます。
  - `move` - 指定された `source_field` が `destination_field` に名前変更されます。 `destination_field` が既に存在する場合は、`destination_field` の新規インスタンスが作成されます。
  - `merge` - `source_field` と `destination_field` のコンテンツが `destination_field` にマージされます。
  - `remove_nulls` - `null` コンテンツを持つフィールドが削除されます。
- `"source_field": ストリング` - _オプション_ - 操作が実行されるフィールド。
- `"destination_field": ストリング` - _オプション_ - 操作が出力される宛先フィールド。  

  **注:** 構成で定義するフィールド名は、「[フィールド名の要件](#field_reqs)」で定義された制約事項に従う必要があります。


## エンリッチメント
{: #enrichments}

```json
"enrichments": [
   {
    "enrichment": "elements",
    "source_field": "html",
    "destination_field": "enriched_html",
    "options": {
      "model": "contract"
    }
  },
  {
    "enrichment": "natural_language_understanding",
    "source_field": "title",
    "destination_field": "enriched_title",
    "options": {
      "features": {
        "keywords": {
          "sentiment": true,
          "emotion": false,
          "limit": 50
        },
        "entities": {
          "sentiment": true,
          "emotion": false,
          "limit": 50,
          "mentions": true,
          "mention_types": true,
          "sentence_locations": true,        
          "model": "WKS-model-id"
        },
        "sentiment": {
          "document": true,
          "targets": [
            "IBM",
            "Watson"
          ]

        },
        "emotion": {
          "document": true,
          "targets": [
            "IBM",
            "Watson"
          ]
        },
        "categories": {},
        "concepts": {
          "limit": 8
        },
        "semantic_roles": {
          "entities": true,
          "keywords": true,
          "limit": 50
        },
        "relations": {
          "model": "WKS-model-id"
        }
      }
    }
  }
]
```
{: codeblock}

{{site.data.keyword.discoveryshort}} は、{{site.data.keyword.nlushort}} エンリッチメントと要素の分類エンリッチメントの追加をサポートします。 エンリッチする各フィールドは、`enrichments` 配列内のオブジェクトによって定義します。 各エンリッチメント・オブジェクトには、`source_field`、`destination_field`、およびエンリッチメントを指定する必要があります。

- `"enrichment" : ストリング` - *必須* - このフィールドに使用するエンリッチメントのタイプ。 {{site.data.keyword.nlushort}} エンリッチメントを抽出するには `natural_language_understanding` を使用し、要素の分類を実行するには `elements` を使用します。

  **注:** `elements` エンリッチメントを使用するときは、「[要素の分類](/docs/services/discovery/element-classification.html)」文書で指定されたガイドラインに従うことが重要です。 特に、このエンリッチメントが指定されているときは、PDF ファイルのみ取り込むことができます。

- `"source_field" : ストリング` - *必須* - エンリッチされるソース・フィールド。 このフィールドは、`json_normalizations` 操作が完了した後のソースに存在していなければなりません。
- `"destination_field" : ストリング` - *必須* - エンリッチメントが作成されるコンテナー・オブジェクトの名前。

  **注:** 構成で定義するフィールド名は、「[フィールド名の要件](#field_reqs)」で定義された制約事項に従う必要があります。

### 要素の分類エンリッチメント

要素の分類を使用するとき、各 `elements` エンリッチメント・オブジェクトは、次のパラメーターを指定した `"options": {}` オブジェクトを保持している必要があります。

- `"model" : ストリング` - *必須* - この文書に使用する要素抽出モデル。 現在サポートされているモデルは `contract` です。

**注:** `elements` エンリッチメントを使用するときは、「[要素の分類](/docs/services/discovery/element-classification.html)」文書で指定されたガイドラインに従うことが重要です。 特に、このエンリッチメントが指定されているときは、PDF ファイルのみ取り込むことができます。

### Natural Language Understanding エンリッチメント

{{site.data.keyword.nlushort}} を使用する場合、`enrichments` 配列内の各オブジェクトは、次のエンリッチメントを 1 つ以上含む `"options": { "features": { } }` オブジェクトも保持している必要があります。

### categories

`categories` エンリッチメントは、取り込んだ文書内の一般的なカテゴリーを識別します。 このエンリッチメントはオプションを持たず、空のオブジェクト `"categories" : {}` として指定する必要があります。

### concepts

`concepts` エンリッチメントは、テキスト内に存在する他の概念とエンティティーに基づいて、入力テキストに関連付けられている概念を検出します。

- `"limit" : 整数` - *必須* - 取り込んだ文書から抽出する概念の最大数。

### emotion

`emotion` エンリッチメントは、文書全体における、または文書内の指定されたターゲット・ストリングにおける総合的な感情トーン (例: `anger`) を評価します。 このエンリッチメントは、英語のコンテンツでのみ使用できます。

- `"document" : ブール ` _オプション_ - `true` の場合、文書全体の感情トーンが評価されます。
- `"targets" : 配列 ` _オプション_ - 文書内で感情の状態を評価するターゲット・ストリングのコンマ区切り配列。

### entities

`entities` エンリッチメントは、既知のエンティティー (ユーザー、プレース、組織など) のインスタンスを抽出します。 オプションで、カスタム・エンティティーを抽出するために {{site.data.keyword.knowledgestudioshort}} カスタム・モデルを指定できます。

- `"sentiment" : ブール` - _オプション_ - `true` の場合、周囲のコンテンツの状況に応じて、抽出されたエンティティーにセンチメント分析が実行されます。
- `"emotion" : ブール` - _オプション_ - `true` の場合、周囲のコンテンツの状況に応じて、抽出されたエンティティーに感情トーン分析が実行されます。
- `"limit" : 整数` - _オプション_ - 取り込んだ文書から抽出するエンティティーの最大数。 デフォルトは `50` です。
- `"mentions": ブール` - _オプション_ - `true` の場合、このエンティティーが言及された回数が記録されます。 デフォルトは、`false` です。
- `"mention_types": ブール` - _オプション_ - `true` の場合、このエンティティーの各言及の言及タイプが保存されます。 デフォルトは、`false` です。
- `"sentence_location": ブール` - _オプション_ - `true` の場合、各エンティティー言及のセンテンスの場所が保存されます。 デフォルトは、`false` です。
- `"model" : ストリング` - _オプション_ - このオプションを指定すると、パブリック・モデルの代わりにカスタム・モデルを使用してエンティティーが抽出されます。 このオプションを使用するには、ご使用の {{site.data.keyword.discoveryshort}} のインスタンスに {{site.data.keyword.knowledgestudioshort}} カスタム・モデルが関連付けられている必要があります。 詳しくは、「[Watson Knowledge Studio との統合](/docs/services/discovery/integrate-wks.html)」を参照してください。

### keywords

`keywords` エンリッチメントは、テキスト内の重要な語を抽出します。 キーワード、概念、およびエンティティーの違いを理解するには、「[エンティティー、概念、およびキーワードの違いについて](/docs/services/discovery/building.html#udbeck)」を参照してください。

- `"sentiment" : ブール` - _オプション_ - `true` の場合、周囲のコンテンツの状況に応じて、抽出されたキーワードにセンチメント分析が実行されます。
- `"emotion" : ブール` - _オプション_ - `true` の場合、周囲のコンテンツの状況に応じて、抽出されたキーワードに感情トーン分析が実行されます。
- `"limit" : 整数` - _optional_ -  取り込んだ文書から抽出するキーワードの最大数。 デフォルトは `50` です。

### semantic_roles

`semantic_roles` エンリッチメントは、取り込んだテキスト内のセンテンス・コンポーネント (サブジェクト、アクション、オブジェクトなど) を識別します。

- `"entities" : ブール` - _オプション_ `true` の場合、センテンス・コンポーネントからエンティティーが抽出されます。
- `"keywords" : ブール` - _オプション_ `true` の場合、センテンス・コンポーネントからキーワードが抽出されます。
- `"limit" : 整数` - _オプション_ - 取り込んだ文書から抽出する `semantic_roles` オブジェクト (解析するセンテンス) の最大数。 デフォルトは `50` です。

### sentiment

`sentiment` エンリッチメントは、文書全体における、または文書内の指定されたターゲット・ストリングにおける総合的なセンチメント・レベルを評価します。

- `"document" : ブール ` _オプション_ - `true` の場合、文書全体のセンチメントが評価されます。
- `"targets" : 配列 ` _オプション_ - 文書内のセンチメントを評価するターゲット・ストリングのコンマ区切り配列。

### relations

`relations` エンリッチメントは、文書内の識別済みエンティティー間の既知の関係を抽出します。 オプションで、カスタム関係を抽出するために、{{site.data.keyword.knowledgestudioshort}} カスタム・モデルを指定できます。

- `"model" : ストリング` - _オプション_ - このオプションを指定すると、パブリック・モデルの代わりにカスタム・モデルを使用して関係が抽出されます。 このオプションを使用するには、ご使用の {{site.data.keyword.discoveryshort}} のインスタンスに {{site.data.keyword.knowledgestudioshort}} カスタム・モデルが関連付けられている必要があります。 詳しくは、「[Watson Knowledge Studio との統合](/docs/services/discovery/integrate-wks.html)」を参照してください。

## 正規化
{: #normalization}

`normalizations` は、JSON `operation` オブジェクトの配列です。このオブジェクトは、`enrichments` の適用後、取り込んだ JSON を保存前にクリーニングするために使用されます。

```json
"normalizations": [
  {
    "operation": "remove",
    "source_field": "enriched_title.entities.text"
  },
  {
    "operation": "copy",
    "source_field": "enriched_title.sentiment.document.score",
    "destination_field": "titlescore"
  }
]
```
{:codeblock}

`operation` オブジェクトのオプションは、[こちら](#operations)にリストされています。

## フィールド名の要件
{: #field_reqs}

フィールド名には、スペースを含められません。 次の文字とストリングは予約されていて、フィールド名には使用できません。


```
  .  ,  # ? :
  id
  score
  highlight
  result_metadata
```
{: pre}

文字 `_`、`+`、および `-` は、`field_name` のプレフィックスには使用できません。

数字の `0 から 9` までは、フィールド名のサフィックスには使用できません (例: `extracted-content2`)。 このようなフィールド名は索引付けされますが、照会できません。
