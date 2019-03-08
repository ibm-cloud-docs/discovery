---

copyright:
  years: 2015, 2018
lastupdated: "2018-01-23"

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

# 구성 참조
{: #configref}

데이터에 특수 [변환](#conversion), [인리치먼트](#enrichment) 또는 [정규화](#normalization) 요구사항이 있는 경우 JSON으로 고유한 {{site.data.keyword.discoveryshort}} 수집 구성을 작성할 수 있습니다.
{: shortdesc}

 다음 절에서는 이 JSON의 구조 및 JSON으로 정의할 수 있는 오브젝트에 대해 자세히 설명합니다.

## 구성의 구조
{: #structure}

{{site.data.keyword.discoveryshort}} 구성은 다음과 같이 구조화됩니다.

```json
{
  "name": "Configuration Name",
  "description": "Descriptive text about the configuration",
  "conversions": {
    "word": {},
    "pdf": {},
    "html": {},
    "segment": {},
    "json_normalizations": []
  },
  "enrichments": [],
  "normalizations": []
}
```
{: codeblock}

기본 JSON 오브젝트에는 다음 항목이 포함됩니다.

-  `"name": "Configuration Name"` - 구성 이름입니다.
-  `"description": "Descriptive text about the configuration"` - 구성 설명입니다.

다음 오브젝트 및 배열이 콜렉션에 업로드되는 문서를 변환, 강화 및 정규화하기 위해 정의되어야 합니다.

- `"conversions": {}` - 문서를 강화할 수 있는 JSON으로 변환하는 방법입니다.
- `"enrichments": []` - JSON의 일부로 적용되는 인리치먼트입니다.
- `"normalizations": []` - 문서 저장 전에 필요한 모든 사후 인리치먼트 조정입니다.

또한 구성이 저장/업데이트될 때 다음 항목이 {{site.data.keyword.discoveryshort}}를 통해 기본 오브젝트에 추가됩니다.

```json
{
  "configuration_id": "4f5b7c7b-ebf4-4963-882e-27eff08f08e3",
  "created": "2017-09-13T14:45:03.575Z",
  "updated": "2017-09-13T14:45:03.575Z"
}
```
{: codeblock}

## 변환
{: #conversion}

문서 변환은 원래의 소스 형식을 가져와서 하나 이상의 단계를 사용하여 나머지 수집 프로세스에 사용할 수 있는 JSON으로 변환합니다. 업로드된 파일 유형에 따른 프로세스는 다음과 같습니다.

- **PDF** 파일은 `pdf` 옵션을 사용하여 HTML로 변환됩니다. 그런 다음, 결과 **HTML**이 `html` 옵션을 사용하여 JSON으로 변환되고, 마지막으로 결과 **JSON**이 `json` 옵션을 사용하여 변환됩니다.

- **Microsoft Word** 파일은 `word` 옵션을 사용하여 HTML로 변환됩니다. 그런 다음, 결과 **HTML**이 `html` 옵션을 사용하여 JSON으로 변환되고, 마지막으로 결과 **JSON**이 `json` 옵션을 사용하여 변환됩니다.

- **HTML** 파일은 `html` 옵션을 사용하여 JSON으로 변환되며, 결과 **JSON**이 `json` 옵션을 사용하여 변환됩니다.

- **JSON** 파일은 `json` 옵션을 사용하여 변환됩니다.

이러한 옵션은 다음 절에서 설명됩니다. 변환이 완료된 후 컨텐츠가 저장되기 전에 [인리치먼트](#enrichment) 및 [정규화](#normalization)가 수행됩니다.

### PDF
{: #pdf}

`pdf` 변환 오브젝트는 PDF 문서가 HTML로 변환되어야 하는 방법을 정의하며 다음과 같은 구조로 되어 있습니다.

```json
"pdf": {
  "heading": {
    "fonts": [
      {
        "level": 1,
        "min_size": 24,
        "max_size": 80,
        "bold": false,
        "italic": true,
        "name": "arial"
      },
      {
        "level": 2,
        "min_size": 18,
        "max_size": 24,
        "bold": true,
        "italic": false,
        "name": "ariel"
      }
    ]
  }
},
```
{: codeblock}

PDF 파일을 변환할 때 각 표제 레벨의 크기, 글꼴 및 스타일을 식별하여 해당 파일의 표제를 식별할 수 있습니다(또한 적절한 HTML "`h`" 태그로 변환할 수 있음). 모든 관련 섹션을 올바르게 식별하기 위해 필요한 경우 여러 번 표제 레벨을 지정할 수 있습니다. HTML 표제 레벨은 CSS 선택기를 사용하여 컨텐츠를 추출할 계획이 있는지 아니면 문서 분할을 사용하여 문서를 분할할 계획이 있는지 식별하는 데 중요합니다. `heading` 오브젝트에는 `fonts` 배열이 있으며 해당 배열의 각 항목은 다음 매개변수를 사용하여 표제 레벨을 지정합니다.

- `"level": INT` - *필수* - 이 매개변수로 식별된 텍스트가 변환될 HTML `h` 레벨입니다.
- `"min_size": INT` - _선택사항_ - 표제 레벨로 식별되는 가장 작은 글꼴 크기입니다.
- `"max_size": INT` - _선택사항_ - 표제 레벨로 식별되는 가장 큰 글꼴 크기입니다.
- `"bold": boolean` - _선택사항_ - `true`인 경우 굵은체만 이 표제 레벨로 식별됩니다.
- `"italic": boolean` - _선택사항_ - `true`인 경우 기울임체만 이 표제 레벨로 식별됩니다.
- `"name": "string"` - _선택사항_ - 이 표제 레벨로 식별되는 글꼴의 이름입니다.

표제로 식별된 텍스트 영역의 경우 특정 배열 항목에 정의된 모든 매개변수와 일치해야 합니다. 정의된 매개변수가 지나치게 유연한 경우 예상보다 더 많은 식별된 표제가 있을 수 있습니다. 올바르지 않은 일치 항목 없이 모든 표제 레벨 변수가 포함되었는지 확인하기 위해 각 표제 레벨을 여러 번 엄격하게 정의하면 더 나은 결과를 얻게 됩니다.


### Word
{: #word}

`word` 변환 오브젝트는 PDF 문서가 HTML로 변환되어야 하는 방법을 정의하며 다음과 같은 구조로 되어 있습니다.

```json
"word": {
  "heading": {
    "fonts": [
      {
        "level": 1,
        "min_size": 24,
        "bold": true,
        "italic": false,
        "name": "arial"
      },
      {
        "level": 2,
        "min_size": 18,
        "max_size": 23,
        "bold": true,
        "italic": false
      }
    ],
    "styles": [
      {
        "level": 1,
        "names": [
          "pullout heading",
          "pulloutheading",
          "header"
        ]
      },
      {
        "level": 2,
        "names": [
          "subtitle"
        ]
      }
    ]
  }
},
```
{: codeblock}

Microsoft Word 변환 오브젝트는 PDF 변환 오브젝트와 유사한 방식으로 작동합니다. 그러나 Microsoft Word 문서에서 표제를 추출할 때 `heading` 오브젝트 내부에 지정될 수 있는 두 개의 다른 배열이 있습니다. Microsoft Word 문서에서 표제 레벨 요소를 추출하는 데 하나 또는 두 개의 표제 추출 배열을 사용할 수 있습니다.

`fonts` 배열의 각 항목은 글꼴 특성을 통해 다음 매개변수를 사용하여 표제 레벨을 지정합니다.

- `"level": INT` - *필수* - 이 매개변수로 식별된 텍스트가 변환될 HTML `h` 레벨입니다.
- `"min_size": INT` - _선택사항_ - 표제 레벨로 식별되는 가장 작은 글꼴 크기입니다.
- `"max_size": INT` - _선택사항_ - 표제 레벨로 식별되는 가장 큰 글꼴 크기입니다.
- `"bold": boolean` - _선택사항_ - `true`인 경우 굵은체만 이 표제 레벨로 식별됩니다.
- `"italic": boolean` - _선택사항_ - `true`인 경우 기울임체만 이 표제 레벨로 식별됩니다.
- `"name": "string"` - _선택사항_ - 이 표제 레벨로 식별되는 글꼴의 이름입니다.

`fonts` 배열에서 표제로 식별된 텍스트 영역의 경우 특정 배열 항목에 정의된 모든 매개변수와 일치해야 합니다. 정의된 매개변수가 지나치게 유연한 경우 예상보다 더 많은 식별된 표제가 있을 수 있습니다. 올바르지 않은 일치 항목 없이 모든 표제 레벨 변수가 포함되었는지 확인하기 위해 각 표제 레벨을 여러 번 엄격하게 정의하면 더 나은 결과를 얻게 됩니다.

`styles` 배열의 각 항목은 해당 구문에 적용되는 Microsoft Word 스타일에서 표제 레벨을 지정합니다.

- `"level": INT` - *필수* - 이 매개변수로 식별된 텍스트가 변환될 HTML `h` 레벨입니다.
- `"names": array` - *필수* - 이 표제 레벨로 식별될 스타일 이름의 배열이며, 쉼표로 구분됩니다.

*fonts 사용 시점 및 styles 사용 시점* - Microsoft Word 문서가 각 단락이 적절한 스타일로 올바르게 태그 지정된 스타일시트를 잘 따르는 경우 `styles`를 사용하여 표제를 추출하는 것이 좋습니다. 그러나 일부 문서에 작성자가 수동으로 겹쳐쓴 스타일이 있을 수 있습니다. 이러한 문서는 `fonts` 추출 메소드가 사용될 때 더 나은 변환을 제공할 가능성이 높습니다.
{: tip}


### HTML
{: #html}

```json
"html": {
  "exclude_tags_completely": [
    "script",
    "sup"
  ],
  "exclude_tags_keep_content": [
    "font",
    "em"
  ],
  "exclude_content": {
    "xpaths": [
      "//*[@id='list-old']",
      "//*[@id='unstable']"
    ]
  },
  "keep_content": {
    "xpaths": [
      "//*[@id='footer']",
      "//*[@id='header']"
    ]
  },
  "exclude_tag_attributes": [
    "EVENT_ACTIONS"
  ],
  "keep_tag_attributes": [
    "id"
  ],
  "extracted_fields": {
    "{field_name}": {
      "css_selector": "{CSS_selector_expression_1}",
      "type": "{field_type}"
    }
  }
},
```
{: codeblock}

#### exclude_tags_completely

`"exclude_tags_completely" : array` - 제외할 HTML 태그 이름의 배열입니다. 여기에는 태그, 컨텐츠 및 지정된 모든 태그 속성이 포함됩니다.

#### exclude_tags_keep_content

`"exclude_tags_keep_content" : array` - 태그 정보가 제거된 HTML 태그 이름의 배열입니다. 결과적으로 HTML 태그 및 태그 속성이 스트라이프됩니다. 태그의 컨텐츠가 지정되지 않으면 더 이상 스트라이프되지 않습니다. 예를 들어, `span` HTML 태그에 `exclude_tags_keep_content`를 지정하는 경우 `<span class="info">일부 <strong>정보</strong></span>`가 `일부 <strong>정보</strong>`로 스트라이프됩니다.

#### exclude_content

`"xpaths" : array` - 제거되는 컨텐츠를 식별하는 XPaths의 배열입니다. 이 값이 설정되면 XPaths 중 하나와 일치하는 항목이 출력에서 제거됩니다.

#### keep_content

`"xpaths" : array` - 변환되는 컨텐츠를 식별하는 XPaths의 배열입니다. 이 값이 설정되면 XPaths 중 하나와 일치하는 항목이 출력에 포함됩니다. 이 매개변수로 지정된 포함은 `exclude_content`로 지정된 처리 후에 처리됩니다.

#### exclude_tag_attributes

`"exclude_tag_attributes" : array` - HTML 속성이 표시되는 HTML 태그와 관계 없이 변환으로 제거되는 HTML 속성 이름의 배열입니다. **참고:** 동일한 구성에서 `exclude_tag_attributes` 및 `keep_tag_attributes`를 모두 지정하면 오류 메시지를 받습니다. 구성당 하나만 지정할 수 있습니다. `keep_tag_attributes`가 있는 경우 구성에서 완전히 제거해야 합니다. 비어 있는 배열로 존재할 수는 없습니다.

#### keep_tag_attributes

`"keep_tag_attributes" : array` - 변환으로 유지되는 HTML 속성 이름의 배열입니다. **참고:** 동일한 구성에서 `keep_tag_attributes` 및 `exclude_tag_attributes`를 모두 지정하면 오류 메시지를 받습니다. 구성당 하나만 지정할 수 있습니다. `exclude_tag_attributes`가 있는 경우 구성에서 완전히 제거해야 합니다. 비어 있는 배열로 존재할 수는 없습니다.

#### extracted_fields

이 오브젝트는 변환의 일부로 개별 JSON 필드로 추출될 HTML 소스의 컨텐츠를 정의합니다. 컨텐츠는 CSS 선택기를 사용하여 식별됩니다.

작성할 각 필드는 다음과 같이 오브젝트로 정의됩니다.

```json
"{field_name}": {
  "css_selector": "{CSS_selector_expression_1}",
  "type": "{field_type}"
}
```
{: codeblock}

- `"{field_name}"` - 작성할 필드의 이름입니다.

**참고:** 구성에 정의된 필드 이름은 [필드 이름 요구사항](#field_reqs)에 정의된 제한사항을 충족해야 합니다.

- `"css_selector" : string` *필수* - 필드에 저장할 컨텐츠의 영역을 정의하는 CSS 선택기 표현식입니다.
- `"type" : string` *필수* - 작성할 필드의 유형으로, `string`, `date`가 해당될 수 있습니다.
자세한 정보는 [CSS 선택기를 사용하여 필드 추출](/docs/services/discovery/building.md#using-css)을 참조하십시오.

### 세그먼트
{: #segment}

`segment` 오브젝트는 식별된 표제(`h1`, `h2`)를 기반으로 수집된 문서를 하나 이상의 세그먼트로 분할하는 구성 옵션의 세트입니다.

```json
"segment": {
  "enabled": true,
  "selector_tags": ["h1", "h2", "h3", "h4", "h5", "h6"]
}
```
{: codeblock}

- `"enabled": boolean` - *필수* - 문서 세그먼트화를 사용으로 설정하려면 `true`로 설정해야 합니다.
- `"selector_tags": array` - *필수* - 문서를 분할할 HTML `h` 태그의 배열이며, 쉼표로 구분됩니다.

개요로서, 문서 세그먼트화가 사용으로 설정되면 다음 항목을 지정할 수 없습니다.

-  `json_normalizations`는 구성의 일부로 지정될 수 없습니다.
-  `normalizations`는 구성의 일부로 지정될 수 없습니다.
-  `html` 변환의 `extracted_fields` 옵션은 구성의 일부로 변환될 수 없습니다.

자세한 정보는 [세그먼트화 수행](/docs/services/discovery/building.html#performing-segmentation)을 참조하십시오.


### JSON
{: #json}

`json_normalizations` 배열에서 `operation` 오브젝트를 정의하여 수집된 JSON의 사전 인리치먼트 정규화를 수행할 수 있습니다.

```json
"json_normalizations": [
  {
    "operation": "remove",
    "source_field": "header"
  },
  {
    "operation": "copy",
    "source_field": "title",
    "destination_field": "title_old"
  },
  {
    "operation": "move",
    "destination_field": "content",
    "source_field": "body"
  },
  {
    "operation": "merge",
    "source_field": "synopsis",
    "destination_field": "preamble"
  },
  {
    "operation": "remove_nulls"
  }
]
```
{: codeblock}

#### 오퍼레이션 오브젝트
{: #operations}

- `"operation": string` - *필수* - JSON에서 수행될 오퍼레이션은 다음 중 하나여야 합니다.
  - `remove` - 지정된 `source_field`가 JSON에서 제거됩니다.
  - `copy` - 지정된 `source_field` 컨텐츠가 `destination_field`의 새 인스턴스로 복사됩니다.
  - `move` - 지정된 `source_field`가 `destination_field`로 이름이 바뀝니다. `destination_field`가 이미 존재하면 `destination_field`의 새 인스턴스가 작성됩니다.
  - `merge` - `source_field` 및 `destination_field`의 컨텐츠가 `destination_field`로 병합됩니다.
  - `remove_nulls` - `null` 컨텐츠가 사용된 필드가 제거됩니다.
- `"source_field": string` - _선택사항_ - 오퍼레이션이 수행될 필드입니다.
- `"destination_field": string` - _선택사항_ - 오퍼레이션이 출력될 대상 필드입니다.  

  **참고:** 구성에 정의된 필드 이름은 [필드 이름 요구사항](#field_reqs)에 정의된 제한사항을 충족해야 합니다.


## 인리치먼트
{: #enrichments}

```json
"enrichments": [
   {
    "enrichment": "elements",
    "source_field": "html",
    "destination_field": "enriched_html",
    "options": {
      "model": "contract"
    }
  },
  {
    "enrichment": "natural_language_understanding",
    "source_field": "title",
    "destination_field": "enriched_title",
    "options": {
      "features": {
        "keywords": {
          "sentiment": true,
          "emotion": false,
          "limit": 50
        },
        "entities": {
          "sentiment": true,
          "emotion": false,
          "limit": 50,
          "mentions": true,
          "mention_types": true,
          "sentence_locations": true,        
          "model": "WKS-model-id"
        },
        "sentiment": {
          "document": true,
          "targets": [
            "IBM",
            "Watson"
          ]

        },
        "emotion": {
          "document": true,
          "targets": [
            "IBM",
            "Watson"
          ]
        },
        "categories": {},
        "concepts": {
          "limit": 8
        },
        "semantic_roles": {
          "entities": true,
          "keywords": true,
          "limit": 50
        },
        "relations": {
          "model": "WKS-model-id"
        }
      }
    }
  }
]
```
{: codeblock}

{{site.data.keyword.discoveryshort}}는 {{site.data.keyword.nlushort}} 및 요소 분류 인리치먼트의 추가를 지원합니다. 강화할 각 필드는 `enrichments` 배열의 오브젝트로 정의됩니다. 각 인리치먼트 오브젝트에는 `source_field`, `destination_field` 및 인리치먼트가 지정되어야 합니다.

- `"enrichment" : string` - *필수* - 이 필드에 사용할 인리치먼트의 유형입니다. {{site.data.keyword.nlushort}} 인리치먼트를 추출하려면 `natural_language_understanding`을 사용하고, 요소 분류를 수행하려면 `elements`를 사용하십시오.

  **참고:** `elements` 인리치먼트를 사용하는 경우 [요소 분류](/docs/services/discovery/element-classification.html) 문서에 지정된 가이드라인을 따르는 것이 중요합니다. 특히 이 인리치먼트가 지정될 때는 PDF 파일만 수집할 수 있습니다.

- `"source_field" : string` - *필수* - 강화될 소스 필드입니다. 이 필드는 `json_normalizations` 오퍼레이션이 완료된 후 소스에 존재해야 합니다.
- `"destination_field" : string` - *필수* - 인리치먼트가 작성될 컨테이너 오브젝트의 이름입니다.

  **참고:** 구성에 정의된 필드 이름은 [필드 이름 요구사항](#field_reqs)에 정의된 제한사항을 충족해야 합니다.

### 요소 분류 인리치먼트

요소 분류를 사용할 때 각 `elements` 인리치먼트 오브젝트에는 지정된 다음 매개변수와 함께 `"options": {}` 오브젝트가 포함되어야 합니다.

- `"model" : string` - *필수* - 이 문서에 사용될 요소 추출 모델입니다. 현재 지원되는 모델은 `contract`입니다.

**참고:** `elements` 인리치먼트를 사용하는 경우 [요소 분류](/docs/services/discovery/element-classification.html) 문서에 지정된 가이드라인을 따르는 것이 중요합니다. 특히 이 인리치먼트가 지정될 때는 PDF 파일만 수집할 수 있습니다.

### Natural Language Understanding(NLU) 인리치먼트

{{site.data.keyword.nlushort}}을 사용할 때 `enrichments` 배열 내의 각 오브젝트는 다음 인리치먼트 중 하나 이상이 포함된 `"options": { "features": { } }` 오브젝트도 포함해야 합니다.

### categories

`categories` 인리치먼트는 수집된 문서의 일반 카테고리를 식별합니다. 이 인리치먼트는 옵션을 포함하지 않으며 비어 있는 오브젝트 `"categories" : {}`로 지정되어야 합니다.

### concepts

`concepts` 인리치먼트는 해당 텍스트에 있는 기타 개념 및 엔티티를 기반으로 입력 텍스트가 연관되는 개념을 찾습니다.

- `"limit" : INT` - *필수* - 수집된 문서에서 추출할 최대 개념의 수입니다.

### emotion

`emotion` 인리치먼트는 전체 문서의 전반적인 감정적 어조(예: `anger`) 또는 전체 문서의 지정된 대상 문자열을 평가합니다. 이 인리치먼트는 영어 컨텐츠에서만 사용될 수 있습니다.

- `"document" : boolean ` _선택사항_ - `true`이면 전체 문서의 감정적 어조가 평가됩니다.
- `"targets" : array ` _선택사항_ - 문서 내의 감정 상태를 평가할 대상 문자열의 배열이며, 쉼표로 구분됩니다.

### entities

`entities` 인리치먼트는 알려진 엔티티(예: 사람, 위치 및 조직)의 인스턴스를 추출합니다. 선택적으로, 사용자 정의 엔티티를 추출하는 데 {{site.data.keyword.knowledgestudioshort}} 사용자 정의 모델을 지정할 수 있습니다.

- `"sentiment" : boolean` - _선택사항_ - `true`이면 감성 분석이 주변 컨텐츠의 컨텍스트에 있는 추출된 엔티티에서 수행됩니다.
- `"emotion" : boolean` - _선택사항_ - `true`이면 감정적 어조 분석이 주변 컨텐츠의 컨텍스트에 있는 추출된 엔티티에서 수행됩니다.
- `"limit" : INT` - _선택사항_ - 수집된 문서에서 추출할 최대 엔티티의 수입니다. 기본값은 `50`입니다.
- `"mentions": boolean` - _선택사항_ - `true`이면 이 엔티티가 언급된 횟수가 기록됩니다. 기본값은 `false`입니다.
- `"mention_types": boolean` - _선택사항_ - `true`이면 이 엔티티의 각 언급에 대한 언급 유형이 저장됩니다. 기본값은 `false`입니다.
- `"sentence_location": boolean` - _선택사항_ - `true`이면 각 엔티티 언급의 문장 위치가 저장됩니다. 기본값은 `false`입니다.
- `"model" : string` - _선택사항_ - 지정되면 공용 모델 대신 사용자 정의 모델이 엔티티를 추출하는 데 사용됩니다. 이 옵션에서는 {{site.data.keyword.knowledgestudioshort}} 사용자 정의 모델이 {{site.data.keyword.discoveryshort}}의 인스턴스와 연관되어야 합니다. 자세한 정보는 [Watson Knowledge Studio와 통합](/docs/services/discovery/integrate-wks.html)을 참조하십시오.

### keywords

`keywords` 인리치먼트는 텍스트 내 중요 단어의 인스턴스를 추출합니다. 키워드, 개념 및 엔티티 간의 차이점을 이해하려면 [엔티티, 개념 및 키워드 간의 차이점 이해](/docs/services/discovery/building.html#udbeck)를 참조하십시오.

- `"sentiment" : boolean` - _선택사항_ - `true`이면 감성 분석이 주변 컨텐츠의 컨텍스트에 있는 추출된 키워드에서 수행됩니다.
- `"emotion" : boolean` - _선택사항_ - `true`이면 감정적 어조 분석이 주변 컨텐츠의 컨텍스트에 있는 추출된 키워드에서 수행됩니다.
- `"limit" : INT` - _선택사항_ - 수집된 문서에서 추출할 최대 키워드의 수입니다. 기본값은 `50`입니다.

### semantic_roles

`semantic_roles` 인리치먼트는 수집된 텍스트 내 문장 컴포넌트(예: 주체, 동작 및 객체)를 식별합니다.

- `"entities" : boolean` - _선택사항_ - `true`이면 엔티티가 문장 컴포넌트에서 추출됩니다.
- `"keywords" : boolean` - _선택사항_ - `true`이면 키워드가 문장 컴포넌트에서 추출됩니다.
- `"limit" : INT` - _선택사항_ - 수집된 문서에서 구문 분석하기 위한 문장을 추출할 최대 `semantic_roles` 오브젝트의 수입니다. 기본값은 `50`입니다.

### sentiment

`sentiment` 인리치먼트는 전체 문서의 전체 감성 레벨 또는 전체 문서의 지정된 대상 문자열을 평가합니다.

- `"document" : boolean ` _선택사항_ - `true`이면 전체 문서의 감성이 평가됩니다.
- `"targets" : array ` _선택사항_ - 문서 내의 감성을 평가할 대상 문자열의 배열이며, 쉼표로 구분됩니다.

### relations

`relations` 인리치먼트는 문서 내 식별된 엔티티 간의 알려진 관계를 추출합니다. 선택적으로, 사용자 정의 관계를 추출하는 데 {{site.data.keyword.knowledgestudioshort}} 사용자 정의 모델을 지정할 수 있습니다.

- `"model" : string` - _선택사항_ - 지정되면 공용 모델 대신 사용자 정의 모델이 관계를 추출하는 데 사용됩니다. 이 옵션에서는 {{site.data.keyword.knowledgestudioshort}} 사용자 정의 모델이 {{site.data.keyword.discoveryshort}}의 인스턴스와 연관되어야 합니다. 자세한 정보는 [Watson Knowledge Studio와 통합](/docs/services/discovery/integrate-wks.html)을 참조하십시오.

## 정규화
{: #normalization}

`normalizations`는 `enrichments`가 적용된 후와 저장되기 전에 수집된 JSON을 정리하는 데 사용되는 JSON `operation` 오브젝트의 배열입니다.

```json
"normalizations": [
  {
    "operation": "remove",
    "source_field": "enriched_title.entities.text"
  },
  {
    "operation": "copy",
    "source_field": "enriched_title.sentiment.document.score",
    "destination_field": "titlescore"
  }
]
```
{:codeblock}

`operation` 오브젝트 옵션은 [여기](#operations)에 나열되어 있습니다.

## 필드 이름 요구사항
{: #field_reqs}

필드 이름에는 공백이 포함될 수 없습니다. 다음 문자 및 문자열은 예약되어 있으며 필드 이름에 사용될 수 없습니다.


```
  .  ,  # ? :
  id
  score
  highlight
  result_metadata
```
{: pre}

문자 `_`, `+` 및 `-`는 `field_name`에 접두부로 사용할 수 없습니다.

숫자 `0 - 9`는 필드 이름의 접미부(예: `extracted-content2`)가 될 수 없습니다. 이 필드 이름은 인덱싱되지만 조회할 수 없습니다.
