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

# Aufbereitungen auf Natural Language Understanding (NLU) migrieren
{: #migrate-nlu}

Am **18. Juli 2017** wurde für {{site.data.keyword.discoveryfull}} eine neue Aufbereitungstechnologie namens {{site.data.keyword.nlushort}} (NLU) eingeführt. {{site.data.keyword.alchemylanguageshort}}-Aufbereitungen werden seit dem **1. März 2018** nicht weiter unterstützt.
{: shortdesc}

Alle vorhandenen Sammlungen, die {{site.data.keyword.alchemylanguageshort}}-Aufbereitungen verwenden, müssen migriert werden. Informationen zum Migrieren von Sammlungen und Konfigurationsdateien, die die {{site.data.keyword.alchemylanguageshort}}-Aufbereitungen verwenden, finden Sie unter [Vergleich von Aufbereitungen](/docs/services/discovery/migrate-nlu.html#enrichment-comparison).

**Hinweis:** Informationen zur Integration mit {{site.data.keyword.knowledgestudioshort}} finden Sie unter [Integration mit {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery/integrate-wks.html).

## Vergleich von Aufbereitungen
{: #enrichment-comparison}

In {{site.data.keyword.alchemylanguageshort}} und {{site.data.keyword.nlushort}} sind die folgenden sieben Aufbereitungen mit den nachstehenden JSON-Objektnamen verfügbar:

| Name der {{site.data.keyword.alchemylanguageshort}}-Aufbereitung         | {{site.data.keyword.alchemylanguageshort}}-JSON-Objekt            | Name der NLU-Aufbereitung                     | NLU-JSON-Objekt        |
|---------------------------|----------------------------------------|----------------------------------------|--------------------------------|
| Entitätsextraktion                     | entities                        |Entitätsextraktion                           |   entities            |
| Schlüsselwortextraktion                    | keywords                        |Schlüsselwortextraktion                          |   keywords            |
| Taxonomieklassifizierung               | taxonomy                        |Kategorieklassifizierung*                    |   categories*         |
| Konzepttagging                       | concepts                        |Konzepttagging                             |   concepts            |
| Stimmungsanalyse                    | docSentiment                    |Stimmungsanalyse                          |   sentiment*          |
| Emotionsanalyse                      | docEmotions                     |Emotionsanalyse                            |   emotion*            |
| Beziehungsextraktion                   | relations                       |Semantikrollenextraktion*                   |   semantic_roles*     |
 \* Namensänderung

Zusätzliche Angaben über {{site.data.keyword.nlushort}}-Aufbereitungen enthält der Abschnitt [Aufbereitungen hinzufügen](/docs/services/discovery/building.html#adding-enrichments).

## Wichtigste Änderungen im Überblick

- Das JSON-Schema für {{site.data.keyword.nlushort}}-Aufbereitungen unterscheidet sich von dem bei den {{site.data.keyword.alchemylanguageshort}}-Aufbereitungen verwendet Schema. Eine vollständige Liste der Änderungen an den einzelnen Aufbereitungen finden Sie unter [Unterschiede beim Aufbereitungsschema](/docs/services/discovery/migrate-nlu.html#enrichment-schema-differences).
- Die Aufbereitung für die _Taxonomieklassifizierung_ ({{site.data.keyword.alchemylanguageshort}}) heißt jetzt _Kategorieklassifizierung_. Ihr JSON-Objektname wurde von `taxonomy` in `categories` geändert.
- Die Aufbereitung für die _Beziehungsextrakion_ ({{site.data.keyword.alchemylanguageshort}}) heißt jetzt _Semantikrollenextraktion_. Ihr JSON-Objektname wurde von `relations` in `semantic_roles` geändert.
- Der JSON-Objektname für die _Stimmungsanalyse_ wurde von `docSentiment` in `sentiment` geändert.
- Der JSON-Objektname für die _Emotionsanalyse_ wurde von `docEmotions` in `emotion` geändert.

## Konfigurationsdateiänderungen

Die **{{site.data.keyword.alchemylanguageshort}}**-Standardkonfigurationsdatei (in den Tools `Standardkonfiguration` genannt) wendete die folgenden Aufbereitungen auf das Textfeld Ihrer Dokumente an: **Entitätsextraktion**, **Schlüsselwortextraktion**, **Taxonomieklassifizierung**, **Konzepttagging**, **Beziehungsextraktion** und **Stimmungsanalyse**. Die Datei beinhaltet auch Standarddokumentkonvertierungen, die auf Schriftstilen und -größen basieren.

Die **{{site.data.keyword.nlushort}}**-Standardkonfigurationsdatei heißt `Standardkonfiguration mit NLU` und hat die folgenden Aufbereitungen auf das Textfeld Ihrer Dokumente angewendet: **Entitätsextraktion**, **Stimmungsanalyse**, **Kategorieklassifizierung** und **Konzepttagging**. Die Datei beinhaltet auch Standarddokumentkonvertierungen, die auf Schriftstilen und -größen basieren. Diese Dokumentkonvertierungen sind mit denen in der {{site.data.keyword.alchemylanguageshort}}-Standardkonfigurationsdatei identisch.

## Konfigurationen, Sammlungen und Abfragen migrieren

Falls Sie angepasste Konfigurationen erstellt haben, müssen Sie neue Konfigurationen erstellen, die die {{site.data.keyword.nlushort}}-Aufbereitungen verwenden. Entsprechende Anweisungen enthalten die folgenden Dokumente:

- [Tools](/docs/services/discovery/building.html#custom-configuration)
- [API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#add_configuration){: new_window}

Falls Sammlungen vorhanden sind, auf die entweder die {{site.data.keyword.alchemylanguageshort}}-Standardkonfiguration oder eine angepasste {{site.data.keyword.alchemylanguageshort}}-Konfiguration angewendet werden, müssen Sie eine neue Sammlung erstellen, die {{site.data.keyword.nlushort}}-Konfigurationsdatei (entweder die Standardkonfiguration oder eine neue angepasste Konfiguration) anwenden und Ihre Dokumente hochladen. Entsprechende Anweisungen enthalten die folgenden Dokumente:

- [Tools](/docs/services/discovery/building.html#preparing-the-service-for-your-documents)
- [API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#create-collection){: new_window}

Für alle Abfragen, die Sie unter Verwendung der Discovery-Abfragesprache erstellt haben, müssen Sie die Änderungen des JSON-Schemas zwischen {{site.data.keyword.alchemylanguageshort}} und {{site.data.keyword.nlushort}} untersuchen und Ihre Abfragen sowie Abfrage-URLs entsprechend ändern. Details können Sie dem Abschnitt [Unterschiede beim Aufbereitungsschema](/docs/services/discovery/migrate-nlu.html#enrichment-schema-differences) entnehmen.

## Unterschiede beim Aufbereitungsschema

Die folgende Tabelle zeigt die Unterschiede beim JSON-Schema für {{site.data.keyword.nlushort}}-Aufbereitungen und {{site.data.keyword.alchemylanguageshort}}-Aufbereitungen.

| {{site.data.keyword.alchemylanguageshort}}                         | {{site.data.keyword.nlushort}}       |
|-----------------------------------------|--------------------------------------|
|enriched_text.concepts                      |enriched_text.concepts|
|enriched_text.concepts.census              |veraltet|
|enriched_text.concepts.ciaFactbook          |veraltet|
|enriched_text.concepts.crunchbase                              |veraltet|
|enriched_text.concepts.dbpedia                               |enriched_text.concepts.dbpedia_resource|
|enriched_text.concepts.freebase                              |veraltet|
|enriched_text.concepts.geonames                                |veraltet|
|enriched_text.concepts.knowledgeGraph.typeHierarchy            |veraltet|
|enriched_text.concepts.musicBrainz                              |veraltet|
|enriched_text.concepts.opencyc                                  |veraltet|
|enriched_text.concepts.relevance                                |enriched_text.concepts.relevance|
|enriched_text.concepts.text                                    |enriched_text.concepts.text|
|enriched_text.concepts.website                                  |veraltet|
|enriched_text.concepts.yago                                    |veraltet|
|enriched_text.docSentiment.mixed                                |veraltet|
|enriched_text.docSentiment.score                                |enriched_text.sentiment.document.score|
|enriched_text.docSentiment.type                                |enriched_text.sentiment.document.label|
|enriched_text.entities                                          |enriched_text.entities|
|enriched_text.entities.count                                    |enriched_text.entities.count|
|enriched_text.entities.disambiguated.census                    |veraltet|
|enriched_text.entities.disambiguated.ciaFactbook                |veraltet|
|enriched_text.entities.disambiguated.crunchbase                |veraltet|
|enriched_text.entities.disambiguated.dbpedia                    |enriched_text.entities.disambiguation.dbpedia_resource|
|enriched_text.entities.disambiguated.freebase                  |veraltet|
|enriched_text.entities.disambiguated.geonames                  |veraltet|
|enriched_text.entities.disambiguated.musicBrainz                |veraltet|
|enriched_text.entities.disambiguated.name                      |enriched_text.entities.disambiguation.name|
|enriched_text.entities.disambiguated.opencyc                    |veraltet|
|enriched_text.entities.disambiguated.subType                    |enriched_text.entities.disambiguation.subtype|
|enriched_text.entities.disambiguated.umbel                      |veraltet|
|enriched_text.entities.disambiguated.website                    |veraltet|
|enriched_text.entities.disambiguated.yago                      |veraltet|
|enriched_text.entities.knowledgeGraph.typeHierarchy            |veraltet|
|enriched_text.entities.quotations                              |veraltet|
|enriched_text.entities.quotations.quotation                    |veraltet|
|enriched_text.entities.quotations.sentiment.mixed              |veraltet|
|enriched_text.entities.quotations.sentiment.score              |veraltet|
|enriched_text.entities.quotations.sentiment.type                |veraltet|
|enriched_text.entities.relevance                                |enriched_text.entities.relevance|
|enriched_text.entities.sentiment.mixed                          |veraltet|
|enriched_text.entities.sentiment.score                          |enriched_text.entities.sentiment.score|
|enriched_text.entities.sentiment.type                          |veraltet|
|enriched_text.entities.text                                    |enriched_text.entities.text|
|enriched_text.entities.type                                    |enriched_text.entities.type|
|enriched_text.keywords                                          |enriched_text.keywords|
|enriched_text.keywords.knowledgeGraph.typeHierarchy            |veraltet|
|enriched_text.keywords.relevance                                |enriched_text.keywords.relevance|
|enriched_text.keywords.sentiment.mixed                          |veraltet|
|enriched_text.keywords.sentiment.score                          |enriched_text.keywords.sentiment.score|
|enriched_text.keywords.sentiment.type                          |veraltet|
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
|enriched_text.relations.location.entities.disambiguated.census    |veraltet|
|enriched_text.relations.location.entities.disambiguated.ciaFactbook    |veraltet|
|enriched_text.relations.location.entities.disambiguated.crunchbase    |veraltet|
|enriched_text.relations.location.entities.disambiguated.dbpedia    |veraltet|
|enriched_text.relations.location.entities.disambiguated.freebase    |veraltet|
|enriched_text.relations.location.entities.disambiguated.geonames    |veraltet|
|enriched_text.relations.location.entities.disambiguated.musicBrainz    |veraltet|
|enriched_text.relations.location.entities.disambiguated.name    |veraltet|
|enriched_text.relations.location.entities.disambiguated.opencyc    |veraltet|
|enriched_text.relations.location.entities.disambiguated.subType    |veraltet|
|enriched_text.relations.location.entities.disambiguated.umbel    |veraltet|
|enriched_text.relations.location.entities.disambiguated.website    |veraltet|
|enriched_text.relations.location.entities.disambiguated.yago    |veraltet|
|enriched_text.relations.location.entities.knowledgeGraph.typeHierarchy    |veraltet|
|enriched_text.relations.location.entities.sentiment.score    |veraltet|
|enriched_text.relations.location.entities.sentiment.type    |veraltet|
|enriched_text.relations.location.entities.text                  |veraltet|
|enriched_text.relations.location.entities.type                  |veraltet|
|enriched_text.relations.location.keywords                      |veraltet|
|enriched_text.relations.location.keywords.text                  |veraltet|
|enriched_text.relations.location.sentiment.score                |veraltet|
|enriched_text.relations.location.sentiment.type                |veraltet|
|enriched_text.relations.location.text                          |veraltet|
|enriched_text.relations.object.entities                        |enriched_text.semantic_roles.object.entities|
|enriched_text.relations.object.entities.disambiguated.census    |veraltet|
|enriched_text.relations.object.entities.disambiguated.ciaFactbook    |veraltet|
|enriched_text.relations.object.entities.disambiguated.crunchbase    |veraltet|
|enriched_text.relations.object.entities.disambiguated.dbpedia    |enriched_text.semantic_roles.object.entities.disambiguation.dbpedia_resource|
|enriched_text.relations.object.entities.disambiguated.freebase    |veraltet|
|enriched_text.relations.object.entities.disambiguated.geonames    |veraltet|
|enriched_text.relations.object.entities.disambiguated.musicBrainz    |veraltet|
|enriched_text.relations.object.entities.disambiguated.name    |enriched_text.semantic_roles.object.entities.disambiguation.name|
|enriched_text.relations.object.entities.disambiguated.opencyc    |veraltet|
|enriched_text.relations.object.entities.disambiguated.subType    |enriched_text.semantic_roles.object.entities.disambiguation.subtype|
|enriched_text.relations.object.entities.disambiguated.umbel    |veraltet|
|enriched_text.relations.object.entities.disambiguated.website    |veraltet|
|enriched_text.relations.object.entities.disambiguated.yago    |veraltet|
|enriched_text.relations.object.entities.knowledgeGraph.typeHierarchy    |veraltet|
|enriched_text.relations.object.entities.sentiment.score    |veraltet|
|enriched_text.relations.object.entities.sentiment.type    |veraltet|
|enriched_text.relations.object.entities.text       |enriched_text.semantic_roles.object.entities.text|
|enriched_text.relations.object.entities.type    |enriched_text.semantic_roles.object.entities.type|
|enriched_text.relations.object.keywords    |enriched_text.semantic_roles.object.keywords|
|enriched_text.relations.object.keywords.knowledgeGraph.typeHierarchy    |veraltet|
|enriched_text.relations.object.keywords.text    |enriched_text.semantic_roles.object.keywords.text|
|enriched_text.relations.object.sentiment.score    |veraltet|
|enriched_text.relations.object.sentiment.type    |veraltet|
|enriched_text.relations.object.sentimentFromSubject.score    |veraltet|
|enriched_text.relations.object.sentimentFromSubject.type    |veraltet|
|enriched_text.relations.object.text    |enriched_text.semantic_roles.object.text|
|enriched_text.relations.sentence    |enriched_text.semantic_roles.sentence|
|enriched_text.relations.subject.entities    |enriched_text.semantic_roles.subject.entities|
|enriched_text.relations.subject.entities.disambiguated.census    |veraltet|
|enriched_text.relations.subject.entities.disambiguated.ciaFactbook    |veraltet|
|enriched_text.relations.subject.entities.disambiguated.crunchbase    |veraltet|
|enriched_text.relations.subject.entities.disambiguated.dbpedia    |enriched_text.semantic_roles.subject.entities.disambiguation.dbpedia_resource|
|enriched_text.relations.subject.entities.disambiguated.freebase    |veraltet|
|enriched_text.relations.subject.entities.disambiguated.geonames    |veraltet|
|enriched_text.relations.subject.entities.disambiguated.musicBrainz    |veraltet|
|enriched_text.relations.subject.entities.disambiguated.name    |enriched_text.semantic_roles.subject.entities.disambiguation.name|
|enriched_text.relations.subject.entities.disambiguated.opencyc    |veraltet|
|enriched_text.relations.subject.entities.disambiguated.subType    |enriched_text.semantic_roles.subject.entities.disambiguation.subtype|
|enriched_text.relations.subject.entities.disambiguated.umbel    |veraltet|
|enriched_text.relations.subject.entities.disambiguated.website    |veraltet|
|enriched_text.relations.subject.entities.disambiguated.yago    |veraltet|
|enriched_text.relations.subject.entities.knowledgeGraph.typeHierarchy    |veraltet|
|enriched_text.relations.subject.entities.sentiment.score    |veraltet|
|enriched_text.relations.subject.entities.sentiment.type    |veraltet|
|enriched_text.relations.subject.entities.text    |enriched_text.semantic_roles.subject.entities.text|
|enriched_text.relations.subject.entities.type    |enriched_text.semantic_roles.subject.entities.type|
|enriched_text.relations.subject.keywords    |enriched_text.semantic_roles.subject.keywords|
|enriched_text.relations.subject.keywords.knowledgeGraph.typeHierarchy    |veraltet|
|enriched_text.relations.subject.keywords.text    |enriched_text.semantic_roles.subject.keywords.text|
|enriched_text.relations.subject.sentiment.score    |veraltet|
|enriched_text.relations.subject.sentiment.type    |veraltet|
|enriched_text.relations.subject.text    |enriched_text.semantic_roles.subject.text|
|enriched_text.taxonomy    |enriched_text.categories|
|enriched_text.taxonomy.confident    |veraltet|
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
