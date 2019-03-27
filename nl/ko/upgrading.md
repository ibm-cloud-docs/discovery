---

copyright:
  years: 2015, 2018, 2019
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

# 사용자의 플랜 업데이트
{: #upgrading-your-plan}

{{site.data.keyword.discoveryfull}} 서비스는 사용자의 요구에 맞게 서로 다른 레벨의 리소스와 기능을 제공하는 세 가지 플랜을 제공합니다.
{: shortdesc}

자세한 사항은 [{{site.data.keyword.discoveryshort}} 가격 플랜](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans) 및 [{{site.data.keyword.discoveryshort}} 카탈로그 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/catalog/services/discovery){: new_window}를 참조하십시오. 

## 서비스 업그레이드
{: #service}

플랜 크기를 Lite에서 고급으로 조정하려면 다음을 수행하십시오.

1. [{{site.data.keyword.Bluemix_notm}} 대시보드](https://{DomainName}/dashboard)를 여십시오. 
1. {{site.data.keyword.discoveryshort}} 서비스 인스턴스를 클릭하여 {{site.data.keyword.discoveryshort}} 서비스 대시보드를 여십시오.
1. {{site.data.keyword.discoveryshort}} 서비스의 **관리** 페이지에서 **업그레이드**를 클릭하여 고급 플랜을 선택하십시오. 그러면 **프랜** 페이지가 열립니다. 단계를 수행하여 업그레이드를 완료하십시오. 
1. **관리** 페이지로 돌아가서 **도구 실행**을 클릭하여 {{site.data.keyword.discoveryshort}} 도구를 여십시오.
   - 고급으로 업그레이드하기 전에 Lite 플랜에 대한 환경을 작성한 적이 없는 경우 ![Cog](images/icon_settings.png) 아이콘을 클릭하고 **환경 작성**을 선택하십시오. 화면에 고급 플랜의 옵션이 표시됩니다. 필요에 따라 항목을 선택하십시오.  (`X-Small`, `Small`, `Medium-Small`, `Medium`, `Medium-Large`, `Large`, `X-Large`, `XX-Large`).
   - 고급으로 업그레이드하기 전에 Lite 플랜에 대한 환경을 작성한 적이 없는 경우 새 고급 플랜 환경은 기본적으로 `Small`입니다. 

## 한 고급 계층에서 다른 계층으로 전환
{: #switchadvanced} 

이미 고급 플랜을 사용 중이고 이를 더 큰 플랜 크기로 업그레이드하려는 경우 [API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/discovery#update-an-environment){: new_window}를 사용하여 이를 수행할 수 있습니다. 

고급 플랜 저장 공간 한계 및 가격에 대한 자세한 정보는 [고급 가격 플랜](/docs/services/discovery?topic=discovery-discovery-pricing-plans#advanced)을 참조하십시오.

사용 가능한 고급 플랜 크기는 다음과 같습니다. 

플랜 크기 | 레이블  
--------- | ------ 
X-Small | XS 
Small | S 
Medium-Small | MS 
Medium | M 
Medium-Large | ML 
Large | L
X-Large | XL 
XX-Large | XXL 

- 업그레이드 중에 조회 및 인덱싱을 진행할 수 있습니다. 업그레이드에 필요한 시간은 여러 요인에 따라 달라집니다. 업그레이드가 완료되는 동안 API를 사용하여 환경을 폴링할 수 있습니다.
- 고급 플랜의 한 레벨에서 다른 레벨로 이동하는 경우 새 인스턴스를 작성할 필요가 없습니다. 
- 업그레이드가 완료되면 새 플랜 등급으로 비용이 청구됩니다.
- 나중에 더 작은 플랜 크기가 필요한 경우 적절한 플랜 크기를 설정하고, 데이터를 마이그레이션한 후 더 큰 플랜을 취소해야 합니다.  

## 프리미엄 플랜으로 업그레이드
{: #premium}

프리미엄 플랜에 관심이 있는 경우 [영업 담당자](https://ibm.biz/contact-wdc-premium)에게 문의하십시오.  
