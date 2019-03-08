---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-17"

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

# Discovery 价格套餐
{: #discovery-pricing-plans}

{{site.data.keyword.discoveryfull}} 服务提供了三种套餐 - **轻量**、**高级**和**高端** - 用于提供不同级别的资源和功能以满足您的需求。
{: shortdesc}

**专用数据用例**的功能、限制和价格如下：

## 轻量
{: #lite}

尺寸|文档存储限制|文档数\*|价格
------ | ------ | ------ | ------  
不适用|50 MB|1,000 个/月|免费

轻量套餐是入门套餐，不应将其用于生产环境。升级到付费套餐时，可以保留所有已摄入的文档。不活动时间超过 30 天的轻量套餐服务将被删除。 

特点：
- 1 个环境
- 最多 2 个集合
- 免费 NLU 扩充项\*\*
- 20 个未完成的文档\*\*\*\* 

其他选项：<br> [定制模型](/docs/services/discovery/integrate-wks.html#integrating-your-custom-model)：<br>
包含一个 Watson Knowledge Studio 模型。更多模型：不可用<br>[元素分类](/docs/services/discovery/element-classification.html)\*\*\*：每月包含 500 个页面。更多页面：不可用<br>[新闻查询](/docs/services/discovery/watson-discovery-news.html)：每月包含 200 个新闻查询。更多查询：不可用<br>[查询扩展](/docs/services/discovery/using.html#query-expansion)：500 个查询扩展，总计 1,000 个术语。更多扩展：不可用

有关从轻量套餐升级到高级套餐的信息，请参阅[升级服务](/docs/services/discovery/upgrading.html#service)

## 高级
{: #advanced}

尺寸|文档存储限制|文档数\*|价格
------ | ------ | ------ | ------ 
XS 号\*\*\*\*\*|40 GB|每月最多 50,000 个文档|起步价：500 美元/月
S 号|160 GB|每月最多 100 万个文档|起步价：1,500 美元/月
M-S 号|320 GB|每月最多 200 万个文档|起步价：3,000 美元/月
M 号|640 GB|每月最多 400 万个文档|起步价：5,000 美元/月
M-L 号|1.2 TB|每月最多 800 万个文档|起步价：10,000 美元/月
L 号|2.4 TB|每月最多 1600 万个文档|起步价：15,000 美元/月
XL 号|4 TB|每月最多 3200 万个文档|起步价：20,000 美元/月
XXL 号|5.5 TB|每月最多 6400 万个文档|起步价：35,000 美元/月
XXXL 号|12 TB|每月最多 1 亿个文档|起步价：45,000 美元/月

XS 号是可用的最小环境，建议仅用于开发和测试。\*\*\*\*\*

从高级套餐的一个级别移至另一个级别无需创建新实例。如果是从高级套餐切换到高端套餐，那么需要新实例。有关从高级套餐的一个层升级到另一层的信息，请参阅[从高级套餐的一个层移至另一个层](/docs/services/discovery/upgrading.html#advanced)。

\*\*\*\*\*XS 号套餐的特点： 
- 1 个环境
- 最多 4 个集合
- 免费 NLU 扩充项\*\*
- 50 个未完成的文档\*\*\*\*

其他所有高级套餐的特点：
- 1 个环境
- 最多 100 个集合
- 免费 NLU 扩充项\*\*
- 105 个未完成的文档\*\*\*\*

其他选项：<br> [定制模型](/docs/services/discovery/integrate-wks.html#integrating-your-custom-model)：<br>
包含一个 Watson Knowledge Studio 模型。更多模型：每个 800 美元<br>[元素分类](/docs/services/discovery/element-classification.html)\*\*\*：每月包含 500 个页面。更多页面：每个页面 0.40 美元<br>[新闻查询](/docs/services/discovery/watson-discovery-news.html)：每月包含 200 个新闻查询  
增加 10,000 个查询（每月）：每个查询 0.10 美元<br>
增加 10,001 - 100,000 个查询（每月）：每个查询 0.05 美元<br>
100,000 个以上的查询（每月）：每个查询 0.03 美元<br>
[查询扩展](/docs/services/discovery/using.html#query-expansion)：5,000 个查询扩展，总计 25,000 个术语。

## 高端
   
高端套餐为开发者和组织提供一个或多个 Watson 服务的单租户实例，以实现更好的隔离和安全性。这些套餐在现有共享平台上提供计算级隔离，以及端到端的动态和静态数据加密。 

有关更多信息或要购买高端套餐，请联系[销售部](https://ibm.biz/contact-wdc-premium)。 
<br>
<br> 

**注：**API 的版本日期已更新为 `2018-08-01`。要利用新的环境大小选项（`LT`、`XS`、`S`、`MS`、`M`、`ML`、`L`、`XL`、`XXL` 和 `XXXL`），必须在使用 API 创建环境时使用此版本日期。现在，环境大小的类型为 `string`（先前类型为 `integer`）。

\* 文档限制假定磁盘上的平均文档大小为 100 KB。文档大小是在文档经过转换和扩充后计算的，因此文档大小可能会与原始输入的大小有明显差异。您可以使用[环境](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#environments-api)或[集合](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#collections-api) API，或者使用工具来查看存储的文档数和使用的存储总量。如果磁盘上的文档平均大小大于 100 KB，那么在达到最大文档数限制之前，会先一步达到套餐的存储限制。如果对文档执行[文档分段](https://console.bluemix.net/docs/services/discovery/building.html#doc-segmentation)，那么每个分段将作为单独的文档进行计数。

\*\* [自然语言理解 (NLU) 扩充项](https://console.bluemix.net/docs/services/discovery/building.html#adding-enrichments)为：“实体抽取”、“观点分析”、“类别分类”、“概念标记”、“关键字抽取”、“关系抽取”、“情绪分析”、“元素分类”和“语义角色抽取”。仅对每个文档的前 50,000 个字符进行扩充。 

\*\*\*“元素分类”扩充项通过管理文档进行解析，以转换、识别和分类重要元素。此扩充项使用“自然语言处理”从 PDF 文档中抽取以下元素：party（所指对象）、nature（元素类型）和 category（特定类）。

\*\*\*\* 如果达到未完成文档数的限制，那么应该降低摄入的速度。使用 Discovery 服务时，文档在添加到集合之前的上传、扩充和处理期间，即处于“未完成”状态。

有关计算成本的信息，请参阅 [IBM Cloud 价格计算器 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.bluemix.net/pricing/platform/watson){: new_window}。

有关 IBM Cloud 安全性的信息，请参阅[云服务数据安全性和隐私 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/software/sla/sladb.nsf/sla/csdsp?OpenDocument){: new_window}。

有关其他定价信息，请参阅 [{{site.data.keyword.discoveryshort}} 目录 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.bluemix.net/catalog/services/discovery){: new_window}。

## 针对使用现有套餐的客户的说明

- 从 **2018 年 8 月 1 日**开始，您的计费和使用情况将基于此价格套餐。
- 轻量套餐已从每月 2,000 个文档/400 个 {{site.data.keyword.discoverynewsshort}} 查询减少到每月 1,000 个文档/200 个 {{site.data.keyword.discoverynewsshort}} 查询。如果您已超过新的轻量套餐限制，那么不能再添加更多文档。但是，您可以继续使用轻量套餐，也可以升级到高级或高端套餐。
- 标准套餐已引退，不再可供新用户使用。如果您当前正在使用现有标准套餐，那么可以继续使用该套餐，也可以升级到高级或高端套餐。
- 高级套餐和高端套餐现在基于文档层，而不再基于文档小时数。除非您在各层之间切换，否则您的每月帐单不会因文档数而波动。
- 对于高端套餐客户，请联系[销售部](https://ibm.biz/contact-wdc-premium)以了解有关计费更改的详细信息。	
