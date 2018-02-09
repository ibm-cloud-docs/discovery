---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-09"

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

{{site.data.keyword.discoveryfull}} 服务提供了三种套餐，用于提供不同级别的资源和功能以满足您的需求。
{: shortdesc}

**专用数据用例**的限制和价格如下：

| Lite|  标准| 高级| 高端|
|--------------------------|-------------------|-------------------|-------------------|
| 每月最多 2,000 个并发文档\*|每月最多 100,000 个并发文档\*<br/> 每月每 1,000 个并发文档 10 美元（0.0139 美元/千文档/小时）\*\*\*<br/> 每月 2,000 个文档免费\*\*\*\*| **保留的环境**</br>基本费率 1,000 美元/月<br/> 每月最多 1,000,000 个文档\*<br/> 每月每 1,000 个并发文档 5 美元（0.00694 美元/千文档/小时）\*\*\*<br/> 含每月 100,000 个文档\*\*\*\*</br> 对于更大型的环境，请联系[销售部 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/marketing/iwm/dre/signup?source=MAIL-watson){: new_window}。| **高端套餐**为开发者和组织提供一个或多个 Watson 服务的单个租户实例，以实现更好的隔离和安全性。这些套餐在现有共享平台上提供计算级隔离，以及端到端的动态和静态数据加密。有关更多信息或要购买高端套餐，请联系[销售部 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://ibm.biz/contact-wdc-premium){: new_window}|
| 200MB\*\*|10GB\*\*| 80GB\*\*|-|
| 最多 2 个集合|最多 4 个集合| 最多 100 个集合|-|
| 最多 1 个 {{site.data.keyword.knowledgestudiofull}} 定制模型|最多 1 个 {{site.data.keyword.knowledgestudioshort}} 定制模型| {{site.data.keyword.knowledgestudioshort}} 定制模型数量不限<br/>含 1 个 {{site.data.keyword.knowledgestudioshort}} 定制模型<br/>每月每个 {{site.data.keyword.knowledgestudioshort}} 模型另外收费 800 美元|-|

**注：**在所有套餐中，每月前 1,000 个 {{site.data.keyword.discoverynewsshort}} 查询都是免费的。超过前 1,000 个 {{site.data.keyword.discoverynewsshort}} 查询后，按每个查询 0.10 美元收费。

**注：**不活动时间超过 30 天的 Lite 套餐服务将被删除。在 Lite 套餐上，每个组织分配有一个免费环境。

 \* 文档限制假定磁盘上的平均文档大小为 100 KB。这是集合中一个文档经过转换和扩充后的大小，因此该大小可能会与原始输入的大小有明显差异。您可以使用 `environments` 或 `collections` API，或者使用工具来查看存储的文档数和使用的存储总量。

 \*\* 如果磁盘上的文档平均大小大于 100 KB，那么在达到最大文档数限制之前，会先一步达到套餐的存储限制。

 \*\*\* 价格基于一批 1000 个文档存储在服务中的小时数（称为“千文档-小时”）。对于定价计算器，这是应该输入的数字（`文档数 * 一个月中这些文档存储的小时数/1000`）。

 \*\*\*\* 免费量基于一个月所存储文档数的等效量。例如，在标准套餐中，免费量等于 2,000 个文档 * 720 小时 / 1000 个文档的批次  = 1440 千文档-小时。

**示例：**标准套餐的用户整个月存储了 4,000 个文档。将按如下所示对其收费：

- `4000 个文档 * 720 小时（一个月中）/ 1000 = 2,880` 千文档-小时已使用

- `2,880 - 1,440（免费文档-小时数）= 1,440` 千文档-小时应计费

- 该月的费用为 `1,440 * 0.0139 美元`（每千文档-小时的价格）= `20.00 美元`

**注：**计算每小时的计费金额时，存储的文档总数将四舍五入为 1,000 的最接近整数倍数以用于计算。例如，如果将 4,678 个文档存储了 1 小时，那么会将其四舍五入为 5000 个文档，从而将按 5 千文档-小时对该帐户计费。

**注：**不会对扩充项额外收费。

有关 {{site.data.keyword.Bluemix_notm}} 安全性的信息，请参阅 [{{site.data.keyword.Bluemix_notm}} 服务描述 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=IBM+Bluemix+Service+Description){: new_window}.

## 从先前的价格套餐转换

在 **2017 年 8 月 1 日**之前预订套餐的客户已迁移到其中一个新套餐。

- 先前使用 30 天免费试用套餐的客户已迁移到 **Lite** 套餐。
  执行此转换后，现有用户可能已达到或超过 Lite 套餐对文档数_（2000 个）_、存储量 _(200 Mb)_ 或集合数_（2 个）_的限制。如果您已超过 **Lite** 套餐的限制，那么将无法向服务添加任何额外的内容，但仍可以查询集合。您可以使用 {{site.data.keyword.discoveryshort}} 工具或 API 来查看所有这些限制的当前状态。为了能够继续向 {{site.data.keyword.discoveryshort}} 实例添加内容，您必须执行以下其中一个操作：
  - 除去集合和/或文档，使其数量不超过 **Lite** 套餐的限制。
    可以使用 [delete-doc ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-doc){: new_window} 方法通过 API 来逐个删除文档，也可以使用 [delete-collection![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-collection){: new_window} 方法通过工具或 API 来删除整个集合。
  - 将套餐升级到满足您存储需求的级别。
- 环境大小为 **`1`**、**`2`** 或 **`3`** 的客户已自动迁移到**高级**套餐。
  如果您已移至“高级”层并且拥有的文档数少于 100,000 个，集合数少于 4 个，那么可移至“标准”层以降低成本。这需要在标准套餐中创建新的 Discovery 实例，然后将数据重新摄入到新实例。摄入操作可以通过工具、API 或 Data Crawler 来完成。

请参阅 [{{site.data.keyword.discoveryshort}} 目录 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window}，以获取更多定价信息。
