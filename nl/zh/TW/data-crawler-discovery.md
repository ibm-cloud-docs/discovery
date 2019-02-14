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

# 配置資料搜索器

若要設定「資料搜索器」來搜索儲存庫，您必須在 `crawler.conf` 檔案中指定適當的輸入配接器，然後在輸入配接器配置檔中配置儲存庫特有的資訊。
{: shortdesc}

您可以使用 {{site.data.keyword.discoveryshort}} 工具或 API 來搜索 Box、Salesforce 及 Microsoft SharePoint Online 資料來源。如需相關資訊，請參閱[連接至資料來源](/docs/services/discovery/connect.html)。
{: tip}

在進行這些步驟所列出的變更之前，請確定您已建立工作目錄，方法是將 `{installation_directory}/share/examples/config` 目錄的內容複製到系統上的工作目錄，例如 `/home/config`。

**重要事項：**請勿直接修改所提供的配置範例檔。請複製後再進行編輯。如果您直接編輯範例檔，則在升級「資料搜索器」時可能會改寫您的配置，或在解除安裝時可能會將其移除。

**附註：**本手冊中提及 `config` 目錄中的檔案（例如 `config/crawler.conf`）時，是指您工作目錄中的該檔案，而「非」已安裝之 `{installation_directory}/share/examples/config` 目錄中的檔案。

指定的值是 `config/crawler.conf` 中的預設值，這些值會配置「檔案系統」連接器：

1.  在文字編輯器中開啟 `config/crawler.conf` 檔案。

    -   將 `crawl_config_file` 選項設為您先前修改的 `.conf`，例如：`connectors/filesystem.conf`。
    -   將 `crawl_seed_file` 選項設為您先前修改的 `-seed.conf`，例如：`seeds/filesystem-seed.conf`。
    -   如下所示，針對 {{site.data.keyword.discoveryshort}} 服務設定 `output_adapter` 的 `class` 和 `config` 選項：

        ```
        class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

        

        config - "discovery_service"

        

        discovery_service {
          include "discovery/discovery_service.conf"
        }
        ```
        {: codeblock}

    此檔案中還有其他選用性的設定，可依適合您環境的方式加以設定。如需關於設定這些值的詳細資訊，請參閱：[配置搜索選項](/docs/services/discovery/data-crawler-discovery.html#configuring-crawl-options)、[配置輸入配接器](/docs/services/discovery/data-crawler-discovery.html#input-adapter)、[配置輸出配接器](/docs/services/discovery/data-crawler-discovery.html#output-adapter)及[其他搜索管理選項](/docs/services/discovery/data-crawler-discovery.html#additional-crawl-management-options)。

1.  在文字編輯器中開啟 `discovery/discovery_service.conf` 檔案。修改您先前在 {{site.data.keyword.Bluemix}} 上建立之 {{site.data.keyword.discoveryshort}} 服務特有的下列值：

    -   `environment_id` - {{site.data.keyword.discoveryshort}} 服務環境 ID。
    -   `collection_id` - {{site.data.keyword.discoveryshort}} 服務集合 ID。
    -   `configuration_id` - {{site.data.keyword.discoveryshort}} 服務配置 ID。
    -   `configuration` - 這個 `discovery_service.conf` 檔案的完整路徑位置，例如 `/home/config/discovery/discovery_service.conf`。
    -   `username` - {{site.data.keyword.discoveryshort}} 服務的使用者名稱認證。
    -   `password` - {{site.data.keyword.discoveryshort}} 服務的密碼認證。

    此檔案中還有其他選用性的設定，可依適合您環境的方式加以設定。如需關於設定這些值的詳細資訊，請參閱[配置服務選項](/docs/services/discovery/data-crawler-discovery.html#configuring-service-options)。

1.  修改這些檔案之後，您就可以開始搜索資料。請前往[搜索資料儲存庫](/docs/services/discovery/data-crawler-run.html#crawling-your-data-repository)以繼續進行。

## 配置搜索選項
{: #configuring-crawl-options}

`config/crawler.conf` 檔案包含的資訊會告知「資料搜索器」要用於其搜索的檔案（輸入配接器）、在搜索完成之後所搜索檔案的集合要傳送至何處（輸出配接器），以及其他搜索管理選項。

**附註：**除非另行註明，否則所有檔案路徑都是相對於 `config` 目錄。

若要存取 `crawler.conf` 檔案的產品內手冊及最新資訊，請從搜索器安裝目錄鍵入下列指令：`man crawler.conf`
{: tip}

可以在此檔案中設定的選項如下：

### 輸入配接器
{: #input-adapter}

-   **`class`** - 僅供內部使用；定義「資料搜索器」輸入配接器類別。預設值為：`com.ibm.watson.crawler.connectorframeworkinputadapter.Crawl`
-   **`config`** - 僅供內部使用；定義連接器架構配置。在此區塊內要傳遞給所選輸入配接器的預設配置索引鍵為：`connector_framework`

    連接器架構可讓您與資料交談。它可以是在企業中的內部資料，或者也可以是 Web 上或雲端中的外部資料。連接器允許存取許多不同的資料來源，而連接實際上是由搜索程序控制。

    **重要事項：**「連接器架構輸入配接器」所擷取的資料會快取存在本端。不會以加密格式儲存它。依預設，該資料會快取至重新開機時應該清除的暫存目錄中，而且應該只可供執行搜索器指令的使用者讀取。

如果連接器架構會在可以清理自己之前就離開，此目錄的存留時間有可能會比搜索器還長。請仔細考量快取資料的位置。您可以將它放在已加密的檔案系統中，但請注意這樣做的效能影響。只有您才能決定搜索速度與安全之間的適當平衡。
-   **`crawl_config_file`** - 用於搜索的配置檔。預設值為：`connectors/filesystem.conf`
-   **`crawl_seed_file`** - 要用於搜索的搜索種子檔。預設值為：`seeds/filesystem-seed.conf`
-   **`id_vcrypt_file`** - 用於搜索器資料加密的金鑰檔；搜索器包含的預設金鑰為 `id_vcrypt`。如果您需要產生新的 `id_vcrypt` 檔案，請使用 `bin` 資料夾中的 vcrypt Script。
-   **`crawler_temp_dir`** - 用於連接器日誌的搜索器暫存資料夾。會提供預設值 `tmp`。如果它還不存在，則將在現行工作目錄中建立 `tmp` 資料夾。
-   **`extra_jars_dir`** - 在連接器架構類別路徑中新增額外 JAR 的目錄。

    **附註：**相對於連接器架構 `lib/java` 目錄。

    -   使用 SharePoint 連接器時，此值必須為 `oakland`。
    -   使用「資料庫」連接器時，此值必須為 `database`。

    使用其他連接器時，您可以將此值保留為空白（亦即，空字串 ""）。

-   **`urls_to_filter`** - 不應搜索的 URL 黑名單，以正規表示式的格式表示。「資料搜索器」不會搜索符合所提供之任何正規表示式的 URL。

    `domain list` 包含無法搜索的網域。請視需要新增。

    `filetype list` 包含「編排服務」不支援的副檔名。

    從正規表示式移除任何支援的檔案類型。

    請確保過濾器允許您的種子 URL 網域。對 `allow everything` 行為使用空的過濾器。

    請確保您的種子 URL 不會被過濾器排除，否則搜索器可能會當掉。

-   **`max_text_size­`** - 文件由「連接器架構」寫入磁碟之前可以具備的大小上限（以位元組為單位）。調高此值會減少寫入至磁碟的文件數量，但會增加記憶體需求。預設值為 `1048576`
-   **`extra_vm_params`** - 可讓您將額外的 Java 參數新增至用來啟動「連接器架構」的指令。

-   **`bootstrap_logging`** - 寫入連接器架構啟動日誌；僅適用於進階除錯。可能值為 `true` 或 `false`。日誌檔將寫入至 `crawler_temp_dir`

-   **`read-timeout`** - 設定搜索器將等待連接器架構回應的時間（以秒為單位）。預設值為 5 秒。

### 輸出配接器
{: #output-adapter}

-   **`class`** - 定義「資料搜索器」輸出配接器類別。
-   **`config`** - 定義要傳遞至輸出配接器的配置索引鍵。字串必須對應於此配置物件內的索引鍵。在下列程式碼範例中：

    ```
        class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

        

    config - "discovery_service"

        

    discovery_service {
        include "discovery/discovery_service.conf"
      }
    ```
    {: codeblock}

    配置索引鍵為 `discovery_service`。

您必須透過指定 `class` 參數和 `config` 索引鍵來選取輸出配接器。

-   **{{site.data.keyword.discoveryshort}} 服務輸出配接器** - 將所搜索的文件上傳至 {{site.data.keyword.discoveryfull}} 服務。如下所示設定 `class` 參數和 `config` 索引鍵，以選取此配接器。

```
class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

config - "discovery_service"

discovery_service {
            include "discovery/discovery_service.conf"
  }
```
{: codeblock}

-   **測試輸出配接器** - 「測試輸出配接器」會將所搜索檔案的代表寫入至磁碟中的指定位置。如下所示設定 `class` 參數和 `config` 索引鍵，以選取此配接器。

    另一參數 `output_directory` 會選取所搜索資料的代表應該寫入至的目錄。

```
class - "com.ibm.watson.crawler.testoutputadapter.TestOutputAdapter"

config - "test"

output_directory - "/tmp/crawler-test-output"`
```
{: codeblock}

-   **`retry`** - 指定若嘗試推送至輸出配接器失敗，用於重試的選項。

    -   `max_attempts` - 重試次數上限。預設值是 `10`
    -   `delay` - 兩次嘗試之間的最短延遲量（以秒為單位）。預設值是 `2`
    -   `exponent_base` - 決定每次失敗嘗試延遲時間增加的因數。預設值是 `2`

    公式如下：

        **`d(nth_retry) - delay * (exponent_base ^ nth_retry)`**

    例如，延遲為 1 秒且指數基數為 2 的預設值，將導致第二次重試（第三次嘗試）延遲 2 秒而不是 1 秒，下一次則會延遲 4 秒。

        `d(0) - 1 * (2 ^ 0)` - 1 second
        `d(1) - 1 * (2 ^ 1)` - 2 seconds
        `d(2) - 1 * (2 ^ 2)` - 4 seconds

    因此，使用預設值時，會最多嘗試提交 10 次，並最多等待大約 1022 秒 - 比 17 分鐘再多一點。此時間為大約值，因為有增加額外的時間，以避免同時執行多個重新提交作業。這個「模糊」時間最長為 10%，因此前一個範例的最後一次重試最多可能延遲 7.7 秒。等待時間不包括連接至服務、上傳資料或等待回應等所耗費的時間。

    `output_timeout` 值的優先順序高於這裡的等待時間：如果總重試等待時間超過該設定，則即使已重試，提交也會失敗。
    {: tip}

### 其他搜索管理選項
{: #additional-crawl-management-options}

-   **`full_node_debugging`** - 啟動除錯模式；可能的值為 `true` 或 `false`。

    **重要事項：**這會將已搜索的每一份文件的完整資料放在日誌中。   

-   **`logging.log4j.configuration_file`*** - 要用於記載的配置檔。在範例 `crawler.conf` 檔案中，此選項是定義在 `logging.log4j`，並且其預設值是 `log4j_custom.properties`。不論是使用 `.properties<­/MD:CODE> 檔或 `.conf` 檔，必須以類似方式定義此選項。   
-   **`shutdown_timeout`** - 指定關閉應用程式之前的逾時值（分鐘）。預設值是 `10`。   
-   **`output_limit`** - 搜索器將嘗試同時傳送至輸出配接器的可檢索項目數量上限。這可以藉由可用來執行作業的核心數進一步限制。它指出任何指定時候都不會有超過 "x" 個可檢索項目傳送至輸出配接器以等待傳回。預設值是 `10`。   
-   **`input_limit`** - 限制一次可向輸入配接器要求的 URL 數目。預設值為 `30`。   
-   **`output_timeout`** - 在「資料搜索器」放棄對輸出配接器的要求，然後從輸出配接器佇列移除項目以容許更多處理之前的時間量（以秒為單位）。預設值是 `1200`。

應該考量輸出配接器所加諸的限制，因為那些限制可能與這裡定義的限制相關。所定義的 `output_limit` 僅與一次可傳送至輸出配接器的可檢索物件數相關。一旦將可檢索物件傳送至輸出配接器後，它便「開始計時」，如 `output_timeout` 變數所定義。輸出配接器本身有可能具有節流控制，使得它無法處理所接收的諸多輸入。例如，編排輸出配接器可能有連線儲存區，可針對服務的 HTTP 連線進行配置。例如，如果它預設為 8，且如果您將 `output_limit` 設定為大於 8 的數字，則您會有開始計時的程序，在等候輪到它執行。接著您可能會遇到逾時。   
-   **`num_threads`** - 可一次執行的平行執行緒數目。此值可以是整數（其直接指定平行執行緒的數目），也可以是格式為 `"xNUM"` 的字串（其指定可用處理器數量的乘數），例如 `"x1.5"`。預設值為 `"30"`

## 配置服務選項
{: #configuring-service-options}

{{site.data.keyword.discoveryshort}} 服務會告知搜索器在使用 {{site.data.keyword.discoveryfull}} 服務時如何管理搜索的檔案。

若要存取 `discovery-service.conf` 檔案的產品內手冊及最新資訊，請從搜索器安裝目錄鍵入下列指令：

  ```bash
  man discovery_service.conf
  ```
  {: pre}
{: tip}

您可以開啟 `config/discovery/discovery_service.conf` 檔案，並指定您的使用案例特有的下列值，以直接變更預設選項：

-   **`http_timeout`** - 文件讀取/索引作業的逾時（以秒為單位）；預設值是 `125`。
-   **`proxy_host_port`** -（選用）在防火牆後面執行資料搜索器時，您可能需要設定 Proxy 主機名稱及 Proxy 埠號，以便讓資料搜索器與 {{site.data.keyword.discoveryshort}} 服務交談。此選項的預設值是空字串，如果您需要變更它，該值的格式應該為 `"<host>:<port>"`.
-   **`concurrent_upload_connection_limit`** - 上傳文件容許的同時連線數。預設值為 `2`。

    **附註：**使用「編排服務輸出配接器」時，此數字應大於或等於配置搜索選項時設定的 `output_limit`。   

-   **`base_url`** - 所搜索文件將傳送至的 URL。以 {{site.data.keyword.discoveryshort}} 服務的現行版本而言，該值為 `https://gateway.watsonplatform.net/discovery/api`。   
-   **`environment_id`** - 所搜索文件集合在基礎 URL 的位置。   
-   **`collection_id`** - 您在 {{site.data.keyword.discoveryshort}} 服務中設定的文件集合名稱。
-   **`api_version`** - 僅供內部使用。前次 API 版本變更的日期。   
-   **`configuration_id`** - {{site.data.keyword.discoveryshort}} 服務所用配置檔的檔名。
-   **`username`** - 用來向所搜索文件集合位置進行鑑別的使用者名稱。   
-   **`password`** - 用來向所搜索文件集合位置進行鑑別的密碼。

「{{site.data.keyword.discoveryshort}} 服務輸出配接器」可傳送統計資料，讓 {{site.data.keyword.IBM}} 能夠更充分地瞭解及服務其使用者。您可以為 `send_stats` 變數設定下列選項：

-   **`jvm`** - 傳送的 Java 虛擬機器 (JVM) 統計資料包括 Java 供應商及版本，如用來執行資料搜索器的 JVM 所報告。值為 `true` 或 `false`。預設值為 `true`。
-   **`os`** - 傳送的作業系統 (OS) 統計資料包括作業系統名稱、版本及架構，如用來執行資料搜索器的 JVM 所報告。值為 `true` 或 `false`。預設值為 `true`。
