---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-25"

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

# 릴리스 정보
{: #release-notes}

릴리스 정보는 이전 릴리스 이후에 발생한 {{site.data.keyword.discoveryfull}} 서비스의 변경사항에 대한 정보를 제공합니다.
{: shortdesc}

## 서비스 API 버전화
{: shortdesc}

API 요청에는 `version=YYYY-MM-DD`의 날짜 형식을 사용하는 버전 매개변수가 필요합니다. 하위 비호환 방식으로 API를 변경할 때마다 API의 새로운 부 버전을 릴리스합니다.

모든 API 요청과 함께 버전 매개변수를 전송합니다. 서비스는 지정한 날짜에 맞는 API 버전을 사용하거나 해당 날짜 이전의 가장 최신 버전을 사용합니다. 현재 날짜로 기본값을 지정하지 마십시오. 대신, 앱과 호환되는 버전과 일치하는 날짜를 지정하고 앱이 이후 버전에 대해 준비될 때까지 변경하지 마십시오.

현재 버전은 `2018-10-15`입니다.

## 베타 기능
{: #beta-features}

IBM은 베타 또는 실험으로 분류되는 서비스, 기능 및 언어 지원을 릴리스할 예정입니다. 이러한 기능은 불안정하고 자주 변경될 수 있으며 충분한 예고 없이 중단될 수 있습니다. 사용자가 해당 기능을 평가할 수 있는 기능이 제공됩니다. 베타 또는 실험 용량은 일반적으로 릴리스된 용량이 제공하는 동일한 레벨의 성능 또는 기능을 제공하지 않을 수 있습니다. 이 용량은 프로덕션 환경에서 사용하도록 설계되지 않았으므로 모든 사용은 사용자의 전적인 책임에 따릅니다.


## 변경사항
{: #change-log}

다음 새 기능 및 서비스에 대한 변경사항이 사용 가능합니다.

## 2018년 10월 25일
{: #25oct}

[요소 분류](/docs/services/discovery/element-classification.html) 인리치먼트에 대한 스키마가 변경되었습니다. 업데이트된 스키마를 사용하려면 `2018-10-15` 이후의 버전 날짜로 API를 사용하여 문서를 수집해야 합니다. {{site.data.keyword.discoveryshort}} 도구에서는 아직 이 API 버전(현재 `2018-08-01` 사용)을 사용하지 않으므로 {{site.data.keyword.discoveryshort}} 도구를 사용하여 수집된 문서는 원래 스키마를 사용하여 강화됩니다.

## 2018년 9월 25일
{: #25sept}

- Continuous Relevancy Training을 릴리스했습니다. 여기서는 사용자의 상호작용을 사용하여 가장 관련성이 높은 결과를 표시하는 방법을 학습합니다. 이는 사용자 행동을 자동으로 학습하여 결과의 관련성 순위를 향상시키는 데 필요한 노력을 크게 줄일 수 있습니다. 세부사항은 [Continuous Relevancy Training](/docs/services/discovery/continuous-training.html#crt)을 참조하십시오.

- 장기간의 조회를 수행하기 위한 API 지원이 추가되었습니다. 이는 문자 한계를 10,000자로 늘리고 조회의 필터 수를 늘리고 더 복잡한 집계를 수행할 수 있도록 합니다. 세부사항은 [API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query){: new_window} 및 [API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#federated-query){: new_window}에서 POST 조회를 참조하십시오.

- 이제 API를 사용하여 고급 플랜을 업그레이드할 수 있습니다. 세부사항은 [플랜 업그레이드](/docs/services/discovery/upgrading.html#advanced)를 참조하십시오. 

- 요소 분류 인리치먼트가 식별되는 분류된 요소, 계약 요소 및 당사자와 테이블을 업데이트했습니다. 업데이트에 대해서는 [요소 분류](https://console.bluemix.net/docs/services/discovery/element-classification.html)를 참조하십시오.

- 브라질 포르투갈어에 대한 전체 지원이 추가되었습니다. 자세한 정보는 [언어 지원](/docs/services/discovery/language-support.html)을 참조하십시오.

- 이제 조회 API(`GET /v1/environments/{environment_id}/collections/{collection_id}/query`)는 특정 결과(예: 최근에 공개된 문서)로 편향될 수 있는 `bias` 매개변수를 지원합니다. 자세한 정보는 API 참조에서 [콜렉션 조회 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query-using-get){: new_window} 방법을 참조하십시오.

- [요소 분류](/docs/services/discovery/element-classification.html#element-collection)에 대한 콜렉션을 강화하기 위해 제공된 **기본 계약 구성** 파일이 HTML 정규화에 문제가 있는 것으로 판명되었습니다. 이 릴리스에는 새로운 **기본 계약 구성**이 포함됩니다. 아래 단계에 따라 새 **기본 계약 구성**을 콜렉션에 적용하십시오.

     1. **기본 계약 구성** 구성 파일 또는 **기본 계약 구성**을 기반으로 하는 사용자 정의 구성을 사용 중인 콜렉션을 판별하십시오.
     1. **기본 계약 구성**을 기반으로 한 사용자 정의 구성에 대한 변경사항을 기록해 두십시오.
     1. 새 구성 파일을 사용하기 전에 환경에서 이전 **기본 계약 구성** 파일을 삭제해야 하므로 API [구성 삭제 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#delete-configuration){: new_window}를 사용하여 콜렉션과 연관된 현재 **기본 계약 구성**을 삭제하십시오. 또한 이전 **기본 계약 구성**을 기반으로 하는 구성을 삭제하십시오.
     1. 이제 새 **기본 계약 구성** 파일을 사용할 수 있습니다. 해당 구성 중 하나를 사용하여 각 콜렉션에 대해 새 콜렉션을 작성하십시오. 새 **기본 계약 구성**을 적용하거나 2단계에서 작성한 메모를 사용하여 새 **기본 계약 구성**을 기반으로 하는 새 사용자 정의 구성을 작성하십시오.
     1. 이전에 수집된 파일을 원래 콜렉션으로 업로드하십시오.
     1. 이전 콜렉션을 삭제하십시오.

## 20118년 8월 15일
{: #15aug}

- 두 개의 새 조회 연산자를 사용할 수 있습니다. `Exists`(`:*`)를 사용하면 지정된 `field`가 있는 모든 결과를 리턴할 수 있습니다. `Does not exist`(`!*`)를 사용하면 지정된 `field`가 없는 모든 결과를 리턴할 수 있습니다. 자세한 정보는 [조회 연산자](/docs/services/discovery/query-operators.html)를 참조하십시오. 

## 20118년 8월 2일
{: #2aug}

- 이제 {{site.data.keyword.discoveryfull}}는 {{site.data.keyword.discoveryshort}} 도구를 사용하여 Box, Salesforce, SharePoint Online에 연결하고 동기화할 때 영어, 스페인어, 독일어, 독일어, 이탈리아어, 포르투갈어, 프랑스어, 아랍어, 한국어 및 일본어 콜렉션을 지원합니다. 

## 2018년 7월 31일
 
 - **2018년 8월 1일**부터 {{site.data.keyword.discoveryfull}}는 새로운 가격 책정 구조를 사용합니다. 이는 보다 단순한 가격 책정 모델(문서 시간은 더 이상 계산의 일부가 아님)이고 {{site.data.keyword.discoverynewsfull}} 조회에 대해 계층화된 가격 책정이라는 특징을 가지고 있습니다. 또한 표준 플랜은 폐기되었으며 라이트 플랜에서는 문서와 {{site.data.keyword.discoverynewsshort}} 조회 한계를 줄였습니다. 현재 {{site.data.keyword.discoverynewsshort}} 사용자는 가격 책정 변경을 위해 어떤 작업도 수행할 필요가 없습니다. 세부사항은 [{{site.data.keyword.discoveryshort}}가격 책정 플랜](/docs/services/discovery/pricing-details.html)을 참조하십시오.
 
**참고:** API의 버전 날짜를 `2018-08-01`로 업데이트했습니다. 새 환경 크기 조정 옵션(`LT`, `XS`, `S`, `MS`, `M`, `ML`, `L`, `XL`, `XXL`, `XXXL`)을 활용하려면 API를 사용하여 환경을 작성할 때 이 버전 날짜를 사용해야 합니다. 이제 환경 크기는 `string` 유형입니다(이전 유형은 `integer`임).

## 2018년 7월 27일

- [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery/watson-discovery-news.html)가 일본어(`collection_id`: `news-ja`)로 추가로 릴리스되었습니다. {{site.data.keyword.discoverynewsfull}}는 영어, 스페인어, 독일어 및 한국어로도 사용할 수 있습니다.

## 2018년 6월 25일

- Salesforce, Microsoft SharePoint Online 및 Box 데이터 소스에 연결하고 동기화하는 옵션을 추가했습니다. 이 데이터 소스는 프리미엄 환경에서 사용할 수 없습니다. 이 데이터 소스에 대한 [소스 인증 정보 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#credentials-api){: new_window} 및 [구성 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#configurations-api){: new_window} API가 릴리스되었습니다. 
  - {{site.data.keyword.discoveryfull}}는 {{site.data.keyword.discoveryshort}} 도구를 사용하여 Box, Salesforce 및 SharePoint Online에 연결하고 동기화할 때 영어 콜렉션만 지원합니다. [해결됨](/docs/services/discovery/release-notes.html#2aug)
  - Box, Salesforce 및 SharePoint Online의 개별 문서 파일 크기 한계는 10MB입니다.
- {{site.data.keyword.discoveryshort}} 도구에 새 성능 대시보드를 추가했습니다. [성능 대시보드에서 메트릭 보기 및 조회 결과 개선](/docs/services/discovery/dashboard.html)을 참조하십시오. 새 대시보드는 프리미엄 또는 전용 환경에서 사용할 수 없습니다.
- 일본어에 대한 전체 지원이 추가되었습니다. 자세한 정보는 [언어 지원](/docs/services/discovery/language-support.html)을 참조하십시오.

## 2018년 6월 22일

- 이벤트 및 피드백 API가 릴리스되었습니다. 자세한 정보는 [API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#events-and-feedback-api){: new_window}를 참조하십시오.

## 2018년 6월 11일

-  워싱턴 DC(미국 동부)에서 호스팅되는 애플리케이션의 경우 이제 서비스는 토큰 기반 IAM(Identity and Access Management) 인증을 지원합니다. IAM은 서비스를 사용한 인증에 서비스 인증 정보가 아닌 액세스 토큰을 사용합니다. 기존 및 새 애플리케이션에 IAM 토큰을 사용하는 방법에 대한 자세한 정보는 [2018년 5월 17일](#17May2018) 릴리스 업데이트를 참조하십시오.
-  이제 추가 계약 요소가 요소 분류 `Safety and Security`에서 지원됩니다. 세부사항은 [계약 요소에 대한 이해](/docs/services/discovery/element-classification.html#contract-elements)를 참조하십시오.

## 2018년 6월 6일

- 이제 {{site.data.keyword.discoverynewsfull}} 조회는 `text` JSON 필드에 각 기사의 처음 50개 단어를 표시합니다.

## 2018년 6월 5일
{: #5jun}

- 이제 요소 분류를 프리미엄 플랜에 등록된 요소에 사용할 수 있습니다.
- `Low` `assurance` 등급은 더 이상 요소 분류에 사용할 수 없습니다.

## 2018년 5월 31일

- 프랑스어에 대한 전체 지원이 추가되었습니다. 자세한 정보는 [언어 지원](/docs/services/discovery/language-support.html)을 참조하십시오.

## 2018년 5월 30일

- {{site.data.keyword.discoverynewsfull}}의 알려진 문제점이 수정되었습니다. 이전에는 {{site.data.keyword.discoverynewsshort}}를 조회할 때 다른 언어로 된 문서가 요청한 언어의 문서와 함께 계수되어 올바르지 않은 문서 수를 받을 수 있었습니다. 이제 더 이상 그렇지 않습니다.
- `2018년 5월 22일` 이후에 작성된 콜렉션부터 {{site.data.keyword.discoveryshort}}는 영어, 독일어, 프랑스어, 네덜란드어, 이탈리아어 및 포르투갈어의 경우에 특수 문자가 포함된 조회 결과를 리턴합니다. 예를 들어 `aqui`를 조회한 경우 `aqui` 및 <code>aqu&iacute;</code> 둘 다에 대한 결과를 받게 됩니다.

## 2018년 5월 21일

- [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery/watson-discovery-news.html)가 독일어(`collection_id`: `news-de`)로 추가로 릴리스되었습니다. {{site.data.keyword.discoverynewsfull}}는 영어, 스페인어 및 한국어로도 사용할 수 있습니다.

## 2018년 5월 17일
{: #17May2018}

- 이제 {{site.data.keyword.discoverynewsfull}} 조회는 `text` JSON 필드에 각 기사의 처음 20개 단어만 표시합니다.

-   이제 서비스는 2018년 5월 15일부터 시드니(**au-syd**)에서 호스팅되는 애플리케이션의 서비스 인스턴스에 대해 새로운 API 인증 프로세스를 지원합니다. 곧 다른 지역에서 호스팅되는 애플리케이션에 대해서도 지원할 예정입니다. {{site.data.keyword.Bluemix}}는 토큰 기반 IAM(Identity and Access Management) 인증으로 마이그레이션하는 프로세스를 사용합니다. IAM은 서비스를 사용한 인증에 서비스 인증 정보가 아닌 액세스 토큰을 사용합니다. 

   시드니 지역에서는 다음에 대한 {{site.data.keyword.discoveryshort}} 서비스에 IAM 액세스 토큰을 사용합니다.

    -   5월 15일 이후에 작성한 *새 서비스 인스턴스*. 자세한 정보는 [IAM 토큰을 사용하여 인증](/docs/services/watson/getting-started-iam.html)을 참조하십시오.
    -   Cloud Foundry에서 RC(Resource Controller)에서 관리하는 리소스 그룹으로 마이그레이션하는 *기존 서비스 인스턴스*. 5월 15일 이전에 작성된 서비스 인스턴스는 마이그레이션할 때까지 인증을 위해 서비스 인증 정보를 계속 사용합니다. 자세한 정보는 [Cloud Foundry 서비스 인스턴스를 리소스 그룹으로 마이그레이션](/docs/resources/instance_migration.html)을 참조하십시오.

    다른 지역의 모든 새 서비스 인스턴스 및 기존 서비스 인스턴스는 계속해서 인증에 서비스 인증 정보(`apikey:{apikey_value}`)를 사용합니다.

### IAM 액세스 토큰을 사용하여 인증

IAM 액세스 토큰을 사용하는 경우 {{site.data.keyword.discoveryshort}} 서비스에 요청을 전송하기 전에 인증을 수행합니다.

1.  IBM Cloud에서 API키를 가져오십시오. 해당 키를 사용하여 IAM 액세스 토큰을 생성하십시오. 자세한 정보는 [{{site.data.keyword.watson}} 서비스 API 키를 사용하여 IAM 토큰을 가져오는 방법](/docs/services/watson/getting-started-iam.html#iamtoken)을 참조하십시오.
1.  `Authorization` 헤더를 사용하여 IAM 액세스 토큰을 {{site.data.keyword.discoveryshort}}에 전달하십시오. 헤더에서 `Authorization: Bearer {access_token}`을 지정하여 액세스 토큰이 `Bearer` 토큰임을 표시하십시오.

    다음은 액세스 토큰을 사용하는 간단한 cURL 예입니다.

    ```bash
    curl -X GET
    --header "Authorization: Bearer eyJhbGciOiJIUz......sgrKIi8hdFs"
    "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    자세한 정보는 [토큰을 사용하여 인증](/docs/services/watson/getting-started-iam.html#use_token)을 참조하십시오.

### IAM 액세스 토큰 새로 고치기

생성한 IAM 액세스 토큰의 구조는 다음과 같습니다. `access_token` 필드의 값을 사용하여 서비스에 인증된 요청을 수행합니다.

```javascript
{
  "access_token": "eyJhbGciOiJIUz......sgrKIi8hdFs",
  "refresh_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353
}
```
{: codeblock}

액세스 토큰은 수명에 제한이 있습니다. `expires_in` 필드는 토큰이 유지되는 기간(이 경우 1시간)을 표시합니다. `expiration` 필드에서는 1970년 1월 1일(UTC/GMT 자정) 이후의 시간(초 수)을 지정하는 UNIC 시간소인으로 토큰의 만기 시간을 표시합니다.

애플리케이션에서 인증된 요청을 작성하는 데 사용하기 전에 액세스 토큰의 만기 시간을 확인하십시오. 만기된 경우 사용하기 전에 액세스 토큰을 새로 고쳐야 합니다. `refresh_token` 필드의 값을 사용하여 액세스 토큰을 새로 고칩니다. 자세한 정보는 [토큰 새로 고치기](/docs/services/watson/getting-started-iam.html#refresh_token)를 참조하십시오.


## 2018년 5월 11일

- 정보 보안에 대한 자세한 정보는 [정보 보안](/docs/services/discovery/information-security.html)을 참조하십시오.
- 다음 {{site.data.keyword.discoveryfull}} Knowledge Graph `query_entities` 알려진 문제점은 `2018-05-04` API 버전 업데이트로 해결되었습니다. 이 수정사항은 `2018-05-04` 이후에 수집되거나 대체된 엔티티에만 적용됩니다. 이전 문서를 다시 수집하거나 해당 엔티티가 포함된 새 문서를 수집하여 엔티티를 대체할 수 있습니다. 이전 엔티티가 대체되지 않는 경우 `query_entities`는 `2018-05-04` API 버전을 사용하여 모든 대문자를 리턴합니다.
  - 모든 엔티티 이름은 이전에 `query_entities`에서 카멜 케이스로 변환되었습니다. 예를 들어 엔티티 이름 "IBM Corporation"는 "Ibm Corporation"으로 변환되었습니다. 이제 더 이상 그렇지 않습니다.

## 2018년 5월 9일

- 이제 샘플 문서는 브라우저의 로컬 로밍 데이터 폴더에 로컬에 저장됩니다. 샘플 문서에 대한 자세한 정보는 [샘플 문서 업로드](/docs/services/discovery/building.html#uploading-sample-documents)를 참조하십시오.

## 2018년 5월 4일

- 이제 요소 분류: 속성 및 통제에서 두 개의 추가 계약 요소가 지원됩니다. 세부사항은 [계약 요소에 대한 이해](/docs/services/discovery/element-classification.html#contract-elements)를 참조하십시오.

## 2018년 4월 26일

- 다음 수집 문제가 해결되었습니다. 사후 인리치먼트 `json_normalizations` 및/또는 `normalizations`가 지정된 경우 정규화가 잘못된 순서로 적용되는 경우가 있었습니다. 이로 인해 예기치 않은 필드 값으로 문서가 인덱싱될 수 있습니다. 이제 더 이상 그렇지 않습니다.
- 이제 샘플 문서의 최대 파일 크기는 1MB입니다. 이전에는 최대 파일 크기가 5MB였습니다.

## 2018년 4월 12일

- Knowledge Graph: 이제 [증거](/docs/services/discovery/building-kg.html#evidence) 및 [정규화 및 필터링](/docs/services/discovery/building-kg.html#canonicalization)을 모든 콜렉션에서 사용할 수 있습니다. `03-05-2018` 이전에 작성된 모든 콜렉션에서 이러한 기능을 사용하려면 문서를 다시 수집해야 합니다. 이전에는 새 콜렉션을 작성하고 문서를 재수집헀어야 합니다.

## 2018년 4월 11일

- 이제 요소 분류: `Asset Use` 및 `Communication`에서 두 개의 추가 카네고리가 지원됩니다. 세부사항은 [계약 요소에 대한 이해](/docs/services/discovery/element-classification.html#contract-elements)를 참조하십시오.

## 2018년 4월 2일

- 이제 샘플 문서는 1개월이 아니라 24시간 후에 자동으로 삭제됩니다.

## 2018년 3월 16일

- 독일어에 대한 전체 지원이 추가되었습니다. 자세한 정보는 [언어 지원](/docs/services/discovery/language-support.html)을 참조하십시오.

{{site.data.keyword.discoveryshort}} 도구:
- PDF의 요소에서 파티, 속성(nature) 및 카테고리를 추출하는 데 사용할 수 있는 **기본 계약 구성**이라는 이름의 새 구성이 추가되었습니다. 세부사항은 [요소 분류](/docs/services/discovery/element-classification.html#element-collection)를 참조하십시오. 

일반 가용성으로 업데이트됨:
- 문서 세그먼트화가 베타 상태에서 GA 상태로 이동되었습니다. 세그먼트화 한계가 250개의 세그먼트로 증가했습니다. 이제 더 이상 문서당 50개의 세그먼트로 제한되지 않습니다. 세부사항은 [문서 세그먼트화](/docs/services/discovery/building.html#doc-segmentation)를 참조하십시오. 

알려진 문제점:
- 와일드카드는 대문자가 포함된 조회에 작동되지 않습니다. 예를 들어, 제공된 키/필드 쌍 `{"borrower": "GOVERNMENT OF INDIA"}`, `query-borrower:*ndia`가 결과를 리턴하지만 `query-borrower:*NDIA`는 결과를 리턴하지 않습니다. 

## 2018년 3월 8일
{: #8mar}

- 베타 버전의 {{site.data.keyword.discoveryfull}} Knowledge Graph에서 몇 가지 기능을 추가했습니다. 베타 릴리스 중에 [Knowledge Graph](/docs/services/discovery/building-kg.html) 기능 및 이와 연관된 메소드는 **고급** 플랜, **프리미엄** 플랜 및 모든 **전용** 환경에 등록된 서비스 인스턴스에 대해서만 사용 가능합니다. 새 기능은 다음과 같습니다.
  - [엔티티 유사성](/docs/services/discovery/building-kg.html#similarity)
  - [증거](/docs/services/discovery/building-kg.html#evidence)
  - [정규화 및 필터링](/docs/services/discovery/building-kg.html#canonicalization)

## 2018년 3월 7일

- 다음 수집에 대해 알려진 문제가 해결되었습니다. 2월 28일과 3월 6일 사이에 작은 비율의 문서가 `id` 및 `extracted_metadata` 필드만 사용하여 인덱싱되었습니다(기타 문서 컨텐츠는 인덱싱되지 않음). 근본적인 문제점은 해결되었지만 수집에 영향을 받는 모든 문서를 다시 제출해야 합니다. 영향을 받는 문서를 간단하게 식별할 수 있는 방법이 없습니다.

## 2018년 3월 5일
{: #5mar}

- 다음 {{site.data.keyword.discoveryfull}} Knowledge Graph 알려진 문제점이 `2018-03-05` API 버전 업데이트로 해결되었습니다. 이 수정사항은 `2018-03-05` 버전 날짜를 사용하는 새로 작성된 콜렉션에만 적용됩니다.  
  - 모든 엔티티 유형 이름 및 관계 유형 이름이 수집 중에 대문자로 변환되었습니다. 예를 들어, "GeoPoliticalEntity" 엔티티는 "GEOPOLITICALENTITY"로 변환되고 "partOf" 관계는 "PARTOF"로 변환되었습니다. 이제 더 이상 그렇지 않습니다.

## 2018년 3월 1일

- [조회 확장](/docs/services/discovery/using.html#query-expansion) 한계가 5,000개의 조회 확장 및 총 25,000개의 용어에 대해 증가되었습니다. 세부사항은 [Discovery 가격 책정 플랜](/docs/services/discovery/pricing-details.html)을 참조하십시오. 

## 2018년 2월 28일

- {{site.data.keyword.alchemylanguageshort}} 인리치먼트는 **2018년 3월 1일**부터 더 이상 사용되지 않았습니다. {{site.data.keyword.alchemylanguageshort}} 인리치먼트를 활용하는 기존 콜렉션 및 구성 파일의 마이그레이션에 대한 정보는 [{{site.data.keyword.nlushort}}으로 인리치먼트 마이그레이션](/docs/services/discovery/migrate-nlu.html)을 참조하십시오.

## 2018년 2월 23일

- 문서 유사성으로 조회할 수 있는 기능이 추가되었습니다. 문서 ID로 유사 문서를 조회할 수 있으며 선택적으로 필드를 지정하여 유사성을 추가로 세분화할 수 있습니다. 자세한 정보는 [문서 유사성](/docs/services/discovery/using.html#doc-similarity)을 참조하십시오.

- 조회 결과의 [`highlight` 매개변수](/docs/services/discovery/query-parameters.html#highlight)가 개선되었습니다. 조회 결과는 `score`로 정렬된 완전한 문장을 리턴합니다.

## 2018년 2월 21일
{: #21feb}

- 이전에 PDF 문서를 수집할 때 `extracted_metadata` 오브젝트에서 그리고 문서 세부사항 API에서 수집 참고사항을 조회하는 경우 리턴되는 `file_type`은 `html`이었습니다. 이제 더 이상 그렇지 않습니다. 이제 리턴되는 `file_type`은 `pdf`입니다. 

## 2018년 1월 26일
{: #26jan}

{{site.data.keyword.discoveryshort}} 도구:

- 도구에서 [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery/watson-discovery-news.html) 타일에 대한 한국어 및 스페인어 콜렉션에 액세스하는 기능이 추가되었습니다. 이전에는 이러한 콜렉션을 API를 통해서만 조회할 수 있었습니다.

## 2018년 1월 23일

- 조회 범위를 확장하는 기능이 추가되었습니다. 예를 들어, "car"에 대한 조회를 "automobile" 및 "motor vehicle"을 포함하도록 확장할 수 있습니다. 또한 일반적으로 잘못된 용어를 대체할 수 있습니다. 예를 들어, "seabizcuit"에 대한 조회를 "seabiscuit"에 대한 조회로 대체할 수 있습니다. 조회 확장은 {{site.data.keyword.discoveryshort}} API를 사용하여 구현됩니다. 세부사항은 [조회 확장](/docs/services/discovery/using.html#query-expansion)을 참조하십시오.  

## 2018년 1월 15일

- {{site.data.keyword.discoverynewsfull}} Original은 서비스에서 더 이상 사용되지 않습니다. 이는 2017년 7월 31일에 새 버전 {{site.data.keyword.discoverynewsfull}}로 대체되었습니다. {{site.data.keyword.discoverynewsfull}} Original에서 새 버전으로 마이그레이션하는 데 대한 지시사항은 [Watson Discovery News Original에서 마이그레이션](/docs/services/discovery/migrate-bwdn.html)을 참조하십시오.

## 2018년 1월 11일

- 한국어에 대한 전체 지원이 추가되었습니다. 자세한 정보는 [언어 지원](/docs/services/discovery/language-support.html)을 참조하십시오.

## 2017년 12월 15일

- 중요한 카테고리 및 유형을 분류하기 위해 운영 문서의 요소(문장, 목록, 테이블)를 구문 분석하는 **요소 분류** 인리치먼트를 릴리스했습니다. 자세한 정보는 [요소 분류](/docs/services/discovery/element-classification.html)를 참조하십시오. 요소 분류는 **프리미엄** 플랜에 등록된 서비스 인스턴스에는 사용할 수 없습니다. [해결됨](/docs/services/discovery/release-notes.html#5jun)
- 중국어 및 네덜란드어에 대한 기본 언어 지원이 추가되었습니다. 자세한 정보는 [언어 지원](/docs/services/discovery/language-support.html)을 참조하십시오. 현재 중국어 및 네덜란드어 콜렉션은 API로 작성되어야 합니다.
- Data Crawler를 위해 새 매개변수인 `proxy_host_port` 및 `read-timeout`을 추가했습니다. 자세한 사항은 [Data Crawler 구성](/docs/services/discovery/data-crawler-discovery.html)을 참조하십시오.
- PDF 문서를 수집할 때 다음 문제점이 발생할 수 있습니다. [해결됨](/docs/services/discovery/release-notes.html#21feb)
  - 수집 알림이 조회되는 경우 PDF 문서에 대한 `file_type` 필드가 `html`로 리턴됩니다.
  - PDF 문서에 대한 결과의 `extracted_metadata` 오브젝트에서 `file_type` 필드가 `html`로 설정됩니다.
  - 문서 세부사항 API는 PDF 문서에 대한 `file_type` 필드를 `html`로도 리턴합니다.
- JSON을 수집하는 경우 혼합 유형 배열은 지원되지 않습니다.  

{{site.data.keyword.discoveryshort}} 도구:

- {{site.data.keyword.discoveryfull}} Knowledge Graph의 베타 버전용 시각적 조회 빌더를 추가했습니다. [{{site.data.keyword.discoveryshort}} 도구를 사용하여 Knowledge Graph 조회](/docs/services/discovery/building-kg.html#querying-kg)를 참조하십시오.

## 2017년 11월 30일

- 문서 전반의 엔티티 및 관계를 조회하기 위해 새 엔드포인트를 제공하는 {{site.data.keyword.discoveryfull}} Knowledge Graph의 베타 버전을 릴리스했습니다. 여기에는 컨텍스트 기반 검색 및 관련성 순위 지정이 포함됩니다. 이 베타 기능은 **고급** 플랜 사용자만 사용할 수 있습니다. **Dedicated** 환경에서는 사용할 수 없습니다. [해결됨](/docs/services/discovery/release-notes.html#8mar) 자세한 정보는 [{{site.data.keyword.discoveryfull}} Knowledge Graph](/docs/services/discovery/building-kg.html)를 참조하십시오. 베타 기능을 설명하는 발표문은 [여기](/docs/services/discovery/release-notes.html#beta-features)에 있습니다.
  - {{site.data.keyword.discoveryfull}} Knowledge Graph의 알려진 문제점: 모든 엔티티 유형 이름 및 관계 유형 이름이 수집 중에 대문자로 변환됩니다. 예를 들어, "GeoPoliticalEntity" 엔티티는 "GEOPOLITICALENTITY"로 변환되고 "partOf" 관계는 "PARTOF"로 변환됩니다. [해결됨](/docs/services/discovery/release-notes.html#5mar)
- 한국어(`collection_id`: `news-ko`) 및 스페인어(`collection_id`: `news-es`)의 두 가지 추가 언어로  [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery/watson-discovery-news.html)를 릴리스했습니다. {{site.data.keyword.discoverynewsfull}} 한국어 및 스페인어는 API를 통해서만 사용 가능합니다. API를 통한 콜렉션 조회에 대한 정보는 [API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")][Resolved](/docs/services/discovery/release-notes.html#26jan)(https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection)를 참조하십시오.{: new_window}. {{site.data.keyword.discoverynewsfull}} 영어에서는 이제 `collection_id`가 `news-en`으로 표시됩니다. 이전에는 `collection_id`가 `news`였습니다. 이전 `collection_id`를 사용하고 있는 경우 계속해서 작동됩니다. 그러나 새 프로젝트의 경우 새 `collection_id`로 전환하려고 할 수 있습니다.
- 조회 결과는 조회 결과 간의 상대 관련성을 표시하는 `score` 값을 리턴합니다. 2017년 11월 30일부터 `score`가 계산되는 방식이 변경되었습니다. `score` 값은 검색 또는 세션 전반이 아닌 단일 검색에서 문서의 순위를 지정하기 위해서만 사용되어야 합니다. 훈련된 콜렉션이 있는 경우 `score` 값은 자연어 조회의 결과에 리턴됩니다. `score`가 조회 결과 간의 상대 관련성을 표시하기 때문에 임계값으로 사용되지 않아야 합니다. 대신, 임계값을 설정하려면 훈련된 모델과 비교하여 결과의 관련성을 표시하는 `confidence`를 사용하십시오. 임계값 설정에 대한 자세한 정보는 [신뢰도 스코어](/docs/services/discovery/train-tooling.html#confidence)를 참조하십시오.
- 이 릴리스로 시작하여 단락 검색은 문장 경계를 발견합니다. 문장을 시작할 때 시작하고 끝날 때 중지하는 단락을 리턴하려고 합니다. 이전에 많은 단락이 문장 중간 쯤에서 시작하거나 중지했습니다. 단락 검색에 대한 자세한 정보는 [단락](/docs/services/discovery/query-parameters.html#passages)을 참조하십시오.

## 2017년 11월 15일
{: #15nov}

{{site.data.keyword.discoveryshort}} 도구:

- {{site.data.keyword.knowledgestudiofull}}로 작성된 사용자 정의 관계 모델을 통합하는 옵션이 포함된 [관계 추출](/docs/services/discovery/building.html#relation-extraction) 인리치먼트를 추가했습니다.
- [엔티티 추출](/docs/services/discovery/building.html#entity-extraction) 인리치먼트 {{site.data.keyword.discoveryshort}} 도구는 이제 {{site.data.keyword.knowledgestudiofull}}로 작성된 사용자 정의 엔티티 모델을 통합하는 옵션을 포함합니다.
- 일본어 콜렉션을 작성하는 옵션은 {{site.data.keyword.discoveryshort}} 도구에서 제거되었습니다. 그러나 {{site.data.keyword.discoveryshort}} API를 사용하여 일본어 콜렉션을 작성하기 위한 옵션은 계속 남아 있습니다.
- {{site.data.keyword.discoveryshort}} 도구는 이제 신디케이트된 환경을 지원합니다.

## 2017년 11월 10일

{{site.data.keyword.discoveryshort}} 도구:

- 단락 검색을 위한 추가 옵션을 {{site.data.keyword.discoveryshort}} 도구에 추가했습니다. 조회할 때 이제 리턴할 단락, 리턴할 단락의 수 및 각 단락의 최대 문자 수에 대한 필드를 지정할 수 있습니다. 제한사항, 최소값 및 최대값에 대한 정보는 [단락](/docs/services/discovery/query-parameters.html#passages)을 참조하십시오.

## 2017년 11월 8일
{: #8nov}

모든 API 호출에 대한 버전 문자열이 `2017-11-07`에서 `2017-10-16`으로 변경되었습니다. 이 버전은 다음과 같습니다.
- 각 조회 결과의 `score`를 `result_metadata`라고 하는 새 오브젝트로 이동했습니다. 
- 콜렉션 조회가 훈련되었고 조회가 자연어 조회인 경우 `result_metadata`에 해당 결과에 대한 신뢰도 스코어를 표시하는 `confidence` 필드가 포함됩니다. 자세한 사항은 [신뢰도 스코어](/docs/services/discovery/train-tooling.html#confidence)를 참조하십시오.
- 공백을 포함하는 필드(예: `body.additional reading`)가 수집 중에 필터링됩니다. `notices` 설명에는 `The field 'additional reading' is invalid: whitespace, '.', '#' and ',' are invalid in a field name`이 표시됩니다.
- `result_metadata` 필드는 수집 중에 필터링됩니다.

## 2017년 10월 16일

- 모든 API 호출에 대한 버전 문자열이 `2017-10-16`에서 `2017-09-01`로 변경되었습니다. 이 버전에서 새 문서를 {{site.data.keyword.alchemylanguageshort}} 인리치먼트로 강화된 기존 콜렉션에 업로드하고 새 콜렉션을 작성하고 새 콜렉션을 {{site.data.keyword.alchemylanguageshort}} 인리치먼트로 강화하기 위한 지원은 더 이상 사용되지 않습니다. {{site.data.keyword.alchemylanguageshort}}로 강화된 기존 콜렉션은 가능한 빨리 {{site.data.keyword.nlushort}} 인리치먼트로 마이그레이션되어야 합니다. 자세한 사항은 [{{site.data.keyword.nlushort}}으로 인리치먼트 마이그레이션](/docs/services/discovery/migrate-nlu.html#migrating-enrichments-to-natural-language-understanding)을 참조하십시오. 또한 {{site.data.keyword.discoveryshort}} 도구는 `2017-10-16` 버전도 사용합니다. 자세한 정보는 다음을 참조하십시오.

{{site.data.keyword.discoveryshort}} 도구:

- {{site.data.keyword.discoveryshort}} 도구는 `2017-10-16` API 버전 문자열을 사용합니다. 그러므로 도구를 사용하고 있는 경우 `2017-10-16` 이후에 더 이상 기존 {{site.data.keyword.alchemylanguageshort}} 콜렉션에 문서를 업로드하거나 {{site.data.keyword.alchemylanguageshort}} 인리치먼트로 강화된 새 콜렉션을 작성할 수 없습니다.  콜렉션을 강화하기 위해 {{site.data.keyword.discoveryshort}} 도구를 계속 사용하려면 먼저 콜렉션을 {{site.data.keyword.nlushort}}으로 마이그레이션하십시오. 자세한 사항은 [{{site.data.keyword.nlushort}}으로 인리치먼트 마이그레이션](/docs/services/discovery/migrate-nlu.html#migrating-enrichments-to-natural-language-understanding)을 참조하십시오.
- **데이터 스키마 탐색기**에서 {{site.data.keyword.discoverynewsfull}} 콜렉션의 여러 인리치먼트에 대한 샘플 조회가 표시됩니다. 이제 {{site.data.keyword.discoverynewsfull}}에서 해당 인리치먼트에 대한 추가 예제 값을 표시하는 **추가 값 표시** 링크도 포함됩니다.
- **데이터 관리** 화면의 콜렉션 통계, 오류 및 경고, 데이터 통찰의 결합을 포함하여 다수의 생산성 개선사항이 있습니다.
- 문서가 처리를 완료할 때 경보를 표시하는 메시지가 추가되었습니다.

## 2017년 10월 9일

- API에서 새 집계 메트릭 `unique_count`를 사용할 수 있습니다. 콜렉션에서 지정된 필드의 고유 인스턴스 수를 리턴합니다. 자세한 정보는 [unique_count](/docs/services/discovery/query-aggregations.html#unique_count)를 참조하십시오.

{{site.data.keyword.discoveryshort}} 도구:

- 이제 히스토그램 및 시분할 집계가 **시각적 조회 빌더**에서 지원됩니다. 또한 시분할 조회에 대한 이상 항목 발견을 설정하는 옵션도 있습니다.
- **데이터 스키마 탐색기**에서 선택된 인리치먼트에 대한 샘플 조회가 표시됩니다. 이제 해당 인리치먼트에 대한 추가 예제 값을 표시하는 **추가 값 표시" 링크도 포함됩니다.
- **데이터 관리**, **데이터 스키마 보기** 및 **조회 빌드** 화면을 좀 더 빠르게 탐색할 수 있도록 하는 햄버거 메뉴가 추가되었습니다.

### 2017년 10월 3일

- 이제 문서 세그먼트화를 사용할 수 있습니다. [문서 세그먼트화로 문서 분할](/docs/services/discovery/building.html#doc-segmentation)을 참조하십시오.

### 2017년 11월 29일

- {{site.data.keyword.discoveryshort}}는 2017년 9월 29일 `Germany` 지역에서 출시되었습니다. EU 데이터 규정을 준수하기 위해 이 지역에서 AlchemyLanguage 인리치먼트는 지원되지 않습니다.
- 알려진 문제점: 조회 필드에 공백을 사용할 수 없습니다.  {{site.data.keyword.discoveryshort}}에서 조회를 작성하는 경우 조회 필드에 공백이 포함되면(예: `body.additional reading`) `400: Invalid query syntax error`가 수신됩니다. [해결됨](/docs/services/discovery/release-notes.html#8nov)

### 2017년 11월 25일

- 이제 프리미엄 가격 책정 플랜을 사용할 수 있습니다. 자세한 정보는 [{{site.data.keyword.discoveryshort}} 가격 책정 플랜](/docs/services/discovery/pricing-details.html)을 참고하십시오.
- 같은 환경에서 콜렉션 전반의 조회, 목록 필드 및 조회 알림에 대한 기능이 추가되었습니다. 자세한 정보는 [다중 콜렉션 조회](/docs/services/discovery/using.html#multiple-collections)를 참조하십시오.
- {{site.data.keyword.discoveryshort}}에 대한 언어 지원 정보는 [언어 지원](/docs/services/discovery/language-support.html)에서 사용 가능합니다.

{{site.data.keyword.discoveryshort}} 도구:
- 시각작 조회 빌더가 베타 상태에서 GA 상태로 이동되었습니다. 현재 필터, 시분할 및 히스토그램 집계는 시각적 조회 빌더에서 지원되지 않습니다. **결과의 분석 포함**을 클릭한 후 **조회 빌더** 화면에서 **조회 언어로 편집**을 클릭하여 해당 집계를 작성하십시오.
- {{site.data.keyword.discoverynewsfull}} 조회에서 중복 제거할 수 있는 베타 기능을 추가했습니다.
- 영어, 독일어, 스페인어 콜렉션 외에도, 이제 아랍어, 프랑스어, 이탈리아어, 한국어, 일본어 및 브라질 포르투갈어 콜렉션을 작성할 수 있습니다.
- 알려진 문제점: {{site.data.keyword.discoveryshort}} 도구는 신디케이트된 환경을 지원하지 않습니다. [해결됨](/docs/services/discovery/release-notes.html#15nov)

### 2017년 9월 14일

{{site.data.keyword.discoveryshort}} 도구:

- 변환된 문서에 필드 및 값을 표시하는 데이터 스키마 탐색기를 추가했습니다. 이 정보는 Discovery 조회 언어를 사용하여 조회를 빌드하기 전에 콜렉션의 데이터 구조를 이해하는 데 사용될 수 있습니다. 두 가지 방법 즉, 문서(문서 보기) 또는 필드(필드 보기)로 데이터 스키마를 볼 수 있습니다. 데이터 스키마 탐색기에 액세스하려면 **내 데이터 통찰** 화면에서 **데이터 스키마 보기** 단추를 클릭하거나 왼쪽의 **데이터 스키마 보기** 아이콘을 클릭하십시오.

### 2017년 9월 6일

- 조회에서 리턴된 문서에서 중복을 제거할 수 있는 베타 기능을 추가했습니다. 이 베타 기능은 개인용 및 Watson Discovery News 콜렉션 모두에 적용됩니다. 자세한 정보는 [조회 결과에서 중복 문서 제외](/docs/services/discovery/query-parameters.html#deduplication)를 참조하십시오.

현재 문서 중복 제거는 베타 기능으로만 지원됩니다. 자세한 정보는 이 문서의 맨 위에 있는 베타에 대한 설명문을 참조하십시오.

### 2017년 8월 31일

- 모든 API 호출에 대한 버전 문자열이 `2017-08-01`에서 `2017-09-01`로 변경되었습니다. 이 버전에는 올바른 JSON 필드만 수집되도록 미리보기 및 수집 중에 다음 올바르지 않은 JSON 필드를 필터링하는 업데이트가 포함됩니다. 충돌 및 발생 가능한 오류를 방지하려면 버전 문자열을 `2017-09-01`로 업데이트하십시오.

   - 최상위 레벨의 `id`, `score` 및 `highlight`(`add a document` 기능으로 문서 ID를 사용하여 문서를 콜렉션에 계속 추가할 수 있습니다.). 자세한 정보는 [API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#add-doc){: new_window}를 참조하십시오.
   - 최상위 레벨에서 `_` 접두부가 사용된 필드 이름(결과적으로 ID로 문서를 조회할 때 `_id` 대신 `id`에 대해 조회할 수 있습니다.)
   - 필드 이름의 `#` 및 `,`
   - `+` 및 `-` 접두부가 사용된 필드 이름
   - `"` `"` 필드 이름에 비어 있는 값

**참고:** JSON 문서에 필드 이름에 이러한 문자 또는 최상위 레벨에 `id`, `score` 및 `highlight`가 포함된 경우 콜렉션에 문서를 추가하기 전에 이들을 제거해야 합니다. 그렇지 않으면 이러한 필드는 비어 있는 상태가 됩니다. 문서를 콜렉션에 추가하기 전에 사용자 정의 구성을 작성하고 JSON을 정규화하여 이 문제점을 방지할 수 있습니다. [사용자 정의 구성](/docs/services/discovery/building.html#custom-configuration)을 참조하십시오.  또한 파일 이름에 `?`, `:` 또는 `#`과 같은 문장 부호 문자를 포함하는 문서로 인해 수집 시 오류가 발생할 수 있습니다. 수집 전에 이러한 문자를 포함하는 문서의 이름을 바꾸십시오.

- `natural_language_query`에 대한 검색 메소드가 관련된 시맨틱으로 단어를 일치시켜 결과의 관련성을 향상시키도록 업데이트되었습니다. 이 업데이트는 관련성 훈련이 포함된 콜렉션에만 적용됩니다. `natural_language_query`를 사용하고 있으나 관련성 교육을 수행하지 않은 경우 리턴된 결과의 순서에서 향상을 볼 수 있습니다.

{{site.data.keyword.discoveryshort}} 도구:

- 조회 빌더로 변경하면 조회, 필터 및 집계에서뿐만 아니라 Discovery 조회 언어 및 자연어 조회 옵션 간을 좀 더 쉽게 전환할 수 있습니다.


### 2017년 8월 25일

- `passages` 배열에는 이제 `field`, `start_offset` 및 `end _offset`이 포함됩니다. `field`는 단락이 추출된 필드의 이름입니다. `start_offset`은 필드 내 단락 텍스트의 시작 문자입니다. `end_offset`은 필드 내 단락 텍스트의 종료 문자입니다.

{{site.data.keyword.discoveryshort}} 도구:
이 조회 빌드 개선사항은 **조회 빌드** 화면에서 볼 수 있습니다.

-  시각적 빌더를 사용하여 {{site.data.keyword.discoveryshort}} 조회 언어로 조회를 작성할 수 있는 베타 기능을 추가했습니다. **문서 검색** 및 **조회하는 문서 제한** 섹션에서 **시각적 모드로 빌드**를 클릭하여 이를 수행하십시오.  조회를 시각적으로 빌드할 때 조회는 **{{site.data.keyword.discoveryshort}} 조회 언어** 아래에 표시됩니다.

   현재 시각적 조회 빌더는 베타 기능으로만 지원됩니다. 자세한 정보는 이 문서의 맨 위에 있는 베타에 대한 설명문을 참조하십시오.

### 2017년 8월 18일

{{site.data.keyword.discoveryshort}} 도구:

- [2017년 8월 11일](/docs/services/discovery/release-notes.html#11aug)에 도입된 베타 시각적 집계 빌더에 중첩된 집계 및 조건에 대한 지원을 추가했습니다. 조건은 집계 행당 세 개로 제한됩니다.

   현재 시각적 집계 빌더는 베타 기능으로만 지원됩니다. 자세한 정보는 이 문서의 맨 위에 있는 베타에 대한 설명문을 참조하십시오.

### 2017년 8월 11일
{: #11aug}

{{site.data.keyword.discoveryshort}} 도구:

두 기능은 조회 빌드 개선사항이고 **조회 빌드** 화면에 표시될 수 있습니다.

- 사전 빌드된 샘플 조회 및 집계의 세트에서 조회를 선택할 수 있는 옵션을 추가했습니다. 오른쪽 맨 위에 있는 **샘플 조회 사용**을 클릭하여 목록에 액세스하십시오. 개인용 데이터 콜렉션을 조회하는 경우 샘플은 콜렉션에 있는 `top entities`, `categories` 등을 사용합니다. 이 조회는 고유한 조회를 작성하기 위한 시작점으로 사용될 수 있습니다. 샘플 조회는 {{site.data.keyword.discoverynewsfull}} 및 개인용 콜렉션 모두에 사용할 수 있습니다.

-  시각적 빌더를 사용하여 집계를 작성할 수 있는 베타 기능을 추가했습니다. **{{site.data.keyword.discoveryshort}} 조회 언어를 사용하여 집계 조회 작성** 필드 위에 있는 **시각적 모드로 빌드**를 클릭하여 이를 수행하십시오.  집계를 시각적으로 빌드할 때 조회는 **{{site.data.keyword.discoveryshort}} 조회 언어** 아래에 표시됩니다.  

   현재 시각적 집계 빌더는 베타 기능으로만 지원됩니다. 자세한 정보는 이 문서의 맨 위에 있는 베타에 대한 설명문을 참조하십시오.

### 2017년 7월 31일

- {{site.data.keyword.discoverynewsfull}}의 새 버전이 릴리스되었습니다. 원래 버전은 {{site.data.keyword.discoverynewsfull}} Original로 이름이 변경되었으며 **2018년 1월 15일**(서비스일)부터 삭제되어 사용이 중지되었습니다. 마이그레이션 지시사항은 [Watson Discovery News Original에서 마이그레이션](/docs/services/discovery/migrate-bwdn.html)을 참조하십시오. **참고:** {{site.data.keyword.discoveryshort}}의 새 인스턴스를 작성한 경우 {{site.data.keyword.discoverynewsfull}}의 새 버전에 대한 액세스 권한만 제공됩니다.

- {{site.data.keyword.discoveryfull}}의 새 가격 책정 플랜이 릴리스되었습니다. 자세한 사항은 [{{site.data.keyword.discoveryshort}} 가격 책정 플랜](/docs/services/discovery/pricing-details.html)을 참조하십시오.

- 모든 API 호출에 대한 버전 문자열이 `2017-07-19`에서 `2017-08-01`로 변경되었습니다. 이 버전에는 새 가격 책정 플랜의 업데이트와 Watson Discovery News의 새 버전이 포함됩니다. 버전 문자열을 업데이트하여 충돌 및 발생 가능한 오류를 방지하십시오.

### 2017년 7월 19일

 - 2017년 8월 1일에 발표한 가격 책정 변경사항의 일부로 현재 더 이상 사용되지 않는 **30일 무료 평가판** 플랜을 사용 중인 사용자는 **라이트** 플랜으로 자동 마이그레이션됩니다. 이 전이의 결과로 기존 사용자는 _(2000)_의 문서, _(200Mb)_의 스토리지 또는 _(2)_의 콜렉션 수로 제한된 라이트 플랜 제한사항을 충족했거나 초과했습니다. **라이트** 플랜의 제한사항을 초과한 경우 추가 컨텐츠를 서비스에 추가할 수 없으나 콜렉션을 계속 조회할 수 있습니다. {{site.data.keyword.discoveryshort}} 도구 및 API를 사용하여 모든 제한사항의 현재 상태를 볼 수 있습니다. {{site.data.keyword.discoveryshort}} 인스턴스에 컨텐츠 추가를 재개하려면 다음 중 하나를 수행해야 합니다.
   - **라이트** 플랜의 제한사항이 초과되지 않도록 콜렉션 및/또는 문서를 제거하십시오.
     문서는 [delete-doc](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-doc) 메소드를 사용하여 API를 통해 개별적으로 삭제될 수 있고, 콜렉션은 [delete-collection](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-collection) 메소드를 사용하여 도구 또는 API를 통해 삭제될 수 있습니다.
   - 스토리지 요구사항을 충족하는 레벨로 플랜을 업그레이드하십시오.
 - **`1`**, **`2`** 또는 **`3`**개의 환경을 갖춘 고객은 **고급** 플랜으로 자동 마이그레이션됩니다.

### 2017년 7월 17일

 - 다음 기능이 베타 상태에서 GA 상태로 이동되었습니다.

   - 관련성 훈련
   - 자연어 조회
   - 강조표시

 - 이 릴리스부터 {{site.data.keyword.discoveryfull}}는 {{site.data.keyword.alchemylanguageshort}}에서 {{site.data.keyword.nlushort}}으로 인리치먼트 메커니즘을 변경합니다. {{site.data.keyword.alchemylanguageshort}}가 더 이상 사용되지 않고 있으므로 가능한 빨리 {{site.data.keyword.nlushort}} 사용을 시작해야 합니다.  자세한 사항은 [{{site.data.keyword.alchemylanguageshort}} 인리치먼트에서 {{site.data.keyword.nlushort}} 환경으로 마이그레이션](/docs/services/discovery/migrate-nlu.html)을 참조하십시오.
   **참고:** Watson Knowledge Studio와 통합할 때 {{site.data.keyword.alchemylanguageshort}} 인리치먼트 구성을 계속 사용해야 합니다. 자세한 사항은 [{{site.data.keyword.knowledgestudiofull}}와 통합](/docs/services/discovery/integrate-wks.html)을 참조하십시오.

 - 모든 API 호출에 대한 버전 문자열이 `2017-06-25`에서 `2017-07-19`로 변경되었습니다. 이 버전에서는 콜렉션 작성 시 NLU 기본 구성을 사용합니다. 사용자는 이전 버전의 {{site.data.keyword.alchemylanguageshort}}로 계속 강화할 수 있어야 합니다.

    {{site.data.keyword.nlushort}}을 사용하도록 기본 구성이 업데이트되었습니다. 충돌 및 발생 가능한 오류를 방지하려면 가능할 빨리 버전 문자열을 업데이트해야 합니다.

 - Discovery 도구:

    {{site.data.keyword.alchemylanguageshort}} 인리치먼트로 강화된 콜렉션에 대한 Insight Cards는 더 이상 자동으로 업데이트되지 않습니다. Insight Cards를 업데이트하려면 콜렉션을 {{site.data.keyword.nlushort}} 인리치먼트로 마이그레이션해야 합니다.

    **2017년 7월 18일** 이전에 콜렉션을 작성했고 **기본 구성**을 적용했던 경우 해당 콜렉션이 {{site.data.keyword.alchemylanguageshort}} 인리치먼트로 강화되었습니다. 이 날짜 이후에 **기본 구성**을 콜렉션에 적용한 경우 {{site.data.keyword.nlushort}} 인리치먼트가 사용됩니다(구성 이름이 도구에서 **NLU를 사용한 기본 구성**으로 전환됨). {{site.data.keyword.alchemylanguageshort}} 인리치먼트는 더 이상 사용되지 않으므로 새 콜렉션에 이를 사용하면 안 됩니다.

### 2017년 6월 30일
{: #30jun}

 -  2017년 5월 5일에 베타 기능으로 도입된 엔티티 정규화 기능이 GA 상태로 이동되었습니다. 자세한 사항은 [엔티티를 정규화하기 위해 사용자 정의 구성 작성](/docs/services/discovery/normalize-entities.html)을 참조하십시오.

### 2017년 6월 23일

 - 모든 API 호출에 대한 버전 문자열이 `2016-12-01`에서 `2017-06-25`로 변경되었습니다. 새 버전 문자열은 독일어(`de`) 또는 스페인어(`es`)로 된 인리치먼트를 사용합니다(콜렉션의 언어가 이러한 언어 중 하나로 설정되는 경우). 이전에는 모든 인리치먼트가 콜렉션의 언어 설정에 관계 없이 영어로 수행되었습니다.

    영어 이외의 언어로 인리치먼트를 사용하지 않는 경우 `2016-12-01` 버전 문자열을 계속 사용할 수 있습니다. 그러나 발생 가능한 이후의 충돌을 방지하려면 가능할 빨리 버전 문자열을 업데이트해야 합니다.

 - 이제 이상 항목 발견은 GA 기능으로서 `timeslice` 집계의 일부로 사용할 수 있습니다. 자세한 사항은 [시분할 이상 항목 발견](/docs/services/discovery/query-aggregations.html#anomaly-detection)을 참조하십시오.

 - Discovery 도구:

   - Discovery 도구(관련성 도구)를 사용하여 조회 결과의 관련성을 향상시킬 수 있는 베타 기능을 추가했습니다. [Discovery 도구로 조회 결과의 관련성 향상](/docs/services/discovery/train-tooling.html)을 참조하십시오.

### 2017년 6월 19일

  - Discovery 도구:

    - 새 콜렉션에서 문서의 언어를 영어, 독일어 또는 스페인어로 지정하는 옵션을 추가했습니다. 이 옵션을 사용하려면 **새 콜렉션 이름 지정** 대화 상자에서 **문서의 언어 선택**을 선택하십시오.

    - **조회 빌드** 화면에 **요약** 탭을 추가했습니다. **요약** 탭에는 기존 **JSON** 탭에 제공된 전체 조회 결과의 개요가 표시됩니다. **요약** 표시는 조회 및 인리치먼트에 따라 달라집니다. 표시될 수 있는 정보에는 문서 이름 또는 ID, 집계 통계, 관련성의 순서로 된 문서 단락 및 인리치먼트별 결과가 포함됩니다.

    - **조회 빌드** 화면에 자연어 조회 옵션을 추가했습니다. 이 옵션을 사용하려면 **문서 검색** 섹션에서 **일반 언어로 질문**을 클릭하십시오. 그러면 필드에 질문을 입력할수 있는 위치가 표시됩니다. 이제 **Discovery 조회 언어 사용** 단추를 클릭하여 원래의 조회 필드(이전에는 **조회 또는 키워드 입력**이라고 함)에 액세스할 수 있습니다.

    - **조회 빌드** 화면이 다시 설계되었으나 모든 필드 및 옵션은 그대로 유지됩니다. 다음은 필드의 이전 이름 및 새 이름입니다.

|**이전 필드 이름 **                                           |**새 필드 또는 섹션 이름**                                                                                             |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
|조회 작성 및 실행                                    |문서 검색                                                                                                  |
|조회 결과 좁히기(필터)                       |조회하는 문서 제한                                                                                       |
|조회 결과 그룹화(집계)                        |결과의 분석 포함                                                                                      |
|표시할 필드                                        |이름이 변경되지 않았으나 새 **사용자 정의 표시 옵션** 섹션으로 이동했습니다.                                      |
|리턴할 문서의 수(계산)                    |리턴할 문서의 수[이 필드는 **사용자 정의 표시 옵션** 섹션으로 이동했습니다.]                    |
|일치하는 단락 포함                                |관련성 단락 포함[이 필드는 **사용자 정의 표시 옵션** 섹션으로 이동했습니다.]                        |
|시작 시 건너뛸 조회 필드의 수(오프셋) |시작 시 건너뛸 조회 결과의 수[이 필드는 **사용자 정의 표시 옵션** 섹션으로 이동했습니다.] |

### 2017년 6월 5일

 - 이제 Watson Discovery News 조회는 `text` 및 `alchemyapi_text` JSON 필드에 각 기사의 처음 150개의 단어만 표시합니다. `blekko.snippet` 필드는 스니펫 배열의 첫 번째 문장만 표시합니다.

### 2017년 5월 30일
{: #30may}

 - 조회 API의 `passages` 매개변수가 베타에서 GA 상태로 이동되었습니다.

### 2017년 5월 25일

 - Discovery 도구: 이 릴리스에서 조회 필드 강조표시가 추가되었습니다. 이 기능은 결과 분할창의 JSON으로 된 필드 이름에 노란색 강조표시를 추가합니다. 필드의 컨텐츠가 조회와 일치하지 않는 경우에도 조회되거나 필터링된 모든 필드가 각 결과에 대해 강조표시됩니다. 집계에 사용된 모든 필드도 조회 결과에 강조표시되지만 첫 번째 집계 오퍼레이션만 강조표시됩니다.

### 2017년 5월 10일

 - 이제 `query` 및 `notices` 메소드는 `highlight` 매개변수를 지원합니다. 매개변수는 부울입니다. 조회를 실행하고 `true`로 `highlight`를 지정한 경우 서비스는 조회와 일치하는 단어가 `*`(강조) 태그로 랩핑된 새 `highlight` 필드를 포함한 출력을 리턴합니다. 자세한 사항은 [조회 매개변수](/docs/services/discovery/query-parameters.html#highlight)를 참조하십시오.

 - 서비스 인스턴스당 하나의 환경만 허용되기 때문에 환경의 삭제가 부분적으로만 완료되어서 새 환경을 작성할 수 없습니다. 환경을 삭제한 후 작성하려고 했으나 오퍼레이션이 `pending` 상태인 경우 이 문제점이 발생할 가능성이 큽니다. 이를 해결하려면 삭제 오퍼레이션을 다시 실행하여 완료한 후 새 환경을 작성하십시오.

### 2017년 5월 8일

 - 감정 분석(`docEmotion`) 인리치먼트의 정밀도를 향상시키기 위해 감정적 어조 스코어 모델을 업데이트했습니다. 훈련 데이터세트가 확장되고 기능 엔지니어링이 변경된 결과 모델이 벤치마크 데이터세트에서 더 높은 정밀도를 갖게 됩니다.

### 2017년 5월 5일

 - 이제 Watson Knowledge Studio로 생성된 사용자 정의 모델을 사용하는 Discovery 서비스와 함께 엔티티 정규화를 사용할 수 있습니다. 엔티티 정규화는 다른 참조를 위해 정규화된(기본) 이름을 소스 문서의 동일한 사용자 또는 오브젝트에 삽입합니다. 자세한 사항은 [엔티티를 정규화하기 위해 사용자 정의 구성 작성](/docs/services/discovery/normalize-entities.html)을 참조하십시오.

     **참고:** 현재 엔티티 정규화는 베타 기능으로만 지원됩니다. 자세한 정보는 이 문서의 맨 위에 있는 베타에 대한 설명문을 참조하십시오. [해결됨](/docs/services/discovery/release-notes.html#30jun)

{{site.data.keyword.discoveryshort}} 도구:

 - 도구 오류 로그는 더 이상 최대 8페이지의 결과로 제한되지 않습니다. 문서 이름을 사용할 수 없는 경우 오류 로그에는 문서 ID가 계속해서 표시됩니다.

 - 구성 이름은 50자로 제한되며 `[a-zA-Z0-9-_]` 문자로 구성되어야 합니다. 

 - 이전에 API를 통해서만 사용 가능했던 `passages` 매개변수는 이제 도구 및 API를 통해 사용할 수 있습니다.

### 2017년 4월 25일

  - 이제 이 서비스를 통해 *훈련 데이터*를 제공하여 조회 결과의 정확성을 향상시킬 수 있습니다. 훈련 데이터로 Discovery 인스턴스를 제공하는 경우 서비스는 고급 Watson 알고리즘을 사용하여 가장 관련성이 높은 결과를 판별합니다. 더 많은 훈련 데이터를 추가할수록 리턴하는 결과로 서비스 인스턴스가 좀 더 정확해지고 정교해집니다. 자세한 정보는 [조회 결과의 관련성 향상](/docs/services/discovery/train.html) 및 [API 참조 ](http://www.ibm.com/watson/developercloud/discovery/api/v1/#training-data)를 참조하십시오.

  - 이제 API는 베타 릴리스로 `natural_language_query` 매개변수를 지원합니다. 이 매개변수를 통해 Discovery 서비스의 조회 언어 대신 자연어로 조회를 지정할 수 있습니다. 자세한 정보는 API 참조의 [콜렉션 조회](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query-using-get) 메소드를 참조하십시오.

  - 문서 업데이트 및 오자 정정이 있습니다.

### 2017년 4월 14일

개선사항이 조회 API(`GET /v1/environments/{environment_id}/collections/{collection_id}/query`)에 추가되었습니다. 자세한 정보는 API 참조의 [콜렉션 조회](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query-using-get) 메소드를 참조하십시오.

  - 이제 조회 API는 `passages` 매개변수를 지원합니다. 매개변수가 `true`로 설정되면 조회는 콜렉션의 문서에서 가장 관련성이 높은 단락의 세트를 리턴합니다. 단락은 조회로 리턴되는 모든 문서에서 최상의 텍스트 단락을 판별하기 위해 정교화된 Watson 알고리즘으로 생성됩니다. 이를 통해 보다 정확하게 정보 및 컨텍스트를 찾을 수 있습니다. 자세한 정보는 API 참조의 [콜렉션 조회](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query-using-get) 메소드를 참조하십시오.

    - 조회에서 `passages=true`를 지정하면 단락을 추출하기 위해 늘어난 처리의 결과로 인해 성능이 저하됩니다. 대형 환경에서 성능 영향이 감소될 수 있습니다.

    - `passages` 매개변수는 개인용 콜렉션에만 지원됩니다. 이는 Watson Discovery News 콜렉션에서 지원되지 않습니다.

    - 현재 `passages` 매개변수는 최대 10개의 결과를 리턴합니다. 리턴된 결과의 수는 변경될 수 없습니다. [업데이트](/docs/services/discovery/query-parameters.html#passages_count)

    - `passages` 매개변수는 콜렉션의 제공된 문서에서 최대 세 개의 단락을 리턴합니다. 문서에 세 개 이상의 추가 관련 단락이 포함되면 매개변수는 이를 리턴하지 않습니다.

### 2017년 4월 7일

- 이제 조회 API(`GET /v1/environments/{environment_id}/collections/{collection_id}/query`)는 문서에 있는 정렬할 필드의 목록(쉼표로 구분됨)을 지정할 수 있는 `sort` 매개변수를 지원합니다. 자세한 정보는 API 참조에서 [콜렉션 조회 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query-using-get){: new_window} 방법을 참조하십시오.
- 이제 조회 집계를 위한 `timeslice` 매개변수가 UNIX epoch 형식으로 된 날짜를 올바르게 처리합니다. 집계 및 `timeslice` 매개변수에 대한 정보는 [조회 참조](/docs/services/discovery/query-reference.html#aggregations)를 참조하십시오.
- 오류 메시지에 대한 개선사항입니다.
- 서비스의 Java SDK에 대한 업데이트입니다. 자세한 사항은 [API 참조](http://www.ibm.com/watson/developercloud/discovery/api/v1/?java)를 참조하십시오.
- 이제 조회에서 와일드카드 사용에 대한 다음 제한사항이 수정되었으며 올바르게 작동합니다.

  - 제공된 조회에서 하나의 와일드카드만 작동됩니다. 예를 들어, `query-month:*ctober`가 작동되었으나 `query-month:*ctobe*`에서 구문 분석 오류를 생성했습니다.
  - 와일드카드는 대문자가 포함된 조회에 작동되지 않습니다. 예를 들어, 제공된 키/필드 쌍 `{"borrower": "GOVERNMENT OF INDIA"}`, `query-borrower:*ndia`가 결과를 리턴했으나 `query-borrower:*NDIA`는 결과를 리턴하지 않았습니다.

**참고:** 조회의 구문 분석 내에서 와일드카드는 필요하지 않습니다. 예를 들어, 제공된 키/필드 쌍 `{"borrower": "GOVERNMENT OF TIMOR"}`, `query-borrower:"GOVERNMENT OF TIMOR"`가 결과를 리턴하지만 `query-borrower:"GOVERNMENT OF TI*OR"`는 결과를 리턴하지 않습니다. 구문의 큰따옴표 (`"`) 내 모든 문서가 이스케이프되었으므로 구문 내 와일드카드 사용은 적용되지 않습니다.

### 2017년 3월 24일

- Discovery 도구의 "내 데이터 통찰" 화면에 필터링을 추가했습니다.

### 2017년 3월 15일

다음 알려진 문제점이 수정되었습니다.

-  HTML, PDF 및 Word 문서에서 수집된 모든 필드가 **문자열**로 입력되었습니다. JSON 필드 및 계산된 필드(예: 감성 스코어)가 정의된 대로 입력됩니다. [업데이트](/docs/services/discovery/adding-content.html#adding-content-with-the-api-or-tooling)
- 현재 `preview` 오퍼레이션은 제출된 JSON 문서 내에서 중첩된 JSON 배열을 확인하지 않습니다. 서비스는 현재 중첩된 JSON 배열을 지원하지 않으므로 중첩된 배열이 포함된 문서는 `preview` 오퍼레이션을 전달하지만 수집 시 실패합니다. [JSON 배열을 업로드할 수 있습니까?](/docs/services/discovery/troubleshooting.html#array)를 참조하십시오.
- `unsupported text language` 메시지가 포함된 수집 오류가 발생하면 다음 예제에 표시된 대로 `"language": "english"` 인리치먼트로 구성을 업데이트하여 모든 텍스트가 영어로 해석되도록 강제 실행하십시오. 
[업데이트](/docs/services/discovery/migrate-nlu.html)
```json
"enrichments": [
   {
     "enrichment": "alchemy_language",
     "source_field": "author.label",
     "options": {
       "extract": "taxonomy,entity,relation,doc-emotion,doc-sentiment,concept,keyword",
       "sentiment": true,
       "quotations": true,
       "language": "english"
     }
   }
 ]
```
{: codeblock}

다음 버그가 수정되었습니다.

- 서비스의 성능 및 안정성이 향상되었습니다.

### 2017년 3월 8일

 - 전체 성능을 향상시키기 위해 새 제한시간 추가를 포함하여 백엔드를 최적화했습니다.
 - 실제 상태와 상관 없이 `pending`의 상태를 보고하기 위해 비어 있는(`0` 크기) 환경 상태의 원인인 버그를 해결했습니다.
 - 현재 {{site.data.keyword.discoveryshort}}에서 지원되는 자국어는 미국 영어(`en_US`) 뿐입니다. [업데이트](/docs/services/discovery/language-support.html)

### 2017년 3월 8일

- Discovery 도구에 "내 데이터 통찰" 화면을 추가했습니다.

### 2017년 2월 26일

-     {{site.data.keyword.discoverynewsshort}} 환경의 성능이 향상되었습니다.
-  {{site.data.keyword.discoverynewsshort}} 서비스는 한 번에 50개의 결과만 리턴합니다. 임시 해결책으로, 조회에 `offset` 매개변수를 사용하여 결과에서 페이지를 이동하십시오.
-  다음 명령을 사용하여 개별 문서가 포함된 새 구성을 제출할 수 있습니다.

```bash
curl -X POST -u apikey:{apikey_value} -F "file=@wikipedia-sample.html" -F "configuration=$(cat config.json)" "https://gateway.watsonplatform.net/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2016-12-01"
```
{: pre}
-  서비스의 PDF 및 Word 변환기는 중간 단계로 HTML을 작성합니다. 서비스는 정규화된 JSON에 대한 최종 변환 전에 중계 HTML에서 추가 변환 및 정규화를 적용할 수 있습니다.

다음 버그가 수정되었습니다.

-  오류 코드가 개선되었습니다.
-  여러 문서 오자를 정정했습니다.

### 2017년 2월 26일

-  이제 CSS 선택기를 사용하여 인리치먼트를 적용할 필드를 선택할 수 있습니다. 자세한 정보는 [CSS 선택기를 사용하여 필드 추출](/docs/services/discovery/building.html#using-css)을 참조하십시오.
-  이제 새 `size: X` 매개변수를 [update-environment 메소드](http://www.ibm.com/watson/developercloud/discovery/api/v1/#update_environment)로 전달하여 환경의 크기를 늘릴 수 있습니다. 여기서, `X`의 범위는 0 - 3(정수)입니다. 환경 크기 및 속성에 대한 정보는 [create-environment 메소드](http://www.ibm.com/watson/developercloud/discovery/api/v1/#create_environment)를 참조하십시오. [업데이트](/docs/services/discovery/pricing-details.html)

    **참고:** 기존 환경의 크기를 줄일 수 없습니다. 환경의 크기를 줄이려면 {{site.data.keyword.IBM}} 지원 센터에 문의하여 도움을 받으십시오.

-  새 조회 연산자를 사용할 수 있습니다. `::!` 연산자가 단항 not-equals 연산자로 추가되었습니다. 예를 들어, `query=field::!value`(같지 않음)를 실행할 수 있습니다. 이전에는 not-contains 연산자로 사용할 수 있는 유일한 제외 연산자는 `:!`였습니다(예: `query=field:!value`).

다음 버그가 수정되었습니다.

-  보안 업데이트가 적용되었습니다.
-  검색 경보에 대한 상태 메시지가 개선되었습니다.

### 2017년 2월 1일

다음 정보는 특히 Data Crawler 1.3.0 릴리스에 적용됩니다.
[업데이트](/docs/services/discovery/data-crawler.html)

-   Data Crawler는 문서를 업로드하는 데 사용된 `document_id` 값과 업로드의 상태를 기록합니다. 변환 알림은 로그 외부에서 지속되지 않습니다. 현재 데이터와 상호 작용하는 도구가 없으나 이러한 도구는 시간이 지나면 개발될 것으로 예상됩니다. 원격 DBMS를 사용하도록 구성될 수 있는 H2 데이터베이스를 통해 데이터에 액세스할 수 있습니다.

### 2017년 1월 16일

다음 정보는 특히 Data Crawler 1.2.5 릴리스에 적용됩니다.
[업데이트](/docs/services/discovery/data-crawler.html)

-  Data Crawler는 선택적으로 파일 업로드 후 문서 상태에 대해 즉각적으로 폴링할 수 있습니다. 이 검사는 "문서 업로드"에 대한 크롤러 개념의 일부이므로, 이 검사가 사용되면 사실상 {{site.data.keyword.discoveryshort}} 서비스가 사용자를 위해 동시에 처리할 수 있는 문서보다 더 많은 문서를 크롤러가 동시에 업로드할 수 없습니다.

    `check_for_completion` 기능의 부작용은 문서 실패 시 문서가 실패한 이유를 사용자에게 알릴 수도 있다는 것입니다. 모든 알림은 업로드에 성공한 문서에 첨부되지만 프로세스에 실패하면 크롤러 로그에 표시됩니다. 알림을 처리 가능한 파일에 내보내지 않지만 IBM은 이에 대한 기능 제안을 환영합니다.

### 2017년 1월 5일

다음 정보는 2016년 12월 15일의 GA 릴리스 후 식별된 문제점에 대해 설명합니다.

[업데이트: API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}

-   `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` 또는
    `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]` 호출을 사용하여 문서를 추가하는 경우 호출은 문서 ID 및 **처리 중** 상태를 리턴합니다. `GET /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]` 호출을 사용하여 문서를 조회하는 경우 수집이 완료될 때까지 상태는 **처리 중**으로 유지되고, 수집이 완료될 때 상태가 **사용 가능**으로 변경됩니다.

    `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]` 호출을 사용하여 기존 문서를 **업데이트**하는 경우 서비스가 업데이트된 문서를 완전히 처리하지 않아도 해당 **GET** 호출은 `available` 상태를 리턴합니다. `available` 상태는 원래 문서 또는 업데이트된 문서를 참조할 수 있습니다. 업데이트 오퍼레이션이 오류를 리턴하지 않으면 현재 업데이트된 문서의 상태를 판별할 수 있는 방법이 없습니다.

        업데이트된 컨텐츠 조회를 시도하기 전에 문서 업데이트 제출 후 최대 10분 동안 기다리면 이를 해결할 수 있습니다.

### GA(General Availability) 릴리스, 2016년 12월 15일

다음 정보는 {{site.data.keyword.discoveryfull}} 서비스의 GA(General Availability)에 적용됩니다.

#### 일반 정보
[업데이트: 컨텐츠 추가](/docs/services/discovery/adding-content.html)

현재 API 버전에 대해서는 [API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}를 참조하십시오.

[업데이트: {{site.data.keyword.knowledgestudiofull}}와 통합](/docs/services/discovery/integrate-wks.html).

-   현재 필드의 데이터 유형을 지정할 수 없습니다. 모든 필드가 텍스트(데이터 유형 **문자열**)로 인덱싱됩니다. 
-   API를 사용하여 서비스와 작업하려는 경우 각 호출로 API 버전을 지정할 수 있습니다. 현재 API 버전은 **2016-12-01**입니다. 

    **참고:** 특정 버전은 GA 릴리스에 적용되지 않지만 이후 릴리스와 호환되도록 계속 나열되어야 합니다.

-   {{site.data.keyword.knowledgestudiofull}}를 사용하여 작성된 사용자 정의 모델로 서비스를 사용할 수 있습니다. 수집된 문서를 보강하는 데 사용자 정의 모델을 사용할 수 있습니다. API를 사용하여 사용자 정의 모델을 {{site.data.keyword.discoveryshort}} 서비스와 통합해야 합니다. 도구를 사용하여 통합을 수행할 수 없습니다.

#### 데이터 관리
[업데이트](/docs/services/discovery/pricing-details.html)

-   검색 인덱스가 암호화되지 않습니다.
-   사용자가 백업 및 복원 기능을 제어할 수 없습니다.

#### 환경
[업데이트](/docs/services/discovery/pricing-details.html)

-   고유한 데이터를 업로드하는 데 서비스 인스턴스당 하나의 환경만 작성할 수 있습니다.
-   {{site.data.keyword.discoveryshort}} 서비스는 하나의 가용성 영역에 위치합니다(미국 남부).
-   현재 Dedicated 및 프리미엄 플랜을 사용할 수 없습니다.

#### 환경 크기 조정
[업데이트](/docs/services/discovery/pricing-details.html)

-   새 환경을 작성하는 경우에만 환경 크기를 선택할 수 있습니다. 현재 사용자는 환경의 크기를 조정하는 기능을 사용할 수 없습니다.
-   추가 RAM을 사용하여 환경 크기를 선택하면 성능이 향상됩니다.
-   특정 유스 케이스에 사용할 수 있는 규정 크기 조정 권장사항이 있습니다.
-   {{site.data.keyword.knowledgestudiofull}} 모델에 대한 사용자 정의 크기 조정은 자체 서비스가 아닙니다. 자세한 정보는 {{site.data.keyword.IBM}} 담당자에게 문의하십시오.

#### 수집 제한사항
[업데이트](/docs/services/discovery/pricing-details.html)

-   현재 수집 비율은 100개의 동시 문서 수집 오퍼레이션으로 제한됩니다. 수집을 위해 서비스에 문서를 제출하는 애플리케이션은 HTTP 429 오류를 수용하고 이에 따라 수집 요청의 속도를 줄여야 합니다.
-   {{site.data.keyword.alchemylanguageshort}} 인리치먼트는 필드당 처음 50KB으로 제한됩니다.
-   {{site.data.keyword.knowledgestudiofull}} 사용자 정의 모델의 인리치먼트는 제한되지 않지만 10KB 청크로 문서를 분할합니다. 관계가 청크 경계 전반에 어노테이션되지 않습니다.

#### 조회 제한사항
[업데이트](/docs/services/discovery/using.html#query-concepts)

-   과도한 조회 로드로 검색 인덱스 처리가 자동으로 다시 시작될 수 있습니다.
-   조회를 실행하는 애플리케이션은 동시 조회의 수에 대한 적절한 제한을 적용해야 합니다.

### 알려진 문제
[업데이트: API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}

[업데이트: 도구](/docs/services/discovery/getting-started-tool.html)

[업데이트: Data Crawler](/docs/services/discovery/data-crawler.html)

[업데이트: 인리치먼트](/docs/services/discovery/building.html#adding-enrichments)

[업데이트: 컨텐츠 추가](/docs/services/discovery/adding-content.html)

-   도구를 사용하여 문서를 삭제할 수 없습니다. 문서를 삭제해야 하는 경우 API 참조에 설명된 대로 API의 [문서 삭제](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-doc) 메소드를 사용해야 합니다.

-   현재 API는 문서 수집 중에 생성되는 알림(경고 및 오류)의 목록 가져오기를 지원하지 않습니다. 그러므로 도구는 수집 알림의 목록을 표시할 수 없으며 삽입하는 데 실패한 Data Crawler로 크롤링된 문서를 판별할 수 있는 쉬운 방법은 없습니다(해당 경우). 
-   문서 상태 정보가 항상 정확하지는 않습니다.
    -   수집 오퍼레이션이 10초의 구성된 제한시간보다 더 오래 걸리는 경우 서비스는 수집 오퍼레이션이 완료될 때까지 문서가 서비스에 알려져 있지 않다고 보고 합니다. 오퍼레이션이 완료되면 문서 상태는 사용 가능하며 정확합니다.
    -   인덱싱되었으나 오류를 생성한 문서는 문서가 인덱스에 완전히 커미트될 때까지 짧은 시간 동안 **실패** 상태가 됩니다. 문서가 인덱스에 커미트되면 나열된 상태는 정확합니다.
-   도구를 사용하여 특정 문서를 대체할 수 없습니다. 사용자가 이를 수행하려고 하는 경우 두 번째 문서는 개별 문서로 업로드됩니다. API를 사용하고 있으며 대체할 문서의 ID를 알고 있는 경우 이를 수행할 수 있습니다. API 참조의 [문서 업데이트](http://www.ibm.com/watson/developercloud/discovery/api/v1/#update-doc)를 참조하십시오. Data Crawler를 사용하고 있는 경우 이전 문서와 동일한 URL에서 업데이트된 문서를 업로드하면 원래의 문서가 대체됩니다.
-   사용자의 구성에서 도구를 사용하여 인리치먼트를 편집하는 경우 추출에 사용되는 인리치먼트만 편집할 수 있습니다. 다른 문서(예: {{site.data.keyword.knowledgestudiofull}} 모델의 사용자 정의 인리치먼트)를 추가하거나 편집하려는 경우 API를 사용해야 합니다. 자세한 정보는 API 참조의 [구성 업데이트](http://www.ibm.com/watson/developercloud/discovery/api/v1/#replace_configuration) 메소드를 참조하십시오.
-   다음 정보는 특히 Data Crawler에 적용됩니다. 
    -   Data Crawler에 업로드 실패가 발생하는 경우 Data Crawler는 업로드를 재시도합니다.
    -   Data Crawler는 업로드했지만 변환하거나 인덱싱하는데 실패한 문서를 재시도할 수 없습니다.
    -   Data Crawler에는 다운스트림을 확인하는 기능이 없으며 Data Crawler는 다운스트림에 실패한 URL을 다시 로드하려고 합니다.
    -   Data Crawler로 수집된 문서를 판별할 수 있는 쉬운 방법은 없습니다. 예를 들어, 500개의 문서에 대해 Data Crawler를 실행하는 경우 Data Crawler는 총 212개의 콜렉션 문서와 65개의 문서 제출 실패를 보고할 수 있습니다. 나머지 223개의 문서의 상태는 판별되지 않습니다.

        임시 해결책은 사용할 수 있으나 복잡하고 API 직접 호출이 포함됩니다. {{site.data.keyword.IBM}} 지원 센터에 문의하여 도움을 받으십시오.
-   {{site.data.keyword.discoveryshort}}용 Java, Python 및 Node.js SDK는 기본 REST(cURL) API로 제공된 모든 기능을 제공하지 않습니다. 모든 cURL 메소드는 비cURL SDK의 동일한 메소드를 보유하고 있 않으며 모든 비cURL 메소드는 cURL 동일한 메소드가 보유한 같은 모든 기능을 제공하지 않습니다. 즉, Java, Pytho 및 Node.js SDK는 현재 cURL API 기능의 서브세트만 제공합니다.
-   Word 변환기를 사용하는 경우 `style` 키를 사용하여 표제에 일치시키는 것은 `level` 키를 사용하여 수행하는 것보다 좀 더 정확하고 효율적입니다.
