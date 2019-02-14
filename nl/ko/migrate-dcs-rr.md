---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-03"

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


# Watson Document Conversion 및 Retrieve and Rank에서 마이그레이션

{{site.data.keyword.documentconversionfull}} 및 {{site.data.keyword.retrieveandrankfull}}는 더 이상 사용되지 않으므로 {{site.data.keyword.discoveryfull}}로 대체되었습니다. 일반적으로, 이 두 서비스는 함께 사용되어 수집하고 순위를 지정한 후 애플리케이션에 결과를 전달합니다. 이 문서는 {{site.data.keyword.documentconversionshort}} 및 {{site.data.keyword.retrieveandrankshort}}에서 {{site.data.keyword.discoveryshort}}로의 마이그레이션 프로세스를 통해 사용자를 안내하기 위해 제공됩니다.

{{site.data.keyword.discoveryfull}}는 좀 더 강력한 조회 인터페이스, 간소화된 데이터 수집, 향상된 훈련 관리 및 증가된 스케일을 제공합니다. {{site.data.keyword.discoveryshort}}에서는 지원 에이전트 보조, 조직 지식 관리 검색 및 연구 지원을 포함한 {{site.data.keyword.retrieveandrankshort}}로의 많은 동일한 코어 유스 케이스를 다룹니다. 이는 {{site.data.keyword.retrieveandrankshort}} 사용자에게 직면한 다수의 도전 과제로 빌드되었으며 많은 문제를 다룹니다. 또한 {{site.data.keyword.discoveryshort}}는 추가 관련성 결과를 찾기 위한 단락 검색 및 개선된 검색 알고리즘을 포함하여 {{site.data.keyword.retrieveandrankshort}}에 사용할 수 없는 정보 검색에 대한 새 기능도 제공합니다.

**기능 비교**

|기능 | {{site.data.keyword.retrieveandrankshort}} | {{site.data.keyword.discoveryshort}} |
|:-------------|:--------------------:|:-------------:|
|자연어 검색 |예 |예 |
|기계 학습 관련성 훈련 |예 |예 |
|훈련용 UI 도구 |예 |예 |
|JSON 응답 단위 입력 |예 |예 |
|문서 분할 |예 |예 |
|단락 검색 |   |예 |
|문서 CRUD |예 |예 |
|배치 JSON 업로드 |예 |   |
|Automatic 문서 NLP 인리치먼트 |   |예 |
|인리치먼트를 위한 사용자 정의 NLP 모델 통합 |   |예 |
|서비스에 저장된 훈련 데이터 |   |예 |
|자동화된 모델 라이프사이클 관리 |   |예 |
|훈련 없이 관련성을 향상시킬 수 있는 시맨틱 유사성 |   |예 |
|테스트 세트를 기반으로 도구의 정확성 측정 |예 |   |
|사용자 정의 기능 벡터 지원 |예 |   |
|사용자 정의 분석기 구성 |예 |사전 구성됨 |
|사용자 정의 제외어 |예 |사전 구성됨 |
|사용자 정의 언어 사전 |예 |사전 구성됨 |
|사용자 정의 동의어 |예 |예 |
**참고:** 이 표는 새 {{site.data.keyword.discoveryshort}} 기능이 추가될 때 업데이트됩니다.

마이그레이션의 조치를 시작하기 전에 먼저 {{site.data.keyword.retrieveandrankshort}} 서비스에 저장된 데이터를 [평가](#evaluate)하고 현재 솔루션을 구성하는 다른 컴포넌트를 이동시키는 방법을 이해해야 합니다.

대부분의 고객은 {{site.data.keyword.retrieveandrankshort}}와 함께 {{site.data.keyword.documentconversionshort}}을 사용합니다. 컨텐츠가 검색 가능한 인덱스로 저장될 수 있도록 {{site.data.keyword.documentconversionshort}}을 사용하지 않고 컨텐츠를 변환하는 경우 [독립형 {{site.data.keyword.documentconversionshort}}을 마이그레이션하는 옵션](#dcs) 검토로 계속 진행하십시오.

{{site.data.keyword.retrieveandrankshort}} 튜토리얼을 원래 사용했으며 사용하며 해당 튜토리얼에 따라 서비스의 고유한 인스턴스를 선택한 경우 동일한 데이터를 {{site.data.keyword.discoveryshort}}에 수집하는 튜토리얼의 확장은 [여기](/docs/services/discovery/migrate-rnr-tut.html)에서 찾을 수 있습니다.

**참고:** 변환 및 인리치먼트 기능은 {{site.data.keyword.discoveryshort}}에 포함되어 있습니다. {{site.data.keyword.documentconversionshort}} 및/또는 {{site.data.keyword.nlushort}}을 사용하여 소스 HTML, PDF 또는 Microsoft Word 문서를 변환하고 강화한 경우 이 서비스는 {{site.data.keyword.discoveryshort}} 서비스 내의 기능으로 대체됩니다.

## Watson Discovery 서비스에 대한 마이그레이션 경로 평가
{: #evaluate}

{{site.data.keyword.retrieveandrankshort}}에서 마이그레이션하는 실질적인 두 옵션 즉, 소스 컨텐츠에서 마이그레이션 및 인덱싱된 컨텐츠에서 마이그레이션이 있습니다. 사용할 옵션을 결정하기 전에 두 옵션을 평가하십시오.

### 소스 컨텐츠에서 마이그레이션
{: #source}

소스 컨텐츠에서 마이그레이션하려면 다음을 수행하십시오.

-  컨텐츠를 수집한 원래의 소스 파일에 대한 액세스 권한이 있어야 합니다.
-  각 문서에 프로그래밍 방식으로 ID를 추출해야 합니다(결과가 인덱싱되기 전에 결과에 ID가 이미 있음).

모든 마이그레이션 기준을 충족시킬 수 있는 경우 {{site.data.keyword.discoveryshort}} 서비스로 이동하는 데 이 메소드를 사용하는 것이 좋습니다.

소스 컨텐츠를 마이그레이션하려면 [마이그레이션 튜토리얼](/docs/services/discovery/migrate-rnr-tut.html)에 설명된 프로시저를 수정하여 소스 데이터의 세부사항을 충족해야 합니다.

#### 마이그레이션 응답 단위

{{site.data.keyword.documentconversionshort}}을 사용하여 응답 단위를 작성한 경우 해당 컨텐츠를 마이그레이션하는 다음 옵션 중 하나를 선택하십시오.

-  순위 지정자를 훈련시켰으며 순위 지정을 마이그레이션해야 하는 경우 {{site.data.keyword.documentconversionshort}}에서 리턴된 컨텐츠를 가져오고 이를 {{site.data.keyword.discoveryshort}}로 수집해야 합니다.
-  마이그레이션하기 위한 훈련 데이터가 없는 경우 [문서 세분화 기능](/docs/services/discovery/building.html#doc-segmentation)을 사용하여 원래의 소스 문서를 {{site.data.keyword.discoveryshort}}로 수집하십시오.

### 인덱싱된 컨텐츠에서 마이그레이션
{: #indexed}

원래의 소스 문서에 대한 액세스 권한이 없는 경우 {{site.data.keyword.retrieveandrankshort}}의 인덱싱된 컨텐츠에서 마이그레이션해야 합니다. 또는 다음과 같습니다.

- 자동 문서 ID 생성을 사용했으며 순위 지정자를 훈련시켰습니다.
- {{site.data.keyword.documentconversionshort}}의 응답 단위를 작성한 후 순위를 지정했으나 {{site.data.keyword.documentconversionshort}} 서비스로 생성된 응답 단위를 보유하지 않았습니다.

**참고:** 모든 필수 컨텐츠가 {{site.data.keyword.retrieveandrankshort}}의 저장된 필드에 있는 경우에만 이 메소드를 사용할 수 있습니다. 컨텐츠가 인덱싱만 되고 저장되지 않은 경우 서비스의 컨텐츠를 조회할 수 없으며 데이터가 변환되고 소스에서 다시 분할되어야 합니다.

문서가 [/v1/solr_clusters/{solr_cluster_id}/solr/\{collection_name\}/select ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/retrieve-and-rank/api/v1/#index_doc){: new_window} 메소드(비어 있는 조회 `q=*:*`)를 사용하여 서비스에서 추출됩니다. 리턴된 문서의 수가 실제 최대 리턴 수(대부분의 콜렉션당 `200`)보다 클 수 있습니다. 이 경우, 모든 문서를 수집하는 데 적절한 [페이징 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://lucene.apache.org/solr/guide/6_6/pagination-of-results.html){: new_window}을 사용하여 다중 호출을 수행해야 합니다.

지정된 **ID**가 사용된 문서는 [/v1/environments/\{environment_id\}/collections/\{collection_id\}/documents/\{document_id\} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#update-doc){: new_window} 메소드를 사용하여 {{site.data.keyword.discoveryshort}} 서비스에 업로드됩니다. 각 문서 업로드는 개별 API 호출입니다.

## 훈련 데이터 마이그레이션

결과를 마이그레이션한 후 다음 단계는 컨텐츠에 대해 작성한 훈련 데이터를 마이그레이션하는 것입니다. 훈련 데이터를 마이그레이션하는 두 옵션 즉, 소스(`csv`)에서 마이그레이션 및 서비스에서 마이그레이션이 있습니다. `csv` 파일에서 훈련 데이터를 업로드했으며 해당 파일에 대한 액세스 권한을 계속 보유하고 있는 경우 소스에서 마이그레이션해야 합니다. {{site.data.keyword.retrieveandrankshort}} 도구를 사용했거나 원래 `csv` 파일에 대한 액세스 권한이 없으면 서비스에서 마이그레이션해야 합니다.

### 소스 컨텐츠에서 훈련 마이그레이션
{: #csv}

순위 지정 소스 컨텐츠에서 마이그레이션하려면 다음을 수행하십시오.

- 훈련 정보를 원래 업로드한 원래의 소스 `csv` 파일에 대한 액세스 권한이 필요합니다.
- 훈련된 문서가 인덱싱될 때 훈련된 문서의 ID가 훈련된 문서가 {{site.data.keyword.retrieveandrankshort}}에 인덱싱되었을 때 훈련된 문서의 ID와 일치하는지 확인하십시오.

모든 마이그레이션 기준을 충족시킬 수 있는 경우 {{site.data.keyword.discoveryshort}} 서비스로 훈련을 이동하는 데 이 메소드를 사용하는 것이 좋습니다.

훈련 데이터를 마이그레이션하려면 [마이그레이션 튜토리얼](/docs/services/discovery/migrate-rnr-tut.html)에 설명된 프로시저를 수정하여 소스 데이터의 세부사항을 충족해야 합니다.

### 서비스에서 훈련 데이터 마이그레이션
{: #extract-train}

{{site.data.keyword.retrieveandrankshort}} 서비스에서 훈련 데이터를 마이그레이션하려면 {{site.data.keyword.retrieveandrankshort}} API를 사용하여 훈련 데이터를 추출하고 {{site.data.keyword.discoveryshort}}에서 사용 가능한 형식으로 {{site.data.keyword.retrieveandrankshort}} 훈련 JSON을 변환한 후 마지막으로 API를 사용하여 훈련 데이터를 {{site.data.keyword.discoveryshort}}로 수집해야 합니다.

{{site.data.keyword.retrieveandrankshort}}에서 훈련 데이터를 추출하려면 {{site.data.keyword.retrieveandrankshort}} 도구 내에서 `Export` 기능을 사용해야 합니다. 전체 내보내기를 다운로드한 후 저장된 `.zip` 파일을 추출하십시오. 아카이브 내에 두 개의 파일이 있습니다. 훈련 데이터는 하나의 이름 지정된 `export-questions.json`에 저장됩니다. 이 파일에 JSON 훈련 오브젝트의 배열이 포함됩니다.

배열의 각 훈련 결과는 다음 양식으로 표시됩니다.

**샘플 {{site.data.keyword.retrieveandrankshort}} 훈련 데이터**
```json
{
    "text":"Who was the first royal to attend Wimbledon?",
    "cluster":{
        "id":"f62c11d3-30fa-11e7-8a0c-333f7f431ce8",
        "answers":{
            "f62c11d3-30fa-11e7-8a0c-33":[
                {
                    "id":"dac41335-0e96-40c9-983f-cc3f1c395782",
                    "ranking":1,
                    "source":{
                        "id":"e26a3d20-30fa-11e7-aa5e-d1632b06e0b1",
                        "file":"wimbledon-wikipedia.html",
                        "sequence":17,
                        "strategy":"retrieve"
                    }
                },
                {
                    "id":"661b4c9f-ecdb-4dad-aafc-6ae561a148c0",
                    "ranking":2,
                    "source":{
                        "id":"da1bc620-30fa-11e7-8f90-3305f35a93c9",
                        "file":"generated-otherFactsFigures.docx",
                        "sequence":67,
                        "strategy":"retrieve"
                    }
                },
                {
                    "id":"0053fdb8-c77e-4fcf-b0e0-6a4cd377266a",
                    "ranking":3,
                    "source":{
                        "id":"d9c0add0-30fa-11e7-aa5e-d1632b06e0b1",
                        "file":"generated-allEngland.docx",
                        "sequence":20,
                        "strategy":"retrieve"
                    }
                },
                {
                    "id":"506d3d50-19ed-49c8-b32f-65f848e60e86",
                    "ranking":4,
                    "source":{
                        "id":"da1bc620-30fa-11e7-8f90-3305f35a93c9",
                        "file":"generated-otherFactsFigures.docx",
                        "sequence":63,
                        "strategy":"retrieve"
                    }
                }
            ]
        },
        "flags":{

        }
    }
},
```
{: codeblock}

{{site.data.keyword.discoveryshort}}에는 {{site.data.keyword.retrieveandrankshort}}에서 내보낸 모든 정보가 필요하지 않습니다. 다음 스니펫은 {{site.data.keyword.discoveryshort}} 훈련 항목의 필수 구조를 표시합니다.

```json
{
  "natural_language_query": "{natural_language_query}",
  "examples": [
    {
      "document_id": "{document_id_1}",
      "relevance": 0
    },
    {
      "document_id": "{document_id_2}",
      "relevance": 10
    }
  ]
}
```
{: codeblock}

이 때 {{site.data.keyword.retrieveandrankshort}} 훈련 데이터를 {{site.data.keyword.discoveryshort}} 훈련 정보로 변환해야 합니다. 변환 시 다음 사항을 고려하십시오.

- **관련성 없음**은 {{site.data.keyword.discoveryshort}}에서 `0`의 `relevance` 스코어로 지정되지만 {{site.data.keyword.retrieveandrankshort}}에서 `1`의 `ranking`으로 지정됩니다. 모든 `"ranking": 1` 항목은 {{site.data.keyword.discoveryshort}}에서 `"relevance": 0`으로 변환되어야 합니다.
- {{site.data.keyword.discoveryshort}} 도구는 `0` 및 `10`의 2진 스케일을 사용합니다. 더 많은 결과의 순위를 지정하고 {{site.data.keyword.discoveryshort}} 도구를 사용하려면 `"ranking": 1` 및 `"ranking": 2` 항목을 `"relevance": 0`으로 변환하고 모든 `"ranking": 3` 및 `"ranking": 4` 항목을 `"relevance": 10`으로 변환해야 합니다. 추가 결과의 순위를 지정하지 않거나 {{site.data.keyword.discoveryshort}} 도구를 사용하지 않는 경우에는 이를 수행할 필요는 없습니다.
- {{site.data.keyword.discoveryshort}}에 답변 없는 질문이 필요하지 않으며 관련성 훈련의 유효성 검사가 수동으로 수행됩니다.

![순위 지정 마이그레이션 플로우](images/migrate-ranking.png)

예를 들어, 위에 나열된 **샘플 {{site.data.keyword.retrieveandrankshort}} 훈련 데이터**는 다음과 같이 {{site.data.keyword.discoveryshort}} 도구에서 사용하도록 변환됩니다.

```json
{
  "natural_language_query": "Who was the first royal to attend Wimbledon?",
  "examples": [
    {
      "document_id": "e26a3d20-30fa-11e7-aa5e-d1632b06e0b1",
      "relevance": 0
    },
    {
      "document_id": "da1bc620-30fa-11e7-8f90-3305f35a93c9",
      "relevance": 0
    },
    {
      "document_id": "d9c0add0-30fa-11e7-aa5e-d1632b06e0b1",
      "relevance": 10
    },
    {
      "document_id": "da1bc620-30fa-11e7-8f90-3305f35a93c9",
      "relevance": 10
    }
  ]
}
```
{: codeblock}

## 언어 지원
{: #language}

[{{site.data.keyword.discoveryshort}}를 위한 언어 지원](/docs/services/discovery/language-support.html)을 참조하십시오. {{site.data.keyword.retrieveandrankshort}} 기능은 주로 **기본** {{site.data.keyword.discoveryshort}} 언어 지원으로 지원됩니다.

## 조회 마이그레이션
{: #queries}

{{site.data.keyword.discoveryfull}} 조회 언어는 {{site.data.keyword.retrieveandrankshort}}에서 사용한 Solr 조회 언어와 다릅니다. 기존 조회는 {{site.data.keyword.discoveryfull}} 조회 메소드 중 하나로 경로 재지정되고 {{site.data.keyword.discoveryfull}} 조회 언어를 사용하도록 변환되어야 합니다. 다음 표는 대부분의 조회에 사용되는 일반적인 일부 연산자에 대해 설명합니다.

**Solr 조회에서 {{site.data.keyword.discoveryshort}}로 마이그레이션 - 일반적인 연산자**

|Solr 연산자 |Discovery 연산자 |설명 |
|:-------------:|--------------------|-------------|
| `.` | `.` |JSON 구분 기호 |
| `:` | `:` |포함 |
|  | `::` |정확히 일치 |
|`-{fieldname}:` | `:!` |포함하지 않음 |
|  | `::!` |정확히 일치하지 않음 |
| ``\` | ``\` |이스케이프 문자 |
| `""` | `""` |구문 조회 |
| `()` | `()`, `[]` |중첩된 그룹화 |
|`OR` |[<code>&#124;</code>] |or |
|`AND` | [,] |and |
|`[* TO 100]` | `<=`, `>=`, `>`, `<` |숫자 비교 |
|`^x` |`^x` |스코어 승수 |
| `*` | `*` |와일드카드 |
|`~`(0 - 1) |[~n] |문자열 변형 |

{{site.data.keyword.discoveryfull}} 조회 언어에 대한 자세한 정보는 [조회 개념](/docs/services/discovery/using.html) 및 [조회 참조](/docs/services/discovery/query-reference.html) 문서를 참조하십시오.


## 독립형 Watson Document Conversion 서비스 마이그레이션
{: #dcs}

{{site.data.keyword.documentconversionshort}}을 사용하여 컨텐츠를 {{site.data.keyword.retrieveandrankshort}}에 수집하는 경우 해당 기능이 단일 서비스인 {{site.data.keyword.discoveryshort}}로 발전했습니다. {{site.data.keyword.discoveryshort}}를 통해 Microsoft Word, PDF, HTML 및 JSON 문서를 훈련 가능하고 검색 가능한 인덱스로 쉽게 변환, 강화 및 수집할 수 있습니다. 유스 케이스가 인덱스에 변환된 컨텐츠 저장을 포함하지 않는 경우 이 절은 사용자와 관련이 있습니다. 인덱스에 문서를 수집하는 경우 [{{site.data.keyword.discoveryshort}} 서비스에 수집](/docs/services/discovery/building.html)을 참조하십시오.

IBM은 더 이상 Microsoft Word, PDF 및 HTML 문서의 독립형 변환을 위해 설계된 서비스를 제공하지 않습니다. 현재 {{site.data.keyword.documentconversionshort}} 서비스를 사용 중이고 온라인 인덱싱된 서비스(예: {{site.data.keyword.discoveryshort}})에 출력을 수집하지 않는 경우 [Apache Tika ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://tika.apache.org/){: new_window}와 같은 오픈 소스 대체로의 마이그레이션을 고려하십시오.
