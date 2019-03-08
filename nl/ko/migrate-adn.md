---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-08"

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

# AlchemyData News에서 마이그레이션
{: #migrate-adn}

**2017년 7월 31일**에 {{site.data.keyword.discoverynewsfull}}의 새 버전이 발표되었습니다. 이 콜렉션에 대한 설명은 [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html)를 참조하십시오.

AlchemyData News는 **2018년 3월 7일**(서비스일)부터 삭제되어 사용이 중지되었습니다.

## 서비스 비교
{: shortdesc}

AlchemyData News에서 {{site.data.keyword.discoveryshort}} 서비스의 {{site.data.keyword.discoverynewsshort}}로 이동할 때 주목할 차이점은 다음과 같습니다.

- {{site.data.keyword.discoveryshort}}는 조회를 통한 뉴스 조회만 요금을 부과합니다. 추가 비용 없이 각 결과와 함께 모든 필드를 리턴할 수 있습니다.
- 각 {{site.data.keyword.discoveryshort}} 조회는 최대 50개의 결과를 리턴할 수 있습니다. `offset` 매개변수를 사용할 수 있으므로 필요한 결과 수만큼 조회를 호출할 수 있습니다.
- {{site.data.keyword.discoveryshort}}는 추가로 집계를 지원합니다. 자세한 정보는 {{site.data.keyword.discoveryshort}} 문서의 [집계](/docs/services/discovery/query-reference.html#aggregations) 절을 참조하십시오.
- {{site.data.keyword.discoverynewsfull}}는 AlchemyData News와 같은 방식으로 순위를 지정하지 않습니다. 현재 순위 지정을 위한 필드는 없습니다.
- {{site.data.keyword.discoverynewsshort}}와 AlchemyData News 간에 조회 구조 및 리턴되는 데이터의 구조가 다릅니다. JSON 구조를 이해하기 위한 좋은 방법은 {{site.data.keyword.discoverynewsshort}}의 단일 결과에 대해 조회하고 결과를 확인하는 것입니다.
- {{site.data.keyword.discoverynewsshort}}는 XML 출력을 지원하지 않습니다.
- 중복 제거는 {{site.data.keyword.discoverynewsshort}}의 베타 기능입니다.

## 인증 차이점

{{site.data.keyword.discoveryshort}} 서비스는 표준 {{site.data.keyword.Bluemix_notm}} `username` 및 `password` 인증 정보를 사용하여 조회에 액세스합니다. 이는 AlchemyData 뉴스에서 사용한 기존 API 키 메소드를 대체합니다. 모든 {{site.data.keyword.discoveryshort}} 조회는 {{site.data.keyword.discoveryshort}} 서비스 인스턴스로 작성된 사용자 이름 및 비밀번호 조합으로 수행되어야 합니다.

{{site.data.keyword.Bluemix_notm}} 내 서비스의 **서비스 인증 정보** 탭 보기를 통해 서비스 인증 정보를 관리할 수 있습니다.

## Discovery 인스턴스 구성

{{site.data.keyword.discoveryshort}} 서비스 인스턴스는 AlchemyData News 인스턴스를 작성한 방법과 동일하게 작성됩니다.

1. [{{site.data.keyword.Bluemix_notm}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window}로 이동하여 로그인한 후 서비스 카탈로그에서 {{site.data.keyword.discoveryshort}}를 선택하십시오.
1. 사용자의 요구에 적합한 구성을 선택하고 **작성**을 클릭하십시오.

  {{site.data.keyword.discoveryshort}} 서비스는 매달 1000개의 뉴스 조회가 포함된 라이트 플랜을 제공합니다. 이 플랜의 인스턴스를 사용하여 무료로 동등한 조회를 식별할 수 있습니다.
  {: tip}

1. **서비스 인증 정보** 탭을 클릭하고 **인증 정보 보기**를 선택하여 이 인스턴스에 대한 `url`, `username` 및 `password`를 식별하십시오.

## Watson Discovery News 조회

API 또는 {{site.data.keyword.watson}} SKD 중 하나를 사용하여 {{site.data.keyword.discoverynewsfull}}를 조회할 수 있습니다. 또한 조회 빌드 도구를 사용하여 대화식으로 조회를 구성할 수 있습니다.

{{site.data.keyword.discoveryshort}} 도구를 실행하고 {{site.data.keyword.discoverynewsshort}}를 조회하려면 다음을 수행하십시오.

1. **서비스** 아래에서 {{site.data.keyword.discoveryshort}}를 위한 **도구 실행**을 클릭하십시오.
1. {{site.data.keyword.discoverynewsshort}} 타일을 클릭하여 **데이터 관리** 화면을 여십시오.
1. **데이터 스키마 보기**, **조회 빌드**를 차례로 클릭하여 조회 빌더를 여십시오.

  {{site.data.keyword.discoverynewsfull}}의 조회가 개인 데이터 콜렉션에 대해 작성된 조회와 동일한 방식으로 구조화됩니다. [조회 개념](/docs/services/discovery/using.html) 및 [조회 참조](/docs/services/discovery/query-reference.html)를 참조하십시오.
  {: tip}

**참고**: AlchemyData News 및 {{site.data.keyword.discoverynewsfull}}에서 유사한 조회에 대해 동일한 결과가 리턴될 것이라고 예상하지 마십시오. 크롤링 시간, 소스 및 인리치먼트가 모두 결합되어 다른 결과를 리턴합니다.

## 애플리케이션에 Watson Discovery News 조회 추가

다음 방법 중 하나를 사용하여 조회를 애플리케이션에 추가하십시오. 모든 예제는 `IBM`의 `text` 값을 사용하는 `enriched_text.entities`(`enriched_text.entities.text:IBM`)에 대해 조회합니다.

다음 모든 예제에서 사용자 이름과 비밀번호를 서비스 인스턴스의 **서비스 인증 정보** 페이지에 나열된 `{username}` 및 `{password}`로 대체하십시오.

### API에 직접 호출 사용

```bash
curl -u "{username}":"{password}"  'https://gateway.watsonplatform.net/discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

### Java SDK 사용

```java
Discovery discovery = new Discovery("2017-11-07");
discovery.setEndPoint("https://gateway.watsonplatform.net/discovery/api/v1");
discovery.setUsernameAndPassword("{username}", "{password}");  
String environmentId = "system";
  String collectionId = "news";

QueryRequest.Builder queryBuilder = new QueryRequest.Builder(environmentId,collectionId);  
queryBuilder.query("enriched_text.entities.text:IBM");  
QueryResponse queryResponse =  
discovery.query(queryBuilder.build()).execute();
```
{: codeblock}

### Watson Node.js SDK 사용

```javascript
var watson = require('watson-developer-cloud');

var discovery = new DiscoveryV1({  
  username: '{username}',  
  password: '{password}',  
  version_date: '2017-11-07'  
});  

discovery.query(('system', 'news', 'enriched_text.entities.text:IBM'),  
  function(error, data) {  
  console.log(JSON.stringify(data, null, 2));  
```
{: codeblock}

### Watson Python SDK 사용

```python
import sys
import os
import json
from watson_developer_cloud import DiscoveryV1

discovery = DiscoveryV1(
  username="{username}",
  password="{password}",
  version="2017-11-07"
)

qopts = {'query': 'enriched_text.entities.text:IBM'}
my_query = discovery.query('{environment_id}', '{collection_id}', qopts)
print(json.dumps(my_query, indent=2))
```
{: codeblock}
