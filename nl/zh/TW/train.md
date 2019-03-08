---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-06"

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

# 利用 API 來改善結果相關性
{: #improving-result-relevance-with-the-api}

您可以訓練 {{site.data.keyword.discoveryshort}} 服務，以改善特定組織或主題區域的查詢結果的相關性。當您提供*訓練資料* 給 {{site.data.keyword.discoveryshort}} 實例時，該服務會使用機器學習 Watson 技術來尋找內容及問題中的信號。之後，該服務會將查詢結果重新排序，將最相關的結果顯示在最上面。當您新增更多訓練資料時，該服務實例在其傳回的結果順序上會變得更準確。
{: shortdesc}

相關性訓練為選用項目；如果您的查詢結果符合您的需求，則不需要進一步的訓練。如需建置訓練使用案例的概觀，請參閱此部落格文章：[如何善用 Revleupancy 訓練 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window}。

如需訓練 API 的綜合性資訊，請參閱 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}。

如果您偏好使用 {{site.data.keyword.discoveryshort}} 工具來訓練 {{site.data.keyword.discoveryshort}}，請參閱[利用工具來改善結果相關性](/docs/services/discovery/train-tooling.html)。

**附註：**相關性訓練目前僅套用於專用集合中的自然語言查詢。它不適用於結構化的「{{site.data.keyword.discoveryshort}} 查詢語言」查詢。如需「{{site.data.keyword.discoveryshort}} 查詢語言」的相關資訊，請參閱[查詢概念](/docs/services/discovery/using.html)。

經過訓練的集合將在自然語言查詢的結果中傳回 `confidence` 評分。如需詳細資料，請參閱[信賴度評分](/docs/services/discovery/train-tooling.html#confidence)。

如需訓練的最低需求及訓練限制，請參閱[訓練資料需求](/docs/services/discovery/train.html#reqs)。

如需追蹤用量以及使用此資料協助您瞭解及改善應用程式的詳細資料，請參閱[用量監視](/docs/services/discovery/feedback.html)。

<!-- A trained Discovery service instance is intended primarily for use with natural language queries, but it works equally well with queries that use structured syntax. -->  <!-- See [Query Concepts](/docs/services/discovery/using.html) and the [Query reference](/docs/services/discovery/query-reference.html) for information about structured queries and natural language queries. -->

訓練 Discovery 實例所需的元件包括下列各項：

 - **訓練資料**。這是該服務用來精簡查詢結果的一組*查詢* 和*範例*。
 - **查詢**。套用至訓練資料集的自然語言查詢。
   每一個查詢有一個以上的相關聯*範例*，如下列項目符號要點所述。
   每一個查詢在訓練資料集內必須是唯一的。
 - **範例**。這是在 Discovery 集合中檢索的文件，作為相關聯查詢的**良好或不正確**範例。當您將範例新增至訓練資料查詢時，您會包含一個相關性標籤，指出該文件套用至所指定查詢的相關性（或「良好」與「不正確」）。

   範例是以檢索的文件 ID 加以識別。如前所述，每個範例都必須包括一個標籤，指出該文件與查詢之間的相關性是「良好」或「不正確」。

   範例可以選擇性地指定交互參照查詢。交互參照查詢只需要傳回範例文件，而且必須與唯一的 Watson Discovery 文件 ID 無關。目前未自動使用交互參照查詢，但萬一在汲取事件期間有新 ID 指派給文件時，它可用來修復訓練資料。

## 訓練資料需求
{: #reqs}

訓練資料必須符合下列**最低**品質準則，才能有效改善 Discovery 服務所傳回答案的相關性。請注意，**最低**並不表示**最佳**。該服務會定期檢查訓練資料，以判斷是否符合這些需求，並根據任何變更而自動更新其本身。

- 集合的訓練資料集必須至少包含 49 個唯一的訓練查詢（亦即，查詢和範例集）。視集合的大小及複雜性而定，資料集的訓練查詢數可能需要高於 49，Watson 才能將相關性訓練套用至該集合。如果需要更多查詢才能訓練，Watson 會提供意見。
- 透過 API 指派相關性評分時：每一個訓練查詢的相關性評分都必須為非負整數，例如 `0` 代表*不相關*、`1` 代表*有點相關*，而 `2` 代表*高度相關*。不過，為了達到最大彈性，對於使用不同評分方法實驗的進階使用者，該服務接受 `0` 與 `100` 之間的非負整數。無論您使用的範圍為何，訓練查詢集的最大整數表示最大相關性。
- 透過工具指派相關性分級時：{{site.data.keyword.discoveryshort}} 工具使用相關性評分 `0` 來代表*不相關*，使用 `10` 來代表*相關*。您應該將這兩個可用的評比套用至結果：`Relevant` 和 `Not relevant`。只有評比 `Relevant` 文件不會提供所需的資料。如果您打算同時使用 {{site.data.keyword.discoveryshort}} 工具和 API 為文件進行評分，或打算先從 API 開始，再移至工具，請使用 `0` 和 `10` 相關性評分。
- 訓練查詢在查詢與所需回答之間必須包含某些詞彙重疊，以便範圍廣泛的 Discovery 服務起始搜尋可以擷取它。

**附註：**Watson 使用訓練資料來學習型樣及一般化，而非記憶個別訓練查詢。因此，對於任何給定的訓練查詢，該服務不一定會重新產生相同的相關性結果。

訓練不能超過下列**上限**需求：
  - 每個環境不能超出 24 個經過訓練的集合。
  - 在單一環境內，您只能執行 10,000 個訓練查詢，每個查詢最多有 100 個範例。 

## 將查詢新增至訓練資料集

使用 `POST /v1/environments/{environment_id}/collections/{collection_id}/training_data` 方法，將查詢新增至集合的訓練資料集。此查詢以下列格式指定為 JSON 物件：

```json
{
  "query_id": "string",
  "natural_language_query": "string",
  "filter": "string",
  "examples": [
    {
      "document_id": "string",
      "cross_reference": "string",
      "relevance": 0
    }
  ]
}
```
{: codeblock}

此物件中的值如下所示：

- `query_id`：查詢的唯一 ID。如果您未指定此欄位，則該服務會自動產生 ID。
- `natural_language_query`：適用於訓練集的 Discovery 自然語言查詢。<!-- The `natural_language_query` parameter is preferred. -->
- `filter`：查詢的選用過濾器，如[查詢參考資料](/docs/services/discovery/query-reference.html#parameter-descriptions)中所述。

    **附註：**如果您在訓練資料查詢中包含過濾器，當您在經過訓練的集合中使用自然語言查詢時，請務必使用相同的過濾器。如果您使用過濾的資料來訓練集合，但在查詢集合時未使用相同類型的過濾器，則結果可能無法預期。

- `examples`：包含下列值的陣列：

   - `document_id`：套用至訓練集之文件的唯一 ID。這是前述的*範例*。
   - `cross_reference`：一個選用標籤，通常由所參照文件中的一個欄位組成，萬一文件 ID 變更（例如，新汲取的文件獲指派相同的 ID），它會將文件和該欄位的資訊「固定」在原地。指定 `cross-reference` 的值**不**會將某個文件鏈結到另一個文件；而是在文件重新命名或改寫時，它可確保該服務保留文件的相關資訊。
   - `relevance`：從 `0` 到 `100`（含）的整數，指出查詢與訓練資料的相對相關性。值越高表示相關性越高。值 `0` 表示與查詢無關，而值 `100` 表示與查詢有絕對相關性。

   **附註：**雖然為了達到最大彈性，`relevance` 參數的範圍是 `0` 到 `100`，但您可以使用較小範圍來簡化評分範例。標準範圍可能是 `0` 到 `4`，您也可以使用整個範圍，但使用者增量只能是 20（`0`、`20`、`40`、`60`、`80` 及 `100`）。{{site.data.keyword.discoveryshort}} 工具使用 `0` 的相關性評分來代表*不相關*，使用 `10` 來代表*相關*。如果您打算同時使用 {{site.data.keyword.discoveryshort}} 工具和 API 為文件進行評分，或打算先從 API 開始，再移至工具，請使用 `0` 和 `10` 相關性評分。

下列物件顯示已移入資料的訓練資料查詢。

```json
{
  "natural_language_query": "why is the sky blue",
  "filter": "text:meteorology",
  "examples": [
    {
      "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
      "relevance": 0
    },
    {
      "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
      "relevance": 1
    },
    {
      "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
      "cross_reference": "my_id_field:1463",
      "relevance": 4
    }
  ]
}
```
{: codeblock}

下列指令範例會將先前的訓練資料查詢新增至 `a56dd9b4-040b-4ea3-a736-c1e7a467e191` 環境中的 `99040100-fe6a-4782-a4f5-28f9eee30850` 集合：

```bash
curl -X POST -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" -H "Content-Type: application/json" -d
'{
  "natural_language_query": "why is the sky blue",
  "filter": "text:meteorology",
  "examples": [
    {
    "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
    "relevance": 0
    },
    {
      "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
      "relevance": 1
    },
    {
      "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
      "cross_reference": "my_id_field:1463",
      "relevance": 4
    }
  ]
}'
"https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
```
{: pre}

## 將範例新增至訓練資料查詢

建立訓練資料查詢之後，您可以繼續對它新增範例，以改善訓練的正確性。請使用 `POST /v1/environments/{environment_id}/collections/{collection_id}/training_data/{query_id}`，將範例新增至現有的訓練資料查詢。

執行下列步驟，將範例新增至訓練資料查詢。

1. 透過[列出集合的訓練資料查詢 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#get-training-data){: new_window}，取得您要新增範例之訓練資料查詢的查詢 ID：

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
   ```
   {: pre}

   傳回的 JSON 格式如下：

   ```json
    {
      "query_id": "484baad4-d440-44b7-a0dd-70bb2ac77baa",
      "natural_language_query": "why is the sky blue",
      "filter": "text:meteorology",
      "examples": [
        {
          "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
          "relevance": 0
        },
        {
          "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
          "relevance": 1
        },
        {
          "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
          "cross_reference": "my_id_field:1463",
          "relevance": 4
        }
      ]
    }
   ```
   {: codeblock}

1. 使用您在建立新的訓練資料查詢時用來定義範例的相同語法來新增範例。下列指令範例不包含交互參照。

   ```bash
    curl -u -X POST -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" -H "Content-Type: application/json" -d
    '{
      "document_id": "46b52fdc-3a72-4700-9849-ac217532b373",
      "relevance": 3
    }' "https://gateway.watsonplatform.net/discovery/api/v1/environments//a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data/484baad4-d440-44b7-a0dd-70bb2ac77baa?version=2016-12-01"
   ```
   {: pre}

1. 同樣地，透過[列出集合的訓練資料查詢 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#get-training-data){: new_window}，驗證新範例已新增至訓練資料查詢：

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
   ```
   {: pre}

   傳回的 JSON 格式如下：

   ```json
    {
      "query_id": "484baad4-d440-44b7-a0dd-70bb2ac77baa",
      "natural_language_query": "why is the sky blue",
      "filter": "text:meteorology",
      "examples": [
        {
          "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
          "relevance": 0
        },
        {
          "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
          "relevance": 1
        },
        {
          "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
          "cross_reference": "my_id_field:1463",
          "relevance": 4
        },
        {
          "document_id": "46b52fdc-3a72-4700-9849-ac217532b373",
          "relevance": 3
        }
      ]
    }
   ```
   {: codeblock}

1. 使用[列出集合詳細資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#list-collection-details){: new_window} 方法並查看 `"training"`/`"available"` 欄位的值，以檢查訓練的狀態。當您新增的查詢和範例足以符合訓練需求時，欄位的值會傳回為 `true`，而服務會自動開始使用訓練資料。

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850?version=2016-12-01"
   ```
   {: pre}

   傳回的 JSON 格式如下：

   ```json
    {
      "collection_id": "99040100-fe6a-4782-a4f5-28f9eee30850",
      "name": "democollection",
      "configuration_id": "def9bd08-8472-470f-ab5a-e377f77e9300",
      "language": "en_us",
      "status": "available",
      "description": "this is a demo collection",
      "created": "2015-08-24T18:42:25.324Z",
      "updated": "2015-08-24T18:42:25.324Z",
      "document_counts": {
        "available": 1000,
        "processing": 20,
        "failed": 180
      },
      "disk_usage": {
        "used_bytes": 895111
      },
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
   {: codeblock}

1. 如果前一個步驟中的下列欄位全部傳回 `true`，請發出一些範例查詢，看看該服務是否會傳回更多相關結果：

   - `minimum_queries_added`
   - `minimum_examples_added`
   - `sufficient_label_diversity`

   如果結果的相關性未改善，請新增更多訓練查詢，直到結果符合您的需求為止。

如需其他訓練指引，請參閱[相關性訓練提示](/docs/services/discovery/train-tips.html#relevancy-tips)。   

## 執行其他訓練資料查詢作業
{: #training-data-operations}

您可以使用 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window} 中所述的其他 API 方法，來管理及維護訓練資料查詢：

 - [列出集合的訓練資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#get-training-data){: new_window}
 - [刪除集合的所有訓練資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-all-training-data){: new_window}
 - [顯示所指定訓練資料查詢的內容 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#show-td-query){: new_window}
 - [從集合中刪除訓練資料查詢 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/watson/developercloud/discovery/api/v1#delete-td-query-example){: new_window}
 - [變更訓練資料查詢範例的相關性標籤或交互參照 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#update-example){: new_window}
 - [從訓練資料查詢中刪除範例文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-example){: new_window}

 **錯誤監視：**訓練資料錯誤出現在通知中，您可以使用[查詢通知 API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-notices){: new_window}
 (`GET /v1/environments/{environment_id}/collections/{collection_id}/notices`) 進行監視。
