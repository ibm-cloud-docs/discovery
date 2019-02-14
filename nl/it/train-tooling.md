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

# Miglioramento della pertinenza dei risultati con la strumentazione

La pertinenza dei risultati della query in linguaggio naturale può essere migliorata nel servizio {{site.data.keyword.discoveryfull}} con la formazione. Puoi formare le tue raccolte private utilizzando la strumentazione {{site.data.keyword.discoveryshort}} oppure le API {{site.data.keyword.discoveryshort}}. Vedi [Miglioramento della pertinenza dei tuoi risultati della query con l'API](/docs/services/discovery/train.html) se preferisci utilizzare le API.
{: shortdesc}

La formazione della pertinenza è facoltativa; se i risultati delle tue query soddisfano le tue esigenze, non è richiesta ulteriore formazione. Per una panoramica della creazione di casi d'uso per la formazione, vedi il post del blog [How to get the most out of Relevancy Training ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window}.

Per formare Watson, dovrai:

  -   Fornire delle query di esempio indicative delle query immesse dai tuoi utenti e
  -   Fornire delle valutazioni per individuare quali risultati per ciascuna query sono pertinenti e non pertinenti

Una volta che Watson avrà un input di formazione sufficiente, le informazioni da te fornite su quali risultati sono buoni e quali invece no per ogni query verranno utilizzate per raccogliere informazioni sulla tua raccolta. Watson non si limita a memorizzare; impara da specifiche informazioni sulle singole query e applica i modelli che ha rilevato a tutte le nuove query. Lo fa con le tecniche Watson di machine-learning (apprendimento automatico) che trovano segnali nel tuo contenuto e nelle tue domande. Una volta applicata la formazione, {{site.data.keyword.discoveryshort}} procede a riordinare i risultati della query per visualizzare i risultati più pertinenti per primi. Man mano che si aggiungono sempre più dati di formazione, {{site.data.keyword.discoveryshort}} diventerà più accurato nell'ordinamento dei risultati della query.

**Nota:** la formazione della pertinenza attualmente si applica solo alle query in linguaggio naturale nelle raccolte private. Non ne è previsto l'uso con query {{site.data.keyword.discoveryshort}} Query Language strutturate. Per ulteriori informazioni su {{site.data.keyword.discoveryshort}} Query Language, vedi [Concetti delle query](/docs/services/discovery/using.html).

Le raccolte formate restituiranno un punteggio `confidence` nel risultato di una query in linguaggio naturale. Per i dettagli, vedi [Punteggi di affidabilità](/docs/services/discovery/train-tooling.html#confidence).

Vedi [Requisiti dei dati di formazione](/docs/services/discovery/train.html#reqs) per i requisiti minimi per la formazione e i limiti della formazione.

Vedi [Monitoraggio dell'utilizzo](/docs/services/discovery/feedback.html) per i dettagli sulla traccia dell'utilizzo e l'impiego di questi dati per aiutarti a comprendere e migliorare le tue applicazioni.

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

Se vuoi eliminare tutti i dati di formazione nella tua raccolta contemporaneamente, devi eseguire tale operazione servendoti dell'API. Per ulteriori informazioni, vedi [Delete all training data for a collection](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-all-training-data). Per ulteriori informazioni sulla formazione tramite l'API, vedi il documento relativo al [miglioramento della pertinenza dei tuoi risultati della query con l'API](/docs/services/discovery/train.html).

## Verifica e iterazione sulla pertinenza dei risultati

Dopo che hai completato i risultati della valutazione e che Watson ha applicato la formazione, devi eseguire una verifica per appurare se i risultati della query sono migliorati. Per eseguire tale operazione, esegui delle query di test correlate alle tue query di formazione (ma non identiche a esse). Verifica se i risultati delle tue query di test sono migliorati.

Se vuoi migliorare ulteriormente i risultati dopo l'esecuzione della verifica, puoi:
- Aggiungere altri documenti alla tua raccolta.
- Aggiungere altre query di formazione.
- Valutare più risultati, assicurandoti di utilizzare entrambe le valutazioni `Relevant` e `Not relevant`.

Per ulteriori istruzioni relative alla formazione, vedi [Suggerimenti per la formazione della pertinenza](/docs/services/discovery/train-tips.html#relevancy-tips).

## Punteggi di affidabilità
{: #confidence}

Le raccolte formate restituiranno un punteggio `confidence` nel risultato di una query in linguaggio naturale. Questo numero `confidence` viene calcolato in base al grado di pertinenza stimato del risultato rispetto al modello formato. Il punteggio `confidence` **non** è uguale al valore `score`. Per ulteriori informazioni sulla determinazione delle soglie per i punteggi di affidabilità, vedi [How to select a threshold for acting using confidence scores ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/watson/blog/2016/06/23/how-to-select-a-threshold-for-acting-using-confidence-scores/). Il punteggio (`score`) non deve essere utilizzato per impostare delle soglie assolute poiché è un calcolo relativo.

L'affidabilità (`confidence`) può avere un valore compreso tra 0,0 e 1,0. Più alto è il numero e più pertinente è il documento.

Il punteggio di affidabilità (`confidence`) può essere trovato nei risultati della query, in `result_metadata` per ciascun documento, ad esempio:

```json
    "results": [
        {
            "id": "eea16dfd5fe6139a25324e7481a32f89_13",
            "result_metadata": {
                "confidence": 0.5893963975910735,
                "score": 0.5006834
            },
```

**Nota:** il campo `confidence` viene restituito solo quando la formazione della pertinenza è stata completata correttamente. Ci possono anche essere dei casi in cui il modello formato non è disponibile e il campo `confidence` non verrà restituito. 

Ad esempio, il modello formato diventerà temporaneamente non valido se vengono introdotti dei nuovi campi di livello superiore o se lo schema della raccolta è stato in altro modo modificato perché sono stati inseriti dei nuovi documenti con uno schema differente. In tale scenario, `confidence` verrà restituito con i risultati, che proverranno dalla ricerca non formata predefinita finché il modello non verrà nuovamente formato automaticamente diventando quindi nuovamente disponibile. Durante la riesecuzione della formazione, `confidence` non verrà restituito.

Le applicazioni che utilizzano `confidence` come una soglia dovrebbero assicurarsi che possono gestire questi scenari. Poiché `score` è relativo alla query, si sconsiglia di farne uso come una soglia fissa. Consigliamo invece che le applicazioni eseguano sempre la stessa modalità di funzionamento per tutti i risultati che non includono il campo `confidence`. Ad esempio, un'applicazione potrebbe mostrare tutti i risultati senza il campo `confidence` o nascondere tutti i risultati senza il campo `confidence` ma non dovrebbe utilizzare il valore di `score` per mostrarne qualcuno e nasconderne altri.
