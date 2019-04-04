---

copyright:
  years: 2015, 2017, 2019
lastupdated: "2019-02-08"

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

# 使用 Data Crawler 添加内容
{: #adding-content-with-data-crawler}

通过 Data Crawler，您可自动将内容上传到 {{site.data.keyword.discoveryshort}} 服务。
{: shortdesc}

Data Crawler 应仅用于搜寻文件共享或数据库，在其他所有情况下，您应使用相应的 {{site.data.keyword.discoveryshort}} 连接器。请参阅[连接到数据源](/docs/services/discovery?topic=discovery-sources#sources)以获取详细信息。如果您将 Data Crawler 用于 {{site.data.keyword.discoveryshort}} 连接器支持的数据源，那么将不再提供有关 Data Crawler 的帮助。
{: important}

## 使用 Data Crawler 搜寻数据
{: #dc-crawling}

Data Crawler 是一个命令行工具，用于帮助您从文档所在的存储库（例如：文件共享和数据库）中获取文档，然后将这些文档推送到云，以供 {{site.data.keyword.discoveryshort}} 服务使用。

Data Crawler 应仅用于搜寻文件共享或数据库，在其他所有情况下，您应使用 Box、SharePoint、Salesforce、IBM Cloud Object Storage 或 Web 搜寻的相应 {{site.data.keyword.discoveryshort}} 连接器。请参阅[连接到数据源](/docs/services/discovery?topic=discovery-sources#sources)以获取详细信息。如果您将 Data Crawler 用于 {{site.data.keyword.discoveryshort}} 连接器支持的数据源，那么将不再提供有关 Data Crawler 的帮助。
{: important}

## 何时使用 Data Crawler
{: #dc-use}

如果要对远程系统中的大量文件进行受管上传，或者要从支持的存储库（例如，Db2 数据库）中抽取内容，那么应该使用 Data Crawler。

Data Crawler 并不是用于从本地驱动器上传文件的解决方案。要从本地驱动器上传文件，应该使用工具或使用直接 API 调用来执行。
另一个用于将大量文件上传到 {{site.data.keyword.discoveryshort}} 的选项是 GitHub 上的 [discovery-files ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/IBM/discovery-files){: new_window}。
{: note}

## 使用 Data Crawler
{: #dc-using}

1. [配置 {{site.data.keyword.discoveryshort}} 服务](/docs/services/discovery?topic=discovery-configservice#configservice)
1. 在有权访问要搜寻的内容的受支持 Linux 系统上，[下载并安装 Data Crawler](/docs/services/discovery?topic=discovery-downloading-and-installing-the-data-crawler#downloading-and-installing-the-data-crawler)。
1. [连接 Data Crawler](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-connector-and-seed-options) 至您的内容。
1. [配置 Data Crawler](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-the-data-crawler) 以连接到 {{site.data.keyword.discoveryshort}} 服务。
1. [搜寻内容](/docs/services/discovery?topic=discovery-crawling-your-data-repository#crawling-your-data-repository)。

您可以通过遵循 [Data Crawler 入门](/docs/services/discovery?topic=discovery-getting-started-with-the-data-crawler#getting-started-with-the-data-crawler)中的示例，快速开始使用 Data Crawler
