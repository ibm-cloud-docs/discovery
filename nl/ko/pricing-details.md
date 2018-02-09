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

# Discovery 가격 책정 플랜

{{site.data.keyword.discoveryfull}} 서비스는 사용자의 요구에 맞게 서로 다른 레벨의 리소스와 기능을 제공하는 세 가지 플랜을 제공합니다.
{: shortdesc}

**개인용 데이터 유스 케이스**에서는 다음 제한사항 및 가격을 표시합니다. 

| 라이트                   |  표준             | 고급              | 프리미엄          |
|--------------------------|-------------------|-------------------|-------------------|
| 매월 최대 2,000개의 동시 문서\*   |매월 최대 100,000개의 동시 문서\*   <br/> 매월 $10로 1,000개의 동시 문서($0.0139USD/1000Doc/Hr)\*\*\*<br/> 매월 2,000개의 무료 문서\*\*\*\*  | **예약된 환경**</br>$1,000/매월 기본 비용<br/> 매월 최대 1,000,000개의 문서\*<br/> 매월 $5로 1,000개의 동시 문서($0.00694 USD/1000Doc/Hr)\*\*\*<br/> 매월 100,000개의 문서 포함\*\*\*\*</br> 대형 환경의 경우 [IBM 담당자에게 문의하기 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/marketing/iwm/dre/signup?source=MAIL-watson){: new_window}를 참조하십시오.| **프리미엄 플랜**은 더 나은 격리 및 보안을 위해 하나 이상의 Watson 서비스의 단일 테넌트 인스턴스를 개발자와 조직에게 제공합니다. 이러한 플랜은 전이 중 및 휴지 중에 엔드-투-엔드 암호화된 데이터를 제공할 뿐만 아니라 기존 공유 플랫폼에서 컴퓨팅 레벨 격리를 제공합니다. 자세한 정보를 확인하거나 프리미엄 플랜을 구입하려는 경우 [IBM 담당자에게 문의하기 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://ibm.biz/contact-wdc-premium){: new_window}를 참조하십시오. |
| 200MB\*\*                  |10GB\*\*  | 80GB\*\* |-|
| 최대 2개의 콜렉션      |최대 4개의 콜렉션 | 최대 100개의 콜렉션|-|
| 최대 1개의 {{site.data.keyword.knowledgestudiofull}} 사용자 정의 모델     |최대 1개의 {{site.data.keyword.knowledgestudioshort}} 사용자 정의 모델     | 무제한 {{site.data.keyword.knowledgestudioshort}} 사용자 정의 모델<br/>1개의 {{site.data.keyword.knowledgestudioshort}} 사용자 정의 모델 포함 <br/>매월 {{site.data.keyword.knowledgestudioshort}} 모델당 추가 $800|-|

**참고:** 모든 플랜에서 처음 1,000건의 {{site.data.keyword.discoverynewsshort}} 조회가 무료입니다. {{site.data.keyword.discoverynewsshort}} 조회는 처음 1000건 이후에는 조회당 $0.10이 부과됩니다. 

**참고:** 라이트 플랜 서비스는 30일의 비활성 기간 후 삭제됩니다. 라이트 플랜에서는 조직당 1개의 환경이 무료로 할당됩니다. 

 \* 문서 제한은 디스크의 평균 문서 크기가 100KB라고 간주합니다. 이는 변환 및 인리치먼트를 수행한 후의 콜렉션의 문서 크기이므로 크기는 원래의 출력에서 크게 변경될 수 있습니다. `environments` 또는 `collections` API를 사용하거나 도구를 사용하여 저장된 문서 수와 사용된 총 스토리지 크기를 볼 수 있습니다. 

 \*\* 디스크에서 문서가 평균적으로 100KB보다 큰 경우 최대 문서 한계 전에 플랜의 스토리지 한계에 도달하게 됩니다. 

 \*\*\* 가격은 1,000개 문서의 일괄처리가 서비스에 저장되는 시간을 기반으로 합니다(Thousand Document-Hour라고 함). 가격 책정 계산기의 경우 `number of documents * number of hours those documents are stored in a month / 1000`의 수를 입력해야 합니다.

 \*\*\*\* 무료 제공은 매월 저장된 문서와 동일한 양을 기반으로 합니다. 예를 들어, 표준 플랜에서 무료 제공은 2,000개의 문서 * 720 시간 / 1000 문서 일괄처리 = 1440 Thousand Document-Hours와 동일합니다.

**예:** 표준 플랜을 이용하는 사용자는 한 달 동안 4,000개의 문서를 저장합니다. 부과되는 금액은 다음과 같습니다. 

- `4000 documents * 720 hours (in a month) / 1000 = 2,880` Thousand Document-Hours 이용

- `2,880 - 1,440 (free document hours) = 1,440` 청구 가능한 Thousand Document-Hours

- `1,440 * $0.0139` (Thousand Document-Hour당 가격) = `$20.00` 월별

**참고:** 시간당 청구된 금액을 계산하는 경우 총 저장된 문서의 수는 계산의 일부로 가장 가까운 1,000으로 반올림됩니다. 예를 들어, 1시간 동안 4,678개의 문서가 저장된 경우 5,000으로 반올림되고 계정에 청구되는 5 Thousand Document-Hours가 발생합니다. 

**참고:** 인리치먼트에 추가되는 비용은 없습니다. 

{{site.data.keyword.Bluemix_notm}} 보안에 대한 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} 서비스 설명 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=IBM+Bluemix+Service+Description){: new_window}을 참조하십시오. 

## 이전 가격 책정 플랜에서의 변환

**2017년 8월 1일** 이전의 플랜을 구독한 고객은 새 플랜 중 하나로 마이그레이션됩니다. 

- 이전에 30일 무료 평가판을 사용한 고객은 **라이트** 플랜으로 마이그레이션되었습니다.
  이 전이의 결과로 기존 사용자는 _(2000)_의 문서, _(200Mb)_의 스토리지 또는 _(2)_의 콜렉션 수로 제한된 라이트 플랜 제한사항을 충족했거나 초과했습니다. **라이트** 플랜의 제한사항을 초과한 경우 추가 컨텐츠를 서비스에 추가할 수 없으나 콜렉션을 계속 조회할 수 있습니다. {{site.data.keyword.discoveryshort}} 도구 및 API를 사용하여 모든 제한사항의 현재 상태를 볼 수 있습니다. {{site.data.keyword.discoveryshort}} 인스턴스에 컨텐츠 추가를 재개하려면 다음 중 하나를 수행해야 합니다. 
  - **라이트** 플랜의 제한사항이 초과되지 않도록 콜렉션 및/또는 문서를 제거하십시오.
    문서는 [delete-doc ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-doc){: new_window} 메소드를 사용하여 API를 통해 개별적으로 삭제될 수 있으며 전체 콜렉션은 [delete-collection ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-collection){: new_window} 메소드를 사용하여 도구 또는 API를 통해 삭제될 수 있습니다. 
  - 스토리지 요구사항을 충족하는 레벨로 플랜을 업그레이드하십시오. 
- **`1`**, **`2`** 또는 **`3`**개의 환경을 갖춘 고객은 **고급** 플랜으로 자동 마이그레이션되었습니다.
  고급 계층으로 이동한 상태에서 100,000개의 문서 및 4개의 콜렉션을 모두 사용하지 않는 경우 표준 계층으로 이동하여 비용을 줄일 수 있습니다. 이 경우 표준 플랜에서 새 Discovery 인스턴스를 작성하고 새 인스턴스에 데이터를 재수집해야 합니다. 수집은 도구, API 또는 Data Crawler를 통해 수행될 수 있습니다. 

추가 가격 책정 정보는 [{{site.data.keyword.discoveryshort}} 카탈로그 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window}를 참조하십시오. 
