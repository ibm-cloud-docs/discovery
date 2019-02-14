---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-17"

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

{{site.data.keyword.discoveryfull}} 서비스는 사용자의 요구에 맞게 서로 다른 레벨의 리소스와 기능을 제공하는 세가지 플랜 **라이트**, **고급** 및 **프리미엄**을 제공합니다.
{: shortdesc}

**개인용 데이터 유스 케이스**에서는 다음 기능, 제한사항 및 가격을 표시합니다.

## 라이트
{: #lite}

크기 | 문서 저장 공간 한계 | 문서 수\* | 가격
------ | ------ | ------ | ------  
해당사항 없음 | 50MB | 1,000(월) | 무료

라이트 플랜은 스타터 플랜이며 프로덕션에 사용할 수 없습니다. 유료 플랜으로 업그레이드할 때 수집된 모든 문서를 보존할 수 있습니다. 라이트 플랜 인스턴스는 30일의 비활성 기간 후 삭제됩니다. 

속성:
- 1개의 환경
- 최대 2개의 콜렉션
- 사용 가능한 NLU 인리치먼트\*\*
- 20개의 인플라이트 문서\*\*\*\* 

추가 옵션:<br> [사용자 정의 모델](/docs/services/discovery/integrate-wks.html#integrating-your-custom-model):<br>
하나의 Watson Knowledge Studio 모델이 포함되어 있습니다. 추가 모델: 사용할 수 없음<br>[요소 분류](/docs/services/discovery/element-classification.html)\*\*\*:
매월 500개의 페이지가 포함되어 있습니다. 추가 페이지: 사용할 수 없음<br>[뉴스 조회](/docs/services/discovery/watson-discovery-news.html):
매월 200개의 뉴스 조회가 포함되어 있습니다. 추가 조회: 사용할 수 없음<br>[조회 확장](/docs/services/discovery/using.html#query-expansion):
총 1,000개의 용어를 사용하는 500개의 조회 확장이 포함되어 있습니다. 추가 확장: 사용할 수 없음

라이트에서 고급으로 업그레이드하는 데 대한 정보는 [서비스 업그레이드](/docs/services/discovery/upgrading.html#service)를 참조하십시오.

## 고급
{: #advanced}

크기 | 문서 저장 공간 한계 | 문서 수\* | 가격
------ | ------ | ------ | ------ 
X-Small\*\*\*\*\* | 40GB | 매월 최대 50,000개의 문서 | 매월 $500부터 시작 
Small | 160GB | 매월 최대 1M개의 문서 | 매월 $1,500부터 시작 
Medium-Small | 320GB | 매월 최대 2M개의 문서 | 매월 $3,000부터 시작 
Medium| 640GB | 매월 최대 4M개의 문서 | 매월 $5,000부터 시작 
Medium-Large | 1.2TB | 매월 최대 8M개의 문서 | 매월 $10,000부터 시작 
Large| 2.4TB | 매월 최대 16M개의 문서 | 매월 $15,000부터 시작 
X-Large| 4TB | 매월 최대 32M개의 문서 | 매월 $20,000부터 시작 
XX-Large | 5.5TB | 매월 최대 64M개의 문서 | 매월 $35,000부터 시작 
XXX-Large | 12TB | 매월 최대 100M개의 문서 | 매월 $45,000부터 시작 

X-Small은 사용 가능한 가장 작은 규모의 환경이며 개발 및 테스트용으로만 권장됩니다.\*\*\*\*\*

고급 플랜의 한 레벨에서 다른 레벨로 이동하는 경우 새 인스턴스를 작성할 필요가 없습니다. 고급 플랜에서 프리미엄 플랜으로 전환하는 경우 새 인스턴스가 필요합니다. 고급 플랜의 한 계층에서 다른 계층으로 업그레이드하는 데 대한 정보는 [한 고급 계층에서 다른 계층으로 이동](/docs/services/discovery/upgrading.html#advanced)을 참조하십시오.

\*\*\*\*\*X-Small 플랜의 속성: 
- 1개의 환경
- 최대 4개의 콜렉션
- 사용 가능한 NLU 인리치먼트\*\*
- 50개의 인플라이트 문서\*\*\*\*

기타 모든 고급 플랜의 속성:
- 1개의 환경
- 최대 100개의 콜렉션
- 사용 가능한 NLU 인리치먼트\*\*
- 105개의 인플라이트 문서\*\*\*\*

추가 옵션:<br> [사용자 정의 모델](/docs/services/discovery/integrate-wks.html#integrating-your-custom-model):<br>
하나의 Watson Knowledge Studio 모델이 포함되어 있습니다. 추가 모델: 각 $800<br>[요소 분류](/docs/services/discovery/element-classification.html)\*\*\*:
매월 500개의 페이지가 포함되어 있습니다. 추가 페이지: 각 $0.40<br>[뉴스 조회](/docs/services/discovery/watson-discovery-news.html):
매월 200개의 뉴스 조회가 포함되어 있습니다.  
10,000개의 추가 조회(매월): 조회당 $0.10<br>
10,001 - 100,000개의 추가 조회(매월): 조회당 $0.05<br>
100,000 이상의 조회(매월): 조회당 $0.03<br>
[조회 확장](/docs/services/discovery/using.html#query-expansion):
총 25,000개의 용어를 사용하는 5,000개의 조회 확장이 포함되어 있습니다.

## 프리미엄
   
프리미엄 플랜은 더 나은 격리 및 보안을 위해 하나 이상의 Watson 서비스의 단일 테넌트 인스턴스를 개발자와 조직에게 제공합니다. 이러한 플랜은 전이 중 및 휴지 중에 엔드-투-엔드 암호화된 데이터를 제공할 뿐만 아니라 기존 공유 플랫폼에서 컴퓨팅 레벨 격리를 제공합니다. 

자세한 정보를 보거나 프리미엄 플랜을 구매하려면 [영업 담당자](https://ibm.biz/contact-wdc-premium)에게 문의하십시오. 
<br>
<br> 

**참고:** API의 버전 날짜를 `2018-08-01`로 업데이트했습니다. 새 환경 크기 조정 옵션(`LT`, `XS`, `S`, `MS`, `M`, `ML`, `L`, `XL`, `XXL`, `XXXL`)을 활용하려면 API를 사용하여 환경을 작성할 때 이 버전 날짜를 사용해야 합니다. 이제 환경 크기는 `string` 유형입니다(이전 유형은 `integer`임).

\* 문서 제한은 디스크의 평균 문서 크기가 100KB라고 간주합니다. 문서 크기는 변환과 인리치먼트를 수행한 후에 계산되므로 문서 크기는 원래의 출력에서 크게 변경될 수 있습니다. [Environments](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#environments-api) 또는 [Collections](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#collections-api) API를 사용하거나 도구를 사용하여 저장된 문서 수와 사용된 총 스토리지 크기를 볼 수 있습니다. 디스크에서 문서가 평균적으로 100KB보다 큰 경우 최대 문서 한계 전에 플랜의 저장 공간 한계에 도달하게 됩니다. 문서에서 [문서 세그먼트화](https://console.bluemix.net/docs/services/discovery/building.html#doc-segmentation)를 수행하는 경우 각 세그먼트는 개별 문서로 계수됩니다.

\*\* [NLU(Natural Language Understanding) 인리치먼트](https://console.bluemix.net/docs/services/discovery/building.html#adding-enrichments)는 엔티티 추출, 감성 분석, 카테고리 분류, 개념 태그 지정, 키워드 추출, 관계 추출, 감정 분석, 요소 분류 및 시맨틱 역할 추출입니다. 각 문서에서 처음 50,000자만 강화됩니다. 

\*\*\* 요소 분류는 중요한 요소를 변환, 식별 및 분류하기 위해 운영 문서를 통해 구문 분석하는 인리치먼트입니다. 이는 자연어 처리를 사용하여 PDF 문서에서 당사자(참조하는 사용자), 네이처(요소 유형) 및 카테고리(특정 클래스) 요소를 추출합니다.

\*\*\*\* 인플라이트 한계에 도달하면 수집 속도를 늦추어야 합니다. Discovery 서비스를 사용하는 경우 문서가 콜렉션에 추가되기 전에 업로드되고 강화되고 처리되는 동안 문서는 "인플라이트" 상태입니다.

비용 계산에 대한 정보는 [IBM Cloud 가격 계산기 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.bluemix.net/pricing/platform/watson){: new_window}를 참조하십시오.

IBM Cloud 보안에 대한 자세한 정보는 [클라우드 서비스 데이터 보안 및 개인정보 보호 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/software/sla/sladb.nsf/sla/csdsp?OpenDocument){: new_window}를 참조하십시오.

추가 가격 책정 정보에 대해서는 [{{site.data.keyword.discoveryshort}} 카탈로그 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.bluemix.net/catalog/services/discovery){: new_window}를 참조하십시오.

## 기존 플랜을 사용하는 고객의 주의사항

- **2018년 8월 1일**부터 비용 청구 및 사용량은 이 가격 책정 플랜을 기반으로 합니다.
- 라이트 플랜은 매월 2,000개의 문서/400개의 {{site.data.keyword.discoverynewsshort}} 조회에서 매월 1,000개의 문서/200개의 {{site.data.keyword.discoverynewsshort}} 조회로 감소되었습니다. 새로운 라이트 플랜 한계를 이미 초과한 경우 문서를 더 이상 추가할 수 없습니다. 그러나 이를 계속 사용하거나 고급 또는 프리미엄 플랜으로 업그레이드할 수 있습니다.
- 표준 플랜은 더 이상 사용되지 않으므로 더 이상 새 사용자가 사용할 수 없습니다. 현재 기존 표준 플랜 사용자인 경우 이를 계속 사용하거나 고급 또는 프리미엄 플랜으로 업그레이드할 수 있습니다.
- 고급 및 프리미엄 플랜은 이제 문서 계층을 기반으로 하며 더 이상 문서 시간을 기반으로 하지 않습니다. 계층 간에 전환하지 않는 한 월별 청구는 문서 수에 따라 변동되지 않습니다.
- 프리미엄 고객의 비용 청구 변경사항에 대한 세부사항은 [영업 담당자](https://ibm.biz/contact-wdc-premium)에게 문의하십시오.	
