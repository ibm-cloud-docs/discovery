---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-18"

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

# 查詢效能
{: #qp}

{{site.data.keyword.discoveryshort}} 中的查詢效能取決於若干因素。 

## 評估效能 
{: #qp-evaluate}

如果您預期應用程式上會有大量同時負載，請務必評估{{site.data.keyword.discoveryshort}} 應用程式的效能。有幾個常用的維度可用來測量效能：
1.  **回應延遲時間** - {{site.data.keyword.discoveryshort}} 傳回查詢結果所需的時間。 
    - 延遲時間會因若干因素而不同，請參閱[影響效能的因素](/docs/services/discovery?topic=discovery-qp#perffactors)，以取得相關資訊。 
    - 請務必使用一組具代表性的查詢，在正式作業環境中執行測試，以判斷您的平均延遲時間。 
1.   **查詢速率** - 在給定時間內可以處理的要求數，通常是以「每秒查詢數」(QPS) 來測量。當您預期應用程式上會有大量同時負載時，此測量是最重要的。  
     - 可達到的速率會因為與延遲時間相同的許多因素而不同。 
     - 查詢速率也應該要以具代表性的查詢和您預期看到的負載量來評估。記得將測試期間的尖峰負載納入考量。

## 影響效能的因素
{: #perffactors}

{{site.data.keyword.discoveryshort}} 中的查詢效能會因若干因素而不同，包括方案大小、查詢複雜性、所使用的特性，以及集合大小和複雜性。

### 方案大小  
{: #qp-plansize}

{{site.data.keyword.discoveryshort}} 定價方案有限制可用的文件數，同時也會提供不同的能力來處理查詢負載。方案大小愈大，可用來處理查詢的資源就愈多。平均速率限制也會依方案大小而不同。將方案升級可提升效能。若要瞭解方案和限制，請參閱[{{site.data.keyword.discoveryshort}}定價方案](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)。 

### 查詢複雜性
{: #qp-query}

有許多方式可以對 {{site.data.keyword.discoveryshort}} 執行查詢，而所使用的不同作業會影響效能。影響效能的查詢特徵如下：

1.   **長度** - 查詢愈長，效能很有可能會愈差。 
1.   **聚集** - 聚集是比較複雜的查詢類型，有巢狀聚集對效能的影響最大。 
1.   **運算子** - 萬用字元和模糊符合會影響效能。
1.   **計數** - 減少傳回的文件計數會影響效能；如果您需要翻看結果，請使用 `offset` 參數。 
1.   **傳回欄位** - 將傳回的欄位限制為僅限應用程式所需的欄位會有所幫助（例如，除非需要標題和段落，否則不要傳回文件全文）。 

如需詳細資訊，請參閱[查詢參考資料](/docs/services/discovery?topic=discovery-query-reference#query-reference)。

### 使用的特性
{: #qp-features}

有些特性可加強查詢結果。影響效能的特性如下：
 
1.   **段落擷取** - 段落擷取會在文件中進行搜尋，以針對您的查詢尋找文字的相關 Snippet。您可以使用 `passages.fields` 參數來調整段落擷取搜尋之文件中的欄位；如果您的內容有很多欄位，這有助於減少段落擷取的延遲時間。如需「段落擷取」的相關資訊，請參閱[段落](/docs/services/discovery?topic=discovery-query-parameters#passages)。
1.   **相關性訓練** - 相關性訓練會運算集合中各個最上層文字欄位的特性（與 JSON 中 `document_id` 相同層次的欄位）。如果有很多最上層欄位，使用訓練時，這會對 `natural_language_query` 造成效能影響。減少最上層欄位數目可以提升效能。若要這麼做，可以透過正規化來執行，或是手動編輯 JSON，將對於尋找相關內容沒有幫助的欄位放在巢狀結構中。變更用於訓練的欄位對模型也有影響，所以您需要考量進行此變更對效能的影響，以及結果的精確度。如需相關性訓練的相關資訊，請參閱[改善結果相關性](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling)。
1.  **持續相關性訓練** - 持續相關性訓練會搜尋環境中的所有集合。環境中的集合愈多，對效能的影響就愈大。如需相關資訊，請參閱[持續相關性訓練](/docs/services/discovery?topic=discovery-crt#crt)。

### 集合大小和複雜性
{: #qp-collection} 

專用集合中的文件構成也會影響查詢效能：
1.  **文件總數** - 當快要達到「進階」方案大小的`文件數`上限時，效能就會受影響。 
1.  **文件大小** - 若為非常大的文件（大小為好幾 MB 的文件），每個要求都需要移動大量資料，這會對效能造成負面影響，尤其是在使用段落擷取和相關性訓練時。 
1.  **強化數目** - 強化會增加大量巢狀欄位，進而增加文件的複雜性。如果您的使用案例不需要強化，請考慮在汲取時將其停用。強化不會直接用於 `natural_language_query` 搜尋相關性。如需有關強化的詳細資料，請參閱[新增強化](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)。
