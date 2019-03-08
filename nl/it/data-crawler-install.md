---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-03"

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

# Scaricamento e installazione del data crawler
{: #downloading-and-installing-the-data-crawler}

Il data crawler raccoglie i dati non elaborati che vengono eventualmente utilizzati per formare i risultati della ricerca per il servizio {{site.data.keyword.discoveryshort}}. Quando indicizzi i repository di dati, il crawler scarica i documenti e i metadati, a partire da un URL seed specificato dall'utente. Il crawler rileva i documenti in una gerarchia o altrimenti collegati dall'URL seed e li accoda per il richiamo.
{: shortdesc}

Puoi utilizzare la strumentazione {{site.data.keyword.discoveryshort}} o l'API per indicizzare le origini dati Box, Salesforce e Microsoft SharePoint Online. Per ulteriori informazioni, vedi [Connessione alle origini dati](/docs/services/discovery/connect.html).
{: tip}

## Prerequisiti

-   Java Runtime Environment versione 8 o superiore

    La tua variabile di ambiente `JAVA_HOME` deve essere impostata correttamente o non deve esserlo affatto per eseguire il crawler.
    {: tip}
-   Red Hat Enterprise Linux 6 o 7, o Ubuntu Linux 15 o 16. Per prestazioni ottimali, il data crawler dovrebbe essere eseguito sulla propria istanza di Linux, sia che si tratti di una macchina virtuale, di un contenitore o di un hardware.

-   Minimo 2 GB di RAM sul sistema Linux

## Scarica e installa il data crawler

1.  Apri un browser e accedi al tuo [Account {{site.data.keyword.Bluemix}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net){: new_window}.

1.  Dal tuo dashboard {{site.data.keyword.Bluemix_notm}}, seleziona il servizio {{site.data.keyword.discoveryshort}} che hai precedentemente creato.

1.  Nella sezione **Automate the upload of content to the Discovery service**, fai clic sul link appropriato per scaricare il data crawler per Linux nei formati DEB, RPM e ZIP.

1.  Verifica di avere in esecuzione Java Runtime Environment versione 8 o superiore. Immetti il comando `java -version` e cerca **1.8**. Se hai in esecuzione una versione precedente alla **1.8**, devi eseguire l'upgrade di Java installando il Java Developer Kit (JDK) 8 dal tuo sistema di gestione del pacchetto, dal sito web [IBM JDK ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/developerworks/java/jdk/){: new_window} o da [java.com ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.java.com){: new_window}.

    La tua variabile di ambiente `JAVA_HOME` deve essere impostata correttamente o non deve esserlo affatto per eseguire il crawler.
    {: tip}

1.  In qualità di amministratore, utilizza i comandi appropriati per installare il file di archivio che hai scaricato:

    -   Su sistemi come Red Hat e CentOS che utilizzano i pacchetti rpm, utilizza un comando come il seguente: `rpm -i /full/path/to/rpm/package/rpm-file-name`
    -   Su sistemi come Ubuntu e Debian che utilizzano i pacchetti deb, utilizza un comando come il seguente: `dpkg -i /full/path/to/deb/package/deb-file-name`
    -   Gli script del crawler vengono installati in `{installation_directory}/bin`; ad esempio, `/opt/ibm/crawler/bin`. Assicurati che `{installation_directory}/bin` sia nella tua variabile di ambiente `PATH` in modo che i comandi del crawler funzionino correttamente.

    Gli script del crawler vengono installati anche in `/usr/local/bin`, in modo che possano essere aggiunti anche alla tua variabile di ambiente `PATH`.
    {: tip}
1.  Crea la tua directory di lavoro copiando il contenuto della directory `{installation_directory}/share/examples/config` in una directory di lavoro sul tuo sistema, ad esempio `/home/config`.

    **Avvertenza:** non modificare direttamente i file di esempio di configurazione forniti. Copiali e poi modificali. Se modifichi i file di esempio sul posto, la tua configurazione potrebbe essere sovrascritta quando aggiorni il data crawler oppure rimossa quando lo disinstalli.

    **Nota:** i riferimenti nel resto di questa guida ai file nella directory `config`, come ad esempio `config/crawler.conf`, fanno riferimento al file nella tua directory di lavoro e NON nella directory `{installation_directory}/share/examples/config` installata.

1.  Sei ora pronto a [configurare il data crawler per il collegamento al tuo repository](/docs/services/discovery/data-crawler-seeds.html)

## Struttura del data crawler

Il download del data crawler crea le seguenti cartelle sul tuo sistema:

-   `doc` - Contiene i file con le informazioni di copyright e licenza.
-   `bin` - File di script per l'esecuzione del crawler.
-   `connectorFramework` - I file in questa directory sono quelli che ti consentono di comunicare con i tuoi dati, sia i dati interni all'azienda che i dati esterni sul web o nel cloud.
-   `lib` - File di libreria utilizzati dal crawler.
-   `share`
    -   `doc` - Fornisce i file della documentazione formattati HTML e Markdown.
    -   `examples/config` - File che ti consentono di comunicare al crawler quali dati utilizzare per l'indicizzazione, dove inviare la tua raccolta di dati indicizzati dopo il completamento dell'indicizzazione e altre opzioni di gestione dell'indicizzazione.
    -   `man` - Documentazione del crawler della pagina del manuale incluso nel prodotto.

## Limitazioni note in questa release

-   Il data crawler potrebbe venire sospeso durante l'esecuzione del connettore del file system con un URL mancante o non valido.
-   Configura il valore `urls_to_filter` nel file `crawler.conf`, in modo tale che tutti gli URL o i RegEx nella whitelist siano inclusi in una sola espressione RegEx. Per ulteriori informazioni, consulta [Configurazione delle opzioni di indicizzazione](/docs/services/discovery/data-crawler-discovery.html#configuring-crawl-options).
-   Il percorso al file di configurazione passato nell'opzione `--config -c` deve essere un percorso completo. Cioè, deve essere nei formati relativi `config/crawler.conf` o `./crawler.conf` o il percorso assoluto `/path/to/config/crawler.conf`. Specificare soltanto `crawler.conf` è possibile solo se il file `orchestration_service.conf` è inline invece che di riferimento utilizzando `include` nel file `crawler.conf` .
