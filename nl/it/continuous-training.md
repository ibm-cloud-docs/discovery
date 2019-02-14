---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-25"

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

# Continuous Relevancy Training
{: #crt}

{{site.data.keyword.discoveryshort}} Continuous Relevancy Training può apprendere dal comportamento dell'utente automaticamente, riducendo in modo significativo lo sforzo richiesto per migliorare la classificazione della rilevanza dei risultati. Utilizza le interazioni dagli utenti per imparare come dare rilievo ai risultati più pertinenti. Può imparare dalle interazioni come i clic per determinare quali risultati sono più importanti per gli utenti e scoprire i segnali più importanti per le query future. Continuous Relevancy Training riclassificherà i documenti per dare rilievo alle informazioni più importanti in cima ai risultati. Può essere utilizzato per:

- Aiutare a migliorare la pertinenza dei risultati per gli agent di supporto, in base ai risultati su cui fanno clic
- Visualizzare risultati più rilevanti in una chatbot del cliente in base ai risultati di lunga coda selezionati 
- Fornire agli esperti risposte più pertinenti, in base ai risultati esplorati

Per configurare Continuous Relevancy Training:

- Continuous Relevancy Training può essere abilitato solo a livello di ambiente. Le query devono utilizzare gli endpoint `/api/v1/environment/{environment_id}/query` e `/api/v1/environments/{environment_id}/query` per eseguire la query di una o più raccolte.
- Poiché gli eventi {{site.data.keyword.discoveryshort}} (`events`) (i clic) sono utilizzati per creare i dati di formazione necessari, integra prima la traccia dell'evento. Per i dettagli, consulta [Monitoraggio dell'utilizzo](/docs/services/discovery/feedback.html#usage).
- Sono richieste un minimo di 1000 query in linguaggio naturale con un evento di clic associato per l'avvio di Continuous Relevancy Training. Gli eventi e i log vengono conservati per 30 giorni nella tua istanza per cui i 1000 clic devono essere raccolti durante quel periodo di tempo.
- Continuous Relevancy Training è disponibile per la dimensione `Small` o maggiori dei piani Advanced e per i piani Premium. Non è disponibile per i piani `Lite`.
- Il numero di raccolte per Continuous Relevancy Training è limitato a `5`. Poiché Continuous Relevancy Training utilizza più raccolte, sia i tempi di formazione che di query potrebbero venire estesi.
- Continuous Relevancy Training si verifica solo sui campi di primo livello e ci sono limiti su quanti campi possono essere utilizzati nel processo di formazione. Nei casi in cui ci sono più di `10` campi di livello superiore, la formazione è più probabile che riscontri degli errori. 

Per utilizzare Continuous Relevancy Training:

Una volta preparato, Continuous Relevancy Training viene utilizzato per influenzare i risultati di un `natural_language_query` quando utilizzi una query al livello dell'ambiente. 

Continuous Relevancy Training può essere utilizzato al tempo della query eseguendo una multi-raccolta `natural_language_query` in tutte le raccolte nel tuo ambiente. Consulta [Query di più raccolte](/docs/services/discovery/using.html#multiple-collections) per le istruzioni. 

**Nota:** Continuous Relevancy Training non influisce sulle query effettuate a una chiamata query al livello della raccolta preparata o non preparata (`/v1/environments/{environment_id}/collections/{collection_id}/query`). 

Stato della traccia:

Lo stato di Continuous Relevancy Training può essere visualizzato dall'endpoint `/api/v1/environment`. Consulta il [Riferimento API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#environments-api){: new_window}. `status ` fornirà le informazioni sullo stato delle operazioni di formazione e ti informerà se Continuous Relevancy Training è attivo:

```
"search_status" : [
        {
            "scope" : "environment",
            "status" : "NO_DATA",
            "status_description" : "Discovery is employing a default strategy for document search natural_language_query. Enable query and event logging so we can initiate relevancy training to improve search accuracy.”
        }
    ]
```
