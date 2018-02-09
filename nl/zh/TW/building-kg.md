---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-15"

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

知識圖不只有資料和資訊，還能夠在文件之間的資料內建立連接及產生新知識。我們提供的 AI 技術透過擷取及釐清實體和關係、使用演算技術強化關係，以及使用相關性演算法將結果進行分級，從非結構化資料中自動建立自訂知識圖。知識圖 (Knowledge Graph) 可以作為公司的「知識中心」，並可用於企業搜尋、摘要、推薦引擎、其他決策制定處理程序（例如，偵測詐騙、浪費或濫用）。在「知識圖」建立程序中使用自訂模型（在 {{site.data.keyword.knowledgestudioshort}} 中所建立）有助於在諸如財務、技術、安全、情報、醫療和其他許多領域中，建立具有適用性的領域專用 KG。

已在 {{site.data.keyword.discoveryfull}} 中新增了兩個新端點，讓您能夠在非結構化文件集合中，跨文件搜尋釐清的實體和強化的關係。搜尋結果可依相關性或熱門程度分級。除了搜尋記號之外，API 還可以使用選用的環境定義單字或段落，在自動建立的大型知識圖內找到更相關的實體和關係。

 下圖顯示「知識圖」如何融入現行 {{site.data.keyword.discoveryfull}} 管線中。{{site.data.keyword.nlushort}} 會利用個別文件層次的實體和文件來強化文件。在建立「知識圖」期間，會使用隱含（自動）實體解析和圖形擴展技術，在文件之間自動建立實體與關係的連接圖。除了所建立的「知識圖」之外，Knowledge Graph 分析服務還新增了相關性分級技術來傳回結果。

![知識圖處理程序](images/knowledge-graph.png)

這個知識與分級技術的連接圖提供：

-  釐清的實體，其利用模糊搜尋記號、類型資訊（選用）及環境定義（選用）來達成。範例：在 `Apple` 的環境定義中搜尋 `Steve`，最先傳回 `Steve Jobs`，而在 `Microsoft` 的環境定義中搜尋 `Steve`，會先傳回 `Steve Ballmer`。
-  依相關性分級的關係，其透過輸入模糊搜尋記號和環境定義（選用）來達成。相關性分級是利用圖形的廣域內容來顯示更具體的資訊。範例：在 `health` 環境定義中搜尋 `Obama` 的關係會傳回 `Afforfordable Care Act` 和其他相關實體。
-  文件之間的推斷和聚集，其透過在連接的知識圖中查詢實體和關係來達成。這類查詢的一些範例如下：人員 X 與人員 Y 之間如何連接？員工 X 的資料存取模式與標準有何差異？人員 X 的影響範圍為何？

## 服務需求

在測試版期間，「知識圖」功能及其相關聯方法僅可用於已訂閱**進階**方案的服務實例。

## 集合需求

{{site.data.keyword.discoveryshort}} 使用從所汲取文件中擷取的「實體」和「關係」來形成「知識圖」，並容許實體和關係查詢。

**附註：**「知識圖」只能用於專用資料集合，而非設計成與 {{site.data.keyword.discoverynewsshort}} 搭配使用。

若要使用「知識圖」，必須配置集合以符合下列特定需求：

-  對於利用「知識圖」的欄位必須同時指定 `entities` 和 `relations` 這兩個強化，而且每一個強化都必須使用相同的自訂模型。如果需要公用模型，則必須以自訂模型 `model="en-news"` 的格式指定它。

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

   如果想要的話，也可以指定其他選用的 `enrichments` 選項，例如 `"sentiment": true`。

這些選項無法使用 {{site.data.keyword.discoveryshort}} 工具來新增，必須使用 API 來上傳自訂配置。[這裡](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/discovery/config-default-kg.json)有一個可用的預設配置副本，它已修改為強化 `text` 欄位，使集合可以與具有公用模型的知識圖搭配使用。

在建立 {{site.data.keyword.discoveryshort}} 服務實例之後，如下所示建立自訂配置：

1. 發出下列指令，以建立一個稱為 `my-first-environment` 的環境。將 `{username}` 和 `{password}` 取代為您的服務認證：

```bash
   curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "api/v1/environments?version=2017-11-07"
```
   {: pre}

   API 會傳回諸如環境 ID、環境狀態以及環境使用的儲存體數量等資訊。

   您需要所傳回的 `{environment_id}`。

1. 接下來，建立自訂配置。此程序假設您要上傳的項目出現在[這裡](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/discovery/config-default-kg.json)。如果您要建置自己的自訂配置，請參閱[配置參考資料](/docs/services/discovery/custom-config.html)。

```bash
   curl -X PUT -u "{username}":"{password}" -H "Content-Type: application/json" -d config-default-kg.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07"
```
   {: pre}

1. 上傳了自訂配置之後，它便可以用於您所建立的任何集合中，只要指定了自訂配置，就可以使用任何方法來上傳文件。如果您不熟悉如何建立集合及上傳文件，請參閱[開始使用工具](/docs/services/discovery/getting-started-tool.html)。當您到達[步驟 3](/docs/services/discovery/getting-started-tool.html#create-custom-configuration) 時，請選取 `Knowledge Graph Configuration`，而不要建立新配置。

## 實體查詢
{: #entities}

在 Knowledge Graph 的測試版中，實體查詢支援基於環境定義的實體釐清。根據所提供的實體文字和選用的環境定義文字，釐清可識別唯一實體，並傳回根據環境定義資訊分級的實體清單。「知識圖」實體查詢的執行方式是將一個 `JSON` 物件張貼 (`POST`) 至 `v1/environments/{environment_id}/collections/{collection_id}/query_entities` 端點。

您可以使用 API 或使用 {{site.data.keyword.discoveryshort}} 工具來查詢實體。如需工具資訊，請參閱[使用 Discovery 工具查詢知識圖](/docs/services/discovery/building-kg.html#querying-kg)。

「知識圖」實體查詢 JSON 物件採用下列格式：

```json
{
  "feature": "disambiguate",
  "entity": {
    "text": "Steve",
    "type": "Person"
  },
  "context": {
    "text": "iphone"
  },
  "count": 10
}
```
{: codeblock}

-  `"feature": string` _必要_ - 要使用的實體查詢特性，必須為 `disambiguate`。
-  `"entity": {}` _必要_ - 包含要釐清之實體資訊的物件。
   -  `"text": string` _必要_ - 將釐清的實體文字
   -  `"type": string` _選用_ - 要釐清的選用性實體類型，如未指定，則包括所有類型。
-  `"context": {}` _選用_ - 包括釐清的環境定義需求的選用性物件。
   -  `"text": string` _選用_ - 要為查詢實體提供環境定義並根據該關聯進行分級的實體文字。例如，如果您想要查詢英國倫敦這個城市，您的查詢會尋找含有 `England` 環境定義的 `London`。此輸入可以是局部名稱，或是包含相關實體詞彙的大型段落。可以同時傳遞多個詞彙。
-  `"count": INT` _選用_ - 要傳回的所釐清實體數目。預設值為 `10`。最大值為 `1000`

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

如果找不到相符項，則傳回下列 JSON 物件：

```json
{
  "entities": []
}
```
{: codeblock}

## 關係查詢
{: #relations}

「知識圖」關係查詢支援根據輸入實體來尋找最相關的關係，其使用隱含的實體釐清、基於環境定義的關係、依相關性評分和提及次數排序，以及依類型和文件 ID 過濾。

您可以使用 API 或使用 {{site.data.keyword.discoveryshort}} 工具來查詢關係。如需工具資訊，請參閱[使用 Discovery 工具查詢知識圖](/docs/services/discovery/building-kg.html#querying-kg)。

「知識圖」實體查詢的執行方式是將一個 `JSON` 物件張貼 (`POST`) 至 `v1/environments/{environment_id}/collections/{collection_id}/query_relations` 端點。「知識圖」關係查詢 JSON 物件採用下列格式：

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
  "count": 10
}
```
{: codeblock}

-  `"entities": []` _必要_ - 包含將查詢關係之實體的陣列。如果只定義一個實體物件，則傳回所有鄰接項關係。如果定義多個實體物件，則傳回相互配對關係。相互配對關係會傳回輸入實體之間的直接關係，而不是與所有實體鄰接項的關係。每個實體物件包含：
   -  `"text": string` _必要_ - 實體文字。
   -  `"type": string` _選用_ - 選用性的實體類型。如果 `"exact"` 為 `true`，則此欄位為必要欄位。
   -  `"exact": boolean` _選用_ - 如果為 `false`，則執行隱含釐清。隱含釐清將對每一個輸入實體物件使用第一個已釐清實體。預設值為 `false`。
-  `"context": {}` _選用_ - 包括環境定義需求的選用性物件。
   -  `"text": string` _選用_ - 要為查詢實體提供環境定義並根據該關聯進行分級的實體文字。例如，如果您想要查詢英國倫敦這個城市，您的查詢會尋找含有 `England` 環境定義的 `London`。此輸入可以是局部名稱，或是包含相關實體詞彙的大型段落。可以同時傳遞多個詞彙。

-  `"sort": string` _選用_ - 關係的排序方法，可以是 `score` 或 `frequency`。預設值為 `score`。`score` 是基於關係和鄰接項對輸入實體的相關性以及對所提供環境定義的相關性。`frequency` 是唯一識別每一個關係的次數。
-  `"filter": {}` _選用_ - 包含關係類型、實體類型以及要針對此查詢而進行過濾之特定文件的物件。依預設，不會排除任何項目。
   -  `"relation_types": {}` _選用_ 要過濾的關係類型清單。
      -  `"exclude": []` _選用_ 要從查詢中排除的關係類型的逗點區隔清單。
      -  `"include": []` _選用_ 明確在查詢中包含關係類型的逗點區隔清單。如果已指定，則會視為已排除所有其他類型。
   -  `"entity_types": {}` _選用_ 要過濾鄰接項的實體類型清單。不適用於多個實體輸入，因為不會傳回新的鄰接項。
      -  `"exclude": []` _選用_ 要從查詢中排除的實體類型的逗點區隔清單。
      -  `"include": []` _選用_ 明確在查詢中包含實體類型的逗點區隔清單。如果已指定，則會視為已排除所有其他類型。
   -  `"document_ids": []` _選用_ 要執行關係查詢的文件的逗點區隔清單。
-  `"count": INT` _選用_ 要傳回的關係數目。預設值為 `10`。最大值為 `1000`。

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

在關係陣列的每一個物件中，傳回的引數陣列包含一對實體陣列，第一個是來源或主旨，第二個是關係的目標或物件。

如果找不到相符項，則傳回下列 JSON 物件：

```json
{
  "relations": []
}
```
{: codeblock}

## 使用 Discovery 工具查詢知識圖
{: #querying-kg}

其服務實例已訂閱[**進階**](/docs/services/discovery/building-kg.html#service-requirements)方案的那些人，可使用 {{site.data.keyword.discoveryshort}} 工具來查詢具有「知識圖」的專用集合。  

若要在 {{site.data.keyword.discoveryshort}} 工具中存取「知識圖」查詢，請執行下列動作：

1.  按一下 ![「查詢」圖示](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->，以開啟查詢頁面。
1.  選取集合，然後按一下**開始使用**。
1.  在**建置查詢**畫面上，選擇**知識圖**標籤，然後選擇**實體**或**關係**。
