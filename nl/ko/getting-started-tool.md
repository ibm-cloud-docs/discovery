---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-08"

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

# 시작하기
{: #getting-started}

이 짧은 튜토리얼에서는 {{site.data.keyword.discoveryshort}} 도구를 소개하고 개별 데이터 콜렉션 작성 및 검색 프로세스를 진행합니다.
{: shortdesc}

API에서 작업하는 것을 선호하는 경우 [API로 시작하기](/docs/services/discovery?topic=discovery-gs-api#gs-api)를 참조하십시오.
{: tip}

## 시작하기 전에
{: #before-you-begin-tool}
{: hide-dashboard}

시작할 서비스 인스턴스가 필요합니다.
{: hide-dashboard}

1.  {: hide-dashboard}{{site.data.keyword.cloud_notm}} 카탈로그에서 [{{site.data.keyword.discoveryshort}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/catalog/services/discovery) 페이지로 이동하십시오. 

    다른 리소스 그룹을 선택하지 않는 경우 서비스 인스턴스는 **기본** 리소스 그룹에 작성되고 나중에 변경할 *수 없습니다*. 이 그룹은 서비스를 시도하는 목적에 충분합니다. 

    더욱 강력한 사용을 위해 인스턴스를 작성하는 경우 [리소스 그룹 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/docs/resources/bestpractice_rgs.html#bp_resourcegroups){: new_window}에 대해 자세히 알아보십시오.
1.  {: hide-dashboard}무료 {{site.data.keyword.cloud_notm}} 계정을 등록하거나 로그인하십시오.
1.  {: hide-dashboard}**작성**을 클릭하십시오.

## 단계 1: 도구 실행
{: #launch-the-tooling}

{{site.data.keyword.discoveryshort}} 서비스 인스턴스를 작성하면 서비스의 목록으로 이동합니다.
{: hide-dashboard}

1.  {: hide-dashboard} 작성한 {{site.data.keyword.discoveryshort}} 서비스 인스턴스를 클릭하여 서비스 대시보드로 이동하십시오.
1.  **관리** 페이지에서 **도구 실행**을 클릭하십시오. 도구에 로그인하기 위한 프롬프트가 표시되는 경우 {{site.data.keyword.cloud_notm}} 인증 정보를 제공하십시오.

<!-- To do: Add screenshot for developer console -->

## 단계 2: 콜렉션 작성
{: #create-a-collection-tool}

{{site.data.keyword.discoveryshort}} 도구의 첫 번째 단계는 데이터 콜렉션을 작성하는 것입니다.

콜렉션은 문서 세트입니다. *하나 이상의 콜렉션이 필요한 이유는 무엇입니까?* 몇 가지 이유가 있습니다.

- 서로 다른 대상에 따라 결과를 구분하기 위해 여러 콜렉션이 필요할 수 있습니다.
- 데이터가 서로 다를 수 있으므로 데이터를 모두 동시에 조회하는 것은 적절하지 않습니다.

사용자는 공용이며 사전 강화된 {{site.data.keyword.discoverynewsshort}} 데이터 콜렉션도 사용할 수 있습니다. 조회할 준비가 되어 있으며 즉시 조회 작성을 시작할 수 있습니다. 구성을 조정하거나 {{site.data.keyword.discoverynewsshort}}에 문서를 추가할 수 없습니다.

1.  ![환경 세부사항](images/env_icon.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->을 클릭하고 **환경 작성**을 선택하십시오.
1.  사용자 환경이 준비되면 **사용자 데이터 업로드** 단추를 클릭한 후 **새 콜렉션 이름 지정**을 수행할 수 있습니다. 콜렉션의 이름을 **InstallDocs**로 지정하십시오.

    **고급**에서 콜렉션을 작성하는 경우 **기본 계약 구성**이라고 하는 구성 파일을 선택할 수 있는 옵션이 제공됩니다. 이 구성은 PDF의 요소에서 당사자, 네이처 및 카테고리를 추출하는 데 사용할 수 있는 요소 분류 인리치먼트만 지원합니다. 세부사항은 [요소 분류](/docs/services/discovery?topic=discovery-element-classification#element-collection)를 참조하십시오. 이 튜토리얼에 대한 해당 옵션을 선택하지 마십시오. 

{{site.data.keyword.discoveryshort}} 도구를 사용하여 Box, Salesforce, Microsoft SharePoint Online, IBM Cloud Object Storage 및 Microsoft SharePoint 2016 데이터 소스에 연결하거나 웹 크롤링을 수행할 수도 있습니다. 자세한 정보를 보려면 **데이터 소스 연결** 단추를 클릭하고 [데이터 소스 연결](/docs/services/discovery?topic=discovery-sources#sources)을 참조하십시오.
{: tip}

## 3단계: 샘플 문서 다운로드 및 콜렉션에 업로드
{: create-custom-configuration}

1.  샘플 PDF 문서인 <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/watsonexplorerinstall.pdf" download>Watson Explorer 설치 안내서 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘" title="외부 링크 아이콘"></a>를 다운로드하십시오. {{site.data.keyword.discoveryshort}}에서 지원되는 문서 유형의 전체 목록은 [지원되는 문서 유형](/docs/services/discovery?topic=discovery-sdu#doctypes)을 참조하십시오.  

    일부 브라우저에서는 링크가 로컬에 저장되는 대신 새 창으로 열립니다. 이 경우, 브라우저의 `File` 메뉴에서 `Save As`를 선택하여 파일 사본을 저장하십시오.
    {: tip}

1.  문서를 콜렉션에 업로드하십시오. 문서를 콜렉션에 끌어서 놓거나 **컴퓨터에서 찾아보기**를 클릭하여 문서를 업로드하십시오. 업로드가 완료되면 다음 정보가 표시됩니다.
    -  문서의 수(1)입니다.
    -  문서에서 식별되는 필드입니다. 식별된 하나의 필드인 `text`가 표시되어야 합니다. 잠시 후 추가 필드를 식별합니다. 
    -  문서에 적용되는 인리치먼트입니다. 엔티티 추출, 감성 분석, 카테고리 분류 및 개념 태그 지정 인리치먼트는 {{site.data.keyword.discoveryshort}}를 통해 `text` 필드에서 자동으로 적용됩니다. [여기](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)에서 인리치먼트에 대해 자세히 알아보십시오. 
    -  즉시 실행할 수 있는 조회를 미리 빌드하십시오. 
1.  레벨 세트에 대해 빠른 자연어 조회를 시도하십시오. 오른쪽 하단에 있는 **고유한 조회 빌드**를 클릭하십시오.
1.  **조회 빌드** 화면에서 **문서 검색**을 클릭한 후 **자연어 사용**을 클릭하십시오. `What are the minimum hardware requirements`를 입력하고 **조회 실행** 단추를 클릭하십시오. 오른쪽에 있는 **JSON** 탭을 클릭하십시오. 결과는 크게 정확하지 않습니다. 그러므로 Smart Document Understanding을 사용하여 결과를 개선해보십시오. 
1.  왼쪽 상단에 있는 콜렉션의 이름(**InstallDocs**)을 클릭하여 **개요** 화면으로 돌아가십시오.  
 
## 4단계: 문서 어노테이션 작성
{: #upload-your-documents}

문서 어노테이션 작성에 대한 자세한 정보는 [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu)을 참조하십시오.
{: tip}

1.  오른쪽 상단에 있는 **데이터 구성**을 클릭하십시오. 
1.  **데이터 구성** 화면에는 **필드 식별**, **필드 관리** 및 **필드 강화**의 세 가지 탭이 있습니다. 
1.  `Watson Explorer Installation Guide`가 표시되며 **필드 식별** 탭의 어노테이션에 대해 준비가 됩니다. 사용 가능한 모든 필드(`answer`, `author`, `footer`, `header`, `question`, `subtitle`, `table_of_contents`, `text` 및 `title`)는 오른쪽의 **필드 레이블** 목록에 표시됩니다. 고급 또는 프리미엄 플랜을 구입하는 경우 고유한 사용자 정의 레이블을 작성할 수 있습니다.

    전체 문서가 현재 `text`로 식별되므로 오른쪽의 마커는 노란색으로만 표시됩니다. 어노테이션을 작성할 때(또한 시스템에서 예측을 시작함) 색상이 업데이트됩니다
.{: tip}

1.  `title`을 클릭한 후 `Installation and Integration Guide` 옆에 있는 마커를 선택하십시오. **페이지 제출** 단추를 클릭하십시오.
1.  왼쪽의 페이지 미리보기에서 3페이지를 클릭하십시오. 이 페이지에서 `title`이 이미 예측되었습니다. **페이지 제출** 단추를 클릭하십시오.
1.  4페이지에서 `footer` 레이블을 선택하고 바닥글 옆에 있는 마커를 선택하십시오. **페이지 제출** 단추를 클릭하십시오.
1.  5페이지 및 6페이지에서 `footer` 레이블로 바닥글 어노테이션을 작성하십시오. 각 페이지를 제출하십시오. 추가로 몇 개의 페이지를 클릭하십시오. 바닥글이 {{site.data.keyword.discoveryshort}}를 통해 올바르게 예측되었음을 알게 됩니다. 7, 9, 10페이지에 있는 `title`(왼쪽 맞추기) 및 `subtitle`(들여쓰기) 어노테이션을 작성하고 각 페이지를 개별적으로 제출하십시오. 
1.  추가로 몇 개의 페이지를 클릭하고 예측된 제목 및 하위 제목을 확인하십시오. 변경해야 하는 경우 해당 페이의 어노테이션을 작성하고 **페이지 제출** 단추를 클릭하십시오. 
1.  이제 **필드 관리** 탭을 클릭하십시오. **문서를 분할하여 조회 결과 개선**을 통해 `subtitle`을 기반으로 한 문서가 분할됩니다.  
1.  현재로서는 더 이상 어노테이션을 작성할 필요가 없습니다. 오른쪽 상단에 있는 **콜렉션에 변경사항 적용** 단추를 클릭하십시오. **문서 업로드** 대화 상자가 표시됩니다. 원래의 `watsonexplorerinstall.pdf` 파일을 찾아보고 이 파일을 업로드하십시오. 이를 통해 모든 어노테이션이 인덱스에 적용합니다. 인덱싱이 완료되면 **개요** 화면이 열립니다. 이제 30개 이상의 문서와 데이터에서 식별된 4개의 필드(`footer`, `subtitle`, `text` 및 `title`)가 표시되어야 합니다. (변경사항이 몇 분 내에 표시되지 않으면 브라우저 창을 새로 고치십시오.)

    **필드 관리** 탭을 열고 해당 필드 `off`를 전환하여 인덱싱에서 필드(예: `footer`)를 제외할 수 있습니다.
    {: tip}

## 5단계: 조회
{: #build-a-query}

1.  오른쪽 맨 아래에 있는 **고유한 조회 빌드**를 클릭하십시오.
1.  **조회 빌드** 화면에서 **문서 검색**을 클릭한 후 **자연어 사용**을 클릭하십시오. `What are the minimum hardware requirements`를 입력하고 **조회 실행** 단추를 클릭하십시오.  
1.  오른쪽에 있는 **JSON** 탭을 클릭하십시오. `results` 아래에 있는 `text`를 살펴보십시오. 조회에 대해 리턴된 응답은 더욱 정확합니다. 

추가 리소스:
-  문서의 데이터 스키마에 대해 자세히 알아보려면 맨 왼쪽에 있는 **데이터 스키마 보기** 아이콘을 클릭하거나 **JSON** 탭을 클릭하십시오. 자세한 사항은 [Discovery 데이터 스키마](/docs/services/discovery?topic=discovery-query-concepts#discovery-schema)를 참조하십시오.
-  **샘플 조회 사용** 단추를 클릭하여 {{site.data.keyword.discoveryshort}} 조회 언어로 작성된 예제 조회를 시도해보십시오. 

## 다음 단계
{: #next-steps-tool}

이제 작동하며 채워진 {{site.data.keyword.discoveryshort}} 서비스 인스턴스가 제공됩니다. 이제 더 많은 문서와 인리치먼트를 추가하여 콜렉션 사용자 정의와 추가 문서 어노테이션 작성을 시작할 수 있습니다. 자세한 정보는 [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu)을 참조하십시오.
