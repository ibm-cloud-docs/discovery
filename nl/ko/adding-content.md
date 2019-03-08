---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-15"

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

# 컨텐츠 추가
{: #addcontent}

사용할 문서 업로드 메소드를 결정하는 방법
{: shortdesc}

-   기존 애플리케이션을 사용한 컨텐츠 업로드에 관심이 있거나 고유한 사용자 정의 업로드 메커니즘을 작성하는 경우 [API](/docs/services/discovery/getting-started.html)를 사용하십시오.
-   액세스 가능한 파일을 로컬로 빠르게 업로드하려는 경우 [{{site.data.keyword.discoveryshort}} 도구](/docs/services/discovery/getting-started-tool.html)를 사용하십시오.
    {{site.data.keyword.discoveryshort}} 도구를 사용하여 문서를 업로드하는 경우 모든 문서의 파일 이름이 고유해야 합니다. 두 파일의 이름이 동일한 경우 새 버전이 업로드될 때 원래 항목이 겹쳐쓰여집니다. 파일 이름이 동일한 여러 문서가 콜렉션에 공존하기를 원하면 문서 ID를 지정해야 합니다. API 또는 Data Crawler를 사용하여 문서를 업로드하는 경우 문서 ID를 지정할 수 있습니다.
-   {{site.data.keyword.discoveryshort}} 도구 또는 API를 사용하여 Box, Salesforce 및 Microsoft SharePoint Online 데이터 소스에 연결하십시오. 자세한 정보는 [데이터 소스에 연결](/docs/services/discovery/connect.html)을 참조하십시오.
-   수많은 파일의 관리 업로드를 수행하려고 하거나 지원되는 저장소(예: DB2 데이터베이스)에서 컨텐츠를 추출하려는 경우 [Data Crawler](/docs/services/discovery/data-crawler.html)를 사용하십시오.

## API 또는 도구를 사용하여 컨텐츠 추가

문서를 콜렉션에 추가할 준비가 되면 다음 사항을 고려하십시오.

-   {{site.data.keyword.discoveryshort}} 서비스에 업로드할 수 있는 최대 파일 크기는 50MB입니다.
-   샘플 문서는 자동으로 콜렉션에 추가되지 않습니다. 샘플 문서가 콜렉션의 일부가 되기를 원하면 샘플 문서를 추가해야 합니다.
-   인리치먼트에 선택된 각 JSON 필드의 처음 50,000자만 강화됩니다. 
-   콜렉션을 작성할 때 문서 언어를 선택해야 합니다(기본 언어는 영어임). 언어의 목록을 보려면 [언어 지원](/docs/services/discovery/language-support.html)을 참조하십시오. 선택한 언어로 문서가 강화됩니다. 동일한 콜렉션 내에서 언어를 혼용하지 마십시오.
-   Microsoft Word, PDF, HTML 및 JSON 문서를 콜렉션에 추가할 수 있습니다. **참고:** 스캔된 이미지 파일인 PDF는 변환하고 강화할 수 없습니다.
-   다른 구성 파일을 선택하지 않는 한 기본 구성이라고 하는 제공된 구성 파일을 사용하여 콜렉션의 문서가 변환됩니다. 구성 파일 작성에 대한 정보는 [사용자 정의 구성](/docs/services/discovery/building.html#custom-configuration)을 참조하십시오.
-   문서가 데이터 콜렉션에 업로드되면 해당 콜렉션에 대해 선택한 구성 파일을 사용하여 문서가 변환되고 강화됩니다. 나중에 콜렉션을 다른 구성 언어로 전환하도록 결정하는 경우 이를 수행할 수 있지만 이미 업로드한 문서는 원래 구성 파일에 의해 변환된 상태로 유지됩니다. 구성 파일을 전환한 후 업로드된 모든 문서는 새 구성 파일을 사용합니다. **전체** 콜렉션에서 새 구성 파일을 사용하려면 새 콜렉션을 작성하고 새 구성 파일을 선택한 다음 모든 문서를 다시 업로드해야 합니다.
-   필드의 `data type`(예: `text` 또는 `date`)을 지정할 수 없습니다. 문서 수집 중에, 인덱스에 아직 존재하지 않는 필드가 발견되면 {{site.data.keyword.discoveryshort}}는 첫 번째 문서의 인덱싱된 필드 값을 기반으로 하여 해당 필드의 `data type`을 자동으로 감지합니다.
-   현재 문서의 데이터와 이전에 수집된 문서의 유사한 데이터 간에 유형 불일치로 인해 문서가 수집되지 않을 수 있습니다. 예를 들어, 하나의 필드가 한 문서에서는 `date`로 입력되고 후속 문서에서는 `string`으로 입력될 수 있으며 이런 경우 후속 문서가 올바르게 인덱싱되지 않습니다.
-   사용자 정의 토큰화를 사용하려는 경우(현재 {{site.data.keyword.discoveryshort}} API 사용 시 일본어 콜렉션에서만 사용 가능) 콜렉션에 대한 토큰화 사전은 문서를 업로드하기 전에 추가되어야 합니다.

문서를 업로드할 때 다음 제한사항이 적용됩니다.

-   **라이트** 플랜: 21개의 인플라이트 문서
-   **고급** 플랜: 105개의 인플라이트 문서(50개의 인플라이트 문서 제한이 있는 X-Small 고급 플랜은 제외)
-   **프리미엄** 플랜: 210개의 인플라이트 문서

이 한계는 변경될 수 있습니다. 

Discovery 서비스를 사용할 때 업로드되는 인플라이트는 콜렉션에 추가되기 전에 업로드되고 처리되는 문서를 나타냅니다. 인플라이트 한계에 도달하면 수집 속도를 늦추어야 합니다. 재시도를 수행하여 자동화된 백오프 메커니즘을 추가하는 옵션이 있습니다.

## Discovery 도구를 사용하여 문서 업로드

1.  콜렉션을 작성하십시오. [문서에 대한 서비스 준비](/docs/services/discovery/building.html#preparing-the-service-for-your-documents)를 참조하십시오.
1.  콜렉션을 클릭하여 여십시오.
1.  **문서 업로드** 단추를 클릭하고 끌어서 놓기 또는 찾아보기를 통해 문서 업로드를 시작하십시오.

이제 문서가 변환되고 강화되도록 큐에 삽입됩니다. 소요되는 시간은 콜렉션의 크기에 따라 달라집니다. 문서가 인덱싱되고 강화된 후 콜렉션의 세부사항이 **개요** 절에 표시됩니다.

-   **작성 날짜** 및 **마지막 업데이트 날짜**(**API의 이 콜렉션 사용**을 클릭하여 `collection_id`, `configuration_id` 및 `environment_id`를 표시함)
-   콜렉션의 **문서 수**
-   **구성** — 이 콜렉션을 변환하는 데 사용되는 구성 파일의 이름
-   **오류 및 경고**

{{site.data.keyword.discoveryshort}} 도구를 사용하여 Box, Salesforce 및 Microsoft SharePoint Online 데이터 소스에 연결하는 방법에 대한 정보는 [데이터 소스에 연결](/docs/services/discovery/connect.html)을 참조하십시오.


## API로 문서 업로드

단계별 튜토리얼은 [{{site.data.keyword.discoveryshort}} API 시작하기](/docs/services/discovery/getting-started.html)를 참조하십시오.

API에 대한 자세한 정보는 [API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}를 참조하십시오.

1.  `POST /v1/environments/{environment_id}/collections` 메소드를 사용하여 콜렉션을 작성하십시오.
1.  그런 다음 `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` 메소드를 사용하여 콜렉션에 문서를 추가하십시오.

## URL 크롤링

{{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} {{site.data.keyword.discoveryshort}} 서비스 [Apache Nutch에 대한 플러그인 인덱싱 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/IBM-Watson/nutch-indexer-discovery)을 사용하여 URL을 크롤링하고 인덱싱할 수 있습니다. 크롤링은 자동으로 업데이트하지 않으므로 인덱스를 최신 상태로 유지하려면 프로시저를 주기적으로 반복해야 합니다.
