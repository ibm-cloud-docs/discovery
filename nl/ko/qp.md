---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-18"

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

# 조회 성능
{: #qp}

{{site.data.keyword.discoveryshort}}의 조회 성능은 여러 요인에 따라 달라집니다.  

## 성능 평가 
{: #qp-evaluate}

사용자 애플리케이션에서 동시에 많은 작업량을 로드하려면 {{site.data.keyword.discoveryshort}} 애플리케이션의 성능을 평가하는 것이 중요합니다. 성능을 측정하는 데 일반적으로 사용되는 여러 차원이 있습니다. 
1.  **응답 대기 시간** - {{site.data.keyword.discoveryshort}}에서 조회의 결과를 리턴하는 데 걸리는 시간입니다.  
    - 대기 시간은 여러 요인에 따라 달라질 수 있습니다. 자세한 정보는 [성능에 영향을 주는 요인](/docs/services/discovery?topic=discovery-qp#perffactors)을 참조하십시오. 
    - 평균 대기 시간을 판별하려면 대표적인 조회 세트를 사용하여 제품 환경에서 테스트를 실행하는 것이 중요합니다. 
1.   **조회 비율** - 지정된 시간에 처리될 수 있는 요청 수이며, 보통 QPS(Queries per Second)에서 측정됩니다. 사용자 애플리케이션에서 동시에 많은 작업량을 로드하려면 이 측정이 가장 중요합니다.  
     - 달성할 수 있는 비율은 대기 시간과 같은 여러 요인에 따라 달라집니다. 
     - 조회 비율은 대표 조회로 평가되고 표시될 로드에서도 평가되어야 합니다. 테스트 중에 최대 로드를 확인해야 합니다.

## 성능에 영향을 주는 요인
{: #perffactors}

{{site.data.keyword.discoveryshort}}의 조회 성능은 플랜 크기, 조회 복잡도, 사용된 기능, 콜렉션 크기 및 복잡도를 포함한 여러 요인에 따라 달라집니다. 

### 플랜 크기
{: #qp-plansize}

{{site.data.keyword.discoveryshort}} 가격 플랜은 사용 가능한 문서의 수를 제한하고, 조회 로드를 처리할 수 있는 다른 기능도 제공합니다. 플랜 크기가 클수록 조회를 처리하는 데 더 많은 리소스를 사용할 수 있습니다. 평균 비율 한계는 플랜 크기에 따라 다릅니다. 플랜을 업그레이드하면 성능이 향상될 수 있습니다. 플랜 및 제한사항은 [{{site.data.keyword.discoveryshort}} 가격 플랜](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)을 참조하십시오. 

### 조회 복잡도
{: #qp-query}

{{site.data.keyword.discoveryshort}}에 대한 조회를 실행할 수 있는 다양한 방법이 있으며 사용되는 여러 오퍼레이션은 성능에 영향을 줄 수 있습니다. 이러한 조회 특성은 성능에 영향을 줄 수 있습니다.

1.   **길이** - 길이가 길면 성능이 저하될 가능성이 높습니다.  
1.   **집계** - 집계는 좀 더 복잡한 조회 유형이며 중첩된 집계는 성능에 가장 큰 영향을 줍니다.  
1.   **연산자** - 와일드카드 및 퍼지 일치는 성능에 영향을 줄 수 있습니다.
1.   **수** - 리턴된 문서의 수가 줄어들면 성능이 향상될 수 있습니다. 결과를 통해 페이징해야 하는 경우 `offset` 매개변수를 사용하십시오. 
1.   **리턴 필드** - 애플리케이션에 필요한 항목에만 리턴되도록 필드를 제한하면 도움이 될 수 있습니다(예를 들어, 제목 및 단락만 필요한 경우 문서의 전체 텍스트를 리턴하지 않음).  

자세한 사항은 [조회 참조](/docs/services/discovery?topic=discovery-query-reference#query-reference)를 참조하십시오.

### 사용된 기능
{: #qp-features}

조회 결과를 향상시키는 많은 기능이 있습니다. 다음 기능은 성능에 영향을 줄 수 있습니다.
 
1.   **단락 검색** - 단락 검색은 조회를 위해 텍스트의 관련 스니펫을 찾기 위해 문서 내에서 검색합니다. 단락 검색이 `passages.fields` 매개변수를 사용하여 검색하는 문서에서 필드를 조정할 수 있습니다. 컨텐츠에 많은 필드가 있으면 이를 통해 단락 검색의 대기 시간이 줄어 듭니다. 단락 검색에 대한 자세한 정보는 [단락](/docs/services/discovery?topic=discovery-query-parameters#passages)을 참조하십시오.
1.   **관련성 훈련** - 관련성 훈련은 각 상위 레벨 텍스트 필드(JSON에서 `document_id`와 동일한 레벨의 필드)에 대한 기능을 컴퓨팅합니다. 상위 레벨 필드가 많으면 훈련 사용 시 `natural_language_query`에 대한 성능에 영향을 줄 수 있습니다. 상위 레벨 필드의 수를 줄이면 성능이 향상될 수 있습니다. 이러한 작업은 중첩된 구조로 된 관련 컨텐츠를 찾는 데 도움이 되지 않는 필드를 배치하도록 정규화를 통하거나 JSON을 수동으로 편집하여 수행될 수 있습니다. 훈련에 사용되는 필드를 변경해도 모델에 영향을 줄 수 있습니다. 그러므로 이 변경사항을 수행하는 경우 결과의 성능 및 정확성에 대한 영향을 모두 고려해야 합니다. 관련성 훈련에 대한 자세한 정보는 [결과 관련성 향상](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling)을 참조하십시오.
1.  **Continuous Relevancy Training** - Continuous Relevancy Training은 환경의 모든 콜렉션 전반에서 검색합니다. 환경에서 콜렉션이 많을수록 성능에 미치는 영향이 커집니다. 자세한 정보는 [Continuous Relevancy Training](/docs/services/discovery?topic=discovery-crt#crt)을 참조하십시오.

### 콜렉션 크기 및 복잡도
{: #qp-collection} 

개인용 콜렉션의 문서 구성은 조회 성능에 영향을 줄 수 있습니다. 
1.  **총 문서 수** - 고급 플랜 크기에 대한 `Number of Documents`의 상한에 도달하는 경우 성능에 영향을 줄 수 있습니다.  
1.  **문서 크기** - 크기가 매우 큰 문서(여러 개의 MB)에는 요청마다 대량의 데이터 이동이 필요하며, 이는 특히 단락 검색 및 관련성 훈련을 사용할 때 성능에 부정적인 영향을 줄 수 있습니다.  
1.  **인리치먼트 수** - 인리치먼트는 수많은 중첩된 필드를 추가하여 복잡도를 문서에 추가합니다. 유스 케이스에 인리치먼트가 필요하지 않은 경우 수집 시 이를 사용 안함으로 설정하십시오. 인리치먼트는 `natural_language_query` 검색 관련성에 직접 사용되지 않습니다. 인리치먼트에 대한 자세한 사항은 [인리치먼트 추가](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)를 참조하십시오.
