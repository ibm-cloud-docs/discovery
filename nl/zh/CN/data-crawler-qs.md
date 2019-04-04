---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-28"

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

# Data Crawler 入门
{: #getting-started-with-the-data-crawler}

本主题说明如何使用 Data Crawler 从本地文件系统中摄入文件，以用于 {{site.data.keyword.discoveryfull}} 服务。
{: shortdesc}

Data Crawler 应仅用于搜寻文件共享或数据库，在其他所有情况下，您应使用相应的 {{site.data.keyword.discoveryshort}} 连接器。请参阅[连接到数据源](/docs/services/discovery?topic=discovery-sources#sources)以获取详细信息。如果您将 Data Crawler 用于 {{site.data.keyword.discoveryshort}} 连接器支持的数据源，那么将不再提供有关 Data Crawler 的帮助。
{: important}

在尝试完成以下任务之前，请先在 {{site.data.keyword.Bluemix}} 中创建一个 {{site.data.keyword.discoveryshort}} 服务实例。要完成本指南，您需要使用与所创建服务实例相关联的凭证。

## 创建环境
{: #dc-create-environment}

使用 bash POST /v1/environments 方法来创建环境。将环境视为用于存储所有文档箱的仓库。以下示例会创建一个名为 `my-first-environment` 的环境：

将 `{apikey}` 替换为您的服务凭证。

（如需使用 {apikey} 凭证的更详细信息，请参阅 [API 入门](/docs/services/discovery?topic=discovery-gs-api#gs-api)。）

```bash
curl -X POST -u "apikey:{apikey}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
```
{: pre}

此 API 返回的响应包含环境标识、环境状态以及环境目前使用的存储量等信息。只有环境状态为 `ready` 时，才能继续执行下一步。创建环境时，如果返回的状态为 `status:pending`，请使用 `GET /v1/environments/{environment_id}` 方法来检查状态，直到环境准备就绪为止。在以下示例中，请将 `{apikey}` 替换为您的服务凭证，并将 `{environment_id}` 替换为创建环境时返回的环境标识。

```bash
curl -u "apikey:{apikey}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}?version=2017-11-07
```
{: pre}

## 创建集合
{: #dc-create-collection}

接下来，使用 `POST /v1/environments/{environment_id}/collections` 方法来创建集合。将集合视为将用于存储环境中文档的箱子。以下示例会在上一步创建的环境中创建一个名为 `my-first-collection` 的集合，并且使用以下缺省配置：

-   将 `{apikey}` 替换为您的服务凭证。
-   将 `{environment_id}` 替换为在步骤 1 中创建的环境的环境标识。

在创建集合之前，必须先获取缺省配置的标识。要查找缺省 `configuration_id`，请使用 `GET /v1/environments/{environment_id}/configurations` 方法：

```bash
curl -u "apikey:{apikey}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07
```
{: pre}

在获取缺省配置标识后，使用该标识来创建集合。将 `{configuration_id}` 替换为环境的缺省配置标识。

```bash
curl -X POST -u "apikey:{apikey}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{configuration_id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07
```
{: pre}

此 API 返回的响应包含集合标识、集合状态以及集合目前使用的存储量等信息。只有集合状态为 `online` 时，才能继续执行下一步。创建集合时，如果返回的状态为 `status:pending`，请使用 `GET /v1/environments/{environment_id}/collections/{collection_id}` 方法来检查状态，直到集合准备就绪为止。在以下示例中，请将 `{apikey}` 替换为您的服务凭证，将 `{environment_id}` 替换为环境标识，并将 `{collection_id}` 替换为此步骤中先前返回的集合标识。

```bash
curl -u "apikey:{apikey}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07
```
{: pre}

## 下载示例文档
{: #dc-download-documents}

下载以下文档：

-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标"></a>

## 下载和安装 Data Crawler
{: #download-and-install-the-data-crawler}

1.  验证系统先决条件

    -   Java 运行时环境 V8 或更高版本

        **注：**要运行搜寻器，必须正确设置 `JAVA_HOME` 环境变量，或者根本不设置此环境变量。
    -   Red Hat Enterprise Linux 6 或 7，或者 Ubuntu Linux 15 或 16。为了获得最佳性能，Data Crawler 应该在其自己的 Linux 实例上运行，该实例可以是虚拟机、容器或硬件。
    -   Linux 系统上至少 2 GB RAM

1.  打开浏览器并登录到 [{{site.data.keyword.Bluemix_notm}} 帐户 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/){: new_window}。
1.  在 {{site.data.keyword.Bluemix_notm}}“仪表板”中，选择先前创建的 {{site.data.keyword.discoveryshort}} 服务。
1.  在**自动将内容上传到 Discovery 服务**下，选择适用于您系统的下载链接（DEB、RPM 或 ZIP）以下载 Data Crawler。
1.  以管理员身份，使用相应命令安装所下载的归档文件：

    -   在使用 rpm 软件包的系统（例如，Red Hat 和 CentOS）上，使用如下命令：`rpm -i /full/path/to/rpm/package/rpm-file-name`
    -   在使用 deb 软件包的系统（例如，Ubuntu 和 Debian）上，使用如下命令：`dpkg -i /full/path/to/deb/package/deb-file-name`
    -   搜寻器脚本会安装到 `{installation_directory}/bin` 中；例如，`/opt/ibm/crawler/bin`。要确保搜寻器命令能够正确运行，`{installation_directory}/bin` 必须位于 `PATH` 环境变量中。

    搜寻器脚本还会安装到 `/usr/local/bin` 中，因此也可以将该路径添加到 `PATH` 环境变量中。
    {: tip}

## 创建工作目录
{: #dc-working-directory}

将 `{installation_directory}/share/examples/config` 目录的内容复制到系统上的某个工作目录，例如 `/home/config`。

**警告：**不要直接修改所提供的配置示例文件。复制这些文件，然后对它们进行编辑。如果直接编辑现有示例文件，那么在升级 Data Crawler 时可能会覆盖您的配置，或者在卸载 Data Crawler 时可能会除去您的配置。

**注：**本指南中提到的 `config` 目录中的文件（例如 `config/crawler.conf`），是指您工作目录中的相应文件，而不是安装目录 `{installation_directory}/share/examples/config` 中的文件。

## 配置搜寻选项
{: #dc-configure-crawl-options}

要将 Data Crawler 设置为搜寻您的存储库，必须指定要搜寻哪些本地系统文件，以及在搜寻完成后要将搜寻到的文件集合发送到哪个 {{site.data.keyword.discoveryshort}} 服务。

1.  **`filesystem-seed.conf`** - 在文本编辑器中打开 `seeds/filesystem-seed.con` 文件。将直接位于 `name-"url"` 属性下的 `value` 属性修改为要搜寻的文件路径。例如：`value-"sdk-fs:///TMP/MY_TEST_DATA/"`

    **注：**URL 必须以 `sdk-fs://` 开头。例如，要搜寻 `/home/watson/mydocs`，此 URL 的值将为 `sdk-fs:///home/watson/mydocs` - 第三个 / 是必需的！

    保存并关闭此文件。

1.  **`discovery_service.conf`** - 在文本编辑器中打开 `discovery/discovery_service.conf` 文件。针对您先前在 {{site.data.keyword.Bluemix_notm}} 上创建的 {{site.data.keyword.discoveryshort}} 服务修改以下值：

    -   `environment_id` - {{site.data.keyword.discoveryshort}} 服务环境标识。
    -   `collection_id` - {{site.data.keyword.discoveryshort}} 服务集合标识。
    -   `configuration_id` - {{site.data.keyword.discoveryshort}} 服务配置标识。
    -   `configuration` - 此 `discovery_service.conf` 文件的完整路径位置，例如 `/home/config/discovery/discovery_service.conf`。
    -   `apikey` - {{site.data.keyword.discoveryshort}} 服务的凭证。
1.  **`crawler.conf`** - 在文本编辑器中打开 `config/crawler.conf` 文件。

    -   为 {{site.data.keyword.discoveryshort}} 服务设置 `output_adapter` `class` 和 `config` 选项，如下所示：

        ```bash
        class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

        

        config - "discovery_service"

        

        discovery_service {
          include "discovery/discovery_service.conf"
        }
        ```
        {: pre}

1.  修改这些文件后，即可搜寻数据。

## 搜寻数据
{: #dc-crawl}

运行以下命令：`crawler crawl --config [config/crawler.conf]`

这将使用配置文件 `crawler.conf` 进行搜寻。

**注：**`--config` 选项中传递的配置文件的路径必须是标准路径。也就是，必须是相对路径，例如 `config/crawler.conf` 或 `./crawler.conf`，或者必须是绝对路径，例如 `/path/to/config/crawler.conf`。

## 搜索文档
{: #dc-search}

最后，使用 `GET /v1/environments/{environment_id}/collections/{collection_id}/query` 方法来搜索文档集合。以下示例会返回名为 `IBM` 的所有实体：

-   将 `{apikey}` 替换为您的服务凭证。
-   将 `{environment_id}` 替换为在步骤 1 中创建的环境的环境标识。
-   将 `{collection_id}` 替换为在步骤 2 中创建的集合的集合标识。

```bash
curl -u "apikey:{apikey}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query-enriched_text.entities.text:IBM'
```
{: pre}

## 结果
{: #dc-results}

现在，您已成功在所创建的环境和集合中查询了文档。您现在可以通过向集合中添加更多文档来开始进行定制。
