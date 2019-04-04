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

# 新增內容
{: #addcontent}

如何決定要使用哪一種文件上傳方法？
{: shortdesc}

-   如果您要整合內容的上傳與現有的應用程式，或建立您自己的自訂上傳機制，請使用 [API](/docs/services/discovery?topic=discovery-gs-api#gs-api)。
-   如果您想要快速上傳本端有權存取的檔案，請使用 [{{site.data.keyword.discoveryshort}} 工具](/docs/services/discovery?topic=discovery-getting-started#getting-started)。當使用 {{site.data.keyword.discoveryshort}} 工具上傳文件時，所有文件都應該有唯一的檔名。如果兩個檔案同名，則上傳新版本時會改寫原始版本。如果您希望具有相同檔名的文件同時存在於集合中，則需要指定「文件 ID」。當您使用 API 或「資料搜索器」上傳文件時，便可以指定「文件 ID」。
-   使用 {{site.data.keyword.discoveryshort}} 工具或 API 來連接至 Box、Salesforce、Microsoft SharePoint Online、IBM Cloud Object Storage 和 Microsoft SharePoint 2016 資料來源，或是執行 Web 搜索。如需相關資訊，請參閱[連接至資料來源](/docs/services/discovery?topic=discovery-sources#sources)。
-   如果您想要以受管理的方式上傳大量檔案，或想要從支援的儲存庫（例如 Db2 資料庫）中擷取內容，請使用[資料搜索器](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)。

## 使用 API 或工具新增內容
{: #adding-content-with-the-api-or-tooling}

當您準備好將文件新增至集合時，請考量下列事項：

-   可以上傳至 {{site.data.keyword.discoveryshort}} 服務的檔案大小上限為 50MB。
-   範例文件不會自動新增至集合。如果您希望它們成為集合的一部分，則必須新增它們。（僅適用於在[智慧型文件理解](/docs/services/discovery?topic=discovery-sdu#sdu)版本之前建立的集合。）
-   針對所選取要強化的每個 JSON 欄位，只會強化前 50,000 個字元。
-   建立集合時，您需要選取文件語言（預設值是英文）。如需語言清單，請參閱[語言支援](/docs/services/discovery?topic=discovery-language-support#language-support)。您的文件將以所選取的語言強化。請勿在同一個集合內混合使用數種語言。
-   {{site.data.keyword.discoveryshort}} 可汲取下列檔案類型，並且會忽略所有其他文件類型：

集合 | 精簡方案 | 進階方案 
---------------- | ------------------------------ | ------------------------------------------- 
在[智慧型文件理解 (SDU)](/docs/services/discovery?topic=discovery-release-notes#22jan19) 版本之前，專為 {{site.data.keyword.discoveryfull}} 建立的現有集合  | Microsoft Word、PDF、HTML、JSON | Microsoft Word、PDF、HTML、JSON     
在 [SDU](/docs/services/discovery?topic=discovery-sdu#sdu) 版本之後建立的集合 | PDF、Word、PowerPoint、Excel、JSON\*、HTML\* | PDF、Word、PowerPoint、Excel、PNG\*\*、TIFF\*\*、JPG\*\*、JSON\*、HTML\* 
    
\* {{site.data.keyword.discoveryfull}} 可支援 JSON 和 HTML 文件，但您無法使用 SDU 編輯器來編輯這些文件。若要變更 HTML 和 JSON 文件的配置，您需要使用 API。如需相關資訊，請參閱 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery/){: new_window}。

\*\* 將會掃描個別影像檔（PNG、TIFF、JPG），並擷取文字（若有的話）。另外也會掃描內嵌在 PDF、Word、PowerPoint 和 Excel 檔案中的 PNG、TIFF 和 JPEG 影像，並擷取文字（若有的話）。
-   除非您選擇不同的配置檔，否則將會使用現行配置來轉換集合中的文件。如需建立配置檔的相關資訊，請參閱[自訂配置](/docs/services/discovery?topic=discovery-configservice#custom-configuration)。（僅適用於在[智慧型文件理解](/docs/services/discovery?topic=discovery-sdu#sdu)版本之前建立的集合。）
-   文件上傳至資料集合後，會使用針對該集合所選擇的配置檔來轉換及強化文件。如果您稍後決定將集合切換至不同的配置檔，則可以執行該動作，但已上傳的文件仍透過原始配置檔轉換。在切換配置檔之後上傳的所有文件都會使用新的配置檔。如果您想要**整個**集合使用新的配置，則需要建立新的集合、選擇新的配置檔，然後重新上傳所有文件。（若是使用[智慧型文件理解](/docs/services/discovery?topic=discovery-sdu#sdu)，在您按下**套用變更至集合**按鈕之後，系統會提示您重新上傳文件。）
-   您不能指定欄位的`資料類型`（例如：`文字`或`日期`）。在文件汲取期間，如果偵測到某欄位尚未存在於索引中，則 {{site.data.keyword.discoveryshort}} 會根據第一個已檢索文件的欄位值，自動偵測該欄位的`資料類型`。
-   現行文件中的資料與先前所汲取文件中的類似資料之間有類型不符的情形時，可能無法汲取文件。例如，在一份文件中的某個欄位可能輸入為 `date`，但在後續文件中卻輸入為 `string`，而導致後續文件無法正確進行檢索。
-   如果您計劃使用自訂記號化（目前僅適用於使用 {{site.data.keyword.discoveryshort}} API 時的日文集合），則必須先新增集合的記號化字典，才能上傳文件。

## 使用 Discovery 工具上傳文件
{: #upload_tooling}

1.  建立集合。請參閱[為您的文件準備服務](/docs/services/discovery?topic=discovery-configservice#preparing-the-service-for-your-documents)。
1.  按一下集合以開啟它。
1.  按一下**上傳文件**按鈕，然後開始透過拖放或瀏覽來上傳文件。

現在，已將您的文件放入佇列中，等待轉換及強化。所需要的時間將視集合的大小而定。在檢索及強化集合之後，集合的詳細資料將顯示在**概觀**區段中。

-   集合中的**識別的欄位**（僅適用「智慧型文件理解」。）
-   **建立**和**前次更新**日期（請按一下**在 API 中使用這個集合**來查看 `collection_id`、`configuration_id` 和 `environment_id`。）
-   集合中的**文件數**
-   **配置** - 用來轉換此集合之配置檔的名稱（僅適用於在[智慧型文件理解](/docs/services/discovery?topic=discovery-sdu#sdu)版本之前建立的集合。）
-   **錯誤和警告**

如需如何使用 {{site.data.keyword.discoveryshort}} 工具連接至 Box、Salesforce、Microsoft SharePoint Online、IBM Cloud Object Storage 和 Microsoft SharePoint 2016 資料來源或如何使用此工具執行 Web 搜索的相關資訊，請參閱[連接至資料來源](/docs/services/discovery?topic=discovery-sources#sources)。


## 使用 API 上傳文件
{: #upload_api}

如需逐步指導教學，請參閱[開始使用 {{site.data.keyword.discoveryshort}} API](/docs/services/discovery?topic=discovery-gs-api#gs-api)。

如需 API 的相關資訊，請參閱 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery/){: new_window}。

1.  使用 `POST /v1/environments/{environment_id}/collections` 方法來建立集合。
1.  然後使用 `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` 方法，將文件新增至集合中。

## 搜索 URL
{: #crawl_urls}

您可以使用 {{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} {{site.data.keyword.discoveryshort}} 服務 [Apache Nutch 的索引外掛程式 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/IBM-Watson/nutch-indexer-discovery)來搜索 URL 並對其進行檢索。搜索不會自動更新，所以需要定期重複此程序，讓索引保持最新。 

您也可以選擇使用測試版 Web 搜索連接器。請參閱[連接至資料來源](/docs/services/discovery?topic=discovery-sources#connectwebcrawl)。
