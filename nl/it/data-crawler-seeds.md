---

copyright:
  years: 2015, 2017, 2019
lastupdated: "2019-01-28"

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

# Configurazione delle opzioni seed e connettore
{: #configuring-connector-and-seed-options}

Quando esegui una ricerca per l'indicizzazione dei dati, il crawler identifica prima il tipo di repository di dati (connettore) e l'ubicazione di partenza specificata dall'utente (seed) per iniziare a scaricare le informazioni.
{: shortdesc}

Il Data Crawler deve essere utilizzato solo per effettuare una ricerca per l'indicizzazione di condivisioni di file o di database; in tutti gli altri casi, devi usare il connettore {{site.data.keyword.discoveryshort}} appropriato. Per i dettagli, vedi [Connessione alle origini dati](/docs/services/discovery?topic=discovery-sources#sources). Non viene più fornita assistenza per il Data Crawler se lo stai utilizzando con un'origine dati supportata dai connettori {{site.data.keyword.discoveryshort}}.
{: important}

**Importante:** quando utilizzi il data crawler, le impostazioni di sicurezza del repository di dati vengono ignorate.

I seed sono i punti di partenza di una ricerca per l'indicizzazione e vengono utilizzati dal data crawler per richiamare i dati dalla risorsa identificata dal connettore. Normalmente, i seed configurano gli URL per accedere alle risorse basate sul protocollo, come le condivisioni di file, le condivisioni SMB, i database e altri repository di dati accessibili tramite vari protocolli. Inoltre, diversi URL seed hanno funzionalità diverse. I seed possono anche essere specifici per il repository, per abilitare la ricerca per l'indicizzazione di applicazioni di terze parti specifiche come i sistemi di gestione delle relazioni con la clientela (CRM), i sistemi del ciclo di vita del prodotto (PLC), i sistemi di gestione dei contenuti (CMS), le applicazioni basate sul cloud e le applicazioni del database web.

Per sottoporre a una ricerca per l'indicizzazione i dati correttamente, devi assicurarti che il crawler sia configurato correttamente in modo da leggere il tuo repository di dati. Il Data Crawler fornisce i connettori per supportare la raccolta di dati dai seguenti repository:

-   [File system](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-filesystem-crawl-options)
-   [Database, tramite JDBC](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-database-crawl-options)
-   [CMIS (Content Management Interoperability Services)](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-cmis-crawl-options)
-   [Condivisioni SMB (Server Message Block), CIFS (Common Internet Filesystem) o Samba](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#smb-cifs-samba-crawl-options)

Viene anche fornito un modello di configurazione del connettore, che ti consente di personalizzare un connettore.

Per configurare il tuo connettore, effettua le seguenti operazioni:

1.  Apri il file nella directory `connectors` che corrisponde al repository a cui ti stai collegando (ad esempio `filesystem.conf` è il file di configurazione per il connettore del file system) in un editor di testo.

1.  Modifica i valori appropriati per il tuo repository:

    -   [File system](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#filesystem-crawl-options)
    -   [Database, tramite JDBC](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#database-crawl-seed)
    -   [CMIS (Content Management Interoperability Services)](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#cmis-crawl-options)
    -   [Condivisioni SMB (Server Message Block), CIFS (Common Internet Filesystem) o Samba](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#smb-cifs-samba-crawl-options)
1.  Salva e chiudi il file.
1.  Ripeti questi passi per il file `-seed.conf` nella directory `connectors/seeds` che corrisponde al repository a cui ti stai collegando (ad esempio `filesystem-seed.conf` è il file di configurazione (a cui collegarsi) seed per il connettore del file system) in un editor di testo.
1.  Procedi con la [configurazione del data crawler per il collegamento a {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-the-data-crawler).

Per accedere al manuale incluso nel prodotto per i file di configurazione del seed e del connettore, con le informazioni più aggiornate, immetti i seguenti comandi dalla directory di installazione del crawler:
-   Per le opzioni di configurazione del connettore:
    ```bash
    man crawler-options.conf
    ```
    {: pre}
-   Per le opzioni di configurazione del seed di ricerca per l'indicizzazione:
    ```bash
    man crawler-seed.conf
    ```
    {: pre}


## Configurazione delle opzioni di ricerca per l'indicizzazione del file system
{: #filesystem-crawl-options}

Il connettore del file system ti consente di eseguire la ricerca per l'indicizzazione dei file locali all'installazione del data crawler.

Un'altra opzione per caricare elevati numeri di file in {{site.data.keyword.discoveryshort}} è [discovery-files ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/IBM/discovery-files){: new_window} su GitHub.
{: note}

### Configurazione del connettore del file system
{: #filesystem-connector}

Le seguenti sono le opzioni di configurazione di base obbligatorie per l'utilizzo del connettore del file system. Per impostare questi valori, apri il file `config/connectors/filesystem.conf` e modifica i seguenti valori specifici per i tuoi casi di utilizzo:

-   **`protocol`** - Il nome del protocollo del connettore utilizzato per la ricerca per l'indicizzazione. Utilizza `sdk-fs` per questo connettore.
-   **`collection`** - Questo attributo viene utilizzato per decomprimere i file temporanei. Il valore predefinito è `crawler-fs`
-   **`logging-config`** - Specifica il file utilizzato per la configurazione delle opzioni di registrazione; deve essere formattato come una stringa XML `log4j`.
-   **`classname`** - Nome della classe Java per il connettore. Il valore da utilizzare con questo connettore deve essere `plugin:filesystem.plugin@filesystem`.

### Configurazione del seed di ricerca per l'indicizzazione del file system
{: #filesystem-crawl-seed}

Possono essere configurati i seguenti valori per il file seed di ricerca per l'indicizzazione del file system. Per impostare questi valori, apri il file `config/seeds/filesystem-seed.conf` e specifica i seguenti valori specifici per i tuoi casi di utilizzo:

-   **`url`** - Elenco di file e cartelle separati da nuove righe da sottoporre a una ricerca per l'indicizzazione. Gli utenti UNIX possono utilizzare un percorso come ad esempio `/usr/local/`.

    **Nota:** Gli URL devono iniziare con `sdk-fs://`. Quindi per sottoporre a una ricerca per l'indicizzazione, ad esempio, `/home/watson/mydocs`, il valore di questo URL dovrebbe essere `sdk-fs:///home/watson/mydocs` - la terza `/` è necessaria!

    I file system utilizzati da sistemi di computer Linux, UNIX e simili a UNIX possono contenere tipi speciali di file, come ad esempio i nodi e i file di dispositivi a caratteri o blocchi che rappresentano pipe denominati, che non possono essere sottoposti a una ricerca per l'indicizzazione perché non contengono dati, ma funzionano come un dispositivo o punti di accesso I/O. Il tentativo di sottoporre a una ricerca per l'indicizzazione tali file genererà degli errori durante la ricerca per l'indicizzazione. Per evitare tali errori, devi escludere la directory `/dev` in tutte le ricerche per l'indicizzazione di livello superiore su un file system Linux, UNIX o simile a UNIX. Se presenti sul sistema di cui stai eseguendo la ricerca per l'indicizzazione, devi escludere anche le directory di sistema temporanee come `/proc`, `/sys` e `/tmp`, che contengono file temporanei e informazioni di sistema.   **`hops`** - Solo uso interno.   **`default-allow`** - Solo uso interno.
    {: tip}

## Configurazione delle opzioni di ricerca per l'indicizzazione del database
{: #database-crawl}

Il connettore del database ti consente di eseguire la ricerca per l'indicizzazione di un database eseguendo un comando SQL personalizzato e creando un documento per riga (record) e un elemento di contenuto per colonna (campo). Puoi specificare una colonna da utilizzare come chiave univoca, nonché una colonna contenente una data/ora che rappresenta l'ultima data di modifica di ogni record. Il connettore richiama tutti i record dal database specificato e può anche essere limitato a tabelle specifiche, unioni e così via nell'istruzione SQL.

Il connettore del database ti consente di eseguire la ricerca per l'indicizzazione dei seguenti database:

-   {{site.data.keyword.IBM}} DB2
-   MySQL
-   Oracle PostgreSQL
-   Microsoft SQL Server
-   Sybase
-   Altri database conformi con SQL, tramite un driver conforme con JDBC 3.0

Il connettore richiama tutti i record dal database e dalla tabella specificati

***Driver JDBC*** - Il connettore del database viene fornito con driver Oracle JDBC (Java Database Connectivity) versione 1.5. Tutti i driver JDBC di terze parti forniti con il data crawler si trovano nella directory `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` della tua installazione del data crawler, dove puoi aggiungerli, rimuoverli e modificarli come necessario. Puoi anche utilizzare l'impostazione `extra_jars_dir` nel file `crawler.conf` per specificare un'altra ubicazione.

***Driver JDBC DB2*** - Il data crawler non viene fornito con i driver JDBC per DB2 a causa di problemi di licenza. Tuttavia, tutte le installazioni DB2 in cui hai installato il supporto JDBC includono i file JAR necessari al data crawler, per poter eseguire la ricerca per l'indicizzazione di un'installazione DB2. Per eseguire una ricerca per l'indicizzazione di un'istanza DB2, devi copiare questi file nella directory appropriata nella tua installazione del data crawler in modo che il connettore del database possa utilizzarli. Per abilitare il data crawler ad eseguire la ricerca per l'indicizzazione di un'installazione DB2, trova il file `db2jcc.jar` e i file JAR di licenza (normalmente, `db2jcc_license_cu.jar`) nella tua installazione DB2 e copiali nella directory secondaria `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` della tua directory di installazione del data crawler, oppure utilizza l'impostazione `extra_jars_dir` nel file `crawler.conf` per specificare un'altra ubicazione.

***Driver JDBC MySQL*** - Il data crawler non viene fornito con i driver JDBC per MySQL a causa di possibili problemi di licenza se vengono forniti come parte del prodotto. Tuttavia, lo scaricare il file JAR che contiene i driver JDBC MySQL e la sua integrazione nella tua installazione del data crawler sono processi facili da eseguire:

1.  Utilizza un browser web per visitare il sito di download di MySQL e individua il link di download di origine e binario per il formato di archivio che vuoi utilizzare (normalmente zip per i sistemi Microsoft Windows o un tarball compresso con GZIP per i sistemi Linux). Fai clic su quel link per avviare il processo di download. Potrebbe essere necessaria la registrazione.
1.  Utilizza il comando unzip archive-file-name o tar zxf archive-file-name appropriato per estrarre il contenuto di tale archivio, in base al tipo e al nome del file di archivio che hai scaricato.
1.  Passa alla directory estratta dal file di archivio e copia il file JAR da questa directory nella directory secondaria `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` della tua directory di installazione del data crawler, oppure utilizza l'impostazione `extra_jars_dir` nel file `crawler.conf` per specificare un'altra ubicazione.

### Configurazione del connettore del database
{: #database-connector}

Le seguenti sono le opzioni di configurazione di base obbligatorie per l'utilizzo del connettore del database. Per impostare questi valori, apri il file config/connectors/database.conf e modifica i seguenti valori specifici per i tuoi casi di utilizzo:

-   **`protocol`** - Il nome del protocollo del connettore utilizzato per la ricerca per l'indicizzazione. Il valore per questo connettore si basa sul sistema di database a cui si deve accede.
-   **`collection`** - Questo attributo viene utilizzato per decomprimere i file temporanei.
-   **`classname`** - Nome della classe Java per il connettore. Il valore da utilizzare con questo connettore deve essere `plugin:database.plugin@database`.
-   **`logging-config`** - Specifica il file utilizzato per la configurazione delle opzioni di registrazione; deve essere formattato come una stringa XML `log4j`.

### Configurazione del seed di ricerca per l'indicizzazione del database
{: #database-crawl-seed}

Possono essere configurati i seguenti valori per il file seed di ricerca per l'indicizzazione del database. Per impostare questi valori, apri il file `config/seeds/database-seed.conf` e specifica i seguenti valori specifici per i tuoi casi di utilizzo:

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
-   **`save-frequency-for-resume`** (opzione Extender) - Specifica il nome di una colonna o di un'etichetta associata, in modo da poter riprendere una ricerca per l'indicizzazione o eseguire un aggiornamento parziale. Il seed salva il nome di questa colonna a intervalli regolari mentre procede con la ricerca per l'indicizzazione e lo salva di nuovo una volta che l'ultima riga del database è stata sottoposta a una ricerca per l'indicizzazione. Quando si riprende la ricerca per l'indicizzazione o la si aggiorna, la ricerca per l'indicizzazione inizia con la riga identificata nel valore salvato per questo campo

## Configurazione delle opzioni di ricerca per l'indicizzazione CMIS
{: #cmis-crawl-options}

Il connettore CMIS (Content Management Interoperability Services) ti consente di eseguire la ricerca per l'indicizzazione dei repository dei sistemi di gestione dei contenuti (CMS) abilitati CMIS, come ad esempio Alfresco, Documentum o {{site.data.keyword.IBM}} Content Manager e di indicizzare i dati che contengono.

### Configurazione del connettore CMIS
{: #cmis-connector}

Le seguenti sono le opzioni di configurazione di base obbligatorie per l'utilizzo del connettore CMIS. Per impostare questi valori, apri il file `config/connectors/cmis.conf` e specifica i seguenti valori specifici per i tuoi casi di utilizzo:

-   **`protocol`** - Il nome del protocollo del connettore utilizzato per la ricerca per l'indicizzazione. Il valore da utilizzare con questo connettore deve essere `cmis`.
-   **`collection`** - Questo attributo viene utilizzato per decomprimere i file temporanei.
-   **`dns`** - Opzione non utilizzata.
-   **`classname`** - Nome della classe Java per il connettore. Utilizza `plugin:cmis-v1.1.plugin@connector` per questo connettore.
-   **`logging-config`** - Specifica il file utilizzato per la configurazione delle opzioni di registrazione; deve essere formattato come una stringa XML `log4j`.
-   **`endpoint`** - L'URL dell'endpoint del servizio di un repository conforme con CMIS. 
-   **`username`** - Il nome utente dell'utente del repository CMIS utilizzato per accedere al contenuto. Questo utente deve avere accesso a tutti i documenti e a tutte le cartelle di destinazione di cui eseguire la ricerca per l'indicizzazione e l'indicizzazione.
-   **`password`** - La password del repository CMIS utilizzata per accedere al contenuto. La password NON deve essere codificata; deve essere fornita in testo semplice.
-   **`repositoryid`** - L'ID del repository CMIS utilizzato per accedere al contenuto per quel repository specifico.
-   **`bindingtype`** - Identifica quale tipo di bind utilizzare per il collegamento a un repository CMIS. Il valore è AtomPub o WebServices.
-   **`authentication`** - Identifica quale tipo di meccanismo di autenticazione utilizzare mentre si contatta un repository compatibile CMIS: autenticazione HTTP di base, NTLM o WS-Security (token nome utente).
-   **`enable-acl`** - Abilita il richiamo degli ACL per i dati sottoposti a una ricerca per l'indicizzazione. Se non sei interessato alla sicurezza dei documenti in questa raccolta, disabilitando questa opzione incrementerai le prestazioni non richiedendo queste informazioni con il documento e non richiamandole e codificandole. Il valore è true o false.
-   **`user-agent`** - Un'intestazione inviata al server durante la ricerca per l'indicizzazione dei documenti.
-   **`method`** - Il metodo (GET o POST) con cui verranno trasmessi i parametri.
-   **`url-logging`** - L'estensione con cui vengono registrati gli URL sottoposti a una ricerca per l'indicizzazione. I valori possibili sono:

    -   `full-logging` - Registra tutte le informazioni sull'URL.
    -   `refined-logging` - Registra solo le informazioni necessarie per selezionare il log del crawler e necessarie al connettore per funzionare correttamente; questo è il valore predefinito.
    -   `minimal-logging` - Registra solo la quantità minima di informazioni necessarie al connettore per funzionare correttamente.

    Impostando questa opzione su `minimal-logging` si ridurrà la dimensione dei log e acquisirà un leggero aumento delle prestazioni per via di I/O più piccoli associati alla riduzione della quantità di dati che sta venendo registrata.
-   **`ssl-version`** - Specifica una versione di SSL da utilizzare per le connessioni HTTPS. Per impostazione predefinita viene utilizzato il protocollo più attendibile disponibile.

### Configurazione del seed di ricerca per l'indicizzazione CMIS
{: #cmis-crawl-seed}

Possono essere configurati i seguenti valori per il file seed di ricerca per l'indicizzazione CMIS. Per impostare questi valori, apri il file `config/seeds/cmis-seed.conf` e modifica i seguenti valori specifici per i tuoi casi di utilizzo:

-   **`url`** - L'URL di una cartella dal repository CMIS da utilizzare come punto di partenza della ricerca per l'indicizzazione, ad esempio: `cmis://alfresco.test.com:8080/alfresco/cmisatom?folderToProcess-workspace://SpacesStore/guid`

    Per eseguire una ricerca per l'indicizzazione dalla cartella root, devi fornire l'URL come: `cmis://alfresco.test.com:8080/alfresco/cmisatom?folderToProcess-`
-   **`at`** - Opzione non utilizzata.
-   **`default-allow`** - Solo uso interno.

## Configurazione delle opzioni di ricerca per l'indicizzazione SMB/CIFS/Samba
{: #smb-cifs-samba-crawl-options}

Il connettore Samba ti consente di sottoporre a una ricerca per l'indicizzazione le condivisioni file SMB (Server Message Block) e CIFS (Common Internet Filesystem). Questo tipo di condivisione file è comune sulle reti Windows ed è fornito anche tramite il progetto open source Samba.

### Configurazione del connettore Samba
{: #smb-cifs-samba-crawl-connector}

Le seguenti sono le opzioni di configurazione di base obbligatorie per l'utilizzo del connettore Samba. Per impostare questi valori, apri il file `config/connectors/samba.conf` e specifica i seguenti valori specifici per i tuoi casi di utilizzo:

-   **`protocol`** - Il nome del protocollo del connettore utilizzato per la ricerca per l'indicizzazione. Il valore per utilizzare questo connettore è smb.
-   **`collection`** - Questo attributo viene utilizzato per decomprimere i file temporanei.
-   **`classname`** - Nome della classe Java per il connettore. Il valore da utilizzare con questo connettore deve essere `plugin:smb.plugin@connector`.
-   **`logging-config`** - Specifica il file utilizzato per la configurazione delle opzioni di registrazione; deve essere formattato come una stringa XML `log4j`.
-   **`username`** - Il nome Samba per l'autenticazione. Se fornito, devono essere forniti anche un dominio e una password. Se non viene fornito, viene utilizzato l'account guest.
-   **`password`** - La password Samba per l'autenticazione. Se viene fornito il nome utente, è obbligatoria. La password deve essere codificata utilizzando il programma vcrypt fornito con il data crawler.
-   **`archive`** - Abilita il connettore Samba a ricercare per l'indicizzazione e indicizzare i file compressi nei file di archivio. Il valore è true o false; il valore predefinito è false.
-   **`max-policies-per-handle`** - Specifica il numero massimo di politiche LSA (Local Security Authority) che possono essere aperte per un solo handle RPC. Queste politiche definiscono le autorizzazioni di accesso obbligatorie per eseguire la query o per modificare un determinato sistema in varie condizioni. Il valore predefinito per questa opzione è 255.
-   **`crawl-fs-metadata`** - L'attivazione di questa opzione provocherà l'aggiunta da parte del data crawler, di un documento VXML che contiene i metadati del file system disponibili sul file (data di creazione, ultima data di modifica, attributi file, ecc)..
-   **`enable-arc-connector`** - Opzione non utilizzata.
-   **`disable-indexes`** - Elenco di indici separati da nuove righe da disabilitare, che può comportare una ricerca per l'indicizzazione più veloce, ad esempio:

    -   `disable-url-index`
    -   `disable-error-state-index`
    -   `disable-crawl-time-index`
-   **`exact-duplicates-hash-size`** - Imposta la dimensione della tabella hash utilizzata per la risoluzione dei duplicati esatti. Fai molta attenzione quando modifichi questo numero. Il valore che selezioni deve essere un numero primo e dimensioni maggiori possono fornire ricerche più rapide ma richiederanno più memoria, mentre dimensioni più piccole possono rallentare le ricerche per l'indicizzazione ma ridurranno notevolmente l'utilizzo della memoria.
-   **`user-agent`** - Opzione non utilizzata.
-   **`timeout`** - Opzione non utilizzata
-   **`n-concurrent-requests`** - Il numero di richieste che verranno inviate in parallelo a un singolo indirizzo IP. Il valore predefinito è `1`.
-   **`enqueue-persistence`** - Opzione non utilizzata.

### Configurazione del seed di ricerca per l'indicizzazione Samba
{: #smb-cifs-samba-crawl-seed}

Possono essere configurati i seguenti valori per il file seed di ricerca per l'indicizzazione Samba. Per impostare questi valori, apri il file `config/seeds/samba-seed.conf` e specifica i seguenti valori specifici per i tuoi casi di utilizzo:

-   **`url`** - Un elenco di condivisioni separate da nuove righe da sottoporre a una ricerca per l'indicizzazione, ad esempio:

    ```
    smb://share.test.com/office
    smb://share.test.com/cash/money/change
    smb://share.test.com/C$/Program Files
    ```
    {: codeblock}

-   **`hops`** - Solo uso interno.
-   **`default-allow`** - Solo uso interno.
