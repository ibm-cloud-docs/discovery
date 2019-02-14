---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-09"

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

# Aggregazioni di query
{: #query-aggregations}

Le aggregazioni restituiscono una serie di valori di dati. Per l'elenco completo delle aggregazioni disponibili, vedi la [Guida di riferimento per le query](/docs/services/discovery/query-reference.html#aggregations).

## term
{: #term}

Restituisce i valori principali (in base al punteggio e alla frequenza) per gli arricchimenti selezionati. Tutti gli arricchimenti sono valori validi. Puoi facoltativamente utilizzare `count` per specificare il numero di termini da restituire. Il parametro `count` ha un valore predefinito di 10. Questo esempio restituisce il testo completo e gli arricchimenti dei valori principali con l'arricchimento concept e specifica di restituire 10 termini.

Ad esempio:
```bash
term(enriched_text.concepts.text,count:10)
```
{: codeblock}

## filter
{: #filter}

Un modificatore che restringerà l'insieme di documenti della query di aggregazione che precede. Questo esempio applica un filtro che riduce l'insieme di documenti a quelli che includono il concetto "cloud computing".

Ad esempio:
```bash
filter(enriched_text.concepts.text:"cloud computing")
```
{: codeblock}

## nested
{: #nested}

L'aggiunta di nested prima di una query di aggregazione limita l'aggregazione all'area dei risultati specificati. Ad esempio, `nested(enriched_text.entities)` significa che solo i componenti `enriched_text.entities` di qualsiasi risultato vengono utilizzati come base per l'esecuzione dell'aggregazione.

Ad esempio:
```bash
nested(enriched_text.entities)
```
{: codeblock}

## histogram
{: #histogram}

Crea segmenti di intervallo numerico per categorizzare i documenti. Utilizza i valori campo da un singolo campo numerico per descrivere la categoria. Il campo utilizzato per creare l'istogramma deve essere di tipo numerico (`integer`, `float`, `double` oppure `date`). I tipi non numerici quali `string` non sono supportati. Ad esempio, "price": 1,30 è un valore numerico che funziona, mentre "price": "1,30" è una stringa e quindi non funzionerà. Utilizza l'argomento `interval` per definire la dimensione delle sezioni in cui vengono suddivisi i risultati. I valori di intervallo devono essere numeri interi e non negativi e sono impostati per avere un senso logico per la segmentazione dei tuoi possibili valori di campo. Ad esempio, se il tuo insieme di dati include il prezzo di diversi articoli, come: “price”: 1,30, “price”: 1,99, e “price”: 2,99, puoi utilizzare degli intervalli di 1 in modo da vedere tutto raggruppato tra 1 e 2 e 2 e 3. Probabilmente non userai un intervallo di 100 perché in quel caso tutti i dati finirebbero nello stesso segmento. Gli istogrammi possono elaborare i valori decimali ma gli intervalli devono essere numeri interi. La sintassi è `histogram(<field>,<interval>)`, come mostrato nel seguente esempio.

Ad esempio:
```bash
histogram(product.price,interval:1)
```
{: codeblock}

## timeslice
{: #timeslice}

Un istogramma specializzato che utilizza le date per creare segmenti di intervallo. I valori di intervallo di date validi sono `second/seconds` `minute/minutes`, `hour/hours`, `day/days`, `week/weeks`, `month/months` e `year/years`. La sintassi è `timeslice(<field>,<interval>,<time_zone>)`. Per utilizzare `timeslice`, i campi di tempo nei tuoi documenti devono essere del tipo di dati `date` e in formato [UNIX time ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://en.wikipedia.org/wiki/Unix_time){: new_window}. A meno che non vengano soddisfatti entrambi questi requisiti, il parametro `timeslice` non funziona correttamente. Puoi creare un intervallo di tempo se i tuoi documenti contengono campi `date` con valori quali `1496228512`. Il valore deve essere in formato numerico (ad esempio `float` o `double`) e non racchiuso tra virgolette. Il servizio tratta le date in formato testuale e le date in formato ISO 8601 come tipo di dati `string`, non come tipo di dati `date`. Puoi rilevare i punti anomali nelle aggregazioni timeslice. Per ulteriori informazioni, vedi [Rilevamento di anomalie di intervallo di tempo](#anomaly-detection). Questo esempio restituisce valori per "sales" ("product.sales") a intervalli di 2 giorni nel fuso orario della città di New York.

Ad esempio:
```bash
timeslice(product.sales,2day,America/New York)
```
{: codeblock}

### Rilevamento di anomalie di intervallo di tempo
{: #anomaly-detection}

Puoi facoltativamente applicare il rilevamento di anomalie ai risultati di un'aggregazione `timeslice`. Il rilevamento di anomalie viene utilizzato per individuare dei punti di dati insoliti entro una serie temporale e per contrassegnarli per un'ulteriore revisione. Degli utilizzi di esempio per il rilevamento di anomalie includono l'identificazione di picchi nell'utilizzo di carte di credito e la ricerca in Watson Discovery News di gruppi di articoli relativi a uno specifico argomento.

Per applicare il rilevamento di anomalie, utilizza la seguente sintassi nella tua aggregazione:

```bash
timeslice(field:<date>,interval:<interval>,anomaly:true)`
```
{: codeblock}

Se specifichi `anomaly:true` con l'aggregazione `timeslice`, l'output include i seguenti due campi aggiuntivi, che sono visualizzati nell'esempio.

  - `"anomaly": true` per indicare che il rilevamento di anomalie è stato eseguito
  - Un campo `anomaly` nei punti anomali nell'array di risultati dell'output. Il campo anomaly ha un valore del tipo di dati `float` che indica la magnitudine della modalità di funzionamento anomala. Più prossimo a `1` è il valore del campo anomaly e maggiore è la probabilità che il risultato sia anomalo.

  - `key` e `key_as_string` in ciascuno degli oggetti nell'array `results` corrispondono a una data/ora UNIX espressa in secondi.
  - Il punteggio di anomalia è relativo a una query, non a tutte le query.

```json
"type": "timeslice",
"field": "blekko.chrondate",
"interval": "1d",
"anomaly": true,
"results": [
  {
    "matching_results": 2933,
    "anomaly": 1,
    "key_as_string": "1496880000",
    "key": 1496880000000
  },
  {
    "matching_results": 3435,
    "anomaly": 1,
    "key_as_string": "1496966400",
    "key": 1496966400000
  },
  {
    "matching_results": 3692,
    "anomaly": 0.598226,
    "key_as_string": "1496016000",
    "key": 1496016000000
  },
  {
    "matching_results": 4551,
    "anomaly": 0.828498,
    "key_as_string": "1495411200",
    "key": 1495411200000
  },
  {
    "matching_results": 947,
    "key_as_string": "1489968000",
    "key": 1489968000000
  },
 ...
]
...
```
{: codeblock}

#### Limitazioni del rilevamento anomalie

- Il rilevamento anomalie è attualmente disponibile solo su aggregazioni `timeslice` di livello superiore. Non è disponibile nelle aggregazioni di livello inferiore (nested).
- Il numero massimo di punti che può essere elaborato dal rilevamento di anomalie in qualsiasi specifica aggregazione `timeslice` è `1500`.
- Il numero massimo di aggregazioni timeslice di livello superiore che può essere elaborato dal rilevamento di anomalie è `20`.

<!--
#### Anomaly detection workflow

The following example workflow detects an anomaly for the text entity `London` and retrieves additional information about the anomalous datapoint.

  1. Timeslice aggregation: `query=entities.text:London&count=0&aggregation=timeslice(blekko.last_crawled,1day,anomaly:true)`
  1. Term aggregation to retrieve top keywords: `query=entities.text:London&count=0&aggregation=term(keywords.text,count:5)&filter=blekko.last_crawled>=1490140800,<=1490227200`
  1. Query to retrieve top enriched title: `query=entities.text:London,keywords.text:Westminster Bridge|police officer|people|Prime Minister Theresa|parliament&count=1&filter=blekko.last_crawled>=1490140800,<=1490227200&return=enrichedTitle.text`
  -->

## top_hits
{: #top_hits}

Restituisce i documenti classificati in base al punteggio della query o dell'arricchimento. Può essere utilizzato con qualsiasi aggregazione o parametro di query. Questo esempio restituisce i 10 riscontri principali per un'aggregazione di termini.

Ad esempio:
```bash
term(enriched_text.concepts.text).top_hits(10)
```
{: codeblock}

## unique_count
{: #unique_count}

Restituisce un conteggio delle istanze univoche del campo specificato nella raccolta.

Esempi:
```bash
unique_count(enriched_text.keyword.text)
```
{: codeblock}

```bash
nested(enriched_text.entities).term(enriched_text.entities.text,count:3).unique_count(enriched_text.entities.type)
```
{: codeblock}

## max
{: #max}

Restituisce il valore più alto nel campo specificato su tutti i documenti corrispondenti.

Ad esempio:
```bash
max(product.price)
```
{: codeblock}

## min
{: #min}

Restituisce il valore più basso nel campo specificato su tutti i documenti corrispondenti.

Ad esempio:
```bash
min(product.price)
```
{: codeblock}

## average
{: #average}

Restituisce la media dei valori del campo specificato su tutti i documenti corrispondenti.

Ad esempio:
```bash
average(product.price)
```
{: codeblock}

## sum
{: #sum}

Aggiunge insieme i valori del campo specificato su tutti i documenti corrispondenti.

Ad esempio:
```bash
sum(product.price)
```
{: codeblock}
