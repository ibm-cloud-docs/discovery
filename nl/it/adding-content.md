---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-15"

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

# Aggiunta di contenuto
{: #addcontent}

Come decido quale metodo di caricamento del documento utilizzare?
{: shortdesc}

-   Utilizza l'[API](/docs/services/discovery/getting-started.html) se stai integrando il caricamento del contenuto con un'applicazione esistente o creando il tuo meccanismo di caricamento personalizzato.
-   Utilizza la [Strumentazione {{site.data.keyword.discoveryshort}}](/docs/services/discovery/getting-started-tool.html) se vuoi caricare velocemente i file accessibili localmente.
    Quando carichi i documenti utilizzando la strumentazione {{site.data.keyword.discoveryshort}}, tutti i documenti devono avere un nome file univoco. Se due file hanno lo stesso nome, l'originale verrà sovrascritto quando viene caricata la versione più recente. Se preferisci che i documenti con lo stesso nome di file coesistano nella tua raccolta, deve essere specificato l'ID documento. Puoi specificare l'ID documento se carichi i documenti utilizzando l'API o il data crawler.
-   Utilizza la strumentazione {{site.data.keyword.discoveryshort}} o l'API per il collegamento alle origini dati Box, Salesforce e Microsoft SharePoint Online. Per ulteriori informazioni, vedi [Connessione alle origini dati](/docs/services/discovery/connect.html).
-   Utilizza il [Data Crawler](/docs/services/discovery/data-crawler.html) se desideri avere un caricamento gestito di un numero significativo di file oppure se vuoi estrarre il contenuto da un repository supportato (come ad esempio un database DB2).

## Aggiunta di contenuto con l'API o la strumentazione

Considera quanto segue quando sei pronto ad aggiungere i documenti alla tua raccolta:

-   La dimensione massima del file che può essere caricata sul servizio {{site.data.keyword.discoveryshort}} è 50MB.
-   I documenti di esempio non vengono aggiunti automaticamente alla raccolta. Devi aggiungerli se vuoi che facciano parte della tua raccolta.
-   Verranno arricchiti solo i primi 50.000 caratteri di ogni campo JSON selezionato per l'arricchimento.
-   Quando crei una raccolta, seleziona la lingua del documento (l'inglese è il valore predefinito). Consulta [Supporto linguistico](/docs/services/discovery/language-support.html) per l'elenco delle lingue. I tuoi documenti saranno arricchiti nella lingua selezionata. Non mescolare le lingue all'interno della stessa raccolta.
-   Puoi aggiungere documenti Microsoft Word, PDF, HTML e JSON alla tua raccolta. **Nota:** i PDF che sono file di immagini scansionate non possono essere convertiti e arricchiti.
-   I documenti presenti nella tua raccolta verranno convertiti utilizzando il file di configurazione fornito, che viene denominato Default Configuration, a meno che non scegli un file di configurazione diverso. Per informazioni sulla creazione di un file di configurazione, consulta [Configurazione personalizzata](/docs/services/discovery/building.html#custom-configuration).
-   Quando i documenti vengono caricati in una raccolta dati, vengono convertiti e arricchiti utilizzando il file di configurazione scelto per tale raccolta. Se decidi in seguito che vuoi passare una raccolta a un file di configurazione diverso, puoi farlo, ma i documenti che sono stati già caricati rimarranno convertiti dal file di configurazione originale. Tutti i documenti caricati dopo il passaggio al file di configurazione utilizzeranno il nuovo file di configurazione. Se vuoi che la raccolta **completa** utilizzi la nuova configurazione, dovrai creare una nuova raccolta, scegliere il nuovo file di configurazione e ricaricare tutti i documenti.
-   Non puoi specificare il `data type` (ad esempio: `text` o `date`) dei campi. Durante l'inserimento di un documento, se viene rilevato che un campo non esiste ancora nell'indice, {{site.data.keyword.discoveryshort}} individuerà automaticamente il `data type` di quel campo in base al valore del campo del primo documento indicizzato.
-   Un documento potrebbe non essere inserito a causa di una mancata corrispondenza del tipo tra i dati nel documento corrente e i dati simili in un documento precedentemente inserito. Ad esempio, un campo potrebbe essere immesso come `date` in un documento e `string` in un documento successivo, impedendo al documento successivo di essere indicizzato correttamente.
-   Se pianifichi di utilizzare la suddivisione in token personalizzata (al momento disponibile solo per le raccolte in giapponese quando utilizzi l'API {{site.data.keyword.discoveryshort}}), il dizionario di tokenizzazione per la tua raccolta deve essere aggiunto prima di caricare i documenti.

I seguenti limiti si applicano quando si caricano i documenti:

-   Piani **Lite**: 21 documenti in elaborazione
-   Piani **Advanced**: 105 documenti in elaborazione (tranne i piani avanzati X-Small, che hanno un limite di 50 documenti in elaborazione)
-   Piani **Premium**: 210 documenti in elaborazione

Questi limiti sono soggetti a cambiamento. 

Quando utilizzi il servizio Discovery, il caricamento in elaborazione rappresenta il documento caricato ed elaborato prima che venga aggiunto alla raccolta. Se raggiungi il tuo limite di elaborazione, dovresti rallentare la velocità del tuo inserimento. Un'opzione potrebbe essere di aggiungere un meccanismo di interruzione automatizzato con i nuovi tentativi.

## Caricamento dei documenti con la strumentazione Discovery

1.  Crea una raccolta. Vedi [Preparazione del servizio per i tuoi documenti](/docs/services/discovery/building.html#preparing-the-service-for-your-documents).
1.  Fai clic sulla raccolta per aprirla.
1.  Fai clic sul pulsante **Upload documents** e avvia il caricamento dei tuoi documenti tramite il trascinamento e il rilascio o la selezione.

I tuoi documenti sono ora messi in coda per essere convertiti e arricchiti. Il tempo necessario dipenderà dalla dimensione della tua raccolta. Dopo che è stata indicizzata e arricchita, verranno visualizzati i dettagli della raccolta nella sezione **Overview**.

-   Date **Created** e **Last updated** (fai clic su **Use this collection in API** per visualizzare `collection_id`, `configuration_id`, e `environment_id`.)
-   **Number of documents** nella tua raccolta
-   **Configuration** — Il nome del file di configurazione utilizzato per convertire questa raccolta
-   **Errors and Warnings**

Per informazioni su come collegarti alle origini dati Box, Salesforce e Microsoft SharePoint Online con la strumentazione {{site.data.keyword.discoveryshort}}, consulta [Connessione alle origini dati](/docs/services/discovery/connect.html).


## Caricamento dei documenti con l'API

Consulta [Introduzione all'{{site.data.keyword.discoveryshort}}API](/docs/services/discovery/getting-started.html) per una procedura dettagliata .

Per ulteriori informazioni sull'API, consulta il [riferimento API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}.

1.  Utilizza il metodo `POST /v1/environments/{environment_id}/collections` per creare una raccolta.
1.  Poi utilizza il metodo `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` per aggiungere i documenti alla tua raccolta.

## Indicizzazione degli URL

Puoi eseguire la ricerca per indicizzazione degli URL e indicizzarli utilizzando il servizio {{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} {{site.data.keyword.discoveryshort}} [Indexing plugin for Apache Nutch ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/IBM-Watson/nutch-indexer-discovery). L'indicizzazione non si aggiorna automaticamente, per cui la procedura dovrà essere ripetuta periodicamente per mantenere l'indice aggiornato.
