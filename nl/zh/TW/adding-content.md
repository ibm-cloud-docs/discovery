---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-15"

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

# 新增內容

如何決定要使用哪一種文件上傳方法？
{: shortdesc}

-   如果您要整合內容的上傳與現有的應用程式，或建立您自己的自訂上傳機制，請使用 [API](/docs/services/discovery/getting-started.html)。
-   如果您想要快速上傳本端可存取的檔案，請使用 [{{site.data.keyword.discoveryshort}} 工具](/docs/services/discovery/getting-started-tool.html)。當使用 {{site.data.keyword.discoveryshort}} 工具上傳文件時，所有文件都應該有唯一的檔名。如果兩個檔案同名，則上傳新版本時會改寫原始版本。如果您希望具有相同檔名的文件同時存在於集合中，則需要指定「文件 ID」。當您使用 API 或「資料搜索器」上傳文件時，便可以指定「文件 ID」。
-   使用 {{site.data.keyword.discoveryshort}} 工具或 API 連接至 Box、Salesforce 及 Microsoft SharePoint Online 資料來源。如需相關資訊，請參閱[連接至資料來源](/docs/services/discovery/connect.html)。
-   如果您想要以受管理的方式上傳大量檔案，或想要從支援的儲存庫（例如 Db2 資料庫）中擷取內容，請使用[資料搜索器](/docs/services/discovery/data-crawler.html)。

## 使用 API 或工具新增內容

當您準備好將文件新增至集合時，請考量下列事項：

-   可以上傳至 {{site.data.keyword.discoveryshort}} 服務的檔案大小上限為 50MB。
-   範例文件不會自動新增至集合。如果您希望它們成為集合的一部分，則必須新增它們。
-   針對所選取要強化的每個 JSON 欄位，只會強化前 50,000 個字元。
-   建立集合時，您需要選取文件語言（預設值是英文）。如需語言清單，請參閱[語言支援](/docs/services/discovery/language-support.html)。您的文件將以所選取的語言強化。請勿在同一個集合內混合使用數種語言。
-   您可以將 Microsoft Word、PDF、HTML 和 JSON 文件新增至集合中。**附註：**PDF 若是掃描的影像檔，將無法轉換及強化。
-   除非您選擇不同的配置檔，否則將使用所提供的配置檔（其名稱為 Default Configuration）來轉換集合中的文件。如需建立配置檔的相關資訊，請參閱[自訂配置](/docs/services/discovery/building.html#custom-configuration)。
-   文件上傳至資料集合後，會使用針對該集合所選擇的配置檔來轉換及強化文件。如果您稍後決定將集合切換至不同的配置檔，則可以執行該動作，但已上傳的文件仍透過原始配置檔轉換。在切換配置檔之後上傳的所有文件都會使用新的配置檔。如果您想要**整個**集合使用新的配置，則需要建立新的集合、選擇新的配置檔，然後重新上傳所有文件。
-   您不能指定欄位的`資料類型`（例如：`文字`或`日期`）。在文件汲取期間，如果偵測到某欄位尚未存在於索引中，則 {{site.data.keyword.discoveryshort}} 會根據第一個已檢索文件的欄位值，自動偵測該欄位的`資料類型`。
-   現行文件中的資料與先前所汲取文件中的類似資料之間有類型不符的情形時，可能無法汲取文件。例如，在一份文件中的某個欄位可能輸入為 `date`，但在後續文件中卻輸入為 `string`，而導致後續文件無法正確進行檢索。
-   如果您計劃使用自訂記號化（目前僅適用於使用 {{site.data.keyword.discoveryshort}} API 時的日文集合），則必須先新增集合的記號化字典，才能上傳文件。

上傳文件時，適用下列限制：

-   **精簡**方案：21 份進行中文件
-   **進階**方案：105 份進行中文件（X-Small 進階方案例外，它的限制為 50 份進行中文件）
-   **超值**方案：210 份進行中文件

這些限制有可能變更。 

使用 Discovery 服務時，上傳進行中表示文件正在上傳及處理，尚未新增至集合。如果您達到進行中限制，則應該減緩汲取速率。有一個選項是新增含有重試的自動化回復機制。

## 使用 Discovery 工具上傳文件

1.  建立集合。請參閱[為您的文件準備服務](/docs/services/discovery/building.html#preparing-the-service-for-your-documents)。
1.  按一下集合以開啟它。
1.  按一下**上傳文件**按鈕，然後開始透過拖放或瀏覽來上傳文件。

現在，已將您的文件放入佇列中，等待轉換及強化。所需要的時間將視集合的大小而定。在檢索及強化集合之後，集合的詳細資料將顯示在**概觀**區段中。

-   **建立**和**前次更新**日期（請按一下**在 API 中使用這個集合**來查看 `collection_id`、`configuration_id` 和 `environment_id`。）
-   集合中的**文件數**
-   **配置** - 用來轉換此集合的配置檔名稱
-   **錯誤和警告**

如需如何使用 {{site.data.keyword.discoveryshort}} 工具連接至 Box、Salesforce 及 Microsoft SharePoint Online 資料來源的相關資訊，請參閱[連接至資料來源](/docs/services/discovery/connect.html)。


## 使用 API 上傳文件

如需逐步指導教學，請參閱[開始使用 {{site.data.keyword.discoveryshort}} API](/docs/services/discovery/getting-started.html)。

如需 API 的相關資訊，請參閱 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}。

1.  使用 `POST /v1/environments/{environment_id}/collections` 方法來建立集合。
1.  然後使用 `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` 方法，將文件新增至集合中。

## 搜索 URL

您可以使用 {{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} {{site.data.keyword.discoveryshort}} 服務 [Apache Nutch 的索引外掛程式 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/IBM-Watson/nutch-indexer-discovery)來搜索 URL 並對其進行檢索。搜索不會自動更新，所以需要定期重複此程序，讓索引保持最新。
