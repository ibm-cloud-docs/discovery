---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-03-07"

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

# 升级套餐
{: #upgrading-your-plan}

{{site.data.keyword.discoveryfull}} 服务有三种套餐，分别提供不同级别的资源和功能来满足您的需求。
{: shortdesc}

请参阅 [{{site.data.keyword.discoveryshort}} 价格套餐](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)和 [{{site.data.keyword.discoveryshort}} 目录 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/catalog/services/discovery){: new_window}，以获取详细信息。

## 升级服务
{: #service}

要将套餐大小从轻量调整为高级，请执行以下操作：

1. 打开 [{{site.data.keyword.Bluemix_notm}} 仪表板](https://{DomainName}/dashboard)。 
1. 单击 {{site.data.keyword.discoveryshort}} 服务实例，以打开 {{site.data.keyword.discoveryshort}} 服务仪表板。
1. 在 {{site.data.keyword.discoveryshort}} 服务的**管理**页面上，单击**升级**以选择高级套餐。这将打开**套餐**页面。请执行相应步骤来完成升级。 
1. 返回到**管理**页面，然后单击**启动工具**以打开 {{site.data.keyword.discoveryshort}} 工具。
   - 在升级到高级套餐之前，如果从来没有为轻量套餐创建过环境，请单击 ![齿轮](images/icon_settings.png) 图标，然后选择**创建环境**。此时屏幕上将显示高级套餐的选项。请选择适合您需求的选项（`XS 号`、`S 号`、`MS 号`、`M 号`、`ML 号`、`L 号`、`XL 号`和 `XXL 号`）。
   - 在升级到高级套餐之前，如果曾经为轻量套餐创建过环境，那么缺省情况下，新的高级套餐环境将为 `S 号`。 

## 从高级套餐的一个等级切换到另一个等级
{: #switchadvanced} 

如果您已拥有高级套餐，并且想要将其升级为更大大小的套餐，那么可以使用 [API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/discovery#update-an-environment){: new_window} 进行升级。 

有关高级套餐存储限制和定价的详细信息，请参阅[高级价格套餐](/docs/services/discovery?topic=discovery-discovery-pricing-plans#advanced)。

可用的高级套餐大小包括： 

套餐大小|标签
--------- | ------ 
XS 号|XS
S 号|S
MS 号|MS
M 号|M
ML 号|ML
L 号|L
XL 号|XL
XXL 号|XXL

- 在升级期间，可以继续执行查询和建立索引。升级所需的时间取决于多个因素。当升级完成时，即可使用 API 来轮询环境。
- 从高级套餐的一个级别移至另一个级别无需创建新实例。 
- 升级完成后，将按新的套餐费率进行收费。
- 如果稍后发现需要较小的套餐大小，您应设置相应的套餐大小，迁移您的数据，然后取消较大的套餐。 

## 升级到高端套餐
{: #premium}

如果您对高端套餐感兴趣，请联系[销售部](https://ibm.biz/contact-wdc-premium)。  
