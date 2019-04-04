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

# Introduzione al data crawler
{: #getting-started-with-the-data-crawler}

Questo argomento spiega come utilizzare il data crawler per inserire i file dal tuo file system locale, da utilizzare con il servizio {{site.data.keyword.discoveryfull}}.
{: shortdesc}

Il Data Crawler deve essere utilizzato solo per effettuare una ricerca per l'indicizzazione di condivisioni di file o di database; in tutti gli altri casi, devi usare il connettore {{site.data.keyword.discoveryshort}} appropriato. Per i dettagli, vedi [Connessione alle origini dati](/docs/services/discovery?topic=discovery-sources#sources). Non viene più fornita assistenza per il Data Crawler se lo stai utilizzando con un'origine dati supportata dai connettori {{site.data.keyword.discoveryshort}}.
{: important}

Prima di tentare questa attività, crea un'istanza del servizio {{site.data.keyword.discoveryshort}} in {{site.data.keyword.Bluemix}}. Per completare questa guida, dovrai utilizzare le credenziali associate all'istanza del servizio che hai creato.

## Crea un ambiente
{: #dc-create-environment}

Utilizza il metodo bash POST /v1/environments per creare un ambiente. Pensa a un ambiente come al magazzino in cui stai archiviando tutte le tue scatole di documenti. Il seguente esempio crea un ambiente denominato `my-first-environment`:

Sostituisci `{apikey}` con le tue credenziali del servizio.

(Per informazioni più dettagliate sull'utilizzo delle credenziali {apikey}, vedi [Introduzione all'API](/docs/services/discovery?topic=discovery-gs-api#gs-api)).

```bash
curl -X POST -u "apikey:{apikey}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
```
{: pre}

L'API restituisce una risposta che include informazioni come l'ID ambiente, lo stato dell'ambiente e la quantità di memoria che il tuo ambiente sta utilizzando. Non andare avanti al passo successivo fino a quando lo stato del tuo ambiente non è `ready`. Quando crei l'ambiente, se lo stato restituisce `status:pending`, utilizza il metodo `GET /v1/environments/{environment_id}` per controllare lo stato finché non diventa ready. In questo esempio, sostituisci `{apikey}` con le tue credenziali del servizio e sostituisci `{environment_id}` con l'ID ambiente che è stato restituito quando hai creato l'ambiente.

```bash
curl -u "apikey:{apikey}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}?version=2017-11-07
```
{: pre}

## Crea una raccolta
{: #dc-create-collection}

Successivamente, utilizza il metodo `POST /v1/environments/{environment_id}/collections` per creare una raccolta. Pensa a una raccolta come a una scatola in cui archivierai i tuoi documenti nel tuo ambiente. Questo esempio crea una raccolta denominata `my-first-collection` nell'ambiente creato nel passo precedente e utilizza la seguente configurazione predefinita:

-   Sostituisci `{apikey}` con le tue credenziali del servizio.
-   Sostituisci `{environment_id}` con l'ID dell'ambiente che hai creato nel passo 1.

Prima di creare una raccolta devi richiamare l'ID della tua configurazione predefinita. Per trovare il tuo valore predefinito per `configuration_id`, utilizza il metodo `GET /v1/environments/{environment_id}/configurations`:

```bash
curl -u "apikey:{apikey}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07
```
{: pre}

Una volta che disponi dell'ID di configurazione predefinito, utilizzalo per creare la tua raccolta. Sostituisci `{configuration_id}` con l'ID di configurazione predefinito del tuo ambiente.

```bash
curl -X POST -u "apikey:{apikey}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{configuration_id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07
```
{: pre}

L'API restituisce una risposta che include informazioni come il tuo ID di raccolta, lo stato della raccolta e quanta memoria sta utilizzando la tua raccolta. Non andare avanti al passo successivo fino a quando lo stato della tua raccolta non è `online`. Quando crei la raccolta, se lo stato restituisce `status:pending`, utilizza il metodo `GET /v1/environments/{environment_id}/collections/{collection_id}` per controllare lo stato finché non diventa ready. In questo esempio, sostituisci `{apikey}` con le tue credenziali del servizio, sostituisci `{environment_id}` con il tuo ID ambiente e sostituisci `{collection_id}` con l'ID raccolta che era stato restituito in precedenza in questo passo.

```bash
curl -u "apikey:{apikey}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07
```
{: pre}

## Scarica i documenti di esempio
{: #dc-download-documents}

Scarica questi documenti:

-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno"></a>

## Scarica e installa il data crawler
{: #download-and-install-the-data-crawler}

1.  Verifica i tuoi prerequisiti di sistema

    -   Java Runtime Environment versione 8 o superiore

        **Nota:** la tua variabile di ambiente `JAVA_HOME` deve essere impostata correttamente o non deve esserlo affatto per eseguire il crawler.
    -   Red Hat Enterprise Linux 6 o 7 o Ubuntu Linux 15 o 16. Per prestazioni ottimali, il data crawler dovrebbe essere eseguito sulla propria istanza di Linux, sia che si tratti di una macchina virtuale, di un contenitore o di un hardware.
    -   Minimo 2 GB di RAM sul sistema Linux

1.  Apri un browser e accedi al tuo [account {{site.data.keyword.Bluemix_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/){: new_window}.
1.  Dal tuo dashboard {{site.data.keyword.Bluemix_notm}}, seleziona il servizio {{site.data.keyword.discoveryshort}} che hai precedentemente creato.
1.  In **Automate the upload of content to the Discovery service**, seleziona il link di scaricamento appropriato per il tuo sistema (DEB, RPM o ZIP) per scaricare il data crawler.
1.  In qualità di amministratore, utilizza i comandi appropriati per installare il file di archivio che hai scaricato:

    -   Su sistemi come Red Hat e CentOS che utilizzano i pacchetti rpm, utilizza un comando come il seguente: `rpm -i /full/path/to/rpm/package/rpm-file-name`
    -   Su sistemi come Ubuntu e Debian che utilizzano i pacchetti deb, utilizza un comando come il seguente: `dpkg -i /full/path/to/deb/package/deb-file-name`
    -   Gli script del crawler vengono installati in `{installation directory}/bin`; ad esempio, `/opt/ibm/crawler/bin`. Assicurati che `{installation_directory}/bin` sia nella tua variabile di ambiente `PATH` in modo che i comandi del crawler funzionino correttamente.

    Gli script del crawler vengono installati anche in `/usr/local/bin`, in modo che possano essere aggiunti anche alla tua variabile di ambiente `PATH`.
    {: tip}

## Crea la tua directory di lavoro
{: #dc-working-directory}

Copia il contenuto della directory `{installation_directory}/share/examples/config` in una directory di lavoro sul tuo sistema, ad esempio `/home/config`.

**Avvertenza:** non modificare direttamente i file di esempio di configurazione forniti. Copiali e poi modificali. Se modifichi i file di esempio sul posto, la tua configurazione potrebbe essere sovrascritta quando aggiorni il data crawler oppure rimossa quando lo disinstalli.

**Nota:** i riferimenti in questa guida ai file nella directory `config`, come ad esempio `config/crawler.conf`, fanno riferimento al file nella tua directory di lavoro e NON nella directory `{installation_directory}/share/examples/config` installata.

## Configura le opzioni di ricerca per l'indicizzazione
{: #dc-configure-crawl-options}

Per configurare il data crawler per eseguire la ricerca per l'indicizzazione del tuo repository, devi specificare quali file system locali vuoi sottoporre a una ricerca per l'indicizzazione e a quale servizio {{site.data.keyword.discoveryshort}} inviare la raccolta di file sottoposti a una ricerca per l'indicizzazione, una volta che è stata completata tale ricerca.

1.  **`filesystem-seed.conf`** - Apri il file `seeds/filesystem-seed.con` in un editor di testo. Modifica l'attributo `value` direttamente nell'attributo `name-"url"` con il percorso file che vuoi sottoporre a una ricerca per l'indicizzazione. Ad esempio: `value-"sdk-fs:///TMP/MY_TEST_DATA/"`

    **Nota:** Gli URL devono iniziare con `sdk-fs://`. Quindi per eseguire una ricerca per l'indicizzazione, ad esempio, `/home/watson/mydocs`, il valore di questo URL dovrebbe essere `sdk-fs:///home/watson/mydocs` - la terza / è necessaria!

    Salva e chiudi il file.

1.  **`discovery_service.conf`** - Apri il file `discovery/discovery_service.conf` in un editor di testo. Modifica i seguenti valori specifici per il servizio {{site.data.keyword.discoveryshort}} che hai precedentemente creato su {{site.data.keyword.Bluemix_notm}}:

    -   `environment_id` - Il tuo ID dell'ambiente del servizio {{site.data.keyword.discoveryshort}}.
    -   `collection_id` - Il tuo ID della raccolta del servizio {{site.data.keyword.discoveryshort}}.
    -   `configuration_id` - Il tuo ID della configurazione del servizio {{site.data.keyword.discoveryshort}}.
    -   `configuration` - L'ubicazione del percorso completo di questo file `discovery_service.conf`, ad esempio, `/home/config/discovery/discovery_service.conf`.
    -   `apikey` - Le credenziali per il tuo servizio {{site.data.keyword.discoveryshort}}.
1.  **`crawler.conf`** - Apri il file `config/crawler.conf` in un editor di testo.

    -   Imposta le opzioni `output_adapter` `class` e `config` per il servizio {{site.data.keyword.discoveryshort}} nel seguente modo:

        ```bash
        class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

        config - "discovery_service"

        discovery_service {
          include "discovery/discovery_service.conf"
        }
        ```
        {: pre}

1.  Dopo aver modificato questi file, sei pronto a eseguire la ricerca per l'indicizzazione dei dati.

## Ricerca per l'indicizzazione i tuoi dati
{: #dc-crawl}

Immetti il seguente comando: `crawler crawl --config [config/crawler.conf]`

Eseguirà una ricerca per l'indicizzazione con il file di configurazione `crawler.conf`.

**Nota:** il percorso al file di configurazione passato nell'opzione `--config` deve essere un percorso completo. Cioè, deve essere in formati relativi, ad esempio `config/crawler.conf` o `./crawler.conf` o un percorso assoluto come `/path/to/config/crawler.conf`.

## Ricerca i tuoi documenti
{: #dc-search}

Infine, utilizza il metodo `GET /v1/environments/{environment_id}/collections/{collection_id}/query` per cercare la tua raccolta di documenti. Il seguente esempio restituisce tutte le entità denominate `IBM`:

-   Sostituisci `{apikey}` con le tue credenziali del servizio.
-   Sostituisci `{environment_id}` con l'ID dell'ambiente che hai creato nel passo 1.
-   Sostituisci `{collection_id}` con l'ID della raccolta che hai creato nel passo 2.

```bash
curl -u "apikey:{apikey}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query-enriched_text.entities.text:IBM'
```
{: pre}

## Risultati
{: #dc-results}

Hai ora eseguito correttamente la query dei documenti in un ambiente e in una raccolta che hai creato. Ora puoi iniziare con la personalizzazione aggiungendo ulteriori documenti alla raccolta.
