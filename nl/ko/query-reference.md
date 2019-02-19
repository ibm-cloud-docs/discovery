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

# 조회 참조

{{site.data.keyword.discoveryfull}} 서비스는 조회를 통해 강력한 컨텐츠 검색 기능을 제공합니다. 컨텐츠가 {{site.data.keyword.discoveryshort}} 서비스를 통해 업로드되고 강화된 후 조회를 빌드하거나 {{site.data.keyword.discoveryshort}}를 고유한 프로젝트에 통합하거나 {{site.data.keyword.watson}} Explorer Application Builder를 사용하여 사용자 정의 애플리케이션을 작성할 수 있습니다.
{: shortdesc}

조회 작성에 대한 자세한 정보는 다음을 참조하십시오.
- [조회 시작하기](/docs/services/discovery/getting-started-query.html)
- [조회 개념](/docs/services/discovery/using.html)

## 매개변수 설명
{: #parameter-descriptions}

조회 매개변수를 통해 콜렉션을 검색하고 결과 세트를 식별하며 결과 세트에 대한 분석을 수행할 수 있습니다.


|매개변수 |설명 |예 |
|:-------------------:|------------------------------------------------------------|--------------------------------|
|**검색 매개변수**|  |  |
|[query](/docs/services/discovery/query-parameters.html#query) |일치하는 문서에 대한 순위가 지정된 조회 언어 검색입니다. |`query=bees` |
|[filter](/docs/services/discovery/query-parameters.html#filter) |일치하는 문서에 대한 순위가 지정되지 않은 조회 언어 검색입니다. |`filter=bees` |
|[natural_language_query](/docs/services/discovery/query-parameters.html#nlq) |일치하는 문서에 대한 순위가 지정된 자연어 검색입니다. |`natural_language_query="How do bees fly"` |
|[aggregation](/docs/services/discovery/query-parameters.html#aggregation) |결과 세트의 통계 조회입니다. |`aggregation=term(enriched_text.entities.type)` |
|**구조 매개변수** | | |
|[count](/docs/services/discovery/query-parameters.html#count) |리턴할 `result` 문서의 수입니다. |`count=15` |
|[offset](/docs/services/discovery/query-parameters.html#offset) |결과 세트에서 `result` 문서를 리턴하기 전에 무시할 결과의 수입니다. |`offset=100` |
|[return](/docs/services/discovery/query-parameters.html#return) |리턴할 필드의 목록입니다. |`return=title,url` |
|[sort](/docs/services/discovery/query-parameters.html#sort) |결과 세트를 정렬할 필드입니다. |`sort=enriched_text.sentiment.document.score` |
| [bias](/docs/services/discovery/query-parameters.html#bias) | 결과 세트에 대한 편향을 지정하는 필드입니다. | `bias=publication_date` |
|[passages.fields](/docs/services/discovery/query-parameters.html#passages_fields) |단락을 추출할 필드입니다. |`passages=true&passages.fields=text,abstract,conclusion` |
|[passages.count](/docs/services/discovery/query-parameters.html#passages_count) |리턴할 단락의 수입니다. | `passages=true&passages.count=6` |
|[passages.characters](/docs/services/discovery/query-parameters.html#passages_characters) |단락의 길이입니다. | `passages=true&passages.characters=144` |
|[highlight](/docs/services/discovery/query-parameters.html#highlight) |조회 일치 항목을 강조표시합니다. |`highlight=true` |
|[deduplicate](/docs/services/discovery/query-parameters.html#deduplicate) |{{site.data.keyword.discoverynewsfull}} 리턴된 결과에서 중복을 제거합니다. |`deduplicate=true` |
| [deduplicate.field](/docs/services/discovery/query-parameters.html#deduplicate_field) |필드에 기반하여 리턴된 결과에서 중복을 제거합니다. |`deduplicate.field=title` |
|[collection_ids](/docs/services/discovery/query-parameters.html#collection_ids) |다중 콜렉션을 조회합니다. |`collection_ids={1},{2},{3}` |
| [similar](/docs/services/discovery/query-parameters.html#similar) | 유사한 문서 찾기를 사용합니다. | `similar=true` |
| [similar.document_ids](/docs/services/discovery/query-parameters.html#similar_document_ids) | 유사한 문서를 찾을 수 있는 문서입니다. | `similar.document_ids={id1},{id2}` |
| [similar.fields](/docs/services/discovery/query-parameters.html#similar_fields) | 유사한 문서를 찾을 때 비교할 필드입니다. | `similar.fields=text,title` |

### 조회 제한사항

다음과 같은 필드 이름은 조회할 수 없습니다.
- 필드 이름의 접미부에 숫자(`0 - 9`)가 포함된 경우(예: `extracted-content2`).
- `field_name`의 접두부에 문자 `_`, `+` 및 `-`이 포함된 경우(예: `+extracted-content`).
- `field_name`에 문자 `.`, `,` 및 `:`이 포함된 경우(예: `new:extracted-content`)

## 연산자
{: #operators}

연산자는 조회의 서로 다른 부분 사이에 있는 구분 기호입니다. 사용 가능한 연산자는 다음과 같습니다.

|연산자 |설명 |예 |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [.](/docs/services/discovery/query-operators.html#delimiter) |JSON 구분 기호 |`enriched_text.concepts.text` |
| [:](/docs/services/discovery/query-operators.html#includes) |포함 |`text:computer` |
| [::](/docs/services/discovery/query-operators.html#match) |정확히 일치 | `title::"Query building"` |
| [:!](/docs/services/discovery/query-operators.html#notinclude) |포함하지 않음 |`text:!computer` |
| [::!](/docs/services/discovery/query-operators.html#notamatch) |정확히 일치하지 않음 | `text::!winter` |
| [\\](/docs/services/discovery/query-operators.html#escape) |이스케이프 문자 | `title::"Dorothy said: \"There's no place like home\""` |
| [""](/docs/services/discovery/query-operators.html#phrase) |구문 조회 |`enriched_text.concepts.text:"IBM Watson"` |
| [(), \[\]](/docs/services/discovery/query-operators.html#nestedquery) |중첩된 그룹화 |`filter-entities:(text:Turkey,type:Location)` |
|[<code>&#124;</code>](/docs/services/discovery/query-operators.html#or) |or |<code>query-enriched.entities.text:Google&#124;IBM</code> |
| [,](/docs/services/discovery/query-operators.html#and) |and |`query-enriched.entities.text:Google,IBM` |
| [<=, >=, >, <](/docs/services/discovery/query-operators.html#comparisons) |숫자 비교 |`enriched_text.sentiment.document.score>0.679`     |
| [^x](/docs/services/discovery/query-operators.html#multiplier) |스코어 승수 |`text:IBM^3` |
| [*](/docs/services/discovery/query-operators.html#wildcard) |와일드카드 |`query-enriched_text.concepts.text:pre*` |
|[~n](/docs/services/discovery/query-operators.html#variation) |문자열 변형 |`query-enriched_text.entities.text:cat~1` |
| [:*](/docs/services/discovery/query-operators.html#exists) | 있음 | `title:*` |
| [!*](/docs/services/discovery/query-operators.html#dnexist) | 없음 | `title!*` |

## 집계
{: #aggregations}

집계에서는 데이터 값 세트를 리턴합니다. 사용 가능한 집계는 다음과 같습니다.

|집계 |설명 |예 |
|:-------------------:|------------------------------------------------------------|--------------------------------|
|[term](/docs/services/discovery/query-aggregations.html#term) |동일한 값의 수입니다. |`term(enriched_text.concepts.text,count:10)` |
|[filter](/docs/services/discovery/query-aggregations.html#filter) |정의된 패턴으로 설정된 필터 결과입니다. |`filter(enriched_text.concepts.text:cloud computing)`
|[nested](/docs/services/discovery/query-aggregations.html#nested) |제한사항 집계입니다. |`nested(enriched_text.entities)` |
|[histogram](/docs/services/discovery/query-aggregations.html#histogram) |간격 기반 분배입니다. |`histogram(product.price,interval:1)` |
|[timeslice](/docs/services/discovery/query-aggregations.html#timeslice) |시간 기반 분배입니다. |`timeslice(last_modified,2day,America/New York)` |
|[top_hits](/docs/services/discovery/query-aggregations.html#top_hits) |현재 집계에 대해 상위로 순위가 지정된 결과 문서입니다. |`term(enriched_text.concepts.text).top_hits(10)` |
|[unique_count](/docs/services/discovery/query-aggregations.html#unique_count) |집계 내 필드의 고유 값 수입니다. |`unique_count(enriched_text.entities.type)` |
| [max](/docs/services/discovery/query-aggregations.html#max) |결과 세트에서 지정된 필드의 최대값입니다. |`max(product.price)` |
| [min](/docs/services/discovery/query-aggregations.html#min) |결과 세트에서 지정된 필드의 최소값입니다. |`min(product.price)` |
|[average](/docs/services/discovery/query-aggregations.html#average) |결과 세트에서 지정된 필드의 평균값입니다. |`average(product.price)` |
|[sum](/docs/services/discovery/query-aggregations.html#sum) |결과 세트에 있는 전체 필드의 총계입니다. |`sum(product.price)` |
