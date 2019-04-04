---

copyright:
  years: 2019
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

# 高可用性和災難回復
{: #recovery}

{{site.data.keyword.discoveryfull}} 支援無單一失敗點的高可用性。此外，客戶有責任備份 {{site.data.keyword.discoveryshort}} 資料，以支援您自己的災難回復計劃，才能重建您的服務。
{: shortdesc}

{{site.data.keyword.discoveryshort}} 資料流量會在一個地區內的多個區域之間進行負載平衡。每個區域都是相同地區內的資料中心。如需相關資訊，請參閱[如何確保零關閉時間？![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/docs/overview?topic=overview-zero-downtime#zero-downtime){: new_window}。

## 備份 Watson Discovery 中的資料
{: #backup}

有數個方法可以用來備份儲存在 {{site.data.keyword.discoveryfull}} 中的資料。這些方法應該納入您的災難回復計劃中。

-  您應該保留資料（例如原始文件）的副本
-  {{site.data.keyword.discoveryshort}} 儲存的資料，您應該加以擷取並備份
  
有些資料需要重新建立（例如，您無法備份的資料，像是意見事件等。） 

### 汲取的文件
{: #backupdocs}

您上傳的文件會轉換並強化，然後儲存在搜尋索引中。發生災難時，無法回復搜尋索引，因此，您應該將所有原始文件的備份儲存在安全的地方。

如果您也有對外部資料來源執行排程的搜索來匯入文件，則應將資料來源認證保存在外部，以便快速重新建立資料來源。請參閱[連接至資料來源](/docs/services/discovery?topic=discovery-sources#sources)，以取得可用來源清單和各來源需要的認證。

### 配置
{: #backupconfigs}

發生災難事件時，您應該備份實例配置，並將其儲存在本端。 

若要備份這些配置，請先針對每個實例[列出您的配置](https://cloud.ibm.com/apidocs/discovery#list-configurations)。 

取得配置清單之後，針對每個配置[取得詳細資料](https://cloud.ibm.com/apidocs/discovery#get-configuration-details)。

### 訓練資料
{: #backuptraining}

發生災難事件時，您應該為每個已訓練的集合備份訓練資料，並將其儲存在本端。 

訓練資料可用來明確訓練您的集合，且其是依各集合儲存。 

若要擷取訓練資料，請使用 API 從 {{site.data.keyword.discoveryshort}} 下載查詢和評級。 

1.  [列出訓練資料](https://cloud.ibm.com/apidocs/discovery#list-training-data)
1.  針對每個查詢[列出範例](https://cloud.ibm.com/apidocs/discovery#list-examples-for-a-training-data-query)。
1.  針對訓練資料範例[取得詳細資料](https://cloud.ibm.com/apidocs/discovery#get-details-for-training-data-example)。 

您在訓練資料中使用的 `document ids` 會指向現行集合中的文件。您「必須」在新的集合中使用相同的 `document ids`，以確保參照正確的 ID。否則，所還原的相關性訓練「將無法運作」。
{: important} 

### 查詢
{: #backupqueries}

依預設（除非您拒絕），{{site.data.keyword.discoveryshort}} 會儲存您傳送給它的查詢。 

如果您想要針對[統計目的](https://cloud.ibm.com/apidocs/discovery#number-of-queries-over-time)來還原這些查詢，則應將這些查詢個別儲存。 

您可以從 {{site.data.keyword.discoveryshort}} [擷取查詢](https://cloud.ibm.com/apidocs/discovery#search-the-query-and-event-log)，但儲存上限為 10,000 個查詢。沒有分頁 API。我們不建議還原查詢；建議您重新開始。

### 意見/點按
{: #clicks}

如果您以意見事件的形式儲存點按記錄，目前並沒有簡單的方式可以備份及還原此資訊。建議您使用 [clicks/feedback data](https://cloud.ibm.com/apidocs/discovery#create-event) API 重新開始。

### 擴展清單
{: #backupexpansions}

如果您使用擴展來進行查詢修改，則應備份擴展清單，並儲存在本端。若要執行此作業，請使用 [get expansion list](https://cloud.ibm.com/apidocs/discovery#get-the-expansion-list) API 指令來要求擴展清單，並儲存在本端。

### 記號化字典或停用字詞
{: #backupstopwords}

如果使用這些功能，您需要備份這些檔案，並儲存在本端。就停用字詞而言，請備份文字檔，而就記號化而言，您應該要備份 JSON 檔案。如需各檔案類型的相關資訊，請參閱[建立自訂記號化字典](/docs/services/discovery?topic=discovery-query-concepts#tokenization)和[定義停用字詞](/docs/services/discovery?topic=discovery-query-concepts#stopwords)。

### 集合資訊
{: #collectioninfo}

這不是必要資訊，但最佳作法是定期針對每個集合[擷取狀態](https://cloud.ibm.com/apidocs/discovery#get-collection-details)，並將該資訊儲存在本端。若保留這些統計資料，之後您就可以在必要時，驗證您的還原程序是否成功。
{: tip} 


### 智慧型文件理解模型
{: #backupsdu}

如果您使用「智慧型文件理解 (SDU)」，您將會有與配置相關聯的模型。為避免此資訊遺失，您應該要[匯出您的模型](/docs/services/discovery?topic=discovery-sdu#import)、加以備份，並將其儲存在本端。SDU 模型的副檔名為 `.sdumodel`。


## 將資料還原至新的 Watson Discovery 實例
{: #restore}

請考慮使用備份來還原至位於不同「資料中心」（又稱為地區/位置 - 例如，達拉斯、休士頓、華盛頓特區、倫敦）的新 {{site.data.keyword.discoveryshort}} 實例。
{: note}

若要開始還原，請先檢閱您的集合與關聯資料來源清單，以及檔案備份。

-  使用所儲存的配置資訊，建立您的[環境](https://cloud.ibm.com/apidocs/discovery#create-an-environment)和[集合](https://cloud.ibm.com/apidocs/discovery#create-a-collection)。確定已正確定義適當的配置，並且已正確設定集合的語言。否則，將會耽誤您的系統回復正常運作。
-  如果您之前有任何自訂配置設定在 {{site.data.keyword.discoveryshort}} 中，將會需要[重建那些自訂配置](/docs/services/discovery?topic=discovery-configservice#when-you-need-a-custom-configuration)。 
-  將記號化字典或停用字詞新增回集合中。請參閱[建立自訂記號化字典](/docs/services/discovery?topic=discovery-query-concepts#tokenization)和[定義停用字詞](/docs/services/discovery?topic=discovery-query-concepts#stopwords)。 
-  如果您之前有自訂的查詢擴展，也需要針對每個集合[新增您的查詢擴展](https://cloud.ibm.com/apidocs/discovery#create-or-update-expansion-list)。 
-  如果您之前有使用 Watson Knowledge Studio (WKS) 中的任何自訂實體模型來進行強化，則需要[將該模型重新匯入](/docs/services/discovery?topic=discovery-configservice#custom-entity-model)至您的 {{site.data.keyword.discoveryshort}} 實例中。

將集合設定成和以前一樣之後，就需要開始汲取您的原始文件。依據您先前汲取文件的方式而定，您可以使用的方法如下：
-  [API](https://cloud.ibm.com/apidocs/discovery#add-a-document)
-  [連接器](/docs/services/discovery?topic=discovery-sources#sources) 
-  [資料搜索器](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)
-  或其他方法

### 還原訓練資料
{: #restoretraining}

集合還原之後，即可開始[重建相關性訓練模型](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api)的程序。 

擷取您備份的訓練資料，然後：

1. [上傳查詢](https://cloud.ibm.com/apidocs/discovery#add-query-to-training-data)
1. 針對每個查詢[上傳範例文件](https://cloud.ibm.com/apidocs/discovery#add-example-to-training-data-query)。
1.  上傳訓練資料之後，請參閱[部落格文章](https://developer.ibm.com/dwblog/2017/get-relevancy-training/)，以確保您符合先前的精確度數值。請記住，舊的 `document ids` 必須轉移至新的訓練資料，或是加以更新，以反映新集合中的新文件 ID。


### 還原與外部資料來源的連線
{: #restoreconnections}

如果資料不慎遺失，您可能會失去已排程的外部資料來源搜索。請參閱[連接至資料來源](/docs/services/discovery?topic=discovery-sources#sources)，以取得可用來源清單。

若要還原外部資料，您需要重新建立與這些資料來源的連線，然後重新搜索。

尋找您先前儲存的資料來源認證，並遵循[這裡](/docs/services/discovery?topic=discovery-sources#sources)的指示。如此可讓您重新連接資料來源，並將資料匯入 {{site.data.keyword.discoveryshort}} 中。


### 還原智慧型文件理解模型
{: #restoresdu}

若要匯入先前匯出的「智慧型文件理解 (SDU)」模型，請遵循[這裡](/docs/services/discovery?topic=discovery-sdu#import)的指示。SDU 模型的副檔名為 `.sdumodel`。

將 SDU 現有的模型匯入新的集合時，最好可以建立新的集合，並新增一個文件，然後匯入該模型，再上傳其餘的文件。
