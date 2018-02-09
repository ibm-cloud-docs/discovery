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

# Migración de enriquecimientos a NLU (Natural Language Understanding)

Desde el **18 de julio del 2017** {{site.data.keyword.discoveryfull}} introdujo una nueva tecnología de enriquecimiento, denominado el NLU ({{site.data.keyword.nlushort}}). Estos enriquecimientos son los mismos que los enriquecimientos existentes pero requieren una configuración y un esquema ligeramente diferente. Los enriquecimientos originales, denominados enriquecimientos de {{site.data.keyword.alchemylanguageshort}}, pasarán a estar en desuso.
{: shortdesc}

El soporte para los enriquecimientos de {{site.data.keyword.alchemylanguageshort}} finalizará el **15 de enero de 2018**. La serie de versión de API `2017-10-16` está en desuso para dar soporte a la carga de nuevos documentos en recopilaciones existentes enriquecidas con {{site.data.keyword.alchemylanguageshort}} y para crear nuevas recopilaciones y enriquecerlas con los enriquecimientos de {{site.data.keyword.alchemylanguageshort}}. Utilice una serie de versión de API anterior para continuar utilizando {{site.data.keyword.alchemylanguageshort}} hasta que el soporte finalice el **15 de enero de 2018**.

Debería enriquecer las nuevas recopilaciones con {{site.data.keyword.nlushort}} y migrar lo antes posible todas las recopilaciones existentes con archivos de configuración de {{site.data.keyword.alchemylanguageshort}}. El soporte para la ingestión de enriquecimiento de {{site.data.keyword.alchemylanguageshort}} finaliza el **15 de enero de 2018**. Para obtener información sobre la migración de recopilaciones y de archivos de configuración que utilizan los enriquecimientos de {{site.data.keyword.alchemylanguageshort}}, consulte [Comparación de enriquecimientos](/docs/services/discovery/migrate-nlu.html#enrichment-comparison).

**Nota:** Para obtener información sobre la integración con {{site.data.keyword.knowledgestudioshort}}, consulte [Integración con {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery/integrate-wks.html). 

## Comparación de enriquecimientos
{: #enrichment-comparison}

Los siete enriquecimientos disponibles en {{site.data.keyword.alchemylanguageshort}} y {{site.data.keyword.nlushort}}, junto con sus nombres de objeto JSON son: 

| Nombre de enriquecimiento de {{site.data.keyword.alchemylanguageshort}} | Objeto JSON de {{site.data.keyword.alchemylanguageshort}}| Nombre de enriquecimiento NLU| 
Objeto JSON de NLU|
|---------------------------|----------------------------------------|----------------------------------------|--------------------------------|
| Extracción de entidades| entities                        |Extracción de entidades|   entities            |
| Extracción de palabras clave| keywords                        |Extracción de palabras clave|   keywords            |
| Clasificación de taxonomías| taxonomy                        |Clasificación de categorías*                    |   categories*         |
| Etiquetado de conceptos| concepts                        |Etiquetado de conceptos|   concepts            |
| Análisis de sentimiento| docSentiment                    |Análisis de sentimiento|   sentiment*          |
| Análisis de emociones| docEmotions                     |Análisis de emociones|   emotion*            |
| Extracción de relaciones| relations                       |Extracción de roles semánticos*                   |   semantic_roles*     |
 \* Cambio de nombre

Para obtener más información sobre los enriquecimientos de {{site.data.keyword.alchemylanguageshort}}, consulte [Enriquecimientos de {{site.data.keyword.alchemylanguageshort}}](/docs/services/discovery/discovery-auxiliary.html#AlchemyLanguage-enrichments). Para obtener información sobre los enriquecimientos de {{site.data.keyword.nlushort}}, consulte [Adición de enriquecimientos](/docs/services/discovery/building.html#adding-enrichments). 

## Visión general de los cambios más importantes

- El esquema JSON para los enriquecimientos de {{site.data.keyword.nlushort}} varía del utilizado en los enriquecimientos de {{site.data.keyword.alchemylanguageshort}}. Si desea obtener una lista completa de los cambios a cada enriquecimiento, consulte [Diferencias en el esquema de enriquecimiento](/docs/services/discovery/migrate-nlu.html#enrichment-schema-differences). 
- El enriquecimiento _Clasificación de taxonomías_ ({{site.data.keyword.alchemylanguageshort}}) ahora se denomina _Clasificación de categorías_. El nombre del objeto JSON se ha cambiado de `taxonomy` a `categories`.
- El enriquecimiento _Extracción de relaciones_ ({{site.data.keyword.alchemylanguageshort}}) ahora se denomina _Extracción de roles semánticos_. El nombre del objeto JSON se ha cambiado de `relations` a `semantic_roles`.
- El nombre del objeto JSON para el _Análisis del sentimiento_ se ha cambiado de `docSentiment` a `sentiment`.
- El nombre del objeto JSON para el _Análisis de las emociones_ se ha cambiado de `docEmotions` a `emotion`.

## Cambios en el archivo de configuración

El archivo de configuración predeterminado de **{{site.data.keyword.alchemylanguageshort}}** (denominado como `Configuración predeterminada` en el conjunto de herramientas) aplicaba los siguientes enriquecimientos al campo de texto de sus documentos: **Extracción de entidades**, **Extracción de palabras clave**, **Clasificación de taxonomías**, **Etiquetado de conceptos**, **Extracción de relaciones** y **Análisis de sentimiento**. El archivo también incluye las conversiones de documento estándar con base a estilos y tamaños de font. 

El archivo de configuración predeterminado de **{{site.data.keyword.nlushort}}** se denomina `Configuración predeterminada con NLU` y aplica los siguientes enriquecimientos al campo de texto de sus documentos: **Extracción de entidades**, **Análisis de sentimiento**, **Clasificación de categorías** y **Etiquetado de conceptos**. El archivo también incluye las conversiones de documento estándar con base a estilos y tamaños de font. Estas conversiones de documento son idénticas a las del archivo de configuración predeterminado de {{site.data.keyword.alchemylanguageshort}}. 

## Migración de configuraciones, recopilaciones y consultas

Si ha creado configuraciones personalizadas, debe crear unas nuevas que utilicen los enriquecimientos de {{site.data.keyword.nlushort}}.  Para obtener instrucciones sobre cómo hacerlo, consulte estos documentos: 

- [Conjunto de herramientas](/docs/services/discovery/building.html#custom-configuration)
- [API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#add_configuration){: new_window}

Si tiene recopilaciones existentes con la configuración predeterminada de {{site.data.keyword.alchemylanguageshort}} o una configuración de {{site.data.keyword.alchemylanguageshort}} personalizada, deberá crear una nueva recopilación, aplicar el archivo de configuración de {{site.data.keyword.nlushort}} (la configuración predeterminada o una nueva configuración personalizada) y cargar los documentos. Para obtener instrucciones sobre cómo hacerlo, consulte estos documentos: 

- [Conjunto de herramientas](/docs/services/discovery/building.html#preparing-the-service-for-your-documents)
- [API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#create-collection){: new_window}

En muchas consultas que haya creado con Discovery Query Language, necesitará examinar los cambios de esquema de JSON entre {{site.data.keyword.alchemylanguageshort}} y {{site.data.keyword.nlushort}} y actualizar sus consultas y los URL de consultas del mismo modo. Consulte [Diferencia de esquemas de enriquecimiento](/docs/services/discovery/migrate-nlu.html#enrichment-schema-differences) para obtener más detalles. 

## Diferencia de esquemas de enriquecimiento

En la siguiente tabla se muestra una lista con las diferencias entre el esquema JSON para los enriquecimientos de {{site.data.keyword.nlushort}} y los enriquecimientos de {{site.data.keyword.alchemylanguageshort}}. 

| {{site.data.keyword.alchemylanguageshort}}                         | {{site.data.keyword.nlushort}}       |
|-----------------------------------------|--------------------------------------|
|enriched_text.concepts                      |enriched_text.concepts|
|enriched_text.concepts.census              |en desuso|
|enriched_text.concepts.ciaFactbook          |en desuso|
|enriched_text.concepts.crunchbase                              |en desuso|
|enriched_text.concepts.dbpedia                               |enriched_text.concepts.dbpedia_resource|
|enriched_text.concepts.freebase                              |en desuso|
|enriched_text.concepts.geonames                                |en desuso|
|enriched_text.concepts.knowledgeGraph.typeHierarchy            |en desuso|
|enriched_text.concepts.musicBrainz                              |en desuso|
|enriched_text.concepts.opencyc                                  |en desuso|
|enriched_text.concepts.relevance                                |enriched_text.concepts.relevance|
|enriched_text.concepts.text                                    |enriched_text.concepts.text|
|enriched_text.concepts.website                                  |en desuso|
|enriched_text.concepts.yago                                    |en desuso|
|enriched_text.docSentiment.mixed                                |en desuso|
|enriched_text.docSentiment.score                                |enriched_text.sentiment.document.score|
|enriched_text.docSentiment.type                                |enriched_text.sentiment.document.label|
|enriched_text.entities                                          |enriched_text.entities|
|enriched_text.entities.count                                    |enriched_text.entities.count|
|enriched_text.entities.disambiguated.census                    |en desuso|
|enriched_text.entities.disambiguated.ciaFactbook                |en desuso|
|enriched_text.entities.disambiguated.crunchbase                |en desuso|
|enriched_text.entities.disambiguated.dbpedia                    |enriched_text.entities.disambiguation.dbpedia_resource|
|enriched_text.entities.disambiguated.freebase                  |en desuso|
|enriched_text.entities.disambiguated.geonames                  |en desuso|
|enriched_text.entities.disambiguated.musicBrainz                |en desuso|
|enriched_text.entities.disambiguated.name                      |enriched_text.entities.disambiguation.name|
|enriched_text.entities.disambiguated.opencyc                    |en desuso|
|enriched_text.entities.disambiguated.subType                    |enriched_text.entities.disambiguation.subtype|
|enriched_text.entities.disambiguated.umbel                      |en desuso|
|enriched_text.entities.disambiguated.website                    |en desuso|
|enriched_text.entities.disambiguated.yago                      |en desuso|
|enriched_text.entities.knowledgeGraph.typeHierarchy            |en desuso|
|enriched_text.entities.quotations                              |en desuso|
|enriched_text.entities.quotations.quotation                    |en desuso|
|enriched_text.entities.quotations.sentiment.mixed              |en desuso|
|enriched_text.entities.quotations.sentiment.score              |en desuso|
|enriched_text.entities.quotations.sentiment.type                |en desuso|
|enriched_text.entities.relevance                                |enriched_text.entities.relevance|
|enriched_text.entities.sentiment.mixed                          |en desuso|
|enriched_text.entities.sentiment.score                          |enriched_text.entities.sentiment.score|
|enriched_text.entities.sentiment.type                          |en desuso|
|enriched_text.entities.text                                    |enriched_text.entities.text|
|enriched_text.entities.type                                    |enriched_text.entities.type|
|enriched_text.keywords                                          |enriched_text.keywords|
|enriched_text.keywords.knowledgeGraph.typeHierarchy            |en desuso|
|enriched_text.keywords.relevance                                |enriched_text.keywords.relevance|
|enriched_text.keywords.sentiment.mixed                          |en desuso|
|enriched_text.keywords.sentiment.score                          |enriched_text.keywords.sentiment.score|
|enriched_text.keywords.sentiment.type                          |en desuso|
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
|enriched_text.relations.location.entities.disambiguated.census    |en desuso|
|enriched_text.relations.location.entities.disambiguated.ciaFactbook    |en desuso|
|enriched_text.relations.location.entities.disambiguated.crunchbase    |en desuso|
|enriched_text.relations.location.entities.disambiguated.dbpedia    |en desuso|
|enriched_text.relations.location.entities.disambiguated.freebase    |en desuso|
|enriched_text.relations.location.entities.disambiguated.geonames    |en desuso|
|enriched_text.relations.location.entities.disambiguated.musicBrainz    |en desuso|
|enriched_text.relations.location.entities.disambiguated.name    |en desuso|
|enriched_text.relations.location.entities.disambiguated.opencyc    |en desuso|
|enriched_text.relations.location.entities.disambiguated.subType    |en desuso|
|enriched_text.relations.location.entities.disambiguated.umbel    |en desuso|
|enriched_text.relations.location.entities.disambiguated.website    |en desuso|
|enriched_text.relations.location.entities.disambiguated.yago    |en desuso|
|enriched_text.relations.location.entities.knowledgeGraph.typeHierarchy    |en desuso|
|enriched_text.relations.location.entities.sentiment.score    |en desuso|
|enriched_text.relations.location.entities.sentiment.type    |en desuso|
|enriched_text.relations.location.entities.text                  |en desuso|
|enriched_text.relations.location.entities.type                  |en desuso|
|enriched_text.relations.location.keywords                      |en desuso|
|enriched_text.relations.location.keywords.text                  |en desuso|
|enriched_text.relations.location.sentiment.score                |en desuso|
|enriched_text.relations.location.sentiment.type                |en desuso|
|enriched_text.relations.location.text                          |en desuso|
|enriched_text.relations.object.entities                        |enriched_text.semantic_roles.object.entities|
|enriched_text.relations.object.entities.disambiguated.census    |en desuso|
|enriched_text.relations.object.entities.disambiguated.ciaFactbook    |en desuso|
|enriched_text.relations.object.entities.disambiguated.crunchbase    |en desuso|
|enriched_text.relations.object.entities.disambiguated.dbpedia    |enriched_text.semantic_roles.object.entities.disambiguation.dbpedia_resource|
|enriched_text.relations.object.entities.disambiguated.freebase    |en desuso|
|enriched_text.relations.object.entities.disambiguated.geonames    |en desuso|
|enriched_text.relations.object.entities.disambiguated.musicBrainz    |en desuso|
|enriched_text.relations.object.entities.disambiguated.name    |enriched_text.semantic_roles.object.entities.disambiguation.name|
|enriched_text.relations.object.entities.disambiguated.opencyc    |en desuso|
|enriched_text.relations.object.entities.disambiguated.subType    |enriched_text.semantic_roles.object.entities.disambiguation.subtype|
|enriched_text.relations.object.entities.disambiguated.umbel    |en desuso|
|enriched_text.relations.object.entities.disambiguated.website    |en desuso|
|enriched_text.relations.object.entities.disambiguated.yago    |en desuso|
|enriched_text.relations.object.entities.knowledgeGraph.typeHierarchy    |en desuso|
|enriched_text.relations.object.entities.sentiment.score    |en desuso|
|enriched_text.relations.object.entities.sentiment.type    |en desuso|
|enriched_text.relations.object.entities.text       |enriched_text.semantic_roles.object.entities.text|
|enriched_text.relations.object.entities.type    |enriched_text.semantic_roles.object.entities.type|
|enriched_text.relations.object.keywords    |enriched_text.semantic_roles.object.keywords|
|enriched_text.relations.object.keywords.knowledgeGraph.typeHierarchy    |en desuso|
|enriched_text.relations.object.keywords.text    |enriched_text.semantic_roles.object.keywords.text|
|enriched_text.relations.object.sentiment.score    |en desuso|
|enriched_text.relations.object.sentiment.type    |en desuso|
|enriched_text.relations.object.sentimentFromSubject.score    |en desuso|
|enriched_text.relations.object.sentimentFromSubject.type    |en desuso|
|enriched_text.relations.object.text    |enriched_text.semantic_roles.object.text|
|enriched_text.relations.sentence    |enriched_text.semantic_roles.sentence|
|enriched_text.relations.subject.entities    |enriched_text.semantic_roles.subject.entities|
|enriched_text.relations.subject.entities.disambiguated.census    |en desuso|
|enriched_text.relations.subject.entities.disambiguated.ciaFactbook    |en desuso|
|enriched_text.relations.subject.entities.disambiguated.crunchbase    |en desuso|
|enriched_text.relations.subject.entities.disambiguated.dbpedia    |enriched_text.semantic_roles.subject.entities.disambiguation.dbpedia_resource|
|enriched_text.relations.subject.entities.disambiguated.freebase    |en desuso|
|enriched_text.relations.subject.entities.disambiguated.geonames    |en desuso|
|enriched_text.relations.subject.entities.disambiguated.musicBrainz    |en desuso|
|enriched_text.relations.subject.entities.disambiguated.name    |enriched_text.semantic_roles.subject.entities.disambiguation.name|
|enriched_text.relations.subject.entities.disambiguated.opencyc    |en desuso|
|enriched_text.relations.subject.entities.disambiguated.subType    |enriched_text.semantic_roles.subject.entities.disambiguation.subtype|
|enriched_text.relations.subject.entities.disambiguated.umbel    |en desuso|
|enriched_text.relations.subject.entities.disambiguated.website    |en desuso|
|enriched_text.relations.subject.entities.disambiguated.yago    |en desuso|
|enriched_text.relations.subject.entities.knowledgeGraph.typeHierarchy    |en desuso|
|enriched_text.relations.subject.entities.sentiment.score    |en desuso|
|enriched_text.relations.subject.entities.sentiment.type    |en desuso|
|enriched_text.relations.subject.entities.text    |enriched_text.semantic_roles.subject.entities.text|
|enriched_text.relations.subject.entities.type    |enriched_text.semantic_roles.subject.entities.type|
|enriched_text.relations.subject.keywords    |enriched_text.semantic_roles.subject.keywords|
|enriched_text.relations.subject.keywords.knowledgeGraph.typeHierarchy    |en desuso|
|enriched_text.relations.subject.keywords.text    |enriched_text.semantic_roles.subject.keywords.text|
|enriched_text.relations.subject.sentiment.score    |en desuso|
|enriched_text.relations.subject.sentiment.type    |en desuso|
|enriched_text.relations.subject.text    |enriched_text.semantic_roles.subject.text|
|enriched_text.taxonomy    |enriched_text.categories|
|enriched_text.taxonomy.confident    |en desuso|
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
