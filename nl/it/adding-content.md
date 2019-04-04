---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-03-07"

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

# Aggiunta di contenuto
{: #addcontent}

Come decido quale metodo di caricamento del documento utilizzare?
{: shortdesc}

-   Utilizza l'[API](/docs/services/discovery?topic=discovery-gs-api#gs-api) se stai integrando il caricamento del contenuto con un'applicazione esistente o creando il tuo meccanismo di caricamento personalizzato.
-   Utilizza la [Strumentazione {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-getting-started#getting-started) se vuoi caricare velocemente i file accessibili localmente.
    Quando carichi i documenti utilizzando la strumentazione {{site.data.keyword.discoveryshort}}, tutti i documenti devono avere un nome file univoco. Se due file hanno lo stesso nome, l'originale verrà sovrascritto quando viene caricata la versione più recente. Se preferisci che i documenti con lo stesso nome di file coesistano nella tua raccolta, deve essere specificato l'ID documento. Puoi specificare l'ID documento se carichi i documenti utilizzando l'API o il data crawler.
-   Utilizza la strumentazione {{site.data.keyword.discoveryshort}} o l'API per stabilire una connessione alle origini dati Box, Salesforce, Microsoft SharePoint Online, IBM Cloud Object Storage e Microsoft SharePoint 2016 o per eseguire una ricerca per l'indicizzazione web. Per ulteriori informazioni, vedi [Connessione alle origini dati](/docs/services/discovery?topic=discovery-sources#sources).
-   Utilizza il [Data Crawler](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler) se desideri avere un caricamento gestito di un numero significativo di file oppure se vuoi estrarre il contenuto da un repository supportato (come ad esempio un database DB2).

## Aggiunta di contenuto con l'API o la strumentazione
{: #adding-content-with-the-api-or-tooling}

Considera quanto segue quando sei pronto ad aggiungere i documenti alla tua raccolta:

-   La dimensione massima del file che può essere caricata sul servizio {{site.data.keyword.discoveryshort}} è 50MB.
-   I documenti di esempio non vengono aggiunti automaticamente alla raccolta. Devi aggiungerli se vuoi che facciano parte della tua raccolta. (Si applica solo alle raccolte create prima della release di [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu)).
-   Verranno arricchiti solo i primi 50.000 caratteri di ogni campo JSON selezionato per l'arricchimento.
-   Quando crei una raccolta, seleziona la lingua del documento (l'inglese è il valore predefinito). Consulta [Supporto linguistico](/docs/services/discovery?topic=discovery-language-support#language-support) per l'elenco delle lingue. I tuoi documenti saranno arricchiti nella lingua selezionata. Non mescolare le lingue all'interno della stessa raccolta.
-   I seguenti tipi di file possono essere inseriti da {{site.data.keyword.discoveryshort}}, tutti gli altri tipi di documento vengono ignorati:

Raccolta | Piani Lite | Piani Advanced 
---------------- | ------------------------------ | ------------------------------------------- 
Raccolte esistenti create specificamente per {{site.data.keyword.discoveryfull}} prima della release di [SDU (Smart Document Understanding)](/docs/services/discovery?topic=discovery-release-notes#22jan19) | Microsoft Word, PDF, HTML, JSON | Microsoft Word, PDF, HTML, JSON     
Raccolte create dopo la release di [SDU](/docs/services/discovery?topic=discovery-sdu#sdu) | PDF, Word, PowerPoint, Excel, JSON\*, HTML\* | PDF, Word, PowerPoint, Excel, PNG\*\*, TIFF\*\*, JPG\*\*, JSON\*, HTML\* 
    
\* I documenti JSON e HTML sono supportati da {{site.data.keyword.discoveryfull}} ma non possono essere modificati utilizzando l'editor SDU. Per modificare la configurazione di documenti HTML e JSON, devi utilizzare l'API. Per ulteriori informazioni, vedi la [Guida di riferimento API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery/){: new_window}.

\*\* I singoli file immagine (PNG, TIFF, JPG) vengono sottoposti a scansione e l'eventuale testo viene estratto. Anche le immagini PNG, TIFF e JPEG integrate in file PDF, Word, PowerPoint ed Excel verranno sottoposte a scansione e l'eventuale testo viene estratto.
-   I documenti nella tua raccolta verranno convertiti utilizzando la configurazione corrente, a meno che tu non scelga un file di configurazione differente. Per informazioni sulla creazione di un file di configurazione, consulta [Configurazione personalizzata](/docs/services/discovery?topic=discovery-configservice#custom-configuration). (Si applica solo alle raccolte create prima della release di [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu)).
-   Quando i documenti vengono caricati in una raccolta dati, vengono convertiti e arricchiti utilizzando il file di configurazione scelto per tale raccolta. Se decidi in seguito che vuoi passare una raccolta a un file di configurazione diverso, puoi farlo, ma i documenti che sono stati già caricati rimarranno convertiti dal file di configurazione originale. Tutti i documenti caricati dopo il passaggio al file di configurazione utilizzeranno il nuovo file di configurazione. Se vuoi che la raccolta **completa** utilizzi la nuova configurazione, dovrai creare una nuova raccolta, scegliere il nuovo file di configurazione e ricaricare tutti i documenti. (Se stai utilizzando [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu), ti verrà richiesto di ricaricare i tuoi documenti dopo che avrai fatto clic sul pulsante **Apply changes to collection**).
-   Non puoi specificare il `data type` (ad esempio: `text` o `date`) dei campi. Durante l'inserimento di un documento, se viene rilevato che un campo non esiste ancora nell'indice, {{site.data.keyword.discoveryshort}} individuerà automaticamente il `data type` di quel campo in base al valore del campo del primo documento indicizzato.
-   Un documento potrebbe non essere inserito a causa di una mancata corrispondenza del tipo tra i dati nel documento corrente e i dati simili in un documento precedentemente inserito. Ad esempio, un campo potrebbe essere immesso come `date` in un documento e `string` in un documento successivo, impedendo al documento successivo di essere indicizzato correttamente.
-   Se pianifichi di utilizzare la suddivisione in token personalizzata (al momento disponibile solo per le raccolte in giapponese quando utilizzi l'API {{site.data.keyword.discoveryshort}}), il dizionario di tokenizzazione per la tua raccolta deve essere aggiunto prima di caricare i documenti.

## Caricamento dei documenti con la strumentazione Discovery
{: #upload_tooling}

1.  Crea una raccolta. Vedi [Preparazione del servizio per i tuoi documenti](/docs/services/discovery?topic=discovery-configservice#preparing-the-service-for-your-documents).
1.  Fai clic sulla raccolta per aprirla.
1.  Fai clic sul pulsante **Upload documents** e avvia il caricamento dei tuoi documenti tramite il trascinamento e il rilascio o la selezione.

I tuoi documenti sono ora messi in coda per essere convertiti e arricchiti. Il tempo necessario dipenderà dalla dimensione della tua raccolta. Dopo che è stata indicizzata e arricchita, verranno visualizzati i dettagli della raccolta nella sezione **Overview**.

-   I campi identificati (**Fields identified**) nella tua raccolta (solo Smart Document Understanding).
-   Le date di creazione (**Created**) e ultimo aggiornamento (**Last updated**) (fai clic su **Use this collection in API** per visualizzare `collection_id`, `configuration_id`, e `environment_id`).
-   Il numero di documenti (**Number of documents**) nella tua raccolta
-   La configurazione (**Configuration**) — Il nome del file di configurazione utilizzato per convertire questa raccolta (solo per le raccolte create prima della release di [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu)).
-   Errori e avvertenze (**Errors and Warnings**)

Per informazioni su come connettersi alle origini dati Box, Salesforce, Microsoft SharePoint Online, IBM Cloud Object Storage e Microsoft SharePoint 2016 o su come eseguire una ricerca per l'indicizzazione con la strumentazione {{site.data.keyword.discoveryshort}}, vedi [Connessione alle origini dati](/docs/services/discovery?topic=discovery-sources#sources).


## Caricamento dei documenti con l'API
{: #upload_api}

Consulta [Introduzione all'{{site.data.keyword.discoveryshort}}API](/docs/services/discovery?topic=discovery-gs-api#gs-api) per una procedura dettagliata .

Per ulteriori informazioni sull'API, consulta il [riferimento API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery/){: new_window}.

1.  Utilizza il metodo `POST /v1/environments/{environment_id}/collections` per creare una raccolta.
1.  Poi utilizza il metodo `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` per aggiungere i documenti alla tua raccolta.

## Ricerca per l'indicizzazione degli URL
{: #crawl_urls}

Puoi eseguire la ricerca per l'indicizzazione degli URL e indicizzarli utilizzando il servizio {{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} {{site.data.keyword.discoveryshort}} [Indexing plugin for Apache Nutch ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/IBM-Watson/nutch-indexer-discovery). La ricerca per l'indicizzazione non si aggiorna automaticamente, per cui la procedura dovrà essere ripetuta periodicamente per mantenere l'indice aggiornato. 

Hai anche l'opzione di utilizzare il connettore Web Crawl beta. Vedi [Connessione alle origini dati](/docs/services/discovery?topic=discovery-sources#connectwebcrawl).
