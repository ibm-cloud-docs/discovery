---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-25"

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

# 持續相關性訓練
{: #crt}

「{{site.data.keyword.discoveryshort}} 持續相關性訓練」可以從使用者行為自動學習，這大幅減少了改善結果相關性分級所需的工作。它使用來自使用者的互動，以學習如何顯示最相關的結果。它可以從互動（例如點按）中學習，判斷哪些結果對使用者最有價值，並揭露對未來查詢最重要的信號。「持續相關性訓練」會將文件重新分級，在結果的頂端顯示最相關的資訊。它的用途如下：

- 根據支援專員點按的結果，為支援專員協助改善結果的相關性
- 根據所選取的長尾結果，在客戶聊天機器人中顯示更相關的結果 
- 根據專家探索的結果，提供更相關的回應

若要設定「持續相關性訓練」：

- 「持續相關性訓練」只能在環境層次啟用。查詢必須使用 `/api/v1/environment/{environment_id}/query` 或 `/api/v1/environments/{environment_id}/query` 端點，才能查詢一個以上的集合。
- 由於使用 {{site.data.keyword.discoveryshort}} `事件`（點按）來建立所需的訓練資料，因此請先整合事件追蹤。如需詳細資料，請參閱[使用情形監視](/docs/services/discovery?topic=discovery-usage#usage)。
- 若要開始「持續相關性訓練」，需要最少 1000 個具有相關聯點按事件的自然語言查詢。實例的事件及日誌將保留 30 天，因此，在該期間內必須收集 1000 個點按。
- 「持續相關性訓練」可用於大小為 `Small` 以上的「進階」方案，以及「超值」方案。它不適用於`精簡`方案。
- 「持續相關性訓練」的集合數限制為 `5`。因為「持續相關性訓練」可以在多個集合之間運作，所以可能延長查詢和訓練時間。
- 「持續相關性訓練」只會發生在最上層欄位，而且在訓練處理程序中可以使用多少個欄位也有限制。如果有超過 `10` 個最上層欄位，訓練比較可能會發生錯誤。 

若要使用「持續相關性訓練」：

訓練之後，當使用環境層次查詢時，會使用「持續相關性訓練」來影響 `natural_language_query` 的結果。 

透過在環境的所有集合之間執行多個集合的 `natural_language_query`，即可在查詢時使用「持續相關性訓練」。如需指示，請參閱[查詢多個集合](/docs/services/discovery?topic=discovery-query-concepts#multiple-collections)。 

**附註：**「持續相關性訓練」不影響對已訓練或未訓練之集合層次 (`/v1/environments/{environment_id}/collections/{collection_id}/query`) 查詢呼叫所做的查詢。 

追蹤狀態：

您可以從 `/api/v1/environments` 端點檢視「持續相關性訓練」的狀態。請參閱 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery#get-environment-info){: new_window}。`status` 會提供訓練作業狀態的相關資訊，並在「持續相關性訓練」為作用中時通知您：

```
"search_status" : [
        {
            "scope" : "environment",
            "status" : "NO_DATA",
            "status_description" : "Discovery is employing a default strategy for document search natural_language_query. Enable query and event logging so we can initiate relevancy training to improve search accuracy.”
        }
    ]
```
