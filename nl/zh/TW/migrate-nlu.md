---

copyright:
  years: 2015, 2018
lastupdated: "2018-02-28"

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

# 將強化移轉至 Natural Language Understanding
{: #migrate-nlu}

從 **2017 年 7 月 18 日**開始，{{site.data.keyword.discoveryfull}} 引進了一項新的強化技術，名稱為 {{site.data.keyword.nlushort}} (NLU)。{{site.data.keyword.alchemylanguageshort}} 強化從 **2018 年 3 月 1 日**起已淘汰。
{: shortdesc}

任何利用 {{site.data.keyword.alchemylanguageshort}} 強化的現有集合都必須加以移轉。如需移轉利用 {{site.data.keyword.alchemylanguageshort}} 強化的集合和配置檔的相關資訊，請參閱[強化比較](/docs/services/discovery/migrate-nlu.html#enrichment-comparison)。

**附註：**如需與 {{site.data.keyword.knowledgestudioshort}} 整合的相關資訊，請參閱[與 {{site.data.keyword.knowledgestudiofull}} 整合](/docs/services/discovery/integrate-wks.html)。

## 強化比較
{: #enrichment-comparison}

{{site.data.keyword.alchemylanguageshort}} 和 {{site.data.keyword.nlushort}} 中可用的七個強化及其 JSON 物件名稱如下：

|{{site.data.keyword.alchemylanguageshort}} 強化的名稱         |{{site.data.keyword.alchemylanguageshort}} JSON 物件            |NLU 強化的名稱                     |NLU JSON 物件        |
|---------------------------|----------------------------------------|----------------------------------------|--------------------------------|
|實體擷取                              |entities                        |實體擷取                                    |entities                        |
|關鍵字擷取                            |keywords                        |關鍵字擷取                                  |keywords                        |
|分類架構分類                          |taxonomy                        |種類分類*                             |categories*         |
|概念標記                              |concepts            |概念標記                                    |concepts            |
|觀感分析                              |docSentiment                    |觀感分析                                    |sentiment*          |
|情緒分析                              |docEmotions                     |情緒分析                                    |emotion*            |
|關係擷取                              |relations                       |語意角色擷取*                         |semantic_roles*     |
 \* 名稱變更



如需 {{site.data.keyword.nlushort}} 強化的相關資訊，請參閱[新增強化](/docs/services/discovery/building.html#adding-enrichments)

## 主要變更概觀

- {{site.data.keyword.nlushort}} 強化的 JSON 綱目與 {{site.data.keyword.alchemylanguageshort}} 強化所使用的綱目不同，如需每一項強化的完整變更清單，請參閱：[強化綱目差異](/docs/services/discovery/migrate-nlu.html#enrichment-schema-differences)。
- _分類架構分類_ ({{site.data.keyword.alchemylanguageshort}}) 強化現在已命名為_種類分類_。它的 JSON 物件名稱已從 `taxonomy` 變更為 `categories`。
- _關係擷取_ ({{site.data.keyword.alchemylanguageshort}}) 強化現在已命名為_語意角色擷取_。它的 JSON 物件名稱已從 `relations` 變更為 `semantic_roles`。
- _觀感分析_ 的 JSON 物件名稱已從 `docSentiment` 變更為 `sentiment`。
- _情緒分析_ 的 JSON 物件名稱已從 `docEmotions` 變更為 `emotion`。

## 配置檔變更

**{{site.data.keyword.alchemylanguageshort}}** 預設配置檔（在工具中名稱為 `Default configuration`）已將下列強化套用至您文件的文字欄位：**實體擷取**、**關鍵字擷取**、**分類架構分類**、**概念標記**、**關係擷取**及**觀感分析**。此檔案也包括基於字型樣式及大小的標準文件轉換。

**{{site.data.keyword.nlushort}}** 預設配置檔名稱為 `Default Configuration with NLU`，它會將下列強化套用至您文件的文字欄位：**實體擷取**、**觀感分析**、**種類分類**及**概念標記**。此檔案也包括基於字型樣式及大小的標準文件轉換。這些文件轉換與 {{site.data.keyword.alchemylanguageshort}} 預設配置檔中的轉換相同。

## 移轉配置、集合及查詢

如果您已建立任何自訂配置，則需要建立使用 {{site.data.keyword.nlushort}} 強化的新配置。如需指示，請參閱下列文件：

- [工具](/docs/services/discovery/building.html#custom-configuration)
- [API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#add_configuration){: new_window}

如果您的現有集合中已套用 {{site.data.keyword.alchemylanguageshort}} 預設配置或自訂 {{site.data.keyword.alchemylanguageshort}} 配置，則需要建立新的集合、套用 {{site.data.keyword.nlushort}} 配置檔（預設配置或新的自訂配置），以及上傳文件。如需指示，請參閱下列文件：

- [工具](/docs/services/discovery/building.html#preparing-the-service-for-your-documents)
- [API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#create-collection){: new_window}

對於您使用「Discovery 查詢語言」建立的任何查詢，您需要檢查 {{site.data.keyword.alchemylanguageshort}} 與 {{site.data.keyword.nlushort}} 之間的 JSON 綱目變更，並據此更新您的查詢和查詢 URL。如需詳細資料，請參閱[強化綱目差異](/docs/services/discovery/migrate-nlu.html#enrichment-schema-differences)。

## 強化綱目差異

下表顯示 {{site.data.keyword.nlushort}} 強化與 {{site.data.keyword.alchemylanguageshort}} 強化的 JSON 綱目之間的差異。

| {{site.data.keyword.alchemylanguageshort}}                         | {{site.data.keyword.nlushort}}       |
|-----------------------------------------|--------------------------------------|
|enriched_text.concepts                      |enriched_text.concepts|
|enriched_text.concepts.census              |已淘汰|
|enriched_text.concepts.ciaFactbook          |已淘汰|
|enriched_text.concepts.crunchbase                              |已淘汰|
|enriched_text.concepts.dbpedia                               |enriched_text.concepts.dbpedia_resource|
|enriched_text.concepts.freebase                              |已淘汰|
|enriched_text.concepts.geonames                                |已淘汰|
|enriched_text.concepts.knowledgeGraph.typeHierarchy            |已淘汰|
|enriched_text.concepts.musicBrainz                              |已淘汰|
|enriched_text.concepts.opencyc                                  |已淘汰|
|enriched_text.concepts.relevance                                |enriched_text.concepts.relevance|
|enriched_text.concepts.text                                    |enriched_text.concepts.text|
|enriched_text.concepts.website                                  |已淘汰|
|enriched_text.concepts.yago                                    |已淘汰|
|enriched_text.docSentiment.mixed                                |已淘汰|
|enriched_text.docSentiment.score                                |enriched_text.sentiment.document.score|
|enriched_text.docSentiment.type                                |enriched_text.sentiment.document.label|
|enriched_text.entities                                          |enriched_text.entities|
|enriched_text.entities.count                                    |enriched_text.entities.count|
|enriched_text.entities.disambiguated.census                    |已淘汰|
|enriched_text.entities.disambiguated.ciaFactbook                |已淘汰|
|enriched_text.entities.disambiguated.crunchbase                |已淘汰|
|enriched_text.entities.disambiguated.dbpedia                    |enriched_text.entities.disambiguation.dbpedia_resource|
|enriched_text.entities.disambiguated.freebase                  |已淘汰|
|enriched_text.entities.disambiguated.geonames                  |已淘汰|
|enriched_text.entities.disambiguated.musicBrainz                |已淘汰|
|enriched_text.entities.disambiguated.name                      |enriched_text.entities.disambiguation.name|
|enriched_text.entities.disambiguated.opencyc                    |已淘汰|
|enriched_text.entities.disambiguated.subType                    |enriched_text.entities.disambiguation.subtype|
|enriched_text.entities.disambiguated.umbel                      |已淘汰|
|enriched_text.entities.disambiguated.website                    |已淘汰|
|enriched_text.entities.disambiguated.yago                      |已淘汰|
|enriched_text.entities.knowledgeGraph.typeHierarchy            |已淘汰|
|enriched_text.entities.quotations                              |已淘汰|
|enriched_text.entities.quotations.quotation                    |已淘汰|
|enriched_text.entities.quotations.sentiment.mixed              |已淘汰|
|enriched_text.entities.quotations.sentiment.score              |已淘汰|
|enriched_text.entities.quotations.sentiment.type                |已淘汰|
|enriched_text.entities.relevance                                |enriched_text.entities.relevance|
|enriched_text.entities.sentiment.mixed                          |已淘汰|
|enriched_text.entities.sentiment.score                          |enriched_text.entities.sentiment.score|
|enriched_text.entities.sentiment.type                          |已淘汰|
|enriched_text.entities.text                                    |enriched_text.entities.text|
|enriched_text.entities.type                                    |enriched_text.entities.type|
|enriched_text.keywords                                          |enriched_text.keywords|
|enriched_text.keywords.knowledgeGraph.typeHierarchy            |已淘汰|
|enriched_text.keywords.relevance                                |enriched_text.keywords.relevance|
|enriched_text.keywords.sentiment.mixed                          |已淘汰|
|enriched_text.keywords.sentiment.score                          |enriched_text.keywords.sentiment.score|
|enriched_text.keywords.sentiment.type                          |已淘汰|
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
|enriched_text.relations.location.entities.disambiguated.census    |已淘汰|
|enriched_text.relations.location.entities.disambiguated.ciaFactbook    |已淘汰|
|enriched_text.relations.location.entities.disambiguated.crunchbase    |已淘汰|
|enriched_text.relations.location.entities.disambiguated.dbpedia    |已淘汰|
|enriched_text.relations.location.entities.disambiguated.freebase    |已淘汰|
|enriched_text.relations.location.entities.disambiguated.geonames    |已淘汰|
|enriched_text.relations.location.entities.disambiguated.musicBrainz    |已淘汰|
|enriched_text.relations.location.entities.disambiguated.name    |已淘汰|
|enriched_text.relations.location.entities.disambiguated.opencyc    |已淘汰|
|enriched_text.relations.location.entities.disambiguated.subType    |已淘汰|
|enriched_text.relations.location.entities.disambiguated.umbel    |已淘汰|
|enriched_text.relations.location.entities.disambiguated.website    |已淘汰|
|enriched_text.relations.location.entities.disambiguated.yago    |已淘汰|
|enriched_text.relations.location.entities.knowledgeGraph.typeHierarchy    |已淘汰|
|enriched_text.relations.location.entities.sentiment.score    |已淘汰|
|enriched_text.relations.location.entities.sentiment.type    |已淘汰|
|enriched_text.relations.location.entities.text                  |已淘汰|
|enriched_text.relations.location.entities.type                  |已淘汰|
|enriched_text.relations.location.keywords                      |已淘汰|
|enriched_text.relations.location.keywords.text                  |已淘汰|
|enriched_text.relations.location.sentiment.score                |已淘汰|
|enriched_text.relations.location.sentiment.type                |已淘汰|
|enriched_text.relations.location.text                          |已淘汰|
|enriched_text.relations.object.entities                        |enriched_text.semantic_roles.object.entities|
|enriched_text.relations.object.entities.disambiguated.census    |已淘汰|
|enriched_text.relations.object.entities.disambiguated.ciaFactbook    |已淘汰|
|enriched_text.relations.object.entities.disambiguated.crunchbase    |已淘汰|
|enriched_text.relations.object.entities.disambiguated.dbpedia    |enriched_text.semantic_roles.object.entities.disambiguation.dbpedia_resource|
|enriched_text.relations.object.entities.disambiguated.freebase    |已淘汰|
|enriched_text.relations.object.entities.disambiguated.geonames    |已淘汰|
|enriched_text.relations.object.entities.disambiguated.musicBrainz    |已淘汰|
|enriched_text.relations.object.entities.disambiguated.name    |enriched_text.semantic_roles.object.entities.disambiguation.name|
|enriched_text.relations.object.entities.disambiguated.opencyc    |已淘汰|
|enriched_text.relations.object.entities.disambiguated.subType    |enriched_text.semantic_roles.object.entities.disambiguation.subtype|
|enriched_text.relations.object.entities.disambiguated.umbel    |已淘汰|
|enriched_text.relations.object.entities.disambiguated.website    |已淘汰|
|enriched_text.relations.object.entities.disambiguated.yago    |已淘汰|
|enriched_text.relations.object.entities.knowledgeGraph.typeHierarchy    |已淘汰|
|enriched_text.relations.object.entities.sentiment.score    |已淘汰|
|enriched_text.relations.object.entities.sentiment.type    |已淘汰|
|enriched_text.relations.object.entities.text       |enriched_text.semantic_roles.object.entities.text|
|enriched_text.relations.object.entities.type    |enriched_text.semantic_roles.object.entities.type|
|enriched_text.relations.object.keywords    |enriched_text.semantic_roles.object.keywords|
|enriched_text.relations.object.keywords.knowledgeGraph.typeHierarchy    |已淘汰|
|enriched_text.relations.object.keywords.text    |enriched_text.semantic_roles.object.keywords.text|
|enriched_text.relations.object.sentiment.score    |已淘汰|
|enriched_text.relations.object.sentiment.type    |已淘汰|
|enriched_text.relations.object.sentimentFromSubject.score    |已淘汰|
|enriched_text.relations.object.sentimentFromSubject.type    |已淘汰|
|enriched_text.relations.object.text    |enriched_text.semantic_roles.object.text|
|enriched_text.relations.sentence    |enriched_text.semantic_roles.sentence|
|enriched_text.relations.subject.entities    |enriched_text.semantic_roles.subject.entities|
|enriched_text.relations.subject.entities.disambiguated.census    |已淘汰|
|enriched_text.relations.subject.entities.disambiguated.ciaFactbook    |已淘汰|
|enriched_text.relations.subject.entities.disambiguated.crunchbase    |已淘汰|
|enriched_text.relations.subject.entities.disambiguated.dbpedia    |enriched_text.semantic_roles.subject.entities.disambiguation.dbpedia_resource|
|enriched_text.relations.subject.entities.disambiguated.freebase    |已淘汰|
|enriched_text.relations.subject.entities.disambiguated.geonames    |已淘汰|
|enriched_text.relations.subject.entities.disambiguated.musicBrainz    |已淘汰|
|enriched_text.relations.subject.entities.disambiguated.name    |enriched_text.semantic_roles.subject.entities.disambiguation.name|
|enriched_text.relations.subject.entities.disambiguated.opencyc    |已淘汰|
|enriched_text.relations.subject.entities.disambiguated.subType    |enriched_text.semantic_roles.subject.entities.disambiguation.subtype|
|enriched_text.relations.subject.entities.disambiguated.umbel    |已淘汰|
|enriched_text.relations.subject.entities.disambiguated.website    |已淘汰|
|enriched_text.relations.subject.entities.disambiguated.yago    |已淘汰|
|enriched_text.relations.subject.entities.knowledgeGraph.typeHierarchy    |已淘汰|
|enriched_text.relations.subject.entities.sentiment.score    |已淘汰|
|enriched_text.relations.subject.entities.sentiment.type    |已淘汰|
|enriched_text.relations.subject.entities.text    |enriched_text.semantic_roles.subject.entities.text|
|enriched_text.relations.subject.entities.type    |enriched_text.semantic_roles.subject.entities.type|
|enriched_text.relations.subject.keywords    |enriched_text.semantic_roles.subject.keywords|
|enriched_text.relations.subject.keywords.knowledgeGraph.typeHierarchy    |已淘汰|
|enriched_text.relations.subject.keywords.text    |enriched_text.semantic_roles.subject.keywords.text|
|enriched_text.relations.subject.sentiment.score    |已淘汰|
|enriched_text.relations.subject.sentiment.type    |已淘汰|
|enriched_text.relations.subject.text    |enriched_text.semantic_roles.subject.text|
|enriched_text.taxonomy    |enriched_text.categories|
|enriched_text.taxonomy.confident    |已淘汰|
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
