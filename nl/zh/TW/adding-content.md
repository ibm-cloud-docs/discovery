---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-10"

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

如何決定要使用哪一個文件上傳方法？
{: shortdesc}

-   如果您要整合內容的上傳與現有的應用程式，或建立您自己的自訂上傳機制，請使用 [API](/docs/services/discovery/getting-started.html)。
-   如果您想要快速上傳本端可存取的檔案，請使用 [{{site.data.keyword.discoveryshort}} 工具](/docs/services/discovery/getting-started-tool.html)。當使用 {{site.data.keyword.discoveryshort}} 工具上傳文件時，所有文件都應該有唯一的檔名。如果兩個檔案同名，則上傳新版本時會改寫原始版本。如果您希望具有相同檔名的文件同時存在於集合中，則需要指定「文件 ID」。當您使用 API 或「資料搜索器」上傳文件時，便可以指定「文件 ID」。
-   如果您想要以受管理的方式上傳大量檔案，或想要從支援的儲存庫（例如 Db2 資料庫）中擷取內容，請使用[資料搜索器](/docs/services/discovery/data-crawler.html)。

## 使用 API 或工具新增內容

當您準備好將文件新增至集合時，請考量下列事項：

-   可以上傳至 {{site.data.keyword.discoveryshort}} 服務的檔案大小上限為 50MB。

-   範例文件不會自動新增至集合。如果您希望它們成為集合的一部分，則必須新增它們。

-   建立集合時，您需要選取文件語言（預設值是英文）。如需語言清單，請參閱[語言支援](/docs/services/discovery/language-support.html)。您的文件將以所選取的語言強化。請勿在同一個集合內混合使用數種語言。

-   您可以將 Microsoft Word、PDF、HTML 和 JSON 文件新增至集合中。**附註：**PDF 若是掃描的影像檔，將無法轉換及強化。 

-   除非您選擇不同的配置檔，否則將使用所提供的配置檔（其名稱為「預設配置」）來轉換集合中的文件。如需建立配置檔的相關資訊，請參閱[自訂配置](/docs/services/discovery/building.html#custom-configuration)。

-   文件上傳至資料集合後，會使用針對該集合所選擇的配置檔來轉換及強化文件。如果您稍後決定將集合切換至不同的配置檔，您可以執行該動作，但已經上傳的文件仍會透過原始配置檔轉換。在切換配置檔之後上傳的所有文件將使用新的配置檔。如果您想要**整個**集合使用新的配置，則需要建立新的集合、選擇新的配置檔，然後重新上傳所有文件。

## 使用 Discovery 工具上傳文件

1.  建立集合。請參閱[為您的文件準備服務](/docs/services/discovery/building.html#preparing-the-service-for-your-documents)。
1.  按一下集合以開啟它。
1.  按一下**上傳文件**按鈕，然後開始透過拖放或瀏覽來上傳文件。

現在，已將您的文件放入佇列中，等待轉換及強化。所需要的時間將視集合的大小而定。在檢索及強化集合之後，集合的詳細資料將顯示在**概觀**區段中。

-   **建立**和**前次更新**日期（請按一下**在 API 中使用這個集合**來查看 `collection_id`、`configuration_id` 和 `environment_id`。）
-   集合中的**文件數**
-   **配置** - 用來轉換此集合的配置檔名稱
-   **錯誤和警告**

## 使用 API 上傳文件

如需逐步指導教學，請參閱[開始使用 {{site.data.keyword.discoveryshort}} API](/docs/services/discovery/getting-started.html)。

如需 API 的相關資訊，請參閱 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}。

1.  使用 `POST /v1/environments/{environment_id}/collections` 方法來建立集合。
1.  然後使用 `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` 方法，將文件新增至集合中。

## 搜索 URL

您可以使用 {{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} {{site.data.keyword.discoveryshort}} 服務 [Apache Nutch 的索引外掛程式 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/IBM-Watson/nutch-indexer-discovery)來搜索 URL 並對其進行檢索。搜索不會自動更新，所以需要定期重複此程序讓索引保持最新。
