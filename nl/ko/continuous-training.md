---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-25"

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

# Continuous Relevancy Training
{: #crt}

{{site.data.keyword.discoveryshort}} Continuous Relevancy Training은 사용자 행동을 자동으로 학습하여 결과의 관련성 순위를 향상시키는 데 필요한 노력을 크게 줄일 수 있습니다. 이는 사용자의 상호작용을 사용하여 가장 관련성이 높은 결과를 표시하는 방법을 학습합니다. 클릭과 같은 상호작용을 학습하여 사용자에게 가장 가치가 높은 결과를 판별하고 향후 조회를 위해 가장 중요한 신호를 공개할 수 있습니다. Continuous Relevancy Training은 관련성이 가장 높은 정보를 결과의 맨 위에 놓기 위해 문서의 순위를 다시 지정합니다. 이를 사용하여 다음을 수행할 수 있습니다.

- 클릭하는 결과를 기반으로 지원 에이전트에 대한 결과 관련성을 향상시키는 데 도움을 줍니다.
- 선택한 롱테일 결과를 기반으로 고객 챗봇에 보다 많은 관련성 결과를 표시합니다. 
- 탐색한 결과를 기반으로 보다 관련성 높은 응답을 전문가에게 제공합니다.

Continuous Relevancy Training을 설정하려면 다음을 수행하십시오.

- Continuous Relevancy Training은 환경 레벨에서만 사용할 수 있습니다. 조회는 `/api/v1/environment/{environment_id}/query` 및 `/api/v1/environments/{environment_id}/query` 엔드포인트를 사용하여 하나 이상의 콜렉션을 조회해야 합니다.
- {{site.data.keyword.discoveryshort}} `events`(클릭)를 사용하여 필요한 훈련 데이터를 작성하므로 먼저 이벤트 추적을 통합하십시오. 세부사항은 [사용 모니터링](/docs/services/discovery?topic=discovery-usage#usage)을 참조하십시오.

- Continuous Relevancy Training을 시작하려면 연관된 클릭 이벤트가 있는 1000개 이상의 자연어 조회가 필요합니다. 이벤트 및 로그는 인스턴스 전체에서 30일 동안 보존되므로 1000번의 클릭은 해당 기간 동안 수집되어야 합니다.
- Continuous Relevancy Training은 고급 플랜 크기 `Small` 이상 및 프리미엄 플랜에서 사용할 수 있습니다. `Lite` 플랜에서는 사용할 수 없습니다.
- Continuous Relevancy Training의 콜렉션 수는 `5`로 제한됩니다. Continuous Relevancy Training은 여러 개의 콜렉션에서 작동하므로 조회와 훈련 항목 모두 확장될 수 있습니다.
- Continuous Relevancy Training은 최상위 레벨 필드에서만 발생하고 훈련 프로세스에 사용할 수 있는 필드 수에 대한 제한이 있습니다. 상위 레벨 필드가 `10` 이상인 경우 훈련에서 오류가 발생할 가능성이 높습니다. 

Continuous Relevancy Training을 사용하려면 다음을 수행하십시오.

훈련되면 Continuous Relevancy Training을 사용하여 환경 레벨 조회 사용 시 `natural_language_query` 결과에 영향을 줍니다. 

환경의 모든 콜렉션에서 다중 콜렉션 `natural_language_query`를 실행하여 조회 시 Continuous Relevancy Training을 사용할 수 있습니다. 지시사항은 [다중 콜렉션 조회](/docs/services/discovery?topic=discovery-query-concepts#multiple-collections)를 참조하십시오. 

**참고:** Continuous Relevancy Training은 훈련되거나 훈련되지 않은 콜렉션 레벨(`/v1/environments/{environment_id}/collections/{collection_id}/query`) 조회 호출에 대한 조회에는 영향을 주지 않습니다. 

추적 상태:

Continuous Relevancy Training 상태는 `/api/v1/environments` 엔드포인트에서 볼 수 있습니다. [API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/discovery#get-environment-info){: new_window}를 참조하십시오. `status`는 훈련 오퍼레이션의 상태에 대한 정보를 제공하고 Continuous Relevancy Training이 활성 상태인지 여부를 알려줍니다.

```
"search_status" : [
        {
            "scope" : "environment",
            "status" : "NO_DATA",
            "status_description" : "Discovery is employing a default strategy for document search natural_language_query. Enable query and event logging so we can initiate relevancy training to improve search accuracy.”
        }
    ]
```
