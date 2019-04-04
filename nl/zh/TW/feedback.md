---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-17"

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

# 使用情形監視
{: #usage}

您可以監視及追蹤 {{site.data.keyword.discoveryshort}} 實例的使用情形，並使用此資料來協助您瞭解及改善應用程式。[事件 API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery#create-event){: new_window} 可用來建立與特定自然語言查詢和動作相關聯的日誌項目。例如，您可以記錄使用者「點按」了結果集裡的哪些文件，以及何時進行點按。

**附註：**僅針對專用資料集合的自然語言查詢監視日誌和事件。並不會在 {{site.data.keyword.discoverynewsfull}} 上收集任何日誌。

{{site.data.keyword.discoveryshort}} 可記載下列資訊：
- **查詢** - 針對環境中的集合所執行的自然語言查詢 
- **效果**（或**結果**） -  針對特定查詢而傳回的結果（通常是文件或段落） 
- **事件** - 使用者對 {{site.data.keyword.discoveryshort}} 的結果或結果集執行的互動（例如，按一下文件結果）

系統會自動記載**查詢**和**效果**；**事件**記載可透過 API 整合到應用程式中。

## 檢視日誌
{: #viewlogs}

您可以搜尋查詢和事件日誌，以尋找符合所指定準則的查詢階段作業。搜尋 `logs` 端點時會針對受支援的參數使用標準的 {{site.data.keyword.discoveryshort}} 查詢語法。端點提供基本查詢功能來檢視及搜尋所記錄的資料。  

`/api/v1/logs` 端點支援下列 {{site.data.keyword.discoveryshort}} 查詢參數。
- query 
- filter
- sort
- count 
- offset
- version

如需參數功能和語法的其他詳細資料，請參閱[查詢參數](/docs/services/discovery?topic=discovery-query-parameters#query-parameters)。

搜尋日誌中包含 "train" 一詞之自然語言查詢的範例：

`https://gateway.watsonplatform.net/discovery/api/v1/logs?version=2018-03-28&query=train`

`logs` 查詢的回應包含的結果類似 {{site.data.keyword.discoveryshort}} 文件結果。每個結果將是查詢或事件（在文件 `type` 欄位中指定）。  

範例查詢日誌：

```
{
            "customer_id": "",
            "environment_id": "252e6e82-c2d2-450e-9670-0008b0a3a99c",
            "natural_language_query": "how do i get from the airport to the city",
            "query_id": "_Qs35yOoa7",
            "document_results": {
                "count": 2,
                "results": [
                    {
                        "collection_id": "af9e1f41-6114-4d77-bca6-c9b99b2601b1",
                        "score": 6.724753491503856,
                        "position": 1,
                        "document_id": "4193eaa727d79b0f74597356dbcbb9a7"
                    },
                    {
                        "collection_id": "af9e1f41-6114-4d77-bca6-c9b99b2601b1",
                        "score": 5.791631414211986,
                        "position": 2,
                        "document_id": "bdcd6a9cc1438a3faa8c925f6a8d9429"
                    }
                ]
            },
            "event_type": "query",
            "session_token": "1_LKczxWGEWx5TJAi1_Qs35yOoa7",
            "created_timestamp": "2018-09-12T05:20:07.469Z"
        }
```

透過查詢日誌，您可以調查傳回給一般使用者的結果類型，並探索如何利用 {{site.data.keyword.discoveryshort}} 中提供的方法來改善結果品質。例如： 
- 相關性訓練，請參閱[利用 API 來改善結果相關性](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api)及[利用工具來改善結果相關性](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling)
- [查詢運算子](/docs/services/discovery?topic=discovery-query-operators#query-operators)
- [查詢擴展](/docs/services/discovery?topic=discovery-query-concepts#query-expansion)
- 自訂配置，請參閱[配置參考資料](/docs/services/discovery?topic=discovery-configref#configref)

## 建立事件日誌
{: #eventlogs}

事件日誌用來追蹤使用者在應用程式內的互動。這可幫助您瞭解應用程式執行的情況，以及識別您需要聚焦在哪些方面才能改善結果。{{site.data.keyword.discoveryshort}} 提供可內嵌在應用程式中以追蹤事件的 API。當使用者執行動作時，使用適當的資訊來呼叫這個 API，會將信號傳回給 {{site.data.keyword.discoveryshort}}，然後可在日誌中檢視該信號。 

事件可以協助收集運算度量值的相關資訊（如點閱率）來測量應用程式在協助一般使用者尋找相關資訊時的效果，也可以透過檢閱查詢和點按來協助進行種子訓練，以開始建置基準。 

您可以在使用者與結果互動的任何位置新增此 API。例如，在搜尋使用者介面中，當使用者按一下文件鏈結時，您可以新增它，或是在聊天機器人介面中，當使用者按一下**展開**或**更多詳細資料**按鈕時，您可以使用它來進行追蹤。

{{site.data.keyword.discoveryshort}} 結果將傳回可用來追蹤事件的其他資訊，包括階段作業記號。 

`"matching_results": 179,`
`"session_token": "1_LKczxWGEWx59fYD0_VV8HFUpb6"`

若要記錄事件，請對 `/api/v1/events` 端點發出 POST。如需詳細資料，請參閱[事件 API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery#create-event){: new_window}。

記錄事件之後，可以使用 `/api/v1/logs` 端點將它再讀取出來。請使用 `session_token`，將事件加入至相關聯的查詢中。
