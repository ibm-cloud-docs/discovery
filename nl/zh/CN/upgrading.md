---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-25"

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

# 升级套餐

{{site.data.keyword.discoveryfull}} 服务提供了三种套餐，用于提供不同级别的资源和功能以满足您的需求。
{: shortdesc}

请参阅 [{{site.data.keyword.discoveryshort}} 价格套餐](/docs/services/discovery/pricing-details.html)和 [{{site.data.keyword.discoveryshort}} 目录 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window} 以获取详细信息。

## 升级服务
{: #service} 

要将套餐大小从轻量调整为高级，请执行以下操作：

1. 打开 [{{site.data.keyword.Bluemix_notm}} 仪表板](https://console.{DomainName}/dashboard)。 
1. 单击 {{site.data.keyword.discoveryshort}} 服务实例以打开 {{site.data.keyword.discoveryshort}} 服务仪表板。
1. 在 {{site.data.keyword.discoveryshort}} 服务的**管理**页面中，单击**升级**以选择高级套餐。这将打开**套餐**页面。执行以下步骤以完成升级。 
1. 返回到**管理**页面，然后单击**启动工具**以打开 {{site.data.keyword.discoveryshort}} 工具。
   - 如果在升级到高级套餐之前，从未为轻量套餐创建过环境，请单击 ![齿轮](images/icon_settings.png) 图标，然后选择**创建环境**。这将显示一个屏幕，其中包含高级套餐的选项。请选择适合您需求的选项（`XS 号`、`S 号`、`M-S 号`、`M 号`、`M-L 号`、`L 号`、`XL 号`、`XXL 号`）。
   - 如果在升级到高级套餐之前为轻量套餐创建过环境，那么缺省情况下，新的高级套餐环境将为 `S 号`。 

## 从高级套餐的一个层切换到另一个层
{: #advanced} 

如果您已具有高级套餐，并且要将其升级为更大大小的套餐，那么可以使用 [API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#update-environment){: new_window} 进行升级。 

有关高级套餐存储限制和定价的详细信息，请参阅[高级价格套餐](/docs/services/discovery/pricing-details.html#advanced)。

您可以升级高级套餐大小，但不能将其降级为更小的大小。可用的高级套餐大小包括： 

套餐大小|标签
--------- | ------ 
XS 号|XS
S 号|S
M-S 号|MS
M 号|M
M-L 号|ML
L 号|L
XL 号|XL
XXL 号|XXL

- 在升级期间，可以继续执行查询和建立索引。升级所需的时间取决于多个因素。您可以在完成升级期间使用 API 来轮询环境。
- 从高级套餐的一个级别移至另一个级别无需创建新实例。 
- 升级完成后，将按新的套餐费率收费。

## 升级到高端套餐
{: #premium}

如果您对高端套餐感兴趣，请联系[销售部](https://ibm.biz/contact-wdc-premium)。  
