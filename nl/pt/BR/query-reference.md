---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-09"

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

# Referência de Consulta

O serviço do {{site.data.keyword.discoveryfull}} oferece poderosos recursos de pesquisa de conteúdo por meio de consultas. Após seu conteúdo ser transferido por upload e enriquecido pelo serviço do {{site.data.keyword.discoveryshort}}, será possível construir consultas, integrar o{{site.data.keyword.discoveryshort}} em seus próprios projetos ou criar um aplicativo customizado usando o {{site.data.keyword.watson}} Explorer Application Builder.
{: shortdesc}

Para obter informações sobre como criar consultas, consulte:
- [Introdução à consulta](/docs/services/discovery/getting-started-query.html)
- [Conceitos de consulta](/docs/services/discovery/using.html)

## Descrições de Parâmetros
{: #parameter-descriptions}

Os parâmetros de consulta permitem procurar pela sua coleção, identificar um conjunto de
resultados e executar análise no conjunto de resultados.


| Parâmetros | Descrição | Exemplo |
|:-------------------:|------------------------------------------------------------|--------------------------------|
|** Parâmetros de procura **|  |  |
| [query](/docs/services/discovery/query-parameters.html#query) | Uma procura de linguagem de
consulta classificada para documentos correspondentes. | `query=bees` |
| [filter](/docs/services/discovery/query-parameters.html#filter) | Uma procura de linguagem
de consulta não classificada para documentos correspondentes. | `filter=bees` |
| [natural_language_query](/docs/services/discovery/query-parameters.html#nlq) | Uma procura
de linguagem natural classificada para documentos correspondentes | `natural_language_query="How do bees fly"` |
| [aggregation](/docs/services/discovery/query-parameters.html#aggregation) | Uma consulta
de estatística do conjunto de resultados | `aggregation=term(enriched_text.entities.type)` |
| **Parâmetros de estrutura** | | |
| [count](/docs/services/discovery/query-parameters.html#count) | O número de
documentos `result` a serem retornados. | `count=15` |
| [offset](/docs/services/discovery/query-parameters.html#offset) | O número de resultados a
serem ignorados antes de retornar documentos `result` por meio do conjunto de resultados | `offset=100` |
| [return](/docs/services/discovery/query-parameters.html#return) | Lista de campos a
serem retornados | `return=title,url` |
| [sort](/docs/services/discovery/query-parameters.html#sort) | Campo pelo qual o
conjunto de resultados será classificado | `sort=enriched_text.sentiment.document.score` |
| [passages.fields](/docs/services/discovery/query-parameters.html#passages_fields) | Campos
dos quais passagens serão extraídas | `passages=true&passages.fields=text,abstract,conclusion` |
| [passages.count](/docs/services/discovery/query-parameters.html#passages_count) | Número de
passagens a serem retornadas | `passages=true&passages.count=6` |
| [passages.characters](/docs/services/discovery/query-parameters.html#passages_characters) | 
Duração das passagens | `passages=true&passages.characters=144` |
| [highlight](/docs/services/discovery/query-parameters.html#highlight) | Destacar
correspondências de consulta | `highlight=true` |
| [deduplicate](/docs/services/discovery/query-parameters.html#deduplicate) | Deduplicar
resultados retornados do {{site.data.keyword.discoverynewsfull}} | `deduplicate=true` |
| [deduplicate.field](/docs/services/discovery/query-parameters.html#deduplicated_field) | 
Deduplicar resultados retornados com base no campo | `deduplicate.field=title` |
| [collection_ids](/docs/services/discovery/query-parameters.html#collection_ids) | Consultar
múltiplas coleções | `collection_ids={1},{2},{3}` |

## Operadores
{: #operators}

Os operadores são os separadores entre diferentes partes de uma consulta. Estes são os operadores
disponíveis:

| Operador | Descrição | Exemplo |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [.](/docs/services/discovery/query-operators.html#delimiter) | delimitador JSON | `enriched_text.concepts.text` |
| [:](/docs/services/discovery/query-operators.html#includes) | Inclui | `text:computer` |
| [::](/docs/services/discovery/query-operators.html#match) | Correspondência exata | `title::Query building` |
| [:!](/docs/services/discovery/query-operators.html#notinclude) | Não inclui | `text:!computer` |
| [::!](/docs/services/discovery/query-operators.html#notamatch) | Não é uma combinação exata | `title::!Query building` |
| [\\](/docs/services/discovery/query-operators.html#escape) | Caractere de escape | `enriched_text.entitle.text:Trinidad \& Tobago` |
| [""](/docs/services/discovery/query-operators.html#phrase) | Consulta de frase | `enriched_text.concepts.text:"IBM Watson"` |
| [(), \[\]](/docs/services/discovery/query-operators.html#nestedquery) | Agrupamento aninhado | `filter-entities:(text:Turkey,type:Location)` |
| [<code>&#124;</code>](/docs/services/discovery/query-operators.html#or) | ou | <code>query-enriched.entities.text:Google&#124;IBM</code> |
| [,](/docs/services/discovery/query-operators.html#and) | e | `query-enriched.entities.text:Google,IBM` |
| [<=, >=, >, <](/docs/services/discovery/query-operators.html#comparisons) | Comparações numéricas |  `enriched_text.sentiment.document.score>0.679`     |
| [^x](/docs/services/discovery/query-operators.html#multiplier) | Multiplicador de pontuação | `text:IBM^3` |
| [*](/docs/services/discovery/query-operators.html#wildcard) | Curinga | `query-enriched_text.concepts.text:pre*` |
| [~n](/docs/services/discovery/query-operators.html#variation) | Variação de sequência | `query-enriched_text.entities.text:cat~1` |

## Agregações
{: #aggregations}

As agregações retornam um conjunto de valores de dados. Estas são as agregações disponíveis:

| Agregação | Descrição | Exemplo |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [term](/docs/services/discovery/query-aggregations.html#term) | Contagem de valores
idênticos | `term(enriched_text.concepts.text,count:10)` |
| [filter](/docs/services/discovery/query-aggregations.html#filter) | Filtrar
conjunto de resultados para o padrão definido | `filter(enriched_text.concepts.text:cloud computing)`
| [nested](/docs/services/discovery/query-aggregations.html#nested) | Restringir agregação | `nested(enriched_text.entities)` |
| [histogram](/docs/services/discovery/query-aggregations.html#histogram) | Distribuição
baseada em intervalo | `histogram(product.price,interval:1)` |
| [timeslice](/docs/services/discovery/query-aggregations.html#timeslice) | Distribuição
baseada em tempo | `timeslice(last_modified,2day,America/New York)` |
| [top_hits](/docs/services/discovery/query-aggregations.html#top_hits) | Principais
documentos de resultados classificados para a agregação atual | `term(enriched_text.concepts.text).top_hits(10)` |
| [unique_count](/docs/services/discovery/query-aggregations.html#unique_count) | Contagem de
valores exclusivos para um campo dentro de uma agregação | `unique_count(enriched_text.entities.type)` |
| [max](/docs/services/discovery/query-aggregations.html#min) | O valor máximo para o campo
especificado no conjunto de resultados. | `max(product.price)` |
| [min](/docs/services/discovery/query-aggregations.html#max) | Valor mínimo para o campo
especificado no conjunto de resultados. | `min(product.price)` |
| [average](/docs/services/discovery/query-aggregations.html#average) |Valor médio para o
campo especificado no conjunto de resultados. | `average(product.price)` |
| [sum](/docs/services/discovery/query-aggregations.html#sum) | Soma de todos os campos no
conjunto de resultados. | `sum(product.price)` |
