---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-08"

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


# 튜토리얼: Retrieve and Rank에서 마이그레이션

{{site.data.keyword.retrieveandrankshort}}에서 {{site.data.keyword.discoveryfull}} 서비스로의 마이그레이션입니다. Cranfield 시작하기 튜토리얼의 연장선입니다. 

## 개요
{: #overview}
이 튜토리얼은 샘플 데이터를 사용한 {{site.data.keyword.discoveryfull}} 서비스 작성 및 훈련의 프로세스에 대해 설명합니다. 이 튜토리얼에서는 [{{site.data.keyword.retrieveandrankshort}} 시작하기 튜토리얼](/docs/services/retrieve-and-rank/getting-started.html)에서 사용한 동일한 데이터 세트를 사용하지만, 같은 접근 방법을 사용하여 고유한 데이터를 사용하는 서비스 인스턴스를 작성할 수 있습니다. 

{{site.data.keyword.retrieveandrankshort}}에서 {{site.data.keyword.discoveryshort}}로 데이터를 마이그레이션하는 사용자를 위한 프로세스는 두 개의 주요 단계로 구성됩니다. 

1. 콜렉션 데이터를 마이그레이션합니다.
2. 훈련 데이터를 마이그레이션합니다.

훈련된 콜렉션 데이터를 마이그레이션할 때 **가장** 중요한 것은 _문서 ID를 동일하게 유지하는 것입니다_. 이는 훈련 데이터가 실제 값을 참조하기 위해 이 ID를 사용하기 때문이며, ID가  {{site.data.keyword.retrieveandrankshort}}에서 {{site.data.keyword.discoveryshort}}로 이동하는 중에 변경되는 경우 순위 재지정은 완전하게 해제됩니다(또는 훈련이 시작도 하지 않을 수 있음). {{site.data.keyword.discoveryshort}}를 통해 API 업로드 프로세스의 문서 ID를 지정할 수 있으므로 이 문서의 가이드라인에 따라 이 문제점을 방지할 수 있습니다. {{site.data.keyword.retrieveandrankshort}} 훈련 데이터는 일반적으로 `csv` 파일에 저장됩니다. 이 튜토리얼에서 이 `csv` 파일은 샘플 훈련 데이터를 {{site.data.keyword.discoveryshort}}에 업로드하는 데 사용됩니다. {{site.data.keyword.retrieveandrankshort}} 도구에서 내보낸 훈련 데이터의 마이그레이션은 [서비스에서 훈련 데이터 마이그레이션](/docs/services/discovery/migrate-dcs-rr.html#extract-train)에서 자세하게 설명됩니다. 

이 튜토리얼에서는 {{site.data.keyword.retrieveandrankshort}}가 [{{site.data.keyword.retrieveandrankshort}} 시작하기 튜토리얼](/docs/services/retrieve-and-rank/getting-started.html)과 유사하게 설정되며 [여기](/docs/services/discovery/migrate-dcs-rr.html#source)에 설명된 소스 경로의 마이그레이션을 사용한다고 간주합니다. 기타 마이그레이션 옵션은 [Watson Discovery 서비스에 대한 마이그레이션 경로 평가](/docs/services/discovery/migrate-dcs-rr.html#evaluate)를 참조하십시오. 

튜토리얼을 완료하려면 다음이 필요합니다. 

-  **cURL.**  [haxx.se ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://curl.haxx.se/){: new_window}에서 사용자의 운영 체제에 맞는 cURL의 버전을 설치할 수 있습니다. SSL(Secure Sockets Layer) 프로토콜을 지원하는 버전을 설치해야 합니다. PATH 환경 변수에 설치된 2진 파일을 포함하는지 확인하십시오. 
-  샘플 Cranfield 데이터. 이 튜토리얼은 {{site.data.keyword.retrieveandrankshort}} 시작하기 튜토리얼의 샘플 콜렉션 데이터를 사용합니다. [Cranfield JSON 데이터 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-data.json){: new_window}를 참조하십시오. 
-  **샘플 데이터 실제 값.** 이 튜토리얼은 {{site.data.keyword.retrieveandrankshort}} 시작하기 튜토리얼에서 샘플 Cranfield 실제 값을 사용합니다. [Cranfield 실제 값 CSV ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-gt.csv){: new_window}를 참조하십시오.
-  **Python 버전 2.**  Python의 설치 여부를 확인하려면 명령 프롬프트에 `python --version`을 입력하고 버전 번호가 2로 시작하는지 확인하십시오. Python을 설치해야 하는 경우 [Python 다운로드 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://wiki.python.org/moin/BeginnersGuide/Download){: new_window}를 참조하십시오.
-  데이터 업로드 스크립트: [Discovery 문서 업로더 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-upload.py){: new_window}
-  훈련 데이터 업로드 스크립트: [Discovery 훈련 업로더 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-train.py){: new_window}

이 튜토리얼을 시작하기 전에 다음 전제조건이 필수입니다. 

-  이 튜토리얼에서는 사용자가 이미 {{site.data.keyword.discoveryshort}} 인스턴스를 작성했다고 간주합니다. {{site.data.keyword.discoveryshort}} 인스턴스 작성 방법에 대한 지시사항이 필요한 경우 [튜토리얼 준수](/docs/services/discovery/getting-started.html)를 참조하십시오.

-  이 튜토리얼에서는 서비스 신임 정보가 있다고 간주합니다. 
   -  {{site.data.keyword.Bluemix_notm}}에 Watson {{site.data.keyword.discoveryshort}} 서비스가 있는 경우 **서비스 신임 정보**를 클릭하십시오. 
   -  조치 아래에서 **신임 정보 보기**를 클릭하십시오. 
   -  `username` 및 `password` 값을 복사하고 `url` 값이 아래 예제의 값과 일치하는지 확인하십시오. 일치하지 않으면 이 값을 대체하십시오. 

## Discovery에 Cranfield 데이터 추가

1.  환경을 작성하십시오. 

    ```bash
    curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{ "name": "my_environment", "description": "My environment" }' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    리턴된 JSON에 나열된 `environment-id`를 복사하십시오. 

1. 콜렉션을 작성하십시오. 

    ```bash
    curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{ "name": "test_collection", "description": "My test collection", "configuration_id": "{configuration_id}", "language_code": "en" }' "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07"
    ```
    {: pre}

    리턴된 JSON에 나열된 `collection-id`를 복사하십시오. 

1.  검색할 문서를 추가하십시오. 
    1.  아직 다운로드하지 않은 경우 [cranfield-data.json ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-data.json){: new_window} 파일을 다운로드하십시오. 이는 {{site.data.keyword.retrieveandrankshort}}에 사용되는 문서의 소스입니다. Cranfield 콜렉션 문서는 JSON 형식으로 되어 있습니다. JSON 형식은 {{site.data.keyword.retrieveandrankshort}}에서 허용한 형식이고 {{site.data.keyword.discoveryshort}}에서도 제대로 작동합니다.
        **참고:** {{site.data.keyword.discoveryshort}}에서는 Solr 스키마를 업데이트하지 않아도 됩니다. 이는 {{site.data.keyword.discoveryshort}}에서 자동으로 JSON 구조의 스키마를 추정하기 때문입니다. 
    1.  데이터 업로드 스크립트를 [여기 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-upload.py){: new_window}에서 다운로드하십시오. 이 스크립트는 {{site.data.keyword.discoveryshort}}에 Cranfield json을 업로드합니다. 스크립트는 JSON 파일을 통해 읽으며 {{site.data.keyword.discoveryshort}}의 기본 구성을 사용하여 각 개별 JSON 문서를 {{site.data.keyword.discoveryshort}} 서비스에 전송합니다.
        **참고:** {{site.data.keyword.discoveryshort}}의 기본 구성은 {{site.data.keyword.retrieveandrankshort}}의 기본 Solr 구성과 유사한 설정을 제공합니다. 
    1.  다음 명령을 실행하여 `cranfield-data-json` 데이터를 `cranfield_collection` 콜렉션에 업로드하십시오. `{username}`, `{password}`, `{path_to_file}`,  `{environment_id}`, `{collection_id}`를 사용자의 정보로 대체하십시오. curl의 추가 옵션으로 -d(디버그용) 및 –v(상세 출력용)가 있습니다. 

        ```bash
        python ./disco-upload.py -u {username}:{password} -i {path_to_file}/cranfield-data.json –e {environment_id} -c {collection_id}
        ```
        {: pre}

1.  업로드 프로세스가 완료되면 다음 명령을 실행하여 문서가 있는지 확인하고 콜렉션 세부사항을 볼 수 있습니다. 

    ```bash
    curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07"
    ```
    {: pre}

    출력이 다음과 같이 표시됩니다.

    ```json
    {
      "collection_id": "f1360220-ea2d-4271-9d62-89a910b13c37",
      "name": "democollection",
      "description": "this is a demo collection",
      "created": "2015-08-24T18:42:25.324Z",
      "updated": "2015-08-24T18:42:25.324Z",
      "status": "available",
      "configuration_id": "6963be41-2dea-4f79-8f52-127c63c479b0",
      "language": "en",
      "document_counts": {
        "available": 1000,
        "processing": 20,
        "failed": 180
      },
      "disk_usage": {
        "used_bytes": 260
      },
      "training": {
        "total_examples": 0,
        "available": false,
        "processing": false,
        "minimum_queries_added": false,
        "minimum_examples_added": true,
        "sufficient_label_diversity": false,
        "notices": 0,
        "successfully_trained": null,
        "data_updated": null
      }
    }
    ```
    {: codeblock}

업로드된 문서의 수를 확인하려면 `document_counts` 섹션을 살펴보십시오. 이 샘플 데이터 세트를 사용하면 문서 오류가 발생하지 않을 것으로 기대합니다. 그러나 기타 데이터 세트를 사용하면 실패한 문서 수가 표시될 수 있습니다. 실패한 문서 수가 있으면 오류 메시지를 표시하는 알림 API를 볼 수 있습니다. 알림 API를 검토하려면 [여기 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-notices){: new_window}를 참조하십시오. 

리턴의 `training` 섹션은 훈련에 대한 정보를 제공합니다. 훈련 데이터 업로드 후 해당 섹션을 검토할 것입니다. 

## Discovery에 훈련 데이터 추가

Watson {{site.data.keyword.discoveryshort}} Service는 문서의 순위를 재지정하기 위해 기계 학습 모델을 사용합니다. 이를 위해 모델 훈련이 필요합니다. 적절하게 등급이 지정된 문서와 함께 충분한 조회를 로드한 후 훈련이 수행됩니다. 충분한 변수를 사용한 충분한 예제를 Watson {{site.data.keyword.discoveryshort}}에 로드하여 "좋은" 문서가 무엇인지 알려줍니다. 이 단계에서 Watson {{site.data.keyword.discoveryshort}}를 훈련시키기 위해 {{site.data.keyword.retrieveandrankshort}}에 사용되는 기존 Cranfield "실제 값"을 사용합니다. 

1.  아직 수행하지 않은 경우 {{site.data.keyword.retrieveandrankshort}} 튜토리얼에서 샘플 [Cranfield 실제 값 CSV 파일 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-gt.csv){: new_window}을 다운로드하십시오. 

   파일은 사용자가 문서에 대해 질문할 수 있는 질문의 세트입니다. 파일은 질문 및 관련된 답변에 대해 순위 지정자({{site.data.keyword.retrieveandrankshort}}) 및 관련성 훈련({{site.data.keyword.discoveryshort}})을 훈련시키기 위한 정보 예제를 제공합니다. 

   각 질문의 경우 답변에 최소 하나의 ID가 있습니다(문서 ID). 각 문서 ID에는 질문에 대한 답변의 관련성을 표시하는 숫자가 포함됩니다. 문서 ID는 이전 단계에서
{{site.data.keyword.discoveryshort}}에 업로드한 `cranfield-data.json` 파일에서 답변을 가리킵니다. 

1.  훈련 데이터 업로드 스크립트를 다운로드하십시오. 이 스크립트를 사용하여 훈련 데이터를 {{site.data.keyword.discoveryshort}}에 업로드합니다. 스크립트는 `csv` 파일을 JSON 조회 및 예제의 세트로 변환하고 [훈련 데이터 API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#training-data){: new_window}를 사용하여 이를 {{site.data.keyword.discoveryshort}} 서비스에 전송합니다.
    **참고:** {{site.data.keyword.discoveryshort}}는 서비스 내의 훈련 데이터를 관리하므로 새 예제 및 훈련 조회를 생성할 때 유지보수되어야 할 개별 CSV 파일의 일부가 아닌 자체적으로 {{site.data.keyword.discoveryshort}}에 저장될 수 있습니다. 
1.  훈련 업로드 스크립트를 실행하여 훈련 데이터를 {{site.data.keyword.discoveryshort}}에 업로드하십시오. `{username}`, `{password}`, `{path_to_file}`,  `{environment_id}`, `{collection_id}`를 사용자의 정보로 대체하십시오. curl의 추가 옵션으로 `-d`(디버그용) 및 `–v`(상세 출력용)가 있습니다. 

    ```bash
    python ./disco-train.py -u {username}:{password} -i {path_to_file}/cranfield-gt.csv –e {environment_id} -c {collection_id}
    ```
    {: pre}

1.  데이터가 로드되면 이전 섹션에서 표시된 콜렉션 세부사항 명령을 사용하여 훈련의 상태를 확인할 수 있습니다. {{site.data.keyword.discoveryshort}}는 시간당 한 번 정도 새 데이터가 있는지 확인하고, 새 데이터가 있으면 새 데이터의 처리를 시작하고 이는 기계 학습 모델로 변경됩니다. 모델을 훈련시키는 중이면 훈련 섹션 상태가 `"processing": false`에서 `"processing": true`로 변경됩니다. 모델을 훈련시킨 후에는 훈련 섹션 상태가 `"available": false`에서 `"available": true`로 변경됩니다. 또한 `"successfully_trained"` 값의 날짜 변경도 표시됩니다.  오류가 있으면 이전 섹션에서 설명된 대로 **알림 API**를 통해 오류를 볼 수 있습니다. 

## 문서 검색
{: search}

{{site.data.keyword.discoveryshort}} 서비스는 훈련된 모델을 자동으로 사용하여 검색 결과의 순위를 재지정합니다(사용 가능한 경우). [API 호출 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection){: new_window}이 `query` 대신 `natural_language_query`로 수행되는 경우 모델이 사용 가능한지 확인하기 위한 검사를 수행합니다. 모델이 사용 가능하면 {{site.data.keyword.discoveryshort}}는 해당 모델을 사용하여 결과의 순위를 재지정합니다. 먼저, 순위가 지정되지 않은 문서를 검색한 후 순위 지정 모델을 사용하여 검색합니다. 

1.  cURL 명령을 사용하여 콜렉션에서 문서를 검색할 수 있습니다. 순위가 지정되지 않은 결과를 확인하려면 조회 API를 사용하여 조회를 수행하십시오. `{username}`, `{password}`, `{environment_id}`, `{collection_id}`를 고유한 값으로 대체하십시오. 리턴된 결과는 순위가 재지정된 결과이며 기본 {{site.data.keyword.discoveryshort}} 순위 지정 공식을 사용합니다. 훈련 데이터 `csv` 파일을 열고 첫 번째 열의 값을 조회 매개변수에 복사하여 기타 조회를 시도할 수 있습니다. 

    ```bash
    curl -u "{username}":"{password}""https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query=what is the basic mechanism of the transonic aileron buzz"
    ```
    {: pre}

1.  이제 `natural_language_query` 매개변수를 설정하여 모델을 사용한 검색을 수행하십시오. 이를 수행하기 전에 이전 섹션에서 설명된 대로 훈련된 모델이 있는지 확인하십시오. `{username}`, `{password}`, `{environment_id}`, `{collection_id}`를 사용자의 값으로 대체하여 콘솔의 다음 코드를 붙여넣으십시오. 

    ```bash
    curl -u "{username}":"{password}""https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&natural_language_query=what is the basic mechanism of the transonic aileron buzz"
    ```
    {: pre}

    이 명령은 이전에 훈련된 모델을 사용하여 결과의 순위를 재지정합니다. 이 검색의 결과 및 이전에 시도한 기타 검색의 일부 결과를 비교하십시오. {{site.data.keyword.retrieveandrankshort}}에서 확인한 것과 비교하여 결과의 일부 차이점을 볼 수 있습니다. 이는 검색에 사용되는 일부 기술이 경험을 단순화하고 결과를 향상시키기 위해 변경되었으나 전체적인 결과의 품질은 유사하기 때문입니다. 

순위가 재지정된 검색 결과를 평가한 후, 추가 훈련 조회 및 예제를 사용하여 훈련 데이터의 업로드 단계를 반복하고 검색 결과를 확인하여 {{site.data.keyword.discoveryshort}}에서 순위가 재지정된 검색 결과를 세분화할 수 있습니다. 또한 첫 번째 단계에 설명된 대로 새 문서를 추가하여 검색의 범위를 확장할 수 있습니다. {{site.data.keyword.retrieveandrankshort}}와 유사하게 훈련을 통한 결과 향상은 반복적인 프로세스입니다. 
