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

# Migrating enrichments to Natural Language Understanding

Starting on **18 July, 2017** {{site.data.keyword.discoveryfull}} introduced a new enrichment technology, named {{site.data.keyword.nlushort}} (NLU). {{site.data.keyword.alchemylanguageshort}} enrichments were deprecated effective **1 March 2018**. 
{: shortdesc}

Any existing collections that utilize {{site.data.keyword.alchemylanguageshort}} enrichments must be migrated. For information on migrating collections and configuration files that utilize the {{site.data.keyword.alchemylanguageshort}} enrichments, see [Enrichment comparison](/docs/services/discovery/migrate-nlu.html#enrichment-comparison).

**Note:** For information about integrating with {{site.data.keyword.knowledgestudioshort}}, see [Integrating with {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery/integrate-wks.html).

## Enrichment comparison
{: #enrichment-comparison}

The seven enrichments available in {{site.data.keyword.alchemylanguageshort}} and {{site.data.keyword.nlushort}}, along with their JSON object names are:

| Name of {{site.data.keyword.alchemylanguageshort}} Enrichment         | {{site.data.keyword.alchemylanguageshort}} JSON object            | Name of NLU Enrichment                     | NLU JSON object        |
|---------------------------|----------------------------------------|----------------------------------------|--------------------------------|
| Entity Extraction                     | entities                        |Entity Extraction                           |   entities            |
| Keyword Extraction                    | keywords                        |Keyword Extraction                          |   keywords            |
| Taxonomy Classification               | taxonomy                        |Category Classification*                    |   categories*         |
| Concept Tagging                       | concepts                        |Concept Tagging                             |   concepts            |
| Sentiment Analysis                    | docSentiment                    |Sentiment Analysis                          |   sentiment*          |
| Emotion Analysis                      | docEmotions                     |Emotion Analysis                            |   emotion*            |
| Relation Extraction                   | relations                       |Semantic Role Extraction*                   |   semantic_roles*     |
 \* Name change

For more information about {{site.data.keyword.nlushort}} enrichments, see [Adding enrichments](/docs/services/discovery/building.html#adding-enrichments)

## Overview of major changes

- The JSON schema for {{site.data.keyword.nlushort}} enrichments differs from the one used in the {{site.data.keyword.alchemylanguageshort}} enrichments, for a full list of the changes to each enrichment, see: [Enrichment schema differences](/docs/services/discovery/migrate-nlu.html#enrichment-schema-differences).
- The _Taxonomy Classification_ ({{site.data.keyword.alchemylanguageshort}}) enrichment is now named _Category Classification_. Its JSON object name has been changed from `taxonomy` to `categories`.
- The _Relation Extraction_ ({{site.data.keyword.alchemylanguageshort}}) enrichment is now named _Semantic Role Extraction_. Its JSON object name has been changed from `relations` to `semantic_roles`.
- The JSON object name for _Sentiment Analysis_ has been changed from `docSentiment` to `sentiment`.
- The JSON object name for _Emotion Analysis_ has been changed from `docEmotions` to `emotion`.

## Configuration file changes

The **{{site.data.keyword.alchemylanguageshort}}** default configuration file (named `Default configuration` in the tooling) applied the following enrichments to the text field of your documents: **Entity Extraction**, **Keyword Extraction**, **Taxonomy Classification**, **Concept Tagging**, **Relation Extraction**, and **Sentiment Analysis**. The file also includes standard document conversions based on font styles and sizes.

The **{{site.data.keyword.nlushort}}** default configuration file is named `Default Configuration with NLU`, and applied the following enrichments to the text field of your documents: **Entity Extraction**, **Sentiment Analysis**, **Category Classification**, and **Concept Tagging**. The file also includes standard document conversions based on font styles and sizes. These document conversions are identical to the ones in the {{site.data.keyword.alchemylanguageshort}} default configuration file.

## Migrating your configurations, collections, and queries

If you have created any custom configurations, you need to create new ones that use the {{site.data.keyword.nlushort}} enrichments. For instructions, see these docs:

- [Tooling](/docs/services/discovery/building.html#custom-configuration)
- [API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/discovery#add-configuration){: new_window}

If you have existing collections that have either the {{site.data.keyword.alchemylanguageshort}} default configuration or a custom {{site.data.keyword.alchemylanguageshort}} configuration applied to them, you need to create a new collection, apply the {{site.data.keyword.nlushort}} configuration file (either the default configuration or a new custom configuration), and upload your documents. For instructions see these docs:

- [Tooling](/docs/services/discovery/building.html#preparing-the-service-for-your-documents)
- [API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/discovery#create-a-collection){: new_window}

For any queries you have created using the Discovery Query Language, you need to examine the JSON schema changes between {{site.data.keyword.alchemylanguageshort}} and {{site.data.keyword.nlushort}} and update your queries and Query URLs accordingly. See [Enrichment schema differences](/docs/services/discovery/migrate-nlu.html#enrichment-schema-differences) for details.

## Enrichment schema differences

The following table shows the differences between the JSON schema for {{site.data.keyword.nlushort}} enrichments and {{site.data.keyword.alchemylanguageshort}} enrichments.

| {{site.data.keyword.alchemylanguageshort}}                         | {{site.data.keyword.nlushort}}       |
|-----------------------------------------|--------------------------------------|
|enriched_text.concepts                      |enriched_text.concepts|
|enriched_text.concepts.census              |deprecated|
|enriched_text.concepts.ciaFactbook          |deprecated|
|enriched_text.concepts.crunchbase                              |deprecated|
|enriched_text.concepts.dbpedia                               |enriched_text.concepts.dbpedia_resource|
|enriched_text.concepts.freebase                              |deprecated|
|enriched_text.concepts.geonames                                |deprecated|
|enriched_text.concepts.knowledgeGraph.typeHierarchy            |deprecated|
|enriched_text.concepts.musicBrainz                              |deprecated|
|enriched_text.concepts.opencyc                                  |deprecated|
|enriched_text.concepts.relevance                                |enriched_text.concepts.relevance|
|enriched_text.concepts.text                                    |enriched_text.concepts.text|
|enriched_text.concepts.website                                  |deprecated|
|enriched_text.concepts.yago                                    |deprecated|
|enriched_text.docSentiment.mixed                                |deprecated|
|enriched_text.docSentiment.score                                |enriched_text.sentiment.document.score|
|enriched_text.docSentiment.type                                |enriched_text.sentiment.document.label|
|enriched_text.entities                                          |enriched_text.entities|
|enriched_text.entities.count                                    |enriched_text.entities.count|
|enriched_text.entities.disambiguated.census                    |deprecated|
|enriched_text.entities.disambiguated.ciaFactbook                |deprecated|
|enriched_text.entities.disambiguated.crunchbase                |deprecated|
|enriched_text.entities.disambiguated.dbpedia                    |enriched_text.entities.disambiguation.dbpedia_resource|
|enriched_text.entities.disambiguated.freebase                  |deprecated|
|enriched_text.entities.disambiguated.geonames                  |deprecated|
|enriched_text.entities.disambiguated.musicBrainz                |deprecated|
|enriched_text.entities.disambiguated.name                      |enriched_text.entities.disambiguation.name|
|enriched_text.entities.disambiguated.opencyc                    |deprecated|
|enriched_text.entities.disambiguated.subType                    |enriched_text.entities.disambiguation.subtype|
|enriched_text.entities.disambiguated.umbel                      |deprecated|
|enriched_text.entities.disambiguated.website                    |deprecated|
|enriched_text.entities.disambiguated.yago                      |deprecated|
|enriched_text.entities.knowledgeGraph.typeHierarchy            |deprecated|
|enriched_text.entities.quotations                              |deprecated|
|enriched_text.entities.quotations.quotation                    |deprecated|
|enriched_text.entities.quotations.sentiment.mixed              |deprecated|
|enriched_text.entities.quotations.sentiment.score              |deprecated|
|enriched_text.entities.quotations.sentiment.type                |deprecated|
|enriched_text.entities.relevance                                |enriched_text.entities.relevance|
|enriched_text.entities.sentiment.mixed                          |deprecated|
|enriched_text.entities.sentiment.score                          |enriched_text.entities.sentiment.score|
|enriched_text.entities.sentiment.type                          |deprecated|
|enriched_text.entities.text                                    |enriched_text.entities.text|
|enriched_text.entities.type                                    |enriched_text.entities.type|
|enriched_text.keywords                                          |enriched_text.keywords|
|enriched_text.keywords.knowledgeGraph.typeHierarchy            |deprecated|
|enriched_text.keywords.relevance                                |enriched_text.keywords.relevance|
|enriched_text.keywords.sentiment.mixed                          |deprecated|
|enriched_text.keywords.sentiment.score                          |enriched_text.keywords.sentiment.score|
|enriched_text.keywords.sentiment.type                          |deprecated|
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
|enriched_text.relations.location.entities.disambiguated.census    |deprecated|
|enriched_text.relations.location.entities.disambiguated.ciaFactbook    |deprecated|
|enriched_text.relations.location.entities.disambiguated.crunchbase    |deprecated|
|enriched_text.relations.location.entities.disambiguated.dbpedia    |deprecated|
|enriched_text.relations.location.entities.disambiguated.freebase    |deprecated|
|enriched_text.relations.location.entities.disambiguated.geonames    |deprecated|
|enriched_text.relations.location.entities.disambiguated.musicBrainz    |deprecated|
|enriched_text.relations.location.entities.disambiguated.name    |deprecated|
|enriched_text.relations.location.entities.disambiguated.opencyc    |deprecated|
|enriched_text.relations.location.entities.disambiguated.subType    |deprecated|
|enriched_text.relations.location.entities.disambiguated.umbel    |deprecated|
|enriched_text.relations.location.entities.disambiguated.website    |deprecated|
|enriched_text.relations.location.entities.disambiguated.yago    |deprecated|
|enriched_text.relations.location.entities.knowledgeGraph.typeHierarchy    |deprecated|
|enriched_text.relations.location.entities.sentiment.score    |deprecated|
|enriched_text.relations.location.entities.sentiment.type    |deprecated|
|enriched_text.relations.location.entities.text                  |deprecated|
|enriched_text.relations.location.entities.type                  |deprecated|
|enriched_text.relations.location.keywords                      |deprecated|
|enriched_text.relations.location.keywords.text                  |deprecated|
|enriched_text.relations.location.sentiment.score                |deprecated|
|enriched_text.relations.location.sentiment.type                |deprecated|
|enriched_text.relations.location.text                          |deprecated|
|enriched_text.relations.object.entities                        |enriched_text.semantic_roles.object.entities|
|enriched_text.relations.object.entities.disambiguated.census    |deprecated|
|enriched_text.relations.object.entities.disambiguated.ciaFactbook    |deprecated|
|enriched_text.relations.object.entities.disambiguated.crunchbase    |deprecated|
|enriched_text.relations.object.entities.disambiguated.dbpedia    |enriched_text.semantic_roles.object.entities.disambiguation.dbpedia_resource|
|enriched_text.relations.object.entities.disambiguated.freebase    |deprecated|
|enriched_text.relations.object.entities.disambiguated.geonames    |deprecated|
|enriched_text.relations.object.entities.disambiguated.musicBrainz    |deprecated|
|enriched_text.relations.object.entities.disambiguated.name    |enriched_text.semantic_roles.object.entities.disambiguation.name|
|enriched_text.relations.object.entities.disambiguated.opencyc    |deprecated|
|enriched_text.relations.object.entities.disambiguated.subType    |enriched_text.semantic_roles.object.entities.disambiguation.subtype|
|enriched_text.relations.object.entities.disambiguated.umbel    |deprecated|
|enriched_text.relations.object.entities.disambiguated.website    |deprecated|
|enriched_text.relations.object.entities.disambiguated.yago    |deprecated|
|enriched_text.relations.object.entities.knowledgeGraph.typeHierarchy    |deprecated|
|enriched_text.relations.object.entities.sentiment.score    |deprecated|
|enriched_text.relations.object.entities.sentiment.type    |deprecated|
|enriched_text.relations.object.entities.text       |enriched_text.semantic_roles.object.entities.text|
|enriched_text.relations.object.entities.type    |enriched_text.semantic_roles.object.entities.type|
|enriched_text.relations.object.keywords    |enriched_text.semantic_roles.object.keywords|
|enriched_text.relations.object.keywords.knowledgeGraph.typeHierarchy    |deprecated|
|enriched_text.relations.object.keywords.text    |enriched_text.semantic_roles.object.keywords.text|
|enriched_text.relations.object.sentiment.score    |deprecated|
|enriched_text.relations.object.sentiment.type    |deprecated|
|enriched_text.relations.object.sentimentFromSubject.score    |deprecated|
|enriched_text.relations.object.sentimentFromSubject.type    |deprecated|
|enriched_text.relations.object.text    |enriched_text.semantic_roles.object.text|
|enriched_text.relations.sentence    |enriched_text.semantic_roles.sentence|
|enriched_text.relations.subject.entities    |enriched_text.semantic_roles.subject.entities|
|enriched_text.relations.subject.entities.disambiguated.census    |deprecated|
|enriched_text.relations.subject.entities.disambiguated.ciaFactbook    |deprecated|
|enriched_text.relations.subject.entities.disambiguated.crunchbase    |deprecated|
|enriched_text.relations.subject.entities.disambiguated.dbpedia    |enriched_text.semantic_roles.subject.entities.disambiguation.dbpedia_resource|
|enriched_text.relations.subject.entities.disambiguated.freebase    |deprecated|
|enriched_text.relations.subject.entities.disambiguated.geonames    |deprecated|
|enriched_text.relations.subject.entities.disambiguated.musicBrainz    |deprecated|
|enriched_text.relations.subject.entities.disambiguated.name    |enriched_text.semantic_roles.subject.entities.disambiguation.name|
|enriched_text.relations.subject.entities.disambiguated.opencyc    |deprecated|
|enriched_text.relations.subject.entities.disambiguated.subType    |enriched_text.semantic_roles.subject.entities.disambiguation.subtype|
|enriched_text.relations.subject.entities.disambiguated.umbel    |deprecated|
|enriched_text.relations.subject.entities.disambiguated.website    |deprecated|
|enriched_text.relations.subject.entities.disambiguated.yago    |deprecated|
|enriched_text.relations.subject.entities.knowledgeGraph.typeHierarchy    |deprecated|
|enriched_text.relations.subject.entities.sentiment.score    |deprecated|
|enriched_text.relations.subject.entities.sentiment.type    |deprecated|
|enriched_text.relations.subject.entities.text    |enriched_text.semantic_roles.subject.entities.text|
|enriched_text.relations.subject.entities.type    |enriched_text.semantic_roles.subject.entities.type|
|enriched_text.relations.subject.keywords    |enriched_text.semantic_roles.subject.keywords|
|enriched_text.relations.subject.keywords.knowledgeGraph.typeHierarchy    |deprecated|
|enriched_text.relations.subject.keywords.text    |enriched_text.semantic_roles.subject.keywords.text|
|enriched_text.relations.subject.sentiment.score    |deprecated|
|enriched_text.relations.subject.sentiment.type    |deprecated|
|enriched_text.relations.subject.text    |enriched_text.semantic_roles.subject.text|
|enriched_text.taxonomy    |enriched_text.categories|
|enriched_text.taxonomy.confident    |deprecated|
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
