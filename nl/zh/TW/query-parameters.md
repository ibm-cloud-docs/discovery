---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-04"

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

# 查詢參數
{: #query-parameters}

{{site.data.keyword.discoveryfull}} 服務透過查詢提供強大的內容搜尋功能。透過 {{site.data.keyword.discoveryshort}} 服務上傳及強化內容之後，您可以建置查詢，將 {{site.data.keyword.discoveryshort}} 整合至您自己的專案，或使用 {{site.data.keyword.watson}} Explorer Application Builder 來建立自訂應用程式。
若要開始使用查詢，請參閱[查詢概念](/docs/services/discovery/using.html)。如需參數的完整清單，請參閱[查詢參考資料](/docs/services/discovery/query-reference.html#parameter-descriptions)。
{: shortdesc}

**搜尋參數**

搜尋參數可讓您搜尋集合、識別結果集，以及對結果集執行分析。

**結果集**是搜尋參數的結合搜尋所識別的文件群組。結果集的大小可能遠大於傳回的結果。如果執行空查詢，則結果集等於該集合中的所有文件。

## query
{: #query}

查詢搜尋會依相關性順序傳回資料集的所有文件，內含完整強化和全文。查詢也會排除未提及查詢內容的任何文件。這些查詢是使用 [{{site.data.keyword.discoveryshort}} 查詢語言](/docs/services/discovery/query-operators.html)撰寫。

## filter
{: #filter}

可快取的查詢，其排除未提及查詢內容的任何文件。過濾器搜尋結果**不**會依相關性順序傳回。這些查詢是使用 [{{site.data.keyword.discoveryshort}} 查詢語言](/docs/services/discovery/query-operators.html)撰寫

### filter 與 query 參數之間的差異
{: #filtervquery}

如果您在小型資料集上測試相同的搜尋詞彙，您會發現 `filter` 和 `query` 參數會傳回非常類似（即使不完全相同）的結果。不過，這兩個參數之間有差異。

- 單獨使用 filter 參數將不會依特定順序傳回搜尋結果。
- 單獨使用 query 參數將依相關性順序傳回搜尋結果。

在大型資料集中，如果您需要依相關性順序傳回結果，則應該結合 `filter` 和 `query` 參數，因為同時使用它們將增進效能。這是因為 `filter` 參數會先執行並快取結果，然後 `query` 參數會對它們進行分級。如需一起使用過濾器和查詢的範例，請參閱[建置合併查詢](/docs/services/discovery/using.html#building-combined-queries)。過濾器也可以用於聚集中。

當您撰寫的查詢同時包含 `filter` 和 `aggregation`、`query` 或 `natural_language_query` 參數時，`filter` 參數會先執行，之後會以平行方式執行任何 `aggregation`、`query` 或 `natural_language_query` 參數。

利用簡式查詢，尤其是在小型資料集上，`filter` 和 `query` 通常會傳回完全相同（或類似）的結果。如果 `filter` 和 `query` 呼叫傳回類似結果，而且依相關性順序取得回應並不重要，則最好使用過濾器，因為過濾器呼叫速度更快而且會快取。快取表示您下次進行該呼叫時，會得到更快的回應，特別是在海量資料集內。

## aggregation
{: #aggregation}

聚集查詢會傳回符合一組資料值的文件計數；例如，熱門關鍵字、實體的整體觀感等等。如需聚集選項的完整清單，請參閱[聚集表格](/docs/services/discovery/query-aggregations.html)。這些聚集是使用 [{{site.data.keyword.discoveryshort}} 查詢語言](/docs/services/discovery/query-operators.html)撰寫

## natural_language_query
{: #nlq}

自然語言查詢可讓您執行以自然語言表示的查詢，這可能是在交談式介面或任意文字介面中從一般使用者接收到的查詢 - 例如："IBM Watson in Healthcare"。此參數使用整個輸入作為查詢文字。它**不能**辨識運算子。`natural_language_query` 參數可啟用諸如段落搜尋和相關性訓練之類的功能。經過訓練的集合將在自然語言查詢的結果中傳回 `confidence` 評分。如需詳細資料，請參閱[信賴度評分](/docs/services/discovery/train-tooling.html#confidence)。自然語言查詢的查詢字串長度上限為 `2048`。

**結構參數**

結構參數定義所傳回 JSON 中文件的內容及組織。這包括傳回的結果數、要從結果集的什麼位置開始傳回文件、結果集如何排序、要針對每一個文件傳回哪些欄位、是否應該移除重複文件，以及是否應該從結果集擷取相關段落。結構參數不影響哪些文件屬於整個結果集的一部分。

## count
{: #count}

您要在回應中傳回的文件數。預設值為 `10`。任何一個查詢中的 `count` 和 `offset` 值的總和上限為 `10000`。

## offset
{: #offset}

要在開頭跳過的查詢結果數。比方說，如果傳回的結果總數為 10，偏移為 8，則它會傳回最後兩個結果。預設值為 `0`。任何一個查詢中的 `count` 和 `offset` 值的總和上限為 `10000`。

## return
{: #return}

文件階層中所要傳回部分的逗點區隔清單。任何文件階層都是有效值。

## sort
{: #sort}

文件中所要排序欄位的逗點區隔清單。您可以選擇性地指定排序方向，方法是以 `-` 作為欄位字首來代表遞減順序，或以 `+` 作為字首來代表遞增順序。遞增順序是預設排序方向。

`sort` 參數目前只能與 API 搭配使用；無法透過工具來使用。

## bias
{: #bias}

調整搜尋結果以偏向特定結果，例如，最近發佈的文件。`bias` 必須設為 `date` 類型欄位或 `number` 類型欄位，例如 `bias=publication_date` 或 `bias=field_1`。當指定 `date` 類型欄位時，傳回的結果會偏向較接近現行日期的欄位值。當指定 `number` 類型欄位時，傳回的結果會偏向較高的欄位值。這個參數無法用於與 `sort` 參數相同的查詢中。

`bias` 參數目前只能用於 API；它無法透過工具使用。

## passages
{: #passages}

這個布林指定該服務是否從使用 `natural_language_query` 參數的查詢所傳回的文件中，傳回一組最相關的段落。段落是由更準確的 Watson 演算法所產生，用來決定該查詢所傳回之所有文件中的最佳文字段落。預設值為 `false`。

`passages` 參數只能用於專用集合。它無法用於 {{site.data.keyword.discoverynewsfull}} 集合。
{: tip}

{{site.data.keyword.discoveryshort}} 會嘗試傳回使用句子界限偵測在句子開頭開始並在尾端結束的段落。為了這樣做，它會先搜尋大約是 [`passages.characters` 參數](/docs/services/discovery/query-parameters.html#passages_characters)所指定長度（預設值 `400`）的段落。然後，它會展開每一個段落到所指定長度的兩倍限制為止，以傳回完整句子。如果 `passages.characters` 參數很短，且（或）文件中的句子很長，則可能沒有足夠接近的句子界限能夠傳回完整句子而不會超出所要求長度的兩倍。在該情況下，{{site.data.keyword.discoveryshort}} 會維持在 `passages.characters` 參數的兩倍限制內，因此傳回的段落不會包含整個句子，並省略開頭及（或）結尾。

因為句子界限調整會展開段落大小，所以您會看到平均段落長度顯著增加。如果應用程式的螢幕空間有限，您可以為 `passages.characters` 設定較小的值，並（或）截斷 {{site.data.keyword.discoveryshort}} 所傳回的段落。句子界限偵測適用於所有支援的語言，並使用語言特定邏輯。

`passages` 參數會傳回相符的段落 (`passage_text`)，以及 `score`、`document_id`、從中擷取段落的欄位名稱 (`field`)，及段落文字在欄位內的開始字元和結束字元（`start_offset` 和 `end_offset`），如下列範例所示。此查詢會顯示在範例頂端。

```bash
 curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-06-25&natural_language_query='Hybrid%20cloud%20companies'&passages=true"
```
{: pre}

傳回的 JSON 格式如下：

```json
 {
   "matching_results":2,
   "passages":[
     {
       "document_id":"ab7be56bcc9476493516b511169739f0",
       "passage_score":15.230205287402338,
       "passage_text":"a privately held company that provides hybrid cloud recovery, cloud migration and business continuity software for enterprise data centers and cloud infrastructure."
       "start_offset":120
       "end_offset":300
       "field":"text"       
     },
     {
       "passage_text":"Disaster Recovery Services for Hybrid Cloud</title></head>\n<body>\n\n\n<p>Published: Thu, 27 Oct 2016 07:01:21 GMT</p>\n"
       "passage_score":10.153470191601558,
       "document_id":"fbb5dcb4d8a6a29f572ebdeb6fbed20e",              
       "start_offset":70
       "end_offset":120
       "field":"html"
     },
  ...
```
{: codeblock}                        

### passages.fields
{: #passages_fields}

索引中將從其中提取段落之以逗點區隔的欄位清單。如果未指定此參數，則會包含所有最上層欄位。

### passages.count
{: #passages_count}

要傳回的段落數上限。搜尋將傳回所發現的總數（即使它比較少）。預設值為 `10`。最大值是 `100`。

### passages.characters
{: #passages_characters}

任何一個段落應該具有的大約字元數。預設值為 `400`。最小值為 `50`。最大值為 `2000`。傳回的段落可長達所要求長度的兩倍（必要的話），使它們能夠在句子界限上開始及結束。

## highlight
{: #highlight}

指定所傳回的輸出是否包含 `highlight` 物件的布林，該物件中的索引鍵是欄位名稱，其值是陣列，其中包含 HTML `*` 標籤所強調顯示之查詢相符文字的區段。

此輸出在 `enriched_text` 物件之後列出 `highlight` 物件，如下列範例所示。

```bash
curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-06-25&natural_language_query=Hybrid%20cloud%20companies&highlight=true"
```
{: pre}

傳回的 JSON 格式如下：

```json
{
   "highlight": {
     "extracted_metadata.title": [
       "IBM to Acquire Sanovi Technologies to Expand Disaster Recovery Services for <em>Hybrid</em> <em>Cloud</em>"
       ],
     "enriched_text.concepts.text": [
       "Privately held <em>company</em>",
       "<em>Cloud</em> computing"
       ],
     "text": [
       " Sanovi Technologies, a privately held <em>company</em> that provides <em>hybrid</em> <em>cloud</em> recovery, <em>cloud</em> migration",
       "IBM to Acquire Sanovi Technologies to Expand Disaster Recovery Services for <em>Hybrid</em> <em>Cloud</em>\n\nPublished",
       " undergoing digital and <em>hybrid</em> <em>cloud</em> transformation.\n\nURL: http://www.ibm.com/press/us/en/pressrelease/50837.wss",
       " and business continuity software for enterprise data centers and <em>cloud</em> infrastructure. Adding"
       ],
     "enriched_text.categories.label": [
       "/business and industrial/<em>company</em>/bankruptcy"
       ],
     "enriched_text.entities.type": [
       "<em>Company</em>"
       ],
     "html": [
       " Technologies, a privately held <em>company</em> that provides <em>hybrid</em> <em>cloud</em>\n recovery, <em>cloud</em> migration and business",
       " Disaster Recovery Services for <em>Hybrid</em> <em>Cloud</em></title></head>\n<body>\n\n\n<p>Published: Thu, 27 Oct 2016 07:01",
       " digital and <em>hybrid</em> <em>cloud</em> transformation.</p>\n<p>URL: http://www.ibm.com/press/us/en/pressrelease/50837.wss</p>\n\n\n\n</body></html>",
       " continuity software for \nenterprise data centers and <em>cloud</em> infrastructure. Adding these \ncapabilities"
       ]
   }
}
```
{: codeblock}

## deduplicate
{: #deduplicate}

 一種測試版功能，它會根據 `title` 欄位，從 {{site.data.keyword.discoverynewsfull}} 集合查詢結果排除重複文件。請參閱[從查詢結果排除重複文件](/docs/services/discovery/query-parameters.html#deduplication)。

### deduplicate.field
{: #deduplicate_field}

一種測試版功能，它會根據指定的 `{field}`，從查詢結果排除重複文件。請參閱[從查詢結果排除重複文件](/docs/services/discovery/query-parameters.html#deduplication)。

### 從查詢結果排除重複文件
{: #deduplication}

如果您要查詢 {{site.data.keyword.discoverynewsfull}} 集合，或者您的專用資料集合包含多個相同的（或幾乎相同的）文件，則可以使用刪除重複文件功能，從查詢結果排除大部分的文件。

**附註：**刪除重複文件目前僅支援作為測試版功能。如需相關資訊，請參閱「版本注意事項」中的[測試版特性](/docs/services/discovery/release-notes.html#beta-features)。目前僅支援英文版的這個測試版特性，如需詳細資料，請參閱[語言支援](/docs/services/discovery/language-support.html#feature-support)。

**附註：**每一項查詢獨立執行刪除重複，因此，不支援跨偏移執行刪除重複。

刪除重複會在擷取 `passages` 之後執行，並計算聚集，因此，如果您在查詢中包含 `passages` 參數，則在刪除重複之前，會先從查詢結果的所有文件中傳回段落。如果您一起執行聚集和查詢，則在刪除重複之前，聚集結果將包括所有傳回文件的資料。

刪除重複只會對傳回的欄位執行。如果您選擇在查詢中指定 `return=`，請包括您要刪除重複的欄位。

若要套用刪除重複，請在查詢中使用下列語法。請將 `{field}` 取代為您要刪除重複的欄位名稱。指定的 `{field}` 必須是字串，例如 `title`。

```
&deduplicate.field={field}
```
{: codeblock}

刪除重複時，JSON 回應包括 `"duplicates_removed": x`，其中 `x` 是從結果中移除的文件數。

#### 在 Watson Discovery News 中刪除重複文件

新聞文章可能聯合供稿給數個新聞管道，{{site.data.keyword.discoverynewsfull}} 將挑選每一個新聞管道，這會導致文章重複。這表示對 {{site.data.keyword.discoverynewsfull}} 的查詢可能會在查詢結果中傳回數篇相同或幾乎相同的文章。使用刪除重複將從搜尋查詢中移除大部分的重複文章。

{{site.data.keyword.discoveryshort}} 是透過在 `title` 欄位上使用近似比對來刪除重複，因此不需要指定欄位。

若要套用刪除重複，請在查詢中使用下列參數。此查詢會在 {{site.data.keyword.discoverynewsfull}} 的 `title` 欄位上自動刪除重複。

```bash
&deduplicate=true
```
{: codeblock}

如果您希望刪除重複的欄位不是 `title`，請在查詢中使用下列語法。請將 `{field}` 取代為您要刪除重複的欄位名稱。指定的 `{field}` 必須是字串。

```bash
&deduplicate.field={field}
```
{: codeblock}

## collection_ids
{: #collection_ids}

相同環境中將查詢的集合的逗點區隔清單。只有在使用 `environments/{environment_id}/query?` 方法時，這個參數才有效。如需相關資訊，請參閱[查詢多個集合](/docs/services/discovery/using.html#multiple-collections)。

```bash
&collection_ids={id1},{id2}
```
{: codeblock}

## similar
{: #similar}

文件相似性可識別與 `similar.document_ids` 參數中所列出之文件類似的文件。透過使用 `similar.fields` 參數來指定考慮要比較哪些欄位，可進一步修正此功能。預設值為 `false`。如需相關資訊，請參閱[文件相似性](/docs/services/discovery/using.html#doc-similarity)。

```bash
&similar=true
```
{: codeblock}

### similar.document_ids
{: #similar_document_ids}

以逗點區隔的文件 ID 清單，用來作為尋找與結果類似之文件的基礎。如果 `similar` 參數設為 `true`，則需要此參數。

```bash
&similar.document_ids={id1},{id2}
```
{: codeblock}

### similar.fields
{: #similar_fields}

用來比較文件以尋找類似文件的選用性欄位清單（以逗點區隔）。此參數只能與 `similar.document_ids` 參數一起使用。

```bash
&similar.fields={field1},{field2}
```
{: codeblock}
