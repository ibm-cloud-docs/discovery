---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-03-07"

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
{:gif: data-image-type='gif'}

# 智慧型文件理解
{: #sdu}

「智慧型文件理解 (SDU)」是訓練 {{site.data.keyword.discoveryfull}} 在您的文件中擷取自訂欄位的新方法。自訂將文件檢索至 {{site.data.keyword.discoveryshort}} 的方式，將改善應用程式傳回的答案。

透過 SDU，您可以在文件中標註欄位，以訓練自訂轉換模型。在您標註時，Watson 會學習並開始預測註釋。SDU 模型可以匯出並用於其他集合。 

## 支援的文件類型和瀏覽器
{: #doctypes}

「智慧型文件理解」支援的文件類型： 
-  精簡方案：PDF、Word、PowerPoint、Excel、JSON\*、HTML\*
-  進階方案：PDF、Word、PowerPoint、Excel、PNG\*\*、TIFF\*\*、JPG\*\*、JSON\*、HTML\* 

\* {{site.data.keyword.discoveryfull}} 可支援 JSON 和 HTML 文件，但您無法使用 SDU 編輯器來編輯這些文件。若要變更 HTML 和 JSON 文件的配置，您需要使用 API。如需相關資訊，請參閱 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery/){: new_window}。

\*\* 將會掃描個別影像檔（PNG、TIFF、JPG），並擷取文字（若有的話）。另外也會掃描內嵌在 PDF、Word、PowerPoint 和 Excel 檔案中的 PNG、TIFF 和 JPEG 影像，並擷取文字（若有的話）。

支援的瀏覽器：Chrome 和 Firefox。

## 使用智慧型文件理解編輯器
{: #annotate}

SDU 編輯器僅適用於包含支援的文件類型且未套用「元素分類」強化的新集合。現有的「專用」集合會使用原始配置方法。如果您想要對現有的集合使用 SDU 編輯器，您需要建立新的集合，並將那些文件上傳至該集合。如果您不想要使用 SDU 編輯器，可以使用 API 來設定您的配置，請參閱 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery/){: new_window}。{: important}

SDU 編輯器功能僅於 {{site.data.keyword.discoveryshort}} 工具中提供，未於 API 中提供。
{: note}

導覽「智慧型文件理解」編輯器：

如果您尚未建立 {{site.data.keyword.discoveryshort}} 實例和環境，請參閱[開始使用](/docs/services/discovery?topic=discovery-getting-started#getting-started)，以取得指示。
{: tip}

1. 在**管理資料**畫面上，按一下**上傳您自己的資料**按鈕，並且在 {{site.data.keyword.discoveryshort}} 中建立新的「專用」集合。
1. 您可以依偏好的方式，將文件拖放至您的集合中，或按一下**從電腦瀏覽**，以上傳文件。上傳完成之後，會顯示下列資訊：
   -  從文件識別的欄位。
   -  已將強化套用至您的文件。{{site.data.keyword.discoveryshort}} 會自動將「實體擷取」、「觀感分析」、「種類分類」和「概念標記」強化套用至 `text` 欄位（除非您是使用連接器來匯入文件）。您可以在 `text` 欄位中新增（或移除）其他強化。
   -  您可以立即執行預先建置的查詢。
1. 按一下右上方的**配置資料**。 
1. **配置資料**畫面上會有三個標籤：**識別欄位**、**管理欄位**和**強化欄位**。

   - **識別欄位**包含 SDU 編輯器。此標籤會取代原始 {{site.data.keyword.discoveryshort}} 畫面上的**轉換**及**正規化**標籤。 
   - **管理欄位**會列出所有檢索的欄位（依預設會檢索所有欄位）。將您不想要檢索的任何欄位切換為關閉。例如，您的 PDF 可能有未包含有用資訊的執行中標頭或標底，所以您可以將那些欄位排除而不要檢索。您也可以在這裡依欄位分割文件，請參閱[分割文件](/docs/services/discovery?topic=discovery-sdu#splitting)。
   - **強化欄位**相當於原始畫面上的**強化**標籤。如需強化的相關資訊，請參閱[新增強化](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)。**上傳範例文件**選項不適用於 SDU 集合。

   如果您先前沒有上傳任何文件，請在左上方按一下您的集合名稱，回到**概觀**畫面，或是按一下 ![管理資料](/images/icon_yourData.png) 圖示，然後選擇您的集合。將文件拖放至您的集合中，或按一下**從電腦瀏覽**。完成起始上傳之後，右上方會出現**上傳文件**按鈕。
{: important}

   使用「智慧型文件理解」時，只能強化 `text` 欄位。請勿嘗試強化任何其他欄位。
   {: important}

1. 開啟**識別欄位**標籤。「智慧型文件理解」編輯器中會從您的集合自動載入最多二十 (20) 個文件。

頂端的工具列可讓您：
- 選擇要標註的文件
- 導覽顯示的文件
- 調整頁面視圖（`單一頁面視圖`、`放大`、`縮小`）、`清除變更`及`匯出/匯入模型`。按一下`單一頁面視圖`來切換顯示畫面 - 您可以將註釋和文件分開或一起檢視。

您也可以使用 {{site.data.keyword.discoveryshort}} 工具來搜索 Box、Salesforce、Microsoft SharePoint Online、IBM Cloud Object Storage 和 Microsoft SharePoint 2016 資料來源，或是執行 Web 搜索。請按一下**連接資料來源**按鈕，如需相關資訊，請參閱[連接至資料來源](/docs/services/discovery?topic=discovery-sources#sources)。如果您使用此方法來建立集合，將不會自動套用任何強化。
{: tip}

## 如何標註文件
{: #documents}

**附註：**表格是在不同步驟中進行標註。

在開始標註之前，請參閱[標註文件和表格的最佳作法](/docs/services/discovery?topic=discovery-sdu#bestpractices)。

1. 一組預設欄位會出現在文件右側。可用欄位為 `answer`、`author`、`footer`、`header`、`question`、`subtitle`、`table_of_contents`、`text` 及 `title`。如果您想要建立一或多個新的自訂欄位，請按一下**建立新的項目**。您的自訂標籤數目限制如下：精簡方案 - `0`，進階方案 - `5`，超值方案 - `20`。
1. 按一下右側的欄位標籤加以啟動。
1. 按一下 SDU 編輯器中代表該欄位的內容。系統會將其強調顯示。 
   - 或者，您也可以選取右側的欄位標籤，並將其拖曳至 SDU 編輯器中的內容。 
   - 若要清除變更，請按一下工具列上的**清除變更**按鈕。
1. 按一下**提交**。
   **附註：**在您標註時，Watson 會學習並開始預測註釋。請繼續標註，直到 Watson 正確且一致地識別欄位為止。
1. 當您完成標註後，請按一下**套用變更至集合**。**上傳文件**畫面隨即開啟。重新上傳集合中的文件。上傳完成之後，系統會將您重新導向至**管理資料**畫面。

欄位  |定義       
------ | ------ 
answer | 問/答配對（通常位於常見問題）中問題的回答。
author | 作者（或多位作者）的名稱。
footer | 使用此標籤來表示出現在頁面底端的文件相關 meta 資訊（例如頁碼或參照）。
header | 使用此標籤來表示出現在頁面頂端的文件相關 meta 資訊。
question | 問/答配對（通常位於常見問題）中的問題。
subtitle | 所要標註之文件的次要標題。
table_of_contents | 在文件目錄的清單上使用此標籤。
text    | 對標準複製文字（包括段落、定義或任何非標題、部分表格、回答、作者、子標題、標頭或標底的字組）使用此標籤。
title    | 所要標註之文件的主要標題。

## 如何標註表格
{: #tables}

表格標註為測試版。可以在[這裡](/docs/services/discovery?topic=discovery-release-notes#beta-features)找到說明測試版特性的陳述。
{: important}

在開始標註之前，請參閱[標註文件和表格的最佳作法](/docs/services/discovery?topic=discovery-sdu#bestpractices)。

1. 從 SDU 編輯器右邊選取 `table` 欄位，然後在文件中選取表格。 
1. 將游標移至表格上方，以顯示**標註表格**按鈕。按一下該按鈕以開啟表格編輯器。
1. 首先，概述該表格：
   - 選取 `column` 欄位。
   - 按一下表格中的直欄加以啟動。
   - 選取 `row` 欄位。
   - 按一下表格中的列加以啟動。

   表格的概述將出現在左側的表格預覽中。

   **附註：**當您標註表格時，Watson 會學習並開始預測註釋。
1. 其次，標示表格內的內容。
1. 當您完成表格的標註後，請按一下**完成標註**。
1. 按一下**套用變更至集合**。**上傳文件**畫面隨即開啟。重新上傳集合中的文件。上傳完成之後，系統會將您重新導向至**管理資料**畫面。

請使用此視訊做為指南 ![表格標註視訊](images/SDU_table_demo.gif){: gif}

欄位  |定義       
------ | ------ 
body | 包含資訊的任何非標頭資料格
column header | 表格中每個直欄的標題資料格（如果存在的話）
multi-column header | 跨越多個直欄的任何標題資料格
row title | 列標題直欄的直欄標頭（如果存在的話）
row header | 表格中每一列的列標籤（如果存在的話）
multi-row header | 橫跨多列的任何列標籤

## 分割文件
{: #splitting}

**管理欄位**標籤包含**分割文件以改善查詢結果**的選項。此選項可讓您依欄位名稱將文件分割成區段。分割之後，每個區段都是個別的文件，將會以個別的查詢結果強化、檢索並傳回。 

文件會依單一欄位名稱分割，例如：`title`、`author`、`question`。 

注意事項：

  - 每份文件的區段數目限制為 `250`。在 `249` 個區段之後的所有其餘文件內容將儲存在區段 `250` 內。

  - 每一個區段都計入您方案的文件限制內。{{site.data.keyword.discoveryshort}} 會進行區段檢索，直到達到方案限制為止。如需文件限制，請參閱 [Discovery 定價方案](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)。

  - PDF 和 Word meta 資料（以及任何自訂 meta 資料）會擷取出來，並連同每個區段一起包含在索引中。文件的每個區段將包括相同的 meta 資料。

  - 如果分割的文件已更新，並需要重新上傳，則應使用[更新文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery#update-a-document){: new_window} 方法來取代文件。應使用 `/environments/{environment_id}/collections/{collection_id}/documents/{document_id}` API 的 POST 方法來上傳文件，並將其中一個現行區段的 `parent_id` 欄位內容指定為 `{document_id}` 路徑變數。所有區段將會改寫，除非文件更新版本的區段總數少於原始版本。那些較舊的區段將保留在索引中，且可使用 API 進行個別刪除。如需詳細資料，請參閱 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery#delete-a-document){: new_window}。 

## 匯入及匯出模型
{: #import}

使用 SDU 編輯器來定義模型之後，可將其儲存，並重複使用於其他集合。

您可以使用編輯器頂端的工具列來匯入或匯出已完成的 SDU 模型。請按一下最後一個圖示，然後選擇 `Import model` 或 `Export model`。

匯出的模型副檔名為 `.sdumodel`。 

匯入的模型旨在不進行任何進一步標註的情況下使用。如果將其匯入之後，又繼續標註，將會完全改寫該模型。如果您計劃將模型匯入新的集合，最佳作法是建立只包含 1 個文件的新集合，匯入該模型，然後再上傳其餘文件。

## 標註文件和表格的最佳作法
{: #bestpractices}

表格標註為測試版。可以在[這裡](/docs/services/discovery?topic=discovery-release-notes#beta-features)找到說明測試版特性的陳述。
{: important}

- 遵循所有準則，並在所有文件上使用一致的標籤
- 不要標示空格
- 在影像和圖表上使用 `image` 標籤
- 請勿以不同方式處理**粗體**、_斜體_或加底線的文字，應依上下文（而非樣式）加上標籤。 
- 標示文件時，請從首頁處理到最後一頁。
- 如果您不正確地標示某個項目，請為該項目選擇另一個標籤來改寫第一個標籤。
- 可以隨時提交頁面。提交之前，請確定已完成所有適當的標籤。
- 出現文字覆蓋其他文字的文件和表格視為「雙重重疊」，因此無法標註。請向管理者報告這些文件。
- 無法標註在單一頁面上包含多個文字直欄的文件和表格。請向管理者報告這些文件。
- 註腳只有在出現於頁面底端時才應加上標籤，並在文件的主要內文中進行參照。
- 出現在區段或清單內的附註（例如，明確稱為「附註」）應該標示為 `text`。
- 如果您不確定表格是否已正確標示，且預覽窗格沒有回應，則應該在您的瀏覽器中重新載入頁面，表格會按順序重新標示以確保正確性。

