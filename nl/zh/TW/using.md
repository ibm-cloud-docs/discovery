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

# 查詢概念
{: #query-concepts}

{{site.data.keyword.discoveryfull}} 服務提供強大的內容搜尋功能。透過 {{site.data.keyword.discoveryshort}} 服務上傳及強化內容之後，您可以建置查詢，然後將 {{site.data.keyword.discoveryshort}} 整合至您自己的專案，或使用 {{site.data.keyword.watson}} Explorer Application Builder 來建立自訂應用程式。
{: shortdesc}

  您撰寫的查詢會因集合而有所不同，因為所有集合都包含唯一的內容。
  {: tip}

當您建立查詢或過濾器時，{{site.data.keyword.discoveryshort}} 會查看每一個結果，並嘗試比對您已定義的路徑。當出現相符項時，會將它們新增至結果集。建立查詢時，視需要可以含糊也可以具體。查詢越具體，結果越鎖定目標。

您也可以選擇開啟段落擷取。段落是從查詢所傳回之完整文件擷取的簡短相關摘錄。這些已設定目標的段落是從您集合中文件的 `text` 欄位中擷取而來。依預設，針對每個查詢最多傳回 10 個段落，大約 400 個字元。最多從單一結果擷取三個段落。`passages` 參數只適用於專用集合；它無法使用於 {{site.data.keyword.discoverynewsshort}} 集合。如需如何識別段落的相關資訊，請參閱[段落](/docs/services/discovery/query-parameters.html#passages)。

  您可以使用 {{site.data.keyword.discoveryshort}} 工具或 API 來撰寫自然語言查詢（例如 "IBM Watson partnerships"）。
  {: tip}

經過訓練的集合將在自然語言查詢的結果中傳回 `confidence` 評分。如需詳細資料，請參閱[信賴度評分](/docs/services/discovery/train-tooling.html#confidence)。

{{site.data.keyword.discoveryshort}} 會傳回包含下列語言之特殊字元的查詢結果：英文、德文、法文、荷蘭文、義大利文及葡萄牙文。比方說，如果您查詢 `aqui`，現在會同時收到 `aqui` 和 <code>aqu&iacute;</code> 的結果。

您可以建立較長、較複雜的查詢，其中包括多個過濾器和複式聚集。此選項只能在 API 中使用，並且將查詢的字元限制增加為 10,000 個字元。如需詳細資料，請參閱[長集合查詢 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query){: new_window} 和[長環境查詢 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#federated-query){: new_window}。

{{site.data.keyword.discoveryfull}} Knowledge Graph 是測試版特性，可提供新的端點來查詢文件之間的實體及關係。這包括以上下文為基礎的搜尋和相關性分級。如需相關資訊，請參閱 [{{site.data.keyword.discoveryfull}} Knowledge Graph](/docs/services/discovery/building-kg.html)。

如需撰寫查詢的相關資訊，請參閱：
- [開始使用查詢指導教學](/docs/services/discovery/getting-started-query.html)
- [查詢參考資料](/docs/services/discovery/query-reference.html)（包括「{{site.data.keyword.discoveryshort}} 查詢語言」可用的參數、運算子和聚集的清單）

## Discovery 資料綱目
{: #discovery-schema}

從認識 {{site.data.keyword.discoveryshort}} JSON 開始。若要瞭解如何使用「{{site.data.keyword.discoveryshort}} 查詢語言」來建置查詢，您需要熟悉 {{site.data.keyword.discoveryshort}} 在強化您集合中的文件之後所產生的 JSON。當您熟悉文件的資料綱目之後，就更容易使用「{{site.data.keyword.discoveryshort}} 查詢語言」來撰寫查詢。有三種方法可以達成此目的。

  1. 在 {{site.data.keyword.discoveryshort}} 工具中，開啟**管理資料**畫面，選擇包含 {{site.data.keyword.IBM_notm}} Press Releases 的集合。按一下**檢視資料綱目**按鈕。**檢視資料綱目**畫面以兩種方式來顯示轉換後文件中的欄位及值：依文件（**文件視圖**）或依欄位（**集合視圖**）。在**文件視圖**中，最多可顯示 50 份文件。**集合視圖**會顯示整個集合的欄位。

    在**集合視圖**的 `enriched_text` 下，您可以檢查您使用 **Default Configuration** 檔案所套用的強化。請按一下 `categories`、`concepts`、`entities` 及 `sentiment`，以查看您的集合因為 Watson 見解而有什麼樣的強化。

  1. 執行「空的」查詢來檢視 JSON。在**檢視資料綱目**畫面上，按一下**建置查詢**按鈕，然後按一下**執行查詢**。結果會顯示在右邊的兩個標籤下：**摘要**（查詢結果的概觀）和 **JSON**。從開啟 **JSON** 標籤開始。

     -  這四份文件中的每一份前面都有 `id` 號碼。
     -  向下捲動至 `enriched_text` 欄位。檢查每一個強化，以瞭解您可以查詢的 JSON 欄位。

        ![預設配置欄位](images/JSON.png)

     -  **entities** - 從尋找 `text` 欄位開始，並檢查其他強化資訊。
     -  **sentiment** - 從尋找 `label` 欄位開始，並檢查其他強化資訊。
     -  **concepts** - 從尋找 `text` 欄位開始，並檢查其他強化資訊。
     -  **categories** - 從尋找 `document` 欄位開始，並檢查其他強化資訊。

     檢查第一份文件中的見解之後，您可以查看其他三份文件。

  1. 在**視覺化查詢建置器**中檢視可用的欄位。在**建置查詢**畫面上，按一下**搜尋文件**，然後按一下**使用 {{site.data.keyword.discoveryshort}} 查詢語言**。按一下**欄位**下拉清單，以檢視資料中可用的欄位。按一下**以查詢語言編輯**，以使用「{{site.data.keyword.discoveryshort}} 查詢語言」來手動建置查詢。      

### 如何建構基本查詢
{: #structure-basic-query}

誠如您所看到的，JSON 為階層式，因此需要使用此相同階層來撰寫查詢。因此，如果您的 JSON 看起來如下：

```json
"enriched_text": {
  "concepts": [
    {
    "text": "Cloud computing",
    "relevance": 0.610029}
    ]
  }
```
{: codeblock}

您的查詢會建構如下：

![查詢結構範例](images/query_structure2.png)

  用來評估欄位的運算子（`<=` 、`>=`、`<`、`>`）需要 `number` 或 `date` 作為值。在值的周圍使用引號一律會使它成為 `string`。因此，`score>=0.5` 是有效的查詢，而 `score>="0.5"` 不是。如需運算子的完整清單，請參閱[查詢運算子](/docs/services/discovery/query-operators.html)。
  {: tip}

注意事項：

- 不確定何時要查詢實體、概念或關鍵字嗎？請參閱[瞭解實體、概念和關鍵字之間的差異](/docs/services/discovery/building.html#udbeck)。

- **附註：**按一下**執行查詢**並開啟 **JSON** 標籤之後，您會注意到依預設已開啟查詢強調顯示。這會將 `highlight` 欄位新增至您的查詢結果。在 `highlight` 欄位內，符合您查詢的單字會包裝在 HTML `<em>`（強調）標籤中。如需詳細資料，請參閱[查詢參數](/docs/services/discovery/query-parameters.html#highlight)。

## 建置合併查詢
{: #building-combined-queries}

您可以將查詢參數結合起來，以建置更多已設定目標的查詢。例如，您可以同時使用 `filter` 和 `query` 參數。如需過濾與查詢的相關資訊，請參閱 [filter 與 query 參數之間的差異](/docs/services/discovery/query-parameters.html#filtervquery)。

## 如何建構聚集
{: #structure-aggregation}

聚集會傳回一組資料值；例如，熱門關鍵字、實體的整體觀感等等。如需聚集選項的完整清單，請參閱[聚集](/docs/services/discovery/query-reference.html#aggregations)。

![聚集查詢結構範例](images/aggregation_structure.png)

此聚集範例會尋找您集合中的所有 `concepts`。此查詢中的定界字元是 `.`，運算子是 `()`，請參閱[查詢運算子](/docs/services/discovery/query-operators.html)，以瞭解「{{site.data.keyword.discoveryshort}} 查詢語言」中可用的其他運算子。

### 聚集查詢範例
{: #example-aggregations}

有數種類型的方式可讓您使用 {{site.data.keyword.discoverynewsshort}} 來聚集結果，包括前幾個值、總和、最小值、最大值、平均值、時間片段及直方圖。您也可以新增過濾器及巢狀聚集。

#### 過濾器聚集
{: #filter-aggregations}

此聚集範例會傳回在 {{site.data.keyword.discoverynewsshort}} 中找到有關 Pittsburgh Steelers 的文章數，以及這些結果有幾個有 `positive`、`negative` 或 `neutral` 觀感。

- `filter(enriched_text.entities.text:"Pittsburgh Steelers").term(enriched_text.sentiment.document.label,count:3)`


此聚集範例會先將 {{site.data.keyword.discoverynewsshort}} 中的文章集縮減（過濾）為只包含 twitter 實體文字的那些文章，然後依文件觀感類型來劃分這些文章。只會傳回前三個文件觀感類型（`positive`、`negative`、`neutral`）。

- `filter(enriched_text.entities.text:twitter).term(enriched_text.sentiment.document.label,count:3)`

#### 巢狀聚集
{: #nested-aggregations}

在聚集之前新增 `nested`，會將聚集限制為所指定結果的區域。例如：`nested(enriched_text.entities)` 表示只會使用任何結果的 `enriched_text.entities` 元件來進行聚集。

查看下列兩個查詢之間的差異，即可一目瞭然：
- `filter(enriched_text.entities.disambiguation.subtype::City)` - 此聚集會計算包含一個以上 `entity` 且類型為 `City` 的*結果*數
- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City)` - 此聚集會計算結果中類型為 `City` 的 `entity` 的實例數。  

此外，任何後續作業都會進一步限制可執行聚集的結果集。例如：

- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City)` 表示只會聚集 `subtype::City` 的實體。
- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City).term(enriched_text.entities.text,count:3)` 將聚集子類型為 `City` 的前 3 個實體
- `filter(enriched_text.entities.disambiguation.subtype::City).term(enriched_text.entities.text,count:3)` 將傳回前 3 個實體，其中的結果至少包含一個子類型為 `City` 的實體。

## 查詢 Watson Discovery News
{: #querying-news}

{{site.data.keyword.discoverynewsshort}} 是一個已利用認知見解預先強化的公用資料集，它也隨附於 {{site.data.keyword.discoveryshort}} 中。如需此集合的相關資訊，請參閱 [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html#watson-discovery-news)。

您可以使用自然語言查詢（例如 "IBM Watson partnerships"）或「{{site.data.keyword.discoveryshort}} 查詢語言」來查詢此集合。若要進一步瞭解自然語言查詢，請參閱[自然語言查詢](/docs/services/discovery/query-parameters.html#nlq)。

您無法調整 {{site.data.keyword.discoverynewsshort}} 配置、訓練，或將文件新增至 {{site.data.keyword.discoverynewsshort}} 集合中。請參閱[這裡 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://discovery-news-demo.ng.bluemix.net/){: new_window}，它示範使用 {{site.data.keyword.discoverynewsshort}} 可建置的內容。

您可以從 {{site.data.keyword.discoveryshort}} 工具和 API 使用英文、韓文、德文、西班牙文及日文語言的 {{site.data.keyword.watson}}{{site.data.keyword.discoverynewsshort}} 集合。

工具中的 {{site.data.keyword.watson}}{{site.data.keyword.discoverynewsshort}} 預設語言是英文。若要切換語言，您必須先按一下 ![管理資料](/images/icon_yourData.png) 圖示，然後從下拉清單中選擇適當的語言。

如需透過 API 查詢集合的相關資訊，請參閱 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection){: new_window}。Watson {{site.data.keyword.discoverynewsshort}} 英文語言版本的 `collection_id` 是 `news-en`。早期，`collection_id` 是 `news` - 如果您是使用先前的 `collection_id`，它會繼續運作，不過，您可能會想要針對新專案切換至新的 `collection_id`。韓語集合的 `collection_id` 是 `news-ko`、西班牙文的 `collection_id` 是 `news-es`、德文的 `collection_id` 是 `news-de`、日文的 `collection_id` 是 `news-ja`。

{{site.data.keyword.discoverynewsfull}} 查詢會於 `text` JSON 欄位中顯示每篇文章的前 50 個字。

針對 {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} 查詢傳回的結果數目上限是 `50`。使用其他查詢及 `offset` 參數，可傳回超過 `50` 個結果。

如果使用「{{site.data.keyword.discoveryshort}} 查詢語言」，您可以在 {{site.data.keyword.discoverynewsshort}} 查詢中包括相對日期範圍，例如：`crawl_date>=now-1month`。有效的日期間隔值為 `second/seconds`、`minute/minutes`、`hour/hours`、`day/days`、`week/weeks`、`month/months` 及 `year/years`。`now` 不受 `time_zone` 參數影響；`UTC` 時區為預設值。

此範例將在特定日期範圍內查詢關鍵字。時區資訊不是必要的：
- `enriched_text.keywords.text:"olympics", publication_date<=2018-02-15T00:00:00Z, publication_date>=2018-02-01T00:00:00Z`

新聞文章可能聯合供稿給數個新聞管道，{{site.data.keyword.discoverynewsfull}} 將挑選每一個新聞管道，這會導致文章重複。這表示對 {{site.data.keyword.discoverynewsfull}} 的查詢可能會在查詢結果中傳回數篇相同或幾乎相同的文章。您可以使用刪除重複來管理此功能。若要進一步瞭解這項測試版功能，請參閱[從查詢結果排除重複文件](/docs/services/discovery/query-parameters.html#deduplication)。

## 查詢多個集合
{: #multiple-collections}

如果您的環境中有多個集合，您可能會想要檢視這些集合之間的結果。`environments` 層次的查詢方法（`query`、`fields` 及 `notices`）可讓您查詢多個指定的集合。{{site.data.keyword.discoveryshort}} 工具目前無法使用集合之間的查詢。

您可以使用 `environments/{environment_id}/query` API 方法來查詢相同環境中的多個集合。在多個集合之間查詢時，請考量下列項目。
-  使用此方法時，必須指定 `collection_ids` 參數。`collection_ids` 是環境中要查詢的集合清單（以逗點區隔）。
-  查詢多個集合時，支援 `passages`。
-  會傳回 `collection_id`，作為每個結果物件的一部分。此欄位指定在其中找到結果的集合。
-  {{site.data.keyword.discoverynewsshort}} 是 `system` 環境的一部分，無法併入多個集合查詢中。
-  在查詢多個集合時，個別的集合相關性訓練不會影響結果的等級。若要重新分級查詢多個集合時傳回的結果，請實作[持續相關性訓練](/docs/services/discovery/continuous-training.html)。
-  即使查詢中的所有集合都已經過訓練，也不會對多個集合查詢的任何部分執行重新分級。

如需相關資訊，請參閱[多個集合查詢 API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-multi-collections){: new_window}。

您可以使用 `environments/{environment_id}/notices` API 方法來檢視相同環境中的多個集合之間的通知。
-  使用此方法時，必須指定 `collection_ids` 參數。`collection_ids` 是環境中要查詢的集合清單（以逗點區隔）。
-  查詢多個集合時，支援 `passages`。

如需相關資訊，請參閱[多個集合通知 API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#collections-notices){: new_window}。

您可以使用 `environments/{environment_id}/fields` API 方法來檢視相同環境中可用於集合之間的欄位。如需相關資訊，請參閱[多個集合欄位查詢 API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#multi-list-fields){: new_window}。

## 查詢擴展
{: #query-expansion}

您可以使用 {{site.data.keyword.discoveryshort}} API 上傳查詢擴展詞彙清單，藉以擴展完全相符的查詢範圍，例如，您可以擴展 "car" 的查詢，以包括 "automobile" 和 "motor vehicle"。查詢擴展詞彙通常是同義字、反義字或拼錯的一般詞彙。

您可以定義兩種類型的擴展：
- **雙向** - 每個 `expanded_term` 會擴展為包含所有擴展的詞彙。例如，`car` 的查詢會擴展為 `car OR automobile OR (motor AND vehicle)`。
- **單向** - 查詢中的 `input_terms` 會取代為 `expanded_terms`。例如，`ibm` 查詢可以擴展為 `international business machines` 和 `big blue`。`input_terms` 不會用來作為結果查詢的一部分。在前一個 `ibm` 範例中，查詢 `IBM` 會轉換為 `international business machines` OR `big blue`，而不包含原始詞彙。

這個檔案可用來作為建置查詢擴展清單的起點：
<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/expansions.json" download>expansions.json <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示" title="外部鏈結圖示" class="style-scope doc-content"></a>。您可以修改此檔案，以建立自訂查詢擴展清單。

雙向範例：
```JSON
 {
   "expansions": [
     {
       "expanded_terms": [
         "car",
         "automobile",
         "motor vehicle"
       ]
     }
   ]
 }
```
{: codeblock}

單向範例：
```JSON
 {
   "expansions": [
     {
      "input_terms": [
        "ibm"
       ],
      "expanded_terms": [
        "ibm",
        "international business machines",
        "big blue"
       ]
     }
   ]
 }
```
{: codeblock}

查詢擴展的相關注意事項：

- 查詢擴展僅適用於專用集合。可用的 `expansions` 陣列數目（雙向和單向陣列總計）及詞彙數目（`input_terms` 加上 `expanded_terms`）依方案而異。如需詳細資料，請參閱 [Discovery 定價方案](/docs/services/discovery/pricing-details.html)。**附註：**所有查詢詞彙（`input_terms` 和 `expanded_terms`）各計為一個詞彙。這個範例包含 `expansions` 陣列中的兩個物件和八個詞彙字串。

```JSON
 {
   "expansions": [
     {
      "input_terms": [
         "ibm"
       ],
      "expanded_terms": [
         "ibm",
         "international business machines",
         "big blue"
       ]
     },
     {
      "input_terms": [
         "banana"
       ],
      "expanded_terms": [
         "banana",
         "plantain",
         "fruit"
       ]
     }
   ]
 }
```
{: codeblock}

- 每個集合只能上傳一個查詢擴展清單；如果上傳第二個擴展清單，則會取代第一個清單。
- 所有 `input_terms` 和 `expanded_terms` 都應該是小寫。小寫詞彙將會擴展到大寫。
- 查詢擴展清單必須以 JSON 撰寫。
- 若要停用查詢擴展，請刪除查詢擴展清單。
- 您目前無法使用 {{site.data.keyword.discoveryshort}} 工具來上傳或刪除查詢擴展清單；必須使用 {{site.data.keyword.discoveryshort}} API 來執行。
- 查詢擴展是在 `query` 和 `multiple collection query` 方法上執行。查詢擴展不會在 Knowledge Graph 查詢上執行。
- 每一組擴展都與某個集合相關聯。跨[多個集合](/docs/services/discovery/using.html#multiple-collections)查詢時，會個別展開每個集合。
- 查詢擴展會在查詢時套用，但不會在檢索時套用，因此可以更新查詢擴展清單，而不需要重新汲取文件。
- 將文件汲取到集合的同時，請不要上傳或刪除查詢擴展清單。這可能會導致索引在該短暫期間內無法使用。

如需上傳及刪除查詢擴展檔案的 API 指令，請參閱[查詢擴展 API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-expansion){: new_window}。

## 自訂記號化字典

記號化會將文字分解成稱為記號的單位。您的集合會套用標準記號化字典，但您可以上傳自訂的記號化字典，來改善領域或語言的搜尋精確度。自訂字典將會置換標準字典。您可以使用 {{site.data.keyword.discoveryshort}} API 來上傳字典。 

如需上傳及刪除記號化檔案的 API 指令，請參閱[記號化 API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#create-tokenization-dictionary){: new_window}。 

**附註：**這個特性目前只適用於日文集合。 

在下列範例中，**text** 是將在遇到時記號化的詞組，**tokens** 是 **text** 將會分割成的字組。**Readings** 會列出不同字集所代表的記號版本，**part_of_speech** 是記號所代表的詞性。

使用此自訂字典，如果您搜尋下列文字：`ネコ`，搜尋結果將包括含有 `すしネコ` 的文字，以及只含有 `ネコ` 的文字。

```
{ "tokenization_rules":
  [
    {
      "text":"すしネコ",
      "tokens":[
        "すし",
        "ネコ"
      ],
      "readings":[
        "寿司",
        "ネコ"
      ],
      "part_of_speech":"カスタム名詞"
    },
    ...
  ]
}
```

您也可以使用單一記號建立規則。在此範例中，`ibm発見` 將記號化為單一記號，因此不會分解成較小單位。

```
{ "tokenization_rules":
  [
    {
      "text":"ibm発見",
      "tokens":[  
      "ibm発見"
      ],
      "readings":[  
      "ibm発見"
      ],
      "part_of_speech":"カスタム名 詞"
    },
    ...
  ]
}
```

- 記號化會在檢索和查詢時發生。 
- 所有集合都會使用標準記號化字典。如果您的集合已使用該字典進行檢索，則您必須在上傳自訂記號化字典之後，重新汲取該集合中的文件。
- 每個集合只能上傳一個記號化字典；如果上傳第二個記號化字典，則會取代第一個字典。如果該集合已包含文件，您必須重新汲取這些文件，才能套用新的自訂記號化字典。
- 必須以 JSON 撰寫自訂記號化字典，範例檔名：`custom_tokenization_dictionary.json`。
- 若要停用記號化，請刪除記號化字典並重新汲取您的文件。
- 您目前無法使用 {{site.data.keyword.discoveryshort}} 工具來上傳或刪除記號化字典；必須使用 {{site.data.keyword.discoveryshort}} API 來執行。
- 記號化是在 `query` 和 `multiple collection query` 方法上執行。記號化不會在 Knowledge Graph 查詢上執行。
- 每個記號化字典都與某個集合相關聯。跨[多個集合](/docs/services/discovery/using.html#multiple-collections)查詢時，會個別將每個集合記號化。
- 將文件汲取到集合的同時，請不要上傳或刪除記號化字典。 

## 文件相似性
{: #doc-similarity}

文件相似性查詢將找到與目前檢視文件類似的其他文件，例如，客服中心操作員可以檢視產品的手冊，並使用文件相似性尋找具有類似性質的其他文件。您可以透過 `similar.document_ids` 查詢類似的文件，並選擇性地指定其他 `similar.fields` 來修正相似性。

文件相似性的判定方式是從原始文件中擷取 25 個相關詞彙，然後搜尋具有類似相關詞彙的文件。

透過 `similar.document_ids` 查詢的範例（如果指定多個 `similar.document_ids`，則逗點後面應該沒有空格）：

`curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&similar.document_ids=4107b6f1-5d3f-4bea-bbcf-fb05bbf960b1,6057k6d1-7d7k-6aeh-cfbb-kj98ssf786c2"`

已新增 `similar.fields` 的範例查詢

`curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&similar.document_ids=4107b6f1-5d3f-4bea-bbcf-fb05bbf960b1&similar.fields=title&return=title&count=100"`

如需相關資訊，請參閱[文件相似性 API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query-using-get){: new_window} 及[查詢參數](/docs/services/discovery/query-parameters.html#similar)。
