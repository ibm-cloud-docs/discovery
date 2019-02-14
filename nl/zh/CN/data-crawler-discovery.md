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

# 配置 Data Crawler

要设置 Data Crawler 来搜寻存储库，必须在 `crawler.conf` 文件中指定相应的输入适配器，然后在输入适配器配置文件中配置特定于存储库的信息。
{: shortdesc}

您可以使用 {{site.data.keyword.discoveryshort}} 工具或 API 来搜寻 Box、Salesforce 和 Microsoft SharePoint Online 数据源。请参阅[连接到数据源](/docs/services/discovery/connect.html)以获取更多信息。
{: tip}

在执行以下步骤中列出的更改之前，请确保已通过将 `{installation_directory}/share/examples/config` 目录的内容复制到系统上的工作目录（例如 `/home/config`）来创建工作目录。

**重要信息：**不要直接修改提供的配置示例文件。请复制这些文件，然后对其进行编辑。如果直接编辑示例文件，那么在升级 Data Crawler 时可能会覆盖您的配置，或者在卸载 Data Crawler 时可能会除去您的配置。

**注：**本指南中提到 `config` 目录中文件（例如 `config/crawler.conf`）均指的是工作目录中的相应文件，而不是位于 `{installation_directory}/share/examples/config` 安装目录中的文件。

指定的值是 `config/crawler.conf` 中的缺省值，请配置文件系统连接器：

1.  在文本编辑器中打开 `config/crawler.conf` 文件。

    -   将 `crawl_config_file` 选项设置为先前修改的 `.conf`，例如：`connectors/filesystem.conf`。
    -   将 `crawl_seed_file` 选项设置为先前修改的 `-seed.conf`，例如：`seeds/filesystem-seed.conf`。
    -   设置 {{site.data.keyword.discoveryshort}} 服务的 `output_adapter` `class` 和 `config` 选项，如下所示：

        ```
        class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

        

        config - "discovery_service"

        

        discovery_service {
          include "discovery/discovery_service.conf"
        }
        ```
        {: codeblock}

    此文件中还有其他可选设置，可以根据您的环境进行相应设置；请参阅：[配置搜寻选项](/docs/services/discovery/data-crawler-discovery.html#configuring-crawl-options)、[配置输入适配器](/docs/services/discovery/data-crawler-discovery.html#input-adapter)、[配置输出适配器](/docs/services/discovery/data-crawler-discovery.html#output-adapter)和[其他搜寻管理选项](/docs/services/discovery/data-crawler-discovery.html#additional-crawl-management-options)，以获取有关设置这些值的详细信息。

1.  在文本编辑器中打开 `discovery/discovery_service.conf` 文件。针对您先前在 {{site.data.keyword.Bluemix}} 上创建的 {{site.data.keyword.discoveryshort}} 服务修改以下值：

    -   `environment_id` - {{site.data.keyword.discoveryshort}} 服务环境标识。
    -   `collection_id` - {{site.data.keyword.discoveryshort}} 服务集合标识。
    -   `configuration_id` - {{site.data.keyword.discoveryshort}} 服务配置标识。
    -   `configuration` - 此 `discovery_service.conf` 文件的完整路径位置，例如 `/home/config/discovery/discovery_service.conf`。
    -   `username` - {{site.data.keyword.discoveryshort}} 服务的用户名凭证。
    -   `password` - {{site.data.keyword.discoveryshort}} 服务的密码凭证。

    此文件中还有其他可选设置，可以根据您的环境进行相应设置。请参阅[配置服务选项](/docs/services/discovery/data-crawler-discovery.html#configuring-service-options)，以获取有关设置这些值的详细信息。

1.  修改这些文件后，即可随时搜寻数据。接着[搜寻数据存储库](/docs/services/discovery/data-crawler-run.html#crawling-your-data-repository)以继续。

## 配置搜寻选项
{: #configuring-crawl-options}

`config/crawler.conf` 文件包含的信息将告知 Data Crawler 哪些文件要用于搜寻（输入适配器）、搜寻完成后将搜寻到的文件集合发送到何处（输出适配器），以及其他搜寻管理选项。

**注：**所有文件路径都相对于 `config` 目录，除非另有说明。

要访问 `crawler.conf` 文件的产品内联机帮助并获取最新信息，请从搜寻器安装目录输入以下命令：`man crawler.conf`
{: tip}

可以在此文件中设置的选项包括：

### 输入适配器
{: #input-adapter}

-   **`class`** - 仅供内部使用；定义 Data Crawler 输入适配器类。缺省值为：`com.ibm.watson.crawler.connectorframeworkinputadapter.Crawl`
-   **`config`** - 仅供内部使用；定义 Connector Framework 配置。此块中要传递到所选输入适配器的缺省配置键为：`connector_framework`

    通过 Connector Framework，您可以与数据进行对话。这可以是企业的内部数据，也可以是 Web 或云上的外部数据。可通过连接器来访问大量不同的数据源，但连接实际由搜寻过程控制。

    **重要信息：**Connector Framework 输入适配器检索到的数据将在本地进行高速缓存。这些数据在存储时不进行加密。缺省情况下，用于缓存这些数据的临时目录应该会在重新引导时被清除，且只能由执行 crawler 命令的用户来读取。

    如果 Connector Framework 在此目录自行清除之前就已退出，此目录的保留时间可能比搜寻器还长。请谨慎考虑缓存数据的存放位置 - 您可以将这些数据放到加密的文件系统中，但需要注意这样做所产生的性能影响。只有您可以决定搜寻速度与安全性之间的适度平衡。
-   **`crawl_config_file`** - 要用于搜寻的配置文件。缺省值为：`connectors/filesystem.conf`
-   **`crawl_seed_file`** - 要用于搜寻的搜寻种子文件。缺省值为：`seeds/filesystem-seed.conf`
-   **`id_vcrypt_file`** - 搜寻器用于数据加密的密钥文件；搜寻器随附的缺省密钥为 `id_vcrypt`。如果需要生成新的 `id_vcrypt` 文件，请使用 `bin` 文件夹中的 vcrypt 脚本。
-   **`crawler_temp_dir`** - 用于存放连接器日志的搜寻器临时文件夹。提供的缺省值为 `tmp`。如果还不存在 `tmp` 文件夹，那么将在当前工作目录中创建该文件夹。
-   **`extra_jars_dir`** - 将额外 JAR 的目录添加到 Connector Framework 类路径。

    **注：**相对于 Connector Framework `lib/java` 目录。

    -   使用 SharePoint 连接器时，此值必须为 `oakland`。
    -   使用数据库连接器时，此值必须为 `database`。

    使用其他连接器时，可将此值保留为空（即，空字符串 ""）。

-   **`urls_to_filter`** - 不应搜寻的 URL 的黑名单，格式为正则表达式。Data Crawler 不会搜寻与提供的任何正则表达式匹配的 URL。

    `domain list` 包含无法搜寻的域。请根据需要向其添加相关域。

    `filetype list` 包含 Orchestration Service 不支持的文件扩展名。

    从正则表达式除去任何支持的文件类型。

    确保过滤器不会排除您的种子 URL 域。使用空过滤器表示`允许所有项`行为。

    确保过滤器不会排除您的种子 URL，否则搜寻器可能挂起。

-   **`max_text_size`** - Connector Framework 将文档写入到磁盘前该文档的最大大小（以字节计）。调高此值会减少写入磁盘的文档量，但会增加内存需求。缺省值为 `1048576`。
-   **`extra_vm_params`** - 允许您向用于启动 Connector Framework 的命令中添加额外的 Java 参数。

-   **`bootstrap_logging`** - 编写 Connector Framework 启动日志；仅用于高级调试。可能的值为 `true` 或 `false`。日志文件将写入 `crawler_temp_dir`。

-   **`read-timeout`** - 设置搜寻器将等待来自 Connector Framework 的响应的时间（以秒计）。缺省值为 5 秒。

### 输出适配器
{: #output-adapter}

-   **`class`** - 定义 Data Crawler 输出适配器类。
-   **`config`** - 定义要传递到输出适配器的配置键。该字符串必须与此配置对象中的键相对应。在以下代码示例中：

    ```
        class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

        

    config - "discovery_service"

        

    discovery_service {
        include "discovery/discovery_service.conf"
      }
    ```
    {: codeblock}

    配置键为 `discovery_service`。

必须通过指定 `class` 参数和 `config` 键来选择输出适配器。

-   **{{site.data.keyword.discoveryshort}} 服务输出适配器** - 将搜寻到的文档上传到 {{site.data.keyword.discoveryfull}} 服务。通过设置 `class` 参数和 `config` 键来选择此适配器，如下所示。

```
class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

config - "discovery_service"

discovery_service {
            include "discovery/discovery_service.conf"
  }
```
{: codeblock}

-   **测试输出适配器** - 测试输出适配器将所搜寻到文件的表示写入磁盘中的指定位置。通过设置 `class` 参数和 `config` 键来选择此适配器，如下所示。

    另外一个参数 `output_directory` 用于选择应该将所搜寻到数据的表示写入的目录。

```
class - "com.ibm.watson.crawler.testoutputadapter.TestOutputAdapter"

config - "test"

output_directory - "/tmp/crawler-test-output"`
```
{: codeblock}

-   **`retry`** - 指定在推送至输出适配器的尝试失败时可用的重试选项。

    -   `max_attempts` - 最大重试次数。缺省值为 `10`。
    -   `delay` - 两次尝试之间的最短延迟（以秒计）。缺省值为 `2`。
    -   `exponent_base` - 用于确定每次失败尝试后延迟时间增长量的因子。缺省值为 `2`。

    公式如下：

        **`d(nth_retry) - delay * (exponent_base ^ nth_retry)`**

    例如，缺省设置的延迟为 1 秒，指数底数为 2，此设置将使第二次重试（即第三次尝试）延迟 2 秒而不是 1 秒，再下一次重试将延迟 4 秒。

        `d(0) - 1 * (2 ^ 0)` - 1 秒
        `d(1) - 1 * (2 ^ 1)` - 2 秒
        `d(2) - 1 * (2 ^ 2)` - 4 秒

    因此，使用缺省设置时，将最多尝试提交 10 次，最长等待大约 1022 秒 - 略长于 17 分钟。此时间为近似值，因为其中会额外增加一些时间以防同时执行多个重新提交操作。此“模糊处理”的时间最大偏差为 10%，因此上面示例中的最后一次重试可延迟最多 7.7 秒。等待时间不包括连接到服务、上传数据或等待响应所用的时间。

    `output_timeout` 值优先于此处的等待时间：如果重试等待总时间超过该设置，那么即便应该会重试提交，该提交也会失败。
    {: tip}

### 其他搜寻管理选项
{: #additional-crawl-management-options}

-   **`full_node_debugging`** - 激活调试方式；可能的值包括 `true` 或 `false`。

    **重要信息：**这会将搜寻到的每个文档的完整数据放入到日志中。   

-   **`logging.log4j.configuration_file`*** - 要用于日志记录的配置文件。在样本 `crawler.conf` 文件中，在 `logging.log4j` 中定义此选项，并且其缺省值为 `log4j_custom.properties`。
无论是使用 `.properties` 还是 `.conf` 文件，必须以同样的方式定义此选项。   
-   **`shutdown_timeout`** - 指定关闭应用程序前的超时值（以分钟计）。缺省值为 `10`。   
-   **`output_limit`** - 搜寻器尝试同时发送到输出适配器的可索引项的最大数量。可用于执行处理的核心数会进一步限制此数量。即，在任何时候向等待返回的输出适配器发送的可索引项数量不得超过“x”。缺省值为 `10`。   
-   **`input_limit`** - 限制可以一次从输入适配器请求的 URL 数。缺省值为 `30`。   
-   **`output_timeout`** - Data Crawler 放弃向输出适配器发出的请求，然后从输出适配器队列中除去该项以允许进行更多处理之前的时间长度（以秒计）。缺省值为 `1200`。

    应考虑输出适配器施加的约束，因为这些约束可能与此处定义的限制相关。定义的 `output_limit` 仅与可以同时发送到输出适配器的可索引对象数相关。将可索引对象发送到输出适配器后，便开始“计时”（如 `output_timeout` 变量所定义）。输出适配器本身可能有调速，使它无法处理收到的所有输入。例如，Orchestration 输出适配器可能有一个连接池（可针对到该服务的 HTTP 连接进行配置）。例如，如果将此值缺省设置为 8，并且您为 `output_limit` 设置的数字大于 8，那么会有一些进程已开始计时并等待轮流执行。这样，您可能会遇到超时。   
-   **`num_threads`** - 可同时运行的并行线程数。此值可以为整数（直接指定并行线程数），也可以为“`xNUM`”格式的字符串（指定可用处理器数的倍增因子，例如“`x1.5`”）。缺省值为“`30`”。

## 配置服务选项
{: #configuring-service-options}

{{site.data.keyword.discoveryshort}} 服务指示搜寻器如何在使用 {{site.data.keyword.discoveryfull}} 服务时管理搜寻到的文件。

要访问 `discovery-service.conf` 文件的产品内联机帮助并获取最新信息，请从搜寻器安装目录输入以下命令：


  ```bash
  man discovery_service.conf
  ```
  {: pre}
{: tip}

通过打开 `config/discovery/discovery_service.conf` 文件，并针对您的用例指定以下值，可直接更改缺省选项：

-   **`http_timeout`** - 文档读取/建立索引操作的超时值（以秒计）；缺省值为 `125`。
-   **`proxy_host_port`** -（可选）在防火墙后运行 Data Crawler 时，您可能需要设置代理主机名和代理端口号，Data Crawler 才能与 {{site.data.keyword.discoveryshort}} 服务进行对话。此选项的缺省值是一个空字符串，如果需要更改该值，那么该值的格式应该为“`<host>:<port>"`.
-   **`concurrent_upload_connection_limit`** - 允许用于上传文档的同时连接数。缺省值为 `2`。

    **注：**使用 Orchestration Service 输出适配器时，此数字应该大于或等于配置搜寻选项时设置的 `output_limit`。   

-   **`base_url`** - 搜寻到的文档将发送到的 URL。对于 {{site.data.keyword.discoveryshort}} 服务的当前发行版，值为 `https://gateway.watsonplatform.net/discovery/api`。   
-   **`environment_id`** - 在基本 URL 中搜寻到的文档集合的位置。   
-   **`collection_id`** - 在 {{site.data.keyword.discoveryshort}} 服务中设置的文档集合的名称。
-   **`api_version`** - 仅供内部使用。上次更改 API 版本的日期。   
-   **`configuration_id`** - {{site.data.keyword.discoveryshort}} 服务使用的配置文件的文件名。
-   **`username`** - 用于向所搜寻到文档集合的位置进行认证的用户名。   
-   **`password`** - 用于向所搜寻到文档集合的位置进行认证的密码。

{{site.data.keyword.discoveryshort}} 服务输出适配器可以发送统计信息，以便 {{site.data.keyword.IBM}} 更好地了解用户并为其提供服务。可设置 `send_stats` 变量的以下选项：

-   **`jvm`** - 已发送的 Java 虚拟机 (JVM) 统计信息（包括 Java 供应商和版本），这些统计信息由用于执行 Data Crawler 的 JVM 来报告。值为 `true` 或 `false`。缺省值为 `true`。
-   **`os`** - 已发送的操作系统 (OS) 统计信息（包括 OS 名称、版本和体系结构），这些统计信息由用于执行 Data Crawler 的 JVM 来报告。值为 `true` 或 `false`。缺省值为 `true`。
