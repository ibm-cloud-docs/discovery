---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-21"

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

# Introduzione all'esecuzione di query

In questa esercitazione, impareremo a scrivere alcuni tipi diversi di query in {{site.data.keyword.discoveryshort}}.
{: shortdesc}

Per ulteriori informazioni relative alla scrittura di query, consulta:
- [Concetti delle query](/docs/services/discovery/using.html)
- [Guida di riferimento per le query](/docs/services/discovery/query-reference.html) (include l'elenco dei parametri, degli operatori e delle aggregazioni disponibili nel {{site.data.keyword.discoveryshort}} Query Language)

Queste query di esempio sono create utilizzando la strumentazione {{site.data.keyword.discoveryshort}}. Se invece desideri utilizzare l'API, aggiungi i parametri di query alla tua chiamata API. Per ulteriori informazioni ed esempi, consulta la sezione Queries del [Riferimento API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection){: new_window}.

Puoi anche scrivere query di linguaggio naturale (come le "collaborazioni di IBM Watson") utilizzando la strumentazione {{site.data.keyword.discoveryshort}}. Questa esercitazione si concentra principalmente su come scrivere le query con il {{site.data.keyword.discoveryshort}} Query Language perché i tuoi requisiti possono richiedere una query strutturata e i filtri e le aggregazioni devono essere scritti nel {{site.data.keyword.discoveryshort}} Query Language.
{: tip}

## Prima di iniziare

**Completa la procedura riportata nell'[Introduzione](/docs/services/discovery/getting-started-tool.html).** Se non hai completato l'**Introduzione**, vai alla schermata **Manage data**, crea una nuova raccolta denominata comunicati stampa di {{site.data.keyword.IBM_notm}} e aggiungi questi quattro documenti (utilizza **Default Configuration**): <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno" class="style-scope doc-content"></a>

## Passo 1: Introduzione rapida allo schema di dati Discovery

Inizia con l'ottenere il JSON {{site.data.keyword.discoveryshort}}. Per comprendere come creare una query utilizzando il {{site.data.keyword.discoveryshort}} Query Language, è utile avere familiarità con il JSON prodotto da {{site.data.keyword.discoveryshort}} dopo che ha arricchito i documenti nella tua raccolta.

1.  [Avvia la strumentazione {{site.data.keyword.discoveryshort}}](/docs/services/discovery/getting-started-tool.html#launch-the-tooling). Nella schermata **Manage data**, scegli la raccolta comunicati stampa di {{site.data.keyword.IBM_notm}}.

1.  Controlla le informazioni approfondite che Watson ha rilevato nei tuoi documenti arricchiti.

    -  **Sensazioni generali** visualizza la percentuale di suddivisione dei documenti contrassegnati come positivi, neutrali o negativi, rilevati dall'arricchimento Sentiment Analysis.
    -  **Entità principali** visualizza le persone, i luoghi e le organizzazioni rilevati nei tuoi documenti dall'arricchimento Entity Extraction.
    -  **Gerarchia contenuto** visualizza le tassonomie gerarchiche rilevate nei tuoi documenti dall'arricchimento Category Classification.
    -  **Concetti correlati** visualizza i concetti rilevati nei tuoi documenti dall'arricchimento Concept Tagging.

         Fai clic su **View in schema** di una qualsiasi scheda per visualizzare gli arricchimenti che comprendono questi risultati.
         {: tip}

1.  Per acquisire familiarità con lo schema di dati dei tuoi documenti, diamo un'occhiata alla schermata **View data schema**. Visualizza i campi e i valori nei tuoi documenti trasformati in due modi: per documento (**vista Document**) o per campo (**vista Collection**). La **vista Collection** visualizzerà tutti i campi nella tua raccolta.

    Fai clic sul pulsante **View data schema**. Nella **vista Collection**, sotto `enriched_text`, puoi esaminare gli arricchimenti applicati con il file **Default Configuration**. Fai clic su `categories`, `concepts`, `entities` e `sentiment` per vedere in che modo la tua raccolta è stata arricchita con l'analisi approfondita di Watson.

Se la tua query non restituisce alcun risultato corrispondente e pensi che dovrebbe, prova a scambiare il campo/valore che la tua query sta utilizzando con uno che puoi verificare nello schema di dati.
{: tip}    

## Passo 2: Crea una query di base

Inizia scrivendo una query che troverà il concetto `Cloud computing` nella tua raccolta:

1.  Fai clic sull'icona di creazione delle query ![icona Query](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> per aprire la pagina della query. Seleziona la raccolta che contiene i comunicati stampa {{site.data.keyword.IBM_notm}} e fai clic su **Get started**.
1.  Nella schermata **Build queries**, fai clic su **Search for Documents** e quindi su **Use the {{site.data.keyword.discoveryshort}} Query Language**:
    - Fai clic sul menu a discesa **Field** e scegli `enriched_text.concepts.text`, per l'**Operator** scegli `contains` e immetti il valore **Value** di `Cloud computing`. La query `enriched_text.concepts.text:Cloud computing` sarà visualizzata in **Visual Query Builder**.

    - In alternativa, potresti fare clic su **Edit in query language** e quindi su **Use the {{site.data.keyword.discoveryshort}} Query Language**. Immetti `enriched_text.concepts.text:"Cloud computing"` nel campo **Enter query here**.

1.  Fai clic su **Run query**. Ci dovrebbe essere una corrispondenza (`"matching_results": 1`). Copia il **Query URL** all'inizio del riepilogo (**Summary**) o della scheda **JSON** da utilizzare nella tua applicazione.

**Bonus:** in **More options**, hai l'opzione di attivare il richiamo dei passaggi con il pulsante di opzione **Include relevant passages**. I passaggi sono estratti brevi e pertinenti dai documenti completi restituiti dalla tua query. Questi passaggi mirati vengono estratti dai campi `text` dei documenti nella tua raccolta. Per ulteriori informazioni, consulta [Passaggi](/docs/services/discovery/query-parameters.html#passages). Il richiamo dei passaggi non è disponibile per la raccolta {{site.data.keyword.discoveryshort}} News.

Se desideri eseguire il checkout di alcune query pre-create, fai clic sul pulsante **Use a sample query**.
{: tip}

## Passo 3: Fai esperimenti con query diverse

Prova queste query:

Per restituire tutti i documenti con un parere `positive`: fai clic su **Search for Documents**, **Use the {{site.data.keyword.discoveryshort}} Query Language**:
-  Fai clic sul menu a discesa **Field** e scegli `enriched_text.sentiment.document.label`, per l'**Operator** scegli `contains` e quindi immetti il valore (**Value**) di `positive`.  

   La query `enriched_text.sentiment.document.label:positive` sarà visualizzata in **Visual Query Builder**.

Per restituire tutti i documenti nella categoria `health and fitness`: fai clic su **Search for Documents**, **Use the {{site.data.keyword.discoveryshort}} Query Language**:
-  Fai clic sul menu a discesa **Field** e scegli `enriched_text.categories.label`, per l'**Operator** scegli `is` e quindi immetti il valore (**Value**) di `"health and fitness"`.

   La query `enriched_text.categories.label::"health and fitness"` sarà visualizzata in **Visual Query Builder**. L'operatore `::` specifica una corrispondenza esatta.

Per restituire tutti i documenti che contengono l'entità `IBM` ma non l'entità `Watson`: fai clic su **Search for Documents**, **Use the {{site.data.keyword.discoveryshort}} Query Language**:
-  Fai clic sul menu a discesa **Field** e scegli `enriched_text.entities.text`, per l'**Operator** scegli `contains` e quindi immetti il valore (**Value**) di `IBM`. Fai clic su **Add rule** e quindi per **Field** scegli `enriched_text.entities.text`, per l'**Operator** scegli `does not contain` e immetti il valore **Value** di `Watson`.

   La query `enriched_text.entities.text:IBM,enriched_text.entities.text:!Watson` sarà visualizzata in **Visual Query Builder**. L'operatore `:!` specifica "does not contain".

## Passo 4: Crea una query combinata

Puoi combinare i parametri di query insieme tra loro per creare query più mirate. Prova utilizzando i parametri `filter` e `query` per restituire i documenti sulle acquisizioni {{site.data.keyword.IBM_notm}}. Il parametro del filtro restringerà i risultati a solo i documenti che parlano di `IBM` e poi il parametro di query restituirà tutti i risultati sulle acquisizioni (`acquisitions`), in ordine di pertinenza.

1.  Fai clic sull'icona di creazione delle query ![icona Query](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> per aprire la pagina della query. Seleziona la raccolta che contiene i comunicati stampa {{site.data.keyword.IBM_notm}} e fai clic su **Get started**.

1.  In **Filter which documents you query**:
    -  Fai clic sul menu a discesa **Field** e scegli `enriched_text.entities.text`, per l'**Operator** scegli `contains` e quindi immetti il valore (**Value**) di `IBM`. 

       La query `enriched_text.entities.text:IBM` restringerà i documenti a solo quelli che citano l'entità `IBM`.

1.  In **Search for Documents**, fai clic su **Use the {{site.data.keyword.discoveryshort}} Query Language**:
    -  Fai clic sul menu a discesa **Field** e scegli `enriched_text.concepts.text`, per l'**Operator** scegli `contains` e immetti il valore **Value** di `world wide web`. 

       La query `enriched_text.concepts.text:"world wide web"` restituirà tutti i documenti che includono il concetto di `world wide web` e tali documenti saranno classificati in ordine di pertinenza.

1.  Fai clic su **More options**, quindi su **Fields to return** e scegli **Specify**. Seleziona `text`. Questo limiterà la risposta al testo degli articoli pertinenti e escluderà tutto il resto.

1.  Fai clic su **Run query**. Ci sarà un documento corrispondente: `"matching_results": 1`

## Passo 5: Creazione di un'aggregazione

Le aggregazioni restituiscono una serie di valori di dati; ad esempio, le parole chiave più importanti, il parere generale delle entità e altro. 

Prova a creare questa aggregazione - restituirà i primi 10 concetti nella raccolta dei comunicati stampa di {{site.data.keyword.IBM_notm}}.

1.  Fai clic sull'icona di creazione delle query ![icona Query](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> per aprire la pagina della query. Seleziona la raccolta che contiene i comunicati stampa {{site.data.keyword.IBM_notm}} e fai clic su **Get started**.

1.  In **Include analysis of your results**:
    -  Fai clic sul menu a discesa **Output** e scegli `Top values`, per **Field** scegli `enriched_text.concepts.text` e quindi immetti il numero (**Count**) di `10`.

       `Term` restituirà i valori più comuni per il campo `concepts` `text`. **Count** specifica il numero di risultati che desideri siano restituiti. La query `term(enriched_text.concepts.text,count:10)` sarà visualizzata in **Visual Query Builder**.   

1.  Fai clic su **More options** e quindi immetti `0` nel campo **Number of documents to return**.

1.  Fai clic su **Run query**. Saranno visualizzati i primi 10 concetti nelle schede **Summary** e **JSON**. Questo è un esempio del riepilogo:

## Passo 6: Crea una query in Watson Discovery News

{{site.data.keyword.discoverynewsshort}}, è un insieme di dati pubblico che è stato pre-arricchito con informazioni approfondite cognitive. È incluso con {{site.data.keyword.discoveryshort}}. Per ulteriori informazioni su questa raccolta, consulta [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html#watson-discovery-news). 

Non puoi regolare la configurazione di {{site.data.keyword.discoverynewsshort}}, formare o aggiungere documenti alla raccolta {{site.data.keyword.discoverynewsshort}}. Guarda una demo di ciò che puoi creare con {{site.data.keyword.discoverynewsshort}} [qui ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://discovery-news-demo.ng.bluemix.net/){: new_window}.

La seguente query di esempio restituisce i primi 10 articoli in {{site.data.keyword.discoverynewsfull}} sui Pittsburgh Steelers che hanno un parere positivo.

1.  Fai clic sull'icona di creazione delle query ![icona Query](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> per aprire la pagina della query. Seleziona la raccolta {{site.data.keyword.discoverynewsshort}} e fai clic su **Get started**. (Per eseguire la query di raccolte spagnole, tedesche e coreane {{site.data.keyword.discoverynewsshort}} devi prima fare clic sull'icona ![Manage Data](/images/icon_yourData.png) e quindi scegliere la lingua appropriata dal menu a discesa).

1.  In **Search for documents**, fai clic su **Use the {{site.data.keyword.discoveryshort}} Query Language**:
    -  Fai clic sul menu a discesa **Field** e scegli `text`, per l'**Operator** scegli `contains` e immetti il valore **Value** di `Pittsburgh Steelers`. Fai clic su **Add rule**, quindi sul menu a discesa **Field** e scegli `enriched_text.sentiment.document.label`, per l'**Operator** scegli `contains` e quindi immetti il valore (**Value**) di `positive.`

       La query `text:"Pittsburgh Steelers",enriched_text.sentiment.document.label:"positive"` sarà visualizzata in **Visual Query Builder**.

1.  Fai clic su **More options** e quindi immetti `10` (questo è il valore predefinito) nel campo **Number of documents to return**.

1.  Fai clic su **Run query**. Saranno visualizzati i primi 10 articoli sui Pittsburgh Steelers con un parere positivo.

**Nota:** il numero massimo di risultati restituiti per una query di Watson Discovery News è `50`.

Gli articoli di notizie possono essere diffusi a diversi canali di notizie e {{site.data.keyword.discoverynewsfull}} rileverà ciascuno di essi, con una conseguente presenza di articoli duplicati. Questo significa che una query a {{site.data.keyword.discoverynewsfull}} potrebbe restituire potenzialmente diversi articoli identici o quasi identici nei risultati della query. Per attivare la deduplicazione, in **More options**, scegli **Exclude duplicate results**. Per ulteriori informazioni su questa funzionalità beta, consulta [Esclusione di documenti duplicati dai risultati della query](/docs/services/discovery/query-parameters.html#deduplication).
