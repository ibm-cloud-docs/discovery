---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-08"

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

# Data Crawler 入门

本主题说明如何使用 Data Crawler 从本地文件系统中摄入文件，以用于 {{site.data.keyword.discoveryfull}} 服务。
{: shortdesc}

在尝试此任务之前，请先在 {{site.data.keyword.Bluemix}} 中创建 {{site.data.keyword.discoveryshort}} 服务的实例。为了完成本指南，您将需要使用与所创建服务实例相关联的凭证。

## 创建环境

使用 bash POST /v1/environments 方法来创建环境。将环境视为用于存储所有文档箱的仓库。以下示例将创建名为 `my-first-environment` 的环境：

将 `{username}` 和 `{password}` 替换为您的服务凭证。

```bash
curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
```
{: pre}

此 API 返回的响应包含环境标识、环境状态以及环境正在使用的存储量等信息。在环境状态为 `ready` 之前，请勿继续执行下一步。创建环境时，如果状态返回 `status:pending`，请使用 `GET /v1/environments/{environment_id}` 方法来检查状态，直至状态为 ready。在此示例中，将 `{username}` 和 `{password}` 替换为您的服务凭证，并将 `{environment_id}` 替换为创建环境时返回的环境标识。

```bash
curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}?version=2017-11-07
```
{: pre}

## 创建集合

接下来，使用 `POST /v1/environments/{environment_id}/collections` 方法来创建集合。将集合视为将在环境中存储文档的箱子。此示例将在先前步骤中所创建的环境中创建名为 `my-first-collection` 的集合，并使用以下缺省配置：

-   将 `{username}` 和 `{password}` 替换为您的服务凭证。
-   将 `{environment_id}` 替换为在步骤 1 中创建的环境的环境标识。

在创建集合之前，必须先获取缺省配置的标识。要查找缺省 `configuration_id`，请使用 `GET /v1/environments/{environment_id}/configurations` 方法：

```bash
curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07
```
{: pre}

一旦您有缺省配置标识，请使用该标识来创建集合。将 `{configuration_id}` 替换为环境的缺省配置标识。

```bash
curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{configuration_id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07
```
{: pre}

此 API 返回的响应包含集合标识、集合状态以及集合正在使用的存储量等信息。在集合状态为 `online` 之前，请勿继续执行下一步。创建集合时，如果状态返回 `status:pending`，请使用 `GET /v1/environments/{environment_id}/collections/{collection_id}` 方法来检查状态，直至状态为 online。在此示例中，将 `{username}` 和 `{password}` 替换为您的服务凭证，将 `{environment_id}` 替换为环境标识，并将 `{collection_id}` 替换为此步骤中早先返回的集合标识。

```bash
curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07
```
{: pre}

## 下载示例文档
下载以下文档：

-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标" class="style-scope doc-content"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标" class="style-scope doc-content"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标" class="style-scope doc-content"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="外部链接图标" title="外部链接图标" class="style-scope doc-content"></a>

## 下载并安装 Data Crawler

1.  验证系统先决条件

    -   Java 运行时环境 V8 或更高版本

        **注：**必须正确设置 `JAVA_HOME` 环境变量或者根本不设置此环境变量，才能运行搜寻器。
    -   Red Hat Enterprise Linux 6 或 7，或者 Ubuntu Linux 15 或 16。为了获得最佳性能，Data Crawler 应该在其自己的 Linux 实例上运行，实例可以是虚拟机、容器或硬件。
    -   Linux 系统上最低 2 GB RAM

1.  打开浏览器并登录到 [{{site.data.keyword.Bluemix_notm}} 帐户 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net){: new_window}。
1.  在 {{site.data.keyword.Bluemix_notm}}“仪表板”中，选择先前创建的 {{site.data.keyword.discoveryshort}} 服务。
1.  在**目标用途**下，选择适用于您系统的下载链接（DEB、RPM 或 ZIP）以下载 Data Crawler。
1.  以管理员身份，使用相应命令安装已下载的归档文件：

    -   在使用 rpm 软件包的系统（例如，Red Hat 和 CentOS）上，使用诸如以下命令之类的命令：`rpm -i /full/path/to/rpm/package/rpm-file-name`
    -   在使用 deb 软件包的系统（例如，Ubuntu Hat 和 Debian）上，使用诸如以下命令之类的命令：`dpkg -i /full/path/to/deb/package/deb-file-name`
    -   搜寻器脚本会安装到 `{installation directory}/bin` 中；例如，`/opt/ibm/crawler/bin`。确保 `{installation_directory}/bin` 位于 `PATH` 环境变量中，这样搜寻器命令才能正确工作。

    搜寻器脚本还会安装到 `/usr/local/bin` 中，因此也可以将其添加到 `PATH` 环境变量中。
    {: tip}

## 创建工作目录

将 `{installation_directory}/share/examples/config` 目录的内容复制到系统上的工作目录（例如 `/home/config`）。

**警告：**不要直接修改提供的配置示例文件。请复制这些文件，然后对其进行编辑。如果直接编辑示例文件，那么在升级 Data Crawler 时可能会覆盖您的配置，或者在卸载 Data Crawler 时可能会除去您的配置。

**注：**本指南中提到 `config` 目录中文件（例如 `config/crawler.conf`）均指的是工作目录中的相应文件，而不是位于 `{installation_directory}/share/examples/config` 安装目录中的文件。

## 配置搜寻选项

要设置 Data Crawler 来搜寻存储库，必须指定要搜寻的本地系统文件，以及搜寻完成后要将所搜寻到文件的集合发送到的 {{site.data.keyword.discoveryshort}} 服务。

1.  **`filesystem-seed.conf`** - 在文本编辑器中打开 `seeds/filesystem-seed.con` 文件。将紧接在 `name-"url"` 属性下的 `value` 属性修改为要搜寻的文件路径。例如：`value-"sdk-fs:///TMP/MY_TEST_DATA/"`

    **注：**URL 必须以 `sdk-fs://` 开头。例如，要搜寻 `/home/watson/mydocs`，此 URL 的值将为 `sdk-fs:///home/watson/mydocs` - 第三个 / 是必需的！

    保存并关闭此文件。

1.  **`discovery_service.conf`** - 在文本编辑器中打开 `discovery/discovery_service.conf` 文件。修改特定于您先前在 {{site.data.keyword.Bluemix_notm}} 上创建的 {{site.data.keyword.discoveryshort}} 服务的以下值：

    -   `environment_id` - {{site.data.keyword.discoveryshort}} 服务环境标识。
    -   `collection_id` - {{site.data.keyword.discoveryshort}} 服务集合标识。
    -   `configuration_id` - {{site.data.keyword.discoveryshort}} 服务配置标识。
    -   `configuration` - 此 `discovery_service.conf` 文件的完整路径位置，例如 `/home/config/discovery/discovery_service.conf`。
    -   `username` - {{site.data.keyword.discoveryshort}} 服务的用户名凭证。
    -   `password` - {{site.data.keyword.discoveryshort}} 服务的密码凭证。
1.  **`crawler.conf`** - 在文本编辑器中打开 `config/crawler.conf` 文件。

    -   设置 {{site.data.keyword.discoveryshort}} 服务的 `output_adapter` `class` 和 `config` 选项，如下所示：

        ```bash
        class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

        config - "discovery_service"

        discovery_service {
          include "discovery/discovery_service.conf"
        }
        ```
        {: pre}

1.  修改这些文件后，即可以随时搜寻数据。

## 搜寻数据

运行以下命令：`crawler crawl --config [config/crawler.conf]`

这将使用配置文件 `crawler.conf` 运行搜寻。

**注：**`--config` 选项中传递的配置文件的路径必须是限定路径。即，此路径必须为相对格式（如 `config/crawler.conf` 或 `./crawler.conf`）或绝对路径（如 `/path/to/config/crawler.conf`）。

## 搜索文档

最后，使用 `GET /v1/environments/{environment_id}/collections/{collection_id}/query` 方法来搜索文档集合。以下示例返回名为 `IBM` 的所有实体：

-   将 `{username}` 和 `{password}` 替换为您的服务凭证。
-   将 `{environment_id}` 替换为在步骤 1 中创建的环境的环境标识。
-   将 `{collection_id}` 替换为在步骤 2 中创建的集合的集合标识。

```bash
curl -u "{username}":"{password}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query-enriched_text.entities.text:IBM'
```
{: pre}

## 结果

现在，您已成功在所创建的环境和集合中查询了文档。现在可以通过向集合添加更多文档开始进行定制。
