---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-11"

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

# 利用工具來改善結果相關性
{: #improving-result-relevance-with-the-tooling}

可以在 {{site.data.keyword.discoveryfull}} 服務中利用訓練來改善自然語言查詢結果的相關性。您可以使用 {{site.data.keyword.discoveryshort}} 工具或 {{site.data.keyword.discoveryshort}} API 來訓練您的專用集合。如果您偏好使用 API，請參閱[透過 API 來改善查詢結果的相關性](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api)。
{: shortdesc}

相關性訓練為選用項目；如果您的查詢結果符合您的需求，則不需要進一步的訓練。如需建置訓練使用案例的概觀，請參閱此部落格文章：[如何善用 Revleupancy 訓練 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window}。

若要訓練 Watson，您需要：

  -   提供代表使用者輸入之查詢的查詢範例，以及
  -   提供評比，以指出每一個查詢有哪些結果相關，哪些不相關

當 Watson 有足夠的訓練輸入時，您所提供關於每一個查詢有哪些是好結果及壞結果的相關資訊，都會用來瞭解您的集合。Watson 不只是記憶，它還會從個別查詢的特定資訊中學習，並將偵測到的型樣套用至所有新查詢。這是使用機器學習 Watson 技術辦到的，它能夠在您的內容和問題中找到信號。套用訓練之後，{{site.data.keyword.discoveryshort}} 會將查詢結果重新排序，將最相關的結果顯示在最上面。當您新增更多訓練資料時，{{site.data.keyword.discoveryshort}} 在查詢結果的排序上應該會變得更準確。

**附註：**相關性訓練目前僅套用於專用集合中的自然語言查詢。它不適用於結構化的「{{site.data.keyword.discoveryshort}} 查詢語言」查詢。如需「{{site.data.keyword.discoveryshort}} 查詢語言」的相關資訊，請參閱[查詢概念](/docs/services/discovery?topic=discovery-query-concepts#query-concepts)。

在大部分情況下，所有專用集合都會在查詢結果中傳回 `confidence` 評分。如需詳細資料，請參閱[信賴度評分](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence)。

新增自訂停用字詞清單可以提高自然語言查詢結果的相關性。如需相關資訊，請參閱[定義停用字詞](/docs/services/discovery?topic=discovery-query-concepts#stopwords)。

如需訓練的最低需求及訓練限制，請參閱[訓練資料需求](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#reqs)。

如需追蹤用量以及使用此資料協助您瞭解及改善應用程式的詳細資料，請參閱[用量監視](/docs/services/discovery?topic=discovery-usage#usage)。

## 新增查詢及評比結果的相關性
{: #results}

訓練包含三個部分：自然語言查詢、查詢的結果，以及您套用至這些結果的評比。

1.  有兩種方式可以存取 {{site.data.keyword.discoveryshort}} 工具中的訓練頁面：
    - 對於個別集合，在**建置查詢**畫面上，按一下右上角的**訓練 Watson 以改善結果**。您不需要在**建置查詢**畫面上輸入查詢，即可開始訓練。 
    - 從「效能」儀表板，按一下左側的**檢視資料度量**圖示，以開啟儀表板。系統會提示您選擇集合來訓練。
1.  在**訓練 Watson** 畫面上，按一下**新增自然語言查詢**，例如："IBM Watson in Healthcare"，並新增它。確定查詢的撰寫方式是使用者所要求的方式。此外，撰寫訓練查詢時也應該在查詢與所需回答之間有某些詞彙重疊。當自然語言查詢執行時，這會改善起始結果。相關性訓練僅使用自然語言查詢，請勿輸入以「{{site.data.keyword.discoveryshort}} 查詢語言」撰寫的查詢。
1.  若要檢視查詢的結果，請按一下它旁邊的**評比結果**按鈕。如果您認為沒有足夠的結果，則可以嘗試重新撰寫查詢，或透過**管理資料**畫面，將更多文件新增至此集合。
1.  開始以 `Relevant` 或 `Not relevant` 來評比結果。完成時，按一下**回到查詢**。在 {{site.data.keyword.discoveryshort}} 工具中，`Relevant` 的評分為 `10`，`Not relevant` 的評分為 `0`。如果您已使用 API 來開始評比此集合的結果，並使用不同的評分標準，則會顯示警告，其中含有修正問題的選項。在畫面頂端，Watson 會為您追蹤訓練狀態，並提供您可以執行什麼動作來改善結果的一些提示。「在您的評比中增加更多變化」，表示您應該同時使用 `Relevant` 和 `Not relevant` 評比。一旦符合需求，訓練將開始定期更新。它在開始之後不到 30 分鐘就完成，而且當 Watson 更新時您仍然可以繼續工作。
1.  繼續新增查詢及評比結果。

若要隨時要回到**建置查詢**畫面，請按一下左上方的**建置查詢**。
{: tip}
若要回到**管理資料**畫面，請按一下右上方的集合名稱。
{: tip}

如果您要一次刪除集合中的所有訓練資料，則必須透過 API 來達成此目的。如需相關資訊，請參閱[刪除集合的所有訓練資料](https://{DomainName}/apidocs/discovery#delete-all-training-data)。如需透過 API 進行訓練的相關資訊，請參閱[透過 API 來改善查詢結果的相關性](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api)。

## 測試及反覆運算結果的相關性
{: #testing-results}

當您完成評比結果且 Watson 已套用訓練之後，您應該進行測試，以查看查詢結果是否已改善。若要這麼做，請執行與訓練查詢相關（但不相同）的測試查詢。請查看測試查詢的結果是否已改善。

如果您想在測試之後進一步改善結果，則可以：
- 將更多文件新增至集合。
- 新增更多訓練查詢。
- 評比更多結果，並確保同時使用 `Relevant` 和 `Not relevant` 評比。

如需其他訓練指引，請參閱[相關性訓練提示](/docs/services/discovery?topic=discovery-relevancy-tips#relevancy-tips)。

## 信賴度評分
{: #confidence}

{{site.data.keyword.discoveryshort}} 會針對自然語言查詢和以「{{site.data.keyword.discoveryshort}} 查詢語言」撰寫的查詢，傳回 `confidence` 評分。

針對已訓練和未訓練的專用集合，都會傳回 `confidence` 評分（未訓練集合的僅限過濾查詢除外）。此外，{{site.data.keyword.discoveryshort}} 還會傳回 `document_retrieval_strategy` 欄位，以指出 `confidence` 評分的來源： 
-  `untrained`
-  `relevancy_training` 或
-  `continuous_relevancy_training`

`document_retrieval_strategy` 可搭配 `confidence` 評分一起使用，以判斷應如何使用所提供的結果。在負載量大的情況下，所傳回的 `document_retrieval_strategy` 可能是 `untrained`，即使集合已經過訓練也一樣。

`confidence` 的範圍是從 0.0 到 1.0。數字越高，文件的相關性就越高。

在查詢結果中，可以在每份文件的 `result_metadata` 下找到 `confidence` 評分。`document_retrieval_strategy` 會列示在 `retrieval_details` 之下。

```json
{
  "matching_results": 4,
  "session_token": "1_2gYuWJyaWx792Ni4_DQ4C5cbnW",
  "retrieval_details" : {
    "document_retrieval_strategy" : "relevancy_training",
  },
  "results": [
    {
      "id": "eea16dfd5fe6139a25324e7481a32f89_13",
            "result_metadata": {
                "confidence": 0.5893963975910735,
        "score": 0.5006834
      }
    }
  ]
}
```
{: codeblock}

若為已訓練的集合，`confidence` 數值是根據與已訓練模型相較之下預估結果的相關程度來計算。已訓練的集合只會針對自然語言查詢計算 `confidence` 評分。如果您使用「{{site.data.keyword.discoveryshort}} 查詢語言」來查詢已訓練的集合，或是訓練模型暫時無法使用，所傳回的 `confidence` 數值會有 `untrained` 的 `document_retrieval_strategy`。如果結果具有 `untrained` 的 `document_retrieval_strategy`，則 `confidence` 評分為文件結果與查詢相關程度的未監督預估值；此值與針對已訓練集合傳回的評分不可交換。與未訓練的集合相較，已訓練的集合可以為自然語言查詢提供更好的答案。

請注意，`confidence` 評分與 `score` **不同**。如需決定信賴度評分臨界值的相關資訊，請參閱[如何選取使用信賴度評分的臨界值 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/watson/blog/2016/06/23/how-to-select-a-threshold-for-acting-using-confidence-scores/)。`score` 不應用於設定絕對臨界值，因為它是相對計算。相反地，建議應用程式一律對所有不含 `confidence` 欄位的結果執行相同的行為。例如，應用程式可以顯示所有不含 `confidence` 欄位的結果或隱藏所有不含 `confidence` 欄位的結果，但不應該使用 `score` 的值來顯示部分結果並隱藏其他結果。由於擷取方法不同，計算 `confidence` 的方式也會不同，所以在設定臨界值時，應該要考量 `document_retrieval_strategy`，而且在訓練之前和之後都要檢閱其值。

如需查詢的相關資訊，請參閱[開始使用查詢](/docs/services/discovery?topic=discovery-getting-started-with-querying#getting-started-with-querying)。

如需受監督訓練方法的相關資訊，請參閱：
-  [相關性訓練](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling)和
-  [持續相關性訓練](/docs/services/discovery?topic=discovery-crt#crt)
