---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-15"

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

# Tipi di relazione

La seguente tabella elenca i possibili tipi di relazione restituiti dall'arricchimento [Relation Extraction](/docs/services/discovery/building.html#relation-extraction).
{: shortdesc}

| Relazione        | Descrizione                                                                                                                                                                                                        |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| affectedBy      | Esiste tra un'entità e un evento che ha una chiara direzionalità e influenza l'entità.                                                                                                                        |
| affiliatedWith  | Esiste tra due entità che hanno un'affiliazione o che sono connesse in modo analogo.                                                                                                                                   |
| ageOf           | Correla un'età a un'entità.                                                                                                                                                                                       |
| agentOf         | Esiste tra un'entità e un evento in cui, secondo il testo, l'entità ha il ruolo più attivo. Non dovrebbe essere richiesta alcuna conoscenza di background..                              |
| authorOf        | Esiste tra una persona e un'investigazione della titolarità (TitleWork) che ha creato.                                                                                             |
| awardedBy       | Esiste tra un premio o una laurea e la persona o l'organizzazione da cui è stato attribuito o è stata conferita.                                                                                                             |
| awardedTo       | Esiste tra un premio o una laurea e la persona o l'organizzazione a cui è stato attribuito o è stata conferita.                                                                                                             |
| basedIn         | Esiste tra un'organizzazione e il luogo in cui si trova principalmente, esclusivamente o intrinsecamente.                                                                                     |
| before          | Indica la relazione temporale di antecedenza (prima) tra due tempi o eventi. Contrassegnato solo quando il testo specifica chiaramente la relazione.                                                      |
| bornAt          | Esiste tra una persona o un animale e il posto dove sono nati.                                                                                                                                     |
| bornOn          | Esiste tra una persona o un animale e la data e l'ora in cui sono nati.                                                                                                                           |
| capitalOf       | Esiste tra una capitale e il suo paese, stato o provincia. Contrassegnato solo quando il testo indica esplicitamente la relazione, non sulla base della conoscenza del mondo.                                                              |
| citizenOf       | Esiste tra una persona e l'entità geopolitica di cui è cittadina.                                                                                                                             |
| clientOf        | Esiste tra due entità quando una è un cliente commerciale diretto dell'altra (ossia, paga per specifici servizi o prodotti).                                                                  |
| colleague       | Esiste tra due persone che fanno parte della stessa organizzazione.                                                                                                                           |
| competitor      | Esiste tra due entità geopolitiche od organizzazioni impegnate in una concorrenza economica.                                                                                                   |
| contactOf       | Correla le informazioni di contatto a un'entità.                                                                                                                                            |
| diedAt          | Esiste tra una persona o un animale e il posto del loro decesso.                                                                                                                               |
| diedOf          | Esiste tra una persona o un animale e la causa del loro decesso.                                                                                                                               |
| diedOn          | Esiste tra una persona o un animale e la data e ora del loro decesso.                                                                                                                              |
| dissolvedOn     | Esiste tra un'entità quale un'organizzazione e la data od ora in cui è stata dissolta.                                                                                                        |
| educatedAt      | Esiste tra una persona e l'organizzazione presso la quale ha studiato.                                                                                                                        |
| employedBy      | Esiste tra due entità quando una paga l'altra per un lavoro o dei servizi specifici: deve essere coinvolto un compenso monetario. In molte circostanze, contrassegnare questa relazione richiede la conoscenza del mondo.                         |
| foundedOn       | Esiste tra un'entità quale un'organizzazione e la data od ora della sua istituzione.                                                                                                          |
| founderOf       | Esiste tra una persona o entità geopolitica e un'entità quale un'organizzazione che viene istituita.                                                                                                     |
| hasDisease      | Indica che una persona o un animale hanno o avevano una malattia.                                                                                                                                  |
| hasMoney        | Indica che un'entità quale una persona ha o aveva soldi.                                                                                                                                      |
| instrumentOf    | Esiste tra un'entità quale un'arma e un evento che l'uso di tale entità fa o ha fatto accadere.                                                                                                           |
| locatedAt       | Esiste tra un'entità e la sua ubicazione fisica.                                                                                                                                              |
| managerOf       | Esiste tra una persona e un'altra entità quale una persona o un'organizzazione che, come suo lavoro, gestisce.                                                                                |
| measureOf       | Indica una specifica misura, quale l'altezza o il peso, di un'entità.                                                                                                                         |
| memberOf        | Esiste tra un'entità quale una persona, un'organizzazione o un'entità geopolitica e un'altra entità a cui appartiene.                                                                                    |
| near            | Esiste tra due entità fisicamente vicine.                                                                                                                                       |
| overlaps        | Indica che due tempi o eventi si sovrappongono temporalmente. Contrassegnato solo quando il testo specifica chiaramente la relazione.                                                                                                   |
| ownerOf         | Esiste tra un'entità quale una persona, un'organizzazione o un'entità geopolitica e un'entità di sua proprietà, in modo permanente o temporaneo.                                                         |
| parentOf        | Esiste tra una persona o un animale e suo figlio o figliastro.                                                                                                                                         |
| participantIn   | Esiste tra un partecipante quale una persona, un animale, un'organizzazione o un'entità geopolitica e un evento cui sta partecipando o ha partecipato.                                                   |
| partner         | Esiste tra due entità geopolitiche od organizzazioni impegnate in una cooperazione economica.                                                                                                  |
| partOf          | Esiste tra un'entità più piccola e una più grande dello stesso tipo o di tipi correlati in cui la seconda entità incorpora la prima. Se le entità sono degli eventi, il primo si deve verificare entro il lasso di tempo del secondo. |
| partOfMany      | Esiste tra entità più piccole e più grandi dello stesso tipo o di tipi correlati in cui la seconda entità, che deve essere plurale, include la prima, che può essere singolare o plurale.                      |
| playsRoleOf     | Esiste tra una persona e uno specifico personaggio che recita o ha recitato in una performance.                                                                                               |
| populationOf    | Esiste tra un numero cardinale e un'entità quale un'organizzazione o un paese per cui il numero rappresenta l'intera popolazione.                                                             |
| productOf       | Esiste tra un prodotto o un'investigazione della titolarità (TitleWork) e l'organizzazione che l'ha prodotto/a.                                                                               |
| quantityOf      | Indica un numero cardinale che è la quantità o l'importo della seconda entità.                                                                                                                |
| rateOf          | Esiste tra un tasso e l'evento di cui specifica la frequenza di ricorrenza.                                                                                                                   |
| relative        | Esiste tra una persona o un animale e un'altra persona o un altro animale di cui è parente quando una relazione più specifica è inappropriata.                                                |
| residesIn       | Esiste tra un'entità vivente e l'ubicazione dove risiede in modo permanente.                                                                                                                  |
| shareholdersOf  | Esiste tra una persona, organizzazione o entità geopolitica e un'organizzazione di cui la prima entità è azionista.                                                                                      |
| siblingOf       | Esiste tra una persona o un animale e un suo fratello o fratellastro.                                                                                                                         |
| spokespersonFor | Esiste tra una persona e un'entità che rappresenta. Contrassegnato solo quando il testo indica esplicitamente la relazione, non sulla base della conoscenza del mondo.                                                           |
| spouseOf        | Esiste tra due persone ufficialmente coniugate.                                                                                                                                    |
| subsidiaryOf    | Esiste tra due organizzazioni quando la prima è una filiale della seconda, a indicare che la prima entità ha una discreta misura di autonomia pur essendo sotto il controllo della seconda.                               |
| timeOf          | Indica la data, l'ora o la durata in cui o per cui si è verificato l'evento; un'investigazione di titolarità (TitleWork) è stata pubblicata, eseguita o trasmessa oppure una legge è stata abbozzata, creata, passata o abolita.    

## Tipi di entità specifici per Relation Extraction
{: #specific-entity-types}

Le seguenti entità possono essere identificate dall'arricchimento Relation Extraction:

|Tipo di entità|
|---|
|Age|
|Anatomy|
|Animal|
|Award|
|Cardinal|
|Crime|
|Date|
|Degree|
|Duration|
|EmailAddress|
|Event|
|EventBusiness|
|EventCommunication|
|EventCustody|
|EventDemonstration|
|EventEducation|
|EventElection|
|EventGathering|
|EventLegal|
|EventLegislation|
|EventMeeting|
|EventPerformance|
|EventPersonnel|
|EventViolence|
|Facility|
|Food|
|GeographicFeature|
|GeopoliticalEntity|
|HealthCondition|
|Law|
|Location|
|Money|
|Measure|
|NaturalEvent|
|Organization|
|Ordinal|
|Percent|
|Person|
|Phone|
|Plant|
|Product|
|SportingEvent|
|Substance|
|Ticker|
|Time|
|TitleWork|
|Vehicle|
|Weapon|
|Weather|
|Web|
