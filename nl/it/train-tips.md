---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-03"

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

# Suggerimenti per la formazione della pertinenza
{: #relevancy-tips}

 Risposte alle domande comuni relative alla formazione di una raccolta e spiegazioni dei messaggi di errore e avvertenza comuni. Per ulteriori informazioni sul miglioramento della pertinenza di query in linguaggio naturale, vedi [Miglioramento della pertinenza dei risultati con la strumentazione](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling) e [Miglioramento della pertinenza dei risultati con l'API](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api).
{: shortdesc}

## Descrizione della formazione
{: #understanding-training}

Risposte alle domande comuni sulla formazione di una raccolta.

### Come faccio a sapere se il mio sistema è formato?
{: #understanding-system}

Utilizza il comando API [List collection details ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery#get-collection-details){: new_window} per verificare che il tuo sistema sia stato formato.  

```bash
curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07"
```
{: pre}

Risposta di esempio:

```json
{
  "training_status": {
    "data_updated": "2017-02-10T14:18:22.786Z",
    "total_examples": 54,
    "sufficient_label_diversity": false,
    "processing": false,
    "minimum_examples_added": true,
    "successfully_trained": "2017-02-08T14:18:22.786Z",
    "available": true,
    "notices": 13,
    "minimum_queries_added": true
    }
}
```

Per soddisfare i requisiti per la formazione, quanto qui di seguito indicato deve essere `true`:
- `minimum_queries_added`
- `minimum_examples_added`
- `sufficient_label_diversity`   

Nella risposta:
- `successfully_trained` indica che l'ultima volta la formazione è stata completata con esito positivo.
- `available: true` indica che la formazione ha avuto luogo e che è disponibile un modello.
- `processing: true` indica che la formazione è in corso.
-  Se la data `data_updated` è successiva alla data `successfully_trained`, un nuovo modello non è stato formato da quando è stato eseguito un recente caricamento di dati.  

### Come controllo gli errori e le avvertenze?
{: #understanding-errors}

Puoi utilizzare la [API di avvisi di query ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery#query-system-notices){: new_window} per visualizzare errori o avvertenze.  

```bash
curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/notices?version=2017-11-07"
```
{: pre}

Altre operazioni API sono elencate in [Esecuzione di altre operazioni di query di dati di formazione](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#training-data-operations).

### Come interpreto il punteggio `confidence` che compare nei risultati della query in linguaggio naturale dopo la formazione?
{: #interpret-confidence}

Per ulteriori informazioni, vedi il documento relativo ai [punteggi di affidabilità](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence).  

## Interpretazione di errori ed avvertenze
{: #interpreting-errors}

Spiegazioni dei messaggi di errore e avvertenza comuni

### Avvertenza: `Invalid training data found: The document was not returned in the top 100 search results for the given query, and will not be used for training`
{: #warning-docnotreturned}

Questa avvertenza è causata dai `document_id` nei tuoi dati di formazione che non corrispondono ai `document_id` in una ricerca eseguita sulla raccolta. Devi controllare le tue query e assicurarti che il `document_id`del documento che stai valutando sia restituito nei primi 100 risultati per tale query. In caso negativo, è opportuno che controlli due cose:  

- Se il documento non viene restituito nei primi 100 risultati, potrebbe non essere un buon esempio di un risultato di alta qualità ed è opportuno che rivedi perché questo documento era stato scelto.  

- Se il documento non viene affatto restituito, devi rivedere perché non viene restituito e appurare se c'è del testo nel documento che corrisponde a parti della query.  

**Nota:** questa avvertenza indica che potresti avere una o più query non valide; non è un'indicazione che la formazione non avrà luogo.  

### Errore: `Invalid training data found: Syntax error when parsing query`
{: #error-syntax}

- Ciò significa che c'è un problema con la sintassi effettiva della query. Convalida che le query restituiscano dei risultati e non generino un errore di sintassi. Ciò si può verificare solo se hai aggiunto un filtro alla tua query in linguaggio naturale.

### Errore: `Invalid training data found: The query string provided exceeds the maximum length, please provide a shorter one`
{: #error-exceedlength}

- La lunghezza massima della stringa di query è `2048`. Dovrai abbreviare la query specifica. Includere un filtro nella tua query è un modo per evitare questo problema.  

### Errore: `This collection cannot be trained: your plan does not support training on this many top-level text fields.`
{: #error-toplevelfields}

- Questo errore si verifica solo con i piani `Lite`. I campi di livello superiore sono campi che non sono nidificati sotto un altro campo. La formazione si verifica solo sui campi di livello superiore e ci sono dei limiti al numero di campi che può essere utilizzato nel processo di formazione. Più campi di alto livello fanno parte di una raccolta e più dati di formazione sono necessari. Inoltre, in casi in cui ci sono più di `10` campi di livello superiore, è probabile che la formazione riscontri degli errori. 

### Errore: `Training data quality standards not met: You will need additional training queries with labeled examples. (To be considered for training, each example must appear in the top 100 search results for its query.)`
{: #error-labels}

- Ciò significa che devi aggiungere ulteriori dati di formazione per eseguire correttamente la formazione. Hai bisogno come minimo di almeno 49 query di formazione univoche e ciascuna di esse ha bisogno di almeno un documento valutato. Il minimo non coincide con l'ottimale; la dimensione della raccolta e altri fattori possono aumentare il numero di esempi di formazione necessario per soddisfare il minimo.  

### Errore: `Training data quality standards not met: Insufficient number of unique training queries. Expected at least n, but found m.`
{: #error-notunique}

- Per soddisfare i requisiti di formazione minimi, hai bisogno come minimo di almeno 49 query di formazione univoche e ciascuna di esse ha bisogno di almeno un documento valutato. Se ne hai un numero anche maggiore ma continui a ricevere questo messaggio di errore, devi controllare i tuoi avvisi per rilevare la presenza di errori aggiuntivi.  

### Errore: `Training data quality standards not met: No documents found with non-zero relevance labels.`
{: #error-relevance}

- I dati di formazione richiedono una quantità sufficiente di dati etichettati che specificano quali documenti sono di alto valore. Questo significa che devi valutare qualche documento con valori diversi da zero. Se stai utilizzando la strumentazione Discovery, devi valutare qualche documento come pertinente (`10`); se stai utilizzando l'API, devi etichettare qualche documento come `1` o superiore.   

### Errore: `Training data quality standards not met: Training examples have no relevance label variety for X queries.`
{: #error-variety}

- Uno dei requisiti per la formazione è quello di disporre di una sufficiente diversità di etichette. Ciò significa che, se vuoi ottenere un sistema ben formato, devi aggiungere non solo documenti che sono la migliore corrispondenza di pertinenza ma anche i documenti che hanno una “buona” pertinenza. In altre parole, se hai una scala che va da 0 a 4, è utile avere dei documenti valutati come 2 e 3, oltre a quelli valutati come 4. (Se stai utilizzando la strumentazione Discovery, i documenti sono valutati come pertinenti (`10`) o non pertinenti (`0`)). Almeno il 25% delle domande deve presentare una certa varietà delle etichette.   
