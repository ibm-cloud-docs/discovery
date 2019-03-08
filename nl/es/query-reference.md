---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-04"

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

# Referencia de consultas
{: #query-reference}

El servicio {{site.data.keyword.discoveryfull}} ofrece potentes funciones de búsqueda de contenido a través de las consultas. Después de que el contenido se haya cargado y el servicio {{site.data.keyword.discoveryshort}} lo haya enriquecido, puede crear consultas, integrar {{site.data.keyword.discoveryshort}} en sus propios proyectos o crear una aplicación personalizada utilizando {{site.data.keyword.watson}} Explorer Application Builder.
{: shortdesc}

Para obtener más información sobre cómo escribir consultas, consulte:
- [Iniciación a la creación de consultas](/docs/services/discovery/getting-started-query.html)
- [Conceptos de consultas](/docs/services/discovery/using.html)

## Descripciones de parámetros
{: #parameter-descriptions}

Los parámetros de consulta permiten buscar en la recopilación, identificar un conjunto de resultados, y realizar análisis sobre dicho conjunto de resultados.


| Parámetro | Descripción | Ejemplo |
|:-------------------:|------------------------------------------------------------|--------------------------------|
|**Parámetros de búsqueda**|  |  |
| [query](/docs/services/discovery/query-parameters.html#query) | Búsqueda de lenguaje de consulta clasificada para buscar documentos coincidentes. | `query=bees` |
| [filter](/docs/services/discovery/query-parameters.html#filter) | Búsqueda de lenguaje de consulta no clasificada para buscar documentos coincidentes. | `filter=bees` |
| [natural_language_query](/docs/services/discovery/query-parameters.html#nlq) | Búsqueda de lenguaje natural clasificada para buscar documentos coincidentes. | `natural_language_query="How do bees fly"` |
| [aggregation](/docs/services/discovery/query-parameters.html#aggregation) | Consulta estadística del conjunto de resultados | `aggregation=term(enriched_text.entities.type)` |
| **Parámetros de estructura** | | |
| [count](/docs/services/discovery/query-parameters.html#count) | Número de `result` documentos a devolver. | `count=15` |
| [offset](/docs/services/discovery/query-parameters.html#offset) | Número de resultados a ignorar antes de devolver `result` documentos del conjunto de resultados. | `offset=100` |
| [return](/docs/services/discovery/query-parameters.html#return) | Lista de campos a devolver | `return=title,url` |
| [sort](/docs/services/discovery/query-parameters.html#sort) | Campo por el que clasificar los resultados | `sort=enriched_text.sentiment.document.score` |
| [bias](/docs/services/discovery/query-parameters.html#bias) | Campo por el que se inclinan los resultados | `bias=publication_date` |
| [passages.fields](/docs/services/discovery/query-parameters.html#passages_fields) | Campos de los que extraer pasajes | `passages=true&passages.fields=text,abstract,conclusion` |
| [passages.count](/docs/services/discovery/query-parameters.html#passages_count) | Número de pasajes a devolver | `passages=true&passages.count=6` |
| [passages.characters](/docs/services/discovery/query-parameters.html#passages_characters) | Longitud de los pasajes | `passages=true&passages.characters=144` |
| [highlight](/docs/services/discovery/query-parameters.html#highlight) | Resaltar coincidencias de consultas | `highlight=true` |
| [deduplicate](/docs/services/discovery/query-parameters.html#deduplicate) | Desduplicar resultados devueltos de {{site.data.keyword.discoverynewsfull}} | `deduplicate=true` |
| [deduplicate.field](/docs/services/discovery/query-parameters.html#deduplicate_field) | Desduplicar resultados devueltos con base a un campo | `deduplicate.field=title` |
| [collection_ids](/docs/services/discovery/query-parameters.html#collection_ids) | Consultar varias recopilaciones | `collection_ids={1},{2},{3}` |
| [similar](/docs/services/discovery/query-parameters.html#similar) | Habilita la búsqueda de un documento similar | `similar=true` |
| [similar.document_ids](/docs/services/discovery/query-parameters.html#similar_document_ids) | Los documentos para encontrar documentos similares | `similar.document_ids={id1},{id2}` |
| [similar.fields](/docs/services/discovery/query-parameters.html#similar_fields) | Los campos para comparar al buscar documentos similares | `similar.fields=text,title` |

### Limitaciones en las consultas

No puede consultar los nombres de campo que contienen lo siguiente:
- Caracteres numéricos (`0 - 9`) en el sufijo del nombre de campo (por ejemplo `extracted-content2`).
- Los caracteres `_`, `+` y `-` en el prefijo de `field_name` (por ejemplo `+extracted-content`).
- Los caracteres `.`, `,` y `:` en `field_name` (por ejemplo `new:extracted-content`)

## Operadores
{: #operators}

Los operadores son los separadores entre diferentes partes de una consulta. Estos son los operadores disponibles:

| Operador | Descripción | Ejemplo |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [.](/docs/services/discovery/query-operators.html#delimiter) | Delimitador JSON | `enriched_text.concepts.text` |
| [:](/docs/services/discovery/query-operators.html#includes) | Incluye | `text:computer` |
| [::](/docs/services/discovery/query-operators.html#match) | Coincidencia exacta | `title::"Query building"` |
| [:!](/docs/services/discovery/query-operators.html#notinclude) | No incluye | `text:!computer` |
| [::!](/docs/services/discovery/query-operators.html#notamatch) | No es una coincidencia exacta | `text::!winter` |
| [\\](/docs/services/discovery/query-operators.html#escape) | Carácter de escape | `title::"Dorothy said: \"There's no place like home\""` |
| [""](/docs/services/discovery/query-operators.html#phrase) | Consulta de frase | `enriched_text.concepts.text:"IBM Watson"` |
| [(), \[\]](/docs/services/discovery/query-operators.html#nestedquery) | Agrupación anidada | `filter-entities:(text:Turkey,type:Location)` |
| [<code>&#124;</code>](/docs/services/discovery/query-operators.html#or) | or | <code>query-enriched.entities.text:Google&#124;IBM</code> |
| [,](/docs/services/discovery/query-operators.html#and) | y | `query-enriched.entities.text:Google,IBM` |
| [<=, >=, >, <](/docs/services/discovery/query-operators.html#comparisons) | Comparaciones numéricas |  `enriched_text.sentiment.document.score>0.679`     |
| [^x](/docs/services/discovery/query-operators.html#multiplier) | Multiplicador de puntuación | `text:IBM^3` |
| [*](/docs/services/discovery/query-operators.html#wildcard) | Comodín | `query-enriched_text.concepts.text:pre*` |
| [~n](/docs/services/discovery/query-operators.html#variation) | Variación de serie | `query-enriched_text.entities.text:cat~1` |
| [:*](/docs/services/discovery/query-operators.html#exists) | Existe | `title:*` |
| [!*](/docs/services/discovery/query-operators.html#dnexist) | No existe | `title!*` |

## Agregaciones
{: #aggregations}

Las agregaciones devuelven un conjunto de valores de datos. Estas son las agregaciones disponibles:

| Agregación | Descripción | Ejemplo |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [term](/docs/services/discovery/query-aggregations.html#term) | Recuento de valores idénticos | `term(enriched_text.concepts.text,count:10)` |
| [filter](/docs/services/discovery/query-aggregations.html#filter) | Filtrar conjuntos de resultados para un patrón definido | `filter(enriched_text.concepts.text:cloud computing)`
| [nested](/docs/services/discovery/query-aggregations.html#nested) | Restringir agregación | `nested(enriched_text.entities)` |
| [histogram](/docs/services/discovery/query-aggregations.html#histogram) | Distribución basada en intervalos | `histogram(product.price,interval:1)` |
| [timeslice](/docs/services/discovery/query-aggregations.html#timeslice) | Distribución basada en tiempo | `timeslice(last_modified,2day,America/New York)` |
| [top_hits](/docs/services/discovery/query-aggregations.html#top_hits) | Documentos de resultados clasificados superiores para la agregación actual | `term(enriched_text.concepts.text).top_hits(10)` |
| [unique_count](/docs/services/discovery/query-aggregations.html#unique_count) | Recuento de valores exclusivos para un campo dentro de una agregación | `unique_count(enriched_text.entities.type)` |
| [max](/docs/services/discovery/query-aggregations.html#max) | Valor máximo para el campo especificado en el conjunto de resultados. | `max(product.price)` |
| [min](/docs/services/discovery/query-aggregations.html#min) | Valor mínimo para el campo especificado en el conjunto de resultados. | `min(product.price)` |
| [average](/docs/services/discovery/query-aggregations.html#average) |Valor medio para el campo especificado en el conjunto de resultados. | `average(product.price)` |
| [sum](/docs/services/discovery/query-aggregations.html#sum) | Suma de todos los campos en el conjunto de resultados. | `sum(product.price)` |
