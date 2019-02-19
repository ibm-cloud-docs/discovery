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

# 升級方案

{{site.data.keyword.discoveryfull}} 服務提供三個方案，提供不同層次的資源及功能來符合您的需求。
{: shortdesc}

如需詳細資料，請參閱 [{{site.data.keyword.discoveryshort}}定價方案](/docs/services/discovery/pricing-details.html)和 [{{site.data.keyword.discoveryshort}} 型錄 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window}。

## 升級服務
{: #service} 

若要將方案大小從「精簡」調整至「進階」，請執行下列動作：

1. 開啟 [{{site.data.keyword.Bluemix_notm}} 儀表板](https://console.{DomainName}/dashboard)。 
1. 按一下 {{site.data.keyword.discoveryshort}} 服務實例，以開啟 {{site.data.keyword.discoveryshort}} 服務儀表板。
1. 從 {{site.data.keyword.discoveryshort}} 服務的**管理**頁面中，按一下**升級**來選擇「進階」方案。這會開啟**方案**頁面。請遵循步驟來完成升級。 
1. 回到**管理**頁面，然後按一下**啟動工具**來開啟 {{site.data.keyword.discoveryshort}} 工具。
   - 如果您在升級至「進階」之前從未建立「精簡」方案的環境，請按一下 ![齒輪](images/icon_settings.png) 圖示，並選擇**建立環境**。畫面會顯示「進階」方案的選項。請選擇符合您需求的方案（`X-Small`、`Small`、`Medium-Small`、`Medium`、`Medium-Large`、`Large`、`X-Large`、`XX-Large`）。
   - 如果您在升級至「進階」之前已建立「精簡」方案的環境，新的「進階」方案環境預設會是 `Small`。 

## 從某個進階層級切換至另一個進階層級
{: #advanced} 

如果您已有「進階」方案，且想要將它升級至更大的方案大小，則可以使用 [API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#update-environment){: new_window} 來執行此動作。 

如需「進階」方案儲存空間限制和定價的詳細資訊，請參閱[進階定價方案](/docs/services/discovery/pricing-details.html#advanced)。

您可以升級「進階」方案大小，但不能將大小降級為較小的大小。可用的「進階」方案大小如下： 

方案大小  | 標籤   
--------- | ------ 
X-Small | XS 
Small | S 
Medium-Small | MS 
Medium | M 
Medium-Large | ML 
Large | L
X-Large | XL 
XX-Large | XXL 

- 在升級期間，可以繼續處理查詢和索引。升級所需的時間取決於若干因素。升級完成時，您可以使用 API 來輪詢環境。
- 從「進階」的某個層次移至另一個層次，並不需要建立新的實例。 
- 升級完成之後，將會以新的方案費率向您收費。

## 升級至超值方案
{: #premium}

如果您對「超值」方案有興趣，請聯絡[銷售人員](https://ibm.biz/contact-wdc-premium)。  
