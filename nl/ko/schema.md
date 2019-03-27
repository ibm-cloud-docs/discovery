---

copyright:
years: 2018, 2019
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

# 출력 스키마에 대한 이해
{: #output_schema}

요소 분류를 사용하여 문서를 수집한 후에는 서비스가 버전 날짜 `2018-10-15` 이상인 다음 스키마에서 JSON 출력을 제공합니다. 출력은 `enriched_html_elements` 오브젝트에 포함됩니다. 

```json
{
  "document": {
    "title": string,
    "html": string,
    "hash": string
  },
  "model_id" : string,
  "model_version" : string,  
  "elements": [
    {
      "location": { 
        "begin": int,
        "end": int
      },
      "text": string,
      "types": [
        {
          "label": { "nature": string, "party": string },
          "provenance_ids": [string, string, ...]
            ...
          ]
        }
        ...
      ],
      "categories": [
        {
          "label": string,
          "provenance_ids": [string, string, ...]
        }
        ...
      ],
      "attributes": [
        {
      	  "type": string,
          "text": string,
          "location": { "begin": int, "end": int }
         }
      ]
    }
    ...
  ],
  "tables": [
    {
      "location" : {
        "begin" : int,
        "end" : int
      },
      "text": string,
      "section_title": {
        "text": string,
        "location": {
          "begin" : int,
          "end" : int
        }
      },
      "table_headers" : [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int
        },
        ...
      ],
      "column_headers" : [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "text_normalized" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int
        },
        ...
      ],
      "row_headers" : [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "text_normalized" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int
        },
        ...
      ],
      "body_cells" : [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int,
          "row_header_ids": [ string ],
          "row_header_texts": [ string ],
          "row_header_texts_normalized": [ string ],
          "column_header_ids": [ string ],
          "column_header_texts": [ string ],
          "column_header_texts_normalized": [ string ],
          "attributes" : [
             {
               "type" : string,
               "text" : string,
               "location" : {
                 "begin" : int,
          "end" : int
        }
             },
             ...
           ]
        },
        ...
      ]
    },
    ...
  ],
  "document_structure": {
    "section_titles": [
      {
        "text": string,
        "location": {
          "begin": int,
          "end": int
        },
        "level": int,
        "element_locations": [
          {
            "begin": int,
            "end": int
          },
          ...
        ]
      },
      ...
    ],
    "leading_sentences": [
      {
        "text": string,
        "location": {
          "begin": int,
          "end": int
        },
        "element_locations": [
          {
            "begin": int,
            "end": int
          },
          ...
        ]
      },
      ...
    ]
  },
  "parties": [
    {
      "party": string,
      "role": string,
      "importance": string,
      "addresses": [
        {
          "text": string,
          "location": {
            "begin": int,
            "end": int
          }
        },
        ...
      ],
      "contacts": [
        {
          "name": string,
          "role": string 
        },
        ...
      ]
    },
    ...
  ],
  "effective_dates": [
    {
      "text": string,
      "confidence_level": string,
      "location": { "begin": int, "end": int }
     },
     ...
  ],
  "contract_amounts": [
    {
      "text": string,
      "confidence_level": string,      
      "location": { "begin": int, "end": int }
    },
    ...
  ],
  "termination_dates": [
    {
      "text": string,
      "confidence_level": string,      
      "location": { "begin": int, "end": int }
    },
    ...
  ]
}
```
{: codeblock}

스키마는 다음으로 구성되어 있습니다.

  - `document`: 다음과 같은 문서에 대한 기본 정보를 나열하는 오브젝트입니다.
    - `title`: 문서 제목입니다(발견되는 경우).
    - `html`: HTML 형식으로 된 입력 문서의 전체 텍스트입니다.
    - `hash`: 입력 문서의 MD5 해시입니다.
  - `model_id`: 서비스에서 사용되는 분석 모델입니다. `/v1/element_classification` 및 `/v1/comparison` 메소드의 경우 기본값은 `contracts`입니다. `/v1/tables` 메소드의 경우 기본값은 `tables`입니다. 이 기본값은 배치 처리 요청 중에 독립형 메소드와 메소드의 사용에 적용됩니다. 
  - `model_version`: 분석 모델의 버전이며 `model_id` 매개변수의 값으로 지정됩니다.
  - `elements`: 서비스에서 발견한 문서 요소의 배열입니다.
    - `location`: 요소의 위치이며 `begin` 및 `end` 인덱스로 정의됩니다.
    - `text`: 요소의 텍스트입니다.
    - `types`: 요소가 무엇인지 그리고 어떤 항목에 영향을 주는지 설명하는 배열입니다.
      - `label`: 다음 요소 쌍을 사용하여 유형을 정의하는 오브젝트입니다.
        - `nature`: 문장에 필요한 조치 유형입니다. 현재 값은 `Definition`, `Disclaimer`, `Exclusion`, `Obligation` 및 `Right`입니다.
        - `party`: 문장이 적용되는 당사자를 식별하는 문자열입니다.
      - `provenance_ids`: 피드백을 제공하거나 지원을 받기 위해 IBM에 보낼 수 있는 하나 이상의 해시 값 배열입니다.
    - `categories`: 요소가 속하는 기능 카테고리를 나열하는 배열입니다. 즉, 요소의 주제입니다.
      - `label`: 식별된 카테고리를 나열하는 문자열입니다. [계약 구문 분석에 대한 이해](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing)에서 [카테고리](/docs/services/discovery?topic=discovery-contract_parsing#contract_categories) 목록을 찾을 수 있습니다.
      - `provenance_ids`: 피드백을 제공하거나 지원을 받기 위해 IBM에 보낼 수 있는 하나 이상의 해시 값 배열입니다.
    - `attributes`: 문서 속성을 식별하는 배열입니다. 배열의 각 오브젝트는 3개의 요소로 구성됩니다.
      - `type`: 속성의 유형입니다. 가능한 값은 `Address`, `Currency`, `DateTime`, `Location`, `Organization` 및 `Person`입니다.
      - `text`: 속성과 연관된 텍스트입니다.
      - `location`: 속성의 위치이며 `begin` 및 `end` 인덱스로 정의됩니다.
  - `tables`\*: 입력 문서에서 식별된 테이블을 정의하는 배열입니다.
    - `location`: 현재 테이블의 위치이며 입력 문서에서 `begin` 및 `end` 인덱스로 정의됩니다.
    - `text`: 연관된 마크업 컨텐츠가 없는 입력 문서에 있는 현재 테이블의 텍스트 컨텐츠입니다.
    - `section_title`: 현재 테이블에 포함된 섹션 제목의 위치입니다(식별되는 경우). 섹션 제목이 식별되지 않으면 비어 있습니다.
      - `text`: 식별된 섹션 제목의 텍스트입니다.
      - `location`: 섹션 제목의 위치이며 입력 문서에서 `begin` 및 `end` 인덱스로 정의됩니다.
    - `table_header`: 현재 테이블의 모든 기타 셀에 대한 헤더로 사용할 수 있는 테이블 레벨 셀의 배열입니다. 각 테이블 헤더는 다음 요소의 콜렉션으로 정의됩니다.
      - `cell_id`: `tableHeader-x-y` 형식의 문자열 값입니다. 여기서, `x` 및 `y`는 원본 입력 문서에 있는 셀 값의 시작 및 끝 오프셋입니다.
      - `location`: 셀의 위치이며 입력 문서에서 `begin` 및 `end` 인덱스로 정의됩니다.
      - `text`: 연관된 마크업 컨텐츠가 없는 입력 문서에 있는 셀의 텍스트 컨텐츠입니다.
      - `row_index_begin`: 현재 테이블에 있는 셀의 `row` 위치에 대한 `begin` 인덱스입니다.
      - `row_index_end`: 현재 테이블에 있는 셀의 `row` 위치에 대한 `end` 인덱스입니다.
      - `column_index_begin`: 현재 테이블에 있는 셀의 `column` 위치에 대한 `begin` 인덱스입니다.
      - `column_index_end`: 현재 테이블에 있는 셀의 `column` 위치에 대한 `end` 인덱스입니다.
    - `column_headers`: 열 레벨 셀의 배열입니다. 각각을 현재 테이블과 동일한 열에 있는 다른 셀의 헤더로 사용할 수 있습니다. 각 열 헤더는 다음 항목의 콜렉션으로 정의됩니다.
      - `cell_id`: `columnHeader-x-y` 형식의 문자열 값입니다. 여기서, `x` 및 `y`는 입력 문서에 있는 이 열 헤더 셀의 시작 및 끝 오프셋입니다.
      - `location`: 셀의 위치이며 입력 문서에서 `begin` 및 `end` 인덱스로 정의됩니다.
      - `text`: 연관된 마크업 컨텐츠가 없는 입력 문서에 있는 셀의 텍스트 컨텐츠입니다.
      - `text_normalized`: 사용자 정의 입력을 제공하는 경우 사용자 정의에 따라 정규화된 버전의 셀 텍스트입니다. 그렇지 않은 경우 `text` 값과 동일합니다. 
      - `row_index_begin`: 현재 테이블에 있는 셀의 `row` 위치에 대한 `begin` 인덱스입니다.
      - `row_index_end`: 현재 테이블에 있는 셀의 `row` 위치에 대한 `end` 인덱스입니다.
      - `column_index_begin`: 현재 테이블에 있는 셀의 `column` 위치에 대한 `begin` 인덱스입니다.
      - `column_index_end`: 현재 테이블에 있는 셀의 `column` 위치에 대한 `end` 인덱스입니다.
    - `row_headers`: 행 레벨 셀의 배열입니다. 각각을 현재 테이블과 동일한 행에 있는 다른 셀의 헤더로 사용할 수 있습니다. 각 행 헤더는 다음 항목의 콜렉션으로 정의됩니다.
      - `cell_id`: `rowHeader-x-y` 형식의 문자열 값입니다. 여기서, `x` 및 `y`는 입력 문서에 있는 이 행 헤더 셀의 시작 및 끝 오프셋입니다.
      - `location`: 셀의 위치이며 입력 문서에서 `begin` 및 `end` 인덱스로 정의됩니다.
      - `text`: 연관된 마크업 컨텐츠가 없는 입력 문서에 있는 셀의 텍스트 컨텐츠입니다.
      - `text_normalized`: 사용자 정의 입력을 제공하는 경우 사용자 정의에 따라 정규화된 버전의 셀 텍스트입니다. 그렇지 않은 경우 `text` 값과 동일합니다. 
      - `row_index_begin`: 현재 테이블에 있는 셀의 `row` 위치에 대한 `begin` 인덱스입니다.
      - `row_index_end`: 현재 테이블에 있는 셀의 `row` 위치에 대한 `end` 인덱스입니다.
      - `column_index_begin`: 현재 테이블에 있는 셀의 `column` 위치에 대한 `begin` 인덱스입니다.
      - `column_index_end`: 현재 테이블에 있는 셀의 `column` 위치에 대한 `end` 인덱스입니다.
    - `body_cells`: 해당 행 및 열 헤더가 연관된 현재 테이블의 테이블 헤더 또는 열 헤더 또는 행 헤더 셀이 아닌 셀의 배열입니다. 각 본문 셀은 다음 항목의 콜렉션으로 정의됩니다.
      - `cell_id`: `bodyCell-x-y` 형식의 문자열 값입니다. 여기서, `x` 및 `y`는 입력 문서에 있는 이 본문 셀의 시작 및 끝 오프셋입니다.
      - `location`: 셀의 위치이며 입력 문서에서 `begin` 및 `end` 인덱스로 정의됩니다.
      - `text`: 연관된 마크업 컨텐츠가 없는 입력 문서에 있는 셀의 텍스트 컨텐츠입니다.
      - `row_index_begin`: 현재 테이블에 있는 이 셀의 `row` 위치에 대한 `begin` 인덱스입니다.
      - `row_index_end`: 현재 테이블에 있는 이 셀의 `row` 위치에 대한 `end` 인덱스입니다.
      - `column_index_begin`: 현재 테이블에 있는 이 셀의 `column` 위치에 대한 `begin` 인덱스입니다.
      - `column_index_end`: 현재 테이블에 있는 이 셀의 `column` 위치에 대한 `end` 인덱스입니다.
      - `row_header_ids`: 이 본문 셀에 사용할 수 있는 행 헤더의 `cell_id` 값 배열입니다.
      - `row_header_texts`: 이 본문 셀에 사용할 수 있는 행 헤더의 `text` 값 배열입니다.
      - `row_header_texts_normalized`: 사용자 정의 입력을 제공하는 경우 사용자 정의에 따라 정규화된 버전의 행 헤더 텍스트입니다. 그렇지 않은 경우 `row_header_texts` 값과 동일합니다. 
      - `column_header_ids`: 이 본문 셀에 사용할 수 있는 열 헤더의 `cell_id` 값 배열입니다.
      - `column_header_texts`: 이 본문 셀에 사용할 수 있는 열 헤더의 `text` 값 배열입니다.
      - `column_header_texts_normalized`: 사용자 정의 입력을 제공하는 경우 사용자 정의에 따라 정규화된 버전의 열 헤더 텍스트입니다. 그렇지 않은 경우 `column_header_texts` 값과 동일합니다.
      - `attributes`: 문서 속성을 식별하는 배열입니다. 배열의 각 오브젝트는 3개의 요소로 구성됩니다.
        - `type`: 속성의 유형입니다. 가능한 값은 `Address`, `Currency`, `DateTime`, `Location`, `Organization` 및 `Person`입니다.
        - `text`: 속성과 연관된 텍스트입니다.
        - `location`: 속성의 위치이며 `begin` 및 `end` 인덱스로 정의됩니다.
  - `document_structure`: 입력 문서의 구조를 설명하는 오브젝트입니다.
    - `section_titles`: 입력 문서에서 발견된 섹션 또는 서브섹션당 하나의 오브젝트를 포함하는 배열입니다. 섹션 및 서브섹션은 중첩되지 않습니다. 대신 동등하게 펼쳐지고 요소의 `begin` 및 `end` 값과 섹션의 `level` 값을 사용하면 순서대로 다시 배치할 수 있습니다.
      - `text`: 섹션 제목을 나열하는 문자열입니다(발견되는 경우).
      - `location`: 제목의 위치이며 입력 문서에서 `begin` 및 `end` 인덱스로 정의됩니다.
      - `level`: 입력 문서에서 섹션이 있는 레벨을 나타내는 정수입니다. 예를 들어 최상위 레벨을 나타내고 레벨 섹션 내의 서브섹션을 나타냅니다.
      - `element_locations`: 섹션에서 문장의 `begin` 및 `end` 값을 지정하는 배열입니다.
    - `leading_sentences`: `section_titles` 배열과 병렬을 이루며 섹션 또는 서브섹션당 하나의 오브젝트를 포함하는 배열입니다. 일치하는 섹션 또는 서브섹션에서 선행 문장을 자세히 설명합니다. `section_titles` 배열에서와 같이 오브젝트가 중첩되지 않습니다. 대신 동등하게 펼쳐지고 요소의 `begin` 및 `end` 값 또는 입력 문서의 레벨 마커를 사용하면 순서대로 다시 배치할 수 있습니다.
      - `text`: 선행 문장을 나열하는 문자열입니다(발견되는 경우).
      - `location`: 선행 문장의 위치이며 입력 문서에서 `begin` 및 `end` 인덱스로 정의됩니다.
      - `element_locations`: 섹션에서 선행 문장의 `begin` 및 `end` 값을 지정하는 배열입니다.
  - `parties`: 서비스에서 식별되는 당사자를 정의하는 배열입니다.
    - `party`: 당사자를 식별하는 문자열 값입니다.
    - `role`: 당사자의 역할을 식별하는 문자열 값입니다.
    - `importance`: 당사자의 중요성을 식별하는 문자열 값입니다. 가능한 값에는 `Primary`(기본 당사자용) 및 `Unknown`(비기본 당사자)이 포함됩니다.
    - `addresses`: 주소를 식별하는 오브젝트의 배열입니다.
      - `text`: 주소를 포함하는 문자열입니다.
      - `location`: 주소의 위치이며 `begin` 및 `end` 인덱스로 정의됩니다.
    - `contacts`: 입력 문서에서 식별되는 담당자의 이름 및 역할을 정의하는 배열입니다. 
      - `name`: 식별된 연락처의 이름을 나열하는 문자열입니다.
      - `role`: 식별된 연락처의 역할을 나열하는 문자열입니다.  
  - `effective_dates`: 문서의 유효 날짜를 식별하는 배열입니다.
    - `text`: 문자열로 나열되는 유효 날짜입니다. 
    - `confidence_level`: 유효 날짜 ID의 신뢰수준입니다. 가능한 값은 `High`, `Medium` 및 `Low`입니다.
    - `location`: 날짜의 위치이며 `begin` 및 `end` 인덱스로 정의됩니다.
  - `contract_amounts`: 문서에서 식별된 금액을 식별하는 배열입니다.
    - `text`: 문자열로 나열되는 계약 금액입니다. 
    - `confidence_level`: 계약 금액 ID의 신뢰수준입니다. 가능한 값은 `High`, `Medium` 및 `Low`입니다.    
    - `location`: 금액의 위치이며 `begin` 및 `end` 인덱스로 정의됩니다.
  - `termination_dates`: 문서의 종료 날짜를 식별하는 배열입니다. 
    - `text`: 문자열로 나열되는 종료 날짜입니다. 
    - `confidence_level`: 종료 날짜 ID의 신뢰수준입니다. 가능한 값은 `High`, `Medium` 및 `Low`입니다.    
    - `location`: 날짜의 위치이며 `begin` 및 `end` 인덱스로 정의됩니다.

**\*테이블 참고사항:**
  - 셀당 행 및 열 인덱스 값은 0 기반이므로 `0`부터 시작하십시오.
  - `row_header_ids` 및 `row_header_texts` 요소 배열의 다중 값은 행 헤더의 가능한 계층 구조를 나타냅니다.
  - `column_header_ids` 및 `column_header_texts` 요소 배열의 다중 값은 열 헤더의 가능한 계층 구조를 나타냅니다.
