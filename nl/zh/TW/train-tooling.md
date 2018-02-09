---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-05"

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

# 利用工具來改善結果相關性

可以在 {{site.data.keyword.discoveryfull}} 服務中利用訓練來改善自然語言查詢結果的相關性。您可以使用 {{site.data.keyword.discoveryshort}} 工具或 {{site.data.keyword.discoveryshort}} API 來訓練您的專用集合。如果您偏好使用 API，請參閱[透過 API 來改善查詢結果的相關性](/docs/services/discovery/train.html)。
{: shortdesc}

相關性訓練為選用項目；如果您的查詢結果符合您的需求，則不需要進一步的訓練。如需建置訓練使用案例的概觀，請參閱此部落格文章：[如何善用 Revleupancy 訓練 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window}。

若要訓練 Watson，您需要：

  -   提供代表使用者輸入之查詢的查詢範例，以及
  -   提供評比，以指出每一個查詢有哪些結果相關，哪些不相關

當 Watson 有足夠的訓練輸入時，您所提供關於每一個查詢有哪些是好結果及壞結果的相關資訊，都會用來瞭解您的集合。Watson 不只是記憶，它還會從個別查詢的特定資訊中學習，並將偵測到的型樣套用至所有新查詢。這是使用機器學習 Watson 技術辦到的，它能夠在您的內容和問題中找到信號。套用訓練之後，{{site.data.keyword.discoveryshort}} 會將查詢結果重新排序，將最相關的結果顯示在最上面。當您新增更多訓練資料時，{{site.data.keyword.discoveryshort}} 在查詢結果的排序上應該會變得更準確。

訓練必須符合下列**最低**需求，{{site.data.keyword.discoveryshort}} 才能開始套用您的評比：

  - 您必須訓練至少 49 個查詢，或許更多。如果需要更多查詢才能訓練，Watson 會提供您意見。
  - 您應該將這兩個可用的評比套用至結果：`Relevant` 和 `Not relevant`。只有評比 `Relevant` 文件不會提供所需的資料。

**附註：**相關性訓練需要符合特定訓練資料需求才能生效。該服務會定期檢查訓練資料，以判斷是否符合這些需求，並根據任何變更而自動更新其本身。

**附註：**相關性訓練目前僅套用於專用集合中的自然語言查詢。它不適用於結構化的「{{site.data.keyword.discoveryshort}} 查詢語言」查詢。如需「{{site.data.keyword.discoveryshort}} 查詢語言」的相關資訊，請參閱[查詢概念](/docs/services/discovery/using.html)。

**附註：**每個環境最多有 4 個訓練的集合。  

## 新增查詢及評比結果的相關性

訓練包含三個部分：自然語言查詢、查詢的結果，以及您套用至這些結果的評比。

1.  在 {{site.data.keyword.discoveryshort}} 工具中，您可以從**建置查詢**畫面到達集合的訓練頁面。按一下右上方的**訓練 Watson 來改善結果**。您不需要在**建置查詢**畫面上輸入查詢，即可開始訓練。
1.  在**訓練 Watson** 畫面上，按一下**新增自然語言查詢**，例如："IBM Watson in Healthcare"，並新增它。確定查詢的撰寫方式是使用者所要求的方式。此外，撰寫訓練查詢時也應該在查詢與所需回答之間有某些詞彙重疊。當自然語言查詢執行時，這會改善起始結果。相關性訓練僅使用自然語言查詢，請勿輸入以「{{site.data.keyword.discoveryshort}} 查詢語言」撰寫的查詢。
1.  若要檢視查詢的結果，請按一下它旁邊的**評比結果**按鈕。如果您認為沒有足夠的結果，則可以嘗試重新撰寫查詢，或透過**管理資料**畫面，將更多文件新增至此集合。
1.  開始以 `Relevant` 或 `Not relevant` 來評比結果。完成時，按一下**回到查詢**。在 {{site.data.keyword.discoveryshort}} 工具中，`Relevant` 的評分為 `10`，`Not relevant` 的評分為 `0`。如果您已使用 API 來開始評比此集合的結果，並使用不同的評分標準，則會顯示警告，其中含有修正問題的選項。在畫面頂端，Watson 會為您追蹤訓練狀態，並提供您可以執行什麼動作來改善結果的一些提示。「在您的評比中增加更多變化」，表示您應該同時使用 `Relevant` 和 `Not relevant` 評比。一旦符合需求，訓練將開始定期更新。它在開始之後不到 30 分鐘就完成，而且當 Watson 更新時您仍然可以繼續工作。
1.  繼續新增查詢及評比結果。

若要隨時要回到**建置查詢**畫面，請按一下左上方的**建置查詢**。
{: tip}
若要回到**管理資料**畫面，請按一下右上方的集合名稱。
{: tip}

如果您要一次刪除集合中的所有訓練資料，則必須透過 API 來達成此目的。如需相關資訊，請參閱[刪除集合的所有訓練資料](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-all-training-data)。如需透過 API 進行訓練的相關資訊，請參閱[透過 API 來改善查詢結果的相關性](/docs/services/discovery/train.html)。

## 測試及反覆運算結果的相關性

當您完成評比結果且 Watson 已套用訓練之後，您應該進行測試，以查看查詢結果是否已改善。若要這麼做，請執行與訓練查詢相關（但不相同）的測試查詢。請查看測試查詢的結果是否已改善。

如果您想在測試之後進一步改善結果，則可以：
- 將更多文件新增至集合。
- 新增更多訓練查詢。
- 評比更多結果，並確保同時使用 `Relevant` 和 `Not relevant` 評比。

如需其他訓練指引，請參閱[相關性訓練提示](/docs/services/discovery/train-tips.html#relevancy-tips)。

## 信賴度評分
{: #confidence}

經過訓練的集合將在自然語言查詢的結果中傳回 `confidence` 評分。這個 `confidence` 數字是根據與訓練模型相較之下預估結果的相關程度計算而來。`confidence` 評分與 `score` **不**相同。如需決定信賴度評分臨界值的相關資訊，請參閱[如何選取使用信賴度評分的臨界值 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/watson/blog/2016/06/23/how-to-select-a-threshold-for-acting-using-confidence-scores/)。`score` 不應用於設定絕對臨界值，因為它是相對計算。

`confidence` 的範圍是從 0.0 到 1.0。數字越高，文件的相關性就越高。

在查詢結果中，可以在每份文件的 `result_metadata` 下找到 `confidence` 評分，例如：

```json
    "results": [
        {
            "id": "eea16dfd5fe6139a25324e7481a32f89_13",
            "result_metadata": {
                "confidence": 0.5893963975910735,
                "score": 0.5006834
            },
```
