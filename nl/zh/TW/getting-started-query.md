---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-16"

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

# 開始使用查詢

在本指導教學中，我們將學習如何在 {{site.data.keyword.discoveryshort}} 中寫入一些不同類型的查詢。
{: shortdesc}

如需撰寫查詢的相關資訊，請參閱：
- [查詢概念](/docs/services/discovery/using.html)
- [查詢參照](/docs/services/discovery/query-reference.html)（包括「{{site.data.keyword.discoveryshort}} 查詢語言」可用的參數、運算子和聚集的清單）

這些範例查詢是使用 {{site.data.keyword.discoveryshort}} 工具所建置。如果您想要改用 API，請將查詢參數新增至您的 API 呼叫。如需相關資訊和範例，請參閱 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection){: new_window} 的「查詢」小節。

您也可以使用 {{site.data.keyword.discoveryshort}} 工具來撰寫自然語言查詢（例如 "IBM Watson partnerships"）。本指導教學主要著重在如何使用「{{site.data.keyword.discoveryshort}} 查詢語言」撰寫查詢，因為您的需求可能需要結構化查詢，而過濾器及聚集必須以「{{site.data.keyword.discoveryshort}} 查詢語言」撰寫。
{: tip}

## 開始之前

**請完成[開始使用](/docs/services/discovery/getting-started-tool.html)中的步驟。**如果您尚未完成**開始使用**，請移至**管理資料**畫面，建立一個名稱為 {{site.data.keyword.IBM_notm}} Press Releases 的新集合，並將這四個文件新增至其中（使用**預設配置**）：<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示" title="外部鏈結圖示" class="style-scope doc-content"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示" title="外部鏈結圖示" class="style-scope doc-content"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示" title="外部鏈結圖示" class="style-scope doc-content"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示" title="外部鏈結圖示" class="style-scope doc-content"></a>

## 步驟 1：快速導覽 Discoery 資料綱目

讓我們從認識 {{site.data.keyword.discoveryshort}} JSON 開始。若要瞭解如何使用「{{site.data.keyword.discoveryshort}} 查詢語言」來建置查詢，熟悉 {{site.data.keyword.discoveryshort}} 在強化您集合中的文件之後所產生的 JSON 會有所幫助。

1.  [啟動 {{site.data.keyword.discoveryshort}} 工具](/docs/services/discovery/getting-started-tool.html#launch-the-tooling)。在**管理資料**畫面上，選擇 {{site.data.keyword.IBM_notm}} Press Releases 集合。

1.  檢閱 Watson 在您的強化文件中探索到的見解。

    -  **一般觀感**會依百分比劃分，來顯示「觀感分析」強化所探索到且標記為正面、中性和負面的文件。
    -  **熱門實體**會顯示「實體擷取」強化在文件中探索到的人員、位置和組織。
    -  **內容階層**會顯示「種類分類」強化在文件中探索到的階層式分類架構。
    -  **相關概念**會顯示「概念標記」強化在文件中探索到的概念。

         在任何卡片上按一下**以綱目檢視**，以查看包含那些結果的強化。
         {: tip}

1.  為了熟悉文件的資料綱目，我們來看看**檢視資料綱目**畫面。在轉換後的文件中，它以兩種方式來顯示欄位和值：依文件（**文件視圖**）或依欄位（**集合視圖**）。**集合視圖**會顯示集合中的所有欄位。

    按一下**檢視資料綱目**按鈕。在**集合視圖**的 `enriched_text` 下，您可以檢查您使用**預設配置**檔案所套用的強化。請按一下 `categories`、`concepts`、`entities` 及 `sentiment`，以查看如何利用 Watson 見解來強化您的集合。

如果您的查詢未傳回任何相符的結果，但您認為它應該傳回，請嘗試以您的查詢所使用的欄位/值來交換您可以在資料綱目中驗證的欄位/值。
{: tip}    

## 步驟 2：建置基本查詢

首先，我們撰寫一個查詢來找出您集合中的 `Cloud computing` 概念：

1.  按一下建置查詢圖示 ![「查詢」圖示](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->，以開啟查詢頁面。選取包含 {{site.data.keyword.IBM_notm}} Press Releases 的集合，然後按一下**開始使用**。
1.  在**建置查詢**畫面上，按一下**搜尋文件**，然後按一下**使用 {{site.data.keyword.discoveryshort}} 查詢語言**，再：
    - 按一下**欄位**下拉清單，並選擇 `enriched_text.concepts.text`，針對**運算子**選擇 `contains`，然後輸入**值** `Cloud computing`。`enriched_text.concepts.text:Cloud computing` 查詢將顯示在**視覺化查詢建置器**下。

    - 或者，您可以按一下**以查詢語言編輯**，然後**使用 {{site.data.keyword.discoveryshort}} 查詢語言**。於**在這裡輸入查詢**欄位中輸入 `enriched_text.concepts.text:Cloud computing`。

1.  按一下**執行查詢**。應該會有一個相符項 (`"matching_results": 1`)。複製**摘要**或 **JSON** 標籤上的**查詢 URL**，以用於應用程式中。

**額外的好處：**在**其他選項**下，您可以選擇使用**包含相關段落**圓鈕來啟動段落擷取。段落是從查詢所傳回的完整文件中擷取的簡短相關摘錄。這些已設定目標的段落是從您集合中文件的 `text` 欄位中擷取而來。如需相關資訊，請參閱[段落](/docs/services/discovery/query-parameters.html#passages)。段落擷取無法用於 {{site.data.keyword.discoveryshort}} News 集合。

如果您想要試試一些預先建置的查詢，請按一下**使用範例查詢**按鈕。
{: tip}

## 步驟 3：實驗不同的查詢

試試這些查詢：

若要傳回具有 `positive` 觀感的所有文件：按一下**搜尋文件**、**使用 {{site.data.keyword.discoveryshort}} 查詢語言**，然後：
-  按一下**欄位**下拉清單，並選擇 `enriched_text.sentiment.document.label`，針對**運算子**選擇 `contains`，然後輸入**值** `positive`。  

   `enriched_text.sentiment.document.label:positive` 查詢將顯示在**視覺化查詢建置器**下。

若要傳回 `health and fitness` 種類中的所有文件：按一下**搜尋文件**、**使用 {{site.data.keyword.discoveryshort}} 查詢語言**，然後：
-  按一下**欄位**下拉清單，並選擇 `enriched_text.categories.label`，針對**運算子**選擇 `is`，然後輸入**值** `"health and fitness"`。

   `enriched_text.categories.label::"health and fitness"` 查詢將顯示在**視覺化查詢建置器**下。運算子 `::` 指定完全相符。

若要傳回包含 `IBM` 實體但不包含 `Watson` 實體的所有文件：按一下**搜尋文件**、**使用 {{site.data.keyword.discoveryshort}} 查詢語言**，然後：
-  按一下**欄位**下拉清單，並選擇 `enriched_text.entities.text`，針對**運算子**選擇 `contains`，然後輸入**值** `IBM`。按一下**新增規則**，然後針對**欄位**選擇 `enriched_text.entities.text`，針對**運算子**選擇 `does not contain`，然後輸入**值** `Watson`。

   `enriched_text.entities.text:IBM,enriched_text.entities.text:!Watson` 查詢將顯示在**視覺化查詢建置器**下。運算子 `:!` 指定 "does not contain"。

## 步驟 4：建置合併的查詢

您可以將查詢參數結合起來，以建置更多已設定目標的查詢。我們可以試試同時使用 `filter` 和 `query` 參數來傳回關於 {{site.data.keyword.IBM_notm}} 收購的文件。filter 參數會將結果範圍縮小到只提及 `IBM` 的文件，然後 query 參數會依相關性順序傳回關於 `acquisitions` 的所有結果。

1.  按一下建置查詢圖示 ![「查詢」圖示](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->，以開啟查詢頁面。選取包含 {{site.data.keyword.IBM_notm}} Press Releases 的集合，然後按一下**開始使用**。

1.  在**過濾您查詢的文件**下：
    -  按一下**欄位**下拉清單，並選擇 `enriched_text.entities.text`，針對**運算子**選擇 `contains`，然後輸入**值** `IBM`。

       `enriched_text.entities.text:IBM` 會將文件縮減為只提及 `IBM` 實體的那些文件。

1.  在**搜尋文件**下，按一下**使用 {{site.data.keyword.discoveryshort}} 查詢語言**，再：
    -  按一下**欄位**下拉清單，並選擇 `enriched_text.concepts.text`，針對**運算子**選擇 `contains`，然後輸入**值** `world wide web`。

       `enriched_text.concepts.text:world wide web` 將傳回包含 `world wide web` 概念的所有文件，而且那些文件將依相關性順序分級。

1.  按一下**其他選項**，然後按一下**要傳回的欄位**，並選擇**指定**。選取 `text`。這會將回應限制為相關文章的文字，並排除其他一切項目。

1.  按一下**執行查詢**。會有一個相符的文件：`"matching_results": 1`

## 步驟 5：建置聚集

聚集會傳回一組資料值；例如，熱門關鍵字、實體的整體觀感等等。

請嘗試建置此聚集 - 它將傳回 {{site.data.keyword.IBM_notm}} 新聞稿集合中的前 10 個概念。

1.  按一下建置查詢圖示 ![「查詢」圖示](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->，以開啟查詢頁面。選取包含 {{site.data.keyword.IBM_notm}} Press Releases 的集合，然後按一下**開始使用**。

1.  在**包含結果的分析**：
    -  按一下**輸出**下拉清單，並選擇 `Top values`，針對**欄位**選擇 `enriched_text.concepts.text`，然後輸入**計數** `10`。

       `Term` 將傳回 `concepts` `text` 欄位的最常用值。**計數**指定您要傳回的結果數。`term(enriched_text.concepts.text,count:10)` 查詢將顯示在**視覺化查詢建置器**下。   

1.  按一下**其他選項**，然後在**要傳回的文件數**欄位中輸入 `0`。

1.  按一下**執行查詢**。前 10 個概念將同時顯示在**摘要**和 **JSON** 標籤中。「摘要」的範例如下：

## 步驟 6：在 Watson Discovery News 中建置查詢

{{site.data.keyword.discoverynewsshort}} 是一個已利用認知見解預先強化的公用資料集。它隨附於 {{site.data.keyword.discoveryshort}} 中。如需此集合的相關資訊，請參閱 [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html#watson-discovery-news)。

您無法調整 {{site.data.keyword.discoverynewsshort}} 配置、訓練，或將文件新增至 {{site.data.keyword.discoverynewsshort}} 集合中。請參閱[這裡 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://discovery-news-demo.mybluemix.net/){: new_window}，它示範使用 {{site.data.keyword.discoverynewsshort}} 可建置的內容。

下列查詢範例會傳回 {{site.data.keyword.discoverynewsfull}} 中關於 Pittsburgh Steelers 且具有正面觀感的前十篇文章。

1.  按一下建置查詢圖示 ![「查詢」圖示](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->，以開啟查詢頁面。選取 {{site.data.keyword.discoverynewsshort}} 集合，然後按一下**開始使用**。

1.  在**搜尋文件**下，按一下**使用 {{site.data.keyword.discoveryshort}} 查詢語言**，再：
    -  按一下**欄位**下拉清單，並選擇 `text`，針對**運算子**選擇 `contains`，然後輸入**值** `Pittsburgh Steelers`。按一下**新增規則**，再按一下**欄位**下拉清單，並選擇 `enriched_text.sentiment.document.label`，針對**運算子**選擇 `contains`，然後輸入**值** `positive`。

       `text:Pittsburgh Steelers, enriched_text.sentiment.document.label:positive` 查詢將顯示在**視覺化查詢建置器**下。

1.  按一下**其他選項**，然後在 `Number of documents to return`（要傳回的文件數）欄位中輸入 **10**（這是預設值）。

1.  按一下**執行查詢**。即會顯示關於 Pittsburgh Steelers 且具有正面觀感的前十篇文章。

**附註：**對 Watson Discovery News 查詢傳回的結果數上限為 `50`。

新聞文章可能聯合供稿給數個新聞渠道，{{site.data.keyword.discoverynewsfull}} 將挑選每一個新聞渠道，這會導致文章重複。這表示對 {{site.data.keyword.discoverynewsfull}} 的查詢可能會在查詢結果中傳回數篇相同或幾乎相同的文章。若要開啟刪除重複功能，請在**其他選項**下，選擇**排除重複結果**。若要進一步瞭解這項測試版功能，請參閱[從查詢結果中排除重複文件](/docs/services/discovery/query-parameters.html#deduplication)。
