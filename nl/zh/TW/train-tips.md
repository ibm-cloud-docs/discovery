---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-03"

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

# 相關性訓練提示
{: #relevancy-tips}

 有關訓練集合的一般問題的回答，以及一般錯誤和警告訊息的說明。如需改善自然語言查詢相關性的相關資訊，請參閱[利用工具來改善結果相關性](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling)及[透過 API 來改善結果相關性](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api)。
{: shortdesc}

## 瞭解訓練
{: #understanding-training}

有關訓練集合的一般問題的回答。

### 如何得知我的系統是否經過訓練？
{: #understanding-system}

請使用 [List collection details ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery#get-collection-details){: new_window} API 指令來驗證您的系統是否已經過訓練。  

```bash
curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07"
```
{: pre}

範例回應：

```json
{
  "training_status": {
    "data_updated": "2017-02-10T14:18:22.786Z",
    "total_examples": 54,
    "sufficient_label_diversity": false,
    "processing": false,
    "minimum_examples_added": true,
    "successfully_trained": "2017-02-08T14:18:22.786Z",
    "available": true,
    "notices": 13,
    "minimum_queries_added": true    
    }
}
```

若要滿足訓練的需求，以下必須全部為 `true`：
- `minimum_queries_added`
- `minimum_examples_added`
- `sufficient_label_diversity`   

在回應中：
- `successfully_trained` 是前次順利完成訓練的時間。
- `available: true` 表示已做過訓練，且有模型可用。
- `processing: true` 表示正在進行訓練。
-  如果 `data_updated` 日期晚於 `successfully_trained` 日期，則表示自從最近一次資料上傳後，尚未訓練過新模型。  

### 如何檢查錯誤和警告？
{: #understanding-errors}

您可以使用[查詢通知 API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery#query-system-notices){: new_window} 來檢視錯誤或警告。  

```bash
curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/notices?version=2017-11-07"
```
{: pre}

其他 API 作業會列在[執行其他訓練資料查詢作業](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#training-data-operations)中。

### 如何解譯訓練後出現在自然語言查詢結果中的 `confidence` 評分？
{: #interpret-confidence}

如需相關資訊，請參閱[信賴度評分](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence)。  

## 解譯錯誤和警告
{: #interpreting-errors}

一般錯誤和警告訊息的說明。

### 警告：`Invalid training data found: The document was not returned in the top 100 search results for the given query, and will not be used for training`
{: #warning-docnotreturned}

此警告是因為訓練資料中的 `document_ids` 不符合針對該集合所執行之搜尋中的 `document_ids` 而引起。您應該檢查查詢，確定您所評比的文件的 `document_id` 會在該查詢的前 100 個結果中傳回。如果不會，您可能想要檢查兩件事：  

- 如果未在前 100 個結果中傳回該文件，則這可能不是高品質結果的理想範例，您可能想要重新視察選擇此文件的原因。  

- 如果根本未傳回該文件，則您應該檢閱未傳回的原因，並查看文件中是否有符合查詢部分的任何文字。  

**附註：**這個警告指出您可能有一個以上的不正確查詢，並不表示訓練不會發生。  

### 錯誤：`Invalid training data found: Syntax error when parsing query`
{: #error-syntax}

- 這表示實際查詢語法有問題。請驗證查詢會傳回結果，而且不會產生語法錯誤。只有當您將過濾器新增至自然語言查詢時，才可能發生此情況。

### 錯誤：`Invalid training data found: The query string provided exceeds the maximum length, please provide a shorter one`
{: #error-exceedlength}

- 查詢字串長度上限是 `2048`。您需要縮短特定的查詢。將過濾器併入查詢中，不失為暫行解決方法。  

### 錯誤：`This collection cannot be trained: your plan does not support training on this many top-level text fields.`
{: #error-toplevelfields}

- 此錯誤只發生於 `Lite` 方案。最上層欄位是未在另一個欄位下形成巢狀的欄位。訓練只發生在最上層欄位，並且會限制訓練處理程序中可以使用多少個欄位。集合中的最上層欄位越多，所需的訓練資料越多。此外，如果最上層欄位超過 `10` 個，訓練比較可能會遇到錯誤。 

### 錯誤：`Training data quality standards not met: You will need additional training queries with labeled examples. (To be considered for training, each example must appear in the top 100 search results for its query.)`
{: #error-labels}

- 這表示您需要新增更多訓練資料，才能順利完成訓練。您至少需要 49 個唯一的訓練查詢，每個查詢至少需要一個評比文件。最小值不等於最佳值；集合的大小及其他因素可能會增加符合最小值所需的訓練範例數目。  

### 錯誤：`Training data quality standards not met: Insufficient number of unique training queries. Expected at least n, but found m.`
{: #error-notunique}

- 為了符合最低訓練需求；您至少需要 49 個唯一的訓練查詢，每個查詢至少需要一個評比文件。如果您已超過此數目但仍收到此錯誤訊息，則應該檢查通知是否有其他錯誤。  

### 錯誤：`Training data quality standards not met: No documents found with non-zero relevance labels.`
{: #error-relevance}

- 訓練資料需要有足夠的標籤資料來指定哪些文件是高值。這表示您需要對某些具有非零值的文件進行評比。如果使用 Discovery 工具，則需要將某些文件評比為「相關」(`10`)；如果使用 API，則需要將部分文件標示為 `1` 或更高。   

### 錯誤：`Training data quality standards not met: Training examples have no relevance label variety for X queries.`
{: #error-variety}

- 訓練的其中一項需求是要具有足夠的標籤多樣性。這表示如果您想要得到一個經過完善訓練的系統，不只要新增其為最佳相關性相符項的文件，也應該新增「良好」相關文件。換言之，如果您的等級是 0-4，則除了評比為 4 的那些文件之外，它亦有助於將文件評比為 2 和 3。（如果您使用的是 Discovery 工具，則會將文件評比為「相關」(`10`) 或「不相關」(`0`)）。至少有 25% 的問題必須有一些標籤變化。   
