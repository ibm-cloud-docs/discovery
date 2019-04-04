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

# Introduzione
{: #getting-started}

In questa breve esercitazione, introdurremo la strumentazione {{site.data.keyword.discoveryshort}} e illustreremo il processo di creazione di una raccolta dati privata e la sua ricerca.
{: shortdesc}

Se preferisci utilizzare l'API, consulta [Introduzione all'API](/docs/services/discovery?topic=discovery-gs-api#gs-api).
{: tip}

## Prima di iniziare
{: #before-you-begin-tool}
{: hide-dashboard}

Ti serve un'istanza del servizio per iniziare.
{: hide-dashboard}

1.  {: hide-dashboard} Vai alla pagina [{{site.data.keyword.discoveryshort}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/catalog/services/discovery) nel catalogo {{site.data.keyword.cloud_notm}}.

    L'istanza del servizio viene creata nel gruppo di risorse predefinito (**default**) se non ne scegli uno diverso e *non può* essere modificato in seguito. Questo gruppo è sufficiente per provare il servizio.

    Se stai creando un'istanza per un utilizzo più impegnativo, scopri di più sui [gruppi di risorse
![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/docs/resources/bestpractice_rgs.html#bp_resourcegroups){: new_window}.
1.  {: hide-dashboard}Registrati per un account {{site.data.keyword.cloud_notm}} gratuito o accedi.
1.  {: hide-dashboard} Fai clic su **Create**.

## Passo 1: avvia la strumentazione
{: #launch-the-tooling}

Dopo che hai creato un'istanza del servizio {{site.data.keyword.discoveryshort}}, vieni portato al tuo elenco di servizi.
{: hide-dashboard}

1.  {: hide-dashboard} Fai clic sulla istanza del servizio {{site.data.keyword.discoveryshort}} che hai creato per andare al dashboard del servizio.
1.  Nella pagina **Manage**, fai clic su **Launch tool**. Se ti viene richiesto di eseguire l'accesso alla strumentazione, fornisci le tue credenziali {{site.data.keyword.cloud_notm}}.

<!-- To do: Add screenshot for developer console -->

## Passo 2: crea una raccolta
{: #create-a-collection-tool}

Il primo passo da compiere nella strumentazione {{site.data.keyword.discoveryshort}} è quello di creare una raccolta di dati.

Una raccolta è un insieme dei tuoi documenti. *Perché dovrei volere più di una raccolta?* Ci sono alcune ragioni:

- Potresti volere più raccolte per separare i risultati per destinatari diversi.
- I dati potrebbero essere così diversi che non ha senso eseguirne la query contemporaneamente.

Anche la raccolta dati {{site.data.keyword.discoverynewsshort}} pubblica e pre-arricchita è disponibile per il tuo utilizzo. È pronta per l'esecuzione di query e puoi iniziare a creare query su di essa immediatamente. Non puoi regolare la configurazione o aggiungere i documenti a {{site.data.keyword.discoverynewsshort}}.

1.  Fai clic su ![Environment details](images/env_icon.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> e scegli **Create environment**.
1.  Quando il tuo ambiente è pronto, fai clic sul pulsante **Upload your own data**, dopodiché puoi dare un **Nome alla tua nuova raccolta**. Denomina la tua raccolta **InstallDocs**.

    Quando crei una collezione, sotto **Advanced**, hai l'opzione di scegliere un file di configurazione denominato **Default Contract Configuration**. Questa configurazione supporta solo l'arricchimento Element Classification, che può essere utilizzato per estrarre parte, natura e categoria dagli elementi nei PDF. Vedi [Element Classification](/docs/services/discovery?topic=discovery-element-classification#element-collection) per i dettagli. Non scegliere questa opzione per questa esercitazione.

Puoi anche eseguire la ricerca per l'indicizzazione di origini dati Box, Salesforce, Microsoft SharePoint Online, IBM Cloud Object Storage e Microsoft SharePoint 2016 oppure eseguire una ricerca per l'indicizzazione web con la strumentazione {{site.data.keyword.discoveryshort}}. Fai clic sul pulsante **Connect a data source** e consulta [Connessione alle origini dati](/docs/services/discovery?topic=discovery-sources#sources) per ulteriori informazioni.
{: tip}

## Passo 3: scarica il documento di esempio ed esegui il caricamento nella tua raccolta
{: create-custom-configuration}

1.  Scarica questo documento PDF di esempio: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/watsonexplorerinstall.pdf" download>Guida all'installazione di Watson Explorer<img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno"></a>. Vedi [Tipi di documento supportati](/docs/services/discovery?topic=discovery-sdu#doctypes) per l'elenco completo di tipi di documento supportati in {{site.data.keyword.discoveryshort}}. 

    In alcuni browser, i link si aprono in una nuova finestra invece di essere salvati localmente. Se questo si verifica, seleziona `Salva con nome` nel menu `File` del tuo browser per salvare una copia del file.
    {: tip}

1.  Carica il documento nella tua raccolta. Trascinalo e rilascialo nella tua raccolta oppure fai clic su **browse from computer** per caricare i documenti. Una volta completato il caricamento, vengono visualizzate le seguenti informazioni:
    -  Il numero di documenti (1).
    -  I campi identificati dal tuo documento. Dovresti vedere un singolo campo identificato, `text`. Identificheremo dei campi aggiuntivi tra poco.
    -  Gli arricchimenti applicati al tuo documento. Gli arricchimenti Entity Extraction, Sentiment Analysis, Category Classification e Concept Tagging vengono applicati automaticamente al campo `text` da {{site.data.keyword.discoveryshort}}. Ulteriori informazioni sugli arricchimenti sono disponibili [qui](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)). 
    -  Delle query pre-create che puoi eseguire immediatamente.
1.  Proviamo una rapida query in linguaggio naturale per stabilire una linea di base di reciproca intesa. Fai clic su **Build your own query** nella parte inferiore destra.
1.  Nella schermata **Build queries**, fai clic su **Search for documents** e quindi su **Use natural language**. Immetti `What are the minimum hardware requirements` e fai clic sul pulsante **Run query**. Fai clic sulla scheda **JSON** sulla destra. Il risultato non è così preciso come potrebbe essere, quindi miglioriamolo con Smart Document Understanding.
1.  Fai clic sul nome della raccolta (**InstallDocs**) nella parte superiore sinistra per ritornare alla schermata **Overview**.  
 
## Passo 4: annota il tuo documento
{: #upload-your-documents}

Per ulteriori informazioni sull'annotazione di documenti, vedi [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu).
{: tip}

1.  Fai clic su **Configure data** nella parte superiore destra. 
1.  Nella schermata **Configure data**, ci saranno tre schede: **Identify fields**, **Manage fields** e **Enrich fields**.
1.  Il manuale `Watson Explorer Installation Guide` viene visualizzato ed è pronto per le annotazioni nella scheda **Identify fields**. Tutti i campi disponibili (`answer`, `author`, `footer`, `header`, `question`, `subtitle`, `table_of_contents`, `text` e `title`) vengono visualizzati nell'elenco **Field labels** sulla destra. Se acquisti un piano Advanced o Premium, puoi creare delle tue etichette personalizzate.

    Poiché l'intero documento è attualmente identificato come `text`, gli indicatori sul lato destro sono interamente in giallo. Man mano che esegui le annotazioni (e il sistema inizia a prevederle), i colori vengono aggiornati.
    {: tip}

1.  Fai clic su `title` e seleziona quindi l'indicatore accanto a `Installation and Integration Guide`. Fai clic sul pulsante **Submit page**.
1.  Nell'anteprima della pagina sulla sinistra, fai clic sulla pagina 3. Nota che `title` è già stato previsto per questa pagina. Fai clic sul pulsante **Submit page**.
1.  Sulla pagina 4, seleziona l'etichetta `footer` e seleziona l'indicatore accanto al piè di pagina. Fai clic sul pulsante **Submit page**.
1.  Sulle pagine 5 e 6, annotata i piè di pagina con l'etichetta `footer`. Inoltra ciascuna pagina. Fai clic su qualche altra pagina; noterai che il piè di pagina è stato previsto correttamente da {{site.data.keyword.discoveryshort}}. Annota i titoli (`title`) (allineati lungo il margine sinistro) e i sottotitoli (`subtitle`) (rientrati) sulle pagine 7, 9 e 10 e inoltra ciascuna pagina singolarmente.
1.  Fai clic su qualche altra pagina e controlla i titoli e i sottotitoli previsti. Se qualcuno ha bisogno di essere modificato, annota queste pagine e fai clic sul pulsante **Submit page**.
1.  Ora fai clic sulla scheda **Manage fields** e, sotto **Improve query results by splitting your documents**, suddividi il documento in base a `subtitle`. 
1.  Le annotazioni dovrebbero essere sufficienti, per ora. Fai clic sul pulsante **Apply changes to collection** nella parte superiore destra. Viene visualizzata una finestra di dialogo **Upload your documents**. Seleziona il file `watsonexplorerinstall.pdf` e caricalo. Tale operazione applica tutte le annotazioni al tuo indice. Una volta terminata l'indicizzazione, viene aperta la schermata **Overview**. Dovresti ora vedere più di 30 documenti e 4 campi identificati dai tuoi dati: `footer`, `subtitle`, `text` e `title`. (Se le modifiche non vengono visualizzate entro qualche minuto, aggiorna la finestra del browser).

    Puoi escludere dei campi (come ad esempio `footer`) dall'indicizzazione aprendo la scheda **Manage fields** e impostando tali campi su `off`.
    {: tip}

## Passo 5: esecuzione di query
{: #build-a-query}

1.  Fai clic su **Build your own query** nella parte inferiore destra.
1.  Nella schermata **Build queries**, fai clic su **Search for documents** e quindi su **Use natural language**. Immetti `What are the minimum hardware requirements` e fai clic sul pulsante **Run query**.  
1.  Fai clic sulla scheda **JSON** sulla destra. Guarda il testo (`text`) sotto `results`. Le risposte restituite per la query sono molto più precise.

Ulteriori risorse:
-  Per ulteriori informazioni sullo schema dei dati dei tuoi documenti, fai clic sull'icona **View Data Schema** sull'estrema sinistra o fai clic sulla scheda **JSON**. Per i dettagli, vedi lo [Schema di dati Discovery](/docs/services/discovery?topic=discovery-query-concepts#discovery-schema).
-  Fai clic sul pulsante **Use a sample query** per provare delle query di esempio scritte in {{site.data.keyword.discoveryshort}} Query Language.

## Passi successivi
{: #next-steps-tool}

Ora hai un'istanza del servizio {{site.data.keyword.discoveryshort}} compilata e funzionante. Puoi ora iniziare a personalizzare la tua raccolta aggiungendo ulteriori documenti e arricchimenti e annotando ulteriori documenti. Per ulteriori informazioni, vedi [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu).
