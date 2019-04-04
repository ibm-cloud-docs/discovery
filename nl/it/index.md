---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-07"

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

# Informazioni
{: #about}

{{site.data.keyword.discoveryfull}} rende possibile creare rapidamente applicazioni di esplorazione basate sul cloud e cognitive che sbloccano le informazioni approfondite azionabili nascoste nei dati non strutturati - inclusi i tuoi dati di proprietà, nonché i dati di terze parti pubblici.
{: shortdesc}

Questa è l'architettura di una soluzione del servizio {{site.data.keyword.discoveryshort}} completa:

![Diagramma architettura di Discovery](images/discovery-flow.png)

Con {{site.data.keyword.discoveryshort}}, ci vogliono solo pochi passi per preparare i tuoi dati non strutturati, creare una query che punterà alle informazioni di cui hai bisogno e poi integrare quelle informazioni approfondite nella tua nuova applicazione o nella soluzione esistente.

Come funziona {{site.data.keyword.discoveryshort}}? Utilizza l'analisi dei dati combinata con l'intuizione cognitiva per ricevere i tuoi dati non strutturati e arricchirli in modo da poter rilevare le informazioni di cui hai bisogno.

{{site.data.keyword.discoveryfull}} riunisce un insieme funzionalmente ricco di API {{site.data.keyword.watson}} integrate e automatizzate per:

- Ricercare per l'indicizzazione, convertire, arricchire e normalizzare i dati.
- Esplorare in modo sicuro il contenuto di tua proprietà nonché il contenuto pubblico gratuito e su licenza.
- Applicare ulteriori arricchimenti come i concetti, le relazioni e il parere tramite {{site.data.keyword.nlushort}} (NLU).
- Semplificare lo sviluppo mentre si fornisce ancora l'accesso diretto alle API.

Per informazioni sul supporto lingua, consulta [Supporto linguistico {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-language-support#language-support).

Per informazioni sulla sicurezza di {{site.data.keyword.Bluemix_notm}}, vedi la [Descrizione del servizio {{site.data.keyword.Bluemix_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=%28IBM+Cloud+Service+description%29){: new_window}

{{site.data.keyword.discoveryfull}} Knowledge Graph è una funzione beta che fornisce nuovi endpoint per l'esecuzione di query di entità e relazioni sui documenti. Ciò include le ricerche basate sul contesto e la classificazione della pertinenza. Per informazioni, vedi [{{site.data.keyword.discoveryfull}} Knowledge Graph](/docs/services/discovery?topic=discovery-kg#kg).

## Supporto browser e prerequisiti
{: #browser-support-and-prerequisites}

Per l'elenco dei browser supportati e dei prerequisiti {{site.data.keyword.Bluemix}}, consulta [Prerequisiti ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/docs/overview/prereqs.html#prereqs){: new_window}.

## Watson Discovery News
{: #wds}

{{site.data.keyword.discoverynewsshort}}, un insieme di dati pubblico che è stato pre-arricchito con analisi approfondite cognitive, è anche incluso con {{site.data.keyword.discoveryshort}}. Puoi utilizzare questo insieme di dati non strutturato e pubblico per eseguire la query di informazioni approfondite che puoi integrare nelle tue applicazioni. Per ulteriori informazioni, consulta [Watson Discovery News](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news). Vedi una demo di quello che puoi creare con {{site.data.keyword.discoverynewsshort}} [qui![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://discovery-news-demo.ng.bluemix.net/){: new_window}.

Il servizio{{site.data.keyword.discoveryshort}} è disponibile su [{{site.data.keyword.Bluemix_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/catalog/services/discovery){: new_window}

## Strumentazione Discovery
{: #discovery-tooling}

Il servizio {{site.data.keyword.discoveryshort}} include una serie completa di strumenti online - la strumentazione {{site.data.keyword.discoveryshort}} - per aiutarti a configurare velocemente un'istanza del servizio e popolarla con i dati.

La strumentazione del servizio {{site.data.keyword.discoveryshort}} è stata progettata per risparmiare del tempo eliminando il bisogno di utilizzare le API per configurare e popolare il tuo servizio. Questo consente ai tuoi sviluppatori delle applicazioni di concentrarsi sulla creazione di modalità di elevato valore disponibili agli utenti finali per sperimentare il servizio {{site.data.keyword.discoveryshort}}. Consulta [Introduzione alla strumentazione](/docs/services/discovery?topic=discovery-getting-started#getting-started) per un'introduzione alla strumentazione {{site.data.keyword.discoveryshort}}.


## Passi successivi
{: #next-steps}

- Inizia a lavorare con la strumentazione {{site.data.keyword.discoveryshort}} o l'API {{site.data.keyword.discoveryshort}}:
    - [Introduzione alla strumentazione {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-getting-started#getting-started)
    - [Introduzione all'API {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-gs-api#gs-api)
- Il servizio {{site.data.keyword.discoveryshort}} supporta un certo numero di SDK per semplificare lo sviluppo delle applicazioni. Gli SDK sono disponibili per molti linguaggi di programmazione e piattaforme popolari, tra cui Node.js, Java e Python. Tutti gli SDK sono disponibili dallo spazio dei nomi [watson-developer-cloud ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/watson-developer-cloud){: new_window} su GitHub.
    - Per un elenco completo degli SDK e per informazioni sul loro utilizzo, consulta [SDK {{site.data.keyword.watson}}](https://cloud.ibm.com/docs/services/watson/getting-started-sdks.html#sdks).
    - Per informazioni dettagliate su tutti i metodi degli SDK Node, Java e Python, consulta il [Riferimento API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery){: new_window}.
