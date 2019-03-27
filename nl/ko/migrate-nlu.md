---

copyright:
  years: 2015, 2018
lastupdated: "2018-02-28"

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

# Natural Language Understanding으로 인리치먼트 마이그레이션
{: #migrate-nlu}

**2017년 7월 18일**에 {{site.data.keyword.discoveryfull}}는 {{site.data.keyword.nlushort}}(NLU)이라는 새 인리치먼트 기술을 도입하였습니다. {{site.data.keyword.alchemylanguageshort}} 인리치먼트는 **2018년 3월 1일**부터 더 이상 사용되지 않습니다. 
{: shortdesc}

{{site.data.keyword.alchemylanguageshort}} 인리치먼트를 사용하는 기존 콜렉션은 마이그레이션해야 합니다. {{site.data.keyword.alchemylanguageshort}} 인리치먼트를 활용하는 콜렉션 및 구성 파일의 마이그레이션에 대한 정보는 [인리치먼트 비교](/docs/services/discovery?topic=discovery-migrate-nlu#enrichment-comparison)를 참조하십시오.

**참고:** {{site.data.keyword.knowledgestudioshort}}와의 통합에 대한 자세한 정보는 [{{site.data.keyword.knowledgestudiofull}}와 통합](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-with-wks)을 참조하십시오.

## 인리치먼트 비교
{: #enrichment-comparison}

다음은 {{site.data.keyword.alchemylanguageshort}} 및 {{site.data.keyword.nlushort}}에서 사용 가능한 일곱 개의 인리치먼트와 해당 JSON 오브젝트 이름입니다.

|{{site.data.keyword.alchemylanguageshort}} 인리치먼트의 이름         |{{site.data.keyword.alchemylanguageshort}} JSON 오브젝트            |NLU 인리치먼트의 이름                     |NLU JSON 오브젝트        |
|---------------------------|----------------------------------------|----------------------------------------|--------------------------------|
|엔티티 추출                     |entities                        |엔티티 추출                           |entities            |
|키워드 추출                    |keywords                        |키워드 추출                          |keywords            |
|택소노미 분류               |taxonomy                        |카테고리 분류*                    |categories*         |
|개념 태그 지정                       |concepts                        |개념 태그 지정                             |concepts            |
|감성 분석                    |docSentiment                    |감성 분석                          |sentiment*          |
|감정 분석                      |docEmotions                     |감정 분석                            |emotion*            |
|관계 추출                   |relations                       |시맨틱 역할 추출*                   |semantic_roles*     |
 \* 이름 변경

{{site.data.keyword.nlushort}} 인리치먼트에 대한 자세한 정보는 [인리치먼트 추가](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)를 참조하십시오.

## 주요 변경사항의 개요
{: #overview-nlu}

- {{site.data.keyword.nlushort}} 인리치먼트의 JSON 스키마는 {{site.data.keyword.alchemylanguageshort}} 인리치먼트에서 사용된 것과 다릅니다. 각 인리치먼트에 대한 변경사항의 전체 목록은 [인리치먼트 스키마 차이점](/docs/services/discovery?topic=discovery-migrate-nlu#enrichment-schema-differences)을 참조하십시오.
- _택소노미 분류_({{site.data.keyword.alchemylanguageshort}}) 인리치먼트는 이제 _카테고리 분류_로 이름이 변경되었습니다. 해당 JSON 오브젝트 이름은 `taxonomy`에서 `categories`로 변경되었습니다.
- _관계 추출_({{site.data.keyword.alchemylanguageshort}}) 인리치먼트는 이제 _시맨틱 역할 추출_로 이름이 변경되었습니다. 해당 JSON 오브젝트 이름은 `relations`에서 `semantic_roles`로 변경되었습니다.
- _감성 분석_의 JSON 오브젝트 이름은 `docSentiment`에서 `sentiment`로 변경되었습니다.
- _감정 분석_의 JSON 오브젝트 이름은 `docEmotions`에서 `emotion`으로 변경되었습니다.

## 구성 파일 변경사항
{: #config-nlu}

**{{site.data.keyword.alchemylanguageshort}}** 기본 구성 파일(도구에서 `Default configuration`으로 이름이 지정됨)에서 **엔티티 추출**, **키워드 추출**, **택소노미 분류**, **개념 태그 지정**, **관계 추출** 및 **감성 분석**의 인리치먼트를 문서의 텍스트 필드에 적용합니다. 또한 파일에는 글꼴 스타일 및 크기에 따른 표준 문서 변환도 포함됩니다.

**{{site.data.keyword.nlushort}}** 기본 구성 파일은 `Default Configuration with NLU`라는 이름으로 지정되고 문서의 텍스트 필드에 **엔티티 추출**, **감성 분석**, **카테고리 분류** 및 **개념 태그 지정**과 같은 인리치먼트를 적용합니다. 또한 파일에는 글꼴 스타일 및 크기에 따른 표준 문서 변환도 포함됩니다. 이 문서 변환은 {{site.data.keyword.alchemylanguageshort}} 기본 구성 파일의 문서 변환과 동일합니다.

## 구성, 콜렉션 및 조회 마이그레이션
{: #migrateconfig-nlu}

사용자 정의 구성을 작성한 경우 {{site.data.keyword.nlushort}} 인리치먼트를 사용하는 새 사용자 정의 구성을 작성해야 합니다. 지시사항은 다음 문서를 참조하십시오.

- [도구](/docs/services/discovery?topic=discovery-configservice#custom-configuration)
- [API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/discovery#add-configuration){: new_window}

기존 콜렉션에 적용된 사용자 정의 {{site.data.keyword.alchemylanguageshort}} 구성 또는 {{site.data.keyword.alchemylanguageshort}} 기본 구성이 있는 기존 콜렉션을 보유한 경우 {{site.data.keyword.nlushort}} 구성 파일(기본 구성 또는 새 사용자 정의 구성)을 적용하고 문서를 업로드하십시오. 지시사항은 다음 문서를 참조하십시오.

- [도구](/docs/services/discovery?topic=discovery-configservice#preparing-the-service-for-your-documents)
- [API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/discovery#create-a-collection){: new_window}

Discovery 조회 언어를 사용하여 작성한 조회의 경우 {{site.data.keyword.alchemylanguageshort}} 및 {{site.data.keyword.nlushort}} 간의 JSON 스키마 변경사항을 확인하고 조회 및 조회 URL을 적절하게 업데이트하십시오. 자세한 사항은 [인리치먼트 스키마 차이점](/docs/services/discovery?topic=discovery-migrate-nlu#enrichment-schema-differences)을 참조하십시오.

## 인리치먼트 스키마 차이점
{: #enrichment-schema-differences}

다음 표는 {{site.data.keyword.nlushort}} 인리치먼트의 JSON 스키마 및 {{site.data.keyword.alchemylanguageshort}} 인리치먼트의 JSON 스키마 간의 차이점을 표시합니다.

| {{site.data.keyword.alchemylanguageshort}}                         | {{site.data.keyword.nlushort}}       |
|-----------------------------------------|--------------------------------------|
|enriched_text.concepts                      |enriched_text.concepts|
|enriched_text.concepts.census              |더 이상 사용되지 않음|
|enriched_text.concepts.ciaFactbook          |더 이상 사용되지 않음|
|enriched_text.concepts.crunchbase                              |더 이상 사용되지 않음|
|enriched_text.concepts.dbpedia                               |enriched_text.concepts.dbpedia_resource|
|enriched_text.concepts.freebase                              |더 이상 사용되지 않음|
|enriched_text.concepts.geonames                                |더 이상 사용되지 않음|
|enriched_text.concepts.knowledgeGraph.typeHierarchy            |더 이상 사용되지 않음|
|enriched_text.concepts.musicBrainz                              |더 이상 사용되지 않음|
|enriched_text.concepts.opencyc                                  |더 이상 사용되지 않음|
|enriched_text.concepts.relevance                                |enriched_text.concepts.relevance|
|enriched_text.concepts.text                                    |enriched_text.concepts.text|
|enriched_text.concepts.website                                  |더 이상 사용되지 않음|
|enriched_text.concepts.yago                                    |더 이상 사용되지 않음|
|enriched_text.docSentiment.mixed                                |더 이상 사용되지 않음|
|enriched_text.docSentiment.score                                |enriched_text.sentiment.document.score|
|enriched_text.docSentiment.type                                |enriched_text.sentiment.document.label|
|enriched_text.entities                                          |enriched_text.entities|
|enriched_text.entities.count                                    |enriched_text.entities.count|
|enriched_text.entities.disambiguated.census                    |더 이상 사용되지 않음|
|enriched_text.entities.disambiguated.ciaFactbook                |더 이상 사용되지 않음|
|enriched_text.entities.disambiguated.crunchbase                |더 이상 사용되지 않음|
|enriched_text.entities.disambiguated.dbpedia                    |enriched_text.entities.disambiguation.dbpedia_resource|
|enriched_text.entities.disambiguated.freebase                  |더 이상 사용되지 않음|
|enriched_text.entities.disambiguated.geonames                  |더 이상 사용되지 않음|
|enriched_text.entities.disambiguated.musicBrainz                |더 이상 사용되지 않음|
|enriched_text.entities.disambiguated.name                      |enriched_text.entities.disambiguation.name|
|enriched_text.entities.disambiguated.opencyc                    |더 이상 사용되지 않음|
|enriched_text.entities.disambiguated.subType                    |enriched_text.entities.disambiguation.subtype|
|enriched_text.entities.disambiguated.umbel                      |더 이상 사용되지 않음|
|enriched_text.entities.disambiguated.website                    |더 이상 사용되지 않음|
|enriched_text.entities.disambiguated.yago                      |더 이상 사용되지 않음|
|enriched_text.entities.knowledgeGraph.typeHierarchy            |더 이상 사용되지 않음|
|enriched_text.entities.quotations                              |더 이상 사용되지 않음|
|enriched_text.entities.quotations.quotation                    |더 이상 사용되지 않음|
|enriched_text.entities.quotations.sentiment.mixed              |더 이상 사용되지 않음|
|enriched_text.entities.quotations.sentiment.score              |더 이상 사용되지 않음|
|enriched_text.entities.quotations.sentiment.type                |더 이상 사용되지 않음|
|enriched_text.entities.relevance                                |enriched_text.entities.relevance|
|enriched_text.entities.sentiment.mixed                          |더 이상 사용되지 않음|
|enriched_text.entities.sentiment.score                          |enriched_text.entities.sentiment.score|
|enriched_text.entities.sentiment.type                          |더 이상 사용되지 않음|
|enriched_text.entities.text                                    |enriched_text.entities.text|
|enriched_text.entities.type                                    |enriched_text.entities.type|
|enriched_text.keywords                                          |enriched_text.keywords|
|enriched_text.keywords.knowledgeGraph.typeHierarchy            |더 이상 사용되지 않음|
|enriched_text.keywords.relevance                                |enriched_text.keywords.relevance|
|enriched_text.keywords.sentiment.mixed                          |더 이상 사용되지 않음|
|enriched_text.keywords.sentiment.score                          |enriched_text.keywords.sentiment.score|
|enriched_text.keywords.sentiment.type                          |더 이상 사용되지 않음|
|enriched_text.keywords.text                                    |enriched_text.keywords.text|
|language                                                        |language|
|enriched_text.typedRelations                                    |enriched_text.relations|
|enriched_text.typedRelations.arguments                          |enriched_text.relations.arguments|
|enriched_text.typedRelations.arguments.entities                |enriched_text.relations.arguments.entities|
|enriched_text.typedRelations.arguments.entities.text            |enriched_text.relations.arguments.entities.text|
|enriched_text.typedRelations.arguments.entities.type            |enriched_text.relations.arguments.entities.type|
|enriched_text.typedRelations.arguments.text                    |enriched_text.relations.arguments.text|
|enriched_text.typedRelations.score                              |enriched_text.relations.score|
|enriched_text.typedRelations.sentence                          |enriched_text.relations.sentence|
|enriched_text.typedRelations.type                              |enriched_text.relations.type|
|enriched_title.typedRelations                                  |enriched_title.relations|
|enriched_title.typedRelations.arguments                        |enriched_title.relations.arguments|
|enriched_title.typedRelations.arguments.entities                |enriched_title.relations.arguments.entities|
|enriched_title.typedRelations.arguments.entities.text          |enriched_title.relations.arguments.entities.text|
|enriched_title.typedRelations.arguments.entities.type          |enriched_title.relations.arguments.entities.type|
|enriched_title.typedRelations.arguments.text                    |enriched_title.relations.arguments.text|
|enriched_title.typedRelations.score                            |enriched_title.relations.score|
|enriched_title.typedRelations.sentence                          |enriched_title.relations.sentence|
|enriched_title.typedRelations.type                              |enriched_title.relations.type|
|enriched_text.relations                                        |enriched_text.semantic_roles|
|enriched_text.relations.action.lemmatized                      |enriched_text.semantic_roles.action.normalized|
|enriched_text.relations.action.text                            |enriched_text.semantic_roles.action.text|
|enriched_text.relations.action.verb.negated                    |enriched_text.semantic_roles.action.verb.negated|
|enriched_text.relations.action.verb.tense                      |enriched_text.semantic_roles.action.verb.tense|
|enriched_text.relations.action.verb.text                        |enriched_text.semantic_roles.action.verb.text|
|enriched_text.relations.location.entities                      |enriched_text.semantic_roles.location.entities|
|enriched_text.relations.location.entities.disambiguated.census    |더 이상 사용되지 않음|
|enriched_text.relations.location.entities.disambiguated.ciaFactbook    |더 이상 사용되지 않음|
|enriched_text.relations.location.entities.disambiguated.crunchbase    |더 이상 사용되지 않음|
|enriched_text.relations.location.entities.disambiguated.dbpedia    |더 이상 사용되지 않음|
|enriched_text.relations.location.entities.disambiguated.freebase    |더 이상 사용되지 않음|
|enriched_text.relations.location.entities.disambiguated.geonames    |더 이상 사용되지 않음|
|enriched_text.relations.location.entities.disambiguated.musicBrainz    |더 이상 사용되지 않음|
|enriched_text.relations.location.entities.disambiguated.name    |더 이상 사용되지 않음|
|enriched_text.relations.location.entities.disambiguated.opencyc    |더 이상 사용되지 않음|
|enriched_text.relations.location.entities.disambiguated.subType    |더 이상 사용되지 않음|
|enriched_text.relations.location.entities.disambiguated.umbel    |더 이상 사용되지 않음|
|enriched_text.relations.location.entities.disambiguated.website    |더 이상 사용되지 않음|
|enriched_text.relations.location.entities.disambiguated.yago    |더 이상 사용되지 않음|
|enriched_text.relations.location.entities.knowledgeGraph.typeHierarchy    |더 이상 사용되지 않음|
|enriched_text.relations.location.entities.sentiment.score    |더 이상 사용되지 않음|
|enriched_text.relations.location.entities.sentiment.type    |더 이상 사용되지 않음|
|enriched_text.relations.location.entities.text                  |더 이상 사용되지 않음|
|enriched_text.relations.location.entities.type                  |더 이상 사용되지 않음|
|enriched_text.relations.location.keywords                      |더 이상 사용되지 않음|
|enriched_text.relations.location.keywords.text                  |더 이상 사용되지 않음|
|enriched_text.relations.location.sentiment.score                |더 이상 사용되지 않음|
|enriched_text.relations.location.sentiment.type                |더 이상 사용되지 않음|
|enriched_text.relations.location.text                          |더 이상 사용되지 않음|
|enriched_text.relations.object.entities                        |enriched_text.semantic_roles.object.entities|
|enriched_text.relations.object.entities.disambiguated.census    |더 이상 사용되지 않음|
|enriched_text.relations.object.entities.disambiguated.ciaFactbook    |더 이상 사용되지 않음|
|enriched_text.relations.object.entities.disambiguated.crunchbase    |더 이상 사용되지 않음|
|enriched_text.relations.object.entities.disambiguated.dbpedia    |enriched_text.semantic_roles.object.entities.disambiguation.dbpedia_resource|
|enriched_text.relations.object.entities.disambiguated.freebase    |더 이상 사용되지 않음|
|enriched_text.relations.object.entities.disambiguated.geonames    |더 이상 사용되지 않음|
|enriched_text.relations.object.entities.disambiguated.musicBrainz    |더 이상 사용되지 않음|
|enriched_text.relations.object.entities.disambiguated.name    |enriched_text.semantic_roles.object.entities.disambiguation.name|
|enriched_text.relations.object.entities.disambiguated.opencyc    |더 이상 사용되지 않음|
|enriched_text.relations.object.entities.disambiguated.subType    |enriched_text.semantic_roles.object.entities.disambiguation.subtype|
|enriched_text.relations.object.entities.disambiguated.umbel    |더 이상 사용되지 않음|
|enriched_text.relations.object.entities.disambiguated.website    |더 이상 사용되지 않음|
|enriched_text.relations.object.entities.disambiguated.yago    |더 이상 사용되지 않음|
|enriched_text.relations.object.entities.knowledgeGraph.typeHierarchy    |더 이상 사용되지 않음|
|enriched_text.relations.object.entities.sentiment.score    |더 이상 사용되지 않음|
|enriched_text.relations.object.entities.sentiment.type    |더 이상 사용되지 않음|
|enriched_text.relations.object.entities.text       |enriched_text.semantic_roles.object.entities.text|
|enriched_text.relations.object.entities.type    |enriched_text.semantic_roles.object.entities.type|
|enriched_text.relations.object.keywords    |enriched_text.semantic_roles.object.keywords|
|enriched_text.relations.object.keywords.knowledgeGraph.typeHierarchy    |더 이상 사용되지 않음|
|enriched_text.relations.object.keywords.text    |enriched_text.semantic_roles.object.keywords.text|
|enriched_text.relations.object.sentiment.score    |더 이상 사용되지 않음|
|enriched_text.relations.object.sentiment.type    |더 이상 사용되지 않음|
|enriched_text.relations.object.sentimentFromSubject.score    |더 이상 사용되지 않음|
|enriched_text.relations.object.sentimentFromSubject.type    |더 이상 사용되지 않음|
|enriched_text.relations.object.text    |enriched_text.semantic_roles.object.text|
|enriched_text.relations.sentence    |enriched_text.semantic_roles.sentence|
|enriched_text.relations.subject.entities    |enriched_text.semantic_roles.subject.entities|
|enriched_text.relations.subject.entities.disambiguated.census    |더 이상 사용되지 않음|
|enriched_text.relations.subject.entities.disambiguated.ciaFactbook    |더 이상 사용되지 않음|
|enriched_text.relations.subject.entities.disambiguated.crunchbase    |더 이상 사용되지 않음|
|enriched_text.relations.subject.entities.disambiguated.dbpedia    |enriched_text.semantic_roles.subject.entities.disambiguation.dbpedia_resource|
|enriched_text.relations.subject.entities.disambiguated.freebase    |더 이상 사용되지 않음|
|enriched_text.relations.subject.entities.disambiguated.geonames    |더 이상 사용되지 않음|
|enriched_text.relations.subject.entities.disambiguated.musicBrainz    |더 이상 사용되지 않음|
|enriched_text.relations.subject.entities.disambiguated.name    |enriched_text.semantic_roles.subject.entities.disambiguation.name|
|enriched_text.relations.subject.entities.disambiguated.opencyc    |더 이상 사용되지 않음|
|enriched_text.relations.subject.entities.disambiguated.subType    |enriched_text.semantic_roles.subject.entities.disambiguation.subtype|
|enriched_text.relations.subject.entities.disambiguated.umbel    |더 이상 사용되지 않음|
|enriched_text.relations.subject.entities.disambiguated.website    |더 이상 사용되지 않음|
|enriched_text.relations.subject.entities.disambiguated.yago    |더 이상 사용되지 않음|
|enriched_text.relations.subject.entities.knowledgeGraph.typeHierarchy    |더 이상 사용되지 않음|
|enriched_text.relations.subject.entities.sentiment.score    |더 이상 사용되지 않음|
|enriched_text.relations.subject.entities.sentiment.type    |더 이상 사용되지 않음|
|enriched_text.relations.subject.entities.text    |enriched_text.semantic_roles.subject.entities.text|
|enriched_text.relations.subject.entities.type    |enriched_text.semantic_roles.subject.entities.type|
|enriched_text.relations.subject.keywords    |enriched_text.semantic_roles.subject.keywords|
|enriched_text.relations.subject.keywords.knowledgeGraph.typeHierarchy    |더 이상 사용되지 않음|
|enriched_text.relations.subject.keywords.text    |enriched_text.semantic_roles.subject.keywords.text|
|enriched_text.relations.subject.sentiment.score    |더 이상 사용되지 않음|
|enriched_text.relations.subject.sentiment.type    |더 이상 사용되지 않음|
|enriched_text.relations.subject.text    |enriched_text.semantic_roles.subject.text|
|enriched_text.taxonomy    |enriched_text.categories|
|enriched_text.taxonomy.confident    |더 이상 사용되지 않음|
|enriched_text.taxonomy.label    |enriched_text.categories.label|
|enriched_text.taxonomy.score    |enriched_text.categories.score|
|enriched_text.docEmotions.sadness    |enriched_text.emotion.document.emotion.sadness|
|enriched_text.docEmotions.joy    |enriched_text.emotion.document.emotion.joy|
|enriched_text.docEmotions.fear    |enriched_text.emotion.document.emotion.fear|
|enriched_text.docEmotions.disgust    |enriched_text.emotion.document.emotion.disgust|
|enriched_text.docEmotions.anger    |enriched_text.emotion.document.emotion.anger|
|text    |text|
|title    |title|
|url    |url|
