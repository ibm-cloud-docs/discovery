---

copyright:
years: 2018
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

# Descrizione dello schema di output
{: #output_schema}

Dopo che un documento è stato inserito utilizzando Element Classification, il servizio fornisce un output JSON nel seguente schema per la data di versione `2018-10-15` o successiva. L'output verrà incluso nell'oggetto `enriched_html_elements`. 

```
{
  "document": {
    "title": string,
    "html": string,
    "hash": string
  },
  "model_id" : string,
  "model_version" : string,
  "elements": [
    {
      "location": {
        "begin": int,
        "end": int
      },
      "text": string,
      "types": [
        {
          "label": { "nature": string, "party": string },
          "provenance_ids": [string, string, ...]
            ...
          ]
        }
        ...
      ],
      "categories": [
        {
          "label": string,
          "provenance_ids": [string, string, ...]
        }
        ...
      ],
      "attributes": [
        {
      	  "type": string,
          "text": string,
          "location": { "begin": int, "end": int }
         }
      ]
    }
    ...
  ],
  "tables": [
    {
      "location" : {
        "begin" : int,
        "end" : int
      },
      "text": string,
      "section_title": {
        "text": string,
        "location": {
          "begin" : int,
          "end" : int
        }
      },
      "table_headers" : [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int
        },
        ...
      ],
      "column_headers" : [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "text_normalized" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int
        },
        ...
      ],
      "row_headers" : [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "text_normalized" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int
        },
        ...
      ],
      "body_cells" : [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int,
          "row_header_ids": [ string ],
          "row_header_texts": [ string ],
          "row_header_texts_normalized": [ string ],
          "column_header_ids": [ string ],
          "column_header_texts": [ string ],
          "column_header_texts_normalized": [ string ]
        },
        ...
      ]
    },
    ...
  ],
  "document_structure": {
    "section_titles": [
      {
        "text": string,
        "location": {
          "begin": int,
          "end": int
        },
        "level": int
        "element_locations": [
          {
            "begin": int,
            "end": int
          },
          ...
        ]
      },
      ...
    ],
    "leading_sentences": [
      {
        "text": string,
        "location": {
          "begin": int,
          "end": int
        },
        "element_locations": [
          {
            "begin": int,
            "end": int
          },
          ...
        ]
      },
      ...
    ]
  },
  "parties": [
    {
      "party": string,
      "role": string,
      "addresses": [
        {
          "text": string,
          "location": {
            "begin": int,
            "end": int
          }
        },
        ...
      ],
      "contacts": [
        {
          "name": string,
          "role": string
        },
        ...
      ]
    },
    ...
  ],
  "effective_dates": [
    {
      "text": string,
      "location": { "begin": int, "end": int }
     },
     ...
  ],
  "contract_amounts": [
    {
      "text": string,
      "location": { "begin": int, "end": int }
    },
    ...
  ]
}
```

Lo schema è disposto nel seguente modo:

  - `document`: un oggetto che elenca le informazioni di base sul documento, tra cui:
    - `title`: il titolo del documento, se rilevato.
    - `html`: il testo completo del documento di input in formato HTML.
    - `hash`: l'hash MD5 del documento di input.
  - `model_id`: il modello di analisi da utilizzare per classificare il documento. Il valore predefinito è `contracts`. 
  - `model_version`: la versione del modello di analisi specificata dal valore del parametro `model_id`.
  - `elements`: un array degli elementi del documento rilevati dal servizio.
    - `location`: l'ubicazione dell'elemento come definita dai relativi indici `begin` e `end`.
    - `text`: il testo dell'elemento.
    - `types`: un array che descrive cos'è l'elemento e chi ne è interessato.
      - `label`: un oggetto che definisce il tipo utilizzando una coppia dei seguenti elementi:
        - `nature`: il tipo di azione richiesta dalla frase. I valori correnti sono `Definition`, `Disclaimer`, `Exclusion`, `Obligation` e `Right`.
        - `party`: una stringa che identifica la parte a cui si applica la frase.
      - `provenance_ids`: un array di uno o più valori con hash che puoi inviare a IBM per fornire un feedback o ricevere supporto.
    - `categories`: un array che elenca le categorie funzionali in cui rientra l'elemento; in altre parole, l'oggetto dell'elemento.
      - `label`: una stringa che elenca la categoria identificata. Puoi trovare un elenco delle [categorie](/docs/services/discovery/parsing.html#contract_categories) in [Descrizione dell'analisi del contratto](/docs/services/discovery/parsing.html#contract_parsing).
      - `provenance_ids`: un array di uno o più valori con hash che puoi inviare a IBM per fornire un feedback o ricevere supporto.
    - `attributes`: un array che identifica gli attributi del documento. Ogni oggetto nell'array è composto da tre elementi:
      - `type`: il tipo di attributo. I valori possibili sono `Location`, `DateTime` e `Currency`.
      - `text`: il testo associato all'attributo.
      - `location`: l'ubicazione dell'attributo come definita dai relativi indici `begin` e `end`.
  - `tables`\*: un array che definisce le tabelle identificate nel documento di input.
    - `location`: l'ubicazione della tabella corrente come definita dai relativi indici `begin` e `end` nel documento di input.
    - `text`: il contenuto testuale della tabella corrente dal documento di input senza il contenuto di markup associato.
    - `section_title`: se identificata, l'ubicazione di un titolo di sezione contenente la tabella corrente. Vuota se non è identificato alcun titolo di sezione.
      - `text`: il testo del titolo di sezione identificato.
      - `location`: l'ubicazione del titolo di sezione nel documento di input come definita dai relativi indici `begin` e `end`.
    - `table_headers`: un array di celle di livello tabella applicabili come intestazioni a tutte le altre celle della tabella corrente. Ogni intestazione di tabella è definita come una raccolta di quanto segue::
      - `cell_id`: valore stringa nel formato `tableHeader-x-y` dove `x` e `y` sono gli offset di inizio e fine del valore di cella nel documento di input originale.
      - `location`: l'ubicazione della cella nel documento di input come definita dai relativi indici `begin` e `end`.
      - `text`: il contenuto testuale della cella dal documento di input senza il contenuto di markup associato.
      - `row_index_begin`: l'indice `begin` dell'ubicazione `row` della cella nella tabella corrente.
      - `row_index_end`: l'indice `end` dell'ubicazione `row` della cella nella tabella corrente.
      - `column_index_begin`: l'indice `begin` dell'ubicazione `column` della cella nella tabella corrente.
      - `column_index_end`: l'indice `end` dell'ubicazione `column` della cella nella tabella corrente.
    - `column_headers`: un array di celle di livello colonna, ciascuna applicabile come un'intestazione ad altre celle nella stessa colonna come se stessa, della tabella corrente. Ogni intestazione di colonna è definita come una raccolta di quanto segue::
      - `cell_id`: un valore stringa nel formato `columnHeader-x-y`, dove `x` e `y` sono gli offset di inizio e fine di questa cella di intestazione colonna nel documento di input.
      - `location`: l'ubicazione della cella nel documento di input come definita dai relativi indici `begin` e `end`.
      - `text`: il contenuto testuale della cella dal documento di input senza il contenuto di markup associato.
      - `text_normalized`: se fornisci un input di personalizzazione, la versione normalizzata del testo della cella in base alla personalizzazione; altrimenti, lo stesso valore di `text`. 
      - `row_index_begin`: l'indice `begin` dell'ubicazione `row` della cella nella tabella corrente.
      - `row_index_end`: l'indice `end` dell'ubicazione `row` della cella nella tabella corrente.
      - `column_index_begin`: l'indice `begin` dell'ubicazione `column` della cella nella tabella corrente.
      - `column_index_end`: l'indice `end` dell'ubicazione `column` della cella nella tabella corrente.
    - `row_headers`: un array di celle di livello riga, ciascuna applicabile come un'intestazione ad altre celle nella stessa riga come se stessa, della tabella corrente. Ogni intestazione di riga è definita come una raccolta di quanto segue::
      - `cell_id`: un valore stringa nel formato `rowHeader-x-y`, dove `x` e `y` sono gli offset di inizio e fine di questa cella di intestazione riga nel documento di input.
      - `location`: l'ubicazione della cella nel documento di input come definita dai relativi indici `begin` e `end`.
      - `text`: il contenuto testuale della cella dal documento di input senza il contenuto di markup associato.
      - `text_normalized`: se fornisci un input di personalizzazione, la versione normalizzata del testo della cella in base alla personalizzazione; altrimenti, lo stesso valore di `text`. 
      - `row_index_begin`: l'indice `begin` dell'ubicazione `row` della cella nella tabella corrente.
      - `row_index_end`: l'indice `end` dell'ubicazione `row` della cella nella tabella corrente.
      - `column_index_begin`: l'indice `begin` dell'ubicazione `column` della cella nella tabella corrente.
      - `column_index_end`: l'indice `end` dell'ubicazione `column` della cella nella tabella corrente.
    - `body_cells`: un array di celle che non sono intestazioni di tabella, colonna o riga, della tabella corrente con le associazioni di intestazione di colonna e riga corrispondenti. Ogni cella del corpo viene definita come una raccolta di quanto segue:
      - `cell_id`: un valore di stringa nel formato `bodyCell-x-y`, dove `x` e `y` sono gli offset begin e end di questa cella del corpo nel documento di input.
      - `location`: l'ubicazione della cella nel documento di input come definita dai relativi indici `begin` e `end`.
      - `text`: il contenuto testuale della cella dal documento di input senza il contenuto di markup associato.
      - `row_index_begin`: l'indice `begin` dell'ubicazione `row` di questa cella nella tabella corrente.
      - `row_index_end`: l'indice `end` dell'ubicazione `row` di questa cella nella tabella corrente.
      - `column_index_begin`: l'indice `begin` dell'ubicazione `column` di questa cella nella tabella corrente.
      - `column_index_end`: l'indice `end` dell'ubicazione `column` di questa cella nella tabella corrente.
      - `row_header_ids`: un array di valori, ognuno che inizia con il valore `cell_id` di un'intestazione della riga applicabile a questa cella del corpo.
      - `row_header_texts`: un array di valori, ognuno che inizia con il valore `text` di un'intestazione della riga applicabile a questa cella del corpo.
      - `row_header_texts_normalized`: se fornisci un input di personalizzazione, la versione normalizzata dei testi di intestazione della riga in base alla personalizzazione; altrimenti, lo stesso valore di `row_header_texts`. 
      - `column_header_ids`: un array di valori, ognuno che inizia con il valore `cell_id` di un'intestazione della colonna applicabile a questa cella del corpo.
      - `column_header_texts`: un array di valori, ognuno che inizia con il valore `text` di un'intestazione della colonna applicabile a questa cella del corpo.
      - `column_header_texts_normalized`: se fornisci un input di personalizzazione, la versione normalizzata dei testi di intestazione della colonna in base alla personalizzazione; altrimenti, lo stesso valore di `column_header_texts`.
  - `document_structure`: un oggetto che descrive la struttura del documento di input.
    - `section_titles`: un array che contiene un singolo oggetto per ogni sezione o sottosezione rilevata nel documento di input. Le sezioni e le sottosezioni non sono nidificate; esse sono invece rese flat e possono essere rimesse in ordine utilizzando i valori `begin` e `end` dell'elemento e il valore `level` della sezione.
      - `text`: una stringa che elenca il titolo di sezione, se rilevato.
      - `location`: l'ubicazione del titolo nel documento di input come definita dai relativi indici `begin` e `end`.
      - `level`: un numero intero che indica il livello al quale si trova la sezione nel documento di input. Ad esempio, `1` rappresenta una sezione di livello superiore, `2` rappresenta una sottosezione all'interno della sezione di livello `1` e così via.
      - `element_locations`: un array che contiene oggetti che specificano i valori `begin` e `end` delle frasi nella sezione.
    - `leading_sentences`: un array che contiene un singolo oggetto per ogni sezione o sottosezione, in parallelo con l'array `section_titles`, che descrive le frasi principali nella sezione o sottosezione corrispondente. Come nell'array `section_titles`, gli oggetti non vengono nidificati; vengono invece resi flat e possono essere rimessi in ordine utilizzando i valori `begin` e `end` dell'elemento o qualsiasi indicatore di livello nel documento di input.
      - `text`: una stringa che elenca la frase principale, se rilevato.
      - `location`: l'ubicazione della frase principale nel documento di input come definita dai relativi indici `begin` e `end`.
      - `element_locations`: un array che contiene oggetti che specificano i valori `begin` e `end` delle frasi principali nella sezione.
  - `parties`: un array che definisce le parti identificate dal servizio.
    - `party`: un valore di stringa che identifica la parte.
    - `role`: un valore di stringa che identifica il ruolo della parte.
    - `addresses`: un array di oggetti che identifica gli indirizzi.
      - `text`: una stringa che contiene l'indirizzo.
      - `location`: l'ubicazione dell'indirizzo come definita dai relativi indici `begin` e `end`.
    - `contacts`: un array che definisce il nome e il ruolo dei contatti identificati nel documento di input.
      - `name`: una stringa che elenca il nome di un contatto identificato.
      - `role`: una stringa che elenca il ruolo del contatto identificato.  
  - `effective_dates`: un array che identifica le date effettive del documento.
    - `text`: le date effettive, elencate come una stringa.
    - `location`: l'ubicazione della data o delle date come definita dai relativi indici `begin` e `end`.
  - `contract_amounts`: un array che identifica gli importi monetari identificati nel documento.
    - `text`: gli importi del contratto, elencati come una stringa.
    - `location`: l'ubicazione dell'importo o degli importi come definiti dai relativi indici `begin` e `end`.

**\*Note sulle tabelle:**
  - I valori di indice riga e colonna per ogni cella sono basati su zero e quindi iniziano con `0`.
  - Più valori negli array di elementi `row_header_ids` e `row_header_texts` indicano una gerarchia di intestazioni di riga.
  - Più valori negli array di elementi `column_header_ids` e `column_header_texts` indicano una gerarchia di intestazioni di colonna.
