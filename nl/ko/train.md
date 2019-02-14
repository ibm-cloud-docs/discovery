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

# API로 결과 관련성 향상

{{site.data.keyword.discoveryshort}} 서비스를 훈련하여 특정 조직 또는 주제 영역에 대한 조회 결과의 관련성을 향상시킬 수 있습니다. *훈련 데이터*와 함께 {{site.data.keyword.discoveryshort}} 인스턴스를 제공하는 경우 서비스는 기계 학습 Watson 기술을 사용하여 컨텐츠 및 질문의 신호를 찾습니다. 그런 다음 서비스는 조회 결과를 다시 정렬하여 맨 위에 가장 관련성이 높은 결과를 표시합니다. 더 많은 훈련 데이터를 추가할수록 리턴하는 결과의 순위 지정 시 서비스 인스턴스가 좀 더 정확해지고 정교해집니다.
{: shortdesc}

관련성 훈련은 선택적입니다. 조회의 결과가 사용자의 요구사항을 충족하는 경우 추가 훈련이 필요하지 않습니다. 훈련에 대한 유스 케이스 빌드의 개요는 블로그 포스트 [How to get the most out of Relevancy Training ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window}을 참조하십시오.

훈련 API에 대한 포괄적인 정보는 [API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}를 참조하십시오.

{{site.data.keyword.discoveryshort}}를 훈련하는 데 {{site.data.keyword.discoveryshort}} 도구를 사용하려는 경우 [도구로 결과 관련성 향상](/docs/services/discovery/train-tooling.html)을 참조하십시오.

**참고:** 관련성 훈련은 현재 개인용 콜렉션의 자연어 조회에만 적용됩니다. 구조화된 {{site.data.keyword.discoveryshort}} 조회 언어 조회와 함께 사용할 수 없습니다.  {{site.data.keyword.discoveryshort}} 조회 언어에 대해 좀 더 알아보려면 [조회 개념](/docs/services/discovery/using.html)을 참조하십시오.

훈련된 콜렉션은 자연어 조회의 결과에 `confidence` 스코어를 리턴합니다. 자세한 사항은 [신뢰도 스코어](/docs/services/discovery/train-tooling.html#confidence)를 참조하십시오.

훈련 한계 및 훈련에 대한 최소 요구사항은 [훈련 데이터 요구사항](/docs/services/discovery/train.html#reqs)을 참조하십시오.

애플리케이션을 이해하고 향상시키기 위해 이 데이터를 사용하고 사용을 추적하는 데 대한 자세한 정보는 [사용 모니터링](/docs/services/discovery/feedback.html)을 참조하십시오.

<!-- A trained Discovery service instance is intended primarily for use with natural language queries, but it works equally well with queries that use structured syntax. -->  <!-- See [Query Concepts](/docs/services/discovery/using.html) and the [Query reference](/docs/services/discovery/query-reference.html) for information about structured queries and natural language queries. -->

Discovery 인스턴스를 훈련하는 데 필요한 컴포넌트에는 다음이 포함됩니다.

 - **훈련 데이터**. 서비스가 조회 결과를 세분화하는 데 사용하는 *조회* 및 *예제*의 세트입니다.
 - **조회**. 훈련 데이터 세트에 적용되는 자연어 조회입니다.
   각 조회에는 다음 글머리 기호에 설명된 대로 하나 이상의 연관된 *예제*가 있습니다.
   각 조회는 훈련 데이터 세트 내에서 고유해야 합니다.
 - **예제**. 이는 연관된 조회에 대해 실례(**올바르거나 잘못됨**)의 역할을 하는 콜렉션에서 인덱싱된 문서입니다. 예제를 훈련 데이터 조회에 추가할 때 지정된 조회에 적용할 수 있는 문서의 관련성(또는 "올바름" 대 "잘못됨")을 표시하는 관련성 레이블을 포함합니다.

   예제는 인덱싱된 문서 ID로 식별됩니다. 언급한 바와 같이, 모든 예제는 조회와 연관될 수 있는 문서의 "올바름" 또는 "잘못됨"을 표시하는 레이블이 포함되어야 합니다.

   예제는 선택적으로 교차 참조 조회를 지정할 수 있습니다. 교차 참조 조회는 예제 문서만 리턴해야 하고 고유한 Watson Discovery 문서 ID와 관계가 없어야 합니다. 교차 참조 조회는 현재 자동으로 사용되지 않지만 수집 이벤트 중에 새 ID가 문서에 지정되는 경우 훈련 데이터를 수리하는 데 사용될 수 있습니다.

## 훈련 데이터 요구사항
{: #reqs}

훈련 데이터는 Discovery 서비스로 리턴되는 답변의 관련성을 효과적으로 향상시키려면 다음 **최소** 품질 기준을 충족해야 합니다. **최소**는 **최적**을 의미하지 않습니다. 서비스는 요구사항이 충족되는지와 모든 변경사항에 따라 자체적으로 자동 업데이트가 수행되는지 여부를 판별하기 위해 주기적으로 훈련 데이터를 확인합니다.

- 콜렉션의 훈련 데이터 세트에는 최소 49개의 고유한 훈련 조회(즉, 조회 및 예제의 세트)가 포함되어야 합니다. Watson이 콜렉션에 관련성 훈련을 적용하기 전에 콜렉션의 크기 및 복잡도에 따라 사용자 세트의 훈련 조회 수는 49보다 커야 할 수 있습니다. Watson은 훈련을 위해 추가 조회가 필요한 경우 사용자에게 피드백을 제공합니다. 
- API를 통해 관련성 스코어를 지정하는 경우: 각 훈련 조회의 관련성 스코어는 음수가 아닌 정수여야 합니다. 예를 들어, `0`은 *관련성 없음*을 나타내고 `1`은 *낮은 관련성*을 나타내며 `2`는 *높은 관련성*을 나타냅니다. 그러나 유연성을 극대화하기 위해 서비스는 고급 사용자가 다른 스코어링 스키마로 실험할 수 있도록 `0` - `100` 범위의 음수가 아닌 정수를 허용합니다. 사용하는 범위에 관계 없이 훈련 세트의 가장 큰 정수는 최대 관련성을 표시합니다.
- 도구를 통해 관련성 등급을 지정하는 경우: {{site.data.keyword.discoveryshort}} 도구는 `0`의 관련성 스코어를 사용하여 *관련성 없음*을 나타내고 `10`을 사용하여 *관련성*을 나타냅니다. `Relevant` 및 `Not relevant` 등급을 결과에 적용해야 합니다. `Relevant` 문서만 등급을 지정하면 필요한 데이터를 제공하지 않습니다.  {{site.data.keyword.discoveryshort}} 도구 및 API를 모두 사용하여 문서를 스코어링할 계획이거나 API로 시작하여 도구로 이동할 계획인 경우 `0` - `10` 관련성 스코어를 사용하십시오.
- 훈련 조회는 범위가 넓은 Discovery 서비스의 초기 검색으로 찾을 수 있도록 조회 및 원하는 답변 사이에 일부 용어 겹침을 포함해야 합니다.

**참고:** Watson은 훈련 데이터를 사용하여 개별 훈련 조회를 기억하는 것이 아닌 패턴을 학습하고 일반화합니다. 그러므로 서비스는 항상 제공된 훈련 조회에 대한 동일한 관련성 결과를 재생하지 않을 수 있습니다.

훈련은 다음 **최대** 요구사항을 초과할 수 없습니다.
  - 환경당 24개의 훈련된 콜렉션을 초과할 수 없습니다.
  - 단일 환경 내에서는 조회당 최대 100개의 예와 함께 10,000개의 훈련 조회로 제한됩니다. 

## 조회를 훈련 데이터 세트에 추가

`POST /v1/environments/{environment_id}/collections/{collection_id}/training_data` 메소드를 사용하여 조회를 훈련 데이터의 콜렉션 세트에 추가하십시오. 조회는 다음과 같은 형식을 사용하여 JSON 오브젝트로 지정됩니다.

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

이 오브젝트의 값은 다음과 같습니다.

- `query_id`: 조회의 고유 ID입니다. 이 필드를 지정하지 않으면 서비스가 자동으로 ID를 생성합니다.
- `natural_language_query`: 훈련 세트에 적용되는 Discovery 자연어 조회입니다. <!-- The `natural_language_query` parameter is preferred. -->
- `filter`: [조회 참조](/docs/services/discovery/query-reference.html#parameter-descriptions)에 설명된 대로 조회에 대한 선택적 필터입니다.

    **참고:** 훈련 데이터 조회에 필터를 포함한 경우 훈련된 콜렉션의 자연어 조회를 사용해야 합니다. 콜렉션을 조회할 때 필터링된 데이터를 사용하여 콜렉션을 훈련시키지만 같은 필터 유형을 사용하지 않는 경우 결과가 예측 불가능할 수 있습니다.

- `examples`: 배열에는 다음 값이 포함됩니다.

   - `document_id`: 훈련 세트에 적용되는 문서의 고유 ID입니다. 이전에 설명된 *예제*입니다.
   - `cross_reference`: 선택적 레이블로, 일반적으로 문서의 ID가 변경되는 경우(예를 들어, 새로 수집된 문서에 동일한 ID가 지정된 경우) 문서 및 필드의 정보를 "고정"하는 참조된 문서의 필드로 구성됩니다. `cross-reference`의 값을 지정하면 하나의 문서에서 다른 문서로 연결되지 **않습니다**. 문서의 이름이 변경되거나 문서가 대체되는 경우 서비스가 문서의 관련 정보를 보유하고 있는지 확인하십시오.
   - `relevance`: `0` - `100` 범위의 정수로, 훈련 데이터에 대한 조회의 상대적 관련성을 표시합니다. 값이 클수록 높은 관련성을 나타냅니다. `0` 값은 조회에 대한 관련성이 없음을 표시하지만 `100` 값은 조회에 대한 관련성이 절대적임을 표시합니다.

   **참고:** 유연성을 극대화하기 위한 `relevance` 매개변수의 범위가 `0` - `100`이지만 더 작은 범위를 사용하여 스코어링 예제를 간소화할 수 있습니다. 표준 범위는 `0` - `4`입니다. 전체 범위를 사용할 수 있으나 20을 기준으로만 증가합니다(`0`,`20`,`40`,`60`,`80` 및 `100`). {{site.data.keyword.discoveryshort}} 도구는 `0`의 관련성 스코어를 사용하여 *관련성 없음*을 나타내고 `10`을 사용하여 *관련성*을 나타냅니다. {{site.data.keyword.discoveryshort}} 도구 및 API를 모두 사용하여 문서를 스코어링할 계획이거나 API로 시작하여 도구로 이동할 계획인 경우 `0` - `10` 관련성 스코어를 사용하십시오.

다음 오브젝트는 채워진 훈련 데이터 조회를 표시합니다.

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

다음 명령 예제는 이전 훈련 데이터 조회를 `a56dd9b4-040b-4ea3-a736-c1e7a467e191` 환경의 `99040100-fe6a-4782-a4f5-28f9eee30850` 콜렉션에 추가합니다.

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

## 예제를 훈련 데이터 조회에 추가

훈련 데이터 조회를 작성하는 경우 훈련의 정확성을 향상시키기 위해 예제를 훈련 데이터 조회에 계속 추가할 수 있습니다. 예제를 기존 훈련 데이터 조회에 추가하려면 `POST /v1/environments/{environment_id}/collections/{collection_id}/training_data/{query_id}`를 사용하십시오.

예제를 훈련 데이터 조회에 추가하려면 다음 단계를 수행하십시오.

1. [콜렉션의 훈련 데이터 조회 나열 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#get-training-data){: new_window}로 새 예제를 추가하려는 훈련 데이터 조회의 조회 ID를 가져오십시오.

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
   ```
   {: pre}

   리턴되는 JSON의 형식은 다음과 같습니다.

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

1. 새 훈련 데이터 조회를 작성할 때 예제를 정의하기 위해 사용하는 동일한 구문을 사용하여 새 예제를 추가하십시오. 다음 명령 예제에는 교차 참조가 포함되지 않습니다.

   ```bash
    curl -u -X POST -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" -H "Content-Type: application/json" -d
    '{
      "document_id": "46b52fdc-3a72-4700-9849-ac217532b373",
      "relevance": 3
    }' "https://gateway.watsonplatform.net/discovery/api/v1/environments//a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data/484baad4-d440-44b7-a0dd-70bb2ac77baa?version=2016-12-01"
   ```
   {: pre}

1. [콜렉션의 훈련 데이터 조회 나열 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#get-training-data){: new_window}을 다시 수행하여 새 예제가 훈련 데이터 조회에 추가되었는지 확인하십시오.

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
   ```
   {: pre}

   리턴되는 JSON의 형식은 다음과 같습니다.

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

1. [콜렉션 세부사항 나열 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#list-collection-details){: new_window} 메소드를 사용하고 `"training"`/`"available"` 필드의 값을 살펴본 후 훈련의 상태를 확인하십시오. 충분한 조회 및 예제를 추가하여 훈련 요구사항을 충족하는 경우 필드의 값은 `true`로 리턴하고 서비스는 자동으로 훈련 데이터 사용을 시작합니다.

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850?version=2016-12-01"
   ```
   {: pre}

   리턴되는 JSON의 형식은 다음과 같습니다.

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

1. 이전 단계의 다음 필드에서 `true`를 모두 리턴하는 경우 서비스가 좀 더 관련성 있는 결과를 리턴하는지 확인하기 위해 일부 샘플 조회를 실행하십시오.

   - `minimum_queries_added`
   - `minimum_examples_added`
   - `sufficient_label_diversity`

   결과의 관련성이 향상되지 않은 경우 결과가 요구사항을 충족할 때까지 더 많은 훈련 조회를 추가하십시오.

추가적인 훈련 지시사항은 [관련성 훈련 팁](/docs/services/discovery/train-tips.html#relevancy-tips)을 참조하십시오.   

## 기타 훈련 데이터 조회 오퍼레이션 수행
{: #training-data-operations}

[API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}에 설명된 대로 기타 API 메소드를 사용하여 훈련 데이터 조회를 관리하고 유지보수할 수 있습니다.

 - [콜렉션의 훈련 데이터 나열 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#get-training-data){: new_window}
 - [콜렉션의 모든 훈련 데이터 삭제 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-all-training-data){: new_window}
 - [지정된 훈련 데이터 조회의 컨텐츠 표시 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#show-td-query){: new_window}
 - [콜렉션에서 훈련 데이터 조회 삭제 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/watson/developercloud/discovery/api/v1#delete-td-query-example){: new_window}
 - [훈련 데이터 조회 예제의 관련성 레이블 또는 교차 참조 변경 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#update-example){: new_window}
 - [훈련 데이터 조회에서 예제 문서 삭제 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-example){: new_window}

 **오류 모니터링:** 훈련 데이터 오류는 알림에 표시되며
 [알림 조회 API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-notices){: new_window}(`GET /v1/environments/{environment_id}/collections/{collection_id}/notices`)를 사용하여 모니터링할 수 있습니다.
