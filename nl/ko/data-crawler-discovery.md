---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-03"

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

# Data Crawler 구성

저장소를 크롤링하기 위해 Data Crawler를 설정하려면 `crawler.conf` 파일에 적절한 입력 어댑터를 지정한 후 입력 어댑터 구성 파일에 있는 저장소 특정 정보를 구성해야 합니다.
{: shortdesc}

{{site.data.keyword.discoveryshort}} 도구 또는 API를 사용하여 Box, Salesforce 및 Microsoft SharePoint Online 데이터 소스를 크롤링할 수 있습니다. 자세한 정보는 [데이터 소스에 연결](/docs/services/discovery/connect.html)을 참조하십시오.
{: tip}

이 단계에 나열된 변경사항을 수행하기 전에 `{installation_directory}/share/examples/config` 디렉토리의 컨텐츠를 시스템의 작업 디렉토리(예: `/home/config`)로 복사하여 작업 디렉토리를 작성했는지 확인하십시오.

**중요:** 제공된 구성 예제 파일을 바로 수정하지 마십시오. 이 예제 파일을 복사한 후 편집하십시오. 제공된 예제 파일을 바로 편집하는 경우 Data Crawler를 업그레이드할 때 구성이 겹쳐쓰이거나 Data Crawler를 설치 제거할 때 구성이 제거될 수 있습니다.

**참고:** `config` 디렉토리에 있는 파일(예: `config/crawler.conf`)과 관련된 이 안내서의 참조는 작업 디렉토리(설치된 `{installation_directory}/share/examples/config` 디렉토리가 아님)의 해당 파일을 참조합니다.

지정된 값은 `config/crawler.conf`의 기본값이며 파일 시스템 커넥터를 구성합니다.

1.  텍스트 편집기에서 `config/crawler.conf` 파일을 여십시오.

    -   이전에 수정한 `.conf`(예: `connectors/filesystem.conf`)에 `crawl_config_file` 옵션을 설정하십시오.
    -   이전에 수정한 `-seed.conf`(예: `seeds/filesystem-seed.conf`)에 `crawl_seed_file` 옵션을 설정하십시오.
    -   다음과 같이 {{site.data.keyword.discoveryshort}} 서비스에 대해 `output_adapter` `class` 및 `config` 옵션을 설정하십시오.

        ```
    class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

        config - "discovery_service"

        discovery_service {
          include "discovery/discovery_service.conf"
        }
        ```
        {: codeblock}

    이 파일에는 사용자의 환경에 적합하도록 설정할 수 있는 기타 선택적 설정이 있습니다. 값 설정에 대한 자세한 정보는 [크롤링 옵션 구성](/docs/services/discovery/data-crawler-discovery.html#configuring-crawl-options), [입력 어댑터 구성](/docs/services/discovery/data-crawler-discovery.html#input-adapter), [출력 어댑터 구성](/docs/services/discovery/data-crawler-discovery.html#output-adapter) 및 [추가 크롤링 관리 옵션](/docs/services/discovery/data-crawler-discovery.html#additional-crawl-management-options)을 참조하십시오.

1.  텍스트 편집기에서 `discovery/discovery_service.conf` 파일을 여십시오. 이전에 {{site.data.keyword.Bluemix}}에서 작성했던 {{site.data.keyword.discoveryshort}} 서비스에 특정한 다음 값을 수정하십시오.

    -   `environment_id` - {{site.data.keyword.discoveryshort}} 서비스 환경 ID입니다.
    -   `collection_id` - {{site.data.keyword.discoveryshort}} 서비스 콜렉션 ID입니다.
    -   `configuration_id` - {{site.data.keyword.discoveryshort}} 서비스 구성 ID입니다.
    -   `configuration` - 이 `discovery_service.conf` 파일의 전체 경로 위치입니다(예: `/home/config/discovery/discovery_service.conf`).
    -   `username` - {{site.data.keyword.discoveryshort}} 서비스에 대한 사용자 이름 인증 정보입니다.
    -   `password` - {{site.data.keyword.discoveryshort}} 서비스에 대한 비밀번호 인증 정보입니다.

    이 파일에는 사용자의 환경에 적합하도록 설정할 수 있는 기타 선택적 설정이 있습니다. 값 설정에 대한 자세한 정보는 [서비스 옵션 구성](/docs/services/discovery/data-crawler-discovery.html#configuring-service-options)을 참조하십시오.

1.  이러한 파일을 수정하면 데이터를 크롤링할 준비가 됩니다. 계속하려면 [데이터 저장소 크롤링](/docs/services/discovery/data-crawler-run.html#crawling-your-data-repository)으로 진행하십시오.

## 크롤링 옵션 구성
{: #configuring-crawl-options}

`config/crawler.conf` 파일에는 Data Crawler에게 크롤링을 위해 사용할 파일(입력 어댑터), 크롤링이 완료된 후 크롤링된 파일의 콜렉션을 전송할 위치(출력 어댑터) 및 기타 크롤링 관리 옵션을 알려주는 정보가 포함되어 있습니다.

**참고:** 언급된 경우를 제외하고 모든 파일 경로는 `config` 디렉토리에 상대적입니다.

최신 정보를 포함하는, `crawler.conf` 파일에 대한 제품 내 매뉴얼에 액세스하려면 크롤러 설치 디렉토리에서 `man crawler.conf` 명령을 입력하십시오.
{: tip}

이 파일에 설정할 수 있는 옵션은 다음과 같습니다.

### 입력 어댑터
{: #input-adapter}

-   **`class`** - 내부 사용 전용으로, Data Crawler 입력 어댑터 클래스를 정의합니다. 기본값은 `com.ibm.watson.crawler.connectorframeworkinputadapter.Crawl`입니다.
-   **`config`** - 내부 사용 전용으로, 커넥터 프레임워크 구성을 정의합니다. 선택된 입력 어댑터로 전달하기 위한 이 블록 내의 기본 구성 키는 `connector_framework`입니다.

    커넥터 프레임워크는 사용자와 데이터 간의 대화를 허용합니다. 엔터프라이즈 내의 내부 데이터이거나 웹 또는 클라우드의 외부 데이터일 수 있습니다. 커넥터는 다수의 다른 데이터 소스에 대한 액세스를 허용하지만 실제로 연결은 크롤링 프로세스로 제어됩니다.

    **중요:** 커넥터 프레임워크 입력 어댑터로 검색되는 데이터는 로컬로 캐시됩니다. 암호화되어 저장되지 않습니다. 기본적으로, 데이터는 재부팅 시 지워져야 하는 임시 디렉토리에 캐시되며 크롤러 명령을 실행한 사용자만 읽을 수 있어야 합니다.

    커넥터 프레임워크가 자체적으로 정리하기 전에 사라지는 경우 이 디렉토리가 크롤러보다 오래 남아있을 수 있습니다. 캐시된 데이터의 위치를 신중하게 고려하십시오. 암호화된 파일 시스템에 캐시된 데이터를 저장할 수 있으나 이로 인해 성능에 미치는 영향을 알고 있어야 합니다. 사용자만이 크롤링에 대한 속도 및 보안 간의 적절한 균형을 결정할 수 있습니다.
-   **`crawl_config_file`** - 크롤링에 사용할 구성 파일입니다. 기본값은 `connectors/filesystem.conf`입니다.
-   **`crawl_seed_file`** - 크롤링에 사용할 크롤링 seed 파일입니다. 기본값은 `seeds/filesystem-seed.conf`입니다.
-   **`id_vcrypt_file`** - 크롤러를 통해 데이터 암호화에 사용되는 키 파일입니다. 크롤러와 함께 포함된 기본 키는 `id_vcrypt`입니다. 새 `id_vcrypt` 파일을 생성해야 하는 경우 `bin` 폴더의 vcrypt 스크립트를 사용하십시오.
-   **`crawler_temp_dir`** - 커넥터 로그에 대한 크롤러 임시 폴더입니다. 기본값 `tmp`가 제공됩니다. 아직 존재하지 않으면 `tmp` 폴더가 현재 작업 디렉토리에 작성됩니다.
-   **`extra_jars_dir`** - 추가 JAR의 디렉토리를 커넥터 프레임워크 classpath에 추가합니다.

    **참고:** 커넥터 프레임워크 `lib/java` 디렉토리에 상대적입니다.

    -   SharePoint 커넥터를 사용할 때 이 값은 `oakland`여야 합니다.
    -   데이터베이스 커넥터를 사용할 때 이 값은 `database`여야 합니다.

    기타 커넥터를 사용할 때 이 값을 비어 있는 상태로 둘 수 있습니다(예: empty string "").

-   **`urls_to_filter`** - 크롤링하지 않아야 하는 URL 블랙리스트입니다(정규식 양식). Data Crawler는 제공된 정규식과 일치하는 URL은 크롤링하지 않습니다.

    `domain list`에는 크롤링할 수 없는 도메인이 포함됩니다. 필요한 경우 추가하십시오.

    `filetype list`에는 오케스트레이션 서비스가 지원되지 않는 파일 확장자가 포함됩니다.

    정규식에서 지원되는 파일 유형을 제거하십시오.

    seed URL 도메인이 필터로 허용되는지 확인하십시오. `allow everything` 동작을 위해서는 비어 있는 필터를 사용하십시오.

    seed URL이 필터로 제외되지 않거나 크롤러가 정지하는지 확인하십시오.

-   **`max_text_size`** - 커넥터 프레임워크에서 문서를 디스크에 쓰기 전에 설정될 수 있는 문서의 최대 크기(바이트)입니다. 더 큰 수로 조정하면 디스크에 쓰여진 문서의 크기가 줄어들지만 메모리 요구사항이 늘어납니다. 기본값은 `1048576`입니다.
-   **`extra_vm_params`** - 커넥터 프레임워크를 실행하기 위해 사용된 명령에 추가 Java 매개변수를 추가할 수 있습니다.

-   **`bootstrap_logging`** - 고급 디버깅에만 유용한 커넥터 프레임워크 시작 로그를 씁니다. 가능한 값은 `true` 또는 `false`입니다. `crawler_temp_dir`에 로그 파일을 씁니다.

-   **`read-timeout`** - 크롤러가 커넥터 프레임워크에서 응답을 기다릴 시간(초)을 설정합니다. 기본값은 5초입니다.

### 출력 어댑터
{: #output-adapter}

-   **`class`** - Data Crawler 출력 어댑터 클래스를 정의합니다.
-   **`config`** - 출력 어댑터로 전달할 구성 키를 정의합니다. 문자열은 이 구성 오브젝트 내의 키와 일치해야 합니다. 다음 코드 예제에서,

    ```
    class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

    config - "discovery_service"

    discovery_service {
        include "discovery/discovery_service.conf"
      }
    ```
    {: codeblock}

    구성 키는 `discovery_service`입니다.

`class` 매개변수 및 `config` 키를 지정하여 출력 어댑터를 선택해야 합니다.

-   **{{site.data.keyword.discoveryshort}} 서비스 출력 어댑터** - {{site.data.keyword.discoveryfull}} 서비스에 크롤링된 문서를 업로드합니다. 다음과 같이 `class` 매개변수 및 `config` 키를 설정하여 이 어댑터를 선택하십시오.

```
class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

config - "discovery_service"

discovery_service {
            include "discovery/discovery_service.conf"
          }
```
{: codeblock}

-   **테스트 출력 어댑터** - 테스트 출력 어댑터는 지정된 위치의 디스크에 크롤링된 파일의 표시를 씁니다. 다음과 같이 `class` 매개변수 및 `config` 키를 설정하여 이 어댑터를 선택하십시오.

    추가 매개변수인 `output_directory`는 크롤링된 데이터의 표시가 쓰여져야 할 디렉토리를 선택합니다.

```
class - "com.ibm.watson.crawler.testoutputadapter.TestOutputAdapter"

config - "test"

output_directory - "/tmp/crawler-test-output"`
```
{: codeblock}

-   **`retry`** - 출력 어댑터를 푸시하는 데 실패한 경우 재시도에 대한 옵션을 지정합니다.

    -   `max_attempts` - 최대 재시도의 수입니다. 기본값은 `10`입니다.
    -   `delay` - 재시도 간의 최소 지연 시간(초)입니다. 기본값은 `2`입니다.
    -   `exponent_base` - 실패한 각 시도 중에 지연 시간의 연장을 결정하는 요인입니다. 기본값은 `2`입니다.

    공식은 다음과 같습니다.

        **`d(nth_retry) - delay * (exponent_base ^ nth_retry)`**

    예를 들어, 기본 설정이 1초의 지연과 2의 지수 밑수로 구성되면 두 번의 재시도(세 번째 시도)가 발생합니다. 즉, 1초 대신 2초가 지연되고 그 다음 4초가 지연됩니다.

        `d(0) - 1 * (2 ^ 0)` - 1 second
        `d(1) - 1 * (2 ^ 1)` - 2 seconds
        `d(2) - 1 * (2 ^ 2)` - 4 seconds

    따라서 기본 설정을 통해 제출이 최대 열 번 시도되며, 최대 1022초(17분 약간 초과)까지 대기합니다. 동시에 여러 번의 다시 제출이 실행되지 않도록 추가된 추가 시간이 있으므로 이 시간은 대략적인 시간입니다. 이 "대략적인" 시간이 최대 10%이므로 이전 예제의 마지막 시도에서 최대 7.7초 지연될 수 있습니다. 대기 시간에는 서비스에 연결하거나 데이터를 업로드하거나 응답을 기다리는 데 소요된 시간은 포함되지 않습니다.

    여기서 `output_timeout` 값은 대기 시간보다 우선합니다. 총 재시도 대기 시간이 해당 설정을 초과하면 제출이 재시도되더라도 실패하게 됩니다.
    {: tip}

### 추가 크롤링 관리 옵션
{: #additional-crawl-management-options}

-   **`full_node_debugging`** - 디버깅 모드를 활성화합니다. 가능한 값은 `true` 또는 `false`입니다.

    **중요:** 이를 통해 크롤링된 모든 문서의 전체 데이터가 로그에 저장됩니다.   

-   **`logging.log4j.configuration_file`*** - 로깅에 사용하는 구성 파일입니다. 샘플 `crawler.conf` 파일에서 이 옵션은 `logging.log4j`에 정의되고 기본값은 `log4j_custom.properties`입니다. `.properties` 또는 `.conf` 파일의 사용 여부에 상관 없이 이 옵션은 유사하게 정의되어야 합니다.   
-   **`shutdown_timeout`** - 애플리케이션을 종료하기 전에 제한시간 값(분)을 지정합니다. 기본값은 `10`입니다.   
-   **`output_limit`** - 크롤러가 동시에 출력 어댑터로의 전송을 시도하는 인덱싱 가능한 최대 항목 수입니다. 이는 작업을 수행하는 데 사용 가능한 코어의 수로 좀 더 제한될 수 있습니다. 즉, 특정 시점에서 리턴을 기다리는 출력 어댑터에 전송된 인덱싱 가능한 항목 수가 "x"보다 적음을 의미합니다. 기본값은 `10`입니다.   
-   **`input_limit`** - 동시에 입력 어댑터에서 요청될 수 있는 URL의 수를 제한합니다. 기본값은 `30`입니다.   
-   **`output_timeout`** - Data Crawler가 출력 어댑터에 대한 요청을 포기한 후 추가 처리를 허용하기 위해 출력 어댑터 큐에서 항목을 제거하기 전의 시간(초)입니다. 기본값은 `1200`입니다.

    제한조건이 여기에 정의된 제한사항과 관련될 수 있으므로 출력 어댑터로 지정된 제한조건을 고려해야 합니다. 정의된 `output_limit`는 출력 어댑터에 즉시 전송될 수 있는 인덱싱 가능한 오브젝트의 수에만 관련됩니다. 인덱싱 가능한 오브젝트가 출력 어댑터로 전송되면 `output_timeout` 변수로 정의된 것과 같이 "작동 중"입니다. 수신하는 입력 수만큼 처리할 수 없도록 출력 어댑터에는 자체 제한이 있을 수 있습니다. 예를 들어, 오케스트레이션 출력 어댑터에는 서비스에 대한 HTTP 연결에 적용 가능한 연결 풀이 있을 수 있습니다. 예를 들어, 기본값이 8인 경우 `output_limit`를 8보다 큰 수로 설정하면 실행될 순서를 기다리는 작동 중인 프로세스가 제공됩니다. 그런 다음 제한시간 초과가 발생할 수 있습니다.   
-   **`num_threads`** - 동시에 실행할 수 있는 최대 병렬 스레드의 수입니다. 이 값은 병렬 스레드의 수를 직접적으로 지정하는 정수 또는 사용 가능한 프로세서 수의 곱셈 인수를 지정하는 `"xNUM"` 형식의 문자열(예: `"x1.5"`) 중 하나입니다. 기본값은 `"30"`입니다.

## 서비스 옵션 구성
{: #configuring-service-options}

{{site.data.keyword.discoveryshort}} 서비스는 {{site.data.keyword.discoveryfull}} 서비스를 사용할 때 크롤링된 파일을 관리하는 방법을 크롤러에게 알려줍니다.

최신 정보를 포함하는, `discovery-service.conf` 파일에 대한 제품 내 매뉴얼에 액세스하려면 크롤러 설치 디렉토리에서 다음 명령을 입력하십시오.

  ```bash
  man discovery_service.conf
  ```
  {: pre}
{: tip}

기본 옵션은 `config/discovery/discovery_service.conf` 파일을 열고 유스 케이스에 특정한 다음 값을 지정하여 직접 변경할 수 있습니다.

-   **`http_timeout`** - 문서 읽기/인덱싱 오퍼레이션에 대한 제한시간(초)입니다. 기본값은 `125`입니다.
-   **`proxy_host_port`** - (선택사항) 방화벽 뒤에서 Data Crawler를 실행할 때 Data Crawler가 {{site.data.keyword.discoveryshort}} 서비스와 대화할 수 있도록 프록시 호스트 이름 및 프록시 포트 번호를 설정해야 할 수 있습니다. 이 옵션의 기본값은 비어 있는 문자열이며 이를 변경해야 하는 경우 `"<host>:<port>"` 양식으로 구성된 값이어야 합니다.
-   **`concurrent_upload_connection_limit`** - 문서를 업로드하기 위해 허용된 동시 연결의 수입니다. 기본값은 `2`입니다.

    **참고:** 오케스트레이션 서비스 출력 어댑터를 사용하는 경우 이 수는 크롤링 옵션을 구성할 때 설정된 `output_limit` 이상이어야 합니다.   

-   **`base_url`** - 크롤링된 문서가 전송된 URL입니다. {{site.data.keyword.discoveryshort}} 서비스의 현재 릴리스의 경우 이 값은 `https://gateway.watsonplatform.net/discovery/api`입니다.   
-   **`environment_id`** - 기본 URL에서 크롤링된 문서 콜렉션의 위치입니다.   
-   **`collection_id`** - {{site.data.keyword.discoveryshort}} 서비스에서 설정한 문서 콜렉션의 이름입니다.
-   **`api_version`** - 내부 사용 전용입니다. 마지막으로 API 버전이 변경된 날짜입니다.   
-   **`configuration_id`** - {{site.data.keyword.discoveryshort}} 서비스에서 사용하는 구성 파일의 파일 이름입니다.
-   **`username`** - 크롤링된 문서 콜렉션의 위치를 인증하는 사용자 이름입니다.   
-   **`password`** - 크롤링된 문서 콜렉션의 위치를 인증하는 비밀번호입니다.

{{site.data.keyword.discoveryshort}} 서비스 출력 어댑터는 {{site.data.keyword.IBM}}이 사용자를 좀 더 이해하고 사용자에게 더 나은 서비스를 제공하기 위해 통계를 전송할 수 있습니다. `send_stats` 변수에 설정될 수 있는 옵션은 다음과 같습니다.

-   **`jvm`** - Data Crawler를 실행하는 데 사용된 JVM(Java Virtual Machine)에서 보고한 대로 전송된 JVM에는 Java 공급업체 및 버전이 포함됩니다. 값은 `true` 또는 `false`입니다. 기본값은 `true`입니다.
-   **`os`** - Data Crawler를 실행하는 데 사용된 JVM(Java Virtual Machine)에서 보고한 대로 전송된 운영 체제(0S) 통계에는 OS 이름, 버전 및 아키텍처가 포함됩니다. 값은 `true` 또는 `false`입니다. 기본값은 `true`입니다.
