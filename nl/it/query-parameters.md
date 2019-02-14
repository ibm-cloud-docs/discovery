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

# Parametri di query
{: #query-parameters}

Il servizio {{site.data.keyword.discoveryfull}} offre potenti funzionalità di ricerca di contenuto tramite le query. Dopo che il tuo contenuto è stato caricato e arricchito dal servizio {{site.data.keyword.discoveryshort}}, puoi creare delle query e integrare {{site.data.keyword.discoveryshort}} nei tuoi progetti oppure creare un'applicazione personalizzata utilizzando il {{site.data.keyword.watson}} Explorer Application Builder. Per un'introduzione alle query, vedi [Concetti delle query](/docs/services/discovery/using.html). Per un elenco completo di parametri, vedi la [Guida di riferimento per le query](/docs/services/discovery/query-reference.html#parameter-descriptions).
{: shortdesc}

**Parametri di ricerca**

I parametri di ricerca ti consentono di eseguire ricerche nella tua raccolta, identificare una serie di risultati ed eseguire l'analisi sull'insieme di risultati.

La **serie di risultati** è il gruppo di documenti identificato dalle ricerche combinate dei parametri di ricerca. La serie dei risultati può essere notevolmente più grande dei risultati restituiti. Se viene eseguita una query vuota, l'insieme di risultati è uguale a tutti i documenti presenti nella raccolta.

## query
{: #query}

Una ricerca query restituisce tutti i documenti presenti nel tuo insieme di dati con gli arricchimenti completi e il testo completo in ordine di pertinenza. Una query esclude anche qualsiasi documento che non menziona il contenuto della query. Queste query vengono scritte utilizzando il [{{site.data.keyword.discoveryshort}} Query Language](/docs/services/discovery/query-operators.html).

## filter
{: #filter}

Una query memorizzabile in cache che esclude qualsiasi documento che non menziona il contenuto della query. I risultati della ricerca di filtro **non** vengono restituiti in ordine di pertinenza. Queste query vengono scritte utilizzando il [{{site.data.keyword.discoveryshort}} Query Language](/docs/services/discovery/query-operators.html)

### Differenze tra i parametri di filtro e di query
{: #filtervquery}

Se verifichi lo stesso termine di ricerca su un piccolo insieme di dati, potresti riscontrare che i parametri `filter` e `query` restituiscono dei risultati molto simili (se non identici). Tuttavia, c'è una differenza tra i due parametri.

- L'utilizzo del solo parametro filter restituirà i risultati della ricerca senza un ordine specifico.
- L'utilizzo del solo parametro query restituirà i risultati della ricerca in ordine di pertinenza.

In insiemi di dati di grandi dimensioni, se ti occorre che i risultati vengano restituiti in ordine di pertinenza, devi combinare i parametri `filter` e `query` perché utilizzarli insieme migliorerà le prestazioni. Ciò è dovuto al fatto che il parametro `filter` verrà eseguito per primo e memorizzerà in cache i risultati e il parametro `query` procederà quindi a classificarli. Per un esempio di utilizzo di filtri e query insieme, vedi [Creazione di query combinate](/docs/services/discovery/using.html#building-combined-queries). I filtri possono essere utilizzati anche nelle aggregazioni.

Quando scrivi una query che include sia un parametro `filter` sia un parametro `aggregation`, `query` o `natural_language_query`, i parametri `filter` vengono eseguiti per primi, dopo di che vengono eseguiti in parallelo gli eventuali parametri `aggregation`, `query` o `natural_language_query`.

Con una semplice query, in particolar modo su un piccolo insieme di dati, `filter` e `query` spesso restituiscono esattamente gli stessi risultati (o simili). Se una chiamata di `filter` e `query` restituisce risultati simili, e ottenere una risposta in ordine di pertinenza non è importante, è preferibile utilizzare filter poiché le chiamate filter sono più rapide e sono memorizzate nella cache. La memorizzazione nella cache significa che, la volta successiva che esegui tale chiamata, ottieni una risposta molto più rapida, soprattutto in un insieme di dati di grandi dimensioni.

## aggregation
{: #aggregation}

Le query di tipo aggregazione (aggregation) restituiscono un conteggio dei documenti corrispondenti a un insieme di valori di dati, ad esempio le parole chiave principali, il parere generale delle entità e altro ancora. Per l'elenco completo di opzioni di aggregazione, vedi la [tabella delle aggregazioni](/docs/services/discovery/query-aggregations.html). Queste aggregazioni vengono scritte utilizzando il [{{site.data.keyword.discoveryshort}} Query Language](/docs/services/discovery/query-operators.html)

## natural_language_query
{: #nlq}

Una query in linguaggio naturale ti consente di eseguire delle query espresse in linguaggio naturale, come potrebbero essere ricevute da un utente finale in un'interfaccia colloquiale o in testo libero, ad esempio "IBM Watson nell'assistenza sanitaria". Il parametro utilizza l'intero input come testo della query. **Non** riconosce gli operatori. Il parametro `natural_language_query` abilita funzionalità quali la ricerca di passaggi e la formazione della pertinenza. Le raccolte formate restituiranno un punteggio `confidence` nel risultato di una query in linguaggio naturale. Per i dettagli, vedi [Punteggi di affidabilità](/docs/services/discovery/train-tooling.html#confidence).La lunghezza della stringa di query massima per una query in linguaggio naturale è `2048`.

**Parametri di struttura**

I parametri di struttura definiscono il contenuto e l'organizzazione dei documenti nel JSON restituito. Ciò include indicazioni quali il numero di risultati restituito, da dove iniziare a restituire i documenti nell'insieme di risultati, come viene ordinato l'insieme dei risultati, quali campi restituire per ciascun documento, se i documenti duplicati devono essere rimossi e se i passaggi pertinenti devono essere estratti dall'insieme di risultati. I parametri di struttura non influiscono sui quali documenti fanno parte dell'intero insieme di risultati.

## count
{: #count}

Il numero di documenti che vuoi che venga restituito nella risposta. Il valore predefinito è `10`.Il valore massimo per i valori `count` e `offset` insieme in qualsiasi singola query è `10000`.

## offset
{: #offset}

Il numero di risultati della query da tralasciare all'inizio. Ad esempio, se il numero totale di risultati restituito è 10, e l'offset è 8, restituisce gli ultimi due risultati. Il valore predefinito è `0`. Il valore massimo per i valori `count` e `offset` insieme in qualsiasi singola query è `10000`.

## return
{: #return}

Un elenco separato da virgole della parte della gerarchia di documenti da restituire. Qualsiasi parte della gerarchia di documenti è un valore valido.

## sort
{: #sort}

Un elenco separato da virgole di campi nel documento in base a cui eseguire l'ordinamento. Puoi, facoltativamente, specificare una direzione di ordinamento anteponendo come prefisso al campo `-` per l'ordine decrescente oppure `+` per l'ordine crescente. L'ordine crescente è la direzione di ordinamento predefinita.

Il parametro `sort` è attualmente disponibile per l'utilizzo solo con l'API; non è disponibile attraverso la strumentazione.

## bias
{: #bias}

Regola i risultati della ricerca per orientarli verso specifici risultati, ad esempio i documenti che sono stati pubblicati più di recente. `bias` deve essere impostato su un campo di tipo `date` oppure un campo di tipo `number`, ad esempio `bias=publication_date` o `bias=field_1`.  Quando viene specificato un campo di tipo `date`, i risultati restituiti saranno orientati verso i valori di campo più prossimi alla data attuale. Quando viene specificato un campo di tipo `number`, i risultati restituiti verranno orientati verso i valori di campo più elevati. Questo parametro non può essere utilizzato nella stessa query del parametro `sort`.

Il parametro `bias` è attualmente disponibile per l'utilizzo solo con l'API; non è disponibile attraverso la strumentazione.

## passages
{: #passages}

Un booleano che specifica se il servizio restituisce un insieme dei passaggi più pertinenti dai documenti restituiti da una query che utilizza il parametro `natural_language_query`.I passaggi sono generati da sofisticati algoritmi Watson per determinare i migliori passaggi di testo da tutti i documenti restituiti dalla query. Il valore predefinito è `false`.

Il parametro `passages` può essere utilizzato solo su raccolte private. Non può essere utilizzato sulla raccolta {{site.data.keyword.discoverynewsfull}}.
{: tip}

{{site.data.keyword.discoveryshort}} prova a restituire passaggi con un inizio e una fine che coincidono con l'inizio e la fine di una frase utilizzando il rilevamento dei limiti della frase. Per eseguire tale operazione, cerca prima i passaggi approssimativamente della lunghezza specificata nel parametro [`passages.characters`](/docs/services/discovery/query-parameters.html#passages_characters) (valore predefinito `400`). Espande quindi ciascun passaggio al limite di due volte la lunghezza specificata al fine di restituire le frasi intere. Se il tuo parametro `passages.characters` è breve e/o le frasi nei tuoi documenti sono molto lunghe, potrebbe non esserci alcun limite della frase abbastanza prossimo alla restituzione dell'intera frase senza andare oltre il doppio della lunghezza richiesta. In tal caso, {{site.data.keyword.discoveryshort}} rimane entro il limite di due volte il parametro `passages.characters`, quindi il passaggio restituito non includerà l'intera frase e ometterà l'inizio, la fine o sia l'inizio che la fine.

Poiché le regolazioni dei limiti della frase espandono la dimensione dei passaggi, vedrai un considerevole aumento della lunghezza media dei passaggi. Se la tua applicazione ha uno spazio su schermo limitato, sarebbe opportuno che impostassi un valore più piccolo per `passages.characters` e/o troncare i passaggi restituiti da {{site.data.keyword.discoveryshort}}. Il rilevamento dei limiti della frase funziona per tutte le lingue supportate e utilizza la logica specifica per la lingua.

Il parametro `passages` restituisce i passaggi corrispondenti (`passage_text`), nonché `score`, `document_id`, il nome del campo da cui era stato estratto il passaggio (`field`) e i caratteri di inizio e fine del testo del passaggio all'interno del campo (`start_offset` e `end_offset`), come mostrato nel seguente esempio. La query viene visualizzata in cima all'esempio.

```bash
 curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-06-25&natural_language_query='Hybrid%20cloud%20companies'&passages=true"
```
{: pre}

Il JSON che viene restituito sarà del seguente formato:

```json
 {
   "matching_results":2,
   "passages":[
     {
       "document_id":"ab7be56bcc9476493516b511169739f0",
       "passage_score":15.230205287402338,
       "passage_text":"a privately held company that provides hybrid cloud recovery, cloud migration and business continuity software for enterprise data centers and cloud infrastructure."
       "start_offset":120
       "end_offset":300
       "field":"text"
     },
     {
       "passage_text":"Disaster Recovery Services for Hybrid Cloud</title></head>\n<body>\n\n\n<p>Published: Thu, 27 Oct 2016 07:01:21 GMT</p>\n"
       "passage_score":10.153470191601558,
       "document_id":"fbb5dcb4d8a6a29f572ebdeb6fbed20e",
       "start_offset":70
       "end_offset":120
       "field":"html"
     },
  ...
```
{: codeblock}                        

### passages.fields
{: #passages_fields}

Un elenco separato da virgole di campi nell'indice da cui verranno presi i passaggi. Se questo parametro non è specificato, vengono inclusi tutti i campi di livello superiore.

### passages.count
{: #passages_count}

Il numero massimo di passaggi da restituire. La ricerca restituirà un numero inferiore se tale numero è quello totale che è stato trovato. Il valore predefinito è `10`. Il massimo è `100`.

### passages.characters
{: #passages_characters}

Il numero approssimativo che un singolo passaggio dovrebbe avere. Il valore predefinito è `400`. Il minimo è `50`. Il massimo è `2000`. I passaggi restituiti possono essere fino a due volte la lunghezza richiesta (se necessario) per fare in modo che inizino e finiscano ai limiti della frase.

## highlight
{: #highlight}

Un booleano che specifica se l'output restituito include un oggetto `highlight` in cui le chiavi sono nomi di campi e i valori sono array che contengono segmenti di testo corrispondente alla query evidenziati dalla tag HTML `*`.

L'output elenca l'oggetto `highlight` dopo l'oggetto `enriched_text`, come mostrato nel seguente esempio.

```bash
curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-06-25&natural_language_query=Hybrid%20cloud%20companies&highlight=true"
```
{: pre}

Il JSON che viene restituito sarà del seguente formato:

```json
{
   "highlight": {
     "extracted_metadata.title": [
       "IBM to Acquire Sanovi Technologies to Expand Disaster Recovery Services for <em>Hybrid</em> <em>Cloud</em>"
       ],
     "enriched_text.concepts.text": [
       "Privately held <em>company</em>",
       "<em>Cloud</em> computing"
       ],
     "text": [
       " Sanovi Technologies, a privately held <em>company</em> that provides <em>hybrid</em> <em>cloud</em> recovery, <em>cloud</em> migration",
       "IBM to Acquire Sanovi Technologies to Expand Disaster Recovery Services for <em>Hybrid</em> <em>Cloud</em>\n\nPublished",
       " undergoing digital and <em>hybrid</em> <em>cloud</em> transformation.\n\nURL: http://www.ibm.com/press/us/en/pressrelease/50837.wss",
       " and business continuity software for enterprise data centers and <em>cloud</em> infrastructure. Adding"
       ],
     "enriched_text.categories.label": [
       "/business and industrial/<em>company</em>/bankruptcy"
       ],
     "enriched_text.entities.type": [
       "<em>Company</em>"
       ],
     "html": [
       " Technologies, a privately held <em>company</em> that provides <em>hybrid</em> <em>cloud</em>\n recovery, <em>cloud</em> migration and business",
       " Disaster Recovery Services for <em>Hybrid</em> <em>Cloud</em></title></head>\n<body>\n\n\n<p>Published: Thu, 27 Oct 2016 07:01",
       " digital and <em>hybrid</em> <em>cloud</em> transformation.</p>\n<p>URL: http://www.ibm.com/press/us/en/pressrelease/50837.wss</p>\n\n\n\n</body></html>",
       " continuity software for \nenterprise data centers and <em>cloud</em> infrastructure. Adding these \ncapabilities"
       ]
   }
}
```
{: codeblock}

## deduplicate
{: #deduplicate}

 Una funzionalità beta che esclude i documenti duplicati dai risultati della query della raccolta {{site.data.keyword.discoverynewsfull}} in base al campo `title`. Vedi [Esclusione di documenti duplicati dai risultati della query](/docs/services/discovery/query-parameters.html#deduplication).

### deduplicate.field
{: #deduplicate_field}

Una funzionalità beta che esclude i documenti duplicati dai tuoi risultati della query in base al `{field}` specificato. Vedi [Esclusione di documenti duplicati dai risultati della query](/docs/services/discovery/query-parameters.html#deduplication).

### Esclusione di documenti duplicati dai risultati della query
{: #deduplication}

Se stai eseguendo una query della raccolta {{site.data.keyword.discoverynewsfull}}, o se la tua raccolta di dati privata contiene più documenti identici (o quasi identici), puoi escludere la maggior parte di essi dai risultati della query utilizzando la deduplicazione dei documenti.

**Nota:** la deduplicazione dei documenti è attualmente supportata solo come funzionalità beta. Per ulteriori informazioni, vedi [Funzioni beta](/docs/services/discovery/release-notes.html#beta-features) nelle note sulla release. Questa funzione beta è attualmente supportata solo in inglese; vedi [Supporto linguistico](/docs/services/discovery/language-support.html#feature-support) per i dettagli.

**Nota:**  ciascuna query viene deduplicata indipendentemente quindi la deduplicazione su interi offset non è supportata.

La deduplicazione viene eseguita dopo che i passaggi (`passages`) sono stati estratti e le aggregazioni sono state calcolate; pertanto, se includi il parametro `passages` nella tua query, i passaggi verranno restituiti da tutti i documenti nei risultati della query, prima della deduplicazione. Se esegui insieme un'aggregazione e una query, i risultati dell'aggregazione includeranno i dati da tutti i documenti restituiti, prima della deduplicazioe.

La deduplicazione viene eseguita solo sui campi restituiti. Se scegli di specificare `return=` nella tua query, includi il campo sul quale stai eseguendo la deduplicazione.

Per applicare la deduplicazione, utilizza la seguente sintassi nella query.  Sostituisci `{field}` con il nome del campo su cui desideri eseguire la deduplicazione. Il `{field}` specificato deve essere una stringa, come ad esempio `title`.

```
&deduplicate.field={field}
```
{: codeblock}

Quando viene eseguita la deduplicazione, la risposta JSON include `"duplicates_removed": x`, dove `x` è il numero di documenti rimosso dai risultati.

#### Deduplicazione di documenti in Watson Discovery News

Gli articoli di notizie possono essere diffusi a diversi canali di notizie e {{site.data.keyword.discoverynewsfull}} rileverà ciascuno di essi, con una conseguente presenza di articoli duplicati. Ciò significa che una query a {{site.data.keyword.discoverynewsfull}} potrebbe, potenzialmente, restituire diversi articoli identici o quasi identici nei risultati della query. L'utilizzo della deduplicazione rimuoverà la maggior parte degli articoli duplicati dalle tue query di ricerca.

{{site.data.keyword.discoveryshort}} esegue la deduplicazione utilizzando una corrispondenza approssimativa sul campo `title` e, pertanto, non è necessario specificare un campo

Per applicare la deduplicazione, utilizza il seguente parametro nella tua query. Questa query esegue automaticamente la deduplicazione sul campo `title` in {{site.data.keyword.discoverynewsfull}}.

```bash
&deduplicate=true
```
{: codeblock}

Se preferisci eseguire la deduplicazione su un campo diverso da `title`, utilizza la seguente sintassi nella tua query. Sostituisci `{field}` con il nome del campo su cui desideri eseguire la deduplicazione. Il `{field}` specificato deve essere una stringa.

```bash
&deduplicate.field={field}
```
{: codeblock}

## collection_ids
{: #collection_ids}

Un elenco separato da virgole di raccolte nello stesso ambiente di cui verrà eseguita la query. Questo parametro è valido solo quando si utilizza il metodo `environments/{environment_id}/query?`. Per ulteriori informazioni, vedi [Query di più raccolte](/docs/services/discovery/using.html#multiple-collections).

```bash
&collection_ids={id1},{id2}
```
{: codeblock}

## similar
{: #similar}

La similarità dei documenti identifica i documenti che sono simili ai documenti elencati nei parametri `similar.document_ids`. Tale operazione può essere ulteriormente perfezionata specificando quali campi saranno presi in considerazione per il confronto utilizzando i parametri `similar.fields`. Il valore predefinito è `false`. Per ulteriori informazioni, vedi [Similarità dei documenti](/docs/services/discovery/using.html#doc-similarity).

```bash
&similar=true
```
{: codeblock}

### similar.document_ids
{: #similar_document_ids}

Un elenco separato da virgole di ID documento che verrà utilizzato come base per trovare documenti simili come risultati. Questo parametro è obbligatorio se il parametro `similar` è impostato su `true`.

```bash
&similar.document_ids={id1},{id2}
```
{: codeblock}

### similar.fields
{: #similar_fields}

Un elenco facoltativo separato da virgole di campi che verrà utilizzato per confrontare i documenti per trovare documenti simili. Questo parametro può essere utilizzato solo insieme al parametro `similar.document_ids`.

```bash
&similar.fields={field1},{field2}
```
{: codeblock}
