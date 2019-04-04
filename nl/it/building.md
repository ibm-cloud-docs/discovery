---

copyright:
  years: 2015, 2018, 2019
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

# Configurazione del tuo servizio
{: #configservice}

La creazione di un servizio {{site.data.keyword.discoveryshort}} renderà possibile acquisire informazioni utili arricchendo i tuoi dati e poi distribuendoli in un formato disponibile per la query.
{: shortdesc}

Prima di aggiungere il tuo contenuto al servizio {{site.data.keyword.discoveryshort}}, devi configurare il servizio per elaborare il contenuto nel modo che desideri.

Il primo passo è quello di configurare i parametri di base del servizio ([Preparazione del servizio per i tuoi documenti](/docs/services/discovery?topic=discovery-configservice#preparing-the-service-for-your-documents)), questo include la creazione di un ambiente e di una o più raccolte all'interno di quell'ambiente. 

Se la tua raccolta è stata creata prima dell'introduzione di [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu), potresti voler specificare una o più configurazioni personalizzate (vedi [Quando hai bisogno di una configurazione personalizzata](/docs/services/discovery?topic=discovery-configservice#when-you-need-a-custom-configuration)). Se è questo il caso, dovrai eseguire quanto segue:

-   identificare alcuni contenuti di esempio (documenti che sono rappresentativi dei tuoi file)
-   caricare il contenuto ([Caricamento dei documenti di esempio](/docs/services/discovery?topic=discovery-configservice#uploading-sample-documents))
-   modificare il processo di conversione ([Conversione dei documenti di esempio](/docs/services/discovery?topic=discovery-configservice#converting-sample-documents))
-   definire gli arricchimenti ([Aggiunta degli arricchimenti](/docs/services/discovery?topic=discovery-configservice#adding-enrichments))
-   normalizzare i risultati ([Normalizzazione dei dati](/docs/services/discovery?topic=discovery-configservice#normalizing-data))

    Dopo aver creato la tua configurazione personalizzata, puoi caricare i tuoi documenti ([Aggiunta di contenuto](/docs/services/discovery?topic=discovery-addcontent#addcontent)).

## Preparazione del servizio per i tuoi documenti
{: #preparing-the-service-for-your-documents}

Nel servizio {{site.data.keyword.discoveryshort}}, il contenuto che carichi viene archiviato in una raccolta che fa parte del tuo ambiente. Devi creare l'ambiente e la raccolta prima di poter caricare il tuo contenuto.

-   **Ambiente** - L'ambiente definisce la quantità di spazio di archiviazione di cui disponi per il contenuto nel servizio {{site.data.keyword.discoveryshort}}. Può essere creato un massimo di un ambiente per ogni istanza del servizio {{site.data.keyword.discoveryshort}}.

    Se hai diversi piani (Lite, Advanced, Premium) da cui scegliere, vedi il [catalogo {{site.data.keyword.discoveryshort}}![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/catalog/services/discovery){: new_window} e i [Piani dei prezzi di {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans) per i dettagli. I tuoi file di origine non vengono conteggiati nel tuo limite della dimensione del piano, solo la dimensione del JSON convertito che viene indicizzato viene conteggiata nel limite della dimensione.

-   **Raccolta** - Una raccolta è un raggruppamento dei tuoi contenuti all'interno dell'ambiente. Devi creare almeno una raccolta per poter caricare il tuo contenuto.

    Le raccolte sono costituite dai tuoi dati privati, ma {{site.data.keyword.discoveryshort}} include anche {{site.data.keyword.discoverynewsshort}}, un insieme di dati pubblico e pre-arricchito. 

    {{site.data.keyword.discoverynewsshort}}, un insieme di dati pubblico che è stato pre-arricchito con analisi approfondite cognitive, è anche incluso con {{site.data.keyword.discoveryshort}}. Puoi utilizzarlo per eseguire la query per le informazioni approfondite; ad esempio: avvisi di notizie, rilevamento eventi e argomenti di tendenza nelle notizie; che puoi integrare nelle tue applicazioni. Per ulteriori informazioni, consulta [Watson Discovery News](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news). Non puoi regolare la configurazione di {{site.data.keyword.discoverynewsshort}} o aggiungere i documenti a questa raccolta. Vedi una demo di quello che puoi creare con {{site.data.keyword.discoverynewsshort}} [qui![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://discovery-news-demo.ng.bluemix.net/){: new_window}.

Per creare un ambiente e una raccolta di dati privata con la strumentazione {{site.data.keyword.discoveryshort}} utilizza la seguente procedura:

1.  Nella schermata **Manage Data**, fai clic sull'icona ![Environment](images/icon_settings.png) nell'angolo superiore destro e scegli **Create environment**. L'ambiente viene creato in base al piano {{site.data.keyword.Bluemix_notm}} selezionato in precedenza. Lo stato del tuo ambiente è sempre disponibile da questo menu a discesa.

1.  Una volta che il tuo ambiente è pronto, fai clic sul pulsante **Upload your own data**, dopodiché puoi dare un **Nome alla tua nuova raccolta**.

     Puoi selezionare la lingua dei documenti che aggiungerai a questa raccolta: inglese, tedesco, spagnolo, arabo, giapponese, francese, italiano, coreano o portoghese brasiliano. Ci dovrebbe essere una sola lingua in ciascuna delle tue raccolte. Dopo aver fatto clic su **Create**, la tua raccolta dati sarà visualizzata come un tile.

Il tuo ambiente e la tua raccolta dati sono pronti! Puoi iniziare ad [aggiungere contenuto](/docs/services/discovery?topic=discovery-addcontent#addcontent) immediatamente. 

Tuttavia, se vuoi personalizzare la tua configurazione {{site.data.keyword.discoveryshort}} con ulteriori arricchimenti e impostazioni della conversione, non dovresti iniziare ad aggiungere i documenti in questo momento e dovresti iniziare creando il tuo file di configurazione personalizzato. Consulta [Configurazione del tuo servizio](/docs/services/discovery?topic=discovery-configservice#custom-configuration).

Se la tua raccolta era stata creata utilizzando [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu), potresti preferire di regolare i tuoi arricchimenti utilizzando la strumentazione {{site.data.keyword.discoveryshort}}.
{: note}

Per le raccolte create prima della release di Smart Document Understanding: quando i documenti vengono caricati in una raccolta di dati, vengono convertiti e arricchiti utilizzando il file di configurazione selezionato per tale raccolta. Se decidi successivamente che desideri modificare il file di configurazione puoi farlo, ma i documenti che sono già stati caricati rimarranno convertiti dalla configurazione originale. Tutti i documenti caricati dopo il passaggio al file di configurazione utilizzeranno il nuovo file di configurazione. Se vuoi che la raccolta **completa** utilizzi la nuova configurazione, dovrai creare una nuova raccolta, scegliere il nuovo file di configurazione e ricaricare tutti i documenti. Il servizio {{site.data.keyword.discoveryshort}} archivia il testo convertito dei documenti che carichi, le immagini integrate nei file **PDF** e **Microsoft Word** non vengono archiviate e non saranno restituite nei risultati. Se la tua raccolta sta utilizzando [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu), le eventuali modifiche apportate ad arricchimenti e conversione in {{site.data.keyword.discoveryshort}} verranno applicati all'intera raccolta quando fai clic sul pulsante **Apply changes to collection**. Se la tua raccolta è grande, l'applicazione delle modifiche potrebbe richiedere un po' di tempo.  
{: important}

Puoi utilizzare la strumentazione {{site.data.keyword.discoveryshort}} o l'API per eseguire la ricerca per l'indicizzazione di origini dati Box, Salesforce, Microsoft SharePoint Online, IBM Cloud Object Storage e Microsoft SharePoint 2016 o per eseguire una ricerca per l'indicizzazione web. Per ulteriori informazioni, vedi [Connessione alle origini dati](/docs/services/discovery?topic=discovery-sources#sources).
{: tip}

### La configurazione predefinita
{: #the-default-configuration}

Il servizio {{site.data.keyword.discoveryshort}} include una configurazione standard che convertirà, arricchirà e normalizzerà i tuoi dati senza richiederti di configurare manualmente queste opzioni.

Il file **Default Configuration** è disponibile solo nelle raccolte create prima della release di [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu). Tuttavia, in caso di utilizzo di Smart Document Understanding, nelle tue raccolte verranno utilizzati per impostazione predefinita gli stessi arricchimenti e le stesse conversioni HTML e JSON.
{: note}

Quando crei una raccolta, {{site.data.keyword.discoveryshort}} arricchirà (aggiungerà ad esso i metadati cognitivi) il campo `text` dei tuoi documenti con informazioni semantiche raccolte da quattro arricchimenti {{site.data.keyword.watson}} - Entity Extraction, Sentiment Analysis, Category Classification e Concept Tagging (ulteriori informazioni [qui](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)).Verranno applicate anche le conversioni di documento basate sugli stili e sulle dimensioni dei font. Puoi regolare gli arricchimenti in un secondo momento utilizzando la scheda **Overview**. (Questa configurazione è denominata **Default Configuration** nelle raccolte create prima della release di [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu)).

Le conversioni predefinite:

-   [Conversione Microsoft Word](/docs/services/discovery?topic=discovery-configservice#microsoft-word-conversion)
-   [Conversione PDF](/docs/services/discovery?topic=discovery-configservice#pdf-conversion)
-   [Conversione HTML](/docs/services/discovery?topic=discovery-configservice#html-conversion)
-   [Conversione JSON](/docs/services/discovery?topic=discovery-configservice#json-conversion)

Una configurazione denominata **Default Contract Configuration** è disponibile quando crei una raccolta con la strumentazione {{site.data.keyword.discoveryshort}}. È configurata per l'arricchimento con l'Element Classification, che può essere utilizzata per estrarre la parte, la natura e la categoria dagli elementi nei PDF. Vedi [Element Classification](/docs/services/discovery?topic=discovery-element-classification#element-collection) per i dettagli. Smart Document Understanding non sarà disponibile se viene utilizzato questo file di configurazione.

Se desideri creare una configurazione personalizzata per le raccolte create prima della release di [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu), vedi [Configurazione personalizzata](/docs/services/discovery?topic=discovery-configservice#custom-configuration).

### Quando hai bisogno di una configurazione personalizzata
{: #when-you-need-a-custom-configuration}

Queste informazioni si applicano solo alle raccolte create prima della release di [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu).
{: note}

Ottenere le informazioni corrette dal tuo contenuto e restituirle ai tuoi utenti è l'obiettivo del servizio {{site.data.keyword.discoveryshort}}. L'identificazione di quali siano tali informazioni e del modo in cui vengono memorizzate nel tuo contenuto è definita dalla configurazione che utilizzi per inserire il contenuto. I tipi di contenuto che il servizio {{site.data.keyword.discoveryshort}} può inserire sono flessibili, il che significa che anche se il tuo contenuto non strutturato viene salvato in un formato specifico, non è necessario che la struttura di tale contenuto corrisponda alla struttura di altro contenuto dello stesso tipo.

-   **Ho capito che i miei documenti potrebbero non essere strutturati nel modo previsto dalla configurazione predefinita. *Come posso sapere
    se le impostazioni predefinite sono corrette per me?***
    -   Il modo più semplice per vedere se il valore predefinito funziona per te è di testarlo con il [Caricamento dei documenti di esempio](/docs/services/discovery?topic=discovery-configservice#uploading-sample-documents). Se i risultati del JSON di esempio soddisfano le tue aspettative, non è richiesta alcuna ulteriore configurazione.
-   **Ho capito che gli arricchimenti predefiniti vengono aggiunti al campo di testo dei miei documenti. Posso aggiungere ulteriori arricchimenti ad altri campi?**
    -   Assolutamente, puoi aggiungere ulteriori arricchimenti a quanti campi vuoi. Per i dettagli, consulta [Aggiunta degli arricchimenti](/docs/services/discovery?topic=discovery-configservice#adding-enrichments).

## Configurazione personalizzata
{: #custom-configuration}

Queste informazioni si applicano solo alle raccolte create prima della release di [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu).
{: note}

Per creare una configurazione personalizzata nella strumentazione {{site.data.keyword.discoveryshort}}, apri una raccolta dati privata e nella schermata **Manage Data**, fa clic su **Switch** accanto al nome della tua **Configurazione**. Nella finestra di dialogo **Switch configuration**, fai clic su **Create a new configuration**.

Dopo aver denominato il tuo nuovo file di configurazione, quel nome verrà visualizzato all'inizio della schermata di configurazione. Questo nuovo file di configurazione conterrà automaticamente le impostazioni e gli arricchimenti del file [Configurazione predefinita](/docs/services/discovery?topic=discovery-configservice#the-default-configuration) per permetterti di iniziare a lavorare.

I tre passi di personalizzazione di un file di configurazione sono: **Conversione**, **Arricchimento** e **Normalizzazione**.

1.  [Conversione dei documenti di esempio](/docs/services/discovery?topic=discovery-configservice#converting-sample-documents)
1.  [Aggiunta degli arricchimenti](/docs/services/discovery?topic=discovery-configservice#adding-enrichments) (Questa scheda è disponibile quando si utilizza Smart Document Configuration).
1.  [Normalizzazione dei dati](/docs/services/discovery?topic=discovery-configservice#normalizing-data)

Per informazioni dettagliate sulle configurazioni, consulta il [Riferimento della configurazione](/docs/services/discovery?topic=discovery-configref#configref).

### Caricamento dei documenti di esempio
{: #uploading-sample-documents}

Queste informazioni si applicano solo alle raccolte create prima della release di [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu).
{: note}

Per rendere il processo di configurazione più efficiente, puoi caricare fino a dieci file Microsoft Word, HTML, JSON o PDF che sono rappresentativi della tua serie di documenti. Questi sono denominati **documenti di esempio**. I documenti di esempio non vengono aggiunti alla tua raccolta - vengono utilizzati solo per identificare i campi comuni nei tuoi documenti e per personalizzare questi campi con i tuoi requisiti.

Quando crei un nuovo file di configurazione nella strumentazione {{site.data.keyword.discoveryshort}}, puoi caricare i documenti di esempio tramite il trascinamento e il rilascio o selezionandoli. Fai clic sul nome del file nel pannello **Upload Sample Documents** per un'anteprima di ogni file.

#### Ricorda quanto segue quando carichi i documenti di esempio:

-   Tutti i tuoi documenti sono convertiti in JSON prima di essere arricchiti e indicizzati.
-   I documenti Microsoft Word e PDF vengono convertiti prima in HTML e poi in JSON.
-   I documenti HTML vengono convertiti direttamente in JSON.
-   La dimensione massima del file per un documento di esempio è di 1MB. I documenti di esempio sono archiviati nella cartella dei dati di roaming locale del tuo browser. Per eliminare i tuoi documenti di esempio, fai clic sull'icona **Delete**.

#### Linee guida per la scelta di documenti di esempio validi:

-   Devi avere (al minimo), un documento di esempio per ogni tipo di file che vuoi inserire - Microsoft Word, PDF, HTML e JSON. (Non puoi visualizzare l'anteprima dei documenti PDF arricchiti con l'arricchimento **Element Classification**).
-   Se hai tipi di documento univoci (come ad esempio i report finanziari o i comunicati stampa), includi uno di ognuno di essi nella tua serie di documenti di esempio.
-   Per i documenti HTML, dovresti scegliere documenti che includono le tag HTML che vorresti escludere, nonché gli attributi tag che vorresti includere o escludere.
-   I documenti JSON dovrebbero includere tutti i campi che vuoi rimuovere o unire tra loro (ad esempio, zipCode e postalCode).

### Conversione dei documenti di esempio
{: #converting-sample-documents}

Queste informazioni si applicano solo alle raccolte create prima della release di [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu).
{: note}

La conversione dei tuoi documenti di esempio è il processo che ti consentirà di definire il modo in cui viene gestito ogni tipo di input. Il tipo di file di contenuto che carichi determina il numero di passi di conversione che dovrai considerare.

Prima di iniziare, [carica i documenti di esempio](/docs/services/discovery?topic=discovery-configservice#uploading-sample-documents) e aprine uno del tipo di file che desideri configurare nel pannello a destra.

Per utilizzare le impostazioni di conversione, fai clic nei tipi di file.

![Conversione di un documento di esempio](images/convert.png)

-   **Se stai convertendo i file Microsoft Word devi effettuare le seguenti operazioni:**
    -   Impostare le opzioni di conversione Microsoft Word
    -   Impostare le opzioni di conversione HTML
    -   Impostare le opzioni di conversione JSON
    -   Controllare il risultato

-   **Se stai convertendo i file PDF devi effettuare le seguenti operazioni:**
    -   Impostare le opzioni di conversione PDF
    -   Impostare le opzioni di conversione HTML
    -   Impostare le opzioni di conversione JSON
    -   Controllare il risultato

-   **Se stai convertendo i file HTML devi effettuare le seguenti operazioni:**
    -   Impostare le opzioni di conversione HTML
    -   Impostare le opzioni di conversione JSON
    -   Controllare il risultato

-   **Se stai convertendo i file JSON** devi impostare le opzioni di conversione JSON e rivedere il risultato.

Per ogni file di configurazione creato, c'è solo una serie di opzioni di conversione per ogni passo del processo. Questo significa che le opzioni di conversione HTML saranno le stesse per i file PDF, Word e HTML. Se hai bisogno di opzioni di conversione diverse per ogni tipo di contenuto che stai inserendo (o se hai file dello stesso tipo che richiedono diversi tipi di conversione) devi archiviare i tuoi file in raccolte differenti e creare file di configurazione separati per ciascuna serie di impostazioni di conversione.

#### Conversione Microsoft Word
{: #microsoft-word-conversion}

Le dimensioni e gli stili del font Microsoft Word vengono utilizzati per convertire correttamente le intestazioni nei tuoi documenti in H1, H2 e così via. H1 è il titolo del documento e H2 e successivi sono i sottotitoli. Utilizza le caselle di testo e i pulsanti di opzione per modificare le impostazioni predefinite se necessario. Puoi anche aggiungere ulteriori livelli di intestazione e stili di Word. Se i tuoi documenti Word tendono ad utilizzare un font specifico o un nome di stile per le intestazioni, assicurati di aggiungere tali informazioni. Questo aiuterà a migliorare la tua conversione, che darà risultati migliori delle query.

**Esempio:** se è comune che i tuoi documenti Word utilizzano un font di 20 pt, corsivo per le intestazioni 2s - modifica **Font size range** da ** 20 ** a **23** e **Font style** con **italic**.

Dopo aver apportato le modifiche, fai clic su **Apply and Save**.

#### Conversione PDF
{: #pdf-conversion}

Le dimensioni e i nomi del font PDF vengono utilizzati per convertire correttamente le intestazioni nei tuoi documenti in H1, H2 e così via. H1 è il titolo del documento e H2 e successivi sono i sottotitoli. Utilizza le caselle di testo e i pulsanti di opzione per modificare le impostazioni predefinite se necessario. Puoi anche aggiungere ulteriori livelli di intestazione. Se i tuoi documenti PDF tendono ad utilizzare un font specifico per le intestazioni, assicurati di aggiungere tali informazioni. Questo aiuterà a migliorare la tua conversione, che darà risultati migliori delle query.

**Esempio:** se è comune che i tuoi documenti PDF utilizzano un font di 20 pt, grassetto per le intestazioni 1s - modifica **Font size range** da ** 20 ** a **80** e **Font style** con **bold**. Modifica gli altri livelli di conseguenza.

Dopo aver apportato le modifiche, fai clic su **Apply and Save**.

#### Conversione HTML
{: #html-conversion}

Puoi utilizzare questo passo per rimuovere le tag non necessarie e altre informazioni sul documento in modo da conservare solo le informazioni necessarie per le tue query.

Impostazioni HTML predefinite:

- Escludi queste tag, così come il loro contenuto: **`script`**, **`sup`**
- Escludi queste tag, ma conservarne il contenuto: **`font`**, **`em`**, **`span`**
- Conserva questi attributi tag: nessun valore predefinito
- Escludi questi attributi tag: **`EVENT_ACTIONS`**
- Conserva il contenuto che corrisponde a questi XPath: nessun valore predefinito
- Escludi il contenuto che corrisponde a questi XPath: nessun valore predefinito

Dopo aver apportato le modifiche, fai clic su **Apply and Save**.

#### Conversione JSON
{: #json-conversion}

L'ultimo passo della conversione è quello di assicurarti che la conversione (o il JSON caricato) sia stata formata nel modo desiderato prima che gli arricchimenti sono applicati al contenuto. Puoi creare delle regole {{site.data.keyword.watson}} che utilizzerai per convertire il tuo HTML in JSON.

-   Puoi spostare, unire, copiare o rimuovere i campi. Ad esempio: potresti voler unire **`zipCode`** e **`postalCode`** perché sono due termini simili per lo stesso campo.
-   I campi vuoti (campi che non contengono informazioni) verranno eliminati per impostazione predefinita. Puoi modificare questa impostazione con il pulsante di attivazione **Remove empty fields**.

Dopo aver apportato le modifiche, fai clic su **Apply and Save**.

## Aggiunta degli arricchimenti
{: #adding-enrichments}

La {{site.data.keyword.discoveryshort}} [configurazione predefinita](/docs/services/discovery?topic=discovery-configservice#the-default-configuration) arricchirà (aggiungerà i metadati cognitivi) il campo `text` dei tuoi documenti inseriti con le informazioni semantiche raccolte da queste quattro funzioni {{site.data.keyword.watson}} - Entity Extraction, Sentiment Analysis, Category Classification e Concept Tagging. (Ci sono un totale di nove arricchimenti {{site.data.keyword.watson}} disponibili; gli altri sono Keyword Extraction, Relation Extraction, Emotion Analysis, Element Classification e Semantic Role Extraction).

Alcuni arricchimenti {{site.data.keyword.watson}} potrebbero non essere disponibili in alcuni piani o ambienti.

Puoi anche integrare uno o più modelli personalizzati da {{site.data.keyword.knowledgestudiofull}} con il servizio {{site.data.keyword.discoveryshort}} per fornire arricchimenti di relazioni ed entità personalizzati. Vedi [Integrazione con Watson Knowledge Studio](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-with-wks).

Verranno arricchiti solo i primi 50.000 caratteri di ogni campo JSON selezionato per l'arricchimento.
{: important}

**Nota:** gli arricchimenti {{site.data.keyword.alchemylanguageshort}} sono diventati obsoleti il primo marzo 2018. Se hai delle raccolte esistenti che utilizzano gli arricchimenti {{site.data.keyword.alchemylanguageshort}} devi migrarle agli arricchimenti {{site.data.keyword.nlushort}}. Per informazioni sulla migrazione di raccolte esistenti e di file di configurazione che utilizzano gli arricchimenti {{site.data.keyword.alchemylanguageshort}}, vedi [Migrazione degli arricchimenti a {{site.data.keyword.nlushort}}](/docs/services/discovery?topic=discovery-migrate-nlu#migrate-nlu).

Puoi incrementare ulteriormente i tuoi documenti aggiungendo ulteriori arricchimenti al campo `text` o arricchendo altri campi. Per eseguire questa operazione utilizzando Smart Document Understanding nella strumentazione {{site.data.keyword.discoveryshort}}, apri la scheda **Enrich Fields**. Per eseguire questa operazione per le raccolte create prima di Smart Document Understanding, [crea una configurazione personalizzata](/docs/services/discovery?topic=discovery-configservice#custom-configuration), scegli il campo o i campi che desideri arricchire e seleziona dall'elenco gli arricchimenti {{site.data.keyword.nlushort}} disponibili:

### Entity Extraction
{: #entity-extraction}

Restituisce gli elementi come persone, luoghi e organizzazioni presenti nel testo di input. L'Entity Extraction aggiunge la conoscenza semantica al contenuto per aiutare a comprendere il soggetto e il contesto del testo che si sta analizzando. Le tecniche dell'Entity Extraction si basano su sofisticati algoritmi statistici e sulla tecnologia di elaborazione del linguaggio naturale e sono unici nel settore con il proprio supporto per l'analisi multilingua e la disambiguazione sensibile al contesto. Visualizza l'elenco completo dei tipi e dei sottotipi di entità [qui](/docs/services/discovery?topic=discovery-entity-types-and-subtypes#entity-types-and-subtypes). Puoi inoltre creare e aggiungere un [modello di entità personalizzato](/docs/services/discovery?topic=discovery-configservice#custom-entity-model) con {{site.data.keyword.knowledgestudiofull}}.

Porzione di esempio di un documento arricchito con l'Entity Extraction:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
  "enriched_text": {
    "entities": [
      {
        "count": 1,
        "sentiment": {
          "score": 0
        },
        "text": "Acme Corporation",
        "relevance": 0.98389,
        "type": "Company"
      },
      {
        "count": 1,
        "sentiment": {
          "score": 0
        },
        "text": "Atlanta",
        "relevance": 0.532754,
        "type": "Location",
        "disambiguation": {
          "subtype": [
            "AdministrativeDivision",
            "GovernmentalJurisdiction",
            "OlympicHostCity",
            "PlaceWithNeighborhoods",
            "City"
          ],
          "name": "Atlanta",
          "dbpedia_resource": "http://dbpedia.org/resource/Atlanta"
        }
      },
      {
        "count": 1,
        "sentiment": {
          "score": 0
        },
        "text": "Georgia",
        "relevance": 0.469643,
        "type": "Location",
        "disambiguation": {
          "subtype": [
            "StateOrCounty"
          ]
        }
      }
    ]
  }
}
```
{: codeblock}

Nell'esempio precedente, puoi eseguire la query del tipo di entità accedendo a `enriched_text.entities.type`

`sentiment` viene calcolato per i tipi di entità anche se l'arricchimento **sentiment** non è selezionato. Per ulteriori informazioni sul punteggio delle sensazioni, consulta [Sentiment Analysis](/docs/services/discovery?topic=discovery-configservice#sentiment-analysis).

Il punteggio di `relevance` è compreso tra `0.0` e `1.0`. Più alto è il punteggio, più importante è l'entità. Il campo `disambiguation` contiene le informazioni di disambiguazione per l'entità, che includono le informazioni dell'entità `subtype` e i link alle risorse, se applicabili. `count` è il numero di volte in cui l'entità viene menzionata nel documento.

#### Utilizzo di un modello di entità personalizzato
{: #custom-entity-model}

Se vuoi creare un modello di arricchimento personalizzato, puoi farlo in {{site.data.keyword.knowledgestudiofull}} e importarlo in {{site.data.keyword.discoveryshort}} aggiungendo l'ID nella casella `Custom Model ID` della strumentazione {{site.data.keyword.discoveryshort}}. Per ulteriori informazioni sull'integrazione con {{site.data.keyword.knowledgestudiofull}}, consulta [Integrazione con {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-with-wks). Il modello {{site.data.keyword.knowledgestudiofull}} personalizzato sovrascriverà l'arricchimento Entity Extraction predefinito.

**Nota:** può essere assegnato solo un modello {{site.data.keyword.knowledgestudiofull}} a un arricchimento.

### Relation Extraction
{: #relation-extraction}

Riconosce quando due entità sono correlate e identifica il tipo di relazione. Puoi inoltre creare e aggiungere un [modello di relazione personalizzato](/docs/services/discovery?topic=discovery-configservice#custom-relation-model) con {{site.data.keyword.knowledgestudiofull}}.

Visualizza l'elenco completo dei tipi di relazione [qui](/docs/services/discovery?topic=discovery-relation-types#relation-types).

Porzione di esempio di un documento arricchito con Relation Extraction:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
  "enriched_text": {
    "relations": [
      {
        "type": "locatedAt",
        "sentence": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
        "score": 0.989245,
        "arguments": [
         {
            "text": "Atlanta",
            "location": [
             94,
             101
            ],
            "entities": [
              {
                "type": "GeopoliticalEntity",
                "text": "Atlanta"
              }
            ]
         },
          {
            "text": "Georgia",
            "location": [
             103,
             110
            ],
            "entities": [
              {
                "type": "GeopoliticalEntity",
                "text": "Georgia"
              }
            ]
          }
        ]
      }
    ]
  }
}
```
{: codeblock}

Nell'esempio precedente, puoi eseguire la query del tipo di relazione accedendo a `enriched_text.relations.type`.

Le entità correlate sono elencate in `arguments`. I tipi di entità che possono essere identificati dall'arricchimento di Relation Extraction possono essere trovati [qui](/docs/services/discovery?topic=discovery-relation-types#specific-entity-types).

`score` è compreso tra `0.0` e `1.0`. Più alto è il punteggio, più importante è la relazione.

#### Utilizzo di un modello di relazione personalizzato
{: #custom-relation-model}

Se vuoi creare un modello di arricchimento personalizzato, puoi farlo in {{site.data.keyword.knowledgestudiofull}} e importarlo in {{site.data.keyword.discoveryshort}} aggiungendo l'ID nella casella `Custom Model ID` della strumentazione {{site.data.keyword.discoveryshort}}. Per ulteriori informazioni sull'integrazione con {{site.data.keyword.knowledgestudiofull}}, consulta [Integrazione con {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-with-wks). Il modello {{site.data.keyword.knowledgestudiofull}} personalizzato sovrascriverà l'arricchimento di Relation Extraction predefinito.

**Nota:** può essere assegnato solo un modello {{site.data.keyword.knowledgestudiofull}} a un arricchimento.

### Keyword Extraction
{: #keyword-extraction}

Argomenti importanti nel tuo contenuto che vengono normalmente utilizzati quando esegui l'indicizzazione dei dati, generando i cloud tag o quando effettui una ricerca. Il servizio {{site.data.keyword.discoveryshort}} identifica automaticamente le lingue supportate nel tuo contenuto di input, quindi identifica e classifica le parole chiave in tale contenuto.

Porzione di esempio di un documento arricchito con Keyword Extraction:

```json
  {
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "keywords": [
        {
          "text": "Acme Corporation",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.985203
        },
        {
          "text": "new factory",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.821033
        },
        {
          "text": "stockholders",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.66497
        },
        {
          "text": "title",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.332438
        },
        {
          "text": "Atlanta",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.307723
        },
        {
          "text": "Georgia",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.306485
        }
      ]
    }
  }
```
{: codeblock}

Nell'esempio precedente, puoi eseguire la query del testo della parola chiave accedendo a `enriched_text.keywords.text`

`sentiment` viene calcolato per le parole chiave anche se l'arricchimento **sentiment** non è selezionato. Per ulteriori informazioni sul punteggio delle sensazioni, consulta [Sentiment Analysis](/docs/services/discovery?topic=discovery-configservice#sentiment-analysis).

Il punteggio di `relevance` è compreso tra `0.0` e `1.0`. Più alto è il punteggio, più importante è la parola chiave.

### Category Classification
{: #category-classification}

Categorizza il testo di input, HTML o il contenuto basato sul web in una tassonomia gerarchica fino a cinque livelli di profondità. Livelli più profondi ti consentono di classificare il contenuto in sottosegmenti più accurati e utili. Visualizza l'elenco completo delle categorie [qui](/docs/services/discovery?topic=discovery-cathierarchy#cathierarchy).

Porzione di esempio di un documento arricchito con Category Classification:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "categories": [
        {
          "score": 0.361614,
          "label": "/business and industrial"
        },
        {
          "score": 0.329377,
          "label": "/business and industrial/company/merger and acquisition"
        },
        {
          "score": 0.154254,
          "label": "/business and industrial/business operations/business plans"
        }
      ]
```
{: codeblock}

Nell'esempio precedente, puoi eseguire la query dell'etichetta della categoria accedendo a `enriched_text.categories.label`

`label` è la categoria rilevata. I livelli di gerarchia sono separati da barre. Il punteggio (`score`) per tale categoria sarà compreso tra `0.0` e `1.0`. Più alto è il punteggio, maggiore è la confidenza in tale categoria.

### Concept Tagging
{: #concept-tagging}

Identifica i concetti con i quali il testo di input è associato, in base ad altri concetti e entità presenti in quel testo. Il Concept Tagging comprende come sono correlati i concetti e può identificare i concetti a cui non viene fatto riferimento direttamente nel testo. Ad esempio, se un articolo menziona il CERN e il bosone di Higgs, le funzioni Concepts API identificheranno Large Hadron Collider come un concetto anche se quel termine non viene citato esplicitamente nella pagina. Il Concept Tagging consente un'analisi di livello superiore del contenuto di input rispetto alla semplice identificazione della parola chiave di base.

Porzione di esempio di un documento arricchito con Concept Tagging:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "concepts": [
        {
          "text": "Acme Corporation",
          "relevance": 0.91136,
          "dbpedia_resource": "http://dbpedia.org/resource/Acme_Corporation"
        },
        {
          "text": "Factory",
          "relevance": 0.886784,
          "dbpedia_resource": "http://dbpedia.org/resource/Factory"
        }
      ]
```
{: codeblock}

Nell'esempio precedente, puoi eseguire la query del tipo di testo del concetto accedendo a `enriched_text.concepts.text`

Il punteggio di `relevance` è compreso tra `0.0` e `1.0`. Più alto è il punteggio, più importante è il concetto. Vengono forniti i link alle risorse, se applicabili.

### Semantic Role Extraction
{: #semantic-role-extraction}

Identifica l'oggetto, l'azione e le relazioni dell'oggetto all'interno di frasi nel contenuto di input. Le informazioni sulla relazione possono essere utilizzate per identificare automaticamente i segnali per l'acquisto, gli eventi chiave e altre azioni importanti.

Porzione di esempio di un documento arricchito con Semantic Role Extraction:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
      "enriched_text": {
      "semantic_roles": [
        {
          "subject": {
            "text": "The stockholders",
            "keywords": [
              {
                "text": "stockholders"
              }
            ]
          },
          "sentence": " The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
          "object": {
            "text": "pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia",
            "keywords": [
              {
                "text": "Acme Corporation"
              },
              {
                "text": "new factory"
              },
              {
                "text": "Atlanta"
              },
              {
                "text": "Georgia"
              }
            ],
            "entities": [
              {
                "type": "Company",
                "text": "Acme Corporation"
              },
              {
                "type": "Location",
                "text": "Atlanta",
                "disambiguation": {
                  "subtype": [
                    "AdministrativeDivision",
                    "GovernmentalJurisdiction",
                    "OlympicHostCity",
                    "PlaceWithNeighborhoods",
                    "CityTown",
                    "City"
                  ],
                  "name": "Atlanta",
                  "dbpedia_resource": "http://dbpedia.org/resource/Atlanta"
                }
              },
              {
                "type": "Location",
                "text": "Georgia",
                "disambiguation": {
                  "subtype": [
                    "StateOrCounty"
                  ]
                }
              }
            ]
          },
          "action": {
            "verb": {
              "text": "be",
              "tense": "past"
            },
            "text": "were",
            "normalized": "be"
          }
        }
      ]
```
{: codeblock}

Nell'esempio precedente, puoi eseguire la query del testo dell'oggetto di relazione accedendo a `enriched_text.relations.subject.text`

`sentiment` viene calcolato per le relazioni anche se l'arricchimento **sentiment** non è selezionato. Per ulteriori informazioni sul punteggio delle sensazioni, consulta [Sentiment Analysis](/docs/services/discovery?topic=discovery-configservice#sentiment-analysis). Non estrarrà `entities` o `keywords` (come mostrato nell'esempio) a meno che non selezioni anche gli arricchimenti **entity** e **keyword**. Consulta [Entity Extraction](/docs/services/discovery?topic=discovery-configservice#entity-extraction) e [Keyword Extraction](/docs/services/discovery?topic=discovery-configservice#keyword-extraction) per ulteriori informazioni su questi arricchimenti.

`subject`, `action` e `object` vengono estratti per ogni frase che contiene una relazione.

### Sentiment Analysis
{: #sentiment-analysis}

Identifica l'atteggiamento, le opinioni o le sensazioni nel contenuto che si sta analizzando. Il servizio {{site.data.keyword.discoveryshort}} può calcolare le sensazioni complessive all'interno di un documento, le sensazioni di obiettivi definiti dall'utente, al livello dell'entità, al livello della citazione, le sensazioni direzionali e le sensazioni al livello della parola chiave. La combinazione di queste funzionalità supporta una varietà di casi di utilizzo che vanno dal monitoraggio dei social media all'analisi di tendenza.

Porzione di esempio di un documento arricchito con Sentiment Analysis:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "sentiment": {
        "document": {
        "score": 0.459813,
        "label": "positive"
  }
}
```
{: codeblock}

Nell'esempio precedente, puoi eseguire la query dell'etichetta delle sensazioni accedendo a `enriched_text.sentiment.document.label`

`label` sono le sensazioni generali del documento (`positive`, `negative` o `neutral`). Le sensazioni di `label` si basano sul punteggio (`score`); un punteggio `0.0` indica che il documento è `neutral`, un numero positivo indica che è `positive` e un numero negativo che è `negative`.

### Emotion Analysis
{: #emotion-analysis}

Rileva la rabbia, il disgusto, la paura, la gioia e la tristezza sottintese nel testo inglese. Emotion Analysis può rilevare le emozioni associate a precise frasi, entità o parole chiave, oppure può analizzare il tono emotivo generale del tuo contenuto.

Porzione di esempio di un documento arricchito con l'Emotion Analysis:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "emotion": {
        "document": {
          "emotion": {
          "disgust": 0.102578,
          "joy": 0.626655,
          "anger": 0.02303,
          "fear": 0.018884,
          "sadness": 0.096802
    }
  }
}
```
{: codeblock}

Nell'esempio precedente, puoi eseguire la query dell'emozione `joy` accedendo a `enriched_text.emotion.document.emotion.joy`

L'Emotion Analysis analizza il tuo testo e calcola un punteggio per ogni emozione (rabbia, disgusto, paura, gioia, tristezza) su una scala da `0.0` a `1.0`. Se il punteggio di ogni emozione è ` 0.5 ` o superiore, allora quella emozione è stata rilevata (più alto il punteggio è di `0.5`, maggiore è la pertinenza). Nel frammento mostrato, `joy` ha un punteggio superiore a 0.5, quindi {{site.data.keyword.watson}} ha rilevato la gioia.

**Nota:** l'Emotion Analysis è supportato solo in inglese.

### Element Classification
{: #elements}

Analizza gli elementi (frasi, elenchi, tabelle) nei documenti applicabili per classificare tipi e categorie importanti
Per ulteriori informazioni, consulta [Element Classification](/docs/services/discovery?topic=discovery-element-classification#element-classification).

[Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu) non sarà disponibile se viene utilizzato questo arricchimento.

#### Prezzi dell'arricchimento
{: #enrichment-pricing}

Le informazioni sui prezzi dell'arricchimento sono disponibili su [{{site.data.keyword.Bluemix_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/catalog/services/discovery){: new_window}.

#### Supporto linguistico dell'arricchimento
{: #enrichment-language-support}

Per informazioni sul supporto linguistico del'arricchimento, vedi [Supporto linguistico per {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-language-support#language-support).

### Descrizione della differenza tra entità, concetti e parole chiave
{: #udbeck}

A prima vista, **Entity Extraction**, **Concept Tagging** e **Keyword Extraction** sembrano essere arricchimenti simili. Useremo il testo dagli esempi di arricchimento per mostrare le differenze tra loro.

```json
"text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia."
```
{: codeblock}

Poiché l'arricchimento **Entity Extraction** estrae persone, posti e organizzazioni nel testo di input, **Entity Extraction** restituisce i seguenti tipi di entità:

```json
"type": "City"
"text": "Atlanta"

"type": "Company"
"text": "Acme"

"type": "StateOrCounty"
"text": "Georgia"
```
{: codeblock}

Poiché l'arricchimento **Concept Tagging** comprende come sono correlati i concetti, può identificare i concetti a cui non viene fatto riferimento direttamente nel testo. Ad esempio, se un articolo menziona il CERN e il bosone di Higgs, identificherà Large Hadron Collider come un concetto anche se quel termine non viene citato esplicitamente. Dal momento che il nostro testo del documento di esempio è solo una frase, non ci sono concetti correlati, quindi **Concept Tagging** restituisce i seguenti concetti:

```json
"text": "Acme Corporation"
"text": "factory"
```
{: codeblock}

Dal momento che l'arricchimento **Keyword Extraction** identifica il contenuto normalmente utilizzato durante l'indicizzazione dei dati, la generazione dei cloud tag o la ricerca, **Keyword Extraction** restituisce le seguenti parole chiave:

```json
"text": "Acme Corporation"
"text": "new factory"
"text": "stockholders"
"text": "Atlanta"
"text": "Georgia"
```
{: codeblock}

Questi arricchimenti lavorano insieme per aiutarti a creare migliori query.

## Normalizzazione dei dati
{: #normalizing-data}

Queste informazioni si applicano solo alle raccolte create prima della release di [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu).
{: note}

L'ultimo passo nella personalizzazione del tuo file di configurazione è di fare una ripulitura finale, nota anche come normalizzazione.

Nella sezione **Normalize** della strumentazione {{site.data.keyword.discoveryshort}}:

-   Puoi spostare, unire, copiare o rimuovere i campi.
-   I campi vuoti (campi che non contengono informazioni) verranno eliminati per impostazione predefinita. Puoi modificare questa impostazione con il pulsante di attivazione **Remove empty fields**.

Dopo aver apportato le modifiche, fai clic su **Apply and Save** e poi su **Done**. Tornerai alla schermata **Manage Data**, dove puoi applicare questa configurazione alla raccolta di tua scelta.

**Nota:** non puoi specificare il `data type` (ad esempio: `text` o `date`) dei campi. Durante l'inserimento di un documento, se viene rilevato che un campo non esiste ancora nell'indice, {{site.data.keyword.discoveryshort}} individuerà automaticamente il `data type` di quel campo in base al valore del campo del primo documento indicizzato.

Se utilizzi l'arricchimento **Element Classification**, non puoi eseguire la normalizzazione post-arricchimento.

## Normalizzazione delle entità
{: #normalizing-entities}

### Utilizzo dei selettori CSS per estrarre i campi
{: #using-css}

Puoi eseguire un'ulteriore normalizzazione utilizzando i selettori CSS tramite l'API Discovery.

Se stai inserendo un HTML formato correttamente, puoi normalizzarlo, utilizzare i selettori CSS per estrarre i campi JSON da esso e quindi applicare gli arricchimenti ai campi estratti. Modifica il tuo file di configurazione per abilitare questa funzione. Nello specifico, aggiungi un elemento `extracted_fields` alla gerarchia `conversions/html`, quindi specifica i nomi campo, i selettori CSS e i tipi di campo, come segue:

```json
{
  "name": "Extract JSON config",
  "description": "New configuration enabling extraction of JSON fields from HTML",
  "conversions": {
    ...
    "html": {
      ...
      "extracted_fields": {
        "{field_name_1}": {
          "css_selector": "{CSS_selector_expression_1}",
          "type": "{field_type}"
        },
        ...
        "{field_name_N}": {
          "css_selector": "{CSS_selector_expression_N}",
          "type": "{field_type}"
        }
      }
    ...
    }
  }
}
```
{: codeblock}

Specifica i valori per i nuovi campi nel modo seguente:

-   `field_name` - Il nome del campo che verrà aggiunto all'output JSON.
-   `CSS_selector_expression` - Il selettore CSS che deve essere eseguito nell'HTML di input per estrarre i campi. L'espressione può avere una o più corrispondenze.

    I selettori CSS validi sono quelli specificati dal [parser JSoup ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://jsoup.org/apidocs/org/jsoup/select/Selector.html){: new_window} e il relativo [selector syntax ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://jsoup.org/cookbook/extracting-data/selector-syntax){: new_window}. Un breve elenco viene fornito in [Selettori comuni](/docs/services/discovery?topic=discovery-configservice#common-selectors).
-   `field_type` - `array` o `string`. Se il tipo di campo non è specificato, viene impostato per default su `array`. Tieni presente che il tipo `string` può essere arricchito, ma le informazioni archiviate in un `array` non possono essere arricchite a meno che gli elementi dell'array non vengano prima estratti in campi di testo.

**Avvertenza:** se un selettore CSS corrisponde sia a un nodo principale che a uno o più dei suoi nodi secondari, il contenuto del testo dei nodi verrà duplicato nell'output JSON.

**Nota:** i nomi dei campi devono soddisfare le limitazioni definite in [Requisiti nome campo](/docs/services/discovery?topic=discovery-configref#field_reqs).

Il seguente passaggio JSON mostra la sezione pertinente della configurazione predefinita alla quale aggiungi le informazioni del selettore CSS.

```json
{
  "name": "Default Configuration",
  "description": "The configuration used by default when creating a new collection without specifying a configuration_id.",
  "conversions": {
    ...
    "html": {
      "exclude_tags_completely": [
        "script",
        "sup"
      ],
      "exclude_tags_keep_content": [
        "font",
        "em",
        "span"
      ],
      "exclude_content": {
        "xpaths": []
      },
      "keep_content": {
        "xpaths": []
      },
      "exclude_tag_attributes": [
        "EVENT_ACTIONS"
      ]
    }
    ...
  }
}
```
{: codeblock}

Il seguente passaggio mostra la configurazione con nuovi nome e descrizione, così come l'ubicazione in cui puoi specificare i selettori CSS.

```json
{
  "name": "Extract JSON config",
  "description": "New configuration enabling extraction of JSON fields from HTML",
  "conversions": {
    ...
    "html": {
      "exclude_tags_completely": [
        "script",
        "sup"
      ],
      "exclude_tags_keep_content": [
        "font",
        "em",
        "span"
      ],
      "exclude_content": {
        "xpaths": []
      },
      "keep_content": {
        "xpaths": []
      },
      "exclude_tag_attributes": [
        "EVENT_ACTIONS"
      ],
      "extracted_fields": {
        "{field_name_1}": {
          "css_selector": "{CSS_selector_expression_1}",
          "type": "{field_type}"
        },
        ...
        "{field_name_N}": {
          "css_selector": "{CSS_selector_expression_N}",
          "type": "{field_type}"
        }
      }
    }
  }
  ...
}
```
{: codeblock}

Infine, il seguente passaggio mostra la configurazione dei nuovi nome e descrizione così come alcuni selettori CSS. I selettori corrispondono agli elementi in un esempio HTML che viene descritto più avanti in questa pagina.

```json
{
  "name": "Extract JSON config",
  "description": "New configuration enabling extraction of JSON fields from HTML",
  "conversions": {
    ...
    "html": {
      "exclude_tags_completely": [
        "script",
        "sup"
      ],
      "exclude_tags_keep_content": [
        "font",
        "em",
        "span"
      ],
      "exclude_content": {
        "xpaths": []
      },
      "keep_content": {
        "xpaths": []
      },
      "exclude_tag_attributes": [
        "EVENT_ACTIONS"
      ],
      "extracted_fields": {
        "chapters": {
          "css_selector": ".chapter",
          "type": "array"
        },
        "authors": {
          "css_selector": ".author"
        },
        "authors_str": {
          "css_selector": ".author",
          "type": "string"
        },
        "comments": {
          "css_selector": "[^comments-content]"
        }
      }
    }
  }
  ...
}
```
{: codeblock}

Se carichi il seguente documento HTML in una raccolta che utilizza una configurazione aggiornata, i selettori CSS corrispondono agli attributi e ai valori appropriati nell'HTML.

```html
<html>
  <body>
    <div id="authors">
      <div class="author"><span class="first_name">Jane</span> <span class="last_name">Rain</span></div>
      <div class="author">Joe Snow</div>
  </div>
  <div class="chapter"><h1>The Rain in Spain</h1><p>falls mainly on the plain.</p></div>
  <div class="chapter"><h1>How I Learned to Stop Worrying</h1><p>and love my snowblower.</p></div>
  <span id="comments-section">
    <h4>Comments:</h4>
    <span id="comments-content-1">Rain gives me pain.</span>
    <span id="comments-content-2">All snow must go!</span>
  </span>
</body></html>
```
{: codeblock}

Dopo che il precedente HTML viene inserito e arricchito, il servizio {{site.data.keyword.discoveryshort}} restituisce il seguente JSON:

```json
{
  "extracted_metadata": { ... },
  "html": "...",
  "text": "...",
  "extracted_fields": {
    "authors": [ "Jane Rain", "Joe Snow" ],
    "authors_str": "Jane Rain\n\nJoe Snow",
    "chapters": [ "The Rain in Spain\n\nfalls mainly on the plain.", "How I Learned to Stop Worrying\n\nand love my snowblower." ],
    "comments": [ "Rain gives me pain.", "All snow must go!" ]
  }
}
```
{: codeblock}

Dopo aver deciso quali elementi HTML vuoi estrarre, puoi apportare ulteriori modifiche al file di configurazione per specificare gli arricchimenti che vuoi applicare ad essi.

#### Selettori comuni
{: #common-selectors}

Alcuni selettori CSS comuni includono quanto segue:

  - `tag` — Corrisponde al nome `tag`
  - `.class` — Corrisponde al valore `class`
  - `#id` — Corrisponde al valore `id`
  - `[attribute]` — Corrisponde ad ogni tag con `attribute` specificato, indipendentemente dal valore
  - `[attribute=value]` o `[attribute="value"]` — Corrisponde ai valori `attribute` e `value` specificati

## Suddivisione dei documenti con la segmentazione del documento
{: #doc-segmentation}

In caso di utilizzo di Smart Document Understanding, non utilizzare la segmentazione dei documenti, utilizza la [suddivisione dei documenti](/docs/services/discovery?topic=discovery-sdu#splitting).
{: note}

Puoi suddividere i tuoi documenti Word, PDF e HTML in segmenti basati su tag di intestazione HTML. Una volta suddiviso, ogni segmento è un documento separato che sarà arricchito e indicizzato separatamente. Poiché le query restituiranno questi segmenti come documenti separati, la segmentazione dei documenti può essere utilizzata per:

  - Eseguire aggregazioni su singoli segmenti di un documento. Ad esempio, la tua aggregazione conterà ogni volta che un segmento menziona un'entità specifica, invece di contarle solo una volta per il documento completo.
  - Eseguire la formazione di pertinenza sui segmenti invece che sui documenti, che migliorerà il risultato di riclassificazione.

I segmenti vengono creati quando i documenti vengono convertiti in HTML (i documenti Word e PDF vengono convertiti in HTML prima di essere convertiti in JSON). I documenti possono essere suddivisi in base alle seguenti tag HTML: `h1` `h2` `h3` `h4` `h5` e `h6`.

Considerazioni:

  - Il numero di segmenti per documento è limitato a `250`. Qualsiasi contenuto del documento rimanente dopo i segmenti `249` verrà archiviato all'interno del segmento `250`.

  - Ogni segmento sarà conteggiato sul limite di documenti del tuo piano. {{site.data.keyword.discoveryshort}} indicizzerà i segmenti finché non viene raggiunto il limite del piano. Consulta [Rilevamento dei piani dei prezzi](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans) per i limiti di documenti.

  - Non puoi normalizzare i dati (consulta [Normalizzazione dei dati](/docs/services/discovery?topic=discovery-configservice#normalizing-data)) o utilizza i selettori CSS per estrarre i campi (consulta [Utilizzo dei selettori CSS per estrarre i campi](/docs/services/discovery?topic=discovery-configservice#using-css)) quando utilizzi la segmentazione del documento.

  - I documenti saranno segmentati ogni volta che viene rilevata la tag HTML specificata. Di conseguenza, la segmentazione potrebbe portare a un HTML malformato perché i documenti potrebbero essere suddivisi prima delle tag di chiusura e dopo le tag di apertura.

  - I metadati HTML, PDF e Word, così come tutti i metadati personalizzati, vengono estratti e inclusi nell'indice con ogni segmento. Ogni segmento di un documento includerà metadati identici.

  - La segmentazione del documento non è supportata quando viene specificato l'arricchimento **Element Classification** (`elements`).

  - Il reinserimento di un documento segmentato ha ulteriori considerazioni, consulta [Aggiornamento di un documento segmentato](/docs/services/discovery?topic=discovery-configservice#update-seg).

### Esecuzione della segmentazione
{: #performing-segmentation}

In caso di utilizzo di Smart Document Understanding, non utilizzare la segmentazione dei documenti, utilizza la [suddivisione dei documenti](/docs/services/discovery?topic=discovery-sdu#splitting).
{: note}

La segmentazione viene configurata tramite l'API nella sezione `conversions`.

```json
{
  "configuration_id": "a23c467d-1212-4b3a-5555-93e788a3622a",
  "name": "Example configuration",
  "conversions": {
    "segment": {
      "enabled": true,
      "selector_tags": ["h1", "h2", "h3", "h4", "h5", "h6"]
    }
  }
}
```
{: codeblock}

`enabled` = `true` attiva la segmentazione del documento.

`selector_tags` è un array che specifica le tag di intestazione per cui possono essere segmentati i documenti.

#### Esempio
{: #example-segmentation}

Configurazione:

```json
"conversions": {
  "segment": {
    "enabled": true,
    "selector_tags": ["h1", "h2"]
```
{: codeblock}

Documento HTML originale:

```
<html>
 <head>
 </head>
 <body>
  first line
   <div name="section 1">
    <h1>heading 1</h1>
     <div name="section 2">This is the text that falls under <b>heading 1</b> and should be therefore split into its own segment.
      <h2>heading 2</h2>
      line under heading 2
     </div>
       <h3>heading 3</h3>
       line under heading 3
   </div>
  last line
 </body>
</html>
```
{: codeblock}

Il primo segmento del documento sarà simile a questo:

```json
{
  "id": "94c686c3-a790-4d8d-ba42-2bddf01b311c",
  "segment_metadata": {
    "parent_id": "94c686c3-a790-4d8d-ba42-2bddf01b311c",
    "segment": 1,
    "total_segments": 3
  },
  "extracted_metadata": {
    "title": "Heading 1",
    "sha1": "45ede479df67d78f2205ea7e714843375d3029c0",
    "filename": "doc-with-different-heading-levels.html",
    "file_type": "html"
  },
  "text": "This is the text that falls under heading 1 and should be therefore split into its own segment.",
  "html": "<div name=\"section 2\">This is the text that falls under <b>heading 1</b> and should be therefore split into its own segment."
}
```
{: codeblock}

Tutti i segmenti includono un:

  - `id` - L'`id` di questo segmento.
  - La sezione `segment_metadata` che contiene:
    - `parent_id` - Il `parent_id` è l'ID del documento originale. Per il primo segmento, l'`id` e il `parent_id` saranno identici.
    - `segment` - Il numero di questo segmento.
    - `total_segments` - Il numero totale di segmenti in cui è stato suddiviso il documento.
  - La sezione `extracted_metadata` che contiene:
    - `title` - Il campo `title` viene estratto dal contenuto della tag di intestazione in tale segmento (ad esempio, `Chapter 1`). Se il primo segmento non include una tag di intestazione, `title` sarà `no-title`.
    - `sha1` - Corrisponde al documento originale.
    - `filename` - Corrisponde al documento originale.
    - `file_type` - Corrisponde al documento originale.
  - Campo `text`
  - Campo `html`

### Aggiornamento di un documento segmentato
{: #update-seg}

Se un documento segmentato è stato aggiornato e deve essere nuovamente inserito, può essere sostituito utilizzando il metodo [Update document ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery#update-a-document){: new_window}.

Quando aggiorni un documento segmentato, il documento deve essere caricato utilizzando il metodo POST dell'API `/environments/{environment_id}/collections/{collection_id}/documents/{document_id}`, specificando il contenuto del campo `parent_id` di uno dei segmenti correnti come variabile di percorso `{document_id}`.

Quando si aggiornano, tutti i segmenti saranno sovrascritti, a meno che la versione aggiornata del documento non abbia meno sezioni totali rispetto all'originale. Questi segmenti più vecchi rimarranno nell'indice e possono essere eliminati individualmente utilizzando l'API. Per i dettagli, consulta il [Riferimento API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery#delete-a-document){: new_window}. Puoi identificare quanti segmenti sono stati creati eseguendo la query di `notices`. A ciascun segmento viene assegnato un campo `document_id` che è composto dal `{parent_id}`, seguito da un carattere di sottolineatura, seguito dal numero di segmento.

Se uno dei segmenti del documento che vuoi aggiornare deve essere classificato per la formazione della pertinenza, devi prima eliminare tutti i segmenti di tale documento e poi inserire il documento aggiornato come un nuovo documento. Questo comporterà un nuovo `document_id` per ogni segmento e ogni segmento formato dovrà essere riaggiornato. L'indice preparato diventerà impreciso se non elimini prima il contenuto precedente.

In alternativa, prendi in considerazione di creare un nuovo documento che contiene solo il nuovo contenuto e inseriscilo separatamente.
