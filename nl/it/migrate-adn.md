---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-08"

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

# Migrazione da AlchemyData News
{: #migrate-adn}

Una nuova versione di {{site.data.keyword.discoverynewsfull}} è stata presentata il 31 luglio 2017**. Per una descrizione su questa raccolta, consulta [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html). 

AlchemyData News è stato ritirato e la data di rimozione del servizio è il **7 marzo 2018**

## Confronto tra i servizi
{: shortdesc}

Le seguenti differenze sono degne di nota quando si passa da AlchemyData News a {{site.data.keyword.discoverynewsshort}} nel servizio {{site.data.keyword.discoveryshort}}.

- {{site.data.keyword.discoveryshort}} addebita le nuove query solo in base alla query. Tutti i campi sono disponibili per la restituzione con ogni risultato senza alcun costo aggiuntivo.
- Ogni query {{site.data.keyword.discoveryshort}} può restituire fino a un massimo di 50 risultati. È disponibile un parametro `offset` in modo che puoi creare le query per qualsiasi numero di risultati di cui hai bisogno.
- {{site.data.keyword.discoveryshort}} supporta anche le aggregazioni. Per ulteriori informazioni, consulta la sezione [aggregazioni](/docs/services/discovery/query-reference.html#aggregations) della documentazione di {{site.data.keyword.discoveryshort}}.
- {{site.data.keyword.discoverynewsfull}} non esegue la classificazione nello stesso modo di AlchemyData. Al momento non esiste un campo per la classificazione.
- La struttura della query e la struttura dei dati restituiti è diversa tra {{site.data.keyword.discoverynewsshort}} e AlchemyData News. Un buon modo per comprendere la struttura JSON è quello di eseguire la query di un solo risultato in {{site.data.keyword.discoverynewsshort}} e controllarlo.
- {{site.data.keyword.discoverynewsshort}} non supporta l'output XML.
- La deduplicazione è una funzione beta in {{site.data.keyword.discoverynewsshort}}.

## Differenze di autenticazione

Il servizio {{site.data.keyword.discoveryshort}} utilizza le credenziali standard {{site.data.keyword.Bluemix_notm}} `username` e `password` per accedere alle query. Ciò sostituisce il metodo della chiave API esistente utilizzato da AlchemyData News. Tutte le query {{site.data.keyword.discoveryshort}} devono essere effettuate con una combinazione di nome utente e password creata dall'istanza del servizio {{site.data.keyword.discoveryshort}}.

Le tue credenziali del servizio possono essere gestite visualizzando la scheda **Credenziali del servizio** del tuo servizio in {{site.data.keyword.Bluemix_notm}}.

## Configurazione di un'istanza di Discovery

Un'istanza del servizio {{site.data.keyword.discoveryshort}} viene creata nello stesso modo con cui hai creato la tua istanza di AlchemyData News.

1. Vai a [{{site.data.keyword.Bluemix_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window}, accedi e seleziona {{site.data.keyword.discoveryshort}} dal catalogo dei servizi.
1. Seleziona il piano appropriato ai tuoi bisogni e fai clic su **Crea**.

  Il servizio {{site.data.keyword.discoveryshort}} offre un piano Lite con 1000 nuove query disponibili al mese. Puoi utilizzare un'istanza di questo piano per identificare query equivalenti senza doverle pagare.
  {: tip}

1. Fai clic sulla scheda **Service Credentials** e seleziona **View Credentials** per identificare `url`, `username` e `password` per questa istanza.

## Query di Watson Discovery News

Puoi eseguire query di {{site.data.keyword.discoverynewsfull}} utilizzando l'API o uno degli SDK {{site.data.keyword.watson}}. Inoltre, puoi utilizzare la strumentazione di creazione della query per creare le query in modo interattivo.

Per avviare la strumentazione {{site.data.keyword.discoveryshort}} e la query di {{site.data.keyword.discoverynewsshort}}:

1. Fai clic su **Launch Tool** per {{site.data.keyword.discoveryshort}} in **Services**.
1. Fai clic sul tile {{site.data.keyword.discoverynewsshort}} per aprire la schermata **Manage data**.
1. Fai clic su **View data schema** e quindi su **Build queries** per aprire il builder di query.

  Le query in {{site.data.keyword.discoverynewsfull}} sono strutturate allo stesso modo delle query scritte per le raccolte di dati private. Consulta [Concetti delle query](/docs/services/discovery/using.html) e [Guida di riferimento per le query](/docs/services/discovery/query-reference.html).
  {: tip}

**Nota**: non aspettarti che vengano restituiti risultati identici per query simili in AlchemyData News e {{site.data.keyword.discoverynewsfull}}. Il tempo di indicizzazione, le origini e gli arricchimenti forniscono tutti risultati diversi.

## Aggiunta di query Watson Discovery News alla tua applicazione

Utilizza uno dei seguenti metodi per aggiungere le query alla tua applicazione. Tutti questi esempi eseguono la query di `enriched_text.entities` con un valore `text` di `IBM` (`enriched_text.entities.text:IBM`).

In tutti i seguenti esempi, sostituisci `{username}` e `{password}` con il nome utente e la password elencati nella pagina **Service Credentials** della tua istanza del servizio.

### Utilizzo di chiamate dirette all'API

```bash
curl -u "{username}":"{password}"  'https://gateway.watsonplatform.net/discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

### Utilizzo dell'SDK Java

```java
Discovery discovery = new Discovery("2017-11-07");
discovery.setEndPoint("https://gateway.watsonplatform.net/discovery/api/v1");
discovery.setUsernameAndPassword("{username}", "{password}");  
String environmentId = "system";
  String collectionId = "news";

QueryRequest.Builder queryBuilder = new QueryRequest.Builder(environmentId,collectionId);  
queryBuilder.query("enriched_text.entities.text:IBM");  
QueryResponse queryResponse =  
discovery.query(queryBuilder.build()).execute();
```
{: codeblock}

### Utilizzo dell'SDK Watson Node.js

```javascript
var watson = require('watson-developer-cloud');

var discovery = new DiscoveryV1({  
  username: '{username}',  
  password: '{password}',  
  version_date: '2017-11-07'  
});  

discovery.query(('system', 'news', 'enriched_text.entities.text:IBM'),  
  function(error, data) {  
  console.log(JSON.stringify(data, null, 2));  
```
{: codeblock}

### Utilizzo dell'SDK Watson Python

```python
import sys
      import os
      import json
      from watson_developer_cloud import DiscoveryV1

discovery = DiscoveryV1(
  username="{username}",
  password="{password}",
  version="2017-11-07"
)

qopts = {'query': 'enriched_text.entities.text:IBM'}
my_query = discovery.query('{environment_id}', '{collection_id}', qopts)
print(json.dumps(my_query, indent=2))
```
{: codeblock}
