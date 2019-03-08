---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-08"

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

# Watson Knowledge Studio와 통합
{: #integrating-with-wks}

{{site.data.keyword.knowledgestudiofull}}의 사용자 정의 모델을 {{site.data.keyword.discoveryshort}} 서비스와 통합하여 사용자 정의 엔티티와 관계 인리치먼트를 제공할 수 있습니다.
{: shortdesc}

산업 또는 과학 전문 분야와 같은 특정 집중 분야에만 사용되는 정보를 사용하여 {{site.data.keyword.discoveryshort}} 서비스의 문서 개선 기능을 적용할 수 있는 유연성을 제공합니다. 인리치먼트 모델의 공용 데이터와 고유한 독점적 데이터를 모두 사용할 수 있습니다.

서비스 API 또는 {{site.data.keyword.discoveryshort}} 도구를 사용하여 {{site.data.keyword.knowledgestudioshort}} 모델을 {{site.data.keyword.discoveryshort}} 서비스와 통합할 수 있습니다.

## 시작하기 전에

{{site.data.keyword.knowledgestudioshort}}의 사용자 정의 모델을 {{site.data.keyword.discoveryshort}} 서비스와 통합하기 전에 {{site.data.keyword.knowledgestudioshort}}를 사용하여 모델을 작성하고 배치해야 합니다. 모델 작성 및 배치에 대한 정보는 [{{site.data.keyword.knowledgestudioshort}} 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.bluemix.net/docs/services/knowledge-studio/tutorials-create-project.html#wks_tutintro){: new_window}를 참조하십시오. 사용자 정의 모델을 {{site.data.keyword.discoveryshort}} 서비스와 통합하려면 배치된 모델의 고유 ID가 필요합니다.

## 사용자 정의 모델을 API와 통합

1.  [환경 나열 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_environments){: new_window}에 설명된 대로 {{site.data.keyword.discoveryshort}}의 ID를 가져오십시오. 환경 ID를 확인하십시오.
1.  [구성 나열 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_configurations){: new_window}에 설명된 대로 현재 {{site.data.keyword.discoveryshort}} 구성의 ID를 나열하십시오. {{site.data.keyword.knowledgestudiofull}} 사용자 정의 모델과 통합할 구성의 ID를 확인하십시오.
1.  bash 쉘 또는 이와 동등한 환경(예: Windows용 Cygwin)에서 다음 명령을 실행하여 현재 {{site.data.keyword.discoveryshort}} 구성의 사본을 다운로드하십시오. `{environment_id}` 및 `{configuration_id}`를 이전의 두 단계에서 기록한 ID로 대체하십시오.

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-11-07" > my_config.json
    ```
    {: pre}

    이 명령은 콜렉션 파일의 컨텐츠를 나열하고 `my_config.json`으로 이름 지정된 JSON 파일에 이 컨텐츠를 저장합니다.
1.  텍스트 편집기에서 `my_config.json` 파일을 열어 다음 변경사항을 수행하십시오.
    1.  `"name"` 필드의 값을 새 구성의 목적을 나타내는 값으로 변경하십시오. 선택적으로 `"description"` 필드의 값도 변경할 수 있습니다.

        ```json
        ...
        "name": "wks-config",
        "description": "This is a configuration to use with a WKS model",
        ...
        ```
        {: codeblock}

    1.  {{site.data.keyword.knowledgestudioshort}} 모델에 대한 정보를 사용하여 인리치먼트 필드를 업데이트하십시오. 원래 인리치먼트 필드에서 다음을 읽는다고 가정하십시오.

        ```json
        "enrichments": [
        {
            "source_field": "text",
            "destination_field": "enriched_text",
            "enrichment": "natural_language_understanding",
            "options": {
                "features": {
                    "entities": {
                        "sentiment": true,
                        "emotion": false,
                        "limit": 50
                    },
                    "sentiment": {
                        "document": true
                    },
                    "categories": {},
                    "concepts": {
                        "limit": 8
                    },
                    "relations": {}
                }
            }
        }]
        ```
        {: codeblock}

    1.  `{watson_knowledge_studio_model_ID}`에 대해 "시작하기 전에"에서 설명된 대로 {{site.data.keyword.knowledgestudioshort}} 모델의 고유 ID를 대체하여 다음과 같이 파일을 업데이트하십시오.

        ```json
        "enrichments": [
        {
            "source_field": "text",
            "destination_field": "enriched_text",
            "enrichment": "natural_language_understanding",
            "options": {
                "features": {
                    "entities": {
                        "sentiment": true,
                        "emotion": false,
                        "limit": 50,
                        "model": "{watson_knowledge_studio_model_ID}"
                    },
                    "sentiment": {
                        "document": true
                    },
                    "categories": {},
                    "concepts": {
                        "limit": 8
                    },
                    "relations": {
                      "model": "{watson_knowledge_studio_model_ID}"
                    }
                }
            }
        }]
        ```
        {: codeblock}

1.  `my_config.json` 파일을 저장하십시오.
1.  [JSLint ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://jslint.com){: new_window}와 같은 JSON 유효성 검증기를 사용하여 유효성을 검증하고 다음 단계를 수행하기 전에 편집된 JSON을 편집하십시오(필요한 경우).
1.  다음과 같이 구성을 업데이트하십시오. 이 프로시저를 시작할 때 수집한 `{environment_id}` 및 `{configuration_id}` ID가 다시 필요할 수 있습니다.

    ```bash
    curl -X PUT -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-11-07"
    ```
    {: pre}

    **참고:** 새 구성을 작성하거나 기본 구성을 수집하는 경우 기존 구성을 업데이트하는 대신 새 사용자 정의 구성을 작성해야 합니다. 새 구성을 작성하기 전에 `"configuration_id":` 필드가 `my_config.json` 파일에서 제거되었는지 확인한 후 다음 명령을 실행하십시오.

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07"
    ```
    {: pre}

    두 명령은 업데이트된 구성 파일의 컨텐츠를 리턴합니다.

## 사용자 정의 모델을 Discovery 도구와 통합

[엔티티 추출](/docs/services/discovery/building.html#entity-extraction) 또는 [관계 추출](/docs/services/discovery/building.html#relation-extraction) 인리치먼트에 대한 {{site.data.keyword.knowledgestudioshort}} 사용자 정의 모델을 {{site.data.keyword.discoveryshort}} 도구와 통합할 수 있습니다.

1. {{site.data.keyword.knowledgestudioshort}} 모델의 `Model ID`를 가져오십시오.
1. {{site.data.keyword.discoveryshort}} 도구에서 왼쪽 상단에 있는 **데이터 관리** 아이콘을 클릭하여 **데이터 관리** 화면을 연 다음 콜렉션을 작성하거나 여십시오. **참고:** 기존 콜렉션을 선택한 경우 비어 있어야 합니다. 그렇지 않은 경우 새 구성 파일을 작성한 후 해당 문서를 다시 수집해야 합니다.
1. 콜렉션의 **데이터 관리** 화면에 있는 **구성** 섹션에서 **전환**을 클릭한 다음 **새 구성 작성**을 선택하십시오. 구성 이름을 지정하십시오. 
1. **인리치먼트 추가**를 클릭하고 **엔티티 추출** 또는 **관계 추출** 인리치먼트를 선택하십시오.
1. 선택된 인리치먼트의 `Custom Model ID` 상자에 `Model ID`를 입력하십시오. 사용자 정의 {{site.data.keyword.knowledgestudiofull}} 모델은 해당 인리치먼트의 기본값을 대체합니다. 
1. **적용**을 클릭한 후 **완료**를 클릭하십시오.

문서가 데이터 콜렉션에 업로드되면 해당 콜렉션에 대해 선택한 구성 파일을 사용하여 문서가 변환되고 강화됩니다. 문서가 업로드된 후 기존 콜렉션을 새 구성 파일로 전환한 경우 업로드된 문서는 원래의 구성 파일에 의해 변환된 상태로 유지됩니다. 구성 파일을 전환한 후 업로드된 모든 문서는 새 구성 파일을 사용합니다. **전체** 콜렉션에서 새 구성 파일을 사용하려면 새 콜렉션을 작성하고 새 구성 파일을 선택한 다음 모든 문서를 다시 업로드해야 합니다.

**참고:** 인리치먼트에 하나의 {{site.data.keyword.knowledgestudiofull}} 모델만 지정할 수 있습니다.

## 다음 단계

새 구성으로 {{site.data.keyword.discoveryshort}} 서비스를 사용하여 개인 데이터를 수집하십시오. 업데이트된 구성으로 수집한 문서는 사용자 정의 모델의 데이터를 사용하여 자동으로 강화됩니다.
