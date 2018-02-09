---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-15"

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

- 合約的 Natural Language Understanding，其中強調「軟體採購合約與法規」文件
- 將程式化 PDF 轉換成標註 JSON 的能力
- 符合主題專門知識之法律實體和種類的識別

「元素分類」結合一組功能豐富的整合型自動化 Watson API，以輸入程式化 PDF 來識別：小節、清單（有編號及項目符號）、註腳和表格，將這些項目轉換成結構化 HTML 格式。此外，這種結構化格式的分類會標註並輸出為具有含標籤元素、類型和種類的 JSON。

「元素分類」可安全地傳輸在進行中或靜止時執行加密的資料。如需 IBM Cloud 安全的相關資訊，請參閱 [IBM Cloud 服務說明 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=IBM+Bluemix+Service+Description){: new_window}。

## 分類需求

若要使用「元素分類」來分類文件，您的配置及來源文件必須符合下列需求：

- 要分析的檔案為 PDF 格式。
- PDF 內容為文字格式（已掃描但未進行 OCR 的文件無法進行剖析）

  **附註：**您可以透過在 PDF 檢視器中開啟文件，並使用**文字選取**工具來選取單字，以識別文字格式的 PDF。如果您無法在文件中選取單字，則無法剖析該檔案。

- 檔案大小不超過 50MB。
- 無法剖析受保護的 PDF（要使用密碼才能開啟）及編輯受限的 PDF（要使用密碼才能進行編輯）。
- 必須建立一個包含 `elements` 強化的自訂 {{site.data.keyword.discoveryshort}} 配置。此配置只能用來汲取 PDF 文件。
- **精簡**和**標準**方案每個月最多可以處理 500 頁。
- 無法用於已訂閱**超值**方案的服務實例。

## 集合需求

若要使用「元素分類」，必須配置集合以符合下列特定需求：

- `PDF` 轉換設定（如已指定）會被忽略。
- `WORD` 轉換設定可以省略，因為指定「元素分類」時無法汲取 Microsoft Word 檔案。
- `html` 正規化設定（如已指定）會被忽略。
- 指定 `elements` 強化時，不支援文件分割。
- 在 {{site.data.keyword.discoveryshort}} 配置中，`html` 欄位必須透過 `elements` 強化來強化，而且 `model` 已指定為 `contract`。在下列範例中，`destination_field` 為 `enriched_html`，但可以使用任何有效的名稱：

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

您可以使用 {{site.data.keyword.discoveryshort}} 工具來新增這些選項，建立自訂配置，並將**元素分類**強化新增至 `html` 欄位。

**附註：**當您使用工具新增**元素分類**時，`destination_field` 會設為 `enriched_html_elements`。

在建立自訂配置之後，它便可以用於任何集合中，只要指定了自訂配置，就可以使用任何方法來上傳文件。如果您不熟悉如何建立集合及上傳文件，請參閱[開始使用工具](/docs/services/discovery/getting-started-tool.html)。

## 分類的元素

使用「元素分類」檢索文件之後，將傳回文件，並以 `elements` 陣列作為可搜尋文件的一部分。

`elements` 陣列中的每一個物件說明「元素分類」已識別的一個合約元素。下列程式碼代表一般元素：

```
{
   "sentence" : {
     "begin" : 34941,
     "end" : 35307
   },
   "sentence_text" : "A buyer must buy from the supplier.",
   "types" : [ {
     "label" : {
       "nature" : "Obligation",
       "party" : "Supplier"
     },
     "assurance" : "High"
   } ],
   "categories" : [ {
     "label : "Responsibilities",
     "assurance : "High"
     }
   ]
}
```

元素有四個重要區段：

- `sentence_text` - 已分析的文字。
- `sentence` - 這個物件說明在轉換的 HTML 中找到元素的位置，它包含起始字元值及結束字元值。
- `types` - 這個陣列說明元素為何以及它影響的對象，它包含一組以上的 `party`（受句子影響的對象）和 `nature`（句子對所識別之參與方的影響）。
- `categories`  - 這個陣列列出所識別的句子所屬的功能種類。句子的主題。

**附註**：有些句子不屬於任何類型或種類，在該情況下，所傳回的 `types` 和 `categories` 陣列是空的。

**附註：**有些句子涵蓋多個主題，因此傳回句子時會列出多個 `types` 和 `categories` 項目。

此外，任何已識別的參與方也會定義在 parties 陣列中：

```
  "parties" : [ {
    "party" : "Customer",
    "role" : "Buyer"
  } ]
```

parties 陣列的每一個元素有兩個重要區段：

- `party` -  已識別為文件內的一個參與方的文字。
- `role` - 已識別之參與方的角色。角色會根據子網域而變更，如需可能的角色清單，請參閱所指定的子網域的相關資訊。無法識別為特定角色的參與方會標示為


## 瞭解合約元素

透過「元素分類」剖析的合約傳回時已分析每個所識別的元素。

下列各節說明傳回的 JSON 如何說明分析。

### 類型

元素 `types` 資訊是物件的陣列，每一個物件都包含已識別為此元素之聯體的本質及參與方。下表說明可識別的可能 `natures` 和 `parties`。

本質是句子需要的動作類型。

| **本質**| **說明** |
| --- | --- |
| Definition | 本元素進一步釐清條款/關係等等。履行此元素並不需要任何動作，且任何參與方均不受影響。|
| Disclaimer | 元素中的參與方沒有義務履行該元素中的特定條款，但不會禁止其履行。|
| Exclusion | 元素中的參與方將不履行該元素所指出的特定條款。|
| Obligation | 元素中的參與方需要履行該元素的條款。|
| Right | 保證元素中的參與方接受該元素的條款。|

### 參與方

對於每一個已識別的條款，會依名稱識別受影響的參與方。然後會依 `role` 將每一個識別的參與方加以分類。參與方是指合約中的參與者。可以針對合約識別的角色如下所示：

| **角色** | **說明** |
| --- | --- |
| `Buyer` | 負責支付商品/服務的參與方。|
| `End User` | 將與實際商品/服務互動的參與方，與 Buyer 明確區別。|
| `None` | 未識別此元素的任何參與方，一律與 Definition 本質搭配。|
| `Supplier` | 負責提供商品/服務的參與方。|

### 種類

種類定義句子的主題。可以識別下列種類。

| **種類** | **說明** |
| --- | --- |
| `Amendments` | 對原始合約進行的修改，其規定變更條款的條件。|
| `Asset Use` | 合約中任一方將使用之任何資產的詳細資料。|
| `Assignments` | 將一方保留的權利轉讓給另一方。|
| `Audits` | 此條款可讓買方檢查或檢驗所提供服務的供應商。|
| `Communication` | 說明可接受的通訊方法及聯絡資訊。|
| `Confidentiality` | 說明如何處理機密或私人資訊，例如誰可以分享什麼內容以及如何分享。|
| `Business Continuity` | 說明在發生干擾性突發事件時，組織將如何在預先定義的層次上繼續交付工作。|
| `Definitions` | 定義文件中所使用條款的區段。|
| `Deliverables` | 在一項工作結束時所要交付的項目或服務。|
| `Delivery` | 用來完成專案的特定排程或處理程序。|
| `Dispute Resolution` | 針對合約雙方之間產生的任何爭議及其處理方式而提供。|
| `Force Majeure` | 讓雙方在遭遇干擾性事件時免除責任的條款。|
| `Indemnification` | 說明違反條款時的補救措施或後果。|
| `Insurance` | 說明供應商必須提供的承保級別。|
| `Intellectual Property` | 與專利、著作權及商標相關的條款。更概括地說，可能與發明、作者或技術相關。|
| `Liability` | 說明每一方責任的義務與限制。|
| `Miscellaneous` | 不符合其他種類的權益區段。|
| `Payment Terms & Billing` | 說明應付款項及付款的排程。|
| `Pricing & Taxes` | 說明如何定價以及如何報稅|
| `Privacy` | 說明適用的隱私權規定。|
| `Responsibilities` | 說明每一方的責任為何。|
| `Safety and Security` | 說明要如何防止傷害對方。包括人員及實體資產安全。|
| `Scope of Work` | 說明工作說明書所詳述參與方將達成的項目。|
| `Subcontracts` | 與涉及履行需求的任何協力廠商相關。|
| `Term & Termination` | 將發生事件的時間，以及它可能在何種條件下結束。|
| `Warranties` | 供應商對於產品運作方式的保證。|

### 保證

「元素分類」所識別的每個項目（類型或種類）都會獲得 `assurance` 評等。可能的保證值說明如下：

| **保證** | **說明** |
| --- | --- |
| `High` | 有明顯證據顯示所給定的分類足以代表內容。|
| `Low` | 有一些證據能夠支援分類，但可能需要進一步檢閱才能確認。|
