---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-18"

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

# Prestazioni delle query
{: #qp}

Le prestazioni delle query in {{site.data.keyword.discoveryshort}} dipendono da diversi fattori. 

## Valutazione delle prestazioni 
{: #qp-evaluate}

Se prevedi un elevato carico simultaneo sulla tua applicazione, è importante valutare le prestazioni della tua applicazione {{site.data.keyword.discoveryshort}}. Ci sono diverse dimensioni comunemente utilizzate per misurare le prestazioni:
1.  **Latenza della risposta** - il tempo impiegato da {{site.data.keyword.discoveryshort}} per restituire i risultati della tua query. 
    - La latenza può variare in base a diversi fattori; per ulteriori informazioni, vedi [Fattori che si ripercuotono sulle prestazioni](/docs/services/discovery?topic=discovery-qp#perffactors). 
    - È importante eseguire dei test nel tuo ambiente di produzione utilizzando una serie rappresentativa di query per determinare la tua latenza media. 
1.   **Frequenza delle query** - il numero di richieste che può essere elaborato in un certo periodo di tempo, di norma misurato in query al secondo (QPS, Query per Second). Questa misura è particolarmente importante quando prevedi un elevato carico simultaneo sulla tua applicazione.  
     - La frequenza che può essere raggiunta varia in base a molti degli stessi fattori della latenza. 
     - La frequenza delle query dovrebbe anche essere valutata con delle query rappresentative e ai carichi che ti aspetti di vedere. Ricordati di tenere conto dei carichi di picco durante l'esecuzione dei test.

## Fattori che si ripercuotono sulle prestazioni
{: #perffactors}

Le prestazioni delle query in {{site.data.keyword.discoveryshort}} varieranno in base a diversi fattori, compresi la dimensione del piano, la complessità delle query, le funzioni utilizzate e la dimensione e la complessità delle raccolte.

### Dimensione del piano
{: #qp-plansize}

I piani dei prezzi di {{site.data.keyword.discoveryshort}} limitano il numero di documenti disponibili e forniscono anche una diversa capacità di gestire il carico delle query. Più grande è la dimensione del piano e maggiore sarà la quantità di risorse disponibile per gestire le query. Anche i limiti di frequenza media variano in base alla dimensione del piano. L'esecuzione dell'upgrade del tuo piano può migliorare le prestazioni. Vedi [Piani dei prezzi di {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans) per i piani e i limiti. 

### Complessità delle query
{: #qp-query}

Ci sono molti modi per eseguire delle query su {{site.data.keyword.discoveryshort}} e le differenti operazioni utilizzate possono ripercuotersi sulle prestazioni. Queste caratteristiche delle query possono incidere sulle prestazioni:

1.   **Lunghezza** - Le query più lunghe molto probabilmente avranno delle prestazioni peggiori. 
1.   **Aggregazioni** - Le aggregazioni sono un tipo di query più complesso; le aggregazioni nidificate sono quelle che si ripercuotono maggiormente sulle prestazioni. 
1.   **Operatori** - La messa a confronto con caratteri jolly e quella di tipo fuzzy può incidere sulle prestazioni.
1.   **Conteggi** - Ridurre il conteggio dei documenti restituiti può migliorare le prestazioni; se devi sfogliare i risultati, utilizza il parametro `offset`. 
1.   **Campi di restituzione** - Limitare i campi restituiti solo a quelli necessari per le tue applicazioni può essere utile (ad esempio, non restituire il testo completo del documento se sono necessari solo il titolo e il passaggio). 

Per i dettagli, vedi la [Guida di riferimento per le query](/docs/services/discovery?topic=discovery-query-reference#query-reference).

### Funzioni utilizzate
{: #qp-features}

Ci sono diverse funzioni che migliorano i risultati della query. Le seguenti funzioni possono ripercuotersi sulle prestazioni:
 
1.   **Richiamo dei passaggi** - Il richiamo dei passaggi esegue una ricerca nei documenti per trovare i frammenti di testo pertinenti per la tua query. Puoi regolare i campi nei documenti su cui il richiamo dei passaggi esegue la ricerca con il parametro `passages.fields`; se il tuo contenuto ha molti campi, questo aiuterà a ridurre la latenza del richiamo dei passaggi. Per ulteriori informazioni sul richiamo dei passaggi, vedi [Passaggi](/docs/services/discovery?topic=discovery-query-parameters#passages).
1.   **Formazione della pertinenza** - La formazione della pertinenza calcola le funzioni per ogni campo di testo di livello superiore (i campi allo stesso livello di x`document_id` in JSON) nella raccolta. La presenza di molti campi di livello superiore può incidere sulle prestazioni per una `natural_language_query` quando si utilizza la formazione. Ridurre il numero dei campi di livello superiore può migliorare le prestazioni. Tale operazione può essere eseguita ricorrendo alla normalizzazione oppure modificando manualmente JSON per mettere i campi che non sono utili per la ricerca del contenuto pertinente in una struttura nidificata. La modifica dei campi utilizzati per la formazione ha anche un impatto sul modello; pertanto, se apporti questa modifica, dovrai tenere conto sia delle ripercussioni sulle prestazioni che della precisione dei risultati. Per ulteriori informazioni sulla formazione della pertinenza, vedi [Miglioramento della pertinenza dei risultati](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling).
1.  **Continuous Relevancy Training** - Continuous Relevancy Training cerca in tutte le raccolte in un ambiente. Maggiore è il numero di raccolte in un ambiente e più grande è l'impatto sulle prestazioni. Per ulteriori informazioni, vedi [Continuous Relevancy Training](/docs/services/discovery?topic=discovery-crt#crt).

### Dimensione e complessità delle raccolte
{: #qp-collection} 

Anche la composizione dei documenti in una raccolta privata si ripercuote sulle prestazioni delle query:
1.  **Numero totale di documenti** - Le prestazioni possono risentirne quando ci si avvicina ai limiti massimi del numero di documenti (`Number of Documents`) per le dimensioni dei piani Advanced. 
1.  **Dimensione dei documenti** - Dei documenti molto grandi (con una dimensione di diversi MB) richiedono lo spostamento di una grande quantità di dati per ogni richiesta, il che si può ripercuotere negativamente sulle prestazioni, soprattutto quando utilizzi il richiamo dei passaggi e la formazione della pertinenza. 
1.  **Numero di arricchimenti** - Gli arricchimenti aggiungono complessità ai documenti aggiungendo un numero significativo di campi nidificati. Se un arricchimento non è necessario per il tuo caso d'uso, valutane la disabilitazione in fase di inserimento. Gli arricchimenti non sono utilizzati direttamente per la pertinenza delle ricerche `natural_language_query`. Vedi [Aggiunta degli arricchimenti](/docs/services/discovery?topic=discovery-configservice#adding-enrichments) per ulteriori informazioni sugli arricchimenti.
