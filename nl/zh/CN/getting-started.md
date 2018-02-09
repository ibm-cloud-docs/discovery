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

# API 入门

在此简短教程中，我们将介绍 {{site.data.keyword.discoveryshort}} API，然后完成创建专用数据集合并对其进行搜索的过程。
{: shortdesc}

## 开始之前
{: #before-you-begin}

- 创建服务的实例：
    - {: download} 如果您看到此信息，说明您已创建服务实例。现在，请获取凭证。
    - 通过服务创建项目：
        1.  转至 {{site.data.keyword.watson}} 开发者控制台[服务 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.{DomainName}/developer/watson/services){: new_window} 页面。
        1.  选择 {{site.data.keyword.discoveryshort}}，单击**添加服务**，然后注册免费 {{site.data.keyword.Bluemix_notm}} 帐户或登录。
        1.  输入 `discovery-tutorial` 作为项目名称，然后单击**创建项目**。
- 复制凭证以向服务实例进行认证：
    - {: download} 在服务仪表板（您正在查看的内容）中：
        1.  单击**服务凭证**选项卡。
        1.  单击**操作**下的**查看凭证**。
        1.  复制 `username`、`password` 和 `url` 值。
        {: download}
    - 在开发者控制台的 **discovery-tutorial** 项目中，复制**凭证**部分中 `"discovery"` 的 `username`、`password` 和 `url` 值。

<!-- Remove this text after dedicated instances have the Developer Console: begin -->

如果使用的是 {{site.data.keyword.Bluemix_dedicated_notm}}，请在“目录”的 [{{site.data.keyword.discoveryshort}} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.{DomainName}/catalog/services/discovery/){: new_window} 页面中创建服务实例。有关如何找到服务凭证的详细信息，请参阅 [Watson 服务的服务凭证 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](/docs/services/watson/getting-started-credentials.html#getting-credentials-manually){: new_window}。

<!-- Remove this text after dedicated instances have the Developer Console: end -->

## 步骤 1：创建环境
{: #create-an-environment}

在 bash shell 或等效环境（例如，Cygwin）中，使用 `POST /v1/environments` 方法来创建环境。将环境视为用于存储所有文档箱的仓库。

1.  发出以下命令以创建名为 `my-first-environment` 的环境。将 `{username}` 和 `{password}` 替换为早先复制的服务凭证：

    ```bash
    curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    此 API 将返回环境标识、环境状态以及环境正在使用的存储量等信息。

1.  定期检查环境状态，直到看到状态为 `ready` 为止。
    - 发出对 `GET /v1/environments/{environment_id}` 方法的调用以检索环境的状态。将 `{username}`、`{password}` 和 `{environment_id}` 替换为您的信息：

    ```bash
    curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}?version=2017-11-07
    ```
    {: pre}

    状态必须为 `ready` 后，才能创建集合。

## 步骤 2：创建集合
{: #create-a-collection}

现在环境已就绪，可以创建集合。将集合视为将在环境中存储文档的箱子。

1.  您首先需要缺省配置的标识。要查找缺省 `configuration_id`，请使用 `GET /v1/environments/{environment_id}/configurations` 方法。将 `{username}`、`{password}` 和 `{environment_id}` 替换为您的信息：

    ```bash
      curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07
    ```
    {: pre}
1.  使用 `POST /v1/environments/{environment_id}/collections` 方法来创建名为 **my-first-collection** 的集合。将 `{username}`、`{password}`、`{environment_id}` 和 `{configuration_id}` 替换为您的信息：

    ```bash
    curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{configuration_id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07
    ```
    {: pre}

    此 API 将返回集合标识、集合状态以及集合正在使用的存储量等信息。
1.  定期检查集合状态，直到看到状态为 `online` 为止。
    - 发出对 `GET /v1/environments/{environment_id}/collections/{collection_id}` 方法的调用以检索集合的状态。同样，将 `{username}`、`{password}`、`{environment_id}` 和 `{configuration_id}` 替换为您的信息：

    ```bash
    curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07
    ```
    {: pre}

## 步骤 3：下载样本文档
{: #download-sample-documents}

下载以下样本文档：<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标" class="style-scope doc-content"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标" class="style-scope doc-content"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标" class="style-scope doc-content"></a> 和 <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标" class="style-scope doc-content"></a>。

## 步骤 4：上传文档
{: #upload-the-documents}

1.  现在，将示例文档添加到集合。此示例将 **test-doc1.html** 文档上传到您的集合。将 `{username}`、`{password}`、`{environment_id}` 和 `{configuration_id}` 替换为您的信息。将样本文档的位置修改为指向保存 `test-doc1.html` 文件的位置。
    - 使用 `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` 方法：

        ```bash
        curl -X POST -u "{username}":"{password}" -F "file=@test-doc1.html" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2017-11-07
        ```
        {: pre}

    或者，使用 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window} 中列出的其中一个 SDK：
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

1.  对其他 3 个样本文件分别重复此过程。

## 步骤 5：查询集合
{: #query-your-collection}

最后，使用 `GET /v1/environments/{environment_id}/collections/{collection_id}/query` 方法来搜索文档集合。

以下示例返回名为 **IBM** 的所有实体。将 `{username}`、`{password}`、`{environment_id}` 和 `{configuration_id}` 替换为您的信息：

```bash
curl -u "{username}":"{password}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}*/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

## 后续步骤
{: #next-steps}

您已成功在所创建的环境和集合中查询了文档。现在，可以开始通过添加更多文档和扩充项以及定制转换设置来定制集合。有关该 API 的更多信息，请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}。
