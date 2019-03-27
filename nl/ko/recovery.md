---

copyright:
  years: 2019
lastupdated: "2019-03-07"

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

# 고가용성 및 재해 복구
{: #recovery}

{{site.data.keyword.discoveryfull}}는 단일 실패 지점 없이 고가용성을 지원합니다. 또한 고객은 서비스를 다시 작성할 수 있도록 고유한 재해 복구를 지원하여 {{site.data.keyword.discoveryshort}} 데이터를 백업해야 합니다.
{: shortdesc}

{{site.data.keyword.discoveryshort}} 트래픽은 지역의 여러 구역에서 로드 밸런싱됩니다. 각 구역은 동일한 지역의 데이터 센터입니다. 자세한 정보는 [작동 중단이 발생하지 않도록 하는 방법 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/docs/overview?topic=overview-zero-downtime#zero-downtime){: new_window}을 참조하십시오.

## Watson Discovery에서 데이터 백업
{: #backup}

{{site.data.keyword.discoveryfull}}에 저장된 데이터를 백업할 수 있는 여러 방법이 있습니다. 이 방법은 재해 복구 플랜에 포함되어야 합니다. 

-  소스 문서와 같은 사본을 보존해야 하는 데이터
-  {{site.data.keyword.discoveryshort}}에서 저장하고 추출하고 백업해야 하는 데이터
  
처음부터 다시 작성되어야 하는 데이터가 있습니다(예: 피드백 이벤트와 같이 백업할 수 없는 데이터). 

### 수집된 문서
{: #backupdocs}

업로드된 문서는 변환되고 강화된 후 검색 인덱스에 저장됩니다. 검색 인덱스는 재해의 경우 복구되지 않으며, 이에 따라 안전한 장소에 모든 소스 문서의 백업을 저장해야 합니다. 

외부 데이터 소스의 스케줄된 크롤링을 수행하여 문서를 가져오는 경우에도 데이터 소스를 빠르게 다시 설정할 수 있도록 데이터 소스 인증 정보를 외부에서 보유하고 있어야 합니다. 사용 가능한 소스 목록 및 각각 필요한 인증 정보는 [데이터 소스에 연결](/docs/services/discovery?topic=discovery-sources#sources)을 참조하십시오.

### 구성
{: #backupconfigs}

재해 발생 시 인스턴스 구성을 백업하고 이를 로컬에 저장해야 합니다.  

이 구성을 백업하려면 먼저 각 인스턴스에 대한 [구성을 나열하십시오](https://cloud.ibm.com/apidocs/discovery#list-configurations). 

구성 목록을 얻은 후 각 구성에 대한 [세부사항을 가져오십시오](https://cloud.ibm.com/apidocs/discovery#get-configuration-details).

### 훈련 데이터
{: #backuptraining}

재해 발생 시 각 훈련된 콜렉션마다 훈련 데이터를 백업하고 이를 로컬에 저장해야 합니다.  

훈련 데이터는 콜렉션의 명시 훈련에 사용되며 콜렉션별로 저장됩니다.  

훈련 데이터를 추출하려면 API를 사용하여 {{site.data.keyword.discoveryshort}}에서 조회와 등급을 다운로드하십시오.  

1.  [훈련 데이터를 나열하십시오](https://cloud.ibm.com/apidocs/discovery#list-training-data).
1.  각 조회에 대한 [예를 나열하십시오](https://cloud.ibm.com/apidocs/discovery#list-examples-for-a-training-data-query).
1.  훈련 데이터 예에 대한 [세부사항을 가져오십시오](https://cloud.ibm.com/apidocs/discovery#get-details-for-training-data-example). 

훈련 데이터에 사용하는 `document ids`는 현재 콜렉션의 문서를 가리킵니다. 올바른 ID가 참조되도록 새 콜렉션에서 동일한 `document ids`를 사용해야 합니다. 그렇지 않으면 복원된 관련성 훈련은 작동하지 않습니다.
{: important} 

### 조회
{: #backupqueries}

기본적으로(선택하지 않는 경우) {{site.data.keyword.discoveryshort}}는 사용자가 전송하는 조회를 저장합니다. 

[통계 목적](https://cloud.ibm.com/apidocs/discovery#number-of-queries-over-time)으로 이 조회를 복원할 수 있으려면 해당 조회를 개별적으로 저장해야 합니다.  

{{site.data.keyword.discoveryshort}}에서 [조회를 추출](https://cloud.ibm.com/apidocs/discovery#search-the-query-and-event-log)할 수 있으나 최대 10,000개의 조회만 저장됩니다. 페이징 API가 없습니다. 조회 복원은 권장되지 않으며 처음부터 시작하는 것이 좋습니다. 

### 피드백/클릭
{: #clicks}

피드백 이벤트 양식으로 클릭을 저장하는 경우 현재 이 정보를 백업하고 복원할 수 있는 간단한 방법은 없습니다. [클릭/피드백 데이터](https://cloud.ibm.com/apidocs/discovery#create-event) API를 사용하여 처음부터 시작하는 것이 좋습니다.

### 확장 목록
{: #backupexpansions}

조회 수정을 위해 확장을 사용하는 경우 확장 목록을 백업하고 이를 로컬에 저장해야 합니다. 이를 수행하려면 [확장 목록 가져오기](https://cloud.ibm.com/apidocs/discovery#get-the-expansion-list) API 명령을 사용하여 확장 목록을 요청하고 이를 로컬에 저장하십시오. 

### 토큰화 사전 또는 제외어
{: #backupstopwords}

이 기능을 사용하는 경우 해당 파일을 백업하고 로컬에 저장해야 합니다. 제외어의 경우 텍스트 파일을 백업하고, 토큰화의 경우 JSON 파일을 백업해야 합니다. 각 파일 유형에 대한 자세한 정보는 [사용자 정의 토큰화 사전 작성](/docs/services/discovery?topic=discovery-query-concepts#tokenization) 및 [제외어 정의](/docs/services/discovery?topic=discovery-query-concepts#stopwords)를 참조하십시오. 

### 콜렉션 정보
{: #collectioninfo}

필수는 아니지만, 정기적으로 각 콜렉션에 대한 [상태를 검색](https://cloud.ibm.com/apidocs/discovery#get-collection-details)하고 정보를 로컬에 저장하는 것이 좋습니다. 이 통계를 유지하면 필요한 경우 복원 프로세스가 성공적이었는지를 나중에 확인할 수 있습니다.
{: tip} 


### Smart Document Understanding 모델
{: #backupsdu}

SDU(Smart Document Understanding)를 사용하는 경우 구성관 연관된 모델을 보유하게 됩니다. 정보 유실을 방지하려면 [모델을 내보내야](/docs/services/discovery?topic=discovery-sdu#import) 하고 백업한 후 로컬에 저장해야 합니다. SDU 모델에는 `.sdumodel`의 파일 확장자가 있습니다.


## 데이터를 새 Watson Discovery 인스턴스에 복원
{: #restore}

다른 데이터 센터(댈러스, 휴스턴, 워싱턴, DC, 런던과 같은 지역/위치라고도 함)에서 새 {{site.data.keyword.discoveryshort}} 인스턴스로 복원하기 위해 백업을 사용해보십시오.
{: note}

복원을 시작하려면 먼저 콜렉션 목록, 연관된 데이터 소스 및 파일 백업의 검토부터 시작하십시오.

-  저장된 구성 정보를 사용하여 [환경](https://cloud.ibm.com/apidocs/discovery#create-an-environment) 및 [콜렉션](https://cloud.ibm.com/apidocs/discovery#create-a-collection)을 작성하십시오. 적절한 구성이 올바르게 정의되었으며 콜렉션의 언어가 올바르게 설정되었는지 확인하십시오. 그렇지 않으면 시스템 백업 및 실행이 지연됩니다. 
-  {{site.data.keyword.discoveryshort}}에서 설정된 사용자 정의 구성이 있는 경우 [해당 사용자 정의 구성을 다시 작성](/docs/services/discovery?topic=discovery-configservice#when-you-need-a-custom-configuration)해야 합니다.  
-  토큰화 사전 또는 제외어를 콜렉션에 다시 추가하십시오. [사용자 정의 토큰화 사전 작성](/docs/services/discovery?topic=discovery-query-concepts#tokenization) 및 [제외어 정의](/docs/services/discovery?topic=discovery-query-concepts#stopwords)를 참조하십시오.  
-  사용자 정의 조회 확장이 있는 경우 각 콜렉션에 대해서도 [조회 확장을 추가](https://cloud.ibm.com/apidocs/discovery#create-or-update-expansion-list)해야 합니다. 
-  강화를 위해 Watson Knowledge Studio(WKS)에서 사용자 정의 엔티티 모델을 사용한 경우 {{site.data.keyword.discoveryshort}} 인스턴스로 [해당 모델을 다시 가져와야](/docs/services/discovery?topic=discovery-configservice#custom-entity-model) 합니다.

이전과 같이 콜렉션을 설정한 후 소스 문서 수집을 시작해야 합니다. 이전에 문서를 수집한 방법에 따라 다음을 사용하여 이를 수행할 수 있습니다.
-  [API](https://cloud.ibm.com/apidocs/discovery#add-a-document)
-  [커넥터](/docs/services/discovery?topic=discovery-sources#sources) 
-  [Data Crawler](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)
-  기타 방법

### 훈련 데이터 복원
{: #restoretraining}

콜렉션이 복원된 후 [관련성 훈련 모델 다시 작성](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api) 프로세스를 시작할 수 있습니다. 

백업한 훈련 데이터를 검색한 후 다음을 수행하십시오.

1. [조회를 업로드](https://cloud.ibm.com/apidocs/discovery#add-query-to-training-data)하십시오. 
1. 각 조회에 대한 [예제 문서를 업로드](https://cloud.ibm.com/apidocs/discovery#add-example-to-training-data-query)하십시오.
1.  훈련 데이터가 업로드되면 이 [블로그 게시물](https://developer.ibm.com/dwblog/2017/get-relevancy-training/)을 살펴보고 이전의 정확도 수치를 충족하는지 확인하십시오. 이전 `document ids`는 새 콜렉션에서 새 훈련 데이터로 전송되거나 새 문서 ID를 반영하도록 업데이트되어야 합니다. 


### 외부 데이터 소스에 대한 연결 복원
{: #restoreconnections}

예기치 않은 데이터 유실이 발생한 경우 외부 데이터 소스의 스케줄된 크롤링을 유실할 수 있습니다. 사용 가능한 소스 목록은 [데이터 소스에 연결](/docs/services/discovery?topic=discovery-sources#sources)을 참조하십시오.

외부 데이터를 복원하려면 데이터 소스에 대한 연결을 다시 설정한 후 이 연결을 다시 크롤링해야 합니다. 

이전에 저장한 데이터 소스 인증 정보를 찾고 [여기](/docs/services/discovery?topic=discovery-sources#sources)의 지시사항을 따르십시오. 이를 통해 데이터 소스에 다시 연결하고 데이터를 {{site.data.keyword.discoveryshort}}로 가져올 수 있습니다.


### Smart Document Understanding 모델 복원
{: #restoresdu}

이전에 가져온 SDU(Smart Document Understanding) 모델을 가져오려면 [여기](/docs/services/discovery?topic=discovery-sdu#import)의 지시사항을 따르십시오. SDU 모델에는 `.sdumodel`의 파일 확장자가 있습니다.

SDU 기존 모델을 새 콜렉션으로 가져오는 경우 새 콜렉션을 작성하고 하나의 문서를 추가한 후 모델을 가져와서 문서의 나머지 부분을 업로드하는 것이 좋습니다. 
