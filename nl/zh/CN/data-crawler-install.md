---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-18"

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

# 下载并安装 Data Crawler

Data Crawler 可收集最终用于构成 {{site.data.keyword.discoveryshort}} 服务搜索结果的原始数据。搜寻数据存储库时，搜寻器将从用户指定的种子 URL 开始下载文档和元数据。搜寻器会在层次结构中发现文档，或发现从种子 URL 链接的文档，然后将这些文档排队以等待检索。
{: shortdesc}

## 先决条件

-   Java 运行时环境 V8 或更高版本

    必须正确设置 `JAVA_HOME` 环境变量或者根本不设置此环境变量，才能运行搜寻器。
    {: tip}
-   Red Hat Enterprise Linux 6 或 7，或者 Ubuntu Linux 15 或 16。为了获得最佳性能，Data Crawler 应该在其自己的 Linux 实例上运行，实例可以是虚拟机、容器或硬件。

-   Linux 系统上最低 2 GB RAM

## 下载并安装 Data Crawler

1.  打开浏览器并登录到 [{{site.data.keyword.Bluemix}} 帐户 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net){: new_window}。

1.  在 {{site.data.keyword.Bluemix_notm}}“仪表板”中，选择先前创建的 {{site.data.keyword.discoveryshort}} 服务。

1.  单击“下载 Data Crawler”链接以下载 Data Crawler。

1.  验证您运行的是否为 Java 运行时环境 V8 或更高版本。运行 `java -version` 命令，然后查找 **1.8**。如果运行的版本低于 **1.8**，那么需要在 [IBM JDK ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/developerworks/java/jdk/){: new_window} Web 站点或 [java.com ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.java.com){: new_window} 中，通过软件包管理系统安装 Java Developer Kit (JDK) 8 来升级 Java。

    必须正确设置 `JAVA_HOME` 环境变量或者根本不设置此环境变量，才能运行搜寻器。
    {: tip}

1.  以管理员身份，使用相应命令安装已下载的归档文件：

    -   在使用 rpm 软件包的系统（例如，Red Hat 和 CentOS）上，使用诸如以下命令之类的命令：`rpm -i /full/path/to/rpm/package/rpm-file-name`
    -   在使用 deb 软件包的系统（例如，Ubuntu Hat 和 Debian）上，使用诸如以下命令之类的命令：`dpkg -i /full/path/to/deb/package/deb-file-name`
    -   搜寻器脚本会安装到 `{installation_directory}/bin` 中；例如，`/opt/ibm/crawler/bin`。确保 `{installation_directory}/bin` 位于 `PATH` 环境变量中，这样搜寻器命令才能正确工作。

    搜寻器脚本还会安装到 `/usr/local/bin` 中，因此也可以将其添加到 `PATH` 环境变量中。
    {: tip}
1.  通过将 `{installation_directory}/share/examples/config` 目录的内容复制到系统上的工作目录（例如 `/home/config`）来创建工作目录。

    **警告：**不要直接修改提供的配置示例文件。请复制这些文件，然后对其进行编辑。如果直接编辑示例文件，那么在升级 Data Crawler 时可能会覆盖您的配置，或者在卸载 Data Crawler 时可能会除去您的配置。

    **注：**本指南其余部分中提到 `config` 目录中文件（例如 `config/crawler.conf`）均指的是工作目录中的文件，而不是位于 `{installation_directory}/share/examples/config` 安装目录中的文件。

1.  现在，您已准备就绪，可[配置 Data Crawler 以连接到存储库](/docs/services/discovery/data-crawler-seeds.html)

## Data Crawler 结构

下载 Data Crawler 会将以下文件夹放在系统上：

-   `doc` - 包含具有版权和许可信息的文件。
-   `bin` - 用于运行搜寻器的脚本文件。
-   `connectorFramework` - 此目录中的文件用于支持您与数据进行对话，包括企业内部数据，或者 Web 上或云中的外部数据。
-   `lib` - 搜寻器使用的库文件。
-   `share`
    -   `doc` - 提供 HTML 和 Markdown 格式的文档文件。
    -   `examples/config` - 这些文件用于告知搜寻器将哪些数据用于进行搜寻、搜寻完成后将搜寻到的数据的集合发送到何处以及其他搜寻管理选项。
    -   `man` - 产品内联机帮助页搜寻器文档。

## 此发行版中的已知限制

-   使用无效或缺失的 URL 运行文件系统连接器时，Data Crawler 可能会挂起。
-   配置 `crawler.conf` 文件中的 `urls_to_filter` 值，使所有白名单 URL 或正则表达式都包含在单个正则表达式中。请参阅[配置搜寻选项](/docs/services/discovery/data-crawler-discovery.html#configuring-crawl-options)以获取更多信息。
-   `--config -c` 选项中传递的配置文件的路径必须是限定路径。即，此路径必须为相对路径 `config/crawler.conf` 或 `./crawler.conf`，或者为绝对路径 `/path/to/config/crawler.conf`。仅当 `orchestration_service.conf` 文件是内联文件（而不是使用 `crawler.conf` 文件中的 `include` 引用的文件）时，才可以仅指定 `crawler.conf`。
