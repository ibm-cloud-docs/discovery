---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-25"

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

# Configurazione delle opzioni seed e connettore
{: #configuring-connector-and-seed-options}

Quando indicizzi i dati, il crawler identifica prima il tipo di repository di dati (connettore) e l'ubicazione di partenza specificata dall'utente (seed) per iniziare a scaricare le informazioni.
{: shortdesc}

**Importante:** quando utilizzi il data crawler, le impostazioni di sicurezza del repository di dati vengono ignorate.

I seed sono i punti di partenza di un'indicizzazione e vengono utilizzati dal data crawler per richiamare i dati dalla risorsa identificata dal connettore. Normalmente, i seed configurano gli URL per accedere alle risorse basate sul protocollo, come le condivisioni di file, le condivisioni SMB, i database e altri repository di dati accessibili tramite vari protocolli. Inoltre, diversi URL seed hanno funzionalità diverse. I seed possono anche essere specifici per il repository, per abilitare l'indicizzazione di applicazioni di terze parti specifiche come i sistemi di gestione delle relazioni con la clientela (CRM), i sistemi del ciclo di vita del prodotto (PLC), i sistemi di gestione dei contenuti (CMS), le applicazioni basate sul cloud e le applicazioni del database web.

Per indicizzare i dati correttamente, devi assicurarti che il crawler sia configurato correttamente in modo da leggere il tuo repository di dati. Il Data Crawler fornisce i connettori per supportare la raccolta di dati dai seguenti repository:

-   [File system](/docs/services/discovery/data-crawler-seeds.html#configuring-filesystem-crawl-options)
-   [Database, tramite JDBC](/docs/services/discovery/data-crawler-seeds.html#configuring-database-crawl-options)
-   [CMIS (Content Management Interoperability Services)](/docs/services/discovery/data-crawler-seeds.html#configuring-cmis-crawl-options)
-   [Condivisioni SMB (Server Message Block), CIFS (Common Internet Filesystem) o Samba](/docs/services/discovery/data-crawler-seeds.html#configuring-smbcifssamba-crawl-options)
-   [SharePoint e SharePoint Online](/docs/services/discovery/data-crawler-seeds.html#configuring-sharepoint-crawl-options)
-   [Box](/docs/services/discovery/data-crawler-seeds.html#configuring-box-crawl-options)

Viene anche fornito un modello di configurazione del connettore, che ti consente di personalizzare un connettore.

Per configurare il tuo connettore, effettua le seguenti operazioni:

1.  Apri il file nella directory `connectors` che corrisponde al repository a cui ti stai collegando (ad esempio `filesystem.conf` è il file di configurazione per il connettore del file system) in un editor di testo.

1.  Modifica i valori appropriati per il tuo repository:

    -   [File system](/docs/services/discovery/data-crawler-seeds.html#filesystem-crawl-options)
    -   [Database, tramite JDBC](/docs/services/discovery/data-crawler-seeds.html#database-crawl-seed)
    -   [CMIS (Content Management Interoperability Services)](/docs/services/discovery/data-crawler-seeds.html#cmis-crawl-options)
    -   [Condivisioni SMB (Server Message Block), CIFS (Common Internet Filesystem) o Samba](/docs/services/discovery/data-crawler-seeds.html#smb-cifs-samba-crawl-options)
    -   [SharePoint e SharePoint Online](/docs/services/discovery/data-crawler-seeds.html#sharepoint-crawl-options)
    -   [Box](/docs/services/discovery/data-crawler-seeds.html#box-crawl-options)
1.  Salva e chiudi il file.
1.  Ripeti questi passi per il file `-seed.conf` nella directory `connectors/seeds` che corrisponde al repository a cui ti stai collegando (ad esempio `filesystem-seed.conf` è il file di configurazione (a cui collegarsi) seed per il connettore del file system) in un editor di testo.
1.  Procedi con la [configurazione del data crawler per il collegamento a {{site.data.keyword.discoveryshort}}](/docs/services/discovery/data-crawler-discovery.html).

Per accedere al manuale incluso nel prodotto per i file di configurazione del seed e del connettore, con le informazioni più aggiornate, immetti i seguenti comandi dalla directory di installazione del crawler:
-   Per le opzioni di configurazione del connettore:
    ```bash
    man crawler-options.conf
    ```
    {: pre}
-   Per le opzioni di configurazione del seed:
    ```bash
    man crawler-seed.conf
    ```
    {: pre}


## Configurazione delle opzioni di indicizzazione del file system
{: #filesystem-crawl-options}

Il connettore del file system ti consente di eseguire l'indicizzazione dei file locali all'installazione del data crawler.

### Configurazione del connettore del file system

Le seguenti sono le opzioni di configurazione di base obbligatorie per l'utilizzo del connettore del file system. Per impostare questi valori, apri il file `config/connectors/filesystem.conf` e modifica i seguenti valori specifici per i tuoi casi di utilizzo:

-   **`protocol`** - Il nome del protocollo del connettore utilizzato per l'indicizzazione. Utilizza `sdk-fs` per questo connettore.
-   **`collection`** - Questo attributo viene utilizzato per decomprimere i file temporanei. Il valore predefinito è `crawler-fs`
-   **`logging-config`** - Specifica il file utilizzato per la configurazione delle opzioni di registrazione; deve essere formattato come una stringa XML `log4j`.
-   **`classname`** - Nome della classe Java per il connettore. Il valore da utilizzare con questo connettore deve essere `plugin:filesystem.plugin@filesystem`.

### Configurazione del seed di indicizzazione del file system

Possono essere configurati i seguenti valori per il file seed di indicizzazione del file system. Per impostare questi valori, apri il file `config/seeds/filesystem-seed.conf` e specifica i seguenti valori specifici per i tuoi casi di utilizzo:

-   **`url`** - Elenco di file e cartelle separati da nuove righe da indicizzare. Gli utenti UNIX possono utilizzare un percorso come ad esempio `/usr/local/`.

    **Nota:** Gli URL devono iniziare con `sdk-fs://`. Quindi per indicizzare, ad esempio, `/home/watson/mydocs`, il valore di questo URL dovrebbe essere `sdk-fs:///home/watson/mydocs` - la terza `/` è necessaria!

    I file system utilizzati da sistemi di computer Linux, UNIX e simili a UNIX possono contenere tipi speciali di file, come ad esempio i nodi e i file di dispositivi a caratteri o blocchi che rappresentano pipe denominati, che non possono essere indicizzati perché non contengono dati, ma funzionano come un dispositivo o punti di accesso I/O. Il tentativo di indicizzare tali file genererà degli errori durante l'indicizzazione. Per evitare tali errori, devi escludere la directory `/dev` in tutte le indicizzazioni di livello superiore su un file system Linux, UNIX o simile a UNIX. Se presenti sul sistema di cui stai eseguendo l'indicizzazione, devi escludere anche le directory di sistema temporanee come `/proc`, `/sys` e `/tmp`, che contengono file temporanei e informazioni di sistema. **`hops`** - Solo uso interno. **`default-allow`** - Solo uso interno.
    {: tip}

## Configurazione delle opzioni di indicizzazione del database

Il connettore del database ti consente di indicizzare un database eseguendo un comando SQL personalizzato e creando un documento per riga (record) e un elemento di contenuto per colonna (campo). Puoi specificare una colonna da utilizzare come chiave univoca, nonché una colonna contenente una data/ora che rappresenta l'ultima data di modifica di ogni record. Il connettore richiama tutti i record dal database specificato e può anche essere limitato a tabelle specifiche, unioni e così via nell'istruzione SQL.

Il connettore del database ti consente di eseguire l'indicizzazione dei seguenti database:

-   {{site.data.keyword.IBM}} DB2
-   MySQL
-   Oracle PostgreSQL
-   Microsoft SQL Server
-   Sybase
-   Altri database conformi con SQL, tramite un driver conforme con JDBC 3.0

Il connettore richiama tutti i record dal database e dalla tabella specificati 

***Driver JDBC*** - Il connettore del database viene fornito con driver Oracle JDBC (Java Database Connectivity) versione 1.5. Tutti i driver JDBC di terze parti forniti con il data crawler si trovano nella directory `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` della tua installazione del data crawler, dove puoi aggiungerli, rimuoverli e modificarli come necessario. Puoi anche utilizzare l'impostazione `extra_jars_dir` nel file `crawler.conf` per specificare un'altra ubicazione.

***Driver JDBC DB2*** - Il data crawler non viene fornito con i driver JDBC per DB2 a causa di problemi di licenza. Tuttavia, tutte le installazioni DB2 in cui hai installato il supporto JDBC includono i file JAR necessari al data crawler, per poter indicizzare un'installazione DB2. Per indicizzare un'istanza DB2, devi copiare questi file nella directory appropriata nella tua installazione del data crawler in modo che il connettore del database possa utilizzarli. Per abilitare il data crawler a indicizzare un'installazione DB2, trova il file `db2jcc.jar` e i file JAR di licenza (normalmente, `db2jcc_license_cu.jar`) nella tua installazione DB2 e copiali nella directory secondaria `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` della tua directory di installazione del data crawler, oppure utilizza l'impostazione `extra_jars_dir` nel file `crawler.conf` per specificare un'altra ubicazione.

***Driver JDBC MySQL*** - Il data crawler non viene fornito con i driver JDBC per MySQL a causa di possibili problemi di licenza se vengono forniti come parte del prodotto. Tuttavia, lo scaricare il file JAR che contiene i driver JDBC MySQL e la sua integrazione nella tua installazione del data crawler sono processi facili da eseguire:

1.  Utilizza un browser web per visitare il sito di download di MySQL e individua il link di download di origine e binario per il formato di archivio che vuoi utilizzare (normalmente zip per i sistemi Microsoft Windows o un tarball compresso con GZIP per i sistemi Linux). Fai clic su quel link per avviare il processo di download. Potrebbe essere necessaria la registrazione.
1.  Utilizza il comando unzip archive-file-name o tar zxf archive-file-name appropriato per estrarre il contenuto di tale archivio, in base al tipo e al nome del file di archivio che hai scaricato.
1.  Passa alla directory estratta dal file di archivio e copia il file JAR da questa directory nella directory secondaria `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` della tua directory di installazione del data crawler, oppure utilizza l'impostazione `extra_jars_dir` nel file `crawler.conf` per specificare un'altra ubicazione.

### Configurazione del connettore del database

Le seguenti sono le opzioni di configurazione di base obbligatorie per l'utilizzo del connettore del database. Per impostare questi valori, apri il file config/connectors/database.conf e modifica i seguenti valori specifici per i tuoi casi di utilizzo:

-   **`protocol`** - Il nome del protocollo del connettore utilizzato per l'indicizzazione. Il valore per questo connettore si basa sul sistema di database a cui si deve accede.
-   **`collection`** - Questo attributo viene utilizzato per decomprimere i file temporanei. 
-   **`classname`** - Nome della classe Java per il connettore. Il valore da utilizzare con questo connettore deve essere `plugin:database.plugin@database`.
-   **`logging-config`** - Specifica il file utilizzato per la configurazione delle opzioni di registrazione; deve essere formattato come una stringa XML `log4j`.

### Configurazione del seed di indicizzazione del database
{: #database-crawl-seed}

Possono essere configurati i seguenti valori per il file seed di indicizzazione del database. Per impostare questi valori, apri il file `config/seeds/database-seed.conf` e specifica i seguenti valori specifici per i tuoi casi di utilizzo:

-   **`url`** - L'URL della tabella o della vista da richiamare. Definisce l'URL del seed del database SQL personalizzato. La struttura è:

    -   `database-system://host:port/database?[per=num]&[sql=SQL]`

    La verifica di un URL seed mostrerà tutti gli URL accodati. Ad esempio, la verifica del seguente URL per un database che contiene 200 record:
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?per=100&sql=select%20*%20from%20vessel&`

    mostra i seguenti URL accodati:
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=0&`
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=100&`
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=200&`

    Mentre la verifica del seguente URL mostrerà i dati richiamati dalla riga 43:
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?per-1&key-val=43`
-   **`hops`** - Solo uso interno. 
-   **`default-allow`** - Solo uso interno.
-   **`user-password`** - Credenziali per il sistema di database. Il nome utente e la password devono essere separati da `:` e la password deve essere codificata utilizzando il programma vcrypt fornito con il data crawler. Ad esempio: `username:[[vcrypt/3]]passwordstring`
-   **`max-data-size`** - Dimensione massima dei dati per un documento. Questo è il blocco più grande di memoria che verrà caricato in una sola volta. Aumenta questo limite solo se disponi di memoria sufficiente sul tuo computer.
-   **`filter-exact-duplicates`** - Solo uso interno.
-   **`timeout`** - Solo uso interno.
-   **`jdbc-class`** (opzione Extender) - Quando specificata, questa stringa sovrascriverà la classe JDBC utilizzata dal connettore quando si sceglie `(other)` come sistema di database.
-   **`connection-string`** (opzione Extender) - Quando specificata, questa stringa sovrascriverà la stringa di connessione JDBC generata automaticamente. Questo ti consente di fornire una configurazione più dettagliata sulla connessione al database, come ad esempio il bilanciamento del carico o le connessioni SSL. Ad esempio: `jdbc:netezza://127.0.0.1:5480/databasename`
-   **`save-frequency-for-resume`** (opzione Extender) - Specifica il nome di una colonna o di un'etichetta associata, in modo da poter riprendere un'indicizzazione o eseguire un aggiornamento parziale. Il seed salva il nome di questa colonna a intervalli regolari mentre procede con l'indicizzazione e lo salva di nuovo una volta che l'ultima riga del database è stata indicizzata. Quando si riprende l'indicizzazione o la si aggiorna, l'indicizzazione inizia con la riga identificata nel valore salvato per questo campo

## Configurazione delle opzioni di indicizzazione CMIS
{: #cmis-crawl-options}

Il connettore CMIS (Content Management Interoperability Services) ti consente di eseguire l'indicizzazione dei repository dei sistemi di gestione dei contenuti (CMS) abilitati CMIS, come ad esempio Alfresco, Documentum o {{site.data.keyword.IBM}} Content Manager e di indicizzare i dati che contengono.

### Configurazione del connettore CMIS

Le seguenti sono le opzioni di configurazione di base obbligatorie per l'utilizzo del connettore CMIS. Per impostare questi valori, apri il file `config/connectors/cmis.conf` e specifica i seguenti valori specifici per i tuoi casi di utilizzo:

-   **`protocol`** - Il nome del protocollo del connettore utilizzato per l'indicizzazione. Il valore da utilizzare con questo connettore deve essere `cmis`.
-   **`collection`** - Questo attributo viene utilizzato per decomprimere i file temporanei. 
-   **`dns`** - Opzione non utilizzata.
-   **`classname`** - Nome della classe Java per il connettore. Utilizza `plugin:cmis-v1.1.plugin@connector` per questo connettore.
-   **`logging-config`** - Specifica il file utilizzato per la configurazione delle opzioni di registrazione; deve essere formattato come una stringa XML `log4j`.
-   **`endpoint`** - L'URL dell'endpoint del servizio di un repository conforme con CMIS. Ad esempio, le strutture URL per SharePoint sono:

    -   Per il bind AtomPub: `http://yourserver/_vti_bin/cmis/rest?getRepositories`
    -   Per il bind WebServices: `http://yourserver/_vti_bin/cmissoapwsdl.aspx`
-   **`username`** - Il nome utente dell'utente del repository CMIS utilizzato per accedere al contenuto. Questo utente deve avere accesso a tutti i documenti e a tutte le cartelle di destinazione da ricercare e indicizzare.
-   **`password`** - La password del repository CMIS utilizzata per accedere al contenuto. La password NON deve essere codificata; deve essere fornita in testo semplice.
-   **`repositoryid`** - L'ID del repository CMIS utilizzato per accedere al contenuto per quel repository specifico.
-   **`bindingtype`** - Identifica quale tipo di bind utilizzare per il collegamento a un repository CMIS. Il valore è AtomPub o WebServices.
-   **`authentication`** - Identifica quale tipo di meccanismo di autenticazione utilizzare mentre si contatta un repository compatibile CMIS: autenticazione HTTP di base, NTLM o WS-Security (token nome utente).
-   **`enable-acl`** - Abilita il richiamo degli ACL per i dati indicizzati. Se non sei interessato alla sicurezza dei documenti in questa raccolta, disabilitando questa opzione incrementerai le prestazioni non richiedendo queste informazioni con il documento e non richiamandole e codificandole. Il valore è true o false.
-   **`user-agent`** - Un'intestazione inviata al server durante l'indicizzazione dei documenti.
-   **`method`** - Il metodo (GET o POST) con cui verranno trasmessi i parametri.
-   **`url-logging`** - L'estensione con cui vengono registrati gli URL indicizzati. I valori possibili sono: 

    -   `full-logging` - Registra tutte le informazioni sull'URL.
    -   `refined-logging` - Registra solo le informazioni necessarie per selezionare il log del crawler e necessarie al connettore per funzionare correttamente; questo è il valore predefinito.
    -   `minimal-logging` - Registra solo la quantità minima di informazioni necessarie al connettore per funzionare correttamente.

    Impostando questa opzione su `minimal-logging` si ridurrà la dimensione dei log e acquisirà un leggero aumento delle prestazioni per via di I/O più piccoli associati alla riduzione della quantità di dati che sta venendo registrata.
-   **`ssl-version`** - Specifica una versione di SSL da utilizzare per le connessioni HTTPS. Per impostazione predefinita viene utilizzato il protocollo più attendibile disponibile.

### Configurazione del seed di indicizzazione CMIS

Possono essere configurati i seguenti valori per il file seed di indicizzazione CMIS. Per impostare questi valori, apri il file `config/seeds/cmis-seed.conf` e modifica i seguenti valori specifici per i tuoi casi di utilizzo:

-   **`url`** - L'URL di una cartella dal repository CMIS da utilizzare come punto di partenza dell'indicizzazione, ad esempio: `cmis://alfresco.test.com:8080/alfresco/cmisatom?folderToProcess-workspace://SpacesStore/guid`

    Per indicizzare da una cartella root, devi fornire l'URL come: `cmis://alfresco.test.com:8080/alfresco/cmisatom?folderToProcess-`
-   **`at`** - Opzione non utilizzata.
-   **`default-allow`** - Solo uso interno.

## Configurazione delle opzioni di indicizzazione SMB/CIFS/Samba
{: #smb-cifs-samba-crawl-options}

Il connettore Samba ti consente di indicizzare le condivisioni file SMB (Server Message Block) e CIFS (Common Internet Filesystem). Questo tipo di condivisione file è comune sulle reti Windows ed è fornito anche tramite il progetto open source Samba.

### Configurazione del connettore Samba

Le seguenti sono le opzioni di configurazione di base obbligatorie per l'utilizzo del connettore Samba. Per impostare questi valori, apri il file `config/connectors/samba.conf` e specifica i seguenti valori specifici per i tuoi casi di utilizzo:

-   **`protocol`** - Il nome del protocollo del connettore utilizzato per l'indicizzazione. Il valore per utilizzare questo connettore è smb.
-   **`collection`** - Questo attributo viene utilizzato per decomprimere i file temporanei. 
-   **`classname`** - Nome della classe Java per il connettore. Il valore da utilizzare con questo connettore deve essere `plugin:smb.plugin@connector`.
-   **`logging-config`** - Specifica il file utilizzato per la configurazione delle opzioni di registrazione; deve essere formattato come una stringa XML `log4j`.
-   **`username`** - Il nome Samba per l'autenticazione. Se fornito, devono essere forniti anche un dominio e una password. Se non viene fornito, viene utilizzato l'account guest.
-   **`password`** - La password Samba per l'autenticazione. Se viene fornito il nome utente, è obbligatoria. La password deve essere codificata utilizzando il programma vcrypt fornito con il data crawler.
-   **`archive`** - Abilita il connettore Samba a ricercare e indicizzare i file compressi nei file di archivio. Il valore è true o false; il valore predefinito è false.
-   **`max-policies-per-handle`** - Specifica il numero massimo di politiche LSA (Local Security Authority) che possono essere aperte per un solo handle RPC. Queste politiche definiscono le autorizzazioni di accesso obbligatorie per eseguire la query o per modificare un determinato sistema in varie condizioni. Il valore predefinito per questa opzione è 255.
-   **`crawl-fs-metadata`** - L'attivazione di questa opzione provocherà l'aggiunta da parte del data crawler, di un documento VXML che contiene i metadati del file system disponibili sul file (data di creazione, ultima data di modifica, attributi file, ecc.).
-   **`enable-arc-connector`** - Opzione non utilizzata.
-   **`disable-indexes`** - Elenco di indici separati da nuove righe da disabilitare, che può comportare un'indicizzazione più veloce, ad esempio:

    -   `disable-url-index`
    -   `disable-error-state-index`
    -   `disable-crawl-time-index`
-   **`exact-duplicates-hash-size`** - Imposta la dimensione della tabella hash utilizzata per la risoluzione dei duplicati esatti. Fai molta attenzione quando modifichi questo numero. Il valore che selezioni deve essere un numero primo e dimensioni maggiori possono fornire ricerche più rapide ma richiederanno più memoria, mentre dimensioni più piccole possono rallentare le indicizzazioni ma ridurranno notevolmente l'utilizzo della memoria.
-   **`user-agent`** - Opzione non utilizzata.
-   **`timeout`** - Opzione non utilizzata
-   **`n-concurrent-requests`** - Il numero di richieste che verranno inviate in parallelo a un singolo indirizzo IP. Il valore predefinito è `1`.
-   **`enqueue-persistence`** - Opzione non utilizzata.

### Configurazione del seed di indicizzazione Samba

Possono essere configurati i seguenti valori per il file seed di indicizzazione Samba. Per impostare questi valori, apri il file `config/seeds/samba-seed.conf` e specifica i seguenti valori specifici per i tuoi casi di utilizzo:

-   **`url`** - Un elenco di condivisioni separate da nuove righe da indicizzare, ad esempio:

    ```
    smb://share.test.com/office
    smb://share.test.com/cash/money/change
    smb://share.test.com/C$/Program Files
    ```
    {: codeblock}

-   **`hops`** - Solo uso interno. 
-   **`default-allow`** - Solo uso interno.

## Configurazione delle opzioni di indicizzazione SharePoint
{: #sharepoint-crawl-options}

**Importante:** il connettore SharePoint richiede Microsoft SharePoint Server 2007 (MOSS 2007), SharePoint Server 2010, SharePoint Server 2013 o SharePoint Online.

Il connettore SharePoint ti consente di indicizzare gli oggetti SharePoint e le informazioni che contengono. Un oggetto come un documento, un profilo utente, una raccolta di siti, un blog, un elemento dell'elenco, un elenco di appartenenza, una pagina della directory e altro, possono essere indicizzati con i relativi metadati associati. Per gli elementi e i documenti dell'elenco, gli indici possono includere gli allegati.

Il connettore SharePoint rispetta l'attributo `noindex` su tutti gli oggetti SharePoint, indipendentemente dal loro tipo specifico (blog, documenti, profili utente e altro). Viene restituito un solo documento per ogni risultato.
{: tip}

**Importante:** l'account SharePoint che utilizzi per indicizzare i tuoi siti SharePoint deve avere almeno i privilegi di accesso in lettura completo.

### Configurazione del connettore SharePoint

Le seguenti sono le opzioni di configurazione di base obbligatorie per l'utilizzo del connettore SharePoint. Per impostare questi valori, apri il file `config/connectors/sharepoint.conf` e modifica i seguenti valori specifici per i tuoi casi di utilizzo:

-   **`protocol`** - Il nome del protocollo del connettore utilizzato per l'indicizzazione. Il valore da utilizzare con questo connettore è `io-sp`.
-   **`collection`** - Questo attributo viene utilizzato per decomprimere i file temporanei. 
-   **`classname`** - Nome della classe Java per il connettore. Utilizza `plugin:io-sharepoint.plugin@connector` per questo connettore.
-   **`logging-config`** - Specifica il file utilizzato per la configurazione delle opzioni di registrazione; deve essere formattato come una stringa XML `log4j`.
-   **`seed-url-type`** - Identifica il tipo di oggetto SharePoint a cui puntano gli URL seed forniti: raccolte di siti o applicazioni web (note anche come server virtuali).

    -   `Site Collections` - Se il tipo di URL seed è impostato su Site Collections, solo l'elemento secondario della raccolta di siti a cui fa riferimento l'URL viene indicizzato.
    -   `Web Applications` - Se il tipo di URL seed è impostato su Web Applications, tutte le raccolte di siti (e i loro elementi secondari) che appartengono alle applicazioni web a cui fa riferimento ogni URL vengono indicizzate.
-   **`auth-type`** - Il meccanismo di autenticazione da utilizzare durante il contatto con il server SharePoint: `BASIC`, `NTLM2`, `KERBEROS` o `CBA`. Il tipo di autenticazione predefinito è `NTLM2`.
-   **`spUser`** - Il nome utente dell'utente SharePoint utilizzato per accedere al contenuto. Questo utente deve avere accesso a tutti gli elenchi e siti di destinazione da ricercare e indicizzare e deve essere in grado di richiamare e risolvere le autorizzazioni associate. È meglio inserirlo con il nome del dominio, come ad esempio: `MYDOMAIN\\Administrator`.
-   **`spPassword`** - La password dell'utente SharePoint utilizzato per accedere al contenuto. La password deve essere codificata utilizzando il programma vcrypt fornito con il data crawler.
-   **`cba-sts`** - L'URL per l'endpoint STS (Security Token Service) con cui tentare di autenticare l'utente dell'indicizzazione. Per SharePoint in loco con ADFS, dovrebbe essere il tuo endpoint ADFS. Se il tipo di autenticazione è impostato su CBA (Claims Based Authentication), allora questo campo è obbligatorio.
-   **`cba-realm`** - L'indicatore di attendibilità della parte di inoltro da utilizzare durante la richiesta di un token di sicurezza da STS. È a volte conosciuto come valore "AppliesTo" o "Realm". Per SharePoint Online, dovrebbe essere l'URL alla root dell'istanza SharePoint Online (ad esempio, `https://mycompany.sharepoint.com `). Per ADFS, è il valore dell'ID per l'attendibilità della parte di inoltro tra SharePoint e ADFS (ad esempio, `"urn: SHAREPOINT:adfs"`).
-   **`everyone-group`** - Quando specificato, questo nome del gruppo viene utilizzato negli ACL quando l'accesso deve essere fornito a tutti. Questo campo è obbligatorio quando è abilitata l'indicizzazione dei profili utente.

    **Nota:** la sicurezza non è rispettata dal servizio Retrieve and Rank.

-   **`user-profile-master-url`** - L'URL di base che il connettore utilizza per creare i link ai profili utente. Dovrebbe essere configurato per puntare al formato di visualizzazione dei profili utente. Se viene rilevato il token `%FIRST_SEED%`, viene sostituito con il primo URL seed. Obbligatorio quando l'indicizzazione dei profili utente è abilitata.
-   **`urls`** - Elenco di URL HTTP separati da nuove righe di raccolte di siti o applicazioni web SharePoint da indicizzare.
-   **`ehcache-config`** - Opzione non utilizzata.
-   **`method`** - Il metodo (`GET` o `POST`) con cui verranno trasmessi i parametri.
-   **`cache-types`** - Opzione non utilizzata.
-   **`cache-size`** - Opzione non utilizzata.
-   **`enable-acl`** - Abilita l'indicizzazione dei profili utente SharePoint; i valori sono `true` o `false`; il valore predefinito è `false`.

### Configurazione del seed di indicizzazione SharePoint

Possono essere configurati i seguenti valori aggiuntivi per il file seed di indicizzazione Samba. Per impostare questi valori, apri il file `config/seeds/sharepoint-seed.conf` e specifica i seguenti valori specifici per i tuoi casi di utilizzo:

-   **`url`** - Elenco di URL separati da nuove righe di raccolte di siti o applicazioni web SharePoint da indicizzare.Ad esempio:

    ```
    io-sp://a.com
    io-sp://b.com:83/site
    io-sp://c.com/site2
    ```
    {: codeblock}

    Saranno indicizzati anche i siti secondari di questi siti (a meno che non siano esclusi da altre regole di indicizzazione).

-   **`filter-url`** - Elenco di URL separati da nuove righe di raccolte di siti o applicazioni web SharePoint da indicizzare. Ad esempio:

    ```
    http://a.com
    http://b.com:83/site
    http://c.com/site2
    ```
    {: codeblock}

-   **`hops`** - Solo uso interno. 
-   **`n-concurrent-requests`** - Solo uso interno.
-   **`delay`** - Solo uso interno.
-   **`default-allow`** - Solo uso interno.
-   **`seed-protocol`** - Imposta il protocollo seed per gli elementi secondari della raccolta di siti. Necessario quando il protocollo di raccolta di siti è SSL, HTTP o HTTPS. Questo valore deve essere impostato sullo stesso protocollo della raccolta di siti.

## Configurazione delle opzioni di indicizzazione Box

Il connettore Box ti consente di indicizzare la tua istanza Enterprise Box e di indicizzare le informazioni che contiene.

### Configurazione del connettore Box

Le seguenti sono le opzioni di configurazione di base obbligatorie per l'utilizzo del connettore Box. Per impostare questi valori, apri il file `config/connectors/box.conf` e modifica i seguenti valori specifici per i tuoi casi di utilizzo:

-   **`protocol`** - Il nome del protocollo del connettore utilizzato per l'indicizzazione. Il valore da utilizzare con questo connettore è `box`.
-   **`classname`** - Nome della classe Java per il connettore. Utilizza `plugin:box.plugin@connector` per questo connettore.
-   **`logging-config`** - Specifica il file utilizzato per la configurazione delle opzioni di registrazione; deve essere formattato come una stringa XML `log4j`.
-   **`box-crawl-seed-url`** - L'URL di base per Box. Il valore per questo connettore è `box://app.box.com/`.

    Puoi indicizzare diversi tipi di URL, ad esempio:

    -   Per indicizzare un'intera azienda: `box://app.box.com/`
    -   Per indicizzare una cartella specifica: `box://app.box.com/user/USER_ID/folder/FOLDER_ID/FolderName`
    -   Per indicizzare un utente specifico: `box://app.box.com/user/USER_ID/`
-   **`client-id`** - Immetti l'ID client fornito da Box quando crei la tua applicazione Box.
-   **`client-secret`** - Immetti il segreto client fornito da Box quando crei la tua applicazione Box.
-   **`path-to-private-key`** - Questa è l'ubicazione, sul tuo file system locale, della chiave privata che fa parte della coppia di chiavi privata-pubblica generata per la comunicazione con Box.
-   **`kid`** - Specifica l'ID della chiave pubblica. Questa è l'altra metà della coppia di chiavi privata-pubblica generata per la comunicazione con Box.
-   **`enterprise-id`** - L'azienda in cui è stata autorizzata l'applicazione. L'ID azienda è elencato nella pagina principale della console di gestione di Box.
-   **`enable-acl`** - Solo uso interno. Abilita il richiamo degli ACL per i dati indicizzati. 
-   **`user-agent`** - Un'intestazione inviata al server durante l'indicizzazione dei documenti.
-   **`method`** - Il metodo (`GET` o `POST`) con cui verranno trasmessi i parametri.
-   **`url-logging`** - L'estensione con cui vengono registrati gli URL indicizzati. I valori possibili sono: 

    -   `full-logging` - Registra tutte le informazioni sull'URL.
    -   `refined-logging` - Registra solo le informazioni necessarie per selezionare il log del crawler e necessarie al connettore per funzionare correttamente; questo è il valore predefinito.
    -   `minimal-logging` - Registra solo la quantità minima di informazioni necessarie al connettore per funzionare correttamente.

    Impostando questa opzione su `minimal-logging` si ridurrà la dimensione dei log e acquisirà un leggero aumento delle prestazioni per via di I/O più piccoli associati alla riduzione della quantità di dati che sta venendo registrata.
-   **`ssl-version`** - Specifica una versione di SSL da utilizzare per le connessioni HTTPS. Per impostazione predefinita viene utilizzato il protocollo più attendibile disponibile.

### Configurazione del seed di indicizzazione Box
{: #box-crawl-options}

Possono essere configurati i seguenti valori aggiuntivi per il file seed di indicizzazione Box. Per impostare questi valori, apri il file `config/seeds/box-seed.conf` e specifica i seguenti valori specifici per i tuoi casi di utilizzo:

-   **`url`** - L'URL da utilizzare come punto di partenza dell'indicizzazione. Il valore predefinito è `box://app.box.com/`.
-   **`default-allow`** - Solo uso interno.

## Limitazioni

Il connettore Box ha alcune limitazioni:

-   I commenti o le attività sui file non vengono richiamati.
-   Il corpo del contenuto delle note viene richiamato come JSON. Potrebbe essere necessaria un ulteriore conversione dei dati delle note.
-   Non è possibile richiamare i singoli documenti tramite Test-It. Possono essere richiamati solo gli URL seed e utente tramite Test-It.
