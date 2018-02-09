---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-18"

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

# 문제점 해결

{{site.data.keyword.discoveryshort}} 서비스 사용에 대한 문제점 해결 팁입니다. 

{{site.data.keyword.discoveryshort}} 서비스를 사용할 때 문제점이 발생하면 하나 다음 문제점 해결 팁 중 하나 이상을 시도하십시오. 

-   현재 문서의 데이터와 이전에 수집된 문서의 유사한 데이터 간에 유형 불일치로 인해 문서가 수집되지 않을 수 있습니다. 예를 들어, 하나의 필드가 한 문서에서는 **date**로 입력되고 후속 문서에서는 **string**으로 입력될 수 있으며 이런 경우 후속 문서가 올바르게 인덱싱되지 않습니다. 

    미리보기 오퍼레이션은 단일 문서만 테스트하고 변환 결과의 레코드를 보관하지 않으므로 유형 불일치를 예측할 수 없습니다.
-   때때로 문서의 빠르거나 대규모 인덱싱으로 인해 백엔드 검색 서비스가 다시 시작할 수 있습니다. 이 경우, {{site.data.keyword.IBM}} 지원 센터에 문의하여 도움을 받으십시오. 
