---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-25"

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

# 성능 대시보드에서 메트릭 보기 및 조회 결과 개선
{: #performance-dashboard}

{{site.data.keyword.discoveryshort}} 도구의 성능 대시보드를 사용하여 조회 메트릭을 보고 조회 관련성 등의 조회 결과를 향상시킬 수 있습니다.

왼쪽에 있는 **데이터 메트릭 보기** 아이콘을 클릭하여 성능 대시보드에 액세스할 수 있습니다. 이 대시보드는 프리미엄 또는 전용 환경에서 사용할 수 없습니다.

자연어 조회 결과를 향상시키는 두 가지 옵션이 있습니다.
- [많은 데이터를 추가하여 결과가 없는 조회 문제 해결](/docs/services/discovery/dashboard.html#addmore)
- [데이터를 훈련하여 관련성 높은 결과를 맨 위로 가져오기](/docs/services/discovery/dashboard.html#traindata)

[조회 개요](/docs/services/discovery/dashboard.html#overview)에서 데이터 메트릭을 볼 수 있습니다. 

## 많은 데이터를 추가하여 결과가 없는 조회 문제 해결
{: #addmore}

대시보드의 이 섹션에서는 0개의 결과를 리턴한 조회를 검토하고 조회가 나중에 결과를 리턴하도록 더 많은 데이터를 추가할 수 있습니다. 시작하려면 **모두 보기 및 데이터 추가** 단추를 클릭하십시오. 

## 데이터를 훈련하여 관련성 높은 결과를 맨 위로 가져오기
{: #traindata}

이 섹션에서는 자연어 조회 결과의 관련성을 향상시키기 위해 콜렉션을 훈련시킬 수 있습니다. 시작하려면 **모두 보기 및 관련성 훈련 수행** 단추를 클릭하십시오. 그런 다음 [조회 추가 및 결과 관련성 등급 지정](/docs/services/discovery/train-tooling.html#results)의 지시사항을 참조하십시오.

훈련 요구 사항 및 옵션에 대한 자세한 정보는 [도구를 사용하여 결과 관련성 향상](/docs/services/discovery/train-tooling.html)을 참조하십시오.

## 조회 개요
{: #overview}

조회 개요 섹션에서는 다음을 표시합니다.
- 사용자가 작성한 총 조회 수.
- 하나 이상의 결과가 클릭된 조회의 백분율.
- 결과가 클릭되지 않은 조회의 백분율.
- 결과가 리턴되지 않은 조회의 백분율.
- 시간 경과에 따라 이러한 결과를 표시하는 그래프로 더 많은 데이터를 추가하는 방법을 추적하고 관련성 훈련이 성능을 향상시키는 방법을 추적할 수 있습니다.

이러한 결과는 이벤트 및 피드백 API를 사용하여 수집됩니다. 자세한 정보는 [API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#events-and-feedback-api)를 참조하십시오.
