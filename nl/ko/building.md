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

# 서비스 구성
{: #configservice}

{{site.data.keyword.discoveryshort}} 서비스를 빌드하면 고유한 데이터를 강화한 후 조회 가능 양식으로 전달하여 유용한 인사이트를 확보할 수 있습니다.
{: shortdesc}

고유한 컨텐츠를 {{site.data.keyword.discoveryshort}} 서비스에 추가하기 전에 원하는 방식으로 컨텐츠를 처리하기 위해 서비스를 구성해야 합니다.

첫 번째 단계는 서비스의 기본 매개변수 구성([문서에 대한 서비스 준비](/docs/services/discovery?topic=discovery-configservice#preparing-the-service-for-your-documents))이며 여기에는 환경 작성 및 해당 환경 내 하나 이상의 콜렉션 작성이 포함됩니다. 

[Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu) 도입 전에 콜렉션이 작성된 경우 하나 이상의 사용자 정의 구성을 지정하려고 할 수 있습니다([사용자 정의 구성이 필요한 경우](/docs/services/discovery?topic=discovery-configservice#when-you-need-a-custom-configuration) 참조). 해당 경우, 다음을 수행해야 합니다.

-   일부 샘플 컨텐츠(파일을 대표하는 문서) 식별
-   컨텐츠 업로드([샘플 문서 업로드](/docs/services/discovery?topic=discovery-configservice#uploading-sample-documents))
-   변환 프로세스 조정([샘플 문서 변환](/docs/services/discovery?topic=discovery-configservice#converting-sample-documents))
-   인리치먼트 정의([인리치먼트 추가](/docs/services/discovery?topic=discovery-configservice#adding-enrichments))
-   결과 정규화([데이터 정규화](/docs/services/discovery?topic=discovery-configservice#normalizing-data))

    사용자 정의 구성을 작성한 후 문서를 업로드([컨텐츠 추가](/docs/services/discovery?topic=discovery-addcontent#addcontent))할 수 있습니다.

## 문서에 대한 서비스 준비
{: #preparing-the-service-for-your-documents}

{{site.data.keyword.discoveryshort}} 서비스에서 업로드한 컨텐츠는 사용자의 환경의 일부인 콜렉션에 저장됩니다. 컨텐츠를 업로드하기 전에 환경 및 콜렉션을 작성해야 합니다.

-   **환경** — 환경은 {{site.data.keyword.discoveryshort}} 서비스에서 컨텐츠용으로 보유하고 있는 스토리지 공간의 크기를 정의합니다. {{site.data.keyword.discoveryshort}} 서비스의 각 인스턴스마다 최대 하나의 환경을 작성할 수 있습니다.

    선택할 수 있는 다양한 플랜(Lite, 고급, 프리미엄)이 있습니다. 세부사항은 [{{site.data.keyword.discoveryshort}} 카탈로그 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/catalog/services/discovery){: new_window} 및 [{{site.data.keyword.discoveryshort}} 가격 플랜](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)을 참조하십시오. 소스 파일은 플랜 크기 한계에 포함되지 않으며 인덱싱되는 변환된 JSON의 크기만 크기 한계에 포함됩니다.

-   **콜렉션** — 콜렉션은 환경에 있는 컨텐츠의 그룹입니다. 컨텐츠를 업로드할 수 있으려면 하나 이상의 콜렉션을 작성해야 합니다.

    콜렉션은 개인용 데이터로 구성되어 있으나 {{site.data.keyword.discoveryshort}}에는 사전 강화된 공용 데이터세트인 {{site.data.keyword.discoverynewsshort}}도 포함되어 있습니다. 

    코그너티브 인사이트로 사전 강화된 공용 데이터 세트인 {{site.data.keyword.discoverynewsshort}}는 {{site.data.keyword.discoveryshort}}에도 함께 포함되어 있습니다. 애플리케이션에 통합할 수 있도록 인사이트를 위한 조회에 이를 사용할 수 있습니다(예: 뉴스 알림, 이벤트 발견 및 뉴스의 인기 주제). 자세한 정보는 [Watson Discovery News](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news)를 참조하십시오. {{site.data.keyword.discoverynewsshort}} 구성을 조정하거나 이 콜렉션에 문서를 추가할 수 없습니다. [여기 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://discovery-news-demo.ng.bluemix.net/){: new_window}에서 {{site.data.keyword.discoverynewsshort}}를 사용하여 무엇을 빌드할 수 있는지에 대한 데모를 보십시오.

{{site.data.keyword.discoveryshort}} 도구를 사용하여 환경 및 개인용 데이터 콜렉션을 작성하려면 다음을 수행하십시오.

1.  **데이터 관리** 화면에서 오른쪽 상단에 있는 ![환경](images/icon_settings.png) 아이콘을 클릭하고 **환경 작성**을 선택하십시오. 환경은 이전에 선택한 {{site.data.keyword.Bluemix_notm}} 플랜에 따라 작성됩니다. 사용자 환경의 상태는 이 드롭 다운에서 언제든 확인할 수 있습니다.

1.  사용자 환경이 준비되면 **사용자 데이터 업로드** 단추를 클릭한 후 **새 콜렉션 이름 지정**을 수행할 수 있습니다.

     또한 이 콜렉션에 추가할 문서의 언어(영어, 독일어, 스페인어, 아랍어, 일본어, 프랑스어, 이탈리아어, 한국어 또는 브라질 포르투갈어)를 선택할 수 있습니다. 각 콜렉션마다 하나의 언어만 사용해야 합니다. **작성**을 클릭하면 데이터 콜렉션이 타일로 표시됩니다.

환경 및 데이터 콜렉션이 준비되었습니다! 즉시 [컨텐츠 추가](/docs/services/discovery?topic=discovery-addcontent#addcontent)를 시작할 수 있습니다.  

그러나 추가 인리치먼트 및 변환 설정을 사용하여 {{site.data.keyword.discoveryshort}} 구성을 사용자 정의하려는 경우 지금 문서 추가를 시작하지 말고 사용자 정의 구성 파일 작성을 시작해야 합니다. [서비스 구성](/docs/services/discovery?topic=discovery-configservice#custom-configuration)을 참조하십시오.

콜렉션이 [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu)을 사용하여 작성된 경우 {{site.data.keyword.discoveryshort}} 도구를 사용하여 인리치먼트를 조정하는 것을 선호할 수 있습니다.
{: note}

Smart Document Understanding 릴리스 전에 작성된 콜렉션의 경우 문서가 데이터 콜렉션에 업로드되면 해당 콜렉션에 대해 선택한 구성 파일을 사용하여 문서가 변환되고 강화됩니다. 나중에 구성 파일을 변경하도록 결정하는 경우 이를 수행할 수 있지만 이미 업로드한 문서는 원래 구성에 의해 변환된 상태로 유지됩니다. 구성 파일을 전환한 후 업로드된 모든 문서는 새 구성 파일을 사용합니다. **전체** 콜렉션에서 새 구성 파일을 사용하려면 새 콜렉션을 작성하고 새 구성 파일을 선택한 다음 모든 문서를 다시 업로드해야 합니다. {{site.data.keyword.discoveryshort}} 서비스에서는 업로드하는 문서의 변환된 텍스트를 저장하며, **PDF** 및 **Microsoft Word** 파일에 있는 임베드된 이미지는 저장되지 않고 결과에 리턴되지 않습니다. 콜렉션이 [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu)을 사용하는 경우 **콜렉션에 변경사항 적용** 단추를 클릭하면 {{site.data.keyword.discoveryshort}}에서 인리치먼트 및 변환에 대해 수행된 변경사항이 전체 콜렉션에 적용됩니다. 대형 콜렉션의 경우 변경사항을 적용하는 데 다소 시간이 걸릴 수 있습니다.   
{: important}

{{site.data.keyword.discoveryshort}} 도구 또는 API를 사용하여 Box, Salesforce, Microsoft SharePoint Online, IBM Cloud Object Storage 및 Microsoft SharePoint 2016 데이터 소스를 크롤링하거나 웹 크롤링을 수행할 수 있습니다. 자세한 정보는 [데이터 소스에 연결](/docs/services/discovery?topic=discovery-sources#sources)을 참조하십시오.
{: tip}

### 기본 구성
{: #the-default-configuration}

{{site.data.keyword.discoveryshort}} 서비스에는 이 옵션을 수동으로 구성할 필요 없이 데이터를 변환, 강화 및 정규화하는 표준 구성이 포함되어 있습니다.

**기본 구성** 파일은 [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu) 릴리스 전에 작성된 콜렉션에만 사용할 수 있습니다. 그러나 Smart Document Understanding을 사용하는 경우 기본적으로 동일한 인리치먼트와 HTML 및 JSON 변환이 콜렉션에 사용됩니다.
{: note}

콜렉션을 작성하는 경우 {{site.data.keyword.discoveryshort}}는 네 개의 {{site.data.keyword.watson}} 인리치먼트 즉, 엔티티 추출, 감성 분석, 카테고리 분류 및 개념 태그 지정으로 수집된 시맨틱 정보로 문서의 `text` 필드를 강화하거나 코그너티브 메타데이터를 해당 텍스트 필드에 추가합니다(자세한 사항은 [여기](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)를 클릭). 글꼴 스타일 및 크기에 따른 표준 문서 변환도 적용됩니다. **개요** 탭을 사용하여 인리치먼트를 나중에 조정할 수 있습니다. (이 구성은 [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu) 릴리스 전에 작성된 콜렉션에서 **기본 구성**이라는 이름으로 지정되었습니다.)

기본 변환:

-   [Microsoft Word 변환](/docs/services/discovery?topic=discovery-configservice#microsoft-word-conversion)
-   [PDF 변환](/docs/services/discovery?topic=discovery-configservice#pdf-conversion)
-   [HTML 변환](/docs/services/discovery?topic=discovery-configservice#html-conversion)
-   [JSON 변환](/docs/services/discovery?topic=discovery-configservice#json-conversion)

**기본 계약 구성**이라는 구성은 {{site.data.keyword.discoveryshort}} 도구로 콜렉션을 작성할 때 사용할 수 있습니다. 이는 PDF의 요소에서 당사자, 네이처 및 카테고리를 추출하는 데 사용할 수 있는 요소 분류를 강화하도록 구성되어 있습니다. 세부사항은 [요소 분류](/docs/services/discovery?topic=discovery-element-classification#element-collection)를 참조하십시오. Smart Document Understanding은 이 구성 파일이 사용되는 경우 사용 불가능합니다. 

[Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu) 릴리스 전에 작성된 콜렉션에 대해 사용자 정의 구성을 작성할 경우 [사용자 정의 구성](/docs/services/discovery?topic=discovery-configservice#custom-configuration)을 참조하십시오.

### 사용자 정의 구성이 필요한 경우
{: #when-you-need-a-custom-configuration}

이 정보는 [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu) 릴리스 전에 작성된 콜렉션에만 적용됩니다.
{: note}

{{site.data.keyword.discoveryshort}} 서비스의 목적은 컨텐츠에서 올바른 정보를 가져와서 이 정보를 사용자에게 리턴하는 것입니다. 이 정보가 무엇이며, 컨텐츠에 어떻게 저장되는지를 식별하는 것은 컨텐츠를 수집하기 위해 사용하는 구성에 의해 정의됩니다. {{site.data.keyword.discoveryshort}} 서비스가 수집할 수 있는 컨텐츠 유형은 유연합니다. 이는 구조화되지 않은 컨텐츠가 특정 형식으로 저장되는 경우에도 컨텐츠의 구조가 유형이 같은 기타 컨텐츠의 구조와 일치할 필요가 없음을 의미합니다.

-   **내 문서가 기본 구성에서 예상하는 방식으로 구조화되지 않을 수 있다는 점을 알고 있습니다. *기본 설정이 적합한지
    알 수 있는 방법은 무엇입니까?***
    -   기본값이 사용자에게 적합한지 여부를 확인하는 가장 쉬운 방법은 [샘플 문서 업로드](/docs/services/discovery?topic=discovery-configservice#uploading-sample-documents)를 통해 테스트하는 것입니다. 샘플 JSON 결과가 기대를 충족시키면 추가 구성이 필요하지 않습니다.
-   **기본 인리치먼트가 내 문서의 텍스트 필드에 추가된다는 점을 알고 있습니다. 추가 인리치먼트를 기타 필드에 추가할 수 있습니까?**
    -   물론입니다. 원하는 만큼의 필드에 추가 인리치먼트를 추가할 수 있습니다. 자세한 사항은 [인리치먼트 추가](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)를 참조하십시오.

## 사용자 정의 구성
{: #custom-configuration}

이 정보는 [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu) 릴리스 전에 작성된 콜렉션에만 적용됩니다.
{: note}

{{site.data.keyword.discoveryshort}} 도구에 사용자 정의 구성을 작성하려면 개인용 데이터 콜렉션을 열고 **데이터 관리** 화면에서 사용자 **구성**의 이름 옆에 있는 **전환**을 클릭하십시오. **구성 전환** 대화 상자에서 **새 구성 작성**을 클릭하십시오.

새 구성 파일의 이름을 지정한 후, 이름이 구성 화면의 맨 위에 표시됩니다. 이 새 구성 파일은 자동으로 [기본 구성](/docs/services/discovery?topic=discovery-configservice#the-default-configuration) 파일의 설정 및 인리치먼트를 포함하여 시작할 위치를 제공합니다.

구성 파일을 사용자 정의하는 세 가지 단계는 **변환**, **강화** 및 **정규화**입니다.

1.  [샘플 문서 변환](/docs/services/discovery?topic=discovery-configservice#converting-sample-documents)
1.  [인리치먼트 추가](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)(이 탭은 Smart Document Configuration 사용 시 사용 가능합니다.)
1.  [데이터 정규화](/docs/services/discovery?topic=discovery-configservice#normalizing-data)

구성에 대한 자세한 정보는 [구성 참조](/docs/services/discovery?topic=discovery-configref#configref)를 참조하십시오.

### 샘플 문서 업로드
{: #uploading-sample-documents}

이 정보는 [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu) 릴리스 전에 작성된 콜렉션에만 적용됩니다.
{: note}

구성 프로세스를 좀 더 효율적으로 만들기 위해 사용자의 문서 세트를 대표하는 최대 10개의 Microsoft Word, HTML, JSON 또는 PDF 파일을 업로드할 수 있습니다. 이를 **샘플 문서**라고 합니다. 샘플 문서는 콜렉션에 추가되지 않습니다. 즉, 문서에 공통인 필드를 식별하고 요구사항에 맞게 이 필드를 사용자 정의하는 용도로만 샘플 문서를 사용합니다.

{{site.data.keyword.discoveryshort}} 도구에서 새 구성을 작성하는 경우 끌어서 놓기 또는 찾아보기를 통해 샘플 문서를 업로드할 수 있습니다. 각 파일을 미리보려면 **샘플 문서 업로드** 분할창에서 파일 이름을 클릭하십시오.

#### 샘플 문서를 업로드할 때 다음 항목을 기억하십시오.

-   모든 문서는 강화되고 인덱싱되기 전에 JSON으로 변환됩니다.
-   Microsoft Word 및 PDF 문서는 먼저 HTML로 변환된 후 JSON으로 변환됩니다.
-   HTML 문서는 JSON으로 직접 변환됩니다.
-   샘플 문서의 최대 파일 크기는 1MB입니다. 샘플 문서는 브라우저의 로컬 로밍 데이터 폴더에 저장됩니다. 샘플 문서를 삭제하려면 **삭제** 아이콘을 클릭하십시오.

#### 양질의 샘플 문서를 선택하기 위한 가이드라인

-   수집할 각 파일 유형(Microsoft Word, PDF, HTML 및 JSON)마다 (최소) 하나의 샘플 문서가 있어야 합니다. (**요소 분류** 인리치먼트를 사용하여 강화된 PDF 문서를 미리볼 수 없습니다.)
-   고유한 문서 유형(예: 재무 보고서 또는 보도 자료)이 있으면 샘플 문서의 각 세트마다 하나씩 포함하십시오.
-   HTML 문서의 경우 제외할 HTML 태그 및 포함하거나 제외할 태그 속성을 포함하는 문서를 선택해야 합니다.
-   JSON 문서는 함께 제거하거나 병합할 모든 필드를 포함해야 합니다(예: zipCode와 postalCode).

### 샘플 문서 변환
{: #converting-sample-documents}

이 정보는 [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu) 릴리스 전에 작성된 콜렉션에만 적용됩니다.
{: note}

샘플 문서 변환은 각 입력 유형을 처리하는 방법을 정의할 수 있는 프로세스입니다. 업로드한 컨텐츠의 파일 유형은 사용자가 고려해야 하는 변환 단계의 수에 영향을 줍니다.

시작하기 전에 [샘플 문서 업로드](/docs/services/discovery?topic=discovery-configservice#uploading-sample-documents)를 수행하고 오른쪽의 분할창에서 구성할 파일 유형의 샘플 문서를 여십시오.

변환 설정을 통해 작업하려면 파일 유형을 클릭하십시오.

![샘플 문서 변환](images/convert.png)

-   **Microsoft Word 파일을 변환하는 경우 다음을 수행해야 합니다. **
    -   Microsoft Word 변환 옵션 설정
    -   HTML 변환 옵션 설정
    -   JSON 변환 옵션 설정
    -   결과 검토

-   **PDF 파일을 변환하는 경우 다음을 수행해야 합니다. **
    -   PDF 변환 옵션 설정
    -   HTML 변환 옵션 설정
    -   JSON 변환 옵션 설정
    -   결과 검토

-   **HTML 파일을 변환하는 경우 다음을 수행해야 합니다. **
    -   HTML 변환 옵션 설정
    -   JSON 변환 옵션 설정
    -   결과 검토

-   **JSON 파일을 변환하는 경우** JSON 변환 옵션을 설정하고 결과를 검토해야 합니다.

작성한 각 구성 파일에 대해 프로세스의 각 단계마다 하나의 변환 옵션 세트만 있습니다. 이는 HTML 변환 옵션이 PDF 파일, Word 파일 및 HTML에서 동일함을 의미합니다. 수집하는 각 컨텐츠 유형마다 다른 변환 옵션이 필요한 경우(또는 다른 변환 유형이 필요한 같은 유형의 파일이 있는 경우) 다른 콜렉션에 파일을 저장하고 변환 설정의 각 세트마다 개별 구성 파일을 작성해야 합니다.

#### Microsoft Word 변환
{: #microsoft-word-conversion}

Microsoft Word 글꼴 크기 및 글꼴 스타일은 문서의 표제를 H1, H2 등으로 적절하게 변환하는 데 사용됩니다. H1은 문서의 제목이고 H2 이하는 하위 표제입니다. 원하는 경우 텍스트 상자 및 단일 선택 단추를 사용하여 기본 설정을 변경하십시오. 또한 추가 표제 레벨 및 Word 스타일도 추가할 수 있습니다. Word 문서가 표제에 특정 글꼴 또는 스타일 이름을 사용하는 경향이 있는 경우 해당 정보를 추가해야 합니다. 이를 통해 변환이 개선되어 더 나은 조회 결과가 생성됩니다.

**예:** Word 문서에서 표제 2에 기울임체의 20pt 글꼴을 사용하는 것이 일반적인 경우 **글꼴 크기 범위**를 **20**에서 **23**으로, **글꼴 스타일**을 **기울임체**로 변경하십시오.

변경한 후에는 **적용 및 저장**을 클릭하십시오.

#### PDF 변환
{: #pdf-conversion}

PDF 글꼴 크기 및 글꼴 이름은 문서의 표제를 H1, H2 등으로 적절하게 변환하는 데 사용됩니다. H1은 문서의 제목이고 H2 이하는 하위 표제입니다. 원하는 경우 텍스트 상자 및 단일 선택 단추를 사용하여 기본 설정을 변경하십시오. 또한 추가 표제 레벨도 추가할 수 있습니다. PDF 문서가 표제에 특정 글꼴을 사용하는 경향이 있는 경우 해당 정보를 추가해야 합니다. 이를 통해 변환이 개선되어 더 나은 조회 결과가 생성됩니다.

**예:** PDF 문서에서 표제 2에 기울임체의 20pt 글꼴을 사용하는 것이 일반적인 경우 **글꼴 크기 범위**를 **20**에서 **80**으로, **글꼴 스타일**을 **기울임체**로 변경하십시오. 다른 레벨을 적절하게 조정하십시오.

변경한 후에는 **적용 및 저장**을 클릭하십시오.

#### HTML 변환
{: #html-conversion}

이 단계를 사용하여 조회에 필요한 정보만 보유하도록 필요하지 않은 태그 및 기타 문서 정보를 제거할 수 있습니다.

기본 HTML 설정:

- 이 태그 및 해당 컨텐츠 제외: **`script`**, **`sup`**
- 이 태그를 제외하지만 해당 컨텐츠 유지: **`font`**, **`em`**, **`span`**
- 이 태그 속성 유지: 기본값 없음
- 이 태그 속성 제외: **`EVENT_ACTIONS`**
- 이 XPath와 일치하는 컨텐츠 유지: 기본값 없음
- 이 XPath와 일치하는 컨텐츠 제외: 기본값 없음

변경한 후에는 **적용 및 저장**을 클릭하십시오.

#### JSON 변환
{: #json-conversion}

변환의 마지막 단계는 인리치먼트가 컨텐츠에 적용되기 전에 변환된(또는 업로드된) JSON이 예상된 방식으로 구성되는지 확인하는 것입니다. {{site.data.keyword.watson}}이 HTML에서 JSON으로 변환하는 데 사용하는 규칙을 작성할 수 있습니다.

-   필드를 이동, 병합, 복사 또는 제거할 수 있습니다. 예를 들어, **`zipCode`**와 **`postalCode`**는 같은 필드에 대한 두 가지 유사한 용어이므로 이를 병합하려고 할 수 있습니다.
-   비어 있는 필드(정보가 없는 필드)는 기본적으로 삭제됩니다. **비어 있는 필드 제거** 토글을 사용하여 이를 변경할 수 있습니다.

변경한 후에는 **적용 및 저장**을 클릭하십시오.

## 인리치먼트 추가
{: #adding-enrichments}

 {{site.data.keyword.discoveryshort}} [기본 구성](/docs/services/discovery?topic=discovery-configservice#the-default-configuration)은 네 개의 {{site.data.keyword.watson}} 기능 즉, 엔티티 추출, 감성 분석, 카테고리 분류 및 개념 태그 지정으로 수집된 시맨틱 정보로 문서의 `text` 필드를 강화하거나 코그너티브 메타데이터를 해당 텍스트 필드에 추가합니다. (총 아홉 개의 {{site.data.keyword.watson}} 인리치먼트가 사용 가능하며, 나머지 인리치먼트는 키워드 추출, 관계 추출, 감정 분석, 요소 분류 및 시맨틱 역할 추출입니다.)

일부 {{site.data.keyword.watson}} 인리치먼트는 특정 플랜또는 환경에서 사용 가능하지 않을 수 있습니다.

{{site.data.keyword.knowledgestudiofull}}의 하나 이상의 사용자 정의 모델을 {{site.data.keyword.discoveryshort}} 서비스와 통합하여 사용자 정의 엔티티와 관계 인리치먼트도 제공할 수 있습니다. [Watson Knowledge Studio와 통합](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-with-wks)을 참조하십시오.

인리치먼트에 선택된 각 JSON 필드의 처음 50,000자만 강화됩니다.
{: important}

**참고:** {{site.data.keyword.alchemylanguageshort}} 인리치먼트는 2018년 3월 1일부터 더 이상 사용되지 않습니다. {{site.data.keyword.alchemylanguageshort}} 인리치먼트를 사용하는 기존 콜렉션을 가지고 있는 경우 {{site.data.keyword.nlushort}} 인리치먼트로 마이그레이션해야 합니다. {{site.data.keyword.alchemylanguageshort}} 인리치먼트를 활용하는 기존 콜렉션 및 구성 파일의 마이그레이션에 대한 정보는 [{{site.data.keyword.nlushort}}으로 인리치먼트 마이그레이션](/docs/services/discovery?topic=discovery-migrate-nlu#migrate-nlu)을 참조하십시오.

추가 인리치먼트를 `text` 필드에 추가하거나 기타 필드를 강화하여 문서를 좀 더 보강할 수 있습니다. {{site.data.keyword.discoveryshort}} 도구에서 Smart Document Understanding을 사용하여 이를 수행하려면 **필드 강화** 탭을 여십시오. Smart Document Understanding 전에 작성된 콜렉션에 대해 이를 수행하려면 [사용자 정의 구성 작성](/docs/services/discovery?topic=discovery-configservice#custom-configuration)을 수행하고, 강화하려는 필드를 선택하여 사용 가능한 {{site.data.keyword.nlushort}} 인리치먼트 목록에서 선택하십시오.

### 엔티티 추출
{: #entity-extraction}

입력 텍스트에 있는 개인, 위치 및 조직과 같은 항목을 리턴합니다. 엔티티 추출은 시맨틱 정보를 컨텐츠에 추가하여 분석 중인 텍스트의 주제 및 컨텍스트를 이해하는 데 도움을 줍니다. 엔티티 추출 기술은 정교한 통계 알고리즘 및 자연어 처리 기술을 기반으로 하며 다국어 분석 및 컨텍스트에 따른 모호성 제거에 대한 지원으로 업계에서 독보적인 기술입니다. [여기](/docs/services/discovery?topic=discovery-entity-types-and-subtypes#entity-types-and-subtypes)에서 엔티티 유형 및 하위 유형의 전체 목록을 보십시오. 또한 {{site.data.keyword.knowledgestudiofull}}를 사용하여 [사용자 정의 엔티티 모델](/docs/services/discovery?topic=discovery-configservice#custom-entity-model)을 작성하고 추가할 수도 있습니다.

엔티티 추출을 사용하여 강화된 문서의 일부 예제:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
    "entities": [
    {
        "count": 1,
           "sentiment": {
          "score": 0
        },
           "text": "Acme Corporation",
           "relevance": 0.98389,
           "type": "Company"
      },
      {
        "count": 1,
           "sentiment": {
          "score": 0
        },
           "text": "Atlanta",
           "relevance": 0.532754,
           "type": "Location",
           "disambiguation": {
          "subtype": [
            "AdministrativeDivision",
               "GovernmentalJurisdiction",
               "OlympicHostCity",
               "PlaceWithNeighborhoods",
               "City"
          ],
               "name": "Atlanta",
               "dbpedia_resource": "http://dbpedia.org/resource/Atlanta"
           }
      },
      {
        "count": 1,
           "sentiment": {
          "score": 0
        },
           "text": "Georgia",
           "relevance": 0.469643,
           "type": "Location",
           "disambiguation": {
          "subtype": [
            "StateOrCounty"
           ]
        }
      }
    ]
  }
}
```
{: codeblock}

이전 예에서는 `enriched_text.entities.type`에 액세스하여 엔티티 유형을 조회할 수 있었습니다.

`sentiment`는 **sentiment** 인리치먼트가 선택되지 않은 경우에도 엔티티 유형에 대해 계산됩니다. 감성 스코어링에 대해 자세히 알아보려면 [감성 분석](/docs/services/discovery?topic=discovery-configservice#sentiment-analysis)을 참조하십시오.

`relevance` 스코어의 범위는 `0.0` - `1.0`입니다. 스코어가 높을수록 엔티티 관련성이 높아집니다. `disambiguation` 필드에는 엔티티에 대한 모호성 제거 정보가 포함되며, 엔티티 `subtype` 정보를 포함하고 리소스에 연결합니다(해당 경우). `count`는 엔티티가 문서에 언급된 횟수입니다.

#### 사용자 정의 엔티티 모델 사용
{: #custom-entity-model}

사용자 정의 인리치먼트 모델을 작성하려는 경우 {{site.data.keyword.knowledgestudiofull}}에서 이를 수행할 수 있으며 {{site.data.keyword.discoveryshort}} 도구의 `Custom Model ID` 상자에 ID를 추가하여 모델을 {{site.data.keyword.discoveryshort}}로 가져올 수 있습니다. {{site.data.keyword.knowledgestudiofull}}와의 통합에 대한 자세한 정보는 [{{site.data.keyword.knowledgestudiofull}}와 통합](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-with-wks)을 참조하십시오. 사용자 정의 {{site.data.keyword.knowledgestudiofull}} 모델은 기본 엔티티 추출 인리치먼트를 대체합니다.

**참고:** 인리치먼트에 하나의 {{site.data.keyword.knowledgestudiofull}} 모델만 지정할 수 있습니다.

### 관계 추출
{: #relation-extraction}

두 개의 엔티티가 관련되는 시점을 인식하고 관계의 유형을 식별합니다. 또한 {{site.data.keyword.knowledgestudiofull}}를 사용하여 [사용자 정의 관계 모델](/docs/services/discovery?topic=discovery-configservice#custom-relation-model)을 작성하고 추가할 수도 있습니다.

[여기](/docs/services/discovery?topic=discovery-relation-types#relation-types)에서 관계 유형의 전체 목록을 보십시오.

관계 추출을 사용하여 강화된 문서의 일부 예제:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
    "relations": [
      {
        "type": "locatedAt",
        "sentence": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
        "score": 0.989245,
        "arguments": [
         {
            "text": "Atlanta",
            "location": [
             94,
             101
            ],
            "entities": [
              {
                "type": "GeopoliticalEntity",
                "text": "Atlanta"
              }
            ]
         },
          {
            "text": "Georgia",
            "location": [
             103,
             110
            ],
            "entities": [
              {
                "type": "GeopoliticalEntity",
                "text": "Georgia"
              }
            ]
          }
        ]
      }
    ]
  }
}
```
{: codeblock}

이전 예에서는 `enriched_text.relations.type`에 액세스하여 관계 유형을 조회할 수 있었습니다.

관련 엔티티가 `arguments`에 나열됩니다. 관계 추출 인리치먼트로 식별될 수 있는 엔티티 유형을 [여기](/docs/services/discovery?topic=discovery-relation-types#specific-entity-types)에서 찾을 수 있습니다.

`score` 범위는 `0.0` - `1.0`입니다. 스코어가 높을수록 관계 관련성이 높아집니다.

#### 사용자 정의 관계 모델 사용
{: #custom-relation-model}

사용자 정의 인리치먼트 모델을 작성하려는 경우 {{site.data.keyword.knowledgestudiofull}}에서 이를 수행할 수 있으며 {{site.data.keyword.discoveryshort}} 도구의 `Custom Model ID` 상자에 ID를 추가하여 모델을 {{site.data.keyword.discoveryshort}}로 가져올 수 있습니다. {{site.data.keyword.knowledgestudiofull}}와의 통합에 대한 자세한 정보는 [{{site.data.keyword.knowledgestudiofull}}와 통합](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-with-wks)을 참조하십시오. 사용자 정의 {{site.data.keyword.knowledgestudiofull}} 모델은 기본 관계 추출 인리치먼트를 대체합니다.

**참고:** 인리치먼트에 하나의 {{site.data.keyword.knowledgestudiofull}} 모델만 지정할 수 있습니다.

### 키워드 추출
{: #keyword-extraction}

데이터를 인덱싱하거나 태그 클라우드를 생성하거나 검색할 때 일반적으로 사용되는 컨텐츠의 중요 주제입니다. {{site.data.keyword.discoveryshort}} 서비스는 자동으로 입력 컨텐츠에서 지원되는 언어를 식별한 후 해당 컨텐츠에서 키워드를 식별하고 순위를 지정합니다.

키워드 추출을 사용하여 강화된 문서의 일부 예제:

```json
  {
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "keywords": [
        {
          "text": "Acme Corporation",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.985203
        },
        {
          "text": "new factory",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.821033
        },
        {
          "text": "stockholders",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.66497
        },
        {
          "text": "title",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.332438
        },
        {
          "text": "Atlanta",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.307723
        },
        {
          "text": "Georgia",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.306485
        }
      ]
    }
  }
```
{: codeblock}

이전 예에서는 `enriched_text.keywords.text`에 액세스하여 키워드 텍스트를 조회할 수 있었습니다.

`sentiment`는 **sentiment** 인리치먼트가 선택되지 않은 경우에도 키워드에 대해 계산됩니다. 감성 스코어링에 대해 자세히 알아보려면 [감성 분석](/docs/services/discovery?topic=discovery-configservice#sentiment-analysis)을 참조하십시오.

`relevance` 스코어의 범위는 `0.0` - `1.0`입니다. 스코어가 높을수록 키워드 관련성이 높아집니다.

### 카테고리 분류
{: #category-classification}

입력 텍스트, HTML 또는 웹 기반 컨텐츠를 최대 다섯 개 레벨의 계층 구조 택소노미로 분류합니다. 레벨이 세분화될수록 컨텐츠를 좀 더 정확하고 유용한 하위 세그먼트로 분류할 수 있습니다. [여기](/docs/services/discovery?topic=discovery-cathierarchy#cathierarchy)에서 카테고리의 전체 목록을 보십시오.

카테고리 분류를 사용하여 강화된 문서의 일부 예제:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "categories": [
        {
          "score": 0.361614,
          "label": "/business and industrial"
        },
        {
          "score": 0.329377,
          "label": "/business and industrial/company/merger and acquisition"
        },
        {
          "score": 0.154254,
          "label": "/business and industrial/business operations/business plans"
        }
      ]
```
{: codeblock}

이전 예에서는 `enriched_text.categories.label`에 액세스하여 카테고리 레이블을 조회할 수 있었습니다.

`label`은 발견된 카테고리입니다. 계층 구조 레벨은 슬래시로 구분됩니다. 해당 카테고리에 대한 `score`의 범위는 `0.0` - `1.0`입니다. 스코어가 높을수록 해당 카테고리의 신뢰도가 높아집니다.

### 개념 태그 지정
{: #concept-tagging}

해당 텍스트에 있는 기타 개념 및 엔티티를 기반으로 입력 텍스트가 연관되는 개념을 식별합니다. 개념 태그 지정에서 개념이 관련되는 방식을 이해하고 텍스트에서 직접 참조되지 않는 개념을 식별할 수 있습니다. 예를 들어, 기사에서 CERN 및 Higgs 입자를 언급한 경우 개념 API 기능은 해당 용어가 페이지에 명시적으로 언급되지 않은 경우에도 개념으로 Large Hadron Collider를 식별합니다. 개념 태그 지정을 사용하면 단지 기본적인 키워드 식별이 아닌 입력 컨텐츠에 대한 좀더 상위 레벨의 분석을 할 수 있습니다.

개념 태그 지정을 사용하여 강화된 문서의 일부 예제:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "concepts": [
        {
          "text": "Acme Corporation",
          "relevance": 0.91136,
          "dbpedia_resource": "http://dbpedia.org/resource/Acme_Corporation"
        },
        {
          "text": "Factory",
          "relevance": 0.886784,
          "dbpedia_resource": "http://dbpedia.org/resource/Factory"
        }
      ]
```
{: codeblock}

이전 예에서는 `enriched_text.concepts.text`에 액세스하여 개념 텍스트 유형을 조회할 수 있었습니다.

`relevance` 스코어의 범위는 `0.0` - `1.0`입니다. 스코어가 높을수록 개념 관련성이 높아집니다. 리소스에 대한 링크가 제공됩니다(해당 경우).

### 시맨틱 역할 추출
{: #semantic-role-extraction}

입력 컨텐츠에서 문장 내 주체(subject), 동작(action) 및 객체(object) 간의 관계를 식별합니다. 구매 신호, 키 이벤트 및 기타 중요 동작을 자동으로 식별하기 위해 관계 정보를 사용할 수 있습니다.

시맨틱 역할 추출을 사용하여 강화된 문서의 일부 예제:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
      "enriched_text": {
      "semantic_roles": [
        {
          "subject": {
            "text": "The stockholders",
            "keywords": [
              {
                "text": "stockholders"
              }
            ]
          },
          "sentence": " The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
          "object": {
            "text": "pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia",
            "keywords": [
              {
                "text": "Acme Corporation"
              },
              {
                "text": "new factory"
              },
              {
                "text": "Atlanta"
              },
              {
                "text": "Georgia"
              }
            ],
            "entities": [
              {
                "type": "Company",
                "text": "Acme Corporation"
              },
              {
                "type": "Location",
                "text": "Atlanta",
                "disambiguation": {
                  "subtype": [
                    "AdministrativeDivision",
                    "GovernmentalJurisdiction",
                    "OlympicHostCity",
                    "PlaceWithNeighborhoods",
                    "CityTown",
                    "City"
                  ],
                  "name": "Atlanta",
                  "dbpedia_resource": "http://dbpedia.org/resource/Atlanta"
                }
              },
              {
                "type": "Location",
                "text": "Georgia",
                "disambiguation": {
                  "subtype": [
                    "StateOrCounty"
                  ]
                }
              }
            ]
          },
          "action": {
            "verb": {
              "text": "be",
              "tense": "past"
            },
            "text": "were",
            "normalized": "be"
          }
        }
      ]
```
{: codeblock}

이전 예에서는 `enriched_text.relations.subject.text`에 액세스하여 관계의 주체(subject) 텍스트를 조회할 수 있었습니다.

`sentiment`는 **sentiment** 인리치먼트가 선택되지 않은 경우에도 관계에 대해 계산됩니다. 감성 스코어링에 대해 자세히 알아보려면 [감성 분석](/docs/services/discovery?topic=discovery-configservice#sentiment-analysis)을 참조하십시오. **entity** 및 **keyword** 인리치먼트도 선택하지 않으면 예에 표시된 대로 `entities` 또는 `keywords`를 추출하지 않습니다. 해당 인리치먼트에 대한 자세한 정보는 [엔티티 추출](/docs/services/discovery?topic=discovery-configservice#entity-extraction) 및 [키워드 추출](/docs/services/discovery?topic=discovery-configservice#keyword-extraction)을 참조하십시오.

관계를 포함한 모든 문장마다 `subject`, `action` 및 `object`가 추출됩니다.

### 감성 분석
{: #sentiment-analysis}

분석 중인 컨텐츠에서 태도, 의견 또는 감정을 식별합니다. {{site.data.keyword.discoveryshort}} 서비스는 문서 내의 전체 감성, 사용자 지정 대상에 대한 감성, 엔티티 레벨 감성, 인용 레벨 감성, 방향 레벨 감성 및 키워드 레벨 감성을 계산할 수 있습니다. 이러한 기능의 조합은 소셜 미디어 모니터링부터 경향 분석까지의 다양한 유스 케이스를 지원합니다.

감성 분석을 사용하여 강화된 문서의 일부 예제:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "sentiment": {
        "document": {
        "score": 0.459813,
        "label": "positive"
  }
}
```
{: codeblock}

이전 예에서는 `enriched_text.sentiment.document.label`에 액세스하여 감성 레이블을 조회할 수 있었습니다.

`label`은 문서의 전체 감성입니다(`positive`, `negative` 또는 `neutral`). 감성 `label`은 `score`를 기반으로 합니다. `0.0`의 스코어는 문서가 `neutral`임을 나타내고 양수는 문서가 `positive`임을 나타내며 음수는 문서가 `negative`임을 나타냅니다.

### 감정 분석
{: #emotion-analysis}

영문 텍스트에서 암시되는 분노, 혐오, 공포, 기쁨 및 슬픔을 발견합니다. 감정 분석은 대상 구문, 엔티티 또는 키워드와 연관된 감정을 발견하거나 컨텐츠의 전반적인 감정적 어조를 분석할 수 있습니다.

감정 분석을 사용하여 강화된 문서의 일부 예제:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "emotion": {
        "document": {
          "emotion": {
          "disgust": 0.102578,
          "joy": 0.626655,
          "anger": 0.02303,
          "fear": 0.018884,
          "sadness": 0.096802
    }
  }
}
```
{: codeblock}

이전 예에서는 `enriched_text.emotion.document.emotion.joy`에 액세스하여 `joy` 감정을 조회할 수 있었습니다.

감정 분석은 텍스트를 분석하고 `0.0` - `1.0`의 범위로 각 감정(분노, 혐오, 공포, 기쁨, 슬픔)의 스코어를 계산합니다. 감정의 스코어가 `0.5` 이상이면 해당 감정이 발견됩니다(`0.5` 이상으로 스코어가 높을수록 관련성이 높아짐). 표시된 스니펫에서 `joy`의 스코어가 0.5 이상이므로 {{site.data.keyword.watson}}에서 기쁨(joy)을 발견했습니다.

**참고:** 감정 분석은 영어에서만 지원됩니다.

### 요소 분류
{: #elements}

운영 문서의 요소(문장, 목록, 표)를 구문 분석하여 중요 유형 및 카테고리를 분류합니다.
자세한 정보는 [요소 분류](/docs/services/discovery?topic=discovery-element-classification#element-classification)를 참조하십시오.

이 인리치먼트가 사용되면 [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu)은 사용할 수 없습니다.

#### 인리치먼트 가격
{: #enrichment-pricing}

인리치먼트 가격에 대한 정보는 [{{site.data.keyword.Bluemix_notm}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/catalog/services/discovery){: new_window}에서 확인할 수 있습니다.

#### 인리치먼트 언어 지원
{: #enrichment-language-support}

인리치먼트 언어 지원에 대한 자세한 정보는 [{{site.data.keyword.discoveryshort}} 언어 지원](/docs/services/discovery?topic=discovery-language-support#language-support)을 참조하십시오.

### 엔티티, 개념 및 키워드 간의 차이점 이해
{: #udbeck}

언뜻 보면 **엔티티 추출**, **개념 태그 지정** 및 **키워드 추출**은 유사한 인리치먼트로 보입니다. 인리치먼트 예제의 텍스트를 사용하여 해당 차이점을 표시할 것입니다.

```json
"text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia."
```
{: codeblock}

**엔티티 추출** 인리치먼트가 입력 텍스트에서 개인, 위치 및 조직을 추출하므로 **엔티티 추출**은 다음 엔티티 유형을 리턴합니다.

```json
"type": "City"
"text": "Atlanta"

"type": "Company"
"text": "Acme"

"type": "StateOrCounty"
"text": "Georgia"
```
{: codeblock}

**개념 태그 지정** 인리치먼트에서 개념이 관련되는 방식을 이해하고 텍스트에서 직접 참조되지 않는 개념을 식별할 수 있습니다. 예를 들어, 기사에서 CERN 및 Higgs 입자를 언급한 경우 해당 용어가 페이지에 명시적으로 언급되지 않은 경우에도 개념으로 Large Hadron Collider를 식별합니다. 문서 텍스트 예제가 단 하나의 문장이기 때문에 관련된 개념이 없습니다. 그러므로 **개념 태그 지정**은 다음 개념을 리턴합니다.

```json
"text": "Acme Corporation"
"text": "factory"
```
{: codeblock}

**키워드 추출** 인리치먼트가 데이터를 인덱싱하거나 태그 클라우드를 생성하거나 검색할 때 일반적으로 사용되는 컨텐츠를 식별하므로 **키워드 추출**은 다음 키워드를 리턴합니다.

```json
"text": "Acme Corporation"
"text": "new factory"
"text": "stockholders"
"text": "Atlanta"
"text": "Georgia"
```
{: codeblock}

이러한 인리치먼트는 함께 작동하여 더 나은 조회를 빌드하는 데 도움이 됩니다.

## 데이터 정규화
{: #normalizing-data}

이 정보는 [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu) 릴리스 전에 작성된 콜렉션에만 적용됩니다.
{: note}

구성 파일을 사용자 정의하는 마지막 단계는 정규화로 알려진 최종 정리를 수행하는 것입니다.

{{site.data.keyword.discoveryshort}} 도구의 **정규화** 섹션에서:

-   필드를 이동, 병합, 복사 또는 제거할 수 있습니다.
-   비어 있는 필드(정보가 없는 필드)는 기본적으로 삭제됩니다. **비어 있는 필드 제거** 토글을 사용하여 이를 변경할 수 있습니다.

변경한 후에는 **적용 및 저장**과 **완료**를 차례로 클릭하십시오. 이 구성을 선택한 콜렉션에 적용할 수 있는 **데이터 관리** 화면으로 돌아갑니다.

**참고:** 필드의 `data type`(예: `text` 또는 `date`)을 지정할 수 없습니다. 문서 수집 중에, 인덱스에 아직 존재하지 않는 필드가 발견되면 {{site.data.keyword.discoveryshort}}는 첫 번째 문서의 인덱싱된 필드 값을 기반으로 하여 해당 필드의 `data type`을 자동으로 감지합니다.

**요소 분류** 인리치먼트를 사용하는 경우 사후 인리치먼트 정규화를 수행할 수 없습니다.

## 엔티티 정규화
{: #normalizing-entities}

### CSS 선택기를 사용하여 필드 추출
{: #using-css}

Discovery API를 통해 CSS 선택기를 사용하여 추가 정규화를 수행할 수 있습니다.

올바르게 구성된 HTML을 수집하는 중이고 이를 정규화할 수 있는 경우 CSS 선택기를 사용하여 이 HTML에서 JSON 필드를 추출한 후 인리치먼트를 추출된 필드에 적용하십시오. 이 기능을 사용하도록 구성 파일을 편집하십시오. 특히 `extracted_fields` 요소를 `conversions/html` 계층 구조에 추가하여 필드 이름, CSS 선택기 및 필드 유형을 다음과 같이 지정하십시오.

```json
{
  "name": "Extract JSON config",
  "description": "New configuration enabling extraction of JSON fields from HTML",
  "conversions": {
    ...
    "html": {
      ...
      "extracted_fields": {
        "{field_name_1}": {
          "css_selector": "{CSS_selector_expression_1}",
          "type": "{field_type}"
        },
        ...
        "{field_name_N}": {
          "css_selector": "{CSS_selector_expression_N}",
          "type": "{field_type}"
        }
      }
    ...
    }
  }
}
```
{: codeblock}

다음과 같이 새 필드의 값을 지정하십시오.

-   `field_name` — JSON 출력에 추가되는 필드의 이름입니다.
-   `CSS_selector_expression` — 필드를 추출하기 위해 입력 HTML에 대해 실행될 CSS 선택기입니다. 표현식에는 하나 이상의 일치 항목이 있을 수 있습니다.

    유효한 CSS 선택기는 [JSoup 구문 분석기 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://jsoup.org/apidocs/org/jsoup/select/Selector.html){: new_window} 및 해당 [선택기 구문 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://jsoup.org/cookbook/extracting-data/selector-syntax){: new_window}으로 지정된 유효한 CSS 선택기입니다. 짧은 목록은 [공통 선택기](/docs/services/discovery?topic=discovery-configservice#common-selectors)에서 제공됩니다.
-   `field_type` — `array` 또는 `string`입니다. 필드 유형이 지정되지 않은 경우 기본값은 `array`입니다. 유형 `string`을 강화할 수 있으나 배열의 항목이 텍스트 필드로 처음 추출되지 않는 한 `array`에 저장된 정보를 강화할 수 없습니다.

**경고:** CSS 선택기에서 두 개의 상위 노드 및 하나 이상의 하위 노드가 일치하면 JSON 출력에서 노드의 텍스트 컨텐츠가 중복됩니다.

**참고:** 필드 이름은 [필드 이름 요구사항](/docs/services/discovery?topic=discovery-configref#field_reqs)에 정의된 제한사항을 충족해야 합니다.

다음 JSON 구문에서는 CSS 선택기 정보를 추가하는 기본 구성의 관련 섹션을 표시합니다.

```json
{
  "name": "Default Configuration",
  "description": "The configuration used by default when creating a new collection without specifying a configuration_id.",
  "conversions": {
    ...
    "html": {
      "exclude_tags_completely": [
        "script",
        "sup"
      ],
      "exclude_tags_keep_content": [
        "font",
        "em",
        "span"
      ],
      "exclude_content": {
        "xpaths": []
      },
      "keep_content": {
        "xpaths": []
      },
      "exclude_tag_attributes": [
        "EVENT_ACTIONS"
      ]
    }
    ...
  }
}
```
{: codeblock}

다음 구문에서는 새 이름과 설명 및 CSS 선택기를 지정할 수 있는 위치가 포함된 구성을 표시합니다.

```json
{
  "name": "Extract JSON config",
  "description": "New configuration enabling extraction of JSON fields from HTML",
  "conversions": {
    ...
    "html": {
      "exclude_tags_completely": [
        "script",
        "sup"
      ],
      "exclude_tags_keep_content": [
        "font",
        "em",
        "span"
      ],
      "exclude_content": {
        "xpaths": []
      },
      "keep_content": {
        "xpaths": []
      },
      "exclude_tag_attributes": [
        "EVENT_ACTIONS"
      ],
      "extracted_fields": {
        "{field_name_1}": {
          "css_selector": "{CSS_selector_expression_1}",
          "type": "{field_type}"
        },
        ...
        "{field_name_N}": {
          "css_selector": "{CSS_selector_expression_N}",
          "type": "{field_type}"
        }
      }
    }
  }
  ...
}
```
{: codeblock}

마지막으로 다음 구문에서는 새 이름과 설명 및 일부 CSS 선택기가 포함된 구성을 표시합니다. 선택기는 이 페이지의 아래에서 설명된 HTML 예제의 항목과 일치합니다.

```json
{
  "name": "Extract JSON config",
  "description": "New configuration enabling extraction of JSON fields from HTML",
  "conversions": {
    ...
    "html": {
      "exclude_tags_completely": [
        "script",
        "sup"
      ],
      "exclude_tags_keep_content": [
        "font",
        "em",
        "span"
      ],
      "exclude_content": {
        "xpaths": []
      },
      "keep_content": {
        "xpaths": []
      },
      "exclude_tag_attributes": [
        "EVENT_ACTIONS"
      ],
      "extracted_fields": {
        "chapters": {
          "css_selector": ".chapter",
          "type": "array"
        },
        "authors": {
          "css_selector": ".author"
        },
        "authors_str": {
          "css_selector": ".author",
          "type": "string"
        },
        "comments": {
          "css_selector": "[^comments-content]"
        }
      }
    }
  }
  ...
}
```
{: codeblock}

업데이트된 구성을 사용하는 콜렉션에 다음 HTML 문서를 로드하는 경우 CSS 선택기는 HTML의 해당 속성 및 값과 일치합니다.

```html
<html>
  <body>
    <div id="authors">
      <div class="author"><span class="first_name">Jane</span> <span class="last_name">Rain</span></div>
      <div class="author">Joe Snow</div>
  </div>
  <div class="chapter"><h1>The Rain in Spain</h1><p>falls mainly on the plain.</p></div>
  <div class="chapter"><h1>How I Learned to Stop Worrying</h1><p>and love my snowblower.</p></div>
  <span id="comments-section">
    <h4>Comments:</h4>
    <span id="comments-content-1">Rain gives me pain.</span>
    <span id="comments-content-2">All snow must go!</span>
  </span>
</body></html>
```
{: codeblock}

이전 HTML이 수집되고 강화된 후 {{site.data.keyword.discoveryshort}} 서비스가 다음 JSON을 리턴합니다.

```json
{
  "extracted_metadata": { ... },
  "html": "...",
  "text": "...",
  "extracted_fields": {
    "authors": [ "Jane Rain", "Joe Snow" ],
    "authors_str": "Jane Rain\n\nJoe Snow",
    "chapters": [ "The Rain in Spain\n\nfalls mainly on the plain.", "How I Learned to Stop Worrying\n\nand love my snowblower." ],
    "comments": [ "Rain gives me pain.", "All snow must go!" ]
  }
}
```
{: codeblock}

추출할 HTML 요소를 결정한 후 구성 파일을 추가로 수정하여 HTML 요소에 적용할 인리치먼트를 지정할 수 있습니다.

#### 공통 선택기
{: #common-selectors}

일부 공통 CSS 선택기에는 다음 항목이 포함됩니다.

  - `tag` — `tag` 이름 일치
  - `.class` — `class` 값 일치
  - `#id` — `id` 값 일치
  - `[attribute]` — 지정된 `attribute`가 사용된 태그 일치(값 상관 없음)
  - `[attribute=value]` 또는 `[attribute="value"]` — 지정된 `attribute` 및 `value` 일치

## 문서 세그먼트화로 문서 분할
{: #doc-segmentation}

Smart Document Understanding을 사용하는 경우 문서 세그먼트화를 사용하지 말고 [문서 분할](/docs/services/discovery?topic=discovery-sdu#splitting)을 사용하십시오.
{: note}

Word, PDF 및 HTML 문서를 HTML 표제 태그를 기반으로 한 세그먼트로 분할할 수 있습니다. 분할하면 각 세그먼트는 별도로 보강되고 인덱싱되는 개별 문서입니다. 조회가 개별 문서로 이 세그먼트를 리턴하므로 문서 세그먼트화를 사용하여 다음을 수행할 수 있습니다.

  - 문서의 개별 세그먼트에 대한 집계를 수행합니다. 예를 들어, 집계는 전체 문서에 대해 세그먼트를 한 번만 포함하지 않고 세그먼트에서 특정 엔티티를 언급할 때마다 포함합니다.
  - 문서 대신 세그먼트에 대한 관련성 훈련을 수행합니다. 이를 통해 결과의 순위 재지정이 개선됩니다.

문서가 HTML로 변환될 때 세그먼트가 작성됩니다(Word 및 PDF 문서는 JSON으로 변환되기 전에 HTML로 변환됨). 문서는 `h1` `h2` `h3` `h4` `h5` 및 `h6`의 HTML 태그를 기반으로 분할될 수 있습니다.

고려사항:

  - 문서당 세그먼트의 수는 `250`으로 제한됩니다. `249` 세그먼트 이후에 남아 있는 모든 문서 컨텐츠가 `250` 세그먼트 내에 저장됩니다.

  - 각 세그먼트는 플랜의 문서 한계를 포함합니다. {{site.data.keyword.discoveryshort}}는 플랜 한계에 도달할 때까지 세그먼트를 인덱싱합니다. 문서 한계에 대해서는 [Discovery 가격 플랜](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)을 참조하십시오.

  - 문서 세그먼트화를 사용할 때는 데이터를 정규화([데이터 정규화](/docs/services/discovery?topic=discovery-configservice#normalizing-data))하거나 CSS 선택기를 사용하여 필드 추출([CSS 선택기를 사용하여 필드 추출](/docs/services/discovery?topic=discovery-configservice#using-css) 참조)을 할 수 없습니다.

  - 지정된 HTML 태그가 삭제될 때마다 문서가 세그먼트화됩니다. 따라서 태그를 닫기 전과 태그를 연 후에 문서를 분할할 수 있으므로 세그먼트화로 올바르지 않은 HTML이 발생할 수 있습니다.

  - 사용자 정의 메타데이터를 비롯하여 HTML, PDF 및 Word 메타데이터는 추출되어 각 세그먼트가 있는 인덱스에 포함됩니다. 문서의 모든 세그먼트는 동일한 메타데이터를 포함합니다.

  - **요소 분류**(`elements`) 인리치먼트가 지정되면 문서 세그먼트화가 지원되지 않습니다.

  - 세그먼트화된 문서를 다시 수집하기 위해서는 추가 고려사항이 있습니다. [세그먼트화된 문서 업데이트](/docs/services/discovery?topic=discovery-configservice#update-seg)를 참조하십시오.

### 세그먼트화 수행
{: #performing-segmentation}

Smart Document Understanding을 사용하는 경우 문서 세그먼트화를 사용하지 말고 [문서 분할](/docs/services/discovery?topic=discovery-sdu#splitting)을 사용하십시오.
{: note}

세그먼트화는 `conversions` 섹션에서 API를 통해 설정됩니다.

```json
{
  "configuration_id": "a23c467d-1212-4b3a-5555-93e788a3622a",
  "name": "Example configuration",
  "conversions": {
    "segment": {
      "enabled": true,
      "selector_tags": ["h1", "h2", "h3", "h4", "h5", "h6"]
    }
  }
}
```
{: codeblock}

`enabled` = `true`는 문서 세그먼트화를 설정합니다.

`selector_tags`는 표제 태그 문서를 세그먼트화할 수 있도록 지정하는 배열입니다.

#### 예
{: #example-segmentation}

구성:

```json
"conversions": {
  "segment": {
    "enabled": true,
    "selector_tags": ["h1", "h2"]
```
{: codeblock}

원래의 HTML 문서:

```
<html>
 <head>
 </head>
 <body>
  first line
   <div name="section 1">
    <h1>heading 1</h1>
     <div name="section 2">This is the text that falls under <b>heading 1</b> and should be therefore split into its own segment.
      <h2>heading 2</h2>
      line under heading 2
     </div>
       <h3>heading 3</h3>
       line under heading 3
   </div>
  last line
 </body>
</html>
```
{: codeblock}

첫 번째 세그먼트는 다음과 같이 표시됩니다.

```json
{
  "id": "94c686c3-a790-4d8d-ba42-2bddf01b311c",
  "segment_metadata": {
    "parent_id": "94c686c3-a790-4d8d-ba42-2bddf01b311c",
    "segment": 1,
    "total_segments": 3
  },
  "extracted_metadata": {
    "title": "Heading 1",
    "sha1": "45ede479df67d78f2205ea7e714843375d3029c0",
    "filename": "doc-with-different-heading-levels.html",
    "file_type": "html"
  },
  "text": "This is the text that falls under heading 1 and should be therefore split into its own segment.",
  "html": "<div name=\"section 2\">This is the text that falls under <b>heading 1</b> and should be therefore split into its own segment."
}
```
{: codeblock}

모든 세그먼트에는 다음 항목이 포함됩니다.

  - `id` - 세그먼트의 `id`입니다.
  - `segment_metadata` 섹션에는 다음 항목이 포함됩니다.
    - `parent_id` - `parent_id`는 원래 문서의 ID입니다. 첫 번째 세그먼트의 경우 `id` 및 `parent_id`가 동일합니다.
    - `segment` - 이 세그먼트의 수입니다.
    - `total_segments` - 문서가 분할된 총 세그먼트 수입니다.
  - `extracted_metadata` 섹션에는 다음 항목이 포함됩니다.
    - `title` - `title` 필드는 해당 세그먼트에 있는 표제 태그의 컨텐츠에서 추출됩니다(예: `Chapter 1`). 첫 번째 세그먼트에 표제 태그가 포함되지 않으면 `title`은 `no-title`이 됩니다.
    - `sha1` - 원래 문서에 해당됩니다.
    - `filename` - 원래 문서에 해당됩니다.
    - `file_type` - 원래 문서에 해당됩니다.
  - `text` 필드
  - `html` 필드

### 세그먼트화된 문서 업데이트
{: #update-seg}

세그먼트화된 문서가 업데이트되어 다시 수집해야 하는 경우 [문서 업데이트 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/discovery#update-a-document){: new_window} 메소드를 사용하여 대체할 수 있습니다.

세그먼트화된 문서를 업데이트하는 경우 문서는 `/environments/{environment_id}/collections/{collection_id}/documents/{document_id}` API의 POST 메소드를 사용하여 업로드되어야 하며, 현재 세그먼트 중 하나의 `parent_id` 필드의 컨텐츠를 `{document_id}` 경로 변수로 지정합니다.

업데이트하는 동안, 업데이트 문서 버전의 총 섹션 수가 원래 버전보다 적지 않으면 모든 세그먼트를 겹쳐씁니다. 이전 세그먼트는 인덱스에 남게 되며 API를 사용하여 개별적으로 삭제할 수 있습니다. 자세한 정보는 [API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/discovery#delete-a-document){: new_window}를 참조하십시오. `notices`를 조회하여 작성된 세그먼트 수를 식별할 수 있습니다. 각 세그먼트에는 `document_id` 필드가 제공되는데, 이 필드는 `{parent_id}`, 밑줄, 세그먼트 번호(순서대로)로 구성됩니다.

업데이트하려는 문서의 세그먼트가 관련성 훈련에 대해 순위 지정된 경우 먼저 해당 문서의 모든 세그먼트를 삭제한 후 업데이트된 문서를 새 문서로 수집해야 합니다. 이렇게 하면 새 각 세그먼트에 대해 `document_id`가 생성되고 훈련된 세그먼트는 다시 훈련해야 합니다. 먼저 이전 컨텐츠를 삭제하지 않으면 훈련된 인덱스가 정확하지 않게 됩니다.

또는 새 컨텐츠만 포함하는 새 문서를 작성하여 이를 별도로 수집하는 방법을 고려해 보십시오.
