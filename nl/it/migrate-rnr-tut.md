---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-09"

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


# Esercitazione: migrazione da Retrieve and Rank
{: #migrate-rnr}

Migrazione da {{site.data.keyword.retrieveandrankshort}} al servizio {{site.data.keyword.discoveryfull}}. Una continuazione dell'esercitazione introduttiva a Cranfield

## Panoramica
{: #overview-rnr}

Questa esercitazione ti giuda nel processo di creazione e formazione di un servizio {{site.data.keyword.discoveryfull}} con dati di esempio. Questa esercitazione utilizza lo stesso insieme di dati utilizzato nell'[esercitazione introduttiva a {{site.data.keyword.retrieveandrankshort}}](/docs/services/retrieve-and-rank/getting-started.html) ma puoi utilizzare lo stesso approccio per creare un'istanza del servizio che utilizza i tuoi dati.

La procedura con la quale gli utenti migrano i dati da {{site.data.keyword.retrieveandrankshort}} a {{site.data.keyword.discoveryshort}} si articola in due fasi:

1. Migrazione dei dati della raccolta.
2. Migrazione dei dati di formazione.

Quando esegui la migrazione dei tuoi dati della raccolta oggetto della formazione, la cosa **più** importante è _mantenere invariati gli ID documento_. Ciò è dovuto al fatto che i dati di formazione utilizzano tali ID per fare riferimento al ground truth (ossia l'evidenza empirica) e, se gli ID vengono modificati nello spostamento da {{site.data.keyword.retrieveandrankshort}} a {{site.data.keyword.discoveryshort}} la riclassificazione potrebbe essere del tutto errata (oppure la formazione potrebbe anche non iniziare). {{site.data.keyword.discoveryshort}} ti consente di specificare l'ID documento nel processo di caricamento dell'API, quindi questo problema può essere evitato attenendosi alle linee guida contenute nel presente documento.  I dati di formazione di {{site.data.keyword.retrieveandrankshort}} sono di norma archiviati in un file `csv`. In questa esercitazione, questo file `csv` viene utilizzato per caricare i dati di formazione di esempio in {{site.data.keyword.discoveryshort}}.  La migrazione di dati di formazione esportati dalla strumentazione {{site.data.keyword.retrieveandrankshort}} è descritta in dettaglio in [Migrazione dei dati di formazione dal servizio](/docs/services/discovery?topic=discovery-migrate-dcs-rr#extract-train).

Questa esercitazione presume che {{site.data.keyword.retrieveandrankshort}} sia stato configurato in modo simile all'[esercitazione introduttiva di {{site.data.keyword.retrieveandrankshort}}](/docs/services/retrieve-and-rank/getting-started.html) e utilizza il percorso di migrazione da un'origine descritto [qui](/docs/services/discovery?topic=discovery-migrate-dcs-rr#source). Vedi [Valuta il tuo percorso di migrazione al servizio Watson Discovery](/docs/services/discovery?topic=discovery-migrate-dcs-rr#evaluate) per altre opzioni di migrazione.

Per completare l'esercitazione, ti occorre quanto segue:

-  **cURL.**  Puoi installare la versione di cURL per il tuo sistema operativo da [haxx.se ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://curl.haxx.se/){: new_window}. Devi installare la versione che supporta il protocollo SSL (Secure Socket Layer). Assicurati di includere il file binario installato nella tua variabile di ambiente PATH.
-  Dati Cranfield di esempio. Questa esercitazione utilizza i dati della raccolta di esempio dall'esercitazione introduttiva a {{site.data.keyword.retrieveandrankshort}}. [dati json cranfield ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-data.json){: new_window}
-  **Ground truth dei dati di esempio** Questa esercitazione utilizza il ground truth Cranfield di esempio dall'esercitazione introduttiva a {{site.data.keyword.retrieveandrankshort}}. [csv del ground truth cranfield![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-gt.csv){: new_window}
-  **Python versione 2.**  Per controllare se Python è installato, immetti `python --version` a un prompt dei comandi e assicurati che il numero versione inizi con 2. Se devi installare Python, vedi [Downloading Python ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://wiki.python.org/moin/BeginnersGuide/Download){: new_window}.
-  Script di caricamento dati: [Programma di caricamento del documento Discovery![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-upload.py){: new_window}
-  Script di caricamento dei dati di formazione: [Programma di caricamento della formazione Discovery ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-train.py){: new_window}

I seguenti prerequisiti sono necessari prima di iniziare questa esercitazione:

-  Questa esercitazione presume che tu abbia già creato un'istanza di {{site.data.keyword.discoveryshort}}; se ti occorrono indicazioni su come creare un'istanza di {{site.data.keyword.discoveryshort}}, fai riferimento alla [seguente esercitazione](/docs/services/discovery?topic=discovery-gs-api#gs-api).

-  Questa esercitazione presume che tu abbia le tue credenziali del servizio.
   -  Dal servizio Watson {{site.data.keyword.discoveryshort}} su {{site.data.keyword.Bluemix_notm}}, fai clic su **Credenziali del servizio**.
   -  Fai clic su **Visualizza credenziali** in Azioni.
   -  Copia il valore `apikey` e assicurati che il valore `url` corrisponda a quello negli esempi di seguito; in caso contrario, sostituisci anche tale valore.

## Aggiunta di dati Cranfield a Discovery
{: #cranfield-rnr}

1.  Crea un ambiente.

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{ "name": "my_environment", "description": "My environment" }' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    Copia l'`environment-id` elencato nel JSON restituito.

1. Crea una raccolta.

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{ "name": "test_collection", "description": "My test collection", "configuration_id": "{configuration_id}", "language_code": "en" }' "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07"
    ```
    {: pre}

    Copia il`collection-id` elencato nel JSON restituito.

1.  Aggiungi i documenti che desideri siano oggetto della ricerca.
    1.  Scarica il file [cranfield-data.json ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-data.json){: new_window}, se non lo hai già fatto. Questa è l'origine dei documenti utilizzati in {{site.data.keyword.retrieveandrankshort}}. I documenti della raccolta Cranfield sono in formato JSON, che è il formato {{site.data.keyword.retrieveandrankshort}} accettato e che funziona bene anche per Watson {{site.data.keyword.discoveryshort}}.
        **Nota:** {{site.data.keyword.discoveryshort}} non richiede il caricamento dello schema Solr. Ciò è dovuto al fatto che {{site.data.keyword.discoveryshort}} deduce lo schema dalla struttura JSON automaticamente.
    1.  Scarica lo script di caricamento dati [qui ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-upload.py){: new_window}. Questo script caricherà il json Cranfield in {{site.data.keyword.discoveryshort}}.
        Lo script legge tutto il file JSON e invia ogni singolo documento JSON al servizio {{site.data.keyword.discoveryshort}} utilizzando una configurazione predefinita in {{site.data.keyword.discoveryshort}}.
        **Nota:** la configurazione predefinita in {{site.data.keyword.discoveryshort}} fornisce impostazioni simili alla configurazione Solr predefinita in {{site.data.keyword.retrieveandrankshort}}.
    1.  Immetti il seguente comando per caricare i dati `cranfield-data-json` nella raccolta `cranfield_collection`. Sostituisci `{apikey_value}`, `{path_to_file}`,  `{environment_id}`, `{collection_id}` con le tue informazioni.  Nota che ci sono delle opzioni aggiuntive, -d per il debug e –v per l'output dettagliato da curl.

        ```bash
        python ./disco-upload.py -u apikey:{apikey_value} -i {path_to_file}/cranfield-data.json -e {environment_id} -c {collection_id}
        ```
        {: pre}

1.  Una volta completato il processo di caricamento, puoi controllare che i documenti siano presenti immettendo il seguente comando per visualizzare i dettagli della raccolta:

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07"
    ```
    {: pre}

    L'output sarà simile al seguente:

    ```json
    {
      "collection_id": "f1360220-ea2d-4271-9d62-89a910b13c37",
      "name": "democollection",
      "configuration_id": "6963be41-2dea-4f79-8f52-127c63c479b0",
      "language": "en",
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
        "used_bytes": 260
      },
      "training_status": {
        "data_updated": null,
        "total_examples": 0,
        "sufficient_label_diversity": false,
        "processing": false,
        "minimum_examples_added": true,
        "successfully_trained": null,
        "available": false,
        "notices": 0,
        "minimum_queries_added": false        
      }
    }
    ```
    {: codeblock}

Consulta la sezione `document_counts` per vedere quanti documenti sono stati caricati correttamente. Non sono previsti errori di documento con questo insieme di dati di esempio. Tuttavia, con altri insiemi di dati potresti vedere dei conteggi di documenti in errore. Se hai qualche conteggio di documenti errato, puoi visualizzare l'API di avvisi per vedere i messaggi di errore. Consulta la sezione [qui![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery#query-system-notices){: new_window} per esaminare il comando dell'API di avvisi.

La sezione `training` della restituzione ti fornisce informazioni sulla tua formazione. Riesamineremo tale sezione dopo che avrai caricato i tuoi dati di formazione.

## Aggiunta di dati di formazione in Discovery
{: #trainingdata-rnr}

Il servizio Watson {{site.data.keyword.discoveryshort}} utilizza un modello di machine learning per riclassificare i documenti. Per eseguire tale operazione, devi formare un modello. La formazione si verifica dopo che hai caricato una quantità sufficiente di query insieme agli appropriati documenti valutati. Caricando una quantità sufficiente di esempi con una varietà sufficiente su Watson {{site.data.keyword.discoveryshort}}, lo stai istruendo a riconoscere in cosa consiste un "buon" documento. In questo passo, utilizzeremo il "ground truth" Cranfield esistente che viene utilizzato in {{site.data.keyword.retrieveandrankshort}} per formare Watson {{site.data.keyword.discoveryshort}}.

1.  Scarica il [file csv di ground truth Cranfield ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-gt.csv){: new_window} di esempio dall'esercitazione {{site.data.keyword.retrieveandrankshort}}, se non lo hai già fatto.

   Il file è una serie di domande che un utente potrebbe porre in merito ai documenti. Il file fornisce le informazioni di esempio per formare il classificatore in {{site.data.keyword.retrieveandrankshort}} e la formazione della pertinenza in {{site.data.keyword.discoveryshort}} sulle domande e le risposte pertinenti.

   Per ogni domanda, c'è almeno un identificativo per una risposta (l'ID documento). Ogni ID documento include un numero per indicare quanto la risposta sia pertinente alla domanda. L'ID documento punta alla risposta nel file `cranfield-data.json` che hai caricato su {{site.data.keyword.discoveryshort}} nel passo precedente.

1.  Scarica lo script di caricamento dei dati di formazione. Utilizzerai questo script per caricare i dati di formazione in {{site.data.keyword.discoveryshort}}. Lo script trasforma il file `csv` in una serie di query ed esempi JSON e li invia al servizio {{site.data.keyword.discoveryshort}} utilizzando le [API dei dati di formazione![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery#list-training-data){: new_window}
    **Nota:** {{site.data.keyword.discoveryshort}} gestisce i dati di formazione nel servizio in modo che, quando vengono generati nuovi esempi e query di formazione, sia possibile archiviarli in {{site.data.keyword.discoveryshort}} stesso invece che come parte di un file CSV separato che è necessario gestire.
1.  Esegui lo script di caricamento di formazione per caricare i dati di formazione in {{site.data.keyword.discoveryshort}}. Sostituisci `{apikey_value}`, `{path_to_file}`, `{environment_id}`, `{collection_id}` con le tue informazioni. Nota che ci sono delle opzioni aggiuntive, `-d` per il debug e `–v` per l'output dettagliato da curl.

    ```bash
    python ./disco-train.py -u apikey:{apikey_value} -i {path_to_file}/cranfield-gt.csv –e {environment_id} -c {collection_id}
    ```
    {: pre}

1.  Una volta caricati i dati, puoi controllare lo stato della formazione utilizzando il comando dei dettagli della raccolta che abbiamo visto nella sezione precedente. {{site.data.keyword.discoveryshort}} eseguirà il controllo circa una volta all'ora per verificare se sono presenti dei nuovi dati e, in caso affermativo, inizierà ad elaborarli e a trasformarli in un modello di machine learning. Quando un modello è in fase di formazione, vedrai lo stato della sezione di formazione cambiare da `"processing": false` a `"processing": true`. Dopo che il modello sarà stato formato, vedrai lo stato nella sezione di formazione cambiare da `"available": false` a `"available": true`. Vedrai anche la variazione della data per il valore `"successfully_trained"`.  Se sono presenti eventuali errori, puoi consultarli visualizzando l'**API di avvisi** come descritto nella sezione precedente.

## Ricerca di documenti
{: #search-rnr}

Il servizio {{site.data.keyword.discoveryshort}} utilizzerà automaticamente un modello formato per riclassificare i risultati della ricerca, se disponibile. Quando viene eseguita [una chiamata API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window} con `natural_language_query` invece di `query`, viene effettuato un controllo per appurare se è disponibile un modello. Se è disponibile un modello, {{site.data.keyword.discoveryshort}} lo utilizza per riclassificare i risultati. Eseguiremo innanzitutto una ricerca sui documenti non classificati ed eseguiremo quindi una ricerca utilizzando il modello di classificazione.

1.  Puoi cercare documenti nella tua raccolta utilizzando un comando cURL. Esegui una query utilizzando la chiamata API query per visualizzare i risultati non classificati. Sostituisci `{apikey_value}`, `{environment_id}` e `{collection_id}` con i tuoi valori.  I risultati restituiti saranno risultati non classificati e utilizzerai le formule di classificazione {{site.data.keyword.discoveryshort}} predefinite. Puoi provare altre query aprendo il file `csv` dei dati di formazione e copiando il valore della prima colonna nel parametro di query.

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query=what is the basic mechanism of the transonic aileron buzz"
    ```
    {: pre}

1.  Esegui ora una ricerca utilizzando il modello impostando il parametro `natural_language_query`. Prima di eseguire tale operazione, assicurati di controllare che disponi di un modello formato come descritto nella sezione precedente.  Incolla il seguente codice nella tua console, sostituendo `{apikey_value}`, `{environment_id}` e `{collection_id}` con i tuoi valori.

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&natural_language_query=what is the basic mechanism of the transonic aileron buzz"
    ```
    {: pre}

    Questo comando restituirà dei risultati riclassificati utilizzando il modello che tu hai formato in precedenza. Confronta i risultati di questa ricerca e i risultati di qualcuna delle altre ricerche che hai provato in precedenza. Potresti vedere qualche differenza nei risultati rispetto a quanto vedi in {{site.data.keyword.retrieveandrankshort}}. Ciò è dovuto al fatto che alcune delle tecniche utilizzate per la ricerca sono cambiate per semplificare l'esperienza e migliorare i risultati ma, globalmente, la qualità dei risultati sarà simile.

Dopo aver valutato i risultati della ricerca riclassificati, puoi affinarli in {{site.data.keyword.discoveryshort}} ripetendo il passo di caricamento dei dati di formazione con ulteriori query ed esempi di formazione e visualizzando i risultati della ricerca.  Puoi anche aggiungere dei nuovi documenti, come descritto nel primo passo, per ampliare l'ambito della ricerca. Analogamente a {{site.data.keyword.retrieveandrankshort}}, il miglioramento dei risultati con la formazione è un processo iterativo.
