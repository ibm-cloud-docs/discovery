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

# Migrando enriquecimento para o Natural Language Understanding

A partir de **18 de julho de 2017**, o {{site.data.keyword.discoveryfull}} introduziu uma nova tecnologia de enriquecimento chamada {{site.data.keyword.nlushort}} (NLU).  Esses enriquecimentos são iguais aos seus enriquecimentos existentes, mas exigem uma configuração e um esquema ligeiramente diferentes. Os enriquecimentos originais, chamados de enriquecimentos {{site.data.keyword.alchemylanguageshort}}, serão descontinuados.
{: shortdesc}

O suporte ao enriquecimento do {{site.data.keyword.alchemylanguageshort}} terminará em **15 de janeiro de 2018**. A sequência de versão da API `2017-10-16` descontinuou o suporte para upload de novos documentos em coleções existentes enriquecidas com o {{site.data.keyword.alchemylanguageshort}} e para a criação de novas coleções e o aprimoramento delas com enriquecimentos do {{site.data.keyword.alchemylanguageshort}}. Use uma sequência de versões da API anterior para continuar usando o {{site.data.keyword.alchemylanguageshort}} até que o suporte seja encerrado em **15 de janeiro de 2018**.

Novas coleções devem ser enriquecidas com o {{site.data.keyword.nlushort}} e todas as coleções existentes com os arquivos de configuração do {{site.data.keyword.alchemylanguageshort}} devem ser migradas o mais rápido possível. 
O suporte para ingestão de enriquecimento do {{site.data.keyword.alchemylanguageshort}} termina em **15 de janeiro de 2018**. Para obter informações sobre como migrar coleções e arquivos de configuração que utilizam os enriquecimentos do {{site.data.keyword.alchemylanguageshort}}, consulte [Comparação de enriquecimento](/docs/services/discovery/migrate-nlu.html#enrichment-comparison).

**Nota:** para obter informações sobre a integração com o {{site.data.keyword.knowledgestudioshort}}, consulte [Integrando-se com o {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery/integrate-wks.html).

## Comparação de enriquecimento
{: #enrichment-comparison}

Os sete enriquecimentos disponíveis no {{site.data.keyword.alchemylanguageshort}} e no {{site.data.keyword.nlushort}}, juntamente com seus nomes de objetos JSON são:

| Nome do enriquecimento do {{site.data.keyword.alchemylanguageshort}}         | Objeto JSON do {{site.data.keyword.alchemylanguageshort}}  | Nome do enriquecimento NLU                     | 
Objeto JSON do NLU        |
|---------------------------|----------------------------------------|----------------------------------------|--------------------------------|
| Extração de entidade                     | entidades                        |Extração de entidade                           |   entidades            |
| Extração de palavra-chave                    | palavras-chave                        |Extração de palavra-chave                          |   palavras-chave            |
| Classificação de Taxonomia               | taxonomia                        |Classificação de categoria*
|   categorias*         |
| Identificação de conceito                       | conceitos                        |Identificação de conceito                             |   
conceitos            |
| Análise de sentimentos                    | docSentiment                    |Análise de sentimentos                          |   impressão*
|
| Análise de Emoção                      | docEmotions                     |Análise de Emoção
|   emoção*            |
| Extração de Relação                  | relações                       |Extração de Função Semântica*
|   semantic_roles*     |
 \* Mudança de nome

Para obter mais informações sobre enriquecimentos do {{site.data.keyword.alchemylanguageshort}}, consulte [Enriquecimentos do {{site.data.keyword.alchemylanguageshort}}](/docs/services/discovery/discovery-auxiliary.html#AlchemyLanguage-enrichments).
Para obter mais informações sobre enriquecimentos do {{site.data.keyword.nlushort}}, consulte [Incluindo enriquecimentos](/docs/services/discovery/building.html#adding-enrichments)

## Visão geral das principais mudanças

- O esquema JSON para enriquecimentos do {{site.data.keyword.nlushort}} é diferente daquele usado nos enriquecimentos do {{site.data.keyword.alchemylanguageshort}}; para obter uma lista completa das mudanças em cada enriquecimento, consulte: [Diferenças no esquema de enriquecimento](/docs/services/discovery/migrate-nlu.html#enrichment-schema-differences).
- O enriquecimento _Classificação de Taxonomia_ ({{site.data.keyword.alchemylanguageshort}}) é agora denominado _Classificação de Categoria_. Seu nome de objeto JSON mudou de `taxonomy` para `categories`.
- O enriquecimento _Extração de Relação_ ({{site.data.keyword.alchemylanguageshort}}) é agora chamado _Extração de Função de Semântica_. Seu nome de objeto JSON mudou de `relations` para `semantic_roles`.
- O nome do objeto JSON para _Análise de Sentimentos_ mudou de `docSentiment` para `sentiment`.
- O nome do objeto JSON para _Análise de Emoção_ mudou de `docEmotions` para `emotion`.

## Mudanças no arquivo de configuração

O arquivo de configuração padrão do **{{site.data.keyword.alchemylanguageshort}}** (denominado `Configuração Padrão` no conjunto de ferramentas) aplica os seguintes enriquecimentos no campo de texto de seus documentos: **Extração de Entidade**, **Extração de Palavra-chave**, **Classificação de Taxonomia**, **Identificação de Conceito**, **Extração de Relação** e **Análise de Sentimentos**. O arquivo também inclui conversões padrão de documentos com base em estilos e tamanhos de fonte.

O arquivo de configuração padrão do **{{site.data.keyword.nlushort}}** é denominado `Configuração Padrão com NLU` e aplica os seguintes enriquecimentos no campo de texto de seus documentos: **Extração de Entidade**, **Análise de Sentimentos**, **Classificação de Categoria** e **Identificação de Conceito**. O arquivo também inclui conversões padrão de documentos com base em estilos e tamanhos de fonte. Essas conversões de documentos são idênticas àquelas no arquivo de configuração padrão do
{{site.data.keyword.alchemylanguageshort}}.

## Migrando suas configurações, coleções e consultas

Se você tiver criado quaisquer configurações customizadas, será necessário criar novas configurações que usem os enriquecimentos do {{site.data.keyword.nlushort}}. Para obter instruções, consulte estes
documentos:

- [Conjunto de ferramentas](/docs/services/discovery/building.html#custom-configuration)
- [API
![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#add_configuration){: new_window}

Se você tiver coleções existentes que possuem a configuração padrão do
{{site.data.keyword.alchemylanguageshort}} ou uma configuração customizada do
{{site.data.keyword.alchemylanguageshort}} aplicada a elas, será necessário criar uma nova coleção,
aplicar o arquivo de configuração do {{site.data.keyword.nlushort}} (a configuração padrão ou uma nova
configuração customizada) e fazer upload de seus documentos. Para obter instruções, consulte esses documentos:

- [Conjunto de ferramentas](/docs/services/discovery/building.html#preparing-the-service-for-your-documents)
- [API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#create-collection){: new_window}

Para quaisquer consultas que você criou usando o Discovery Query Language, é necessário
examinar as mudanças no esquema JSON entre o {{site.data.keyword.alchemylanguageshort}} e
o {{site.data.keyword.nlushort}} e atualizar suas consultas e URLs de consulta apropriadamente. 
Consulte [Diferenças
de esquema de enriquecimento](/docs/services/discovery/migrate-nlu.html#enrichment-schema-differences) para obter detalhes.

## Diferenças de esquema de enriquecimento

A tabela a seguir mostra as diferenças entre o esquema JSON para os enriquecimentos do {{site.data.keyword.nlushort}} e os enriquecimentos do {{site.data.keyword.alchemylanguageshort}}.

| {{site.data.keyword.alchemylanguageshort}}                         | {{site.data.keyword.nlushort}}       |
|-----------------------------------------|--------------------------------------|
|enriched_text.concepts                      |enriched_text.concepts|
|enriched_text.concepts.census              |descontinuado|
|enriched_text.concepts.ciaFactbook          |descontinuado|
|enriched_text.concepts.crunchbase                              |descontinuado|
|enriched_text.concepts.dbpedia                               |enriched_text.concepts.dbpedia_resource|
|enriched_text.concepts.freebase                              |descontinuado|
|enriched_text.concepts.geonames                                |descontinuado|
|enriched_text.concepts.knowledgeGraph.typeHierarchy            |descontinuado|
|enriched_text.concepts.musicBrainz                              |descontinuado|
|enriched_text.concepts.opencyc                                  |descontinuado|
|enriched_text.concepts.relevance                                |enriched_text.concepts.relevance|
|enriched_text.concepts.text                                    |enriched_text.concepts.text|
|enriched_text.concepts.website                                  |descontinuado|
|enriched_text.concepts.yago                                    |descontinuado|
|enriched_text.docSentiment.mixed                                |descontinuado|
|enriched_text.docSentiment.score                                |enriched_text.sentiment.document.score|
|enriched_text.docSentiment.type                                |enriched_text.sentiment.document.label|
|enriched_text.entities                                          |enriched_text.entities|
|enriched_text.entities.count                                    |enriched_text.entities.count|
|enriched_text.entities.disambiguated.census                    |descontinuado|
|enriched_text.entities.disambiguated.ciaFactbook                |descontinuado|
|enriched_text.entities.disambiguated.crunchbase                |descontinuado|
|enriched_text.entities.disambiguated.dbpedia                    |enriched_text.entities.disambiguation.dbpedia_resource|
|enriched_text.entities.disambiguated.freebase                  |descontinuado|
|enriched_text.entities.disambiguated.geonames                  |descontinuado|
|enriched_text.entities.disambiguated.musicBrainz                |descontinuado|
|enriched_text.entities.disambiguated.name                      |enriched_text.entities.disambiguation.name|
|enriched_text.entities.disambiguated.opencyc                    |descontinuado|
|enriched_text.entities.disambiguated.subType                    |enriched_text.entities.disambiguation.subtype|
|enriched_text.entities.disambiguated.umbel                      |descontinuado|
|enriched_text.entities.disambiguated.website                    |descontinuado|
|enriched_text.entities.disambiguated.yago                      |descontinuado|
|enriched_text.entities.knowledgeGraph.typeHierarchy            |descontinuado|
|enriched_text.entities.quotations                              |descontinuado|
|enriched_text.entities.quotations.quotation                    |descontinuado|
|enriched_text.entities.quotations.sentiment.mixed              |descontinuado|
|enriched_text.entities.quotations.sentiment.score              |descontinuado|
|enriched_text.entities.quotations.sentiment.type                |descontinuado|
|enriched_text.entities.relevance                                |enriched_text.entities.relevance|
|enriched_text.entities.sentiment.mixed                          |descontinuado|
|enriched_text.entities.sentiment.score                          |enriched_text.entities.sentiment.score|
|enriched_text.entities.sentiment.type                          |descontinuado|
|enriched_text.entities.text                                    |enriched_text.entities.text|
|enriched_text.entities.type                                    |enriched_text.entities.type|
|enriched_text.keywords                                          |enriched_text.keywords|
|enriched_text.keywords.knowledgeGraph.typeHierarchy            |descontinuado|
|enriched_text.keywords.relevance                                |enriched_text.keywords.relevance|
|enriched_text.keywords.sentiment.mixed                          |descontinuado|
|enriched_text.keywords.sentiment.score                          |enriched_text.keywords.sentiment.score|
|enriched_text.keywords.sentiment.type                          |descontinuado|
|enriched_text.keywords.text                                    |enriched_text.keywords.text|
|linguagem                                                        |linguagem|
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
|enriched_text.relations.location.entities.disambiguated.census    |descontinuado|
|enriched_text.relations.location.entities.disambiguated.ciaFactbook    |descontinuado|
|enriched_text.relations.location.entities.disambiguated.crunchbase    |descontinuado|
|enriched_text.relations.location.entities.disambiguated.dbpedia    |descontinuado|
|enriched_text.relations.location.entities.disambiguated.freebase    |descontinuado|
|enriched_text.relations.location.entities.disambiguated.geonames    |descontinuado|
|enriched_text.relations.location.entities.disambiguated.musicBrainz    |descontinuado|
|enriched_text.relations.location.entities.disambiguated.name    |descontinuado|
|enriched_text.relations.location.entities.disambiguated.opencyc    |descontinuado|
|enriched_text.relations.location.entities.disambiguated.subType    |descontinuado|
|enriched_text.relations.location.entities.disambiguated.umbel    |descontinuado|
|enriched_text.relations.location.entities.disambiguated.website    |descontinuado|
|enriched_text.relations.location.entities.disambiguated.yago    |descontinuado|
|enriched_text.relations.location.entities.knowledgeGraph.typeHierarchy    |descontinuado|
|enriched_text.relations.location.entities.sentiment.score    |descontinuado|
|enriched_text.relations.location.entities.sentiment.type    |descontinuado|
|enriched_text.relations.location.entities.text                  |descontinuado|
|enriched_text.relations.location.entities.type                  |descontinuado|
|enriched_text.relations.location.keywords                      |descontinuado|
|enriched_text.relations.location.keywords.text                  |descontinuado|
|enriched_text.relations.location.sentiment.score                |descontinuado|
|enriched_text.relations.location.sentiment.type                |descontinuado|
|enriched_text.relations.location.text                          |descontinuado|
|enriched_text.relations.object.entities                        |enriched_text.semantic_roles.object.entities|
|enriched_text.relations.object.entities.disambiguated.census    |descontinuado|
|enriched_text.relations.object.entities.disambiguated.ciaFactbook    |descontinuado|
|enriched_text.relations.object.entities.disambiguated.crunchbase    |descontinuado|
|enriched_text.relations.object.entities.disambiguated.dbpedia    |enriched_text.semantic_roles.object.entities.disambiguation.dbpedia_resource|
|enriched_text.relations.object.entities.disambiguated.freebase    |descontinuado|
|enriched_text.relations.object.entities.disambiguated.geonames    |descontinuado|
|enriched_text.relations.object.entities.disambiguated.musicBrainz    |descontinuado|
|enriched_text.relations.object.entities.disambiguated.name    |enriched_text.semantic_roles.object.entities.disambiguation.name|
|enriched_text.relations.object.entities.disambiguated.opencyc    |descontinuado|
|enriched_text.relations.object.entities.disambiguated.subType    |enriched_text.semantic_roles.object.entities.disambiguation.subtype|
|enriched_text.relations.object.entities.disambiguated.umbel    |descontinuado|
|enriched_text.relations.object.entities.disambiguated.website    |descontinuado|
|enriched_text.relations.object.entities.disambiguated.yago    |descontinuado|
|enriched_text.relations.object.entities.knowledgeGraph.typeHierarchy    |descontinuado|
|enriched_text.relations.object.entities.sentiment.score    |descontinuado|
|enriched_text.relations.object.entities.sentiment.type    |descontinuado|
|enriched_text.relations.object.entities.text       |enriched_text.semantic_roles.object.entities.text|
|enriched_text.relations.object.entities.type    |enriched_text.semantic_roles.object.entities.type|
|enriched_text.relations.object.keywords    |enriched_text.semantic_roles.object.keywords|
|enriched_text.relations.object.keywords.knowledgeGraph.typeHierarchy    |descontinuado|
|enriched_text.relations.object.keywords.text    |enriched_text.semantic_roles.object.keywords.text|
|enriched_text.relations.object.sentiment.score    |descontinuado|
|enriched_text.relations.object.sentiment.type    |descontinuado|
|enriched_text.relations.object.sentimentFromSubject.score    |descontinuado|
|enriched_text.relations.object.sentimentFromSubject.type    |descontinuado|
|enriched_text.relations.object.text    |enriched_text.semantic_roles.object.text|
|enriched_text.relations.sentence    |enriched_text.semantic_roles.sentence|
|enriched_text.relations.subject.entities    |enriched_text.semantic_roles.subject.entities|
|enriched_text.relations.subject.entities.disambiguated.census    |descontinuado|
|enriched_text.relations.subject.entities.disambiguated.ciaFactbook    |descontinuado|
|enriched_text.relations.subject.entities.disambiguated.crunchbase    |descontinuado|
|enriched_text.relations.subject.entities.disambiguated.dbpedia    |enriched_text.semantic_roles.subject.entities.disambiguation.dbpedia_resource|
|enriched_text.relations.subject.entities.disambiguated.freebase    |descontinuado|
|enriched_text.relations.subject.entities.disambiguated.geonames    |descontinuado|
|enriched_text.relations.subject.entities.disambiguated.musicBrainz    |descontinuado|
|enriched_text.relations.subject.entities.disambiguated.name    |enriched_text.semantic_roles.subject.entities.disambiguation.name|
|enriched_text.relations.subject.entities.disambiguated.opencyc    |descontinuado|
|enriched_text.relations.subject.entities.disambiguated.subType    |enriched_text.semantic_roles.subject.entities.disambiguation.subtype|
|enriched_text.relations.subject.entities.disambiguated.umbel    |descontinuado|
|enriched_text.relations.subject.entities.disambiguated.website    |descontinuado|
|enriched_text.relations.subject.entities.disambiguated.yago    |descontinuado|
|enriched_text.relations.subject.entities.knowledgeGraph.typeHierarchy    |descontinuado|
|enriched_text.relations.subject.entities.sentiment.score    |descontinuado|
|enriched_text.relations.subject.entities.sentiment.type    |descontinuado|
|enriched_text.relations.subject.entities.text    |enriched_text.semantic_roles.subject.entities.text|
|enriched_text.relations.subject.entities.type    |enriched_text.semantic_roles.subject.entities.type|
|enriched_text.relations.subject.keywords    |enriched_text.semantic_roles.subject.keywords|
|enriched_text.relations.subject.keywords.knowledgeGraph.typeHierarchy    |descontinuado|
|enriched_text.relations.subject.keywords.text    |enriched_text.semantic_roles.subject.keywords.text|
|enriched_text.relations.subject.sentiment.score    |descontinuado|
|enriched_text.relations.subject.sentiment.type    |descontinuado|
|enriched_text.relations.subject.text    |enriched_text.semantic_roles.subject.text|
|enriched_text.taxonomy    |enriched_text.categories|
|enriched_text.taxonomy.confident    |descontinuado|
|enriched_text.taxonomy.label    |enriched_text.categories.label|
|enriched_text.taxonomy.score    |enriched_text.categories.score|
|enriched_text.docEmotions.sadness    |enriched_text.emotion.document.emotion.sadness|
|enriched_text.docEmotions.joy    |enriched_text.emotion.document.emotion.joy|
|enriched_text.docEmotions.fear    |enriched_text.emotion.document.emotion.fear|
|enriched_text.docEmotions.disgust    |enriched_text.emotion.document.emotion.disgust|
|enriched_text.docEmotions.anger    |enriched_text.emotion.document.emotion.anger|
|text    |texto|
|title    |title|
|url    |url|
