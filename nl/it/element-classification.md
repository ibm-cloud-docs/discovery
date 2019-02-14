---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-23"

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

# Element Classification
{: #element-classification}

L'Element Classification rende possibile analizzare rapidamente i documenti di controllo per convertire, identificare e classificare gli elementi rilevanti. Con l'utilizzo di Natural Language Processing al top della tecnologia, vengono estratte la parte (a cui fa riferimento), la natura (tipo di elemento) e la categoria (classe specifica) dagli elementi di un documento.

L'Element Classification è progettata per fornire:

-  Natural Language Understanding of Contracts dei contratti con enfasi sui contratti di approvvigionamento software.
-  La capacità di convertire il PDF programmatico in JSON annotato
-  Identificazione di entità giuridiche e categorie che si allineano con le competenze in materia

L'Element Classification riunisce un insieme funzionalmente ricco di API Watson integrate e automatizzate per inserire un PDF programmatico per identificare sezioni, elenchi (numerati e puntati), note a piè di pagina e tabelle, convertendo questi elementi in un formato HTML strutturato. Inoltre, la classificazione di questo formato strutturato è annotata e prodotta come JSON con elementi, tipi e categorie etichettati. 

L'Element Classification trasmette in modo sicuro i tuoi dati eseguendo la crittografia dei dati in fase di elaborazione e mentre sono inattivi. Per informazioni sulla sicurezza di IBM Cloud, vedi la [Descrizione del servizio {{site.data.keyword.Bluemix_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=%28IBM+Cloud+Service+description%29){: new_window}

L'Element Classification restituisce un oggetto JSON che contiene:

-  Un oggetto `documents` che include il titolo, una versione HTML e l'hash MD5 del documento di input.
-  Le informazioni sul modello utilizzato per classificare il documento di input.  
-  Un array `elements` che descrive gli elementi semantici identificati nel documento di input.
-  Un array `tables` che suddivide le tabelle identificate nel documento di input.
-  Un oggetto `document_structure` che elenca i titoli delle sezioni e le frasi più importanti identificate nel documento di input.
-  Un array `parties` che elenca le parti, i ruoli, gli indirizzi e i contatti delle parti identificate nel documento di input.
-  Gli array che definiscono `effective_dates` e `contract_amounts`.

Questa funzione è attualmente supportata solo in inglese, consulta [Supporto per la lingua](/docs/services/discovery/language-support.html#feature-support) per i dettagli.


## Requisiti della classificazione
{: #element-class}

Per classificare i documenti utilizzando l'Element Classification, i tuoi documenti di origine e di configurazione devono soddisfare i seguenti requisiti:

-  I file da analizzare sono in formato PDF. 
-  I contenuti del PDF sono in formato testo. I documenti che sono stati scansionati non possono essere analizzati, anche se sono stati scansionati con il riconoscimento ottico dei caratteri.
   **Nota:** puoi identificare un PDF in formato testo aprendo il documento in un programma di visualizzazione PDF e utilizzando la strumentazione di **selezione testo** per selezionare una singola parola. Se non puoi selezionare una singola parola nel documento, il file non può essere analizzato. 
-  I file non hanno una dimensione superiore a 50 Mb. 
-  I PDF protetti (con una password per l'apertura) e i PDF con restrizioni di modifica (con una password per la modifica) non possono essere analizzati. 
-  La strumentazione {{site.data.keyword.discoveryshort}} include una configurazione denominata **Default Contract Configuration** che può essere utilizzata per arricchire la tua raccolta di documenti PDF. Hai anche l'opzione di creare una configurazione personalizzata che include l'arricchimento `elements`. Per i dettagli, consulta [Requisiti della raccolta](/docs/services/discovery/element-classification.html#element-collection).
-  I piani **Lite** possono elaborare un massimo di 500 pagine al mese.
-  Non disponibile negli ambienti **Dedicated**.
-  Impossibile eseguire la normalizzazione post-arricchimento quando utilizzi l'Element Classification.

**Nota:** il file **Default Contract Configuration** è stato aggiornato il 25 settembre 2018. Se hai applicato questa configurazione a una raccolta prima di questa data, consulta le [note sulla release](/docs/services/discovery/release-notes.html#25sept) per informazioni sull'aggiornamento della tua raccolta.

## Requisiti della raccolta
{: #element-collection}

Per utilizzare l'Element Classification, la raccolta deve essere configurata per soddisfare requisiti specifici:

La strumentazione {{site.data.keyword.discoveryshort}} include una configurazione denominata **Default Contract Configuration** che è stata preconfigurata per arricchire i documenti PDF con l'arricchimento **Element Classification** e altre opzioni obbligatorie. Puoi scegliere questa configurazione quando crei la tua raccolta. Il JSON per questa configurazione è:

```json
 {
   "name": "Default Contract Configuration",
   "description": "Extract party, nature, and category from elements in PDFs.",
  "conversions": {
     "html": {
       "exclude_tags_completely": [],
       "exclude_tags_keep_content": []
     }
   },
   "enrichments": [
     {
       "source_field": "html",
       "destination_field": "enriched_html_elements",
       "enrichment": "elements",
       "options": {
         "model": "contract"
    }
     }
   ]
 }
```
{: codeblock}

Se desideri creare un file di configurazione personalizzato, configura la tua raccolta in modo da soddisfare i seguenti requisiti:  

-  Le impostazioni di conversione `PDF` vengono ignorate se specificato.
-  Le impostazioni di conversione `WORD` possono essere omesse perché i file Microsoft Word non possono essere inseriti quando viene specificata l'Element Classification.
-  Le impostazioni di normalizzazione `html` vengono ignorate se specificato.
-  La segmentazione del documento non è supportata quando viene specificato l'arricchimento `elements`.
-  Nella configurazione {{site.data.keyword.discoveryshort}}, il campo `html` deve essere arricchito dall'arricchimento `elements` e `model` specificato come `contract`. Nel seguente esempio, `destination_field` è `enriched_html`, ma può essere utilizzato qualsiasi nome valido:

```json
 "enrichments": [
  {
     "source_field": "html",
     "destination_field": "enriched_html",
     "enrichment": "elements",
     "options": {
       "model": "contract"
    }
   }
 ]
```
{: codeblock}

Dopo aver selezionato `Default Contract Configuration` nella strumentazione, puoi caricare i tuoi documenti. Se non hai familiarità con la creazione di raccolte e sul caricamento dei documenti, consulta l'[Introduzione alla strumentazione](/docs/services/discovery/getting-started-tool.html).

## Elementi classificati

Una volta che un documento è stato indicizzato con l'Element Classification, verrà restituito con un array `elements` come parte del documento ricercabile.

Ogni oggetto presente nell'array `elements` descrive un elemento del contratto che {{site.data.keyword.discoveryshort}} ha identificato. Il seguente codice rappresenta un elemento tipico:

```json
 {
    "location" : {
     "begin" : 134323,
     "end" : 135109
    },
    "text" : "9. In the event that the Participant's total vested account balance is determined to be less than or equal to $2,000.00 as of the date that the Order is received, the parties will be informed in writing that the QDRO determination fee may potentially liquidate the account.",
    "types" : [ {
      "label" : {
        "nature" : "Obligation",
        "party" : "All Parties"
      },
      "provenance_ids" : ["Nlu0ogWAEGms4vjhhzpMv3iXhm8b8fBqMBNtT/bXH8JI=", "PlyERkjg5is36RpFjVUFXp69eDmGmCxLCXRs1sDMDUCo="
      ]
    } ],
    "categories" : [ {
      "label" : "Communication",
      "provenance_ids" : [ "Cs38YyU6VBFtJK1/bgtEJBlqqWmX5F6OYUciRxQXf7HrN5TOCPuI7QXbkbj4LRXoxVuB3/i9H15q5TU+vFxorhUBeWFfF998OYQiPYViD2yI="
      ]
    } ],
    "attributes" : [ {
      "type" : "Currency",
      "text" : "$2,000.00",
      "location" : {
        "begin" : 134780,
        "end" : 134789
      }
    } ]
 }
 ```
{: codeblock}

Ogni elemento ha cinque sezioni importanti:
-  `location`: gli indici `begin` e `end` che indicano l'ubicazione dell'elemento nel documento di input.
-  `text`: il testo dell'elemento classificato.
-  `types`: un array che include zero o più oggetti `label`. Ogni oggetto `label` include un campo `nature` che elenca gli effetti dell'elemento sulla parte identificata (ad esempio, `Right` o `Exclusion`) e un campo `party` che identifica la parte o le parti interessate dall'elemento. Per ulteriori informazioni, consulta i [Tipi](/docs/services/discovery/parsing.html#contract_types) in [Descrizione dell'analisi del contratto](/docs/services/discovery/parsing.html#contract_parsing).
-  `categories`: un array che contiene zero o più oggetti `label`. Il valore di ogni oggetto `label` elenca una categoria funzionale in cui risiede l'elemento identificato. Per ulteriori informazioni, consulta le [Categorie](/docs/services/discovery/parsing.html#contract_categories) in [Descrizione dell'analisi del contratto](/docs/services/discovery/parsing.html#contract_parsing).
-  `attributes`: un array che elenca zero o più oggetti che definiscono gli attributi dell'elemento. Al momento i tipi di attributi supportati includono `Location` (ubicazione o regione geografica a cui fa riferimento l'elemento), `DateTime` (data, ora, intervallo di date o intervallo di tempo specificati dall'elemento) e `Currency` (valore e unità monetarie). Ogni oggetto nell'array `attributes` include anche il testo e l'ubicazione dell'elemento identificato; l'ubicazione viene definita dagli indici `begin` e `end` del testo nel documento di input. Per ulteriori informazioni, consulta gli [Attributi](/docs/services/discovery/parsing.html#attributes) in [Descrizione dell'analisi del contratto](/docs/services/discovery/parsing.html#contract_parsing).

Inoltre, ogni oggetto negli array `types` e `categories` include un array `provenance_ids`. I valori elencati nell'array `provenance_ids` sono valori hash che puoi inviare a IBM per fornire un feedback o ricevere supporto sulla parte dell'analisi associata all'elemento.

**Nota**: alcune frasi non rientrano in alcun tipo o categoria, in questo caso il servizio restituisce gli array `types` e `categories` come oggetti vuoti.

**Nota:** alcune frasi coprono più argomenti, in questo caso il servizio restituisce più insiemi di oggetti `types` e `categories`.

**Nota**: alcune frasi non contengono alcun attributo identificabile, in questo caso il servizio restituisce l'array `attributes` come oggetto vuoto.
