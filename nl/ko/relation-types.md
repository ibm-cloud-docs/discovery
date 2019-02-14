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

# 관계 유형

다음 표는 [관계 추출](/docs/services/discovery/building.html#relation-extraction) 인리치먼트로 리턴되는 가능한 관계 유형을 나열합니다.
{: shortdesc}

|관계        |설명                                                                                                                                                                                                        |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|affectedBy      |한 엔티티와 명확한 방향성이 있고 해당 엔티티에 영향을 주는 이벤트 사이에 존재합니다.                                                                                                                        |
|affiliatedWith  |유사성이 있거나 유사하게 연결되는 두 개의 엔티티 사이에 존재합니다.                                                                                                                                   |
|ageOf           |수명을 엔티티와 관련시킵니다.                                                                                                                                                                                       |
|agentOf         |한 엔티티와 해당 엔티티가 텍스트에 따라 가장 활성화된 역할을 수행하는 이벤트 사이에 존재합니다. 배경 지식이 필요하지 않습니다.                                                            |
|authorOf        |한 사람과 그 사람이 작성한 TitleWork 사이에 존재합니다.                                                                                                                                                    |
|awardedBy       |한 Award 또는 Degree와 이를 수여하거나 부여한 사람 또는 조직 사이에 존재합니다.                                                                                                             |
|awardedTo       |한 Award 또는 Degree와 이를 수여받거나 부여받은 사람 또는 조직 사이에 존재합니다.                                                                                                             |
|basedIn         |한 Organization과 주로, 유일하게 또는 본질적으로 배치된 위치 사이에 존재합니다.                                                                                                                   |
|before          |두 개의 Time 또는 Event 사이의 시간적 관계 "이전"을 나타냅니다. 텍스트가 명확하게 관계를 지정하는 경우에만 표시됩니다.                                                                                      |
|bornAt          |한 Person 또는 Animal과 해당 Person 또는 Animal이 태어난 위치 사이에 존재합니다.                                                                                                                                     |
|bornOn          |한 Person 또는 Animal과 해당 Person 또는 Animal이 태어난 Date 또는 Time 사이에 존재합니다.                                                                                                                           |
|capitalOf       |도시 및 국가, 시/도 사이에 존재합니다. 텍스트가 세계 정세의 지식을 따르지 않고 명시적으로 관계를 언급하는 경우에만 표시됩니다.                                                              |
|citizenOf       |한 사람과 그 사람이 국적을 가진 GeopoliticalEntity 사이에 존재합니다.                                                                                                                                |
|clientOf        |하나의 엔티티가 다른 엔티티의 직접적인 업무상 고객인 경우 두 개의 엔티티 사이에 존재합니다(즉, 특정 서비스 또는 제품에 대해 지불함).                                                                                    |
|colleague       |동일한 Organization의 구성원인 두 명의 People 사이에 존재합니다.                                                                                                                                                   |
|competitor      |경제적 경쟁 관계에 있는 두 Organization 또는 GeopoliticalEntity 사이에 존재합니다.                                                                                                                  |
|contactOf       |연락처 정보를 엔티티와 관련시킵니다.                                                                                                                                                                        |
|diedAt          |한 Person 또는 Animal과 해당 Person 또는 Animal이 사망한 위치 사이에 존재합니다.                                                                                                                                      |
|diedOf          |한 Person 또는 Animal과 해당 Person 또는 Animal의 사망 원인 사이에 존재합니다.                                                                                                                                         |
|diedOn          |한 Person 또는 Animal과 해당 Person 또는 Animal이 사망한 Date 사이에 존재합니다.                                                                                                                               |
|dissolvedOn     |한 엔티티(예: Organization)와 해당 엔티티가 사라지는 Date 또는 Time 사이에 존재합니다.                                                                                                                   |
|educatedAt      |한 Person과 해당 Person이 교육을 받은 Organization 사이에 존재합니다.                                                                                                                                |
|employedBy      |하나의 엔티티가 특정 작업 또는 서비스에 대해 다른 엔티티에게 지불하는 경우 두 엔티티 사이에 존재합니다. 금전적 보상이 포함되어야 합니다. 많은 환경에서 이 관계를 표시하는 데 세계 정세의 지식이 필요합니다.                         |
|foundedOn       |한 엔티티(예: Organization)와 해당 엔티티가 설립된 Date 또는 Time 사이에 존재합니다.                                                                                                                     |
|founderOf       |한 Person 또는 GeopoliticalEntity와 해당 Person 또는 GeopoliticalEntity가 설립한 엔티티(예: Organization) 사이에 존재합니다.                                                                                                                          |
|hasDisease      |한 Person 또는 Animal이 질병이 있거나 과거에 질병이 있었음을 표시합니다.                                                                                                                                                            |
|hasMoney        |한 엔티티(예: 사람)가 돈을 갖고 있거나 예전에 갖고 있었음을 표시합니다.                                                                                                                                                        |
|instrumentOf    |한 엔티티(예: Weapon)와 해당 엔티티로 발생되거나 이전에 발생되었던 Event 사이에 존재합니다.                                                                                                              |
|locatedAt       |한 엔티티와 해당 엔티티의 실제 위치 사이에 존재합니다.                                                                                                                                                                |
|managerOf       |한 Person과 해당 Person이 자신의 일로서 관리하는 다른 엔티티(예: Person 또는 Organization) 사이에 존재합니다.                                                                                              |
|measureOf       |한 엔티티의 높이 또는 중량과 같이 특정 Measure를 표시합니다.                                                                                                                                          |
|memberOf        |Person, Organization 또는 GeopoliticalEntity와 같은 한 엔티티와 해당 엔티티가 속하는 또다른 엔티티 사이에 존재합니다.                                                                                            |
|near            |물리적으로 서로 가깝게 위치하는 두 개의 엔티티 사이에 존재합니다.                                                                                                                                       |
|overlaps        |두 Time 또는 Event가 일시적으로 겹치는 것을 표시합니다. 텍스트가 명확하게 관계를 지정하는 경우에만 표시됩니다.                                                                                                   |
|ownerOf         |Person, Organization 또는 GeopoliticalEntity와 같은 한 엔티티와 해당 엔티티가 영구적으로 또는 일시적으로 소유하는 엔티티 사이에 존재합니다.                                                                     |
|parentOf        |한 Person 또는 Animal과 해당 Person 또는 Animal의 자식/새끼 또는 의붓자식/새끼 사이에 존재합니다.                                                                                                                                         |
|participantIn   |Person, Animal, Organization 또는 GeopoliticalEntity와 같은 한 참여자와 해당 참여자가 참여하거나 이전에 참여했던 이벤트 사이에 존재합니다.                                                         |
|partner         |경제적 협력 관계에 있는 두 Organization 또는 GeopoliticalEntity 사이에 존재합니다.                                                                                                                  |
|partOf          |두 번째 엔티티가 첫 번째 엔티티를 포함하는 관련된 유형 또는 동일한 유형의 더 작거나 더 큰 엔티티 사이에 존재합니다. 엔티티가 Event인 경우 첫 번째 엔티티는 두 번째 엔티티의 기간 내에 발생합니다. |
|partOfMany      |두 번째 엔티티가 복수여야 하며 첫 번째 엔티티를 포함하고 하나 이상의 엔티티로 구성할 수 있는 동일한 유형 또는 관련 유형의 더 작은 엔티티와 더 큰 엔티티 사이에 존재합니다.                      |
|playsRoleOf     |한 Person과 해당 Person이 임무를 수행하는 특정 특성 사이에 존재합니다.                                                                                                                  |
|populationOf    |Cardinal과 숫자가 전체 인구를 나타내는 엔티티(예: 조직 또는 국가) 사이에 존재합니다.                                                                                  |
|productOf       |한 Product 또는 TitleWork과 해당 Product 또는 TitleWork를 생성한 Organization 사이에 존재합니다.                                                                                                                                       |
|quantityOf      |두 번째 엔티티의 양 또는 수량인 Cardinal을 표시합니다.                                                                                                                                            |
|rateOf          |Rate와 발생 빈도를 지정하는 Event 사이에 존재합니다.                                                                                                                                     |
|relative        |좀 더 특정한 관계가 부적절한 경우 한 Person 또는 Animal과 해당 Person 또는 Animal이 상대적인 다른 Person 또는 Animal 사이에 존재합니다.                                                               |
|residesIn       |살아 있는 한 엔티티와 해당 엔티티가 영구적으로 위치하는 위치 사이에 존재합니다.                                                                                                                       |
|shareholdersOf  |한 사람, Organization 또는 GeopoliticalEntity와 첫 번째 엔티티가 주주인 Organization 사이에 존재합니다.                                                                                                  |
|siblingOf       |Person 또는 Animal과 해당 Person 또는 Animal의 형제 또는 이복 형제 사이에 존재합니다.                                                                                                                                     |
|spokespersonFor |한 Person과 해당 Person이 표현하는 엔티티 사이에 존재합니다. 텍스트가 세계 정세의 지식을 따르지 않고 명시적으로 관계를 언급하는 경우에만 표시됩니다.                                                           |
|spouseOf        |정식 배우자인 두 명의 People 사이에 존재합니다.                                                                                                                                                      |
|subsidiaryOf    |첫 번째가 두 번째의 부속 항목일 때 두 개의 Organization 사이에 존재합니다. 이는 첫 번째 엔티티가 두 번째 엔티티의 제어 하에 있더라도 자율성이 높음을 의미합니다.                               |
|timeOf          |이벤트가 발생한 Date, Time 또는 Duration을 표시합니다. TitleWork는 공개되거나 수행되거나 브로드캐스트됩니다. 또는 법이 처음 초안 작성되거나 작성되거나 통과되거나 폐기되었습니다.    

## 관계 추출에 특정한 엔티티 유형
{: #specific-entity-types}

다음 엔티티는 관계 추출 인리치먼트로 식별될 수 있습니다.

|엔티티 유형|
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
