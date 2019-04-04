---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-01-28"

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

# 下载和安装 Data Crawler
{: #downloading-and-installing-the-data-crawler}

Data Crawler 可收集最终用于构成 {{site.data.keyword.discoveryshort}} 服务搜索结果的原始数据。搜寻数据存储库时，搜寻器会从用户指定的种子 URL 开始下载文档和元数据。搜寻器会发现位于层次结构中的文档或从种子 URL 链接的文档，然后将这些文档排入队列以等待检索。
{: shortdesc}

Data Crawler 应仅用于搜寻文件共享或数据库，在其他所有情况下，您应使用相应的 {{site.data.keyword.discoveryshort}} 连接器。请参阅[连接到数据源](/docs/services/discovery?topic=discovery-sources#sources)以获取详细信息。如果您将 Data Crawler 用于 {{site.data.keyword.discoveryshort}} 连接器支持的数据源，那么将不再提供有关 Data Crawler 的帮助。
{: important}

## 先决条件
{: #dc-prerequisites}

-   Java 运行时环境 V8 或更高版本

    要运行搜寻器，必须正确设置 `JAVA_HOME` 环境变量，或者根本不设置此环境变量。
    {: tip}
-   Red Hat Enterprise Linux 6 或 7，或者 Ubuntu Linux 15 或 16。为了获得最佳性能，Data Crawler 应该在其自己的 Linux 实例上运行，该实例可以是虚拟机、容器或硬件。

-   Linux 系统上至少 2 GB RAM

## 下载和安装 Data Crawler
{: #dc-download-install}

1.  打开浏览器并登录到 [{{site.data.keyword.Bluemix}} 帐户 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/){: new_window}。

1.  在 {{site.data.keyword.Bluemix_notm}}“仪表板”中，选择先前创建的 {{site.data.keyword.discoveryshort}} 服务。

1.  在**自动将内容上传到 Discovery 服务**部分中，单击相应链接以下载适用于 Linux 的 Data Crawler（DEB、RPM 和 ZIP 格式）。

1.  验证您运行的是否为 Java 运行时环境 V8 或更高版本。运行 `java -version` 命令，然后查找 **1.8**。如果运行的版本低于 **1.8**，那么需要从您的软件包管理系统、从 [IBM JDK ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/developerworks/java/jdk/){: new_window} Web 站点或从 [java.com ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.java.com){: new_window} 中安装 Java Developer Kit (JDK) 8 来升级 Java。

    要运行搜寻器，必须正确设置 `JAVA_HOME` 环境变量，或者根本不设置此环境变量。
    {: tip}

1.  以管理员身份，使用相应命令安装所下载的归档文件：

    -   在使用 rpm 软件包的系统（例如，Red Hat 和 CentOS）上，使用如下命令：`rpm -i /full/path/to/rpm/package/rpm-file-name`
    -   在使用 deb 软件包的系统（例如，Ubuntu 和 Debian）上，使用如下命令：`dpkg -i /full/path/to/deb/package/deb-file-name`
    -   搜寻器脚本会安装到 `{installation_directory}/bin` 中；例如，`/opt/ibm/crawler/bin`。要确保搜寻器命令能够正确运行，`{installation_directory}/bin` 必须位于 `PATH` 环境变量中。

    搜寻器脚本还会安装到 `/usr/local/bin` 中，因此也可以将该路径添加到 `PATH` 环境变量中。
    {: tip}
1.  通过将 `{installation_directory}/share/examples/config` 目录的内容复制到系统上的某个工作目录（例如 `/home/config`）来创建您的工作目录。

    **警告：**不要直接修改所提供的配置示例文件。复制这些文件，然后对它们进行编辑。如果直接编辑现有示例文件，那么在升级 Data Crawler 时可能会覆盖您的配置，或者在卸载 Data Crawler 时可能会除去您的配置。

    **注：**本指南其余部分中提到的 `config` 目录中的文件（例如 `config/crawler.conf`），是指您工作目录中的相应文件，而不是安装目录 `{installation_directory}/share/examples/config` 中的文件。

1.  现在，您可以开始[配置 Data Crawler 以连接到存储库](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-connector-and-seed-options)了

## Data Crawler 结构
{: #dc-structure}

下载 Data Crawler 时，会将以下文件夹放置到系统上：

-   `doc` - 包含版权和许可信息相关文件。
-   `bin` - 包含用于运行搜寻器的脚本文件。
-   `connectorFramework` - 通过此目录中的文件，您可以与企业内部数据或者 Web 或云上的外部数据进行交互。
-   `lib` - 包含搜寻器所使用的库文件。
-   `share`
    -   `doc` - 提供 HTML 和 Markdown 格式的文档文件。
    -   `examples/config` - 通过此目录中的文件，您可以告诉搜寻器要搜寻哪些数据，以及在搜寻完成后要将搜寻到的数据集合发送到何处，还可以设置其他搜寻管理选项。
    -   `man` - 产品内联机帮助页面搜寻器文档。

## 此发行版中的已知限制
{: #dc-limitations}

-   使用无效或缺失的 URL 运行文件系统连接器时，Data Crawler 可能会挂起。
-   配置 `crawler.conf` 文件中的 `urls_to_filter` 值，使所有白名单 URL 或正则表达式都包含在单个正则表达式中。有关更多信息，请参阅[配置搜寻选项](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-crawl-options)。
-   `--config -c` 选项中传递的配置文件的路径必须是标准路径。也就是，必须是相对路径 `config/crawler.conf` 或 `./crawler.conf`，或者必须是绝对路径 `/path/to/config/crawler.conf`。仅当 `orchestration_service.conf` 文件是内联文件（而不是使用 `crawler.conf` 文件中的 `include` 引用的文件）时，才可以仅指定 `crawler.conf`。
