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
{:gif: data-image-type='gif'}

# SDU(Smart Document Understanding)
{: #sdu}

SDU(Smart Document Understanding)는 문서의 사용자 정의 필드를 추출하도록 {{site.data.keyword.discoveryfull}}를 훈련하는 새로운 방법입니다. 문서를 {{site.data.keyword.discoveryshort}}로 인덱싱하는 방법을 사용자 정의하면 애플리케이션으로 리턴되는 답변을 개선할 수 있습니다.

SDU를 사용하여 사용자 정의 변환 모델을 훈련하도록 문서 내에서 필드 어노테이션을 작성합니다. 어노테이션을 작성할 때 Watson은 학습하며 어노테이션을 예측하기 시작합니다. SDU 모델을 내보내고 다른 콜렉션에서 사용할 수 있습니다.  

## 지원되는 문서 유형 및 브라우저
{: #doctypes}

Smart Document Understanding에 대해 지원되는 문서 유형: 
-  Lite 플랜: PDF, Word, PowerPoint, Excel, JSON\*, HTML\* 
-  고급 플랜: PDF, Word, PowerPoint, Excel, PNG\*\*, TIFF\*\*, JPG\*\*, JSON\*, HTML\*  

\* JSON 및 HTML 문서는 {{site.data.keyword.discoveryfull}}에서 지원되지만 SDU 편집기를 사용하여 편집할 수 없습니다. HTML 및 JSON 문서의 구성을 변경하려면 API를 사용해야 합니다. 자세한 정보는 [API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/discovery/){: new_window}를 참조하십시오.

\*\* 개별 이미지 파일(PNG, TIFF, JPG)은 스캔되고 텍스트(해당 경우)가 추출됩니다. PDF, Word, PowerPoint 및 Excel 파일에 임베드된 PNG, TIFF 및 JPEG 이미지도 스캔되고 텍스트(해당 경우)가 추출됩니다. 

지원되는 브라우저: Chrome 및 Firefox

## Smart Document Understanding 편집기 사용
{: #annotate}

SDU 편집기는 지원되는 문서 유형이 포함된 새 콜렉션에만 사용 가능하며 요소 분류 인리치먼트가 적용되지 않습니다. 기존의 개인용 콜렉션은 원래의 구성 방법을 사용합니다. 기존 콜렉션에서 SDU 편집기를 사용할 경우 새 콜렉션을 작성하고 해당 문서를 이 콜렉션에 업로드해야 합니다. SDU 편집기를 사용하지 않으려면 API를 사용하여 구성을 설정할 수 있습니다. [API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/discovery/){: new_window}를 참조하십시오.
{: important}

SDU 편집기 기능은 {{site.data.keyword.discoveryshort}} 도구에만 사용 가능하며 API에서 사용할 수 없습니다.
{: note}

Smart Document Understanding 편집기 탐색

아직 {{site.data.keyword.discoveryshort}} 인스턴스 및 환경을 작성하지 않은 경우 지시사항은 [시작하기](/docs/services/discovery?topic=discovery-getting-started#getting-started)를 참조하십시오.
{: tip}

1. **데이터 관리** 화면에서 **고유한 데이터 업로드** 단추를 클릭하고 {{site.data.keyword.discoveryshort}}에서 새 개인용 콜렉션을 작성하십시오. 
1. 원하는 경우 문서를 콜렉션에 끌어서 놓거나 **컴퓨터에서 찾아보기**를 클릭하여 문서를 업로드하십시오. 업로드가 완료되면 다음 정보가 표시됩니다.
   -  문서에서 식별되는 필드입니다. 
   -  문서에 적용되는 인리치먼트입니다. 엔티티 추출, 감성 분석, 카테고리 분류 및 개념 태그 지정 인리치먼트는 {{site.data.keyword.discoveryshort}}를 통해 `text` 필드에서 자동으로 적용됩니다(커넥터를 사용하여 문서를 가져오지 않는 한). 추가 인리치먼트를 `text` 필드에 추가(또는 제거)할 수 있습니다.
   -  즉시 실행할 수 있는 조회를 미리 빌드하십시오. 
1. 오른쪽 상단에 있는 **데이터 구성**을 클릭하십시오. 
1. **데이터 구성** 화면에는 **필드 식별**, **필드 관리** 및 **필드 강화**의 세 가지 탭이 있습니다. 

   - **필드 식별**에는 SDU 편집기가 있습니다. 이 탭은 원래 {{site.data.keyword.discoveryshort}} 화면의 **변환** 및 **정규화** 탭을 모두 대체합니다. 
   - **필드 관리**는 인덱싱된 모든 필드를 나열합니다(기본적으로 모든 필드가 인덱싱됨). 인덱싱하지 않을 모든 필드를 해제하십시오. 예를 들어, PDF에는 유용한 정보가 포함되지 않은 실행 중인 머리글 또는 바닥글이 포함될 수 있으므로 인덱스에서 해당 필드를 제외할 수 있습니다. 필드를 기반으로 한 문서를 여기에서 분할할 수도 있습니다. [문서 분할](/docs/services/discovery?topic=discovery-sdu#splitting)을 참조하십시오.
   - **필드 강화**는 원래 화면의 **강화** 탭과 동일합니다. 인리치먼트에 대한 자세한 정보는 [인리치먼트 추가](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)를 참조하십시오. SDU 콜렉션에서 **샘플 문서 업로드** 옵션은 사용할 수 없습니다. 

   이전에 문서를 업로드하지 않는 경우 왼쪽 상단에 있는 콜렉션의 이름을 클릭하여 **개요** 화면으로 돌아가거나 ![데이터 관리](/images/icon_yourData.png) 아이콘을 클릭하고 콜렉션을 선택하십시오. 문서를 콜렉션에 끌어서 놓거나 **컴퓨터에서 찾아보기**를 클릭하십시오. 초기 업로드를 완료한 후 **문서 업로드** 단추가 오른쪽 상단에 표시됩니다.
   {: important}

   Smart Document Understanding을 사용하는 경우 `text` 필드만 강화될 수 있습니다. 다른 필드의 강화를 시도하지 마십시오.
   {: important}

1. **필드 식별** 탭을 여십시오. 콜렉션에서 최대 20개의 문서가 Smart Document Understanding 편집기에 자동으로 로드됩니다.

맨 위의 도구 모음을 사용하여 다음을 수행할 수 있습니다.
- 어노테이션을 작성할 문서 선택
- 표시된 문서 탐색
- 페이지 보기(`단일 페이지 보기`, `확대`, `축소`), `clear changes` 및 `export/import models` 조정. `single page view`를 클릭하여 표시를 전환하십시오. 그러면 어노테이션 및 문서를 개별적으로 또는 함께 볼 수 있습니다. 

{{site.data.keyword.discoveryshort}} 도구를 사용하여 Box, Salesforce, Microsoft SharePoint Online, IBM Cloud Object Storage 및 Microsoft SharePoint 2016 데이터 소스에 연결하거나 웹 크롤링을 수행할 수도 있습니다. 자세한 정보를 보려면 **데이터 소스 연결** 단추를 클릭하고 [데이터 소스 연결](/docs/services/discovery?topic=discovery-sources#sources)을 참조하십시오. 이 방법을 사용하여 콜렉션을 작성하는 경우 인리치먼트가 자동으로 적용되지 않습니다.
{: tip}

## 문서 어노테이션을 작성하는 방법
{: #documents}

**참고:** 테이블은 별도의 단계에서 어노테이션을 작성합니다.

어노테이션 작성을 시작하기 전에 [문서 및 테이블 어노테이션 작성에 대한 우수 사례](/docs/services/discovery?topic=discovery-sdu#bestpractices)를 참조하십시오.

1. 기본 필드 세트가 문서 오른쪽에 표시됩니다. 사용 가능한 필드는 `answer`, `author`, `footer`, `header`, `question`, `subtitle`, `table_of_contents`, `text` 및 `title`입니다. 하나 이상의 새 사용자 정의 필드 레이블을 작성하려면 **새 작성**을 클릭하십시오. 사용자 정의 레이블 즉, Lite 플랜 - `0`, 고급 플랜 - `5`, 프리미엄 플랜 - `20`으로 제한됩니다.
1. 오른쪽에 있는 필드 레이블을 클릭하여 활성화하십시오.
1. SDU 편집기에서 해당 필드를 표시하는 컨텐츠를 클릭하십시오. 강조표시됩니다. 
   - 또는 오른쪽에 있는 필드 레이블을 선택하고 이를 SDU 편집기의 컨텐츠로 끌어올 수 있습니다. 
   - 변경사항을 지우려면 도구 모음에서 **변경사항 지우기** 단추를 클릭하십시오.
1. **제출**을 클릭하십시오.
   **참고:** 어노테이션을 작성할 때 Watson은 학습하며 어노테이션을 예측하기 시작합니다. Watson이 올바르고 일관되게 필드를 식별할 때까지 계속 어노테이션을 작성하십시오.
1. 어노테이션 작성을 완료하면 **콜렉션에 변경사항 적용**을 클릭하십시오. **문서 업로드** 화면이 열립니다. 콜렉션에서 문서를 다시 업로드하십시오. 업로드가 완료되면 **데이터 관리** 화면으로 경로가 재지정됩니다.

필드 |정의  
------ | ------ 
answer | Q/A 쌍(대개 FAQ)에서 질문에 대한 답변입니다.
author | 작성자의 이름입니다.
footer | 이 태그를 사용하여 페이지 맨 아래에 표시되는 문서에 대한 메타 정보(예: 페이지 번호 또는 참조)를 표시합니다.
header | 이 태그를 사용하여 페이지의 맨 위에 표시되는 문서에 대한 메타 정보를 표시합니다.
question | Q/A 쌍(대개 FAQ)에서 질문입니다.
subtitle | 어노테이션이 있는 문서의 보조 제목입니다. 
table_of_contents |문서 목차에 있는 목록에서 이 태그를 사용합니다.
text | 표준 복사 텍스트에 이 태그를 사용합니다(단락, 정의 또는 제목이 아닌 단어 세트, 테이블 일부, 답변, 작성자, 하위 제목, 머리글 또는 바닥글 포함). 
title | 어노테이션이 있는 문서의 기본 제목입니다.

## 테이블 어노테이션을 작성하는 방법
{: #tables}

테이블 어노테이션은 베타 릴리스에 있습니다. 베타 기능을 설명하는 발표문은 [여기](/docs/services/discovery?topic=discovery-release-notes#beta-features)에 있습니다.
{: important}

어노테이션 작성을 시작하기 전에 [문서 및 테이블 어노테이션 작성에 대한 우수 사례](/docs/services/discovery?topic=discovery-sdu#bestpractices)를 참조하십시오.

1. SDU 편집기의 오른쪽에서 `테이블` 필드를 선택한 후 문서에서 테이블을 선택하십시오. 
1. 테이블 위에 마우스를 올리면 **테이블 어노테이션 작성** 단추가 표시됩니다. 이 단추를 클릭하여 테이블 편집기를 여십시오.
1. 먼저 테이블의 아웃라인을 만드십시오.
   - `column` 필드를 선택하십시오.
   - 테이블에서 열을 클릭하여 이를 활성화하십시오.
   - `row` 필드를 선택하십시오.
   - 테이블에서 행을 클릭하여 이를 활성화하십시오.

   왼쪽의 테이블 미리보기에서 테이블의 아웃라인이 표시됩니다.

   **참고:** 테이블 어노테이션을 작성할 때 Watson은 학습하며 어노테이션을 예측하기 시작합니다. 
1. 두 번째로, 테이블 내의 컨텐츠에 레이블을 지정하십시오.
1. 테이블 어노테이션 작성을 완료한 후 **어노테이션 완료**를 클릭하십시오.
1. **콜렉션에 변경사항 적용**을 클릭하십시오. **문서 업로드** 화면이 열립니다. 콜렉션에서 문서를 다시 업로드하십시오. 업로드가 완료되면 **데이터 관리** 화면으로 경로가 재지정됩니다.

지침서로 이 동영상을 사용하십시오![테이블 어노테이션 동영상](images/SDU_table_demo.gif){: gif}. 

필드 |정의  
------ | ------ 
body | 정보가 포함된 비헤더 셀
column header |테이블의 각 열에 대한 표제 셀(있는 경우) 
multi-column header | 둘 이상의 열에 걸쳐 있는 표제 셀
row title | 행 표제 열의 열 헤더(있는 경우)
row header | 테이블의 각 행에 대한 행 레이블(있는 경우)
multi-row header |둘 이상의 행에 걸쳐 있는 행 레이블

## 문서 분할
{: #splitting}

**필드 관리** 탭에는 **문서를 분할하여 조회 결과 개선**에 대한 옵션이 포함됩니다. 이 옵션을 사용하면 필드 이름을 기반으로 한 세그먼트로 문서를 분할할 수 있습니다. 분할하면 각 세그먼트는 별도로 강화되고, 인덱싱되고, 별도의 조회 결과로 리턴되는 개별 문서입니다.  

문서는 단일 필드 이름을 기반으로 하여 분할됩니다(예: `title`, `author`, `question`). 

고려사항:

  - 문서당 세그먼트의 수는 `250`으로 제한됩니다. `249` 세그먼트 이후에 남아 있는 모든 문서 컨텐츠가 `250` 세그먼트 내에 저장됩니다.

  - 각 세그먼트는 플랜의 문서 한계를 포함합니다. {{site.data.keyword.discoveryshort}}는 플랜 한계에 도달할 때까지 세그먼트를 인덱싱합니다. 문서 한계에 대해서는 [Discovery 가격 플랜](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)을 참조하십시오.

  - 사용자 정의 메타데이터를 비롯하여 PDF 및 Word 메타데이터는 추출되어 각 세그먼트가 있는 인덱스에 포함됩니다. 문서의 모든 세그먼트는 동일한 메타데이터를 포함합니다.

  - 분할 문서가 업데이트되어 다시 업로드해야 하는 경우 문서는 [문서 업데이트 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/discovery#update-a-document){: new_window} 메소드를 사용하여 대체할 수 있습니다. 문서는 `/environments/{environment_id}/collections/{collection_id}/documents/{document_id}` API의 POST 메소드를 사용하여 업로드되어야 하며, 현재 세그먼트 중 하나의 `parent_id` 필드의 컨텐츠를 `{document_id}` 경로 변수로 지정합니다. 업데이트 문서 버전의 총 섹션 수가 원래 버전보다 적지 않으면 모든 세그먼트를 겹쳐씁니다. 이전 세그먼트는 인덱스에 남게 되며 API를 사용하여 개별적으로 삭제할 수 있습니다. 자세한 정보는 [API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/discovery#delete-a-document){: new_window}를 참조하십시오. 

## 모델 가져오기 및 내보내기
{: #import}

SDU 편집기를 사용하여 모델을 정의하면 모델을 저장하여 다른 콜렉션에서 재사용할 수 있습니다. 

편집기의 맨 위에 있는 도구 모음을 사용하여 완료된 SDU 모델을 가져오거나 내보낼 수 있습니다. 마지막 아이콘을 클릭하여 `Import model` 또는 `Export model`을 선택하십시오.

내보낸 모델에는 `.sdumodel`의 파일 확장자가 있습니다. 

가져온 모델은 추가 어노테이션 없이 사용됩니다. 모델을 가져온 후 계속해서 어노테이션을 작성하면 모델이 완전하게 겹쳐쓰여집니다. 모델을 새 콜렉션으로 가져오는 경우 하나의 문서만 포함된 새 콜렉션을 작성하고 모델을 가져온 후 문서의 나머지 부분을 업로드하는 것이 좋습니다. 

## 문서 및 테이블 어노테이션 작성에 대한 우수 사례
{: #bestpractices}

테이블 어노테이션은 베타 릴리스에 있습니다. 베타 기능을 설명하는 발표문은 [여기](/docs/services/discovery?topic=discovery-release-notes#beta-features)에 있습니다.
{: important}

- 모든 가이드라인에 따르고 모든 문서에서 일관된 레이블링을 사용하십시오.
- 공백에 레이블을 지정하지 마십시오.
- 이미지 및 다이어그램에 `image` 레이블을 사용하십시오.
- **굵은체**, _기울임체_ 또는 밑줄이 있는 텍스트를 다르게 처리하지 마십시오. 스타일이 아닌 컨텍스트를 기반으로 레이블하십시오. 
- 문서 레이블을 지정할 때 첫 번째 페이지부터 마지막 페이지까지 작업하십시오.
- 항목 레이블을 잘못 지정한 경우 먼저 항목에 대해 다른 레이블을 선택하여 겹쳐쓰십시오.
- 페이지는 언제든지 제출할 수 있습니다. 제출 전에 모든 레이블이 적절하게 완료되었는지 확인하십시오.
- 다른 텍스트를 오버레이하는 텍스트가 있는 것으로 보이는 문서 및 테이블은 “이중 오버레이”로 간주되며 어노테이션을 작성할 수 없습니다. 이 문서를 관리자에게 보고하십시오.
- 단일 페이지의 여러 텍스트 열을 포함하는 문서 및 테이블에는 어노테이션을 작성할 수 없습니다. 이 문서를 관리자에게 보고하십시오.
- 각주는 페이지의 맨 아래에 표시되고 문서의 기본 본문에서 참조되는 경우에만 레이블되어야 합니다.
- 섹션 또는 목록 내에 표시되는 참고사항(예: 명시적으로 "Notes"로 호출됨)은 `text`로 레이블이 지정되어야 합니다.
- 테이블의 레이블이 올바르게 지정되었고 미리보기 분할창이 응답하지 않는 경우 페이지가 브라우저에 다시 로드되고 올바른지 확인하기 위해 테이블의 레이블을 다시 지정해야 합니다.

