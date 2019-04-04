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

# 關係類型
{: #relation-types}

下表列出[關係擷取](/docs/services/discovery?topic=discovery-configservice#relation-extraction)強化所傳回的可能關係類型。
{: shortdesc}

|關係            |說明|
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|affectedBy      |存在於實體與具有明確方向性且會影響該實體的事件之間。|
|affiliatedWith  |存在於具有連結或類似連接的兩個實體之間。|
|ageOf           |與實體的經歷時間相關。|
|agentOf         |存在於實體與該實體在其中根據文字擔任最活躍的角色的事件之間。不需要背景知識。|
|authorOf        |存在於人員與其建立的 TitleWork 之間。|
|awardedBy       |存在於「獎項」或「學位」與頒予或授予它的人員或組織之間。|
|awardedTo       |存在於「獎項」或「學位」與它頒予或授予的人員或組織之間。|
|basedIn         |存在於「組織」與其主要、唯一或本質上所在位置之間。|
|before          |表示兩個「時間」或「事件」之間的時間關係 "before"。只有在文字明確指定關係時才加以標示。|
|bornAt          |存在於「人員」或「動物」與其出生地之間。|
|bornOn          |存在於「人員」或「動物」與其出生「日期」或「時間」之間。|
|capitalOf       |存在於資本與其國家、州省（縣市）之間。只有在文字明確指出關係時才加以標示，並非以全球知識為基礎。|
|citizenOf       |存在於人員與其為公民的 GeopolticalEntity 之間。|
|clientOf        |存在於兩個實體之間，其中一個實體為另一個實體的直接商業客戶（亦即，支付特定服務或產品）。|
|colleague       |存在於兩個屬於相同「組織」的「人員」之間。|
|competitor      |存在於從事經濟競爭的兩個 GeopolticalEntity 或「組織」之間。|
|contactOf       |使聯絡資訊與實體相關。|
|diedAt          |存在於「人員」或「動物」與其死亡地之間。|
|diedOf          |存在於「人員」或「動物」與其死亡原因之間。|
|diedOn          |存在於「人員」或「動物」與其死亡「日期」或「時間」之間。|
|dissolvedOn     |存在於「組織」之類的實體與其解散「日期」或「時間」之間。|
|educatedAt      |存在於「人員」與其受教育之「組織」之間。|
|employedBy      |存在於兩個實體之間，其中一個實體因特定工作或服務而支付另一個實體；必須涉及酬金。在許多情況下，標示此關係需要全球知識。|
|foundedOn       |存在於「組織」之類的實體與其成立「日期」或「時間」之間。|
|founderOf       |存在於「人員」或 GeopoliticalEntity 與實體（例如其所成立的「組織」）之間。|
|hasDisease      |指出「人員」或「動物」有疾病。|
|hasMoney        |指出實體（例如人員）有錢。|
|instrumentOf    |存在於實體（例如「武器」）與使用該實體而引起的「事件」之間。|
|locatedAt       |存在於實體與其實際位置之間。|
|managerOf       |存在於「人員」與另一個實體（例如其在工作上管理的「人員」或「組織」）之間。|
|measureOf       |指出特定「測量」，例如實體的高度或重量。|
|memberOf        |存在於實體（例如「人員」、「組織」或 GeopoliticalEntity）與其所屬的另一個實體之間。|
|near            |存在於實際上彼此位置很接近的兩個實體之間。|
|overlaps        |指出兩個「時間」或「事件」暫時重疊。只有在文字明確指定關係時才加以標示。|
|ownerOf         |存在於實體（例如「人員」、「組織」或 GeopoliticalEntity）與其所擁有（不論是永久或暫時）的實體之間。|
|parentOf        |存在於「人員」或「動物」與其子女或繼子女之間。|
|participantIn   |存在於參與者（例如「人員」、「動物」、「組織」或 GeopoliticalEntity）與其正在參與或曾經參與的「事件」之間。|
|partner         |存在於從事經濟合作的兩個 GeopolticalEntity 或「組織」之間。|
|partOf          |存在於相同類型或相關類型的一個較小實體與一個較大實體之間，其中第二個實體包含第一個實體。如果實體為「事件」，則第一個實體必須在第二個實體的時間跨距內發生。|
|partOfMany      |存在於相同類型或相關類型的多個較小實體與較大實體之間，其中第二個實體必須是複數，它包含第一個實體，且可以由一個以上的實體組成。|
|playsRoleOf     |存在於「人員」與其在績效中扮演的特定角色之間。|
|populationOf    |存在於「基數」與實體（例如該數字代表其整個人口的組織或國家）之間。|
|productOf       |存在於「產品」或 TitleWork 與產生它的「組織」之間。|
|quantityOf      |指出「基數」，它是第二個實體的數量或金額。|
|rateOf          |存在於「比率」與其指定發生頻率的事件之間。|
|relative        |存在於「人員」或「動物」與身為其親屬的另一個「人員」或「動物」之間（當更具體的關係不適當時）。|
|residesIn       |存在於活著的實體與其永久居住位置之間。|
|shareholdersOf  |存在於人員、「組織」或 GeopolticalEntity 與第一個實體為其股東的「組織」之間。|
|siblingOf       |存在於「人員」或「動物」與其兄弟姐妹或異父母兄弟姐妹之間。|
|spokespersonFor |存在於「人員」與其代表的實體之間。只有在文字明確指出關係時才加以標示，並非以全球知識為基礎。|
|spouseOf        |存在於正式配偶的兩個「人員」之間。|
|subsidiaryOf    |存在於兩個「組織」之間，第一個組織是第二個的子公司，表示無論是否在第二個實體的控制下，第一個實體都有一定的自主權。|
|timeOf          |指出發生事件的「日期」、「時間」或「持續時間」；已發佈、執行或播送 TitleWork；或初次起草、建立、通過或廢除「法律」。    

## 關係擷取特有的實體類型
{: #specific-entity-types}

下列實體可透過「關係擷取」強化加以識別：

|實體類型|
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
