---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-30"

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
{:download: .download}

# 開始使用工具

在這個簡短的指導教學中，我們將介紹 {{site.data.keyword.discoveryshort}} 工具，並逐步完成建立及搜尋專用資料集合的處理程序。
{: shortdesc}

## 開始之前
{: #before-you-begin}

您需要服務實例來開始。

<!-- Remove the text marked `download` after there's no g-s tab in the catalog dashboard -->

您已建立服務實例。請按一下**管理**，然後按一下**啟動工具**。請前往[步驟 2](/docs/services/discovery/getting-started-tooling.html#create-a-collection)。
{: download tip}

如果您已使用 {{site.data.keyword.discoveryshort}} 服務建立專案，則所有這些必備項目已準備妥當。請前往[步驟 1](/docs/services/discovery/getting-started-tooling.html#launch-the-tooling)。

1.  移至 {{site.data.keyword.watson}} Developer Console [服務 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.{DomainName}/developer/watson/services){: new_window} 頁面。
1.  選取 {{site.data.keyword.discoveryshort}}，按一下**新增服務**，然後註冊免費 {{site.data.keyword.Bluemix_notm}} 帳戶或登入。
1.  鍵入 `discovery-tutorial` 作為專案名稱，然後按一下**建立專案**。

<!-- Remove this text after dedicated instances have the Developer Console: begin -->

如果您使用 {{site.data.keyword.Bluemix_dedicated_notm}}，請從「型錄」的 [{{site.data.keyword.discoveryshort}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.{DomainName}/catalog/services/discovery/){: new_window} 頁面建立服務實例。

<!-- Remove this text after dedicated instances have the Developer Console: end -->

## 步驟 1：啟動工具
{: #launch-the-tooling}

建立包含 {{site.data.keyword.discoveryshort}} 服務的專案之後，您會看到專案詳細資料頁面。請從這裡啟動 {{site.data.keyword.discoveryshort}} 工具。

在**服務**下，對 {{site.data.keyword.discoveryshort}} 按一下**啟動工具**。

<!-- To do: Add screenshot for developer console -->

如果系統提示您登入工具，請提供您的 {{site.data.keyword.Bluemix_notm}} 認證。

如果您不在 {{site.data.keyword.discoveryshort}} 服務的專案詳細資料頁面上，請移至 {{site.data.keyword.watson}} Developer Console [專案 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.{DomainName}/developer/watson/projects) 頁面，然後選取該專案。
{: tip}

<!-- Remove this text after dedicated instances have the Developer Console: begin -->

{{site.data.keyword.Bluemix_dedicated_notm}}：從「儀表板」選取服務實例以啟動工具。

<!-- Remove this text after dedicated instances have the Developer Console: end -->

## 步驟 2：建立集合
{: #create-a-collection}

您在 {{site.data.keyword.discoveryshort}} 工具中的首要步驟是建立資料集合。

集合是您的文件集。*為什麼我需要多個集合？*有幾個原因：

- 您可能想要多個集合，以區隔不同對象的結果。
- 資料可能差異很大，以致於同時查詢所有資料並沒有意義。

您也可以使用公用、預先強化的 {{site.data.keyword.discoverynewsshort}} 資料集合。它已備妥可供查詢，您可以立即開始對其建立查詢。您無法調整其配置，或將文件新增至 {{site.data.keyword.discoverynewsshort}} 中。

1.  按一下 ![齒輪](images/icon_settings.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->，並選擇**建立環境**。
1.  當您的環境已經備妥時，會出現**命名您的新集合**對話框。請命名您的集合，並從**選取要套用的配置**中選擇**預設配置**（您可以稍後再變更配置）。

## 步驟 3：建立自訂配置
{: create-custom-configuration}

建立集合之後，您可以立即開始使用上傳區域來上傳內容，但我們想要建立並測試自訂配置。

1.  按一下集合名稱旁邊的**切換**，然後選擇**建立新的配置**。請為您的配置命名，然後按一下**建立**。
1.  建立配置之後，您可以自訂它：
    1.  下載 <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示" title="外部鏈結圖示" class="style-scope doc-content"></a> 範例文件。
    1.  使用**上傳範例文件**畫面來上傳範例文件。上傳之後，您可以按一下文件名稱鏈結來檢視轉換。
1.  現在可以調整配置。以這項作業而言，您可以變更已套用至每一個文件的強化：
    1.  按一下配置的**強化**區段。查看畫面右邊已產生的 JSON。向下捲動至 *enriched_text* 區段，並注意到它包含許多*概念*。
    1.  接下來，按一下名稱為*概念* 的文字強化旁邊的 **X** 來移除它，然後按一下**套用並儲存**。
    1.  最後，再次查看 JSON。請注意，此輸出已變更，不再包含*概念*。

## 步驟 4：上傳文件
{: #upload-your-documents}

當您對範例文件的自訂轉換感到滿意時，就可以將真實內容汲取到集合中。

1. 下載這三個範例文件：<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示" title="外部鏈結圖示" class="style-scope doc-content"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示" title="外部鏈結圖示" class="style-scope doc-content"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示" title="外部鏈結圖示" class="style-scope doc-content"></a>。
1.  按一下 ![「檔案」圖示](images/icon_yourData.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->，然後選取集合。
1.  請確定您建立的自訂配置已列在**配置**下。如果未列出，請按一下配置名稱旁邊的**切換**，然後選取它。
1.  按一下**上傳文件**按鈕，然後開始上傳這四個範例文件：test-doc1.html、test-doc2.html、test-doc3.html、test-doc4.html。
1.  等待文件上傳。文件的狀態會顯示在**概觀**區段中。

## 步驟 5：建置查詢
{: #build-a-query}

1.  按一下 ![「查詢」圖示](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->，以開啟查詢頁面。選取集合，然後按一下**開始使用**。
1.  在**建置查詢**畫面上，按一下**搜尋文件**，然後按一下**使用 {{site.data.keyword.discoveryshort}} 查詢語言**：
    - 若要搜尋含有名稱為 "IBM" 之實體的結果，請執行下列動作：
        1.  按一下**欄位**，並選取 `enriched_text.entities.text`。針對**運算子**選取 `contains`，並針對**值**選取 `IBM`。`enriched_text.entities.text:IBM` 查詢會顯示在**視覺化查詢建置器**中。
        1.  按一下**執行查詢**。查詢會傳回 4 個結果。
    - 若要搜尋含有名稱為 "Watson" 之實體的結果，請執行下列動作：
        1.  按一下**欄位**，並選取 `enriched_text.entities.text`。針對**運算子**選取 `contains`，並針對**值**選取 `watson`。`enriched_text.entities.text:watson` 查詢會顯示在**視覺化查詢建置器**中。
        1.  按一下**執行查詢**。查詢會傳回 2 個結果。
    - 若要搜尋同時含有名稱為 "Watson" 和 "Slack" 之實體的結果，請執行下列動作：
        1.  按一下**欄位**，並選取 `enriched_text.entities.text`。針對**運算子**選取 `contains`，並針對**值**選取 `watson`。按一下**新增規則**，然後重複您的選取動作，但要選擇**值** `Slack`。`enriched_text.entities.text:watson,enriched_text.entities.text:Slack` 查詢會顯示在**視覺化查詢建置器**中。
        1.  按一下**執行查詢**。查詢會傳回 1 個結果。

    按一下**以查詢語言編輯**，以使用「{{site.data.keyword.discoveryshort}} 查詢語言」建置查詢。若要進一步瞭解「{{site.data.keyword.discoveryshort}} 查詢語言」，請參閱[查詢參照](/docs/services/discovery/query-reference.html)及[查詢概念](/docs/services/discovery/using.html)。
1.  您的查詢結果會顯示在**結果**區段中：
    - **摘要**標籤提供查詢結果的概觀。
    - **JSON** 標籤顯示完整 JSON 結果。

    對於列出的查詢，**摘要**會先顯示文件段落（依相關性順序），接著是所找到的文件名稱，然後是強化的結果。**段落**是從查詢所傳回的完整文件中擷取的簡短相關摘錄。

    **JSON** 標籤和**摘要**這兩個標籤下提供的**查詢 URL**鏈結，已備妥可供您的應用程式使用。

    您也可以按一下**使用自然語言**，並撰寫自然語言查詢，例如 "IBM Watson partnerships"。若要進一步瞭解自然語言查詢，請參閱[自然語言查詢](/docs/services/discovery/query-parameters.html#nlq)。

    Watson 可透過訓練來改善自然語言查詢的結果，請參閱[利用工具來改善結果相關性](/docs/services/discovery/train-tooling.html)。

    其他資源：
    - 若要進一步瞭解文件的資料綱目，請按一下**檢視資料綱目**圖示，或按一下 **JSON** 標籤。如需詳細資料，請參閱 [Discovery 資料綱目](/docs/services/discovery/using.html#discovery-schema)。
    - 如果以「{{site.data.keyword.discoveryshort}} 查詢語言」進行編輯，請按一下任何**在這裡輸入查詢**欄位旁邊的 **?** 圖示，以取得更多範例。

## 後續步驟
{: #next-steps}

現在，您有一個能發揮作用且已移入資料的 {{site.data.keyword.discoveryshort}} 服務實例。您現在可以開始自訂集合，方法是新增更多文件和強化，以及自訂轉換設定。
