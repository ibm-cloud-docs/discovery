---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-03"

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


# Migrazione da Watson Document Conversion e Retrieve and Rank

{{site.data.keyword.documentconversionfull}} e {{site.data.keyword.retrieveandrankfull}} sono obsoleti e sono stati sostituiti da {{site.data.keyword.discoveryfull}}. Normalmente, questi due servizi sono utilizzati insieme per inserire, classificare e distribuire i risultati alle tue applicazioni. Questo documento viene fornito come guida nel processo di migrazione da {{site.data.keyword.documentconversionshort}} e {{site.data.keyword.retrieveandrankshort}} a {{site.data.keyword.discoveryshort}}.

{{site.data.keyword.discoveryfull}} fornisce un'interfaccia di query più robusta, l'inserimento dei dati semplificato, la gestione della formazione migliorata e il ridimensionamento aumentato. {{site.data.keyword.discoveryshort}} risolve molti degli stessi casi di utilizzo principali di {{site.data.keyword.retrieveandrankshort}} tra cui l'assistenza dell'agent di supporto, la ricerca della knowledge base organizzativa e l'assistenza alla ricerca. È stato creato tenendo conto di molte delle difficoltà affrontate dagli utenti di {{site.data.keyword.retrieveandrankshort}} e risolve molti di questi problemi. {{site.data.keyword.discoveryshort}} fornisce inoltre nuove funzionalità per il richiamo delle informazioni non disponibili in {{site.data.keyword.retrieveandrankshort}} incluso il richiamo dei passaggi e gli algoritmi di ricerca migliorati per trovare risultati più pertinenti.

**Confronto delle funzioni**

| Funzione | {{site.data.keyword.retrieveandrankshort}} | {{site.data.keyword.discoveryshort}} |
|:-------------|:--------------------:|:-------------:|
| Ricerca in linguaggio naturale | Sì | Sì |
| Formazione della pertinenza del machine learning | Sì | Sì |
| Strumentazione dell'IU per la formazione | Sì | Sì |
| Input dell'unità di risposta JSON | Sì | Sì |
| Suddivisione del documento | Sì | Sì |
| Richiamo dei passaggi |   | Sì |
| CRUD del documento | Sì | Sì |
| Caricamento del JSON batch | Sì |   |
| Arricchimento NLP del documento automatico |   | Sì |
| Integrazione del modello NLP personalizzato per l'arricchimento |   | Sì |
| Formazione dei dati archiviati nel servizio |   | Sì |
| Gestione del ciclo di vita del modello automatizzata |   | Sì |
| Somiglianza semantica per migliorare la pertinenza senza la formazione |   | Sì |
| Misurazione dell'accuratezza nella strumentazione basata sulla serie di test | Sì |   |
| Supporto del vettore della funzione personalizzato | Sì |   |
| Configurazione dell'analizzatore personalizzata | Sì | Preconfigurato |
| Parole non significative personalizzate | Sì | Preconfigurato |
| Dizionari linguistici personalizzati | Sì | Preconfigurato |
| Sinonimi personalizzati | Sì | Sì |
**Nota:** questa tabella verrà aggiornata come vengono aggiunte nuove funzionalità {{site.data.keyword.discoveryshort}}.

Prima di iniziare l'azione di migrazione, devi prima [valutare](#evaluate) i dati archiviati nel tuo servizio {{site.data.keyword.retrieveandrankshort}} e capire come sposterai i diversi componenti che formano la tua soluzione corrente.

La maggior parte dei clienti utilizza {{site.data.keyword.documentconversionshort}} insieme a {{site.data.keyword.retrieveandrankshort}}. Se non stai utilizzando {{site.data.keyword.documentconversionshort}} per convertire il contenuto in modo che possa essere archiviato in un indice ricercabile, procedi al controllo delle [opzioni per la migrazione di {{site.data.keyword.documentconversionshort}} autonomo](#dcs).

Se in origine hai utilizzato l'esercitazione {{site.data.keyword.retrieveandrankshort}} e basato la tua istanza del servizio su tale esercitazione, un'estensione dell'esercitazione che inserisce gli stessi dati in {{site.data.keyword.discoveryshort}} può essere trovata [qui](/docs/services/discovery/migrate-rnr-tut.html).

**Nota:** la funzionalità di conversione e di arricchimento è inclusa con {{site.data.keyword.discoveryshort}}. Se hai utilizzato {{site.data.keyword.documentconversionshort}} e/o {{site.data.keyword.nlushort}} per convertire e arricchire i documenti HTML, PDF o Microsoft Word di origine; questi servizi vengono sostituiti dalle funzioni all'interno del servizio {{site.data.keyword.discoveryshort}}.

## Valuta il tuo percorso di migrazione al servizio Watson Discovery
{: #evaluate}

Esistono due opzioni pratiche per la migrazione da {{site.data.keyword.retrieveandrankshort}}: migrazione dal contenuto di origine e migrazione dal contenuto indicizzato. Valuta entrambe le opzioni prima di decidere quale utilizzare.

### Migrazione dal contenuto di origine
{: #source}

Per poter eseguire la migrazione dal contenuto di origine dovrai:

-  avere accesso ai file di origine iniziali da cui è stato inserito il contenuto.
-  estrarre in modo programmatico l'ID di ogni documento (il risultato dispone già di un ID prima che venga indicizzato)

Se puoi soddisfare tutti i criteri di migrazione, ti consigliamo di utilizzare questo metodo per passare al servizio {{site.data.keyword.discoveryshort}}.

Per migrare il tuo contenuto di origine, modifica la procedura descritta nell'[esercitazione di migrazione](/docs/services/discovery/migrate-rnr-tut.html) per soddisfare le specifiche dei tuoi dati di origine.

#### Migrazione delle unità di risposta

Se hai creato delle unità di risposta utilizzando {{site.data.keyword.documentconversionshort}} scegli una delle seguenti opzioni per migrare tale contenuto:

-  se hai formato un classificatore e devi migrare la classificazione, devi prendere il contenuto restituito da {{site.data.keyword.documentconversionshort}} e inserirlo in {{site.data.keyword.discoveryshort}}
-  se non hai dati di formazione da migrare, inserisci i documenti di origine iniziali in {{site.data.keyword.discoveryshort}} utilizzando la [funzione di suddivisione del documento](/docs/services/discovery/building.html#doc-segmentation)

### Migrazione dal contenuto indicizzato
{: #indexed}

Devi eseguire la migrazione dal contenuto indicizzato in {{site.data.keyword.retrieveandrankshort}} se non hai accesso ai documenti di origine iniziali oppure se:

- hai utilizzato la generazione dell'ID documento automatica e hai formato un classificatore.
- hai creato e classificato delle unità di risposta in {{site.data.keyword.documentconversionshort}} ma non hai conservato le unità di risposta che sono state generate dal servizio {{site.data.keyword.documentconversionshort}}.

**Nota:** questo metodo è possibile solo se tutto il contenuto necessario si trova nei campi archiviati in {{site.data.keyword.retrieveandrankshort}}. Se il contenuto è stato solo indicizzato ma non archiviato, non sarà possibile eseguire la query del contenuto al di fuori del servizio e i dati dovranno essere convertiti e separati nuovamente dall'origine.

I documenti vengono estratti dal servizio utilizzando il metodo [/v1/solr_clusters/{solr_cluster_id}/solr/\{collection_name\}/select ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/watson/developercloud/retrieve-and-rank/api/v1/#index_doc){: new_window} utilizzando una query vuota `q=*:*`. Il numero di documenti restituiti potrebbe essere superiore al numero massimo possibile di restituzioni (`200` per la maggior parte delle raccolte). In questo caso, è necessario effettuare più chiamate con l'appropriato [paging ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://lucene.apache.org/solr/guide/6_6/pagination-of-results.html){: new_window} per raccogliere tutti i documenti.

I documenti con gli **ID** specificati vengono caricati sul servizio {{site.data.keyword.discoveryshort}} utilizzando il metodo [/v1/environments/\{environment_id\}/collections/\{collection_id\}/documents/\{document_id\} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#update-doc){: new_window}. Ogni caricamento di documento è una chiamata API separata.

## Migrazione dei dati di formazione

Dopo aver migrato i tuoi risultati, il passo successivo è quello di migrare i dati di formazione che sono stati creati per il contenuto. Esistono due opzioni per migrare i dati di formazione: migrazione dall'origine (`csv`) e migrazione dal servizio. Se hai caricato i dati di formazione da un file `csv` e hai ancora accesso a quel file, devi eseguire la migrazione dall'origine. Se hai utilizzato la strumentazione {{site.data.keyword.retrieveandrankshort}} o non hai accesso al file `csv` originale devi eseguire la migrazione dal servizio.

### Migrazione della formazione dal contenuto di origine
{: #csv}

Per poter eseguire la migrazione dal contenuto di origine della classificazione dovrai:

- avere accesso al file `csv` di origine iniziale con cui sono state caricate in origine le informazioni di formazione.
- assicurarti che gli ID dei documenti formati quando vengono indicizzati corrispondano agli ID dei documenti formati quando sono stati indicizzati in {{site.data.keyword.retrieveandrankshort}}.

Se puoi soddisfare tutti i criteri di migrazione, ti consigliamo di utilizzare questo metodo per passare la formazione al servizio {{site.data.keyword.discoveryshort}}.

Per migrare i tuoi dati di formazione, modifica la procedura descritta nell'[esercitazione di migrazione](/docs/services/discovery/migrate-rnr-tut.html) per soddisfare le specifiche dei tuoi dati di origine.

### Migrazione dei dati di formazione dal servizio
{: #extract-train}

Per migrare i dati di formazione dal servizio {{site.data.keyword.retrieveandrankshort}}, dovrai: estrarre i dati di formazione utilizzando le API {{site.data.keyword.retrieveandrankshort}}, convertire il JSON di formazione {{site.data.keyword.retrieveandrankshort}} in un formato utilizzabile da {{site.data.keyword.discoveryshort}} ed infine inserire i dati di formazione in {{site.data.keyword.discoveryshort}} utilizzando l'API.

Per estrarre i dati di formazione da {{site.data.keyword.retrieveandrankshort}}, utilizza la funzione `Export` all'interno della strumentazione {{site.data.keyword.retrieveandrankshort}}. Dopo aver scaricato correttamente un'esportazione completa, estrai il file `.zip` salvato. All'interno dell'archivio ci sono due file. I dati di formazione sono archiviati in quello denominato `export-questions.json`. Questo file contiene un array di oggetti di formazione JSON.

Ogni risultato di formazione nell'array viene presentato nel seguente formato:

**Esempio di dati di formazione di {{site.data.keyword.retrieveandrankshort}}**
```json
{
    "text":"Who was the first royal to attend Wimbledon?",
    "cluster":{
        "id":"f62c11d3-30fa-11e7-8a0c-333f7f431ce8",
        "answers":{
            "f62c11d3-30fa-11e7-8a0c-33":[
                {
                    "id":"dac41335-0e96-40c9-983f-cc3f1c395782",
                    "ranking":1,
                    "source":{
                        "id":"e26a3d20-30fa-11e7-aa5e-d1632b06e0b1",
                        "file":"wimbledon-wikipedia.html",
                        "sequence":17,
                        "strategy":"retrieve"
                    }
                },
                {
                    "id":"661b4c9f-ecdb-4dad-aafc-6ae561a148c0",
                    "ranking":2,
                    "source":{
                        "id":"da1bc620-30fa-11e7-8f90-3305f35a93c9",
                        "file":"generated-otherFactsFigures.docx",
                        "sequence":67,
                        "strategy":"retrieve"
                    }
                },
                {
                    "id":"0053fdb8-c77e-4fcf-b0e0-6a4cd377266a",
                    "ranking":3,
                    "source":{
                        "id":"d9c0add0-30fa-11e7-aa5e-d1632b06e0b1",
                        "file":"generated-allEngland.docx",
                        "sequence":20,
                        "strategy":"retrieve"
                    }
                },
                {
                    "id":"506d3d50-19ed-49c8-b32f-65f848e60e86",
                    "ranking":4,
                    "source":{
                        "id":"da1bc620-30fa-11e7-8f90-3305f35a93c9",
                        "file":"generated-otherFactsFigures.docx",
                        "sequence":63,
                        "strategy":"retrieve"
                    }
                }
            ]
        },
        "flags":{

        }
    }
},
```
{: codeblock}

{{site.data.keyword.discoveryshort}} non ha bisogno di tutte le informazioni che vengono esportate da {{site.data.keyword.retrieveandrankshort}}. Il seguente frammento mostra la struttura richiesta di una voce di formazione {{site.data.keyword.discoveryshort}}.

```json
{
  "natural_language_query": "{natural_language_query}",
  "examples": [
    {
      "document_id": "{document_id_1}",
      "relevance": 0
    },
    {
      "document_id": "{document_id_2}",
      "relevance": 10
    }
  ]
}
```
{: codeblock}

A questo punto, dovrai convertire le tue informazioni di formazione {{site.data.keyword.retrieveandrankshort}} in informazioni di formazione {{site.data.keyword.discoveryshort}} . Tieni conto dei seguenti punti quando esegui la conversione.

- **Non pertinente** viene specificato da un punteggio di `relevance` di `0` in {{site.data.keyword.discoveryshort}}, ma è stato specificato da un `ranking` di `1` in {{site.data.keyword.retrieveandrankshort}} - tutte le voci `"ranking": 1` devono essere convertite con `"relevance": 0` in {{site.data.keyword.discoveryshort}}
- La strumentazione {{site.data.keyword.discoveryshort}} utilizza una scala binaria di `0` e `10`. Se vuoi classificare più risultati e utilizzare la strumentazione {{site.data.keyword.discoveryshort}}, devi convertire tutte le voci `"ranking": 1` e `"ranking": 2` con `"relevance": 0` e tutte le voci `"ranking": 3` e `"ranking": 4` con `"relevance": 10`. Questo non è necessario se non stai classificando ulteriori risultati o non stai utilizzando la strumentazione {{site.data.keyword.discoveryshort}}.
- Le domande senza risposta non sono richieste da {{site.data.keyword.discoveryshort}}, la verifica della validità della formazione della pertinenza viene eseguita manualmente.

![Classificazione del flusso di migrazione](images/migrate-ranking.png)

Ad esempio, il precedente **Esempio di dati di formazione {{site.data.keyword.retrieveandrankshort}}** sarà convertito in modo da essere utilizzato nella strumentazione {{site.data.keyword.discoveryshort}} nel seguente modo:

```json
{
  "natural_language_query": "Who was the first royal to attend Wimbledon?",
  "examples": [
    {
      "document_id": "e26a3d20-30fa-11e7-aa5e-d1632b06e0b1",
      "relevance": 0
    },
    {
      "document_id": "da1bc620-30fa-11e7-8f90-3305f35a93c9",
      "relevance": 0
    },
    {
      "document_id": "d9c0add0-30fa-11e7-aa5e-d1632b06e0b1",
      "relevance": 10
    },
    {
      "document_id": "da1bc620-30fa-11e7-8f90-3305f35a93c9",
      "relevance": 10
    }
  ]
}
```
{: codeblock}

## Supporto linguistico
{: #language}

Consulta la [tabella di supporto linguistico per {{site.data.keyword.discoveryshort}}](/docs/services/discovery/language-support.html). Le funzioni di {{site.data.keyword.retrieveandrankshort}} sono principalmente supportate dal supporto linguistico **Di base** {{site.data.keyword.discoveryshort}}.

## Migrazione delle query
{: #queries}

Il linguaggio di query {{site.data.keyword.discoveryfull}} è diverso dal linguaggio di query Solr utilizzato da {{site.data.keyword.retrieveandrankshort}}. Le query esistenti devono essere reinstradate a uno dei metodi di query {{site.data.keyword.discoveryfull}} e convertite per utilizzare il linguaggio di query {{site.data.keyword.discoveryfull}}. La seguente tabella descrive alcuni degli operatori tipici che vengono utilizzati nella maggior parte delle query:

**Migrazione dalla query Solr a {{site.data.keyword.discoveryshort}} - Operatori tipici**

| Operatore Solr | Operatore Discovery | Descrizione |
|:-------------:|--------------------|-------------|
| `.` | `.` | Delimitatore JSON |
| `:` | `:` | Include |
|  | `::` | Corrispondenza esatta |
| `-{fieldname}:` | `:!` | Non include |
|  | `::!` | Non è una corrispondenza esatta |
| ``\` | ``\` | Carattere di escape |
| `""` | `""` | Query di frasi |
| `()` | `()`, `[]` | Raggruppamento nidificato |
| `OR` | [<code>&#124;</code>] | o |
| `AND` | [,] | e |
| `[* TO 100]` | `<=`, `>=`, `>`, `<` | Confronti numerici |
| `^x` | `^x` | Moltiplicatore del punteggio |
| `*` | `*` | Carattere jolly |
| `~`(da 0 a 1) | [~n] | Variazione di stringa |

Consulta la documentazione [Concetti delle query](/docs/services/discovery/using.html) e [Guida di riferimento per le query](/docs/services/discovery/query-reference.html) per informazioni dettagliate sul linguaggio di query {{site.data.keyword.discoveryfull}}.


## Migrazione del servizio Watson Document Conversion autonomo
{: #dcs}

Se stai utilizzando {{site.data.keyword.documentconversionshort}} per inserire il contenuto in {{site.data.keyword.retrieveandrankshort}}, allora tale funzionalità si è evoluta in un unico servizio - {{site.data.keyword.discoveryshort}}. {{site.data.keyword.discoveryshort}} ti consente di convertire, arricchire e inserire i documenti Microsoft Word, PDF, HTML e JSON facilmente in un indice ricercabile e formabile. Questa sezione è importante se il tuo caso di utilizzo non implica l'archiviazione del contenuto convertito in un indice. Se stai inserendo i documenti in un indice, consulta [inserimento nel servizio {{site.data.keyword.discoveryshort}}](/docs/services/discovery/building.html).

IBM non fornisce più un servizio progettato per la conversione autonoma dei documenti Microsoft Word, PDF e HTML. Se al momento stai utilizzando il servizio {{site.data.keyword.documentconversionshort}} e non inserisci l'output in un servizio indicizzato online (come ad esempio {{site.data.keyword.discoveryshort}}), ti consigliamo di prendere in considerazione la migrazione a un open source alternativo come [Apache Tika ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://tika.apache.org/){: new_window}.
