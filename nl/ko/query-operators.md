---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-09"

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

# 조회 연산자
{: #query-operators}

연산자는 조회의 서로 다른 부분 사이에 있는 구분 기호입니다. 사용 가능한 연산자의 전체 목록은 [조회 참조](/docs/services/discovery/query-reference.html#operators)를 참조하십시오.

## . \[JSON 구분 기호\]
{: #delimiter}

이 구분 기호는 JSON 스키마에서 계층 구조의 레벨을 구분합니다. 

예:
```bash
enriched_text.concepts.text
```
{: codeblock}

## : \[포함\]
{: #includes}

이 연산자는 조회 용어에 대한 일치 항목을 지정합니다. 

예:
```bash
enriched_text.concepts.text:cloud computing
```
{: codeblock}

## :: \[정확히 일치\]
{: #match}

이 연산자는 조회 용어에 대한 정확한 일치 항목을 지정합니다. 

예:
```bash
enriched_text.concepts.text::cloud computing
```
{: codeblock}

## :! \[포함하지 않음\]
{: #notinclude}

이 연산자는 결과가 조회 용어와 일치하는 항목을 포함하지 않도록 지정합니다.

예:
```bash
enriched_text.concepts.text:!cloud computing
```
{: codeblock}

## ::! \[정확히 일치하지 않음\]
{: #notamatch}

이 연산자는 결과가 조회 용어와 정확하게 일치하지 않도록 지정합니다. 

예:
```bash
enriched_text.concepts.text::!cloud computing
```
{: codeblock}

## \\ \[이스케이프 문자\]
{: #escape}

제어 문자가 포함된 문자열 리터럴을 사용하여 용어를 조회하는 기능을 필요로 하는 조회의 이스케이프 문자입니다. 

예:
```bash
enriched_text.concepts.text:\!cloud computing
```
{: codeblock}

## "" \[구문 조회\]
{: #phrase}

구문 조회의 모든 컨텐츠는 이스케이프된 상태로 처리됩니다. 그러므로 구문 분석 내의 특수 문자가 구문 분석됩니다. 단, 구문 조회 내의 큰따옴표(`"`)는 제외되며 이스케이프되어야 합니다(`\"`). 전체 텍스트가 포함된 구문 조회, 순위 기반의 조회를 사용하십시오(부울 필터 연산자는 포함하지 않음). 구문 조회에 와일드카드(`*`)를 사용하지 마십시오. **참고**: 작은따옴표(`'`)는 지원되지 않습니다. 

예:
```bash
enriched_text.concepts.text:"IBM watson"
```
{: codeblock}

## (), \[\] \[중첩된 그룹화\]
{: #nestedquery}

좀 더 특정한 정보를 지정하기 위해 논리 그룹화를 구성할 수 있습니다. 

예:
```bash
enriched_text.entities:(text:IBM,type:Company)
```
{: codeblock}

## \| \[or\]
{: #or}

부울 연산자인 "or"입니다.

예:
```bash
enriched_text.entities.text:Google|IBM
```
{: codeblock}

## , \[and\]
{: #and}

부울 연산자인 "and"입니다.

예:
```bash
enriched_text.entities.text:Google,IBM
```
{: codeblock}

## <=, >=, >, < \[숫자 비교\]
{: #comparisons}

이하, 이상, 초과 및 미만의 숫자 비교를 작성합니다. 

예:
```bash
enriched_text.sentiment.document.score>0.679
```
{: codeblock}

## ^x \[스코어 승수\]
{: #multiplier}

검색 용어의 스코어 값을 증가시킵니다. 

예:
```bash
enriched_text.concepts.text:IBM^3
```
{: codeblock}

## * \[와일드카드\]
{: #Wildcard}

검색 표현식의 알 수 없는 문자를 일치시킵니다. 

예:
```bash
enriched_text.concepts.text:IBM*
```
{: codeblock}

## ~n \[문자열 변형\]
{: #variation}

한 문자열을 다른 문자열과 동일하게 하기 위해 필요한 한 문자 변경의 수입니다. 예를 들어, `car~1`은 `car`,`cap`,`cat`,`can` 등과 일치합니다. 

예:
```bash
enriched_text.concepts.text:Watson~3
```
{: codeblock}
