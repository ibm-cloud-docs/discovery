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

# Discovery 定價方案
{: #discovery-pricing-plans}

{{site.data.keyword.discoveryfull}} 服務提供三個方案：**精簡**、**進階**及**超值**，它們提供不同層次的資源及功能以符合您的需求。
{: shortdesc}

**專用資料使用案例**的特性、限制及價格如下：

## 精簡
{: #lite}

大小 | 文件儲存空間限制 | 文件數\* | 價格 
------ | ------ | ------ | ------  
N/A | 50 MB | 每月 1,000 | 免費 

「精簡」方案是入門方案，不應該用於正式作業。當您升級至付費方案時，可以保留所有已汲取的文件。「精簡」方案實例在閒置 30 天之後會遭到刪除。 

屬性：
- 1 個環境
- 最多 2 個集合
- 免費 NLU 強化\*\*

其他選項：<br> [自訂模型](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-your-custom-model)：<br>
包含一個 Watson Knowledge Studio 模型。其他模型：未提供<br>[元素分類](/docs/services/discovery?topic=discovery-element-classification#element-classification)\*\*\*：每月包含 500 頁。其他頁面：未提供<br>[新聞查詢](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news)：每月包含 200 個新聞查詢。其他查詢：未提供<br>[查詢擴展](/docs/services/discovery?topic=discovery-query-concepts#query-expansion)：500 個查詢擴展，總計 1,000 個詞彙。其他擴展：未提供

如需從「精簡」升級至「進階」的相關資訊，請參閱[升級服務](/docs/services/discovery?topic=discovery-upgrading-your-plan#service)

如需查詢效能資訊，請參閱[查詢效能](/docs/services/discovery?topic=discovery-qp#qp)。查詢依方案而有所限制。每個**精簡**和**標準**方案的「預估平均查詢」速率：針對具有兩個最上層文字欄位的重新分級查詢為 1 QPS。

## 進階              
{: #advanced}

在選擇「進階方案」大小時，請注意文件儲存和查詢都需要資源。因此，如果您很接近方案大小的文件上限，而且還有下列需求，您可能需要更大的環境： 

-  更高的查詢效能需求（例如，使用相關性訓練）
-  您預期有大量的並行使用者
-  複雜的查詢需要 

如需有關查詢效能影響因素的其他詳細資料，請參閱[查詢效能](/docs/services/discovery?topic=discovery-qp#qp)。查詢依方案而有所限制。**進階**（S、MS）方案的「預估平均查詢」速率：針對具有兩個最上層文字欄位的重新分級查詢為 10 QPS。

大小 | 文件儲存空間限制 | 文件數\* | 價格 
------ | ------ | ------ | ------ 
X-Small\*\*\*\* | 40 GB |每月最多 50,000 份文件| 每月起跳價格為 $500 美元  
Small | 160 GB |每月最多 1M 份文件| 每月起跳價格為 $1,500 美元  
Medium-Small | 320 GB |每月最多 2M 份文件| 每月起跳價格為 $3,000 美元 
Medium| 640 GB |每月最多 4M 份文件| 每月起跳價格為 $5,000 美元 
Medium-Large | 1.2 TB |每月最多 8M 份文件| 每月起跳價格為 $10,000 美元 
Large| 2.4 TB |每月最多為 16M 份文件| 每月起跳價格為 $15,000 美元 
X-Large| 4 TB |每月最多為 32M 份文件| 每月起跳價格為 $20,000 美元 
XX-Large | 5.5 TB |每月最多為 64M 份文件| 每月起跳價格為 $35,000 美元 
XXX-Large | 12 TB |每月最多為 100M 份文件| 每月起跳價格為 $45,000 美元 

X-Small 是可用的最小環境，建議僅用於開發及測試。\*\*\*\*

從「進階」的某個層次移至另一個層次，並不需要建立新的實例。如果從「進階」切換至「超值」方案，則需要新實例。如需從「進階」的某個層級升級至另一個層級的相關資訊，請參閱[從某個進階層級移至另一個層級](/docs/services/discovery?topic=discovery-upgrading-your-plan#upgrading-your-plan)。

\*\*\*\*X-Small 方案的屬性： 
- 1 個環境
- 最多 4 個集合
- 免費 NLU 強化\*\*

所有其他「進階」方案的屬性：
- 1 個環境
- 最多 100 個集合
- 免費 NLU 強化\*\*

其他選項：<br> [自訂模型](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-your-custom-model)：<br>
包含一個 Watson Knowledge Studio 模型。其他模型：每個 $800 美元<br>[元素分類](/docs/services/discovery?topic=discovery-element-classification#element-classification)\*\*\*：每月包含 500 頁。其他頁面：每頁 $0.40 美元<br>[新聞查詢](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news)：每月包含 200 個新聞查詢  
10,000 個其他查詢（每月）：每個查詢 $0.10 美元<br>
10,001 - 100,000 個其他查詢（每月）：每個查詢 $0.05 美元<br>
100,000 個以上的查詢（每月）：每個查詢 $0.03 美元<br>
[查詢擴展](/docs/services/discovery?topic=discovery-query-concepts#query-expansion)：5,000 個查詢擴展，總計 25,000 個詞彙

`-----`
<br>
\* 文件限制假設磁碟上的平均文件大小為 100KB。文件大小是在經過轉換與強化之後算出，因此，文件大小可能會與原始輸入大不相同。您可以使用[環境](https://{DomainName}/apidocs/discovery#get-environment-info)或[集合](https://{DomainName}/apidocs/discovery#get-collection-details) API，或是使用本工具，來檢視已儲存的文件數和已使用的儲存空間總量。如果您的文件在磁碟上的平均值大於 100KB，則您將在達到文件上限之前就達到方案的儲存空間限制。如果您對文件執行[文件分段](/docs/services/discovery?topic=discovery-configservice#doc-segmentation)，則每個區段都算是個別文件。

\*\* [Natural Language Understanding (NLU) 強化](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)為：實體擷取、觀感分析、種類分類、概念標記、關鍵字擷取、關係擷取、情緒分析、元素分類及語意角色擷取。只會強化每份文件的前 50,000 個字元。 

\*\*\* 「元素分類」是透過控管文件進行剖析的強化，以轉換、識別及分類重要元素。它使用「自然語言處理程序」，從 PDF 文件中擷取下列元素：參與方（它所參照的對象）、本質（元素類型）及種類（特定類別）。

若要利用新的環境調整大小選項（`LT`、`XS`、`S`、`MS`、`M`、`ML`、`L`、`XL`、`XXL`、`XXXL`），您必須在使用 API 建立環境時，使用 `2018-08-01` 或更新的 API 版本日期。環境大小的類型現在是 `string`（之前類型為 `integer`。）
{: note}

## 超值
{: #premiumplan}
   
「超值」方案為開發人員及組織提供一個以上 Watson 服務的單一承租戶實例，以達到更好的隔離與安全。這些方案在現有的共用平台上提供運算層次隔離，以及傳送中與靜止的端對端加密資料。 

如需相關資訊，或要購買「超值」方案，請與[銷售人員](https://ibm.biz/contact-wdc-premium)聯絡。 

## 其他資訊
{: #pricingadd}

如需計算成本的相關資訊，請參閱 [IBM Cloud 定價計算機 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/pricing/platform/watson){: new_window}。

如需 IBM Cloud 安全的相關資訊，請參閱[雲端服務資料安全與隱私權 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/software/sla/sladb.nsf/sla/csdsp?OpenDocument){: new_window}。

如需其他計價資訊，請參閱 [{{site.data.keyword.discoveryshort}} 型錄 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/catalog/services/discovery){: new_window}。

## 現有方案之客戶的注意事項
{: #pricingnotes}

- 從 **2018 年 8 月 1 日**開始，您的計費和用量將以此定價方案為基礎。
- 「精簡」方案已從每月 2,000 份文件/400 個 {{site.data.keyword.discoverynewsshort}} 查詢，減少為每月 1,000 份文件/200 個 {{site.data.keyword.discoverynewsshort}} 查詢。如果您已超出新的「精簡」方案限制，則無法再新增更多文件。不過，您可以繼續使用它，或升級至「進階」或「超值」方案。
- 「標準」方案已下架，不再提供給新使用者。如果您目前使用現有的「標準」方案，則可以繼續使用它，或升級至「進階」或「超值」方案。
- 「進階」及「超值」方案現在是以文件層級為基礎，而不再以文件小時數為基礎。您的每月帳單將不會根據文件數而波動，除非您在層級之間切換。
- 如果您是「超值」客戶，請與[銷售人員 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://ibm.biz/contact-wdc-premium){: new_window} 聯絡，以取得計費變更的詳細資料。	
