---

copyright:
  years: 2015, 2018
lastupdated: "2018-01-23"

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

# Riferimento di configurazione

Puoi creare la tua configurazione di inserimento {{site.data.keyword.discoveryshort}} in JSON se i tuoi dati hanno esigenze speciali di [conversione](#conversion), [arricchimento](#enrichment) o [normalizzazione](#normalization).
{: shortdesc}

 Le seguenti sezioni illustrano nel dettaglio la struttura di questo JSON e dell'oggetto che può essere definito in esso. 

## Struttura di configurazione
{: #structure}

Una configurazione {{site.data.keyword.discoveryshort}} è strutturata nel modo seguente:

```json
{
  "name": "Configuration Name",
  "description": "Descriptive text about the configuration",
  "conversions": {
    "word": {},
    "pdf": {},
    "html": {},
    "segment": {},
    "json_normalizations": []
  },
  "enrichments": [],
  "normalizations": []
}
```
{: codeblock}

L'oggetto JSON di base contiene i seguenti elementi:

-  `"name": "Configuration Name"` - Il nome della tua configurazione
-  `"description": "Descriptive text about the configuration"` - Una descrizione della tua configurazione

I seguenti oggetti e array devono essere definiti per convertire, arricchire e normalizzare i documenti che vengono caricati nella tua raccolta.

- `"conversions": {}` - Come i documenti vengono trasformati in JSON che possono essere arricchiti.
- `"enrichments": []` - Quali arricchimenti vengono applicati a quali parti del JSON.
- `"normalizations": []` - Qualsiasi modifica post-arricchimento necessaria prima di archiviare il documento.

Inoltre, i seguenti elementi vengono aggiunti all'oggetto di base da {{site.data.keyword.discoveryshort}} quando la configurazione viene creata/aggiornata:

```json
{
  "configuration_id": "4f5b7c7b-ebf4-4963-882e-27eff08f08e3",
  "created": "2017-09-13T14:45:03.575Z",
  "updated": "2017-09-13T14:45:03.575Z"
}
```
{: codeblock}

## Conversione
{: #conversion}

La conversione dei documenti prende il formato di origine iniziale e utilizzando uno o più passi trasforma il documento in JSON, che può essere utilizzato per il resto del processo di inserimento. A seconda del tipo di file caricato, il processo è il seguente:

- I file **PDF** vengono convertiti in HTML utilizzando le opzioni `pdf`, il risultante **HTML** viene quindi convertito in JSON utilizzando le opzioni `html` e infine il risultante **JSON** viene convertito utilizzando le opzioni `json`.

- I file **Microsoft Word** vengono convertiti in HTML utilizzando le opzioni `word`, il risultante **HTML** viene quindi convertito in JSON utilizzando le opzioni `html` e infine il risultante **JSON** viene convertito utilizzando le opzioni `json`.

- I file **HTML** vengono convertiti in JSON utilizzando le opzioni `html` e il risultante **JSON** viene convertito utilizzando le opzioni `json`.

- I file **JSON** vengono convertiti utilizzando le opzioni `json`.

Queste opzioni sono descritte nelle seguenti sezioni. Dopo che la conversione è stata completata, l'[arricchimento](#enrichment) e la [normalizzazione](#normalization) vengono eseguiti prima che il contenuto venga archiviato.

### PDF
{: #pdf}

L'oggetto di conversione `pdf` definisce il modo in cui i documenti PDF devono essere convertiti in HTML e ha la seguente struttura:

```json
"pdf": {
  "heading": {
    "fonts": [
      {
        "level": 1,
        "min_size": 24,
        "max_size": 80,
        "bold": false,
        "italic": true,
        "name": "arial"
      },
      {
        "level": 2,
        "min_size": 18,
        "max_size": 24,
        "bold": true,
        "italic": false,
        "name": "ariel"
      }
    ]
  }
},
```
{: codeblock}

Quando converti le intestazioni dei file PDF in quei file possono essere identificate (e convertite in una tag HTML "`h`" appropriata) identificando la dimensione, il font e lo stile di ogni livello di intestazione. I livelli di intestazione possono essere specificati più volte se necessario al fine di identificare correttamente tutte le sezioni pertinenti. I livelli di intestazione HTML sono importanti per l'identificazione se pianifichi di estrarre il contenuto utilizzando i selettori CSS o se vuoi suddividere il documento utilizzando la suddivisione del documento. L'oggetto `heading` contiene l'array `fonts` e ogni elemento in tale array specifica un livello di intestazione utilizzando i seguenti parametri:

- `"level": INT` - *obbligatorio* - il livello `h` HTML in cui sarà convertito il testo identificato con questi parametri.
- `"min_size": INT` - _facoltativo_ - la dimensione font più piccola identificata come questo livello di intestazione.
- `"max_size": INT` - _facoltativo_ - la dimensione font più grande identificata come questo livello di intestazione.
- `"bold": boolean` - _facoltativo_ - Quando `true` sono identificati solo i font in grassetto come questo livello di intestazione.
- `"italic": boolean` - _facoltativo_ - Quando `true` sono identificati solo i font in corsivo come questo livello di intestazione.
- `"name": "string"` - _facoltativo_ - Il nome del font identificato come questo livello di intestazione.

Un'area del testo da identificare come intestazione deve corrispondere a tutti i parametri definiti nell'elemento dell'array specifico. Se i parametri definiti sono troppo flessibili, potresti avere più intestazioni identificate rispetto a quanto previsto. Potrai ottenere risultati migliori se definisci rigorosamente ogni livello di intestazione più volte per assicurarti che tutte le variazioni del livello di intestazione siano incluse senza corrispondenze non valide.


### Word
{: #word}

L'oggetto di conversione `word` definisce il modo in cui i documenti PDF devono essere convertiti in HTML e ha la seguente struttura:

```json
"word": {
  "heading": {
    "fonts": [
      {
        "level": 1,
        "min_size": 24,
        "bold": true,
        "italic": false,
        "name": "arial"
      },
      {
        "level": 2,
        "min_size": 18,
        "max_size": 23,
        "bold": true,
        "italic": false
      }
    ],
    "styles": [
      {
        "level": 1,
        "names": [
          "pullout heading",
          "pulloutheading",
          "header"
        ]
      },
      {
        "level": 2,
        "names": [
          "subtitle"
        ]
      }
    ]
  }
},
```
{: codeblock}

L'oggetto di conversione Microsoft Word funziona in modo simile all'oggetto di conversione PDF. Tuttavia, ci sono due diversi array che possono essere specificati all'interno dell'oggetto `heading` quando estrai le intestazioni dai documenti Microsoft Word. Puoi utilizzare uno o entrambi gli array di intestazione per estrarre gli elementi del livello di intestazione dai tuoi documenti Microsoft Word.

Ogni elemento nell'array `fonts` specifica un livello di intestazione utilizzando i seguenti parametri che utilizzano le caratteristiche del font:

- `"level": INT` - *obbligatorio* - il livello `h` HTML in cui sarà convertito il testo identificato con questi parametri.
- `"min_size": INT` - _facoltativo_ - la dimensione font più piccola identificata come questo livello di intestazione.
- `"max_size": INT` - _facoltativo_ - la dimensione font più grande identificata come questo livello di intestazione.
- `"bold": boolean` - _facoltativo_ - Quando `true` sono identificati solo i font in grassetto come questo livello di intestazione.
- `"italic": boolean` - _facoltativo_ - Quando `true` sono identificati solo i font in corsivo come questo livello di intestazione.
- `"name": "string"` - _facoltativo_ - Il nome del font identificato come questo livello di intestazione.

Un'area del testo da identificare come intestazione nell'array `font` deve corrispondere a tutti i parametri definiti nell'elemento dell'array specifico. Se i parametri definiti sono troppo flessibili, potresti avere più intestazioni identificate rispetto a quanto previsto. Potrai ottenere risultati migliori se definisci rigorosamente ogni livello di intestazione più volte per assicurarti che tutte le variazioni del livello di intestazione siano incluse senza corrispondenze non valide.

Ogni elemento nell'array `styles` specifica un livello di intestazione dagli stili Microsoft Word applicati a quel paragrafo.

- `"level": INT` - *obbligatorio* - il livello `h` HTML in cui sarà convertito il testo identificato con questi parametri.
- `"names": array` - *obbligatorio* - un array separato da virgole di nomi di stile che verrà identificato come questo livello di intestazione.

*Quando utilizzare i font e quando gli stili* - Se i tuoi documenti Microsoft Word si conformano correttamente al foglio di stile con ogni paragrafo correttamente etichettato con lo stile appropriato, si consiglia di utilizzare `styles` per estrarre le intestazioni. Tuttavia, potresti scoprire che alcuni documenti hanno stili che sono stati sovrascritti manualmente dallo scrittore. Questi documenti molto probabilmente forniscono una buona conversione quando viene utilizzato il metodo di estrazione `fonts`.
{: tip}


### HTML
{: #html}

```json
"html": {
  "exclude_tags_completely": [
    "script",
    "sup"
  ],
  "exclude_tags_keep_content": [
    "font",
    "em"
  ],
  "exclude_content": {
    "xpaths": [
      "//*[@id='list-old']",
      "//*[@id='unstable']"
    ]
  },
  "keep_content": {
    "xpaths": [
      "//*[@id='footer']",
      "//*[@id='header']"
    ]
  },
  "exclude_tag_attributes": [
    "EVENT_ACTIONS"
  ],
  "keep_tag_attributes": [
    "id"
  ],
  "extracted_fields": {
    "{field_name}": {
      "css_selector": "{CSS_selector_expression_1}",
      "type": "{field_type}"
    }
  }
},
```
{: codeblock}

#### exclude_tags_completely

`"exclude_tags_completely" : array` - Un array di nomi tag HTML che saranno esclusi. Sono inclusi la tag, il contenuto e tutti gli attributi tag definiti.

#### exclude_tags_keep_content

`"exclude_tags_keep_content" : array` - Un array di nomi tag HTML in cui le informazioni tag vengono rimosse. Di conseguenza, la tag HTML e tutti gli attributi tag vengono rimossi. Il contenuto della tag non viene ulteriormente rimosso a meno che non venga specificato. Ad esempio se viene specificato `exclude_tags_keep_content` per la tag HTML `span`, allora `<span class="info">Some <strong>Information</strong></span>` diventa: `Some <strong>Information</strong>`

#### exclude_content

`"xpaths" : array` - Un array di XPath che identifica il contenuto che viene rimosso. Se questo valore è impostato, qualsiasi cosa corrisponda ad uno degli XPath viene rimossa dall'output.

#### keep_content

`"xpaths" : array` - Un array di XPath che identifica il contenuto che viene convertito. Se questo valore è impostato, qualsiasi cosa corrisponda ad uno degli XPath viene inclusa nell'output .Le inclusioni specificate da questo parametro vengono elaborate dopo qualsiasi elaborazione specificata da `exclude_content`.

#### exclude_tag_attributes

`"exclude_tag_attributes" : array` - Un array di nomi attributo HTML che vengono rimossi dalla conversione a prescindere dalla tag HTML in cui sono presenti. **Nota:** riceverai un messaggio di errore se viene specificato sia `exclude_tag_attributes` che `keep_tag_attributes` nella stessa configurazione - è possibile specificarne solo uno per configurazione. Se presente, `keep_tag_attributes` deve essere completamente rimosso dalla configurazione; non può essere presente come un array vuoto.

#### keep_tag_attributes

`"keep_tag_attributes" : array` - Un array di nomi attributo HTML che vengono conservati dalla conversione. **Nota:** riceverai un messaggio di errore se viene specificato sia `keep_tag_attributes` che `exclude_tag_attributes` nella stessa configurazione - è possibile specificarne solo uno per configurazione. Se presente, `exclude_tag_attributes` deve essere completamente rimosso dalla configurazione; non può essere presente come un array vuoto.

#### extracted_fields

Questo oggetto definisce tutto il contenuto proveniente dall'origine HTML che deve essere estratto in un campo JSON separato come parte della conversione. Il contenuto viene identificato utilizzando i selettori CSS.

Ogni campo che vuoi creare viene definito da un oggetto nel modo seguente:

```json
"{field_name}": {
  "css_selector": "{CSS_selector_expression_1}",
  "type": "{field_type}"
}
```
{: codeblock}

- `"{field_name}"` - Il nome del campo da creare.

**Nota:** i nomi del campo definiti nella configurazione devono soddisfare le limitazioni definite nei [Requisiti nome campo](#field_reqs).

- `"css_selector" : string` *obbligatorio* - un'espressione del selettore CSS che definisce l'area del contenuto da archiviare in un campo.
- `"type" : string` *obbligatorio* - Il tipo di campo da creare, può essere `string`, `date`
Per informazioni dettagliate, consulta [Utilizzo dei selettori CSS per estrarre i campi](/docs/services/discovery/building.md#using-css).

### Segmento
{: #segment}

L'oggetto `segment` è una serie di opzioni di configurazione che suddivide i documenti inseriti in uno o più segmenti in base alle intestazioni HTML identificate (`h1`, `h2`).

```json
"segment": {
  "enabled": true,
  "selector_tags": ["h1", "h2", "h3", "h4", "h5", "h6"]
}
```
{: codeblock}

- `"enabled": boolean` - *obbligatorio* - deve essere impostato su `true` per abilitare la segmentazione del documento.
- `"selector_tags": array` - *obbligatorio* - un array separato da virgole di tag HTML `h` in cui suddividere i documenti.

Come panoramica, quando la segmentazione del documento è abilitata, non può essere specificato quanto segue:

-  `json_normalizations` non può essere specificato come parte della configurazione.
-  `normalizations` non può essere specificato come parte della configurazione.
-  L'opzione `extracted_fields` della conversione `html` non può essere specificata come parte della configurazione.

Per informazioni dettagliate, vedi [Esecuzione della segmentazione](/docs/services/discovery/building.html#performing-segmentation).


### JSON
{: #json}

Puoi eseguire la normalizzazione pre-arricchimento del JSON inserito definendo gli oggetti `operation` nell'array `json_normalizzazione_jr`.

```json
"json_normalizations": [
  {
    "operation": "remove",
    "source_field": "header"
  },
  {
    "operation": "copy",
    "source_field": "title",
    "destination_field": "title_old"
  },
  {
    "operation": "move",
    "destination_field": "content",
    "source_field": "body"
  },
  {
    "operation": "merge",
    "source_field": "synopsis",
    "destination_field": "preamble"
  },
  {
    "operation": "remove_nulls"
  }
]
```
{: codeblock}

#### Oggetti delle operazioni
{: #operations}

- `"operation": string` - *obbligatorio* - l'operazione che verrà eseguita sul JSON, deve essere una delle seguenti:
  - `remove` - il `source_field` specificato sarà rimosso dal JSON.
  - `copy` - il contenuto del `source_field` specificato sarà copiato in una nuova istanza di `destination_field`.
  - `move` - il `source_field` specificato viene ridenominato con `destination_field`. Se `destination_field` già esiste, viene creata una nuova istanza di `destination_field`.
  - `merge` - i contenuti di `source_field` e `destination_field` vengono uniti in `destination_field`.
  - `remove_nulls` - i campi con il contenuto `null` vengono rimossi.
- `"source_field": string` - _facoltativo_ - il campo in cui sarà eseguita l'operazione.
- `"destination_field": string` - _facoltativo_ - il campo di destinazione dell'output dell'operazione.  

  **Nota:** i nomi del campo definiti nella configurazione devono soddisfare le limitazioni definite nei [Requisiti nome campo](#field_reqs).


## Arricchimenti
{: #enrichments}

```json
"enrichments": [
  {
    "enrichment": "elements",
    "source_field": "html",
    "destination_field": "enriched_html",
    "options": {
      "model": "contract"
    }
  },
  {
    "enrichment": "natural_language_understanding",
    "source_field": "title",
    "destination_field": "enriched_title",
    "options": {
      "features": {
        "keywords": {
          "sentiment": true,
          "emotion": false,
          "limit": 50
        },
        "entities": {
          "sentiment": true,
          "emotion": false,
          "limit": 50,
          "mentions": true,
          "mention_types": true,
          "sentence_locations": true,        
          "model": "WKS-model-id"
        },
        "sentiment": {
          "document": true,
          "targets": [
            "IBM",
            "Watson"
          ]

        },
        "emotion": {
          "document": true,
          "targets": [
            "IBM",
            "Watson"
          ]
        },
        "categories": {},
        "concepts": {
          "limit": 8
        },
        "semantic_roles": {
          "entities": true,
          "keywords": true,
          "limit": 50
        },
        "relations": {
          "model": "WKS-model-id"
        }
      }
    }
  }
]
```
{: codeblock}

{{site.data.keyword.discoveryshort}} supporta l'aggiunta degli arricchimenti {{site.data.keyword.nlushort}} e Element Classification. Ogni campo che vuoi arricchire viene definito da un oggetto nell'array `enrichments`. Ogni oggetto di arricchimento ha bisogno che vengano specificati `source_field`, `destination_field` e gli arricchimenti.

- `"enrichment" : string` - *obbligatorio* - Il tipo di arricchimento da utilizzare su questo campo. Per estrarre gli arricchimenti {{site.data.keyword.nlushort}} utilizza `natural_language_understanding`, per eseguire l'Element Classification utilizza `elements`.

  **Nota:** quando utilizzi l'arricchimento `elements`, è importante seguire le linee guida specificate nella documentazione di [Element Classification](/docs/services/discovery/element-classification.html). In particolare, solo i file PDF possono essere inseriti quando viene specificato questo arricchimento.

- `"source_field" : string` - *obbligatorio* - Il campo di origine che verrà arricchito. Questo campo deve essere presente nella tua origine dopo che l'operazione `json_normalizations` è stata completata.
- `"destination_field" : string` - *obbligatorio* - Il nome dell'oggetto contenitore in cui verranno creati gli arricchimenti.

  **Nota:** i nomi del campo definiti nella configurazione devono soddisfare le limitazioni definite nei [Requisiti nome campo](#field_reqs).

### Arricchimenti Element Classification

Quando utilizzi l'Element Classification, ogni oggetto di arricchimento `elements` deve contenere un oggetto `"options": {}` con i seguenti parametri specificati:

- `"model" : string` - *obbligatorio* - Il modello di estrazione dell'elemento da utilizzare con questo documento. I modelli al momento supportati sono: `contract`

**Nota:** quando utilizzi l'arricchimento `elements`, è importante seguire le linee guida specificate nella documentazione di [Element Classification](/docs/services/discovery/element-classification.html). In particolare, solo i file PDF possono essere inseriti quando viene specificato questo arricchimento.

### Arricchimenti Natural Language Understanding 

Quando utilizzi {{site.data.keyword.nlushort}}, ogni oggetto all'interno dell'array `enrichments` deve contenere anche un oggetto `"options": { "features": { } }` che contiene uno o più dei seguenti arricchimenti:

### categories

L'arricchimento `categories` identifica tutte le categorie generali nel documento inserito. Questo arricchimento non ha opzioni e deve essere specificato come un oggetto vuoto `"categories" : {}`

### concepts

L'arricchimento `concepts` trova i concetti con i quali il testo di input è associato, in base ad altri concetti e entità presenti in quel testo.

- `"limit" : INT` - *obbligatorio* - Il numero massimo di concetti da estrarre dal documento inserito.

### emotion

L'arricchimento `emotion` valuta il tono emotivo complessivo (ad esempio `anger`) del documento completo o di stringhe di destinazione specificate in tutto il documento. Questo arricchimento può essere utilizzato solo con il contenuto inglese.

- `"document" : boolean ` _facoltativo_ - Quando `true` viene valutato il tono emotivo dell'intero documento.
- `"targets" : array ` _facoltativo_ - Un array separato da virgole di stringhe di destinazione di cui valutare lo stato emotivo all'interno del documento.

### entities

L'arricchimento `entities` estrae le istanze di entità conosciute come persone, luoghi o organizzazioni. Facoltativamente, può essere specificato un modello personalizzato {{site.data.keyword.knowledgestudioshort}} per estrarre le entità personalizzate.

- `"sentiment" : boolean` - _facoltativo_ - Quando `true`, Sentiment Analysis viene eseguito sull'entità estratta nel contesto del contenuto circostante.
- `"emotion" : boolean` - _facoltativo_ - Quando `true`, l'analisi del tono emotivo viene eseguita sull'entità estratta nel contesto del contenuto circostante.
- `"limit" : INT` - _obbligatorio_ - Il numero massimo di entità da estrarre dal documento inserito. Il valore predefinito è `50`.
- `"mentions": boolean` - _facoltativo_ - Quando `true`, viene registrato il numero di volte in cui viene menzionata questa entità. Il valore predefinito è `false`.
- `"mention_types": boolean` - _facoltativo_ - Quando `true`, viene memorizzato il tipo di menzione per ogni menzione di questa entità. Il valore predefinito è `false`.
- `"sentence_location": boolean` - _facoltativo_ - Quando `true`, viene memorizzata l'ubicazione della frase di ogni menzione dell'entità. Il valore predefinito è `false`.
- `"model" : string` - _facoltativo_ - Quando specificato, il modello personalizzato viene utilizzato per estrarre le entità invece del modello pubblico. Questa opzione richiede un modello personalizzato {{site.data.keyword.knowledgestudioshort}} da associare alla tua istanza di {{site.data.keyword.discoveryshort}}. Per ulteriori informazioni, consulta [Integrazione con Watson Knowledge Studio](/docs/services/discovery/integrate-wks.html).

### keywords

L'arricchimento `keywords` estrae le istanze di parole significative all'interno del testo. Per comprendere la differenza tra parole chiave, concetti e entità vedi: [Descrizione della differenza tra entità, concetti e parole chiave](/docs/services/discovery/building.html#udbeck).

- `"sentiment" : boolean` - _facoltativo_ - Quando `true`, Sentiment Analysis viene eseguito sulla parola chiave estratta nel contesto del contenuto circostante.
- `"emotion" : boolean` - _facoltativo_ - Quando `true`, l'analisi del tono emotivo viene eseguita sulla parola chiave estratta nel contesto del contenuto circostante.
- `"limit" : INT` - _obbligatorio_ - Il numero massimo di parole chiave da estrarre dal documento inserito. Il valore predefinito è `50`.

### semantic_roles

L'arricchimento `semantic_roles` identifica i componenti della frase come il soggetto, l'azione e l'oggetto all'interno del testo inserito.

- `"entities" : boolean` - _facoltativo_ Quando `true`, le entità vengono estratte dai componenti della frase.
- `"keywords" : boolean` - _facoltativo_ Quando `true`, le parole chiave vengono estratte dai componenti della frase.
- `"limit" : INT` - _obbligatorio_ - Il numero massimo di oggetti `semantic_roles` da estrarre (frasi da analizzare) dal documento inserito. Il valore predefinito è `50`.

### sentiment

L'arricchimento `sentiment` valuta il livello delle sensazioni complessivo di tutto il documento o di stringhe di destinazione specificate in tutto il documento.

- `"document" : boolean ` _facoltativo_ - Quando `true` vengono valutate le sensazioni dell'intero documento.
- `"targets" : array ` _facoltativo_ - Un array separato da virgole di stringhe di destinazione per valutare le sensazioni all'interno del documento.

### relations

L'arricchimento `relations` estrae le relazioni note tra le entità identificate all'interno del documento. Facoltativamente, può essere specificato un modello personalizzato {{site.data.keyword.knowledgestudioshort}} per estrarre le relazioni personalizzate.

- `"model" : string` - _facoltativo_ - Quando specificato, il modello personalizzato viene utilizzato per estrarre le relazioni invece del modello pubblico. Questa opzione richiede un modello personalizzato {{site.data.keyword.knowledgestudioshort}} da associare alla tua istanza di {{site.data.keyword.discoveryshort}}. Per ulteriori informazioni, consulta [Integrazione con Watson Knowledge Studio](/docs/services/discovery/integrate-wks.html).

## Normalizzazione
{: #normalization}

`normalizations` è un array di oggetti JSON `operation` utilizzati per ripulire il JSON inserito dopo che sono stati applicati gli arricchimenti (`enrichments`) e prima che venga archiviato.

```json
"normalizations": [
  {
    "operation": "remove",
    "source_field": "enriched_title.entities.text"
  },
  {
    "operation": "copy",
    "source_field": "enriched_title.sentiment.document.score",
    "destination_field": "titlescore"
  }
]
```
{:codeblock}

Le opzioni dell'oggetto `operation` sono elencate [qui](#operations)

## Requisiti nome campo
{: #field_reqs}

I nomi dei campi non possono contenere spazi. I seguenti caratteri e stringhe sono riservati e non possono essere utilizzati nei nomi campo:


```
  .  ,  # ? :
  id
  score
  highlight
  result_metadata
```
{: pre}

I caratteri `_`, `+` e `-` non possono essere utilizzati come prefisso di `field_name`

I caratteri numerici `0 - 9` non devono essere il suffisso di un nome di campo (ad esempio `extracted-content2`). Questi nomi campo saranno indicizzati, ma non possono essere interrogati.
