---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-28"

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

# Configurazione del data crawler
{: #configuring-the-data-crawler}

Per configurare il data crawler per eseguire la ricerca per l'indicizzazione del tuo repository, devi specificare l'adattatore di input appropriato nel file `crawler.conf` e quindi configurare le informazioni specifiche del repository nei file di configurazione dell'adattatore di input.
{: shortdesc}

Il Data Crawler deve essere utilizzato solo per effettuare una ricerca per l'indicizzazione di condivisioni di file o di database; in tutti gli altri casi, devi usare il connettore {{site.data.keyword.discoveryshort}} appropriato. Per i dettagli, vedi [Connessione alle origini dati](/docs/services/discovery?topic=discovery-sources#sources). Non viene più fornita assistenza per il Data Crawler se lo stai utilizzando con un'origine dati supportata dai connettori {{site.data.keyword.discoveryshort}}.
{: important}

Prima di apportare le modifiche elencate in queste fasi, assicurati di aver creato la tua directory di lavoro copiando il contenuto della directory `{installation_directory}/share/examples/config` in una directory di lavoro sul tuo sistema, ad esempio `/home/config`.

**Importante:** non modificare direttamente i file di esempio di configurazione forniti. Copiali e poi modificali. Se modifichi i file di esempio sul posto, la tua configurazione potrebbe essere sovrascritta quando aggiorni il data crawler oppure rimossa quando lo disinstalli.

**Nota:** i riferimenti in questa guida ai file nella directory `config`, come ad esempio `config/crawler.conf`, fanno riferimento al file nella tua directory di lavoro e NON nella directory `{installation_directory}/share/examples/config` installata.

I valori specificati sono i valori predefiniti in `config/crawler.conf` e poi configura il connettore del file system:

1.  Apri il file `config/crawler.conf` in un editor di testo.

    -   Imposta l'opzione `crawl_config_file` sul `.conf` che hai precedentemente modificato, ad esempio: `connectors/filesystem.conf`.
    -   Imposta l'opzione `crawl_seed_file` sul `-seed.conf` che hai precedentemente modificato, ad esempio: `seeds/filesystem-seed.conf`.
    -   Imposta le opzioni `output_adapter` `class` e `config` per il servizio {{site.data.keyword.discoveryshort}} nel seguente modo:

        ```
        class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

        config - "discovery_service"

        discovery_service {
          include "discovery/discovery_service.conf"
        }
        ```
        {: codeblock}

    Esistono altre impostazioni facoltative in questo file che possono essere impostate in modo appropriato per il tuo ambiente, consulta: [Configurazione delle opzioni di ricerca per l'indicizzazione ](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-crawl-options), [Configurazione dell'adattatore di input](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#input-adapter), [Configurazione dell'adattatore di output](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#output-adapter) e [Ulteriori opzioni di gestione della ricerca per l'indicizzazione](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#additional-crawl-management-options) per informazioni dettagliate sull'impostazione di questi valori.

1.  Apri il file `discovery/discovery_service.conf` in un editor di testo. Modifica i seguenti valori specifici per il servizio {{site.data.keyword.discoveryshort}} che hai precedentemente creato su {{site.data.keyword.Bluemix}}:

    -   `environment_id` - Il tuo ID dell'ambiente del servizio {{site.data.keyword.discoveryshort}}.
    -   `collection_id` - Il tuo ID della raccolta del servizio {{site.data.keyword.discoveryshort}}.
    -   `configuration_id` - Il tuo ID della configurazione del servizio {{site.data.keyword.discoveryshort}}.
    -   `configuration` - L'ubicazione del percorso completo di questo file `discovery_service.conf`, ad esempio, `/home/config/discovery/discovery_service.conf`.
    -   `username` - Le credenziali di nome utente per il tuo servizio {{site.data.keyword.discoveryshort}}.
    -   `apikey` - Le credenziali per il tuo servizio {{site.data.keyword.discoveryshort}}.

    Esistono altre impostazioni facoltative in questo file che possono essere impostate in modo appropriato sul tuo ambiente. Per informazioni dettagliate, consulta [Configurazione delle opzioni del servizio](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-service-options) sulla configurazione di questi valori.

1.  Dopo aver modificato questi file, sei pronto a eseguire la ricerca per l'indicizzazione dei dati. Per continuare procedi con [Ricerca per l'indicizzazione del tuo repository di dati](/docs/services/discovery?topic=discovery-crawling-your-data-repository#crawling-your-data-repository).

## Configurazione delle opzioni di ricerca per l'indicizzazione
{: #configuring-crawl-options}

Il file `config/crawler.conf` contiene informazioni che indicano al data crawler quali file utilizzare per la sua ricerca per l'indicizzazione (adattatore di input), dove inviare la raccolta di file oggetto di tale ricerca una volta completata quest'ultima (adattatore di output) e altre opzioni di gestione dell'indicizzazione.

**Nota:** tutti i percorsi di file sono correlati alla directory `config`, tranne dove indicato.

Per accedere al manuale incluso nel prodotto per il file `crawler.conf`, con le informazioni più aggiornate, immetti il seguente comando dalla directory di installazione del crawler: `man crawler.conf`
{: tip}

Le opzioni che possono essere impostate in questo file sono:

### Adattatore di input
{: #input-adapter}

-   **`class`** - Solo uso interno; definisce la classe dell'adattatore di input del data crawler. Il valore predefinito è: `com.ibm.watson.crawler.connectorframeworkinputadapter.Crawl`
-   **`config`** - Solo uso interno; definisce la configurazione del framework del connettore. La chiave di configurazione predefinita all'interno di questo blocco da passare all'adattatore di input scelto è: `connector_framework`

    Il framework del connettore è ciò che ti consente di comunicare con i tuoi dati. Potrebbero essere dati interni all'azienda o dati esterni sul web o nel cloud. I connettori consentono l'accesso ad un certo numero di origini dati diverse, mentre la connessione è al momento controllata dal processo di ricerca per l'indicizzazione.

    **Importante:** i dati richiamati dall'adattatore di input del framework del connettore vengono memorizzati nella cache localmente. Non vengono memorizzati crittografati. Per impostazione predefinita, i dati vengono memorizzati nella cache in una directory temporanea che dovrebbe essere ripulita al riavvio ed essere leggibile solo dall'utente che ha eseguito il comando del crawler.

    Esiste una possibilità che questa directory abbia una durata superiore al crawler se il framework del connettore è stato eliminato prima della ripulitura. Considera con attenzione l'ubicazione dei tuoi dati memorizzati nella cache - potresti averli messi su un file system crittografato, ma devi tenere presenti le implicazioni sulle prestazioni di far ciò. Solo tu puoi decidere il giusto equilibrio tra velocità e sicurezza per le tue ricerche per l'indicizzazione.
-   **`crawl_config_file`** - Il file di configurazione da utilizzare per la ricerca per l'indicizzazione. Il valore predefinito è: `connectors/filesystem.conf`
-   **`crawl_seed_file`** - Il file seed di ricerca per l'indicizzazione da utilizzare per la ricerca per l'indicizzazione. Il valore predefinito è: `seeds/filesystem-seed.conf`
-   **`id_vcrypt_file`** - Il keyfile utilizzato per la codifica dei dati dal crawler; la chiave predefinita inclusa con il crawler è `id_vcrypt`. Utilizza lo script vcrypt nella cartella `bin` se hai bisogno di generare un nuovo file `id_vcrypt`.
-   **`crawler_temp_dir`** - La cartella temporanea del crawler per i log del connettore. Viene fornito il valore predefinito `tmp`. Se non esiste già, la cartella `tmp` verrà creata nella directory di lavoro corrente.
-   **`extra_jars_dir`** - Aggiunge una directory di ulteriori JAR al classpath del framework del connettore.

    **Nota:** relativa alla directory `lib/java` del framework del connettore.

    -   Questo valore deve essere `database` quando utilizzi il connettore Database.

    Puoi lasciare questo valore vuoto (ad esempio, la stringa vuota "") quando utilizzi altri connettori.

-   **`urls_to_filter`** - Blacklist di URL che non dovrebbero essere sottoposti a una ricerca per l'indicizzazione, nel formato dell'espressione regolare. Il data crawler non eseguirà la ricerca per l'indicizzazione degli URL che corrispondono ad una qualsiasi delle espressioni regolari fornite.

    Il `domain list` contiene i domini che non possono essere sottoposti a una ricerca per l'indicizzazione. Aggiungi a questo elenco se necessario.

    Il `filetype list` contiene le estensioni file che il servizio di orchestrazione non supporta.

    Rimuovi tutti i tipi di file supportati dalle espressioni regolari.

    Assicurati che il tuo dominio URL seed sia consentito dal filtro. Utilizza un filtro vuoto per il funzionamento `allow everything`.

    Assicurati che l'URL seed non sia escluso da un filtro o che il crawler possa essere sospeso.

-   **`max_text_size`** - La dimensione massima, in byte, di un documento prima di essere scritto su disco dal framework del connettore. Modificando questo valore massimo, si diminuisce la quantità di documenti scritti sul disco, ma si aumentano i requisiti di memoria. Il valore predefinito è `1048576`
-   **`extra_vm_params`** - Ti consente di aggiungere ulteriori parametri Java al comando utilizzato per avviare il framework del connettore.

-   **`bootstrap_logging`** - Scrive il log di avvio del framework del connettore; utile solo per il debug avanzato. I possibili valori sono `true` o `false`. Il file di log verrà scritto in `crawler_temp_dir`

-   **`read-timeout`** - Imposta il tempo (in secondi) in cui il crawler attenderà una risposta dal framework del connettore. Il valore predefinito è 5 secondi.

### Adattatore di output
{: #output-adapter}

-   **`class`** - Definisce la classe dell'adattatore di output del data crawler.
-   **`config`** - Definisce quale chiave di configurazione passare all'adattatore di output. La stringa deve corrispondere a una chiave all'interno di questo oggetto di configurazione. Nel seguente esempio di codice:

    ```
    class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

    config - "discovery_service"

    discovery_service {
        include "discovery/discovery_service.conf"
      }
    ```
    {: codeblock}

    la chiave di configurazione è `discovery_service`.

Devi selezionare un adattatore di output specificando il relativo parametro `class` e la chiave `config`.

-   **Adattatore di output del servizio {{site.data.keyword.discoveryshort}}** - Carica i documenti sottoposti a una ricerca per l'indicizzazione nel servizio {{site.data.keyword.discoveryfull}}. Seleziona questo adattatore impostando il parametro `class` e la chiave `config` nel seguente modo.

```
class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

config - "discovery_service"

discovery_service {
            include "discovery/discovery_service.conf"
          }
```
{: codeblock}

-   **Adattatore di output di verifica** - L'adattatore di output di verifica scrive una rappresentazione dei file sottoposti a una ricerca per l'indicizzazione sul disco in un'ubicazione specificata. Seleziona questo adattatore impostando il parametro `class` e la chiave `config` nel seguente modo.

    Un parametro aggiuntivo, `output_directory`, seleziona la directory in cui deve essere scritta la rappresentazione dei dati sottoposti a una ricerca per l'indicizzazione.

```
class - "com.ibm.watson.crawler.testoutputadapter.TestOutputAdapter"

config - "test"

output_directory - "/tmp/crawler-test-output"`
```
{: codeblock}

-   **`retry`** - Specifica le opzioni per il nuovo tentativo in caso di tentativi non riusciti di inserimento nell'adattatore di output.

    -   `max_attempts` - Numero massimo di nuovi tentativi. Il valore predefinito è `10`
    -   `delay` - Quantità di tempo minima di ritardo tra i tentativi, in secondi. Il valore predefinito è `2`
    -   `exponent_base` - Fattore che determina la crescita del tempo di ritardo per ogni tentativo non riuscito. Il valore predefinito è `2`

    La formula è:

        **`d(nth_retry) - delay * (exponent_base ^ nth_retry)`**

    Ad esempio, le impostazioni predefinite con un ritardo di 1 secondo e una base esponente di 2, provocheranno il secondo tentativo - il terzo tentativo - con un ritardo di 2 secondi invece di 1 e il successivo di 4 secondi.

        `d(0) - 1 * (2 ^ 0)` - 1 secondo
        `d(1) - 1 * (2 ^ 1)` - 2 secondi
        `d(2) - 1 * (2 ^ 2)` - 4 secondi

    Pertanto, con le impostazioni predefinite, si tenterà un invio fino a 10 volte, attendendo fino a circa 1022 secondi - un po' più di 17 minuti. Questo tempo è approssimativo perché viene aggiunto del tempo aggiuntivo al fine di evitare di eseguire contemporaneamente più nuovi invii. Questo tempo "approssimativo" è fino al 10%, per cui l'ultimo tentativo nel precedente esempio potrebbe avere un ritardo fino a 7.7 secondi. Il tempo di attesa non include il tempo utilizzato per il collegamento al servizio, il caricamento dei dati o di attesa di una risposta.

    Il valore `output_timeout` ha qui la precedenza sul tempo di attesa: se il tempo di attesa totale dei nuovi tentativi supera tale impostazione, l'inoltro avrà esito negativo anche se dovesse essere ritentato.
    {: tip}

### Ulteriori opzioni di gestione della ricerca per l'indicizzazione
{: #additional-crawl-management-options}

-   **`full_node_debugging`** - Attiva la modalità di debug; i valori possibili sono `true` o `false`.

    **Importante:** questo inserirà i dati completi di ogni documento sottoposto a una ricerca per l'indicizzazione nei log.   

-   **`logging.log4j.configuration_file`*** - Il file di configurazione da utilizzare per la registrazione. Nel file `crawler.conf` di esempio, questa opzione viene definita in `logging.log4j` e il relativo valore predefinito è `log4j_custom.properties`. Questa opzione deve essere definita in modo simile anche se si utilizza un file `.properties` o `.conf`.   
-   **`shutdown_timeout`** - Specifica il valore di timeout, in minuti, prima di arrestare l'applicazione. Il valore predefinito è `10`.   
-   **`output_limit`** - Il numero più elevato di elementi indicizzabili che il crawler tenterà di inviare contemporaneamente all'adattatore di output. Questo può essere ulteriormente limitato dal numero di core disponibili per l'utilizzo. Viene specificato che in qualsiasi momento dato non ci saranno più di "x" elementi indicizzabili inviati all'adattatore di output in attesa di restituzione. Il valore predefinito è `10`.   
-   **`input_limit`** - Limita il numero di URL che possono essere richiesti dall'adattatore di input in una sola volta. Il valore predefinito è `30`.   
-   **`output_timeout`** - La quantità di tempo, in secondi, prima che il data crawler smetta di effettuare una richiesta all'adattatore di output e poi rimuovere l'elemento dalla coda dell'adattatore di output per consentire un ulteriore elaborazione. Il valore predefinito è `1200`.

    Si dovrebbe tener conto dei vincoli imposti dall'adattatore di output, poiché questi vincoli possono essere collegati ai limiti definiti qui. L'`output_limit` definito si riferisce solo a quanti oggetti indicizzabili possono essere inviati all'adattatore di output alla volta. Una volta che un oggetto indicizzabile viene inviato all'adattatore di output, è "in servizio", come definito dalla variabile `output_timeout`. È possibile che l'adattatore di output stesso abbia un limite che gli impedisce di elaborare tutti gli input che riceve. Ad esempio, l'adattatore di output di orchestrazione può disporre di un pool di connessioni, configurabile per le connessioni HTTP al servizio. Se il valore predefinito è 8, ad esempio, e imposti l'`output_limit` su un numero maggiore di 8, avrai dei processi, in servizio, in attesa di un turno per l'esecuzione. Potresti avere dei timeout.   
-   **`num_threads`** - Il numero di thread paralleli che possono essere eseguiti alla volta. Questo valore può essere un numero intero, che specifica il numero di thread paralleli direttamente o può essere una stringa, con il formato `"xNUM"`, che specifica il fattore di moltiplicazione del numero di processori disponibili, ad esempio, `"x1.5"`. Il valore predefinito è `"30"`

## Configurazione delle opzioni del servizio
{: #configuring-service-options}

Il servizio {{site.data.keyword.discoveryshort}} comunica al crawler come gestire i file sottoposti a una ricerca per l'indicizzazione quando utilizzi il servizio {{site.data.keyword.discoveryfull}}.

Per accedere al manuale incluso nel prodotto per il file `discovery-service.conf`, con le informazioni più aggiornate, immetti il seguente comando dalla directory di installazione del crawler:

  ```bash
  man discovery_service.conf
  ```
  {: pre}
{: tip}

Le opzioni predefinite possono essere modificate direttamente aprendo il file `config/discovery/discovery_service.conf` e specificando i seguenti valori specifici per il tuo caso di utilizzo:

-   **`http_timeout`** - Il timeout, in secondi, per l'operazione di lettura/indicizzazione del documento; il valore predefinito è ` 125 `.
-   **`proxy_host_port`** - (facoltativo) Quando si esegue il data crawler dietro un firewall, potrebbe essere necessario impostare il nome host e il numero di porta del proxy per consentire al data crawler di comunicare con il servizio {{site.data.keyword.discoveryshort}}. Il valore predefinito per questa opzione è una stringa vuota e se è necessario modificarlo, il valore deve essere del formato ` "<host>:<port>"`.
-   **`concurrent_upload_connection_limit`** - Il numero di connessioni simultanee consentite per il caricamento dei documenti. Il valore predefinito è `2`.

    **Nota:** quando utilizzi l'adattatore di output del servizio di orchestrazione, questo numero dovrebbe essere maggiore di o uguale all'`output_limit` impostato quando si configurano le opzioni di ricerca per l'indicizzazione.   

-   **`base_url`** - L'URL a cui verranno inviati i tuoi documenti sottoposti a una ricerca per l'indicizzazione. Per la release corrente del servizio {{site.data.keyword.discoveryshort}}, il valore è `https://gateway.watsonplatform.net/discovery/api`.   
-   **`environment_id`** - L'ubicazione della tua raccolta di documenti indicizzati nell'URL di base.   
-   **`collection_id`** - Il nome della raccolta di documenti che hai configurato nel servizio {{site.data.keyword.discoveryshort}}.
-   **`api_version`** - Solo uso interno. Data dell'ultima modifica della versione dell'API.   
-   **`configuration_id`** - Il nome file del file di configurazione utilizzato dal servizio {{site.data.keyword.discoveryshort}}.
-   **`apikey`** - Le credenziali per eseguire l'autenticazione presso l'ubicazione della tua raccolta di documenti su sui è stata eseguita la ricerca per l'indicizzazione.

L'adattatore di output del servizio {{site.data.keyword.discoveryshort}} può inviare statistiche in modo che {{site.data.keyword.IBM}} comprenda e soddisfi in modo migliore i propri utenti. Le seguenti opzioni possono essere impostate per la variabile `send_stats`:

-   **`jvm`** - Le statistiche JVM (Java Virtual Machine) inviate includono la versione e il fornitore Java, come riportato dalla JVM utilizzata per eseguire il data crawler. Il valore è `true` o `false`. Il valore predefinito è `true`.
-   **`os`** - Le statistiche del sistema operativo (SO) inviate includono il nome del sistema operativo, la versione, e l'architettura, come riportato dalla JVM utilizzata per eseguire il data crawler. Il valore è `true` o `false`. Il valore predefinito è `true`.
