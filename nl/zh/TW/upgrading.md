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

# 升級方案
{: #upgrading-your-plan}

{{site.data.keyword.discoveryfull}} 服務提供三個方案，提供不同層次的資源及功能來符合您的需求。
{: shortdesc}

如需詳細資料，請參閱 [{{site.data.keyword.discoveryshort}} 定價方案](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)和 [{{site.data.keyword.discoveryshort}} 型錄 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/catalog/services/discovery){: new_window}。

## 升級服務
{: #service}

若要將方案大小從「精簡」調整至「進階」，請執行下列動作：

1. 開啟 [{{site.data.keyword.Bluemix_notm}} 儀表板](https://{DomainName}/dashboard)。 
1. 按一下 {{site.data.keyword.discoveryshort}} 服務實例，以開啟 {{site.data.keyword.discoveryshort}} 服務儀表板。
1. 從 {{site.data.keyword.discoveryshort}} 服務的**管理**頁面中，按一下**升級**來選擇「進階」方案。這會開啟**方案**頁面。請遵循步驟來完成升級。 
1. 回到**管理**頁面，然後按一下**啟動工具**來開啟 {{site.data.keyword.discoveryshort}} 工具。
   - 如果您在升級至「進階」之前從未建立「精簡」方案的環境，請按一下 ![齒輪](images/icon_settings.png) 圖示，並選擇**建立環境**。畫面會顯示「進階」方案的選項。請選擇符合您需求的方案（`X-Small`、`Small`、`Medium-Small`、`Medium`、`Medium-Large`、`Large`、`X-Large`、`XX-Large`）。
   - 如果您在升級至「進階」之前已建立「精簡」方案的環境，新的「進階」方案環境預設會是 `Small`。 

## 從某個進階層級切換至另一個進階層級
{: #switchadvanced} 

如果您已有「進階」方案，且想要將它升級至更大的方案大小，則可以使用 [API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery#update-an-environment){: new_window} 來執行此動作。 

如需「進階」方案儲存空間限制和定價的詳細資訊，請參閱[進階定價方案](/docs/services/discovery?topic=discovery-discovery-pricing-plans#advanced)。

可用的「進階」方案大小如下： 

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
- 如果後來發現您需要較小的方案大小，您應該設定適當的方案大小、移轉資料，然後取消較大的方案。 

## 升級至超值方案
{: #premium}

如果您對「超值」方案有興趣，請聯絡[銷售人員](https://ibm.biz/contact-wdc-premium)。  
