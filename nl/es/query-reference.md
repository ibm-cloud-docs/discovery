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

# Referencia de consultas
{: #query-reference}

El servicio {{site.data.keyword.discoveryfull}} ofrece potentes funciones de búsqueda de contenido a través de las consultas. Después de que el contenido se haya cargado y el servicio {{site.data.keyword.discoveryshort}} lo haya enriquecido, puede crear consultas, integrar {{site.data.keyword.discoveryshort}} en sus propios proyectos o crear una aplicación personalizada utilizando {{site.data.keyword.watson}} Explorer Application Builder.
{: shortdesc}

Para obtener más información sobre cómo escribir consultas, consulte:
- [Iniciación a la creación de consultas](/docs/services/discovery?topic=discovery-getting-started-with-querying#getting-started-with-querying)
- [Conceptos de consultas](/docs/services/discovery?topic=discovery-query-concepts#query-concepts)

## Descripciones de parámetros
{: #parameter-descriptions}

Los parámetros de consulta permiten buscar en la recopilación, identificar un conjunto de resultados, y realizar análisis sobre dicho conjunto de resultados.


| Parámetro | Descripción | Ejemplo |
|:-------------------:|------------------------------------------------------------|--------------------------------|
|**Parámetros de búsqueda**|  |  |
| [query](/docs/services/discovery?topic=discovery-query-parameters#query) | Búsqueda de lenguaje de consulta clasificada para buscar documentos coincidentes. | `query=bees` |
| [filter](/docs/services/discovery?topic=discovery-query-parameters#filter) | Búsqueda de lenguaje de consulta no clasificada para buscar documentos coincidentes. | `filter=bees` |
| [natural_language_query](/docs/services/discovery?topic=discovery-query-parameters#nlq) | Búsqueda de lenguaje natural clasificada para buscar documentos coincidentes. | `natural_language_query="How do bees fly"` |
| [aggregation](/docs/services/discovery?topic=discovery-query-parameters#aggregation) | Consulta estadística del conjunto de resultados | `aggregation=term(enriched_text.entities.type)` |
| **Parámetros de estructura** | | |
| [count](/docs/services/discovery?topic=discovery-query-parameters#count) | Número de `result` documentos a devolver. | `count=15` |
| [offset](/docs/services/discovery?topic=discovery-query-parameters#offset) | Número de resultados a ignorar antes de devolver `result` documentos del conjunto de resultados. | `offset=100` |
| [return](/docs/services/discovery?topic=discovery-query-parameters#return) | Lista de campos a devolver | `return=title,url` |
| [sort](/docs/services/discovery?topic=discovery-query-parameters#sort) | Campo por el que clasificar los resultados | `sort=enriched_text.sentiment.document.score` |
| [bias](/docs/services/discovery?topic=discovery-query-parameters#bias) | Campo por el que se inclinan los resultados | `bias=publication_date` |
| [passages.fields](/docs/services/discovery?topic=discovery-query-parameters#passages_fields) | Campos de los que extraer pasajes | `passages=true&passages.fields=text,abstract,conclusion` |
| [passages.count](/docs/services/discovery?topic=discovery-query-parameters#passages_count) | Número de pasajes a devolver | `passages=true&passages.count=6` |
| [passages.characters](/docs/services/discovery?topic=discovery-query-parameters#passages_characters) | Longitud de los pasajes | `passages=true&passages.characters=144` |
| [highlight](/docs/services/discovery?topic=discovery-query-parameters#highlight) | Resaltar coincidencias de consultas | `highlight=true` |
| [deduplicate](/docs/services/discovery?topic=discovery-query-parameters#deduplicate) | Desduplicar resultados devueltos de {{site.data.keyword.discoverynewsfull}} | `deduplicate=true` |
| [deduplicate.field](/docs/services/discovery?topic=discovery-query-parameters#deduplicate_field) | Desduplicar resultados devueltos con base a un campo | `deduplicate.field=title` |
| [collection_ids](/docs/services/discovery?topic=discovery-query-parameters#collection_ids) | Consultar varias recopilaciones | `collection_ids={1},{2},{3}` |
| [similar](/docs/services/discovery?topic=discovery-query-parameters#similar) | Habilita la búsqueda de un documento similar | `similar=true` |
| [similar.document_ids](/docs/services/discovery?topic=discovery-query-parameters#similar_document_ids) | Los documentos para encontrar documentos similares | `similar.document_ids={id1},{id2}` |
| [similar.fields](/docs/services/discovery?topic=discovery-query-parameters#similar_fields) | Los campos para comparar al buscar documentos similares | `similar.fields=text,title` |

### Limitaciones en las consultas
{: #query-limitations}

No puede consultar los nombres de campo que contienen lo siguiente:
- Caracteres numéricos (`0 - 9`) en el sufijo del nombre de campo (por ejemplo `extracted-content2`).
- Los caracteres `_`, `+` y `-` en el prefijo de `field_name` (por ejemplo `+extracted-content`).
- Los caracteres `.`, `,` y `:` en `field_name` (por ejemplo `new:extracted-content`)

## Operadores
{: #operators}

Los operadores son los separadores entre diferentes partes de una consulta. Estos son los operadores disponibles:

| Operador | Descripción | Ejemplo |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [.](/docs/services/discovery?topic=discovery-query-operators#delimiter) | Delimitador JSON | `enriched_text.concepts.text` |
| [:](/docs/services/discovery?topic=discovery-query-operators#includes) | Incluye | `text:computer` |
| [::](/docs/services/discovery?topic=discovery-query-operators#match) | Coincidencia exacta | `title::"Query building"` |
| [:!](/docs/services/discovery?topic=discovery-query-operators#notinclude) | No incluye | `text:!computer` |
| [::!](/docs/services/discovery?topic=discovery-query-operators#notamatch) | No es una coincidencia exacta | `text::!winter` |
| [\\](/docs/services/discovery?topic=discovery-query-operators#escape) | Carácter de escape | `title::"Dorothy said: \"There's no place like home\""` |
| [""](/docs/services/discovery?topic=discovery-query-operators#phrase) | Consulta de frase | `enriched_text.concepts.text:"IBM Watson"` |
| [(), \[\]](/docs/services/discovery?topic=discovery-query-operators#nestedquery) | Agrupación anidada | `filter-entities:(text:Turkey,type:Location)` |
| [<code>&#124;</code>](/docs/services/discovery?topic=discovery-query-operators#or) | or | <code>query-enriched.entities.text:Google&#124;IBM</code> |
| [,](/docs/services/discovery?topic=discovery-query-operators#and) | y | `query-enriched.entities.text:Google,IBM` |
| [<=, >=, >, <](/docs/services/discovery?topic=discovery-query-operators#comparisons) | Comparaciones numéricas |  `enriched_text.sentiment.document.score>0.679`     |
| [^x](/docs/services/discovery?topic=discovery-query-operators#multiplier) | Multiplicador de puntuación | `text:IBM^3` |
| [*](/docs/services/discovery?topic=discovery-query-operators#wildcard) | Comodín | `query-enriched_text.concepts.text:pre*` |
| [~n](/docs/services/discovery?topic=discovery-query-operators#variation) | Variación de serie | `query-enriched_text.entities.text:cat~1` |
| [:*](/docs/services/discovery?topic=discovery-query-operators#exists) | Existe | `title:*` |
| [!*](/docs/services/discovery?topic=discovery-query-operators#dnexist) | No existe | `title!*` |

## Agregaciones
{: #aggregations}

Las agregaciones devuelven un conjunto de valores de datos. Estas son las agregaciones disponibles:

| Agregación | Descripción | Ejemplo |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [term](/docs/services/discovery?topic=discovery-query-aggregations#term) | Recuento de valores idénticos | `term(enriched_text.concepts.text,count:10)` |
| [filter](/docs/services/discovery?topic=discovery-query-aggregations#aggfilter) | Filtrar conjuntos de resultados para un patrón definido | `filter(enriched_text.concepts.text:cloud computing)`
| [nested](/docs/services/discovery?topic=discovery-query-aggregations#nested) | Restringir agregación | `nested(enriched_text.entities)` |
| [histogram](/docs/services/discovery?topic=discovery-query-aggregations#histogram) | Distribución basada en intervalos | `histogram(product.price,interval:1)` |
| [timeslice](/docs/services/discovery?topic=discovery-query-aggregations#timeslice) | Distribución basada en tiempo | `timeslice(last_modified,2day,America/New York)` |
| [top_hits](/docs/services/discovery?topic=discovery-query-aggregations#top_hits) | Documentos de resultados clasificados superiores para la agregación actual | `term(enriched_text.concepts.text).top_hits(10)` |
| [unique_count](/docs/services/discovery?topic=discovery-query-aggregations#unique_count) | Recuento de valores exclusivos para un campo dentro de una agregación | `unique_count(enriched_text.entities.type)` |
| [max](/docs/services/discovery?topic=discovery-query-aggregations#max) | Valor máximo para el campo especificado en el conjunto de resultados. | `max(product.price)` |
| [min](/docs/services/discovery?topic=discovery-query-aggregations#min) | Valor mínimo para el campo especificado en el conjunto de resultados. | `min(product.price)` |
| [average](/docs/services/discovery?topic=discovery-query-aggregations#average) |Valor medio para el campo especificado en el conjunto de resultados. | `average(product.price)` |
| [sum](/docs/services/discovery?topic=discovery-query-aggregations#sum) | Suma de todos los campos en el conjunto de resultados. | `sum(product.price)` |
