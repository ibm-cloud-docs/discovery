---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-16"

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

# 将扩充项迁移到 Natural Language Understanding

从 **2017 年 7 月 18 日**开始，{{site.data.keyword.discoveryfull}} 引入了名为 {{site.data.keyword.nlushort}} (NLU) 的新扩充技术。这些扩充项与现有扩充项相同，但需要的配置和模式略有不同。不推荐使用名为 {{site.data.keyword.alchemylanguageshort}} 扩充项的原始扩充项。
{: shortdesc}

对 {{site.data.keyword.alchemylanguageshort}} 扩充项的支持将于 **2018 年 1 月 15 日**结束。`2017-10-16` API 版本字符串放弃支持将新文档上传到通过 {{site.data.keyword.alchemylanguageshort}} 扩充的现有集合，并且放弃支持创建新集合并通过 {{site.data.keyword.alchemylanguageshort}} 扩充项来扩充这些集合。使用较早的 API 版本字符串可继续使用 {{site.data.keyword.alchemylanguageshort}}，直到在 **2018 年 1 月 15 日**结束支持为止。

新集合应该使用 {{site.data.keyword.nlushort}} 进行扩充，任何使用 {{site.data.keyword.alchemylanguageshort}} 配置文件的现有集合应该尽快迁移。对 {{site.data.keyword.alchemylanguageshort}} 扩充项摄入的支持将于 **2018 年 1 月 15 日**结束。有关迁移利用 {{site.data.keyword.alchemylanguageshort}} 扩充项的集合和配置文件的信息，请参阅[扩充项比较](/docs/services/discovery/migrate-nlu.html#enrichment-comparison)。

**注：**有关与 {{site.data.keyword.knowledgestudioshort}} 集成的信息，请参阅[与 {{site.data.keyword.knowledgestudiofull}} 集成](/docs/services/discovery/integrate-wks.html)。

## 扩充项比较
{: #enrichment-comparison}

{{site.data.keyword.alchemylanguageshort}} 和 {{site.data.keyword.nlushort}} 中提供的七个扩充项及其 JSON 对象名称如下：

| {{site.data.keyword.alchemylanguageshort}} 扩充项的名称| {{site.data.keyword.alchemylanguageshort}} JSON 对象| NLU 扩充项的名称| NLU JSON 对象|
|---------------------------|----------------------------------------|----------------------------------------|--------------------------------|
| 实体抽取| entities|实体抽取|   entities|
| 关键字抽取| keywords|关键字抽取|   keywords|
| 分类法分类| taxonomy                        |类别分类*|   categories*|
| 概念标记| concepts                        |概念标记|   concepts            |
| 观点分析| docSentiment                    |观点分析|   sentiment*          |
| 情绪分析| docEmotions                     |情绪分析|   emotion*            |
| 关系抽取| relations                       |语义角色抽取*|   semantic_roles*     |
 \* 名称更改

有关 {{site.data.keyword.alchemylanguageshort}} 扩充项的更多信息，请参阅 [{{site.data.keyword.alchemylanguageshort}} 扩充项](/docs/services/discovery/discovery-auxiliary.html#AlchemyLanguage-enrichments)。有关 {{site.data.keyword.nlushort}} 扩充项的更多信息，请参阅[添加扩充项](/docs/services/discovery/building.html#adding-enrichments)

## 主要更改概述

- {{site.data.keyword.nlushort}} 扩充项的 JSON 模式不同于 {{site.data.keyword.alchemylanguageshort}} 扩充项中使用的 JSON 模式；要获取对每个扩充项的更改的完整列表，请参阅：[扩充项模式差异](/docs/services/discovery/migrate-nlu.html#enrichment-schema-differences)。
- _分类法分类_ ({{site.data.keyword.alchemylanguageshort}}) 扩充项现在名为_类别分类_。其 JSON 对象名称已从 `taxonomy` 更改为 `categories`。
- _关系抽取_ ({{site.data.keyword.alchemylanguageshort}}) 扩充项现在名为_语义角色抽取_。其 JSON 对象名称已从 `relations` 更改为 `semantic_roles`。
- _观点分析_的 JSON 对象名称已从 `docSentiment` 更改为 `sentiment`。
- _情绪分析_的 JSON 对象名称已从 `docEmotions` 更改为 `emotion`。

## 配置文件更改

**{{site.data.keyword.alchemylanguageshort}}** 缺省配置文件（在工具中名为 `Default Configuration`）对文档的 text 字段应用了以下扩充项：**实体抽取**、**关键字抽取**、**分类法分类**、**概念标记**、**关系抽取**和**观点分析**。该文件还包含基于字体样式和大小的标准文档转换。

**{{site.data.keyword.nlushort}}** 缺省配置文件名为 `Default Configuration with NLU`，对文档的 text 字段应用了以下扩充项：**实体抽取**、**观点分析**、**类别分类**和**概念标记**。该文件还包含基于字体样式和大小的标准文档转换。这些文档转换与 {{site.data.keyword.alchemylanguageshort}} 缺省配置文件中的转换完全相同。

## 迁移配置、集合和查询

如果已创建任何定制配置，那么需要创建使用 {{site.data.keyword.nlushort}} 扩充项的新配置。有关指示信息，请参阅以下文档：

- [工具](/docs/services/discovery/building.html#custom-configuration)
- [API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#add_configuration){: new_window}

如果现有集合已应用 {{site.data.keyword.alchemylanguageshort}} 缺省配置或定制 {{site.data.keyword.alchemylanguageshort}} 配置，那么需要创建新的集合，应用 {{site.data.keyword.nlushort}} 配置文件（缺省配置或新的定制配置），然后上传文档。有关指示信息，请参阅以下文档：

- [工具](/docs/services/discovery/building.html#preparing-the-service-for-your-documents)
- [API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#create-collection){: new_window}

对于使用 Discovery Query Language 创建的任何查询，需要检查 {{site.data.keyword.alchemylanguageshort}} 和 {{site.data.keyword.nlushort}} 之间的 JSON 模式更改，并相应地更新查询和查询 URL。请参阅[扩充项模式差异](/docs/services/discovery/migrate-nlu.html#enrichment-schema-differences)以获取详细信息。

## 扩充项模式差异

下表显示了 {{site.data.keyword.nlushort}} 扩充项和 {{site.data.keyword.alchemylanguageshort}} 扩充项的 JSON 模式之间的差异。

| {{site.data.keyword.alchemylanguageshort}}                         | {{site.data.keyword.nlushort}}       |
|-----------------------------------------|--------------------------------------|
|enriched_text.concepts                      |enriched_text.concepts|
|enriched_text.concepts.census              |不推荐|
|enriched_text.concepts.ciaFactbook          |不推荐|
|enriched_text.concepts.crunchbase                              |不推荐|
|enriched_text.concepts.dbpedia                               |enriched_text.concepts.dbpedia_resource|
|enriched_text.concepts.freebase                              |不推荐|
|enriched_text.concepts.geonames                                |不推荐|
|enriched_text.concepts.knowledgeGraph.typeHierarchy            |不推荐|
|enriched_text.concepts.musicBrainz                              |不推荐|
|enriched_text.concepts.opencyc                                  |不推荐|
|enriched_text.concepts.relevance                                |enriched_text.concepts.relevance|
|enriched_text.concepts.text                                    |enriched_text.concepts.text|
|enriched_text.concepts.website                                  |不推荐|
|enriched_text.concepts.yago                                    |不推荐|
|enriched_text.docSentiment.mixed                                |不推荐|
|enriched_text.docSentiment.score                                |enriched_text.sentiment.document.score|
|enriched_text.docSentiment.type                                |enriched_text.sentiment.document.label|
|enriched_text.entities                                          |enriched_text.entities|
|enriched_text.entities.count                                    |enriched_text.entities.count|
|enriched_text.entities.disambiguated.census                    |不推荐|
|enriched_text.entities.disambiguated.ciaFactbook                |不推荐|
|enriched_text.entities.disambiguated.crunchbase                |不推荐|
|enriched_text.entities.disambiguated.dbpedia                    |enriched_text.entities.disambiguation.dbpedia_resource|
|enriched_text.entities.disambiguated.freebase                  |不推荐|
|enriched_text.entities.disambiguated.geonames                  |不推荐|
|enriched_text.entities.disambiguated.musicBrainz                |不推荐|
|enriched_text.entities.disambiguated.name                      |enriched_text.entities.disambiguation.name|
|enriched_text.entities.disambiguated.opencyc                    |不推荐|
|enriched_text.entities.disambiguated.subType                    |enriched_text.entities.disambiguation.subtype|
|enriched_text.entities.disambiguated.umbel                      |不推荐|
|enriched_text.entities.disambiguated.website                    |不推荐|
|enriched_text.entities.disambiguated.yago                      |不推荐|
|enriched_text.entities.knowledgeGraph.typeHierarchy            |不推荐|
|enriched_text.entities.quotations                              |不推荐|
|enriched_text.entities.quotations.quotation                    |不推荐|
|enriched_text.entities.quotations.sentiment.mixed              |不推荐|
|enriched_text.entities.quotations.sentiment.score              |不推荐|
|enriched_text.entities.quotations.sentiment.type                |不推荐|
|enriched_text.entities.relevance                                |enriched_text.entities.relevance|
|enriched_text.entities.sentiment.mixed                          |不推荐|
|enriched_text.entities.sentiment.score                          |enriched_text.entities.sentiment.score|
|enriched_text.entities.sentiment.type                          |不推荐|
|enriched_text.entities.text                                    |enriched_text.entities.text|
|enriched_text.entities.type                                    |enriched_text.entities.type|
|enriched_text.keywords                                          |enriched_text.keywords|
|enriched_text.keywords.knowledgeGraph.typeHierarchy            |不推荐|
|enriched_text.keywords.relevance                                |enriched_text.keywords.relevance|
|enriched_text.keywords.sentiment.mixed                          |不推荐|
|enriched_text.keywords.sentiment.score                          |enriched_text.keywords.sentiment.score|
|enriched_text.keywords.sentiment.type                          |不推荐|
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
|enriched_text.relations.location.entities.disambiguated.census    |不推荐|
|enriched_text.relations.location.entities.disambiguated.ciaFactbook    |不推荐|
|enriched_text.relations.location.entities.disambiguated.crunchbase    |不推荐|
|enriched_text.relations.location.entities.disambiguated.dbpedia    |不推荐|
|enriched_text.relations.location.entities.disambiguated.freebase    |不推荐|
|enriched_text.relations.location.entities.disambiguated.geonames    |不推荐|
|enriched_text.relations.location.entities.disambiguated.musicBrainz    |不推荐|
|enriched_text.relations.location.entities.disambiguated.name    |不推荐|
|enriched_text.relations.location.entities.disambiguated.opencyc    |不推荐|
|enriched_text.relations.location.entities.disambiguated.subType    |不推荐|
|enriched_text.relations.location.entities.disambiguated.umbel    |不推荐|
|enriched_text.relations.location.entities.disambiguated.website    |不推荐|
|enriched_text.relations.location.entities.disambiguated.yago    |不推荐|
|enriched_text.relations.location.entities.knowledgeGraph.typeHierarchy    |不推荐|
|enriched_text.relations.location.entities.sentiment.score    |不推荐|
|enriched_text.relations.location.entities.sentiment.type    |不推荐|
|enriched_text.relations.location.entities.text                  |不推荐|
|enriched_text.relations.location.entities.type                  |不推荐|
|enriched_text.relations.location.keywords                      |不推荐|
|enriched_text.relations.location.keywords.text                  |不推荐|
|enriched_text.relations.location.sentiment.score                |不推荐|
|enriched_text.relations.location.sentiment.type                |不推荐|
|enriched_text.relations.location.text                          |不推荐|
|enriched_text.relations.object.entities                        |enriched_text.semantic_roles.object.entities|
|enriched_text.relations.object.entities.disambiguated.census    |不推荐|
|enriched_text.relations.object.entities.disambiguated.ciaFactbook    |不推荐|
|enriched_text.relations.object.entities.disambiguated.crunchbase    |不推荐|
|enriched_text.relations.object.entities.disambiguated.dbpedia    |enriched_text.semantic_roles.object.entities.disambiguation.dbpedia_resource|
|enriched_text.relations.object.entities.disambiguated.freebase    |不推荐|
|enriched_text.relations.object.entities.disambiguated.geonames    |不推荐|
|enriched_text.relations.object.entities.disambiguated.musicBrainz    |不推荐|
|enriched_text.relations.object.entities.disambiguated.name    |enriched_text.semantic_roles.object.entities.disambiguation.name|
|enriched_text.relations.object.entities.disambiguated.opencyc    |不推荐|
|enriched_text.relations.object.entities.disambiguated.subType    |enriched_text.semantic_roles.object.entities.disambiguation.subtype|
|enriched_text.relations.object.entities.disambiguated.umbel    |不推荐|
|enriched_text.relations.object.entities.disambiguated.website    |不推荐|
|enriched_text.relations.object.entities.disambiguated.yago    |不推荐|
|enriched_text.relations.object.entities.knowledgeGraph.typeHierarchy    |不推荐|
|enriched_text.relations.object.entities.sentiment.score    |不推荐|
|enriched_text.relations.object.entities.sentiment.type    |不推荐|
|enriched_text.relations.object.entities.text       |enriched_text.semantic_roles.object.entities.text|
|enriched_text.relations.object.entities.type    |enriched_text.semantic_roles.object.entities.type|
|enriched_text.relations.object.keywords    |enriched_text.semantic_roles.object.keywords|
|enriched_text.relations.object.keywords.knowledgeGraph.typeHierarchy    |不推荐|
|enriched_text.relations.object.keywords.text    |enriched_text.semantic_roles.object.keywords.text|
|enriched_text.relations.object.sentiment.score    |不推荐|
|enriched_text.relations.object.sentiment.type    |不推荐|
|enriched_text.relations.object.sentimentFromSubject.score    |不推荐|
|enriched_text.relations.object.sentimentFromSubject.type    |不推荐|
|enriched_text.relations.object.text    |enriched_text.semantic_roles.object.text|
|enriched_text.relations.sentence    |enriched_text.semantic_roles.sentence|
|enriched_text.relations.subject.entities    |enriched_text.semantic_roles.subject.entities|
|enriched_text.relations.subject.entities.disambiguated.census    |不推荐|
|enriched_text.relations.subject.entities.disambiguated.ciaFactbook    |不推荐|
|enriched_text.relations.subject.entities.disambiguated.crunchbase    |不推荐|
|enriched_text.relations.subject.entities.disambiguated.dbpedia    |enriched_text.semantic_roles.subject.entities.disambiguation.dbpedia_resource|
|enriched_text.relations.subject.entities.disambiguated.freebase    |不推荐|
|enriched_text.relations.subject.entities.disambiguated.geonames    |不推荐|
|enriched_text.relations.subject.entities.disambiguated.musicBrainz    |不推荐|
|enriched_text.relations.subject.entities.disambiguated.name    |enriched_text.semantic_roles.subject.entities.disambiguation.name|
|enriched_text.relations.subject.entities.disambiguated.opencyc    |不推荐|
|enriched_text.relations.subject.entities.disambiguated.subType    |enriched_text.semantic_roles.subject.entities.disambiguation.subtype|
|enriched_text.relations.subject.entities.disambiguated.umbel    |不推荐|
|enriched_text.relations.subject.entities.disambiguated.website    |不推荐|
|enriched_text.relations.subject.entities.disambiguated.yago    |不推荐|
|enriched_text.relations.subject.entities.knowledgeGraph.typeHierarchy    |不推荐|
|enriched_text.relations.subject.entities.sentiment.score    |不推荐|
|enriched_text.relations.subject.entities.sentiment.type    |不推荐|
|enriched_text.relations.subject.entities.text    |enriched_text.semantic_roles.subject.entities.text|
|enriched_text.relations.subject.entities.type    |enriched_text.semantic_roles.subject.entities.type|
|enriched_text.relations.subject.keywords    |enriched_text.semantic_roles.subject.keywords|
|enriched_text.relations.subject.keywords.knowledgeGraph.typeHierarchy    |不推荐|
|enriched_text.relations.subject.keywords.text    |enriched_text.semantic_roles.subject.keywords.text|
|enriched_text.relations.subject.sentiment.score    |不推荐|
|enriched_text.relations.subject.sentiment.type    |不推荐|
|enriched_text.relations.subject.text    |enriched_text.semantic_roles.subject.text|
|enriched_text.taxonomy    |enriched_text.categories|
|enriched_text.taxonomy.confident    |不推荐|
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
