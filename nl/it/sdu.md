---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-10"

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

# Smart Document Understanding
{: #sdu}

SDU (Smart Document Understanding) è un nuovo modo per annotare i tuoi documenti in {{site.data.keyword.discoveryfull}}. 

L'editor semplifica la formazione di modelli di conversione personalizzati. La personalizzazione della modalità di indicizzazione dei tuoi documenti in Discovery migliorerà le risposte restituite per la tua applicazione.

SDU è in release beta. Una dichiarazione che spiega le funzioni beta è disponibile [qui](/docs/services/discovery/release-notes.html#beta-features).

## Tipi di documento e browser supportati
{: #doctypes}

Tipi di documento supportati: PDF, Word, HTML. I documenti JSON sono supportati da {{site.data.keyword.discoveryfull}} ma non si aprono nell'editor SDU perché sono documenti strutturati.

Browser supportati per questa release beta: Chrome e Firefox

## Come annotare i tuoi documenti
{: #annotate}

Per aprire l'editor Smart Document Understanding:

1. Apri {{site.data.keyword.discoveryfull}} utilizzando il link beta.
1. Apri una raccolta di dati privata e, nella schermata **Manage Data**, fai clic su **Go to Data Settings**. 
1. Nella schermata **Data Settings**, ci saranno due schede: **Extract fields** e **Enrich fields**.

   - **Extract fields** contiene l'editor SDU. Questa scheda sostituisce sia **Convert** che **Normalize** nella tua schermata {{site.data.keyword.discoveryshort}} originale. 
   - **Enrich fields** è identico alla scheda **Enrich** nella schermata originale. Per ulteriori informazioni sugli arricchimenti, vedi [Aggiunta di arricchimenti](/docs/services/discovery/building.html#adding-enrichments). L'opzione **Upload sample documents** non è disponibile in **Enrich fields** perché non è necessaria.

1. Venti (20) documenti dalla tua raccolta saranno caricati automaticamente sotto la scheda **Extract fields** nell'editor Smart Document Understanding.

La barra degli strumenti in alto ti consentirà di:
- Scegliere un documento
- Spostarti nel documento visualizzato
- Regolare la vista della pagina (`single page view`, `zoom in`, `zoom out`), `clear changes` e `export/import models`. Fai clic su `single page view` per passare a una schermata che visualizzerà le tue annotazioni e il documento separatamente. 

### Annotazione di un documento nell'editor SDU
{: #documents}

**Nota:** le tabelle sono annotate in un passo separato.

Prima di iniziare l'annotazione, vedi [Prassi ottimali per l'etichettatura di documenti e tabelle](/docs/services/discovery/sdu.html#bestpractices).

1. Una serie di campi predefinita sarà visualizzata a destra del tuo documento. (Per la versione beta, non puoi creare campi personalizzati ma questa funzione sarà disponibile in futuro). I campi disponibili sono `answer`, `author`, `footer`, `header`, `question`, `subtitle`, `table_of_contents`, `text` e `title`.
1. Fai clic su un nome campo sulla destra per attivarlo.
1. Fai clic sul contenuto che rappresenta tale campo nell'editor SDU. Verrà evidenziato. 
   - In alternativa, puoi selezionare un nome campo sulla destra e trascinarlo al contenuto nell'editor SDU. 
   - Per cancellare una modifica, fai clic sul pulsante **Clear change** sulla barra degli strumenti.
1. Fai clic su **Submit**.
   **Nota:** man mano che specifichi le tue annotazioni, Watson impara e inizierà e prevedere le annotazioni. Continua ad annotare finché Watson non identificherà i campi in modo corretto e congruente.
1. Dopo che hai completato la specifica di annotazioni, fai clic su **Apply changes to collection**. Viene visualizzata la schermata **Upload your documents**. (Questo cambierà dopo la versione beta).Puoi ora caricare i tuoi documenti in modo che le impostazioni aggiornate vengano applicate all'intera raccolta. Una volta completato il caricamento, verrai reindirizzato alla schermata **Manage Data**.


Campo | Definizione  
------ | ------ 
answer | In una coppia D/R (spesso in una domanda frequente), la risposta alla domanda.
author | Nome dell'autore (o degli autori).
footer | Utilizza questa tag per denotare le metainformazioni sul documento (quali il numero pagina o i riferimenti) che sono visualizzate nella parte inferiore della pagina.
header | Utilizza questa tag per denotare le metainformazioni sul documento che sono visualizzate nella parte superiore della pagina.
question | In una coppia D/R (spesso in una domanda frequente), la domanda.
subtitle | Il titolo secondario del documento in fase di annotazione. Utilizza questa etichetta solo una volta per ogni documento.
table-of-contents | Utilizza questa tag sugli elenchi contenuti nel sommario del documento.
text | Utilizza questa tag per il testo di copia standard, inclusi i paragrafi, le definizioni o qualsiasi insieme di parole che non sia un titolo, parte di una tabella, una risposta, un autore, un sottotitolo, un'intestazione o un piè di pagina. 
title | Il titolo principale del documento in fase di annotazione. Utilizza questa etichetta solo una volta per ogni documento.

### Annotazione di una tabella nell'editor SDU
{: #tables} 

1. Seleziona il campo `table` sulla destra, quindi seleziona la tabella nell'editor SDU. 
1. Passa il puntatore del mouse sulla tabella nell'editor SDU per visualizzare il pulsante **Annotate table**. Fai clic sul pulsante per aprire l'editor di tabella.
1. Per prima cosa, delinea la tabella:
   - Seleziona il campo `column`.
   - Fai clic su una colonna nella tabella per attivarla.
   - Seleziona il campo `row`.
   - Fai clic su una riga nella tabella per attivarla.

   La delineazione della tabella verrà visualizzata nell'anteprima della tabella sulla sinistra.

   **Nota:** puoi fare clic su **Predict** per visualizzare una previsione del modello della tua annotazione di tabella.
1. Etichetta quindi il contenuto all'interno della tabella.
1. Dopo che hai completato l'annotazione della tabella, fai clic su **Done annotating**.
1. Fai clic su **Apply changes to collection.** Viene visualizzata la schermata **Upload your documents**. (Questo cambierà dopo la versione beta). Una volta completato il caricamento, verrai reindirizzato alla schermata **Manage Data**.

Campo | Definizione  
------ | ------ 
table body | Qualsiasi cella non di intestazione contenente informazioni
column header | La cella di intestazione (se presente) per ogni colonna nella tabella 
multi-column header | Qualsiasi cella di intestazione che si estende a più di una colonna
subsection title | L'intestazione di colonna per la colonna delle intestazioni riga (se presente)
row header | L'etichetta riga (se presente) per ogni riga nella tabella
multi-row header | Qualsiasi etichetta di riga che si estende a più di una riga

## Prassi ottimali per l'etichettatura di documenti e tabelle
{: #bestpractices}

- Attieniti a tutte le linee guida e utilizza un'etichettatura congruente su tutti i documenti
- Non etichettare lo spazio vuoto
- Non etichettare diagrammi e immagini
- Non elaborare il testo **in grassetto**, _in corsivo_ o sottolineato differentemente; l'etichetta è basata sul contesto, non sullo stile. 
- Quando etichetti un documenti, lavora dalla prima pagina all'ultima. Ciascuna pagina deve essere inoltrata, anche se non è stato etichettato nulla. 
- Se etichetti in modo non corretto un elemento, scegli un'altra etichetta per l'elemento per sovrascrivere quella di prima.
- Le pagine possono essere inoltrate in qualsiasi momento. Assicurati che tutta l'etichettatura appropriata sia completa, prima di eseguire l'inoltro.
- Non utilizzare la funzione di zoom sul tuo browser quando etichetti i documenti.
- I documenti e le tabelle che sembra abbiano del testo che si sovrappone ad altro testo sono considerati a “doppia sovrapposizione” e non possono essere annotati. Segnala questi documenti al tuo amministratore.
- I documenti e le tabelle che contengono più colonne di testo su una singola pagina non possono essere annotati. Segnala questi documenti al tuo amministratore.
- Le note a piè di pagina devono essere contrassegnate come tali solo quando appaiono in fondo alla pagina e si fa riferimento ad esse nel corpo principale del testo nel documento.
- Le note che appaiono all'interno di sezioni o elenchi (ad esempio esplicitamente denominate come “Note”) devono essere etichettate come `text`.
- Se non sei sicuro che la tabella sia stata etichettata correttamente e il riquadro dell'anteprima smette di rispondere, la pagina deve essere ricaricata nel tuo browser e devi rietichettare la tabella per garantire la correttezza.

