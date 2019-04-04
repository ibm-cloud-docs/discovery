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

# Connessione alle origini dati
{: #sources}

Il servizio {{site.data.keyword.discoveryshort}} ti consente di collegarti e di effettuare una ricerca per la ricerca per l'indicizzazione dei documenti dalle origini remote.
{: shortdesc}

Puoi collegarti a un'origine dati ed estrarre i documenti su una pianificazione (se desiderato) nel servizio {{site.data.keyword.discoveryshort}} configurando una raccolta da associare a tale origine. Ogni raccolta può essere configurata con una origine dati in caso di utilizzo della strumentazione {{site.data.keyword.discoveryshort}}; in caso di utilizzo dell'API, puoi inviare i documenti da più origini dati in una singola raccolta. Il servizio {{site.data.keyword.discoveryshort}} estrae i documenti dall'origine dati utilizzando un processo denominato ricerca per l'indicizzazione. La ricerca per l'indicizzazione è il processo di selezione sistematica e di richiamo dei documenti dall'ubicazione di partenza specificata. Solo gli elementi specificati in modo esplicito vengono sottoposti a una ricerca per l'indicizzazione dal servizio {{site.data.keyword.discoveryshort}}. I seguenti tipi di origini dati possono essere sottoposti a una ricerca per l'indicizzazione:

-  [Box](/docs/services/discovery?topic=discovery-sources#connectbox)
-  [Salesforce](/docs/services/discovery?topic=discovery-sources#connectsf)
-  [Microsoft SharePoint Online](/docs/services/discovery?topic=discovery-sources#connectsp)
-  [Microsoft SharePoint 2016 in loco](/docs/services/discovery?topic=discovery-sources#connectsp_op)
-  [Web Crawl](/docs/services/discovery?topic=discovery-sources#connectwebcrawl) (beta)
-  [IBM Cloud Object Storage](/docs/services/discovery?topic=discovery-sources#connectcos)

La connessione a un'origine dati può essere eseguita utilizzando la strumentazione {{site.data.keyword.discoveryshort}} o l'API. La strumentazione {{site.data.keyword.discoveryshort}} fornisce un metodo semplificato di connessione che richiede meno informazioni sui sistemi di origine e l'API fornisce un'interfaccia più granulare e altamente configurabile che richiede maggiori informazioni sull'origine a cui ti stai collegando. La seguente panoramica del processo ti permette di sapere quali sezioni di questo documento leggere successivamente:

1.  Leggi i [Requisiti dell'origine generali](/docs/services/discovery?topic=discovery-sources#gen_req) per avere una comprensione generale di ciò che sarà necessario.
2.  Leggi i requisiti specifici per il tuo sistema di origine:
    -  [Box](/docs/services/discovery?topic=discovery-sources#connectbox)
    -  [Salesforce](/docs/services/discovery?topic=discovery-sources#connectsf)
    -  [Microsoft SharePoint Online](/docs/services/discovery?topic=discovery-sources#connectsp)
    -  [Microsoft SharePoint 2016 in loco](/docs/services/discovery?topic=discovery-sources#connectsp_op)
    -  [Web Crawl](/docs/services/discovery?topic=discovery-sources#connectwebcrawl) (beta)
    -  [IBM Cloud Object Storage](/docs/services/discovery?topic=discovery-sources#connectcos)
3.  Leggi le istruzioni di configurazione dell'origine in base alla tua scelta di configurazione:
    -  [Utilizzo della strumentazione](/docs/services/discovery?topic=discovery-sources#source_tooling)
    -  [Utilizzo dell'API](/docs/services/discovery?topic=discovery-sources#source_api)

Se selezioni un'origine dati in loco, devi prima installare e configurare IBM Secure Gateway. Per ulteriori informazioni, vedi [Installazione di IBM Secure Gateway per i dati in loco](/docs/services/discovery?topic=discovery-sources#gateway).

## Requisiti dell'origine generali
{: #gen_req}

I seguenti requisiti generali si applicano a tutte le origini dati:

-  Il limite di dimensione di singolo file di documento per Box, Salesforce, SharePoint Online, SharePoint 2016, IBM Cloud Object Storage e Web Crawl è 10MB.
-  Avrai bisogno delle credenziali e delle ubicazioni dei file (o URL) per ogni origine dati - queste sono normalmente fornite da uno sviluppatore/amministratore di sistema dell'origine dati.
-  Dovrai conoscere quali sono le risorse dell'origine dati di cui eseguire la ricerca per l'indicizzazione. Queste possono essere fornite dall'amministratore dell'origine. Quando esegui la ricerca per l'indicizzazione di Box o Salesforce, viene presentato un elenco di risorse disponibili quando configuri un'origine utilizzando la strumentazione {{site.data.keyword.discoveryshort}}.
-  In caso di utilizzo della strumentazione {{site.data.keyword.discoveryshort}}, una raccolta può essere configurata con una singola origine dati. In caso di utilizzo dell'API, i documenti da più origini dati possono essere inviati in una singola raccolta.
-  La ricerca per l'indicizzazione in un'origine dati utilizzerà le risorse (chiamate API) dell'origine dati. Il numero di chiamate API dipende dal numero di documenti di cui bisogna eseguire la ricerca per l'indicizzazione. Deve essere ottenuto un livello di licenza di servizio appropriato (ad esempio Enterprise) per l'origine dati e deve essere consultato l'amministratore del sistema di origine.
-  Le ricerche per l'indicizzazione dell'origine {{site.data.keyword.discoveryshort}} non eliminano i documenti archiviati in una raccolta. Quando un'origine viene nuovamente sottoposta a una ricerca per l'indicizzazione, i nuovi documenti vengono aggiunti, il documento aggiornato viene modificato nella versione corrente e i documenti eliminati sono conservati come ultima versione archiviata.
-  I seguenti tipi di file possono essere inseriti da {{site.data.keyword.discoveryshort}}, tutti gli altri tipi di documento vengono ignorati:

Raccolta | Piani Lite | Piani Advanced 
---------------- | ------------------------------ | ------------------------------------------- 
Raccolte esistenti create specificamente per {{site.data.keyword.discoveryfull}} prima della release di [SDU (Smart Document Understanding)](/docs/services/discovery?topic=discovery-release-notes#22jan19) | Microsoft Word, PDF, HTML, JSON | Microsoft Word, PDF, HTML, JSON     
Raccolte create dopo la release di [SDU](/docs/services/discovery?topic=discovery-sdu#sdu) | PDF, Word, PowerPoint, Excel, JSON\*, HTML\* | PDF, Word, PowerPoint, Excel, PNG\*\*, TIFF\*\*, JPG\*\*, JSON\*, HTML\* 
    
\* I documenti JSON e HTML sono supportati da {{site.data.keyword.discoveryfull}} ma non possono essere modificati utilizzando l'editor SDU. Per modificare la configurazione di documenti HTML e JSON, devi utilizzare l'API. Per ulteriori informazioni, vedi la [Guida di riferimento API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery/){: new_window}.

\*\* I singoli file immagine (PNG, TIFF, JPG) vengono sottoposti a scansione e l'eventuale testo viene estratto. Anche le immagini PNG, TIFF e JPEG integrate in file PDF, Word, PowerPoint ed Excel verranno sottoposte a scansione e l'eventuale testo viene estratto.

## Box
{: #connectbox}

Dovrai creare una nuova applicazione personalizzata Box per stabilire una connessione a {{site.data.keyword.discoveryfull}}. L'applicazione Box che crei richiede un accesso di livello Enterprise o Applicazione.

-  Se non sei l'amministratore Box per la tua organizzazione, è consigliato l'[accesso di **livello Applicazione**](/docs/services/discovery?topic=discovery-sources#applevelbox). Avrai bisogno di un amministratore che approvi la tua applicazione.
-  Se sei l'amministratore Box per la tua organizzazione, è consigliato un [accesso di **livello Enterprise**](/docs/services/discovery?topic=discovery-sources#entlevelbox).

I passi per configurare l'accesso Box possono variare, se c'è un aggiornamento di Box. Consulta la [documentazione per gli sviluppatori Box ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.box.com/){: new_window} per gli aggiornamenti.
{: note}

### Configurazione dell'accesso di livello Applicazione
{: #applevelbox}

1.   Vai a `https://app.box.com/developers/console` (utilizza l'URL Box della tua azienda) e fai clic su **Create New App**.
1.   Dalla schermata **Create a New App**, seleziona **Enterprise Integration** e fai clic su **Next**.
1.   Nella schermata **Authentication Method**, seleziona **OAuth 2.0 with JWT (Server Authentication)** e fai clic su **Next**.
1.   Denomina la tua applicazione e fai clic sul pulsante **Create App**. Dopo che la tua applicazione Box è stata creata, fai clic su **View Your App**.
1.   Durante la visualizzazione della tua applicazione, seleziona **Application access** come **Application**. Puoi utilizzare i tuoi utenti gestiti esistenti man mano che continui; non devi necessariamente crearne di nuovi.
1.   Scorri in basso fino alla sezione **Application Scopes** della pagina e abilita le seguenti caselle di spunta: 
     - `Read and write all folders stored in Box`
     - `Manage Users`
1.   Scorri verso il basso fino alla sezione **Advanced Features** e abilita i seguenti interruttori:
     - `Perform Actions as Users`
     - `Generate User Access Tokens` 
1.  Fai clic sul pulsante **Save Changes**.

I prossimi passi richiederanno l'assistenza dell'amministratore dell'account Box della tua organizzazione. Se non sei l'amministratore Box della tua organizzazione, puoi identificarlo aprendo una console dello sviluppatore di Box e controllando sotto **Account settings** > **Account details** > **Settings**.

1.  [Passo dell'amministratore] Autorizza il tuo id client dell'applicazione a `https://app.box.com/master/settings/openbox` facendo clic sul pulsante **Authorize New App**.
1.  [Passo dell'amministratore] Immetti l'**ID client**) da `https://app.box.com/developers/console` nel campo **API key** e fai quindi clic sul pulsante **Authorize**.
1.  [Passo dell'amministratore] Richiama un token dello sviluppatore per l'applicazione. Per eseguire questa operazione, vai a `https://app.box.com/developers/console`, scorri alla sezione **Developer Token** e genera il tuo token.
1.  Ora che l'applicazione è stata autorizzata dall'amministratore, vai a `https://developer.box.com/reference#page-create-an-enterprise-user` e crea un utente dell'applicazione utilizzando la pagina di riferimento API.

   Esempio Curl per creare un utente dell'applicazione:

   ```bash
    curl https://api.box.com/2.0/users -H "Authorization: Bearer ACCESS_TOKEN" -d '{"name": "NedStark", "is_platform_access_only": true}' -X POST
   ```
   {: pre}

1.  Copia il contenuto del campo **id** appena generato e forniscilo al non amministratore che connette l'applicazione Box a {{site.data.keyword.discoveryfull}}.
1.  Una volta creato l'utente dell'applicazione, è necessario condividere con tale utente le cartelle di cui desideri eseguire la ricerca per l'indicizzazione e bisogna concedergli le autorizzazioni di `Viewer` su tali cartelle. Ciò richiede il nome di accesso dell'utente dell'applicazione dalla risposta al comando curl di cui sopra. Esempio: `"login":"AppUser_737729_jmUo@boxdevedition.com"`.
1.  Ritorna alla console per gli sviluppatori Box `https://app.box.com/developers/console` e scorri alla sezione **Add and Manage Public Keys**. Fai clic su **Generate the public/private keypair** e scarica il tuo file di coppia di chiavi. Apri il file.
1.  Dal file di coppia di chiavi, taglia e incolla i seguenti campi nella strumentazione {{site.data.keyword.discoveryshort}}.
    -  `client_id`
    -  `enterprise_id`
    -  `client_secret` 
    -  `public_key_id` 
    -  `private_key` 
    -  `passphrase` 

### Configurazione dell'accesso di livello Enterprise
{: #entlevelbox}

1.  Vai a `https://app.box.com/developers/console` (utilizza l'URL Box della tua azienda) e fai clic su **Create New App**.
1.  Dalla schermata **Create a New App**, seleziona **Enterprise Integration** e fai clic su **Next**.
1.  Nella schermata **Authentication Method**, seleziona **OAuth 2.0 with JWT (Server Authentication)** e fai clic su **Next**.
1.  Denomina la tua applicazione e fai clic sul pulsante **Create App**. Dopo che la tua applicazione Box è stata creata, fai clic su **View Your App**.
1.  Durante la visualizzazione della tua applicazione, seleziona **Application access** come **Enterprise**. Puoi utilizzare i tuoi utenti gestiti esistenti man mano che continui; non devi necessariamente crearne di nuovi.
1.  Scorri in basso fino alla sezione **Application Scopes** della pagina e abilita le seguenti caselle di spunta: 
    - `Read and write all folders stored in Box`
    - `Manage Users`
    - `Manage Enterprise Properties`
1.  Scorri verso il basso fino alla sezione **Advanced Features** e abilita i seguenti interruttori:
    - `Perform Actions as Users`
    - `Generate User Access Tokens` 
1.  Fai clic sul pulsante **Save Changes**.

`Refresh` è supportato solo con l'accesso di livello Enterprise.
{: note}

Se modifichi le tue impostazioni dell'applicazione Box, autorizza nuovamente (`Reauthorize`) la tua applicazione in modo che le modifiche diventino effettive.
{: tip}

I prossimi passi richiederanno l'assistenza dell'amministratore dell'account Box della tua organizzazione. Se non sei l'amministratore Box della tua organizzazione, puoi identificarlo aprendo una console dello sviluppatore di Box e controllando sotto **Account settings** > **Account details** > **Settings**.

1.  [Passo dell'amministratore] Autorizza il tuo id client dell'applicazione andando a **Admin console** > **Enterprise settings** > **Apps** e scorrendo a `Custom applications`. URL di esempio: `https://app.box.com/master/settings/openbox`.
1.  [Passo dell'amministratore] Immetti l'**ID client**) da `https://app.box.com/developers/console` nel campo **API key** e fai quindi clic sul pulsante **Authorize**.
1.  Ritorna alla console per gli sviluppatori Box `https://app.box.com/developers/console` e scorri alla sezione **Add and Manage Public Keys**. Fai clic su **Generate the public/private keypair** e scarica il tuo file di coppia di chiavi. Apri il file.
1.  Dal file di coppia di chiavi, taglia e incolla i seguenti campi nella strumentazione {{site.data.keyword.discoveryshort}}.
    -  `client_id`
    -  `enterprise_id`
    -  `client_secret` 
    -  `public_key_id` 
    -  `private_key` 
    -  `passphrase` 

Altri elementi da considerare durante la ricerca per l'indicizzazione con Box:

-  Le note Box sono archiviate nel formato JSON, per cui tutte le note Box nelle cartelle specificate saranno inserite da {{site.data.keyword.discoveryshort}}.
-  Quando utilizzi l'API, dovrai disporre di un elenco di ID cartelle e dell'ID proprietario associato ad ogni cartella di cui desideri eseguire la ricerca per l'indicizzazione. La strumentazione {{site.data.keyword.discoveryshort}} ti consente di sfogliare e selezionare il contenuto di cui eseguire la ricerca per l'indicizzazione.

## Salesforce
{: #connectsf}

Quando ti colleghi a un'origine Salesforce, assicurati che l'istanza a cui prevedi di collegarti sia un piano Enterprise o superiore.

Le seguenti credenziali sono necessarie per il collegamento a un'origine Salesforce e devono essere ottenute dall'amministratore di Salesforce:
-  `url` - L'`url` dell'origine a cui si collegano queste credenziali.
-  `username` - L'`username` dell'origine a cui si collegano queste credenziali.
-  `password` - La `password` è costituita dalla password Salesforce e da un token di sicurezza Salesforce valido concatenato. Questo valore non viene mai restituito e viene utilizzato solo quando crei o modifichi le credenziali.

Quando identifichi le credenziali, potrebbe essere utile consultare la [documentazione dello sviluppatore Salesforce ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.salesforce.com/docs/){: new_window}.

Altri elementi da considerare durante l'esecuzione della ricerca per l'indicizzazione con Salesforce:

-  Gli articoli Knowledge vengono sottoposti alla ricerca per l'indicizzazione solo se **version** è `published` e la lingua è `en-us`.
-  Quando utilizzi l'API, dovrai disporre di un elenco di oggetti Salesforce di cui desideri eseguire la ricerca per l'indicizzazione. La strumentazione {{site.data.keyword.discoveryshort}} ti consente di sfogliare e selezionare il contenuto di cui eseguire la ricerca per l'indicizzazione.

## SharePoint Online
{: #connectsp}

Quando ti colleghi a un'origine Microsoft SharePoint Online assicurati che l'istanza a cui prevedi di collegarti sia un piano Enterprise (E1) o superiore.

Le seguenti credenziali sono necessarie per il collegamento a un'origine SharePoint Online e devono essere ottenute dall'amministratore di SharePoint:

-  `organization_url` - L'`organization_url` dell'origine a cui si collegano queste credenziali.
-  `site_collection_path` - Il `site_collection_path` dell'origine a cui si connettono queste credenziali.
-  `username` - Il `client_id` dell'origine a cui si collegano queste credenziali. Questo utente deve avere accesso a tutti i siti e a tutti gli elenchi di cui deve essere eseguita la ricerca per l'indicizzazione e l'indicizzazione.
-  `password` - La `password` dell'origine a cui si collegano queste credenziali. Questo valore non viene mai restituito e viene utilizzato solo quando crei o modifichi le credenziali.

Quando identifichi le credenziali, potrebbe essere utile consultare la [documentazione dello sviluppatore Microsoft SharePoint ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.microsoft.com/en-us/sharepoint/dev/){: new_window}.

Altri elementi da considerare durante la ricerca per l'indicizzazione con Microsoft SharePoint Online:

-  Per eseguire la ricerca per l'indicizzazione di SharePoint, l'account `Crawl User` deve disporre delle autorizzazioni `SiteCollection Administrator`.
-  Quando esegui la ricerca per l'indicizzazione di SharePoint, ti servirà l'elenco di percorsi di raccolta del sito SharePoint di cui desideri eseguire la ricerca per l'indicizzazione.{{site.data.keyword.discoveryshort}} non supporta i percorsi cartella come input.

## Web Crawl
{: #connectwebcrawl}

Questa funzione beta può essere utilizzata per eseguire ricerche per l'indicizzazione di siti web pubblici che non richiedono una password. Puoi selezionare la frequenza con la quale desideri che {{site.data.keyword.discoveryshort}} esegua la sincronizzazione con i siti web, la lingua e il numero di hop.

-  `Sync my data` - Puoi scegliere di eseguire la sincronizzazione ogni 5 minuti, orni ora, ogni giorno, ogni settimana od ogni mese. 
-  `Select language` - Scegli la lingua dei siti web dall'elenco di lingue supportate. Vedi [Supporto linguistico](/docs/services/discovery?topic=discovery-language-support#supported-languages) per l'elenco delle lingue supportate da {{site.data.keyword.discoveryshort}}. Ti consigliamo di creare una raccolta separata per ogni lingua.
-  `URL group to sync` - Immetti il tuo URL e fai clic sul segno più per aggiungerlo al gruppo di URL. Per specificare le impostazioni della ricerca per l'indicizzazione (**Crawl settings**) per questo gruppo di URL, fai clic sull'icona ![Cog](images/icon_settings.png). Puoi impostare il numero massimo di hop (**Maximum hops**), che è il numero di link consecutivi da seguire dall'URL iniziale (l'URL iniziale è `0`). Il numero predefinito di hop è `2` e quello massimo è `20` (se utilizzi l'API, il massimo è `1000`). 

Per la release beta, il numero di pagine web di cui viene eseguita la ricerca per l'indicizzazione sarà limitato; pertanto, è possibile che il web crawler non esegua la ricerca per l'indicizzazione di tutti i siti web specificati e raggiunga il numero massimo di hop.
{: note}

Se hai bisogno di impostazioni della ricerca per l'indicizzazione (**Crawl settings**) per altri URL, fai clic su **Add URL group** e crea un nuovo gruppo. Puoi creare tutti i gruppi di URL di cui hai bisogno.
{: tip}

## SharePoint 2016 in loco
{: #connectsp_op}

Microsoft SharePoint 2016 (nota anche come SharePoint Server 2016) è un'origine dati in loco. Per connetterti a essa, devi prima installare e configurare IBM Secure Gateway. Per ulteriori informazioni, vedi [Installazione di IBM Secure Gateway per i dati in loco](/docs/services/discovery?topic=discovery-sources#gateway).
{: note}

Le seguenti credenziali sono necessarie per la connessione a un'origine dati SharePoint 2016 e devono essere ottenute dall'amministratore di SharePoint:

-  `username` - Il `client_id` dell'origine a cui si collegano queste credenziali. Questo utente deve avere accesso a tutti i siti e a tutti gli elenchi di cui deve essere eseguita la ricerca per l'indicizzazione e l'indicizzazione.
-  `password` - La `password` dell'origine a cui si collegano queste credenziali. Questo valore non viene mai restituito e viene utilizzato solo quando crei o modifichi le credenziali.
-  `web_application_url` - L'URL dell'applicazione web (`web_application_url`) di SharePoint 2016; ad esempio, https://sharepointwebapp.com:8443. Se non viene fornita, la porta impostata automaticamente è la `80` per http e la `443` per https.
-  `domain` - Il dominio (`domain`) dell'account SharePoint 2016.

Quando identifichi le credenziali, potrebbe essere utile consultare la [documentazione dello sviluppatore Microsoft SharePoint ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.microsoft.com/en-us/sharepoint/dev/){: new_window}.

Altri elementi da notare quando esegui la ricerca per l'indicizzazione di Microsoft SharePoint 2016:

-  Per eseguire la ricerca per l'indicizzazione di SharePoint 2016, l'account `Crawl User` deve disporre delle autorizzazioni `SiteCollection Administrator`.
-  Quando esegui la ricerca per l'indicizzazione di SharePoint, ti servirà l'elenco di percorsi di raccolta del sito SharePoint di cui desideri eseguire la ricerca per l'indicizzazione.{{site.data.keyword.discoveryshort}} non supporta i percorsi cartella come input.

## IBM Cloud Object Storage
{: #connectcos}

Quando stabilisci una connessione a un'origine IBM Cloud Object Storage, sono necessarie le seguenti credenziali. Devono essere ottenute dal tuo amministratore di IBM Cloud Object Storage:

-  `endpoint` - L'`endpoint` utilizzato per interagire con i dati IBM Cloud Object Storage.
-  `access_key_id` - L'ID di chiave di accesso (`access_key_id`) ottenuto quando è stata creata l'istanza di IBM Cloud Object Storage.
-  `secret_access_key` - La chiave di accesso segreta (`secret_access_key`) per firmare le richieste ottenute quando è stata creata l'istanza di IBM Cloud Object Storage.

Dopo l'immissione di queste informazioni, puoi scegliere la frequenza con la quale desideri eseguire la sincronizzazione dei tuoi dati e selezionare i bucket con i quali desideri eseguire la sincronizzazione.

Altri elementi da notare quando esegui la ricerca per l'indicizzazione di IBM Cloud Object Storage:

-  Questo connettore non supporta la ricerca per l'indicizzazione degli endpoint privati.
-  Si verifica un piccolo problema di prestazioni se vengono selezionati tutti i bucket. In questo caso, ci potrebbe essere un ritardo prima che l'indicizzazione dei documenti venga completata.

## Utilizzo della strumentazione
{: #source_tooling}

La connessione a un'origine dati utilizzando la strumentazione {{site.data.keyword.discoveryshort}} viene eseguita creando una raccolta specifica per un'origine. Effettua le seguenti operazioni per creare una raccolta di origine ed eseguirne la ricerca per l'indicizzazione:

1.  Dalla pagina **Manage data** della strumentazione {{site.data.keyword.discoveryshort}}, seleziona **Connect a data source**.
2.  Seleziona l'origine dati a cui vuoi collegarti. Se hai selezionato un'origine dati in loco, dovrai prima installare IBM Secure Gateway; per ulteriori informazioni, vedi [Installazione di IBM Secure Gateway per i dati in loco](/docs/services/discovery?topic=discovery-sources#gateway). 
3.  Immetti le tue credenziali di origine e fai clic per collegarti. Le tue credenziali di origine devono essere ottenute dal tuo amministratore del sistema di origine.
4.  Scegli quali sono i dati di cui desideri eseguire la ricerca per l'indicizzazione e la frequenza con cui vuoi sincronizzarli. Opzioni di sincronizzazione:
    -  Every five minutes; l'esecuzione avviene ogni cinque minuti
    -  Hourly: l'esecuzione avviene ogni ora
    -  Daily: l'esecuzione avviene ogni giorno tra le 00:00 e le 06:00 nel fuso orario specificato
    -  Weekly: l'esecuzione avviene ogni settimana di domenica tra le 00:00 e le 06:00 nel fuso orario specificato
    -  Monthly: l'esecuzione avviene ogni mese la prima domenica del mese tra le 00:00 e led 06:00 nel fuso orario specificato.
    
    Stato della ricerca per l'indicizzazione di esempio:
    
    ```json
    "crawl_status" : {
    "source_crawl" : {
      "status" : "completed",
      "next_crawl" : "2019-02-10T05:00:00-05:00"
    }
    ```
5.  Fai clic su **Save & Sync objects** per avviare la ricerca per l'indicizzazione della tua origine dati. Vieni poi reindirizzato alla schermata dello stato della raccolta che si aggiorna quando vengono aggiunti documenti alla raccolta.

La ricerca per l'indicizzazione sincronizzerà i dati inizialmente e poi in base alla frequenza che hai specificato.
**Nota:** se modifichi qualcosa nella schermata **Sync settings** e poi fai clic su **Save and Sync objects** verrà avviata una ricerca per l'indicizzazione (o riavviata se ne è già in esecuzione una) in quel momento.

## Utilizzo dell'API
{: #source_api}

Utilizza il seguente processo per creare una raccolta collegata a un'origine dati utilizzando l'API.

Se intendi stabilire una connessione a un'origine dati in loco, dovrai prima installare IBM Secure Gateway; per ulteriori informazioni, vedi [Installazione di IBM Secure Gateway per i dati in loco](/docs/services/discovery?topic=discovery-sources#gateway). 

Il seguente esempio utilizza l'origine dati SharePoint.

1.  Crea le credenziali per l'origine a cui ti stai collegando utilizzando l'[API delle credenziali dell'origine ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery#create-credentials){: new_window}. Registra il **credential_id** restituito delle credenziali appena create.
2.  Crea una nuova configurazione utilizzando [Configuration API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery#add-configuration){: new_window}. Questa configurazione deve contenere un oggetto **source** che definisce cosa deve essere sottoposto a una ricerca per l'indicizzazione. L'oggetto **source** deve contenere il **credential_id** che hai registrato precedentemente.
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
3.  Crea una nuova raccolta utilizzando [Collections API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery#create-a-collection){: new_window}. L'oggetto che definisce la raccolta deve contenere il **configuration_id** che hai registrato precedentemente.

La ricerca per l'indicizzazione dell'origine inizia non appena la raccolta viene creata e poi nuovamente in base alla frequenza che hai specificato.
**Nota:** se modifichi qualcosa nell'oggetto **source** della configurazione, sarà avviata una nuova ricerca per l'indicizzazione (o riavviata se ne è già in esecuzione una) in quel momento.

### Specifica di un `customer_id`
{: #source_customer_id}

Un campo `customer_id` in un documento inserito {{site.data.keyword.discoveryshort}} può essere utilizzato per eliminare il contenuto basato sul `customer_id` utilizzando il metodo **user-data** nell'API. I documenti in entrata da un'origine dati non sono automaticamente assegnati a un `customer_id` quando viene inserito. Se la tua applicazione richiede che venga definito un `customer_id`, puoi specificare che uno (o più) dei campi in entrata dal sistema di origine siano copiati e utilizzati come `customer_id`. A tale scopo devi modificare la configurazione che viene utilizzata per il collegamento all'origine.

1.  Esegui una query di esempio e identifica il campo che vuoi utilizzare come `customer_id`.
2.  Modifica la configurazione. Dovrai aggiungere una sezione **Normalization** per creare il campo `customer_id`.
    -  Nella strumentazione, passa alla tua raccolta e fai clic sul link **edit** nella sezione di configurazione. Successivamente, fai clic sulla scheda **Normalization** e aggiungi una normalizzazione **copy** per creare il campo `customer_id`. Fai quindi clic su **Apply & save**.
    ![Copia normalizzazione](images/norm_copy.png)
    -  Quando utilizzi l'API, aggiungi il seguente oggetto all'array **normalizations**:
       ```json
  {
         "operation" : "copy",
         "source_field" : "{original_field_name}",
         "destination_field" : "customer_id"
       }
       ```
       {: codeblock}
3.  La successiva ricerca per l'indicizzazione pianificata aggiungerà il campo `customer_id` a tutti i documenti. Se vuoi che una ricerca per l'indicizzazione venga avviata immediatamente, modifica la configurazione di origine (**Sync settings** nella strumentazione).

Per ulteriori informazioni e per saperne di più sull'eliminazione basata su `customer_id`, vedi [Sicurezza delle informazioni](/docs/services/discovery?topic=discovery-information-security#information-security).

## Installazione di IBM Secure Gateway per i dati in loco 
{: #gateway}

Per stabilire una connessione a un'origine dati in loco, dovrai prima scaricare, installare e configurare IBM Secure Gateway. Dopo che avrai installato IBM Secure Gateway per la tua prima origine dati in loco, non dovrai ripetere questo processo.

1.  Dalla pagina **Manage data** della strumentazione {{site.data.keyword.discoveryshort}}, seleziona **Connect a data source**.
1.  Seleziona l'origine dati a cui vuoi collegarti. Quando selezioni un'origine dati in loco, vai alla sezione **Connect to your on-premise network** e fai clic sul pulsante **Make connection**.
1.  Nella schermata **Download and install the Secure Gateway Client**, scarica la versione appropriata di IBM Secure Gateway.
1.  Dopo che hai completato il download, fai clic sul pulsante **Download Secure Gateway and Continue**. Durante l'installazione, ti serviranno l'ID gateway (**Gateway ID**) e il **Token** forniti a schermo quando richiesto dal client Secure Gateway. Vedi il documento relativo all'[installazione del client ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/docs/services/SecureGateway/securegateway_install.html#installing-the-client){: new_window} nella documentazione di Secure Gateway per le istruzioni di installazione.
1.  Sulla macchina che esegue il client Secure Gateway, apri il dashboard Secure Gateway all'indirizzo http://localhost:9003.
1.  Fai clic su **add ACL** nel dashboard. Aggiungi l'URL dell'endpoint di ogni raccolta SharePoint all'elenco **Allow access**. Ad esempio, nome host: `mycompany.sharepoint.com` e porta: `80`.
1.  Ritorna alla strumentazione {{site.data.keyword.discoveryshort}} e fai clic su **Continue**. Se la connessione viene stabilita correttamente, vedrai il messaggio `Connection successful`. Se la connessione non è riuscita, apri il dashboard Secure Gateway e verifica che gli endpoint nell'elenco **Allow access** siano corretti.

Una volta stabilita correttamente la connessione, puoi cominciare immettendo le credenziali per la tua origine dati in loco.

## Connessione alle origini dati e isolamento dei dati
{: #source_isolation}

La [connessione a origini dati esterne](/docs/services/discovery?topic=discovery-sources#sources) riduce l'isolamento dei dati della tua istanza del servizio perché i dati in transito tra l'origine e il servizio non possono essere isolati. Tutti gli altri tipi di dati (inattivo, amministrazione, query) restano completamente isolati. Tutte le transito in elaborazione tra i servizi e le origini dati e al loro interno sono crittografate utilizzando TLS v1.2. Le chiavi private per i certificati TLS sono crittografate quando sono inattive utilizzando AES-256-GCM, i certificati del servizio scadono ogni tre anni e gli elenchi di revoca dei certificati vengono aggiornati mensilmente. Tutte le credenziali vengono inviate su una connessione crittografata utilizzando TLS v1.2 e crittografate quando sono inattive utilizzando AES-256. Le connessioni a queste origini dati utilizzano qualsiasi protocollo protetto sia supportato da tali origini dati.
