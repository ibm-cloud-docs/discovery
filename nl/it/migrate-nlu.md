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

# Migrazione degli arricchimenti a Natural Language Understanding
{: #migrate-nlu}

A partire dal **18 luglio 2017** {{site.data.keyword.discoveryfull}} ha introdotto una nuova tecnologia di arricchimento denominata {{site.data.keyword.nlushort}} (NLU). Gli arricchimenti {{site.data.keyword.alchemylanguageshort}} sono da considerare obsoleti a partire dal **1° marzo 2018**. 
{: shortdesc}

Qualsiasi raccolta esistente che utilizza gli arricchimenti {{site.data.keyword.alchemylanguageshort}} sarà migrata. Per informazioni sulla migrazione di raccolte e file di configurazione che utilizzano gli arricchimenti {{site.data.keyword.alchemylanguageshort}}, vedi [Confronto degli arricchimenti](/docs/services/discovery?topic=discovery-migrate-nlu#enrichment-comparison).

**Nota:** per informazioni sull'integrazione con {{site.data.keyword.knowledgestudioshort}}, vedi [Integrazione con {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-with-wks).

## Confronto degli arricchimenti
{: #enrichment-comparison}

I sette arricchimenti disponibili in {{site.data.keyword.alchemylanguageshort}} e {{site.data.keyword.nlushort}}, insieme ai loro nomi oggetto JSON, sono:

| Nome dell'arricchimento {{site.data.keyword.alchemylanguageshort}}         | Oggetto JSON {{site.data.keyword.alchemylanguageshort}}            | Nome dell'arricchimento NLU                     | Oggetto JSON NLU        |
|---------------------------|----------------------------------------|----------------------------------------|--------------------------------|
| Entity Extraction                     | entities                        |Entity Extraction                           |   entities            |
| Keyword Extraction                    | keywords                        |Keyword Extraction                          |   keywords            |
| Taxonomy Classification               | taxonomy                        |Category Classification*                    |   categories*         |
| Concept Tagging                       | concepts                        |Concept Tagging                             |   concepts            |
| Sentiment Analysis                    | docSentiment                    |Sentiment Analysis                          |   sentiment*          |
| Emotion Analysis                      | docEmotions                     |Emotion Analysis                            |   emotion*            |
| Relation Extraction                   | relations                       |Semantic Role Extraction*                   |   semantic_roles*     |
 \* Modifica del nome

Per ulteriori informazioni sugli arricchimenti {{site.data.keyword.nlushort}}, vedi [Aggiunta di arricchimenti](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)

## Panoramica delle principali modifiche
{: #overview-nlu}

- Lo schema JSON (per gli arricchimenti {{site.data.keyword.nlushort}} differisce da quello utilizzato negli arricchimenti {{site.data.keyword.alchemylanguageshort}}; per un elenco completo di tutte le modifiche a ciascun arricchimento, vedi [Differenze dello schema degli arricchimenti](/docs/services/discovery?topic=discovery-migrate-nlu#enrichment-schema-differences).
- L'arricchimento _Taxonomy Classification_ ({{site.data.keyword.alchemylanguageshort}}) è ora denominato _Category Classification_. Il suo nome oggetto JSON è stato modificato da `taxonomy` a `categories`.
- L'arricchimento _Relation Extraction_ ({{site.data.keyword.alchemylanguageshort}}) è ora denominato _Semantic Role Extraction_. Il suo nome oggetto JSON è stato modificato da `relations` a `semantic_roles`.
- Il nome oggetto JSON per _Sentiment Analysis_ è stato modificato da `docSentiment` a `sentiment`.
- Il nome oggetto JSON per _Emotion Analysis_ è stato modificato da `docEmotions` a `emotion`.

## Modifiche del file di configurazione
{: #config-nlu}

Il file di configurazione predefinito di **{{site.data.keyword.alchemylanguageshort}}** (denominato `Default configuration` nella strumentazione) ha applicato i seguenti arricchimenti al campo di testo dei tuoi documenti: **Entity Extraction**, **Keyword Extraction**, **Taxonomy Classification**, **Concept Tagging**, **Relation Extraction** e **Sentiment Analysis**. Il file include anche delle conversioni di documento standard basate su stili e dimensioni del carattere.

Il file di configurazione predefinito di **{{site.data.keyword.nlushort}}** è denominato `Default Configuration with NLU` e ha applicato i seguenti arricchimenti al campo di testo dei tuoi documenti **Entity Extraction**, **Sentiment Analysis**, **Category Classification** e **Concept Tagging**. Il file include anche delle conversioni di documento standard basate su stili e dimensioni del carattere. Queste conversioni di documenti sono identiche a quelle nel file di configurazione predefinito di {{site.data.keyword.alchemylanguageshort}}.

## Migrazione delle tue configurazioni, raccolte e query
{: #migrateconfig-nlu}

Se hai creato qualche configurazione personalizzata, devi crearne di nuove per utilizzare gli arricchimenti {{site.data.keyword.nlushort}}. Per le istruzioni, consulta questi documenti:

- [Strumentazione](/docs/services/discovery?topic=discovery-configservice#custom-configuration)
- [API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery#add-configuration){: new_window}

Se hai delle raccolte esistenti con applicate la configurazione predefinita {{site.data.keyword.alchemylanguageshort}} oppure una configurazione {{site.data.keyword.alchemylanguageshort}} personalizzata, devi creare una nuova raccolta, applicare il file di configurazione di {{site.data.keyword.nlushort}} (la configurazione predefinita oppure una nuova configurazione personalizzata) e caricare i tuoi documenti. Per le istruzioni, consulta questi documenti:

- [Strumentazione](/docs/services/discovery?topic=discovery-configservice#preparing-the-service-for-your-documents)
- [API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery#create-a-collection){: new_window}

Per eventuali query che hai creato utilizzando Discovery Query Language, devi esaminare le modifiche dello schema JSON tra {{site.data.keyword.alchemylanguageshort}} e {{site.data.keyword.nlushort}} e aggiornare le tue query e i tuoi URL query di conseguenza. Vedi [Differenze dello schema degli arricchimenti](/docs/services/discovery?topic=discovery-migrate-nlu#enrichment-schema-differences) per i dettagli.

## Differenze dello schema degli arricchimenti
{: #enrichment-schema-differences}

La seguente tabella mostra le differenze tra lo schema JSON per gli arricchimenti {{site.data.keyword.nlushort}} e gli arricchimenti {{site.data.keyword.alchemylanguageshort}}.

| {{site.data.keyword.alchemylanguageshort}}                         | {{site.data.keyword.nlushort}}       |
|-----------------------------------------|--------------------------------------|
|enriched_text.concepts                      |enriched_text.concepts|
|enriched_text.concepts.census              |obsoleto|
|enriched_text.concepts.ciaFactbook          |obsoleto|
|enriched_text.concepts.crunchbase                              |obsoleto|
|enriched_text.concepts.dbpedia                               |enriched_text.concepts.dbpedia_resource|
|enriched_text.concepts.freebase                              |obsoleto|
|enriched_text.concepts.geonames                                |obsoleto|
|enriched_text.concepts.knowledgeGraph.typeHierarchy            |obsoleto|
|enriched_text.concepts.musicBrainz                              |obsoleto|
|enriched_text.concepts.opencyc                                  |obsoleto|
|enriched_text.concepts.relevance                                |enriched_text.concepts.relevance|
|enriched_text.concepts.text                                    |enriched_text.concepts.text|
|enriched_text.concepts.website                                  |obsoleto|
|enriched_text.concepts.yago                                    |obsoleto|
|enriched_text.docSentiment.mixed                                |obsoleto|
|enriched_text.docSentiment.score                                |enriched_text.sentiment.document.score|
|enriched_text.docSentiment.type                                |enriched_text.sentiment.document.label|
|enriched_text.entities                                          |enriched_text.entities|
|enriched_text.entities.count                                    |enriched_text.entities.count|
|enriched_text.entities.disambiguated.census                    |obsoleto|
|enriched_text.entities.disambiguated.ciaFactbook                |obsoleto|
|enriched_text.entities.disambiguated.crunchbase                |obsoleto|
|enriched_text.entities.disambiguated.dbpedia                    |enriched_text.entities.disambiguation.dbpedia_resource|
|enriched_text.entities.disambiguated.freebase                  |obsoleto|
|enriched_text.entities.disambiguated.geonames                  |obsoleto|
|enriched_text.entities.disambiguated.musicBrainz                |obsoleto|
|enriched_text.entities.disambiguated.name                      |enriched_text.entities.disambiguation.name|
|enriched_text.entities.disambiguated.opencyc                    |obsoleto|
|enriched_text.entities.disambiguated.subType                    |enriched_text.entities.disambiguation.subtype|
|enriched_text.entities.disambiguated.umbel                      |obsoleto|
|enriched_text.entities.disambiguated.website                    |obsoleto|
|enriched_text.entities.disambiguated.yago                      |obsoleto|
|enriched_text.entities.knowledgeGraph.typeHierarchy            |obsoleto|
|enriched_text.entities.quotations                              |obsoleto|
|enriched_text.entities.quotations.quotation                    |obsoleto|
|enriched_text.entities.quotations.sentiment.mixed              |obsoleto|
|enriched_text.entities.quotations.sentiment.score              |obsoleto|
|enriched_text.entities.quotations.sentiment.type                |obsoleto|
|enriched_text.entities.relevance                                |enriched_text.entities.relevance|
|enriched_text.entities.sentiment.mixed                          |obsoleto|
|enriched_text.entities.sentiment.score                          |enriched_text.entities.sentiment.score|
|enriched_text.entities.sentiment.type                          |obsoleto|
|enriched_text.entities.text                                    |enriched_text.entities.text|
|enriched_text.entities.type                                    |enriched_text.entities.type|
|enriched_text.keywords                                          |enriched_text.keywords|
|enriched_text.keywords.knowledgeGraph.typeHierarchy            |obsoleto|
|enriched_text.keywords.relevance                                |enriched_text.keywords.relevance|
|enriched_text.keywords.sentiment.mixed                          |obsoleto|
|enriched_text.keywords.sentiment.score                          |enriched_text.keywords.sentiment.score|
|enriched_text.keywords.sentiment.type                          |obsoleto|
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
|enriched_text.relations.location.entities.disambiguated.census    |obsoleto|
|enriched_text.relations.location.entities.disambiguated.ciaFactbook    |obsoleto|
|enriched_text.relations.location.entities.disambiguated.crunchbase    |obsoleto|
|enriched_text.relations.location.entities.disambiguated.dbpedia    |obsoleto|
|enriched_text.relations.location.entities.disambiguated.freebase    |obsoleto|
|enriched_text.relations.location.entities.disambiguated.geonames    |obsoleto|
|enriched_text.relations.location.entities.disambiguated.musicBrainz    |obsoleto|
|enriched_text.relations.location.entities.disambiguated.name    |obsoleto|
|enriched_text.relations.location.entities.disambiguated.opencyc    |obsoleto|
|enriched_text.relations.location.entities.disambiguated.subType    |obsoleto|
|enriched_text.relations.location.entities.disambiguated.umbel    |obsoleto|
|enriched_text.relations.location.entities.disambiguated.website    |obsoleto|
|enriched_text.relations.location.entities.disambiguated.yago    |obsoleto|
|enriched_text.relations.location.entities.knowledgeGraph.typeHierarchy    |obsoleto|
|enriched_text.relations.location.entities.sentiment.score    |obsoleto|
|enriched_text.relations.location.entities.sentiment.type    |obsoleto|
|enriched_text.relations.location.entities.text                  |obsoleto|
|enriched_text.relations.location.entities.type                  |obsoleto|
|enriched_text.relations.location.keywords                      |obsoleto|
|enriched_text.relations.location.keywords.text                  |obsoleto|
|enriched_text.relations.location.sentiment.score                |obsoleto|
|enriched_text.relations.location.sentiment.type                |obsoleto|
|enriched_text.relations.location.text                          |obsoleto|
|enriched_text.relations.object.entities                        |enriched_text.semantic_roles.object.entities|
|enriched_text.relations.object.entities.disambiguated.census    |obsoleto|
|enriched_text.relations.object.entities.disambiguated.ciaFactbook    |obsoleto|
|enriched_text.relations.object.entities.disambiguated.crunchbase    |obsoleto|
|enriched_text.relations.object.entities.disambiguated.dbpedia    |enriched_text.semantic_roles.object.entities.disambiguation.dbpedia_resource|
|enriched_text.relations.object.entities.disambiguated.freebase    |obsoleto|
|enriched_text.relations.object.entities.disambiguated.geonames    |obsoleto|
|enriched_text.relations.object.entities.disambiguated.musicBrainz    |obsoleto|
|enriched_text.relations.object.entities.disambiguated.name    |enriched_text.semantic_roles.object.entities.disambiguation.name|
|enriched_text.relations.object.entities.disambiguated.opencyc    |obsoleto|
|enriched_text.relations.object.entities.disambiguated.subType    |enriched_text.semantic_roles.object.entities.disambiguation.subtype|
|enriched_text.relations.object.entities.disambiguated.umbel    |obsoleto|
|enriched_text.relations.object.entities.disambiguated.website    |obsoleto|
|enriched_text.relations.object.entities.disambiguated.yago    |obsoleto|
|enriched_text.relations.object.entities.knowledgeGraph.typeHierarchy    |obsoleto|
|enriched_text.relations.object.entities.sentiment.score    |obsoleto|
|enriched_text.relations.object.entities.sentiment.type    |obsoleto|
|enriched_text.relations.object.entities.text       |enriched_text.semantic_roles.object.entities.text|
|enriched_text.relations.object.entities.type    |enriched_text.semantic_roles.object.entities.type|
|enriched_text.relations.object.keywords    |enriched_text.semantic_roles.object.keywords|
|enriched_text.relations.object.keywords.knowledgeGraph.typeHierarchy    |obsoleto|
|enriched_text.relations.object.keywords.text    |enriched_text.semantic_roles.object.keywords.text|
|enriched_text.relations.object.sentiment.score    |obsoleto|
|enriched_text.relations.object.sentiment.type    |obsoleto|
|enriched_text.relations.object.sentimentFromSubject.score    |obsoleto|
|enriched_text.relations.object.sentimentFromSubject.type    |obsoleto|
|enriched_text.relations.object.text    |enriched_text.semantic_roles.object.text|
|enriched_text.relations.sentence    |enriched_text.semantic_roles.sentence|
|enriched_text.relations.subject.entities    |enriched_text.semantic_roles.subject.entities|
|enriched_text.relations.subject.entities.disambiguated.census    |obsoleto|
|enriched_text.relations.subject.entities.disambiguated.ciaFactbook    |obsoleto|
|enriched_text.relations.subject.entities.disambiguated.crunchbase    |obsoleto|
|enriched_text.relations.subject.entities.disambiguated.dbpedia    |enriched_text.semantic_roles.subject.entities.disambiguation.dbpedia_resource|
|enriched_text.relations.subject.entities.disambiguated.freebase    |obsoleto|
|enriched_text.relations.subject.entities.disambiguated.geonames    |obsoleto|
|enriched_text.relations.subject.entities.disambiguated.musicBrainz    |obsoleto|
|enriched_text.relations.subject.entities.disambiguated.name    |enriched_text.semantic_roles.subject.entities.disambiguation.name|
|enriched_text.relations.subject.entities.disambiguated.opencyc    |obsoleto|
|enriched_text.relations.subject.entities.disambiguated.subType    |enriched_text.semantic_roles.subject.entities.disambiguation.subtype|
|enriched_text.relations.subject.entities.disambiguated.umbel    |obsoleto|
|enriched_text.relations.subject.entities.disambiguated.website    |obsoleto|
|enriched_text.relations.subject.entities.disambiguated.yago    |obsoleto|
|enriched_text.relations.subject.entities.knowledgeGraph.typeHierarchy    |obsoleto|
|enriched_text.relations.subject.entities.sentiment.score    |obsoleto|
|enriched_text.relations.subject.entities.sentiment.type    |obsoleto|
|enriched_text.relations.subject.entities.text    |enriched_text.semantic_roles.subject.entities.text|
|enriched_text.relations.subject.entities.type    |enriched_text.semantic_roles.subject.entities.type|
|enriched_text.relations.subject.keywords    |enriched_text.semantic_roles.subject.keywords|
|enriched_text.relations.subject.keywords.knowledgeGraph.typeHierarchy    |obsoleto|
|enriched_text.relations.subject.keywords.text    |enriched_text.semantic_roles.subject.keywords.text|
|enriched_text.relations.subject.sentiment.score    |obsoleto|
|enriched_text.relations.subject.sentiment.type    |obsoleto|
|enriched_text.relations.subject.text    |enriched_text.semantic_roles.subject.text|
|enriched_text.taxonomy    |enriched_text.categories|
|enriched_text.taxonomy.confident    |obsoleto|
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
