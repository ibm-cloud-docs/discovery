---

copyright:
  years: 2019
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

# Alta disponibilità e ripristino di emergenza
{: #recovery}

{{site.data.keyword.discoveryfull}} supporta l'alta disponibilità senza un singolo punto di errore. È inoltre tua responsabilità eseguire il backup dei tuoi dati {{site.data.keyword.discoveryshort}} a supporto del tuo piano di ripristino di emergenza in modo da poter ricreare il tuo servizio.
{: shortdesc}

Il carico del traffico {{site.data.keyword.discoveryshort}} è bilanciato su più zone in una regione. Ciascuna zona è un data center nella stessa regione. Per ulteriori informazioni, vedi [Come garantisco nessun tempo di inattività?![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/docs/overview?topic=overview-zero-downtime#zero-downtime){: new_window}.

## Backup dei tuoi dati in Watson Discovery
{: #backup}

Ci sono diversi metodi per eseguire il backup dei dati archiviati in {{site.data.keyword.discoveryfull}}. Questi metodi devono essere inclusi nel tuo piano di ripristino di emergenza.

-  I dati di cui devi conservare una copia, come ad esempio i documenti di origine
-  I dati archiviati da {{site.data.keyword.discoveryshort}} e di cui dovresti eseguire l'estrazione e il backup
  
Ci saranno dei dati che dovrai ricreare da zero (ad esempio i dati di cui non puoi eseguire il backup, come gli eventi di feedback). 

### Documenti inseriti
{: #backupdocs}

I tuoi documenti caricati vengono convertiti e arricchiti e vengono quindi archiviati nell'indice di ricerca. L'indice di ricerca non è recuperabile in caso di emergenza e, pertanto, devi archiviare un backup di tutti i tuoi documenti di origine in un posto sicuro.

Se importi anche i documenti eseguendo delle ricerche per l'indicizzazione pianificate di origini dati esterne, devi conservare le tue credenziali dell'origine dati esternamente in modo da poter ristabilire le tue origini dati rapidamente. Vedi [Connessione alle origini dati](/docs/services/discovery?topic=discovery-sources#sources) per l'elenco di origini disponibili e per le credenziali necessarie per ciascuna di esse.

### Configurazioni
{: #backupconfigs}

Devi eseguire il backup delle tue configurazioni di istanza e archiviarle localmente in caso di emergenza. 

Per eseguire il backup di queste configurazioni, per prima cosa [elenca le tue configurazioni](https://cloud.ibm.com/apidocs/discovery#list-configurations) per ciascuna istanza. 

Dopo aver ottenuto l'elenco di configurazioni, [ottieni i dettagli](https://cloud.ibm.com/apidocs/discovery#get-configuration-details) per ciascuna configurazione.

### Dati di formazione
{: #backuptraining}

Devi eseguire il backup dei tuoi dati di formazione per ciascuna raccolta formata e archiviarli localmente in caso di emergenza. 

I dati di formazione sono utilizzati per formare in modo esplicito le tue raccolte e sono archiviati in base a ogni singola raccolta. 

Per estrarre i dati di formazione, utilizza l'API per scaricare le query e le valutazioni da {{site.data.keyword.discoveryshort}}. 

1.  [Elenca i dati di formazione](https://cloud.ibm.com/apidocs/discovery#list-training-data)
1.  [Elenca gli esempi](https://cloud.ibm.com/apidocs/discovery#list-examples-for-a-training-data-query) per ciascuna query.
1.  [Ottieni i dettagli](https://cloud.ibm.com/apidocs/discovery#get-details-for-training-data-example) per degli esempi di dati di formazione. 

Gli ID documento (`document ids`) che utilizzi nei tuoi dati di formazione puntano ai documenti nella tua raccolta corrente. DEVI utilizzare gli stessi ID documento (`document ids`) nelle tue nuove raccolte per assicurarti che si faccia riferimento agli ID corretti. In caso contrario, la formazione della pertinenza ripristinata NON FUNZIONERÀ.
{: important} 

### Query
{: #backupqueries}

Per impostazione predefinita (se non rifiuti esplicitamente), {{site.data.keyword.discoveryshort}} archivierà le query che invii a esso. 

Se desideri poterne eseguire il ripristino per [finalità statistiche](https://cloud.ibm.com/apidocs/discovery#number-of-queries-over-time), devi archiviare queste query separatamente. 

Puoi [estrarre le query](https://cloud.ibm.com/apidocs/discovery#search-the-query-and-event-log) da {{site.data.keyword.discoveryshort}}; tuttavia, viene archiviato un massimo di 10.000 query. Non c'è alcuna API di paginazione. Il ripristino delle query è sconsigliato; consigliamo di iniziare da zero.

### Feedback/clic
{: #clicks}

Se stai archiviando i clic sotto forma di eventi di feedback, non c'è attualmente un modo facile per eseguire il backup e il ripristino di queste informazioni. Consigliamo di iniziare da zero con l'API dei [dati di clic/feedback](https://cloud.ibm.com/apidocs/discovery#create-event). 

### Elenchi di espansione
{: #backupexpansions}

Se stai utilizzando le espansioni per la modifica delle query, devi eseguire il backup del tuo elenco di espansione e archiviarlo localmente. Per eseguire tale operazione, richiedi l'elenco di espansione utilizzando il comando API [get expansion list](https://cloud.ibm.com/apidocs/discovery#get-the-expansion-list) e archivialo localmente.

### Parole non significative o dizionari di tokenizzazione
{: #backupstopwords}

Se utilizzi queste funzionalità, dovrai eseguire un backup di questi file e archiviarli localmente. Nei caso delle parole non significative, esegui un backup del file di testo e, nel caso delle tokenizzazioni, devi eseguire il backup del file JSON. Vedi [Creazione di dizionari di tokenizzazione personalizzati](/docs/services/discovery?topic=discovery-query-concepts#tokenization) e [Definizione delle parole non significative](/docs/services/discovery?topic=discovery-query-concepts#stopwords) per ulteriori informazioni su ciascun tipo di file.

### Informazioni sulla raccolta
{: #collectioninfo}

Pur non essendo obbligatorio, è buona prassi [richiamare lo stato](https://cloud.ibm.com/apidocs/discovery#get-collection-details) per ciascuna raccolta su base regolare e archiviare le informazioni localmente. Conservando queste statistiche, puoi successivamente verificare che i tuoi processi di ripristino siano stati eseguiti correttamente, se necessario.
{: tip} 


### Modelli di Smart Document Understanding
{: #backupsdu}

Se stai utilizzando SDU (Smart Document Understanding), avrai dei modelli associati alla tua configurazione. Per evitare una perdita di queste informazioni, devi [esportare i tuoi modelli](/docs/services/discovery?topic=discovery-sdu#import), eseguirne il backup e archiviarli localmente. I modelli SDU hanno l'estensione file `.sdumodel`.


## Ripristino dei tuoi dati in una nuova istanza di Watson Discovery
{: #restore}

Considera l'utilizzo dei tuoi backup per eseguire il ripristino a una nuova istanza {{site.data.keyword.discoveryshort}} in un data center differente (noto anche come regione/ubicazione), ad esempio Dallas, Houston, Washington DC, Londra). 
{: note}

Per iniziare il ripristino, comincia riesaminando il tuo elenco di raccolte e origini dati associate, nonché i tuoi backup di file.

-  Crea il tuo [ambiente](https://cloud.ibm.com/apidocs/discovery#create-an-environment) e le tue [raccolte](https://cloud.ibm.com/apidocs/discovery#create-a-collection) utilizzando le informazioni di configurazione salvate. Assicurati che la corretta configurazione sia definita in modo appropriato e che la lingua per la raccolta sia impostata in modo appropriato. In caso contrario, ci vorrà più tempo perché il tuo sistema possa essere ripristinato ed essere operativo.
-  Se avevi qualche configurazione personalizzata impostata in {{site.data.keyword.discoveryshort}}, dovrai [creare nuovamente tali configurazioni personalizzate](/docs/services/discovery?topic=discovery-configservice#when-you-need-a-custom-configuration). 
-  Aggiungi nuovamente i dizionari di tokenizzazione o le parole non significative nelle raccolte. Vedi [Creazione di dizionari di tokenizzazione personalizzati](/docs/services/discovery?topic=discovery-query-concepts#tokenization) e [Definizione delle parole non significative](/docs/services/discovery?topic=discovery-query-concepts#stopwords).  
-  Se avevi un'espansione di query personalizzata, dovrai anche [aggiungere le tue espansioni di query](https://cloud.ibm.com/apidocs/discovery#create-or-update-expansion-list) per ciascuna raccolta. 
-  Se stavi utilizzando qualsiasi modello di entità personalizzato da WKS (Watson Knowledge Studio) per l'arricchimento, dovrai [reimportare tale modello](/docs/services/discovery?topic=discovery-configservice#custom-entity-model) nella tua istanza {{site.data.keyword.discoveryshort}}. 

Dopo che avrai configurato le tue raccolte come prima, dovrai iniziare a inserire i tuoi documenti di origine. A seconda di come avevi inserito i tuoi documenti in precedenza, puoi eseguire tale operazione utilizzando:
-  L'API [](https://cloud.ibm.com/apidocs/discovery#add-a-document)
-  Un [connettore](/docs/services/discovery?topic=discovery-sources#sources) 
-  Il [Data Crawler](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)
-  o un altro metodo

### Ripristino dei dati di formazione
{: #restoretraining}

Dopo che le raccolte sono state ripristinate, puoi iniziare il processo di [ricreazione dei tuoi modelli di formazione della pertinenza](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api). 

Richiama i dati di formazione di cui hai eseguito il backup, quindi:

1. [Carica le tue query](https://cloud.ibm.com/apidocs/discovery#add-query-to-training-data)
1. [Carica i documenti di esempio](https://cloud.ibm.com/apidocs/discovery#add-example-to-training-data-query) per ciascuna query.
1.  Dopo che i dati di formazione sono stati caricati, consulta questo [post del blog](https://developer.ibm.com/dwblog/2017/get-relevancy-training/) per assicurarti che soddisfi i numeri di accuratezza precedenti.Tieni presente che i vecchi `ID documento` devono essere trasferiti ai nuovi dati di formazione o aggiornati per riflettere i nuovi ID documento nella tua nuova raccolta.


### Ripristino delle connessioni alle origini dati esterne
{: #restoreconnections}

Nel caso di una perdita di dati imprevista, potresti perdere le tue ricerche per l'indicizzazione pianificate di origini dati esterne. Per l'elenco di origini disponibili, vedi [Connessione alle origini dati](/docs/services/discovery?topic=discovery-sources#sources).

Per ripristinare i tuoi dati esterni, dovrai ristabilire le tue connessioni a tali origini dati e quindi eseguirne nuovamente la ricerca per l'indicizzazione.

Trova le credenziali delle origini dati che hai archiviato precedentemente e attieniti alle istruzioni [qui](/docs/services/discovery?topic=discovery-sources#sources). Ciò ti consentirà di ristabilire una connessione alle tue origini dati e di fare in modo che i dati siano importati in {{site.data.keyword.discoveryshort}}.


### Ripristino di modelli Smart Document Understanding
{: #restoresdu}

Per importare un modello SDU (Smart Document Understanding) precedentemente esportato, attieniti alle istruzioni [qui](/docs/services/discovery?topic=discovery-sdu#import). I modelli SDU hanno l'estensione file `.sdumodel`.

Quando importi un modello SDU esistente in una nuova raccolta, è buona prassi creare la nuova raccolta e aggiungere un singolo documento, quindi importare il modello e caricare il resto dei tuoi documenti.
