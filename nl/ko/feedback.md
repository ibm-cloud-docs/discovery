---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-17"

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

# 사용 모니터링
{: #usage}

{{site.data.keyword.discoveryshort}} 인스턴스의 사용을 모니터 및 추적하고 이 데이터를 사용하여 애플리케이션을 이해하고 향상시킬 수 있습니다. [이벤트 API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/discovery#create-event){: new_window}를 사용하여 특정 자연어 조회 및 조치와 연관된 로그 항목을 작성할 수 있습니다. 예를 들어 결과 세트에서 사용자가 "클릭"한 문서 및 언제 클릭되었는지를 기록할 수 있습니다.

**참고:** 로그 및 이벤트는 개인용 데이터 콜렉션의 자연어 조회에 대해서만 모니터됩니다. {{site.data.keyword.discoverynewsfull}}에서는 로그가 수집되지 않습니다.

{{site.data.keyword.discoveryshort}}는 다음 정보를 로그할 수 있습니다.
- **조회** - 사용자 환경의 콜렉션에 대해 자연어 조회를 실행합니다. 
- **노출**(또는 **결과**) -  특정한 조회에 대해 리턴되는 결과입니다(일반적으로 문서 또는 구절). 
- **이벤트** - 사용자가 {{site.data.keyword.discoveryshort}}에서 결과 또는 결과 세트에 대해 수행하는 상호작용입니다(예: 문서 결과 클릭).

**조회** 및 **노출**은 자동으로 로그되며, **이벤트** 로깅은 API를 통해 애플리케이션에 통합될 수 있습니다.

## 로그 보기
{: #viewlogs}

조회 및 이벤트 로그를 검색하여 지정된 기준과 일치하는 조회 세션을 찾을 수 있습니다. `logs` 엔드포인트를 검색하면 지원되는 매개변수에 표준 {{site.data.keyword.discoveryshort}} 조회 구문을 사용합니다. 엔드포인트는 기록된 데이터를 통해 보고 검색하는 데 필요한 기본 조회 기능을 제공합니다.  

`/api/v1/logs` 엔드포인트는 다음 {{site.data.keyword.discoveryshort}} 조회 매개변수를 지원합니다.
- query 
- filter
- sort
- count 
- offset
- version

매개변수의 기능 및 구문에 대한 추가 세부사항은 [조회 매개변수](/docs/services/discovery?topic=discovery-query-parameters#query-parameters)를 참조하십시오.

다음은 용어 “train”이 포함된 자연어 조회에 대한 로그 검색 예입니다.

`https://gateway.watsonplatform.net/discovery/api/v1/logs?version=2018-03-28&query=train`

`logs` 조회의 응답에는 {{site.data.keyword.discoveryshort}} 문서 결과와 유사하게 표시되는 결과가 포함됩니다. 각 결과는 문서 `type` 필드에 지정된 조회 또는 이벤트입니다.  

다음은 조회 로그 예입니다.

```
{
            "customer_id": "",
            "environment_id": "252e6e82-c2d2-450e-9670-0008b0a3a99c",
            "natural_language_query": "how do i get from the airport to the city",
            "query_id": "_Qs35yOoa7",
            "document_results": {
                "count": 2,
                "results": [
                    {
                        "collection_id": "af9e1f41-6114-4d77-bca6-c9b99b2601b1",
                        "score": 6.724753491503856,
                        "position": 1,
                        "document_id": "4193eaa727d79b0f74597356dbcbb9a7"
                    },
                    {
                        "collection_id": "af9e1f41-6114-4d77-bca6-c9b99b2601b1",
                        "score": 5.791631414211986,
                        "position": 2,
                        "document_id": "bdcd6a9cc1438a3faa8c925f6a8d9429"
                    }
                ]
            },
            "event_type": "query",
            "session_token": "1_LKczxWGEWx5TJAi1_Qs35yOoa7",
            "created_timestamp": "2018-09-12T05:20:07.469Z"
        }
```

조회 로그를 사용하여 일반 사용자에게 리턴되는 결과 유형을 조사하고 {{site.data.keyword.discoveryshort}}에서 사용 가능한 접근 방식을 통해 결과 품질을 향상시킬 수 있는 방법을 조사할 수 있습니다. 예: 
- 관련성 훈련, [API를 사용하여 결과 관련성 향상](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api) 및 [도구를 사용하여 결과 관련성 향상](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling)
- [조회 연산자](/docs/services/discovery?topic=discovery-query-operators#query-operators)
- [조회 확장](/docs/services/discovery?topic=discovery-query-concepts#query-expansion)
- 사용자 정의 구성, [구성 참조](/docs/services/discovery?topic=discovery-configref#configref)를 참조하십시오.

## 이벤트 로그 작성
{: #eventlogs}

이벤트 로그는 애플리케이션 내에서 사용자의 상호작용을 추적하는 데 사용됩니다. 이를 통해 애플리케이션이 얼마나 잘 수행되는지 이해하고 결과를 향상시키기 위해 중점을 두어야 하는 영역을 식별할 수 있습니다. {{site.data.keyword.discoveryshort}}는 이벤트를 추적하기 위해 애플리케이션에 임베드할 수 있는 API를 제공합니다. 사용자가 조치를 수행할 때 적절한 정보를 사용하여 이 API를 호출하면 {{site.data.keyword.discoveryshort}}로 다시 신호를 전송하며, 이는 로그에서 볼 수 있습니다. 

이벤트는 애플리케이션이 일반 사용자가 관련 정보를 찾는 데 얼마나 유효한지 측정하기 위해 컴퓨팅 메트릭(예: 클릭 비율)에서 정보를 수집하거나 기반이 되는 사실을 빌드하기 위해 조회 및 클릭을 검토하여 훈련 기반을 확보하는 데 도움을 줄 수 있습니다. 

사용자가 결과와 상호작용할 수 있는 어디서든 이 API를 추가할 수 있습니다. 예를 들어 검색 UI에서 사용자가 문서 링크를 클릭할 때 이를 추가할 수 있습니다. 또는 챗봇 인터페이스에서 사용자가 **확장** 또는 **추가 세부사항** 단추를 클릭할 때를 추적하기 위해 사용할 수 있습니다.

{{site.data.keyword.discoveryshort}} 결과는 세션 토큰을 포함하여 이벤트 추적에 사용할 수 있는 추가 정보를 리턴합니다. 

`"matching_results": 179,`
`"session_token": "1_LKczxWGEWx59fYD0_VV8HFUpb6"`

이벤트를 기록하려면 `/api/v1/events` 엔드포인트에 POST를 작성하십시오. 세부사항은 [이벤트 API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/discovery#create-event){: new_window}를 참조하십시오.

이벤트가 기록되면 `/api/v1/logs` 엔드포인트를 사용하여 다시 읽을 수 있습니다. `session_token`을 사용하여 연관된 조회에 이벤트를 결합하십시오.
