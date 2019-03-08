---

copyright:
  years: 2015, 2018
lastupdated: "2018-01-16"

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

# Watson Discovery News Original에서 마이그레이션
{: #migrate-bwdn}

**2017년 7월 31일**에 {{site.data.keyword.discoverynewsshort}}의 새 버전이 발표되었습니다. 원본 버전의 이름이 {{site.data.keyword.discoverynewsshort}} Original로 변경되고 **2018년 1월 15일** 서비스부터 더 이상 사용되지 않습니다. {{site.data.keyword.discoverynewsshort}} Original에 액세스하려고 시도하면 `410 GONE` 메시지를 받게 됩니다.
{: shortdesc}

{{site.data.keyword.discoverynewsshort}} Original에서 새 버전으로 마이그레이션하려면 {{site.data.keyword.discoverynewsshort}} Original에 대해 작성된 조회의 업데이트를 포함한 일부 변경사항을 수행해야 합니다.

  **참고:** {{site.data.keyword.discoverynewsshort}} Original은 **2017년 7월 31일** 이전에 작성된 {{site.data.keyword.discoveryshort}}의 인스턴스에서만 사용 가능하며 **2018년 1월 15일** 서비스부터 더 이상 사용되지 않습니다.

이 콜렉션에 대한 설명은 [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html)를 참조하십시오.

{{site.data.keyword.discoverynewsshort}} Original에 대한 설명 및 정보는 [Watson Discovery News Original](/docs/services/discovery/discovery-auxiliary.html#watson-discovery-news-original)을 참조하십시오.

## 서비스 비교

|{{site.data.keyword.discoverynewsshort}} Original         | {{site.data.keyword.discoverynewsshort}}           |
|----------------------------------------|---------------------------------|
| **{{site.data.keyword.discoverynewsshort}} Original**은 Alchemy Language 인리치먼트(키워드 추출, 엔티티 추출, 개념 태그 지정, 관계 추출, 감성 분석 및 텍소노미 분류)를 사용하여 사전에 강화되었습니다. 추가 메타데이터(크롤링 날짜, 발행 날짜, URL 순위 지정, 호스트 순서 및 앵커 텍스트)도 추가됩니다.|**{{site.data.keyword.discoverynewsshort}}**는 {{site.data.keyword.nlushort}}(NLU) 인리치먼트(키워츠 추출, 엔티티 추출, 감성 역할 추출, 감성 분석, 관계 및 카테고리 분류)로 사전 강화됩니다. 추가 메타데이터(크롤링 날짜 및 발행 날짜)도 추가됩니다. NLU 인리치먼트에 대해 자세히 알아보려면 [인리치먼트 추가](/docs/services/discovery/building.html#adding-enrichments)를 참조하십시오.                         |
|**{{site.data.keyword.discoverynewsshort}} Original**은 서비스 인스턴스에 고유한 환경을 통해 액세스할 수 있습니다.                       |**{{site.data.keyword.discoverynewsshort}}**를 사용할 때 모든 사용자는 동일한 환경 및 콜렉션을 조회합니다. 이는 환경 및 콜렉션에 대한 모든 참조를 변경해야 함을 의미합니다.      |
| **{{site.data.keyword.discoverynewsshort}} Original**에서 API를 통해 환경을 검색할 때 콜렉션 크기, 문서 수 등과 같은 정보를 수신했습니다. |**{{site.data.keyword.discoverynewsshort}}** API는 이 정보를 리턴하지 않습니다.                          |

**{{site.data.keyword.discoverynewsshort}}**에서 다음 새 필드가 사용 가능합니다.

`enriched_text.relations.arguments.text`  
`enriched_text.relations.score`  
`enriched_text.relations.sentence`  
`enriched_text.relations.type`  
`enriched_title.relations`  
`enriched_title.relations.arguments`  
`enriched_title.relations.arguments.entities`<br/>
`enriched_title.relations.arguments.entities.text`  
`enriched_title.relations.arguments.entities.type`  
`enriched_title.relations.arguments.text`  
`enriched_title.relations.score`  
`enriched_title.relations.sentence`  
`enriched_title.relations.type`  
`external_links`  
`extracted_metadata`  
`extracted_metadata.file_type`  
`extracted_metadata.filename`  
`extracted_metadata.sha1`  
`forum_title`  
`main_image_url`

또한 많은 필드가 제거되었습니다(예: `blekko.hostrank`, `duplicate_url`, `domain`). 전체 목록은 <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/News_migration_v_1.01.xlsx" download>여기 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘" title="외부 링크 아이콘" class="style-scope doc-content"></a>를 참조하십시오.

## 새 Watson Discovery News로 조회 이동

{{site.data.keyword.discoverynewsshort}} Original에서 새 {{site.data.keyword.discoverynewsshort}}로 조회를 이동하려면 다음 방법으로 모든 기존 조회를 수정해야 합니다.  

- 조회가 호출하는 환경 ID를 변경하십시오. 뉴스 환경 이름이 모든 {{site.data.keyword.discoveryshort}} 서비스 인스턴스에서 다음으로 표준화되었습니다.

  `system`  

- 조회가 호출하는 콜렉션 ID를 변경하십시오. 뉴스 콜렉션 이름이 모든 {{site.data.keyword.discoveryshort}} 서비스 인스턴스에서 다음으로 표준화되었습니다.

  `news`

- 새 {{site.data.keyword.discoverynewsshort}}에 새 JSON 경로 구조를 사용하도록 조회를 수정하십시오. 대부분의 필드에서 경로를 변경하였고 여러 필드가 추가되었으며 하한 값 필드의 선택된 그룹이 제거되었습니다. 전체 세부사항은 필드 마이그레이션 스프레드시트(<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/News_migration_v_1.01.xlsx" download>여기 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘" title="외부 링크 아이콘" class="style-scope doc-content"></a>)를 참조하십시오. 예를 들면, 다음 조회를

  `discovery/api/v1/environments/ae5790c2-592f-432a-804a-ee16de7154d7/collections/3edcd8f1-e25a-4f44-a069-58332ad17651/query?version=2017-11-07&query=entities.type:"Company"`

  다음과 같이 변경해야 합니다.

  `discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.type:"Company"`  

## Watson Discovery News 조회

API 또는 {{site.data.keyword.watson}} SKD 중 하나를 사용하여 {{site.data.keyword.discoverynewsshort}}를 조회할 수 있습니다. 또한 조회 빌드 도구를 사용하여 대화식으로 조회를 구성할 수 있습니다.

**{{site.data.keyword.discoveryshort}} 도구를 실행하고 {{site.data.keyword.discoverynewsshort}}를 조회하려면 다음을 수행하십시오.**

1. **서비스** 아래에서 {{site.data.keyword.discoveryshort}}를 위한 **도구 실행**을 클릭하십시오.
1. {{site.data.keyword.discoverynewsshort}} 타일을 클릭하여 **데이터 관리** 화면을 여십시오.
1. **데이터 스키마 보기**, **조회 빌드**를 차례로 클릭하여 조회 빌더를 여십시오.

  {{site.data.keyword.discoverynewsshort}}의 조회가 개인 데이터 콜렉션에 대해 작성된 조회와 동일한 방식으로 구조회됩니다. [조회 개념](/docs/services/discovery/using.html) 및 [조회 참조](/docs/services/discovery/query-reference.html)를 참조하십시오.
  {: tip}

**참고:** {{site.data.keyword.discoverynewsshort}} Original 및 {{site.data.keyword.discoverynewsshort}}에서 유사한 조회에 대해 동일한 결과가 리턴될 것이라고 예상하지 마십시오. 크롤링 시간, 소스 및 인리치먼트가 모두 결합되어 다른 결과를 리턴합니다.

## 애플리케이션에 Watson Discovery News 조회 추가

다음 방법 중 하나를 사용하여 조회를 애플리케이션에 추가하십시오. 모든 예제는 `IBM`의 `text` 값을 사용하는 `enriched_text.entities`(`enriched_text.entities.text:IBM`)에 대해 조회합니다.

다음 모든 예제에서 사용자 이름과 비밀번호를 서비스 인스턴스의 **서비스 인증 정보** 페이지에 나열된 `{username}` 및 `{password}`로 대체하십시오.

### API에 직접 호출 사용

```bash
curl -u "{username}":"{password}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

### Watson Java SDK 사용

```java
Discovery discovery = new Discovery("2017-11-07");  
discovery.setEndPoint("https://gateway.watsonplatform.net/discovery/api/v1");
discovery.setUsernameAndPassword("{username}", "{password}");  
String environmentId = "system";
String collectionId = "news";

QueryRequest.Builder queryBuilder = new QueryRequest.Builder(environmentId, collectionId);  
queryBuilder.query("enriched_text.entities.text:IBM");  
QueryResponse queryResponse = discovery.query(queryBuilder.build()).execute();
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
  }
);
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
my_query = discovery.query('system', 'news', qopts)  
print(json.dumps(my_query, indent=2))  
```
{: codeblock}
