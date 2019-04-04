---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-11"

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

# Miglioramento della pertinenza dei risultati con la strumentazione
{: #improving-result-relevance-with-the-tooling}

La pertinenza dei risultati della query in linguaggio naturale può essere migliorata nel servizio {{site.data.keyword.discoveryfull}} con la formazione. Puoi formare le tue raccolte private utilizzando la strumentazione {{site.data.keyword.discoveryshort}} oppure le API {{site.data.keyword.discoveryshort}}. Vedi [Miglioramento della pertinenza dei tuoi risultati della query con l'API](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api) se preferisci utilizzare le API.
{: shortdesc}

La formazione della pertinenza è facoltativa; se i risultati delle tue query soddisfano le tue esigenze, non è richiesta ulteriore formazione. Per una panoramica della creazione di casi d'uso per la formazione, vedi il post del blog [How to get the most out of Relevancy Training ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window}.

Per formare Watson, dovrai:

  -   Fornire delle query di esempio indicative delle query immesse dai tuoi utenti e
  -   Fornire delle valutazioni per individuare quali risultati per ciascuna query sono pertinenti e non pertinenti

Una volta che Watson avrà un input di formazione sufficiente, le informazioni da te fornite su quali risultati sono buoni e quali invece no per ogni query verranno utilizzate per raccogliere informazioni sulla tua raccolta. Watson non si limita a memorizzare; impara da specifiche informazioni sulle singole query e applica i modelli che ha rilevato a tutte le nuove query. Lo fa con le tecniche Watson di machine-learning (apprendimento automatico) che trovano segnali nel tuo contenuto e nelle tue domande. Una volta applicata la formazione, {{site.data.keyword.discoveryshort}} procede a riordinare i risultati della query per visualizzare i risultati più pertinenti per primi. Man mano che si aggiungono sempre più dati di formazione, {{site.data.keyword.discoveryshort}} diventerà più accurato nell'ordinamento dei risultati della query.

**Nota:** la formazione della pertinenza attualmente si applica solo alle query in linguaggio naturale nelle raccolte private. Non ne è previsto l'uso con query {{site.data.keyword.discoveryshort}} Query Language strutturate. Per ulteriori informazioni su {{site.data.keyword.discoveryshort}} Query Language, vedi [Concetti delle query](/docs/services/discovery?topic=discovery-query-concepts#query-concepts).

Nella maggior parte dei casi, tutte le raccolte private restituiranno un punteggio di affidabilità (`confidence`) nei risultati della query. Per i dettagli, vedi [Punteggi di affidabilità](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence).

l'aggiunta di un elenco di parole non significative personalizzato può migliorare la pertinenza dei risultati per le query in linguaggio naturale. Per ulteriori informazioni, vedi [Definizione delle parole non significative](/docs/services/discovery?topic=discovery-query-concepts#stopwords).

Vedi [Requisiti dei dati di formazione](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#reqs) per i requisiti minimi per la formazione e i limiti della formazione.

Vedi [Monitoraggio dell'utilizzo](/docs/services/discovery?topic=discovery-usage#usage) per i dettagli sulla traccia dell'utilizzo e l'impiego di questi dati per aiutarti a comprendere e migliorare le tue applicazioni.

## Aggiunta di query e valutazione della pertinenza dei risultati
{: #results}

La formazione si articola in tre parti: una query in linguaggio naturale, i risultati della query e le valutazioni da te applicate a questi risultati.

1.  Ci sono due modi per accedere alla pagina di formazione nella strumentazione {{site.data.keyword.discoveryshort}}:
    - Per una singola raccolta, nella schermata **Build queries**, fai clic su **Train Watson to improve results** nella parte superiore destra. Non hai bisogno di immettere una query nella schermata **Build queries** per avviare la formazione. 
    - Dal dashboard Performance, fai clic sull'icona **View data metrics** sulla sinistra per aprire il dashboard. Ti verrà richiesto di scegliere una raccolta da formare.
1.  Nella schermata **Train Watson**, fai clic su **Add a natural language query**, ad esempio: "IBM Watson nell'assistenza sanitaria" e aggiungila. Assicurati che le tue query siano scritte nel modo in cui i tuoi utenti le chiederebbero. Inoltre, le query di formazione dovrebbero essere scritte con una certa sovrapposizione di termini tra la query e la risposta desiderata. Ciò migliorerà i risultati iniziali quando verrà eseguita la query in linguaggio naturale. La formazione di pertinenza utilizza solo query in linguaggio naturale, non immettere query scritte in {{site.data.keyword.discoveryshort}} Query Language.
1.  Per visualizzare i risultati della tua query, fai clic sul pulsante **Rate Results** accanto ad essa. Se non pensi che ci siano abbastanza risultati, puoi provare a riscrivere la query o ad aggiungere più documenti a questa raccolta tramite la schermata **Manage data**.
1.  Inizia a valutare i risultati come `Relevant` o `Not relevant`. Dopo che hai finito, fai clic su **Back to queries**. Nella strumentazione {{site.data.keyword.discoveryshort}}, `Relevant` ha un punteggio di `10` e `Not relevant` ha un punteggio di `0`. se già hai iniziato a valutare i risultati per questa raccolta utilizzando l'API, e hai utilizzato una scala di valutazione differente, verrà visualizzata un'avvertenza con le opzioni per correggere il problema.
    Nella parte superiore dello schermo, Watson tiene traccia dello stato di formazione per tuo conto e fornisce suggerimenti su cosa puoi fare per migliorare i risultati. "Add more variety to your ratings" significa che dovresti utilizzare entrambe le valutazioni `Relevant` e `Not relevant`. Dopo che avrai soddisfatto i requisiti, la formazione inizierà ad aggiornarsi a intervalli regolari. L'operazione, una volta avviata, verrà completata in meno di 30 minuti e tu puoi continuare a lavorare mentre Watson si aggiorna.
1.  Continua ad aggiungere query e risultati della valutazione.

Per ritornare alla schermata **Build queries** in qualsiasi momento, fai clic su **Build queries** nell'angolo superiore sinistro.
{: tip}
Per ritornare alla schermata **Manage data**, fai clic sul nome della raccolta nell'angolo superiore destro.
{: tip}

Se vuoi eliminare tutti i dati di formazione nella tua raccolta contemporaneamente, devi eseguire tale operazione servendoti dell'API. Per ulteriori informazioni, vedi [Delete all training data for a collection](https://{DomainName}/apidocs/discovery#delete-all-training-data). Per ulteriori informazioni sulla formazione tramite l'API, vedi il documento relativo al [miglioramento della pertinenza dei tuoi risultati della query con l'API](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api).

## Verifica e iterazione sulla pertinenza dei risultati
{: #testing-results}

Dopo che hai completato i risultati della valutazione e che Watson ha applicato la formazione, devi eseguire una verifica per appurare se i risultati della query sono migliorati. Per eseguire tale operazione, esegui delle query di test correlate alle tue query di formazione (ma non identiche a esse). Verifica se i risultati delle tue query di test sono migliorati.

Se vuoi migliorare ulteriormente i risultati dopo l'esecuzione della verifica, puoi:
- Aggiungere altri documenti alla tua raccolta.
- Aggiungere altre query di formazione.
- Valutare più risultati, assicurandoti di utilizzare entrambe le valutazioni `Relevant` e `Not relevant`.

Per ulteriori istruzioni relative alla formazione, vedi [Suggerimenti per la formazione della pertinenza](/docs/services/discovery?topic=discovery-relevancy-tips#relevancy-tips).

## Punteggi di affidabilità
{: #confidence}

{{site.data.keyword.discoveryshort}} restituisce un punteggio di affidabilità (`confidence`) sia per le query in linguaggio naturale che per quelle scritte in {{site.data.keyword.discoveryshort}} Query Language.

Il punteggio di affidabilità (`confidence`) verrà restituito sia per le raccolte private formate che per quelle non formate (fatta eccezione per le query di solo filtro di raccolte non formate). Inoltre, {{site.data.keyword.discoveryshort}} restituisce un campo `document_retrieval_strategy` che indica l'origine del punteggio di affidabilità (`confidence`): 
-  `untrained`
-  `relevancy_training` oppure
-  `continuous_relevancy_training`

La strategia di richiamo dei documenti (`document_retrieval_strategy`) può essere utilizzata insieme al punteggio di affidabilità (`confidence`) per determinare in che modo devono essere utilizzati i risultati forniti. Nei casi di carico elevato, la strategia di richiamo dei documenti (`document_retrieval_strategy`) può essere non formata (`untrained`), anche se la raccolta è stata formata.

L'affidabilità (`confidence`) può avere un valore compreso tra 0,0 e 1,0. Più alto è il numero e più pertinente è il documento.

Il punteggio di affidabilità (`confidence`) può essere trovato nei risultati della query, sotto i metadati dei risultati (`result_metadata`) per ciascun documento. La strategia di richiamo dei documenti (`document_retrieval_strategy`) sarà elencata sotto i dettagli del richiamo (`retrieval_details`).

```json
{
  "matching_results": 4,
  "session_token": "1_2gYuWJyaWx792Ni4_DQ4C5cbnW",
  "retrieval_details" : {
    "document_retrieval_strategy" : "relevancy_training",
  },
  "results": [
    {
      "id": "eea16dfd5fe6139a25324e7481a32f89_13",
            "result_metadata": {
        "confidence": 0.5893963975910735,
        "score": 0.5006834
      }
    }
  ]
}
```
{: codeblock}

Per le raccolte formate, il punteggio di affidabilità (`confidence`) viene calcolato in base al grado di pertinenza stimato del risultato rispetto al modello formato. Le raccolte formate calcolano i punteggi di affidabilità (`confidence`) solo per le query in linguaggio naturale. Se esegui una query di una raccolta formata utilizzando il {{site.data.keyword.discoveryshort}} Query Language, o se il modello formato è temporaneamente non disponibile, il punteggio di affidabilità (`confidence`) restituito avrà una strategia di richiamo del documento (`document_retrieval_strategy`) di `untrained`. Il punteggio di affidabilità (`confidence`) per un risultato con la strategia di richiamo dei documenti (`document_retrieval_strategy`) di `untrained` è una stima non supervisionata di quanto siano pertinenti i risultati del documento alla query; non è intercambiabile con il punteggio restituito per le raccolte formate. Una raccolta formata può fornire delle risposte migliori alle query in linguaggio naturale rispetto alle raccolte non formate.

Nota che il punteggio di affidabilità (`confidence`) **non** è uguale al punteggio (`score`). Per ulteriori informazioni sulla determinazione delle soglie per i punteggi di affidabilità, vedi [How to select a threshold for acting using confidence scores ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/watson/blog/2016/06/23/how-to-select-a-threshold-for-acting-using-confidence-scores/). Il punteggio (`score`) non deve essere utilizzato per impostare delle soglie assolute poiché è un calcolo relativo. Consigliamo invece che le applicazioni eseguano sempre la stessa modalità di funzionamento per tutti i risultati che non includono il campo `confidence`. Ad esempio, un'applicazione potrebbe mostrare tutti i risultati senza il campo `confidence` o nascondere tutti i risultati senza il campo `confidence` ma non dovrebbe utilizzare il valore di `score` per mostrarne qualcuno e nasconderne altri. Poiché il modo in cui l'affidabilità (`confidence`) è calcolata varia tra i diversi metodi di richiamo, devi valutare la strategia di richiamo dei documenti (`document_retrieval_strategy`) quando imposti una soglia e riesaminare i valori prima e dopo la formazione.

Per ulteriori informazioni sull'esecuzione di query, vedi [Introduzione all'esecuzione di query](/docs/services/discovery?topic=discovery-getting-started-with-querying#getting-started-with-querying).

Per ulteriori informazioni sui metodi di formazione supervisionati, vedi:
-  [Formazione della pertinenza](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling) e
-  [Continuous Relevancy Training](/docs/services/discovery?topic=discovery-crt#crt)
