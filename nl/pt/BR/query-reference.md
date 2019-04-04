---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-04"

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

# Referência de Consulta
{: #query-reference}

O serviço do {{site.data.keyword.discoveryfull}} oferece poderosos recursos de pesquisa de conteúdo por meio de consultas. Após seu conteúdo ser transferido por upload e enriquecido pelo serviço do {{site.data.keyword.discoveryshort}}, será possível construir consultas, integrar o{{site.data.keyword.discoveryshort}} em seus próprios projetos ou criar um aplicativo customizado usando o {{site.data.keyword.watson}} Explorer Application Builder.
{: shortdesc}

Para obter informações sobre como criar consultas, consulte:
- [Introdução à consulta](/docs/services/discovery?topic=discovery-getting-started-with-querying#getting-started-with-querying)
- [Conceitos de consulta](/docs/services/discovery?topic=discovery-query-concepts#query-concepts)

## Descrições de Parâmetros
{: #parameter-descriptions}

Os parâmetros de consulta permitem procurar pela sua coleção, identificar um conjunto de
resultados e executar análise no conjunto de resultados.


| Parâmetros | Descrição | Exemplo |
|:-------------------:|------------------------------------------------------------|--------------------------------|
|** Parâmetros de procura **|  |  |
| [query](/docs/services/discovery?topic=discovery-query-parameters#query) | Uma procura de linguagem de
consulta classificada para documentos correspondentes. | `query=bees` |
| [filter](/docs/services/discovery?topic=discovery-query-parameters#filter) | Uma procura de linguagem
de consulta não classificada para documentos correspondentes. | `filter=bees` |
| [natural_language_query](/docs/services/discovery?topic=discovery-query-parameters#nlq) | Uma procura
de linguagem natural classificada para documentos correspondentes | `natural_language_query="How do bees fly"` |
| [aggregation](/docs/services/discovery?topic=discovery-query-parameters#aggregation) | Uma consulta
de estatística do conjunto de resultados | `aggregation=term(enriched_text.entities.type)` |
| **Parâmetros de estrutura** | | |
| [count](/docs/services/discovery?topic=discovery-query-parameters#count) | O número de
documentos `result` a serem retornados. | `count=15` |
| [offset](/docs/services/discovery?topic=discovery-query-parameters#offset) | O número de resultados a
serem ignorados antes de retornar documentos `result` por meio do conjunto de resultados | `offset=100` |
| [return](/docs/services/discovery?topic=discovery-query-parameters#return) | Lista de campos a
serem retornados | `return=title,url` |
| [sort](/docs/services/discovery?topic=discovery-query-parameters#sort) | Campo pelo qual o
conjunto de resultados será classificado | `sort=enriched_text.sentiment.document.score` |
| [bias](/docs/services/discovery?topic=discovery-query-parameters#bias) | Campo para resultados de envios configurados por | `bias=publication_date` |
| [passages.fields](/docs/services/discovery?topic=discovery-query-parameters#passages_fields) | Campos
dos quais passagens serão extraídas | `passages=true&passages.fields=text,abstract,conclusion` |
| [passages.count](/docs/services/discovery?topic=discovery-query-parameters#passages_count) | Número de
passagens a serem retornadas | `passages=true&passages.count=6` |
| [passages.characters](/docs/services/discovery?topic=discovery-query-parameters#passages_characters) | Duração das passagens | `passages=true&passages.characters=144` |
| [highlight](/docs/services/discovery?topic=discovery-query-parameters#highlight) | Destacar
correspondências de consulta | `highlight=true` |
| [deduplicate](/docs/services/discovery?topic=discovery-query-parameters#deduplicate) | Deduplicar
resultados retornados do {{site.data.keyword.discoverynewsfull}} | `deduplicate=true` |
| [deduplicate.field](/docs/services/discovery?topic=discovery-query-parameters#deduplicate_field) | Deduplicar resultados retornados com base no campo | `deduplicate.field=title` |
| [collection_ids](/docs/services/discovery?topic=discovery-query-parameters#collection_ids) | Consultar
múltiplas coleções | `collection_ids={1},{2},{3}` |
| [similar](/docs/services/discovery?topic=discovery-query-parameters#similar) | Ativa a descoberta de documento semelhante | `similar=true` |
| [similar.document_ids](/docs/services/discovery?topic=discovery-query-parameters#similar_document_ids) | A quais documentos localizar documentos semelhantes | `similar.document_ids={id1},{id2}` |
| [similar.fields](/docs/services/discovery?topic=discovery-query-parameters#similar_fields) | Quais campos comparar ao localizar documentos semelhantes | `similar.fields=text,title` |

### Limitações de consulta
{: #query-limitations}

Não é possível consultar nomes de campos que contêm o seguinte:
- Caracteres numéricos (`0 - 9`) no sufixo do nome do campo (por exemplo, `extracted-content2`).
- Os caracteres `_`, `+` e `-` no prefixo do `field_name` (por exemplo, `+extracted-content`).
- Os caracteres `.`, `,` e `:` no `field_name` (por exemplo, `new:extracted-content`)

## Operadores
{: #operators}

Os operadores são os separadores entre diferentes partes de uma consulta. Estes são os operadores
disponíveis:

| Operador | Descrição | Exemplo |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [.](/docs/services/discovery?topic=discovery-query-operators#delimiter) | delimitador JSON | `enriched_text.concepts.text` |
| [:](/docs/services/discovery?topic=discovery-query-operators#includes) | Inclui | `text:computer` |
| [::](/docs/services/discovery?topic=discovery-query-operators#match) | Correspondência exata | `title::"Query building"` |
| [:!](/docs/services/discovery?topic=discovery-query-operators#notinclude) | Não inclui | `text:!computer` |
| [::!](/docs/services/discovery?topic=discovery-query-operators#notamatch) | Não é uma combinação exata | `text::!winter` |
| [\\](/docs/services/discovery?topic=discovery-query-operators#escape) | Caractere de escape | `title::"Dorothy said: \"There's no place like home\""` |
| [""](/docs/services/discovery?topic=discovery-query-operators#phrase) | Consulta de frase | `enriched_text.concepts.text:"IBM Watson"` |
| [(), \[\]](/docs/services/discovery?topic=discovery-query-operators#nestedquery) | Agrupamento aninhado | `filter-entities:(text:Turkey,type:Location)` |
| [<code>&#124;</code>](/docs/services/discovery?topic=discovery-query-operators#or) | ou | <code>query-enriched.entities.text:Google&#124;IBM</code> |
| [,](/docs/services/discovery?topic=discovery-query-operators#and) | e | `query-enriched.entities.text:Google,IBM` |
| [<=, >=, >, <](/docs/services/discovery?topic=discovery-query-operators#comparisons) | Comparações numéricas |  `enriched_text.sentiment.document.score>0.679`     |
| [^x](/docs/services/discovery?topic=discovery-query-operators#multiplier) | Multiplicador de pontuação | `text:IBM^3` |
| [*](/docs/services/discovery?topic=discovery-query-operators#wildcard) | Curinga | `query-enriched_text.concepts.text:pre*` |
| [~n](/docs/services/discovery?topic=discovery-query-operators#variation) | Variação de sequência | `query-enriched_text.entities.text:cat~1` |
| [:*](/docs/services/discovery?topic=discovery-query-operators#exists) | Existe | `title:*` |
| [!*](/docs/services/discovery?topic=discovery-query-operators#dnexist) | Não existe | `title!*` |

## Agregações
{: #aggregations}

As agregações retornam um conjunto de valores de dados. Estas são as agregações disponíveis:

| Agregação | Descrição | Exemplo |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [term](/docs/services/discovery?topic=discovery-query-aggregations#term) | Contagem de valores
idênticos | `term(enriched_text.concepts.text,count:10)` |
| [filter](/docs/services/discovery?topic=discovery-query-aggregations#aggfilter) | Filtrar
conjunto de resultados para o padrão definido | `filter(enriched_text.concepts.text:cloud computing)`
| [nested](/docs/services/discovery?topic=discovery-query-aggregations#nested) | Restringir agregação | `nested(enriched_text.entities)` |
| [histogram](/docs/services/discovery?topic=discovery-query-aggregations#histogram) | Distribuição
baseada em intervalo | `histogram(product.price,interval:1)` |
| [timeslice](/docs/services/discovery?topic=discovery-query-aggregations#timeslice) | Distribuição
baseada em tempo | `timeslice(last_modified,2day,America/New York)` |
| [top_hits](/docs/services/discovery?topic=discovery-query-aggregations#top_hits) | Principais
documentos de resultados classificados para a agregação atual | `term(enriched_text.concepts.text).top_hits(10)` |
| [unique_count](/docs/services/discovery?topic=discovery-query-aggregations#unique_count) | Contagem de
valores exclusivos para um campo dentro de uma agregação | `unique_count(enriched_text.entities.type)` |
| [max](/docs/services/discovery?topic=discovery-query-aggregations#max) | O valor máximo para o campo
especificado no conjunto de resultados. | `max(product.price)` |
| [min](/docs/services/discovery?topic=discovery-query-aggregations#min) | Valor mínimo para o campo
especificado no conjunto de resultados. | `min(product.price)` |
| [average](/docs/services/discovery?topic=discovery-query-aggregations#average) |Valor médio para o
campo especificado no conjunto de resultados. | `average(product.price)` |
| [sum](/docs/services/discovery?topic=discovery-query-aggregations#sum) | Soma de todos os campos no
conjunto de resultados. | `sum(product.price)` |
