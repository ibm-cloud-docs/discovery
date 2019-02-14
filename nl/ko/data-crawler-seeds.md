---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-25"

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

# 커넥터 및 seed 옵션 구성

데이터를 크롤링하는 경우 크롤러는 먼저 데이터 저장소의 유형(커넥터)과 사용자가 지정한 시작 위치(seed)를 식별하여 정보의 다운로드를 시작합니다.
{: shortdesc}

**중요:** Data Crawler를 사용할 때 데이터 저장소 보안 설정은 무시됩니다.

seed는 크롤러의 시작점이며 커넥터로 식별된 리소스에서 데이터를 검색하기 위해 Data Crawler에서 사용합니다. 일반적으로 seed는 URL을 구성하여 프로토콜 기반 리소스(예: 파일 공유, SMB 공유, 데이터베이스 및 여러 프로토콜에서 액세스할 수 있는 기타 데이터 저장소)에 액세스합니다. 또한 seed URL마다 기능이 다릅니다. 또한 seed가 저장소에 특정하게 지정되어 고객 관계 관리(CRM) 시스템, 제품 수명 주기(PLC) 시스템, 컨텐츠 관리 시스템(CMS), 클라우드 기반 애플리케이션 및 웹 데이터베이스 애플리케이션과 같은 특정 써드파티 애플리케이션의 크롤링을 사용으로 설정할 수도 있습니다.

데이터를 올바르게 크롤링하려면 크롤러가 적절하게 구성되어 데이터 저장소를 읽는지 확인해야 합니다. Data Crawler는 다음 저장소에서 데이터 콜렉션을 지원하기 위해 커넥터를 제공합니다.

-   [파일 시스템](/docs/services/discovery/data-crawler-seeds.html#configuring-filesystem-crawl-options)
-   [JDBC를 통한 데이터베이스](/docs/services/discovery/data-crawler-seeds.html#configuring-database-crawl-options)
-   [CMIS(Content Management Interoperability Services)](/docs/services/discovery/data-crawler-seeds.html#configuring-cmis-crawl-options)
-   [SMB(Server Message Block), CIFS(Common Internet Filesystem) 또는 Samba 파일 시스템](/docs/services/discovery/data-crawler-seeds.html#configuring-smbcifssamba-crawl-options)
-   [SharePoint 및 SharePoint Online](/docs/services/discovery/data-crawler-seeds.html#configuring-sharepoint-crawl-options)
-   [Box](/docs/services/discovery/data-crawler-seeds.html#configuring-box-crawl-options)

커넥터 구성 템플리트도 제공되며, 이를 통해 사용자가 커넥터를 사용자 정의할 수 있습니다.

커넥터를 구성하려면 다음을 수행하십시오.

1.  텍스트 편집기에서 사용자가 연결 중인 저장소에 해당하는 `connectors` 디렉토리에 있는 파일(예를 들어, `filesystem.conf`는 파일 시스템 커넥터에 대한 구성 파일임)을 여십시오.

1.  저장소에 적합한 값을 수정하십시오.

    -   [파일 시스템](/docs/services/discovery/data-crawler-seeds.html#filesystem-crawl-options)
    -   [JDBC를 통한 데이터베이스](/docs/services/discovery/data-crawler-seeds.html#database-crawl-seed)
    -   [CMIS(Content Management Interoperability Services)](/docs/services/discovery/data-crawler-seeds.html#cmis-crawl-options)
    -   [SMB(Server Message Block), CIFS(Common Internet Filesystem) 또는 Samba 파일 시스템](/docs/services/discovery/data-crawler-seeds.html#smb-cifs-samba-crawl-options)
    -   [SharePoint 및 SharePoint Online](/docs/services/discovery/data-crawler-seeds.html#sharepoint-crawl-options)
    -   [Box](/docs/services/discovery/data-crawler-seeds.html#box-crawl-options)
1.  파일을 저장한 후 닫으십시오.
1.  텍스트 편집기에서 사용자가 연결 중인 저장소에 해당하는 `connectors/seeds` 디렉토리에 있는 `-seed.conf` 파일(예를 들어, `filesystem-seed.conf`는 파일 시스템 커넥터에 대한 seed(연결되는 위치) 구성 파일임)을 여십시오.
1.  [{{site.data.keyword.discoveryshort}}에 연결하도록 Data Crawler 구성](/docs/services/discovery/data-crawler-discovery.html)으로 계속 진행하십시오.

최신 정보를 포함하는, 커넥터 및 seed 구성 파일에 대한 제품 내 매뉴얼에 액세스하려면 크롤러 설치 디렉토리에서 다음 명령을 입력하십시오.
-   커넥터 구성 옵션의 경우:
    ```bash
    man crawler-options.conf
    ```
    {: pre}
-   크롤링 seed 구성 옵션의 경우:
    ```bash
    man crawler-seed.conf
    ```
    {: pre}


## 파일 시스템 크롤링 옵션 구성
{: #filesystem-crawl-options}

파일 시스템 커넥터를 통해 Data Crawler 설치에 로컬인 파일을 크롤링할 수 있습니다.

### 파일 시스템 커넥터 구성

다음은 파일 시스템 커넥터를 사용하는 데 필요한 기본 구성 옵션입니다. 이 값을 설정하려면 `config/connectors/filesystem.conf` 파일을 열고 유스 케이스에 특정한 다음 값을 수정하십시오.

-   **`protocol`** - 크롤링에 사용되는 커넥터 프로토콜의 이름입니다. 이 커넥터에 `sdk-fs`를 사용하십시오.
-   **`collection`** - 이 속성은 임시 파일의 압축을 푸는 데 사용됩니다. 기본값은 `crawler-fs`입니다.
-   **`logging-config`** - 로깅 옵션을 구성하기 위해 사용되는 파일을 지정합니다. `log4j` XML 문자열로 형식화되어야 합니다.
-   **`classname`** - 커넥터에 대한 Java 클래스 이름입니다. 이 커넥터를 사용하기 위한 값은 `plugin:filesystem.plugin@filesystem`이어야 합니다.

### 파일 시스템 크롤링 seed 구성

다음 값은 파일 시스템 크롤링 seed 파일에 대해 구성될 수 있습니다. 이 값을 설정하려면 `config/seeds/filesystem-seed.conf` 파일을 열고 유스 케이스에 특정한 다음 값을 지정하십시오.

-   **`url`** - 크롤링할 파일 및 폴더의 목록이며, 줄 바꾸기로 구분됩니다. UNIX 사용자는 `/usr/local/`과 같은 경로를 사용할 수 있습니다.

    **참고:** URL은 `sdk-fs://`로 시작되어야 합니다. 예를 들어, `/home/watson/mydocs`를 크롤링하려면 이 URL의 값은 `sdk-fs:///home/watson/mydocs`가 되어야 합니다. 세 번째 `/`가 필수입니다!

    Linux, UNIX 및 UNIX와 유사한 컴퓨터 시스템에서 사용하는 파일 시스템은 데이터를 포함하지 않으므로 크롤링할 수는 없으나 디바이스 또는 I/O 액세스 지점으로 작동하는 특수한 유형의 파일(예: 블록 및 문자 디바이스 노드와 이름 지정된 파이프를 나타내는 파일)을 포함할 수 있습니다. 이러한 파일에 대한 크롤링을 시도하면 크롤링 중에 오류가 생성됩니다. 이 오류가 발생하지 않도록 하려면  UNIX 또는 UNIX와 유사한 파일 시스템의 최상위 레벨 크롤링에서 `/dev` 디렉토리를 제외해야 합니다. 크롤링 중인 시스템에 존재하는 경우 일시적인 파일 및 시스템 정보가 포함된 임시 시스템 디렉토리(예: `/proc`, `/sys` 및 `/tmp`)도 제외해야 합니다.   **`hops`** - 내부 사용 전용입니다.   **`default-allow`** - 내부 사용 전용입니다.
    {: tip}

## 데이터베이스 크롤링 옵션 구성

데이터베이스 커넥터를 통해 사용자 정의 SQL 명령을 실행하고 행(레코드)당 하나의 문서 및 열(필드)당 하나의 컨텐츠 요소를 작성하여 데이터베이스를 크롤링할 수 있습니다. 고유 키로 사용할 열 및 각 레코드의 마지막 수정 날짜를 나타내는 시간소인이 포함된 열을 지정할 수 있습니다. 커넥터는 지정된 데이터베이스에서 모든 레코드를 검색하고 SQL문에 있는 특정 테이블, 결합 등으로 제한될 수도 있습니다.

데이터베이스 커넥터를 통해 다음 데이터베이스를 크롤링할 수 있습니다.

-   {{site.data.keyword.IBM}} DB2
-   MySQL
-   Oracle PostgreSQL
-   Microsoft SQL Server
-   Sybase
-   기타 SQL 호환 데이터베이스(JDBC 3.0 호환 드라이버를 통해)

커넥터가 지정된 데이터베이스와 테이블에서 모든 레코드를 검색합니다.

***JDBC 드라이버*** - 데이터베이스 커넥터는 Oracle JDBC(Java Database Connectivity) 드라이버 버전 1.5와 함께 제공됩니다. Data Crawler와 함께 제공된 모든 써드파티 JDBC 드라이버는 Data Crawler 설치의 `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` 디렉토리에 위치하며, 필요에 따라 추가, 제거 및 수정할 수 있습니다. 또한 `crawler.conf` 파일의 `extra_jars_dir` 설정을 사용하여 다른 위치를 지정할 수도 있습니다.

***DB2 JDBC 드라이버*** - Data Crawler는 라이센싱 문제로 인해 DB2용 JDBC 드라이버와 함께 제공되지 않습니다. 그러나 DB2 설치를 크롤링할 수 있도록 JDBC 지원을 설치한 모든 DB2 설치에는 Data Crawler에 필요한 JAR 파일이 포함됩니다. DB2 인스턴스를 크롤링하려면 데이터베이스 커넥터가 이 파일을 사용할 수 있도록 Data Crawler 설치의 적절한 디렉토리에 이를 복사해야 합니다. DB2 설치를 크롤링하기 위해 Data Crawler를 사용으로 설정하려면 DB2 설치 시 `db2jcc.jar` 및 라이센스(일반적으로, `db2jcc_license_cu.jar`) JAR 파일을 찾고 해당 파일을 Data Crawler 설치 디렉토리의 `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` 하위 디렉토리에 복사하거나 `crawler.conf` 파일의 `extra_jars_dir` 설정을 사용하여 다른 위치를 지정할 수 있습니다.

***MySQL JDBC 드라이버*** - MySQL용 JDBC 드라이버가 제품의 일부로 제공된 경우 Data Crawler는 라이센싱 문제로 인해 MySQL용 JDBC 드라이버와 함께 제공되지 않습니다. 그러나 MySQL JDBC 드라이버가 포함된 JAR 파일을 다운로드하고 해당 JAR 파일을 Data Crawler 설치에 통합하는 것은 다음과 같이 매우 간단합니다.

1.  웹 브라우저를 사용하여 MySQL 다운로드 사이트에 방문하고 사용할 아카이브 형식에 대한 소스 및 2진 다운로드 링크를 찾으십시오(일반적으로 Microsoft Windows 시스템용 zip 또는 Linux 시스템용 gzip된 tarball). 해당 링크를 클릭하여 다운로드 프로세스를 시작하십시오. 등록이 필요할 수 있습니다.
1.  적절한 압축 풀기 archive-file-name 또는 tar zxf archive-file-name 명령을 사용하여 다운로드하는 아카이브 파일의 유형 및 이름에 따라 해당 아카이브의 컨텐츠를 추출하십시오.
1.  아카이브 파일에서 추출된 디렉토리로 변경하고 이 디렉토리에서 Data Crawler 설치 디렉토리의 `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` 하위 디렉토리로 JAR 파일을 복사하거나, `crawler.conf` 파일의 `extra_jars_dir` 설정을 사용하여 다른 위치에 지정할 수 있습니다.

### 데이터베이스 커넥터 구성

다음은 데이터베이스 커넥터를 사용하는 데 필요한 기본 구성 옵션입니다. 이 값을 설정하려면 config/connectors/database.conf 파일을 열고 유스 케이스에 특정한 다음 값을 수정하십시오.

-   **`protocol`** - 크롤링에 사용되는 커넥터 프로토콜의 이름입니다. 이 커넥터의 값은 액세스할 데이터베이스 시스템을 기반으로 합니다.
-   **`collection`** - 이 속성은 임시 파일의 압축을 푸는 데 사용됩니다.
-   **`classname`** - 커넥터에 대한 Java 클래스 이름입니다. 이 커넥터를 사용하기 위한 값은 `plugin:database.plugin@database`여야 합니다.
-   **`logging-config`** - 로깅 옵션을 구성하기 위해 사용되는 파일을 지정합니다. `log4j` XML 문자열로 형식화되어야 합니다.

### 데이터베이스 크롤링 seed 구성
{: #database-crawl-seed}

다음 값은 데이터베이스 크롤링 seed 파일에 대해 구성될 수 있습니다. 이 값을 설정하려면 `config/seeds/database-seed.conf` 파일을 열고 유스 케이스에 특정한 다음 값을 지정하십시오.

-   **`url`** - 검색할 테이블 또는 보기의 URL입니다. 사용자 정의 SQL 데이터베이스 seed URL을 정의합니다. 구조는 다음과 같습니다.

    -   `database-system://host:port/database?[per=num]&[sql=SQL]`

    seed URL을 테스트하면 큐에 삽입된 URL이 모두 표시됩니다. 예를 들어, 200개의 레코드가 포함된 데이터베이스의 다음 URL을 테스트합니다.
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?per=100&sql=select%20*%20from%20vessel&`

    큐에 삽입된 다음 URL이 표시됩니다.
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=0&`
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=100&`
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=200&`

    다음 URL을 테스트하는 동안 43행에서 검색된 데이터가 표시됩니다.
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?per-1&key-val=43`
-   **`hops`** - 내부 사용 전용입니다.
-   **`default-allow`** - 내부 사용 전용입니다.
-   **`user-password`** - 데이터베이스 시스템에 대한 인증 정보입니다. 사용자 이름 및 비밀번호는 `:`으로 구분되어야 하고, 비밀번호는 Data Crawler와 함께 제공된 vcrypt 프로그램을 사용하여 암호화되어야 합니다. 예를 들면, `username:[[vcrypt/3]]passwordstring`입니다.
-   **`max-data-size`** - 문서의 최대 데이터 크기입니다. 한 번에 로드될 가장 큰 메모리의 블록입니다. 컴퓨터에 충분한 메모리가 있는 경우에만 이 한계를 늘리십시오.
-   **`filter-exact-duplicates`** - 내부 사용 전용입니다.
-   **`timeout`** - 내부 사용 전용입니다.
-   **`jdbc-class`**(익스텐더 옵션) - 지정된 경우 이 문자열은 `(other)`가 데이터베이스 시스템으로 선택된 경우 커넥터에서 사용되는 JDBC 클래스를 대체합니다.
-   **`connection-string`**(익스텐더 옵션) - 지정된 경우 이 문자열은 자동으로 생성된 JDBC 연결 문자열을 대체합니다. 이를 통해 데이터베이스 연결에 대한 좀 더 세부적인 구성(예: 로드 밸런싱 또는 SSL 연결)을 제공할 수 있습니다. 예를 들면, `jdbc:netezza://127.0.0.1:5480/databasename`입니다.
-   **`save-frequency-for-resume`**(익스텐더 옵션) - 크롤링을 재개하거나 부분적인 새로 고치기를 수행하기 위해 열 또는 연관된 레이블의 이름을 지정합니다. seed는 크롤링을 계속할 때 정기적으로 이 열의 이름을 저장하고 데이터베이스의 마지막 행이 크롤링되면 다시 이를 저장합니다. 크롤링을 재개하거나 새로 고치기를 수행하는 경우 크롤링은 이 필드에 대해 저장된 값으로 식별된 행부터 시작됩니다.

## CMIS 크롤링 옵션 구성
{: #cmis-crawl-options}

CMIS(Content Management Interoperability Services) 커넥터를 통해 CMIS 사용 CMS(컨텐츠 관리 시스템) 저장소(예: Alfresco, Documentum 또는 {{site.data.keyword.IBM}} Content Manager)를 크롤링하고 이 저장소에 포함된 데이터를 인덱싱할 수 있습니다.

### CMIS 커넥터 구성

다음은 CMIS 커넥터를 사용하는 데 필요한 기본 구성 옵션입니다. 이 값을 설정하려면 `config/connectors/cmis.conf` 파일을 열고 유스 케이스에 특정한 다음 값을 지정하십시오.

-   **`protocol`** - 크롤링에 사용되는 커넥터 프로토콜의 이름입니다. 이 커넥터를 사용하기 위한 값은 `cmis`여야 합니다.
-   **`collection`** - 이 속성은 임시 파일의 압축을 푸는 데 사용됩니다.
-   **`dns`** - 사용되지 않는 옵션입니다.
-   **`classname`** - 커넥터에 대한 Java 클래스 이름입니다. 이 커넥터에 `plugin:cmis-v1.1.plugin@connector`를 사용하십시오.
-   **`logging-config`** - 로깅 옵션을 구성하기 위해 사용되는 파일을 지정합니다. `log4j` XML 문자열로 형식화되어야 합니다.
-   **`endpoint`** - CMIS 호환 저장소의 서비스 엔드포인트 URL입니다. 예를 들어, SharePoint의 URL 구조는 다음과 같습니다.

    -   AtomPub 바인딩의 경우: `http://yourserver/_vti_bin/cmis/rest?getRepositories`
    -   WebServices 바인딩의 경우: `http://yourserver/_vti_bin/cmissoapwsdl.aspx`
-   **`username`** - 컨텐츠에 액세스하는 데 사용되는 CMIS 저장소 사용자의 사용자 이름입니다. 이 사용자는 크롤링하고 인덱싱할 모든 대상 폴더 및 문서에 대한 액세스 권한이 있어야 합니다.
-   **`password`** - 컨텐츠에 액세스하는 데 사용되는 CMIS 저장소의 비밀번호입니다. 비밀번호는 암호화되지 않고 일반 텍스트로 제공되어야 합니다.
-   **`repositoryid`** - 특정 저장소에 대한 컨텐츠에 액세스하는 데 사용되는 CMIS 저장소의 ID입니다.
-   **`bindingtype`** - CMIS 저장소에 연결하는 데 사용되는 바인딩의 유형을 식별합니다. 값은 AtomPub 또는 WebServices입니다.
-   **`authentication`** - CMIS 호환 저장소에 연결하는 중에 사용할 인증 메커니즘의 유형(기본 HTTP 인증, NTLM 또는 WS-Security(사용자 이름 토큰))을 식별합니다.
-   **`enable-acl`** - 크롤링된 데이터에 대한 ACL 검색을 사용합니다. 사용자가 이 콜렉션에서 문서의 보안에 대해 신경쓰지 않는 경우, 이 옵션을 사용 안함으로 설정하면 문서에 대한 이 정보를 요청하지 않고 이 정보를 검색 및 인코딩하지 않아야 성능이 향상됩니다. 값은 true 또는 false입니다.
-   **`user-agent`** - 문서를 크롤링할 때 서버에 전송되는 헤더입니다.
-   **`method`** - 매개변수가 전달되는 메소드(GET 또는 POST)입니다.
-   **`url-logging`** - 크롤링된 URL이 로깅되는 범위입니다. 가능한 값은 다음과 같습니다.

    -   `full-logging` - URL에 대한 모든 정보를 로깅합니다.
    -   `refined-logging` - 커넥터가 올바르게 작동하고 크롤러 로그를 찾는 데 필요한 정보만 로깅합니다. 이는 기본값입니다.
    -   `minimal-logging` - 커넥터가 올바르게 작동하는 데 필요한 최소한의 정보만 로깅합니다.

    이 옵션을 `minimal-logging`으로 설정하면 로깅된 데이터의 양을 최소화하는 데 관련된 더 작은 I/O로 인해 로그 크기가 줄어들고 성능이 일부 향상됩니다.
-   **`ssl-version`** - SSL의 버전을 지정하여 HTTPS 연결에 사용합니다. 기본적으로 사용 가능한 가장 강력한 프로토콜이 사용됩니다.

### CMIS 크롤링 seed 구성

다음 값은 CMIS 크롤링 seed 파일에 대해 구성될 수 있습니다. 이 값을 설정하려면 `config/seeds/cmis-seed.conf` 파일을 열고 유스 케이스에 특정한 다음 값을 수정하십시오.

-   **`url`** - 크롤링의 시작점으로 사용할 CMIS 저장소의 폴더 URL입니다(예: `cmis://alfresco.test.com:8080/alfresco/cmisatom?folderToProcess-workspace://SpacesStore/guid`).

    루트 폴더에서 크롤링하려면 `cmis://alfresco.test.com:8080/alfresco/cmisatom?folderToProcess-`와 같은 URL을 제공해야 합니다.
-   **`at`** - 사용되지 않는 옵션입니다.
-   **`default-allow`** - 내부 사용 전용입니다.

## SMB/CIFS/Samba 크롤링 옵션 구성
{: #smb-cifs-samba-crawl-options}

Samba 커넥터를 통해 SMB(Server Message Block) 및 CIFS(Common Internet filesystem) 파일 공유를 크롤링할 수 있습니다. 이 파일 공유 유형은 Windows 네트워크에 일반적인 유형이며 오픈 소스 프로젝트 Samba를 통해서도 제공됩니다.

### Samba 커넥터 구성

다음은 Samba 커넥터를 사용하는 데 필요한 기본 구성 옵션입니다. 이 값을 설정하려면 `config/connectors/samba.conf` 파일을 열고 유스 케이스에 특정한 다음 값을 지정하십시오.

-   **`protocol`** - 크롤링에 사용되는 커넥터 프로토콜의 이름입니다. 이 커넥터를 사용하기 위한 값은 smb입니다.
-   **`collection`** - 이 속성은 임시 파일의 압축을 푸는 데 사용됩니다.
-   **`classname`** - 커넥터에 대한 Java 클래스 이름입니다. 이 커넥터를 사용하기 위한 값은 `plugin:smb.plugin@connector`여야 합니다.
-   **`logging-config`** - 로깅 옵션을 구성하기 위해 사용되는 파일을 지정합니다. `log4j` XML 문자열로 형식화되어야 합니다.
-   **`username`** - 인증할 Samba 사용자 이름입니다. 제공되는 경우 도메인 및 비밀번호도 제공해야 합니다. 제공되지 않는 경우 게스트 계정이 사용됩니다.
-   **`password`** - 인증할 Samba 비밀번호입니다. 사용자 이름이 제공되는 경우 이는 필수입니다. Data Crawler와 함께 제공된 vcrypt 프로그램을 사용하여 비밀번호를 암호화해야 합니다.
-   **`archive`** - Samba 커넥터를 통해 아카이브 파일 내에서 압축된 파일을 크롤링하고 인덱싱할 수 있습니다. 값은 true 또는 false이며, 기본값은 false입니다.
-   **`max-policies-per-handle`** - 단일 RPC 처리를 위해 열 수 있는 최대 LSA(Local Security Authority) 정책 수를 지정합니다. 이 정책은 다양한 조건에서 특정 시스템을 조회하거나 수정하는 데 필요한 액세스 권한을 정의합니다. 이 옵션의 기본값은 255입니다.
-   **`crawl-fs-metadata`** - 이 옵션을 설정하면 Data Crawler가 파일에 대해 사용 가능한 파일 시스템 메타데이터(작성 날짜, 마지막 수정된 날짜, 파일 속성 등)가 포함된 VXML 문서를 추가합니다..
-   **`enable-arc-connector`** - 사용되지 않는 옵션입니다.
-   **`disable-indexes`** - 사용 안함으로 설정할 인덱스의 목록이며, 줄 바꾸기로 구분됩니다. 이를 통해 크롤링이 더 빠르게 수행될 수 있습니다. 예를 들면, 다음과 같습니다.

    -   `disable-url-index`
    -   `disable-error-state-index`
    -   `disable-crawl-time-index`
-   **`exact-duplicates-hash-size`** - 정확히 일치하는 중복을 해결하기 위해 사용된 해시 테이블의 크기를 설정합니다. 이 수를 수정할 때 유의하십시오. 선택하는 값이 주요 값이 되어야 합니다. 더 큰 수를 선택하면 빠른 검색이 가능하지만 더 많은 메모리를 사용하는 반면 더 작은 수를 선택하면 크롤링의 속도가 저하되지만 더 적은 메모리를 사용합니다.
-   **`user-agent`** - 사용되지 않는 옵션입니다.
-   **`timeout`** - 사용되지 않는 옵션입니다.
-   **`n-concurrent-requests`** - 단일 IP 주소에 병렬로 전송되는 요청 수입니다. 기본값은 `1`입니다.
-   **`enqueue-persistence`** - 사용되지 않는 옵션입니다.

### Samba 크롤링 seed 구성

다음 값은 Samba 크롤링 seed 파일에 대해 구성될 수 있습니다. 이 값을 설정하려면 `config/seeds/samba-seed.conf` 파일을 열고 유스 케이스에 특정한 다음 값을 지정하십시오.

-   **`url`** - 크롤링할 고유 목록이며, 줄 바꾸기로 구분됩니다. 예를 들면, 다음과 같습니다.

    ```
    smb://share.test.com/office
    smb://share.test.com/cash/money/change
    smb://share.test.com/C$/Program Files
    ```
    {: codeblock}

-   **`hops`** - 내부 사용 전용입니다.
-   **`default-allow`** - 내부 사용 전용입니다.

## SharePoint 크롤링 옵션 구성
{: #sharepoint-crawl-options}

**중요:** SharePoint 커넥터에는 Microsoft SharePoint Server 2007(MOSS 2007), SharePoint Server 2010, SharePoint Server 2013 또는 SharePoint Online이 필요합니다.

SharePoint 커넥터를 통해 SharePoint 오브젝트를 크롤링하고 여기에 포함된 정보를 인덱싱할 수 있습니다. 문서, 사용자 프로파일, 사이트 콜렉션, 블로그, 목록 항목, 멤버십 목록, 디렉토리 페이지 등과 같은 오브젝트는 연관된 메타데이터를 사용하여 인덱싱될 수 있습니다. 목록 항목 및 문서의 경우 인덱스에 첨부 파일이 포함될 수 있습니다.

SharePoint 커넥터는 특정 유형(블로그, 문서, 사용자 프로파일 등)에 관계 없이 모든 SharePoint 오브젝트의 `noindex` 속성을 준수합니다. 결과마다 하나의 문서가 리턴됩니다.
{: tip}

**중요:** SharePoint 사이트를 크롤링하는 데 사용하는 SharePoint 계정에는 최소한 전체 읽기 액세스 권한이 있어야 합니다.

### SharePoint 커넥터 구성

다음은 SharePoint 커넥터를 사용하는 데 필요한 기본 구성 옵션입니다. 이 값을 설정하려면 `config/connectors/sharepoint.conf` 파일을 열고 유스 케이스에 특정한 다음 값을 수정하십시오.

-   **`protocol`** - 크롤링에 사용되는 커넥터 프로토콜의 이름입니다. 이 커넥터를 사용하기 위한 값은 `io-sp`입니다.
-   **`collection`** - 이 속성은 임시 파일의 압축을 푸는 데 사용됩니다.
-   **`classname`** - 커넥터에 대한 Java 클래스 이름입니다. 이 커넥터에 `plugin:io-sharepoint.plugin@connector`를 사용하십시오.
-   **`logging-config`** - 로깅 옵션을 구성하기 위해 사용되는 파일을 지정합니다. `log4j` XML 문자열로 형식화되어야 합니다.
-   **`seed-url-type`** - 제공된 seed URL이 가리키는 SharePoint 오브젝트 유형 즉, 사이트 콜렉션 또는 웹 애플리케이션(가상 서버라고도 함)을 식별합니다.

    -   `Site Collections` - seed URL 유형이 Site Collections로 설정되는 경우 URL로 참조된 사이트 콜렉션의 하위만 크롤링됩니다.
    -   `Web Applications` - seed URL 유형이 Web Applications로 설정된 경우 각 URL로 참조된 웹 애플리케이션에 속하는 모든 사이트 콜렉션(및 하위)이 크롤링됩니다.
-   **`auth-type`** - SharePoint 서버에 접속할 때 사용하는 인증 메커니즘으로, `BASIC`, `NTLM2`, `KERBEROS` 또는 `CBA`입니다. 기본 인증 유형은 `NTLM2`입니다.
-   **`spUser`** - 컨텐츠에 액세스하는 데 사용되는 SharePoint 사용자의 사용자 이름입니다. 이 사용자는 크롤링하고 인덱싱할 모든 대상 사이트 및 목록에 대한 액세스 권한이 있어야 하며, 연관된 권한을 검색하고 분석할 수 있어야 합니다. `MYDOMAIN\\Administrator`와 같은 도메인 이름으로 입력하는 것이 좋습니다.
-   **`spPassword`** - 컨텐츠에 액세스하는 데 사용되는 SharePoint 사용자의 비밀번호입니다. Data Crawler와 함께 제공된 vcrypt 프로그램을 사용하여 비밀번호를 암호화해야 합니다.
-   **`cba-sts`** - 크롤링 사용자를 인증하려고 하는 STS(Security Token Service) 엔드포인트의 URL입니다. ADFS를 사용한 SharePoint 온프레미스의 경우 ADFS 엔드포인트여야 합니다. 인증 유형이 CBA(Claims Based Authentication)로 설정된 경우 이 필드는 필수입니다.
-   **`cba-realm`** - STS에서 보안 토큰을 요청할 때 사용할 릴레이하는 당사자 신뢰 ID입니다. "AppliesTo" 값 또는 "Realm"으로 알려져 있기도 합니다. SharePoint Online의 경우 SharePoint Online 인스턴스의 루트에 대한 URL(예: `https://mycompany.sharepoint.com`)이어야 합니다. ADFS의 경우 SharePoint와 ADFS 간에 릴레이하는 당사자 신뢰에 대한 ID 값(예: `"urn:SHAREPOINT:adfs"`)입니다.
-   **`everyone-group`** - 지정된 경우 이 그룹 이름은 모두에게 액세스 권한을 제공해야 할 때 ACL에서 사용됩니다. 이 필드는 사용자 프로파일 크롤링이 사용 가능할 때 필수입니다.

    **참고:** 보안은 검색 및 순위 지정 서비스에서 고려되지 않습니다.

-   **`user-profile-master-url`** - 커넥터가 사용자 프로파일에 대한 링크를 빌드하는 데 사용하는 기본 URL입니다. 사용자 프로파일의 표시 양식을 가리키도록 구성되어야 합니다. `%FIRST_SEED%` 토큰이 발생하면 첫 번째 seed URL로 대체됩니다. 사용자 프로파일 크롤링이 사용으로 설정된 경우 필수입니다.
-   **`urls`** - 크롤링할 SharePoint 웹 애플리케이션 또는 사이트 콜렉션의 HTTP URL 목록이며, 줄 바꾸기로 구분됩니다.
-   **`ehcache-config`** - 사용되지 않는 옵션입니다.
-   **`method`** - 매개변수가 전달되는 메소드(`GET` 또는 `POST`)입니다.
-   **`cache-types`** - 사용되지 않는 옵션입니다.
-   **`cache-size`** - 사용되지 않는 옵션입니다.
-   **`enable-acl`** - SharePoint 사용자 프로파일의 크롤링을 사용합니다. 값은 `true` 또는 `false`이며, 기본값은 `false`입니다.

### SharePoint 크롤링 seed 구성

다음 추가 값은 SharePoint 크롤링 seed 파일에 대해 구성될 수 있습니다. 이 값을 설정하려면 `config/seeds/sharepoint-seed.conf` 파일을 열고 유스 케이스에 특정한 다음 값을 지정하십시오.

-   **`url`** - 크롤링할 SharePoint 웹 애플리케이션 또는 사이트 콜렉션의 URL 목록이며, 줄 바꾸기로 구분됩니다. 예:

    ```
    io-sp://a.com
    io-sp://b.com:83/site
    io-sp://c.com/site2
    ```
    {: codeblock}

    이 사이트의 하위 사이트도 크롤링됩니다(기타 크롤링 규칙으로 제외되지 않는 경우).

-   **`filter-url`** - 크롤링할 SharePoint 웹 애플리케이션 또는 사이트 콜렉션의 URL 목록이며, 줄 바꾸기로 구분됩니다. 예:

    ```
    http://a.com
    http://b.com:83/site
    http://c.com/site2
    ```
    {: codeblock}

-   **`hops`** - 내부 사용 전용입니다.
-   **`n-concurrent-requests`** - 내부 사용 전용입니다.
-   **`delay`** - 내부 사용 전용입니다.
-   **`default-allow`** - 내부 사용 전용입니다.
-   **`seed-protocol`** - 사이트 콜렉션의 하위에 대한 seed 프로토콜을 설정합니다. 사이트 콜렉션의 프로토콜이 SSL, HTTP 또는 HTTPS인 경우 필수입니다. 이 값은 사이트 콜렉션의 프로토콜과 동일하게 설정되어야 합니다.

## Box 크롤링 옵션 구성

Box 커넥터를 통해 엔터프라이즈 Box 인스턴스를 크롤링하고 여기에 포함된 정보를 인덱싱할 수 있습니다.

### Box 커넥터 구성

다음은 Box 커넥터를 사용하는 데 필요한 기본 구성 옵션입니다. 이 값을 설정하려면 `config/connectors/box.conf` 파일을 열고 유스 케이스에 특정한 다음 값을 수정하십시오.

-   **`protocol`** - 크롤링에 사용되는 커넥터 프로토콜의 이름입니다. 이 커넥터를 사용하기 위한 값은 `box`입니다.
-   **`classname`** - 커넥터에 대한 Java 클래스 이름입니다. 이 커넥터에 `plugin:box.plugin@connector`를 사용하십시오.
-   **`logging-config`** - 로깅 옵션을 구성하기 위해 사용되는 파일을 지정합니다. `log4j` XML 문자열로 형식화되어야 합니다.
-   **`box-crawl-seed-url`** - Box의 기본 URL입니다. 이 커넥터의 값은 `box://app.box.com/`입니다.

    다른 유형의 URL을 크롤링할 수 있습니다. 예를 들면, 다음과 같습니다.

    -   전체 엔터프라이즈를 크롤링할 경우: `box://app.box.com/`
    -   특정 폴더를 크롤링할 경우: `box://app.box.com/user/USER_ID/folder/FOLDER_ID/FolderName`
    -   특정 사용자를 크롤링할 경우: `box://app.box.com/user/USER_ID`
-   **`client-id`** - Box 애플리케이션을 작성할 때 Box에서 제공된 클라이언트 ID를 입력하십시오.
-   **`client-secret`** - Box 애플리케이션을 작성할 때 Box에서 제공된 클라이언트 시크릿을 입력하십시오.
-   **`path-to-private-key`** - Box와의 통신을 위해 생성된 개인-공용 키 쌍의 일부인 개인 키의 위치로, 로컬 파일 시스템에 있습니다.
-   **`kid`** - 공용 키 ID를 지정하십시오. Box와의 통신을 위해 설정된 개인-공용 키 쌍의 나머지 절반입니다.
-   **`enterprise-id`** - 애플리케이션의 권한이 부여된 엔터프라이즈입니다. 엔터프라이즈 ID는 Box 관리자 콘솔의 기본 페이지에 나열됩니다.
-   **`enable-acl`** - 내부 사용 전용입니다. 크롤링된 데이터에 대한 ACL 검색을 사용합니다.
-   **`user-agent`** - 문서를 크롤링할 때 서버에 전송되는 헤더입니다.
-   **`method`** - 매개변수가 전달되는 메소드(`GET` 또는 `POST`)입니다.
-   **`url-logging`** - 크롤링된 URL이 로깅되는 범위입니다. 가능한 값은 다음과 같습니다.

    -   `full-logging` - URL에 대한 모든 정보를 로깅합니다.
    -   `refined-logging` - 커넥터가 올바르게 작동하고 크롤러 로그를 찾는 데 필요한 정보만 로깅합니다. 이는 기본값입니다.
    -   `minimal-logging` - 커넥터가 올바르게 작동하는 데 필요한 최소한의 정보만 로깅합니다.

    이 옵션을 `minimal-logging`으로 설정하면 로깅된 데이터의 양을 최소화하는 데 관련된 더 작은 I/O로 인해 로그 크기가 줄어들고 성능이 일부 향상됩니다.
-   **`ssl-version`** - SSL의 버전을 지정하여 HTTPS 연결에 사용합니다. 기본적으로 사용 가능한 가장 강력한 프로토콜이 사용됩니다.

### Box 크롤링 seed 구성
{: #box-crawl-options}

다음 추가 값은 Box 크롤링 seed 파일에 대해 구성될 수 있습니다. 이 값을 설정하려면 `config/seeds/box-seed.conf` 파일을 열고 유스 케이스에 특정한 다음 값을 지정하십시오.

-   **`url`** - 크롤링의 시작점으로 사용할 URL입니다. 기본값은 `box://app.box.com/`입니다.
-   **`default-allow`** - 내부 사용 전용입니다.

## 제한사항

Box 커넥터에는 일부 제한사항이 있습니다.

-   파일의 주석 또는 태스크가 검색되지 않습니다.
-   Notes 컨텐츠 본문이 JSON으로 검색됩니다. Notes 데이터의 추가 변환이 필요할 수 있습니다.
-   Test-It을 통해 개별 문서를 검색할 수 없습니다. Test-It을 통해 seed URL, 폴더 URL 및 사용자 URL만 검색할 수 있습니다.
