---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-18"

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
{:download: .download}

# Introduzione

In questa breve esercitazione, introdurremo la strumentazione {{site.data.keyword.discoveryshort}} e illustreremo il processo di creazione di una raccolta dati privata e la sua ricerca.
{: shortdesc}

Se preferisci utilizzare l'API, consulta [Introduzione all'API](/docs/services/discovery/getting-started.html).
{: tip}

## Prima di iniziare
{: #before-you-begin}

Avrai bisogno di un'istanza del servizio da avviare.

<!-- Remove the text marked `download` after there's no g-s tab in the catalog dashboard -->


Hai creato la tua istanza del servizio. Fai clic su **Manage** e quindi su **Open tool**. Vai al [Passo 2](/docs/services/discovery/getting-started-tooling.html#create-a-collection).
{: download tip}

Se hai creato un'istanza del servizio {{site.data.keyword.discoveryshort}}, tutti questi prerequisiti sono impostati. Vai al [Passo 1](/docs/services/discovery/getting-started-tool.html#launch-the-tooling).

1.  Vai alla pagina [{{site.data.keyword.discoveryshort}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.{DomainName}/catalog/services/discovery){: new_window} nel catalogo {{site.data.keyword.Bluemix_notm}}.
1.  Registrati per un account {{site.data.keyword.Bluemix_notm}} gratuito o accedi.
1.  Fai clic su **Create**.


## Passo 1: Avvia la strumentazione
{: #launch-the-tooling}

Dopo aver creato un'istanza del servizio {{site.data.keyword.discoveryshort}}, verrai portato al [dashboard {{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/dashboard). Fai clic sulla tua istanza del servizio {{site.data.keyword.discoveryshort}} per andare al dashboard del servizio {{site.data.keyword.discoveryshort}}.

Nella pagina **Manage**, fai clic su **Open tool**.

<!-- To do: Add screenshot for developer console -->

Se ti viene richiesto di accedere alla strumentazione, fornisci le tue credenziali {{site.data.keyword.Bluemix_notm}}.

Se non sei nella pagina dei dettagli del progetto per il servizio {{site.data.keyword.discoveryshort}}, vai alla pagina {{site.data.keyword.watson}} Developer Console [Projects ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.{DomainName}/developer/watson/projects) e seleziona il progetto.
{: tip}

<!-- Remove this text after dedicated instances have the Developer Console: begin -->

{{site.data.keyword.Bluemix_dedicated_notm}}: seleziona la tua istanza del servizio dal dashboard per avviare la strumentazione.

<!-- Remove this text after dedicated instances have the Developer Console: end -->

## Passo 2: Crea una raccolta
{: #create-a-collection}

Il primo passo da compiere nella strumentazione {{site.data.keyword.discoveryshort}} è quello di creare una raccolta di dati.

Una raccolta è un insieme dei tuoi documenti. *Perché dovrei volere più di una raccolta?* Ci sono alcune ragioni:

- Potresti volere più raccolte per separare i risultati per destinatari diversi.
- I dati potrebbero essere così diversi che non ha senso eseguirne la query contemporaneamente.

Anche la raccolta dati {{site.data.keyword.discoverynewsshort}} pubblica e pre-arricchita è disponibile per il tuo utilizzo. È pronta per la query e puoi iniziare a creare query immediatamente. Non puoi regolare la configurazione o aggiungere i documenti a {{site.data.keyword.discoverynewsshort}}.

1.  Fai clic su ![Cog](images/icon_settings.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> e scegli **Create environment**.
1.  Quando il tuo ambiente è pronto, fai clic sul pulsante **Upload your own data**, dopodiché puoi dare un **Nome alla tua nuova raccolta**. Fornisci un nome alla tua raccolta e scegli **Default Configuration** da **Select a configuration to apply** (puoi modificare la configurazione successivamente).

Esiste un'altra configurazione disponibile denominata **Default Contract Configuration** che supporta l'Element Classification, che può essere utilizzata per estrarre la parte, la natura e la categoria dagli elementi nei PDF. Per i dettagli, consulta [Element Classification](/docs/services/discovery/element-classification.html#element-collection).

Puoi anche indicizzare le origini dati Box, Salesforce e Microsoft SharePoint Online con la strumentazione {{site.data.keyword.discoveryshort}}. Fai clic sul pulsante **Connect a data source** e consulta [Connessione alle origini dati](/docs/services/discovery/connect.html) per ulteriori informazioni.
{: tip}

## Passo 3: crea una configurazione personalizzata
{: create-custom-configuration}

Dopo aver creato la tua raccolta, potresti avviare immediatamente il caricamento del contenuto utilizzando l'area di caricamento, ma vogliamo creare e verificare una configurazione personalizzata.

1.  Fai clic su **Switch** accanto al nome della raccolta e scegli **Create a new configuration**. Fornisci un nome alla tua configurazione e fai clic su **Create**.
1.  Dopo aver creato la tua configurazione, puoi personalizzarla:
    1.  Scarica il documento di esempio <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno" class="style-scope doc-content"></a>.
    1.  Utilizza il pannello **Upload Sample Documents** per caricare il documento di esempio. Dopo averlo caricato, puoi fare clic sul link del nome del documento per visualizzare la trasformazione.
1.  Ora è il momento di modificare la configurazione. Per questa attività, modifica gli arricchimenti applicati a ciascun documento:
    1.  Fai clic sulla sezione **Enrich** della configurazione. Consulta il JSON generato a destra dello schermo. Scorri verso il basso fino alla sezione *enriched_text* e nota che contiene molti *concepts*.
    1.  Successivamente, rimuovi l'arricchimento di testo denominato *concepts* facendo clic sulla **X** accanto a esso e quindi fai clic su **Apply & Save**.
    1.  Infine, consulta nuovamente il JSON. Nota come l'output è stato modificato e non include più *concepts*.

## Passo 4: Carica i tuoi documenti
{: #upload-your-documents}

Quando sei soddisfatto della conversione personalizzata del tuo documento di esempio, è ora di inserire del contenuto reale nella tua raccolta.

1. Scarica questi tre documenti di esempio: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno" class="style-scope doc-content"></a>.
1.  Fai clic su ![Icona File](images/icon_yourData.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> e seleziona la tua raccolta.
1.  Assicurati che la configurazione personalizzata che hai creato sia elencata in **Configuration**. Se non lo è, fai clic su **Switch** accanto al nome della configurazione e selezionala.
1.  Fai clic sul pulsante **Upload documents** e avvia il caricamento dei quattro documenti di esempio: test-doc1.html, test-doc2.html, test-doc3.html, test-doc4.html.
1.  Attendi che i documenti vengano caricati. Lo stato dei tuoi documenti viene visualizzato nella sezione **Overview**.

## Passo 5: Crea una query
{: #build-a-query}

1.  Fai clic su ![Icona query](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> per aprire la pagina della query. Seleziona la tua raccolta e fai clic su **Get started**. 
1.  Nella schermata **Build queries**, fai clic su **Search for documents** e quindi su **Use the {{site.data.keyword.discoveryshort}} Query Language**:
    - Per cercare i risultati con entità denominate "IBM":
        1.  Fai clic su **Field** e seleziona `enriched_text.entities.text`. Seleziona `contains` per **Operator** e `IBM` per **Value**. La query `enriched_text.entities.text:IBM` viene visualizzata in **Visual Query Builder**.
        1.  Fai clic su **Run Query**. La query restituisce 4 risultati.
    - Per cercare i risultati con entità denominate "Watson":
        1.  Fai clic su **Field** e seleziona `enriched_text.entities.text`. Seleziona `contains` per **Operator** e `watson` per **Value**. La query `enriched_text.entities.text:watson` viene visualizzata in **Visual Query Builder**.
        1.  Fai clic su **Run Query**. La query restituisce 2 risultati.
    - Per cercare i risultati con le entità "Watson" e "Slack":
        1.  Fai clic su **Field** e seleziona `enriched_text.entities.text`. Seleziona `contains` per **Operator** e `watson` per **Value**. Fai clic su **Add rule**, ripeti le tue selezioni, ma scegli il valore **Value** di `Slack`. La query `enriched_text.entities.text:watson,enriched_text.entities.text:Slack` viene visualizzata in **Visual Query Builder**.
        1.  Fai clic su **Run Query**. La query restituisce 1 risultato.

    Fai clic su **Edit in query language** per creare le query utilizzando il {{site.data.keyword.discoveryshort}} Query Language. Per ulteriori informazioni sul {{site.data.keyword.discoveryshort}} Query Language, consulta [Guida di riferimento per le query](/docs/services/discovery/query-reference.html) e [Concetti delle query](/docs/services/discovery/using.html).
1.  I risultati della tua query vengono visualizzati nella sezione **Results**:
    - La scheda **Summary** fornisce una panoramica dei risultati della query.
    - La scheda **JSON** visualizza i risultati JSON completi.

    Per le query elencate, **Summary** visualizza prima i passaggi del documento (in ordine di pertinenza), seguiti dai nomi dei documenti trovati e poi i risultati in base all'arricchimento. I **Passaggi** sono estratti brevi e pertinenti dai documenti completi restituiti dalla tua query. 

    Il link **Query URL** fornito nelle schede **JSON** e **Summary** è pronto per l'utilizzo nella tua applicazione.

    Puoi anche fare clic su **Use natural language** e scrivere una query in linguaggio naturale, come ad esempio "IBM Watson partnerships". Per ulteriori informazioni sulle query in linguaggio naturale, consulta [Query in linguaggio naturale](/docs/services/discovery/query-parameters.html#nlq).

    Watson può essere formato per migliorare i risultati delle query in linguaggio naturale, consulta [Miglioramento della pertinenza dei risultati con la strumentazione](/docs/services/discovery/train-tooling.html).

    Ulteriori risorse:
    - Per informazioni sullo schema dei dati nei tuoi documenti, fai clic sull'icona **View Data Schema** o sulla scheda **JSON**. Per i dettagli, consulta [Lo schema di dati Discovery](/docs/services/discovery/using.html#discovery-schema).
    - Se stai eseguendo la modifica nel linguaggio della query nativo {{site.data.keyword.discoveryshort}}, fai clic sull'icona **?** accanto ad ogni campo **Enter query here** per ulteriori esempi.

## Passi successivi
{: #next-steps}

Ora hai un'istanza del servizio {{site.data.keyword.discoveryshort}} compilata e funzionante. Puoi ora iniziare a personalizzare la tua raccolta aggiungendo più documenti e arricchimenti e a personalizzare le impostazioni di conversione.
