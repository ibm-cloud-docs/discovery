---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-01-15"

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

# 요소 분류
{: #element-classification}

요소 분류를 사용하면 운영 문서를 통해 빠르게 구문 분석하여 중요한 요소를 변환, 식별 및 분류할 수 있습니다. 최첨단 자연어 처리, 당사자(참조하는 사용자), 네이처(요소 유형) 및 카테고리(특정 클래스)가 문서의 요소에서 추출됩니다.

요소 분류는 다음을 제공하도록 설계되었습니다.

-  소프트웨어 조달 계약에 중점을 둔 계약의 NLU(Natural Language Understanding)
-  프로그램의 PDF를 어노테이션이 있는 JSON으로 변환하는 기능
-  주제별 전문 지식으로 정렬되는 법적 엔티티 및 카테고리의 식별

요소 분류는 섹션, 목록(번호 매기기 및 글머리표 지정), 각주 및 테이블을 식별하여 이러한 항목을 구조화된 HTML 형식으로 변환할 수 있는 프로그래밍 방식 PDF를 입력하기 위한 기능상으로 풍부한 통합 및 자동화된 Watson API 세트를 함께 제공합니다. 또한 이 구조화된 형식의 분류가 어노테이션되고 레이블 지정된 요소, 유형 및 카테고리를 사용하여 JSON으로 출력됩니다.

요소 분류는 전송 시와 저장 시 암호화를 수행하여 데이터를 안전하게 전송합니다. IBM Cloud 보안에 대한 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} 서비스 설명 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=%28IBM+Cloud+Service+description%29){: new_window}을 참조하십시오.

요소 분류는 다음이 포함된 JSON 오브젝트를 리턴합니다.

-  입력 문서의 제목, 입력 문서의 HTML 버전 및 입력 문서의 MD5 해시를 포함하는 `documents` 오브젝트.
-  입력 문서를 분류하는 데 사용되는 모델에 대한 정보.  
-  입력 문서에서 식별된 시맨틱 요소를 자세히 설명하는 `elements` 배열.
-  입력 문서에서 식별된 테이블을 분해하는 `tables` 배열.
-  입력 문서에서 식별된 섹션 제목 및 선행 문장을 나열하는 `document_structure` 오브젝트.
-  입력 문서에서 식별된 당사자, 역할, 주소 및 당사자 연락처를 나열하는 `parties` 배열.
-  `effective_dates`,`contract_amounts` 및 `termination_dates`를 정의하는 배열.

이 기능은 현재 영어로만 지원되며 세부사항은 [언어 지원](/docs/services/discovery?topic=discovery-language-support#feature-support)을 참조하십시오.


## 분류 요구사항
{: #element-class}

요소 분류를 사용하여 문서를 분류하려면 구성 및 소스 문서가 다음 요구사항을 충족해야 합니다.

-  분석할 파일은 PDF 형식입니다.
-  PDF 컨텐츠는 텍스트 양식입니다. 스캔된 문서는 OCR 처리가 되어도 구문 분석할 수 없습니다.
   **참고:** 하나의 단어를 선택하기 위해 PDF 뷰어로 문서를 열고 **텍스트 선택** 도구를 사용하여 텍스트로 된 PDF를 식별할 수 있습니다. 문서에서 하나의 단어를 선택할 수 없는 경우 파일을 구문 분석할 수 없습니다.
-  파일 크기는 50MB보다 크지 않습니다.
-  보안 설정된 PDF(비밀번호를 사용하여 열기) 및 제한된 PDF 편집(비밀번호를 사용하여 편집)은 구문 분석될 수 없습니다.
-  {{site.data.keyword.discoveryshort}} 도구에는 PDF 문서 콜렉션을 강화하는 데 사용할 수 있는 **기본 계약 구성**이라는 구성이 포함되어 있습니다. `elements` 인리치먼트가 포함된 사용자 정의 구성을 작성하는 옵션도 있습니다. 세부사항은 [콜렉션 요구사항](/docs/services/discovery?topic=discovery-element-classification#element-collection)을 참조하십시오.
-  **Lite** 플랜은 매월 최대 500페이지를 처리할 수 있습니다.
-  **전용** 환경에서는 사용할 수 없습니다.
-  요소 분류를 사용하는 경우 사후 인리치먼트 정규화를 수행할 수 없습니다.

**참고:** **기본 계약 구성** 파일이 2018년 9월 25일에 업데이트되었습니다. 이 날짜 이전에 이 구성을 콜렉션에 적용한 경우 콜렉션 업데이트에 대한 정보를 보려면 [릴리스 정보](/docs/services/discovery?topic=discovery-release-notes#25sept)를 참조하십시오.

## 콜렉션 요구사항
{: #element-collection}

요소 분류를 사용하려면 특정 요구사항을 충족하도록 콜렉션을 구성해야 합니다.

{{site.data.keyword.discoveryshort}} 도구에는 **요소 분류** 인리치먼트 및 기타 필수 옵션을 사용하여 PDF 문서를 강화하기 위해 사전 구성된 **기본 계약 구성**이라는 구성이 포함되어 있습니다. 콜렉션을 작성할 때 이 구성을 선택할 수 있습니다. 이 구성에 대한 JSON은 다음과 같습니다.

```json
 {
   "name": "Default Contract Configuration",
   "description": "Extract party, nature, and category from elements in PDFs.",
  "conversions": {
     "html": {
       "exclude_tags_completely": [],
       "exclude_tags_keep_content": []
     }
   },
   "enrichments": [
     {
       "source_field": "html",
       "destination_field": "enriched_html_elements",
       "enrichment": "elements",
       "options": {
         "model": "contract"
    }
     }
   ]
 }
```
{: codeblock}

사용자 정의 구성 파일을 작성하려는 경우 다음 요구사항을 충족하도록 콜렉션을 구성하십시오.  

-  지정된 경우 `PDF` 변환 설정이 무시됩니다.
-  Microsoft Word 파일로 생략할 수 있는 `WORD` 변환 설정은 요소 분류를 지정할 때 수집될 수 없습니다.
-  지정된 경우 `html` 정규화 설정이 무시됩니다.
-  `elements` 인리치먼트가 지정되면 문서 세그먼트화가 지원되지 않습니다.
-  {{site.data.keyword.discoveryshort}} 구성에서 `html` 필드는 `elements` 인리치먼트와 `contract`로 지정된 `model`로 강화되어야 합니다. 다음 예에서 `destination_field`는 `enriched_html`이지만 올바른 이름은 사용할 수 있습니다.

```json
"enrichments": [
   {
     "source_field": "html",
    "destination_field": "enriched_html",
    "enrichment": "elements",
    "options": {
       "model": "contract"
    }
   }
 ]
```
{: codeblock}

도구에서 `기본 계약 구성`을 선택한 후에 문서를 업로드할 수 있습니다. 콜렉션을 작성하고 문서를 업로드하는 데 익숙하지 않은 경우 [도구 시작하기](/docs/services/discovery?topic=discovery-getting-started#getting-started)를 참조하십시오.

## 분류된 요소
{: #classified-elements}

문서가 요소 분류로 인덱싱되면 검색 가능한 문서의 일부로 `elements` 배열을 사용하여 리턴됩니다.

`elements` 배열의 각 오브젝트는 {{site.data.keyword.discoveryshort}}가 식별한 계약의 요소를 설명합니다. 다음 코드는 일반 요소를 나타냅니다.

```json
 {
    "location" : {
     "begin" : 134323,
     "end" : 135109
    },
    "text" : "9. In the event that the Participant's total vested account balance is determined to be less than or equal to $2,000.00 as of the date that the Order is received, the parties will be informed in writing that the QDRO determination fee may potentially liquidate the account.",
   "types" : [ {
      "label" : {
        "nature" : "Obligation",
        "party" : "All Parties"
      },
      "provenance_ids" : ["Nlu0ogWAEGms4vjhhzpMv3iXhm8b8fBqMBNtT/bXH8JI=", "PlyERkjg5is36RpFjVUFXp69eDmGmCxLCXRs1sDMDUCo="
      ]
    } ],
   "categories" : [ {
      "label" : "Communication",
      "provenance_ids" : [ "Cs38YyU6VBFtJK1/bgtEJBlqqWmX5F6OYUciRxQXf7HrN5TOCPuI7QXbkbj4LRXoxVuB3/i9H15q5TU+vFxorhUBeWFfF998OYQiPYViD2yI="
      ]
    } ],
    "attributes" : [ {
      "type" : "Currency",
      "text" : "$2,000.00",
      "location" : {
        "begin" : 134780,
        "end" : 134789
      }
    } ]
 }
 ```
{: codeblock}

각 요소에는 다섯 개의 중요한 섹션이 있습니다.
-  `location`: 입력 문서에서 요소의 일치를 나타내는 `begin` 및 `end` 인덱스입니다.
-  `text`: 분류된 요소의 텍스트입니다.
-  `types`: 0개 이상의 `label` 오브젝트를 포함하는 배열입니다. 각 `label` 오브젝트에는 식별된 당사자에 대한 요소 영향을 나열하는 `nature` 필드(예: `Right` 또는 `Exclusion`) 및 해당 요소의 영향을 받는 당사자를 식별하는 `party` 필드가 포함되어 있습니다. 추가 정보는 [계약 구문 분석에 대한 이해](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing)에서 [유형](/docs/services/discovery?topic=discovery-contract_parsing#contract_types)을 참조하십시오.
-  `categories`: 0개 이상의 `label` 오브젝트를 포함하는 배열입니다. 각 `label` 오브젝트의 값은 식별된 요소가 속하는 기능 카테고리를 나열합니다. 추가 정보는 [계약 구문 분석에 대한 이해](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing)에서 [카테고리](/docs/services/discovery?topic=discovery-contract_parsing#contract_categories)를 참조하십시오.
-  `attributes`: 요소 속성을 정의하는 0개 이상의 오브젝트를 나열하는 배열입니다. 현재 지원되는 속성 유형은 `Location`(요소에서 참조하는 지리적 위치), `DateTime`(요소에서 지정한 날짜, 시간, 날짜 범위 또는 시간 범위) 및 `Currency`(금액 값 및 단위)입니다. `attributes` 배열의 각 오브젝트에는 식별된 요소의 텍스트와 위치도 포함됩니다. 위치는 입력 문서에서 텍스트의 `begin` 및 `end` 인덱스로 정의됩니다. 추가 정보는 [계약 구문 분석](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing)에서 [속성](/docs/services/discovery?topic=discovery-contract_parsing#attributes)을 참조하십시오.

추가로 `types` 및 `categories` 배열의 각 오브젝트에는 `provenance_ids` 배열이 포함됩니다. `provenance_ids` 배열에 나열되는 값은 요소와 연관된 분석의 일부분에 대해 피드백을 보내거나 지원을 받기 위해 IBM에 보낼 수 있는 해시 값입니다. 

일부 문장은 유형 또는 카테고리에 속하지 않고, 이 경우 서비스는 `types` 및 `categories` 배열을 빈 오브젝트로 리턴합니다.
{: note}

일부 문장은 여러 주제를 다루며, 이 경우 서비스는 여러 세트의 `types` 및 `categories` 오브젝트를 리턴합니다.
{: note}

일부 문장에는 식별 가능한 속성이 포함되지 않으며, 이 경우 서비스는 `attributes` 배열을 빈 오브젝트로 리턴합니다.
{: note}
