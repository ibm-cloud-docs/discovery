---

copyright:
  years: 2015, 2018
lastupdated: "2018-01-16"

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

# Migrazione da Watson Discovery News Original
{: #migrate-bwdn}

Una nuova versione di {{site.data.keyword.discoverynewsshort}} è stata presentata il 31 luglio 2017**. La versione originale è stata ridenominata {{site.data.keyword.discoverynewsshort}} Original ed è stata ritirata dal servizio il **15 gennaio 2018**. Se tenti di accedere a {{site.data.keyword.discoverynewsshort}} Original, riceverai il messaggio `410 GONE`.
{: shortdesc}

Per la migrazione da {{site.data.keyword.discoverynewsshort}} Original alla nuova versione, devi apportare alcune modifiche, incluso l'aggiornamento di tutte le query create per {{site.data.keyword.discoverynewsshort}} Original.

  **Nota:** {{site.data.keyword.discoverynewsshort}} Original era disponibile solo nelle istanze di {{site.data.keyword.discoveryshort}} create prima del **31 luglio 2017** ed è stato ritirato dal servizio il **15 gennaio 2018**.

Per una descrizione su questa raccolta, consulta [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html). 

Per una descrizione e per le informazioni sull'esecuzione di query di {{site.data.keyword.discoverynewsshort}} Original, consulta [Watson Discovery News Original](/docs/services/discovery/discovery-auxiliary.html#watson-discovery-news-original).

## Confronto tra i servizi

| {{site.data.keyword.discoverynewsshort}} Original         | {{site.data.keyword.discoverynewsshort}}           |
|----------------------------------------|---------------------------------|
| **{{site.data.keyword.discoverynewsshort}} Original** è stato pre-arricchito con i seguenti arricchimenti del linguaggio Alchemy: Keyword Extraction, Entity Extraction, Concept Tagging, Relation Extraction, Sentiment Analysis e Taxonomy Classification. Sono stati aggiunti anche i seguenti ulteriori metadati: data di indicizzazione, data di pubblicazione, classificazione dell'URL, classificazione dell'host e il testo dell'aggancio.     | **{{site.data.keyword.discoverynewsshort}}** viene pre-arricchito con i seguenti arricchimenti {{site.data.keyword.nlushort}} (NLU): Keyword Extraction, Entity Extraction, Semantic Role Extraction, Sentiment Analysis, Relations e Category Classification. Vengono aggiunti anche i seguenti ulteriori metadati: data di indicizzazione e data di pubblicazione. Per ulteriori informazioni sugli arricchimenti NLU, consulta [Aggiunta degli arricchimenti](/docs/services/discovery/building.html#adding-enrichments).                         |
| **{{site.data.keyword.discoverynewsshort}} Original** era accessibile tramite un ambiente che era univoco per la tua istanza del servizio.                       | Quando utilizzi **{{site.data.keyword.discoverynewsshort}}**, tutti gli utenti eseguono le query dello stesso ambiente e della stessa raccolta. Questo significa che tutti i riferimenti al tuo ambiente e alla tua raccolta devono essere modificati.      |
| In **{{site.data.keyword.discoverynewsshort}} Original**, durante il richiamo dell'ambiente tramite l'API hai ricevuto informazioni come la dimensione della raccolta, il numero di documenti, ecc.  | L'API **{{site.data.keyword.discoverynewsshort}}** non restituisce queste informazioni.                          |

I seguenti nuovi campi sono disponibili in **{{site.data.keyword.discoverynewsshort}}**:

`enriched_text.relations.arguments.text`  
`enriched_text.relations.score`  
`enriched_text.relations.sentence`  
`enriched_text.relations.type`  
`enriched_title.relations`  
`enriched_title.relations.arguments`  
`enriched_title.relations.arguments.entities`<br/>
`enriched_title.relations.arguments.entities.text`  
`enriched_title.relations.arguments.entities.type`  
`enriched_title.relations.arguments.text`  
`enriched_title.relations.score`  
`enriched_title.relations.sentence`  
`enriched_title.relations.type`  
`external_links`  
`extracted_metadata`  
`extracted_metadata.file_type`  
`extracted_metadata.filename`  
`extracted_metadata.sha1`  
`forum_title`  
`main_image_url`

Molti campi sono stati rimossi come ad esempio `blekko.hostrank`, `duplicate_url`, `domain` e altro. Per un elenco completo, vedi <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/News_migration_v_1.01.xlsx" download>QUI <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno" class="style-scope doc-content"></a>.

## Spostamento delle query al nuovo Watson Discovery News

Per spostare le tue query da {{site.data.keyword.discoverynewsshort}} Original al nuovo {{site.data.keyword.discoverynewsshort}}, devi modificare tutte le query esistenti nei seguenti modi:  

- Modifica l'ID ambiente che sta venendo chiamato dalla query. I nuovi nomi dell'ambiente sono stati standardizzati tra tutte le istanze del servizio {{site.data.keyword.discoveryshort}} con:

  `system`  

- Modifica l'ID raccolta che sta venendo chiamato dalla query. I nuovi nomi della raccolta sono stati standardizzati tra tutte le istanze del servizio {{site.data.keyword.discoveryshort}} con:

  ` news                      `

- Modifica la query per utilizzare la nuova struttura del percorso JSON per il nuovo {{site.data.keyword.discoverynewsshort}}. La maggior parte dei campi hanno i percorsi modificati, sono stati aggiunti più campi e un gruppo selezionato di campi di poco valore è stato rimosso. Per i dettagli completi, consulta il foglio di calcolo della migrazione <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/News_migration_v_1.01.xlsx" download>QUI <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno" class="style-scope doc-content"></a>). Ad esempio la seguente query:

  `discovery/api/v1/environments/ae5790c2-592f-432a-804a-ee16de7154d7/collections/3edcd8f1-e25a-4f44-a069-58332ad17651/query?version=2017-11-07&query=entities.type:"Company"`

  Dovrebbe essere modificata in:

  `discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.type:"Company"`  

## Query di Watson Discovery News

Puoi eseguire query di {{site.data.keyword.discoverynewsshort}} utilizzando l'API o uno degli SDK {{site.data.keyword.watson}}. Inoltre, puoi utilizzare la strumentazione di creazione della query per creare le query in modo interattivo.

**Per avviare la strumentazione {{site.data.keyword.discoveryshort}} e la query di {{site.data.keyword.discoverynewsshort}}:**

1. Fai clic su **Launch Tool** per {{site.data.keyword.discoveryshort}} in **Services**.
1. Fai clic sul tile {{site.data.keyword.discoverynewsshort}} per aprire la schermata **Manage data**.
1. Fai clic su **View data schema** e quindi su **Build queries** per aprire il builder di query.

  Le query in {{site.data.keyword.discoverynewsshort}} sono strutturate allo stesso modo delle query scritte per le raccolte di dati private. Consulta [Concetti delle query](/docs/services/discovery/using.html) e [Guida di riferimento per le query](/docs/services/discovery/query-reference.html).
  {: tip}

**Nota:** non aspettarti che vengano restituiti risultati identici per query simili in {{site.data.keyword.discoverynewsshort}} Original e {{site.data.keyword.discoverynewsshort}}. Il tempo di indicizzazione, le origini e gli arricchimenti forniscono tutti risultati diversi.

## Aggiunta di query Watson Discovery News alla tua applicazione

Utilizza uno dei seguenti metodi per aggiungere le query alla tua applicazione. Tutti questi esempi eseguono la query di `enriched_text.entities` con un valore `text` di `IBM` (`enriched_text.entities.text:IBM`).

In tutti i seguenti esempi, sostituisci `{username}` e `{password}` con il nome utente e la password elencati nella pagina **Service Credentials** della tua istanza del servizio.

### Utilizzo di chiamate dirette all'API

```bash
curl -u "{username}":"{password}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

### Utilizzo dell'SDK Watson Java

```java
Discovery discovery = new Discovery("2017-11-07");  
discovery.setEndPoint("https://gateway.watsonplatform.net/discovery/api/v1");
discovery.setUsernameAndPassword("{username}", "{password}");  
String environmentId = "system";
String collectionId = "news";

QueryRequest.Builder queryBuilder = new QueryRequest.Builder(environmentId, collectionId);  
queryBuilder.query("enriched_text.entities.text:IBM");  
QueryResponse queryResponse = discovery.query(queryBuilder.build()).execute();
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
        }
);
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
my_query = discovery.query('system', 'news', qopts)  
print(json.dumps(my_query, indent=2))  
```
{: codeblock}
