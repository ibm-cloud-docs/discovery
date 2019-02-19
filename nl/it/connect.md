---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-14"

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

# Connessione alle origini dati 
{: #sources}

Il servizio {{site.data.keyword.discoveryshort}} ti consente di collegarti e di effettuare una ricerca per indicizzazione dei documenti dalle origini remote.
{: shortdesc}

Puoi collegarti a un'origine dati ed estrarre i documenti su una pianificazione (se desiderato) nel servizio {{site.data.keyword.discoveryshort}} configurando una raccolta da associare a tale origine. Ogni raccolta può essere configurata con un'origine dati. Il servizio {{site.data.keyword.discoveryshort}} estrae i documenti dall'origine dati utilizzando un processo denominato indicizzazione. L'indicizzazione è il processo di selezione sistematica e di richiamo dei documenti dall'ubicazione di partenza specificata. Solo gli elementi specificati in modo esplicito vengono indicizzati dal servizio {{site.data.keyword.discoveryshort}}. I seguenti tipi di origini dati possono essere indicizzati:

-  [Box](/docs/services/discovery/connect.html#connectbox)
-  [Salesforce](/docs/services/discovery/connect.html#connectsf)
-  [Microsoft SharePoint Online](/docs/services/discovery/connect.html#connectsp)

La connessione a un'origine dati può essere eseguita utilizzando la strumentazione {{site.data.keyword.discoveryshort}} o l'API. La strumentazione {{site.data.keyword.discoveryshort}} fornisce un metodo semplificato di connessione che richiede meno informazioni sui sistemi di origine e l'API fornisce un'interfaccia più granulare e altamente configurabile che richiede maggiori informazioni sull'origine a cui ti stai collegando. La seguente panoramica del processo ti permette di sapere quali sezioni di questo documento leggere successivamente:

1.  Leggi i [Requisiti dell'origine generali](/docs/services/discovery/connect.html#gen_req) per avere una comprensione generale di ciò che sarà necessario.
2.  Leggi i requisiti specifici per il tuo sistema di origine:
    -  [Box](/docs/services/discovery/connect.html#connectbox)
    -  [Salesforce](/docs/services/discovery/connect.html#connectsf)
    -  [Microsoft SharePoint Online](/docs/services/discovery/connect.html#connectsp)
3.  Leggi le istruzioni di configurazione dell'origine in base alla tua scelta di configurazione:
    -  [Utilizzo della strumentazione](/docs/services/discovery/connect.html#source_tooling)
    -  [Utilizzo dell'API](/docs/services/discovery/connect.html#source_api)

## Requisiti dell'origine generali 
{: #gen_req}

I seguenti requisiti generali si applicano a tutte le origini dati:

-  Il limite di dimensione di file documento singolo per Box, Salesforce e SharePoint Online è 10MB.
-  Avrai bisogno delle credenziali e delle ubicazioni dei file (o URL) per ogni origine dati - queste sono normalmente fornite da uno sviluppatore/amministratore di sistema dell'origine dati.
-  Dovrai conoscere quali risorse dell'origine dati indicizzare. Queste possono essere fornite dall'amministratore dell'origine. Quando esegui l'indicizzazione di Box o Salesforce, viene presentato un elenco di risorse disponibili quando configuri un'origine utilizzando la strumentazione {{site.data.keyword.discoveryshort}}.
-  L'indicizzazione in un'origine dati utilizzerà le risorse (chiamate API) dell'origine dati. Il numero di chiamate dipende dal numero di documenti indicizzati. Deve essere ottenuto un livello di servizio appropriato (ad esempio Enterprise) per l'origine dati e deve essere consultato l'amministratore del sistema di origine.
-  I seguenti tipi di file possono essere inseriti da {{site.data.keyword.discoveryshort}}, tutti gli altri tipi di documento vengono ignorati:
   -  Microsoft Word
   -  PDF
   -  HTML
   -  JSON
-  Le indicizzazioni dell'origine {{site.data.keyword.discoveryshort}} non eliminano i documenti archiviati in una raccolta. Quando un'origine viene nuovamente indicizzata, i nuovi documenti vengono aggiunti, il documento aggiornato viene modificato nella versione corrente e i documenti eliminati sono conservati come ultima versione archiviata.

## Box
{: #connectbox}

Quando ti colleghi a un'origine Box, assicurati che l'istanza a cui prevedi di collegarti sia un piano Enterprise o superiore.

Configurazione di un account di Box per utilizzare {{site.data.keyword.discoveryshort}}:

1.  Crea una nuova applicazione personalizzata Box all'indirizzo `https://app.box.com/developers/console` (utilizza l'URL di Box aziendale).
1.  Effettua una delle seguenti operazioni: 
    - Seleziona l'**Application access** di `Enterprise`, poi continua utilizzando gli utenti gestiti esistenti.
      OPPURE
    - Seleziona l'**Application access** di `Application` e crea un'`Application User` con l'applicazione appena creata utilizzando l'[API Box ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.box.com/reference#create-app-user){: new_window}.
1.  Abilita i seguenti **Application Scopes**:
    - `Read and Write All Folders Stored In Box`
    - `Manage Users`
1.  Abilita le seguenti **Advanced Features**
    - `Perform Actions as Users`
    - `Generate User Access Tokens`
1.  Fai autorizzare il tuo ID client dell'applicazione dall'amministratore `https://app.box.com/master/settings/openbox` immettendo il `Client ID` da `https://app.box.com/developers/console` nel campo `API Key`.
1.  Genera `public/private keypair` (verrà scaricato sul tuo computer).
1.  Apri il file scaricato e copia/incolla i campi in {{site.data.keyword.discoveryshort}}. Rimuovi la nuova riga finale `\n` alla fine di `privateKey` quando copi in {{site.data.keyword.discoveryshort}}.

**Nota:** {{site.data.keyword.discoveryshort}} non supporta l'indicizzazione dell'applicazione personalizzata per se stessa (non puoi impersonare te stesso). 

Le seguenti credenziali sono necessarie per il collegamento a un'origine Box, devono essere ottenute dall'amministratore di Box (a meno che non le hai già ottenute impostando un'applicazione personalizzata Box utilizzando i passi precedenti):

-  `client_id` - Il `client_id` dell'origine a cui si collegano queste credenziali.    
-  `enterprise_id` - L'`enterprise_id` del sito di Box a cui si collegano queste credenziali.
-  `client_secret` - Il `client_secret` dell'origine a cui si collegano queste credenziali. Questo valore non viene mai restituito e viene utilizzato solo quando crei o modifichi le credenziali.
-  `public_key_id` - Il `public_key_id` dell'origine a cui si collegano queste credenziali. Questo valore non viene mai restituito e viene utilizzato solo quando crei o modifichi le credenziali.
-  `private_key` - Il `private_key` dell'origine a cui si collegano queste credenziali. Questo valore non viene mai restituito e viene utilizzato solo quando crei o modifichi le credenziali.
-  `passphrase` - Il `passphrase` dell'origine a cui si collegano queste credenziali. Questo valore non viene mai restituito e viene utilizzato solo quando crei o modifichi le credenziali.

Quando identifichi le credenziali, potrebbe essere utile consultare la [documentazione dello sviluppatore Box ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.box.com/){: new_window}.

Altri elementi da considerare durante l'indicizzazione con Box:

-  Le note Box sono archiviate nel formato JSON, per cui tutte le note Box nelle cartelle specificate saranno inserite da {{site.data.keyword.discoveryshort}}.
-  Quando utilizzi l'API, dovrai disporre di un elenco di ID cartelle e dell'ID proprietario associato ad ogni cartella che vuoi indicizzare. La strumentazione {{site.data.keyword.discoveryshort}} ti consente di sfogliare e selezionare il contenuto da indicizzare.

## Salesforce
{: #connectsf}

Quando ti colleghi a un'origine Salesforce, assicurati che l'istanza a cui prevedi di collegarti sia un piano Enterprise o superiore.

Le seguenti credenziali sono necessarie per il collegamento a un'origine Salesforce, devono essere ottenute dall'amministratore di Salesforce: 
-  `url` - L'`url` dell'origine a cui si collegano queste credenziali. 
-  `username` - L'`username` dell'origine a cui si collegano queste credenziali. 
-  `password` - La `password` è costituita dalla password Salesforce e da un token di sicurezza Salesforce valido concatenato. Questo valore non viene mai restituito e viene utilizzato solo quando crei o modifichi le credenziali.

Quando identifichi le credenziali, potrebbe essere utile consultare la [documentazione dello sviluppatore Salesforce ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.salesforce.com/docs/){: new_window}.

Altri elementi da considerare durante l'indicizzazione con Salesforce:

-  Gli articoli Knowledge vengono indicizzati solo se **version** è `published` e la lingua è `en-us`.
-  Quando utilizzi l'API, dovrai disporre di un elenco di oggetti Salesforce che vuoi indicizzare. La strumentazione {{site.data.keyword.discoveryshort}} ti consente di sfogliare e selezionare il contenuto da indicizzare.


## SharePoint Online
{: #connectsp}

Quando ti colleghi a un'origine Microsoft SharePoint Online assicurati che l'istanza a cui prevedi di collegarti sia un piano Enterprise (E1) o superiore.

Le seguenti credenziali sono necessarie per il collegamento a un'origine SharePoint Online, devono essere ottenute dall'amministratore di SharePoint: 

-  `organization_url` - L'`organization_url` dell'origine a cui si collegano queste credenziali. 
-  `site_collection.path` - Il `site_collection.path` dell'origine a cui si collegano queste credenziali. 
-  `username` - Il `client_id` dell'origine a cui si collegano queste credenziali.
-  `password` - La `password` dell'origine a cui si collegano queste credenziali. Questo valore non viene mai restituito e viene utilizzato solo quando crei o modifichi le credenziali.

Quando identifichi le credenziali, potrebbe essere utile consultare la [documentazione dello sviluppatore Microsoft SharePoint ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.microsoft.com/en-us/sharepoint/dev/){: new_window}.

Altri elementi da considerare durante l'indicizzazione con Microsoft SharePoint Online:

-  Quando indicizzi SharePoint, dovrai disporre di un elenco dei percorsi della raccolta del sito SharePoint che vuoi indicizzare. La strumentazione {{site.data.keyword.discoveryshort}} ti consente di sfogliare e selezionare il contenuto da indicizzare.Per indicizzare tutto il tuo sito SharePoint Online, non selezionare più percorsi (URL) in questo campo. In tale scenario, immetti una `/` nel campo `site_collection.path`.

## Utilizzo della strumentazione
{: #source_tooling}

La connessione a un'origine dati utilizzando la strumentazione {{site.data.keyword.discoveryshort}} viene eseguita creando una raccolta specifica per un'origine. Effettua le seguenti operazioni per creare una raccolta di origine e indicizzarla:

1.  Dalla pagina **Manage data** della strumentazione {{site.data.keyword.discoveryshort}}, seleziona **Connect a data source**.
2.  Seleziona l'origine dati a cui vuoi collegarti.
3.  Immetti le tue credenziali di origine e fai clic per collegarti. Le tue credenziali di origine devono essere ottenute dal tuo amministratore del sistema di origine.
4.  Scegli quali dati vuoi indicizzare e la frequenza con cui vuoi sincronizzarli.
5.  Fai clic su **Save & Sync objects** per avviare l'indicizzazione della tua origine dati. Vieni poi reindirizzato alla schermata dello stato della raccolta che si aggiorna quando vengono aggiunti documenti alla raccolta.

La ricerca per indicizzazione sincronizzerà i dati inizialmente e poi in base alla frequenza che hai specificato.
**Nota:** se modifichi qualcosa nella schermata **Sync settings** e poi fai clic su **Save and Sync objects** verrà avviata un'indicizzazione (o riavviata se ne è già in esecuzione una) in quel momento.

## Utilizzo dell'API
{: #source_api}

Utilizza il seguente processo per creare una raccolta collegata a un'origine dati utilizzando l'API.
1.  Crea le credenziali per l'origine a cui ti stai collegando utilizzando l'[API delle credenziali dell'origine ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#credentials-api){: new_window}. Registra il **credential_id** restituito delle credenziali appena create.
2.  Crea una nuova configurazione utilizzando [Configuration API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#configurations-api){: new_window}. Questa configurazione deve contenere un oggetto **source** che definisce cosa deve essere indicizzato. L'oggetto **source** deve contenere il **credential_id** che hai registrato precedentemente.
    ```json
    "source" : {
      "type" : "salesforce",
      "credential_id" : "{credential_id}",
      "schedule" : {
        "enabled" : true,
        "time_zone" : "America/New_York",
        "frequency" : "weekly"
      },
      "options" : {
         "site_collections" : [ {
         "site_collection_path" : "/sites/TestSiteA",
         "limit" : 10
         } ]
      }
    }
    ```
    {: codeblock}
Registra il **configuration_id** restituito della configurazione appena creata.
3.  Crea una nuova raccolta utilizzando [Collections API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#configurations-api){: new_window}. L'oggetto che definisce la raccolta deve contenere il **configuration_id** che hai registrato precedentemente.

L'indicizzazione dell'origine inizia non appena la raccolta viene creata e poi nuovamente in base alla frequenza che hai specificato.
**Nota:** se modifichi qualcosa nell'oggetto **source** della configurazione, sarà avviata una nuova ricerca per indicizzazione (o riavviata se ne è già in esecuzione una) in quel momento.

## Specifica di un `customer_id`
{:# source_customer_id}

Un campo `customer_id` in un documento inserito {{site.data.keyword.discoveryshort}} può essere utilizzato per eliminare il contenuto basato sul `customer_id` utilizzando il metodo **user-data** nell'API. I documenti in entrata da un'origine dati non sono automaticamente assegnati a un `customer_id` quando viene inserito. Se la tua applicazione richiede che venga definito un `customer_id`, puoi specificare che uno (o più) dei campi in entrata dal sistema di origine siano copiati e utilizzati come `customer_id`. A tale scopo devi modificare la configurazione che viene utilizzata per il collegamento all'origine.

1.  Esegui una query di esempio e identifica il campo che vuoi utilizzare come `customer_id`.
2.  Modifica la configurazione. Dovrai aggiungere una sezione **Normalization** per creare il campo `customer_id`.
    -  Nella strumentazione, passa alla tua raccolta e fai clic sul link **edit** nella sezione di configurazione. Successivamente, fai clic sulla scheda **Normalization** e aggiungi una normalizzazione **copy** per creare il campo `customer_id`. Fai quindi clic su **Apply & save**.
    ![Copia normalizzazione](images/norm_copy.png)
    -  Quando utilizzi l'API, aggiungi il seguente oggetto all'array **noramizations**"
       ```json
  {
         "operation" : "copy",
         "source_field" : "{original_field_name}",
         "destination_field" : "customer_id"
       }
       ```
       {: codeblock}
3.  La successiva indicizzazione pianificata aggiungerà il campo `customer_id` a tutti i documenti. Se vuoi che un'indicizzazione venga avviata immediatamente, modifica la configurazione di origine (**Sync settings** nella strumentazione).

Consulta [Informazioni sulla sicurezza di ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.bluemix.net/docs/services/discovery/information-security.html){: new_window} per ulteriori informazioni sull'eliminazione in base al `customer_id`.
