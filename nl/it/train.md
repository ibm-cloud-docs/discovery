---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-06"

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

# Miglioramento della pertinenza dei risultati con l'API
{: #improving-result-relevance-with-the-api}

Puoi formare il servizio {{site.data.keyword.discoveryshort}} per migliorare la pertinenza dei risultati della query per la tua organizzazione o la tua area di settore specifiche. Quando fornisci un'istanza {{site.data.keyword.discoveryshort}} con *dati di formazione*, il servizio utilizza le tecniche Watson di machine learning per trovare segnali nel tuo contenuto e nelle tue domande. Il servizio riordina quindi i risultati della query per visualizzare i risultati più pertinenti per primi. Man mano che aggiungi ulteriori dati di formazione, l'istanza del servizio diventa più accurata e sofisticata nell'ordinamento dei risultati che restituisce.
{: shortdesc}

La formazione della pertinenza è facoltativa; se i risultati delle tue query soddisfano le tue esigenze, non è richiesta ulteriore formazione. Per una panoramica della creazione di casi d'uso per la formazione, vedi il post del blog [How to get the most out of Relevancy Training ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window}.

Per informazioni complete sulle API di formazione, vedi la [Guida di riferimento per le API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}.

Se preferisci utilizzare la strumentazione {{site.data.keyword.discoveryshort}} per formare {{site.data.keyword.discoveryshort}}, vedi [Miglioramento della pertinenza dei risultati con la strumentazione](/docs/services/discovery/train-tooling.html).

**Nota:** la formazione della pertinenza attualmente si applica solo alle query in linguaggio naturale nelle raccolte private. Non ne è previsto l'uso con query {{site.data.keyword.discoveryshort}} Query Language strutturate. Per ulteriori informazioni su {{site.data.keyword.discoveryshort}} Query Language, vedi [Concetti delle query](/docs/services/discovery/using.html).

Le raccolte formate restituiranno un punteggio `confidence` nel risultato di una query in linguaggio naturale. Per i dettagli, vedi [Punteggi di affidabilità](/docs/services/discovery/train-tooling.html#confidence).

Vedi [Requisiti dei dati di formazione](/docs/services/discovery/train.html#reqs) per i requisiti minimi per la formazione e i limiti della formazione.

Vedi [Monitoraggio dell'utilizzo](/docs/services/discovery/feedback.html) per i dettagli sulla traccia dell'utilizzo e l'impiego di questi dati per aiutarti a comprendere e migliorare le tue applicazioni.

<!-- A trained Discovery service instance is intended primarily for use with natural language queries, but it works equally well with queries that use structured syntax. -->  <!-- See [Query Concepts](/docs/services/discovery/using.html) and the [Query reference](/docs/services/discovery/query-reference.html) for information about structured queries and natural language queries. -->

I componenti necessari per formare un'istanza di Discovery includono quanto segue:

 - **Dati di formazione**. Si tratta di un insieme di *query* ed *esempi* utilizzata dal servizio per affinare i risultati della query.
 - **Query**. Una query in linguaggio naturale che si applica all'insieme di dati di formazione.
   Ogni query ha uno o più *esempi* associati, come descritto nel seguente punto.
   Ogni query deve essere univoca all'interno dell'insieme di dati di formazione.
 - **Esempio**. Questo è un documento indicizzato in una raccolta Discovery che funge da esempio, **valido o non valido**, per la query associata. Quando aggiungi un esempio a una query di dati di formazione, includi un'etichetta di pertinenza che indica la pertinenza (o la "validità" rispetto alla "non validità") del documento così come si applica alla query specificata.

   Gli esempi sono identificati dall'ID documento indicizzato. Come osservato, ogni esempio deve includere un'etichetta che indica la "validità" o la "non validità" del documento per quanto riguarda la query.

   Degli esempi possono, facoltativamente, specificare una query a riferimento incrociato. La query a riferimento incrociato deve restituire solo il documento di esempio e deve essere indipendente dall'ID documento Watson Discovery univoco. Le query a riferimento incrociato non sono attualmente utilizzate in modo automatico ma possono essere utilizzate per riparare i dati di formazione nel caso in cui vengano assegnati dei nuovi ID ai documenti durante un evento di inserimento.

## Requisiti dei dati di formazione
{: #reqs}

I dati di formazione devono soddisfare i seguenti criteri di qualità **minimi** per migliorare efficacemente la pertinenza delle risposte restituite dal servizio Discovery. Nota: **minimi** non significa **ottimali**. Il servizio controlla i dati di formazione periodicamente per determinare se questi requisiti sono soddisfatti e si aggiorna automaticamente sulla base di eventuali modifiche.

- L'insieme di dati di formazione della raccolta deve contenere almeno 49 query di formazione univoche (ossia, insiemi di query ed esempi). A seconda della dimensione e della complessità della tua raccolta, il numero di query di formazione nel tuo insieme potrebbe dover essere superiore a 49 prima che Watson sia in grado di applicare la formazione della pertinenza alla raccolta. Watson fornirà un feedback se ha bisogno di più query al fine della formazione.
- Quando si assegnano dei punteggi di pertinenza tramite l'API: il punteggio di pertinenza per ogni query di formazione deve essere un numero intero non negativo, ad esempio `0`, per rappresentare *non pertinente*, `1` per rappresentare *alquanto pertinente* e `2` per rappresentare *altamente pertinente*. Tuttavia, per una flessibilità massima, il servizio accetta numeri interi non negativi compresi tra `0` e `100` per utenti avanzati che sperimentano i diversi schemi di punteggio. Indipendentemente dall'intervallo da te utilizzato, il numero intero più grande nell'insieme di query di formazione indica la pertinenza massima.
- Quando si assegnano punteggi di pertinenza tramite la strumentazione: la strumentazione {{site.data.keyword.discoveryshort}} utilizza i punteggi di pertinenza `0` per rappresentare *non pertinente* e `10` per rappresentare *pertinente*. Devi applicare entrambe le valutazioni disponibili ai tuoi risultati: `Relevant` e `Not relevant`. Valutare solo i documenti `Relevant` non fornirà i dati necessari. Se intendi dare un punteggio ai tuoi documenti utilizzando sia l'API che la strumentazione {{site.data.keyword.discoveryshort}}, o se intendi iniziare con l'API e passare alla strumentazione, utilizza i punteggi di pertinenza `0` e `10`.
- Le query di formazione devono includere una certa sovrapposizione dei termini tra la query e la risposta desiderata in modo da consentire alla ricerca iniziale del servizio Discovery, che ha una portata ampia, di eseguirne il richiamo.

**Nota:** Watson utilizza i dati di formazione per imparare i pattern e per generalizzare, non per memorizzare le singole query di formazione. Il servizio potrebbe quindi non sempre riprodurre identici risultati di pertinenza per una specifica query di formazione.

La formazione non può superare i seguenti requisiti **massimi**:
  - Non puoi superare le 24 raccolte formate per ogni ambiente.
  - All'interno di un unico ambiente, sei limitato a 10.000 query di formazione, con un massimo di 100 esempi per ogni query. 

## Aggiunta di una query all'insieme di dati di formazione

Utilizza il metodo `POST /v1/environments/{environment_id}/collections/{collection_id}/training_data` per aggiungere una query a un insieme di dati di formazione di una raccolta. La query è specificata come un oggetto JSON nel seguente formato:

```json
{
  "query_id": "string",
  "natural_language_query": "string",
  "filter": "string",
  "examples": [
    {
      "document_id": "string",
      "cross_reference": "string",
      "relevance": 0
    }
  ]
}
```
{: codeblock}

I valori in questo oggetto sono i seguenti:

- `query_id`: un ID univoco per la query. Se non specifichi questo campo, il servizio genera automaticamente un ID.
- `natural_language_query`: una query in linguaggio naturale Discovery che si applica all'insieme di formazione<!-- The `natural_language_query` parameter is preferred. -->
- `filter`: un filtro facoltativo per la query, come descritto nella [Guida di riferimento per le query](/docs/services/discovery/query-reference.html#parameter-descriptions).

    **Nota:** se includi i filtri nelle tue query di dati di formazione, assicurati di utilizzare gli stessi filtri quando utilizzi le query in linguaggio naturale nella tua raccolta formata. Se formi la raccolta con dati filtrati ma non utilizzi gli stessi tipi di filtri quando esegui una query della raccolta, i risultati possono essere imprevedibili.

- `examples`: un array che contiene i seguenti valori:

   - `document_id`: l'ID univoco del documento che si applica all'insieme di formazione. Questo è l'*esempio* descritto in precedenza.
   - `cross_reference`: un'etichetta facoltativa, di norma formata da un campo nel documento a cui si fa riferimento, che "blocca" fissandole le informazioni sul documento e sul campo nel caso in cui l'ID del documento vari, ad esempio se a un documento di nuovo inserimento viene assegnato lo stesso ID. La specifica di un valore per `cross-reference` **non** collega un documento a un altro; garantisce piuttosto che il servizio conservi le informazioni pertinenti del documento nel caso in cui il documento venga rinominato o sovrascritto.
   - `relevance`: un numero intero da `0` a `100`, inclusi, che indica la pertinenza relativa della query ai dati di formazione. Dei valori più alti indicano una maggiore pertinenza. Un valore `0` indica nessuna pertinenza alla query, mentre un valore `100` indica una pertinenza assoluta alla query.

   **Nota:** anche se l'intervallo del parametro `relevance` è compreso tra `0` e `100` per una flessibilità massima, puoi utilizzare un intervallo più piccolo per semplificare gli esempi di punteggio. Un intervallo standard potrebbe essere compreso tra `0` e `4` oppure potresti utilizzare l'intero intervallo ma utilizzare esclusivamente incrementi di 20 (`0`,`20`,`40`,`60`,`80` e `100`). La strumentazione {{site.data.keyword.discoveryshort}} utilizza i punteggi di pertinenza di `0` per rappresentare *non pertinente* e `10` per rappresentare *pertinente*. Se intendi dare un punteggio ai tuoi documenti utilizzando sia l'API che la strumentazione {{site.data.keyword.discoveryshort}}, o se intendi iniziare con l'API e passare alla strumentazione, utilizza i punteggi di pertinenza `0` e `10`.

Il seguente oggetto mostra una query di dati di formazione compilata.

```json
{
  "natural_language_query": "why is the sky blue",
  "filter": "text:meteorology",
  "examples": [
    {
      "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
      "relevance": 0
    },
    {
      "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
      "relevance": 1
    },
    {
      "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
      "cross_reference": "my_id_field:1463",
      "relevance": 4
    }
  ]
}
```
{: codeblock}

Il seguente esempio di comando aggiunge la precedente query di dati di formazione a una raccolta denominata `99040100-fe6a-4782-a4f5-28f9eee30850` in un ambiente denominato `a56dd9b4-040b-4ea3-a736-c1e7a467e191`:

```bash
curl -X POST -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" -H "Content-Type: application/json" -d
'{
  "natural_language_query": "why is the sky blue",
  "filter": "text:meteorology",
  "examples": [
    {
    "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
    "relevance": 0
    },
    {
      "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
      "relevance": 1
    },
    {
      "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
      "cross_reference": "my_id_field:1463",
      "relevance": 4
    }
  ]
}'
"https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
```
{: pre}

## Aggiunta di un esempio a una query di dati di formazione

Dopo che hai creato una query di dati di formazione, puoi continuare ad aggiungere ad essa degli esempi per migliorare l'accuratezza della formazione. Utilizza `POST /v1/environments/{environment_id}/collections/{collection_id}/training_data/{query_id}` per aggiungere un esempio a una query di dati di formazione esistente.

Esegui la seguente procedura per aggiungere un esempio a una query di dati di formazione.

1. Ottieni l'ID query della query di dati di formazione a cui vuoi aggiungere un nuovo esempio [elencando le query di dati di formazione della raccolta ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#get-training-data){: new_window}:

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
   ```
   {: pre}

   Il JSON che viene restituito sarà del seguente formato:

   ```json
    {
      "query_id": "484baad4-d440-44b7-a0dd-70bb2ac77baa",
      "natural_language_query": "why is the sky blue",
      "filter": "text:meteorology",
      "examples": [
        {
          "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
          "relevance": 0
        },
        {
          "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
          "relevance": 1
        },
        {
          "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
          "cross_reference": "my_id_field:1463",
          "relevance": 4
        }
      ]
    }
   ```
   {: codeblock}

1. Aggiungi il nuovo esempio utilizzando la stessa sintassi che usi per definire gli esempi quando crei una nuova query di dati di formazione. Il seguente esempio di comando non include un riferimento incrociato.

   ```bash
    curl -u -X POST -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" -H "Content-Type: application/json" -d
    '{
      "document_id": "46b52fdc-3a72-4700-9849-ac217532b373",
      "relevance": 3
    }' "https://gateway.watsonplatform.net/discovery/api/v1/environments//a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data/484baad4-d440-44b7-a0dd-70bb2ac77baa?version=2016-12-01"
   ```
   {: pre}

1. Verifica che il nuovo esempio sia stato aggiunto alla query di dati di formazione [elencando nuovamente le query di dati di formazione della raccolta ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#get-training-data){: new_window}:

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
   ```
   {: pre}

   Il JSON che viene restituito sarà del seguente formato:

   ```json
    {
      "query_id": "484baad4-d440-44b7-a0dd-70bb2ac77baa",
      "natural_language_query": "why is the sky blue",
      "filter": "text:meteorology",
      "examples": [
        {
          "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
          "relevance": 0
        },
        {
          "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
          "relevance": 1
        },
        {
          "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
          "cross_reference": "my_id_field:1463",
          "relevance": 4
        },
        {
          "document_id": "46b52fdc-3a72-4700-9849-ac217532b373",
          "relevance": 3
        }
      ]
    }
   ```
   {: codeblock}

1. Controlla lo stato della formazione utilizzando il metodo [List collection details ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#list-collection-details){: new_window} e verificando il valore del campo `"training"`/`"available"`. Dopo che hai aggiunto una quantità di query ed esempi sufficiente per soddisfare i requisiti di formazione, il valore del campo viene restituito come `true` e il servizio inizia automaticamente a utilizzare i dati di formazione.

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850?version=2016-12-01"
   ```
   {: pre}

   Il JSON che viene restituito sarà del seguente formato:

   ```json
    {
      "collection_id": "99040100-fe6a-4782-a4f5-28f9eee30850",
      "name": "democollection",
      "configuration_id": "def9bd08-8472-470f-ab5a-e377f77e9300",
      "language": "en_us",
      "status": "available",
      "description": "this is a demo collection",
      "created": "2015-08-24T18:42:25.324Z",
      "updated": "2015-08-24T18:42:25.324Z",
      "document_counts": {
        "available": 1000,
        "processing": 20,
        "failed": 180
      },
      "disk_usage": {
        "used_bytes": 895111
      },
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
   {: codeblock}

1. Quando i seguenti campi nel passo precedente restituiscono tutti `true`, immetti qualche query di esempio per verificare se il servizio restituisce risultati più pertinenti.

   - `minimum_queries_added`
   - `minimum_examples_added`
   - `sufficient_label_diversity`

   Se la pertinenza dei tuoi risultati non è migliorata, aggiungi ulteriori query di formazione finché i risultati non soddisferanno i tuoi requisiti.

Per ulteriori istruzioni relative alla formazione, vedi [Suggerimenti per la formazione della pertinenza](/docs/services/discovery/train-tips.html#relevancy-tips).   

## Esecuzione di altre operazioni di query di dati di formazione
{: #training-data-operations}

Puoi amministrare e gestire le query di dati di formazione utilizzando altri metodi API, come descritto nella [Guida di riferimento per le API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}:

 - [Elencare i dati di formazione per una raccolta ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#get-training-data){: new_window}
 - [Eliminare tutti i dati di formazione per una raccolta ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-all-training-data){: new_window}
 - [Visualizzare i contenuti di una specifica query di dati di formazione![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#show-td-query){: new_window}
 - [Eliminare una query di dati di formazione da una raccolta![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/watson/developercloud/discovery/api/v1#delete-td-query-example){: new_window}
 - [Modifica dell'etichetta di pertinenza o di un riferimento incrociato di un esempio di query di dati di formazione ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#update-example){: new_window}
 - [Eliminare un documento di esempio da una query di dati di formazione![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-example){: new_window}

 **Monitoraggio degli errori:** gli errori di dati di formazione sono visualizzati negli avvisi, che possono essere monitorati utilizzando le [API di avvisi di query ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-notices){: new_window}
 (`GET /v1/environments/{environment_id}/collections/{collection_id}/notices`).
