---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-06"

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

# 조회 시작하기
{: #getting-started-with-querying}

이 튜토리얼에서는 {{site.data.keyword.discoveryshort}} 조회 언어에서 몇 가지 다른 유형의 조회를 작성하는 방법에 대해 학습합니다.
{: shortdesc}

조회 작성에 대한 자세한 정보는 다음을 참조하십시오.
- [조회 개념](/docs/services/discovery?topic=discovery-query-concepts#query-concepts)
- [조회 참조](/docs/services/discovery?topic=discovery-query-reference#query-reference)({{site.data.keyword.discoveryshort}} 조회 언어에 사용 가능한 매개변수, 연산자 및 집계의 목록 포함)

이 조회 예제는 {{site.data.keyword.discoveryshort}} 도구를 사용하여 빌드됩니다. 그 대신 API를 사용하려는 경우 조회 매개변수를 API 호출에 추가하십시오. 자세한 정보 및 예제는 [API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window}의 조회 절을 참조하십시오.

또한 {{site.data.keyword.discoveryshort}} 도구를 사용하여 자연어 조회(예: "IBM Watson partnerships")도 작성할 수 있습니다. 조회가 구조화되어야 할 수 있고 필터 및 집계가 {{site.data.keyword.discoveryshort}} 조회 언어로 작성되어야 하므로 이 튜토리얼은 주로 {{site.data.keyword.discoveryshort}} 조회 언어로 조회를 작성하는 방법에 중점을 둡니다.
{: tip}

## 시작하기 전에
{: #querying-before-you-begin}

**데이터 관리** 화면으로 이동하고 {{site.data.keyword.IBM_notm}} Press Releases라는 새 콜렉션을 작성하며 네 개의 문서 즉, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘" title="외부 링크 아이콘"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘" title="외부 링크 아이콘"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘" title="외부 링크 아이콘"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘" title="외부 링크 아이콘"></a>을 새 콜렉션에 추가하십시오. 

일부 브라우저에서는 링크가 로컬에 저장되는 대신 새 창으로 열립니다. 이 경우, 브라우저의 `File` 메뉴에서 `Save As`를 선택하여 파일 사본을 저장하십시오.
{: tip}

## 단계 1: Discovery 데이터 스키마의 빠른 둘러보기
{: #querying-step1}

먼저 {{site.data.keyword.discoveryshort}} JSON에 대해 알아보십시오. {{site.data.keyword.discoveryshort}} 조회 언어를 사용하여 조회를 빌드하는 방법을 이해하려면 이 조회 언어가 콜렉션의 문서를 강화한 후 {{site.data.keyword.discoveryshort}}로 생성된 JSON과 익숙해지는 것이 도움이 됩니다.

1.  [{{site.data.keyword.discoveryshort}} 도구를 시작](/docs/services/discovery?topic=discovery-getting-started#launch-the-tooling)하십시오. **데이터 관리** 화면에서 {{site.data.keyword.IBM_notm}} Press Releases 콜렉션을 선택하십시오.

1.  강화된 문서에서 발견된 인사이트 Watson을 검토하십시오.

    -  **감성 분석**은 감성 분석 인리치먼트로 발견한 긍정, 중립, 부정으로 태그 지정된 문서의 백분율 분석을 표시합니다.
    -  **엔티티 추출**은 엔티티 추출 인리치먼트로 문서에서 발견한 사용자, 위치 및 조직을 표시합니다.
    -  **카테고리 분류**는 카테고리 분류 인리치먼트로 문서에서 발견한 계층 구조 택소노미를 표시합니다.
    -  **개념 태그 지정**은 개념 태그 지정 인리치먼트로 문서에서 발견한 개념을 표시합니다.

1.  문서의 데이터 스키마에 익숙해지려면 **데이터 스키마 보기** 화면을 살펴보십시오. 두 가지 방법 즉, 문서(**문서 보기**) 또는 필드(**콜렉션 보기**)로 변환된 문서에서 필드 및 값을 표시합니다. **콜렉션 보기**에 콜렉션의 모든 필드가 표시됩니다.

    왼쪽에 있는 **데이터 스키마 보기** 아이콘을 클릭하십시오. `enriched_text`의 **콜렉션 보기**에서 콜렉션에 적용된 인리치먼트를 검토할 수 있습니다. 콜렉션이 Watson 인사이트로 강화되는 방법을 보려면 `categories`, `concepts`, `entities` 및 `sentiment`를 클릭하십시오.

조회가 일치하는 결과를 리턴하지 않으나 리턴해야 한다고 판단하는 경우, 조회가 데이터 스키마에서 확인할 수 있는 필드/값에 사용 중인 필드/값의 스왑 아웃을 시도하십시오.
{: tip}    

## 단계 2: 기본 조회 빌드
{: #querying-step2}

먼저 콜렉션에서 `Cloud computing` 개념을 찾을 조회 작성을 수행하십시오.

1.  **조회 빌드** 아이콘 ![조회 아이콘](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->을 클릭하여 조회 페이지를 여십시오. {{site.data.keyword.IBM_notm}} Press Releases가 포함된 콜렉션을 선택하고 **시작하기**를 클릭하십시오.
1.  **조회 빌드** 화면에서 **문서 검색**을 클릭하고 **{{site.data.keyword.discoveryshort}} 조회 언어 사용**을 클릭한 후 다음을 수행하십시오.
    - **필드** 드롭 다운을 클릭하고 `enriched_text.concepts.text`를 선택하고(**연산자**에 `contains` 선택) `Cloud computing`의 **값**을 입력하십시오. 조회 `enriched_text.concepts.text:Cloud computing`이 **시각적 조회 빌더** 아래에 표시됩니다.

    - 또는 **조회 언어로 편집**을 클릭한 후 **{{site.data.keyword.discoveryshort}} 조회 언어 사용**을 클릭할 수 있습니다. `enriched_text.concepts.text:"Cloud computing"`을 **여기에 조회 입력** 필드에 입력하십시오.

1.  **조회 실행**을 클릭하십시오. 하나가 일치해야 합니다(`"matching_results": 1`). **요약** 또는 **JSON** 탭의 상단에서 **조회 URL**을 복사하여 애플리케이션에서 사용하십시오.

**보너스:** **추가 옵션**에서 **관련 단락 포함** 단일 선택 단추를 사용하여 단락 검색을 설정하는 옵션이 제공됩니다. 단락은 조회로 리턴된 전체 문서에서 추출된 짧은 관련 발췌입니다. 이 대상 단락은 콜렉션에 있는 문서의 `text` 필드에서 추출됩니다. 자세한 정보는 [단락](/docs/services/discovery?topic=discovery-query-parameters#passages)을 참조하십시오. 단락 검색은 {{site.data.keyword.discoveryshort}} 새 콜렉션에는 불가능합니다.

일부 사전 빌드된 조회를 체크아웃하려는 경우 **샘플 조회 사용** 단추를 클릭하십시오.
{: tip}

## 단계 3: 다른 조회를 사용한 실험
{: #querying-step3}

다음 조회를 시도하십시오.

`positive` 감성이 포함된 모든 문서를 리턴하려면 **문서 검색**, **{{site.data.keyword.discoveryshort}} 조회 언어 사용**을 클릭한 후 다음을 수행하십시오.
-  **필드** 드롭 다운을 클릭하고 `enriched_text.sentiment.document.label`을 선택하고(**연산자**에 `contains` 선택) `Cloud computing`의 **값**을 입력하십시오.  

   조회 `enriched_text.sentiment.document.label:positive`가 **시각적 조회 빌더** 아래에 표시됩니다.

`health and fitness` 카테고리의 모든 문서를 리턴하려면 **문서 검색**, **{{site.data.keyword.discoveryshort}} 조회 언어 사용**을 클릭한 후 다음을 수행하십시오.
-  **필드** 드롭 다운을 클릭하고 `enriched_text.categories.label`을 선택하고(**연산자**에 `is` 선택) `Cloud computing`의 **값**을 입력하십시오.

   조회 `enriched_text.categories.label::"health and fitness"`가 **시각적 조회 빌더** 아래에 표시됩니다. 연산자 `::`은 정확한 일치를 지정합니다.

`IBM` 엔티티가 포함되지만 `Watson`은 포함되지 않은 모든 문서를 리턴하려면 **문서 검색**, **{{site.data.keyword.discoveryshort}} 조회 언어 사용**을 클릭한 후 다음을 수행하십시오.
-  **필드** 드롭 다운을 클릭하고 `enriched_text.entities.text`를 선택하고(**연산자**에 `contains` 선택) `Cloud computing`의 **값**을 입력하십시오. **규칙 추가**를 클릭한 후(**필드**에 `enriched_text.entities.text` 선택, **연산자**에 `does not contain` 선택) `Watson`의 **값**을 입력하십시오.

   조회 `enriched_text.entities.text:IBM,enriched_text.entities.text:!Watson`이 **시각적 조회 빌더** 아래에 표시됩니다. 연산자 `:!`는 "포함하지 않음(does not contain)"을 지정합니다.

## 단계 4: 결합된 조회 빌드
{: #querying-step4}

더 많은 대상 조회를 빌드하기 위해 조회 매개변수를 함께 결합할 수 있습니다. {{site.data.keyword.IBM_notm}}의 인수에 대한 문서를 리턴하려면 `filter` 및 `query` 매개변수를 사용하십시오. 필터 매개변수가 `IBM`을 언급한 문서로 결과 범위를 좁힌 후 조회 매개변수는 `acquisitions`에 대한 모든 결과를 관련성 순서로 리턴합니다.

1.  조회 빌드 아이콘 ![조회 아이콘](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->을 클릭하여 조회 페이지를 여십시오. {{site.data.keyword.IBM_notm}} Press Releases가 포함된 콜렉션을 선택하고 **시작하기**를 클릭하십시오.

1.  **조회하는 문서 필터링**에서 다음을 수행하십시오.
    -  **필드** 드롭 다운을 클릭하고 `enriched_text.entities.text`를 선택하고(**연산자**에 `contains` 선택) `Cloud computing`의 **값**을 입력하십시오.

       조회 `enriched_text.entities.text:IBM`이 `IBM` 엔티티를 언급한 항목으로만 문서 범위를 좁힙니다.

1.  **문서 검색**에서 **{{site.data.keyword.discoveryshort}} 조회 언어 사용**을 클릭한 후 다음을 수행하십시오.
    -  **필드** 드롭 다운을 클릭하고 `enriched_text.concepts.text`를 선택하고(**연산자**에 `contains` 선택) `world wide web`의 **값**을 입력하십시오.

       조회 `enriched_text.concepts.text:"world wide web"`이 `world wide web`의 개념을 포함한 모든 문서를 리턴하고 해당 문서는 관련성 순서로 순위가 지정됩니다.

1.  **추가 옵션**, **리턴할 필드**를 차례로 클릭한 후 **지정**을 선택하십시오. `text`를 선택하십시오. 이렇게 하면 관련 기사의 텍스트로 응답이 제한되며 다른 모든 기사는 제외됩니다.

1.  **조회 실행**을 클릭하십시오. 한 개의 문서가 일치합니다(`"matching_results": 1`).

## 단계 5: 집계 빌드
{: #querying-step5}

집계에서는 데이터 값의 세트(예: 상위 키워드, 엔티티의 전체 감성 등)를 리턴합니다.

이 집계를 빌드하면 {{site.data.keyword.IBM_notm}} Press Releases 콜렉션의 상위 10개 개념을 리턴합니다.

1.  **조회 빌드** 아이콘 ![조회 아이콘](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->을 클릭하여 조회 페이지를 여십시오. {{site.data.keyword.IBM_notm}} Press Releases가 포함된 콜렉션을 선택하고 **시작하기**를 클릭하십시오.

1.  **결과의 분석 포함**에서 다음을 수행하십시오.
    -  **출력** 드롭 다운을 클릭하고 `Top values`를 클릭한 후(**필드**에 `enriched_text.concepts.text` 선택) **수**를 `10`으로 입력하십시오.

       `Term`은 `concepts` `text` 필드에 대한 가장 일반적인 값을 리턴합니다. **수**는 리턴할 결과의 수를 지정합니다. 조회 `term(enriched_text.concepts.text,count:10)`이 **시각적 조회 빌더** 아래에 표시됩니다.   

1.  **추가 옵션**을 클릭한 후 `Number of documents to return` 필드에 **0**을 입력하십시오.

1.  **조회 실행**을 클릭하십시오. 상위 10개의 개념이 **요약** 및 **JSON** 탭 모두에 표시됩니다. 다음은 요약의 예입니다.

## 단계 6: Watson Discovery News에서 조회 빌드
{: #querying-step6}

{{site.data.keyword.discoverynewsshort}}는 코그너티브 인사이트로 사전 강화된 공용 데이터 세트입니다. {{site.data.keyword.discoveryshort}}에 포함되어 있습니다. 이 콜렉션에 대한 자세한 정보는 [Watson Discovery News](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news)를 참조하십시오.

{{site.data.keyword.discoverynewsshort}} 구성을 조정하거나 훈련하거나 또는 {{site.data.keyword.discoverynewsshort}} 콜렉션에 문서를 추가할 수 없습니다. [여기 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://discovery-news-demo.ng.bluemix.net/){: new_window}에서 {{site.data.keyword.discoverynewsshort}}를 사용하여 무엇을 빌드할 수 있는지에 대한 데모를 보십시오.

다음 조회 예제는 {{site.data.keyword.discoverynewsfull}}에서 Pittsburgh Steelers에 대해 긍정적인 어조의 상위 10개 기사를 리턴합니다.

1.  **조회 빌드** 아이콘 ![조회 아이콘](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->을 클릭하여 조회 페이지를 여십시오. {{site.data.keyword.discoverynewsshort}} 콜렉션을 선택하고 **시작하기**를 클릭하십시오. (스페인어, 독일어 또는 한국어 {{site.data.keyword.discoverynewsshort}} 콜렉션을 조회하려면 먼저 ![데이터 관리](/images/icon_yourData.png) 아이콘을 클릭한 다음 드롭 다운에서 적절한 언어를 선택하십시오.)

1.  **문서 검색**에서 **{{site.data.keyword.discoveryshort}} 조회 언어 사용**을 클릭한 후 다음을 수행하십시오.
    -  **필드** 드롭 다운을 클릭하고 `text`를 선택하고(**연산자**에 `contains` 선택) `Cloud computing`의 **값**을 입력하십시오. **규칙 추가**를 클릭한 후 **필드** 드롭 다운을 클릭하고 `enriched_text.sentiment.document.label`을 선택하고(**연산자**에 `contains` 선택) `Cloud computing`의 **값**을 입력하십시오.

       조회 `text:"Pittsburgh Steelers",enriched_text.sentiment.document.label:"positive"` 가 **시각적 조회 빌더** 아래에 표시됩니다.

1.  **추가 옵션**을 클릭한 후 `Number of documents to return` 필드에 **10**(기본값)을 입력하십시오.

1.  **조회 실행**을 클릭하십시오. Pittsburgh Steelers에 대해 긍정적인 어조의 상위 10개 기사가 표시됩니다.

**참고:** Watson Discovery News 조회에 대해 리턴되는 최대 결과의 수는 `50`입니다.

뉴스 기사는 여러 언론 매체에 신디케이트될 수 있습니다. {{site.data.keyword.discoverynewsfull}}는 기사를 각각 선별하므로 기사가 중복됩니다. 이는 {{site.data.keyword.discoverynewsfull}}에 대한 조회가 잠재적으로 조회 결과에서 동일한 여러 기사 또는 거의 동일한 기사를 리턴할 수 있음을 의미합니다. 중복 제거를 설정하려면 **추가 옵션**에서 **중복 결과 제외**를 선택하십시오. 이 베타 기능에 대해 자세히 알아보려면 [조회 결과에서 중복 문서 제외](/docs/services/discovery?topic=discovery-query-parameters#deduplication)를 참조하십시오.
