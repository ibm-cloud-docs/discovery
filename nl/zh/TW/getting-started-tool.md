---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-08"

subcollection: discovery

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:pre: .pre}
{:important: .important}
{:deprecated: .deprecated}
{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:hide-dashboard: .hide-dashboard}
{:apikey: data-credential-placeholder='apikey'}
{:url: data-credential-placeholder='url'}
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}

# 開始使用
{: #getting-started}

在這個簡短的指導教學中，我們將介紹 {{site.data.keyword.discoveryshort}} 工具，並逐步完成建立及搜尋專用資料集合的處理程序。
{: shortdesc}

如果您偏好在 API 中工作，請參閱[開始使用 API](/docs/services/discovery?topic=discovery-gs-api#gs-api)。
{: tip}

## 開始之前
{: #before-you-begin-tool}
{: hide-dashboard}

您需要服務實例才能開始。
{: hide-dashboard}

1.  {: hide-dashboard}移至 {{site.data.keyword.cloud_notm}} 型錄中的 [{{site.data.keyword.discoveryshort}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/catalog/services/discovery) 頁面。

    如果您未另行選擇，則服務實例會建立在**預設**資源群組中，且之後*無法*變更。此群組足以用來嘗試此服務。

    如果您是為更完善的用途而建立實例，則請進一步瞭解[資源群組 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/docs/resources/bestpractice_rgs.html#bp_resourcegroups){: new_window}。
1.  {: hide-dashboard}註冊免費的 {{site.data.keyword.cloud_notm}} 帳戶或登入。
1.  {: hide-dashboard}按一下**建立**。

## 步驟 1：啟動工具
{: #launch-the-tooling}

建立 {{site.data.keyword.discoveryshort}} 服務的實例之後，將會顯示您的服務清單。
{: hide-dashboard}

1.  {: hide-dashboard}按一下您建立的 {{site.data.keyword.discoveryshort}} 服務實例，以移至服務儀表板。
1.  在**管理**頁面上，按一下**啟動工具**。如果系統提示您登入工具，請提供您的 {{site.data.keyword.cloud_notm}} 認證。

<!-- To do: Add screenshot for developer console -->

## 步驟 2：建立集合
{: #create-a-collection-tool}

您在 {{site.data.keyword.discoveryshort}} 工具中的首要步驟是建立資料集合。

集合是您的文件集。*為什麼我需要多個集合？*有幾個原因：

- 您可能想要多個集合，以區隔不同對象的結果。
- 資料可能差異很大，以致於同時查詢所有資料並沒有意義。

您也可以使用公用、預先強化的 {{site.data.keyword.discoverynewsshort}} 資料集合。其已備妥可供查詢，您可以立即開始對其建立查詢。您無法調整其配置，或將文件新增至 {{site.data.keyword.discoverynewsshort}} 中。

1.  按一下 ![環境詳細資料](images/env_icon.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->，然後選擇**建立環境**。
1.  當環境備妥後，按一下**上傳您自己的資料**按鈕，即可**命名您的新集合**。將您的集合命名為 **InstallDocs**。

    建立集合時，您可以在**進階**之下選擇名為 **Default Contract Configuration** 的配置檔。此配置僅支援「元素分類」強化，可用來從 PDF 中的元素擷取參與方、本質和種類。如需詳細資料，請參閱[元素分類](/docs/services/discovery?topic=discovery-element-classification#element-collection)。針對此指導教學，請勿選擇此選項。

您也可以使用 {{site.data.keyword.discoveryshort}} 工具來搜索 Box、Salesforce、Microsoft SharePoint Online、IBM Cloud Object Storage 和 Microsoft SharePoint 2016 資料來源，或是執行 Web 搜索。請按一下**連接資料來源**按鈕，如需相關資訊，請參閱[連接至資料來源](/docs/services/discovery?topic=discovery-sources#sources)。
{: tip}

## 步驟 3：下載範例文件，並上傳至您的集合
{: create-custom-configuration}

1.  下載此 PDF 範例文件：<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/watsonexplorerinstall.pdf" download>Watson Explorer Installation Guide <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示" title="外部鏈結圖示"></a>。請參閱[支援的文件類型](/docs/services/discovery?topic=discovery-sdu#doctypes)，以取得 {{site.data.keyword.discoveryshort}} 支援的文件類型完整清單。 

    在某些瀏覽器中，鏈結會在新視窗中開啟，而不是儲存在本端。如果發生此情況，請在瀏覽器的`檔案`功能表中選取`另存新檔`，以儲存檔案的副本。{: tip}

1.  將文件上傳至您的集合。將其拖放至您的集合中，或按一下**從電腦瀏覽**，以上傳文件。上傳完成之後，會顯示下列資訊：
    -  文件數 (1)。
    -  從文件識別的欄位。您應該會看到一個已識別的欄位 `text`。我們會稍微識別其他欄位。
    -  已將強化套用至您的文件。{{site.data.keyword.discoveryshort}} 會自動將「實體擷取」、「觀感分析」、「種類分類」和「概念標記」強化套用至 `text` 欄位。請在[這裡](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)進一步瞭解強化。 
    -  您可以立即執行預先建置的查詢。
1.  讓我們試著對所設定的層次進行快速的「自然語言查詢」。按一下右下方的**建置您自己的查詢**。
1.  在**建置查詢**畫面上，按一下**搜尋文件**，然後按一下**使用自然語言**。輸入 `What are the minimum hardware requirements`，然後按一下**執行查詢**按鈕。按一下右邊的 **JSON** 標籤。該結果的精確度應該還可以更好，所以我們要使用「智慧型文件理解」來改善。
1.  按一下左上方的集合名稱 (**InstallDocs**)，以回到**概觀**畫面。  
 
## 步驟 4：標註文件
{: #upload-your-documents}

如需標註文件的相關資訊，請參閱[智慧型文件理解](/docs/services/discovery?topic=discovery-sdu#sdu)。
{: tip}

1.  按一下右上方的**配置資料**。 
1.  **配置資料**畫面上會有三個標籤：**識別欄位**、**管理欄位**和**強化欄位**。
1.  畫面上會顯示 `Watson Explorer Installation Guide`，可供在**識別欄位**標籤上進行標註。所有可用欄位（`answer`、`author`、`footer`、`header`、`question`、`subtitle`、`table_of_contents`、`text` 和 `title`）都會顯示在右邊的**欄位標籤**清單中。如果您購買「進階」或「超值」方案，則可以建立您自己的自訂標籤。

    由於整個文件目前是識別為 `text`，所以右邊的標記整個都是黃色。當您進行標註時（系統即開始預測），顏色會隨著更新。
    {: tip}

1.  按一下 `title`，然後選取 `Installation and Integration Guide` 旁邊的標記。按一下**提交頁面**按鈕。
1.  在左邊的頁面預覽中，按一下第 3 頁。請注意已經為此頁面預測其為 `title`。按一下**提交頁面**按鈕。
1.  在第 4 頁上選取 `footer` 標籤，並選取標底旁邊的標記。按一下**提交頁面**按鈕。
1.  在第 5 頁和第 6 頁上，使用 `footer` 標籤來標註標底。提交每一頁。再往下按幾頁，您會發現 {{site.data.keyword.discoveryshort}} 已正確地預測標底。在第 7 頁、第 9 頁和第 10 頁上標註 `title`（靠左）和 `subtitle`（縮排），並個別提交每一頁。
1.  再往下按幾頁，查看所預測的標題和子標題。如果需要任何變更，則標註那些頁面，然後按一下**提交頁面**按鈕。
1.  現在按一下**管理欄位**標籤，然後在**分割文件以改善查詢結果**之下，依據 `subtitle` 分割文件。 
1.  目前說明這些標註事項應該就夠了。按一下右上方的**套用變更至集合**按鈕。**上傳您的文件**對話框隨即出現。瀏覽至原始 `watsonexplorerinstall.pdf` 檔案並將其上傳。這樣會將所有註釋套用至您的索引。完成檢索之後，**概觀**畫面隨即開啟。您現在應該會看到超過 30 個文件，並且從您的資料識別了下列 4 個欄位：`footer`、`subtitle`、`text` 和 `title`。（如果變更未於數分鐘內顯示，請重新整理瀏覽器視窗。）

    若要排除不進行檢索的欄位（例如 `footer`），您可以開啟**管理欄位**標籤，然後將該欄位切換為 `off`。
    {: tip}

## 步驟 5：開始查詢
{: #build-a-query}

1.  按一下右下方的**建置您自己的查詢**。
1.  在**建置查詢**畫面上，按一下**搜尋文件**，然後按一下**使用自然語言**。輸入 `What are the minimum hardware requirements`，然後按一下**執行查詢**按鈕。 
1.  按一下右邊的 **JSON** 標籤。查看 `results` 之下的 `text`。針對該查詢傳回的答案會更加精準。

其他資源：
-  若要進一步瞭解文件的資料綱目，請按一下靠最左邊的**檢視資料綱目**圖示，或按一下 **JSON** 標籤。如需詳細資訊，請參閱 [Discovery 資料綱目](/docs/services/discovery?topic=discovery-query-concepts#discovery-schema)。
-  按一下**使用範例查詢**按鈕，試用一下以「{{site.data.keyword.discoveryshort}} 查詢語言」撰寫的範例查詢。

## 後續步驟
{: #next-steps-tool}

現在，您有一個能發揮作用且已移入資料的 {{site.data.keyword.discoveryshort}} 服務實例。您現在可以開始新增更多文件和強化，以及標註其他文件，以自訂您的集合。如需相關資訊，請參閱[智慧型文件理解](/docs/services/discovery?topic=discovery-sdu#sdu)。
