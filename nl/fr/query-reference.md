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

# Référence de requête
{: #query-reference}

Le service {{site.data.keyword.discoveryfull}} offre des fonctions de recherche de contenu puissantes par l'intermédiaire de requêtes. Une fois votre contenu téléchargé et enrichi par le service {{site.data.keyword.discoveryshort}}, vous pouvez créer des requêtes, intégrer {{site.data.keyword.discoveryshort}} dans vos propres projets ou créer une application personnalisée en utilisant {{site.data.keyword.watson}} Explorer Application Builder.
{: shortdesc}

Pour plus d'informations sur l'écriture de requêtes, voir :
- [Initiation à l'écriture de requêtes](/docs/services/discovery?topic=discovery-getting-started-with-querying#getting-started-with-querying)
- [Concepts de requête](/docs/services/discovery?topic=discovery-query-concepts#query-concepts)

## Description des paramètres
{: #parameter-descriptions}

Les paramètres de requête vous permettent d'effectuer des recherches dans votre collection, d'identifier un ensemble de résultats et d'analyser l'ensemble de résultats.


| Paramètre | Description | Exemple |
|:-------------------:|------------------------------------------------------------|--------------------------------|
|**Paramètres de recherche**|  |  |
| [query](/docs/services/discovery?topic=discovery-query-parameters#query) | Recherche classée de documents correspondants par l'intermédiaire d'un langage de requête | `query=bees` |
| [filter](/docs/services/discovery?topic=discovery-query-parameters#filter) | Recherche non classée de documents correspondants par l'intermédiaire d'un langage de requête | `filter=bees` |
| [natural_language_query](/docs/services/discovery?topic=discovery-query-parameters#nlq) | Recherche classée de documents correspondants par l'intermédiaire d'un langage naturel | `natural_language_query="How do bees fly"` |
| [aggregation](/docs/services/discovery?topic=discovery-query-parameters#aggregation) | Requête de statistique portant sur l'ensemble de résultats | `aggregation=term(enriched_text.entities.type)` |
| **Paramètres de structure** | | |
| [count](/docs/services/discovery?topic=discovery-query-parameters#count) | Nombre de documents `result` à renvoyer. | `count=15` |
| [offset](/docs/services/discovery?topic=discovery-query-parameters#offset) | Nombre de résultats à ignorer avant de renvoyer les documents `result` de l'ensemble de résultats | `offset=100` |
| [return](/docs/services/discovery?topic=discovery-query-parameters#return) | Liste des zones à renvoyer | `return=title,url` |
| [sort](/docs/services/discovery?topic=discovery-query-parameters#sort) | Zone à partir de laquelle trier l'ensemble de résultats | `sort=enriched_text.sentiment.document.score` |
| [bias](/docs/services/discovery?topic=discovery-query-parameters#bias) | Zone en fonction de laquelle pondérer l'ensemble de résultats | `bias=publication_date` |
| [passages.fields](/docs/services/discovery?topic=discovery-query-parameters#passages_fields) | Zones à partir desquelles extraire des passages | `passages=true&passages.fields=text,abstract,conclusion` |
| [passages.count](/docs/services/discovery?topic=discovery-query-parameters#passages_count) | Nombre de passages à renvoyer | `passages=true&passages.count=6` |
| [passages.characters](/docs/services/discovery?topic=discovery-query-parameters#passages_characters) | Longueur des passages | `passages=true&passages.characters=144` |
| [highlight](/docs/services/discovery?topic=discovery-query-parameters#highlight) | Mettre en évidence les correspondances de requête | `highlight=true` |
| [deduplicate](/docs/services/discovery?topic=discovery-query-parameters#deduplicate) | Dédoublonner les résultats renvoyés par {{site.data.keyword.discoverynewsfull}} | `deduplicate=true` |
| [deduplicate.field](/docs/services/discovery?topic=discovery-query-parameters#deduplicate_field) | Dédoublonner les résultats renvoyés en fonction des zones | `deduplicate.field=title` |
| [collection_ids](/docs/services/discovery?topic=discovery-query-parameters#collection_ids) | Exécuter une requête sur plusieurs collections | `collection_ids={1},{2},{3}` |
| [similar](/docs/services/discovery?topic=discovery-query-parameters#similar) | Active la recherche de documents similaires | `similar=true` |
| [similar.document_ids](/docs/services/discovery?topic=discovery-query-parameters#similar_document_ids) | Dans quels documents rechercher des documents similaires | `similar.document_ids={id1},{id2}` |
| [similar.fields](/docs/services/discovery?topic=discovery-query-parameters#similar_fields) | Quelles zones comparer lors de la recherche de documents similaires | `similar.fields=text,title` |

### Limitations affectant les requêtes
{: #query-limitations}

Vous ne pouvez pas effectuer de requête sur les noms de zone comportant les éléments suivants :
- Les caractères numériques (`0 - 9`) figurant dans le suffixe du nom de zone (par exemple, `extracted-content2`).
- Les caractères `_`, `+` et `-` figurant dans le préfixe du `field_name` (par exemple, `+extracted-content`).
- Les caractères `.`, `,` et `:` figurant dans le `field_name` (par exemple, `new:extracted-content`)

## Opérateurs
{: #operators}

Les opérateurs sont les séparateurs entre les différentes parties d'une requête. Les opérateurs disponibles sont les suivants :

| Opérateur | Description | Exemple |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [.](/docs/services/discovery?topic=discovery-query-operators#delimiter) | Délimiteur JSON | `enriched_text.concepts.text` |
| [:](/docs/services/discovery?topic=discovery-query-operators#includes) | Inclut | `text:computer` |
| [::](/docs/services/discovery?topic=discovery-query-operators#match) | Correspondance exacte | `title::"Query building"` |
| [:!](/docs/services/discovery?topic=discovery-query-operators#notinclude) | N'inclut pas | `text:!computer` |
| [::!](/docs/services/discovery?topic=discovery-query-operators#notamatch) | N'est pas une correspondance exacte | `text::!winter` |
| [\\](/docs/services/discovery?topic=discovery-query-operators#escape) | Caractère d'échappement | `title::"Dorothy said: \"There's no place like home\""` |
| [""](/docs/services/discovery?topic=discovery-query-operators#phrase) | Requête de phrase | `enriched_text.concepts.text:"IBM Watson"` |
| [(), \[\]](/docs/services/discovery?topic=discovery-query-operators#nestedquery) | Regroupement imbriqué | `filter-entities:(text:Turkey,type:Location)` |
| [<code>&#124;</code>](/docs/services/discovery?topic=discovery-query-operators#or) | ou | <code>query-enriched.entities.text:Google&#124;IBM</code> |
| [,](/docs/services/discovery?topic=discovery-query-operators#and) | et | `query-enriched.entities.text:Google,IBM` |
| [<=, >=, >, <](/docs/services/discovery?topic=discovery-query-operators#comparisons) | Comparaisons numériques |  `enriched_text.sentiment.document.score>0.679`     |
| [^x](/docs/services/discovery?topic=discovery-query-operators#multiplier) | Multiplicateur de score | `text:IBM^3` |
| [*](/docs/services/discovery?topic=discovery-query-operators#wildcard) | Caractère générique | `query-enriched_text.concepts.text:pre*` |
| [~n](/docs/services/discovery?topic=discovery-query-operators#variation) | Variation de chaîne | `query-enriched_text.entities.text:cat~1` |
| [:*](/docs/services/discovery?topic=discovery-query-operators#exists) | Existe | `title:*` |
| [!*](/docs/services/discovery?topic=discovery-query-operators#dnexist) | N'existe pas | `title!*` |

## Agrégations
{: #aggregations}

Les agrégations renvoient un ensemble de valeurs de données. Les agrégations disponibles sont les suivantes :

| Agrégation | Description | Exemple |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [term](/docs/services/discovery?topic=discovery-query-aggregations#term) | Nombre de valeurs identiques | `term(enriched_text.concepts.text,count:10)` |
| [filter](/docs/services/discovery?topic=discovery-query-aggregations#aggfilter) | Filtrer l'ensemble de résultats en fonction d'un modèle défini | `filter(enriched_text.concepts.text:cloud computing)`
| [nested](/docs/services/discovery?topic=discovery-query-aggregations#nested) | Restreindre l'agrégation | `nested(enriched_text.entities)` |
| [histogram](/docs/services/discovery?topic=discovery-query-aggregations#histogram) | Distribution basée sur un intervalle | `histogram(product.price,interval:1)` |
| [timeslice](/docs/services/discovery?topic=discovery-query-aggregations#timeslice) | Distribution basée sur le temps | `timeslice(last_modified,2day,America/New York)` |
| [top_hits](/docs/services/discovery?topic=discovery-query-aggregations#top_hits) | Premiers documents de résultats classés pour l'agrégation en cours | `term(enriched_text.concepts.text).top_hits(10)` |
| [unique_count](/docs/services/discovery?topic=discovery-query-aggregations#unique_count) | Nombre de valeurs uniques pour une zone dans une agrégation | `unique_count(enriched_text.entities.type)` |
| [max](/docs/services/discovery?topic=discovery-query-aggregations#max) | Valeur maximale de la zone spécifiée dans l'ensemble de résultats | `max(product.price)` |
| [min](/docs/services/discovery?topic=discovery-query-aggregations#min) | Valeur minimale de la zone spécifiée dans l'ensemble de résultats | `min(product.price)` |
| [average](/docs/services/discovery?topic=discovery-query-aggregations#average) |Valeur moyenne de la zone spécifiée dans l'ensemble de résultats | `average(product.price)` |
| [sum](/docs/services/discovery?topic=discovery-query-aggregations#sum) | Somme de toutes les zones dans l'ensemble de résultats | `sum(product.price)` |
