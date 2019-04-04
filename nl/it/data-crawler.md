---

copyright:
  years: 2015, 2017, 2019
lastupdated: "2019-02-08"

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

# Aggiunta di contenuto con il data Crawler
{: #adding-content-with-data-crawler}

Il data crawler ti consente di automatizzare il caricamento del contenuto nel servizio {{site.data.keyword.discoveryshort}}.
{: shortdesc}

Il Data Crawler deve essere utilizzato solo per effettuare una ricerca per l'indicizzazione di condivisioni di file o di database; in tutti gli altri casi, devi usare il connettore {{site.data.keyword.discoveryshort}} appropriato. Per i dettagli, vedi [Connessione alle origini dati](/docs/services/discovery?topic=discovery-sources#sources). Non viene più fornita assistenza per il Data Crawler se lo stai utilizzando con un'origine dati supportata dai connettori {{site.data.keyword.discoveryshort}}.
{: important}

## Ricerca per l'indicizzazione dei dati con il data crawler
{: #dc-crawling}

Il Data Crawler è uno strumento della riga di comando che ti aiuterà a prendere i tuoi documenti dai repository in cui risiedono (ad esempio: condivisioni di file, database) e a eseguirne il push nel cloud per essere utilizzati dal servizio {{site.data.keyword.discoveryshort}}.

Il Data Crawler deve essere utilizzato solo per effettuare una ricerca per l'indicizzazione di condivisioni di file o di database; in tutti gli altri casi, devi usare il connettore {{site.data.keyword.discoveryshort}} appropriato per Box, SharePoint, Salesforce, IBM Cloud Object Storage o la ricerca per l'indicizzazione web. Per i dettagli, vedi [Connessione alle origini dati](/docs/services/discovery?topic=discovery-sources#sources). Non viene più fornita assistenza per il Data Crawler se lo stai utilizzando con un'origine dati supportata dai connettori {{site.data.keyword.discoveryshort}}.
{: important}

## Quando utilizzare il data crawler
{: #dc-use}

Il data crawler dovrebbe essere utilizzato se desideri avere un caricamento gestito di un numero significativo di file da un sistema remoto oppure se vuoi estrarre il contenuto da un repository supportato (come ad esempio un database DB2).

Il data crawler non è concepito per essere una soluzione per caricare i file dalla tua unità locale. Il caricamento dei file da un'unità locale dovrebbe essere effettuato utilizzando la strumentazione o le chiamate API dirette. Un'altra opzione per caricare elevati numeri di file in {{site.data.keyword.discoveryshort}} è [discovery-files ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/IBM/discovery-files){: new_window} su GitHub.
{: note}

## Utilizzo del data crawler
{: #dc-using}

1. [Configura il servizio {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-configservice#configservice)
1. [Scarica e installa il data crawler](/docs/services/discovery?topic=discovery-downloading-and-installing-the-data-crawler#downloading-and-installing-the-data-crawler) su un sistema Linux supportato che ha accesso al contenuto che vuoi sottoporre a una ricerca per l'indicizzazione.
1. [Collega il data crawler](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-connector-and-seed-options) al tuo contenuto.
1. [Configura il data crawler](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-the-data-crawler) per collegarsi al servizio {{site.data.keyword.discoveryshort}}.
1. [Indicizza il tuo contenuto](/docs/services/discovery?topic=discovery-crawling-your-data-repository#crawling-your-data-repository).

Puoi iniziare rapidamente ad utilizzare il data crawler seguendo l'esempio in: [Introduzione al data crawler](/docs/services/discovery?topic=discovery-getting-started-with-the-data-crawler#getting-started-with-the-data-crawler)
