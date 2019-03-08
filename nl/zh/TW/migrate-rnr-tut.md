---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-09"

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


# 指導教學：從 Retrieve and Rank 移轉
{: #migrate-rnr}

從 {{site.data.keyword.retrieveandrankshort}} 移轉至 {{site.data.keyword.discoveryfull}} 服務。「Cranfield 入門指導教學」的延續

## 概觀
{: #overview}
本指導教學使用範例資料來引導您完成建立及訓練的 {{site.data.keyword.discoveryfull}} 服務的處理程序。本指導教學使用 [{{site.data.keyword.retrieveandrankshort}} 入門指導教學](/docs/services/retrieve-and-rank/getting-started.html)中所使用的相同資料集，但您可以使用相同的方法來建立使用您自己的資料的服務實例。

使用者將資料從 {{site.data.keyword.retrieveandrankshort}} 移轉到 {{site.data.keyword.discoveryshort}} 的處理程序是由兩個主要步驟組成。

1. 移轉集合資料。
2. 移轉訓練資料。

移轉訓練的集合資料時，**最**重要的是_保持相同的文件 ID_。這是因為您的訓練資料使用這些 ID 來參照基準 (ground truth)，如果從 {{site.data.keyword.retrieveandrankshort}} 移到 {{site.data.keyword.discoveryshort}} 時變更了 ID，則重新分級將完全關閉（或訓練甚至不會啟動）。{{site.data.keyword.discoveryshort}} 可讓您在 API 上傳處理程序中指定文件 ID，因此遵循本文件中的準則即可避免此問題。{{site.data.keyword.retrieveandrankshort}} 訓練資料通常儲存在 `csv` 檔案中。在本指導教學中，會使用這個 `csv` 檔案將範例訓練資料上傳至 {{site.data.keyword.discoveryshort}}。從 {{site.data.keyword.retrieveandrankshort}} 工具中匯出之訓練資料的移轉，詳述於[從服務移轉訓練資料](/docs/services/discovery/migrate-dcs-rr.html#extract-train)。

本指導教學假設 {{site.data.keyword.retrieveandrankshort}} 的設定類似於 [{{site.data.keyword.retrieveandrankshort}} 入門指導教學](/docs/services/retrieve-and-rank/getting-started.html)，並使用[這裡](/docs/services/discovery/migrate-dcs-rr.html#source)所說明的「從來源路徑移轉」。如需其他移轉選項，請參閱[評估您到 Watson Discovery 服務的移轉路徑](/docs/services/discovery/migrate-dcs-rr.html#evaluate)。

若要完成本指導教學，您需要下列各項：

-  **cURL**。您可以從 [haxx.se ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://curl.haxx.se/){: new_window} 安裝您的作業系統所適用的 cURL 版本。您必須安裝支援 Secure Sockets Layer (SSL) 通訊協定的版本。請務必在 PATH 環境變數中包含已安裝的二進位檔。
-  範例 Cranfield 資料。本指導教學使用 {{site.data.keyword.retrieveandrankshort}} 入門指導教學中的範例集合資料。[Cranfield json 資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-data.json){: new_window}
-  **範例資料基準**。本指導教學使用來自 {{site.data.keyword.retrieveandrankshort}} 入門指導教學中的範例 Cranfield 基準。[Cranfield 基準 csv ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-gt.csv){: new_window}
-  **Python 第 2 版**。若要檢查是否已安裝 Python，請在命令提示字元中輸入 `python --version`，並確定版本號碼是從 2 開始。如果您需要安裝 Python，請參閱[下載 Python ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://wiki.python.org/moin/BeginnersGuide/Download){: new_window}。
-  資料上傳 Script：[Discovery 文件上傳器 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-upload.py){: new_window}
-  訓練資料上傳 Script：[Discovery 訓練上傳器 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-train.py){: new_window}

開始本指導教學之前，需要符合下列必要條件：

-  本指導教學假設您已建立 {{site.data.keyword.discoveryshort}} 實例，如果您需要如何建立 {{site.data.keyword.discoveryshort}} 實例的指示，請參閱[下列指導教學](/docs/services/discovery/getting-started.html)。

-  本指導教學假設您有服務認證。
   -  如果您位於 {{site.data.keyword.Bluemix_notm}} 上的 Watson {{site.data.keyword.discoveryshort}} 服務中，請按一下**服務認證**。
   -  按一下「動作」下的**檢視認證**。
   -  複製 `apikey` 值，並確定 `url` 值符合下面範例中的值，如果不符合，請一併取代。

## 將 Cranfield 資料新增至 Discovery

1.  建立環境。

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{ "name": "my_environment", "description": "My environment" }' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    複製所傳回 JSON 中列出的 `environment-id`。

1. 建立集合。

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{ "name": "test_collection", "description": "My test collection", "configuration_id": "{configuration_id}", "language_code": "en" }' "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07"
    ```
    {: pre}

    複製所傳回 JSON 中列出的 `collection-id`。

1.  新增要搜尋的文件。
    1.  如果尚未下載 [cranfield-data.json ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-data.json){: new_window} 檔案，請下載它。這是在 {{site.data.keyword.retrieveandrankshort}} 中使用之文件的來源。Cranfield 集合文件採用 JSON 格式，其為 {{site.data.keyword.retrieveandrankshort}} 接受的格式，也非常適用於 Watson {{site.data.keyword.discoveryshort}}。
        **附註：**{{site.data.keyword.discoveryshort}} 不需要上傳 Solr 綱目。這是因為 {{site.data.keyword.discoveryshort}} 會自動從 JSON 結構推斷綱目。
    1.  在[這裡 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-upload.py){: new_window} 下載「資料上傳 Script」。這個 Script 會將 Cranfield json 上傳至 {{site.data.keyword.discoveryshort}}。
        Script 會讀取整個 JSON 檔案，並使用 {{site.data.keyword.discoveryshort}} 中的預設配置，將每個個別的 JSON 文件傳送至 {{site.data.keyword.discoveryshort}} 服務。
        **附註：**{{site.data.keyword.discoveryshort}} 中的預設配置提供的設定類似於 {{site.data.keyword.retrieveandrankshort}} 中的預設 Solr 配置。
    1.  發出下列指令，將 `cranfield-data-json` 資料上傳至 `cranfield_collection` 集合。將 `{apikey_value}`、`{path_to_file}`、`{environment_id}`、`{collection_id}` 取代為您的資訊。請注意，還有其他選項，-d 代表除錯，而 –v 代表 curl 的詳細輸出。

        ```bash
        python ./disco-upload.py -u apikey:{apikey_value} -i {path_to_file}/cranfield-data.json -e {environment_id} -c {collection_id}
        ```
        {: pre}

1.  上傳處理程序完成之後，您可以發出下列指令來檢視集合詳細資料，以檢查文件是否存在於該處：

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07"
    ```
    {: pre}

    其輸出將如下所示：

    ```json
    {
      "collection_id": "f1360220-ea2d-4271-9d62-89a910b13c37",
      "name": "democollection",
      "configuration_id": "6963be41-2dea-4f79-8f52-127c63c479b0",
      "language": "en",
      "status": "available",
      "description": "this is a demo collection",
      "created": "2015-08-24T18:42:25.324Z",
      "updated": "2015-08-24T18:42:25.324Z",      
      "document_counts": {
        "available": 1000,
        "processing": 20,
        "failed": 180
      },
      "disk_usage": {
        "used_bytes": 260
      },
      "training_status": {
        "data_updated": null,
        "total_examples": 0,
        "sufficient_label_diversity": false,
        "processing": false,
        "minimum_examples_added": true,
        "successfully_trained": null,
        "available": false,
        "notices": 0,
        "minimum_queries_added": false        
      }
    }
    ```
    {: codeblock}

請查看 `document_counts` 區段，看看已順利上傳多少文件。我們預期此範例資料集不會有任何文件失敗。不過，如果是其他資料集，您可能會看到失敗文件計數。如果您有任何失敗文件計數，則可以檢視通知 API，以查看錯誤訊息。請在[這裡 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-notices){: new_window} 查看該區段，以檢閱通知 API 指令。

傳回的 `training` 區段會提供您訓練的相關資訊。我們將在您上傳訓練資料之後，檢閱該區段。

## 將訓練資料新增至 Discovery

Watson {{site.data.keyword.discoveryshort}} 服務使用機器學習模型將文件重新分級。若要這麼做，您需要訓練模型。訓練是發生在您載入足夠的查詢以及適當的評比文件之後。透過將具有充足變異的足夠範例載入至 Watson {{site.data.keyword.discoveryshort}}，即可教導它何謂「良好」文件。在此步驟中，我們將使用 {{site.data.keyword.retrieveandrankshort}} 中所使用的現有 Cranfield「基準」，來訓練 Watson {{site.data.keyword.discoveryshort}}。

1.  如果您尚未這樣做，請從 {{site.data.keyword.retrieveandrankshort}} 指導教學下載範例 [Cranfield 基準 csv 檔案 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-gt.csv){: new_window}。

   該檔案是使用者可能會詢問的一組關於文件的問題。該檔案提供範例資訊，用來在 {{site.data.keyword.discoveryshort}} 中訓練分級者，並在 {{site.data.keyword.retrieveandrankshort}} 中進行關於問題和相關回答的相關性訓練。

   對於每一個問題，回答至少有一個 ID（文件 ID）。每個文件 ID 都包含一個數字，指出回答與問題的相關程度。文件 ID 指向您在前一個步驟中上傳至 {{site.data.keyword.discoveryshort}} 之 `cranfield-data.json` 檔案的回答。

1.  下載「訓練資料上傳 Script」。您將使用此 Script 將訓練資料上傳至 {{site.data.keyword.discoveryshort}}。此 Script 會將 `csv` 檔案轉換成一組 JSON 查詢和範例，並使用[訓練資料 API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#training-data){: new_window}，將它們傳送至 {{site.data.keyword.discoveryshort}} 服務
**附註：**{{site.data.keyword.discoveryshort}} 在該服務內管理訓練資料，因此當產生新的範例和訓練查詢時，它們可以儲存在 {{site.data.keyword.discoveryshort}} 本身，而不是作為需要維護之個別 CSV 檔案的一部分。
1.  執行「訓練上傳 Script」，將訓練資料上傳至 {{site.data.keyword.discoveryshort}}。將 `{apikey_value}`、`{path_to_file}`、`{environment_id}`、`{collection_id}` 取代為您的資訊。請注意，還有其他選項，`-d` 代表除錯，而 `–v` 代表 curl 的詳細輸出。

    ```bash
    python ./disco-train.py -u apikey:{apikey_value} -i {path_to_file}/cranfield-gt.csv –e {environment_id} -c {collection_id}
    ```
    {: pre}

1.  一旦載入資料之後，您就可以使用在上一節所看到的集合詳細資料指令，來檢查訓練的狀態。{{site.data.keyword.discoveryshort}} 會每小時檢查一次，以查看是否有任何新資料，如果有，就會開始處理它，並將它轉換成機器學習模型。當模型在訓練時，您會看到訓練區段的狀態從 `"processing": false` 變更為 `"processing": true`。當模型訓練完成後，您會看到訓練區段的狀態從 `"available": false` 變更為 `"available": true`。您也會看到 `"successfully_trained"` 值的日期變更。如果有任何錯誤，您可以查看**通知 API** 來檢視它們，如上一節所述。

## 搜尋文件
{: search}

{{site.data.keyword.discoveryshort}} 服務會自動使用訓練過的模型將搜尋結果重新分級（如果有的話）。如果是使用 `natural_language_query` 而非 `query` 來發出 [API 呼叫 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection){: new_window}，則會檢查是否有可用的模型。如果有可用的模型，則 {{site.data.keyword.discoveryshort}} 會使用該模型將結果重新分級。首先，我們將搜尋未分級的文件，然後將使用分級模型來執行搜尋。

1.  您可以使用 cURL 指令，在集合中搜尋文件。使用查詢 API 呼叫來執行查詢，以查看未分級的結果。將 `{apikey_value}`、`{environment_id}`、`{collection_id}` 取代為您的資訊。傳回的結果將是未分級的結果，並將使用預設的 {{site.data.keyword.discoveryshort}} 分級公式。您可以開啟訓練資料 `csv` 檔案，並將第一個直欄的值複製到查詢參數中，來嘗試其他查詢。

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query=what is the basic mechanism of the transonic aileron buzz"
    ```
    {: pre}

1.  現在，透過設定 `natural_language_query` 參數，來使用模型執行搜尋。在這麼做之前，請務必先檢查您是否有訓練過的模型，如前一節所述。在主控台貼上下列程式碼，並將 `{apikey_value}`、`{environment_id}`、`{collection_id}` 取代為您的值。

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&natural_language_query=what is the basic mechanism of the transonic aileron buzz"
    ```
    {: pre}

    此指令將使用您先前所訓練的模型，傳回重新分級的結果。比較此搜尋的結果以及您先前嘗試的一些其他搜尋的結果。相較於您在 {{site.data.keyword.retrieveandrankshort}} 中看到的內容，您可能會看到結果有一些差異。這是由於為了簡化體驗及改善結果，已變更某些用於搜尋的技術，但整體而言，結果的品質很類似。

在評估重新分級的搜尋結果之後，您可以使用其他的訓練查詢和範例來重複上傳訓練資料的步驟，並檢視搜尋結果，如此即可在 {{site.data.keyword.discoveryshort}} 中精簡這些搜尋結果。您也可以依照第一個步驟的說明來新增文件，以擴大搜尋範圍。與 {{site.data.keyword.retrieveandrankshort}} 類似，利用訓練改善結果是一種反覆運算的過程。
