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

# 관련성 훈련 팁
{: #relevancy-tips}

 콜렉션 훈련에 대한 일반적인 질문에 대한 답변과 일반적인 오류 및 경고 메시지에 대한 설명입니다. 자연어 조회 향상에 대한 자세한 정보는 [도구로 결과 관련성 향상](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling) 및 [API로 결과 관련성 향상](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api)을 참조하십시오.
{: shortdesc}

## 훈련 이해
{: #understanding-training}

콜렉션 훈련에 대한 일반적인 질문에 대한 답변입니다.

### 내 시스템이 훈련되었는지를 알 수 있는 방법
{: #understanding-system}

[콜렉션 세부사항 나열 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/discovery#get-collection-details){: new_window} API 명령을 사용하여 시스템이 훈련되었는지 확인하십시오.  

```bash
curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07"
```
{: pre}

응답 예제:

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

훈련에 대한 요구사항을 충족하려면 다음 항목이 모두 `true`여야 합니다.
- `minimum_queries_added`
- `minimum_examples_added`
- `sufficient_label_diversity`   

응답에서:
- `successfully_trained`는 훈련이 완료된 마지막 시간입니다.
- `available: true`는 훈련이 발생했으며 모델이 사용 가능함을 표시합니다.
- `processing: true`는 훈련이 진행 중임을 표시합니다.
-  `data_updated` 날짜가 `successfully_trained` 날짜 이후인 경우 새 모델은 최신 데이터 업로드 이후에 훈련됩니다.  

### 오류 및 경과 확인 방법
{: #understanding-errors}

[알림 조회 API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/discovery#query-system-notices){: new_window}를 사용하여 오류 또는 경고를 볼 수 있습니다.  

```bash
curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/notices?version=2017-11-07"
```
{: pre}

기타 API 연산자는 [기타 훈련 데이터 조회 오퍼레이션 수행](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#training-data-operations)에 나열되어 있습니다.

### 훈련 후 자연어 조회 결과에 표시되는 `confidence` 스코어를 해석하는 방법
{: #interpret-confidence}

자세한 정보는 [신뢰도 스코어](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence)를 참조하십시오.  

## 오류 및 경고 해석
{: #interpreting-errors}

일반적인 오류 및 경고 메시지에 대한 설명입니다.

### 경고: `Invalid training data found: The document was not returned in the top 100 search results for the given query, and will not be used for training`
{: #warning-docnotreturned}

경고는 콜렉션에 대해 수행된 검색의 `document_ids`와 일치하지 않는 훈련 데이터의 `document_ids`로 인해 발생합니다. 조회를 확인하고 순위를 지정하는 문서의 `document_id`가 해당 조회에 대한 상위 100개의 결과에 리턴되는지 확인해야 합니다. 그렇지 않은 경우 다음 두 가지를 확인하려고 할 수 있습니다.  

- 문서가 상위 100개에 리턴되지 않은 경우 뛰어난 결과를 보여주는 좋은 예가 될 수 없으며 이 문서를 선택한 이유를 다시 검토할 수 있습니다.  

- 어떠한 문서도 리턴되지 않은 경우 리턴되지 않은 이유를 검토하고 텍스트가 조회의 부분과 일치하는 문서에 있는지 확인해야 합니다.  

**참고:** 이 경고는 하나 이상의 올바르지 않은 조회가 있을 수 있음을 표시합니다. 그러나 훈련이 발생하지 않을 것임을 표시하는 것은 아닙니다.  

### 오류: `Invalid training data found: Syntax error when parsing query`
{: #error-syntax}

- 이는 실제 조회 구문에 문제가 있음을 의미합니다. 조회가 결과를 리턴하여 구문 오류가 발생하지 않는지 확인하십시오. 필터를 자연어 조회에 추가하는 경우에만 발생할 수 있습니다.

### 오류: `Invalid training data found: The query string provided exceeds the maximum length, please provide a shorter one`
{: #error-exceedlength}

- 최대 조회 문자열 길이는 `2048`입니다. 특정 조회를 줄여야 합니다. 임시 해결책 중 하나는 조회에 필터를 포함하는 것입니다.  

### 오류: `This collection cannot be trained: your plan does not support training on this many top-level text fields.`
{: #error-toplevelfields}

- 이 오류는 `Lite` 플랜에만 발생합니다. 최상위 레벨 필드는 다른 필드 아래에 중첩되지 않는 필드입니다. 훈련은 최상위 레벨 필드에서만 발생하고 훈련 프로세스에 사용할 수 있는 필드의 수에 대한 제한이 있습니다. 콜렉션의 최상위 레벨 필드가 많을수록 더 많은 훈련 데이터가 필요합니다. 또한 상위 레벨 필드가 `10` 이상인 경우 훈련에서 오류가 발생할 가능성이 높습니다. 

### 오류: `Training data quality standards not met: You will need additional training queries with labeled examples. (To be considered for training, each example must appear in the top 100 search results for its query.)`
{: #error-labels}

- 이는 성공적으로 훈련하려면 더 많은 훈련 데이터를 추가해야 함을 의미합니다. 최소 49개의 고유 훈련 조회가 필요하며 각 훈련 조회에는 최소 하나의 순위 지정된 문서가 필요합니다. 최소값이 최적이 아닙니다. 콜렉션의 크기 및 기타 요인은 최소값을 충족시키기 위해 필요한 훈련 예제의 수를 늘릴 수 있습니다.  

### 오류: `Training data quality standards not met: Insufficient number of unique training queries. Expected at least n, but found m.`
{: #error-notunique}

- 최소 훈련 요구사항을 충족하기 위해 최소 49개의 고유 훈련 조회가 필요하며 각 훈련 조회에는 최소 하나의 순위 지정된 문서가 필요합니다. 고유 훈련 조회의 수가 충분하지만 계속해서 이 오류 메시지를 수신하는 경우 추가 오류에 대한 알림을 확인해야 합니다.  

### 오류: `Training data quality standards not met: No documents found with non-zero relevance labels.`
{: #error-relevance}

- 훈련 데이터에는 어떠한 문서가 상위 값인지를 지정하는 충분한 수의 레이블 지정된 데이터가 필요합니다. 이는 0이 아닌 값으로 일부 문서의 순위를 지정해야 함을 의미합니다. Discovery 도구를 사용하는 경우 관련성(`10`)으로 일부 문서의 순위를 지정해야 하고 API를 사용하는 경우 `1` 이상으로 일부 문서의 레이블을 지정해야 합니다.   

### 오류: `Training data quality standards not met: Training examples have no relevance label variety for X queries.`
{: #error-variety}

- 훈련에 대한 요구사항 중 하나는 충분한 레이블 관련성을 보유하는 것입니다. 이는 시스템이 잘 훈련되기를 원하는 경우 가장 관련성이 높은 일치 항목인 문서 뿐만 아니라 “좋은” 관련성이 있는 문서인 문서도 추가해야 함을 의미합니다. 즉, 범위가 0 - 4인 경우 문서가 2's, 3's 및 4's로 등급이 지정되는 것이 좋습니다. (Discovery 도구를 사용하는 경우 문서는 관련성(`10`) 또는 관련성 없음(`0`)으로 등급이 지정됩니다.) 질문의 최소 25%에는 일부 레이블 다양성이 있어야 합니다.   
