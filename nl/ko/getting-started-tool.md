---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-30"

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
{:download: .download}

# 도구 시작하기

이 짧은 튜토리얼에서는 {{site.data.keyword.discoveryshort}} 도구를 소개하고 개별 데이터 콜렉션 작성 및 검색 프로세스를 진행합니다.
{: shortdesc}

## 시작하기 전에
{: #before-you-begin}

시작할 서비스가 필요합니다. 

<!-- Remove the text marked `download` after there's no g-s tab in the catalog dashboard -->

서비스 인스턴스를 작성했습니다. **관리**를 클릭한 후 **도구 실행**을 클릭하십시오. [단계 2](/docs/services/discovery/getting-started-tooling.html#create-a-collection)로 이동하십시오.
{: download tip}

{{site.data.keyword.discoveryshort}} 서비스를 사용하여 프로젝트를 작성한 경우 전제조건이 충족됩니다. [단계 1](/docs/services/discovery/getting-started-tooling.html#launch-the-tooling)로 이동하십시오. 

1.  {{site.data.keyword.watson}} Developer Console [서비스 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.{DomainName}/developer/watson/services){: new_window} 페이지로 이동하십시오. 
1.  {{site.data.keyword.discoveryshort}}를 선택하고 **서비스 추가**를 클릭한 후 무료 {{site.data.keyword.Bluemix_notm}} 계정을 등록하거나 로그인하십시오. 
1.  프로젝트 이름으로 `discovery-tutorial`을 입력하고 **프로젝트 작성**을 클릭하십시오.

<!-- Remove this text after dedicated instances have the Developer Console: begin -->

{{site.data.keyword.Bluemix_dedicated_notm}}를 사용하는 경우 카탈로그의 [{{site.data.keyword.discoveryshort}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.{DomainName}/catalog/services/discovery/){: new_window} 페이지에서 서비스 인스턴스를 작성하십시오. 

<!-- Remove this text after dedicated instances have the Developer Console: end -->

## 단계 1: 도구 실행
{: #launch-the-tooling}

{{site.data.keyword.discoveryshort}} 서비스를 포함한 프로젝트를 작성한 후 프로젝트 세부사항 페이지가 표시됩니다. 여기에서 {{site.data.keyword.discoveryshort}} 도구를 실행하십시오. 

**서비스** 아래에서 {{site.data.keyword.discoveryshort}}를 위한 **도구 실행**을 클릭하십시오. 

<!-- To do: Add screenshot for developer console -->

도구에 로그인하기 위한 프롬프트가 표시되는 경우 {{site.data.keyword.Bluemix_notm}} 신임 정보를 제공하십시오. 

{{site.data.keyword.discoveryshort}} 서비스에 대한 프로젝트 세부사항 페이지에 있지 않으면 {{site.data.keyword.watson}} Developer Console [프로젝트 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.{DomainName}/developer/watson/projects) 페이지로 이동하여 프로젝트를 선택하십시오.
{: tip}

<!-- Remove this text after dedicated instances have the Developer Console: begin -->

{{site.data.keyword.Bluemix_dedicated_notm}}: 대시보드에서 서비스 인스턴스를 선택하여 도구를 실행하십시오.

<!-- Remove this text after dedicated instances have the Developer Console: end -->

## 단계 2: 콜렉션 작성
{: #create-a-collection}

{{site.data.keyword.discoveryshort}} 도구의 첫 번째 단계는 데이터 콜렉션을 작성하는 것입니다. 

콜렉션은 문서 세트입니다. *하나 이상의 콜렉션이 필요한 이유는 무엇입니까?* 몇 가지 이유가 있습니다.

- 서로 다른 대상에 따라 결과를 구분하기 위해 여러 콜렉션이 필요할 수 있습니다. 
- 데이터가 서로 다를 수 있으므로 데이터를 모두 동시에 조회하는 것은 적절하지 않습니다. 

사용자는 공용이며 사전 강화된 {{site.data.keyword.discoverynewsshort}} 데이터 콜렉션도 사용할 수 있습니다. 조회할 준비가 되어 있으며 즉시 조회 작성을 시작할 수 있습니다. 구성을 조정하거나 {{site.data.keyword.discoverynewsshort}}에 문서를 추가할 수 없습니다.

1.  ![Cog](images/icon_settings.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->를 클릭하고 **환경 작성**을 선택하십시오.
1.  사용자의 환경이 준비가 되면 **새 콜렉션 이름 지정** 대화 상자가 표시됩니다. 콜렉션의 이름을 지정하고 **적용할 구성 선택**에서 **기본 구성**을 선택하십시오(나중에 구성을 변경할 수 있음). 

## 단계 3: 사용자 정의 구성 작성
{: create-custom-configuration}

콜렉션이 작성된 후 업로드 영역을 사용하여 컨텐츠 업로드를 즉시 시작할 수 있으나 먼저 사용자 정의 구성을 작성하고 테스트하려고 합니다. 

1.  콜렉션 이름 옆에 있는 **전환**을 클릭하고 **새 구성 작성**을 선택하십시오. 구성의 이름을 지정하고 **작성**을 클릭하십시오.
1.  구성을 작성한 후 사용자 정의할 수 있습니다. 
    1.  <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘" title="외부 링크 아이콘" class="style-scope doc-content"></a> 샘플 문서를 다운로드하십시오. 
    1.  샘플 문서를 업로드하려면 **샘플 문서 업로드** 패널을 사용하십시오. 업로드한 후 문서 이름을 클릭하여 변환을 볼 수 있습니다. 
1.  이제 구성을 조정해야 합니다. 이 태스크의 경우 각 문서에 적용된 인리치먼트를 변경하십시오. 
    1.  구성의 **강화** 섹션을 클릭하십시오. 화면의 오른쪽에 생성된 JSON을 살펴보십시오. *enriched_text* 섹션을 아래로 스크롤하고 이 섹션에 많은 *개념*이 포함되어 있다는 점에 유의하십시오. 
    1.  그런 다음 *개념*으로 이름 지정된 텍스트 인리치먼트 옆에 있는 **X**를 클릭하여 이 텍스트 인리치먼트를 제거한 후 **적용 및 저장**을 클릭하십시오.
    1.  마지막으로 JSON을 다시 살펴보십시오. 출력이 어떻게 변경되었는지 및 출력에 더 이상 *개념*이 포함되지 않는다는 점을 확인하십시오. 

## 단계 4: 문서 업로드
{: #upload-your-documents}

샘플 문서의 사용자 정의 변환에 만족하면 콜렉션에 실제 컨텐츠를 수집하십시오. 

1. 세 개의 샘플 문서 즉, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘" title="외부 링크 아이콘" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘" title="외부 링크 아이콘" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘" title="외부 링크 아이콘" class="style-scope doc-content"></a>을 다운로드하십시오.
1.  ![파일 아이콘](images/icon_yourData.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->을 클릭하고 콜렉션을 선택하십시오. 
1.  작성한 사용자 정의 구성이 **구성** 아래에 나열되는지 확인하십시오. 그렇지 않은 경우 구성 이름 옆에 있는 **변환**을 클릭하고 이를 선택하십시오. 
1.  **문서 업로드** 단추를 클릭하고 네 개의 샘플 문서 즉, test-doc1.html, test-doc2.html, test-doc3.html, test-doc4.html의 업로드를 시작하십시오. 
1.  문서를 업로드할 때까지 기다리십시오. 문서의 상태는 **개요** 섹션에 표시됩니다. 

## 단계 5: 조회 빌드
{: #build-a-query}

1.  ![조회 아이콘](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->을 클릭하여 조회 페이지를 여십시오. 콜렉션을 선택하고 **시작하기**를 클릭하십시오.
1.  **조회 빌드** 화면에서 **문서 검색**을 클릭한 후 **{{site.data.keyword.discoveryshort}} 조회 언어 사용**를 클릭하십시오. 
    - "IBM"으로 이름 지정된 엔티티를 사용하여 결과를 검색하려면 다음을 수행하십시오. 
        1.  **필드**를 클릭하고 `enriched_text.entities.text`를 선택하십시오. **연산자**에 `contains`를 선택하고 **값**에 `IBM`을 선택하십시오. 조회 `enriched_text.entities.text:IBM`이 **시각적 조회 빌더**에 표시됩니다.
        1.  **조회 실행**을 클릭하십시오. 조회는 네 개의 결과를 리턴합니다. 
    - "Watson"으로 이름 지정된 엔티티를 사용하여 결과를 검색하려면 다음을 수행하십시오. 
        1.  **필드**를 클릭하고 `enriched_text.entities.text`를 선택하십시오. **연산자**에 `contains`를 선택하고 **값**에 `watson`을 선택하십시오. 조회 `enriched_text.entities.text:watson`이 **시각적 조회 빌더**에 표시됩니다.
        1.  **조회 실행**을 클릭하십시오. 조회는 두 개의 결과를 리턴합니다. 
    - "Watson" 및 "Slack"으로 이름 지정된 두 개의 엔티티를 사용하여 결과를 검색하려면 다음을 수행하십시오. 
        1.  **필드**를 클릭하고 `enriched_text.entities.text`를 선택하십시오. **연산자**에 `contains`를 선택하고 **값**에 `watson`을 선택하십시오. **규칙 추가**를 클릭한 후 선택사항을 반복한 후 `Slack`의 **값**을 선택하십시오. 조회 `enriched_text.entities.text:watson,enriched_text.entities.text:Slack`이 **시각적 조회 빌더**에 표시됩니다.
        1.  **조회 실행**을 클릭하십시오. 조회는 한 개의 결과를 리턴합니다. 

    {{site.data.keyword.discoveryshort}} 조회 언어를 사용하여 조회를 빌드하려면 **조회 언어로 편집**을 클릭하십시오. {{site.data.keyword.discoveryshort}} 조회 언어에 대해 자세히 알아보려면 [조회 참조](/docs/services/discovery/query-reference.html) 및 [조회 개념](/docs/services/discovery/using.html)을 참조하십시오.
1.  조회의 결과가 **결과** 섹션에 표시됩니다. 
    - **요약** 탭은 조회 결과의 개요를 제공합니다. 
    - **JSON** 탭은 전체 JSON 결과를 표시합니다. 

    나열된 조회에 대해 **요약**에서는 문서 단락(관련성 순서로), 발견된 문서의 이름, 인리치먼트별 결과가 차례로 표시됩니다. **단락**은 조회로 리턴된 전체 문서에서 추출된 짧은 관련 발췌입니다. 

    애플리케이션에서 두 개의 **JSON** 및 **요약** 탭 아래의 제공된 **조회 URL** 링크를 사용할 수 있습니다. 

    또한 **자연어 사용**을 클릭하여 자연어 조회를 작성할 수도 있습니다(예: "IBM Watson partnerships"). 자연어 조회에 대해 자세히 알아보려면 [자연어 조회](/docs/services/discovery/query-parameters.html#nlq)를 참조하십시오.

    자연어 조회의 결과를 향상시키기 위해 Watson을 훈련시킬 수 있습니다. [도구로 결과 관련성 향상](/docs/services/discovery/train-tooling.html)을 참조하십시오.

    추가 리소스:
    - 문서의 데이터 스키마에 대해 자세히 알아보려면 **데이터 스키마 보기** 아이콘을 클릭하거나 **JSON** 탭을 클릭하십시오. 자세한 사항은 [Discovery 데이터 스키마](/docs/services/discovery/using.html#discovery-schema)를 참조하십시오. 
    - {{site.data.keyword.discoveryshort}} 조회 언어로 편집하는 경우 **여기에 조회 입력** 필드 옆에 있는 **?** 아이콘을 클릭하여 추가 예제를 확인하십시오. 

## 다음 단계
{: #next-steps}

이제 작동하며 채워진 {{site.data.keyword.discoveryshort}} 서비스 인스턴스가 제공됩니다. 더 많은 문서 및 인리치먼트를 추가하여 콜렉션 사용자 정의와 변환 설정 사용자 정의를 시작할 수 있습니다. 
