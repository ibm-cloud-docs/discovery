---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-09"

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

# 조회 집계
{: #query-aggregations}

집계에서는 데이터 값 세트를 리턴합니다. 사용 가능한 집계의 전체 목록은 [조회 참조](/docs/services/discovery/query-reference.html#aggregations)를 참조하십시오.

## term
{: #term}

선택한 인리치먼트를 위해 상위 값(스코어별, 빈도별)을 리턴합니다. 모든 인리치먼트는 올바른 값입니다. 선택적으로 `count`를 사용하여 리턴할 용어의 수를 지정할 수 있습니다. 이 예제에서는 개념 인리치먼트를 사용하여 전체 텍스트 및 상위 값의 인리치먼트를 리턴하며 10개의 용어를 지정합니다. 

예:
```bash
term(enriched_text.concepts.text,count:10)
```
{: codeblock}

## filter
{: #filter}

앞서 수행하는 집계 조회의 문서 세트 범위를 좁히는 수정자입니다. 이 예제는 개념 클라우드 컴퓨팅을 포함하는 문서 세트를 필터링합니다. 

예:
```bash
filter(enriched_text.concepts.text:cloud computing)
```
{: codeblock}

## nested
{: #nested}

집계 조회 전에 nested를 적용하면 지정된 결과의 영역으로 집계를 제한합니다. 예를 들어, `nested(enriched_text.entities)`는 결과의 `enriched_text.entities` 컴포넌트만 집계하는 데 사용됨을 의미합니다. 

예:
```bash
nested(enriched_text.entities)
```
{: codeblock}

## histogram
{: #histogram}

문서를 분류하는 숫자 간격 세그먼트를 작성합니다. 카테고리를 설명하기 위해 단일 숫자 필드에서 필드 값을 사용합니다. 히스토그램을 작성하기 위해 사용되는 필드는 숫자(`integer`, `float`, `double` 또는 `date`) 유형이어야 합니다. 숫자가 아닌 유형(예: `string`)은 지원되지 않습니다. 예를 들어, "price": 1.30은 지원되는 숫자 값이며 "price": "1.30"은 문자열이므로 지원되지 않습니다. `interval` 인수를 사용하여 결과가 분할되는 섹션의 크기를 정의하십시오. 간격 값은 숫자가 아닌 전체 값이어야 하고 가능한 필드 값 분할에 적합하도록 설정됩니다. 예를 들어, 데이터 세트에“price”: 1.30, “price”: 1.99 및 “price”: 2.99와 같은 여러 항목의 가격이 포함되는 경우 1 - 2 및 2 - 3 사이의 모든 가격이 표시되도록 1의 간격을 사용할 수 있습니다. 모든 데이터가 같은 세그먼트에서 끝나기 때문에 100의 간격을 사용하지 않습니다. 히스토그램은 10진수 값을 처리할 수 있으나 간격에는 전체 숫자 값이 있어야 합니다. 구문은 다음 예제에 표시된 대로 `histogram(<field>,<interval>)`입니다. 

예:
```bash
histogram(product.price,interval:1)
```
{: codeblock}

## timeslice
{: #timeslice}

간격 세그먼트를 작성하기 위해 날짜를 사용하는 특수 히스토그램입니다. 올바른 날짜 간격 값은 `second/seconds` `minute/minutes`, `hour/hours`, `day/days`, `week/weeks`, `month/months` 및 `year/years`입니다. 구문은 `timeslice(<field>,<interval>,<time_zone>)`입니다. `timeslice`를 사용하려면 문서의 시간 필드는 `date` 데이터 유형이고 [UNIX 시간 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://en.wikipedia.org/wiki/Unix_time){: new_window} 형식이어야 합니다. 이 두 가지 요구사항이 충족되지 않으면 `timeslice` 매개변수가 올바르게 적용되지 않습니다. 문서에 `1496228512`와 같은 값이 포함된 `date` 필드가 포함되면 시분할을 작성할 수 있습니다. 값은 숫자 형식(예: `float` 또는 `double`)이어야 하며 따옴표로 묶지 않아야 합니다. 서비스는 텍스트로 된 날짜와 ISO 8601 형식으로 된 날짜를 `date` 유형이 아닌 `string` 데이터 유형으로 처리합니다. 시분할 집계의 비정상적인 지점을 발견할 수 있습니다. 추가 정보는 [시분할 이상 항목 발견](#anomaly-detection)을 참조하십시오. 이 예제에서는 뉴욕 도시 시간대에서 2일 간격으로 "sales ("prod이 uct.sales")의 값을 리턴합니다. 

예:
```bash
timeslice(product.sales,2day,America/New York)
```
{: codeblock}

### 시분할 이상 항목 발견
{: #anomaly-detection}

선택적으로 `timeslice` 집계의 결과에 이상 항목 발견을 적용할 수 있습니다. 이상 항목 발견은 시계열 내의 비정상 데이터 지점을 찾고 이후 검토를 위해 비정상 데이터 지점의 플래그를 지정하는 데 사용됩니다. 이상 항목 발견 사용 예제에는 신용카드 사용 급증의 식별 및 특정 주제에 대한 기사의 클러스터용 Watson Discovery News 검색이 포함됩니다. 

이상 항목 발견을 적용하려면 집계에 다음 구문을 사용하십시오. 

```bash
timeslice(field:<date>,interval:<interval>,anomaly:true)`
```
{: codeblock}

`timeslice` 집계를 사용하여 `anomaly:true`를 지정한 경우 출력에는 예제에 표시된 다음 두 개의 추가 필드가 포함됩니다. 

  - `"anomaly": true` - 이상 항목 발견이 수행되었음을 식별합니다. 
  - `anomaly` - 출력의 결과 배열에서 비정상적인 지점에 있습니다. 이상 항목 필드에는 비정상적인 작동의 정도를 나타내는 `float` 데이터 유형의 값이 있습니다. 이상 항목 필드의 값이 `1`에 가까울수록 결과가 비정상적일 가능성이 큽니다. 

  - `results` 배열의 각 오브젝트에서 `key` 및 `key_as_string`은 UNIX 시간소인(초)에 해당합니다. 
  - 이상 항목 스코어가 조회 전반이 아닌 단일 조회에 관련됩니다. 

```json
"type": "timeslice",
"field": "blekko.chrondate",
"interval": "1d",
"anomaly": true,
"results": [
  {
    "matching_results": 2933,
    "anomaly": 1,
    "key_as_string": "1496880000",
    "key": 1496880000000
  },
  {
    "matching_results": 3435,
    "anomaly": 1,
    "key_as_string": "1496966400",
    "key": 1496966400000
  },
  {
    "matching_results": 3692,
    "anomaly": 0.598226,
    "key_as_string": "1496016000",
    "key": 1496016000000
  },
  {
    "matching_results": 4551,
    "anomaly": 0.828498,
    "key_as_string": "1495411200",
    "key": 1495411200000
  },
  {
    "matching_results": 947,
    "key_as_string": "1489968000",
    "key": 1489968000000
  },
 ...
]
...
```
{: codeblock}

#### 이상 항목 발견의 제한사항

- 이상 항목 발견은 현재 최상위 레벨 `timeslice` 집계에서만 사용 가능합니다. 하위 레벨(중첩됨) 집계에 사용할 수 없습니다. 
- 제공된 `timeslice` 집계에서 이상 항목 발견으로 처리할 수 있는 최대 지점 수는 `1500`입니다.
- 이상 항목 발견으로 처리할 수 있는 최상위 레벨 시분할은 `20`입니다.

<!--
#### Anomaly detection workflow

The following example workflow detects an anomaly for the text entity `London` and retrieves additional information about the anomalous datapoint.

  1. Timeslice aggregation: `query=entities.text:London&count=0&aggregation=timeslice(blekko.last_crawled,1day,anomaly:true)`
  1. Term aggregation to retrieve top keywords: `query=entities.text:London&count=0&aggregation=term(keywords.text,count:5)&filter=blekko.last_crawled>=1490140800,<=1490227200`
  1. Query to retrieve top enriched title: `query=entities.text:London,keywords.text:Westminster Bridge|police officer|people|Prime Minister Theresa|parliament&count=1&filter=blekko.last_crawled>=1490140800,<=1490227200&return=enrichedTitle.text`
  -->

## top_hits
{: #top_hits}

조회 또는 인리치먼트의 스코어에 의해 순위가 지정된 문서를 리턴합니다. 조회 매개변수 또는 집계에서 사용될 수 있습니다. 이 예제는 용어 집계에 대해 10개의 상위 힌트를 리턴합니다. 

예:
```bash
term(enriched_text.concepts.text).top_hits(10)
```
{: codeblock}

## unique_count
{: #unique_count}

콜렉션에서 지정된 필드의 고유 인스턴스 수를 리턴합니다. 

예:
```bash
unique_count(enriched_text.keyword.text)
```
{: codeblock}

```bash
nested(enriched_text.entities).term(enriched_text.entities.text,count:3).unique_count(enriched_text.entities.type)
```
{: codeblock}

## max
{: #max}

일치하는 모든 문서 전반에 지정된 필드의 최대값을 리턴합니다. 

예:
```bash
max(product.price)
```
{: codeblock}

## min
{: #min}

일치하는 모든 문서 전반에 지정된 필드의 최소값을 리턴합니다. 

예:
```bash
min(product.price)
```
{: codeblock}

## average
{: #average}

일치하는 모든 문서 전반에 지정된 필드의 평균값을 리턴합니다. 

예:
```bash
average(product.price)
```
{: codeblock}

## sum
{: #sum}

일치하는 모든 문서 전반에 지정된 필드의 값을 합산합니다. 

예:
```bash
sum(product.price)
```
{: codeblock}
