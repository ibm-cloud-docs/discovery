---

copyright:
  years: 2017, 2018, 2019
lastupdated: "2019-01-15"

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

# Analisi dei contratti
{: #contract_parsing}

Element Classification restituisce i contratti analizzati con un'analisi di ciascun elemento identificato.

Le seguenti sezioni descrivono in che modo il JSON restituito restituisce l'analisi.

## Tipi
{: #contract_types}

L'array `types` include diversi oggetti, ciascuno dei quali contiene delle chiavi `nature` e `party` i cui valori identificano un couplet per l'elemento.

Le seguenti tabelle elencano i possibili valori delle chiavi `nature` e `party`.

| `nature`         |Descrizione                                                |
|:----------------:|-----------------------------------------------------------|
|`Definition`      |Questo elemento aggiunge chiarezza a un termine, una relazione o elementi simili. Non è richiesta alcuna azione per soddisfare l'elemento, né alcuna parte è interessata.|
|`Disclaimer`      |La parte (`party`) nell'elemento non è obbligata a soddisfare i termini specificati dall'elemento ma non le è vietato farlo.|
|`Exclusion`       |La parte (`party`) nell'elemento non soddisferà i termini specificati dall'elemento.|
|`Obligation`      |Alla parte (`party`) nell'elemento è richiesto di soddisfare i termini specificati dall'elemento.|
|`Right`           |Alla parte (`party`) nell'elemento è garantita la ricezione dei termini specificati dall'elemento.|

Ogni chiave `nature` è accoppiata a una chiave `party`, che conterrà il nome o il ruolo della parte o delle parti che si applicano alla natura (degli esempi includono, tra gli altri, `Buyer`, `IBM` o `All Parties`). Nota che, per la natura `Definition`, la parte è sempre `None`.

## Parti
{: #contract_parties}

L'array `parties` specifica i partecipanti elencati nel contratto. Ogni oggetto `party` è associato ad altri oggetti che forniscono dettagli sulla parte, compresi:

  - `role`: il ruolo della parte. I valori sono elencati nella tabella che segue questo elenco.
  - `importance`: l'importanza della parte. I valori possibili sono `Primary` per una parte primaria e `Unknown` per una parte non primaria.
  - `addresses`: un array che identifica gli indirizzi.
    - `text`: un indirizzo.
    - `location`: l'ubicazione dell'indirizzo come definita dai relativi indici `begin` ed `end`.
  - `contacts`: un array che definisce i nomi e i ruoli dei contratti identificati nel documento di input.
    - `name`: il nome di un contatto.
    - `role`: il ruolo del contatto.

I valori di `role` che possono essere restituiti per i contratti includono, tra gli altri:

| `role`           |Descrizione                                                |
|:----------------:|-----------------------------------------------------------|
|`Buyer`           |La parte responsabile del pagamento delle merci o dei servizi elencati nel contratto.|
|`End User`        |La parte che interagisce con le merci o i servizi forniti, distinta in modo esplicito dal `Buyer`.|
|`None`            |Non è stata identificata alcuna parte per l'elemento.|
|`Supplier`        |La parte responsabile della fornitura delle merci o dei servizi elencati nel contratto.|

## Categorie
{: #contract_categories}

L'array `categories` definisce l'argomento della frase. 

Le categorie e le descrizioni in questa tabella sono basate sulla legislazione degli Stati Uniti e potrebbero non essere valide in giurisdizioni fuori dagli Stati Uniti.
{: important}

Le categorie attualmente supportate includono:

| `categories`     |Descrizione                                                |
|:----------------:|-----------------------------------------------------------|
|`Amendments`      |Elementi che specificano le modifiche al contratto dopo che è stato firmato oppure alterazioni a un contratto standard. Include le discussioni delle condizioni per modificare i termini di un contratto.|
|`Asset Use`       |Elementi che fanno riferimento al modo in cui una parte può o meno utilizzare gli asset di un'altra parte. Ciò si applica specificamente a una parte che ha accesso a, o che utilizza, asset quali le licenze, l'attrezzatura, gli strumenti o il personale dell'altra parte nell'adempimento delle sue mansioni sulla base dell'accordo, incluse le autorizzazioni e le limitazioni che ne derivano.  Ciò non si estende alle specifiche degli obblighi o dei diritti di una parte per quanto riguarda eventuali licenze, merci, servizi acquistati ecc. poiché questi sono asset che appartengono alla parte, piuttosto che asset di un'altra parte.|
|`Assignments`     |Elementi che descrivono il trasferimento di diritti, obblighi o entrambi a una terza parte.|
|`Audits`          |Elementi che fanno riferimento al diritto di una parte di esaminare o riesaminare la conformità o i requisiti che una parte sia disponibile per l'ispezione o la revisione della conformità. Ciò include i riferimenti alla conservazione della documentazione (in principal modo in quanto correlata al diritto all'ispezione) e la gestione e la conservazione di registrazioni delle attività che possono essere esaminate.|
|`Business Continuity`|Elementi che fanno riferimento alle conseguenze se l'intera attività commerciale di una delle parti viene venduta.|
|`Communication`  |Elementi che fanno riferimento ai requisiti per la comunicazione, risposta, notifica o fornitura di avvisi, informazioni di contratto o informazioni relative alle modifiche al contratto. Include anche i riferimenti ai dettagli relativi ai metodi di comunicazione, all'atto o alla procedura di scambio di informazioni e ai mezzi accettabili di scambio di informazioni tra le parti (nonché altri che non sono necessariamente parti dirette per il contratto).|
|`Confidentiality` |Elementi che descrivono in che modo le parti possono o non possono utilizzare le informazioni acquisite nel corso del completamento del contratto e successivamente. Include anche una discussione delle informazioni che devono essere mantenute riservate, come la conservazione di segreti commerciali o la non diffusione di informazioni aziendali.|
|`Deliverables`    |Elementi che specificano gli articoli, quali merci o servizi, che una parte fornisce a un'altra in base ai termini del contratto, di norma in cambio di un pagamento. Include una discussione sulla preparazione dei deliverable.|
|`Delivery`        |Elementi che specificano i mezzi o i modi di trasferimento di deliverable (cose, piuttosto che servizi personali) da una parte a un'altra. Include le discussioni delle caratteristiche di recapito, quali la pianificazione o la località.|
|`Dispute Resolution`|Elementi che discutono le disposizioni per risolvere qualsiasi controversia (ad esempio per quanto riguarda il lavoro, le fatture o la fatturazione) che dovesse insorgere tra le parti contraenti.  Degli esempi di disposizioni includono la composizione delle controversie in base a una procedura definita, quale un collegio arbitrarle, un procedimento per ottenere un'ingiunzione, la rinuncia a un diritto al processo oppure il divieto di perseguimento di una class action. Include anche i riferimenti alla legislazione vigente o alla scelta di quella da adottare del contratto, come ad esempio uno specifico paese o una specifica giurisdizione. |
|`Force Majeure`   |Elementi che fanno riferimento ad eventi inaspettati o distruttivi fuori dal controllo di una parte che solleverebbero la parte dall'adempimento del suo obbligo contrattuale.|
|`Indemnification` |Elementi che specificano la compensazione di determinate perdite, quando una parte del contratto diventa responsabile della compensazione di un'altra parte in seguito alla perdita o ai danni sostenuti nel corso della durata contrattuale o derivanti dalle circostanze del contratto. Include anche riferimenti ad eventuali esenzioni legali da perdita o danni.|
|`Insurance`       |Elementi che fanno riferimento alla copertura assicurativa o ai termini di copertura forniti da una parte a un'altra parte (comprese terze parti quali subappaltatori o altri). Include una varietà di assicurazioni, tra cui, tra le altre, l'assicurazione medica.|
|`Intellectual Property`|Elementi che discutono l'assegnazione di diritti (quali diritti d'autore, brevetti e segreti commerciali) a parti del contratto. Include i riferimenti a brevetti, diritti da applicare per brevetti, marchi, nomi commerciali, marchi di servizi, nomi dominio, diritti d'autore e tutte le presentazioni di richieste e la registrazione di tali schemi, modelli industriali, invenzioni, titolarità di autore, know-how, segreti commerciali, programmi software per computer e altre informazioni proprietarie intangibili. Include inoltre una discussione delle conseguenze della violazione dei diritti di proprietà intellettuale.|
|`Liability`       |Elementi che descrivono il metodo per determinare quando e come la responsabilità ricade su una parte. Degli esempi possono includere, tra gli altri, dichiarazioni relative a limitazioni di responsabilità, richieste di terze parti e riparazioni, sostituzioni o rimborsi come richiesto alla parte ritenuta responsabile.|
|`Payment Terms & Billing`|Elementi che indicano in dettaglio come e quando una parte deve pagare o essere pagata, nonché gli elementi o le tariffe che le parti pagheranno o si vedranno addebitare in fattura. Include riferimenti alle modalità di pagamento o ai meccanismi di pagamento.|
|`Pricing & Taxes` |Elementi che fanno riferimento a specifici importi o specifiche cifre associati a singoli deliverable scambiati (ad esempio, quanto costa qualcosa) come parte della soddisfazione dei termini del contratto. Include riferimenti a specifiche cifre o specifici metodi per calcolare i prezzi o gli importi delle imposte.|
|`Privacy`         |Elementi particolarmente interessati al trattamento delle informazioni personali sensibili, di norma relativi alla loro protezione (ad esempio per soddisfare regolamenti quali quello generale sulla protezione dei dati (GDPR, General Data Protection Regulation)).|
|`Responsibilities`|Elementi che discutono delle attività accessorie al contratto che sono sotto il controllo di solo una delle parti, specificamente concentrati sulla discussione della vigilanza dei dipendenti.|
|`Safety and Security`|Elementi che fanno riferimento alla sicurezza fisica o alla protezione della sicurezza cibernetica per persone, dati o sistemi. Degli esempi includono le discussioni dei controlli dei precedenti personali, le precauzioni di sicurezza, la sicurezza del posto di lavoro, i protocolli di accesso protetti e i difetti del prodotto che potrebbero rappresentare un pericolo.|
|`Scope of Work`   |Elementi che definiscono cosa è presente nel contratto rispetto a quanto invece non è incluso e, di conseguenza, quali sono gli impegni presi. Degli esempi includono dichiarazioni che definiscono uno specifico ordine o che descrivono gli obiettivi o gli scopi delineati nel contratto.|
|`Subcontracts`    |Elementi che fanno riferimento all'assunzione di terze parti per eseguire specifici compiti nel rispetto del contratto e le autorizzazioni, i diritti, le limitazioni e le conseguenze a esso attinenti e da esso derivanti.|
|`Term & Termination`|Elementi che fanno riferimento alla durata del contratto, alla pianificazione e ai termini della risoluzione del contratto e le eventuali conseguenze di tale risoluzione, compresi gli eventuali obblighi che si applicano al momento della risoluzione o successivamente ad essa.|
|`Warranties`      |Elementi che fanno riferimento alle promesse e agli obblighi in essere espressi nel contratto che sono attualmente veri e continueranno a esserlo in futuro. Anche elementi che trattano delle conseguenze derivanti dal mancato rispetto di tali promesse od obblighi e i diritti a porre rimedio alla situazione (ad esempio, tra gli altri, la richiesta di un risarcimento danni. Questa categoria non si applica agli elementi puramente interessati alle dichiarazioni di rappresentazione (dichiarazioni fattuali sul passato o il presente) o agli elementi basati su presupposti relativi a cose successe nel passato.|

## Attributes (Attributi)
{: #attributes}

L'array `attributes` specifica gli eventuali attributi identificati nella frase. Ciascun oggetto nell'array include tre chiavi: `type` (il tipo di attributo dalla seguente tabella), `text` (il testo applicabile) e `location` (gli indici `begin` e `end` dell'attributo nel documento di input). Gli attributi attualmente supportati includono:

| `attributes`     |Descrizione                                                |
|:----------------:|-----------------------------------------------------------|
|`Address`         |Un indirizzo postale.                                          |
|`Currency`        |Valore e unità monetarie.                                  |
|`DateTime`        |Una data, un'ora, un intervallo di date o un intervallo di tempo.                   |
|`Location`        |Una località o una regione geografica.                         |
|`Organization`    |Un'organizzazione.                                           |
|`Person`          |Una persona.                                                  |

## Date effettive
{: #effective_dates}

L'array `effective_dates` identifica le date durante le quali il documento sarà in vigore.

| `effective_dates`|Descrizione                                                |
|:----------------:|-----------------------------------------------------------|
|`text`            |Una data effettiva, elencata come una stringa.                     |
|`confidence_level`|Il livello di affidabilità dell'identificazione della data effettiva. I valori possibili includono `High`, `Medium` e `Low`.|
|`location`        |L'ubicazione della data come definita dai relativi indici `begin` ed `end`.|

## Importi del contratto
{: #contract_amounts}

L'array `contract_amounts` identifica gli importi monetari specificati nel documento.

| `contract_amounts`|Descrizione                                               |
|:----------------:|-----------------------------------------------------------|
|`text`            |Un importo del contratto, elencato come una stringa.                  |
|`confidence_level`|Il livello di affidabilità dell'identificazione dell'importo del contratto. I valori possibili includono `High`, `Medium` e `Low`.|
|`location`        |L'ubicazione dell'importazione del contratto come definita dai relativi indici `begin` ed `end`.|

## Date di terminazione
{: #termination_dates}

L'array `termination_dates` identifica le date di terminazione del documento.

| `contract_amounts`|Descrizione                                               |
|:----------------:|-----------------------------------------------------------|
|`text`            |La data di terminazione, elencata come una stringa.                  |
|`confidence_level`|Il livello di affidabilità dell'identificazione della data di terminazione. I valori possibili includono `High`, `Medium` e `Low`.|
|`location`        |L'ubicazione della data di terminazione come definita dai relativi indici `begin` ed `end`.|

## Provenance (Provenienza)
{: #provenance}

Ogni oggetto negli array `types` e `categories` include un array `provenance_ids`. L'array `provenance_ids` ha una o più chiavi. Ciascuna chiave è un valore con hash che puoi inviare a IBM per fornire un feedback o ricevere supporto.
