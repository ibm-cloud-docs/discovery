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

# 配置參考資料

如果您的資料具有特殊的[轉換](#conversion)、[強化](#enrichment)或[正規化](#normalization)需求，您可以在 JSON 中建立自己的 {{site.data.keyword.discoveryshort}} 汲取配置。
{: shortdesc}

 下列各節詳述此 JSON 的結構以及可在其中定義的物件。

## 配置結構
{: #structure}

{{site.data.keyword.discoveryshort}} 配置的結構如下所示：

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

基礎 JSON 物件包含下列項目：

-  `"name": "Configuration Name"` - 配置的名稱
-  `"description": "Descriptive text about the configuration"` - 配置的說明

必須定義下列物件及陣列，才能轉換、強化及正規化上傳至集合的文件。

- `"conversions": {}` - 文件如何轉換成可強化的 JSON。
- `"enrichments": []` - 哪些強化套用至 JSON 的哪些部分。
- `"normalizations": []` - 儲存文件之前所需要的任何貼文強化調整。

此外，在建立/更新配置時，下列項目會由 {{site.data.keyword.discoveryshort}} 新增至基礎物件中：

```json
{
  "configuration_id": "4f5b7c7b-ebf4-4963-882e-27eff08f08e3",
  "created": "2017-09-13T14:45:03.575Z",
  "updated": "2017-09-13T14:45:03.575Z"
}
```
{: codeblock}

## 轉換
{: #conversion}

轉換文件時採用原始來源格式，並使用一個以上的步驟將其轉換成 JSON，供其餘的汲取處理程序使用。視上傳的檔案類型而定，處理程序如下所示：

- **PDF** 檔案利用 `pdf` 選項轉換為 HTML，然後使用 `html` 選項將產生的 **HTML** 轉換為 JSON，最後使用 `json` 選項來轉換所產生的 **JSON**。

- **Microsoft Word** 檔案利用 `word` 選項轉換為 HTML，然後使用 `html` 選項將產生的 **HTML** 轉換為 JSON，最後使用 `json` 選項來轉換所產生的 **JSON**。

- **HTML** 檔案利用 `html` 選項轉換為 JSON，然後使用 `json` 選項來轉換所產生的 **JSON**。

- **JSON** 檔案則利用 `json` 選項來轉換。

下列各節說明這些選項。完成轉換之後，會先執行[強化](#enrichment)和[正規化](#normalization)，然後再儲存內容。

### PDF
{: #pdf}

`pdf` 轉換物件會定義應如何將 PDF 文件轉換成 HTML，並具有下列結構：

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

轉換 PDF 檔時，可透過識別每一個標題層次的大小、字型和樣式來識別那些檔案中的標題（並轉換成適當的 HTML "`h`" 標籤）。必要的話，可以多次指定標題層次，以正確識別所有相關區段。HTML 標題層次非常重要，其能夠識別您計劃使用 CSS 選取器來擷取內容，或是想要使用文件分割來分割文件。`heading` 物件包含 `fonts` 陣列，該陣列中的每一個項目會使用下列參數來指定標題層次：

- `"level": INT` - *必要* - 以這些參數識別的文字將轉換成的 HTML `h` 層次。
- `"min_size": INT` - _選用_ - 識別為此標題層次的最小字型大小。
- `"max_size": INT` - _選用_ - 識別為此標題層次的最大字型大小。
- `"bold": boolean` - _選用_ - 若為 `true`，則僅將粗體字型識別為此標題層次。
- `"italic": boolean` - _選用_ - 若為 `true`，則僅將斜體字型識別為此標題層次。
- `"name": "string"` - _選用_ - 識別為此標題層次的字型名稱。

對於要識別為標題的文字區域，它必須符合特定陣列項目中定義的所有參數。如果所定義的參數太有彈性，則所識別的標題可能超過您預期的數量。如果您多次嚴格定義每一個標題層次，以確保包含所有標題層次變異，而不包含無效的相符項，則會有較好的結果。


### Word
{: #word}

`word` 轉換物件會定義應如何將 PDF 文件轉換成 HTML，並具有下列結構：

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

Microsoft Word 轉換物件的運作方式類似 PDF 轉換物件。不過，在從 Microsoft Word 文件擷取標題時，可以在 `heading` 物件內指定兩個不同的陣列。您可以使用這兩個標題擷取陣列的其中一個或兩個，從 Microsoft Word 文件中擷取標題層次元素。

`fonts` 陣列中的每一個項目會透過下列參數使用字型特徵來指定標題層次：

- `"level": INT` - *必要* - 以這些參數識別的文字將轉換成的 HTML `h` 層次。
- `"min_size": INT` - _選用_ - 識別為此標題層次的最小字型大小。
- `"max_size": INT` - _選用_ - 識別為此標題層次的最大字型大小。
- `"bold": boolean` - _選用_ - 若為 `true`，則僅將粗體字型識別為此標題層次。
- `"italic": boolean` - _選用_ - 若為 `true`，則僅將斜體字型識別為此標題層次。
- `"name": "string"` - _選用_ - 識別為此標題層次的字型名稱。

對於要識別為 `font` 陣列中標題的文字區域，它必須符合特定陣列項目中定義的所有參數。如果所定義的參數太有彈性，則所識別的標題可能超過您預期的數量。如果您多次嚴格定義每一個標題層次，以確保包含所有標題層次變異，而不包含無效的相符項，則會有較好的結果。

`styles` 陣列中的每一個項目會從套用至該段落的 Microsoft Word 樣式指定標題層次。

- `"level": INT` - *必要* - 以這些參數識別的文字將轉換成的 HTML `h` 層次。
- `"names": array` - *必要* - 以逗點區隔的樣式名稱陣列，這些樣式名稱將識別為此標題層次。

*何時使用字型及何時使用樣式* - 如果您的 Microsoft Word 文件十分符合樣式表，且每一個段落都正確標記了適當樣式，則建議您使用 `styles` 來擷取標題。然而，您可能會發現部分文件具有作者手動改寫的樣式。使用 `fonts` 擷取方法時，這些文件更可能提供良好的轉換。
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

`"exclude_tags_completely" : array` - 將排除的 HTML 標籤名稱的陣列。這包括標籤、內容及任何已定義的標籤屬性。

#### exclude_tags_keep_content

`"exclude_tags_keep_content" : array` - 移除標籤資訊的 HTML 標籤名稱的陣列。這會導致刪去 HTML 標籤及任何標籤屬性。除非已指定，否則不會進一步刪去標籤的內容。例如，如果您對 `span` HTML 標籤指定 `exclude_tags_keep_content`，則會刪去 `<span class="info">Some <strong>Information</strong></span>`，變成：`Some <strong>Information</strong>`

#### exclude_content

`"xpaths" : array` - 識別所移除內容的 XPaths 陣列。如果設定此值，則會從輸出中移除符合其中一個 XPath 的任何項目。

#### keep_content

`"xpaths" : array` - 識別所轉換內容的 XPaths 陣列。如果設定此值，則符合其中一個 XPath 的任何項目都會包含在輸出中。在 `exclude_content` 所指定的任何處理之後，會處理此參數所指定的併入項目。

#### exclude_tag_attributes

`"exclude_tag_attributes" : array` - 轉換所移除之 HTML 屬性名稱的陣列（不管它們出現在哪一個 HTML 標籤中）。**附註：**如果您在相同的配置中同時指定 `exclude_tag_attributes` 和 `keep_tag_attributes`，將會收到錯誤訊息（每個配置只能指定一個）。如果出現的話，必須從配置中完全移除 `keep_tag_attributes`；它不能以空陣列呈現。

#### keep_tag_attributes

`"keep_tag_attributes" : array` - 轉換所保留的 HTML 屬性名稱的陣列。**附註：**如果您在相同的配置中同時指定 `keep_tag_attributes` 和 `exclude_tag_attributes`，將會收到錯誤訊息（每個配置只能指定一個）。如果出現的話，必須從配置中完全移除 `exclude_tag_attributes`；它不能以空陣列呈現。

#### extracted_fields

此物件會定義 HTML 原始檔中要在轉換時擷取至個別 JSON 欄位的任何內容。可使用 CSS 選取器來識別內容。

您要建立的每一個欄位由物件定義，如下所示：

```json
"{field_name}": {
  "css_selector": "{CSS_selector_expression_1}",
  "type": "{field_type}"
}
```
{: codeblock}

- `"{field_name}"` - 要建立的欄位名稱。

**附註：**在配置中定義的欄位名稱必須符合[欄位名稱需求](#field_reqs)中定義的限制。

- `"css_selector" : string` *必要* - 可定義要儲存在欄位中的內容區域的 CSS 選取器表示式。
- `"type" : string` *必要* - 要建立的欄位類型可以是 `string`、`date`
如需詳細資訊，請參閱[使用 CSS 選取器來擷取欄位](/docs/services/discovery/building.md#using-css)。

### 區段
{: #segment}

`segment` 物件是一組配置選項，可根據所識別的 HTML 標題（`h1`、`h2`）將所汲取的文件分割為一個以上的區段。

```json
"segment": {
  "enabled": true,
  "selector_tags": ["h1", "h2", "h3", "h4", "h5", "h6"]
}
```
{: codeblock}

- `"enabled": boolean` - *必要* - 必須設定為 `true`，才能啟用文件分段。
- `"selector_tags": array` - *必要* - 以逗點區隔的 HMTL `h` 標籤陣列，這些標籤用來分割文件。

概括來看，當啟用文件分段時，無法指定下列項目：

-  `json_normalizations` 無法指定作為配置的一部分。
-  `normalizations` 無法指定作為配置的一部分。
-  `html` 轉換的 `extracted_fields` 選項無法指定作為配置的一部分。

如需詳細資訊，請參閱[執行分段](/docs/services/discovery/building.html#performing-segmentation)。


### JSON
{: #json}

您可以在 `json_normalizations` 陣列中定義 `operation` 物件，以執行所汲取 JSON 的預先強化正規化。

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

#### Operations 物件
{: #operations}

- `"operation": string` - *必要* - 將對 JSON 執行的作業必須是下列其中一項：
  - `remove` - 將從 JSON 中移除所指定的 `source_field`。
  - `copy` - 指定的 `source_field` 內容將複製到 `destination_field` 的新實例。
  - `move` - 指定的 `source_field` 將重新命名為 `destination_field`。如果 `destination_field` 已存在，則會建立 `destination_field` 的新實例。
  - `merge` - `source_field` 和 `destination_field` 的內容會合併到 `destination_field` 中。
  - `remove_nulls` - 會移除含有 `null` 內容的欄位。
- `"source_field": string` - _選用_ - 將執行作業的欄位。
- `"destination_field": string` - _選用_ - 作業將輸出至其中的目的地欄位。  

  **附註：**在配置中定義的欄位名稱必須符合[欄位名稱需求](#field_reqs)中定義的限制。


## 強化
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

{{site.data.keyword.discoveryshort}} 支援新增 {{site.data.keyword.nlushort}} 及「元素分類」強化。您要強化的每一個欄位是由 `enrichments` 陣列中的某個物件所定義。每一個強化物件都需要指定 `source_field`、`destination_field` 及強化。

- `"enrichment" : string` - *必要* - 要用於此欄位的強化類型。若要擷取 {{site.data.keyword.nlushort}} 強化，請使用 `natural_language_understands`，若要執行「元素分類」，請使用 `elements`。

  **附註：**使用 `elements` 強化時，務必遵循[元素分類](/docs/services/discovery/element-classification.html)文件中指定的準則。特別是，指定此強化時，只能汲取 PDF 檔案。

- `"source_field" : string` - *必要* - 將強化的來源欄位。在 `json_normalizations` 作業完成之後，此欄位必須存在於來源中。
- `"destination_field" : string` - *必要* - 將建立強化的儲存器物件的名稱。

  **附註：**在配置中定義的欄位名稱必須符合[欄位名稱需求](#field_reqs)中定義的限制。

### 元素分類強化

使用「元素分類」時，每一個 `elements` 強化物件必須包含 `"options": {}` 物件，並指定了下列參數：

- `"model" : string` - *必要* - 要與此文件一起使用的元素擷取模型。目前支援的模型為：`contract`

**附註：**使用 `elements` 強化時，務必遵循[元素分類](/docs/services/discovery/element-classification.html)文件中指定的準則。特別是，指定此強化時，只能汲取 PDF 檔案。

### Natural Language Understanding 強化

使用 {{site.data.keyword.nlushort}} 時，`enrichments` 陣列內的每一個物件也必須包含 `"options": { "features": { } }` 物件，該物件包含下列其中一個以上的強化：

### categories

`categories` 強化會識別所汲取文件中的任何一般種類。此強化沒有選項，而且必須指定為空物件 `"categories" : {}`

### concepts

`concepts` 強化會根據存在於該文字中的其他概念和實體，尋找與輸入文字相關聯的概念。

- `"limit" : INT` - *必要* - 要從所汲取文件中擷取的概念數上限。

### emotion

`emotion` 強化會評估整份文件的整體情緒語氣（例如 `anger`），或是整份文件中指定的目標字串。此強化只能與英文內容搭配使用。

- `"document" : boolean ` _選用_ - 若為 `true`，將評估整份文件的情緒語氣。
- `"targets" : array ` _選用_ - 以逗點區隔的目標字串陣列，以評估文件內其情緒狀態。

### entities

`entities` 強化會擷取已知實體（例如，人員、位置及組織）的實例。可選擇性地指定 {{site.data.keyword.knowledgestudioshort}} 自訂模型來擷取自訂實體。

- `"sentiment" : boolean` - _選用_ - 若為 `true`，會在周圍內容的上下文中，對擷取的實體執行觀感分析。
- `"emotion" : boolean` - _選用_ - 若為 `true`，會在周圍內容的上下文中，對擷取的實體執行情緒語氣分析。
- `"limit" : INT` - _選用_ - 要從所汲取文件中擷取的實體數目上限。預設值為 `50`。
- `"mentions": boolean` - _選用_ - 若為 `true`，會記錄提及此實體的次數。預設值為 `false`。
- `"mention_types": boolean` - _選用_ - 若為 `true`，會儲存每一次提及此實體的提及類型。預設值為 `false`。
- `"sentence_location": boolean` - _選用_ - 若為 `true`，會儲存每一次提及實體的句子位置。預設值為 `false`。
- `"model" : string` - _選用_ - 若指定，則會使用自訂模型來擷取實體，而非公用模型。此選項需要 {{site.data.keyword.knowledgestudioshort}} 自訂模型與 {{site.data.keyword.discoveryshort}} 的實例相關聯。如需相關資訊，請參閱[與 Watson Knowledge Studio 整合](/docs/services/discovery/integrate-wks.html)。

### keywords

`keywords` 強化會擷取文字內重要文字的實例。若要瞭解關鍵字、概念和實體之間的差異，請參閱：[瞭解實體、概念和關鍵字之間的差異](/docs/services/discovery/building.html#udbeck)。

- `"sentiment" : boolean` - _選用_ - 若為 `true`，會在周圍內容的上下文中，對擷取的關鍵字執行觀感分析。
- `"emotion" : boolean` - _選用_ - 若為 `true`，會在周圍內容的上下文中，對擷取的關鍵字執行情緒語氣分析。
- `"limit" : INT` - _選用_ - 要從所汲取文件中擷取的關鍵字數目上限。預設值為 `50`。

### semantic_roles

`semantic_roles` 強化會識別所汲取文字內的句子元件，例如主旨、動作及物件。

- `"entities" : boolean` - _選用_ 若為 `true`，會從句子元件中擷取實體。
- `"keywords" : boolean` - _選用_ 若為 `true`，會從句子元件中擷取關鍵字。
- `"limit" : INT` - _選用_ - 要從所汲取文件中擷取的 `semantic_roles` 物件（要剖析的句子）數上限。預設值為 `50`。

### sentiment

`sentiment` 強化會評估整份文件的整體觀感層次，或是整份文件中指定的目標字串。

- `"document" : boolean ` _選用_ - 若為 `true`，將評估整份文件的觀感。
- `"targets" : array ` _選用_ - 以逗點區隔的目標字串陣列，以評估文件內的觀感。

### relations

`relations` 強化會擷取文件內所識別實體之間的已知關係。可選擇性地指定 {{site.data.keyword.knowledgestudioshort}} 自訂模型來擷取自訂關係。

- `"model" : string` - _選用_ - 若指定，則會使用自訂模型來擷取關係，而非公用模型。此選項需要 {{site.data.keyword.knowledgestudioshort}} 自訂模型與 {{site.data.keyword.discoveryshort}} 的實例相關聯。如需相關資訊，請參閱[與 Watson Knowledge Studio 整合](/docs/services/discovery/integrate-wks.html)。

## Normalization
{: #normalization}

`normalizations` 是 JSON `operation` 物件的陣列，用來在套用 `enrichments` 之後及儲存所汲取 JSON 之前清除 JSON。

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

[這裡](#operations)列出 `operation` 物件選項

## 欄位名稱需求
{: #field_reqs}

欄位名稱不能包含空格。下列字元和字串已保留，無法使用於欄位名稱：


```
  .  ,  # ? :
  id
  score
  highlight
  result_metadata
```
{: pre}

`_`、`+` 及 `-` 字元無法用來作為 `field_name` 的字首

`0 - 9` 數字字元不得為欄位名稱的字尾（例如 `extracted-content2`）。這些欄位名稱會進行檢索，但無法查詢。
