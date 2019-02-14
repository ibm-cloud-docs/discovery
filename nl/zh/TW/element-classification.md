---

copyright:
  years: 2015, 2018
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

# 元素分類
{: #element-classification}

「元素分類」可透過控管文件進行快速剖析，以轉換、識別及分類重要元素。使用最先進的「自然語言處理程序」時，會從文件的元素中擷取參與方（它所參照的對象）、本質（元素類型）以及種類（特定類別）。

「元素分類」的設計是為了提供：

-  合約的 Natural Language Understanding，並強調「軟體採購合約」
-  將程式化 PDF 轉換成標註 JSON 的能力
-  符合主題專門知識之法律實體和種類的識別

「元素分類」結合一組功能豐富的整合型自動化 Watson API，以輸入程式化 PDF 來識別：小節、清單（有編號及項目符號）、註腳和表格，並將這些項目轉換成結構化 HTML 格式。此外，這種結構化格式的分類會標註並輸出為具有含標籤元素、類型和種類的 JSON。

「元素分類」可安全地傳輸資料，並在進行中或靜止時執行加密。如需 IBM Cloud 安全的相關資訊，請參閱 [{{site.data.keyword.Bluemix_notm}} 服務說明 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=%28IBM+Cloud+Service+description%29){: new_window}

「元素分類」傳回包含下列各項的 JSON 物件：

-  `docments` 物件，其包含輸入文件的標題、輸入文件的 HTML 版本，以及輸入文件的 MD5 雜湊值。
-  用來分類輸入文件之模型的相關資訊。  
-  `elements` 陣列，其詳述輸入文件中所識別的語意元素。
-  `tables` 陣列，其分解輸入文件中所識別的表格。
-  `document_structure` 物件，其列出輸入文件中所識別的區段標題及前導句子。
-  `parties` 陣列，其列出輸入文件中所識別的參與方、角色、地址及參與方的聯絡人。
-  定義 `effective_dates` 和 `contract_amounts` 的陣列。

目前此特性僅支援英文版，如需詳細資料，請參閱[語言支援](/docs/services/discovery/language-support.html#feature-support)。


## 分類需求
{: #element-class}

若要使用「元素分類」來分類文件，您的配置及來源文件必須符合下列需求：

-  要分析的檔案為 PDF 格式。
-  PDF 內容是以文字形式表示。無法剖析已掃描的文件，即使它們已經過 OCR 辨識也一樣。**附註：**您可以透過在 PDF 檢視器中開啟文件，並使用**文字選取**工具來選取單字，以識別文字格式的 PDF。如果您無法在文件中選取單字，則無法剖析該檔案。
-  檔案大小不超過 50MB。
-  無法剖析受保護的 PDF（要使用密碼才能開啟）及編輯受限的 PDF（要使用密碼才能進行編輯）。
-  {{site.data.keyword.discoveryshort}} 工具包括一個名稱為 **Default Contract Configuration** 的配置，可用來強化您的 PDF 文件集合。您也可以選擇建立包含 `elements` 強化的自訂配置。如需詳細資料，請參閱[集合需求](/docs/services/discovery/element-classification.html#element-collection)。
-  **精簡**方案每個月最多可以處理 500 頁。
-  無法用於**專用**環境。
-  使用「元素分類」時，無法執行強化後的正規化。

**附註**：**Default Contract Configuration** 檔已於 2018 年 9 月 25 日更新。如果您在此日期之前就已將此配置套用至集合，請參閱[版本注意事項](/docs/services/discovery/release-notes.html#25sept)，以取得更新集合的相關資訊。

## 集合需求
{: #element-collection}

若要使用「元素分類」，必須配置集合以符合特定需求。

{{site.data.keyword.discoveryshort}} 工具包含一個名稱為 **Default Contract Configuration** 的配置，該配置已預先配置為使用**元素分類**強化及其他必要選項來強化 PDF 文件。您可以在建立集合時選擇此配置。此配置的 JSON 如下：

```json
 {
   "name": "Default Contract Configuration",
   "description": "Extract party, nature, and category from elements in PDFs.",
   "conversions": {
     "html": {
       "exclude_tags_completely": [],
       "exclude_tags_keep_content": []
     }
   },
   "enrichments": [
     {
       "source_field": "html",
       "destination_field": "enriched_html_elements",
       "enrichment": "elements",
       "options": {
         "model": "contract"
    }
  }
   ]
 }
```
{: codeblock}

如果您要建立自訂配置檔，請配置您的集合，使其符合下列需求：  

-  `PDF` 轉換設定（如已指定）會被忽略。
-  `WORD` 轉換設定可以省略，因為指定「元素分類」時無法汲取 Microsoft Word 檔案。
-  `html` 正規化設定（如已指定）會被忽略。
-  指定 `elements` 強化時，不支援文件分段。
-  在 {{site.data.keyword.discoveryshort}} 配置中，`html` 欄位必須透過 `elements` 強化來強化，而且 `model` 必須指定為 `contract`。在下列範例中，`destination_field` 為 `enriched_html`，但可以使用任何有效的名稱：

```json
"enrichments": [
   {
     "source_field": "html",
    "destination_field": "enriched_html",
    "enrichment": "elements",
    "options": {
      "model": "contract"
    }
  }
 ]
```
{: codeblock}

在工具中選取 `Default Contract Configuration` 之後，您就可以上傳文件。如果您不熟悉如何建立集合及上傳文件，請參閱[開始使用工具](/docs/services/discovery/getting-started-tool.html)。

## 分類的元素

使用「元素分類」檢索文件之後，將傳回文件，並以 `elements` 陣列作為可搜尋文件的一部分。

`elements` 陣列中的每個物件說明 {{site.data.keyword.discoveryshort}} 已識別之合約的元素。下列程式碼代表一般的元素：

```json
 {
    "location" : {
     "begin" : 134323,
     "end" : 135109
    },
    "text" : "9. In the event that the Participant's total vested account balance is determined to be less than or equal to $2,000.00 as of the date that the Order is received, the parties will be informed in writing that the QDRO determination fee may potentially liquidate the account.",
    "types" : [ {
      "label" : {
        "nature" : "Obligation",
        "party" : "All Parties"
      },
      "provenance_ids" : ["Nlu0ogWAEGms4vjhhzpMv3iXhm8b8fBqMBNtT/bXH8JI=", "PlyERkjg5is36RpFjVUFXp69eDmGmCxLCXRs1sDMDUCo="
      ]
    } ],
    "categories" : [ {
      "label" : "Communication",
      "provenance_ids" : [ "Cs38YyU6VBFtJK1/bgtEJBlqqWmX5F6OYUciRxQXf7HrN5TOCPuI7QXbkbj4LRXoxVuB3/i9H15q5TU+vFxorhUBeWFfF998OYQiPYViD2yI="
      ]
    } ],
    "attributes" : [ {
      "type" : "Currency",
      "text" : "$2,000.00",
      "location" : {
        "begin" : 134780,
        "end" : 134789
      }
    } ]
 }
 ```
{: codeblock}

每個元素都有五個重要區段：
-  `location`：`begin` 和 `end` 索引，指出元素在輸入文件中的位置。
-  `text`：所分類元素的文字。
-  `types`：包含零個以上 `label` 物件的陣列。每個 `label` 物件都包含 `nature` 欄位，其列出該元素對於所識別參與方的作用（例如 `Right` 或 `Exclusion`），物件也包含一個 `party` 欄位，其識別受該元素影響的一個或多個參與方。如需相關資訊，請參閱[瞭解合約剖析](/docs/services/discovery/parsing.html#contract_parsing)中的[類型](/docs/services/discovery/parsing.html#contract_types)。
-  `categories`：包含零個以上 `label` 物件的陣列。每個 `label` 物件的值會列出所識別元素所屬的功能種類。如需相關資訊，請參閱[瞭解合約剖析](/docs/services/discovery/parsing.html#contract_parsing)中的[種類](/docs/services/discovery/parsing.html#contract_categories)。
-  `attributes`：這個陣列會列出定義元素屬性的零個以上物件。目前支援的屬性類型包含 `location`（元素所參照的地理位置或地區）、`DateTime`（元素指定的日期、時間、日期範圍或時間範圍）及 `Currency`（貨幣值和單位）。`attributes` 陣列中的每個物件也包含所識別元素的文字和位置；位置是由輸入文件中文字的 `begin` 和 `end` 索引所定義。如需相關資訊，請參閱[瞭解合約剖析](/docs/services/discovery/parsing.html#contract_parsing)中的[屬性](/docs/services/discovery/parsing.html#attributes)。

此外，`types` 和 `categories` 陣列中的每個物件都包含 `proventance_id` 陣列。`provenance_ids` 陣列中所列出的值是雜湊值，您可以將這些值傳送給 IBM，以針對與元素相關聯的分析部分提供意見或獲得支援。

**附註**：部分句子不屬於任何類型或種類，在此情況下，服務會以空物件傳回 `types` 和 `categories` 陣列。

**附註：**部分句子涵蓋多個主題，在此情況下，服務會傳回多組 `types` 和 `categories` 物件。

**附註**：部分句子不包含任何可識別的屬性，在此情況下，服務會以空物件傳回 `attributes` 陣列。
