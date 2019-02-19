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

# API 入门
{: #gs-api}

在此简短教程中，我们将介绍 {{site.data.keyword.discoveryshort}} API，然后完成创建专用数据集合并对其进行搜索的过程。
{: shortdesc}

如果您倾向于使用 {{site.data.keyword.discoveryshort}} 工具，请参阅[入门](/docs/services/discovery/getting-started-tool.html)。
{: tip}

## 开始之前
{: #before-you-begin}

- 创建服务的实例：
    1.  转至 {{site.data.keyword.Bluemix_notm}}“目录”中的 [{{site.data.keyword.discoveryshort}} 页面 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.{DomainName}/catalog/services/discovery){: new_window}。
    1.  注册免费的 {{site.data.keyword.Bluemix_notm}} 帐户或登录。
    1.  单击**创建**。
- 复制凭证以向服务实例进行认证：
    1. 在 [{{site.data.keyword.Bluemix_notm}} 仪表板](https://console.{DomainName}/dashboard/apps)中，单击 {{site.data.keyword.discoveryshort}} 服务实例以转至 {{site.data.keyword.discoveryshort}} 服务仪表板页面。
    1.  在**管理**页面上，单击**显示**以查看凭证。
    1.  复制 `apikey` 和 `url` 值。

    在某些情况下，您可通过提供基本认证来进行认证。如果在凭证中看到 `username` 和 `password`，请使用这些值，而不要使用本教程的示例中的 `"apikey":"{apikey_value}"`。
{: tip}

## 步骤 1：创建环境
{: #create-an-environment}

在 bash shell 或等效环境（例如，安装了 `curl` 应用程序的 Cygwin）中，使用 `POST /v1/environments` 方法来创建环境。将环境视为用于存储所有文档箱的仓库。

本教程使用 API 密钥进行认证。对于生产用途，请确保查看 API 密钥[最佳实践](/docs/services/watson/apikey-bp.html#api-bp)。
{: tip}

1.  发出以下命令以创建名为 `my-first-environment` 的环境。将 `{apikey_value}` 替换为先前复制的 API 密钥：

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    此 API 将返回环境标识、环境状态以及环境正在使用的存储量等信息。

1.  定期检查环境状态，直到看到状态为 `active`。
    - 发出对 `GET /v1/environments/{environment_id}` 方法的调用以检索环境的状态。将 `{apikey_value}` 和 `{environment_id}` 替换为您的信息：

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}?version=2017-11-07"
    ```
    {: pre}

    状态必须为 `active` 后，才能创建集合。

## 步骤 2：创建集合
{: #create-a-collection}

现在环境已就绪，可以创建集合。将集合视为将在环境中存储文档的箱子。

1.  您首先需要缺省配置的标识。要查找缺省 `configuration_id`，请使用 `GET /v1/environments/{environment_id}/configurations` 方法。将 `{apikey_value}` 和 `{environment_id}` 替换为您的信息：

    ```bash
      curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07
    ```
    {: pre}
1.  使用 `POST /v1/environments/{environment_id}/collections` 方法来创建名为 **my-first-collection** 的集合。将 `{apikey_value}`、`{environment_id}` 和 `{configuration_id}` 替换为您的信息：

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{configuration_id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07
    ```
    {: pre}

    此 API 将返回集合标识、集合状态以及集合正在使用的存储量等信息。
1.  定期检查集合状态，直到看到状态为 `active`。
    - 发出对 `GET /v1/environments/{environment_id}/collections/{collection_id}` 方法的调用以检索集合的状态。同样将 `{apikey_value}`、`{environment_id}` 和 `{configuration_id}` 替换为您的信息：

    ```bash
    curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07
    ```
    {: pre}

## 步骤 3：下载样本文档
{: #download-sample-documents}

下载以下样本文档：<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标" class="style-scope doc-content"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标" class="style-scope doc-content"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标" class="style-scope doc-content"></a> 和 <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标" class="style-scope doc-content"></a>。

**注：**在某些浏览器中，先前的链接将在新窗口中打开，而不是在本地保存。如果发生这种情况，请选择浏览器的`文件`菜单中的`另存为`，以保存该文件的副本。

## 步骤 4：上传文档
{: #upload-the-documents}

1.  现在，将示例文档添加到集合。此示例将 **test-doc1.html** 文档上传到您的集合。将 `{apikey_value}`、`{environment_id}` 和 `{configuration_id}` 替换为您的信息。将样本文档的位置修改为指向保存 `test-doc1.html` 文件的位置。
    - 使用 `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` 方法：

        ```bash
        curl -X POST -u "apikey":"{apikey_value}" -F "file=@test-doc1.html" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2017-11-07
        ```
        {: pre}

    或者，使用 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window} 中列出的其中一个 SDK：
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

1.  对其他 3 个样本文件分别重复此过程。

## 步骤 5：查询集合
{: #query-your-collection}

最后，使用 `GET /v1/environments/{environment_id}/collections/{collection_id}/query` 方法来搜索文档集合。

以下示例返回名为 **IBM** 的所有实体。将 `{apikey_value}`、`{environment_id}` 和 `{configuration_id}` 替换为您的信息：

```bash
curl -u "apikey":"{apikey_value}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

## 后续步骤
{: #next-steps}

您已成功在所创建的环境和集合中查询了文档。现在，可以开始通过添加更多文档和扩充项以及定制转换设置来定制集合。

- 请阅读 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window} 中有关 API 的内容。
- [配置](/docs/services/discovery/building.html)服务
- 了解[使用 IAM 进行认证](/docs/services/watson/getting-started-iam.html)
