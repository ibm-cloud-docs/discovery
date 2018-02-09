---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-30"

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

# Watson Discovery Visual Insights
{: #visual-insights}

{{site.data.keyword.discoveryfull}} Visual Insights는 시맨틱 요소, 관계, 개념 등에 대한 {{site.data.keyword.discoveryshort}}의 이해로 식별된 연결을 시각적으로 탐색하는 데 사용할 수 있는 실험 기능입니다. 

사용자에게 필요한 정보를 제공하는 기존 솔루션 또는 새 애플리케이션에 통합할 수 있는 조회를 작성하기 위해 {{site.data.keyword.discoveryshort}}를 사용하기 전에 {{site.data.keyword.discoveryfull}} Visual Insights를 사용하여 콜렉션에 대해 자세히 알아볼 수 있습니다. 

실험 릴리스 중에 Visual Insights는 공용 환경에서만 사용할 수 있습니다. 

**면책사항:** Visual Insights는 실험 기능입니다. 이 기능은 불안정하고 자주 변경될 수 있으며 충분한 예고 없이 중단될 수 있습니다. 해당 기능을 평가할 수 있는 기능이 제공됩니다. 일반적으로 릴리스된 용량이 제공하는 동일한 레벨의 성능 또는 기능을 제공하지 않을 수 있습니다. 이 용량은 프로덕션 환경에서 사용하도록 설계되지 않았으므로 모든 사용은 사용자의 전적인 책임에 따릅니다. 자세한 사항은 [베타/실험 기능](/docs/services/discovery/release-notes.html#beta-features)을 참조하십시오. 

## Visual Insights의 빠른 둘러보기
{: #quick-tour-visual-insights}

![Discovery Visual Insights 빠른 둘러보기](images/discovery-visualinsights-quicktour.png)

Visual Insights 화면은 네 개의 기본 영역으로 구성됩니다. 

### 검색 표시줄
{: #search-bar}

맨 위에서 **검색 표시줄**을 사용하여 {{site.data.keyword.discoveryshort}} 콜렉션을 조회할 수 있습니다. 

- {{site.data.keyword.Bluemix_notm}} 신임 정보를 사용하여 로그인한 경우 사용자의 계정과 연관된 {{site.data.keyword.discoveryshort}} 인스턴스의 모든 콜렉션은 콜렉션 드롭 다운(기본적으로 {{site.data.keyword.discoverynewsfull}})에서 사용할 수 있습니다. 로그인하지 않은 경우 {{site.data.keyword.discoverynewsfull}} 콜렉션만 사용할 수 있습니다. 
- 콜렉션을 선택하고 검색 상자에 조회를 입력한(예: `What is net neutrality`) 후 **검색** 단추를 클릭하여 검색하십시오. 대형 콜렉션의 경우 결과를 표시하는 데 1분 이상 소요될 수 있습니다. `documents`, `concepts`, `people`, `locations`, `organizations` 또는 `companies` 단추를 클릭하여 검색을 필터링할 수 있습니다. 
- 선택적으로 머리글의 ![조회 아이콘](images/discovery-query-icon.png) 아이콘을 클릭하여 표시된 결과(엔티티, 개념 또는 문서)의 모든 항목을 선택할 수 있습니다. 
- 개인용 콜렉션이 선택되고 조회가 입력되지 않은 경우 콜렉션의 최대 1000개의 문서가 [세부사항 분할창](/docs/services/discovery/visual-insights.html#details-pane)에 표시됩니다. {{site.data.keyword.discoverynewsshort}} 콜렉션이 선택되고 조회가 입력되지 않은 경우 선택한 100개의 최신 기사가 표시됩니다. 

### 네트워크 디스플레이
{: #network-display}

검색 표시줄 아래의 중앙 패널이 **네트워크 디스플레이**입니다. 이는 조회 결과의 대화식 시각화입니다. 

- **네트워크 디스플레이**는 조회 결과에서 추출된 문서, 엔티티 및 개념의 표시입니다. 분홍색 노드는 문서를 나타내고 파란색 노드는 엔티티 또는 개념을 나타냅니다. 각 문서 노드는 {{site.data.keyword.discoveryshort}}로 해당 문서에서 발견된 모든 엔티티 및 개념 노드로 연결합니다. 문서가 더 많이 유사할수록 시각화에서 좀 더 서로 가깝게 위치합니다. 
- **네트워크 디스플레이**의 노드에 마우스를 놓으면 연관된 제목이 표시되고 다른 노드에 대한 링크가 강조표시됩니다. 
- 노드를 클릭하면 해당 노드에 대한 정보가 [세부사항 분할창](/docs/services/discovery/visual-insights.html#details-pane)에 표시됩니다. 

### 세부사항 분할창
{: #details-pane}

네트워크 디스플레이의 오른쪽에 **세부사항 분할창**이 있습니다. 

- 세부사항 분할창은 분류 및 날짜(사용 가능한 경우), 짧은 발췌(전체 문서를 여는 옵션 포함) 및 연결된 엔티티 및 개념을 포함하여 각 문서에 대한 추가 세부사항을 제공합니다. 
- 문서가 아닌 노드가 네트워크 디스플레이에서 선택되면 해당 노드에 대한 정보가 세부사항 분할창의 맨 위에 표시됩니다. 
- 세부사항 분할창에서 연결된 엔티티 또는 개념을 클릭하면 네트워크 디스플레이에서 해당 노드가 선택됩니다. 

### 탐색 분할창
{: #navigation-pane}

네트워크 디스플레이의 왼쪽에 **탐색 분할창**이 있습니다. 이 분할창은 선택된 콜렉션의 조회 결과에서 추출된 가장 일반적인 용어의 태그 클라우드 개요를 제공합니다. 용어가 클수록 조회 결과에 더욱 일반적인 용어가 포함됩니다. 

- 태그에 있는 용어를 선택하면 분홍색으로 변경되고 용어와 연관된 네트워크 디스플레이의 문서가 강조표시됩니다. 세부사항 분할창은 강조표시된 문서의 목록을 표시합니다. 이제 태그 클라우드의 기타 용어는 선택된 용어와의 관계를 표시하게 됩니다. 
  - 회색으로 표시된 용어는 강조표시된 문서와 연관되지 않습니다. 
  - 용어가 보라색이 되면 강조표시된 모든 문서와 연관되고 문서 중에서 구분하려는 경우 도움이 되지 않습니다. 
  - 파란색의 용어는 전체 문서가 아닌 일부 문서와 연관되고 이에 따라 강조표시된 문서의 세트를 추가로 세분화하는데 사용될 수 있습니다. 이 용어 중 하나만 선택하면 강조표시된 문서의 세트가 두 태그와 연관된 용어로만 축소되고 네트워크 디스플레이는 문서가 위치한 영역에 맞게 확대/축소됩니다. 몇 번의 클릭만으로 대형 문서 세트를 소형 문서 세트로 세분화하는 데 이 메소드를 사용할 수 있습니다. 
- 선택된 용어를 선택 취소하려면 용어를 다시 클릭하십시오. 선택된 모든 용어를 선택 취소하려면 태그 클라우드에서 단어 사이의 공백을 클릭하십시오. 회색 태그를 클릭하면 기존의 선택사항이 선택 취소되고 해당 용어를 선택됩니다. 
- 문서, 사람, 개념, 조직, 위치 및 회사의 유형 및 수는 태그 클라우드 위에 표시됩니다. 이들 중 하나를 클릭하여 태그 클라우드 및 네트워크 디스플레이 시각화를 필터링하십시오. 

## Visual Insights 사용
{: #using-visual-insights}

로그인하지 않고 Visual Insights를 사용하여 {{site.data.keyword.discoverynewsfull}}를 조회할 수 있습니다. 고유한 콜렉션으로 Visual Insights를 사용하려면 다음 항목이 필요합니다. 

- {{site.data.keyword.discoveryshort}}인스턴스가 포함된 {{site.data.keyword.Bluemix_notm}} 계정. 
- [엔티티 추출](/docs/services/discovery/building.html#entity-extraction) 인리치먼트로 강화되며, 선택적으로 [개념 태그 지정](/docs/services/discovery/building.html#concept-tagging), [키워드 추출](/docs/services/discovery/building.html#keyword-extraction), [관계 추출](/docs/services/discovery/building.html#relation-extraction) 및 [카테고리 분류](/docs/services/discovery/building.html#category-classification) 인리치먼트로 강화된 해당 {{site.data.keyword.discoveryshort}} 인스턴스에 있는 하나 이상의 콜렉션. 기타 인리치먼트가 포함될 수 있지만 Visual Insights로 표시되지 않습니다. 

{{site.data.keyword.discoveryshort}} 및 무료로 시작하는 방법에 대한 자세한 정보는 [Watson {{site.data.keyword.discoveryshort}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/services/discovery/){: new_window}를 참조하십시오.

사용자가 {{site.data.keyword.Bluemix_notm}} 계정, {{site.data.keyword.discoveryshort}} 인스턴스 및 채워진 하나 이상의 콜렉션을 갖게 되면 로그인할 때 Visual Insights에서 콜렉션을 볼 수 있습니다. 

Visual Insights에 로그인

1. [{{site.data.keyword.discoveryshort}} Visual Insights ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://visual-insights.bluemix.net){: new_window}를 여십시오.
1. 검색 표시줄의 ![프로파일 아이콘](images/discovery-profile-icon.png) 아이콘을 클릭하십시오. 
1. {{site.data.keyword.Bluemix_notm}} ID 및 비밀번호를 입력하십시오. 몇 분 후 검색 표시줄에서 콜렉션을 선택할 수 있습니다. 

## 피드백 제공
{: #providing-feedback}

{{site.data.keyword.discoveryshort}} Visual Insights에 대한 사용자의 피드백에 관심이 있습니다. 피드백 링크에 액세스하려면 머리글의 ![정보 아이콘](images/discovery-info-icon.png) 아이콘을 클릭하십시오. 
