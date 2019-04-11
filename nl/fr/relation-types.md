---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-15"

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

# Types de relation
{: #relation-types}

Le tableau ci-après recense les types de relation possibles qui sont renvoyés par l'enrichissement [Relation Extraction](/docs/services/discovery?topic=discovery-configservice#relation-extraction).
{: shortdesc}

| Relation        | Description                                                                                                                                                                                                        |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| affectedBy      | Existe entre une entité et un événement qui a une orientation claire et qui affecte l'entité.                                                                                                                        |
| affiliatedWith  | Existe entre deux entités qui ont une affiliation ou qui sont connectées de façon similaire.                                                                                                                                   |
| ageOf           | Relie un âge à une entité.                                                                                                                                                                                       |
| agentOf         | Existe entre une entité et un événement dans lequel l'entité joue le rôle le plus actif en fonction du texte. Aucune connaissance de base ne devrait être requise.                                                            |
| authorOf        | Existe entre une personne et une entité TitleWork qu'elle a créée.                                                                                                                                                    |
| awardedBy       | Existe entre une récompense ou un diplôme et la personne ou l'organisation ayant remis cette récompense ou ce diplôme.                                                                                                             |
| awardedTo       | Existe entre une récompense ou un diplôme et la personne ou l'organisation à laquelle cette récompense ou ce diplôme a été remis.                                                                                                             |
| basedIn         | Existe entre une organisation et l'emplacement où elle se trouve principalement, uniquement, ou intrinsèquement.                                                                                                                   |
| before          | Signifie la relation temporelle "before" entre deux périodes ou événements. Marquée uniquement lorsque le texte spécifie clairement la relation.                                                                                      |
| bornAt          | Existe entre une personne ou un animal et le lieu de naissance de cette personne ou de cet animal.                                                                                                                                     |
| bornOn          | Existe entre un individu ou un animal et la date ou l'heure de sa naissance.                                                                                                                           |
| capitalOf       | Existe entre une capitale et son pays ou état ou province. Marquée uniquement lorsque le texte indique explicitement la relation ; ne requiert aucune connaissance du monde.                                                              |
| citizenOf       | Existe entre une personne et l'entité géopolitique dont cette personne est citoyenne.                                                                                                                                |
| clientOf        | Existe entre deux entités lorsque l'une est un client direct de l'autre (autrement dit, elle paie pour certains services ou produits).                                                                                    |
| colleague       | Existe entre deux personnes qui font partie de la même organisation.                                                                                                                                                   |
| competitor      | Existe entre deux entités géopolitiques ou organisations engagées dans une concurrence économique.                                                                                                                  |
| contactOf       | Relie des informations de contact à une entité.                                                                                                                                                                        |
| diedAt          | Existe entre un individu ou un animal et le lieu de son décès.                                                                                                                                      |
| diedOf          | Existe entre un individu ou un animal et la cause de son décès.                                                                                                                                         |
| diedOn          | Existe entre un individu ou un animal et la date ou l'heure de son décès.                                                                                                                               |
| dissolvedOn     | Existe entre une entité, par exemple une organisation, et la date ou l'heure à laquelle elle a été dissoute.                                                                                                                   |
| educatedAt      | Existe entre une personne et l'organisation où cette personne fait ou a fait ses études.                                                                                                                                |
| employedBy      | Existe entre deux entités lorsque l'une d'entre d'elles paie pour certains travaux ou services ; une récompense financière doit être impliquée. Dans de nombreuses circonstances, le marquage de cette relation requiert une certaine connaissance du monde.                         |
| foundedOn       | Existe entre une entité, par exemple, une organisation, et la date ou l'heure à laquelle elle a été fondée.                                                                                                                     |
| founderOf       | Existe entre une personne ou une entité géopolitique et une entité, par exemple, une organisation, qu'elle a fondée.                                                                                                                          |
| hasDisease      | Indique qu'un individu ou un animal est ou était atteint d'une maladie.                                                                                                                                                            |
| hasMoney        | Indique qu'une entité, par exemple, une personne, est ou était riche.                                                                                                                                                        |
| instrumentOf    | Existe entre une entité, par exemple, une arme, et un événement que l'entité a ou avait pour habitude de déclencher.                                                                                                              |
| locatedAt       | Existe entre une entité et son emplacement physique.                                                                                                                                                                |
| managerOf       | Existe entre une personne et une autre entité, par exemple, une personne ou une organisation, que cette personne gère dans le cadre de son travail.                                                                                              |
| measureOf       | Indique une mesure particulière, par exemple, la hauteur ou le poids d'une entité.                                                                                                                                          |
| memberOf        | Existe entre une entité, par exemple, une personne, une organisation ou une entité géopolitique, et une autre entité à laquelle elle appartient.                                                                                            |
| near            | Existe entre deux entités proches l'une de l'autre physiquement.                                                                                                                                       |
| overlaps        | Indique que deux périodes ou événements se chevauchent dans le temps. Marquée uniquement lorsque le texte spécifie clairement la relation.                                                                                                   |
| ownerOf         | Existe entre une entité, par exemple, une personne, une organisation ou une entité géopolitique, et une entité qu'elle possède, que ce soit de manière permanente ou temporaire.                                                                     |
| parentOf        | Existe entre une personne et son enfant ou son beau-fils ou sa belle-fille ou entre un animal et son petit ou le petit de son partenaire.                                                                                                                                         |
| participantIn   | Existe entre un participant, par exemple, un individu, un animal, une organisation ou une entité géopolitique, et un événement auquel il participe ou a participé.                                                         |
| partner         | Existe entre deux entités géopolitiques ou organisations engagées dans une coopération économique.                                                                                                                  |
| partOf          | Existe entre une entité plus petite et une entité plus grande de même type ou de types connexes, la seconde englobant la première. Si les deux entités sont des événements, la première doit se produire dans l'intervalle de temps de la seconde. |
| partOfMany      | Existe entre des entités plus petites et plus grandes de même type ou de types connexes, la seconde (qui doit être multiple) englobant la première (qui peut être constituée d'une ou de plusieurs entités).                      |
| playsRoleOf     | Existe entre une personne et un rôle spécifique qu'elle joue ou qu'elle a joué dans un spectacle.                                                                                                                  |
| populationOf    | Existe entre un nombre cardinal et une entité, par exemple, une organisation ou un pays, dont le nombre représente l'ensemble de la population.                                                                                  |
| productOf       | Existe entre un produit ou une entité TitleWork et l'organisation qui l'a généré.                                                                                                                                       |
| quantityOf      | Indique un nombre cardinal qui représente la quantité ou le montant d'une seconde entité.                                                                                                                                            |
| rateOf          | Existe entre un taux et un événement dont il spécifie la fréquence d'occurrence.                                                                                                                                     |
| relative        | Existe entre un individu ou un animal et un autre individu ou un autre animal avec lequel il a un lien de parenté lorsqu'une relation plus spécifique est inappropriée.                                                               |
| residesIn       | Existe entre une entité vivante et l'emplacement où elle réside en permanence.                                                                                                                       |
| shareholdersOf  | Existe entre une personne et une organisation ou une entité géopolitique et une organisation dont la première entité est un actionnaire.                                                                                                  |
| siblingOf       | Existe entre un individu ou un animal et son frère ou sa soeur ou son demi-frère ou sa demi-soeur.                                                                                                                                     |
| spokespersonFor | Existe entre une personne et une entité qu'elle représente. Marquée uniquement lorsque le texte indique explicitement la relation ; ne requiert aucune connaissance du monde.                                                           |
| spouseOf        | Existe entre deux personnes qui sont des époux formels.                                                                                                                                                      |
| subsidiaryOf    | Existe entre deux organisations lorsque la première est une filiale de la seconde, la première entité étant relativement autonome bien que sous le contrôle de la seconde.                               |
| timeOf          | Indique la date, l'heure ou la durée d'un événement ; une entité TitleWork a été publiée, effectuée ou diffusée ou une loi a d'abord été élaborée, créée, votée ou abrogée.    

## Types d'entité propres à Relation Extraction
{: #specific-entity-types}

Les entités suivantes peuvent être identifiées par l'enrichissement Relation Extraction :

|Type d'entité|
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
