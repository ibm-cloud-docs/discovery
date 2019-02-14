---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-25"

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

# 使用性能仪表板查看度量值并改进查询结果

{{site.data.keyword.discoveryshort}} 工具中的性能仪表板可用于查看查询度量值以及改进查询结果，包括查询相关性。

您可以通过单击左侧的**查看数据度量值**图标来访问性能仪表板。该仪表板在高端或专用环境中不可用。

有两个选项可用于改进自然语言查询结果：
- [通过添加更多数据来修正无结果的查询](/docs/services/discovery/dashboard.html#addmore)
- [通过训练数据使相关结果显示在最前](/docs/services/discovery/dashboard.html#traindata)

您可以在[查询概述](/docs/services/discovery/dashboard.html#overview)中查看数据度量值。 

## 通过添加更多数据来修正无结果的查询
{: #addmore}

在仪表板的此部分中，可以查看返回零个结果的查询，然后添加更多数据，以便未来查询可返回结果。单击**查看所有数据并添加数据**按钮以开始操作。 

## 通过训练数据使相关结果显示在最前
{: #traindata}

在此部分中，可以对集合进行训练，以提高自然语言查询结果的相关性。单击**查看所有数据并执行相关训练**按钮以开始操作。然后，请参阅[添加查询并对结果相关性评级](/docs/services/discovery/train-tooling.html#results)以获取相关指示信息。

有关训练需求和选项的更多信息，请参阅[使用工具改进结果相关性](/docs/services/discovery/train-tooling.html)。

## 查询概述
{: #overview}

“查询概述”部分显示了以下内容：
- 用户所做查询的总数
- 单击了一个或多个结果的查询的百分比
- 未单击任何结果的查询的百分比
- 未返回任何结果的查询的百分比
- 随时间推移显示这些结果的图形，以便您可以跟踪添加更多数据和相关性训练对性能的提高程度

这些结果是使用事件和反馈 API 收集的。请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#events-and-feedback-api) 以获取更多信息。
