---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-25"

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

# 使用效能儀表板來檢視度量值及改善查詢結果
{: #performance-dashboard}

{{site.data.keyword.discoveryshort}} 工具中的「效能」儀表板可用來檢視查詢度量值，以及改善查詢結果（包括查詢相關性）。

您可以按一下左側的**檢視資料度量值**圖示來存取「效能」儀表板。此儀表板不適用於「超值」或「專用」環境。

有兩個選項可改善自然語言查詢結果：
- [新增更多資料來修正沒有結果的查詢](/docs/services/discovery/dashboard.html#addmore)
- [訓練您的資料以將相關結果置於頂端](/docs/services/discovery/dashboard.html#traindata)

您可以在[查詢概觀](/docs/services/discovery/dashboard.html#overview)中檢視資料度量值。 

## 新增更多資料來修正沒有結果的查詢
{: #addmore}

在儀表板的這個區段中，您可以檢閱傳回零個結果的查詢，並新增更多資料，使查詢未來能傳回結果。請按一下**檢視全部並新增資料**按鈕，以開始進行。 

## 訓練您的資料以將相關結果置於頂端
{: #traindata}

在這個區段中，您可以訓練集合，以改善自然語言查詢結果的相關性。請按一下**檢視全部並執行相關性訓練**按鈕，以開始進行。然後，請參閱[新增查詢並將結果的相關性分級](/docs/services/discovery/train-tooling.html#results)，以取得指示。

如需訓練需求與選項的相關資訊，請參閱[利用工具來改善結果相關性](/docs/services/discovery/train-tooling.html)。

## 查詢概觀
{: #overview}

「查詢概觀」區段會顯示：
- 使用者所發出的查詢總數
- 點按一個以上結果的查詢百分比
- 未點按結果的查詢百分比
- 未傳回結果的查詢百分比
- 隨著時間顯示這些結果的圖形，它可讓您追蹤新增更多資料和相關性訓練對於效能的改善情況

這些結果是使用事件及意見 API 加以收集。如需相關資訊，請參閱 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#events-and-feedback-api)。
