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

# 瞭解輸出綱目
{: #output_schema}

使用「元素分類」來汲取文件之後，服務會針對日期為 `2018-10-15` 或該日期之後的版本，以下列綱目提供 JSON 輸出。此輸出將包含在 `enriched_html_elements` 物件內。 

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

綱目的排列方式如下。

  - `document`：列出文件基本資訊的物件，包括：
    - `title`：文件標題（如果偵測到的話）。
    - `html`：HTML 格式之輸入文件的全文。
    - `hash`：輸入文件的 MD5 雜湊。
  - `model_id`：要用來分類文件的分析模型。預設值為 `contracts`。 
  - `model_version`：`model_id` 參數值所指定之分析模型的版本。
  - `elements`：服務所偵測到之文件元素的陣列。
    - `location`：元素的位置，如其 `begin` 和 `end` 索引所定義。
    - `text`：元素的文字。
    - `types`：說明何謂元素及其影響對象的陣列。
      - `label`：使用下列元素配對來定義類型的物件：
        - `nature`：句子所需的動作類型。現行值為 `Definition`、`Disclaimer`、`Exclusion`、`Obligation` 及 `Right`。
        - `party`：識別句子所適用對象的字串。
      - `provenance_ids`：您可以傳送給 IBM 以提供意見或取得支援之一個以上雜湊值的陣列。
    - `categories`：列出元素所在功能種類的陣列；換句話說，就是元素的主題。
      - `label`：列出所識別種類的字串。您可以在[瞭解合約剖析](/docs/services/discovery/parsing.html#contract_parsing)中找到[種類](/docs/services/discovery/parsing.html#contract_categories)清單。
      - `provenance_ids`：您可以傳送給 IBM 以提供意見或取得支援之一個以上雜湊值的陣列。
    - `attributes`：識別文件屬性的陣列。陣列中的每個物件都是由三個元素組成：
      - `type`：屬性的類型。可能值為 `Location`、`DateTime` 及 `Currency`。
      - `text`：與屬性相關聯的文字。
      - `location`：屬性的位置，如其 `begin` 和 `end` 索引所定義。
  - `tables`\*：定義輸入文件中所識別表格的陣列。
    - `location`：現行表格在輸入文件中的位置，如其 `begin` 和 `end` 索引所定義。
    - `text`：輸入文件中現行表格的文字內容，不含相關聯的標記內容。
    - `section_title`：如果已識別，則為包含現行表格之區段標題的位置。如果未識別任何區段標題，則為空白。
      - `text`：所識別區段標題的文字。
      - `location`：區段標題在輸入文件中的位置，如其 `begin` 和 `end` 索引所定義。
    - `table_headers`：表格層次資料格的陣列，這些資料格適合作為現行表格之所有其他資料格的標頭。每個表格標頭都定義為下列元素的集合：
      - `cell_id`：格式為 `tableHeader-x-y` 的字串值，其中 `x` 和 `y` 是資料格值在原始輸入文件中的開始和結束偏移。
      - `location`：資料格在輸入文件中的位置，如其 `begin` 和 `end` 索引所定義。
      - `text`：輸入文件中資料格的文字內容，不含相關聯的標記內容。
      - `row_index_begin`：此資料格之 `row` 位置在現行表格中的 `begin` 索引。
      - `row_index_end`：此資料格之 `row` 位置在現行表格中的 `end` 索引。
      - `column_index_begin`：此資料格之 `column` 位置在現行表格中的 `begin` 索引。
      - `column_index_end`：此資料格之 `column` 位置在現行表格中的 `end` 索引。
    - `column_headers`：現行表格之直欄層次資料格的陣列，每個都適合作為與其本身相同直欄之其他資料格的標頭。每個直欄標頭都定義為下列各項的集合：
      - `cell_id`：格式為 `columnHeader-x-y` 的字串值，其中 `x` 和 `y` 是這個直欄標頭資料格在輸入文件中的開始和結束偏移。
      - `location`：資料格在輸入文件中的位置，如其 `begin` 和 `end` 索引所定義。
      - `text`：輸入文件中資料格的文字內容，不含相關聯的標記內容。
      - `text_normalized`：如果您提供自訂輸入，則為根據自訂之資料格文字的正規化版本；否則，其為與 `text` 相同的值。 
      - `row_index_begin`：此資料格之 `row` 位置在現行表格中的 `begin` 索引。
      - `row_index_end`：此資料格之 `row` 位置在現行表格中的 `end` 索引。
      - `column_index_begin`：此資料格之 `column` 位置在現行表格中的 `begin` 索引。
      - `column_index_end`：此資料格之 `column` 位置在現行表格中的 `end` 索引。
    - `row_headers`：現行表格之列層次資料格的陣列，每個都適合作為與其本身相同列之其他資料格的標頭。每個列標頭都定義為下列各項的集合：
      - `cell_id`：格式為 `rowHeader-x-y` 的字串值，其中 `x` 和 `y` 是這個列標頭資料格在輸入文件中的開始和結束偏移。
      - `location`：資料格在輸入文件中的位置，如其 `begin` 和 `end` 索引所定義。
      - `text`：輸入文件中資料格的文字內容，不含相關聯的標記內容。
      - `text_normalized`：如果您提供自訂輸入，則為根據自訂之資料格文字的正規化版本；否則，其為與 `text` 相同的值。 
      - `row_index_begin`：此資料格之 `row` 位置在現行表格中的 `begin` 索引。
      - `row_index_end`：此資料格之 `row` 位置在現行表格中的 `end` 索引。
      - `column_index_begin`：此資料格之 `column` 位置在現行表格中的 `begin` 索引。
      - `column_index_end`：此資料格之 `column` 位置在現行表格中的 `end` 索引。
    - `body_cells`：現行表格中既不是表格標頭、不是直欄標頭也不是列標頭資料格的資料格陣列（具有相對應的列和直欄標頭關聯）。每個內文資料格都定義為下列各項的集合：
      - `cell_id`：格式為 `bodyCell-x-y` 的字串值，其中 `x` 和 `y` 是這個內文資料格在輸入文件中的開始和結束偏移。
      - `location`：資料格在輸入文件中的位置，如其 `begin` 和 `end` 索引所定義。
      - `text`：輸入文件中資料格的文字內容，不含相關聯的標記內容。
      - `row_index_begin`：這個資料格之 `row` 位置在現行表格中的 `begin` 索引。
      - `row_index_end`：這個資料格之 `row` 位置在現行表格中的 `end` 索引。
      - `column_index_begin`：這個資料格之 `column` 位置在現行表格中的 `begin` 索引。
      - `column_index_end`：這個資料格之 `column` 位置在現行表格中的 `end` 索引。
      - `row_header_ids`：值的陣列，每個值都是適用於這個內文資料格之列標頭的 `cell_id` 值。
      - `row_header_texts`：值的陣列，每個值都是適用於這個此內文資料格之列標頭的 `text` 值。
      - `row_header_texts_normalized`：如果您提供自訂輸入，則為根據自訂之列標頭文字的正規化版本；否則，其為與 `row_header_texts` 相同的值。 
      - `column_header_id`：值的陣列，每個值都是適用於這個內文資料格之直欄標頭的 `cell_id` 值。
      - `column_header_texts`：值的陣列，每個值都是適用於這個內文資料格之直欄標頭的 `text` 值。
      - `column_header_texts_normalized`：如果您提供自訂輸入，則為根據自訂之直欄標頭文字的正規化版本；否則，其為與 `column_header_texts` 相同的值。
  - `document_structure`：說明輸入文件結構的物件。
    - `section_titles`：輸入文件中偵測到的每個區段或子區段各包含一個物件的陣列。區段及子區段不是巢狀；它們反而是扁平的，並且可以使用元素的 `begin` 和 `end` 值以及區段的 `level` 值，按順序放回去。
      - `text`：列出區段標題的字串（如果偵測到的話）。
      - `location`：標題在輸入文件中的位置，如其 `begin` 和 `end` 索引所定義。
      - `level`：指出區段在輸入文件中所處層次的整數。例如，`1` 代表最上層區段，`2` 代表層次 `1` 區段內的子區段，依此類推。
      - `element_locations`：包含物件的陣列，這些物件可指定區段中句子的 `begin` 和 `end` 值。
    - `leading_sentences`：每個區段或子區段各包含一個物件的陣列（同時使用 `section_titles` 陣列），該陣列詳述相符區段或子區段中的前導句子。如同 `section_titles` 陣列，物件不是巢狀；它們反而是扁平的，並且可以使用元素的 `begin` 和 `end` 值或輸入文件中的任何層次標記，按順序放回去。
      - `text`：列出前導句子的字串（如果偵測到的話）。
      - `location`：前導句子在輸入文件中的位置，如其 `begin` 和 `end` 索引所定義。
      - `element_locations`：包含物件的陣列，這些物件可指定區段中前導句子的 `begin` 和 `end` 值。
  - `parties`：定義服務所識別之參與方的陣列。
    - `party`：識別參與方的字串值。
    - `role`：識別參與方角色的字串值。
    - `addresses`：識別地址的物件陣列。
      - `text`：包含地址的字串。
      - `location`：地址的位置，如其 `begin` 和 `end` 索引所定義。
    - `contacts`：定義輸入文件中所識別聯絡人名稱和角色的陣列。
      - `name`：列出所識別聯絡人名稱的字串。
      - `role`：列出所識別聯絡人角色的字串。  
  - `effective_dates`：識別文件有效日期的陣列。
    - `text`：以字串列出的有效日期。
    - `location`：日期或多個日期的位置，如其 `begin` 和 `end` 索引所定義。
  - `contract_amounts`：識別文件中所識別之貨幣金額的陣列。
    - `text`：以字串列出的合約金額。
    - `location`：金額或多個金額的位置，如其 `begin` 和 `end` 索引所定義。

**\*表格的附註：**
  - 每個資料格的列和直欄索引值都以零為基礎，因此從 `0` 開始。
  - `row_header_ids` 和 `row_header_texts` 元素陣列中的多個值指出列標頭的階層。
  - `column_header_ids` 和 `column_header_texts` 元素陣列中的多個值指出直欄標頭的階層。
