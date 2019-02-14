---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-03"

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

# Aggiunta di contenuto con il data Crawler

Il data crawler ti consente di automatizzare il caricamento del contenuto nel servizio {{site.data.keyword.discoveryshort}}.
{: shortdesc}

## Indicizzazione dei dati con il data crawler

Il data crawler è uno strumento della riga di comando che ti aiuterà a prendere i tuoi documenti dai repository in cui risiedono (ad esempio: condivisioni di file, database, Microsoft SharePoint) e trasmetterli nel cloud, per essere utilizzati dal servizio {{site.data.keyword.discoveryshort}}.

Puoi utilizzare la strumentazione {{site.data.keyword.discoveryshort}} o l'API per indicizzare le origini dati Box, Salesforce e Microsoft SharePoint Online. Per ulteriori informazioni, vedi [Connessione alle origini dati](/docs/services/discovery/connect.html).
{: tip}

## Quando utilizzare il data crawler

Il data crawler dovrebbe essere utilizzato se desideri avere un caricamento gestito di un numero significativo di file da un sistema remoto oppure se vuoi estrarre il contenuto da un repository supportato (come ad esempio un database DB2).

Il data crawler non è concepito per essere una soluzione per caricare i file dalla tua unità locale. Il caricamento dei file da un'unità locale dovrebbe essere effettuato utilizzando la strumentazione o le chiamate API dirette.
{: tip}

## Utilizzo del data crawler

1. [Configura il servizio {{site.data.keyword.discoveryshort}}](/docs/services/discovery/building.html#configuring-your-service)
1. [Scarica e installa il data crawler](/docs/services/discovery/data-crawler-install.html) su un sistema Linux supportato che ha accesso al contenuto che vuoi indicizzare.
1. [Collega il data crawler](/docs/services/discovery/data-crawler-seeds.html) al tuo contenuto.
1. [Configura il data crawler](/docs/services/discovery/data-crawler-discovery.html) per collegarsi al servizio {{site.data.keyword.discoveryshort}}.
1. [Indicizza il tuo contenuto](/docs/services/discovery/data-crawler-run.html).

Puoi iniziare rapidamente ad utilizzare il data crawler seguendo l'esempio in: [Introduzione al data crawler](/docs/services/discovery/data-crawler-qs.html)
