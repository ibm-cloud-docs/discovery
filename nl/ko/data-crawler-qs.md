---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-28"

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

# Data Crawler 시작하기
{: #getting-started-with-the-data-crawler}

이 절에서는 로컬 파일 시스템에서 파일을 수집하고, {{site.data.keyword.discoveryfull}} 서비스로 사용하기 위해 Data Crawler를 사용하는 방법에 대해 설명합니다.
{: shortdesc}

Data Crawler는 파일 공유 또는 데이터베이스를 크롤링하기 위해서만 사용되어야 합니다. 기타 모든 경우에는 적합한 {{site.data.keyword.discoveryshort}} 커넥터를 사용해야 합니다. 자세한 사항은 [데이터 소스에 연결](/docs/services/discovery?topic=discovery-sources#sources)을 참조하십시오. {{site.data.keyword.discoveryshort}} 커넥터에서 지원되는 데이터 소스를 사용하여 Data Crawler를 사용하는 경우 Data Crawler에 대한 지원이 더 이상 제공되지 않습니다.
{: important}

이 태스크를 시도하기 전에 {{site.data.keyword.Bluemix}}에 {{site.data.keyword.discoveryshort}} 서비스의 인스턴스를 작성하십시오. 이 안내서를 완료하려면 작성한 서비스의 인스턴스와 연관된 인증 정보를 사용해야 합니다.

## 환경 작성
{: #dc-create-environment}

bash POST /v1/environments 메소드를 사용하여 환경을 작성하십시오. 환경을 모든 문서 상자를 저장하는 창고로 간주하십시오. 다음 예는 `my-first-environment`라는 환경을 작성합니다.

`{apikey}`를 서비스 인증 정보로 대체하십시오.

({apikey} 인증 정보 사용에 대한 자세한 정보는 [API 시작하기](/docs/services/discovery?topic=discovery-gs-api#gs-api)를 참조하십시오.)

```bash
curl -X POST -u "apikey:{apikey}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
```
{: pre}

API가 환경 ID, 환경 상태 및 환경에서 사용 중인 스토리지의 크기와 같은 정보가 포함된 응답을 리턴합니다. 사용자 환경이 `ready` 상태가 될 때까지 다음 단계로 이동하지 마십시오. 환경을 작성 중일 때 상태에서 `status:pending`을 리턴하면 `GET /v1/environments/{environment_id}` 메소드를 사용하여 준비될 때까지 상태를 확인하십시오. 이 예에서 `{apikey}`를 서비스 인증 정보로 대체하고 `{environment_id}`를 환경을 작성할 때 리턴된 환경 ID로 대체하십시오.

```bash
curl -u "apikey:{apikey}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}?version=2017-11-07
```
{: pre}

## 콜렉션 작성
{: #dc-create-collection}

그런 다음 `POST /v1/environments/{environment_id}/collections` 메소드를 사용하여 콜렉션을 작성하십시오. 콜렉션을 사용자의 환경에 문서를 저장하는 상자로 간주하십시오. 이 예에서는 이전 단계에서 작성한 환경에 `my-first-collection`이라는 콜렉션을 작성하고 다음 구성을 사용합니다.

-   `{apikey}`를 서비스 인증 정보로 대체하십시오.
-   `{environment_id}`를 단계 1에서 작성한 환경의 환경 ID로 대체하십시오.

콜렉션을 작성하기 전에 기본 구성의 ID를 가져와야 합니다. 기본 `configuration_id`를 찾으려면 `GET /v1/environments/{environment_id}/configurations` 메소드를 사용하십시오.

```bash
curl -u "apikey:{apikey}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07
```
{: pre}

기본 구성 ID가 제공되면 이를 사용하여 콜렉션을 작성하십시오. `{configuration_id}`를 사용자 환경의 기본 구성 ID로 대체하십시오.

```bash
curl -X POST -u "apikey:{apikey}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{configuration_id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07
```
{: pre}

API가 콜렉션 ID, 콜렉션 상태 및 콜렉션에서 사용 중인 스토리지의 크기와 같은 정보가 포함된 응답을 리턴합니다. 사용자 콜렉션이 `online` 상태가 될 때까지 다음 단계로 이동하지 마십시오. 콜렉션을 작성 중일 때 상태에서 `status:pending`을 리턴하면 `GET /v1/environments/{environment_id}/collections/{collection_id}` 메소드를 사용하여 준비될 때까지 상태를 확인하십시오. 이 예에서 `{apikey}`를 서비스 인증 정보로 대체하고 `{environment_id}`를 환경 ID로 대체하며 `{collection_id}`를 이 단계에서 이전에 리턴한 콜렉션 ID로 대체하십시오.

```bash
curl -u "apikey:{apikey}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07
```
{: pre}

## 예제 문서 다운로드
{: #dc-download-documents}

다음과 같은 문서를 다운로드하십시오.

-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘" title="외부 링크 아이콘"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘" title="외부 링크 아이콘"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘" title="외부 링크 아이콘"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘" title="외부 링크 아이콘"></a>

## Data Crawler 다운로드 및 설치
{: #download-and-install-the-data-crawler}

1.  시스템 전제조건을 확인하십시오.

    -   Java Runtime Environment 버전 8 이상

        **참고:** 크롤러를 실행하려면 `JAVA_HOME` 환경 변수가 올바르게 설정되거나 전혀 설정되지 않아야 합니다.
    -   Red Hat Enterprise Linux 6 또는 7 또는 Ubuntu Linux 15 또는 16. 최적의 성능을 위해 Data Crawler는 가상 머신, 컨테이너 또는 하드웨어 여부에 상관 없이 Linux의 자체 인스턴스에서 실행되어야 합니다.
    -   Linux 시스템에서 최소 2GB RAM

1.  브라우저를 열고 [{{site.data.keyword.Bluemix_notm}} 계정 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/){: new_window}에 로그인하십시오.
1.  {{site.data.keyword.Bluemix_notm}} 대시보드에서 이전에 작성한 {{site.data.keyword.discoveryshort}} 서비스를 선택하십시오.
1.  **Discovery 서비스에 컨텐츠 업로드 자동화**에서 사용자 시스템에 맞는 적절한 다운로드 링크(DEB, RPM 또는 ZIP)를 선택하여 Data Crawler를 다운로드하십시오.
1.  관리자로서 적절한 명령을 사용하여 다운로드한 아카이브 파일을 설치해야 합니다.

    -   rpm 패키지를 사용하는 시스템(예: Red Hat, CentOS)에서 `rpm -i /full/path/to/rpm/package/rpm-file-name`과 같은 명령을 사용하십시오.
    -   deb 패키지를 사용하는 시스템(예: Ubuntu, Debian)에서 `dpkg -i /full/path/to/deb/package/deb-file-name`과 같은 명령을 사용하십시오.
    -   크롤러 스크립트는 `{installation directory}/bin`에 설치됩니다. 예를 들면, `/opt/ibm/crawler/bin`입니다. 크롤러 명령이 올바르게 작동하려면 `{installation_directory}/bin`이 사용자의 `PATH` 환경 변수에 있어야 합니다.

    또한 크롤러 스크립트는 `/usr/local/bin`에 설치되므로 `PATH` 환경 변수에도 추가될 수 있습니다.
    {: tip}

## 작업 디렉토리 작성
{: #dc-working-directory}

`{installation_directory}/share/examples/config` 디렉토리의 컨텐츠를 시스템의 작업 디렉토리에 복사하십시오. 예를 들면, `/home/config`입니다.

**경고:** 제공된 구성 예제 파일을 바로 수정하지 마십시오. 이 예제 파일을 복사한 후 편집하십시오. 제공된 예제 파일을 바로 편집하는 경우 Data Crawler를 업그레이드할 때 구성이 겹쳐쓰이거나 Data Crawler를 설치 제거할 때 구성이 제거될 수 있습니다.

**참고:** `config` 디렉토리에 있는 파일(예: `config/crawler.conf`)과 관련된 이 안내서의 참조는 작업 디렉토리(설치된 `{installation_directory}/share/examples/config` 디렉토리가 아님)의 해당 파일을 참조합니다.

## 크롤러 옵션 구성
{: #dc-configure-crawl-options}

저장소를 크롤링하기 위해 Data Crawler를 설정하려면 크롤링할 로컬 시스템 파일 및 크롤링이 완료된 후 크롤링된 파일의 콜렉션에 전송할 {{site.data.keyword.discoveryshort}} 서비스를 지정해야 합니다.

1.  **`filesystem-seed.conf`** - 텍스트 편집기에서 `seeds/filesystem-seed.con` 파일을 여십시오. 크롤링할 파일 경로로 `name-"url"` 속성 바로 아래에서 `value` 속성을 수정하십시오. 예를 들면, `value-"sdk-fs:///TMP/MY_TEST_DATA/"`입니다.

    **참고:** URL은 `sdk-fs://`로 시작되어야 합니다. 예를 들어, `/home/watson/mydocs`를 크롤링하려면 이 URL의 값은 `sdk-fs:///home/watson/mydocs`가 되어야 합니다. 세 번째 /가 필수입니다!

    파일을 저장한 후 닫으십시오.

1.  **`discovery_service.conf`** - 텍스트 편집기에서 `discovery/discovery_service.conf` 파일을 여십시오. 이전에 {{site.data.keyword.Bluemix_notm}}에서 작성했던 {{site.data.keyword.discoveryshort}} 서비스에 특정한 다음 값을 수정하십시오.

    -   `environment_id` - {{site.data.keyword.discoveryshort}} 서비스 환경 ID입니다.
    -   `collection_id` - {{site.data.keyword.discoveryshort}} 서비스 콜렉션 ID입니다.
    -   `configuration_id` - {{site.data.keyword.discoveryshort}} 서비스 구성 ID입니다.
    -   `configuration` - 이 `discovery_service.conf` 파일의 전체 경로 위치입니다(예: `/home/config/discovery/discovery_service.conf`).
    -   `apikey` - {{site.data.keyword.discoveryshort}} 서비스에 대한 인증 정보입니다. 
1.  **`crawler.conf`** - 텍스트 편집기에서 `config/crawler.conf` 파일을 여십시오.

    -   다음과 같이 {{site.data.keyword.discoveryshort}} 서비스에 대해 `output_adapter` `class` 및 `config` 옵션을 설정하십시오.

        ```bash
    class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

        config - "discovery_service"

        discovery_service {
          include "discovery/discovery_service.conf"
        }
        ```
        {: pre}

1.  이러한 파일을 수정하면 데이터를 크롤링할 준비가 됩니다.

## 데이터 크롤링
{: #dc-crawl}

`crawler crawl --config [config/crawler.conf]` 명령을 실행하십시오.

구성 파일 `crawler.conf`를 사용하여 크롤링이 실행됩니다.

**참고:** `--config` 옵션에 전달된 구성 파일에 대한 경로는 완전한 경로여야 합니다. 즉, 상대 형식(예: `config/crawler.conf` 또는 `./crawler.conf`)으로 되어 있거나 절대 경로(예: `/path/to/config/crawler.conf`)로 되어 있어야 합니다.

## 문서 검색
{: #dc-search}

마지막으로 `GET /v1/environments/{environment_id}/collections/{collection_id}/query` 메소드를 사용하여 문서의 콜렉션을 검색하십시오. 다음 예에서는 `IBM`이라고 하는 모든 엔티티를 리턴합니다.

-   `{apikey}`를 서비스 인증 정보로 대체하십시오.
-   `{environment_id}`를 단계 1에서 작성한 환경의 환경 ID로 대체하십시오.
-   `{collection_id}`를 단계 2에서 작성한 콜렉션의 콜렉션 ID로 대체하십시오.

```bash
curl -u "apikey:{apikey}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query-enriched_text.entities.text:IBM'
```
{: pre}

## 결과
{: #dc-results}

작성한 환경 및 콜렉션에서 문서 조회를 완료했습니다. 이제 더 많은 문서를 콜렉션에 추가하여 사용자 정의를 시작할 수 있습니다.
