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

# Référence de requête
{: #query-reference}

Le service {{site.data.keyword.discoveryfull}} offre des fonctions de recherche de contenu puissantes par l'intermédiaire de requêtes. Une fois votre contenu téléchargé et enrichi par le service {{site.data.keyword.discoveryshort}}, vous pouvez créer des requêtes, intégrer {{site.data.keyword.discoveryshort}} dans vos propres projets ou créer une application personnalisée en utilisant {{site.data.keyword.watson}} Explorer Application Builder.
{: shortdesc}

Pour plus d'informations sur l'écriture de requêtes, voir :
- [Initiation à l'écriture de requêtes](/docs/services/discovery/getting-started-query.html)
- [Concepts de requête](/docs/services/discovery/using.html)

## Description des paramètres
{: #parameter-descriptions}

Les paramètres de requête vous permettent d'effectuer des recherches dans votre collection, d'identifier un ensemble de résultats et d'analyser l'ensemble de résultats.


| Paramètre | Description | Exemple |
|:-------------------:|------------------------------------------------------------|--------------------------------|
|**Paramètres de recherche**|  |  |
| [query](/docs/services/discovery/query-parameters.html#query) | Recherche classée de documents correspondants par l'intermédiaire d'un langage de requête | `query=bees` |
| [filter](/docs/services/discovery/query-parameters.html#filter) | Recherche non classée de documents correspondants par l'intermédiaire d'un langage de requête | `filter=bees` |
| [natural_language_query](/docs/services/discovery/query-parameters.html#nlq) | Recherche classée de documents correspondants par l'intermédiaire d'un langage naturel | `natural_language_query="How do bees fly"` |
| [aggregation](/docs/services/discovery/query-parameters.html#aggregation) | Requête de statistique portant sur l'ensemble de résultats | `aggregation=term(enriched_text.entities.type)` |
| **Paramètres de structure** | | |
| [count](/docs/services/discovery/query-parameters.html#count) | Nombre de documents `result` à renvoyer. | `count=15` |
| [offset](/docs/services/discovery/query-parameters.html#offset) | Nombre de résultats à ignorer avant de renvoyer les documents `result` de l'ensemble de résultats | `offset=100` |
| [return](/docs/services/discovery/query-parameters.html#return) | Liste des zones à renvoyer | `return=title,url` |
| [sort](/docs/services/discovery/query-parameters.html#sort) | Zone à partir de laquelle trier l'ensemble de résultats | `sort=enriched_text.sentiment.document.score` |
| [bias](/docs/services/discovery/query-parameters.html#bias) | Zone en fonction de laquelle pondérer l'ensemble de résultats | `bias=publication_date` |
| [passages.fields](/docs/services/discovery/query-parameters.html#passages_fields) | Zones à partir desquelles extraire des passages | `passages=true&passages.fields=text,abstract,conclusion` |
| [passages.count](/docs/services/discovery/query-parameters.html#passages_count) | Nombre de passages à renvoyer | `passages=true&passages.count=6` |
| [passages.characters](/docs/services/discovery/query-parameters.html#passages_characters) | Longueur des passages | `passages=true&passages.characters=144` |
| [highlight](/docs/services/discovery/query-parameters.html#highlight) | Mettre en évidence les correspondances de requête | `highlight=true` |
| [deduplicate](/docs/services/discovery/query-parameters.html#deduplicate) | Dédoublonner les résultats renvoyés par {{site.data.keyword.discoverynewsfull}} | `deduplicate=true` |
| [deduplicate.field](/docs/services/discovery/query-parameters.html#deduplicate_field) | Dédoublonner les résultats renvoyés en fonction des zones | `deduplicate.field=title` |
| [collection_ids](/docs/services/discovery/query-parameters.html#collection_ids) | Exécuter une requête sur plusieurs collections | `collection_ids={1},{2},{3}` |
| [similar](/docs/services/discovery/query-parameters.html#similar) | Active la recherche de documents similaires | `similar=true` |
| [similar.document_ids](/docs/services/discovery/query-parameters.html#similar_document_ids) | Dans quels documents rechercher des documents similaires | `similar.document_ids={id1},{id2}` |
| [similar.fields](/docs/services/discovery/query-parameters.html#similar_fields) | Quelles zones comparer lors de la recherche de documents similaires | `similar.fields=text,title` |

### Limitations affectant les requêtes

Vous ne pouvez pas effectuer de requête sur les noms de zone comportant les éléments suivants :
- Les caractères numériques (`0 - 9`) figurant dans le suffixe du nom de zone (par exemple, `extracted-content2`). 
- Les caractères `_`, `+` et `-` figurant dans le préfixe du `field_name` (par exemple, `+extracted-content`).
- Les caractères `.`, `,` et `:` figurant dans le `field_name` (par exemple, `new:extracted-content`)

## Opérateurs
{: #operators}

Les opérateurs sont les séparateurs entre les différentes parties d'une requête. Les opérateurs disponibles sont les suivants :

| Opérateur | Description | Exemple |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [.](/docs/services/discovery/query-operators.html#delimiter) | Délimiteur JSON | `enriched_text.concepts.text` |
| [:](/docs/services/discovery/query-operators.html#includes) | Inclut | `text:computer` |
| [::](/docs/services/discovery/query-operators.html#match) | Correspondance exacte | `title::"Query building"` |
| [:!](/docs/services/discovery/query-operators.html#notinclude) | N'inclut pas | `text:!computer` |
| [::!](/docs/services/discovery/query-operators.html#notamatch) | N'est pas une correspondance exacte | `text::!winter` |
| [\\](/docs/services/discovery/query-operators.html#escape) | Caractère d'échappement | `title::"Dorothy said: \"There's no place like home\""` |
| [""](/docs/services/discovery/query-operators.html#phrase) | Requête de phrase | `enriched_text.concepts.text:"IBM Watson"` |
| [(), \[\]](/docs/services/discovery/query-operators.html#nestedquery) | Regroupement imbriqué | `filter-entities:(text:Turkey,type:Location)` |
| [<code>&#124;</code>](/docs/services/discovery/query-operators.html#or) | ou | <code>query-enriched.entities.text:Google&#124;IBM</code> |
| [,](/docs/services/discovery/query-operators.html#and) | et | `query-enriched.entities.text:Google,IBM` |
| [<=, >=, >, <](/docs/services/discovery/query-operators.html#comparisons) | Comparaisons numériques |  `enriched_text.sentiment.document.score>0.679`     |
| [^x](/docs/services/discovery/query-operators.html#multiplier) | Multiplicateur de score | `text:IBM^3` |
| [*](/docs/services/discovery/query-operators.html#wildcard) | Caractère générique | `query-enriched_text.concepts.text:pre*` |
| [~n](/docs/services/discovery/query-operators.html#variation) | Variation de chaîne | `query-enriched_text.entities.text:cat~1` |
| [:*](/docs/services/discovery/query-operators.html#exists) | Existe | `title:*` |
| [!*](/docs/services/discovery/query-operators.html#dnexist) | N'existe pas | `title!*` |

## Agrégations
{: #aggregations}

Les agrégations renvoient un ensemble de valeurs de données. Les agrégations disponibles sont les suivantes :

| Agrégation | Description | Exemple |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [term](/docs/services/discovery/query-aggregations.html#term) | Nombre de valeurs identiques | `term(enriched_text.concepts.text,count:10)` |
| [filter](/docs/services/discovery/query-aggregations.html#filter) | Filtrer l'ensemble de résultats en fonction d'un modèle défini | `filter(enriched_text.concepts.text:cloud computing)`
| [nested](/docs/services/discovery/query-aggregations.html#nested) | Restreindre l'agrégation | `nested(enriched_text.entities)` |
| [histogram](/docs/services/discovery/query-aggregations.html#histogram) | Distribution basée sur un intervalle | `histogram(product.price,interval:1)` |
| [timeslice](/docs/services/discovery/query-aggregations.html#timeslice) | Distribution basée sur le temps | `timeslice(last_modified,2day,America/New York)` |
| [top_hits](/docs/services/discovery/query-aggregations.html#top_hits) | Premiers documents de résultats classés pour l'agrégation en cours | `term(enriched_text.concepts.text).top_hits(10)` |
| [unique_count](/docs/services/discovery/query-aggregations.html#unique_count) | Nombre de valeurs uniques pour une zone dans une agrégation | `unique_count(enriched_text.entities.type)` |
| [max](/docs/services/discovery/query-aggregations.html#max) | Valeur maximale de la zone spécifiée dans l'ensemble de résultats | `max(product.price)` |
| [min](/docs/services/discovery/query-aggregations.html#min) | Valeur minimale de la zone spécifiée dans l'ensemble de résultats | `min(product.price)` |
| [average](/docs/services/discovery/query-aggregations.html#average) |Valeur moyenne de la zone spécifiée dans l'ensemble de résultats | `average(product.price)` |
| [sum](/docs/services/discovery/query-aggregations.html#sum) | Somme de toutes les zones dans l'ensemble de résultats | `sum(product.price)` |
