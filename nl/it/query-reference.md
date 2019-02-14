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

# Guida di riferimento per le query

Il servizio {{site.data.keyword.discoveryfull}} offre potenti funzionalità di ricerca di contenuto tramite le query. Dopo che il tuo contenuto è stato caricato e arricchito dal servizio {{site.data.keyword.discoveryshort}}, puoi creare delle query e integrare {{site.data.keyword.discoveryshort}} nei tuoi progetti oppure creare un'applicazione personalizzata utilizzando il {{site.data.keyword.watson}} Explorer Application Builder.
{: shortdesc}

Per ulteriori informazioni relative alla scrittura di query, consulta:
- [Introduzione alle query](/docs/services/discovery/getting-started-query.html)
- [Concetti delle query](/docs/services/discovery/using.html)

## Descrizioni dei parametri
{: #parameter-descriptions}

I parametri di query ti consentono di eseguire ricerche nella tua raccolta, identificare una serie di risultati ed eseguire l'analisi sull'insieme di risultati.


| Parametro | Descrizione | Esempio |
|:-------------------:|------------------------------------------------------------|--------------------------------|
|** Parametri di ricerca **|  |  |
| [query](/docs/services/discovery/query-parameters.html#query) | Una ricerca in linguaggio di query classificata per i documenti che corrispondono. | `query=bees` |
| [filter](/docs/services/discovery/query-parameters.html#filter) | Una ricerca in linguaggio di query non classificata per i documenti che corrispondono. | `filter=bees` |
| [natural_language_query](/docs/services/discovery/query-parameters.html#nlq) | Una ricerca in linguaggio naturale classificata per i documenti che corrispondono. | `natural_language_query="How do bees fly"` |
| [aggregation](/docs/services/discovery/query-parameters.html#aggregation) | Una query statistica dell'insieme di risultati | `aggregation=term(enriched_text.entities.type)` |
| **Parametri di struttura** | | |
| [count](/docs/services/discovery/query-parameters.html#count) | Il numero di documenti `result` da restituire. | `count=15` |
| [offset](/docs/services/discovery/query-parameters.html#offset) | Il numero di risultati da ignorare prima di restituire i documenti `result` dall'insieme di risultati | `offset=100` |
| [return](/docs/services/discovery/query-parameters.html#return) | Elenco dei campi da restituire | `return=title,url` |
| [sort](/docs/services/discovery/query-parameters.html#sort) | Campo in base a cui ordinare l'insieme di risultati | `sort=enriched_text.sentiment.document.score` |
| [bias](/docs/services/discovery/query-parameters.html#bias) | Campo in base a cui orientare l'insieme di risultati | `bias=publication_date` |
| [passages.fields](/docs/services/discovery/query-parameters.html#passages_fields) | Campi da cui estrarre i passaggi | `passages=true&passages.fields=text,abstract,conclusion` |
| [passages.count](/docs/services/discovery/query-parameters.html#passages_count) | Numero di passaggi da restituire | `passages=true&passages.count=6` |
| [passages.characters](/docs/services/discovery/query-parameters.html#passages_characters) | Lunghezza dei passaggi | `passages=true&passages.characters=144` |
| [highlight](/docs/services/discovery/query-parameters.html#highlight) | Evidenzia le corrispondenze di query | `highlight=true` |
| [deduplicate](/docs/services/discovery/query-parameters.html#deduplicate) | Deduplica i risultati restituiti {{site.data.keyword.discoverynewsfull}} | `deduplicate=true` |
| [deduplicate.field](/docs/services/discovery/query-parameters.html#deduplicate_field) | Deduplica i risultati restituiti in base al campo | `deduplicate.field=title` |
| [collection_ids](/docs/services/discovery/query-parameters.html#collection_ids) | Esegui una query di più raccolte | `collection_ids={1},{2},{3}` |
| [similar](/docs/services/discovery/query-parameters.html#similar) | Abilita la ricerca di documenti simili | `similar=true` |
| [similar.document_ids](/docs/services/discovery/query-parameters.html#similar_document_ids) | Per quali documenti trovare documenti simili | `similar.document_ids={id1},{id2}` |
| [similar.fields](/docs/services/discovery/query-parameters.html#similar_fields) | Quali campi confrontare quando trovi documenti simili | `similar.fields=text,title` |

### Limitazioni delle query

Non puoi eseguire query sui nomi di campo che contengono quanto segue:
- Caratteri numerici (`0 - 9`) nel suffisso del nome di campo (ad esempio `extracted-content2`).
- I caratteri `_`, `+` e `-` nel prefisso del nome di campo (`field_name`) (ad esempio `+extracted-content`).
- I caratteri `.`, `,` e `:` nel nome di campo (`field_name`) (ad esempio `new:extracted-content`)

## Operatori
{: #operators}

Gli operatori sono i separatori tra le diverse parti di una query. Questi sono gli operatori disponibili:

| Operatore | Descrizione | Esempio |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [.](/docs/services/discovery/query-operators.html#delimiter) | Delimitatore JSON | `enriched_text.concepts.text` |
| [:](/docs/services/discovery/query-operators.html#includes) | Include | `text:computer` |
| [::](/docs/services/discovery/query-operators.html#match) | Corrispondenza esatta | `title::"Query building"` |
| [:!](/docs/services/discovery/query-operators.html#notinclude) | Non include | `text:!computer` |
| [::!](/docs/services/discovery/query-operators.html#notamatch) | Non una corrispondenza esatta | `text::!winter` |
| [\\](/docs/services/discovery/query-operators.html#escape) | Carattere di escape | `title::"Dorothy said: \"There's no place like home\""` |
| [""](/docs/services/discovery/query-operators.html#phrase) | Query di frasi | `enriched_text.concepts.text:"IBM Watson"` |
| [(), \[\]](/docs/services/discovery/query-operators.html#nestedquery) | Raggruppamento nidificato | `filter-entities:(text:Turkey,type:Location)` |
| [<code>&#124;</code>](/docs/services/discovery/query-operators.html#or) | o | <code>query-enriched.entities.text:Google&#124;IBM</code> |
| [,](/docs/services/discovery/query-operators.html#and) | e | `query-enriched.entities.text:Google,IBM` |
| [<=, >=, >, <](/docs/services/discovery/query-operators.html#comparisons) | Confronti numerici |  `enriched_text.sentiment.document.score>0.679`     |
| [^x](/docs/services/discovery/query-operators.html#multiplier) | Moltiplicatore del punteggio | `text:IBM^3` |
| [*](/docs/services/discovery/query-operators.html#wildcard) | Carattere jolly | `query-enriched_text.concepts.text:pre*` |
| [~n](/docs/services/discovery/query-operators.html#variation) | Variazione di stringa | `query-enriched_text.entities.text:cat~1` |
| [:*](/docs/services/discovery/query-operators.html#exists) | Esiste | `title:*` |
| [!*](/docs/services/discovery/query-operators.html#dnexist) | Non esiste | `title!*` |

## Aggregazioni
{: #aggregations}

Le aggregazioni restituiscono una serie di valori di dati. Queste sono le aggregazioni disponibili:

| Aggregazione | Descrizione | Esempio |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [term](/docs/services/discovery/query-aggregations.html#term) | Conteggio dei valori identici | `term(enriched_text.concepts.text,count:10)` |
| [filter](/docs/services/discovery/query-aggregations.html#filter) | I risultati del filtro impostati su un modello definito | `filter(enriched_text.concepts.text:cloud computing)`
| [nested](/docs/services/discovery/query-aggregations.html#nested) | Limita aggregazione | `nested(enriched_text.entities)` |
| [histogram](/docs/services/discovery/query-aggregations.html#histogram) | Distribuzione basata sull'intervallo | `histogram(product.price,interval:1)` |
| [timeslice](/docs/services/discovery/query-aggregations.html#timeslice) | Distribuzione basata sul tempo| `timeslice(last_modified,2day,America/New York)` |
| [top_hits](/docs/services/discovery/query-aggregations.html#top_hits) | I documenti dei risultati classificati più in alto per l'aggregazione attuale. | `term(enriched_text.concepts.text).top_hits(10)` |
| [unique_count](/docs/services/discovery/query-aggregations.html#unique_count) | Conteggio dei valori univoci per un campo all'interno di un'aggregazione | `unique_count(enriched_text.entities.type)` |
| [max](/docs/services/discovery/query-aggregations.html#max) | Valore massimo per il campo specificato nell'insieme di risultati.| `max(product.price)` |
| [min](/docs/services/discovery/query-aggregations.html#min) | Valore minimo per il campo specificato nell'insieme di risultati. | `min(product.price)` |
| [average](/docs/services/discovery/query-aggregations.html#average) |Valore medio per il campo specificato nell'insieme di risultati. | `average(product.price)` |
| [sum](/docs/services/discovery/query-aggregations.html#sum) | Somma di tutti i campi nell'insieme di risultati. | `sum(product.price)` |
