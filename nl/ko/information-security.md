---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-26"

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

# 정보 보안
{: #information-security}

IBM은 클라이언트와 파트너에게 혁신적인 데이터 개인정보 보호, 보안 및 통제 솔루션을 제공하기 위해 최선을 다하고 있습니다.
{: shortdesc}

**주의:**
클라이언트는 유럽 연합 GDPR(General Data Protection Regulation)을 포함하여 다양한 법률과 규정을 준수할 책임이 있습니다. 고객은 고객의 비즈니스에 영향을 줄 수 있는 관련 법령 및 규정에 대한 확인과 해석,
그러한 법령 및 규정의 준수를 위해 필요한 고객의 모든 조치와 관련하여 적절한 법률 자문을 받아야 할
단독 책임이 있습니다.

여기에서 설명하는 제품, 서비스 및 기타 기능은 일부 고객의 상황에는 해당되지 않을 수 있으며
그 가용성이 제한될 수 있습니다. IBM은 법률, 회계 또는 감사 관련 자문을 제공하지 않으며, IBM의 서비스나 제품 사용이 고객의 관련 법령이나 규정 준수를 보장한다는 진술이나 보증을 제공하지 않습니다.

작성되는 {{site.data.keyword.cloud}} {{site.data.keyword.watson}} 리소스에 대해 GDPR 지원을 요쳥해야 하는 경우

-   유럽 연합(EU)의 경우 [Requesting support for IBM Cloud Watson resources created in the European Union](/docs/services/watson/getting-started-gdpr-sar.html#request-EU)을 참조하십시오.
-   EU 이외 지역의 경우 [Requesting support for resources outside the European Union](/docs/services/watson/getting-started-gdpr-sar.html#request-non-EU)을 참조하십시오.

## 유럽 연합 GDPR(General Data Protection Regulation)
{: #gdpr}

IBM은 GDPR 준수를 향한 여정에서 클라이언트와 파트너에게 혁신적인 데이터 개인정보 보호, 보안 및 통제 솔루션을 제공하기 위해 최선을 다하고 있습니다.

[[여기 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/gdpr)에서 규제 준수 과정을 지원하는 IBM 고유의 GDPR 준비 과정과 GDPR 기능 및 오퍼링에 대해 자세히 알아보십시오.{: new_window}.

## {{site.data.keyword.discoveryshort}}의 데이터 레이블 지정 및 삭제
{: #gdpr-discovery}

{{site.data.keyword.discoveryshort}} 서비스에는 호출당 데이터의 레이블 지정하는 API가 포함되어 있습니다.

이 API를 사용하여 다음을 수행할 수 있습니다

- 고객 ID로 데이터의 레이블을 지정합니다.
- 관련 주의사항을 포함하여 특정 고객 ID에 대한 모든 데이터를 삭제합니다.

사용자가 선택한 `customer_id`([데이터 레이블 지정 방법](/docs/services/discovery/information-security.html#labeling)의 지시사항 참조)를 선택적 `X-Watson-Metadata` 헤더에 추가하여 데이터 레이블을 지정합니다. 그런 다음 {{site.data.keyword.discoveryshort}}는 `customer_id`로 데이터를 삭제할 수 있습니다.

REST 호출에서는 선택적 `X-Watson-Metadata`를 세미콜론으로 구분된 `field=value` 쌍과 함께 보낼 수 있습니다. 현재 `customer_id`만 유지됩니다. 해당 `customer_id`를 `X-Watson-Metadata` 헤더에 추가하여 요청은 이 `customer_id`에 속한 데이터를 포함하고 있음을 표시합니다.

`customer_id`는 단일 {{site.data.keyword.discoveryshort}} 서비스 인스턴스 내에서 고유합니다. 이는 환경 또는 콜렉션별로 고유하지는 않습니다. 여기에는 개인 데이터가 포함되지 않아야 합니다.

**참고:** 데이터 레이블을 지정하고 데이터를 삭제할 때 예상되는 기능이 보장되지 않으므로 실험 및 베타 기능은 프로덕션 환경에서 사용하기 위한 것이 아닙니다. 데이터 레이블을 지정하고 데이터를 삭제해야 하는 솔루션을 구현할 때는 실험 및 베타 기능을 사용하면 안 됩니다.

## 데이터 레이블 지정을 지원하는 메소드
{: #pi_methods}

연관된 메소드를 사용하여 원래 정보를 추가할 때 `customer_id`를 지정한 경우 `customer_id`를 사용하여 다음 저장된 정보를 삭제할 수 있습니다.

- 조회(`/v1/environments/{environment_id}/collections/{collection_id}/query`) `passages` 또는 `natural_language_query` 매개변수와 함께 사용되는 경우에만 해당됩니다.
- 이벤트(`/v1/events`)
- 문서(`/v1/environments/{environment_id}/collections/{collection_id}/documents`)
- 주의사항(`/v1/environments/{environment_id}/collections/{collection_id}/notices`) 수집 `notices`의 레이블이 지정된 경우에만 해당됩니다.
- Knowledge Graph 엔티티(`/v1/environments/{environment_id}/collections/{collection_id}/query_entities`)
- Knowledge Graph 관계(`/v1/environments/{environment_id}/collections/{collection_id}/query_relations`)
- 훈련 데이터(`/v1/environments/{environment_id}/collections/{collection_id}/training_data`)

다음 저장된 정보는 명시적으로 레이블이 지정되지 않아 `customer_id`를 지정하여 삭제할 수 없습니다. 개인 데이터는 이러한 필드에서 지원되지 않습니다.

다음 저장된 항목의 문자열 필드(`name` 및 `description`을 포함하지만 이에 한하지 않음):
- 구성
- 콜렉션
- 환경

## 데이터 레이블 지정
{: #labeling}

문서를 수집할 때 `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` 또는 `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/ID` 오퍼레이션을 사용하여 `X-Watson-Metadata` 헤더를 포함시키십시오. `customer_id` 필드가 문서의 `extracted_metadata`에 추가됩니다. 오퍼레이션을 수행할 때 `X-Watson-Metadata` 헤더에 `customer_id`를 제공하도록 애플리케이션을 구성해야 합니다.

선택적으로 `X-Watson-Metadata` 헤더를 사용하는 대신 `metadata` 멀티파트 양식 파트와 함께 `customer_id`를 포함시킬 수 있습니다.

**참고:** 문서가 이미 수집된 경우 `X-Watson-Metadata` 헤더 및 `customer_id`를 추가하려면 문서를 다시 수집해야 합니다.

**참고:** 동일한 문서에 대해 `metadata` 멀티파트 양식 파트 및 `X-Watson-Metadata` 헤더에 `customer_id`를 지정한 경우 `X-Watson-Metadata` 헤더의 `customer_id`가 사용됩니다.

제한사항:

- `X-Watson-Metadata` 헤더의 값은 4킬로바이트의 텍스트를 초과할 수 없습니다.
- `X-Watson-Metadata` 헤더에는 세미콜론으로 구분된 `field=value` 쌍 목록이 포함되어야 합니다. `field` 및 `value`에는 세미콜론(`;`) 또는 등호(`=`)가 포함되면 안 됩니다.
- `customer_id`는 각 {{site.data.keyword.discoveryshort}} 인스턴스 내에서 고유합니다. 이는 환경 또는 콜렉션별로 고유하지는 않습니다.
- `customer_id`의 길이는 256자를 넘을 수 없습니다.
- `customer_id`에 공백만 있거나 완전히 비어 있는 경우 `customer_id`가 제공되지 않는 것처럼 처리되고 오류 메시지가 리턴되지 않습니다.

### Discovery 도구를 사용하여 데이터 레이블 지정
{: #labelingtooling}

{{site.data.keyword.discoveryshort}} 도구를 사용하는 경우 `customer_id` 필드를 사용하여 데이터 레이블을 지정할 수 있습니다. ![Cog](images/icon_settings.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->를 클릭하고 **GDPR 데이터 레이블** 필드에 `customer_id`를 입력하십시오. 이 필드를 설정하면 이 브라우저 세션을 사용하여 업로드한 모든 데이터에 대해 `customer_id`를 사용하여 레이블이 지정됩니다. 연관된 고객 ID가 변경되면 이 필드를 수동으로 변경해야 합니다.

**GDPR 데이터 레이블** 필드에 `customer_id`를 추가하면 해당 시점 이후부터 해당 도메인 아래의 각 인스턴스를 포함하여 도메인 내에 있는 문서, 주의사항, Knowledge Graph 엔티티, Knowledge Graph 관계 및 훈련 데이터의 레이블이 지정됩니다. **GDPR 데이터 레이블** 필드를 추가하기 전에 {{site.data.keyword.discoveryshort}} 에서 발생한 조치(문서 업로드 포함)에는 레이블이 지정되지 않습니다.

**참고:** {{site.data.keyword.discoveryshort}} 도구의 **GDPR 데이터 레이블** 필드를 사용하여 `customer_id`를 지정한 후에 도메인, 브라우저를 전환하거나 브라우저 캐시를 비우거나 incognito 세션을 시작하는 경우 `customer_id`는 유지되지 않으며 데이터에 레이블이 지정되지 않습니다. 도메인 또는 브라우저를 전환해야 하는 경우 **GDPR 데이터 레이블** 필드에 `customer_id`를 다시 입력하십시오.

### Data Crawler를 사용하여 문서 레이블 지정
{: #labelingdc}

Data Crawler를 사용하여 문서를 이미 크롤링한 경우 `X-Watson-Metadata` 헤더 및 `customer_id`를 추가하려면 문서를 다시 크롤링해야 합니다.

1. `customer_id`를 포함하도록 {{site.data.keyword.discoveryshort}} Data Crawler 출력 어댑터 구성을 업데이트하십시오. [출력 어댑터 구성](/docs/services/discovery/data-crawler-discovery.html#output-adapter)을 참조하십시오.
1. 크롤링을 스케줄하십시오. 문서는 `X-Watson-Metadata` 헤더를 사용하여 {{site.data.keyword.discoveryshort}}에 제출되고 구성된 `customer_id`로 레이블이 지정됩니다.

## 레이블 지정된 데이터 삭제
{: #deletingdata}

나중에 삭제하려면 데이터가 `customer_id`로 레이블이 지정되어 있어야 합니다.

1. `DELETE /v1/user_data` 오퍼레이션을 사용하고 삭제할 데이터의 `customer_id`를 제공하십시오. `DELETE /v1/user_data`는 [데이터 레이블 지정을 지원하는 메소드](/docs/services/discovery/information-security.html#pi_methods)에서 지정된 대로 서비스 인스턴스 내에서 특별한 `customer_id`와 연관된 모든 데이터를 삭제합니다. [API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html#delete-user-data){: new_window}도 참조하십시오.

삭제는 비동기식으로 수행됩니다. 삭제 진행 상태를 추적할 수 없습니다.

비공존 `customer_id`를 제공하는 경우 아무 것도 삭제되지 않지만 `200 - OK`의 응답이 리턴됩니다.

환경 및 콜렉션을 작성하기 위해 `X-Watson-Metadata` 헤더가 요청에 포함되는 경우에도 환경 및 콜렉션은 `customer_id`로 레이블이 지정되지 않습니다. 콜렉션 내 또는 환경 내의 개별 문서에만 레이블이 지정됩니다. 따라서 데이터를 삭제해도 개별 환경 및 콜렉션은 삭제되지 않습니다.

{{site.data.keyword.discoveryshort}} 도구를 사용하여 레이블 지정된 데이터를 삭제할 수 없습니다.
