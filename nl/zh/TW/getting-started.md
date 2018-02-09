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
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}

# 開始使用 API

在這個簡短的指導教學中，我們將介紹 {{site.data.keyword.discoveryshort}} API，並逐步完成建立及搜尋專用資料集合的處理程序。
{: shortdesc}

## 開始之前
{: #before-you-begin}

- 建立服務的實例：
    - {: download} 如果您看到了這一項，表示您已建立服務實例。現在要取得您的認證。
    - 從服務中建立專案：
        1.  移至 {{site.data.keyword.watson}} Developer Console [服務 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.{DomainName}/developer/watson/services){: new_window} 頁面。
        1.  選取 {{site.data.keyword.discoveryshort}}，按一下**新增服務**，然後註冊免費 {{site.data.keyword.Bluemix_notm}} 帳戶或登入。
        1.  鍵入 `discovery-tutorial` 作為專案名稱，然後按一下**建立專案**。
- 複製認證以鑑別您的服務實例：
    - {: download} 從服務儀表板（如您目前所見）：
        1.  按一下**服務認證**標籤。
        1.  按一下**動作**下的**檢視認證**。
        1.  複製 `username`、`password` 及 `url` 值。
        {: download}
    - 在 Developer Console 的 **discovery-tutorial** 專案中，從**認證**區段複製 `"discovery"` 的 `username`、`password` 及 `url` 值。

<!-- Remove this text after dedicated instances have the Developer Console: begin -->

如果您使用 {{site.data.keyword.Bluemix_dedicated_notm}}，請從「型錄」的 [{{site.data.keyword.discoveryshort}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.{DomainName}/catalog/services/discovery/){: new_window} 頁面建立服務實例。如需如何尋找服務認證的詳細資料，請參閱 [Watson 服務的服務認證 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/watson/getting-started-credentials.html#getting-credentials-manually){: new_window}。

<!-- Remove this text after dedicated instances have the Developer Console: end -->

## 步驟 1：建立環境
{: #create-an-environment}

在 Bash Shell 或同等環境（例如 Cygwin）中，使用 `POST /v1/environments` 方法來建立環境。請將環境視為要儲存所有文件箱的倉儲。

1.  發出下列指令，以建立一個稱為 `my-first-environment` 的環境。將 `{username}` 和 `{password}` 取代為您先前複製的服務認證：

    ```bash
    curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    API 會傳回諸如環境 ID、環境狀態以及環境使用的儲存體數量等資訊。

1.  定期檢查環境狀態，直到看到 `ready` 狀態為止。
    - 對 `GET /v1/environments/{environment_id}` 方法發出呼叫，以擷取環境的狀態。將 `{username}`、`{password}` 及 `{environment_id}` 取代為您的資訊：

    ```bash
    curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}?version=2017-11-07
    ```
    {: pre}

    狀態必須是 `ready`，您才能建立集合。

## 步驟 2：建立集合
{: #create-a-collection}

由於環境已備妥，您便可以建立集合。請將集合視為儲存您環境中文件的箱子。

1.  首先您需要預設配置的 ID。若要尋找預設的 `configuration_id`，請使用 `GET /v1/environments/{environment_id}/configurations` 方法。將 `{username}`、`{password}` 及 `{environment_id}` 取代為您的資訊：

    ```bash
      curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07
    ```
    {: pre}
1.  使用 `POST /v1/environments/{environment_id}/collections` 方法來建立稱為 **my-first-collection** 的集合。將 `{username}`、`{password}`、`{environment_id}` 及 `{configuration_id}` 取代為您的資訊：

    ```bash
    curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{configuration_id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07
    ```
    {: pre}

    API 會傳回諸如集合 ID、集合狀態以及集合使用的儲存體數量等資訊。
1.  定期檢查集合狀態，直到看到 `online` 狀態為止。
    - 對 `GET /v1/environments/{environment_id}/collections/{collection_id}` 方法發出呼叫，以擷取集合的狀態。同樣地，將 `{username}`、`{password}`、`{environment_id}` 及 `{configuration_id}` 取代為您的資訊：

    ```bash
    curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07
    ```
    {: pre}

## 步驟 3：下載範例文件
{: #download-sample-documents}

下載這些範例文件：<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示" title="外部鏈結圖示" class="style-scope doc-content"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示" title="外部鏈結圖示" class="style-scope doc-content"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示" title="外部鏈結圖示" class="style-scope doc-content"></a> 及 <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示" title="外部鏈結圖示" class="style-scope doc-content"></a>。

## 步驟 4：上傳文件
{: #upload-the-documents}

1.  現在，將範例文件新增至集合中。此範例會將文件 **test-doc1.html** 上傳至您的集合。將 `{username}`、`{password}`、`{environment_id}` 及 `{configuration_id}` 取代為您的資訊。修改範例文件的位置，以指向您儲存 `test-doc1.html` 檔案的位置。
    - 使用 `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` 方法：

        ```bash
        curl -X POST -u "{username}":"{password}" -F "file=@test-doc1.html" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2017-11-07
        ```
        {: pre}

    或者，使用 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window} 所列出的其中一個 SDK：
    - Java：

      ```java
      Discovery discovery = new Discovery("2017-11-07");
      discovery.setEndPoint("https://gateway.watsonplatform.net/discovery/api/v1");
      discovery.setUsernameAndPassword("{username}", "{password}");
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
        username="{username}",
        password="{password}",
        version="2017-11-07"
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
        username: '{username}',
        password: '{password}',
        version_date: '2017-11-07'
      });

      var file = fs.readFileSync('{/path/to/file}');

      discovery.addDocument(('{environment_id}', '{collection_id}', file),
      function(error, data) {
        console.log(JSON.stringify(data, null, 2));
        }
      );
      ```
      {: codeblock}

1.  針對其他三個範例檔案的每一個檔案重複此處理程序。

## 步驟 5：查詢集合
{: #query-your-collection}

最後，請使用 `GET /v1/environments/{environment_id}/collections/{collection_id}/query` 方法來搜尋您的文件集合。

下列範例會傳回所有稱為 **IBM** 的實體。將 `{username}`、`{password}`、`{environment_id}` 及 `{configuration_id}` 取代為您的資訊：

```bash
curl -u "{username}":"{password}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}*/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

## 後續步驟
{: #next-steps}

您已在所建立的環境和集合中順利查詢文件。您現在可以開始自訂集合，方法是新增更多文件和強化，以及自訂轉換設定。如需 API 的相關資訊，請參閱 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}。
