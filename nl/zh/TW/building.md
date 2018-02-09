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

# 配置服務

建置 {{site.data.keyword.discoveryshort}} 服務可強化您自己的資料，然後以可查詢的形式遞送它，來取得有用的見解。
{: shortdesc}

在將您自己的內容新增至 {{site.data.keyword.discoveryshort}} 服務之前，您應該配置該服務依您想要的方式來處理此內容。

首要步驟是配置該服務的基本參數（[為您的文件準備服務](/docs/services/discovery/building.html#preparing-the-service-for-your-documents)），這包括建立環境，以及在該環境內建立一個以上的集合。當建立集合時，會自動提供一組預設值（[預設配置](/docs/services/discovery/building.html#the-default-configuration)）。如果您對這些預設值感到滿意，則可以繼續上傳內容（[新增內容](/docs/services/discovery/adding-content.html)）。

不過，您很可能想要指定一個以上的自訂配置（請參閱[當您需要自訂配置時](/docs/services/discovery/building.html#when-you-need-a-custom-configuration)）。如果是這種情況，您必須執行下列動作：

-   識別某些範例內容（代表您檔案的文件）
-   上傳內容（[（上傳範例文件](/docs/services/discovery/building.html#uploading-sample-documents)）
-   調整轉換處理程序（[轉換範例文件](/docs/services/discovery/building.html#converting-sample-documents)）
-   定義強化（[新增強化](/docs/services/discovery/building.html#adding-enrichments)）
-   將結果正規化（[將資料正規化](/docs/services/discovery/building.html#normalizing-data)）

    建立自訂配置之後，您可以上傳文件（[新增內容](/docs/services/discovery/adding-content.html)）。

## 為您的文件準備服務
{: #preparing-the-service-for-your-documents}

在 {{site.data.keyword.discoveryshort}} 服務中，您上傳的內容會儲存在屬於您環境一部分的集合中。您必須先建立環境及集合，然後才能上傳內容。

-   **環境** - 環境定義您在 {{site.data.keyword.discoveryshort}} 服務中提供給內容的儲存空間數量。對於 {{site.data.keyword.discoveryshort}} 服務的每一個實例，最多只能建立一個環境。

    您有幾個方案（精簡、標準及進階）可選擇，如需詳細資料，請參閱 [{{site.data.keyword.discoveryshort}} 型錄 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window}。您的原始檔不計入檔案大小限制。

-   **集合** - 集合是您環境內的內容分組。您必須至少建立一個集合，才能上傳內容。

    集合包含您的專用資料，但 {{site.data.keyword.discoveryshort}} 還包括 {{site.data.keyword.discoverynewsshort}} 這個預先強化的公用資料集。您可以使用它來查詢見解；例如：新聞警示、事件偵測及新聞中的熱門話題；您可以將其整合到應用程式中。

    {{site.data.keyword.discoverynewsshort}} 是一個已利用認知見解預先強化的公用資料集，它也隨附於 {{site.data.keyword.discoveryshort}} 中。如需相關資訊，請參閱 [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html#watson-discovery-news)。您無法調整 {{site.data.keyword.discoverynewsshort}} 配置，或將文件新增至此集合中。請參閱[這裡 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://discovery-news-demo.mybluemix.net/){: new_window}，它示範使用 {{site.data.keyword.discoverynewsshort}} 可建置的內容。

若要使用 {{site.data.keyword.discoveryshort}} 工具來建立環境及專用資料集合，請執行下列動作：

1.  在**管理資料**畫面上，按一下 ![齒輪](images/icon_settings.png) 圖示，並選擇**建立環境**。環境會根據您先前選取的 {{site.data.keyword.Bluemix_notm}} 方案而建立。一律可從這個下拉清單取得環境的狀態。

1.  當環境備妥後，請按一下**建立資料集合**按鈕，然後就可以**命名您的新集合**。

    依預設，此配置檔將是**預設配置**。如果您有另一個可用的配置檔，則可以選擇它，也可以稍後再建立新的配置檔，並將它套用至此集合。您也可以選取將新增至此集合的文件語言：英文、德文、西班牙文、阿拉伯文、法文、義大利文、韓文或巴西葡萄牙文。每一個集合只能有一種語言。按一下**建立**之後，您的資料集合將顯示為磚。

您的環境及資料集合已備妥！如果您要使用預設配置檔，就可以立即開始[新增內容](/docs/services/discovery/adding-content.html)。但是，如果您要使用其他的強化和轉換設定來自訂您的 {{site.data.keyword.discoveryshort}} 配置，就不應該立即開始新增文件，而應該開始建立自訂配置檔。請參閱[配置服務](/docs/services/discovery/building.html#custom-configuration)。

**附註：**當文件上傳至資料集合時，會使用針對該集合所選擇的配置檔來轉換及強化文件。如果您稍後決定將集合切換至不同的配置檔，則可以執行該動作，但已上傳的文件仍透過原始配置檔轉換。在切換配置檔之後上傳的所有文件都會使用新的配置檔。如果您想要**整個**集合使用新的配置，則需要建立新的集合，選擇新的配置檔，然後重新上傳所有文件。{{site.data.keyword.discoveryshort}} 服務會儲存您所上傳文件的已轉換文字，但不會儲存 **PDF** 和 **Microsoft Word** 檔案中的內嵌影像，而且在結果中不會傳回它們。

### 預設配置
{: #the-default-configuration}

{{site.data.keyword.discoveryshort}} 服務包含標準配置檔，它將轉換、強化及正規化資料，而不需要您手動配置這些選項。

這個預設配置檔的名稱是**預設配置**。它包含強化，以及根據字型樣式和大小的標準文件轉換。

首先是預設強化。{{site.data.keyword.discoveryshort}} 將透過四個 {{site.data.keyword.watson}} 強化（「實體擷取」、「觀感分析」、「種類分類」及「概念標記」）所收集到的語意資訊來強化（新增認知 meta 資料至）文件的文字欄位（[這裡](/docs/services/discovery/building.html#adding-enrichments)可讓您進一步瞭解它們）。

**附註：**從 **2017 年 7 月 18 日**開始，{{site.data.keyword.discoveryfull}} 引進了一項新的強化技術，名稱為 {{site.data.keyword.nlushort}} (NLU)。如需詳細資料，請參閱[新增強化](/docs/services/discovery/building.html#adding-enrichments)。如果您在這個日期之前已將**預設配置**套用至集合，則該集合已使用 {{site.data.keyword.alchemylanguageshort}} 強化來強化。如果您在此日期之後將**預設配置**套用至集合，則會使用 {{site.data.keyword.nlushort}} 強化。

-   [Microsoft Word 轉換](/docs/services/discovery/building.html#microsoft-word-conversion)
-   [PDF 轉換](/docs/services/discovery/building.html#pdf-conversion)
-   [HTML 轉換](/docs/services/discovery/building.html#html-conversion)
-   [JSON 轉換](/docs/services/discovery/building.html#json-conversion)

如果您想建立自訂配置，請參閱[自訂配置](/docs/services/discovery/building.html#custom-configuration)。

### 當您需要自訂配置時
{: #when-you-need-a-custom-configuration}

從您的內容中取出正確的資訊，並將它傳回給您的使用者，這是 {{site.data.keyword.discoveryshort}} 服務的目標。識別資訊的內容，以及資訊儲存在內容中的方式，是由您用來汲取內容的配置所定義。{{site.data.keyword.discoveryshort}} 服務可以汲取的內容類型有彈性，也就是說，即使您的未結構化內容是以特定格式儲存，該內容的結構也不需要符合相同類型之其他內容的結構。

-   **我瞭解無法以預設配置所預期的方式來建構我的文件。*我如何知道預設值是否適合我？***
    -   要知道預設值是否適合您，最簡單的方法是透過[上傳範例文件](/docs/services/discovery/building.html#uploading-sample-documents)來測試它。如果範例 JSON 結果符合您的預期，則不需要其他配置。
-   **我瞭解預設的強化會新增至我的文件的文字欄位。我可以將其他強化新增至其他欄位嗎？**
    -   當然，您可以將其他強化新增至您想要的任意數目的欄位。如需詳細資料，請參閱[新增強化](/docs/services/discovery/building.html#adding-enrichments)。

## 自訂配置
{: #custom-configuration}

若要在 {{site.data.keyword.discoveryshort}} 工具中建立自訂配置，請開啟「專用」資料集合，並在**管理資料**畫面上，按一下**配置**名稱旁的**切換**。在**切換配置**對話框上，按一下**建立新的配置**。

為新的配置檔命名之後，該名稱會顯示在配置畫面的頂端。這個新的配置檔會自動包含[預設配置](/docs/services/discovery/building.html#the-default-configuration)檔案的設定及強化，讓您能夠開始進行。

自訂配置檔的三個步驟如下：**轉換**、**強化**及**正規化**。

1.  [轉換範例文件](/docs/services/discovery/building.html#converting-sample-documents)
1.  [新增強化](/docs/services/discovery/building.html#adding-enrichments)
1.  [將資料正規化](/docs/services/discovery/building.html#normalizing-data)

### 上傳範例文件
{: #uploading-sample-documents}

為了讓配置處理程序更有效率，您可以上傳多達 10 個 Microsoft Word、HTML、JSON 或 PDF 檔，來代表您的文件集。這些稱為**範例文件**。範例文件不會新增至集合中，它們只會用來識別文件的一般欄位，並根據您的需求自訂那些欄位。

在 {{site.data.keyword.discoveryshort}} 工具中建立新的配置檔時，您可以透過拖放或瀏覽來上傳範例文件。按一下**上傳範例文件**窗格中的檔名，以預覽每一個檔案。

#### 上傳範例文件時要記住下列項目：

-   所有文件在進行強化和檢索之前都會轉換成 JSON。
-   Microsoft Word 和 PDF 文件會先轉換成 HTML，再轉換成 JSON。
-   HTML 文件會直接轉換成 JSON。
-   範例文件的檔案大小上限為 5MB。1 個月後，會自動刪除範例文件，但如果您想要對配置進行其他變更，則可以再次上傳相同的文件。

#### 選擇理想範例文件的準則：

-   對於您想要汲取的每一種檔案類型（Microsoft Word、PDF、HTML 及 JSON），您應該具有（至少）一個範例文件。
-   如果您有任何唯一的文件類型（例如財務報告或新聞稿），請將其中一個包括在範例文件集中。
-   對於 HTML 文件，您應該選擇包括要排除之 HTML 標籤的文件，以及您想要併入或排除的標籤屬性。
-   JSON 文件應該包括您想要一併移除或合併的任何欄位（例如，zipCode 和 postalCode）。

### 轉換範例文件
{: #converting-sample-documents}

轉換範例文件的處理程序可讓您定義如何處理每一種輸入類型。您所上傳內容的檔案類型會指定您必須考量的轉換步驟數目。

開始之前，請[上傳範例文件](/docs/services/discovery/building.html#uploading-sample-documents)，並在右側窗格中開啟您要配置之檔案類型的範例文件。

若要瀏覽一遍「轉換」設定，請按一下全部的檔案類型。

![轉換範例文件](images/convert.png)

-   **如果您要轉換 Microsoft Word 檔案，則必須執行下列動作：**
    -   設定 Microsoft Word 轉換選項
    -   設定 HTML 轉換選項
    -   設定 JSON 轉換選項
    -   檢閱結果

-   **如果您要轉換 PDF 檔案，則必須執行下列動作：**
    -   設定 PDF 轉換選項
    -   設定 HTML 轉換選項
    -   設定 JSON 轉換選項
    -   檢閱結果

-   **如果您要轉換 HTML 檔案，則必須執行下列動作：**
    -   設定 HTML 轉換選項
    -   設定 JSON 轉換選項
    -   檢閱結果

-   **如果您要轉換 JSON 檔案**，則必須設定 JSON 轉換選項，並檢閱結果。

對於您建立的每一個配置檔，此處理程序的每一個步驟都只有一組轉換選項。這表示 PDF 檔案、Word 檔案及 HTML 的 HTML 轉換選項都一樣。如果您要汲取的每一種內容類型都需要不同的轉換選項（或者您有相同類型的檔案需要不同類型的轉換），則需要將檔案儲存在不同的集合中，並為每一組轉換設定建立個別的配置檔。

#### Microsoft Word 轉換
{: #microsoft-word-conversion}

Microsoft Word 字型大小及字型樣式用來將文件中的標題適當地轉換成 H1、H2 等等。H1 是文件標題，H2 及其以下是子標題。您可以使用文字框和圓鈕來變更預設值。您也可以新增其他標題層次和 Word 樣式。如果您的 Word 文件傾向於使用特定字型或樣式名稱作為標題，請務必新增該資訊。這將有助於改善轉換，以產生較佳的查詢結果。

**範例：**如果您的 Word 文件常常對標題 2s 使用 20 pt 斜體字型，請將**字型大小範圍**變更為 **20** 到 **23**，並將**字型樣式**變更為**斜體**。

進行任何變更之後，請按一下**套用並儲存**。

#### PDF 轉換
{: #pdf-conversion}

PDF 字型大小及字型名稱用來將文件中的標題適當地轉換成 H1、H2 等等。H1 是文件標題，H2 及其以下是子標題。您可以使用文字框和圓鈕來變更預設值。您也可以新增其他標題層次。如果您的 PDF 文件傾向於使用特定字型作為標題，請務必新增該資訊。這將有助於改善轉換，以產生較佳的查詢結果。

**範例：**如果您的 PDF 文件常常對標題 1s 使用 20 pt 粗體字型，請將**字型大小範圍**變更為 **20** 到 **80**，並將**字型樣式**變更為**粗體**。請相應地調整其他層次。

進行任何變更之後，請按一下**套用並儲存**。

#### HTML 轉換
{: #html-conversion}

您可以使用此步驟來移除不必要的標籤及其他文件資訊，而只保留您需要的查詢資訊。

預設 HTML 設定：

- 排除這些標籤及其內容：**`script`**、**`sup`**
- 排除這些標籤，但保留其內容：**`font`**、**`em`**、**`span`**
- 保留這些標籤屬性：無預設值
- 排除這些標籤屬性：**`EVENT_ACTIONS`**
- 保留符合此/這些 XPath 的內容：無預設值
- 排除符合此/這些 XPath 的內容：無預設值

進行任何變更之後，請按一下**套用並儲存**。

#### JSON 轉換
{: #json-conversion}

轉換的最後一個步驟是為了確保在對內容套用強化之前，轉換的（或上傳的）JSON 已依照您預期的方式形成。您可以建立 {{site.data.keyword.watson}} 用來將 HTML 轉換為 JSON 的規則。

-   您可以移動、合併、複製或移除欄位。例如：您可能想要合併 **`zipCode`** 和 **`posialCode`**，因為它們是代表相同欄位的兩個類似詞彙。
-   依預設，將刪除空欄位（未包含資訊的欄位）。您可以使用**移除空欄位**切換參數加以變更。

進行任何變更之後，請按一下**套用並儲存**。

## 新增強化
{: #adding-enrichments}

**附註：**從 **2017 年 7 月 18 日**開始，{{site.data.keyword.discoveryfull}} 引進了一項新的強化技術，名稱為 {{site.data.keyword.nlushort}} (NLU)。這些強化與您現有的強化相同，但需要稍微不同的配置和綱目。原始強化的名稱為 {{site.data.keyword.alchemylanguageshort}} 強化，將遭到淘汰。
{{site.data.keyword.alchemylanguageshort}} 強化支援將在 **2018 年 1 月 15 日**結束。新集合應該使用 {{site.data.keyword.nlushort}} 來強化，並儘快移轉含有 {{site.data.keyword.alchemylanguageshort}} 配置檔的任何現有集合。如需移轉利用 {{site.data.keyword.alchemylanguageshort}} 強化的集合及配置檔的相關資訊，請參閱[將強化移轉至 {{site.data.keyword.nlushort}}](/docs/services/discovery/migrate-nlu.html)。

{{site.data.keyword.discoveryshort}} [預設配置](/docs/services/discovery/building.html#the-default-configuration)將透過這四個 {{site.data.keyword.watson}} 功能（「實體擷取」、「觀感分析」、「種類分類」及「概念標記」）所收集的語意資訊來強化（新增認知 meta 資料至）所汲取文件的 `text` 欄位。（總共有九個可用的 {{site.data.keyword.watson}} 強化；其他是「關鍵字擷取」、「關係擷取」、「情緒分析」、「元素分類」及「語意角色擷取」。）

**重要事項：**針對所選取要強化的每一個 JSON 欄位，只會強化前 50,000 個字元。

您可以進一步擴增文件，方法是將更多的強化新增至 `text` 欄位，或強化其他欄位。若要使用 {{site.data.keyword.discoveryshort}} 工具來達成此目的，請[建立自訂配置](/docs/services/discovery/building.html#custom-configuration)，選擇您要強化的欄位，並從可用的 {{site.data.keyword.nlushort}} 強化清單中進行選取：

### 實體擷取
{: #entity-extraction}

傳回在輸入文字中呈現的項目，例如人員、位置及組織。實體擷取會將語意知識新增至內容，以協助瞭解所分析文字的主旨及環境定義。實體擷取技術是以精密的統計演算法和自然語言處理程序技術為基礎，憑藉其對多語言分析、環境定義相關的釐清及引文擷取的支援，在業界獨一無二。請在[這裡](/docs/services/discovery/entity-types.html)檢視實體類型及子類型的完整清單。您也可以使用 {{site.data.keyword.knowledgestudiofull}} 來建立及新增[自訂實體模型](/docs/services/discovery/building.html#custom-entity-model)。

使用「實體擷取」強化的文件的部分範例：

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "entities": [
         {
           "count": 1,
           "sentiment": {
             "score": 0
           },
           "text": "Acme Corporation",
           "relevance": 0.98389,
           "type": "Company"
           },
           {
           "count": 1,
           "sentiment": {
             "score": 0
           },
           "text": "Atlanta",
           "relevance": 0.532754,
           "type": "Location",
           "disambiguation": {
             "subtype": [
               "AdministrativeDivision",
               "GovernmentalJurisdiction",
               "OlympicHostCity",
               "PlaceWithNeighborhoods",
               "City"
           ],
               "name": "Atlanta",
               "dbpedia_resource": "http://dbpedia.org/resource/Atlanta"
           }
           },
           {
           "count": 1,
           "sentiment": {
             "score": 0
           },
           "text": "Georgia",
           "relevance": 0.469643,
           "type": "Location",
           "disambiguation": {
             "subtype": [
               "StateOrCounty"
           ]
    }
  }
```
{: codeblock}

在前述範例中，您可以透過存取 `enriched_text.entities.type` 來查詢實體類型

即使未選取**觀感**強化，也會計算實體類型的 `sentiment`。若要進一步瞭解觀感評分，請參閱[觀感分析](/docs/services/discovery/building.html#sentiment-analysis)。

`relevance` 評分範圍是從 `0.0` 到 `1.0`。評分越高，實體的相關性就越高。`disambiguation` 欄位包含實體的釐清資訊，其中包括實體 `subtype` 資訊，以及資源的鏈結（適用的話）。`count` 是文件中提及實體的次數。

#### 使用自訂實體模型
{: #custom-entity-model}

如果您要建立自訂強化模型，則可以在 {{site.data.keyword.knowledgestudiofull}} 中執行這個動作，然後透過在 {{site.data.keyword.discoveryshort}} 工具的`自訂模型 ID` 方框中新增 ID，將模型匯入至 {{site.data.keyword.discoveryshort}}。如需與 {{site.data.keyword.knowledgestudiofull}} 整合的相關資訊，請參閱[與 {{site.data.keyword.knowledgestudiofull}} 整合](/docs/services/discovery/integrate-wks.html#integrating-with-watson-knowledge-studio)。自訂 {{site.data.keyword.knowledgestudiofull}} 模型會置換預設的「實體擷取」強化。

**附註：**只能對強化指派一個 {{site.data.keyword.knowledgestudiofull}} 模型。

### 關係擷取
{: #relation-extraction}

辨識兩個實體何時相關，並識別關係的類型。您也可以使用 {{site.data.keyword.knowledgestudiofull}} 來建立及新增[自訂關係模型](/docs/services/discovery/building.html#custom-relation-model)。

請在[這裡](/docs/services/discovery/relation-types.html)檢視關係類型的完整清單。

使用「關係擷取」強化的文件的部分範例：

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
  "enriched_text": {
    "relations": [
      {
        "type": "locatedAt",
        "sentence": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
        "score": 0.989245,
        "arguments": [
         {
            "text": "Atlanta",
            "location": [
             94,
             101
            ],
            "entities": [
              {
                "type": "GeopoliticalEntity",
                "text": "Atlanta"
              }
            ]
         },
          {
            "text": "Georgia",
            "location": [
             103,
             110
            ],
            "entities": [
              {
                "type": "GeopoliticalEntity",
                "text": "Georgia"
              }
            ]
          }
        ]
      }
    ]
  }
}
```
{: codeblock}

在前述範例中，您可以透過存取 `enriched_text.relations.type` 來查詢關係類型。

相關實體會列在 `arguments` 中。您可以在[這裡](/docs/services/discovery/relation-types.html#specific-entity-types)找到「關係擷取」強化可以識別的實體類型。

`score` 範圍是從 `0.0` 到 `1.0`。評分越高，關係的相關性就越高。

#### 使用自訂關係模型
{: #custom-relation-model}

如果您要建立自訂強化模型，則可以在 {{site.data.keyword.knowledgestudiofull}} 中執行這個動作，然後透過在 {{site.data.keyword.discoveryshort}} 工具的`自訂模型 ID` 方框中新增 ID，將模型匯入至 {{site.data.keyword.discoveryshort}}。如需與 {{site.data.keyword.knowledgestudiofull}} 整合的相關資訊，請參閱[與 {{site.data.keyword.knowledgestudiofull}} 整合](/docs/services/discovery/integrate-wks.html#integrating-with-watson-knowledge-studio)。自訂 {{site.data.keyword.knowledgestudiofull}} 模型會置換預設的「關係擷取」強化。

**附註：**只能對強化指派一個 {{site.data.keyword.knowledgestudiofull}} 模型。

### 關鍵字擷取
{: #keyword-extraction}

在檢索資料、產生標籤雲或搜尋時通常會使用的內容中的重要主題。{{site.data.keyword.discoveryshort}} 服務會自動識別輸入內容中支援的語言，然後識別該內容中的關鍵字並進行分級。

使用「關鍵字擷取」強化的文件的部分範例：

```json
  {
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "keywords": [
        {
          "text": "Acme Corporation",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.985203
        },
        {
          "text": "new factory",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.821033
        },
        {
          "text": "stockholders",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.66497
        },
        {
          "text": "title",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.332438
        },
        {
          "text": "Atlanta",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.307723
        },
        {
          "text": "Georgia",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.306485
        }
      ]
    }
  }
```
{: codeblock}

在前述範例中，您可以透過存取 `enriched_text.keywords.text` 來查詢關鍵字

即使未選取**觀感**強化，也會計算關鍵字的 `sentiment`。若要進一步瞭解觀感評分，請參閱[觀感分析](/docs/services/discovery/building.html#sentiment-analysis)。

`relevance` 評分範圍是從 `0.0` 到 `1.0`。評分越高，關鍵字的相關性就越高。

### 種類分類

將輸入文字、HTML 或 Web 型內容分類為多達五個層次的階層式分類架構。更深入的層次可讓您將內容分類為更精確且有用的子區段。請在[這裡](/docs/services/discovery/categories.html)檢視種類的完整清單。

使用「種類分類」強化的文件的部分範例：

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "categories": [
        {
          "score": 0.361614,
          "label": "/business and industrial"
        },
        {
          "score": 0.329377,
          "label": "/business and industrial/company/merger and acquisition"
        },
        {
          "score": 0.154254,
          "label": "/business and industrial/business operations/business plans"
        }
      ]
```
{: codeblock}

在前述範例中，您可以透過存取 `enriched_text.categories.label` 來查詢種類標籤

`label` 是偵測到的種類。階層層次以正斜線區隔。該種類的 `score` 範圍是從 `0.0` 到 `1.0`。評分越高，該種類的信賴度就越高。

### 概念標記
{: #concept-tagging}

會根據存在於該文字中的其他概念和實體，識別與輸入文字相關聯的概念。概念標記瞭解概念之間的關係，而且可以識別文字中未直接參照的概念。例如，如果文章提及 CERN 和 Higgs boson，則概念 API 功能會將 Large Hadron Collider 識別為概念（即使頁面中並未明確提及該詞彙也一樣）。概念標記可以對輸入內容進行比基本關鍵字識別更高層次的分析。

使用「概念標記」強化的文件的部分範例：

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "concepts": [
        {
          "text": "Acme Corporation",
          "relevance": 0.91136,
          "dbpedia_resource": "http://dbpedia.org/resource/Acme_Corporation"
        },
        {
          "text": "Factory",
          "relevance": 0.886784,
          "dbpedia_resource": "http://dbpedia.org/resource/Factory"
        }
      ]
```
{: codeblock}

在前述範例中，您可以透過存取 `enriched_text.concepts.text` 來查詢概念文字

`relevance` 評分範圍是從 `0.0` 到 `1.0`。評分越高，概念的相關性就越高。有提供資源的鏈結（適用的話）。

### 語意角色擷取

識別輸入內容中句子內的主旨、動作及物件關係。關係資訊可用來自動識別購買信號、重要事件及其他重要動作。

使用「語意角色擷取」強化的文件的部分範例：

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
      "enriched_text": {
      "semantic_roles": [
        {
          "subject": {
            "text": "The stockholders",
            "keywords": [
              {
                "text": "stockholders"
              }
            ]
          },
          "sentence": " The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
          "object": {
            "text": "pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia",
            "keywords": [
              {
                "text": "Acme Corporation"
              },
              {
                "text": "new factory"
              },
              {
                "text": "Atlanta"
              },
              {
                "text": "Georgia"
              }
            ],
            "entities": [
              {
                "type": "Company",
                "text": "Acme Corporation"
              },
              {
                "type": "Location",
                "text": "Atlanta",
                "disambiguation": {
                  "subtype": [
                    "AdministrativeDivision",
                    "GovernmentalJurisdiction",
                    "OlympicHostCity",
                    "PlaceWithNeighborhoods",
                    "CityTown",
                    "City"
                  ],
                  "name": "Atlanta",
                  "dbpedia_resource": "http://dbpedia.org/resource/Atlanta"
                }
              },
              {
                "type": "Location",
                "text": "Georgia",
                "disambiguation": {
                  "subtype": [
                    "StateOrCounty"
                  ]
                }
              }
            ]
          },
          "action": {
            "verb": {
              "text": "be",
              "tense": "past"
            },
            "text": "were",
            "normalized": "be"
          }
        }
      ]
```
{: codeblock}

在前述範例中，您可以透過存取 `enriched_text.relations.subject.text` 來查詢關係主旨文字

即使未選取**觀感**強化，也會計算關係的 `sentiment`。若要進一步瞭解觀感評分，請參閱[觀感分析](/docs/services/discovery/building.html#sentiment-analysis)。除非您也選取**實體**和**關鍵字**強化，否則它不會擷取 `entities` 或 `keywords`（如下列範例所示）。如需那些強化的相關資訊，請參閱[實體擷取](/docs/services/discovery/building.html#entity-extraction)及[關鍵字擷取](/docs/services/discovery/building.html#keyword-extraction)。

會針對包含關係的每個句子，擷取 `subject`、`action` 及 `object`。

### 觀感分析
{: #sentiment-analysis}

識別要分析之內容中的態度、意見或感受。{{site.data.keyword.discoveryshort}} 服務可以計算文件內的整體觀感、使用者所指定目標的觀感、實體層次觀感、引文層次觀感、方向觀感及關鍵字層次觀感。這些功能的組合可支援範圍從社交媒體監視到趨勢分析的各種使用案例。

使用「觀感分析」強化的文件的部分範例：

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "sentiment": {
        "document": {
        "score": 0.459813,
        "label": "positive"
  }
}
```
{: codeblock}

在前述範例中，您可以透過存取 `enriched_text.sentiment.document.label` 來查詢觀感標籤

`label` 是文件的整體觀感（`positive`、`negative` 或 `neutral`）。觀感 `label` 是根據 `score`；`0.0` 的評分指出文件是 `neutral`，正數指出文件為 `positive`，負數指出文件為 `negative`。

### 情緒分析
{: #emotion-analysis}

偵測英文字中隱含的生氣、厭惡、恐懼、歡樂及悲傷。「情緒分析」可以偵測與目標詞組、實體或關鍵字相關聯的情緒，也可以分析內容的整體情緒語氣。

使用「情緒分析」強化的文件的部分範例：

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "emotion": {
        "document": {
          "emotion": {
          "disgust": 0.102578,
          "joy": 0.626655,
          "anger": 0.02303,
          "fear": 0.018884,
          "sadness": 0.096802
    }
  }
}
```
{: codeblock}

在前述範例中，您可以透過存取 `enriched_text.emotion.document.emotion.joy` 來查詢 `joy` 情緒

「情緒分析」會分析您的文字，並以 `0.0` 到 `1.0` 的刻度來計算每一種情緒（生氣、厭惡、恐懼、歡樂、悲傷）的評分。如果有任何情緒的評分為 `0.5` 或更高，則會偵測到該情緒（高於 `0.5` 的評分越高，相關性就越高）。在顯示的 Snippet 中，`joy` 的評分高於 0.5，因此 {{site.data.keyword.watson}} 偵測到 joy。

**附註：**僅支援英文版的「情緒分析」。

### 元素分類
{: #elements}

剖析控管文件中的元素（句子、清單、表格），以對重要類型和種類進行分類。如需相關資訊，請參閱[元素分類](/docs/services/discovery/element-classification.html)。

#### 強化定價
{: #enrichment-pricing}

[{{site.data.keyword.Bluemix_notm}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window} 有可用的強化定價資訊。

#### 強化語言支援
{: #enrichment-language-support}

如需強化語言支援的相關資訊，請參閱 [{{site.data.keyword.discoveryshort}} 語言支援](/docs/services/discovery/language-support.html)。

### 瞭解實體、概念及關鍵字之間的差異
{: #udbeck}

乍看之下，**實體擷取**、**概念標記**及**關鍵字擷取**似乎為類似的強化。我們將使用強化範例中的文字來顯示它們之間的差異。

```json
"text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia."
```
{: codeblock}

由於**實體擷取**強化會擷取輸入文字中的人員、位置及組織，因此**實體擷取**會傳回下列實體類型：

```json
"type": "City"
"text": "Atlanta"

"type": "Company"
"text": "Acme"

"type": "StateOrCounty"
"text": "Georgia"
```
{: codeblock}

由於**概念標記**強化瞭解概念之間的關係，因此它可識別文字中未直接參照的概念。例如，如果文章提及 CERN 和 Higgs boson，它會將 Large Hadron Collider 識別為概念（即使未明確提及該詞彙也一樣）。由於我們的範例文件文字只有一個句子，因此沒有相關概念，所以**概念標記**會傳回下列概念：

```json
"text": "Acme Corporation"
"text": "factory"
```
{: codeblock}

由於**關鍵字擷取**強化會識別在檢索資料、產生標籤雲或搜尋時通常使用的內容，因此**關鍵字擷取**會傳回下列關鍵字：

```json
"text": "Acme Corporation"
"text": "new factory"
"text": "stockholders"
"text": "Atlanta"
"text": "Georgia"
```
{: codeblock}

這些強化搭配使用，可協助您建置更好的查詢。

## 將資料正規化
{: #normalizing-data}

自訂配置檔的最後一個步驟是執行最終清理，也稱為正規化。

在 {{site.data.keyword.discoveryshort}} 工具的**正規化**區段中：

-   您可以移動、合併、複製或移除欄位。
-   依預設，將刪除空欄位（未包含資訊的欄位）。您可以使用**移除空欄位**切換參數加以變更。

進行任何變更之後，請按一下**套用並儲存**，然後按一下**完成**。您會回到**管理資料**畫面，您可以在其中將此配置套用至您選擇的集合。

## 將實體正規化
{: #normalizing-entities}

### 使用 CSS 選取器來擷取欄位
{: #using-css}

您可以透過 Discovery API，使用 CSS 選取器來執行其他正規化。

如果您要汲取形式完整的 HTML，則可以將它正規化，使用 CSS 選取器來擷取其中的 JSON 欄位，然後將強化套用至所擷取的欄位。請編輯配置檔，以啟用此特性。具體而言，請將 `extracted_fields` 元素新增至 `conversions/html` 階層，然後指定欄位名稱、CSS 選取器及欄位類型，如下所示：

```json
{
  "name": "Extract JSON config",
  "description": "New configuration enabling extraction of JSON fields from HTML",
  "conversions": {
    ...
    "html": {
      ...
      "extracted_fields": {
        "{field_name_1}": {
          "css_selector": "{CSS_selector_expression_1}",
          "type": "{field_type}"
        },
        ...
        "{field_name_N}": {
          "css_selector": "{CSS_selector_expression_N}",
          "type": "{field_type}"
        }
      }
    ...
    }
  }
}
```
{: codeblock}

請如下所示指定新欄位的值：

-   `field_name` - 將新增至 JSON 輸出的欄位名稱。
-   `CSS_selector_expression` - 要對輸入 HTML 執行以擷取欄位的 CSS 選取器。表示式可以有一個以上的相符項。

    有效的 CSS 選取器是 [JSoup 剖析器 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://jsoup.org/apidocs/org/jsoup/select/Selector.html){: new_window} 及其[選取器語法 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://jsoup.org/cookbook/extracting-data/selector-syntax){: new_window} 所指定的那些選取器。[一般選取器](/docs/services/discovery/building.html#common-selectors)有提供簡短清單。
-   `field_type` - `array` 或 `string`。如果未指定欄位類型，則其預設為 `array`。請注意，可以強化 `string` 類型，但無法強化儲存在 `array` 中的資訊，除非先將陣列的項目擷取到文字欄位中。

**警告：**如果 CSS 選取器同時符合母節點及其一個以上的子節點，則節點的文字內容將重複出現在 JSON 輸出中。

**附註：**欄位名稱必須符合[欄位名稱需求](/docs/services/discovery/custom-config.html#field_reqs)中定義的限制。

下列 JSON 段落顯示您將 CSS 選取器資訊新增至其中的「預設配置」的相關區段。

```json
{
  "name": "Default Configuration",
  "description": "The configuration used by default when creating a new collection without specifying a configuration_id.",
  "conversions": {
    ...
    "html": {
      "exclude_tags_completely": [
        "script",
        "sup"
      ],
      "exclude_tags_keep_content": [
        "font",
        "em",
        "span"
      ],
      "exclude_content": {
        "xpaths": []
      },
      "keep_content": {
        "xpaths": []
      },
      "exclude_tag_attributes": [
        "EVENT_ACTIONS"
      ]
    }
    ...
  }
}
```
{: codeblock}

下列段落顯示具有新名稱和說明的配置，以及您可以指定 CSS 選取器的位置。

```json
{
  "name": "Extract JSON config",
  "description": "New configuration enabling extraction of JSON fields from HTML",
  "conversions": {
    ...
    "html": {
      "exclude_tags_completely": [
        "script",
        "sup"
      ],
      "exclude_tags_keep_content": [
        "font",
        "em",
        "span"
      ],
      "exclude_content": {
        "xpaths": []
      },
      "keep_content": {
        "xpaths": []
      },
      "exclude_tag_attributes": [
        "EVENT_ACTIONS"
      ],
      "extracted_fields": {
        "{field_name_1}": {
          "css_selector": "{CSS_selector_expression_1}",
          "type": "{field_type}"
        },
        ...
        "{field_name_N}": {
          "css_selector": "{CSS_selector_expression_N}",
          "type": "{field_type}"
        }
      }
    }
  }
  ...
}
```
{: codeblock}

最後，下列段落顯示配置的新名稱和說明，以及一些 CSS 選取器。這些選取器符合 HTML 範例中的項目，而此頁面將對這個範例做進一步的說明。

```json
{
  "name": "Extract JSON config",
  "description": "New configuration enabling extraction of JSON fields from HTML",
  "conversions": {
    ...
    "html": {
      "exclude_tags_completely": [
        "script",
        "sup"
      ],
      "exclude_tags_keep_content": [
        "font",
        "em",
        "span"
      ],
      "exclude_content": {
        "xpaths": []
      },
      "keep_content": {
        "xpaths": []
      },
      "exclude_tag_attributes": [
        "EVENT_ACTIONS"
      ],
      "extracted_fields": {
        "chapters": {
          "css_selector": ".chapter",
          "type": "array"
        },
        "authors": {
          "css_selector": ".author"
        },
        "authors_str": {
          "css_selector": ".author",
          "type": "string"
        },
        "comments": {
          "css_selector": "[^comments-content]"
        }
      }
    }
  }
  ...
}
```
{: codeblock}

如果您將下列 HTML 文件載入到使用已更新配置的集合中，則 CSS 選取器將符合 HTML 中的適當屬性和值。

```html
<html>
  <body>
    <div id="authors">
      <div class="author"><span class="first_name">Jane</span> <span class="last_name">Rain</span></div>
      <div class="author">Joe Snow</div>
  </div>
  <div class="chapter"><h1>The Rain in Spain</h1><p>falls mainly on the plain.</p></div>
  <div class="chapter"><h1>How I Learned to Stop Worrying</h1><p>and love my snowblower.</p></div>
  <span id="comments-section">
    <h4>Comments:</h4>
    <span id="comments-content-1">Rain gives me pain.</span>
    <span id="comments-content-2">All snow must go!</span>
  </span>
</body></html>
```
{: codeblock}

在汲取及加強前述 HTML 之後，{{site.data.keyword.discoveryshort}} 服務將傳回下列 JSON：

```json
{
  "extracted_metadata": { ... },
  "html": "...",
  "text": "...",
  "extracted_fields": {
    "authors": [ "Jane Rain", "Joe Snow" ],
    "authors_str": "Jane Rain\n\nJoe Snow",
    "chapters": [ "The Rain in Spain\n\nfalls mainly on the plain.", "How I Learned to Stop Worrying\n\nand love my snowblower." ],
    "comments": [ "Rain gives me pain.", "All snow must go!" ]
  }
}
```
{: codeblock}

決定要擷取哪些 HTML 元素之後，您可以進一步修改配置檔，以指定您要套用至其中的強化。

#### 一般選取器

以下是一些一般 CSS 選取器：

  - `tag` - 符合 `tag` 名稱
  - `.class` - 符合 `class` 的值
  - `#id` - 符合 `id` 的值
  - `[attribute]` - 符合含有指定的 `attribute` 的任何標籤，不論其值為何
  - `[attribute=value]` 或 `[attribute="value"]` - 符合指定的 `attribute` 和 `value`

## 使用文件分段來分割文件
{: #doc-segmentation}

您可以根據 HTML 標題標籤將 Word、PDF 及 HTML 文件分割為區段。分割之後，每一個區段都是一份將轉換成 JSON 的個別文件，會個別進行檢索及強化。由於查詢將以個別文件傳回這些區段，因此文件分段可以用來：

  - 對文件的個別區段執行聚集。例如，您的聚集會在每次區段提及特定實體時計算一次，而不是只對整份文件計算一次。
  - 對區段（而非文件）執行相關性訓練，這會使結果有更好的重新分級。

當文件轉換為 HTML（Word 和 PDF 文件在轉換為 JSON 之前會先轉換為 HTML）時，會建立區段。您可以根據下列 HTML 標籤來分割文件：`h1` `h2` `h3` `h4` `h5` 及 `h6`。

注意事項：

  - 每份文件的區段數目限制為 `50`。在 `49` 個區段之後的所有其餘文件內容將儲存在區段 `50` 內。

  - 每一個區段都計入您方案的文件限制內。

  - 使用文件分段時，您不能將資料正規化（請參閱[將資料正規化](/docs/services/discovery/building.html#normalizing-data)）或使用 CSS 選取器擷取欄位（請參閱[使用 CSS 選取器來擷取欄位](/docs/services/discovery/building.html#using-css)）。

  - 如果文件已更新，且需要重新汲取，則刪除的區段會在重新汲取之後仍保留在後面，而且必須使用 API 手動刪除（請參閱[API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/watson/developercloud/discovery/api/v1/?curl#delete-doc){: new_window}）。此外，如果您的文件更新所新增的內容將建立新區段，或刪除的內容將移除區段，則每一個區段將獲指派新的 `document_id`。如果這些區段已使用相關性訓練進行分級，則需要重新執行訓練。在此情況下，請不要將內容新增至現有文件中，而是考量建立新文件來包含新內容，並個別汲取它。請不要從現有文件中刪除區段並重新汲取，而是使用 API 來刪除那些區段。

  - 每次偵測到指定的 HTML 標籤時，都會對文件進行分段。因此，分段可能會導致形態異常的 HTML，因為文件可能會在結束（右）標籤之前及開啟（左）標籤之後分割。

  - 不會擷取 HTML、PDF 及 Word meta 資料，因此不會將這些資料併入索引中。此外，使用文件上傳所傳入的自訂 meta 資料將不會併入索引中。

### 執行分段
{: #performing-segmentation}

在 `conversions` 區段中，透過 API 來設定分段。

```json
{
  "configuration_id": "a23c467d-1212-4b3a-5555-93e788a3622a",
  "name": "Example configuration",
  "conversions": {
    "segment": {
      "enabled": true,
      "selector_tags": ["h1", "h2", "h3", "h4", "h5", "h6"]
    }
  }
}
```
{: codeblock}

`enabled` = `true` 會開啟文件分段功能。

`selector_tags` 是一個陣列，其指定可以用來將文件分段的標題標籤。

#### 範例

配置：

```json
"conversions": {
  "segment": {
    "enabled": true,
    "selector_tags": ["h1", "h2"]
```
{: codeblock}

原始 HTML 文件：

```
<html>
 <head>
 </head>
 <body>
  first line
   <div name="section 1">
    <h1>heading 1</h1>
     <div name="section 2">This is the text that falls under <b>heading 1</b> and should be therefore split into its own segment.
      <h2>heading 2</h2>
      line under heading 2
     </div>
       <h3>heading 3</h3>
       line under heading 3
   </div>
  last line
 </body>
</html>
```
{: codeblock}

第一個文件區段看起來如下：

```json
{
  "id": "94c686c3-a790-4d8d-ba42-2bddf01b311c",
  "segment_metadata": {
    "parent_id": "94c686c3-a790-4d8d-ba42-2bddf01b311c",
    "segment": 1,
    "total_segments": 3
  },
  "extracted_metadata": {
    "title": "Heading 1",
    "sha1": "45ede479df67d78f2205ea7e714843375d3029c0",
    "filename": "doc-with-different-heading-levels.html",
    "file_type": "html"
  },
  "text": "This is the text that falls under heading 1 and should be therefore split into its own segment.",
  "html": "<div name=\"section 2\">This is the text that falls under <b>heading 1</b> and should be therefore split into its own segment."
}
```
{: codeblock}

所有區段都包含：

  - `id` - 此區段的 `id`。
  - `segment_metadata` 區段，它包含下列各項：
    - `parent_id` - `parent_id` 是原始文件的 ID。第一個區段的 `id` 與 `parent_id` 相同。
    - `segment` - 此區段的號碼。
    - `total_segments` - 文件分割成的區段總數。
  - `extracted_metadata` 區段，它包含下列各項：
    - `title` - `title` 欄位擷取自該區段的標題標籤內容（例如，`Chapter 1`）。如果第一個區段沒有包含標題標籤，則 `title` 會是 `no-title`。
    - `sha1` - 對應於原始文件。
    - `filename` - 對應於原始文件。
    - `file_type`- 對應於原始文件。
  - `text` 欄位
  - `html` 欄位
