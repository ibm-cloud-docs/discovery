---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-05"

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

# Watson Discovery News

{{site.data.keyword.discoverynewsfull}}는 {{site.data.keyword.discoveryshort}}에 포함되어 있습니다. {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}}는 **키워드 추출**, **엔티티 추출**, **감성 역할 추출**, **감성 분석**, **관계 추출** 및 **카테고리 분류**의 코그너티브 통찰로 사전 강화되는 인덱싱된 데이터 세트입니다. (인리치먼트에 대해 자세히 알아보려면 [인리치먼트 추가](building.html#adding-enrichments)를 참조하십시오.) 추가 메타데이터(크롤링 날짜 및 발행 날짜)도 추가됩니다. 뉴스 데이터에 대한 이전 60일 동안의 히스토리 검색이 가능합니다. [여기 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://discovery-news-demo.ng.bluemix.net/){: new_window}에서 {{site.data.keyword.discoverynewsfull}}를 사용하여 무엇을 빌드할 수 있는지에 대한 데모를 보십시오.

{{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}}는 새로운 기사로 계속 업데이트되며 영어, 스페인어, 독일어, 한국어 및 일본어로 사용할 수 있습니다. {{site.data.keyword.discoverynewsshort}} 영어 버전은 매일 약 300,000개의 새 기사로 업데이트됩니다. {{site.data.keyword.discoverynewsshort}} 스페인어 버전은 매일 약 60,000개의 새 기사로 업데이트됩니다. {{site.data.keyword.discoverynewsshort}} 독일어 버전은 매일 약 40,000개의 새 기사로 업데이트됩니다. {{site.data.keyword.discoverynewsshort}} 한국어 버전은 매일 10,000개의 새 기사로 업데이트됩니다. {{site.data.keyword.discoverynewsshort}} 일본어 버전은 매일 약 17,000개의 새 기사로 업데이트됩니다. 뉴스 소스는 언어에 따라 다르므로 각 콜렉션의 조회 결과는 동일하지 않습니다.

{{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}}에 대한 유스 케이스:

- 뉴스 알림 - 뉴스와 인식 방법을 모두 확인하기 위해 엔티티, 키워드, 카테고리 및 감성 분석에 대한 지원을 활용하여 뉴스 알림을 작성합니다.

- 이벤트 발견 - 주제/조치/오브젝트 시맨틱 역할 추출은 용어/조치(예: "획득", "선거 결과" 또는 "IPO")를 확인합니다.

- 뉴스의 동향 주제 - 인기 있는 주제를 식별하고 인기 있는 주제(또는 관련 주제)가 언급되는 빈도의 증가 또는 감소를 모니터링합니다.

{{site.data.keyword.discoverynewsfull}}의 쓰기 조회에 대한 정보는 다음을 참조하십시오.
- [Watson Discovery News 조회](/docs/services/discovery/using.html#querying-news)
- [조회 개념](/docs/services/discovery/using.html)
- [조회 참조](/docs/services/discovery/query-reference.html).

{{site.data.keyword.discoverynewsfull}} 구성을 조정하거나 훈련하거나 또는 {{site.data.keyword.discoverynewsfull}} 콜렉션에 문서를 추가할 수 없습니다.

{{site.data.keyword.discoverynewsfull}} 조회는 `text` JSON 필드에 각 기사의 처음 50개 단어를 표시합니다.

{{site.data.keyword.discoverynewsfull}} 조회에 리턴되는 최대 결과 수는 `50`개입니다. `50`개 이상의 결과를 리턴하려면 추가 조회와 `offset` 매개변수를 사용하십시오.

**참고:** **2017년 7월 31일**에 {{site.data.keyword.discoverynewsfull}}의 이 버전이 발표되었습니다. {{site.data.keyword.discoverynewsfull}} Original은 **2018년 1월 15일** 서비스부터 더 이상 사용되지 않습니다. 마이그레이션에 대한 자세한 정보는 [Watson Discovery News Original에서 마이그레이션](/docs/services/discovery/migrate-bwdn.html)을 참조하십시오.
