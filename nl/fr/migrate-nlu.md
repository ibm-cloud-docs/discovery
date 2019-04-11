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

# Migration des enrichissements vers Natural Language Understanding
{: #migrate-nlu}

Le **18 juillet 2017**, {{site.data.keyword.discoveryfull}} a introduit une nouvelle technologie d'enrichissement, nommée {{site.data.keyword.nlushort}} (NLU). Les enrichissements {{site.data.keyword.alchemylanguageshort}} ont été dépréciés à la date du **1er mars 2018**. 
{: shortdesc}

Toute collection existante qui utilise des enrichissements {{site.data.keyword.alchemylanguageshort}} doit être migrée. Pour plus d'informations sur la migration des collections et des fichiers de configuration qui utilisent les enrichissements {{site.data.keyword.alchemylanguageshort}}, voir [Comparaison des enrichissements](/docs/services/discovery?topic=discovery-migrate-nlu#enrichment-comparison).

**Remarque :** pour plus d'informations sur l'intégration à {{site.data.keyword.knowledgestudioshort}}, voir [Intégration à {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-with-wks).

## Comparaison des enrichissements
{: #enrichment-comparison}

Les sept enrichissements disponibles dans {{site.data.keyword.alchemylanguageshort}} et {{site.data.keyword.nlushort}} et leurs noms d'objet JSON sont les suivants :

| Nom d'enrichissement {{site.data.keyword.alchemylanguageshort}}         | Objet JSON {{site.data.keyword.alchemylanguageshort}}            | Nom d'enrichissement NLU                     | Objet JSON NLU        |
|---------------------------|----------------------------------------|----------------------------------------|--------------------------------|
| Entity Extraction                     | entities                        |Entity Extraction                           |   entities            |
| Keyword Extraction                    | keywords                        |Keyword Extraction                          |   keywords            |
| Taxonomy Classification               | taxonomy                        |Category Classification*                    |   categories*         |
| Concept Tagging                       | concepts                        |Concept Tagging                             |   concepts            |
| Sentiment Analysis                    | docSentiment                    |Sentiment Analysis                          |   sentiment*          |
| Emotion Analysis                      | docEmotions                     |Emotion Analysis                            |   emotion*            |
| Relation Extraction                   | relations                       |Semantic Role Extraction*                   |   semantic_roles*     |
 \* Name change

Pour plus d'informations sur les enrichissements {{site.data.keyword.nlushort}}, voir[Ajout d'enrichissements](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)

## Présentation des principales modifications
{: #overview-nlu}

- Le schéma JSON pour les enrichissements {{site.data.keyword.nlushort}} est légèrement différent de celui utilisé dans les enrichissements {{site.data.keyword.alchemylanguageshort}}. Pour obtenir la liste complète des modifications apportées à chaque enrichissement, voir [Différences entre les schémas d'enrichissement](/docs/services/discovery?topic=discovery-migrate-nlu#enrichment-schema-differences).
- L'enrichissement _Taxonomy Classification_ ({{site.data.keyword.alchemylanguageshort}}) s'appelle désormais _Category Classification_. Son nom d'objet JSON, `taxonomy`, a été remplacé par `categories`.
- L'enrichissement _Relation Extraction_ ({{site.data.keyword.alchemylanguageshort}}) s'appelle désormais _Semantic Role Extraction_. Son nom d'objet JSON, `relations`, a été remplacé par `semantic_roles`.
- Le nom d'objet JSON pour _Sentiment Analysis_, `docSentiment`, a été remplacé par `sentiment`.
- Le nom d'objet JSON pour _Emotion Analysis_, `docEmotions`, a été remplacé par `emotion`.

## Modifications apportées au fichier de configuration
{: #config-nlu}

Le fichier de configuration par défaut **{{site.data.keyword.alchemylanguageshort}}** (nommé `Default configuration` dans les outils) appliquait les enrichissements suivants à la zone de texte de vos documents : **Entity Extraction**, **Keyword Extraction**, **Taxonomy Classification**, **Concept Tagging**, **Relation Extraction** et **Sentiment Analysis**. Ce fichier contient également des conversions de document standard basées sur des styles et des tailles de police.

Le fichier de configuration par défaut **{{site.data.keyword.nlushort}}** (nommé `Default Configuration with NLU` dans les outils) a appliqué les enrichissements suivants à la zone de texte de vos documents : **Entity Extraction**, **Sentiment Analysis**, **Category Classification** et **Concept Tagging**. Ce fichier contient également des conversions de document standard basées sur des styles et des tailles de police. Ces conversions de document sont identiques à celles utilisées dans le fichier de configuration par défaut {{site.data.keyword.alchemylanguageshort}}.

## Migration de vos configurations, collections et requêtes
{: #migrateconfig-nlu}

Si vous avez créé des configurations personnalisées, vous devez en créer de nouvelles qui utilisent les enrichissements {{site.data.keyword.nlushort}}. Pour obtenir des instructions, voir les documents suivants :

- [Outils](/docs/services/discovery?topic=discovery-configservice#custom-configuration)
- [API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#add-configuration){: new_window}

Si la configuration par défaut {{site.data.keyword.alchemylanguageshort}} ou une configuration {{site.data.keyword.alchemylanguageshort}} personnalisée est appliquée à vos collections, appliquez le fichier de configuration {{site.data.keyword.nlushort}} (soit la configuration par défaut, soit une nouvelle configuration personnalisée) et téléchargez vos documents. Pour obtenir des instructions, voir les documents suivants :

- [Outils](/docs/services/discovery?topic=discovery-configservice#preparing-the-service-for-your-documents)
- [API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#create-a-collection){: new_window}

Pour les requêtes que vous avez créées à l'aide du langage de requête Discovery, vous devez examiner les différences de schéma JSON entre{{site.data.keyword.alchemylanguageshort}} et  {{site.data.keyword.nlushort}} et mettre à jour vos requêtes et vos URL de requête en conséquence. Pour plus d'informations, voir [Différences entre les schémas d'enrichissement](/docs/services/discovery?topic=discovery-migrate-nlu#enrichment-schema-differences).

## Différences entre les schémas d'enrichissement
{: #enrichment-schema-differences}

Le tableau suivant présente les différences entre le schéma JSON des enrichissements {{site.data.keyword.nlushort}} et le schéma JSON des enrichissements {{site.data.keyword.alchemylanguageshort}} :

| {{site.data.keyword.alchemylanguageshort}}                         | {{site.data.keyword.nlushort}}       |
|-----------------------------------------|--------------------------------------|
|enriched_text.concepts                      |enriched_text.concepts|
|enriched_text.concepts.census              |obsolète|
|enriched_text.concepts.ciaFactbook          |obsolète|
|enriched_text.concepts.crunchbase                              |obsolète|
|enriched_text.concepts.dbpedia                               |enriched_text.concepts.dbpedia_resource|
|enriched_text.concepts.freebase                              |obsolète|
|enriched_text.concepts.geonames                                |obsolète|
|enriched_text.concepts.knowledgeGraph.typeHierarchy            |obsolète|
|enriched_text.concepts.musicBrainz                              |obsolète|
|enriched_text.concepts.opencyc                                  |obsolète|
|enriched_text.concepts.relevance                                |enriched_text.concepts.relevance|
|enriched_text.concepts.text                                    |enriched_text.concepts.text|
|enriched_text.concepts.website                                  |obsolète|
|enriched_text.concepts.yago                                    |obsolète|
|enriched_text.docSentiment.mixed                                |obsolète|
|enriched_text.docSentiment.score                                |enriched_text.sentiment.document.score|
|enriched_text.docSentiment.type                                |enriched_text.sentiment.document.label|
|enriched_text.entities                                          |enriched_text.entities|
|enriched_text.entities.count                                    |enriched_text.entities.count|
|enriched_text.entities.disambiguated.census                    |obsolète|
|enriched_text.entities.disambiguated.ciaFactbook                |obsolète|
|enriched_text.entities.disambiguated.crunchbase                |obsolète|
|enriched_text.entities.disambiguated.dbpedia                    |enriched_text.entities.disambiguation.dbpedia_resource|
|enriched_text.entities.disambiguated.freebase                  |obsolète|
|enriched_text.entities.disambiguated.geonames                  |obsolète|
|enriched_text.entities.disambiguated.musicBrainz                |obsolète|
|enriched_text.entities.disambiguated.name                      |enriched_text.entities.disambiguation.name|
|enriched_text.entities.disambiguated.opencyc                    |obsolète|
|enriched_text.entities.disambiguated.subType                    |enriched_text.entities.disambiguation.subtype|
|enriched_text.entities.disambiguated.umbel                      |obsolète|
|enriched_text.entities.disambiguated.website                    |obsolète|
|enriched_text.entities.disambiguated.yago                      |obsolète|
|enriched_text.entities.knowledgeGraph.typeHierarchy            |obsolète|
|enriched_text.entities.quotations                              |obsolète|
|enriched_text.entities.quotations.quotation                    |obsolète|
|enriched_text.entities.quotations.sentiment.mixed              |obsolète|
|enriched_text.entities.quotations.sentiment.score              |obsolète|
|enriched_text.entities.quotations.sentiment.type                |obsolète|
|enriched_text.entities.relevance                                |enriched_text.entities.relevance|
|enriched_text.entities.sentiment.mixed                          |obsolète|
|enriched_text.entities.sentiment.score                          |enriched_text.entities.sentiment.score|
|enriched_text.entities.sentiment.type                          |obsolète|
|enriched_text.entities.text                                    |enriched_text.entities.text|
|enriched_text.entities.type                                    |enriched_text.entities.type|
|enriched_text.keywords                                          |enriched_text.keywords|
|enriched_text.keywords.knowledgeGraph.typeHierarchy            |obsolète|
|enriched_text.keywords.relevance                                |enriched_text.keywords.relevance|
|enriched_text.keywords.sentiment.mixed                          |obsolète|
|enriched_text.keywords.sentiment.score                          |enriched_text.keywords.sentiment.score|
|enriched_text.keywords.sentiment.type                          |obsolète|
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
|enriched_text.relations.location.entities.disambiguated.census    |obsolète|
|enriched_text.relations.location.entities.disambiguated.ciaFactbook    |obsolète|
|enriched_text.relations.location.entities.disambiguated.crunchbase    |obsolète|
|enriched_text.relations.location.entities.disambiguated.dbpedia    |obsolète|
|enriched_text.relations.location.entities.disambiguated.freebase    |obsolète|
|enriched_text.relations.location.entities.disambiguated.geonames    |obsolète|
|enriched_text.relations.location.entities.disambiguated.musicBrainz    |obsolète|
|enriched_text.relations.location.entities.disambiguated.name    |obsolète|
|enriched_text.relations.location.entities.disambiguated.opencyc    |obsolète|
|enriched_text.relations.location.entities.disambiguated.subType    |obsolète|
|enriched_text.relations.location.entities.disambiguated.umbel    |obsolète|
|enriched_text.relations.location.entities.disambiguated.website    |obsolète|
|enriched_text.relations.location.entities.disambiguated.yago    |obsolète|
|enriched_text.relations.location.entities.knowledgeGraph.typeHierarchy    |obsolète|
|enriched_text.relations.location.entities.sentiment.score    |obsolète|
|enriched_text.relations.location.entities.sentiment.type    |obsolète|
|enriched_text.relations.location.entities.text                  |obsolète|
|enriched_text.relations.location.entities.type                  |obsolète|
|enriched_text.relations.location.keywords                      |obsolète|
|enriched_text.relations.location.keywords.text                  |obsolète|
|enriched_text.relations.location.sentiment.score                |obsolète|
|enriched_text.relations.location.sentiment.type                |obsolète|
|enriched_text.relations.location.text                          |obsolète|
|enriched_text.relations.object.entities                        |enriched_text.semantic_roles.object.entities|
|enriched_text.relations.object.entities.disambiguated.census    |obsolète|
|enriched_text.relations.object.entities.disambiguated.ciaFactbook    |obsolète|
|enriched_text.relations.object.entities.disambiguated.crunchbase    |obsolète|
|enriched_text.relations.object.entities.disambiguated.dbpedia    |enriched_text.semantic_roles.object.entities.disambiguation.dbpedia_resource|
|enriched_text.relations.object.entities.disambiguated.freebase    |obsolète|
|enriched_text.relations.object.entities.disambiguated.geonames    |obsolète|
|enriched_text.relations.object.entities.disambiguated.musicBrainz    |obsolète|
|enriched_text.relations.object.entities.disambiguated.name    |enriched_text.semantic_roles.object.entities.disambiguation.name|
|enriched_text.relations.object.entities.disambiguated.opencyc    |obsolète|
|enriched_text.relations.object.entities.disambiguated.subType    |enriched_text.semantic_roles.object.entities.disambiguation.subtype|
|enriched_text.relations.object.entities.disambiguated.umbel    |obsolète|
|enriched_text.relations.object.entities.disambiguated.website    |obsolète|
|enriched_text.relations.object.entities.disambiguated.yago    |obsolète|
|enriched_text.relations.object.entities.knowledgeGraph.typeHierarchy    |obsolète|
|enriched_text.relations.object.entities.sentiment.score    |obsolète|
|enriched_text.relations.object.entities.sentiment.type    |obsolète|
|enriched_text.relations.object.entities.text       |enriched_text.semantic_roles.object.entities.text|
|enriched_text.relations.object.entities.type    |enriched_text.semantic_roles.object.entities.type|
|enriched_text.relations.object.keywords    |enriched_text.semantic_roles.object.keywords|
|enriched_text.relations.object.keywords.knowledgeGraph.typeHierarchy    |obsolète|
|enriched_text.relations.object.keywords.text    |enriched_text.semantic_roles.object.keywords.text|
|enriched_text.relations.object.sentiment.score    |obsolète|
|enriched_text.relations.object.sentiment.type    |obsolète|
|enriched_text.relations.object.sentimentFromSubject.score    |obsolète|
|enriched_text.relations.object.sentimentFromSubject.type    |obsolète|
|enriched_text.relations.object.text    |enriched_text.semantic_roles.object.text|
|enriched_text.relations.sentence    |enriched_text.semantic_roles.sentence|
|enriched_text.relations.subject.entities    |enriched_text.semantic_roles.subject.entities|
|enriched_text.relations.subject.entities.disambiguated.census    |obsolète|
|enriched_text.relations.subject.entities.disambiguated.ciaFactbook    |obsolète|
|enriched_text.relations.subject.entities.disambiguated.crunchbase    |obsolète|
|enriched_text.relations.subject.entities.disambiguated.dbpedia    |enriched_text.semantic_roles.subject.entities.disambiguation.dbpedia_resource|
|enriched_text.relations.subject.entities.disambiguated.freebase    |obsolète|
|enriched_text.relations.subject.entities.disambiguated.geonames    |obsolète|
|enriched_text.relations.subject.entities.disambiguated.musicBrainz    |obsolète|
|enriched_text.relations.subject.entities.disambiguated.name    |enriched_text.semantic_roles.subject.entities.disambiguation.name|
|enriched_text.relations.subject.entities.disambiguated.opencyc    |obsolète|
|enriched_text.relations.subject.entities.disambiguated.subType    |enriched_text.semantic_roles.subject.entities.disambiguation.subtype|
|enriched_text.relations.subject.entities.disambiguated.umbel    |obsolète|
|enriched_text.relations.subject.entities.disambiguated.website    |obsolète|
|enriched_text.relations.subject.entities.disambiguated.yago    |obsolète|
|enriched_text.relations.subject.entities.knowledgeGraph.typeHierarchy    |obsolète|
|enriched_text.relations.subject.entities.sentiment.score    |obsolète|
|enriched_text.relations.subject.entities.sentiment.type    |obsolète|
|enriched_text.relations.subject.entities.text    |enriched_text.semantic_roles.subject.entities.text|
|enriched_text.relations.subject.entities.type    |enriched_text.semantic_roles.subject.entities.type|
|enriched_text.relations.subject.keywords    |enriched_text.semantic_roles.subject.keywords|
|enriched_text.relations.subject.keywords.knowledgeGraph.typeHierarchy    |obsolète|
|enriched_text.relations.subject.keywords.text    |enriched_text.semantic_roles.subject.keywords.text|
|enriched_text.relations.subject.sentiment.score    |obsolète|
|enriched_text.relations.subject.sentiment.type    |obsolète|
|enriched_text.relations.subject.text    |enriched_text.semantic_roles.subject.text|
|enriched_text.taxonomy    |enriched_text.categories|
|enriched_text.taxonomy.confident    |obsolète|
|enriched_text.taxonomy.label    |enriched_text.categories.label|
|enriched_text.taxonomy.score    |enriched_text.categories.score|
|enriched_text.docEmotions.sadness    |enriched_text.emotion.document.emotion.sadness|
|enriched_text.docEmotions.joy    |enriched_text.emotion.document.emotion.joy|
|enriched_text.docEmotions.fear    |enriched_text.emotion.document.emotion.fear|
|enriched_text.docEmotions.disgust    |enriched_text.emotion.document.emotion.disgust|
|enriched_text.docEmotions.anger    |enriched_text.emotion.document.emotion.anger|
|text    |texte|
|title    |titre|
|url    |url|
