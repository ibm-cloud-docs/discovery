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

# Discovery 价格套餐
{: #discovery-pricing-plans}

{{site.data.keyword.discoveryfull}} 服务有三种套餐（**轻量**、**高级**和**高端**），分别提供不同级别的资源和功能来满足您的需求。
{: shortdesc}

**专用数据用例**具有以下功能、限制和价格：

## 轻量
{: #lite}

大小|文档存储限制|文档数\*|价格
------ | ------ | ------ | ------  
不适用|50 MB|1,000 个/月|免费

轻量套餐是入门套餐，不应用于生产环境。升级到付费套餐时，可以保留所有已摄入的文档。轻量套餐实例处于不活动状态达到 30 天后将会被删除。 

特色：
- 1 个环境
- 最多 2 个集合
- 免费 NLU 扩充项\*\*

其他选项：<br> [定制模型](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-your-custom-model)：<br>
包含一个 Watson Knowledge Studio 模型。更多模型：不可用<br>[元素分类](/docs/services/discovery?topic=discovery-element-classification#element-classification)\*\*\*：每月包含 500 个页面。更多页面：不可用<br>[新闻查询](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news)：每月包含 200 个新闻查询。更多查询：不可用<br>[查询扩展](/docs/services/discovery?topic=discovery-query-concepts#query-expansion)：500 个查询扩展，总计 1,000 个词汇。更多扩展：不可用

有关从轻量套餐升级到高级套餐的信息，请参阅[升级服务](/docs/services/discovery?topic=discovery-upgrading-your-plan#service)

有关查询性能信息，请参阅[查询性能](/docs/services/discovery?topic=discovery-qp#qp)。查询基于套餐受到相应限制。每个**轻量**和**标准**套餐的估算平均查询比率为：具有两个顶级文本字段的重新排名查询为 1 QPS。

## 高级
{: #advanced}

选择高级套餐大小时，请注意，文档存储和查询均需要资源。因此，如果您接近套餐大小的最大文档限制，并且还具有以下需求，那么您可能需要较大环境： 

-  更高的查询性能需求（例如，使用相关性训练）
-  预期有大量并发用户
-  需要复杂查询 

有关影响查询性能的因素的更多详细信息，请参阅[查询性能](/docs/services/discovery?topic=discovery-qp#qp)。查询基于套餐受到相应限制。每个**高级**（S 和 MS）套餐的估算平均查询比率为：具有两个顶级文本字段的重新排名查询为 10 QPS。

大小|文档存储限制|文档数\*|价格
------ | ------ | ------ | ------ 
XS 号\*\*\*\* |40 GB|每月最多 50,000 个文档|起步价：500 美元/月
S 号|160 GB|每月最多 100 万个文档|起步价：1,500 美元/月
MS 号|320 GB|每月最多 200 万个文档|起步价：3,000 美元/月
M 号|640 GB|每月最多 400 万个文档|起步价：5,000 美元/月
ML 号|1.2 TB|每月最多 800 万个文档|起步价：10,000 美元/月
L 号|2.4 TB|每月最多 1600 万个文档|起步价：15,000 美元/月
XL 号|4 TB|每月最多 3200 万个文档|起步价：20,000 美元/月
XXL 号|5.5 TB|每月最多 6400 万个文档|起步价：35,000 美元/月
XXXL 号|12 TB|每月最多 1 亿个文档|起步价：45,000 美元/月

XS 号是可用的最小环境，建议仅用于开发和测试。\*\*\*\*

从高级套餐的一个级别移至另一个级别无需创建新实例。如果从高级套餐切换到高端套餐，那么需要新实例。有关从高级套餐的一个等级升级到另一个等级的信息，请参阅[从高级套餐的一个层移至另一个层](/docs/services/discovery?topic=discovery-upgrading-your-plan#upgrading-your-plan)。

\*\*\*\*XS 号套餐的特色： 
- 1 个环境
- 最多 4 个集合
- 免费 NLU 扩充项\*\*

其他所有高级套餐的特色：
- 1 个环境
- 最多 100 个集合
- 免费 NLU 扩充项\*\*

其他选项：<br> [定制模型](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-your-custom-model)：<br>
包含一个 Watson Knowledge Studio 模型。更多模型：每个 800 美元<br>[元素分类](/docs/services/discovery?topic=discovery-element-classification#element-classification)\*\*\*：每月包含 500 个页面。更多页面：每个页面 0.40 美元<br>[新闻查询](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news)：每月包含 200 个新闻查询  
另加 10,000 个查询（每月）：每个查询 0.10 美元<br>
另加 10,001 - 100,000 个查询（每月）：每个查询 0.05 美元<br>
100,000 个以上的查询（每月）：每个查询 0.03 美元<br>
[查询扩展](/docs/services/discovery?topic=discovery-query-concepts#query-expansion)：5,000 个查询扩展，总计 25,000 个词汇。

`-----`
<br>
\* 文档限制假定磁盘上的平均文档大小为 100 KB。文档大小是在文档经过转换和扩充后计算的，因此文档大小可能会与原始输入的大小有明显差异。您可以使用[环境](https://{DomainName}/apidocs/discovery#get-environment-info)或[集合](https://{DomainName}/apidocs/discovery#get-collection-details) API 或者使用工具来查看存储的文档数和使用的存储总量。如果磁盘上的文档平均大小大于 100 KB，那么在达到最大文档限制之前，会先一步达到套餐的存储限制。如果对文档执行[文档分段](/docs/services/discovery?topic=discovery-configservice#doc-segmentation)，那么每个分段将作为单独的文档进行计数。

\*\* [Natural Language Understanding (NLU) 扩充项](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)为：“实体抽取”、“观点分析”、“类别分类”、“概念标记”、“关键字抽取”、“关系抽取”、“情绪分析”、“元素分类”和“语义角色抽取”。仅会对每个文档的前 50,000 个字符进行扩充。 

\*\*\*“元素分类”扩充项会解析管理文档来转换、识别和分类重要元素。此扩充项使用“自然语言处理”从 PDF 文档中抽取以下元素：party（所指对象）、nature（元素类型）和 category（特定类）。

要利用新的环境大小选项（`LT`、`XS`、`S`、`MS`、`M`、`ML`、`L`、`XL`、`XXL` 和 `XXXL`），在使用 API 创建环境时必须使用 API 版本日期 `2018-08-01` 或更新日期。现在，环境大小的类型为 `string`（先前类型为 `integer`）。
{: note}

## 高端
{: #premiumplan}
   
高端套餐为开发者和组织提供一个或多个 Watson 服务的单租户实例，从而实现更好的隔离和安全性。这些套餐在现有共享平台上提供计算级隔离，以及端到端的动态和静态数据加密。 

有关更多信息或要购买高端套餐，请联系[销售部](https://ibm.biz/contact-wdc-premium)。 

## 其他信息
{: #pricingadd}

有关计算成本的信息，请参阅 [IBM Cloud Pricing Calculator ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/pricing/platform/watson){: new_window}。

有关 IBM Cloud 安全性的信息，请参阅 [Cloud Services data security and privacy ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/software/sla/sladb.nsf/sla/csdsp?OpenDocument){: new_window}。

有关其他定价信息，请参阅 [{{site.data.keyword.discoveryshort}} 目录 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/catalog/services/discovery){: new_window}。

## 针对使用现有套餐的客户的说明
{: #pricingnotes}

- 从 **2018 年 8 月 1 日**开始，您的计费和使用情况将基于此价格套餐。
- 轻量套餐已从每月 2,000 个文档/400 个 {{site.data.keyword.discoverynewsshort}} 查询减少到每月 1,000 个文档/200 个 {{site.data.keyword.discoverynewsshort}} 查询。如果您已超过新的轻量套餐限制，那么将无法再添加更多文档。但是，您可以继续使用轻量套餐，也可以升级到高级或高端套餐。
- 标准套餐已引退，将不再供新用户使用。如果您目前使用的是现有标准套餐，那么可以继续使用该套餐，也可以升级到高级或高端套餐。
- 高级套餐和高端套餐现在基于文档层，而不再基于文档小时数。除非您在各层之间切换，否则您的每月帐单不会随文档数的变化而波动。
- 对于高端套餐客户，请联系[销售部 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://ibm.biz/contact-wdc-premium){: new_window} 以了解有关计费更改的详细信息。	
