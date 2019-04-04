---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-03-07"

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
{:gif: data-image-type='gif'}

# Smart Document Understanding
{: #sdu}

SDU (Smart Document Understanding) è un nuovo modo per formare {{site.data.keyword.discoveryfull}} per estrarre i campi personalizzati nei tuoi documenti. La personalizzazione della modalità di indicizzazione dei tuoi documenti in {{site.data.keyword.discoveryshort}} migliorerà le risposte restituite dalla tua applicazione.

Con SDU, annoti i campi all'interno dei documenti per formare i modelli di conversione personalizzati. Man mano che specifichi le tue annotazioni, Watson impara e inizierà e prevedere le annotazioni. I modelli SDU possono essere esportati e utilizzati su altre raccolte. 

## Tipi di documento e browser supportati
{: #doctypes}

Tipi di documento supportati per Smart Document Understanding: 
-  Piani Lite: PDF, Word, PowerPoint, Excel, JSON\*, HTML\*
-  Piani Advanced: PDF, Word, PowerPoint, Excel, PNG\*\*, TIFF\*\*, JPG\*\*, JSON\*, HTML\* 

\* I documenti JSON e HTML sono supportati da {{site.data.keyword.discoveryfull}} ma non possono essere modificati utilizzando l'editor SDU. Per modificare la configurazione di documenti HTML e JSON, devi utilizzare l'API. Per ulteriori informazioni, vedi la [Guida di riferimento API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery/){: new_window}.

\*\* I singoli file immagine (PNG, TIFF, JPG) vengono sottoposti a scansione e l'eventuale testo viene estratto. Anche le immagini PNG, TIFF e JPEG integrate in file PDF, Word, PowerPoint ed Excel verranno sottoposte a scansione e l'eventuale testo viene estratto.

Browser supportati: Chrome e Firefox.

## Utilizzo dell'editor Smart Document Understanding
{: #annotate}

L'editor SDU è disponibile solo per le nuove raccolte che contengono tipi di documento supportati e non hanno applicato l'arricchimento Element Classification. Le raccolte private esistenti utilizzeranno il metodo di configurazione originale.Se desideri utilizzare l'editor SDU su una raccolta esistente, dovrai creare una nuova raccolta e caricare tali documenti in essa. Se non desideri utilizzare l'editor SDU, puoi impostare la tua configurazione utilizzando l'API; vedi la [Guida di riferimento API![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery/){: new_window}.
{: important}

Le funzioni dell'editor SDU sono disponibili solo nella strumentazione {{site.data.keyword.discoveryshort}}. non sono disponibili nell'API.
{: note}

Navigazione nell'editor Smart Document Understanding:

Se non ha ancora creato un'istanza e un ambiente {{site.data.keyword.discoveryshort}}, vedi [Introduzione](/docs/services/discovery?topic=discovery-getting-started#getting-started) per le istruzioni.
{: tip}

1. Nella schermata **Manage Data**, fai clic sul pulsante **Upload your own data** e crea una nuova raccolta privata in {{site.data.keyword.discoveryshort}}.
1. Se lo desideri, trascina e rilascia i documenti nella tua raccolta oppure fai clic su **browse from computer** per caricare i documenti. Una volta completato il caricamento, vengono visualizzate le seguenti informazioni:
   -  I campi identificati dai tuoi documenti.
   -  Gli arricchimenti applicati ai tuoi documenti. Gli arricchimenti Entity Extraction, Sentiment Analysis, Category Classification e Concept Tagging vengono applicati automaticamente al campo `text` da {{site.data.keyword.discoveryshort}} (a meno che tu non stia importando i documenti utilizzando un connettore). Puoi aggiungere (o rimuovere) degli arricchimenti aggiuntivi al campo `text`.
   -  Delle query pre-create che puoi eseguire immediatamente.
1. Fai clic su **Configure data** nella parte superiore destra. 
1. Nella schermata **Configure data**, ci saranno tre schede: **Identify fields**, **Manage fields** e **Enrich fields**.

   - **Identify fields** contiene l'editor SDU. Questa scheda sostituisce sia la scheda **Convert** che quella **Normalize** nella schermata {{site.data.keyword.discoveryshort}} originale. 
   - **Manage fields** elenca tutti i campi indicizzati (tutti i campi sono indicizzati per impostazione predefinita). Disattiva tutti i campi che non desideri indicizzare. Ad esempio, i tuoi PDF potrebbero contenere un'intestazione o un piè di pagina ricorrente che non contiene informazioni utili e puoi quindi escludere tali campi dall'indice. Qui puoi anche suddividere i documenti sulla base dei campi; vedi [Suddivisione dei documenti](/docs/services/discovery?topic=discovery-sdu#splitting).
   - **Enrich fields** è identico alla scheda **Enrich** nella schermata originale. Per ulteriori informazioni sugli arricchimenti, vedi [Aggiunta di arricchimenti](/docs/services/discovery?topic=discovery-configservice#adding-enrichments). L'opzione **Upload sample documents** non è disponibile con le raccolte SDU.

   Se non hai caricato alcun documento in precedenza, ritorna alla schermata **Overview** facendo clic sul nome della tua raccolta nella parte superiore sinistra oppure fai clic sull'icona ![Manage Data](/images/icon_yourData.png) e scegli la tua raccolta. Trascina e rilascia i documenti nella tua raccolta oppure fai clic su **browse from computer**. Dopo che hai eseguito un caricamento iniziale, il pulsante **Upload documents** verrà visualizzato nella parte superiore destra.
   {: important}

   Quando utilizzi Smart Document Understanding, può essere arricchito solo il campo `text`. Non provare ad arricchire qualsiasi altro campo.
   {: important}

1. Apri la scheda **Identify fields**. Nell'editor Smart Document Understanding verrà automaticamente caricato un massimo di venti (20) documenti dalla tua raccolta.

La barra degli strumenti in alto ti consentirà di:
- Scegliere un documento da annotare
- Spostarti nel documento visualizzato
- Regolare la vista della pagina (`single page view`, `zoom in`, `zoom out`), `clear changes` e `export/import models`). Fai clic su `single page view` per alternare la visualizzazione - puoi visualizzare le tue annotazioni e il documento separatamente o insieme.

Puoi anche eseguire la ricerca per l'indicizzazione di origini dati Box, Salesforce, Microsoft SharePoint Online, IBM Cloud Object Storage e Microsoft SharePoint 2016 oppure eseguire una ricerca per l'indicizzazione web con la strumentazione {{site.data.keyword.discoveryshort}}. Fai clic sul pulsante **Connect a data source** e consulta [Connessione alle origini dati](/docs/services/discovery?topic=discovery-sources#sources) per ulteriori informazioni. Se crei una raccolta utilizzando questo metodo, non verrà applicato automaticamente alcun arricchimento.
{: tip}

## Come annotare un documento
{: #documents}

**Nota:** le tabelle sono annotate in un passo separato.

Prima di iniziare l'annotazione, vedi [Prassi ottimali per l'annotazione di documenti e tabelle](/docs/services/discovery?topic=discovery-sdu#bestpractices).

1. Una serie di campi predefinita sarà visualizzata a destra del tuo documento. I campi disponibili sono `answer`, `author`, `footer`, `header`, `question`, `subtitle`, `table_of_contents`, `text` e `title`. Se desideri creare una o più etichette di campo personalizzate nuove, fai clic su **Create new**. Sei limitato al seguente numero di etichette personalizzate: piani Lite - `0`, piani Advanced - `5`, piani Premium - `20`.
1. Fai clic su un'etichetta di campo sulla destra per attivarla.
1. Fai clic sul contenuto che rappresenta tale campo nell'editor SDU. Verrà evidenziato. 
   - In alternativa, puoi selezionare un'etichetta di campo sulla destra e trascinarla nel contenuto nell'editor SDU. 
   - Per cancellare una modifica, fai clic sul pulsante **Clear change** sulla barra degli strumenti.
1. Fai clic su **Submit**.
   **Nota:** man mano che specifichi le tue annotazioni, Watson impara e inizierà e prevedere le annotazioni. Continua ad annotare finché Watson non identificherà i campi in modo corretto e congruente.
1. Dopo che hai completato la specifica di annotazioni, fai clic su **Apply changes to collection**. Viene visualizzata la schermata **Upload your documents**. Ricarica i documenti nella tua raccolta. Una volta completato il caricamento, verrai reindirizzato alla schermata **Manage Data**.

Campo | Definizione  
------ | ------ 
answer | In una coppia D/R (spesso in una domanda frequente), la risposta alla domanda.
author | Nome dell'autore (o degli autori).
footer | Utilizza questa tag per denotare le metainformazioni sul documento (quali il numero pagina o i riferimenti) che sono visualizzate nella parte inferiore della pagina.
header | Utilizza questa tag per denotare le metainformazioni sul documento che sono visualizzate nella parte superiore della pagina.
question | In una coppia D/R (spesso in una domanda frequente), la domanda.
subtitle | Il titolo secondario del documento in fase di annotazione. 
table_of_contents | Utilizza questa tag sugli elenchi contenuti nel sommario del documento.
text | Utilizza questa tag per il testo di copia standard, inclusi i paragrafi, le definizioni o qualsiasi insieme di parole che non sia un titolo, parte di una tabella, una risposta, un autore, un sottotitolo, un'intestazione o un piè di pagina. 
title | Il titolo principale del documento in fase di annotazione.

## Come annotare una tabella
{: #tables}

L'annotazione di tabella è nella release beta. Una dichiarazione che spiega le funzioni beta è disponibile [qui](/docs/services/discovery?topic=discovery-release-notes#beta-features).
{: important}

Prima di iniziare l'annotazione, vedi [Prassi ottimali per l'annotazione di documenti e tabelle](/docs/services/discovery?topic=discovery-sdu#bestpractices).

1. Seleziona il campo `table` dal lato destro dell'editor SDU e seleziona quindi la tabella nel documento. 
1. Passa il puntatore del mouse sulla tabella per visualizzare il pulsante **Annotate table**. Fai clic sul pulsante per aprire l'editor di tabella.
1. Per prima cosa, delinea la tabella:
   - Seleziona il campo `column`.
   - Fai clic su una colonna nella tabella per attivarla.
   - Seleziona il campo `row`.
   - Fai clic su una riga nella tabella per attivarla.

   La delineazione della tabella verrà visualizzata nell'anteprima della tabella sulla sinistra.

   **Nota:** man mano che annoti le tabelle, Watson impara e inizierà e prevedere le annotazioni. 
1. Etichetta quindi il contenuto all'interno della tabella.
1. Dopo che hai completato l'annotazione della tabella, fai clic su **Done annotating**.
1. Fai clic su **Apply changes to collection.** Viene visualizzata la schermata **Upload your documents**. Ricarica i documenti nella tua raccolta. Una volta completato il caricamento, verrai reindirizzato alla schermata **Manage Data**.

Utilizza questo video come una guida ![video sull'annotazione delle tabelle](images/SDU_table_demo.gif){: gif}

Campo | Definizione  
------ | ------ 
body | Qualsiasi cella non di intestazione contenente informazioni
column header | La cella di intestazione (se presente) per ogni colonna nella tabella 
multi-column header | Qualsiasi cella di intestazione che si estende a più di una colonna
row title | L'intestazione di colonna per la colonna delle intestazioni riga (se presente)
row header | L'etichetta riga (se presente) per ogni riga nella tabella
multi-row header | Qualsiasi etichetta di riga che si estende a più di una riga

## Suddivisione di documenti
{: #splitting}

La scheda **Manage fields** contiene l'opzione per migliorare i risultati della tua query suddividendo i tuoi documenti (**Improve query results by splitting your documents**). Questa opzione ti consente di suddividere i tuoi documenti in segmenti in base a un nome di campo. Una volta suddiviso, ciascun documento è un documento separato che verrà arricchito, indicizzato e restituito come un risultato della query separato. 

I documenti vengono suddivisi in base a un singolo nome di campo, ad esempio: `title`, `author`, `question`. 

Considerazioni:

  - Il numero di segmenti per documento è limitato a `250`. Qualsiasi contenuto del documento rimanente dopo i segmenti `249` verrà archiviato all'interno del segmento `250`.

  - Ogni segmento sarà conteggiato sul limite di documenti del tuo piano. {{site.data.keyword.discoveryshort}} indicizzerà i segmenti finché non viene raggiunto il limite del piano. Consulta [Rilevamento dei piani dei prezzi](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans) per i limiti di documenti.

  - I metadati PDF e Word, così come tutti i metadati personalizzati, vengono estratti e inclusi nell'indice con ogni segmento. Ogni segmento di un documento includerà metadati identici.

  - Se un documento suddiviso è stato aggiornato e deve essere ricaricato, deve essere sostituito utilizzando il metodo [Update document ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery#update-a-document){: new_window}.Il documento deve essere caricato utilizzando il metodo POST dell'API `/environments/{environment_id}/collections/{collection_id}/documents/{document_id}`, specificando il contenuto del campo `parent_id` di uno dei segmenti correnti come variabile di percorso `{document_id}`. Tutti i segmenti saranno sovrascritti, a meno che la versione aggiornata del documento non abbia meno sezioni totali rispetto all'originale. Questi segmenti più vecchi rimarranno nell'indice e possono essere eliminati individualmente utilizzando l'API. Vedi la [Guida di riferimento per le API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery#delete-a-document){: new_window} per i dettagli. 

## Importazione ed esportazione di modelli
{: #import}

Dopo che hai definito un modello con l'editor SDU, puoi salvarlo e riutilizzarlo su altre raccolte.

Puoi importare o esportare il tuo modello SDU completato utilizzando la barra degli strumenti nella parte superiore dell'editor. Fai clic sull'ultima icona e scegli `Import model` o `Export model`.

I modelli esportati hanno l'estensione file `.sdumodel`. 

L'uso previsto di un modello importato è senza ulteriori annotazioni. Il modello sarà completamente sovrascritto se continui ad annotarlo dopo l'importazione. Se intendi importare un modello in una nuova raccolta, è buona prassi creare una nuova raccolta che contiene solo 1 documento, importare il modello e caricare quindi il resto dei tuoi documenti.

## Prassi ottimali per l'annotazione di documenti e tabelle
{: #bestpractices}

L'annotazione di tabella è nella release beta. Una dichiarazione che spiega le funzioni beta è disponibile [qui](/docs/services/discovery?topic=discovery-release-notes#beta-features).
{: important}

- Attieniti a tutte le linee guida e utilizza un'etichettatura congruente su tutti i documenti
- Non etichettare lo spazio vuoto
- Utilizza le etichette `image` su immagini e diagrammi
- Non trattare il testo **in grassetto**, _in corsivo_ o sottolineato in modo diverso. L'etichetta è basata sul contesto, non sullo stile. 
- Quando etichetti un documenti, lavora dalla prima pagina all'ultima.
- Se etichetti in modo non corretto un elemento, scegli un'altra etichetta per l'elemento per sovrascrivere quella di prima.
- Le pagine possono essere inoltrate in qualsiasi momento. Assicurati che tutta l'etichettatura appropriata sia completa, prima di eseguire l'inoltro.
- I documenti e le tabelle che sembra abbiano del testo che si sovrappone ad altro testo sono considerati a “doppia sovrapposizione” e non possono essere annotati. Segnala questi documenti al tuo amministratore.
- I documenti e le tabelle che contengono più colonne di testo su una singola pagina non possono essere annotati. Segnala questi documenti al tuo amministratore.
- Le note a piè di pagina devono essere etichettate solo quando appaiono in fondo alla pagina e si fa riferimento ad esse nel corpo principale del testo nel documento.
- Le note che appaiono all'interno di sezioni o elenchi (ad esempio esplicitamente denominate come “Note”) devono essere etichettate come `text`.
- Se non sei sicuro che la tabella sia stata etichettata correttamente e il riquadro dell'anteprima smette di rispondere, la pagina deve essere ricaricata nel tuo browser e devi rietichettare la tabella per garantire la correttezza.

