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

# 故障诊断

使用 {{site.data.keyword.discoveryshort}} 服务的故障诊断技巧

如果在使用 {{site.data.keyword.discoveryshort}} 服务时遇到问题，请尝试以下一个或多个故障诊断技巧。

-   可能由于当前文档中的数据与先前摄入文档中的类似数据之间的类型不匹配，导致文档摄入失败。例如，某个字段在一个文档中的类型可能为 **date**，而在后续文档中的类型为 **string**，这会阻止后续文档正确建立索引。

    预览操作无法预测类型不匹配的情况，因为此操作仅测试单个文档，而不持续记录转换结果。
-   快速或大规模对文档建立索引有时可能会导致后端搜索服务重新启动。如果发生这种情况，请联系 {{site.data.keyword.IBM}} 支持人员以获取帮助。
