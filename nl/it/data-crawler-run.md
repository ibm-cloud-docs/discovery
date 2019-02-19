---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-18"

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

# Indicizzazione del tuo repository di dati

Dopo che le opzioni del crawler sono state tutte configurate correttamente, puoi eseguire un'indicizzazione sul tuo repository di dati.
{: shortdesc}

Non eseguire mai il crawler come `root`, a meno che non hai bisogno di accedere ai file che solo `root` può leggere.
{: tip}

Immetti il seguente comando: `crawler`

Il crawler ti richiede la documentazione che spiega cosa fare. Puoi eseguire un'indicizzazione di verifica o eseguire un'indicizzazione, in aggiunta ad altre opzioni di indicizzazione.

## Esecuzione di un'indicizzazione di verifica

Immetti il seguente comando: `crawler testit`

Questo comando esegue un'indicizzazione di verifica, che indicizza solo l'URL seed e visualizza tutti gli URL accodati. Se l'URL seed crea un contenuto indicizzabile (ad esempio, è un documento), tale contenuto viene inviato all'adattatore di output e viene stampato sulla schermata. Se il richiamo dell'URL seed provoca l'accodamento degli URL, tali URL verranno visualizzati e nessun contenuto verrà inviato all'adattatore di output. Per impostazione predefinita, vengono visualizzati cinque URL accodati.

Puoi anche specificare un file di configurazione personalizzato come opzione per il comando crawl, ad esempio: `crawler testit --config [config/myconfigfile.conf]`

Il percorso al file di configurazione passato nell'opzione `--config` deve essere un percorso completo. Cioè, deve essere in formati relativi, ad esempio `config/myconfigfile.conf` o `./myconfigfile.conf` o un percorso assoluto come `/path/to/config/myconfigfile.conf`. 

Inoltre, puoi impostare un limite per il numero di URL accodati che vengono visualizzati come opzione per il comando testit, ad esempio: `crawler testit --limit [number]`

## Esecuzione di un'indicizzazione

Immetti il seguente comando: `crawler crawl`

Questo comando esegue un'indicizzazione con il file di configurazione predefinito (`crawler.conf`).

Puoi anche specificare un file di configurazione personalizzato come opzione per il comando crawl, ad esempio: `crawler crawl --config [config/myconfigfile.conf]`

Il percorso al file di configurazione passato nell'opzione `--config` deve essere un percorso completo. Cioè, deve essere in formati relativi, ad esempio `config/myconfigfile.conf` o `./myconfigfile.conf` o un percorso assoluto come `/path/to/config/myconfigfile.conf`. 

## Riavvio di un'indicizzazione

Immetti il seguente comando: `crawler restart`

Questo comando esegue un riavvio dell'indicizzazione avviando una nuova indicizzazione con il file di configurazione predefinito (`crawler.conf`).

Puoi anche specificare un file di configurazione personalizzato come opzione per il comando restart, ad esempio: `crawler restart --config [config/myconfigfile.conf]`

Il percorso al file di configurazione passato nell'opzione `--config` deve essere un percorso completo. Cioè, deve essere in formati relativi, ad esempio `config/myconfigfile.conf` o `./myconfigfile.conf` o un percorso assoluto come `/path/to/config/myconfigfile.conf`. 

## Ripresa di un'indicizzazione

Immetti il seguente comando: `crawler resume`

Questo comando riprende un'indicizzazione da dove era stata arrestata con il file di configurazione predefinito (`crawler.conf`).

Puoi anche specificare un file di configurazione personalizzato come opzione per il comando resume, ad esempio: `crawler resume --config [config/myconfigfile.conf]`

Il percorso al file di configurazione passato nell'opzione `--config` deve essere un percorso completo. Cioè, deve essere in formati relativi, ad esempio `config/myconfigfile.conf` o `./myconfigfile.conf` o un percorso assoluto come `/path/to/config/myconfigfile.conf`. 

## Aggiornamento di un'indicizzazione 

Immetti il seguente comando: `crawler refresh`

Il comando aggiorna un'indicizzazione precedente con il file di configurazione predefinito (`crawler.conf`).

Puoi anche specificare un file di configurazione personalizzato come opzione per il comando refresh, ad esempio: `crawler refresh --config [config/myconfigfile.conf]`

Il percorso al file di configurazione passato nell'opzione `--config` deve essere un percorso completo. Cioè, deve essere in formati relativi, ad esempio `config/myconfigfile.conf` o `./myconfigfile.conf` o un percorso assoluto come `/path/to/config/myconfigfile.conf`. 
