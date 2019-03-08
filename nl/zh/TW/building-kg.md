---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-09"

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

# Watson Discovery Knowledge Graph
{: #kg}

知識圖不只有資料和資訊，還能夠在文件之間的資料內建立連接及產生新知識。我們提供的 AI 技術透過擷取及釐清實體和關係、使用演算技術強化關係，以及使用相關性演算法將結果進行分級，從非結構化資料中自動建立自訂知識圖。知識圖 (Knowledge Graph) 可以作為公司的「知識中心」，並可用於企業搜尋、摘要、推薦引擎、其他決策制定處理程序（例如，偵測詐騙、浪費或濫用）。在「知識圖」建立程序中使用自訂模型（在 {{site.data.keyword.knowledgestudioshort}} 中所建立）有助於在諸如財務、技術、安全、情報、醫療和其他許多領域中，建立具有適用性的領域專用 KG。如需將 {{site.data.keyword.discoveryshort}} 與 {{site.data.keyword.knowledgestudioshort}} 整合的相關資訊，請參閱[與 {{site.data.keyword.knowledgestudiofull}} 整合](/docs/services/discovery/integrate-wks.html)。


新增至 {{site.data.keyword.discoveryfull}} 的兩個 RESTful 端點讓您能夠在非結構化文件集合中，跨文件搜尋已釐清、已強化的實體及關係。搜尋結果可依相關性或熱門程度分級。除了搜尋記號之外，API 還可以使用選用的上下文單字或段落，在自動建立的大型知識圖內找到更相關的實體和關係。

 下圖顯示「知識圖」如何融入現行 {{site.data.keyword.discoveryfull}} 管線中。{{site.data.keyword.nlushort}} 強化使用自訂 {{site.data.keyword.knowledgestudioshort}} 模型 (`en-news`)，以擷取個別文件層次的實體及關係。在建立「知識圖」期間，會使用隱含（自動）實體解析和圖形擴展技術，在文件之間自動建立實體與關係的連接圖。除了所建立的「知識圖」之外，Knowledge Graph 分析服務還新增了相關性分級技術來傳回結果。

![知識圖處理程序](images/knowledge-graph.png)

這個知識與分級技術的連接圖可協助下列使用案例：

-  釐清的實體，其利用模糊搜尋記號、類型資訊（選用）及上下文（選用）來達成。範例：在 `Apple` 的上下文中搜尋 `Steve`，最先傳回 `Steve Jobs`，而在 `Microsoft` 的上下文中搜尋 `Steve`，會先傳回 `Steve Ballmer`。
-  依相關性分級的關係，其透過輸入模糊搜尋記號和上下文（選用）來達成。相關性分級是利用圖形的廣域內容來顯示更具體的資訊。範例：在 `health` 上下文中搜尋 `Obama` 的關係會傳回 `Afforfordable Care Act` 和其他相關實體。
-  文件之間的推斷和聚集，其透過在連接的知識圖中查詢實體和關係來達成。這類查詢的一些範例如下：人員 X 與人員 Y 之間如何連接？員工 X 的資料存取模式與標準有何差異？人員 X 的影響範圍為何？

## 服務需求

在測試版期間，「知識圖」功能及其相關聯方法僅可用於已訂閱**進階**方案、**超值**方案的服務實例，以及所有專用環境。

目前僅支援英文版的這個測試版特性，如需詳細資料，請參閱[語言支援](/docs/services/discovery/language-support.html#feature-support)。

## 集合需求

{{site.data.keyword.discoveryshort}} 使用從所汲取文件中擷取的「實體」和「關係」來形成「知識圖」，並容許實體和關係查詢。

**附註：**[實體相似性](/docs/services/discovery/building-kg.html#similarity)、[證明](/docs/services/discovery/building-kg.html#evidence)和[標準化及過濾](/docs/services/discovery/building-kg.html#canonicalization)可使用於所有集合。對於在 `03-05-2018` 之前建立的集合，您需要重新汲取文件才能使用這些特性。

**附註：**「知識圖」只能用於專用資料集合，而非設計成與 {{site.data.keyword.discoverynewsshort}} 搭配使用。

若要使用「知識圖」，必須配置集合以符合下列特定需求：

-  對於利用「知識圖」的欄位必須同時指定 `entities` 和 `relations` 這兩個強化，而且每一個強化都必須使用相同的自訂模型。如果使用公用模型（在不使用 {{site.data.keyword.knowledgestudioshort}} 的情況下可用），則必須以自訂模型 `model="en-news"` 的格式指定它。

-  必須如下所示指定 `relations` 強化：
   ```json
   "relations": {
     "model": "en-news"
   }
   ```
   {: codeblock}

-  必須如下所示指定 `entities` 強化，而且必須同時指定 `mentions`、`mentions_types` 及 `sentence_locations` 參數：
   ```json
   "entities": {
     "mentions": true,
     "mention_types": true,
     "sentence_locations": true,
     "model": "en-news"
    }
    ```
   {: codeblock}

   如果想要的話，也可以指定其他選用的 `enrichments` 選項，例如 `"sentiment": true`。它們將儲存在探索索引中作為強化選項，但不會用來作為知識庫本身的節點。

使用 {{site.data.keyword.discoveryshort}} 工具**無法新增**這些選項，必須使用 API 來上傳自訂配置。[這裡](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/discovery/config-default-kg.json)有一個可用的預設配置副本，它已修改為強化 `text` 欄位，使集合可以與具有公用模型的知識圖搭配使用。

在建立 {{site.data.keyword.discoveryshort}} 服務實例之後，如下所示建立自訂配置：

1. 發出下列指令，以建立一個稱為 `my-first-environment` 的環境。將 `{apikey_value}` 取代為您的服務 API 金鑰的值：

   ```bash
   curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "api/v1/environments?version=2017-11-07"
   ```
   {: pre}

   API 會傳回諸如環境 ID、環境狀態及環境使用的儲存體數量等資訊。

   您需要傳回的 `{environment_id}`；請務必儲存該 ID 以供稍後使用。

1. 接下來，建立自訂配置。此程序假設您要上傳的項目在 [這裡](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/discovery/config-default-kg.json)。如果您要建置自己的自訂配置，請參閱 [配置參考資料](/docs/services/discovery/custom-config.html)。

   ```bash
   curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d @config-default-kg.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07"
   ```
   {: pre}

   **如果您已有自訂配置，且想要更新它並使用它**，請在此指令中使用您自訂配置的 {configuration ID}。

   ```bash
   curl -X PUT -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d @config-default-kg.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration ID}?version=2017-11-07"
   ```
   {: pre}

1. 上傳了自訂配置之後，它便可以用於您所建立的任何集合中，只要指定了自訂配置，就可以使用任何方法來上傳文件。如果您不熟悉如何建立集合及上傳文件，請參閱[開始使用工具](/docs/services/discovery/getting-started-tool.html)。當您到達[步驟 3](/docs/services/discovery/getting-started-tool.html#create-custom-configuration) 時，請選取「知識圖配置」而不是建立新配置。

## 標準化及過濾
{: #canonicalization}

在 2018 年 3 月 5 日或此日期之後汲取之文件中的所有實體，將以從公用字典衍生的標準名稱正規化。此外，實體或關係中所包含的任何代名詞（例如 `he`、`she`、`they` 或 `it`）會在汲取至「知識圖」之前自動過濾掉。在 2018 年 3 月 5 日之前所汲取的文件將不會包括此層次的標準化及過濾；您應該建立新的集合並重新汲取文件，才能使用此特性。

在「知識圖」中建置實體查詢或關係查詢時，您可以在 `query_entities` 或 `query_relations` 方法的 `text` 欄位中輸入實體的標準名稱或原始文字。


## 實體查詢
{: #entities}

「知識圖」實體查詢的測試版支援環境定義型實體 [釐清](/docs/services/discovery/building-kg.html#disambiguation) 及 [相似性](/docs/services/discovery/building-kg.html#similarity) 查詢。「知識圖」實體查詢的執行方式是將一個 `JSON` 物件 `POST` 到 `v1/environments/{environment_id}/collections/{collection_id}/query_entities` 端點。

您可以使用 API 或使用 {{site.data.keyword.discoveryshort}} 工具來查詢實體。如需工具資訊，請參閱[使用 Discovery 工具來查詢知識圖](/docs/services/discovery/building-kg.html#querying-kg)。

「知識圖」實體查詢 JSON 物件採用下列格式：

```json
{
  "feature": "disambiguate",
  "entity": {
    "text": "Steve",
    "type": "Person",
    "exact": "false"
  },
  "context": {
    "text": "iphone"
  },
  "count": 10,
  "evidence_count": 0
}
```
{: codeblock}

-  `"feature": string` _必要_ - 要使用的實體查詢特性。支援的特性如下：[disambiguate](/docs/services/discovery/building-kg.html#disambiguation) 及 [similar_entities](/docs/services/discovery/building-kg.html#similarity)。
-  `"entity": {}` _必要_ - 包含要釐清之實體資訊的物件。
   -  `"text": string` _必要_ - 要釐清的實體文字
   -  `"type": string` _選用_ - 要釐清的選用性實體類型，如未指定，則包括所有類型。
   -  `"exact": boolean` _選用_ - 若為 `false`，則執行隱含釐清。隱含釐清將對每一個輸入實體物件使用第一個已釐清實體。應該將 `"feature": "disambiguate"` 設定為 `false`。預設值為 `false`。
-  `"context": {}` _選用_ - 包括釐清的環境定義需求的選用性物件。
   -  `"text": string` _選用_ - 根據該關聯為查詢的實體和等級提供環境定義的實體文字。例如，如果您想要查詢英國倫敦這個城市，您的查詢會尋找 `London`，其環境定義為 `England`。此輸入可以是局部名稱，或是包含相關實體詞彙的大型段落。可以同時傳遞多個詞彙。
-  `"count": INT` _選用_ - 要傳回的已釐清實體數目。預設值為 `10`。最大值為 `1000`
-  `"evidence_count": INT` _選用_ 要針對每個識別的實體傳回的證明實例數目。預設值為 `0`。`evidence_count` 欄位的最大值為 10,000，再除以 `count` 欄位中指定的數目。如需詳細說明及範例，請參閱這個頁面的 [證明](/docs/services/discovery/building-kg.html#evidence) 區段。

該查詢傳回下列格式的結果：

```json
{
  "entities": [
    {
      "text": "Steve Jobs",
      "type": "PERSON"
    },
    {
      "text": "Steve Wozniak",
      "type": "PERSON"
    }
  ]
}
```
{: codeblock}

如果找不到相符項目，則會傳回下列 JSON 物件：

```json
{
  "entities": []
}
```
{: codeblock}

### 實體釐清
{: #disambiguation}

「知識圖」實體查詢提供內容型實體釐清。根據所提供的實體文字和選用性環境定義文字，`disambiguation` 可識別唯一實體，並傳回根據環境定義資訊分級的實體清單。

要求實體釐清查詢時，需指定 `"disambiguation"` 作為知識圖查詢物件中 `"feature" :` 欄位的值。

例如，在 `iphone` 的環境定義中釐清實體文字 `Steve` 可能會導致傳回 `Steve Jobs` 及 `Steve Wozniak`。


### 實體相似性
{: #similarity}

「知識圖」實體查詢提供環境定義型實體相似性偵測。根據所提供的實體文字和選用性環境定義文字，`similar_entities` 可識別唯一實體，並傳回根據環境定義資訊分級的實體清單。

要求實體相似性查詢時，需指定 `"similar_entities"` 作為知識圖查詢物件中 `"feature" :` 欄位的值。

例如，如果您在環境定義 `car` 中尋找 `Ford` 的類似實體，則類似實體結果可能包括 `GM`、`Toyota` 及 `Nissan`。

## 關係查詢
{: #relations}

「知識圖」關係查詢支援根據輸入實體來尋找最相關的關係，其使用隱含的實體釐清、環境定義型關係、依相關性評分和提及次數排序，以及依類型和文件 ID 過濾。

您可以使用 API 或使用 {{site.data.keyword.discoveryshort}} 工具來查詢關係。如需工具資訊，請參閱[使用 Discovery 工具來查詢知識圖](/docs/services/discovery/building-kg.html#querying-kg)。

「知識圖」實體查詢的執行方式是將一個 `JSON` 物件 `POST` 到 `v1/environments/{environment_id}/collections/{collection_id}/query_relations` 端點。「知識圖」關係查詢 JSON 物件採用下列格式：

```json
{
  "entities": [
    {
      "text": "Steve Jobs",
      "type": "PERSON",
      "exact": true
    }
  ],
  "context": {
    "text": "iphone"
  },
  "sort": "score",
  "filter": {
    "relation_types": {
      "exclude": ["colocation"],
      "include": ["locatedAt", "employedBy", "managerOf", "founderOf"]
    },
    "entity_types": {
      "exclude": ["EVENT"],
      "include": ["PERSON", "GPE", "ORGANIZATION"]
    },
    "document_ids": ["b95df4c1-d00f-4771-abb2-a52baea0444a", "ad340635-bf3e-47a5-bea5-5e778f600c32"]
  },
  "count": 10,
  "evidence_count": 0
}
```
{: codeblock}

-  `"entities": []` _必要_ - 包含將查詢關係之實體的陣列。如果只定義一個實體物件，則傳回所有鄰接項關係。如果定義多個實體物件，則傳回相互配對關係。相互配對關係會傳回輸入實體之間的直接關係，而不是與所有實體鄰接項的關係。每一個實體物件包含：
   -  `"text": string` _必要_ - 實體文字。
   -  `"type": string` _選用_ - 選用性實體類型。如果 `"exact"` 為 `true`，則此為必要欄位。
   -  `"exact": boolean` _選用_ - 若為 `false`，則執行隱含釐清。隱含釐清將對每一個輸入實體物件使用第一個已釐清實體。預設值為 `false`。
-  `"context": {}` _選用_ - 包括環境定義需求的選用性物件。
   -  `"text": string` _選用_ - 根據該關聯為查詢的實體和等級提供環境定義的實體文字。例如，如果您想要查詢英國倫敦這個城市，您的查詢會尋找 `London`，其環境定義為 `England`。此輸入可以是局部名稱，或是包含相關實體詞彙的大型段落。可以同時傳遞多個詞彙。
-  `"sort": string` _選用_ - 關係的排序方法，可以是 `score` 或 `frequency`。預設值為 `score`。`score` 是基於關係和鄰接項對輸入實體的相關性以及對所提供環境定義的相關性。`frequency` 是唯一識別每個關係的次數。
-  `"filter": {}` _選用_ - 包含關係類型、實體類型以及要針對此查詢而進行過濾之特定文件的物件。依預設，不會排除任何項目。
   -  `"relation_types": {}` _optional_ 要過濾的關係類型清單。
      -  `"exclude": []` _選用_ 要從查詢中排除之關係類型的逗點區隔清單。
      -  `"include": []` _選用_ 明確包含在查詢中之關係類型的逗點區隔清單。如果已指定，則會視為已排除所有其他類型。
   -  `"entity_types": {}` _選用_ 要過濾鄰接項的實體類型清單。不適用於多個實體輸入，因為不會傳回新的鄰接項。
      -  `"exclude": []` _選用_ 要從查詢中排除之關係類型的逗點區隔清單。
      -  `"include": []` _選用_ 明確包含在查詢中之實體類型的逗點區隔清單。如果已指定，則會視為已排除所有其他類型。
   -  `"document_ids": []` _選用_ 要執行關係查詢之文件的逗點區隔清單。
-  `"count": INT` _選用_ 要傳回的關係數目。預設值為 `10`。最大值為 `1000`。
-  `"evidence_count": INT` _選用_ 要針對每個識別的關係傳回的證明實例數目。預設值為 `0`。`evidence_count` 欄位的最大值為 10,000，再除以 `count` 欄位中指定的數目。如需詳細說明及範例，請參閱這個頁面的[證明](/docs/services/discovery/building-kg.html#evidence)區段。

該查詢傳回下列格式的結果：

```json
{
  "relations": [
    {
      "type": "FOUNDEROF",
      "frequency": 7,
      "arguments": [
        {
          "entities": [
            {
              "type": "PERSON",
              "text": "Steve Jobs"
            }
          ]
        },
        {
          "entities": [
            {
              "type": "ORGANIZATION",
              "text": "Apple"
            }
          ]
        }
      ]
    }
  ]
}
```
{: codeblock}

在關係陣列的每個物件中，傳回的引數陣列包含一對實體陣列，第一個是來源或主體，第二個是關係的目標或物件。

如果找不到相符項，則傳回下列 JSON 物件：

```json
{
  "relations": []
}
```
{: codeblock}

## 證明
{: #evidence}

對於某些實體或關係查詢而言，瞭解識別連線的位置很重要。連線的證明可讓您參照原始文件、澄清結果，或進一步做適當的釐清。從 `03-05-2018` 之後建立的集合開始，`query_entities` 和 `query_relations` 端點可選擇在傳回的結果中提供證明。此特性可用於 `03-05-2018` 之前建立的集合，但需要重新汲取文件，才能對那些較舊集合使用此特性。
透過將 `"evidence_count": INT` 欄位新增至查詢物件來傳回證明。此數字代表將針對每個回應項目傳回的證明項目數。比方說，如果您指定 `"count":` 為 `5` 個回應項目，且 `"evidence_count": 2`，則回應會包含總計 `10` 個證明項目（每個回應 2 個）。針對單一查詢所傳回的證明項目數上限總計為 10,000。

在 `query_entities` 回應中，`entities` 陣列中的每個物件都會包含所指定數目的 `evidence` 物件。這些物件包括：找到證明之文件的 `document_id`、其所在的 `field`、證明在該欄位內的位置，以及所識別實體的確切位置。

```json
    {
      "text": "Steve Jobs",
      "type": "Person",
      "evidence": [
        {
          "document_id": "cb77ce6b-bb93-42a0-8643-dfb523e14da8",
          "field": "description",
          "start_offset": 305,
          "end_offset": 392,
          "entities": [
            {
              "type": "Person",
              "text": "Steve Jobs",
              "start_offset": 311,
              "end_offset": 321
            }
          ]
        }
      ]
    }

```
{: codeblock}

在 `query_relations` 中，`relations` 陣列中的每個物件都會包含所指定數目的 `evidence` 物件。所傳回 `evidence` 的結構與 `query_relations` 中的結構相同，並包含所有指定之相關實體的位置：he returned `evidence` is structured the same as in `query_relations` with the locations of all related entities specified:

```json
    {
      "type": "founderOf",
      "frequency": 7,
      "arguments": [
        {
          "entities": [
            {
              "type": "Person",
              "text": "Steve Jobs"
            }
          ]
        },
        {
          "entities": [
            {
              "type": "Organization",
              "text": "Apple"
            }
          ]
        }
      ],
      "evidence": [
        {
          "document_id": "b95df4c1-d00f-4771-abb2-a52baea0444a",
          "field": "text",
          "start_offset": 243,
          "end_offset": 303,
          "entities": [
            {
              "type": "Organization",
              "text": "Apple",
              "start_offset": 293,
              "end_offset": 298
            },
            {
              "type": "Person",
              "text": "Steve Jobs",
              "start_offset": 243,
              "end_offset": 253
            }
          ]
        }
      ]
    }
```
{: codeblock}

## 使用 Discovery 工具查詢知識圖
{: #querying-kg}

其服務實例已訂閱 [**進階**](/docs/services/discovery/building-kg.html#service-requirements) 方案的那些人，可使用 {{site.data.keyword.discoveryshort}} 工具來查詢具有「知識圖」的專用集合。

若要在 {{site.data.keyword.discoveryshort}} 工具中存取「知識圖」查詢，請執行下列動作：

1.  按一下 ![查詢圖示](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> 以開啟查詢頁面。
1.  選取您的集合，然後按一下**開始使用**。
1.  在**建置查詢**畫面中，選擇**知識圖**標籤，然後選擇**實體**或**關係**。

**附註：**使用 {{site.data.keyword.discoveryshort}} 工具時，並非所有「知識圖」特性都可供使用。
