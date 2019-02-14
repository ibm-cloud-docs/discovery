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

# 조회 매개변수
{: #query-parameters}

{{site.data.keyword.discoveryfull}} 서비스는 조회를 통해 강력한 컨텐츠 검색 기능을 제공합니다. 컨텐츠가 {{site.data.keyword.discoveryshort}} 서비스를 통해 업로드되고 강화된 후 조회를 빌드하거나 {{site.data.keyword.discoveryshort}}를 고유한 프로젝트에 통합하거나 {{site.data.keyword.watson}} Explorer Application Builder를 사용하여 사용자 정의 애플리케이션을 작성할 수 있습니다. 조회로 시작하려면 [조회 개념](/docs/services/discovery/using.html)을 참조하십시오. 매개변수의 전체 목록은 [조회 참조](/docs/services/discovery/query-reference.html#parameter-descriptions)를 참조하십시오.
{: shortdesc}

**검색 매개변수**

검색 매개변수를 통해 콜렉션을 검색하고 결과 세트를 식별하며 결과 세트에 대한 분석을 수행할 수 있습니다.

**결과 세트**는 검색 매개변수의 결합된 검색으로 식별되는 문서의 그룹입니다. 결과 세트는 리턴된 결과보다 훨씬 더 클 수 있습니다. 비어 있는 조회가 수행되면 결과 세트는 콜렉션의 모든 문서와 동일합니다.

## query
{: #query}

조회 검색은 관련성 순서로 전체 인리치먼트 및 전체 텍스트가 포함된 데이터 세트의 모든 문서를 리턴합니다. 또한 조회는 조회 컨텐츠를 언급하지 않은 문서도 제외합니다. 이 조회는 [{{site.data.keyword.discoveryshort}} 조회 언어](/docs/services/discovery/query-operators.html)를 사용하여 작성됩니다.

## filter
{: #filter}

조회 컨텐츠를 언급하지 않은 문서를 제외하는 캐시 가능한 조회입니다. 필터 검색 결과는 관련성 순서로 리턴되지 **않습니다**. 이 조회는 [{{site.data.keyword.discoveryshort}} 조회 언어](/docs/services/discovery/query-operators.html)를 사용하여 작성됩니다.

### 필터 및 조회 매개변수 간의 차이점
{: #filtervquery}

소형 데이터 세트에서 동일한 검색 용어를 테스트하는 경우 `filter` 및 `query` 매개변수가 매우 유사한(동일하지 않은 경우) 결과를 리턴하는 것을 발견할 수 있습니다. 그러나 두 매개변수 간에는 차이점이 있습니다.

- 필터 매개변수 하나만 사용하면 특정하지 않은 순서로 검색 결과를 리턴합니다.
- 조회 매개변수 하나만 사용하면 관련성 순서로 검색 결과를 리턴합니다.

대형 데이터 세트에서 관련성 순서로 리턴된 결과가 필요한 경우 `filter` 및 `query` 매개변수를 함께 사용하면 성능이 향상되므로 결합해야 합니다. 이는 `filter` 매개변수가 먼저 실행되고 결과를 캐시하기 때문에 `query` 매개변수는 결과의 순위를 지정합니다. 필터와 조회를 함께 사용하는 예는 [결합된 조회 빌드](/docs/services/discovery/using.html#building-combined-queries)를 참조하십시오. 또한 필터는 집계에 사용할 수도 있습니다.

`filter` 및 `aggregation`, `query` 또는 `natural_language_query` 매개변수를 포함하는 조회를 작성하는 경우 `aggregation`, `query` 또는 `natural_language_query` 매개변수가 병렬로 실행된 후 `filter` 매개변수가 먼저 실행됩니다.

단순 조회를 사용하면 특히 소형 데이터 세트에서 `filter` 및 `query`가 정확하게 동일한(또는 유사한) 결과를 리턴하기도 합니다. `filter` 및 `query` 호출이 유사한 결과를 리턴하는 경우 관련성 순서로 응답을 가져오는 것은 중요하지 않습니다. 필터 호출이 좀 더 빠르고 캐시되므로 필터를 사용하는 것이 좋습니다. 캐싱은 다음에 해당 호출을 수행할 때 특히 빅데이터 세트에서 좀 더 빠른 응답을 받게됨을 의미합니다.

## aggregation
{: #aggregation}

집계 조회가 데이터 값의 세트(예: 상위 키워드, 엔티티의 전체 감성 등)와 일치하는 문서의 수를 리턴합니다. 집계 옵션의 전체 목록은 [집계 테이블](/docs/services/discovery/query-aggregations.html)을 참조하십시오. 이 집계는 [{{site.data.keyword.discoveryshort}} 조회 언어](/docs/services/discovery/query-operators.html)를 사용하여 작성됩니다.

## natural_language_query
{: #nlq}

대화식 또는 자유 텍스트 인터페이스로 일반 사용자로부터 수신되는 것처럼 자연어 조회를 통해 자연어로 표시되는 조회를 수행할 수 있습니다(예: "IBM Watson in healthcare"). 매개변수는 조회 텍스트로 전체 입력을 사용합니다. 연산자를 인식하지 **않습니다**. `natural_language_query` 매개변수를 통해 단락 검색 및 관련성 훈련과 같은 기능을 제공할 수 있습니다. 훈련된 콜렉션은 자연어 조회의 결과에 `confidence` 스코어를 리턴합니다. 자세한 사항은 [신뢰도 스코어](/docs/services/discovery/train-tooling.html#confidence)를 참조하십시오. 자연어 조회의 최대 조회 문자열 길이는 `2048`입니다.

**구조 매개변수**

구조 매개변수는 리턴된 JSON으로 된 문서의 조직 및 컨텐츠를 정의합니다. 여기에는 리턴되는 결과의 수, 결과 세트에서 리턴되는 문서를 시작하는 위치, 결과 세트 정렬 방법, 각 문서의 리턴할 필드, 중복 문서의 제거 여부 및 결과 세트에서 관련 단락의 추출 여부가 포함됩니다. 구조 매개변수는 전체 결과 세트의 일부인 문서에 영향을 주지 않습니다.

## count
{: #count}

응답에서 리턴할 문서의 수입니다. 기본값은 `10`입니다. 하나의 조회에 `count` 및 `offet`을 함께 사용할 경우 최대값은 `10000`입니다.

## offset
{: #offset}

처음에 건너뛸 조회의 수입니다. 예를 들어, 리턴된 총 결과 수가 10이고 오프셋이 8인 경우 마지막 두 개의 결과를 리턴합니다. 기본값은 `0`입니다. 하나의 조회에 `count` 및 `offet`을 함께 사용할 경우 최대값은 `10000`입니다.

## return
{: #return}

리턴할 문서 계층 구조의 부분에 대한 목록이며, 쉼표로 구분됩니다. 모든 문서 계층 구조가 올바른 값입니다.

## sort
{: #sort}

문서에 있는 정렬할 필드의 목록이며, 쉼표로 구분됩니다. `-`(내림차순) 또는 `+`(오름차순)로 필드에 접두부를 작성하여 정렬 방향을 선택적으로 지정할 수 있습니다. 오름차순이 기본 정렬 방향입니다.

`sort` 매개변수는 현재 API로만 사용할 수 있습니다. 도구를 통해 사용할 수 없습니다.

## bias
{: #bias}

검색 결과를 특정 결과(예: 최근에 게시된 문서)로 편향하도록 조정합니다. `bias`는 `date` 유형 필드 또는 `number` 유형 필드로 설정되어야 합니다(예: `bias=publication_date` 또는 `bias=field_1`). `date` 유형 필드를 지정하는 경우 필드 값이 현재 날짜에 가까운 결과가 리턴됩니다. `number` 유형 필드를 지정하는 경우 필드 값이 더 큰 결과가 리턴됩니다. 이 매개변수는 `sort` 매개변수와 동일한 조회에 사용할 수 없습니다.

`bias` 매개변수는 현재 API로만 사용할 수 있습니다. 도구를 통해 사용할 수 없습니다. 

## passages
{: #passages}

서비스가 `natural_language_query` 매개변수를 사용하는 조회로 리턴되는 문서에서 가장 관련성이 높은 단락의 세트를 리턴하는지 여부를 지정하는 부울입니다. 단락은 조회로 리턴되는 모든 문서에서 최상의 텍스트 단락을 판별하기 위해 정교화된 Watson 알고리즘으로 생성됩니다. 기본값은 `false`입니다.

`passages` 매개변수는 개인용 콜렉션에만 사용할 수 있습니다. {{site.data.keyword.discoverynewsfull}} 콜렉션에는 사용할 수 없습니다.
{: tip}

{{site.data.keyword.discoveryshort}}는 문장을 시작할 때 시작하고 문장 경계 발견을 사용하여 중지하는 단락을 리턴하려고 합니다. 이를 수행하려면 먼저 [`passages.characters` 매개변수](/docs/services/discovery/query-parameters.html#passages_characters)에 지정된 대략적인 단락 길이를 검색합니다(기본값 `400`). 그런 다음 전체 문장을 리턴하기 위해 각 단락을 지정된 길이의 두 배까지 확장합니다. `passages.characters` 매개변수가 짧고/짧거나 문서의 문장이 매우 긴 경우 요청된 길이의 두 배를 넘지 않고 전체 문장을 리턴할 수 있는 정도로 근접한 문장 경계가 없을 수 있습니다. 이 경우 {{site.data.keyword.discoveryshort}}는 `passages.characters` 매개변수의 두 배를 넘지 않으므로 리턴된 단락은 전체 문장을 포함하지 않고 시작 또는 끝(또는 둘 다)을 생략할 수 있습니다.

문장 경계 조정으로 단락 길이가 늘어나므로 평균 단락 길이에서 크게 증가할 수 있습니다. 애플리케이션에 제한된 화면 공간이 있는 경우 사용자는 `passages.characters`에 더 적은 값을 설정하고/설정하거나 {{site.data.keyword.discoveryshort}}로 리턴된 단락을 자르려고 할 수 있습니다. 문장 경계 발견은 모든 지원되는 언어에 적용되고 언어별 로직을 사용합니다.

다음 예제에서 표시된 대로 `passages` 매개변수는 일치하는 단락(`passage_text`, `score`, `document_id`), 단락에서 추출된 필드의 이름(`field`) 및 필드 내 단락 텍스트의 시작 및 종료 문자(`start_offset` 및 `end_offset`)를 리턴합니다. 조회는 예제의 맨 위에 표시됩니다.

```bash
 curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-06-25&natural_language_query='Hybrid%20cloud%20companies'&passages=true"
```
{: pre}

리턴되는 JSON의 형식은 다음과 같습니다.

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

단락이 추출된 인덱스에 있는 필드의 목록이며, 쉼표로 구분됩니다. 매개변수가 지정되지 않으면 모든 최상위 레벨 필드가 포함됩니다.

### passages.count
{: #passages_count}

리턴할 최대 단락의 수입니다. 발견된 총 수인 경우 검색은 더 적은 단락을 리턴합니다. 기본값은 `10`입니다. 최대값은 `100`입니다.

### passages.characters
{: #passages_characters}

하나의 단락에 포함되어야 할 대략적인 문자의 수입니다. 기본값은 `400`입니다. 최소값은 `50`입니다. 최대값은 `2000`입니다. 단락을 시작하고 문장 경계에서 끝내기 위해 단락은 요청된 길이(필요한 경우)의 두 배의 길이가 될 수 있습니다.

## highlight
{: #highlight}

리턴된 출력에 `highlight` 오브젝트가 포함되는지 여부를 지정하는 부울입니다. 이 오브젝트에서 키는 필드 이름이고 값은 HTML `*` 태그로 강조표시되는 조회 일치 텍스트의 세그먼트가 포함된 배열입니다.

다음 예제에서 표시된 대로 출력은 `enriched_text` 오브젝트 뒤에 `highlight` 오브젝트를 나열합니다.

```bash
curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-06-25&natural_language_query=Hybrid%20cloud%20companies&highlight=true"
```
{: pre}

리턴되는 JSON의 형식은 다음과 같습니다.

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

 `title` 필드를 기반으로 한 {{site.data.keyword.discoverynewsfull}} 콜렉션 조회 결과에서 중복 문서를 제외하는 베타 기능입니다. [조회 결과에서 중복 문서 제외](/docs/services/discovery/query-parameters.html#deduplication)를 참조하십시오.

### deduplicate.field
{: #deduplicate_field}

지정된 `{field}`를 기반으로 한 조회 결과에서 중복 문서를 제외하는 베타 기능입니다. [조회 결과에서 중복 문서 제외](/docs/services/discovery/query-parameters.html#deduplication)를 참조하십시오.

### 조회 결과에서 중복 문서 제외
{: #deduplication}

{{site.data.keyword.discoverynewsfull}} 콜렉션을 조회하거나 개인용 데이터 콜렉션에 여러 개의 동일(또는 거의 동일) 문서가 포함되어 있는 경우 문서 중복 제거를 사용하여 조회 결과에서 대부분의 동일 문서를 제외할 수 있습니다.

**참고:** 현재 문서 중복 제거는 베타 기능으로만 지원됩니다. 자세한 정보는 릴리스 정보의 [베타 기능](/docs/services/discovery/release-notes.html#beta-features)을 참조하십시오. 이 베타 기능은 현재 영어로만 지원되며 세부사항은 [언어 지원](/docs/services/discovery/language-support.html#feature-support)을 참조하십시오.

**참고:** 각 조회는 독립적으로 중복 제거되므로 오프셋 전반의 중복 제거는 지원되지 않습니다.

중복 제거는 `passages`가 추출되고 집계가 계산된 후 수행되므로 조회에 `passages` 매개변수를 포함하는 경우 단락은 중복 제거 전에 조회 결과의 모든 문서에서 리턴됩니다. 집계 및 조회를 함께 수행하는 경우 집계 결과는 중복 제거 전에 리턴된 모든 문서의 데이터를 포함합니다.

중복 제거는 리턴된 필드에서만 수행됩니다. 조회에서 `return=`을 지정도록 선택한 경우 중복 제거하는 필드를 포함하십시오.

중복 제거를 적용하려면 조회에 다음 구문을 사용하십시오.  `{field}`를 중복 제거할 필드의 이름으로 대체하십시오. 지정된 `{field}`는 문자열이어야 합니다(예: `title`).

```
&deduplicate.field={field}
```
{: codeblock}

중복 제거 시 JSON 응답에는 `"duplicates_removed": x`가 포함됩니다. 여기서, `x`는 결과에서 제거된 문서의 수입니다.

#### Watson Discovery News의 중복 제거

뉴스 기사는 여러 언론 매체에 신디케이트될 수 있습니다. {{site.data.keyword.discoverynewsfull}}는 기사를 각각 선별하므로 기사가 중복됩니다. 이는 {{site.data.keyword.discoverynewsfull}}에 대한 조회가 잠재적으로 조회 결과에서 동일한 여러 기사 또는 거의 동일한 기사를 리턴할 수 있음을 의미합니다. 중복 제거를 사용하면 검색 조회에서 가장 많이 중복된 기사를 제거합니다.

{{site.data.keyword.discoveryshort}}는 `title` 필드에 대략적인 일치를 사용하여 중복 제거를 수행하므로 필드를 지정할 필요가 없습니다.

중복 제거를 적용하려면 조회에 다음 매개변수를 사용하십시오. 이 조회는 {{site.data.keyword.discoverynewsfull}}의 `title` 필드에서 자동으로 중복 제거를 수행합니다.

```bash
&deduplicate=true
```
{: codeblock}

`title` 이외의 필드에서 중복 제거를 수행하려는 경우 조회에 다음 구문을 사용하십시오. `{field}`를 중복 제거할 필드의 이름으로 대체하십시오. 지정된 `{field}`는 문자열이어야 합니다.

```bash
&deduplicate.field={field}
```
{: codeblock}

## collection_ids
{: #collection_ids}

같은 환경에서 조회할 콜렉션의 목록이며, 쉼표로 구분됩니다. 이 매개변수는 `environments/{environment_id}/query?` 메소드를 사용하는 경우에만 유용합니다. 자세한 정보는 [다중 콜렉션 조회](/docs/services/discovery/using.html#multiple-collections)를 참조하십시오.

```bash
&collection_ids={id1},{id2}
```
{: codeblock}

## similar
{: #similar}

문서 유사성은 `similar.document_ids` 매개변수에 나열된 문서와 유사한 문서를 식별합니다. 이는 `similar.fields` 매개변수를 사용하여 비교할 필드를 지정함으로써 더 세분화할 수 있습니다. 기본값은 `false`입니다. 자세한 정보는 [문서 유사성](/docs/services/discovery/using.html#doc-similarity)을 참조하십시오.

```bash
&similar=true
```
{: codeblock}

### similar.document_ids
{: #similar_document_ids}

결과와 유사한 문서를 찾기 위해 bias로 사용되는 쉼표로 구분된 문서 ID 목록입니다. `similar` 매개변수가 `true`로 설정된 경우 이 매개변수는 필수입니다.

```bash
&similar.document_ids={id1},{id2}
```
{: codeblock}

### similar.fields
{: #similar_fields}

유사한 문서를 찾기 위해 문서를 비교하는 데 사용되는 쉼표로 구분된 필드 목록입니다(선택사항). 이 매개변수는 `similar.document_ids` 매개변수와 함께 사용해야 합니다.

```bash
&similar.fields={field1},{field2}
```
{: codeblock}
