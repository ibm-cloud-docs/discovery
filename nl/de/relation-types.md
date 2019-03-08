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

# Beziehungstypen
{: #relation-types}

In der folgenden Tabelle sind die möglichen Beziehungstypen aufgelistet, die durch die Aufbereitung für die [Beziehungsextraktion](/docs/services/discovery/building.html#relation-extraction) zurückgegeben werden.
{: shortdesc}

| Beziehung        | Beschreibung                                                                                                                                                                                                        |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| affectedBy      | Besteht zwischen einer Entität und einem Ereignis, das eine klare Ausrichtung besitzt und sich auf die Entität auswirkt.                                                                                                                        |
| affiliatedWith  | Besteht zwischen zwei Entitäten, die zusammengehören oder ähnlich miteinander verbunden sind.                                                                                                                                   |
| ageOf           | Bezieht ein Alter auf eine Entität.                                                                                                                                                                                       |
| agentOf         | Besteht zwischen einer Entität und einem Ereignis, in dem die Entität gemäß dem Text die aktivste Rolle einnimmt. Ein Hintergrundwissen sollte nicht erforderlich sein.                                                            |
| authorOf        | Besteht zwischen einer Person und einer von ihr erstellten Entität des Typs 'TitleWork'.                                                                                                                                                    |
| awardedBy       | Besteht zwischen einer Entität des Typs 'Award' oder 'Degree' und der Person bzw. Organisation, die die Entität zugesprochen hat.                                                                                                             |
| awardedTo       | Besteht zwischen einer Entität des Typs 'Award' oder 'Degree' und der Person bzw. Organisation, der die Entität zugesprochen wurde.                                                                                                             |
| basedIn         | Besteht zwischen einer Organisation und dem Standort, an dem sie sich hauptsächlich, ausschließlich oder im Wesentlichen befindet.                                                                                                                   |
| before          | Gibt die zeitliche Beziehung 'vor' zwischen zwei Zeitpunkten oder Ereignissen an. Ist nur markiert, wenn der Text die Beziehung klar angibt.                                                                                      |
| bornAt          | Besteht zwischen einer Person oder einem Tier und dem Ort, an dem er/sie/es geboren wurde.                                                                                                                                     |
| bornOn          | Besteht zwischen einer Person oder einem Tier und dem Datum oder der Uhrzeit, an dem bzw. zu der er/sie/es geboren wurde.                                                                                                                           |
| capitalOf       | Besteht zwischen einer Hauptstadt und ihrem Land, Staat oder Bundesland. Ist nur markiert, wenn der Text die Beziehung explizit angibt, basiert nicht auf Weltwissen.                                                              |
| citizenOf       | Besteht zwischen einer Person und der Entität des Typs 'GeopoliticalEntity', deren Bürger/in er/sie ist.                                                                                                                                |
| clientOf        | Besteht zwischen zwei Entitäten, wenn eine ein direkter Geschäftskunde der anderen ist (also für bestimmte Services oder Produkte bezahlt).                                                                                    |
| colleague       | Besteht zwischen zwei Personen, die zu derselben Organisation gehören.                                                                                                                                                   |
| competitor      | Besteht zwischen zwei Entitäten des Typs 'GeopoliticalEntity' oder 'Organization', die in wirtschaflichem Wettbewerb stehen.                                                                                                                  |
| contactOf       | Bezieht Kontaktinformationen auf eine Entität.                                                                                                                                                                        |
| diedAt          | Besteht zwischen einer Person oder einem Tier und dem Ort, an dem er/sie/es gestorben ist.                                                                                                                                      |
| diedOf          | Besteht zwischen einer Person oder einem Tier und seiner/ihrer Todesursache.                                                                                                                                         |
| diedOn          | Besteht zwischen einer Person oder einem Tier und dem Datum oder der Uhrzeit, an dem bzw. zu der er/sie/es gestorben ist.                                                                                                                               |
| dissolvedOn     | Besteht zwischen einer Entität wie einer Organisation und dem Datum oder der Uhrzeit, an dem bzw. zu der sie aufgelöst wurde.                                                                                                                   |
| educatedAt      | Besteht zwischen einer Person und der Organisation, bei der er/sie ausgebildet wurde.                                                                                                                                |
| employedBy      | Besteht zwischen zwei Entitäten, bei denen eine Entität die andere Entität für bestimmte Arbeiten oder Dienstleistungen bezahlt, eine finanzielle Entgeltung muss einbezogen sein. Die Markierung dieser Beziehung erfordert in vielen Situationen Weltwissen.                         |
| foundedOn       | Besteht zwischen einer Entität wie einer Organisation und dem Datum oder der Uhrzeit, an dem bzw. zu der sie gegründet wurde.                                                                                                                     |
| founderOf       | Besteht zwischen einer Person oder einer Entität des Typs 'GeopoliticalEntity' und einer Entität wie einer Organisation, die von ihr gegründet wurde.                                                                                                                          |
| hasDisease      | Gibt an, dass eine Person oder ein Tier eine Krankheit aufweist oder aufwies.                                                                                                                                                            |
| hasMoney        | Gibt an, dass eine Entität wie eine Person Geld besitzt oder besaß.                                                                                                                                                        |
| instrumentOf    | Besteht zwischen einer Entität wie einer Waffe und einem Ereignis, bei dem die Verwendung der Entität verursacht wird bzw. wurde.                                                                                                              |
| locatedAt       | Besteht zwischen einer Entität und ihrem physischen Standort.                                                                                                                                                                |
| managerOf       | Besteht zwischen einer Person und einer anderen Entität wie einer Person oder Organisation, die deren Verwaltung sein/ihr Job ist.                                                                                              |
| measureOf       | Gibt eine bestimmte Kennzahl wie die Höhe oder das Gewicht einer Entität an.                                                                                                                                          |
| memberOf        | Besteht zwischen einer Entität wie einer Person, Organisation oder geopolitischen Entität und einer anderen Entität, zu der er/sie gehört.                                                                                            |
| near            | Besteht zwischen zwei Entitäten, die sich physisch nah beieinander befinden.                                                                                                                                       |
| overlaps        | Gibt an, dass sich zwei Zeiten oder Ereignisse zeitlich überschneiden. Ist nur markiert, wenn der Text die Beziehung klar angibt.                                                                                                   |
| ownerOf         | Besteht zwischen einer Entität wie einer Person, Organisation oder geopolitischen Entität und einer anderen Entität, die er/sie/es dauerhaft oder vorübergehend besitzt.                                                                     |
| parentOf        | Besteht zwischen einer Person oder einem Tier und seinem/ihrem Kind bzw. Stiefkind.                                                                                                                                         |
| participantIn   | Besteht zwischen einem Teilnehmer wie einer Person, einem Tier, einer Organisation oder einer geopolitischen Entität und einem Ereignis, an dem er/sie/es beteiligt ist oder war.                                                         |
| partner         | Besteht zwischen zwei geopolitischen Entitäten oder Organisationen, die wirtschaftlich zusammenarbeiten.                                                                                                                  |
| partOf          | Besteht zwischen einer kleineren und einer größeren Entität desselben oder verwandten Typs, wobei die zweite Entität die erste subsummiert. Falls es sich bei den Entitäten um Ereignisse handelt, muss das erste innerhalb des Zeitraums des zweiten stattfinden. |
| partOfMany      | Besteht zwischen kleineren und größeren Entitäten desselben oder verwandten Typs, wobei die zweite Entität, die einen Plural darstellen muss, die erste Entität subsummiert, die aus einer oder mehreren Entitäten bestehen kann.                      |
| playsRoleOf     | Besteht zwischen einer Person und einem bestimmten Charakter, den er/sie in einer Aufführung darstellt.                                                                                                                  |
| populationOf    | Besteht zwischen einer Kardinalzahl und einer Entität wie einer Organisation oder einen Land, für die/das die Zahl die gesamte Bevölkerung darstellt.                                                                                  |
| productOf       | Besteht zwischen einem Produkt oder einer Entität des Typs 'TitleWork' und der Organisation, es/sie produziert hat.                                                                                                                                       |
| quantityOf      | Gibt eine Kardinalzahl an, die die Menge oder den Umfang einer zweiten Entität angibt.                                                                                                                                            |
| rateOf          | Besteht zwischen einer Rate und einem Ereignis, dessen Häufigkeit sie angibt.                                                                                                                                     |
| relative        | Besteht zwischen einer Person oder einem Tier und einer anderen Person bzw. einem anderen Tier, mit dem er/sie/es verwandt ist, wenn eine speziellere Beziehung ungeeignet ist.                                                               |
| residesIn       | Besteht zwischen einem Lebewesen und der Position an dem er/sie/es ständig lebt.                                                                                                                       |
| shareholdersOf  | Besteht zwischen einer Person, Organisation oder geopolitischen Entität und einer Organisation, an der die erste Entität beteiligt ist.                                                                                                  |
| siblingOf       | Besteht zwischen einer Person oder einem Tier und ihren/seinen Geschwistern oder Stiefgeschwistern.                                                                                                                                     |
| spokespersonFor | Besteht zwischen einer Person und einer Entität, die er/sie repräsentiert. Ist nur markiert, wenn der Text die Beziehung explizit angibt, basiert nicht auf Weltwissen.                                                           |
| spouseOf        | Besteht zwischen zwei Personen, die rechtmäßige Eheleute sind.                                                                                                                                                      |
| subsidiaryOf    | Besteht zwischen zwei Organisationen, wenn die erste der zweiten untergeordnet ist, wobei die erste Entität trotz Kontrolle durch die zweite Entität ein gewisses Maß an Autonomie besitzt.                               |
| timeOf          | Gibt das Datum, die Uhrzeit oder die Dauer für ein Ereignis an (eine Entität des Typs 'TitleWork' wurde veröffentlicht, aufgeführt oder gesendet oder ein Gesetz wurde entworfen, erstellt, verabschiedet oder aufgehoben).    

## Spezielle Entitätstypen für die Beziehungsextraktion
{: #specific-entity-types}

Die folgenden Entitäten können durch die Aufbereitung für die Beziehungsextraktion erkannt werden:

|Entitätstyp|
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
