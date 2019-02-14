---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}

# 開始使用 API
{: #gs-api}

在這個簡短的指導教學中，我們將介紹 {{site.data.keyword.discoveryshort}} API，並逐步完成建立及搜尋專用資料集合的處理程序。
{: shortdesc}

如果您偏好在 {{site.data.keyword.discoveryshort}} 工具中工作，請參閱[開始使用](/docs/services/discovery/getting-started-tool.html)。
{: tip}

## 開始之前
{: #before-you-begin}

- 建立服務的實例：
    1.  移至「{{site.data.keyword.Bluemix_notm}} 型錄」中的 [{{site.data.keyword.discoveryshort}} 頁面 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.{DomainName}/catalog/services/discovery){: new_window}。
    1.  註冊免費的 {{site.data.keyword.Bluemix_notm}} 帳戶或登入。
    1.  按一下**建立**。
- 複製認證以向服務實例進行鑑別：
    1. 從 [{{site.data.keyword.Bluemix_notm}} 儀表板](https://console.{DomainName}/dashboard/apps)，按一下 {{site.data.keyword.discoveryshort}} 服務實例，以移至 {{site.data.keyword.discoveryshort}} 服務儀表板頁面。
    1.  在**管理**頁面上，按一下**顯示**以檢視您的認證。
    1.  複製 `apikey` 和 `url` 值。

    在某些情況下，您可以透過提供基本鑑別來進行鑑別。如果您在認證中看到 `username` 和 `password`，請使用那些值，而不要使用本指導教學範例中的 `"apikey":"{apikey_value}"`。
{: tip}

## 步驟 1：建立環境
{: #create-an-environment}

在已安裝 `curl` 應用程式的 Bash Shell 或相等環境中（例如 Cygwin），請使用 `POST /v1/environments` 方法來建立環境。請將環境視為要儲存所有文件箱的倉儲。

本指導教學使用 API 金鑰來進行鑑別。若為正式作業用途，請務必檢閱 API 金鑰的[最佳作法](/docs/services/watson/apikey-bp.html#api-bp)。
{: tip}

1.  發出下列指令，以建立一個稱為 `my-first-environment` 的環境。將 `{apikey_value}` 取代為您先前複製的 API 金鑰：

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    API 會傳回諸如環境 ID、環境狀態以及環境所使用儲存空間量等資訊。

1.  定期檢查環境狀態，直到看到 `active` 狀態為止。
    - 對 `GET /v1/environments/{environment_id}` 方法發出呼叫，以擷取環境的狀態。將 `{apikey_value}` 和 `{environment_id}` 取代為您的資訊：

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}?version=2017-11-07"
    ```
    {: pre}

    狀態必須是 `active`，您才能建立集合。

## 步驟 2：建立集合
{: #create-a-collection}

由於環境已備妥，您可以建立集合。請將集合視為您用來儲存環境中文件的箱子。

1.  首先您需要預設配置的 ID。若要尋找預設的 `configuration_id`，請使用 `GET /v1/environments/{environment_id}/configurations` 方法。將 `{apikey_value}` 和 `{environment_id}` 取代為您的資訊：

    ```bash
      curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07
    ```
    {: pre}
1.  使用 `POST /v1/environments/{environment_id}/collections` 方法來建立稱為 **my-first-collection** 的集合。將 `{apikey_value}`、`{environment_id}` 及 `{configuration_id}` 取代為您的資訊：

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{configuration_id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07
    ```
    {: pre}

    API 會傳回諸如集合 ID、集合狀態以及集合所使用儲存空間量等資訊。
1.  定期檢查集合狀態，直到看到 `active` 狀態為止。
    - 對 `GET /v1/environments/{environment_id}/collections/{collection_id}` 方法發出呼叫，以擷取集合的狀態。同樣地，將 `{apikey_value}`、`{environment_id}` 及 `{configuration_id}` 取代為您的資訊：

    ```bash
    curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07
    ```
    {: pre}

## 步驟 3：下載範例文件
{: #download-sample-documents}

下載這些範例文件：<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示" title="外部鏈結圖示" class="style-scope doc-content"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示" title="外部鏈結圖示" class="style-scope doc-content"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示" title="外部鏈結圖示" class="style-scope doc-content"></a> 及 <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示" title="外部鏈結圖示" class="style-scope doc-content"></a>。

**附註：**在某些瀏覽器中，之前的鏈結會在新視窗中開啟，而不是儲存在本端。如果發生此情況，請在瀏覽器的`檔案`功能表中選取`另存新檔`，以儲存檔案的副本。

## 步驟 4：上傳文件
{: #upload-the-documents}

1.  現在，將範例文件新增至集合中。此範例會將文件 **test-doc1.html** 上傳至您的集合。將 `{apikey_value}`、`{environment_id}` 及 `{configuration_id}` 取代為您的資訊。修改範例文件的位置，以指向您儲存 `test-doc1.html` 檔案的位置。
    - 使用 `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` 方法：

        ```bash
        curl -X POST -u "apikey":"{apikey_value}" -F "file=@test-doc1.html" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2017-11-07
        ```
        {: pre}

    或者，使用 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window} 所列出的其中一個 SDK：
    - Java：

      ```java
      Discovery discovery = new Discovery("2017-11-07");
      discovery.setEndPoint("https://gateway.watsonplatform.net/discovery/api/v1");
      IamOptions options = new IamOptions.Builder()
        .apiKey("{apikey_value}")
        .build();
      discovery.setIamCredentials(options);
      String environmentId = "{environment_id}";
      String collectionId = "{collection_id}";
      String documentJson = "{\"field\":\"value\"}";
      InputStream documentStream = new ByteArrayInputStream(documentJson.getBytes());

      CreateDocumentRequest.Builder builder = new CreateDocumentRequest.Builder(environmentId, collectionId);
      builder.inputStream(documentStream, HttpMediaType.APPLICATION_JSON);
      CreateDocumentResponse createResponse = discovery.createDocument(builder.build()).execute();
      ```
      {: codeblock}

    - Python：

      ```python
      import sys
      import os
      import json
      from watson_developer_cloud import DiscoveryV1

      

      discovery = DiscoveryV1(
        version='2017-11-07',
        api_key='{apikey_value}'
      )

      with open((os.path.join(os.getcwd(), '{path_element}', '{filename}' as fileinfo:
        add_doc = discovery.add_document('{environment_id}', '{collection_id}', file_info=fileinfo)
      print(json.dumps(add_doc, indent=2))
      ```
      {: codeblock}

    - Node.js：

      ```javascript
      var DiscoveryV1 = require('watson-developer-cloud/discovery/v1');
      var fs = require('fs');

      

      var discovery = new DiscoveryV1({
        version_date: '2017-11-07',
        iam_apikey: '{apikey_value}',
      });

      var file = fs.readFileSync('{/path/to/file}');

      

      discovery.addDocument({ environment_id: '{environment_id}', collection_id: '{collection_id}', file: file },
      function(error, data) {
        console.log(JSON.stringify(data, null, 2));
        }
      );
      ```
      {: codeblock}

1.  針對其他三個範例檔案的每一個檔案，重複此處理程序。

## 步驟 5：查詢集合
{: #query-your-collection}

最後，請使用 `GET /v1/environments/{environment_id}/collections/{collection_id}/query` 方法來搜尋您的文件集合。

下列範例會傳回所有稱為 **IBM** 的實體。將 `{apikey_value}`、`{environment_id}` 及 `{configuration_id}` 取代為您的資訊：

```bash
curl -u "apikey":"{apikey_value}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

## 後續步驟
{: #next-steps}

您已在所建立的環境和集合中順利查詢文件。您現在可以藉由新增更多文件和強化，以及自訂轉換設定，開始自訂集合。

- 請閱讀 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window} 中關於 API 的資訊
- [配置](/docs/services/discovery/building.html)服務
- 瞭解[使用 IAM 進行鑑別](/docs/services/watson/getting-started-iam.html)
