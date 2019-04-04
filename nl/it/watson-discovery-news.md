---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-05"

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

# Watson Discovery News
{: #watson-discovery-news}

{{site.data.keyword.discoverynewsfull}} è incluso con {{site.data.keyword.discoveryshort}}. {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} è un insieme di dati indicizzato pre-arricchito con le seguenti analisi approfondite cognitive: **Keyword Extraction**, **Entity Extraction**, **Semantic Role Extraction**, **Sentiment Analysis**, **Relation Extraction** e **Category Classification**. (Per ulteriori informazioni sugli arricchimenti, vedi [Aggiunta di arricchimenti](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)). Vengono aggiunti anche i seguenti metadati aggiuntivi: data di ricerca per l'indicizzazione e data di pubblicazione. La ricerca cronologica è disponibile per gli ultimi 60 giorni di dati di notizie. Vedi una demo di quello che puoi creare con {{site.data.keyword.discoverynewsfull}} [qui![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://discovery-news-demo.ng.bluemix.net/){: new_window}.

{{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} viene aggiornato continuamente con nuovi articoli ed è disponibile in inglese, spagnolo, tedesco, coreano e giapponese. {{site.data.keyword.discoverynewsshort}} in inglese viene aggiornato con circa 300.000 nuovi articoli al giorno. {{site.data.keyword.discoverynewsshort}} in spagnolo viene aggiornato con circa 60.000 nuovi articoli ogni giorno; {{site.data.keyword.discoverynewsshort}} in tedesco viene aggiornato con circa 15.000 nuovi articoli ogni giorno; {{site.data.keyword.discoverynewsshort}} in coreano viene aggiornato con 10.000 nuovi articoli ogni giorno. {{site.data.keyword.discoverynewsshort}} in giapponese viene aggiornato con circa 17.000 nuovi articoli ogni giorno. Le fonti di notizie variano in base alla lingua; pertanto, i risultati della query per ciascuna risorsa non saranno identici.

Casi d'uso per {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}}:

- Avvisi relativi alle notizie - crea dei nuovi avvisi avvalendoti del supporto per entità, parole chiave, categorie e analisi dei pareri per ricevere segnalazioni relative sia alle notizie che al modo in cui vengono percepite.

- Rilevamento degli eventi - l'estrazione dei ruoli semantici soggetto/azione/oggetto controlla termini/azioni quali "acquisizione", "risultati dell'elezione" o "IPO".

- Argomenti di tendenza nelle notizie - identifica gli argomenti popolari e monitora gli aumenti e le diminuzioni nella frequenza con cui tali argomenti (o gli argomenti correlati) vengono menzionati.

Per informazioni sulla scrittura di query per {{site.data.keyword.discoverynewsfull}}, vedi:
- [Query di Watson Discovery News](/docs/services/discovery?topic=discovery-query-concepts#querying-news)
- [Concetti delle query](/docs/services/discovery?topic=discovery-query-concepts)
- [Guida di riferimento per le query](/docs/services/discovery?topic=discovery-query-reference#query-reference).

Non puoi regolare la configurazione di {{site.data.keyword.discoverynewsfull}}, formare o aggiungere documenti alla raccolta {{site.data.keyword.discoverynewsfull}}.

Le query {{site.data.keyword.discoverynewsfull}} visualizzano circa 50 parole da ciascun articolo nel campo JSON `text`. Queste parole vengono estratte dagli highlight (punti salienti). Vedi [highlight](/docs/services/discovery?topic=discovery-query-parameters#highlight) per una spiegazione degli highlight (punti salienti). Gli highlight non devono necessariamente essere inclusi esplicitamente nella tua query per abilitare questa modalità di funzionamento.

Il numero massimo di risultati restituiti per una query {{site.data.keyword.discoverynewsfull}} è `50`. Utilizza query aggiuntive e il parametro `offset` per restituire più di `50` risultati.

**Nota:** questa versione di {{site.data.keyword.discoverynewsfull}} è stata presentata il **31 luglio 2017**. {{site.data.keyword.discoverynewsfull}} Original è stato ritirato dal servizio il **15 gennaio 2018**. Per informazioni sulla migrazione, vedi [Migrazione da Watson Discovery News Original](/docs/services/discovery?topic=discovery-migrate-bwdn#migrate-bwdn).
