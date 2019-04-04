---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-08"

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

# 版本注意事項
{: #release-notes}

版本注意事項提供自舊版以來 {{site.data.keyword.discoveryfull}} 服務變更的相關資訊。
{: shortdesc}

## 服務 API 版本化
{: #apiversioning}

API 要求需要以 `version=YYYY-MM-DD` 格式採用日期的版本參數。每當我們變更 API 的方式與舊版不相容時，我們就會發行該 API 新的次要版本。

請隨每一個 API 要求傳送版本參數。服務會使用您指定日期的 API 版本，或該日期之前的最新版本。不要預設為現行日期。請改為指定符合您應用程式相容版本的日期，而且在您的應用程式備妥可用於較新版本之前，請勿變更此日期。

現行版本為 `2019-01-01`。

## 測試版特性
{: #beta-features}

IBM 將提供分類為測試版或實驗性的服務、特性及語言支援。這些功能可能不穩定，可能會經常變更，因此可能一經通知就停止使用。它們是為了讓您評估其功能而提供。測試版或實驗性功能可能未提供一般發行功能所提供的相同效能或相容性層次。這些功能並非設計用於正式作業環境，如有這類使用需由您自行承擔風險。


## 變更
{: #change-log}

該服務有下列新增特性和變更。

## 2019 年 2 月 10 日
{: #10feb19}

- 新增連接至 IBM Cloud Object Storage 並與其同步的選項。此資料來源無法用於「專用」環境。如需相關資訊，請參閱 [IBM Cloud Object Storage](/docs/services/discovery?topic=discovery-sources#connectcos)。

## 2019 年 2 月 4 日
{: #4feb19}

更新至通用版

-  [智慧型文件理解 (SDU)](/docs/services/discovery?topic=discovery-sdu#sdu) 已從測試版狀態移至 GA 狀態。
   -  表格標註仍在測試版狀態。可以在[這裡](/docs/services/discovery?topic=discovery-release-notes#beta-features)找到說明測試版特性的陳述。
   -  右上方的`資料設定`按鈕已更名為`配置資料`。
   -  上傳文件時不再需要存取`配置資料`（以前稱為`資料設定`）按鈕。

SDU 測試版發表於 [2019 年 1 月 22 日](/docs/services/discovery?topic=discovery-release-notes#22jan19)。   
    
## 2019 年 1 月 28 日
{: #28jan19}

如果您將「資料搜索器」用於 {{site.data.keyword.discoveryshort}} 連接器支援的資料來源，則不再為其提供協助。
{{site.data.keyword.discoveryshort}} 連接器支援搜索 Box、SharePoint、Salesforce 等等。如需詳細資訊，請參閱[連接至資料來源](/docs/services/discovery?topic=discovery-sources#sources)。「資料搜索器」應該只用來搜索檔案共用或資料庫，針對所有其他用途，請使用 {{site.data.keyword.discoveryshort}} 連接器。將大量檔案上傳至 {{site.data.keyword.discoveryshort}} 的另一個選項，就是 GitHub 上的 [discovery-files ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/IBM/discovery-files){: new_window}。


## 2019 年 1 月 22 日
{: #22jan19}

- 發行[智慧型文件理解 (SDU)](/docs/services/discovery?topic=discovery-sdu#sdu) 測試版，這是訓練 {{site.data.keyword.discoveryfull}} 在您的文件中擷取自訂欄位的新方法。透過「智慧型文件理解」，您可以在文件中標註欄位，以訓練自訂轉換模型。可以在[這裡](/docs/services/discovery?topic=discovery-release-notes#beta-features)找到說明測試版特性的陳述。

測試版 SDU 編輯器僅適用於包含支援的文件類型且未套用「元素分類」強化的新集合。現有的「專用」集合會使用原始配置方法。

如果您之前是使用已結束的「智慧型文件理解」測試版，請勿將在該測試版中建立的模型匯入此版本中。「智慧型文件理解」目前無法用於「專用」環境。

SDU 編輯器功能僅於 {{site.data.keyword.discoveryshort}} 工具中提供，未於 API 中提供。

## 2019 年 1 月 15 日
{: #15jan19}

「元素分類」更新項目：
-  「元素分類」強化已更新 API `2018-10-15` 版或更新版本中的參與方、種類和屬性。請參閱[剖析合約](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing)，以瞭解更新項目。

- `/v1/element_classification` 方法的輸出現在包含下列項目：
    - `parties` 陣列現在包含 `importance` 欄位，指出參與方為 `Primary` 參與方或 `Unknown`（非主要）參與方。
    - `effective_dates`、`contract_amounts` 和 `termination_dates` 陣列現在各包含一個 `confidence_level` 欄位，指出 `High`、`Medium` 或 `Low` 值。如需相關資訊，請參閱[元素分類](/docs/services/discovery?topic=discovery-output_schema#output_schema)和[剖析合約](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing)。

    {{site.data.keyword.discoveryshort}} 工具尚未使用現行 API 版本：`2019-01-01`（其目前使用 `2018-08-01`），所以您不會在 {{site.data.keyword.discoveryshort}} 工具的「元素分類」輸出中看到這些新欄位。

## 2019 年 1 月 10 日
{: #10jan19}

已知問題：

-  如果您使用[指定 `customer_id`](/docs/services/discovery?topic=discovery-sources#source_customer_id) 中說明的正規化方法來指定 `customer-id`，後續又試圖使用[刪除標示的資料](/docs/services/discovery?topic=discovery-information-security#deletingdata)中說明的方法來刪除包含該 `customer_id` 的文件，將不會刪除相關聯的來源文件。

## 2019 年 1 月 1 日
{: #1jan19}

- 所有 API 呼叫的版本字串已從 `2018-12-03` 變更為 `2019-01-01`。此版本建立一個新的文件汲取狀態：`pending`。針對已接受但尚未開始處理的文件，將會傳回 `pending` 狀態。之前這些文件的狀態為 `processing`。{{site.data.keyword.discoveryshort}} 工具尚未使用此 API 版本（其目前使用 `2018-08-01`），所以當您在 {{site.data.keyword.discoveryshort}} 工具中檢查文件狀態時，將不會傳回 `pending` 狀態。

## 2018 年 12 月 21 日
{: #21dec18}

- 新增連接至 Microsoft SharePoint 2016 On-Premise 並與其同步的選項。此資料來源無法使用於「專用」環境。如需相關資訊，請參閱 [SharePoint 2016 On-Premise](/docs/services/discovery?topic=discovery-sources#connectsp_op)。

- 新增測試版 Web 搜索連接器，其可用來連接、搜索網站，以及與其同步。此資料來源無法使用於「專用」環境。如需相關資訊，請參閱 [Web 搜索](/docs/services/discovery?topic=discovery-sources#connectwebcrawl)。可以在[這裡](/docs/services/discovery?topic=discovery-release-notes#beta-features)找到說明測試版特性的陳述。

- Microsoft SharePoint Online、Salesforce 和 Box 資料來源現在可用於「超值」環境，無法用於「專用」環境。

## 2018 年 12 月 17 日
{: #17dec18}

- 新增義大利文的完整支援。如需相關資訊，請參閱[語言支援](/docs/services/discovery?topic=discovery-language-support#language-support)。

## 2018 年 12 月 14 日
{: #14dec18}

您現在可以建立託管於倫敦資料中心的 {{site.data.keyword.discoveryshort}} 服務實例，而不需聯合供稿。就像所有位置一樣，{{site.data.keyword.cloud}} 倫敦位置 (eu-gb) 也是使用記號型 Identity and Access Management (IAM) 鑑別。您在此位置建立的所有新服務實例都是使用 IAM 鑑別。

## 2018 年 12 月 12 日
{: #12dec18}

- 新增定義及上傳自訂停用字詞清單的功能。自訂停用字詞是使用 {{site.data.keyword.discoveryshort}} API 來實作。如需詳細資訊，請參閱[定義停用字詞](/docs/services/discovery?topic=discovery-query-concepts#stopwords)。 

## 2018 年 12 月 3 日
{: #3dec18}

- 針對使用 `2018-12-03` 或以上版本 API 來撰寫的所有查詢（僅限過濾的查詢除外），{{site.data.keyword.discoveryshort}} 現在會在查詢結果集中傳回 `confidence` 評分，即使該集合之前不是使用受監督的訓練方法（例如[相關性訓練](//docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling)或[持續相關性訓練](/docs/services/discovery?topic=discovery-crt#crt)）來進行訓練也一樣。此外，{{site.data.keyword.discoveryshort}} 還會傳回 `document_retrieval_strategy` 欄位，以指出 `untrained`、`relevancy_training` 或 `continuous_relevancy_training` 的 `confidence` 評分來源。如需相關資訊，請參閱[信任評分](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence)。

- 所有 API 呼叫的版本字串已從 `2018-10-15` 變更為 `2018-12-03`。{{site.data.keyword.discoveryshort}} 工具尚未使用此 API 版本（其目前使用 `2018-08-01`），所以使用{{site.data.keyword.discoveryshort}} 工具來撰寫的查詢不會針對未訓練的集合傳回 `confidence` 評分。

## 2018 年 11 月 8 日
{: #8nov18}

- {{site.data.keyword.discoveryshort}} 已在 2018 年 11 月 8 日於 `Tokyo` 位置推出。「超值」和「專用」環境目前無法用於 `Tokyo`。

## 2018 年 10 月 30 日
{: #30oct18}

- {{site.data.keyword.discoveryshort}} 服務現在可在所有地區支援記號型 Identity and Access Management (IAM) 鑑別。IAM 會使用存取記號（而非服務認證）來進行服務鑑別。如需將 IAM 記號與現有及新應用程式搭配使用的相關資訊，請參閱 [2018 年 5 月 17 日](#17May18)版本更新。

## 2018 年 10 月 25 日
{: #25oct18}

已變更[元素分類](/docs/services/discovery?topic=discovery-element-classification#element-classification)強化的綱目。如果您想要使用更新的綱目，您必須使用版本日期為 `2018-10-15` 或該日期之後的 API 來汲取您的文件。{{site.data.keyword.discoveryshort}} 工具尚未使用此 API 版本（它目前使用 `2018-08-01`），因此使用 {{site.data.keyword.discoveryshort}} 工具汲取的文件將利用原始綱目來強化。

## 2018 年 10 月 24 日
{: #24oct18}

- {{site.data.keyword.discoverynewsfull}} 查詢會在 `text` JSON 欄位中顯示每篇文章的大約 50 個字。這些字現在是從強調顯示內容擷取出來，而不只是顯示文章的前 50 個字。請參閱[強調顯示](/docs/services/discovery?topic=discovery-query-parameters#highlight)，以瞭解強調顯示的說明。不需要將強調顯示內容明確地包含在您的查詢中來啟用此行為。

## 2018 年 9 月 25 日
{: #25sept18}

- 已發行連續相關性訓練，其可利用使用者的互動，學習如何顯露出最相關的結果。它可以自動從使用者行為學習，大幅減少改善結果相關性評等所需的工作量。如需詳細資料，請參閱[持續相關性訓練](/docs/services/discovery?topic=discovery-crt#crt)。

- 已新增 API 支援以執行較長的查詢。這會將字元限制增加到 10,000 個字元，讓您可以在查詢中增加過濾器數目，以及執行更複雜的聚集。如需詳細資料，請參閱位於 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery#long-collection-queries){: new_window} 和 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery#long-environment-queries){: new_window} 的 POST 查詢。

- 您現在可以使用 API 來升級您的「進階」方案。如需詳細資料，請參閱[升級方案](/docs/services/discovery?topic=discovery-upgrading-your-plan#switchadvanced)。 

- 「元素分類」強化已更新分類的元素、合約元素以及識別的參與方和表格。如需相關更新，請參閱[元素分類](/docs/services/discovery?topic=discovery-element-classification#element-classification)。

- 已新增巴西葡萄牙文的完整支援。如需相關資訊，請參閱[語言支援](/docs/services/discovery?topic=discovery-language-support#language-support)。

- 查詢 API (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`) 現在支援 `bias` 參數，該參數可讓您偏向某些結果，例如最近發佈的文件。如需相關資訊，請參閱 API 參考資料中的[查詢集合 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window} 方法。

- 提供用來強化[元素分類](/docs/services/discovery?topic=discovery-element-classification#element-collection)集合的 **Default Contract Configuration** 檔被發現具有 HTML 正規化的問題。這個版本隨附了新的 **Default Contract Configuration**。請遵循下列步驟，將新的 **Default Contract Configuration** 套用到您的集合。

     1. 找出哪些集合正在使用 **Default Contract Configuration** 配置檔，或是以 **Default Contract Configuration** 為基礎的自訂配置。
     1. 記下您對以 **Default Contract Configuration** 為基礎之任何自訂配置所做的變更。
     1. 您必須從環境中刪除舊的 **Default Contract Configuration** 檔，才能使用新的檔案，因此，請使用 API [刪除配置 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery#delete-a-configuration){: new_window} 來刪除與任何集合相關聯的現行 **Default Contract Configuration**。同時也請刪除以舊 **Default Contract Configuration** 為基礎的任何配置。
     1. 現在，您可以使用新的 **Default Contract Configuration** 檔。對於使用上述其中一個配置的每個集合，建立新的集合。請套用新的 **Default Contract Configuration**，或是使用步驟 2 所做的記錄，根據新的 **Default Contract Configuration** 來建立新的自訂配置。
     1. 將先前汲取的檔案上傳至原始集合。
     1. 刪除舊集合。

## 2018 年 8 月 15 日
{: #15aug18}

- 有兩個新的查詢運算子可供使用。`Exists` (`:*`) 可用來傳回所有存在指定 `field` 的結果。`Does not exist` (`!*`) 可用來傳回所有未包含指定 `field` 的結果。如需相關資訊，請參閱[查詢運算子](/docs/services/discovery?topic=discovery-query-operators#query-operators)。 

## 2018 年 8 月 2 日
{: #2aug18}

- {{site.data.keyword.discoveryfull}} 在使用 {{site.data.keyword.discoveryshort}} 工具連接並同步到 Box、Salesforce 及 SharePoint Online 時，目前支援英文、西班牙文、德文、義大利文、葡萄牙文、法文、阿拉伯文、韓文及日文語言集合。 

## 2018 年 7 月 31 日
{: #31jul18}
 
 - 從 **2018 年 8 月 1 日**開始，{{site.data.keyword.discoveryfull}} 具有新的計價結構。它的特色是更簡單的定價模型（文件小時數不再是計算的一部分），以及用於 {{site.data.keyword.discoverynewsfull}} 查詢的分層定價。此外，「標準」方案已下架，而「精簡」方案降低了文件和 {{site.data.keyword.discoverynewsshort}} 查詢限制。定價變更不需要由現行 {{site.data.keyword.discoverynewsshort}} 使用者執行任何動作。如需詳細資料，請參閱 [{{site.data.keyword.discoveryshort}} 定價方案](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)。
 
**附註：**API 的版本日期已更新為 `2018-08-01`。若要利用新的環境調整大小選項（`LT`、`XS`、`S`、`MS`、`M`、`ML`、`L`、`XL`、`XXL`、`XXXL`），您必須在使用 API 建立環境時使用此版本日期。環境大小的類型現在是 `string`（之前類型為 `integer`。）

## 2018 年 7 月 27 日
{: #27jul18}

- 已發行另一種語言的 [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news)：日文 (`collection_id`: `news-ja`)。{{site.data.keyword.discoverynewsfull}} 也提供英文版、西班牙文版、德文版及韓文版。

## 2018 年 6 月 25 日
{: #25jun18}

- 已新增選項來連接至 Salesforce、Microsoft SharePoint Online 及 Box 資料來源並與其同步。在「超值」環境中無法使用這些資料來源。已發行這些資料來源的 [來源認證 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery#list-credentials){: new_window} 和 [配置 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery#add-configuration){: new_window} API。 
  - {{site.data.keyword.discoveryfull}} 在使用 {{site.data.keyword.discoveryshort}} 工具連接並同步到 Box、Salesforce 及 SharePoint Online 時，僅支援英文語言集合。[已解決](/docs/services/discovery?topic=discovery-release-notes#2aug18)
  - Box、Salesforce 及 SharePoint Online 的個別文件檔案大小限制為 10MB。
- 已在 {{site.data.keyword.discoveryshort}} 工具中新增「效能」儀表板。請參閱[使用效能儀表板檢視度量並改善查詢結果](/docs/services/discovery?topic=discovery-performance-dashboard#performance-dashboard)。新的儀表板在「超值」環境或「專用」環境中無法使用。
- 已新增日文的完整支援。如需相關資訊，請參閱[語言支援](/docs/services/discovery?topic=discovery-language-support#language-support)。

## 2018 年 6 月 22 日
{: #22jun18}

- 已發行事件及意見 API。如需相關資訊，請參閱[API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery#create-event){: new_window}。

## 2018 年 6 月 11 日
{: #11jun18}

-  對於華盛頓特區（美國東部）中管理的應用程式，服務現在支援記號型 Identity and Access Management (IAM) 鑑別。IAM 會使用存取記號（而非服務認證）來進行服務鑑別。如需將 IAM 記號與現有及新應用程式搭配使用的相關資訊，請參閱 [2018 年 5 月 17 日](#17May18)版本更新。
-  現在，「元素分類」支援其他合約元素：`Safety and Security`。如需詳細資料，請參閱[瞭解合約元素](/docs/services/discovery?topic=discovery-element-classification#contract-elements)。

## 2018 年 6 月 6 日
{: #6jun18}

- {{site.data.keyword.discoverynewsfull}} 查詢現在會於 `text` JSON 欄位中顯示每篇文章的前 50 個字。[更新](#24oct18)

## 2018 年 6 月 5 日
{: #5jun18}

- 「元素分類」現在提供給「超值」方案的訂閱者使用。
- `Low` 的 `assurance` 分級不再適用於「元素分類」。

## 2018 年 5 月 31 日
{: #31may18}

- 已新增法文的完整支援。如需相關資訊，請參閱[語言支援](/docs/services/discovery?topic=discovery-language-support#language-support)。

## 2018 年 5 月 30 日
{: #30may18}

- 已修正 {{site.data.keyword.discoverynewsfull}} 中的已知問題。之前，當查詢 {{site.data.keyword.discoverynewsshort}} 時，可能會收到不正確的文件計數，因為其他語言中的文件會與您所要求的語言一起計算。不會再出現這種情況。
- 從 `22 May 2018` 及該日期之後建立的集合開始，{{site.data.keyword.discoveryshort}} 現在會傳回包含下列語言之特殊字元的查詢結果：英文、德文、法文、荷蘭文、義大利文及葡萄牙文。比方說，如果您查詢 `aqui`，現在會同時收到 `aqui` 和 <code>aqu&iacute;</code> 的結果。

## 2018 年 5 月 21 日
{: #21may18}

- 已發行另一種語言的 [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news)：德文 (`collection_id`: `news-de`)。{{site.data.keyword.discoverynewsfull}} 也提供英文、西班牙文及韓文。

## 2018 年 5 月 17 日
{: #17May18}

- {{site.data.keyword.discoverynewsfull}} 查詢現在會於 `text` JSON 欄位中顯示每篇文章的前 20 個字。

-   針對 2018 年 5 月 15 日起雪梨 (**au-syd**) 所管理之應用程式的服務實例，服務現在支援新的 API 鑑別處理程序。對於其他地區中所管理的應用程式，將會盡快啟用這些處理程序。{{site.data.keyword.Bluemix}} 正在移轉至記號型 Identity and Access Management (IAM) 鑑別。IAM 會使用存取記號（而非服務認證）來進行服務鑑別。

   在雪梨位置，您會針對下列項目將 IAM 存取記號與 {{site.data.keyword.discoveryshort}} 服務搭配使用：

    -   在 5 月 15 日之後建立的*新服務實例*。如需相關資訊，請參閱[使用 IAM 記號進行鑑別](/docs/services/watson/getting-started-iam.html)。
    -   您從 Cloud Foundry 移轉至「資源控制器 (RC)」所管理之資源群組的*現有服務實例*。5 月 15 日之前建立的服務實例會繼續使用服務認證進行鑑別，直到您移轉它們為止。如需相關資訊，請參閱[將 Cloud Foundry 服務實例移轉至資源群組](/docs/resources/instance_migration.html)。

    其他地區中的所有新增和現有服務實例則會繼續使用服務認證（`apikey:{apikey_value}`）進行鑑別。

### 使用 IAM 存取記號來進行鑑別
{: #iam-token}

使用 IAM 存取記號時，您會在將要求傳送至 {{site.data.keyword.discoveryshort}} 服務之前進行鑑別。

1.  從 IBM Cloud 取得 API 金鑰。使用該金鑰來產生 IAM 存取記號。如需相關資訊，請參閱[如何使用 {{site.data.keyword.watson}} 服務 API 金鑰來取得 IAM 記號](/docs/services/watson/getting-started-iam.html#iamtoken)。
1.  使用 `Authorization` 標頭，將 IAM 存取記號傳遞給 {{site.data.keyword.discoveryshort}} 服務。在此標頭中，請指定 `Authorization: Bearer {access_token}` 來指出存取記號是 `Bearer` 記號。

    下列簡單 cURL 範例使用存取記號：

    ```bash
    curl -X GET
    --header "Authorization: Bearer eyJhbGciOiJIUz......sgrKIi8hdFs"
    "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    如需相關資訊，請參閱[使用記號來進行鑑別](/docs/services/watson/getting-started-iam.html#use_token)。

### 重新整理 IAM 存取記號
{: #iam-refreshing}

您產生的 IAM 存取記號具有下列結構。您可以使用 `access_token` 欄位的值，對服務發出經過鑑別的要求。

```javascript
{
  "access_token": "eyJhbGciOiJIUz......sgrKIi8hdFs",
  "refresh_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353
}
```
{: codeblock}

存取記號的存活時間有限。`expires_in` 欄位指出記號持續存在多久（在此案例中為一小時）。`expiration` 欄位會以指定 1970 年 1 月 1 日（UTC/GMT 午夜）以來秒數的 UNIX 時間戳記，顯示記號的到期時間。

在您的應用程式中，檢查存取記號的有效期限，然後使用它來發出經過鑑別的要求。如果已過期，您必須先重新整理存取記號，然後才能使用它。您可以使用 `refresh_token` 欄位的值來重新整理存取記號。如需相關資訊，請參閱[重新整理記號](/docs/services/watson/getting-started-iam.html#refresh_token)。


## 2018 年 5 月 11 日
{: #11may18}

- 您可以在這裡找到資訊安全的詳細資料：[資訊安全](/docs/services/discovery?topic=discovery-information-security#information-security)。
- 下列 {{site.data.keyword.discoveryfull}} Knowledge Graph `query_entities` 已知問題已使用 `2018-05-04` API 版本更新加以修正。只有在 `2018-05-04` 之後汲取或取代的實體，才適用此修正程式。實體可以透過重新汲取舊文件，或汲取包含那些實體的新文件來進行取代。如果未取代舊的實體，則 `query_entities` 會傳回所有包含 `2018-05-04` API 版本的大寫。
  - 先前已在 `query_entities` 中將所有實體名稱轉換為駝峰式大小寫。例如，實體名稱 "IBM Corporation" 轉換為 "Ibm Corporation"。不會再出現這種情況。

## 2018 年 5 月 9 日
{: #9may18}

- 範例文件現在會儲存在本端（在瀏覽器的本端漫遊資料資料夾中）。如需範例文件的相關資訊，請參閱[上傳範例文件](/docs/services/discovery?topic=discovery-configservice#uploading-sample-documents)。

## 2018 年 5 月 4 日
{: #4may18}

- 「元素分類」現在支援兩個額外的合約元素：屬性和起源。如需詳細資料，請參閱[瞭解合約元素](/docs/services/discovery?topic=discovery-element-classification#contract-elements)。

## 2018 年 4 月 26 日
{: #26apr18}

- 已修正下列汲取問題：在指定了後置強化 `json_normalizations` 和/或 `normalizations` 的某些情況下，可能會以錯誤順序套用正規化。這可能導致文件進行檢索時使用非預期的欄位值。不會再出現這種情況。
- 範例文件的檔案大小上限現在為 1MB。檔案大小上限之前為 5MB。

## 2018 年 4 月 12 日
{: #12apr18}

- Knowledge Graph：所有集合現在都可以使用[證明](/docs/services/discovery?topic=discovery-kg#kg_evidence)和[標準化及過濾](/docs/services/discovery?topic=discovery-kg#kg_canonicalization)。在 `03-05-2018` 之前建立的任何集合中，您需要重新汲取文件才能使用這些特性。之前，您需要建立新的集合，並重新汲取文件。

## 2018 年 4 月 11 日
{: #11apr18}

- 「元素分類」現在支援兩個額外的種類：`Asset Use` 和 `Communication`。如需詳細資料，請參閱[瞭解合約元素](/docs/services/discovery?topic=discovery-element-classification#contract-elements)。

## 2018 年 4 月 2 日
{: #2apr18}

- 現在，系統會在 24 小時（而非 1 個月）之後自動刪除範例文件。

## 2018 年 3 月 16 日
{: #16mar18}

- 已新增對德文的完整支援。如需相關資訊，請參閱[語言支援](/docs/services/discovery?topic=discovery-language-support#language-support)。

{{site.data.keyword.discoveryshort}} 工具：
- 已新增名為 **Default Contract Configuration** 的新配置來支援「元素分類」，該分類可用來從 PDF 中的元素擷取參與方、本質和種類。如需詳細資料，請參閱[元素分類](/docs/services/discovery?topic=discovery-element-classification#element-collection)。

更新至通用版
- 文件分段已從測試版狀態移至 GA 狀態。分段限制已增加到 250 個區段。每個文件不再限制為 50 個區段。如需詳細資料，請參閱[文件分段](/docs/services/discovery?topic=discovery-configservice#doc-segmentation)。

已知問題：
- 萬用字元對於包含大寫字母的查詢無效。例如，假設指定索引鍵/欄位配對 `{"borrower": "GOVERNMENT OF INDIA"}`，`query-borrower:*ndia` 會傳回結果，但 `query-borrower:*NDIA` 則不會。

## 2018 年 3 月 8 日
{: #8mar18}

- {{site.data.keyword.discoveryfull}} Knowledge Grap 的測試版已新增數個特性。在測試版期間，[知識圖](/docs/services/discovery?topic=discovery-kg#kg)功能及其相關聯方法僅可用於已訂閱**進階**方案、**超值**方案的服務實例，以及所有**專用**環境。新特性如下：
  - [實體相似性](/docs/services/discovery?topic=discovery-kg#kg_similarity)
  - [證明](/docs/services/discovery?topic=discovery-kg#kg_evidence)
  - [標準化及過濾](/docs/services/discovery?topic=discovery-kg#kg_canonicalization)

## 2018 年 3 月 7 日
{: #7mar18}

- 已修正下列汲取已知問題：在 2 月 28 日和 3 月 6 日之間，只有較小百分比的文件會使用 `id` 和 `extracted_metadata` 欄位來進行檢索（其他文件內容不會進行檢索）。基礎問題已修正，不過，您需要重新提交所有受影響的文件來進行汲取。沒有簡單的方法可識別受影響的文件。

## 2018 年 3 月 5 日
{: #5mar18}

- 下列 {{site.data.keyword.discoveryfull}} Knowledge Graph 已知問題已使用 `2018-03-05` API 版本更新加以修正。此修正程式僅適用於使用 `2018-03-05` 版本更新的新建立集合。  
  - 在汲取期間，所有實體類型名稱及關係類型名稱先前都會轉換為大寫。例如，實體 "GeoPoliticalEntity" 轉換為 "GEOPOLITICALENTITY"，而關係 "partOf" 轉換為 "PARTOF"。不會再出現這種情況。

## 2018 年 3 月 1 日
{: #1mar18}

- [查詢擴展](/docs/services/discovery?topic=discovery-query-concepts#query-expansion)限制已針對「進階」和「超值」方案增加到 5,000 個查詢擴展及總計 25,000 個詞彙。如需詳細資料，請參閱 [Discovery 定價方案](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)。

## 2018 年 2 月 28 日
{: #28feb18}

- {{site.data.keyword.alchemylanguageshort}} 強化從 **2018 年 3 月 1 日**起已淘汰。如需移轉利用 {{site.data.keyword.alchemylanguageshort}} 強化之現有集合及配置檔的相關資訊，請參閱[將強化移轉至 {{site.data.keyword.nlushort}}](/docs/services/discovery?topic=discovery-migrate-nlu#migrate-nlu)。

## 2018 年 2 月 23 日
{: #23feb18}

- 已新增依文件相似性查詢的能力。您可以透過文件 ID 查詢類似的文件，並選擇性地指定欄位，以進一步修正相似性。如需相關資訊，請參閱[文件相似性](/docs/services/discovery?topic=discovery-query-concepts#doc-similarity)。

- 已強化查詢結果中的 [`highlight` 參數](/docs/services/discovery?topic=discovery-query-parameters#highlight)。查詢結果將會傳回依其 `score` 排序的完整句子。

## 2018 年 2 月 21 日
{: #21feb18}

- 之前，如果汲取 PDF 文件，則查詢汲取通知時在 `extracted_metadata` 物件以及從文件詳細資料 API 中傳回的 `file_type` 是 `html`。不會再出現這種情況。傳回的 `file_type` 現在是 `pdf`。 

## 2018 年 1 月 26 日
{: #26jan18}

{{site.data.keyword.discoveryshort}} 工具：

- 已將存取韓文和西班牙文集合的功能新增至工具中的 [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) 磚。之前，只能透過 API 來查詢這些集合。

## 2018 年 1 月 23 日
{: #23jan18}

- 已新增擴展查詢範圍的能力；例如，您可以擴展 "car" 的查詢，以包括 "automobile" 和 "motor vehicle"。此外，您還可以取代通常拼錯的詞彙，例如，您可以將 "seabizcuit" 的查詢取代為 "seabiscuit"。查詢擴展是使用 {{site.data.keyword.discoveryshort}} API 來實作。如需詳細資料，請參閱[查詢擴展](/docs/services/discovery?topic=discovery-query-concepts#query-expansion)。  

## 2018 年 1 月 15 日
{: #15jan18}

- {{site.data.keyword.discoverynewsfull}} Original 已從服務下架。它已於 2017 年 7 月 31 日使用名為 {{site.data.keyword.discoverynewsfull}} 的新版本加以取代。如需從 {{site.data.keyword.discoverynewsfull}} Original 移轉至新版本的相關指示，請參閱[從 Watson Discovery News Original 移轉](/docs/services/discovery?topic=discovery-migrate-bwdn#migrate-bwdn)。

## 2018 年 1 月 11 日
{: #11jan18}

- 已新增韓文的完整支援。如需相關資訊，請參閱[語言支援](/docs/services/discovery?topic=discovery-language-support#language-support)。

## 2017 年 12 月 15 日
{: #15dec17}

- 發行了**元素分類**強化，其可剖析控管文件中的元素（句子、清單、表格），以對重要種類和類型進行分類。如需相關資訊，請參閱[元素分類](/docs/services/discovery?topic=discovery-element-classification#element-classification)。「元素分類」無法用於已訂閱**超值**方案的服務實例。[已解決](/docs/services/discovery?topic=discovery-release-notes#5jun18)
- 新增了簡體中文和荷蘭文的基本語言支援。如需相關資訊，請參閱[語言支援](/docs/services/discovery?topic=discovery-language-support#language-support)。目前，必須使用 API 來建立簡體中文和荷蘭文集合。
- 新增了「資料搜索器」的兩個新參數：`proxy_host_port` 和 `read-timeout`。如需詳細資料，請參閱[配置資料搜索器](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-the-data-crawler)。
- 汲取 PDF 文件時，可能會看到下列問題：[已解決](/docs/services/discovery?topic=discovery-release-notes#21feb18)
  - 當查詢汲取通知時，會以 `html` 傳回 PDF 文件的 `file_type` 欄位。
  - 針對 PDF 文件，結果的 `extracted_metadata` 物件中的 `file_type` 欄位是設為 `html`。
  - 文件詳細資料 API 也會將 PDF 文件的 `file_type` 欄位傳回為 `html`。
- 如果您要汲取 JSON，則不支援混合類型陣列。  

{{site.data.keyword.discoveryshort}} 工具：

- 針對 {{site.data.keyword.discoveryfull}} Knowledge Graph 測試版新增了視覺化查詢建置器。請參閱[使用 {{site.data.keyword.discoveryshort}} 工具查詢知識圖](/docs/services/discovery?topic=discovery-kg#querying-kg)

## 2017 年 11 月 30 日
{: #30nov17}

- 發行了 {{site.data.keyword.discoveryfull}} Knowledge Graph 的測試版，其可提供新的端點來查詢文件之間的實體及關係。這包括以上下文為基礎的搜尋和相關性分級。這項測試版特性只提供給**進階**方案使用者。它無法使用於**專用**環境。[已解決](/docs/services/discovery?topic=discovery-release-notes#8mar18) 如需相關資訊，請參閱 [{{site.data.keyword.discoveryfull}}Knowledge Graph](/docs/services/discovery?topic=discovery-kg#kg)。可以在[這裡](/docs/services/discovery?topic=discovery-release-notes#beta-features)找到說明測試版特性的陳述。
  - {{site.data.keyword.discoveryfull}} Knowledge Graph 中的已知問題：在汲取期間，所有實體類型名稱及關係類型名稱都會轉換為大寫。例如，實體 "GeoPoliticalEntity" 轉換為 "GEOPOLITICALENTITY"，而關係 "partOf”轉換為 "PARTOF"。[已解決](/docs/services/discovery?topic=discovery-release-notes#5mar18)
- 發行了其他兩種語言的 [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news)：韓文 (`collection_id`: `news-ko`) 和西班牙文 (`collection_id`: `news-es`)。{{site.data.keyword.discoverynewsfull}} 韓文版和西班牙文版只能透過 API 來使用；如需透過 API 來查詢集合的相關資訊，請參閱 [API 參考資料  ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window} [已解決](/docs/services/discovery?topic=discovery-release-notes#26jan18)。{{site.data.keyword.discoverynewsfull}} 英文版現在的 `collection_id` 為 `news-en`。早期，`collection_id` 是 `news` - 如果您是使用先前的 `collection_id`，它會繼續運作，不過，您可能會想要針對新專案切換至新的 `collection_id`。
- 查詢結果傳回 `score` 值，其指出查詢結果之間的相對相關性。從 2017 年 11 月 30 日開始，計算 `score` 的方式已變更。`score` 值只能用於在單一搜尋中對文件進行分級，而不能跨搜尋或階段作業。如果您已訓練集合，則會在自然語言查詢的結果中傳回 `score` 值。由於 `score` 指出查詢結果之間的相對相關性，因此不應使用它作為臨界值。請改用 `confidence` 來設定臨界值，它可指出與訓練模型相較之下的結果相關性。如需設定臨界值的相關資訊，請參閱[信賴度評分](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence)。
- 從這個版本開始，段落擷取會偵測句子界限 - 它會嘗試傳回在句子開頭開始並在尾端結束的段落。以前，許多段落會在句子中間開始或結束。如需「段落擷取」的相關資訊，請參閱[段落](/docs/services/discovery?topic=discovery-query-parameters#passages)。

## 2017 年 11 月 15 日
{: #15nov17}

{{site.data.keyword.discoveryshort}} 工具：

- 新增了[關係擷取](/docs/services/discovery?topic=discovery-configservice#relation-extraction)強化，其中包含可納入使用 {{site.data.keyword.knowledgestudiofull}} 所建立之自訂關係模型的選項。
- [實體擷取](/docs/services/discovery?topic=discovery-configservice#entity-extraction)強化 {{site.data.keyword.discoveryshort}} 工具，現在包括可納入使用 {{site.data.keyword.knowledgestudiofull}} 所建立之自訂實體模型的選項。
- 從 {{site.data.keyword.discoveryshort}} 工具中移除了建立日文集合的選項，但是，使用 {{site.data.keyword.discoveryshort}} API 建立日文集合的選項仍保留。
- {{site.data.keyword.discoveryshort}} 工具現在支援聯合環境。

## 2017 年 11 月 10 日
{: #10nov17}

{{site.data.keyword.discoveryshort}} 工具：

- 新增了其他選項來進行 {{site.data.keyword.discoveryshort}} 工具的「段落擷取」。現在當您查詢時，可以指定要從其中傳回段落的欄位、要傳回的段落數，以及每一個段落的字元數上限。如需限制、最小值和最大值，請參閱[段落](/docs/services/discovery?topic=discovery-query-parameters#passages)。

## 2017 年 11 月 8 日
{: #8nov17}

所有 API 呼叫的版本字串已從 `2017-10-16` 變更為 `2017-11-07`。此版本：
- 已將每一個查詢結果中的 `score` 移至名稱為 `result_metadata` 的新物件。
- 如果所查詢的集合已訓練，且查詢是自然語言查詢，則 `result_metadata` 會包含 `confidence` 欄位，其顯示該結果的信賴度評分。如需詳細資料，請參閱[信賴度評分](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence)。
- 在汲取期間將過濾掉包含空格的欄位（例如：`body.additional reading`）。`notices` 說明會變成 `The field 'additional reading' is invalid: whitespace, '.', '#' and ',' are invalid in a field name`。
- 在汲取期間將過濾掉 `result_metadata` 欄位。

## 2017 年 10 月 16 日
{: #16oct17}

- 所有 API 呼叫的版本字串已從 `2017-09-01` 變更為 `2017-10-16`。此版本不再支援將新文件上傳至使用 {{site.data.keyword.alchemylanguageshort}} 強化來強化的現有集合，也不再支援建立新集合及使用 {{site.data.keyword.alchemylanguageshort}} 強化來強化它們。以 {{site.data.keyword.alchemylanguageshort}} 強化的現有集合應儘快移轉到 {{site.data.keyword.nlushort}} 強化。如需詳細資料，請參閱[將強化移轉至 {{site.data.keyword.nlushort}}](/docs/services/discovery?topic=discovery-migrate-nlu#migrate-nlu)。{{site.data.keyword.discoveryshort}} 工具也使用 `2017-10-16` 版本，如需相關資訊，請參閱下面。

{{site.data.keyword.discoveryshort}} 工具：

- {{site.data.keyword.discoveryshort}} 工具使用 `2017-10-16` API 版本字串，因此，如果您是使用該工具，則無法再將文件上傳至現有的 {{site.data.keyword.alchemylanguageshort}} 集合，或建立利用 `2017-10-16` 之後的 {{site.data.keyword.alchemylanguageshort}} 強化來強化的新集合。如果您要繼續使用 {{site.data.keyword.discoveryshort}} 工具來強化集合，請先將集合移轉到 {{site.data.keyword.nlushort}}。如需詳細資料，請參閱[將強化移轉至 {{site.data.keyword.nlushort}}](/docs/services/discovery?topic=discovery-migrate-nlu#migrate-nlu)。
- **資料綱目瀏覽器**顯示對 {{site.data.keyword.discoverynewsfull}} 集合中的數個強化的範例查詢。它現在也有一個**顯示其他值**鏈結，此鏈結將在 {{site.data.keyword.discoverynewsfull}} 中顯示該強化的其他範例值。
- 多個生產力加強功能，包括結合集合統計資料、錯誤和警告，以及**管理資料**畫面的資料見解。
- 新增了一則訊息，可在文件完成處理時顯示警示。

## 2017 年 10 月 9 日
{: #9oct17}

- 此 API 提供了新的聚集度量值 `unique_count`。它將傳回集合中所指定欄位的唯一實例計數。如需相關資訊，請參閱 [unique_count](/docs/services/discovery?topic=discovery-query-aggregations#unique_count)。

{{site.data.keyword.discoveryshort}} 工具：

- 現在，**視覺化查詢建置器**中支援「直方圖」及「時間片段」聚集。您也可以選擇開啟「時間片段」查詢的異常偵測。
- **資料綱目瀏覽器**顯示所選擇強化的範例查詢。它現在也有一個「顯示其他值」鏈結，此鏈結將顯示該強化的其他範例值。
- 新增了 hamburger 功能表，使導覽**管理資料**、**檢視資料綱目**及**建置查詢**畫面更快速。

### 2017 年 10 月 3 日
{: #3oct17}

- 現在可以使用文件分段。請參閱[使用文件分段來分割文件](/docs/services/discovery?topic=discovery-configservice#doc-segmentation)。

### 2017 年 9 月 29 日
{: #29sept17}

- {{site.data.keyword.discoveryshort}} 已在 2017 年 9 月 29 日於 `Germany` 位置推出。為了遵守 EU 資料法規，此位置不支援 AlchemyLanguage 強化。
- 已知問題：查詢欄位不能包含空格。在 {{site.data.keyword.discoveryshort}} 中撰寫查詢時，如果有任何查詢欄位包含空格（例如，`body.additional reading`），您會收到 `400: Invalid query syntax error`。[已解決](/docs/services/discovery?topic=discovery-release-notes#8nov17)

### 2017 年 9 月 25 日
{: #25sept17}

- 現在提供「超值」定價方案。如需相關資訊，請參閱 [{{site.data.keyword.discoveryshort}} 定價方案](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)。
- 新增了在相同環境內的集合之間查詢、列出欄位及查詢通知的能力。如需詳細資料，請參閱[查詢多個集合](/docs/services/discovery?topic=discovery-query-concepts#multiple-collections)。
- [語言支援](/docs/services/discovery?topic=discovery-language-support#language-support)提供了 {{site.data.keyword.discoveryshort}} 的語言支援資訊

{{site.data.keyword.discoveryshort}} 工具：
- 「視覺化查詢建置器」已從測試版狀態移至 GA 狀態。「視覺化查詢建置器」目前不支援「過濾器」、「時間片段」及「直方圖」聚集。可按一下**包含結果的分析**，然後按一下**建置查詢**畫面上的**以查詢語言編輯**，來撰寫那些聚集。
- 新增了測試版功能，以刪除 {{site.data.keyword.discoverynewsfull}} 查詢的重複項目。
- 除了英文、德文及西班牙文語言集合之外，您現在還可以建立阿拉伯文、法文、義大利文、韓文、日文及巴西葡萄牙文集合。
- 已知問題：{{site.data.keyword.discoveryshort}} 工具不支援聯合環境。[已解決](/docs/services/discovery?topic=discovery-release-notes#15nov17)

### 2017 年 9 月 14 日
{: #14sept17}

{{site.data.keyword.discoveryshort}} 工具：

- 新增了「資料綱目瀏覽器」，它會顯示轉換後文件中的欄位和值。利用本資訊，您可以在使用「Discovery 查詢語言」建置查詢之前，先瞭解集合的資料結構。有兩種方式可檢視資料綱目：依文件（文件視圖）或依欄位（集合視圖）。若要存取「資料綱目瀏覽器」：在**我的資料見解**畫面上，按一下**檢視資料綱目**按鈕，或按一下左邊的**檢視資料綱目**圖示。

### 2017 年 9 月 6 日
{: #6sept17}

- 新增了對您的查詢傳回的文件進行刪除重複文件的能力。此測試版特性同時適用於專用集合與 Watson Discovery News 集合。如需詳細資料，請參閱[從查詢結果排除重複文件](/docs/services/discovery?topic=discovery-query-parameters#deduplication)。

刪除重複文件目前僅支援作為測試版功能。如需相關資訊，請參閱本文件頂端有關測試版的陳述。

### 2017 年 8 月 31 日
{: #31aug17}

- 所有 API 呼叫的版本字串已從 `2017-08-01` 變更為 `2017-09-01`。這個版本包含的更新項目將在預覽和汲取期間將過濾掉下列無效 JSON 欄位，因此只汲取有效的 JSON 欄位。將您的版本字串更新為 `2017-09-01`，以避免衝突和可能的錯誤。

   - 最上層的 `id`、`score` 及 `highlight`（您可以繼續透過 `add a document` 功能，使用文件 ID 將文件新增至集合中）。如需詳細資料，請參閱 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery#add-a-document){: new_window}。
   - 最上層以 `_` 作為字首的欄位名稱（因此，在依 ID 查詢文件時，您可以查詢 `id` 而非 `_id`）。
   - 欄位名稱中的 `#` 和 `,`
   - 以 `+` 和 `-` 作為字首的欄位名稱
   - 欄位名稱的 `"` `"` 空白值

**附註：**如果 JSON 文件在欄位名稱中包含這些字元，或最上層是 `id`、`score` 及 `highlight`，您必須先移除它們，然後才能將文件新增至集合，否則這些欄位會是空的。您可以先建立自訂配置並將 JSON 正規化，然後再將文件新增至集合以避免此問題。請參閱[自訂配置](/docs/services/discovery?topic=discovery-configservice#custom-configuration)。此外，檔名中包含標點符號字元 `?`、`:` 或 `#` 的文件將導致汲取時發生錯誤。請先將任何包含這些字元的文件重新命名，然後再汲取它們。

- 更新了 `natural_language_query` 的擷取方法，透過比對單字與相關語意來改善結果的相關性。這個更新項目只會影響沒有相關性訓練的集合。如果您使用 `natural_language_query` 且未進行相關性訓練，則可能會看到所傳回結果的順序有所改善。

{{site.data.keyword.discoveryshort}} 工具：

- 對查詢建置器的一些變更，讓您在「Discovery 查詢語言」與「自然語言」查詢選項之間，以及在查詢、過濾器和聚集之間更容易進行切換。


### 2017 年 8 月 25 日
{: #25aug17}

- `passages` 陣列現在包含 `field`、`start_offset` 及 `end _offset`。`field` 是從其中擷取段落的欄位名稱。`start_offset` 是欄位內的段落文字起始字元。`end_offset` 是欄位內的段落文字結束字元。

{{site.data.keyword.discoveryshort}} 工具：
這個查詢建置加強功能可以在**建置查詢**畫面上找到。

-  新增了透過視覺化建置器，以「{{site.data.keyword.discoveryshort}} 查詢語言」撰寫查詢的測試版能力。按一下**搜尋文件**及**限制查詢的文件**區段中的**在視覺化模式中建置**，即可試用它的功能。當您以視覺化方式建置查詢時，它會顯示在其下方的 **{{site.data.keyword.discoveryshort}} 查詢語言**中。

   視覺化查詢建置器目前僅支援作為測試版功能。如需相關資訊，請參閱本文件頂端有關測試版的陳述。

### 2017 年 8 月 18 日
{: #18aug17}

{{site.data.keyword.discoveryshort}} 工具：

- 在 [2017 年 8 月 11 日](/docs/services/discovery?topic=discovery-release-notes#11aug17)引進的測試版視覺化聚集建置器中，新增了對巢狀聚集和條件的支援。每個聚集列有 3 個條件的限制。

   視覺化聚集建置器目前僅支援作為測試版功能。如需相關資訊，請參閱本文件頂端有關測試版的陳述。

### 2017 年 8 月 11 日
{: #11aug17}

{{site.data.keyword.discoveryshort}} 工具：

這兩個特性都是查詢建置加強功能，可以在**建置查詢**畫面上找到。

- 新增了從一組預先建置的範例查詢和聚集中選取查詢的選項。按一下右上方的**使用範例查詢**以存取清單。如果您要查詢專用資料集合，則範例會使用在您集合中找到的 `top entities`、`categories` 等等。這些查詢可作為撰寫您自己的查詢的起點。{{site.data.keyword.discoverynewsfull}} 集合和專用集合都有可用的範例查詢。

-  新增了透過視覺化建置器來撰寫聚集的測試版能力。按一下**使用 {{site.data.keyword.discoveryshort}} 查詢語言撰寫聚集查詢**欄位上方的**在視覺化模式中建置**，以試用它的功能。當您以視覺化方式建置聚集時，該查詢將顯示在其下方的 **{{site.data.keyword.discoveryshort}} 查詢語言**中。  

   視覺化聚集建置器目前僅支援作為測試版功能。如需相關資訊，請參閱本文件頂端有關測試版的陳述。

### 2017 年 7 月 31 日
{: #31jul17}

- 發行了 {{site.data.keyword.discoverynewsfull}} 的新版本。原始版本已重新命名為 {{site.data.keyword.discoverynewsfull}} Original，並已下架，在 **2018 年 1 月 15 日**已從服務移除。如需移轉指示，請參閱[從 Watson Discovery News Original 移轉](/docs/services/discovery?topic=discovery-migrate-bwdn#migrate-bwdn)。
  **附註：**如果您已建立 {{site.data.keyword.discoveryshort}} 的新實例，您只能存取 {{site.data.keyword.discoverynewsfull}} 的新版本。

- 發行了 {{site.data.keyword.discoveryfull}} 的新定價方案。如需詳細資料，請參閱 [{{site.data.keyword.discoveryshort}} 定價方案](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)。

- 所有 API 呼叫的版本字串已從 `2017-07-19` 變更為 `2017-08-01`。此版本包含新定價方案的更新項目，以及 Watson Discovery News 的新版本。請更新版本字串，以避免衝突和可能的錯誤。

### 2017 年 7 月 19 日
{: #19jul17}

 - 在 2017 年 8 月 1 日發表的定價變更中，目前使用已淘汰之 **30 天免費試用**方案的使用者將自動移轉至**精簡**方案。由於這項轉移，現有的使用者可能已達到或已超出精簡方案限制，亦即文件數 _(2000)_、儲存空間 _(200Mb)_ 或集合數 _(2)_。如果您已超出**精簡**方案的限制，則無法將任何其他內容新增至該服務，但仍然可以查詢集合。您可以使用 {{site.data.keyword.discoveryshort}} 工具或 API 來檢視所有這些限制的現行狀態。若要能夠繼續將內容新增至 {{site.data.keyword.discoveryshort}} 實例，您必須執行下列其中一項：
   - 移除集合及（或）文件，使其不超出**精簡**方案的限制。
    可以透過 API 使用 [delete-doc](https://{DomainName}/apidocs/discovery#delete-a-document) 方法個別地刪除文件，或利用工具或 API，使用 [delete-collection](https://{DomainName}/apidocs/discovery#delete-a-collection) 方法來刪除整個集合。
   - 將方案升級至符合儲存空間需求的層次。
 - 大小為 **`1`**、**`2`** 或 **`3`** 環境的客戶將自動移轉至**進階**方案。

### 2017 年 7 月 17 日
{: #17jul17}

 - 下列功能已從測試版狀態移至 GA 狀態：

   - 相關性訓練
   - 自然語言查詢
   - 強調顯示

 - 從這個版本開始，{{site.data.keyword.discoveryfull}} 會將其強化機制從 {{site.data.keyword.alchemylanguageshort}} 變更為 {{site.data.keyword.nlushort}}。{{site.data.keyword.alchemylanguageshort}} 正在進行淘汰，您應該儘快開始使用 {{site.data.keyword.nlushort}}。如需詳細資料，請參閱[從 {{site.data.keyword.alchemylanguageshort}} 強化移轉至 {{site.data.keyword.nlushort}} 強化](/docs/services/discovery?topic=discovery-migrate-nlu#migrate-nlu)。
   **附註：**當與 Watson Knowledge Studio 整合時，仍必須使用 {{site.data.keyword.alchemylanguageshort}} 強化配置。如需詳細資料，請參閱[與 {{site.data.keyword.knowledgestudiofull}} 整合](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-with-wks)。

 - 所有 API 呼叫的版本字串已從 `2017-06-25` 變更為 `2017-07-19`。此版本在建立集合時啟用 NLU 預設配置。在舊版中，您仍然能夠以 {{site.data.keyword.alchemylanguageshort}} 進行強化。

    預設配置已更新為使用 {{site.data.keyword.nlushort}}。您應該儘快更新版本字串，以避免衝突和可能的錯誤。

 - Discovery 工具：

    對於使用 {{site.data.keyword.alchemylanguageshort}} 強化進行強化的集合，Insight Cards 將不再自動更新。您必須將集合移轉至 {{site.data.keyword.nlushort}} 強化，Insight Cards 才會更新。

    如果您在 **2017 年 7 月 18 日**之前已建立集合，且已套用 **Default Configuration**，則該集合已使用 {{site.data.keyword.alchemylanguageshort}} 強化來強化。如果您在此日期之後將 **Default Configuration** 套用至集合，將會使用 {{site.data.keyword.nlushort}} 強化（配置名稱會變成工具中的 **Default Configuration with NLU**）。由於 {{site.data.keyword.alchemylanguageshort}} 強化會被淘汰，所以不應用於新集合。

### 2017 年 6 月 30 日
{: #30jun17}

 -  在 2017 年 5 月 5 日引進作為測試版特性的實體正規化功能，已移至 GA 狀態。如需詳細資料，請參閱[建立自訂配置以將實體正規化](/docs/services/discovery?topic=discovery-normalizing-entities-cc#normalizing-entities-cc)。

### 2017 年 6 月 23 日
{: #23jun17}

 - 所有 API 呼叫的版本字串已從 `2016-12-01` 變更為 `2017-06-25`。如果集合的語言是設為其中一種語言，新的版本字串會以德文 (`de`) 或西班牙文 (`es`) 啟用強化。之前，無論集合的語言設定為何，都以英文執行所有強化。

    如果您未使用非英文語言的強化，則可以繼續使用 `2016-12-01` 版本字串。不過，您應該儘快更新版本字串，以避免潛在的未來衝突。

 - 現在，在 `timeslice` 聚集中，提供了異常偵測作為 GA 功能。如需詳細資料，請參閱[時間片段異常偵測](/docs/services/discovery?topic=discovery-query-aggregations#anomaly-detection)。

 - Discovery 工具：

   - 新增了使用 Discovery 工具（相關性工具）來改善查詢結果相關性的測試版能力。請參閱[透過 Discovery 工具來改善查詢結果的相關性](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling)。

### 2017 年 6 月 19 日
{: #19jun17}

  - Discovery 工具：

    - 新增了可將新集合中的文件語言指定為英文、西班牙文或德文的選項。若要使用它，請在**命名您的新集合**對話框上，選擇**選取文件的語言**。

    - 在**建置查詢**畫面中新增了**摘要**標籤。**摘要**標籤顯示現有 **JSON** 標籤中所提供的完整查詢結果的概觀。**摘要**顯示畫面會根據您的查詢和強化而有所不同。可能顯示的資訊包括：文件名稱或 ID、聚集統計資料、依相關性順序列出的文件段落，以及依強化列出的結果。

    - 在**建置查詢**畫面中新增了「自然語言查詢」選項。若要使用它，請按一下**搜尋文件**區段中的**以簡單語言提出問題**，即會出現一個可讓您輸入問題的欄位。現在，以按一下**使用 Discovery 查詢語言**按鈕，即可存取原始查詢欄位（之前稱為**輸入查詢或關鍵字**）。

    - 已重新設計**建置查詢**畫面，但仍保留所有欄位和選項。以下是欄位的新舊名稱。

|**舊欄位名稱**                                           |**新欄位或區段名稱**                                                                                             |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
|撰寫並執行查詢                                           |搜尋文件                                                                                                                         |
|縮小查詢結果（過濾器）                                   |限制您查詢的文件                                                                                                                         |
|將查詢結果分組（聚集）                                   |包含結果的分析                                                                                                                          |
|要顯示的欄位                                             |名稱不變，但已移至新的**自訂顯示選項**區段。                                                                        |
|要傳回的文件數（計數）                                   |要傳回的文件數 [此欄位已移至**自訂顯示選項**區段。]                                                                            |
|包括相符的段落                                           |包含相關段落 [此欄位已移至**自訂顯示選項**區段。]                                                                    |
|要在開始時跳過的查詢欄位數（偏移）                       |要在開始時跳過的查詢結果數 [此欄位已移至**自訂顯示選項**區段。]                                                                             |

### 2017 年 6 月 5 日
{: #5jun17}

 - 現在，Watson Discovery News 查詢只會顯示 `text` 和 `alchemyapi_text` JSON 欄位中每一篇文章的前 150 個字。`blekko.snippet` 欄位只會顯示 Snippet 陣列的第一個句子。

### 2017 年 5 月 30 日
{: #30may17}

 - 查詢 API 上的 `passages` 參數已從測試版移至 GA 狀態。

### 2017 年 5 月 25 日
{: #25may17}

 - Discovery 工具：這一版新增了查詢欄位強調顯示。此特性會在「結果」窗格的 JSON 中加上黃色來強調顯示欄位名稱。每一個結果的所有已查詢或已過濾的欄位都會強調顯示，即使該欄位的內容不符合查詢也一樣。在聚集中使用的任何欄位也會在查詢結果中強調顯示，但只會強調顯示第一個聚集作業。

### 2017 年 5 月 10 日
{: #10may17}

 - `query` 和 `notices` 方法現在支援 `highlight` 參數。參數是布林。當您執行查詢且 `highlight` 是指定為 `true` 時，該服務傳回的輸出將包含一個新的 `highlight` 欄位，其中符合查詢的單字會包裝在 HTML `*`（強調）標籤中。如需詳細資料，請參閱[查詢參數](/docs/services/discovery?topic=discovery-query-parameters#highlight)。

 - 可以只局部完成環境的刪除，但會導致無法建立新環境的狀況，因為只允許每個服務實例有一個環境。如果您試圖在刪除環境後再建立環境，但發現其中一項作業停留在 `pending` 狀態，則可能會發生這個問題。解決之道是重新執行刪除作業以完成它，然後建立新環境。

### 2017 年 5 月 8 日
{: #8may17}

 - 更新了情緒語氣評分模型，以改善情緒分析（`docEmotion`）強化的精準度。擴充了訓練資料集，且改變了特性工程設計，因此模型在基準性能測試資料集上具有更高的精準度。

### 2017 年 5 月 5 日
{: #5may17}

 - 實體正規化現在可以與使用 Watson Knowledge Studio 所產生之自訂模型的 Discovery 服務搭配使用。實體正規化會將不同參照的正規化（標準）名稱插入至來源文件中的相同人員或物件。如需詳細資料，請參閱[建立自訂配置以將實體正規化](/docs/services/discovery?topic=discovery-normalizing-entities-cc#normalizing-entities-cc)。

     **附註：**實體正規化目前僅支援作為測試版功能。如需相關資訊，請參閱本文件頂端有關測試版的陳述。[已解決](/docs/services/discovery?topic=discovery-release-notes#30jun17)

{{site.data.keyword.discoveryshort}} 工具：

 - 工具錯誤日誌不再限制為最多八 (8) 頁的結果。如果沒有文件名稱，則錯誤日誌仍會顯示文件 ID。

 - 配置名稱限制為 50 個字元，而且必須由 `[a-zA-Z0-9-_]` 字元組成。 

 - 先前只能透過 API 使用的 `passages` 參數，現在透過「工具」及 API 都可以使用。

### 2017 年 4 月 25 日
{: #25apr17}

  - 該服務現在可讓您提供*訓練資料* 來改善查詢結果的正確性。當您提供具有訓練資料的 Discovery 實例時，該服務會使用進階 Watson 演算法來判定最相關的結果。當您新增更多訓練資料時，該服務實例在它傳回的結果中會變得更準確。如需相關資訊，請參閱[改善查詢結果的相關性](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api)及 [API 參考資料](https://{DomainName}/apidocs/discovery#list-training-data)。

  - 現在，API 支援 `natural_language_query` 參數作為測試版。此參數可讓您以自然語言（而非 Discovery 服務的查詢語言）指定查詢。如需相關資訊，請參閱 API 參考資料中的[查詢集合](https://{DomainName}/apidocs/discovery#query-your-collection)方法。

  - 文件更新及勘誤更正。

### 2017 年 4 月 14 日
{: #14apr17}

已將加強功能新增至查詢 API (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`)。如需相關資訊，請參閱 API 參考資料中的[查詢集合](https://{DomainName}/apidocs/discovery#query-your-collection)方法。

  - 現在，查詢 API 支援 `passages` 參數。如果此參數設為 `true`，則查詢會從集合的文件中傳回一組最相關的段落。段落是由更準確的 Watson 演算法所產生，用來決定該查詢所傳回之所有文件中的最佳文字段落。這可讓您更精確地尋找資訊及上下文。如需相關資訊，請參閱 API 參考資料中的[查詢集合](https://{DomainName}/apidocs/discovery#query-your-collection)方法。

    - 在查詢中指定 `passages=true` 可能會降低效能，這是因為增加了處理來擷取段落。在較大型的環境下，效能影響會減輕。

    - 只有在專用集合上才支援 `passages` 參數。在 Watson Discovery News 集合中不支援它。

    - `passages` 參數目前最多傳回 10 個結果。無法變更傳回的結果數。[更新](/docs/services/discovery?topic=discovery-query-parameters#passages_count)

    - `passages` 參數從集合的任何給定文件中最多傳回三 (3) 個段落。如果文件包含超過三個其他相關段落，該參數不會傳回它們。

### 2017 年 4 月 7 日
{: #7apr17}

- 現在，查詢 API (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`) 支援 `sort` 參數，它可讓您指定文件中要排序的欄位清單（以逗點區隔）。如需相關資訊，請參閱 API 參考資料中的[查詢集合 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window} 方法。
- 現在，查詢聚集的 `timeslice` 參數可正確處理 UNIX epoch 格式的日期。如需聚集和 `timeslice` 參數的相關資訊，請參閱[查詢參考資料](/docs/services/discovery?topic=discovery-query-reference#aggregations)。
- 改善錯誤訊息。
- 更新服務的 Java SDK。如需詳細資料，請參閱 [API 參考資料](https://{DomainName}/apidocs/discovery?language=java)。
- 在查詢中使用萬用字元的下列限制，現在已修正並可正確運作：

  - 在任何給定的查詢中，只能使用一個萬用字元。例如，`query-month:*ctober` 有效，但 `query-month:*ctobe*` 則產生剖析錯誤。
  - 萬用字元對於包含大寫字母的查詢無效。例如，假設指定索引鍵/欄位配對 `{"borrower": "GOVERNMENT OF INDIA"}`，`query-borrower:*ndia` 會傳回結果，但 `query-borrower:*NDIA` 則不會。

**附註：**在查詢的詞組中，不需要萬用字元。例如，假設指定索引鍵/欄位配對 `{"borrower": "GOVERNMENT OF TIMOR"}`，`query-borrower:"GOVERNMENT OF TIMOR"` 會傳回結果，但 `query-borrower:"GOVERNMENT OF TI*OR"` 則不會。在詞組內使用萬用字元並不適合，因為詞組的引號 (`"`) 內的所有字元都會跳出。

### 2017 年 3 月 24 日
{: #24mar17}

- 在 Discovery 工具的「我的資料見解」畫面中新增了過濾

### 2017 年 3 月 15 日
{: #15mar17}

探索到下列已知問題。

-  從 HTML、PDF 和 Word 文件汲取的所有欄位都是輸入為**字串**。JSON 欄位和計算欄位（例如觀感評分）會依定義的方式輸入。[更新](/docs/services/discovery?topic=discovery-addcontent#adding-content-with-the-api-or-tooling)
- `preview` 作業目前不檢查已提交的 JSON 文件內的巢狀 JSON 陣列。該服務目前不支援巢狀 JSON 陣列，因此具有巢狀陣列的文件可以順利通過 `preview` 作業，但在嘗試汲取時會失敗。請參閱[可以上傳 JSON 陣列嗎？](/docs/services/discovery?topic=discovery-faqs#array)
- 如果發生汲取錯誤，並看到 `unsupported text language` 訊息，請以 `"language": "english"` 強化選項更新您的配置，以強制所有文字以英文解譯，如下列範例所示。[更新](/docs/services/discovery?topic=discovery-migrate-nlu#migrate-nlu)
```json
"enrichments": [
   {
     "enrichment": "alchemy_language",
     "source_field": "author.label",
     "options": {
       "extract": "taxonomy,entity,relation,doc-emotion,doc-sentiment,concept,keyword",
       "sentiment": true,
       "quotations": true,
       "language": "english"
     }
   }
 ]
```
{: codeblock}

下列錯誤已修正。

- 已改善服務的效能和穩定性。

### 2017 年 3 月 8 日
{: #8mar17}

 - 後端已最佳化，包括增加了新的逾時值，以改善整體效能。
 - 導致免費（大小為 `0`）環境的環境狀態不論實際狀態如何都報告為 `pending` 狀態，此錯誤已修正。
 - {{site.data.keyword.discoveryshort}} 目前唯一支援的國家語言是美國英文 (`en_US`)。[更新](/docs/services/discovery?topic=discovery-language-support#language-support)

### 2017 年 3 月 3 日
{: #3mar17}

- 在 Discovery 工具中新增了「我的資料見解」畫面。

### 2017 年 2 月 26 日
{: #26feb17}

-     改善了 {{site.data.keyword.discoverynewsshort}} 環境的效能。
-  {{site.data.keyword.discoverynewsshort}} 服務一次只傳回 50 個結果。暫行解決方法是在查詢中使用 `offset` 參數來翻看結果。
-  您可以使用下列指令，對個別文件提交新的配置：

```bash
curl -X POST -u apikey:{apikey_value} -F "file=@wikipedia-sample.html" -F "configuration=$(cat config.json)" "https://gateway.watsonplatform.net/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2016-12-01"
```
{: pre}
-  該服務的 PDF 和 Word 轉換器會建立 HTML 作為中間步驟。在最終轉換成正規化 JSON 之前，該服務可以在中間 HTML 上套用其他轉換和正規化。

下列錯誤已修正。

-  改進了錯誤碼。
-  更正了數個文件勘誤。

### 2017 年 2 月 16 日
{: #16feb17}

-  現在，您可以使用 CSS 選取器來選取 JSON 欄位，然後對其套用強化。如需相關資訊，請參閱[使用 CSS 選取器來擷取欄位](/docs/services/discovery?topic=discovery-configservice#using-css)。
-  現在，您可以將新的 `size: X` 參數傳遞給 [update-environment 方法](https://{DomainName}/apidocs/discovery#update-an-environment)來增加環境的大小，其中 `X` 是 0 與 3 之間的整數。如需環境大小和屬性的相關資訊，請參閱 [create-environment 方法](https://{DomainName}/apidocs/discovery#create-an-environment)。[更新](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

    **附註：**您無法減少現有環境的大小。如果您想要減少環境的大小，請聯絡 {{site.data.keyword.IBM}} 支援人員以尋求協助。

-  有新的查詢運算子可用。`::!` 運算子已新增為 not-equals 一元運算子。例如，您現在可以執行 `query=field::!value`（不等於）。先前唯一的排他運算子是 `:!`，代表 not-contains 運算子（例如，`query=field:!value`）。

下列錯誤已修正。

-  已套用安全更新項目。
-  已改善搜尋警示的狀態訊息。

### 2017 年 2 月 1 日
{: #1feb17}

下列附註特別適用於「資料搜索器」1.3.0 版。[更新](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)

-   「資料搜索器」會記錄用來上傳文件的 `document_id` 值，以及上傳的狀態。轉換通知在日誌外不會持續保存。目前沒有工具可與該資料互動，但若時間允許，預期將會開發這類工具。可透過 H2 資料庫來存取資料，該資料庫可配置為使用遠端 DBMS。

### 2017 年 1 月 16 日
{: #16jan17}

下列附註特別適用於「資料搜索器」1.2.5 版。[更新](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)

-  「資料搜索器」可以選擇性地在上傳檔案之後立即輪詢文件狀態。這項檢查是搜索器「上傳文件」概念的一部分，因此當啟用這項檢查時，「搜索器」要同時上傳的文件數目，幾乎不太可能超過 {{site.data.keyword.discoveryshort}} 服務可以為該使用者同時處理的文件。

    `check_for_completion` 特性的負面影響是「搜索器」也可以向使用者公開文件失敗的原因和時間。附加至已順利上傳但無法處理的文件的任何通知，都會顯示在「搜索器」日誌中。通知不會匯出為可處理的檔案，但 IBM 歡迎對此提出特性建議。

### 2017 年 1 月 5 日
{: #5jan17}

下列附註說明在 2016 年 12 月 15 日 GA 發行之後所識別的問題。

[更新：API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery){: new_window}

-   如果您使用 `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` 或 `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]` 呼叫來新增文件，則該呼叫會傳回文件 ID 及**處理中**狀態。如果您隨後使用 `GET /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]` 呼叫來查詢該文件，則狀態會保持在**處理中**直到汲取完成，屆時狀態會變更為**可用**。

    如果您使用 `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]` 呼叫來**更新**現有文件，則即使該服務尚未完全處理已更新的文件，對應的 **GET** 呼叫仍會傳回 `available` 狀態。`available` 狀態係指原始文件或已更新的文件。除非更新作業傳回錯誤，否則目前無從判定已更新文件的狀態。

        暫行解決之道是在提交文件更新之後，先等待最多 10 分鐘，再嘗試查詢更新的內容。


### 2016 年 12 月 15 日，通用版
{: #15dec16}

下列附註適用於 {{site.data.keyword.discoveryfull}} 服務的「通用版 (GA)」。

#### 一般注意事項
{: #rn-general-notes}

[更新：內容](/docs/services/discovery?topic=discovery-addcontent#addcontent)

如需現行 API 版本，請參閱[API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery){: new_window}。

[更新：與 {{site.data.keyword.knowledgestudiofull}} 整合](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-with-wks)。

-   您目前無法指定欄位的資料類型。所有欄位都是以文字進行檢索（資料類型**字串**）。 
-   如果您使用 API 來使用該服務，則必須在每一個呼叫中指定 API 版本。現行 API 版本為 **2016-12-01**。 

    **附註：**GA 版本不強制使用特定版本，但仍必須列出它，才能啟用與未來版本的相容性。

-   您可以利用一個以 {{site.data.keyword.knowledgestudiofull}} 建立的自訂模型來使用該服務。自訂模型可用來強化所汲取的文件。您必須使用 API 來整合自訂模型與 {{site.data.keyword.discoveryshort}} 服務；您無法使用該工具來執行整合。

#### 資料管理
{: #rn-data}

[更新](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

-   搜尋索引未加密。
-   備份及還原功能不是使用者可控制的。

#### 環境
{: #rn-environments}

[更新](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

-   您只能為每個服務實例建立一個環境來上傳您自己的資料。
-   {{site.data.keyword.discoveryshort}} 服務位於單一可用性區域（美國南部）。
-   目前無法使用專用及超值方案。

#### 環境大小調整
{: #rn-sizing}

[更新](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

-   只有在建立新環境時，您才能選擇環境大小。使用者目前無法調整環境的大小。
-   選擇具有更多 RAM 的環境大小可增加效能。
-   目前沒有規定的調整大小建議可用於特定使用案例。
-   {{site.data.keyword.knowledgestudiofull}} 模型的自訂大小調整不是自助式。如需相關資訊，請聯絡您的 {{site.data.keyword.IBM}} 代表。

#### 汲取限制
{: #rn-ingestion}

[更新](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

-   汲取率目前限制為 100 個並行文件汲取作業。將文件提交至該服務進行汲取的應用程式需要重視 HTTP 429 錯誤，並據此對汲取要求進行節流控制。
-   {{site.data.keyword.alchemylanguageshort}} 強化限制為每個欄位前 50 KB。
-   來自 {{site.data.keyword.knowledgestudiofull}} 自訂模型的強化不受限制，但會將文件分割成 10-KB 區塊。不會在區塊界限之間標註任何關係。

#### 查詢限制
{: #rn-query}

[更新](/docs/services/discovery?topic=discovery-query-concepts#query-concepts)

-   過多的查詢負載可能導致搜尋索引處理程序自動重新啟動。
-   發出查詢的應用程式必須對並行查詢數目施行合理的限制。

### 已知問題
{: #rn-issues}

[更新：API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery){: new_window}

[更新：工具](/docs/services/discovery?topic=discovery-getting-started#getting-started)

[更新：資料搜索器](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)

[更新：強化](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)

[更新：內容](/docs/services/discovery?topic=discovery-addcontent#addcontent)

-   您無法使用該工具來刪除文件。如果您需要刪除文件，必須如 API 參考資料所述使用 API 的[刪除文件](https://{DomainName}/apidocs/discovery#delete-a-document)方法。

-   API 目前不支援取得在文件汲取期間產生的通知（警告和錯誤）清單。因此，該工具無法顯示汲取通知清單，所以不容易判斷「資料搜索器」所搜索到的哪些文件（如果有的話）無法進行汲取。 
-   文件狀態資訊不一定精確。
    -   如果汲取作業所花費的時間超過所配置的 10 分鐘逾時，則該服務會報告其無法辨識出此文件，直到汲取作業完成為止。作業完成之後，文件狀態就會變成可用且精確。
    -   已順利檢索但產生錯誤的文件，可能短時間內的狀態為**失敗**，直到文件完全確定至索引為止。在文件確定至索引之後，列出的狀態才精確。
-   您無法使用該工具來取代特定文件。如果您嘗試這麼做，第二份文件會以個別文件的形式上傳。如果您要使用 API，且知道您要取代的文件 ID，您可以這麼做；請參閱 API 參考資料中的[更新文件](https://{DomainName}/apidocs/discovery#update-a-document)。如果您要使用「資料搜索器」，則從與前一個文件相同的 URL 上傳已更新的文件，會取代原始文件。
-   如果您要使用該工具來編輯配置中的強化，則只能編輯用於擷取的強化。如果您想要新增或編輯其他強化（例如，來自 {{site.data.keyword.knowledgestudiofull}} 模型的自訂強化），則必須使用 API。如需相關資訊，請參閱 API 參考資料中的[更新配置](https://{DomainName}/apidocs/discovery#update-a-configuration)方法。
-   下列附註特別適用於「資料搜索器」。 
    -   如果發生上傳失敗，「資料搜索器」會重試上傳。
    -   「資料搜索器」無法重試已順利上傳但無法轉換或檢索的文件。
    -   「資料搜索器」沒有功能可檢查下游狀態，以及嘗試重新上傳下游失敗的 URL。
    -   不容易判斷「資料搜索器」汲取了哪些文件。比方說，如果您針對一組 500 份的文件執行「資料搜索器」，則「資料搜索器」在提交 65 份文件（總計 212 份文件的集合）時可能報告失敗。剩餘 223 份文件的狀態為「不確定」。

        有暫行解決方法可用，但它很複雜，且涉及直接呼叫 API。請聯絡 {{site.data.keyword.IBM}} 支援人員以尋求協助。
-   {{site.data.keyword.discoveryshort}} 的 Java、Python 及 Node.js SDK 沒有提供預設 REST (cURL) API 所提供的所有功能。並非所有 cURL 方法在非 cURL SDK 中都有對等的方法，而且並非所有非 cURL 方法都提供其 cURL 對等項目具有的所有相同特性。換言之，Java、Python 及 Node.js SDK 目前只會提供 cURL API 功能的子集。
-   如果您使用 Word 轉換器，則使用 `style` 索引鍵比對標題，比使用 `level` 索引鍵更精確且更有效率。
