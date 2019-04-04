---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-17"

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

# Monitoraggio dell'utilizzo
{: #usage}

Puoi monitorare e tracciare l'utilizzo della tua istanza {{site.data.keyword.discoveryshort}} e utilizzare questi dati per comprendere e migliorare le tue applicazioni. L'[API Events ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery#create-event){: new_window} può essere utilizzata per creare voci di log associate a specifiche azioni e query in linguaggio naturale. Ad esempio, puoi registrare su quali documenti in una serie di risultati è stato "fatto clic" da un utente e quando si sono verificati i clic.

**Nota:** i log e gli eventi vengono monitorati solo per le query in linguaggio naturale su raccolte di dati privati. Nessun log viene raccolto su {{site.data.keyword.discoverynewsfull}}.

{{site.data.keyword.discoveryshort}} può registrare le seguenti informazioni:
- **Query** - le query in linguaggio naturale che vengono eseguite sulle raccolte nel tuo ambiente 
- **Impressioni** (o **Risultati**) -  i risultati restituiti da una particolare query, normalmente documenti o passaggi. 
- **Eventi** - interazioni eseguite da un utente su un risultato o una serie di risultati in {{site.data.keyword.discoveryshort}} (ad esempio, un clic su un risultato di documento)

Le **query** e le **impressioni** vengono registrate automaticamente; la registrazione degli **eventi** può essere integrata nella tua applicazione tramite l'API.

## Visualizzazione dei log
{: #viewlogs}

Puoi ricercare la query e il log eventi per trovare le sessioni di query che corrispondono ai criteri specificati. La ricerca dell'endpoint `logs` utilizza la sintassi di query {{site.data.keyword.discoveryshort}} per i parametri supportati. L'endpoint fornisce la funzionalità di query di base per la visualizzazione e la ricerca tramite i dati registrati.  

L'endpoint `/api/v1/logs` supporta i seguenti parametri di query {{site.data.keyword.discoveryshort}}.
- query 
- filter
- sort
- count 
- offset
- version

Per ulteriori dettagli sulla funzione e la sintassi dei parametri, consulta [Parametri di query](/docs/services/discovery?topic=discovery-query-parameters#query-parameters).

Esempio di ricerca di log per una query in linguaggio naturale che contiene il termine “train”:

`https://gateway.watsonplatform.net/discovery/api/v1/logs?version=2018-03-28&query=train`

La risposta di una query `logs` include i risultati che sembrano simili ai risultati del documento {{site.data.keyword.discoveryshort}}. Ogni risultato sarà una query o un evento, specificato nel campo `type` del documento.  

Esempio di query di log:

```
{
            "customer_id": "",
            "environment_id": "252e6e82-c2d2-450e-9670-0008b0a3a99c",
            "natural_language_query": "how do i get from the airport to the city",
            "query_id": "_Qs35yOoa7",
            "document_results": {
                "count": 2,
                "results": [
                    {
                        "collection_id": "af9e1f41-6114-4d77-bca6-c9b99b2601b1",
                        "score": 6.724753491503856,
                        "position": 1,
                        "document_id": "4193eaa727d79b0f74597356dbcbb9a7"
                    },
                    {
                        "collection_id": "af9e1f41-6114-4d77-bca6-c9b99b2601b1",
                        "score": 5.791631414211986,
                        "position": 2,
                        "document_id": "bdcd6a9cc1438a3faa8c925f6a8d9429"
                    }
                ]
            },
            "event_type": "query",
            "session_token": "1_LKczxWGEWx5TJAi1_Qs35yOoa7",
            "created_timestamp": "2018-09-12T05:20:07.469Z"
        }
```

Con la query dei log puoi analizzare il tipo di risultati restituiti ai tuoi utenti finali e analizzare i modi per migliorare la qualità dei risultati utilizzando gli approcci disponibili in {{site.data.keyword.discoveryshort}}. Ad esempio: 
- formazione della pertinenza, consulta [Miglioramento della pertinenza dei risultati con l'API](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api) e [Miglioramento della pertinenza del risultato con la strumentazione](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling)
- [operatori di query](/docs/services/discovery?topic=discovery-query-operators#query-operators)
- [espansione di query](/docs/services/discovery?topic=discovery-query-concepts#query-expansion)
- configurazioni personalizzate, consulta il [Riferimento della configurazione](/docs/services/discovery?topic=discovery-configref#configref)

## Creazione di log eventi
{: #eventlogs}

I log eventi vengono utilizzati per tenere traccia delle interazioni degli utenti all'interno della tua applicazione. Questo può aiutarti a capire quanto bene sta venendo eseguita la tua applicazione, oltre a identificare le aree su cui potresti aver bisogno di focalizzarti per migliorare i risultati. {{site.data.keyword.discoveryshort}} fornisce un'API che può essere integrata nella tua applicazione per tenere traccia degli eventi. Chiamando questa API con le informazioni appropriate quando un utente esegue un'azione, invia un segnale di ritorno a {{site.data.keyword.discoveryshort}}, che può quindi essere visualizzato nei log. 

Gli eventi possono aiutare a raccogliere le informazioni sulle metriche di calcolo (come frequenza di clickthrough) per misurare quanto sia efficace l'applicazione nell'aiutare gli utenti finali a trovare informazioni rilevant, o possono essere utilizzati per aiutare la formazione dei seed riesaminando le query e i clic per iniziare a creare il ground truth. 

Puoi aggiungere questa API ovunque gli utenti interagiscono con i tuoi risultati. Ad esempio, in un'IU di ricerca potresti volerla aggiungere quando un utente fa clic su un link di un documento o in un'interfaccia chatbot che potresti voler utilizzare per tenere traccia di quando l'utente fa clic su un pulsante **Espandi** o **Ulteriori dettagli**.

I risultati di {{site.data.keyword.discoveryshort}} restituiranno ulteriori informazioni che possono essere utilizzate per tenere traccia degli eventi, incluso un token di sessione. 

`"matching_results": 179,`
`"session_token": "1_LKczxWGEWx59fYD0_VV8HFUpb6"`

Per registrare un evento, esegui un POST per l'endpoint `/api/v1/events`. Per i dettagli, consulta
l'[API Events ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery#create-event){: new_window}.

Quando un evento viene registrato, può essere riletto utilizzando l'endpoint `/api/v1/logs`. Unisci gli eventi alla query associata utilizzando `session_token`.
