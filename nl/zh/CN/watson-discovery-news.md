---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-30"

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

# Watson Discovery News

{{site.data.keyword.discoverynewsfull}} 随附于 {{site.data.keyword.discoveryshort}}。{{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} 是一个已建立索引的数据集，已使用以下认知见解进行预扩充：**关键字抽取**、**实体抽取**、**语义角色抽取**、**观点分析**、**关系抽取**和**类别分类**。（要了解有关扩充项的更多信息，请参阅[添加扩充项](building.html#adding-enrichments)。）此外，还添加了以下其他元数据：搜寻日期和发布日期。历史搜索可用于搜索过去 60 天的新闻数据。请在[此处 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://discovery-news-demo.mybluemix.net/){: new_window} 查看可以使用 {{site.data.keyword.discoverynewsfull}} 构建的内容的演示。

{{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} 会持续使用新文章进行更新。{{site.data.keyword.discoverynewsshort}} 英语版每天更新约 300,000 篇新文章。{{site.data.keyword.discoverynewsshort}} 西班牙语版每天更新约 60,000 篇新文章；{{site.data.keyword.discoverynewsshort}} 韩语版每天更新 10,000 篇新文章。

{{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} 的用例：

- 新闻提醒 - 利用对实体、关键字、类别和观点分析的支持来创建新闻提醒，以监视新闻以及对新闻的观点。

- 事件检测 - 主题/行动/对象语义角色抽取会检查词汇/行动，例如“收购”、“选举结果”或“IPO”。

- 新闻中的趋势主题 - 识别热门主题，并监视提及这些主题（或相关主题）的频率的上升和下降情况。

有关为 {{site.data.keyword.discoverynewsfull}} 编写查询的信息，请参阅[查询概念](/docs/services/discovery/using.html)和[查询参考](/docs/services/discovery/query-reference.html)。

不能调整 {{site.data.keyword.discoverynewsfull}} 配置，也不能培训 {{site.data.keyword.discoverynewsfull}} 集合或向其中添加文档。

**注：**针对 Watson Discovery News 查询返回的最大结果数为 `50`。使用其他查询和 `offset` 参数可返回 `50` 个以上的结果。

**注：**此版本的 {{site.data.keyword.discoverynewsfull}} 已于 **2017 年 7 月 31 日**推出。原始版本已重命名为 {{site.data.keyword.discoverynewsfull}} Original，该版本已引退，其终止服务日期为 **2018 年 1 月 15 日**。有关迁移的信息，请参阅[从 Watson Discovery News Original 迁移](/docs/services/discovery/migrate-bwdn.html)。
