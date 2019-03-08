---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-25"

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

# Note sulla release
{: #release-notes}

Le note sulla release forniscono informazioni sulle modifiche apportate al servizio {{site.data.keyword.discoveryfull}} successivamente alla release precedente.
{: shortdesc}

## Controllo versioni delle API del servizio
{: shortdesc}

Le richieste API richiedono un parametro di versione che prende una data nel formato `version=YYYY-MM-DD`. Ogni volta che modifichiamo l'API in un modo non compatibile con le versioni precedenti, rilasciamo una nuova versione secondaria della API.

Invia il parametro di versione con ogni richiesta API. Il servizio utilizza la versione API per la data che specifichi oppure la versione più recente prima di tale data. Non utilizzare, per impostazione predefinita, la data attuale. Specifica invece una data che corrisponde a una versione compatibile con la tua applicazione e non modificarla finché la tua applicazione non è pronta per una versione successiva.

La versione attuale è `2018-10-15`.

## Funzioni beta
{: #beta-features}

IBM rilascerà servizi, funzioni e supporto linguistico classificati come beta o sperimentali. Tali capacità possono essere instabili, possono cambiare frequentemente e possono essere sospese con breve preavviso. Sono fornite per consentirti di valutarne la funzionalità. Una capacità beta o sperimentale potrebbe non fornire lo stesso livello di prestazioni o compatibilità generalmente fornito dalle capacità rilasciate. Queste capacità non sono progettate per essere utilizzate in un ambiente di produzione e qualsiasi utilizzo di questo tipo che ne fai è a tuo rischio e pericolo.


## Modifiche
{: #change-log}

Sono disponibili le seguenti nuove funzioni e modifiche al servizio.

## 25 ottobre 2018
{: #25oct}

Lo schema per l'arricchimento [Element Classification](/docs/services/discovery/element-classification.html) è cambiato. Se vuoi utilizzare lo schema aggiornato, devi inserire i tuoi documenti con l'API, utilizzando la data di versione `2018-10-15` o successiva. La strumentazione {{site.data.keyword.discoveryshort}} non utilizza ancora questa versione API (attualmente utilizza `2018-08-01`), quindi i documenti inseriti utilizzando la strumentazione {{site.data.keyword.discoveryshort}} saranno arricchiti con lo schema originale.

## 25 settembre 2018
{: #25sept}

- È stato rilasciato Continuous Relevancy Training, che utilizza le interazioni dagli utenti per imparare a tirare fuori i risultati più pertinenti. Può imparare dal comportamento degli utenti automaticamente, riducendo notevolmente lo sforzo richiesto per migliorare la classificazione della pertinenza dei risultati. Per i dettagli, vedi [Continuous Relevancy Training](/docs/services/discovery/continuous-training.html#crt).

- È stato aggiunto il supporto API per l'esecuzione di query più lunghe. Ciò aumenta il limite dei caratteri a 10.000 e consente di aumentare il numero di filtri nelle tue query e di eseguire aggregazioni più complesse. Vedi la query POST nella [Guida di riferimento per le API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query){: new_window} e la [Guida di riferimento per le API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#federated-query){: new_window} per i dettagli.

- Puoi ora eseguire l'upgrade al piano Advanced utilizzando l'API. Vedi [Upgrade del tuo piano](/docs/services/discovery/upgrading.html#advanced) per i dettagli. 

- L'arricchimento Element Classification ha aggiornato gli elementi classificati, gli elementi del contratto e le parti e le tabelle identificate. Vedi [Element Classification](https://console.bluemix.net/docs/services/discovery/element-classification.html) per gli aggiornamenti.

- È stato aggiunto un supporto completo per la lingua portoghese (Brasile). Per ulteriori informazioni, vedi [Supporto linguistico](/docs/services/discovery/language-support.html).

- L'API query (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`) ora supporta il parametro `bias`, che ti consente di orientarti a specifici risultati, ad esempio i documenti che sono stati pubblicati più di recente. Per informazioni, vedi il metodo [Eseguire una query della tua raccolta ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query-using-get){: new_window} nella Guida di riferimento per le API.

- È stato rilevato che il file **Default Contract Configuration** (Configurazione del contratto predefinita) fornito per arricchire le raccolte per [Element Classification](/docs/services/discovery/element-classification.html#element-collection) presenta un problema con le normalizzazioni HTML. Un nuovo **Default Contract Configuration** è incluso con questa release. Attieniti alla procedura indicata di seguito per applicare il nuovo **Default Contract Configuration** alle tue raccolte.

     1. Determina quali delle tue raccolte stanno utilizzando il file di configurazione **Default Contract Configuration** oppure una configurazione personalizzata basata su **Default Contract Configuration**.
     1. Annota le modifiche che hai apportato ad eventuali configurazioni personalizzate in base a **Default Contract Configuration**.
     1. Poiché il vecchio file **Default Contract Configuration** deve essere eliminato dal tuo ambiente prima che venga utilizzato quello nuovo, utilizza l'API[Delete configuration ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#delete-configuration){: new_window} per eliminare l'attuale **Default Contract Configuration** eventualmente associato alle tue raccolte. Elimina anche le eventuali configurazioni basate sul vecchio **Default Contract Configuration**.
     1. Ora puoi utilizzare il nuovo file **Default Contract Configuration**. Per ogni raccolta che utilizza una di queste configurazioni, crea una nuova raccolta. Applica il nuovo **Default Contract Configuration** oppure crea una nuova configurazione personalizzata basata sul nuovo **Default Contract Configuration** utilizzando le tue annotazioni del passo 2.
     1. Carica i file precedentemente inseriti nelle raccolte originali.
     1. Elimina le vecchie raccolte.

## 15 agosto 2018
{: #15aug}

- Sono disponibili due nuovi operatori di query. `Exists` (`:*`) può essere utilizzato per restituire tutti i risultati in cui è presente il campo )`field`) specificato. `Does not exist` (`!*`) può essere utilizzato per restituire tutti i risultati che non includono il campo (`field`) specificato. Per ulteriori informazioni, vedi [Operatori di query](/docs/services/discovery/query-operators.html). 

## 2 agosto 2018
{: #2aug}

- {{site.data.keyword.discoveryfull}} ora supporta le raccolte di lingua inglese, spagnola, tedesca, italiana, portoghese, francese, araba, coreana e giapponese quando si stabilisce una connessione e ci si sincronizza con Box, Salesforce e SharePoint Online con la strumentazione {{site.data.keyword.discoveryshort}}. 

## 31 luglio 2018
 
 - A partire dal **1° agosto 2018**, {{site.data.keyword.discoveryfull}} ha una nuova struttura dei prezzi. Offre un modello dei prezzi più semplice (le ore documento non fanno più parte del calcolo) e dei prezzi a livelli per le query {{site.data.keyword.discoverynewsfull}}. Inoltre, il piano Standard è stato ritirato e il piano Lite ha ridotto i limiti di query di {{site.data.keyword.discoverynewsshort}} e documenti. Le modifiche dei prezzi non richiederanno alcuna azione da parte degli utenti {{site.data.keyword.discoverynewsshort}} attuali. Per i dettagli, vedi [Piani dei prezzi {{site.data.keyword.discoveryshort}}](/docs/services/discovery/pricing-details.html).
 
**Nota:** la data della versione dell'API è stata aggiornata a `2018-08-01`. Per avvalerti delle nuove opzioni di dimensione dell'ambiente (`LT`, `XS`, `S`, `MS`, `M`, `ML`, `L`, `XL`, `XXL`, `XXXL`), devi utilizzare questa data della versione quando crei ambienti con l'API. Le dimensioni dell'ambiente ora hanno il tipo `string` (in precedenza il tipo era `integer`.)

## 27 luglio 2018

- È stato rilasciato [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery/watson-discovery-news.html) in una lingua aggiuntiva: giapponese (`collection_id`: `news-ja`). {{site.data.keyword.discoverynewsfull}} è anche disponibile in inglese, spagnolo, tedesco e coreano.

## 25 giugno 2018

- È stata aggiunta l'opzione per connettersi a, e sincronizzarsi con, le origini dati Box, Salesforce e Microsoft SharePoint Online. Queste origini dati non sono disponibili in ambienti Premium. Sono state rilasciate le API [Source Credential ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#credentials-api){: new_window} e [Configuration ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#configurations-api){: new_window} per queste origini dati. 
  - {{site.data.keyword.discoveryfull}} supporta solo le raccolte di lingua inglese quando si stabilisce una connessione a, e ci si sincronizza con, Box, Salesforce e SharePoint Online con la strumentazione {{site.data.keyword.discoveryshort}}. [Risolto](/docs/services/discovery/release-notes.html#2aug)
  - Il limite di dimensione di file documento singolo per Box, Salesforce e SharePoint Online è 10MB.
- È stato aggiunto un nuovo dashboard Prestazioni nella strumentazione {{site.data.keyword.discoveryshort}}. Vedi [Visualizzazione delle metriche e miglioramento dei risultati della query con il dashboard Prestazioni](/docs/services/discovery/dashboard.html). Il nuovo dashboard non è disponibile negli ambienti Premium o Dedicated.
- È stato aggiunto un supporto completo per la lingua giapponese. Per ulteriori informazioni, vedi [Supporto linguistico](/docs/services/discovery/language-support.html).

## 22 giugno 2018

- È stata rilasciata l'API Events and Feedback. Per ulteriori informazioni, vedi la [Guida di riferimento per le API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#events-and-feedback-api){: new_window}.

## 11 giugno 2018

-  Per le applicazioni ospitate a Washington, DC (Stati Uniti Est), il servizio ora supporta l'autenticazione IAM (Identity and Access Management) basata sui token. IAM utilizza i token di accesso piuttosto che le credenziali di servizio per l'autenticazione con un servizio. Per ulteriori informazioni sull'utilizzo dei token IAM con le applicazioni esistenti e nuove, vedi l'aggiornamento della release del [17 maggio 2018](#17May2018).
-  Un ulteriore elemento di contratto è ora supportato in Element Classification, `Safety and Security`. Per i dettagli, vedi la [descrizione degli elementi del contratto](/docs/services/discovery/element-classification.html#contract-elements).

## 6 giugno 2018

- Le query {{site.data.keyword.discoverynewsfull}} ora visualizzano le prime 50 parole di ogni articolo nel campo JSON `text`.

## 5 giugno 2018
{: #5jun}

- Element Classification è ora disponibile per gli utenti che hanno sottoscritto piani Premium.
- La valutazione `assurance` di `Low` non è più disponibile per Element Classification.

## 31 maggio 2018

- È stato aggiunto un supporto completo per la lingua francese. Per ulteriori informazioni, vedi [Supporto linguistico](/docs/services/discovery/language-support.html).

## 30 maggio 2018

- È stato corretto un problema noto in {{site.data.keyword.discoverynewsfull}}. In precedenza, quando eseguivi query di {{site.data.keyword.discoverynewsshort}} potevi ricevere un conteggio dei documenti non corretto perché i documenti in altre lingue venivano contati insieme alla lingua da te richiesta. Non è più così.
- A partire dalla raccolta creata dal `22 maggio 2018` in poi, {{site.data.keyword.discoveryshort}} restituisce ora dei risultati della query che includono i caratteri speciali dalle seguenti lingue: inglese, tedesco, francese, olandese, italiano e portoghese. Ad esempio, se esegui una query per `aqui`, riceverai ora i risultati sia per `aqui` che per <code>aqu&iacute;</code>.

## 21 maggio 2018

- È stato rilasciato [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery/watson-discovery-news.html) in una lingua aggiuntiva: tedesco (`collection_id`: `news-de`). {{site.data.keyword.discoverynewsfull}} è anche disponibile in inglese, spagnolo e coreano.

## 17 maggio 2018
{: #17May2018}

- Le query {{site.data.keyword.discoverynewsfull}} ora visualizzano solo le prime 20 parole di ciascun articolo nel campo JSON `text`.

-   Il servizio ora supporta un nuovo processo di autenticazione API per le istanze del servizio per le applicazioni ospitate a Sydney (**au-syd**) a partire dal 15 maggio 2018. Ne verrà a breve eseguita l'abilitazione per le applicazioni ospitate in altre regioni. {{site.data.keyword.Bluemix}} è in frase di migrazione all'autenticazione IAM (Identity and Access Management) basata sui token.IAM utilizza i token di accesso piuttosto che le credenziali di servizio per l'autenticazione con un servizio. 

   Nella regione di Sydney, utilizzi i token di accesso IAM con il servizio {{site.data.keyword.discoveryshort}} per

    -   *Nuova istanze del servizio* che crei dopo il 15 maggio. Per ulteriori informazioni, vedi [Autenticazione con i token IAM](/docs/services/watson/getting-started-iam.html).
    -   *Istanze del servizio esistenti* di cui esegui la migrazione da Cloud Foundry a un gruppo di risorse gestito dall'RC (Resource Controller). Le istanze del servizio che erano state create prima del 15 maggio continuano a utilizzare le credenziali del servizio per l'autenticazione finché non ne esegui la migrazione. Per ulteriori informazioni, vedi [Migrazione di istanze del servizio Cloud Foundry a un gruppo di risorse](/docs/resources/instance_migration.html).

    Tutte le istanze del servizio nuove ed esistenti in altre regioni continuano a utilizzare le credenziali del servizio (`apikey:{apikey_value}`) per l'autenticazione.

### Utilizzo di un token di accesso IAM per l'autenticazione

Quando utilizzi i token di accesso IAM, esegui l'autenticazione prima di inviare una richiesta al servizio {{site.data.keyword.discoveryshort}}.

1.  Ottieni una chiave API da IBM Cloud. Utilizza tale chiave per generare un token di accesso IAM. Per ulteriori informazioni, vedi [Come ottenere un token IAM utilizzando una chiave API del servizio {{site.data.keyword.watson}}](/docs/services/watson/getting-started-iam.html#iamtoken).
1.  Passa il token di accesso IAM al servizio {{site.data.keyword.discoveryshort}} utilizzando l'intestazione `Authorization`. Nell'intestazione, indica che il token di accesso è un token `Bearer` specificando `Authorization: Bearer {access_token}`.

    Il seguente esempio cURL semplice utilizza un token di accesso:

    ```bash
    curl -X GET
    --header "Authorization: Bearer eyJhbGciOiJIUz......sgrKIi8hdFs"
    "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    Per ulteriori informazioni, vedi [Utilizzo di un token per l'autenticazione](/docs/services/watson/getting-started-iam.html#use_token).

### Aggiornamento di un token di accesso IAM

I token di accesso IAM che generi hanno la seguente struttura. Utilizzi il valore del campo `access_token` per effettuare una richiesta autenticata al servizio.

```javascript
{
  "access_token": "eyJhbGciOiJIUz......sgrKIi8hdFs",
  "refresh_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353
}
```
{: codeblock}

I token di accesso hanno una durata limitata. Il campo `expires_in` indica la durata del token, in questo caso 1 ora. Il campo `expiration` mostra quando scade il token come una data/ora UNIX che specifica il numero di secondi a partire dal 1° gennaio 1970 (mezzanotte UTC/GMT).

Nella tua applicazione, controlla quando scade il token di accesso prima di utilizzarlo per effettuare una richiesta autenticata. Se è scaduto, devi aggiornare il token di accesso prima di poterlo utilizzare. Utilizzi il valore del campo `refresh_token` per aggiornare il token di accesso. Per ulteriori informazioni, vedi [Aggiornamento di un token](/docs/services/watson/getting-started-iam.html#refresh_token).


## 11 maggio 2018

- I dettagli sulla sicurezza delle informazioni sono disponibili qui: [Sicurezza delle informazioni](/docs/services/discovery/information-security.html).
- Il seguente problema noto di `query_entities` di {{site.data.keyword.discoveryfull}} Knowledge Graph è stato corretto con l'aggiornamento della versione API del 4 maggio 2018 (`2018-05-04`). Questa correzione si applica solo se le entità vengono inserite o sostituite dopo il 4 maggio 2018 (`2018-05-04`). Le entità possono essere sostituite reinserendo vecchi documenti oppure inserendo nuovi documenti che contengono tali entità. Se le vecchie entità non vengono sostituite, `query_entities` restituirà tutti caratteri maiuscoli con la versione API `2018-05-04`.
  - Tutti i nomi entità venivano in precedenza convertiti in notazione Camel in `query_entities`. Ad esempio, il nome entità "IBM Corporation" veniva convertito in "Ibm Corporation". Non è più così.

## 9 maggio 2018

- I documenti di esempio sono ora archiviati localmente, nella cartella dei dati di roaming locale del tuo browser. Per ulteriori informazioni sui documenti di esempio, vedi [Caricamento di documenti di esempio](/docs/services/discovery/building.html#uploading-sample-documents).

## 4 maggio 2018

- Due elementi di contratto aggiuntivi sono ora supportati in Element Classification: Attributes e Provenance. Per i dettagli, vedi la [descrizione degli elementi del contratto](/docs/services/discovery/element-classification.html#contract-elements).

## 26 aprile 2018

- Il seguente problema di inserimento è stato corretto: in alcuni casi in cui venivano specificate `json_normalizations` e/o `normalizations` successive all'arricchimento, poteva succedere che le normalizzazioni venissero applicate nell'ordine errato. Ciò poteva causare un'indicizzazione dei documenti con valori di campo imprevisti. Non è più così.
- La dimensione massima del file per un documento di esempio è ora 1MB. La dimensione massima del file era in precedenza 5MB.

## 12 aprile 2018

- Knowledge Graph: [Evidence](/docs/services/discovery/building-kg.html#evidence) e [Canonicalization and filtering](/docs/services/discovery/building-kg.html#canonicalization) sono ora disponibili in tutte le raccolte. Nelle eventuali raccolte create prima del 5 marzo 2018 (`03-05-2018`), devi reinserire i tuoi documenti per utilizzare queste funzioni. In precedenza, dovevi creare una nuova raccolta e reinserire i tuoi documenti. 

## 11 aprile 2018

- Due categorie aggiuntive sono ora supportate in Element Classification: `Asset Use` e `Communication`. Per i dettagli, vedi la [descrizione degli elementi del contratto](/docs/services/discovery/element-classification.html#contract-elements).

## 2 aprile 2018

- I documenti di esempio vengono ora automaticamente eliminati dopo 24 ore, invece di 1 mese.

## 16 marzo 2018

- È stato aggiunto un supporto completo per la lingua tedesca. Per ulteriori informazioni, vedi [Supporto linguistico](/docs/services/discovery/language-support.html).

Strumentazione {{site.data.keyword.discoveryshort}}:
- Una nuova configurazione denominata **Default Contract Configuration** è stata aggiunta per supportare Element Classification, che può essere utilizzata per estrarre parte, natura e categoria dagli elementi nei PDF. Vedi [Element Classification](/docs/services/discovery/element-classification.html#element-collection) per i dettagli.

È stato eseguito un aggiornamento della disponibilità generale:
- La segmentazione della documentazione è stata passata dallo stato beta allo stato di disponibilità generale (GA, general availability). Il limite di segmentazione è stato aumentato a 250 segmenti. Non è più limitato a 50 segmenti per documento. Vedi [Segmentazione della documentazione](/docs/services/discovery/building.html#doc-segmentation) per i dettagli.

Problema noto:
- I caratteri jolly non funzionano con le query che contengono lettere maiuscole. Ad esempio, data la coppia chiave/campo `{"borrower": "GOVERNMENT OF INDIA"}`, `query-borrower:*ndia` restituirà i risultati mentre invece `query-borrower:*NDIA` non lo farà.

## 8 marzo 2018
{: #8mar}

- La versione beta di {{site.data.keyword.discoveryfull}} Knowledge Graph ha aggiunto diverse funzioni. Durante la release beta, la funzionalità [Knowledge Graph](/docs/services/discovery/building-kg.html) e i metodi ad essa associati sono disponibili solo per le istanze del servizio che hanno sottoscritto piani **Advanced**, piani **Premium** e tutti gli ambienti **Dedicated**. Le nuove funzioni sono:
  - [Entity similarity](/docs/services/discovery/building-kg.html#similarity)
  - [Evidence](/docs/services/discovery/building-kg.html#evidence)
  - [Canonicalization and filtering](/docs/services/discovery/building-kg.html#canonicalization)

## 7 marzo 2018

- Il seguente problema noto di inserimento è stato corretto: tra il 28 febbraio e il 6 marzo, una piccola percentuale di documenti è stata indicizzata solo con i campi `id` e `extracted_metadata` (altro contenuto dei documenti non è stato indicizzato). Il problema sottostante è stato corretto; tuttavia, dovrai inoltrare nuovamente per l'inserimento gli eventuali documenti interessati. Non esiste un modo semplice per identificare i documenti interessati.

## 5 marzo 2018
{: #5mar}

- Il seguente problema noto di {{site.data.keyword.discoveryfull}} Knowledge Graph è stato corretto con l'aggiornamento della versione API del 5 marzo 2018 (`2018-03-05`). Questa correzione si applica solo alle raccolte di nuova creazione che utilizzano l'aggiornamento della versione `2018-03-05`.  
  - Tutti i nomi di tipo di entità e di tipo di relazione venivano precedentemente convertiti in maiuscole durante l'inserimento. Ad esempio, l'entità "GeoPoliticalEntity" veniva convertita in "GEOPOLITICALENTITY" e la relazione "partOf" veniva convertita in "PARTOF." Non è più così.

## 1° marzo 2018

- I limiti di [espansione di query](/docs/services/discovery/using.html#query-expansion) sono stati aumentati per i piani Advanced e Premium a 5.000 espansioni di query e 25.000 termini in totale. Per i dettagli, vedi [Piani dei prezzi Discovery](/docs/services/discovery/pricing-details.html).

## 28 febbraio 2018

- Gli arricchimenti {{site.data.keyword.alchemylanguageshort}} sono stati dichiarati obsoleti a partire dal **1° marzo 2018**. Per informazioni sulla migrazione di raccolte esistenti e di file di configurazione che utilizzano gli arricchimenti {{site.data.keyword.alchemylanguageshort}}, vedi [Migrazione degli arricchimenti a {{site.data.keyword.nlushort}}](/docs/services/discovery/migrate-nlu.html).

## 23 febbraio 2018

- È stata aggiunta la capacità di eseguire query in base alla similarità dei documenti. Puoi eseguire query per documenti simili in base agli ID documento e, facoltativamente, perfezionare ulteriormente la similarità specificando i campi. Per ulteriori informazioni, vedi [Similarità dei documenti](/docs/services/discovery/using.html#doc-similarity).

- Il [parametro `highlight`](/docs/services/discovery/query-parameters.html#highlight) nei risultati della query è stato potenziato. I risultati della query restituiranno delle frasi complete, ordinate in base al loro punteggio (`score`).

## 21 febbraio 2018
{: #21feb}

- In precedenza, quando si inserivano documenti PDF, il `file_type` restituito quando venivano eseguite query di avvisi di inserimento, nell'oggetto `extracted_metadata` e dall'API dei dettagli del documento era `html`. Non è più così. Il `file_type` restituito sarà ora `pdf`. 

## 26 gennaio 2018
{: #26jan}

Strumentazione {{site.data.keyword.discoveryshort}}:

- È stata aggiunta la capacità di accedere a raccolte in coreano e spagnolo al tile [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery/watson-discovery-news.html) nella strumentazione. In precedenza, era possibile eseguire query di queste raccolte solo tramite l'API.

## 23 gennaio 2018

- È stata aggiunta la capacità di espandere l'ambito di una query, ad esempio puoi espandere una query per "car" per includere "automobile" e "motor vehicle". Inoltre, puoi sostituire i termini comunemente scritti in modo errato, ad esempio puoi sostituire le query per "seabizcuit" con "seabiscuit". L'espansione di query è implementata con l'API {{site.data.keyword.discoveryshort}}. Vedi [Espansione di query](/docs/services/discovery/using.html#query-expansion) per i dettagli.  

## 15 gennaio 2018

- {{site.data.keyword.discoverynewsfull}} Original è stato ritirato dal servizio. È stato sostituito il 31 luglio 2017 con una nuova versione, denominata {{site.data.keyword.discoverynewsfull}}. Per istruzioni sulla migrazione da {{site.data.keyword.discoverynewsfull}} Original alla nuova versione, consulta [Migrazione da Watson Discovery News Original](/docs/services/discovery/migrate-bwdn.html).

## 11 gennaio 2018

- È stato aggiunto un supporto completo per la lingua coreana. Per ulteriori informazioni, vedi [Supporto linguistico](/docs/services/discovery/language-support.html).

## 15 dicembre 2017

- È stato rilasciato l'arricchimento **Element Classification** che analizza gli elementi (frasi, elenchi, tabelle) nei documenti di controllo per classificare tipi e categorie importanti. Per ulteriori informazioni, vedi [Element classification](/docs/services/discovery/element-classification.html). Element Classification non è disponibile per le istanze del servizio che hanno sottoscritto il piano **Premium**. [Risolto](/docs/services/discovery/release-notes.html#5jun)
- È stato aggiunto un supporto linguistico di base per il cinese semplificato e l'olandese. Per ulteriori informazioni, vedi il documento relativo al [supporto per la lingua](/docs/services/discovery/language-support.html). Attualmente, le raccolte in cinese semplificato e olandese devono essere create con l'API.
- Sono stati aggiunti due nuovi parametri per il Data Crawler: `proxy_host_port` e `read-timeout`. Vedi [Configurazione del Data Crawler](/docs/services/discovery/data-crawler-discovery.html) per i dettagli.
- Potrebbero essere riscontrati i seguenti problemi in fase di inserimento di documenti PDF: [Risolto](/docs/services/discovery/release-notes.html#21feb)
  - Quando vengono eseguite query degli avvisi di inserimento, il campo `file_type` per i documenti pdf viene restituito come `html`.
  - Il campo `file_type` nell'oggetto `extracted_metadata` dei risultati per i documenti pdf è impostato su `html`.
  - L'API dei dettagli del documento restituisce anche il campo `file_type` per i documenti pdf come `html`.
- Se stai inserendo JSON, gli array di tipo misto non sono supportati.  

Strumentazione {{site.data.keyword.discoveryshort}}:

- È stato aggiunto un Visual Query Builder per la versione beta di {{site.data.keyword.discoveryfull}} Knowledge Graph. Vedi [Query di Knowledge Graph utilizzando la strumentazione {{site.data.keyword.discoveryshort}}](/docs/services/discovery/building-kg.html#querying-kg)

## 30 novembre 2017

- È stata rilasciata la versione beta di {{site.data.keyword.discoveryfull}} Knowledge Graph, che fornisce dei nuovi endpoint per l'esecuzione di query di entità e relazioni sui documenti. Ciò include le ricerche basate sul contesto e la classificazione della pertinenza. Questa funzione beta è disponibile solo per gli utenti del piano **Advanced**. Non è disponibile negli ambienti **Dedicated**. [Risolto](/docs/services/discovery/release-notes.html#8mar) Per ulteriori informazioni, vedi [{{site.data.keyword.discoveryfull}} Knowledge Graph](/docs/services/discovery/building-kg.html). Una dichiarazione che spiega le funzioni beta è disponibile [qui](/docs/services/discovery/release-notes.html#beta-features).
  - Problema noto in {{site.data.keyword.discoveryfull}} Knowledge Graph: tutti i nomi di tipo di entità e di tipo di relazione vengono convertiti in maiuscole durante l'inserimento. Ad esempio, l'entità "GeoPoliticalEntity" viene convertita in "GEOPOLITICALENTITY," e la relazione "partOf" viene convertita in "PARTOF." [Risolto](/docs/services/discovery/release-notes.html#5mar)
- [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery/watson-discovery-news.html) è stato rilasciato in due lingue aggiuntive: coreano (`collection_id`: `news-ko`) e spagnolo (`collection_id`: `news-es`). {{site.data.keyword.discoverynewsfull}} in coreano e spagnolo sono disponibili per l'utilizzo solo tramite l'API; per informazioni sull'esecuzione di una query di una raccolta tramite l'API, vedi la [Guida di riferimento per le API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")][Resolved](/docs/services/discovery/release-notes.html#26jan)(https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection){: new_window}. {{site.data.keyword.discoverynewsfull}} in inglese ora ha il `collection_id` `news-en`. In precedenza, il `collection_id` era `news`; se stai usando il `collection_id` precedente, continuerà a funzionare; tuttavia, sarebbe opportuno passare al nuovo `collection_id` per i nuovi progetti.
- I risultati della query restituiscono un valore `score`, che indica la pertinenza relativa tra i risultati della query. A partire dal 30 novembre 2017, il modo in cui viene calcolato il punteggio (`score`) è cambiato. Il valore `score` deve essere utilizzato solo per classificare i documenti in una singola ricerca, non in un ambito che coinvolge diverse ricerche o sessioni. Se hai formato una raccolta, un valore `score` viene restituito nei risultati di una query in linguaggio naturale. Poiché il punteggio (`score`) indica la pertinenza relativa tra i risultati della query, non deve essere utilizzato come una soglia. Per impostare le soglie, utilizza invece il valore `confidence`, che indica la pertinenza del risultato rispetto al modello formato. Per ulteriori informazioni sull'impostazione di soglie, vedi il documento relativo ai [punteggi di affidabilità](/docs/services/discovery/train-tooling.html#confidence).
- A partire da questa release, il richiamo dei passaggi rileva i limiti delle frasi e prova a restituire passaggi con un inizio e una fine che coincidono con l'inizio e la fine di una frase. In precedenza, molti passaggi iniziavano o finivano da qualche parte a metà frase. Vedi [Passaggi](/docs/services/discovery/query-parameters.html#passages) per ulteriori informazioni sul richiamo dei passaggi.

## 15 novembre 2017
{: #15nov}

Strumentazione {{site.data.keyword.discoveryshort}}:

- È stato aggiunto l'arricchimento [Relation Extraction](/docs/services/discovery/building.html#relation-extraction), che include l'opzione per incorporare un modello di relazione personalizzato creato con {{site.data.keyword.knowledgestudiofull}}.
- La strumentazione {{site.data.keyword.discoveryshort}} dell'arricchimento [Entity Extraction](/docs/services/discovery/building.html#entity-extraction) ora include l'opzione di incorporare un modello di entità personalizzato creato con {{site.data.keyword.knowledgestudiofull}}.
- L'opzione di creare una raccolta in lingua giapponese è stata rimossa dalla strumentazione {{site.data.keyword.discoveryshort}}; tuttavia, l'opzione di creare una raccolta in lingua giapponese utilizzando l'API {{site.data.keyword.discoveryshort}} continua a essere disponibile.
- La strumentazione {{site.data.keyword.discoveryshort}} ora supporta gli ambienti diffusi su diversi canali.

## 10 novembre 2017

Strumentazione {{site.data.keyword.discoveryshort}}:

- Alla strumentazione {{site.data.keyword.discoveryshort}} sono state aggiunte delle ulteriori opzioni per il richiamo dei passaggi. Quando esegui una query, puoi ora specificare i campi da cui vuoi che vengano restituiti i passaggi, il numero di passaggi da restituire e il numero massimo di caratteri per ogni passaggio. Vedi [Passaggi](/docs/services/discovery/query-parameters.html#passages) per i limiti, i minimi e i massimi.

## 8 novembre 2017
{: #8nov}

La stringa della versione per tutte le chiamate API è cambiata da `2017-11-07` a `2017-10-16`. Questa versione:
- Ha spostato il punteggio (`score`) in ciascuna query a un nuovo oggetto denominato `result_metadata`.
- Se la raccolta oggetto della query era stata formata, ed è una query in linguaggio naturale, `result_metadata` includerà un campo `confidence` che visualizza il punteggio di affidabilità per tale risultato. Per i dettagli, vedi [Punteggi di affidabilità](/docs/services/discovery/train-tooling.html#confidence).
- I campi che includono spazi vuoti (ad esempio: `body.additional reading`) saranno esclusi mediante filtro durante l'inserimento. La descrizione `notices` indicherà `The field 'additional reading' is invalid: whitespace, '.', '#' and ',' are invalid in a field name`.
- Il campo `result_metadata` verrà escluso mediante filtro durante l'inserimento.

## 16 ottobre 2017

- La stringa della versione per tutte le chiamate API è cambiata da `2017-10-16` a `2017-09-01`. Questa versione abbandona, perché obsoleto, il supporto per caricare nuovi documenti nelle raccolte esistenti arricchite con gli arricchimenti {{site.data.keyword.alchemylanguageshort}} e per creare nuove raccolte e arricchirle con gli arricchimenti {{site.data.keyword.alchemylanguageshort}}. Le raccolte esistenti arricchite con {{site.data.keyword.alchemylanguageshort}} devono essere migrate agli arricchimenti {{site.data.keyword.nlushort}} il più presto possibile. Vedi [Migrazione degli arricchimenti a {{site.data.keyword.nlushort}}](/docs/services/discovery/migrate-nlu.html#migrating-enrichments-to-natural-language-understanding) per i dettagli. La strumentazione {{site.data.keyword.discoveryshort}} utilizza anche la versione `2017-10-16`; per ulteriori informazioni, vedi di seguito.

Strumentazione {{site.data.keyword.discoveryshort}}:

- La strumentazione {{site.data.keyword.discoveryshort}} utilizza la stringa della versione API `2017-10-16`; pertanto, se stai utilizzando la strumentazione, non sarai più in grado di caricare i documenti nelle raccolte {{site.data.keyword.alchemylanguageshort}} esistenti o di creare nuove raccolte arricchite con gli arricchimenti {{site.data.keyword.alchemylanguageshort}} dopo il 16 ottobre 2017 (`2017-10-16`).  Se vuoi continuare a utilizzare la strumentazione {{site.data.keyword.discoveryshort}} per arricchire le raccolte, migra prima le tue raccolte a {{site.data.keyword.nlushort}}. Vedi [Migrazione degli arricchimenti a {{site.data.keyword.nlushort}}](/docs/services/discovery/migrate-nlu.html#migrating-enrichments-to-natural-language-understanding) per i dettagli. 
- Il **Data Schema Explorer** visualizza le query di esempio per diversi arricchimenti nella raccolta {{site.data.keyword.discoverynewsfull}}. Presenta ora anche un link **Show more values** che visualizzerà dei valori di esempio aggiuntivi per tale arricchimento in {{site.data.keyword.discoverynewsfull}}.
- Molteplici potenziamenti della produttività, compresa la combinazione delle statistiche di raccolta, di errori e avvertenze e di analisi approfondite dei dati nella schermata **Manage data**.
- È stato aggiunto un messaggio che visualizza un avviso quando termina l'elaborazione dei documenti.

## 9 ottobre 2017

- Una nuova metrica di aggregazione `unique_count` è disponibile nell'API. Restituirà un conteggio delle istanze univoche del campo specificato in una raccolta. Vedi [unique_count](/docs/services/discovery/query-aggregations.html#unique_count) per ulteriori informazioni,

Strumentazione {{site.data.keyword.discoveryshort}}:

- Le aggregazioni Histogram e Timeslice sono ora supportate nel **Visual Query Builder**. Ora disponi anche dell'opzione di attivare il rilevamento delle anomalie per le query Timeslice.
- Il **Data Schema Explorer** visualizza le query di esempio per l'arricchimento scelto. Presenta ora anche un link **Show more values" che visualizzerà dei valori di esempio aggiuntivi per tale arricchimento.
- È stato aggiunto un menu hamburger per spostarsi più rapidamente nelle schermate **Manage data**, **View data schema** e **Build queries**.

### 3 ottobre 2017

- La segmentazione del documento è ora disponibile. Vedi [Suddivisione di documenti con la segmentazione del documento](/docs/services/discovery/building.html#doc-segmentation).

### 29 settembre 2017

- {{site.data.keyword.discoveryshort}} è stato avviato nella regione `Germany` in data 29 settembre 2017. Al fine di rispettare i regolamenti UE sui dati, gli arricchimenti AlchemyLanguage non sono supportati in questa regione.
- Problema noto: i campi di query non possono contenere spazi vuoti. Quando si scrive una query in {{site.data.keyword.discoveryshort}}, se qualche campo della query contiene uno spazio vuoto (ad esempio `body.additional reading`), riceverai un errore `400: Invalid query syntax error`. [Risolto](/docs/services/discovery/release-notes.html#8nov)

### 25 settembre 2017

- Un piano dei prezzi Premium è ora disponibile. Per ulteriori informazioni, vedi [Piani dei prezzi {{site.data.keyword.discoveryshort}}](/docs/services/discovery/pricing-details.html).
- È stata aggiunta la capacità di eseguire query, elencare campi ed eseguire query degli avvisi su tutte le raccolte nello stesso ambiente. Vedi [Query di più raccolte](/docs/services/discovery/using.html#multiple-collections) per i dettagli.
- Le informazioni sul supporto linguistico per {{site.data.keyword.discoveryshort}} sono disponibili in [Supporto linguistico](/docs/services/discovery/language-support.html)

Strumentazione {{site.data.keyword.discoveryshort}}:
- Il Visual Query Builder è passato dallo stato beta allo stato di disponibilità generale (GA, general availability). Le aggregazioni Filter, Timeslice e Histogram non sono attualmente supportate con il Visual Query Builder. Fai clic su **Include analysis of your results** e quindi su **Edit in Query Language** nella schermata **Build queries** per scrivere queste aggregazioni.
- È stata aggiunta la funzionalità beta di eseguire la deduplicazione sulle query {{site.data.keyword.discoverynewsfull}}.
- Oltre alle raccolte in inglese, tedesco e spagnolo, puoi ora creare raccolte in arabo, francese, italiano, coreano, giapponese e portoghese (Brasile).
- Problema noto: la strumentazione {{site.data.keyword.discoveryshort}} non supporta gli ambienti diffusi su diversi canali. [Risolto](/docs/services/discovery/release-notes.html#15nov)

### 14 settembre 2017

Strumentazione {{site.data.keyword.discoveryshort}}:

- È stato aggiunto il Data Schema Explorer, che visualizza i campi e i valori nei tuoi documenti trasformati. Queste informazioni possono essere utilizzate per comprendere la struttura dei dati della tua raccolta prima di creare delle query utilizzando il Discovery Query Language. Lo schema di dati può essere visualizzato in due modi: in base al documento (vista Document) o in base al campo (vista Collection). Per accedere al Data Schema Explorer: nella schermata **My Data Insights**, fai clic sul pulsante **View data schema** oppure fai clic sull'icona **View Data Schema** sulla sinistra.

### 6 settembre 2017

- È stata aggiunta la capacità beta di deduplicare i documenti restituiti dalla tua query. Questa funzione beta funziona sia con le raccolte Watson Discovery News sia con quelle private. Vedi [Esclusione di documenti duplicati dai risultati della query](/docs/services/discovery/query-parameters.html#deduplication) per i dettagli.

La deduplicazione dei documenti è attualmente supportata solo come una funzionalità beta. Per ulteriori informazioni, vedi la dichiarazione relativa ai beta nella parte superiore di questo documento.

### 31 agosto 2017

- La stringa della versione per tutte le chiamate API è cambiata da `2017-09-01` a `2017-08-01`. Questa versione include degli aggiornamenti che escluderanno mediante filtro i seguenti campi JSON non validi durante l'anteprima e l'inserimento in modo che vengano inseriti solo campi JSON validi. Aggiorna la tua stringa della versione a `2017-09-01` per evitare conflitti e possibili errori.

   - `id`, `score` e `highlight` al livello superiore (puoi continuare ad aggiungere documenti alla tua raccolta utilizzando gli ID documento con la funzione `add a document`. Vedi la [Guida di riferimento per le API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#add-doc){: new_window} per i dettagli.
   - i nomi di campo che hanno come prefisso `_` al livello superiore (di conseguenza, quando esegui una query per un documento in base all'ID, puoi eseguire una query per `id` invece di `_id`.)
   - `#` e `,` nel nome di campo
   - i nomi di campo che hanno come prefisso `+` e `-`
   - i valori vuoti `"` `"` per un nome di campo

**Nota:** se i tuoi documenti JSON includono questi caratteri nei nomi di campo oppure `id`, `score` e `highlight` al livello superiore, devi rimuoverli prima di aggiungere i documenti alla tua raccolta, altrimenti questi campi saranno vuoti. Per evitare questo problema, puoi creare una configurazione personalizzata e normalizzare il tuo JSON prima di aggiungere documenti alla tua raccolta. Vedi [Configurazione personalizzata](/docs/services/discovery/building.html#custom-configuration).  Inoltre, i documenti che includono i caratteri di punteggiatura `?`, `:` o `#` nel nome file causeranno errori quando viene eseguito l'inserimento. Rinomina gli eventuali documenti che includono questi caratteri prima di inserirli.

- I metodi di richiamo per `natural_language_query` sono stati aggiornati per migliorare la pertinenza dei risultati mettendo in corrispondenza le parole con la semantica correlata. Questo aggiornamento influenza solo le raccolte che non hanno avuto una formazione della pertinenza. Se stai utilizzando `natural_language_query` e non hai condotto alcuna formazione della pertinenza, potresti vedere un miglioramento nell'ordine dei risultati restituiti.

Strumentazione {{site.data.keyword.discoveryshort}}:

- Modifiche al builder di query per semplificare l'alternanza tra le opzioni di query Discovery Query Language e Natural Language, così come tra query, filtro e aggregazione.


### 25 agosto 2017

- L'array `passages` ora include `field`, `start_offset` e `end _offset`. `field` è il nome del campo da cui è stato estratto il passaggio. `start_offset` è il carattere iniziale del testo del passaggio all'interno del campo. `end_offset` è il carattere finale del testo del passaggio all'interno del campo.

Strumentazione {{site.data.keyword.discoveryshort}}:
questo potenziamento della creazione di query è disponibile nella schermata **Build queries**.

-  È stata aggiunta la capacità beta di scrivere query in {{site.data.keyword.discoveryshort}} Query Language con un builder visivo. Fai clic su **Build in visual mode** nelle sezioni **Search for documents** e **Limit which documents you query** per provarla. Man mano che crei la tua query visivamente, verrà visualizzata nel **{{site.data.keyword.discoveryshort}} Query Language** sotto di essa.

   Il builder di query visivo è attualmente supportato solo come una funzionalità beta. Per ulteriori informazioni, vedi la dichiarazione relativa ai beta nella parte superiore di questo documento.

### 18 agosto 2017

Strumentazione {{site.data.keyword.discoveryshort}}:

- È stato aggiunto il supporto per le aggregazioni e le condizioni nidificate al build di aggregazioni visivo beta introdotto in data [11 agosto 2017](/docs/services/discovery/release-notes.html#11aug). C'è un limite di 3 condizioni per ogni riga di aggregazione.

   Il builder di aggregazioni visivo è attualmente supportato solo come funzionalità beta. Per ulteriori informazioni, vedi la dichiarazione relativa ai beta nella parte superiore di questo documento.

### 11 agosto 2017
{: #11aug}

Strumentazione {{site.data.keyword.discoveryshort}}:

Entrambe le funzioni sono potenziamenti della creazione di query e sono disponibili nella schermata **Build queries**.

- È stata aggiunta l'opzione per selezionare una query da una serie di query e aggregazioni di esempio precostruite. Fai clic su **Use a sample query** nella parte superiore destra per accedere all'elenco. Se stai eseguendo una query di una raccolta di dati privata, gli esempi utilizzano `top entities`, `categories`, ecc. disponibili nella tua raccolta. Queste query possono essere utilizzate come punto di partenza per scrivere le tue query. Query di esempio sono disponibili per le raccolte sia private sia {{site.data.keyword.discoverynewsfull}}.

-  È stata aggiunta la capacità di scrivere aggregazioni con un builder visivo. Fai clic su **Build in visual mode** sopra al campo **Write an aggregation query using the {{site.data.keyword.discoveryshort}} Query Language** per provarla. Man mano che crei la tua aggregazione visivamente, la query verrà visualizzata in **{{site.data.keyword.discoveryshort}} Query Language** sotto di essa.  

   Il builder di aggregazioni visivo è attualmente supportato solo come funzionalità beta. Per ulteriori informazioni, vedi la dichiarazione relativa ai beta nella parte superiore di questo documento.

### 31 luglio 2017

- È stata rilasciata una nuova versione di {{site.data.keyword.discoverynewsfull}}. La versione originale è stata rinominata {{site.data.keyword.discoverynewsfull}} Original ed è stata ritirata con una rimozione dal servizio datata **15 gennaio 2018**. Vedi [Migrazione da Watson Discovery News Original](/docs/services/discovery/migrate-bwdn.html) per le istruzioni di migrazione.
  **Nota:** se hai creato una nuova istanza di {{site.data.keyword.discoveryshort}}, avrai accesso solo alla nuova versione di {{site.data.keyword.discoverynewsfull}}.

- È stato rilasciato un nuovo piano dei prezzi per {{site.data.keyword.discoveryfull}}. Vedi [Piani dei prezzi {{site.data.keyword.discoveryshort}}](/docs/services/discovery/pricing-details.html) per i dettagli.

- La stringa della versione per tutte le chiamate API è cambiata da `2017-08-01` a `2017-07-19`. Questa versione include gli aggiornamenti per il nuovo piano dei prezzi e la nuova versione di Watson Discovery News. Aggiorna la stringa della versione per evitare conflitti e possibili errori.

### 19 luglio 2017

 - Come parte della modifica dei prezzi annunciata per il 1° agosto 2017, gli utenti attualmente nell'obsoleto piano di **prova gratuita di 30** verranno automaticamente migrati al piano **Lite**. Come conseguenza di questa transazione, gli utenti esistenti potrebbero aver raggiunto o superato il limite del piano Lite per quanto riguarda documenti _(2000)_, archiviazione _(200Mb)_ o numero di raccolte _(2)_. Se hai superato il limite del piano **Lite**, non potrai aggiungere ulteriore contenuto nel servizio ma puoi comunque eseguire query delle raccolte. Puoi visualizzare lo stato attuale di tutti questi limiti utilizzando l'API o la strumentazione {{site.data.keyword.discoveryshort}}. Per poter essere nuovamente in grado di aggiungere contenuto all'istanza {{site.data.keyword.discoveryshort}}, devi eseguire una delle seguenti operazioni:
   - rimuovi raccolte e/o documenti in modo che i limiti del piano **Lite** non siano superati.
     I documenti possono essere eliminati singolarmente oppure tramite l'API utilizzando il metodo [delete-doc](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-doc) oppure possono essere eliminate delle intere raccolte utilizzando la strumentazione o l'API con il metodo [delete-collection](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-collection)
   - esegui un upgrade del tuo piano a un livello che soddisfi le tue esigenze di archiviazione.
 - I clienti con ambienti di dimensione **`1`** **`2`** o **`3`** verranno automaticamente migrati al piano **Advanced**.

### 17 luglio 2017

 - Le seguenti funzionalità sono state passate dallo stato beta allo stato di disponibilità generale (GA, general availability):

   - Formazione della pertinenza
   - Query in linguaggio naturale
   - Evidenziazione

 - A partire da questa release, {{site.data.keyword.discoveryfull}} sta cambiando il suo meccanismo di arricchimento da {{site.data.keyword.alchemylanguageshort}} a {{site.data.keyword.nlushort}}. {{site.data.keyword.alchemylanguageshort}} sta per essere dichiarato obsoleto; devi iniziare a utilizzare {{site.data.keyword.nlushort}} il prima possibile. Vedi [Migrazione dagli arricchimenti {{site.data.keyword.alchemylanguageshort}} agli arricchimenti {{site.data.keyword.nlushort}}](/docs/services/discovery/migrate-nlu.html) per i dettagli.
   **Nota:** quando si esegue l'integrazione con Watson Knowledge Studio, deve essere ancora utilizzata la configurazione dell'arricchimento {{site.data.keyword.alchemylanguageshort}}. Vedi [Integrazione con {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery/integrate-wks.html) per i dettagli.

 - La stringa della versione per tutte le chiamate API è stata modificata da `2017-06-25` a `2017-07-19`. Questa versione abilita una configurazione predefinita NLU sulla creazione della raccolta. Dovresti essere ancora in grado di eseguire l'arricchimento con {{site.data.keyword.alchemylanguageshort}} nelle versioni precedenti.

    La configurazione predefinita è stata aggiornata per utilizzare {{site.data.keyword.nlushort}}. Devi aggiornare la stringa della versione il prima possibile per evitare conflitti e possibili errori.

 - Strumentazione Discovery:

    Le schede di analisi approfondita per le raccolte arricchite con gli arricchimenti {{site.data.keyword.alchemylanguageshort}} non verranno più aggiornate automaticamente. Devi eseguire la migrazione della tua raccolta agli arricchimenti {{site.data.keyword.nlushort}} perché le schede di analisi approfondita vengano aggiornate.

    Se hai creato un raccolta antecedente al **18 luglio 2017** e hai applicato la configurazione predefinita (**Default Configuration**), tale raccolta è stata arricchita con gli arricchimenti {{site.data.keyword.alchemylanguageshort}}. Se applichi la configurazione predefinita (**Default Configuration**) a una raccolta dopo tale data, verranno utilizzati gli arricchimenti {{site.data.keyword.nlushort}} (il nome della configurazione sarà commutato alla configurazione predefinita con NLU (**Default Configuration with NLU**) nella strumentazione). Poiché ne è in corso l'indicazione come obsoleti, gli arricchimenti {{site.data.keyword.alchemylanguageshort}} non devono essere utilizzati con le nuove raccolte.

### 30 giugno 2017
{: #30jun}

 -  La funzionalità di normalizzazione delle entità introdotta come funzione beta il 5 maggio 2017 è stata passata allo stato di disponibilità generale (GA, general availability). Vedi il documento relativo alla [creazione di una configurazione personalizzata per normalizzare le entità](/docs/services/discovery/normalize-entities.html).

### 23 giugno 2017

 - La stringa della versione per tutte le chiamate API è cambiata da `2017-06-25` a `2016-12-01`. La nuova stringa della versione abilita gli arricchimenti in tedesco (`de`) o spagnolo (`es`) se la lingua di una raccolta è impostata su una di queste lingue. In precedenza, tutti gli arricchimenti venivano eseguiti in inglese indipendentemente dall'impostazione della lingua di una raccolta.

    Se non utilizzi gli arricchimenti in lingue diverse dall'inglese, puoi continuare a utilizzare la stringa della versione `2016-12-01`. Devi tuttavia aggiornare la stringa della versione il prima possibile per evitare potenziali conflitti futuri.

 - Il rilevamento delle anomalie è ora disponibile come parte delle aggregazioni `timeslice` come una funzionalità GA. Vedi [Rilevamento delle anomalie di intervallo di tempo](/docs/services/discovery/query-aggregations.html#anomaly-detection) per i dettagli.

 - Strumentazione Discovery:

   - È stata aggiunta la capacità beta di migliorare la pertinenza dei risultati della query utilizzando la strumentazione Discovery (strumentazione della pertinenza). Vedi il documento relativo al [miglioramento della pertinenza dei tuoi risultati della query con la strumentazione Discovery](/docs/services/discovery/train-tooling.html).

### 19 giugno 2017

  - Strumentazione Discovery:

    - È stata aggiunta l'opzione per specificare la lingua dei documenti in una nuova raccolta come inglese, spagnolo o tedesco. Per utilizzarla, scegli **Select the language of your documents** nella finestra di dialogo **Name your new collection**.

    - È stata aggiunta una scheda **Summary** alla schermata **Build queries**. La scheda **Summary** visualizza una panoramica dei risultati della query completi forniti nella scheda **JSON** esistente. La visualizzazione **Summary** varierà in base alla tua query e ai tuoi arricchimenti. Le informazioni che possono essere visualizzate includono: nome o ID documento, statistiche di aggregazione, passaggi dei documenti in ordine di pertinenza e risultati in base all'arricchimento.

    - È stata aggiunta un'opzione Natural Language Query alla schermata **Build queries**. Per utilizzarla, fai clic su **Ask a question in plain language** nella sezione **Search for documents**; verrà visualizzato un campo dove potrai immettere la tua domanda. È ora possibile accedere al campo di query originale (precedentemente denominato **Enter a query or keyword**) facendo clic sul pulsante **Use the Discovery Query Language**.

    - La schermata **Build queries** è stata riprogettata ma tutti i campi e tutte le opzioni permangono. Ecco di seguito indicati i vecchi nomi e quelli nuovi per i campi.

| **Vecchio nome campo**                                           | **Nuovo nome campo o sezione**                                                                                             |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| Write and run a query                                    | Search for documents                                                                                                  |
| Narrow your query results (Filter)                       | Limit which documents you query                                                                                       |
| Group query results (Aggregation)                        | Include analysis of your results                                                                                      |
| Fields to display                                        | Il nome non è cambiato ma è stato spostato alla nuova sezione **Customize display options**.       |
| Number of documents to return (Count)                    | Number of documents to return [questo campo è stato spostato alla sezione **Customize display options**.]                    |
| Include matching passages                                | Include relevant passages [questo campo è stato spostato alla sezione **Customize display options**.]                        |
| Number of query fields to skip at the beginning (Offset) | Number of query results to skip at the beginning [questo campo è stato spostato alla sezione **Customize display options**.] |

### 5 giugno 2017

 - Le query Watson Discovery News ora visualizzano solo le prime 150 parole di ciascun articolo nei campi JSON `text` e `alchemyapi_text`. Il campo `blekko.snippet` visualizzerà solo la prima frase dell'array di frammento.

### 30 maggio 2017
{: #30may}

 - Il parametro `passages` nell'API di query è stato passato dallo stato beta a quello di disponibilità generale (GA, general availability).

### 25 maggio 2017

 - Strumentazione Discovery: in questa release è stata aggiunta l'evidenziazione dei campi di query. Questa funzione aggiunge un'evidenziazione gialla ai nomi campo nel JSON del riquadro Results. Tutti i campi di cui viene eseguita una query oppure usati come base di filtro sono evidenziati per ciascun risultato, anche se il contenuto del campo non corrisponde alla query. Gli eventuali campi utilizzati nelle aggregazioni sono anch'essi evidenziati nei risultati della query, anche se tale evidenziazione interessa solo la prima operazione di aggregazione.

### 10 maggio 2017

 - I metodi `query` e `notices` ora supportano il parametro `highlight`. Il parametro è un booleano. Quando esegui una query con `highlight` specificato come `true`, il servizio restituisce un output che include un nuovo campo `highlight` in cui le parole che corrispondono alla query sono racchiuse in tag HTML `*` (enfasi). Vedi [Parametri di query](/docs/services/discovery/query-parameters.html#highlight) per i dettagli.

 - È possibile che l'eliminazione di un ambiente venga completata solo parzialmente, con una conseguente situazione in cui non è possibile creare un nuovo ambiente perché è consentito solo un singolo ambiente per ogni istanza del servizio. Se provi ad eliminare e quindi a creare un ambiente ma constati che l'una o l'altra di queste operazioni si blocca nello stato `pending`, è probabile che tu abbia riscontrato questo problema. Come soluzione alternativa, esegui nuovamente l'operazione di eliminazione per completarla e quindi crea il nuovo ambiente.

### 8 maggio 2017

 - È stato aggiornato il modello di punteggio del tono dell'emozione per migliorare la precisione negli arricchimenti di analisi delle emozioni (`docEmotion`). L'insieme di dati di formazione è stato espanso e la progettazione delle funzioni è stata modificata; di conseguenza, il modello ha una precisione maggiore sull'insieme di dati di benchmark.

### 5 maggio 2017

 - La normalizzazione delle entità è ora disponibile per l'utilizzo con i servizi Discovery che utilizzano un modello personalizzato generato da Watson Knowledge Studio. La normalizzazione delle entità inserisce dei nomi normalizzati (canonici) per riferimenti differenti alla stessa persona o allo stesso oggetto nel documento di origine. Vedi il documento relativo alla [creazione di una configurazione personalizzata per normalizzare le entità](/docs/services/discovery/normalize-entities.html).

     **Nota:** la normalizzazione delle entità è attualmente supportata solo come una funzionalità beta. Per ulteriori informazioni, vedi la dichiarazione relativa ai beta nella parte superiore di questo documento. [Risolto](/docs/services/discovery/release-notes.html#30jun)

Strumentazione {{site.data.keyword.discoveryshort}}:

 - Il log degli errori della strumentazione non è più limitato a un massimo di otto (8) pagine di risultati. Il log degli errori continua a visualizzare l'ID documento, se il nome documento non è disponibile.

 - I nomi configurazione sono limitati a 50 caratteri e devono essere costituiti dai caratteri `[a-zA-Z0-9-_]`. 

 - Il parametro `passages` precedentemente disponibile solo tramite l'API è ora disponibile tramite la strumentazione nonché tramite l'API.

### 25 aprile 2017

  - Il servizio ora ti consente di fornire *dati di formazione* per migliorare l'accuratezza dei tuoi risultati della query. Quando fornisci un'istanza Discovery con i dati di formazione, il servizio utilizza gli algoritmi Watson avanzati per determinare i risultati più pertinenti. Man mano che aggiungi ulteriori dati di formazione, l'istanza del servizio diventa più accurata e sofisticata nei risultati che restituisce. Per informazioni, vedi il documento relativo al [miglioramento della pertinenza dei tuoi risultati della query](/docs/services/discovery/train.html) e la [Guida di riferimento per le API](http://www.ibm.com/watson/developercloud/discovery/api/v1/#training-data).

  - L'API ora supporta il parametro `natural_language_query` come una release beta. Questo parametro ti consente di specificare una query in linguaggio naturale invece che in linguaggio di query del servizio Discovery. Per informazioni, vedi il metodo [Eseguire una query della tua raccolta](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query-using-get) nella Guida di riferimento per le API.

  - Aggiornamenti della documentazione e correzioni di errori.

### 14 aprile 2017

Dei potenziamenti sono stati aggiunti all'API query (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`). Per informazioni, vedi il metodo [Eseguire una query della tua raccolta](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query-using-get) nella Guida di riferimento per le API.

  - L'API query supporta ora il parametro `passages`. Se il parametro è impostato su `true`, la query restituisce una serie dei passaggi più pertinenti dai documenti nella tua raccolta. I passaggi sono generati da sofisticati algoritmi Watson per determinare i migliori passaggi di testo da tutti i documenti restituiti dalla query. Questo ti consente di trovare informazioni e contesto più precisamente. Per informazioni, vedi il metodo [Eseguire una query della tua raccolta](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query-using-get) nella Guida di riferimento per le API.

    - La specifica di `passages=true` nella tua query può ridurre le prestazioni come risultato di un aumento dell'elaborazione per estrarre i passaggi. Con ambienti più grandi, l'impatto sulle prestazioni può essere ridotto.

    - Il parametro `passages` è supportato solo su raccolte private. Non è supportato nella raccolta Watson Discovery News.

    - Il parametro `passages` attualmente restituisce un massimo di 10 risultati. Il numero di risultati restituiti non può essere modificato. [Aggiornamento](/docs/services/discovery/query-parameters.html#passages_count)

    - Il parametro `passages` restituisce un massimo di tre (3) passaggi da qualsiasi specifico documento nella raccolta. Se un documento contiene più di tre passaggi pertinenti aggiuntivi, il parametro non li restituisce.

### 7 aprile 2017

- L'API query /`GET /v1/environments/{environment_id}/collections/{collection_id}/query`) ora supporta il parametro `sort`, che ti consente di specificare un elenco separato da virgole di campi nel documento in base a cui ordinare. Per informazioni, vedi il metodo [Eseguire una query della tua raccolta ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query-using-get){: new_window} nella Guida di riferimento per le API.
- Il parametro `timeslice` per le aggregazioni di query ora gestisce correttamente le date in formato epoch UNIX. Vedi [Guida di riferimento per le query](/docs/services/discovery/query-reference.html#aggregations) per informazioni sulle aggregazioni e sul parametro `timeslice`.
- Miglioramenti ai messaggi di errore.
- Aggiornamenti all'SDK Java del servizio. Vedi la [Guida di riferimento per le API](http://www.ibm.com/watson/developercloud/discovery/api/v1/?java) per i dettagli.
- Le seguenti limitazioni all'utilizzo di caratteri jolly nelle query sono state corrette e ora funzionano in modo appropriato.

  - Solo un singolo carattere jolly funzionava in una specifica query. Ad esempio, `query-month:*ctober` funzionava, ma `query-month:*ctobe*` generava un errore di analisi.
  - I caratteri jolly non funzionavano con le query contenenti lettere maiuscole. Ad esempio, data la coppia chiave/campo `{"borrower": "GOVERNMENT OF INDIA"}`, `query-borrower:*ndia` restituiva dei risultati mentre invece `query-borrower:*NDIA` non lo faceva.

**Nota:** i caratteri jolly non sono necessari all'interno delle frasi nelle query. Ad esempio, data la coppia chiave/campo `{"borrower": "GOVERNMENT OF TIMOR"}`, `query-borrower:"GOVERNMENT OF TIMOR"` restituisce dei risultati mentre invece `query-borrower:"GOVERNMENT OF TI*OR"` non lo farà. L'utilizzo di un carattere jolly non è applicabile all'interno delle frasi perché tutti i caratteri all'interno delle virgolette (`"`) di una frase sono elaborati come se fossero preceduti da un carattere di escape.

### 24 marzo 2017

- È stato aggiunto il filtro alla schermata "My data insights" nella strumentazione Discovery

### 15 marzo 2017

Sono stati rilevati i seguenti problemi noti.

-  Tutti i campi che vengono inseriti dai documenti HTML, PDF e Word vengono scritti come **string**. I campi JSON e i campi calcolati, come il punteggio del parere, sono scritti come definiti. [Aggiornamento](/docs/services/discovery/adding-content.html#adding-content-with-the-api-or-tooling)
- L'operazione `preview` attualmente non verifica la presenza di array JSON nidificati all'interno di un documento JSON inoltrato. Il servizio attualmente non supporta gli array JSON nidificati e, pertanto, un documento con degli array nidificati può superare con esito positivo l'operazione `preview` ma non riuscire quando viene eseguito un tentativo di inserimento. Vedi [Posso caricare gli array JSON?](/docs/services/discovery/troubleshooting.html#array)
- Se riscontri degli errori di inserimento con il messaggio `unsupported text language`, aggiorna la tua configurazione con l'opzione di arricchimento `"language": "english"` per forzare un'interpretazione di tutto il testo come se fosse in lingua inglese, come mostrato nel seguente esempio.
[Aggiornamento](/docs/services/discovery/migrate-nlu.html)
```json
"enrichments": [
   {
     "enrichment": "alchemy_language",
     "source_field": "author.label",
     "options": {
       "extract": "taxonomy,entity,relation,doc-emotion,doc-sentiment,concept,keyword",
       "sentiment": true,
       "quotations": true,
       "language": "english"
     }
   }
 ]
```
{: codeblock}

Sono stati corretti i seguenti bug.

- Sono state migliorate le prestazioni e la stabilità del servizio.

### 8 marzo 2017

 - È stato ottimizzato il backend, compresa l'aggiunta di nuovi timeout, per migliorare le prestazioni complessive.
 - È stato corretto un bug a causa del quale lo stato dell'ambiente che indica che gli ambienti sono liberi (di dimensione `0`) segnalava uno stato di in sospeso (`pending`) indipendentemente dallo stato effettivo.
 - La sola lingua nazionale attualmente supportata da {{site.data.keyword.discoveryshort}} è l'inglese (USA) (`en_US`). [Aggiornamento](/docs/services/discovery/language-support.html)

### 3 marzo 2017

- È stata aggiunta la schermata "My data insights" nella strumentazione Discovery

### 26 febbraio 2017

-     Le prestazioni dell'ambiente {{site.data.keyword.discoverynewsshort}} sono state migliorate.
-  Il servizio {{site.data.keyword.discoverynewsshort}} restituisce solo 50 risultati alla volta. Come soluzione temporanea, utilizza il parametro `offset` nella tua query per sfogliare i risultati.
-  Puoi inoltrare una nuova configurazione con un singolo documento utilizzando il seguente comando:

```bash
curl -X POST -u apikey:{apikey_value} -F "file=@wikipedia-sample.html" -F "configuration=$(cat config.json)" "https://gateway.watsonplatform.net/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2016-12-01"
```
{: pre}
-  I convertitori PDF e Word del servizio creano HTML come passo intermedio. Il servizio può applicare ulteriori trasformazioni e normalizzazioni sull'HTML intermedio prima della trasformazione finale in JSON normalizzato.

Sono stati corretti i seguenti bug.

-  I codici di errore sono stati migliorati.
-  Sono stati corretti diversi errori della documentazione.

### 16 febbraio 2017

-  Puoi ora utilizzare i selettori CSS per selezionare i campi JSON a cui puoi quindi applicare gli arricchimenti. Per informazioni, vedi [Utilizzo di selettori CSS per estrarre i campi](/docs/services/discovery/building.html#using-css).
-  Puoi ora aumentare la dimensione di un ambiente passando un nuovo parametro `size: X` al [metodo update-environment](http://www.ibm.com/watson/developercloud/discovery/api/v1/#update_environment), dove `X` è un numero intero compreso tra 0 e 3. Per informazioni sulle dimensioni e sugli attributi degli ambienti, vedi il [metodo create-environment](http://www.ibm.com/watson/developercloud/discovery/api/v1/#create_environment). [Aggiornamento](/docs/services/discovery/pricing-details.html)

    **Nota:** non puoi ridurre la dimensione di un ambiente esistente. Se vuoi ridurre la dimensione dell'ambiente, contatta il supporto {{site.data.keyword.IBM}} per assistenza.

-  È disponibile un nuovo operatore di query. L'operatore `::!` è stato aggiunto come un operatore not-equals unario. Ad esempio, puoi ora eseguire `query=field::!value` (non uguale). In precedenza, il solo operatore di esclusione era `:!` per l'operatore not-contains (ad esempio, `query=field:!value`).

Sono stati corretti i seguenti bug.

-  Sono stati applicati degli aggiornamenti della sicurezza.
-  Sono stati migliorati i messaggi di stato per gli avvisi di ricerca.

### 1° febbraio 2017

Le seguenti note si applicano in modo specifico alla release Data Crawler 1.3.0.
[Aggiornamento](/docs/services/discovery/data-crawler.html)

-   Il Data Crawler registra i valori `document_id` utilizzati per caricare i documenti e lo stato del caricamento. Gli avvisi di conversione non vengono conservati fuori dal log. Non è attualmente disponibile uno strumento per interagire con tali dati ma ci si aspetta che verranno sviluppati appena ce ne sarà il tempo. I dati sono accessibili tramite il database H2, che può essere configurato per utilizzare un DBMS remoto.

### 16 gennaio 2017

Le seguenti note si applicano in modo specifico alla release Data Crawler 1.2.5.
[Aggiornamento](/docs/services/discovery/data-crawler.html)

-  Il Data Crawler può, facoltativamente, eseguire il polling per lo stato del documento subito dopo il caricamento di un file. Questo controllo fa parte del concetto di Crawler di "caricamento di un documento" e, pertanto, quando viene abilitato, è virtualmente impossibile per il Crawler di caricare simultaneamente più documenti di quanti il servizio {{site.data.keyword.discoveryshort}} possa elaborare simultaneamente per l'utente.

    Un effetto collaterale della funzione `check_for_completion` è che il Crawler può anche mostrare all'utente perché un documento non è riuscito, quando ciò accade. Nel log di Crawler viene visualizzato qualsiasi avviso collegato a un documento che era stato caricato correttamente ma la cui elaborazione non era riuscita. Gli avvisi non vengono esportati in un file elaborabile ma IBM accoglierà con favore il suggerimento di una funzione in tal senso.

### 5 gennaio 2017

Le seguenti note descrivono i problemi che sono stati identificati dopo la release GA del 15 dicembre 2016.

[Aggiornamento: Guida di riferimento per le API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}

-   Se aggiungi un documento utilizzando la chiamata `POST /v1/environments/{environment_id}/collections/{collection_id}/documents`
    o `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]`, la chiamata restituisce un ID documento e lo stato **processing**. Se esegui quindi una query del documento utilizzando la chiamata `GET /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]`, lo stato rimane a **processing** fino al completamento dell'inserimento, punto al quale lo stato cambia in **available**.

    Se **aggiorni** un documento esistente utilizzando la chiamata `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]`, la chiamata **GET** corrispondente restituisce lo stato `available` anche se il servizio non ha ancora elaborato completamente il documento aggiornato. Lo stato `available` può fare riferimento al documento originale o al documento aggiornato. A meno che l'operazione di aggiornamento non restituisca un errore, non c'è attualmente un modo per determinare lo stato del documento aggiornato.

    Come soluzione temporanea, puoi attendere fino a 10 minuti dopo l'inoltro di un aggiornamento del documento prima di provare a eseguire una query del contenuto aggiornato.

### Release GA (General Availability), 15 dicembre 2016

Le seguenti note si applicano alla release GA (General Availability) del servizio {{site.data.keyword.discoveryfull}}.

#### Note generali
[Aggiornamento: Aggiunta di contenuto](/docs/services/discovery/adding-content.html)

Vedi la [Guida di riferimento per le API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window} per la versione API corrente,

[Aggiornamento: Integrazione con {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery/integrate-wks.html).

-   Non puoi attualmente specificare il tipo di dati dei campi. Tutti i campi sono indicizzati come testo (tipo di dati **string**). 
-   Se utilizzi l'API per gestire il servizio, devi specificare la versione API con ogni chiamata. La versione API corrente è **2016-12-01**. 

    **Nota:** la versione specifica non è implementata nella release GA ma deve essere comunque elencata per abilitare la compatibilità con le release future.

-   Puoi utilizzare il servizio con un modello personalizzato creato con {{site.data.keyword.knowledgestudiofull}}. Il modello personalizzato può essere utilizzato per arricchire i documenti inseriti. Devi utilizzare l'API per integrare il modello personalizzato con il servizio {{site.data.keyword.discoveryshort}}; non puoi eseguire l'integrazione utilizzando la strumentazione.

#### Gestione dati
[Aggiornamento](/docs/services/discovery/pricing-details.html)

-   Gli indici di ricerca non sono crittografati.
-   Le funzioni di backup e ripristino non sono controllabili dall'utente.

#### Ambienti
[Aggiornamento](/docs/services/discovery/pricing-details.html)

-   Puoi creare solo un singolo ambiente per ogni istanza del servizio per caricare i tuoi dati.
-   Il servizio {{site.data.keyword.discoveryshort}} si trova in una singola zona di disponibilità (Stati Uniti Sud).
-   I piani dedicati e premium non sono attualmente disponibili.

#### Dimensione dell'ambiente
[Aggiornamento](/docs/services/discovery/pricing-details.html)

-   Puoi scegliere una dimensione dell'ambiente solo quando crei un nuovo ambiente. La capacità di ridimensionare un ambiente non è attualmente disponibile per gli utenti.
-   La scelta di una dimensione dell'ambiente con maggiore RAM aumenta le prestazioni.
-   Al momento non ci sono suggerimenti di dimensione prescrittivi disponibili per gli specifici casi d'uso.
-   La dimensione personalizzata per i modelli {{site.data.keyword.knowledgestudiofull}} non è self-service. Per ulteriori
informazioni, contatta il rappresentante {{site.data.keyword.IBM}}.

#### Limitazioni dell'inserimento
[Aggiornamento](/docs/services/discovery/pricing-details.html)

-   La frequenza di inserimento è attualmente limitata a 100 operazioni simultanee di inserimento di documenti. Un'applicazione che inoltra i documenti al servizio per l'inserimento deve rispettare gli errori HTTP 429 e ridurre le richieste di inserimento di conseguenza.
-   Gli arricchimenti {{site.data.keyword.alchemylanguageshort}} sono limitati ai primi 50 kB per ogni campo.
-   Gli arricchimenti dai modelli personalizzati {{site.data.keyword.knowledgestudiofull}} non sono limitati ma suddividono i documenti in frammenti da 10-kB. Non viene annotata alcuna relazione oltre i limiti dei frammenti.

#### Limitazioni delle query
[Aggiornamento](/docs/services/discovery/using.html#query-concepts)

-   Un carico di query eccessivo può causare un riavvio automatico del processo di indice di ricerca.
-   Le applicazioni che emettono query devono implementare dei limiti ragionevoli al numero di query simultanee.

### Problemi noti
[Aggiornamento: Guida di riferimento per le API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}

[Aggiornamento: Strumentazione](/docs/services/discovery/getting-started-tool.html)

[Aggiornamento: Data Crawler](/docs/services/discovery/data-crawler.html)

[Aggiornamento: Arricchimenti](/docs/services/discovery/building.html#adding-enrichments)

[Aggiornamento: Aggiunta di contenuto](/docs/services/discovery/adding-content.html)

-   Non puoi eliminare un documento utilizzando la strumentazione. Se hai bisogno di eliminare un documento, devi utilizzare il metodo [Eliminare un documento](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-doc)) dell'API come descritto nella Guida di riferimento per le API.

-   L'API attualmente non supporta l'acquisizione di un elenco di avvisi (avvertenze ed errori) generati durante l'inserimento dei documenti. La strumentazione non è quindi in grado di mostrare un elenco di avvisi di inserimento e non esiste un modo semplice per determinare quali sono gli eventuali documenti sottoposti a ricerca per l'indicizzazione da Data Crawler per cui l'inserimento non è riuscito. 
-   Le informazioni sullo stato del documento non sono sempre accurate.
    -   Se un'operazione di inserimento impiega più tempo del timeout configurato di 10 minuti, il servizio notifica che il documento non è noto al servizio fino al completamento dell'operazione di inserimento. Dopo il completamento dell'operazione, lo stato del documento è disponibile e accurato.
    -   I documenti che sono stati indicizzati correttamente ma che hanno generato errori possono avere uno stato di **non riuscito** per un breve periodo finché non sarà stato eseguito un commit completo del documento all'indice. Dopo l'esecuzione del commit del documento all'indice, lo stato elencato è corretto.
-   Non puoi utilizzare la strumentazione per sostituire un documento specifico. Se provi un'operazione di questo tipo, il secondo documento viene caricato come un documento separato. Se stai utilizzando l'API e conosci l'ID del documento che vuoi sostituire, puoi farlo; vedi [Aggiornare un documento](http://www.ibm.com/watson/developercloud/discovery/api/v1/#update-doc) nella Guida di riferimento per le API. Se stai utilizzando il Data Crawler, il caricamento di un documento aggiornato dallo stesso URL di un documento precedente sostituisce il documento originale.
-   Se stai utilizzando la strumentazione per modificare gli arricchimenti nella tua configurazione, puoi modificare solo gli arricchimenti utilizzati per l'estrazione. Se vuoi aggiungere o modificare altri arricchimenti (ad esempio gli arricchimenti personalizzati da un modello {{site.data.keyword.knowledgestudiofull}}), devi utilizzare l'API. Per informazioni, vedi il metodo [Aggiornare una configurazione](http://www.ibm.com/watson/developercloud/discovery/api/v1/#replace_configuration)) nella Guida di riferimento per le API.
-   Le seguenti note si applicano in modo specifico al Data Crawler. 
    -   Il Data Crawler ritenta i caricamenti se riscontra un errore di caricamento.
    -   Il Data Crawler non è in grado di ritentare i documenti che sono stati caricati correttamente ma la cui conversione o indicizzazione non è riuscita.
    -   Il Data Crawler non ha una funzione per controllare lo stato downstream e prova a ricaricare gli URL non riusciti downstream.
    -   Non esiste un modo semplice per determinare quali documenti siano stati inseriti dal Data Crawler. Ad esempio, se lo esegui su un insieme di 500 documenti, il Data Crawler potrebbe segnalare degli errori di inoltro di 65 documenti con una raccolta totale di 212 documenti. Lo stato dei restanti 223 documenti non è determinato.

        È disponibile una soluzione temporanea ma è complicata e implica il richiamo diretto dell'API. Contatta il supporto {{site.data.keyword.IBM}} per assistenza.
-   Gli SDK Java, Python e Node.js per {{site.data.keyword.discoveryshort}} non forniscono tutta la funzionalità fornita dall'API REST (cURL) predefinita. Non tutti i metodi cURL hanno un metodo equivalente negli SDK non cURL e non tutti i metodi non cURL forniscono tutte le stesse funzioni che hanno i loro equivalenti cURL. In altre parole, gli SDK Java, Python e Node.js attualmente forniscono solo un sottoinsieme delle funzionalità dell'API cURL.
-   Se utilizzi il convertitore Word, una messa in corrispondenza sulle intestazioni utilizzando la chiave `style` risulta molto più accurata ed efficiente di quanto sia l'utilizzo della chiave `level`.
