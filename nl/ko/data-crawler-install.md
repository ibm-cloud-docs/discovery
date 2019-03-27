---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-01-28"

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

# Data Crawler 다운로드 및 설치
{: #downloading-and-installing-the-data-crawler}

Data Crawler는 결국 {{site.data.keyword.discoveryshort}} 서비스에 대한 검색 결과를 구성하는 데 사용되는 원시 데이터를 수집합니다. 데이터 저장소를 크롤링할 때 크롤러는 사용자가 지정한 seed URL로 시작하는 문서 및 메타데이터를 다운로드합니다. 크롤러는 계층 구조의 문서를 발견하고(그렇지 않으면 seed URL에서 연결됨) 재검색을 위해 해당 문서를 큐에 넣습니다.
{: shortdesc}

Data Crawler는 파일 공유 또는 데이터베이스를 크롤링하기 위해서만 사용되어야 합니다. 기타 모든 경우에는 적합한 {{site.data.keyword.discoveryshort}} 커넥터를 사용해야 합니다. 자세한 사항은 [데이터 소스에 연결](/docs/services/discovery?topic=discovery-sources#sources)을 참조하십시오. {{site.data.keyword.discoveryshort}} 커넥터에서 지원되는 데이터 소스를 사용하여 Data Crawler를 사용하는 경우 Data Crawler에 대한 지원이 더 이상 제공되지 않습니다.
{: important}

## 전제조건
{: #dc-prerequisites}

-   Java Runtime Environment 버전 8 이상

    크롤러를 실행하려면 `JAVA_HOME` 환경 변수가 올바르게 설정되거나 전혀 설정되지 않아야 합니다.
    {: tip}
-   Red Hat Enterprise Linux 6 또는 7 또는 Ubuntu Linux 15 또는 16. 최적의 성능을 위해 Data Crawler는 가상 머신, 컨테이너 또는 하드웨어 여부에 상관 없이 Linux의 자체 인스턴스에서 실행되어야 합니다.

-   Linux 시스템에서 최소 2GB RAM

## Data Crawler 다운로드 및 설치
{: #dc-download-install}

1.  브라우저를 열고 [{{site.data.keyword.Bluemix}} 계정 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/){: new_window}에 로그인하십시오.

1.  {{site.data.keyword.Bluemix_notm}} 대시보드에서 이전에 작성한 {{site.data.keyword.discoveryshort}} 서비스를 선택하십시오.

1.  **Discovery 서비스에 컨텐츠 업로드 자동화** 섹션에서 적절한 링크를 클릭하여 DEB, RPM 및 ZIP 형식의 Linux용 Data Crawler를 다운로드하십시오.

1.  Java Runtime Environment 버전 8 이상을 실행 중인지 확인하십시오. `java -version` 명령을 실행하여 **1.8**을 찾으십시오. **1.8** 이전 버전을 실행 중인 경우 [IBM JDK ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/developerworks/java/jdk/){: new_window} 웹 사이트 또는 [java.com ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.java.com){: new_window}을 통해 패키지 관리 시스템에서 Java Developer Kit(JDK) 8을 설치하여 Java를 업그레이드해야 합니다.

    크롤러를 실행하려면 `JAVA_HOME` 환경 변수가 올바르게 설정되거나 전혀 설정되지 않아야 합니다.
    {: tip}

1.  관리자로서 적절한 명령을 사용하여 다운로드한 아카이브 파일을 설치해야 합니다.

    -   rpm 패키지를 사용하는 시스템(예: Red Hat, CentOS)에서 `rpm -i /full/path/to/rpm/package/rpm-file-name`과 같은 명령을 사용하십시오.
    -   deb 패키지를 사용하는 시스템(예: Ubuntu, Debian)에서 `dpkg -i /full/path/to/deb/package/deb-file-name`과 같은 명령을 사용하십시오.
    -   크롤러 스크립트는 `{installation_directory}/bin`에 설치됩니다. 예를 들면, `/opt/ibm/crawler/bin`입니다. 크롤러 명령이 올바르게 작동하려면 `{installation_directory}/bin`이 사용자의 `PATH` 환경 변수에 있어야 합니다.

    또한 크롤러 스크립트는 `/usr/local/bin`에 설치되므로 `PATH` 환경 변수에도 추가될 수 있습니다.
    {: tip}
1.  `{installation_directory}/share/examples/config` 디렉토리의 컨텐츠를 시스템의 작업 디렉토리에 복사하여 작업 디렉토리를 작성하십시오. 예를 들면, `/home/config`입니다.

    **경고:** 제공된 구성 예제 파일을 바로 수정하지 마십시오. 이 예제 파일을 복사한 후 편집하십시오. 제공된 예제 파일을 바로 편집하는 경우 Data Crawler를 업그레이드할 때 구성이 겹쳐쓰이거나 Data Crawler를 설치 제거할 때 구성이 제거될 수 있습니다.

    **참고:** `config` 디렉토리에 있는 파일(예: `config/crawler.conf`)과 관련된 이 안내서의 나머지 부분의 참조는 작업 디렉토리(설치된 `{installation_directory}/share/examples/config` 디렉토리가 아님)의 해당 파일을 참조합니다.

1.  이제 [저장소에 연결하기 위해 Data Crawler 구성](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-connector-and-seed-options)을 수행할 준비가 되었습니다.

## Data Crawler 구조
{: #dc-structure}

Data Crawler 다운로드는 시스템에 다음 폴더를 배치합니다.

-   `doc` - 저작권 및 라이센싱 정보가 있는 파일을 포함합니다.
-   `bin` - 크롤러를 실행하기 위한 스크립트 파일입니다.
-   `connectorFramework` - 엔터프라이즈 내의 내부 데이터이거나 웹 또는 클라우드의 외부 데이터인지 여부에 상관 없이 이 디렉토리의 파일은 사용자와 데이터 간의 대화를 허용합니다.
-   `lib` - 크롤러에서 사용하는 라이브러리 파일입니다.
-   `share`
    -   `doc` - HTML 및 Markdown으로 형식화된 문서 파일을 모두 제공합니다.
    -   `examples/config` - 크롤링을 위해 사용할 데이터, 크롤링이 완료된 후 크롤링된 데이터의 콜렉션을 전송할 위치 및 기타 크롤링 관리 옵션에 대해 사용자에게 알려주는 파일입니다.
    -   `man` - 제품 내 매뉴얼 페이지 크롤러 문서입니다.

## 이 릴리스의 알려진 제한사항
{: #dc-limitations}

-   올바르지 않거나 누락된 URL을 사용하여 파일 시스템 커넥터를 실행 중일 때 Data Crawler가 정지될 수 있습니다.
-   모든 화이트리스트 URL 또는 RegExe가 단일 RegEx 표현식에 포함되도록 `crawler.conf` 파일의 `urls_to_filter` 값을 구성하십시오. 자세한 정보는 [크롤링 옵션 구성](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-crawl-options)을 참조하십시오.
-   `--config -c` 옵션에 전달된 구성 파일에 대한 경로는 완전한 경로여야 합니다. 즉, 상대 형식 `config/crawler.conf` 또는 `./crawler.conf` 또는 절대 경로 `/path/to/config/crawler.conf`로 되어 있어야 합니다. `crawler.conf`만 지정하는 것은 `orchestration_service.conf` 파일이 `crawler.conf` 파일에서 `include`를 사용하여 참조되는 대신 인라인되어 있어야만 가능합니다.
