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

# 使用 Data Crawler 添加内容

通过 Data Crawler，您可自动将内容上传到 {{site.data.keyword.discoveryshort}} 服务。
{: shortdesc}

## 使用 Data Crawler 搜寻数据

Data Crawler 是一个命令行工具，用于帮助您从文档所在的存储库（例如：文件共享、数据库和 Microsoft SharePoint&reg;）中获取文档，然后将这些文档推送到云，以供 {{site.data.keyword.discoveryshort}} 服务使用。

## 何时使用 Data Crawler

如果要对远程系统中的大量文件进行受管上传，或者要从支持的存储库（例如，Db2 数据库）中抽取内容，那么应该使用 Data Crawler。

Data Crawler 并不是用于从本地驱动器上传文件的解决方案。要从本地驱动器上传文件，应该使用工具或使用直接 API 调用来执行。
{: tip}

## 使用 Data Crawler

1. [配置 {{site.data.keyword.discoveryshort}} 服务](/docs/services/discovery/building.html#configuring-your-service)
1. 在有权访问要搜寻的内容的受支持 Linux 系统上，[下载并安装 Data Crawler](/docs/services/discovery/data-crawler-install.html)。
1. [连接 Data Crawler](/docs/services/discovery/data-crawler-seeds.html) 至您的内容。
1. [配置 Data Crawler](/docs/services/discovery/data-crawler-discovery.html) 以连接到 {{site.data.keyword.discoveryshort}} 服务。
1. [搜寻内容](/docs/services/discovery/data-crawler-run.html)。

您可以通过遵循 [Data Crawler 入门](/docs/services/discovery/data-crawler-qs.html)中的示例，快速开始使用 Data Crawler
