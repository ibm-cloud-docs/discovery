---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-09"

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


# 教程：从 Retrieve and Rank 迁移
{: #migrate-rnr}

从 {{site.data.keyword.retrieveandrankshort}} 迁移到 {{site.data.keyword.discoveryfull}} 服务。这是《Cranfield 入门教程》的附加部分。

## 概述
{: #overview-rnr}

本教程将逐步指导您完成使用样本数据创建和训练 {{site.data.keyword.discoveryfull}} 服务的过程。本教程使用的数据集与 [{{site.data.keyword.retrieveandrankshort}} 入门教程](/docs/services/retrieve-and-rank/getting-started.html)中所用的相同，但您也可以使用相同的方法来创建使用您自己数据的服务实例。

对于将数据从 {{site.data.keyword.retrieveandrankshort}} 迁移到 {{site.data.keyword.discoveryshort}} 的用户，此过程由两个主要步骤组成。

1. 迁移集合数据。
2. 迁移训练数据。

迁移已训练的集合数据时，**最**重要的是_使文档标识保持一致_。这是因为训练数据会使用这些标识来引用参考标准。如果在将标识从 {{site.data.keyword.retrieveandrankshort}} 移至 {{site.data.keyword.discoveryshort}} 时更改了标识，那么重新排名会被完全打乱（或者训练甚至可能无法启动）。{{site.data.keyword.discoveryshort}} 支持在 API 上传过程中指定文档标识，因此通过遵循本文档中的准则可避免此问题。{{site.data.keyword.retrieveandrankshort}} 训练数据通常存储在 `csv` 文件中。在本教程中，此 `csv` 文件用于将样本训练数据上传到 {{site.data.keyword.discoveryshort}}。在[从服务迁移训练数据](/docs/services/discovery?topic=discovery-migrate-dcs-rr#extract-train)中详细描述了如何迁移从 {{site.data.keyword.retrieveandrankshort}} 工具中导出的训练数据。

本教程假定 {{site.data.keyword.retrieveandrankshort}} 的设置与 [{{site.data.keyword.retrieveandrankshort}} 入门教程](/docs/services/retrieve-and-rank/getting-started.html)的类似，并使用[此处](/docs/services/discovery?topic=discovery-migrate-dcs-rr#source)描述的“从源迁移”路径。请参阅[评估指向 Watson Discovery 服务的迁移路径](/docs/services/discovery?topic=discovery-migrate-dcs-rr#evaluate)，以获取有关其他迁移选项的信息。

要完成本教程，您需要满足以下条件：

-  **cURL**。可以从 [haxx.se ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://curl.haxx.se/){: new_window} 安装适用于您操作系统的 cURL 版本。必须安装支持安全套接字层 (SSL) 协议的版本。确保在 PATH 环境变量中包含安装的二进制文件。
-  样本 Cranfield 数据。本教程使用《{{site.data.keyword.retrieveandrankshort}} 入门教程》中的样本集合数据。[Cranfield JSON 数据 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-data.json){: new_window}
-  **样本数据参考标准**。本教程使用《{{site.data.keyword.retrieveandrankshort}} 入门教程》中的样本 Cranfield 参考标准。[Cranfield 参考标准 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-gt.csv){: new_window}
-  **Python V2**。要检查是否已安装 Python，请在命令提示符处输入 `python --version`，并确保版本号以 2 开头。如果需要安装 Python，请参阅[下载 Python ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://wiki.python.org/moin/BeginnersGuide/Download){: new_window}。
-  “数据上传”脚本：[Discovery 文档上传程序 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-upload.py){: new_window}
-  “训练数据上传”脚本：[Discovery 训练上传程序 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-train.py){: new_window}

开始本教程之前，必须满足以下先决条件：

-  本教程假定您已创建 {{site.data.keyword.discoveryshort}} 实例，如果需要有关如何创建 {{site.data.keyword.discoveryshort}} 实例的指导信息，请参阅[以下教程](/docs/services/discovery?topic=discovery-gs-api#gs-api)。

-  本教程假定您具有服务凭证。
   -  在 {{site.data.keyword.Bluemix_notm}} 上的 Watson {{site.data.keyword.discoveryshort}} 服务中，单击**服务凭证**。
   -  单击“操作”下的**查看凭证**。
   -  复制 `apikey` 值，并确保 `url` 值与以下示例中的 url 值相匹配，如果不匹配，也要进行替换。

## 向 Discovery 添加 Cranfield 数据
{: #cranfield-rnr}

1.  创建环境。

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{ "name": "my_environment", "description": "My environment" }' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    复制返回的 JSON 中列出的 `environment-id`。

1. 创建集合。

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{ "name": "test_collection", "description": "My test collection", "configuration_id": "{configuration_id}", "language_code": "en" }' "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07"
    ```
    {: pre}

    复制返回的 JSON 中列出的 `collection-id`。

1.  添加要搜索的文档。
    1.  如果尚未下载 [cranfield-data.json ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-data.json){: new_window} 文件，请进行下载。这是 {{site.data.keyword.retrieveandrankshort}} 中所用文档的源。Cranfield 集合文档采用 JSON 格式，这是 {{site.data.keyword.retrieveandrankshort}} 接受的格式，也适用于 Watson {{site.data.keyword.discoveryshort}}。
        **注：**{{site.data.keyword.discoveryshort}} 无需上传 Solr 模式。这是因为 {{site.data.keyword.discoveryshort}} 会自动从 JSON 结构推断模式。
    1.  在[此处 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-upload.py){: new_window} 下载“数据上传”脚本。此脚本用于将 Cranfield JSON 上传到 {{site.data.keyword.discoveryshort}}。此脚本会读取整个 JSON 文件，并使用 {{site.data.keyword.discoveryshort}} 中的缺省配置将每个单独的 JSON 文档发送到 {{site.data.keyword.discoveryshort}} 服务。
        **注：**{{site.data.keyword.discoveryshort}} 中缺省配置提供的设置与 {{site.data.keyword.retrieveandrankshort}} 中的缺省 Solr 配置类似。
    1.  发出以下命令以将 `cranfield-data-json` 数据上传到 `cranfield_collection` 集合。将 `{apikey_value}`、`{path_to_file}`、`{environment_id}` 和 `{collection_id}` 替换为您的信息。请注意，还有其他选项，-d 表示调试，-v 表示来自 curl 的详细输出。

        ```bash
        python ./disco-upload.py -u apikey:{apikey_value} -i {path_to_file}/cranfield-data.json -e {environment_id} -c {collection_id}
        ```
        {: pre}

1.  上传过程完成后，即可以通过发出以下命令来查看集合详细信息，从而检查文档是否已就位：

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07"
    ```
    {: pre}

    输出将如下所示：

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

查看 `document_counts` 部分以确定成功上传的文档数。我们预计使用此样本数据集不会发生任何文档失败。但是，对于其他数据集，您可能会看到失败的文档计数。如果有任何失败的文档计数，可以查看“通知 API”以了解错误消息。请在[此处 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/discovery#query-system-notices){: new_window} 查看该部分，以查看“通知 API”命令。

返回的 `training` 部分提供了有关训练的信息。上传您的训练数据后，我们将复查该部分。

## 向 Discovery 添加训练数据
{: #trainingdata-rnr}

Watson {{site.data.keyword.discoveryshort}} 服务使用机器学习模型对文档进行重新排名。为此，您需要对模型进行训练。在装入足够的查询以及相应的已评级文档后，即会执行训练。通过将具有足够差异的足够示例装入到 Watson {{site.data.keyword.discoveryshort}}，可以教会它什么是“良好”文档。在此步骤中，我们将使用在 {{site.data.keyword.retrieveandrankshort}} 中所用的现有 Cranfield“参考标准”来训练 Watson {{site.data.keyword.discoveryshort}}。

1.  如果尚未通过 {{site.data.keyword.retrieveandrankshort}} 教程下载样本 [Cranfield 参考标准 csv 文件 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-gt.csv){: new_window}，请进行下载。

   该文件是用户可能询问的一组文档相关问题。该文件提供的示例信息用于训练 {{site.data.keyword.retrieveandrankshort}} 中的排名器以及在 {{site.data.keyword.discoveryshort}} 中执行有关问题和相关答案的相关性训练。

   对于每个问题，至少有一个答案标识（文档标识）。每个文档标识都包含一个数字，用于指示答案与问题的相关程度。文档标识指向在先前步骤中上传到 {{site.data.keyword.discoveryshort}} 的 `cranfield-data.json` 文件中的答案。

1.  下载“训练数据上传”脚本。您将使用此脚本来将训练数据上传到 {{site.data.keyword.discoveryshort}}。此脚本将 `csv` 文件变换为一组 JSON 查询和示例，然后使用[训练数据 API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/discovery#list-training-data){: new_window} 将这些内容发送到 {{site.data.keyword.discoveryshort}} 服务。
    **注：**{{site.data.keyword.discoveryshort}} 可管理服务内的训练数据，因此，生成新的示例和训练查询时，可以将其存储在 {{site.data.keyword.discoveryshort}} 本身中，而不是存储为需要维护的单独 CSV 文件的一部分。
1.  执行训练上传脚本，以将训练数据上传到 {{site.data.keyword.discoveryshort}}。将 `{apikey_value}`、`{path_to_file}`、`{environment_id}` 和 `{collection_id}` 替换为您的信息。请注意，还有其他选项，`-d` 表示调试，`-v` 表示来自 curl 的详细输出。

    ```bash
    python ./disco-train.py -u apikey:{apikey_value} -i {path_to_file}/cranfield-gt.csv –e {environment_id} -c {collection_id}
    ```
    {: pre}

1.  装入数据后，即可以使用在上一部分中看到的集合详细信息命令来检查训练的状态。{{site.data.keyword.discoveryshort}} 将按大致每小时一次的频率进行检查，以查看是否有任何新数据，如果有，将开始处理这些数据，并将其转换为机器学习模型。正在训练模型时，您将看到 training 部分的状态从 `"processing": false` 更改为 `"processing": true`。模型经过训练后，您将看到 training 部分中的状态从 `"available": false` 更改为 `"available": true`。此外，您还将看到值 `"successfully_trained"` 的日期发生更改。如果有任何错误，可以如上一部分中所述，通过查看**通知 API** 来查看这些错误。

## 搜索文档
{: #search-rnr}

{{site.data.keyword.discoveryshort}} 服务将自动使用已训练的模型来对搜索结果（如果可用）进行重新排名。使用 `natural_language_query` 而不是 `query` 发出 [API 调用 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window} 时，会检查是否有模型可用。如果模型可用，那么 {{site.data.keyword.discoveryshort}} 会使用该模型来对结果进行重新排名。我们将先对未排名的文档执行搜索，然后使用排名模型来执行搜索。

1.  可以使用 cURL 命令来搜索集合中的文档。使用“查询 API”调用来执行查询可查看未排名的结果。将 `{apikey_value}`、`{environment_id}` 和 `{collection_id}` 替换为您自己的值。返回的结果将是未排名的结果，并将使用缺省的 {{site.data.keyword.discoveryshort}} 排名公式。可以通过打开训练数据 `csv` 文件，并将第一列的值复制到查询参数来尝试其他查询。

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query=what is the basic mechanism of the transonic aileron buzz"
    ```
    {: pre}

1.  现在，通过设置 `natural_language_query` 参数来使用模型执行搜索。在此之前，请确保检查您是否具有上一部分中所述的已训练模型。在控制台中粘贴以下代码，并将 `{apikey_value}`、`{environment_id}` 和 `{collection_id}` 替换为您的值。

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&natural_language_query=what is the basic mechanism of the transonic aileron buzz"
    ```
    {: pre}

    此命令将使用早先训练的模型来返回重新排名的结果。将此搜索的结果与早先尝试的其他某些搜索的结果进行比较。与在 {{site.data.keyword.retrieveandrankshort}} 中看到的结果相比，您可能会看到结果中有一些差异。这是因为一些用于搜索的方法已更改，简化了体验并改进了结果，但结果的总体质量类似。

在评估重新排名的搜索结果后，可以在 {{site.data.keyword.discoveryshort}} 中通过重复上传具有其他训练查询和示例的训练数据以及查看搜索结果，对这些结果进行优化。您还可以如第一步中所述添加新文档以扩大搜索范围。与 {{site.data.keyword.retrieveandrankshort}} 类似，通过训练来改进结果也是一个迭代式过程。
