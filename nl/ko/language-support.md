---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-18"

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

# 언어 지원
{: #language-support}

{{site.data.keyword.discoveryfull}} 서비스는 **기본** 및 **전체**의 두 가지 언어 지원 레벨을 제공합니다.
{: shortdesc}

|언어                         |지원 레벨         |
|---------------------------------|------------------------|
|영어(en)                    |전체         |
|아랍어(ar)                     |기본         |
|중국어(zh-CN)     |기본         |
|네덜란드어(nl)                     |기본         |
|프랑스어(fr)                     |전체         |
|독일어(de)                     |전체         |
|이탈리아어(it)                    |전체        |
|일본어(ja)                  |전체         |
|한국어(ko)                    |전체         |
|포르투갈어, 브라질어(pt-br)   |전체         |
|스페인어(es)                    |전체         |

## 기본 지원
{: #basic-support}

- {{site.data.keyword.discoveryshort}} 지원에는 다음 기능이 포함됩니다.
    - 문서 변환
    - 오케스트레이션
    - {{site.data.keyword.discoveryshort}} 도구 기능
    - 프론트 엔드 API(프론트 엔드 조회 API 제외)
    - 언어가 최적화된 인덱스
    - 관련성 훈련
    - 조회 확장
    - 제외어
    - 9개 언어로 지원되는 문서: 영어, 프랑스어, 독일어, 일본어, 한국어, 브라질 포르투갈어, 스페인어, 중국어 간체 및 중국어 번체. 언어를 선택하려면 {{site.data.keyword.Bluemix_notm}} 문서의 맨 아래로 스크롤하십시오.
- 인리치먼트
    - {{site.data.keyword.knowledgestudiofull}} 사용자 정의 모델과 통합
    - 언어 발견

## 전체 지원
{: #full-support}

전체 지원에는 기본 지원 외에 다음 기능이 포함됩니다.

- 단락 검색
- 변환된 {{site.data.keyword.knowledgestudiofull}} 인터페이스
- 모든 {{site.data.keyword.nlushort}}(NLU) 인리치먼트 및 메타데이터 추출. NLU 인리치먼트는 다음과 같습니다.
    - 엔티티 추출
    - 키워드 추출
    - 카테고리 분류
    - 개념 태그 지정
    - 시맨틱 역할 추출
    - 감성 분석
    - 감정 분석(영어 전용)

## 영어만 지원
{: #feature-support}

다음 기능은 현재 영어에서만 지원됩니다.

- 요소 분류 인리치먼트
- {{site.data.keyword.discoveryfull}} Knowledge Graph(베타)
- 문서 중복 제거(베타)

## 일본어만 지원
{: #japanese-support}

다음 기능은 현재 일본어에서만 지원됩니다.

- 사용자 정의 토큰화 사전
