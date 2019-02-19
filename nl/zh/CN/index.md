---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-07"

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

# 关于

{{site.data.keyword.discoveryfull}} 能够快速构建基于云的认知性浏览应用程序，用于挖掘非结构化数据中隐藏的可行性洞察，非结构化数据包括您自己的专有数据以及公共和第三方数据。
{: shortdesc}

下面是完整 {{site.data.keyword.discoveryshort}} 服务解决方案的体系结构：

![Discovery 体系结构图](images/discovery-flow.png)

通过 {{site.data.keyword.discoveryshort}}，只需几个步骤即可准备非结构化数据，创建用于查明所需信息的查询，然后将这些洞察集成到新的应用程序或现有解决方案中。

{{site.data.keyword.discoveryshort}} 是怎样实现上述目标的？方法是将数据分析与认知直觉相结合来获取非结构化数据并对其进行扩充，以便您可以发现所需的信息。

{{site.data.keyword.discoveryfull}} 将一组功能丰富的集成、自动化 {{site.data.keyword.watson}} API 整合在一起，用于：

- 搜寻、转换、扩充和规范化数据。
- 安全地浏览专有内容以及免费和许可的公共内容。
- 通过 {{site.data.keyword.nlushort}} (NLU) 应用其他扩充项（例如，概念、关系和观点）。
- 简化开发工作，同时仍然提供对 API 的直接访问。

有关语言支持的信息，请参阅 [{{site.data.keyword.discoveryshort}} 语言支持](/docs/services/discovery/language-support.html)。

有关 {{site.data.keyword.Bluemix_notm}} 安全性的信息，请参阅 [{{site.data.keyword.Bluemix_notm}} 服务描述 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=%28IBM+Cloud+Service+description%29){: new_window}。

{{site.data.keyword.discoveryfull}} Knowledge Graph 是一个 Beta 功能，提供用于跨文档查询实体和关系的新端点。这包括基于上下文的搜索和相关性排名。请参阅 [{{site.data.keyword.discoveryfull}} Knowledge Graph](/docs/services/discovery/building-kg.html) 以获取更多信息。

## 浏览器支持和先决条件

有关 {{site.data.keyword.Bluemix}} 先决条件和受支持浏览器的列表，请参阅[先决条件 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.bluemix.net/docs/overview/prereqs.html#prereqs){: new_window}。

## Watson Discovery News
{: #watson-discovery-news}

{{site.data.keyword.discoverynewsshort}} 是已使用认知洞察进行预扩充的公共数据集，并且随附于 {{site.data.keyword.discoveryshort}} 中。您可以使用此公共非结构化数据集来查询可以集成到应用程序中的洞察。请参阅 [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html#watson-discovery-news) 以获取更多信息。请在[此处 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://discovery-news-demo.ng.bluemix.net/){: new_window} 查看可以使用 {{site.data.keyword.discoverynewsshort}} 构建的内容的演示。

{{site.data.keyword.discoveryshort}} 服务在 [{{site.data.keyword.Bluemix_notm}} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window} 上提供

## Discovery 工具
{: #discovery-tooling}

{{site.data.keyword.discoveryshort}} 服务包括一组完整的联机工具，即 {{site.data.keyword.discoveryshort}} 工具，可帮助您快速设置服务的实例并使用数据填充该实例。

{{site.data.keyword.discoveryshort}} 服务工具旨在通过避免使用 API 来配置和填充服务，从而节省时间。这样一来，应用程序开发者能够集中精力为最终用户创建高价值的方法来体验 {{site.data.keyword.discoveryshort}} 服务。请参阅[工具入门](/docs/services/discovery/getting-started-tool.html)，以获取对 {{site.data.keyword.discoveryshort}} 工具的介绍。


## 后续步骤
{: #next-steps}

- 开始使用 {{site.data.keyword.discoveryshort}} 工具或 {{site.data.keyword.discoveryshort}} API：
    - [{{site.data.keyword.discoveryshort}} 工具入门](/docs/services/discovery/getting-started-tool.html)
    - [{{site.data.keyword.discoveryshort}} API 入门](/docs/services/discovery/getting-started.html)
- {{site.data.keyword.discoveryshort}} 服务支持若干 SDK，可简化应用程序的开发工作。SDK 可用于许多常用编程语言和平台，包括 Node.js、Java 和 Python。所有 SDK 都可从 GitHub 上的 [watson-developer-cloud 名称空间 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/watson-developer-cloud){: new_window} 获取。
    - 有关 SDK 的完整列表及其使用信息，请参阅 [{{site.data.keyword.watson}} SDK](https://console.bluemix.net/docs/services/watson/getting-started-sdks.html#sdks)。
    - 有关 Node、Java 和 Python SDK 的所有方法的详细信息，请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl){: new_window}。
