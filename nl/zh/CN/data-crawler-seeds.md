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

# 配置连接器和种子选项

搜寻数据时，搜寻器首先确定数据存储库（连接器）的类型和用户指定的起始位置（种子）以开始下载信息。
{: shortdesc}

**重要信息：**使用 Data Crawler 时，将忽略数据存储库安全设置。

种子是搜寻的起始点，Data Crawler 将使用种子从连接器所确定的资源中检索数据。通常，种子会配置 URL 来访问基于协议的资源，例如各种协议可访问的文件共享、SMB 共享、数据库和其他数据存储库。此外，不同的种子 URL 也具有不同的功能。种子也可以特定于存储库，可用于搜寻特定的第三方应用程序（例如，客户关系管理 (CRM) 系统、产品生命周期 (PLC) 系统、内容管理系统 (CMS)、基于云的应用程序以及 Web 数据库应用程序）。

要正确搜寻数据，必须确保已将搜寻器正确配置为读取数据存储库。Data Crawler 提供连接器来支持从以下存储库收集数据：

-   [文件系统](/docs/services/discovery/data-crawler-seeds.html#configuring-filesystem-crawl-options)
-   [使用 JDBC 的数据库](/docs/services/discovery/data-crawler-seeds.html#configuring-database-crawl-options)
-   [CMIS（内容管理互操作性服务）](/docs/services/discovery/data-crawler-seeds.html#configuring-cmis-crawl-options)
-   [SMB（服务器消息块）、CIFS（公共因特网文件系统）或 Samba 文件共享](/docs/services/discovery/data-crawler-seeds.html#configuring-smbcifssamba-crawl-options)
-   [SharePoint 和 SharePoint Online](/docs/services/discovery/data-crawler-seeds.html#configuring-sharepoint-crawl-options)
-   [Box](/docs/services/discovery/data-crawler-seeds.html#configuring-box-crawl-options)

此外还提供了一个连接器配置模板，您可以使用此模板来定制连接器。

要配置连接器，请执行以下操作：

1.  在文本编辑器中打开 `connectors` 目录中与要连接的存储库相对应的文件（例如，`filesystem.conf` 是文件系统连接器的配置文件）。

1.  修改与存储库相应的值：

    -   [文件系统](/docs/services/discovery/data-crawler-seeds.html#filesystem-crawl-options)
    -   [使用 JDBC 的数据库](/docs/services/discovery/data-crawler-seeds.html#database-crawl-seed)
    -   [CMIS（内容管理互操作性服务）](/docs/services/discovery/data-crawler-seeds.html#cmis-crawl-options)
    -   [SMB（服务器消息块）、CIFS（公共因特网文件系统）或 Samba 文件共享](/docs/services/discovery/data-crawler-seeds.html#smb-cifs-samba-crawl-options)
    -   [SharePoint 和 SharePoint Online](/docs/services/discovery/data-crawler-seeds.html#sharepoint-crawl-options)
    -   [Box](/docs/services/discovery/data-crawler-seeds.html#box-crawl-options)
1.  保存并关闭此文件。
1.  在文本编辑器中对 `connectors/seeds` 目录中与要连接的存储库相对应的 `-seed.conf` 文件重复上述操作（例如，`filesystem-seed.conf` 是文件系统连接器的（要连接到的）种子配置文件）。
1.  继续[配置 Data Crawler 以连接到 {{site.data.keyword.discoveryshort}}](/docs/services/discovery/data-crawler-discovery.html)。

要访问连接器和种子配置文件的产品内联机帮助并获取最新信息，请从搜寻器安装目录输入以下命令：
-   对于连接器配置选项：
    ```bash
    man crawler-options.conf
    ```
    {: pre}
-   对于搜寻种子配置选项：
    ```bash
    man crawler-seed.conf
    ```
    {: pre}


## 配置文件系统搜寻选项
{: #filesystem-crawl-options}

通过文件系统连接器，可以搜寻 Data Crawler 安装的本地文件。

### 配置文件系统连接器

下面是使用文件系统连接器时需要设置的基本配置选项。要设置这些值，请打开 `config/connectors/filesystem.conf` 文件，并针对您的用例修改以下值：

-   **`protocol`** - 用于搜寻的连接器协议的名称。请对此连接器使用 `sdk-fs`。
-   **`collection`** - 该属性用于解包临时文件。缺省值为 `crawler-fs`
-   **`logging-config`** - 指定用于配置日志记录选项的文件；它必须格式化为 `log4j` XML 字符串。
-   **`classname`** - 连接器的 Java 类名。使用此连接器时，该值必须为 `plugin:filesystem.plugin@filesystem`。

### 配置文件系统搜寻种子

可配置文件系统搜寻种子文件的以下值。要设置这些值，请打开 `config/seeds/filesystemseed.conf` 文件，并针对您的用例指定以下值：

-   **`url`** - 要搜寻的文件和文件夹的换行符分隔列表。UNIX 用户可以使用诸如 `/usr/local/` 的路径。

    **注：**URL 必须以 `sdk-fs://` 开头。例如，要搜寻 `/home/watson/mydocs`，此 URL 的值将为 `sdk-fs:///home/watson/mydocs` - 第三个 `/` 是必需的！

    Linux、UNIX 和类 UNIX 计算机系统使用的文件系统可能包含特殊类型的文件，例如表示指定管道的块和字符设备节点与文件；无法搜寻这些文件，因为它们不包含数据，而是充当设备或 I/O 访问点。在搜寻期间尝试搜寻此类文件将生成错误。要避免此类错误，应该在 Linux、UNIX 或类 UNIX 文件系统上的任何顶级搜寻中排除 `/dev` 目录。如果在要搜寻的系统上存在此目录，那么还应排除包含瞬态文件和系统信息的临时系统目录，例如 `/proc`、`/sys` 和 `/tmp`。**`hops`** - 仅供内部使用。**`default-allow`** - 仅供内部使用。
    {: tip}

## 配置数据库搜寻选项

您可以使用数据库连接器，通过执行定制 SQL 命令并针对每行（记录）创建一个文档且针对每列（字段）创建一个内容元素，以搜寻数据库。您可以指定要用作唯一键的列，还可以指定包含时间戳记（表示每个记录的上次修改日期）的列。该连接器将从指定数据库中检索所有记录，也可以通过 SQL 语句将记录检索范围限制为特定的表和连接等。

您可以使用数据库连接器来搜寻以下数据库：

-   {{site.data.keyword.IBM}} Db2
-   MySQL
-   Oracle PostgreSQL
-   Microsoft SQL Server
-   Sybase
-   通过符合 JDBC 3.0 的驱动程序使用的其他符合 SQL 的数据库

该连接器将从指定数据库和表中检索所有记录。

***JDBC 驱动程序*** - 数据库连接器随附 Oracle JDBC（Java 数据库连接）驱动程序 V1.5。Data Crawler 随附的所有第三方 JDBC 驱动程序都位于 Data Crawler 安装的 `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` 目录中；在此目录中可以根据需要添加、除去和修改这些驱动程序。您也可以使用 `crawler.conf` 文件中的 `extra_jars_dir` 设置来指定其他位置。

***Db2 JDBC 驱动程序*** - 由于许可问题，Data Crawler 并未随附用于 Db2 的 JDBC 驱动程序。但是，安装了 JDBC 支持的所有 Db2 安装都包含 Data Crawler 需要的 JAR 文件，以便能够搜寻 Db2 安装。要搜寻 Db2 实例，必须将这些文件复制到 Data Crawler 安装中的相应目录，以便数据库连接器可以使用这些文件。要支持 Data Crawler 搜寻 Db2 安装，请在 Db2 安装中找到 `db2jcc.jar` 和许可证 JAR 文件（通常为 `db2jcc_license_cu.jar`），然后将这些文件复制到 Data Crawler 安装目录的 `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` 子目录，或者可以使用 `crawler.conf` 文件中的 `extra_jars_dir` 设置来指定其他位置。

***MySQL JDBC 驱动程序*** - 由于可能的许可证问题，Data Crawler 并未随附用于 MySQL 的 JDBC 驱动程序（如果这些驱动程序已作为产品的一部分交付）。但是，下载包含 MySQL JDBC 驱动程序的 JAR 文件并将该 JAR 文件集成到 Data Crawler 安装非常容易：

1.  使用 Web 浏览器访问 MySQL 下载站点，找到您要使用的归档格式（通常，对于 Microsoft Windows 系统，格式为 zip；对于 Linux 系统，格式为 gzipped tarball）的源文件和二进制文件下载链接。单击该链接以启动下载过程。可能需要进行注册。
1.  根据下载的归档文件的类型和名称，使用相应的 unzip archive-file-name 或 tar zxf archive-file-name 命令来解压缩该归档的内容。
1.  切换到该归档文件的解压缩目录，然后将此目录中的 JAR 文件复制到 Data Crawler 安装目录的 `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` 子目录，或者可以使用 `crawler.conf` 文件中的 `extra_jars_dir` 设置来指定其他位置。

### 配置数据库连接器

下面是使用数据库连接器时需要设置的基本配置选项。要设置这些值，请打开 config/connectors/database.conf 文件，并针对您的用例修改以下值：

-   **`protocol`** - 用于搜寻的连接器协议的名称。此连接器的这个值取决于要访问的数据库系统。
-   **`collection`** - 该属性用于解包临时文件。
-   **`classname`** - 连接器的 Java 类名。使用此连接器时，该值必须为 `plugin:database.plugin@database`。
-   **`logging-config`** - 指定用于配置日志记录选项的文件；它必须格式化为 `log4j` XML 字符串。

### 配置数据库搜寻种子
{: #database-crawl-seed}

可配置数据库搜寻种子文件的以下值。要设置这些值，请打开 `config/seeds/database-seed.conf` 文件，并针对您的用例指定以下值：

-   **`url`** - 要检索的表或视图的 URL。定义定制的 SQL 数据库种子 URL。结构为：

    -   `database-system://host:port/database?[per=num]&[sql=SQL]`

    测试种子 URL 将显示所有排队的 URL。例如，测试包含 200 条记录的数据库的以下 URL：
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?per=100&sql=select%20*%20from%20vessel&`

    将显示以下排队的 URL：
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=0&`
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=100&`
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=200&`

    测试以下 URL 将显示从第 43 行检索的数据：
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?per-1&key-val=43`
-   **`hops`** - 仅供内部使用。
-   **`default-allow`** - 仅供内部使用。
-   **`user-password`** - 用于数据库系统的凭证。用户名和密码需要用 `:` 分隔，并且密码必须使用 Data Crawler 随附的 vcrypt 程序加密。例如：`username:[[vcrypt/3]]passwordstring`
-   **`max-data-size`** - 单个文档的最大数据量。这是一次可装入的最大内存块。仅当您的计算机上有足够的内存时，才可增加此限制。
-   **`filter-exact-duplicates`** - 仅供内部使用。
-   **`timeout`** - 仅供内部使用。
-   **`jdbc-class`**（Extender 选项）- 如果指定了此选项，该字符串将覆盖当选择`（其他）`作为数据库系统时连接器使用的 JDBC 类。
-   **`connection-string`**（Extender 选项）- 如果指定了此选项，此字符串将覆盖自动生成的 JDBC 连接字符串。这样，您便可以提供关于数据库连接的更详细的配置，例如，负载均衡或 SSL 连接。例如：`jdbc:netezza://127.0.0.1:5480/databasename`
-   **`save-frequency-for-resume`**（Extender 选项）- 指定列或关联标签的名称，以便能够恢复搜寻或执行部分刷新。种子在搜寻过程中会定期保存该列的名称，并在搜寻完数据库最后一行后再次保存该名称。恢复搜寻或刷新搜寻后，搜寻会从此字段的保存值中标识的行开始执行。

## 配置 CMIS 搜寻选项
{: #cmis-crawl-options}

通过 CMIS（内容管理互操作性服务）连接器，可以搜寻支持 CMIS 的 CMS（内容管理系统）存储库（例如，Alfresco、Documentum 或 {{site.data.keyword.IBM}} Content Manager），并对它们包含的数据建立索引。

### 配置 CMIS 连接器

下面是使用 CMIS 连接器时需要设置的基本配置选项。要设置这些值，请打开 `config/connectors/cmis.conf` 文件，并针对您的用例指定以下值：

-   **`protocol`** - 用于搜寻的连接器协议的名称。使用此连接器时，该值必须为 `cmis`。
-   **`collection`** - 该属性用于解包临时文件。
-   **`dns`** - 未使用的选项。
-   **`classname`** - 连接器的 Java 类名。对于此连接器，请使用 `plugin:cmis-v1.1.plugin@connector`。
-   **`logging-config`** - 指定用于配置日志记录选项的文件；它必须格式化为 `log4j` XML 字符串。
-   **`endpoint`** - 与 CMIS 兼容的存储库的服务端点 URL。例如，SharePoint 的 URL 结构包括：

    -   对于 AtomPub 绑定：`http://yourserver/_vti_bin/cmis/rest?getRepositories`
    -   对于 WebServices 绑定：`http://yourserver/_vti_bin/cmissoapwsdl.aspx`
-   **`username`** - 用于访问内容的 CMIS 存储库用户的用户名。该用户必须有权访问要搜寻和建立索引的所有目标文件夹和文档。
-   **`password`** - 用于访问内容的 CMIS 存储库的密码。此密码不得加密，应以纯文本格式提供。
-   **`repositoryid`** - 要访问其内容的 CMIS 存储库的标识。
-   **`bindingtype`** - 标识在连接 CMIS 存储库时要使用的绑定类型。值为 AtomPub 或 WebServices。
-   **`authentication`** - 标识在联系与 CMIS 兼容的存储库时要使用的认证机制类型：基本 HTTP 认证、NTLM 或 WS-Security（用户名令牌）。
-   **`enable-acl`** - 启用用于检索已搜寻数据 ACL 的功能。如果您不担心此集合中文档的安全性，那么禁用此选项可以提高性能，因为将不会向文档请求这些信息，也不会对这些信息进行检索和编码。值为 true 或 false。
-   **`user-agent`** - 搜寻文档时发送到服务器的头。
-   **`method`** - 用于传递参数的方法（GET 或 POST）。
-   **`url-logging`** - 已搜寻 URL 的日志记录范围。可能的值为：

    -   `full-logging` - 记录有关 URL 的所有信息。
    -   `refined-logging` - 仅记录浏览搜寻器日志和连接器正常运行所需的信息；这是缺省值。
    -   `minimal-logging` - 仅记录连接器正常运行所需的最少信息量。

    因为将所记录的数据量降至最少会减少 I/O，因此将此选项设置为 `minimal-logging` 可减小日志大小并略微提高性能。
-   **`ssl-version`** - 指定要用于 HTTPS 连接的 SSL 版本。缺省情况下，会使用安全性最高的协议。

### 配置 CMIS 搜寻种子

可配置 CMIS 搜寻种子文件的以下值。要设置这些值，请打开 `config/seeds/cmisseed.conf` 文件，并针对您的用例修改以下值：

-   **`url`** - CMIS 存储库中要用作搜寻起始点的文件夹的 URL，例如：`cmis://alfresco.test.com:8080/alfresco/cmisatom?folderToProcess-workspace://SpacesStore/guid`

    要从根文件夹中进行搜寻，您需要将 URL 指定为：`cmis://alfresco.test.com:8080/alfresco/cmisatom?folderToProcess-`
-   **`at`** - 未使用的选项。
-   **`default-allow`** - 仅供内部使用。

## 配置 SMB/CIFS/Samba 搜寻选项
{: #smb-cifs-samba-crawl-options}

通过 Samba 连接器，可以搜寻服务器消息块 (SMB) 和公共因特网文件系统 (CIFS) 文件共享。这种类型的文件共享在 Windows 网络上十分普遍，也可通过开放式源代码项目 Samba 来提供。

### 配置 Samba 连接器

下面是使用 Samba 连接器时需要设置的基本配置选项。要设置这些值，请打开 `config/connectors/samba.conf` 文件，并针对您的用例指定以下值：

-   **`protocol`** - 用于搜寻的连接器协议的名称。使用此连接器时，该值为 smb。
-   **`collection`** - 该属性用于解包临时文件。
-   **`classname`** - 连接器的 Java 类名。使用此连接器时，该值必须为 `plugin:smb.plugin@connector`。
-   **`logging-config`** - 指定用于配置日志记录选项的文件；它必须格式化为 `log4j` XML 字符串。
-   **`username`** - 用于进行认证的 Samba 用户名。如果已提供此选项，那么还必须提供域和密码。如果未提供此项，那么将使用访客帐户。
-   **`password`** - 用于进行认证的 Samba 密码。如果提供了用户名，那么此选项为必填。必须使用 Data Crawler 随附的 vcrypt 程序来加密密码。
-   **`archive`** - 可使 Samba 连接器搜寻归档文件中压缩的文件并对其建立索引。值为 true 或 false；缺省值为 false。
-   **`max-policies-per-handle`** - 指定可以为单个 RPC 句柄打开的本地安全授权 (LSA) 策略的最大数量。这些策略定义在各种情况下查询或修改特定系统所需的访问许可权。此选项的缺省值为 255。
-   **`crawl-fs-metadata`** - 开启此选项将使 Data Crawler 添加包含文件相关可用文件系统元数据（创建日期、上次修改日期、文件属性等）的 VXML 文档.
-   **`enable-arc-connector`** - 未使用的选项。
-   **`disable-indexes`** - 要禁用的索引的换行符分隔列表，此选项可能会加快搜寻，例如：

    -   `disable-url-index`
    -   `disable-error-state-index`
    -   `disable-crawl-time-index`
-   **`exact-duplicates-hash-size`** - 设置用于解析完全重复项的散列表的大小。修改此数字时请格外小心。您选择的值必须适宜；此值越大，查找速度越快但需要更多内存，反之，此值越小，搜寻速度越慢但会显著降低内存使用率。
-   **`user-agent`** - 未使用的选项。
-   **`timeout`** - 未使用的选项。
-   **`n-concurrent-requests`** - 并行发送到单个 IP 地址的请求数。缺省值为 `1`。
-   **`enqueue-persistence`** - 未使用的选项。

### 配置 Samba 搜寻种子

可配置 Samba 搜寻种子文件的以下值。要设置这些值，请打开 `config/seeds/samba-seed.conf` 文件，并针对您的用例指定以下值：

-   **`url`** - 要搜寻的共享的换行符分隔列表，例如：

    ```
    smb://share.test.com/office
    smb://share.test.com/cash/money/change
    smb://share.test.com/C$/Program Files
    ```
    {: codeblock}

-   **`hops`** - 仅供内部使用。
-   **`default-allow`** - 仅供内部使用。

## 配置 SharePoint 搜寻选项
{: #sharepoint-crawl-options}

**重要信息：**SharePoint 连接器需要 Microsoft SharePoint Server 2007 (MOSS 2007)、SharePoint Server 2010、SharePoint Server 2013 或 SharePoint Online。

通过 SharePoint 连接器，可以搜寻 SharePoint 对象，并对这些对象包含的信息建立索引。可以使用关联的元数据对文档、用户概要文件、站点集合、博客、列表项、成员资格列表、目录页面等对象建立索引。对于列表项和文档，索引可以包含附件。

SharePoint 连接器会考虑所有 SharePoint 对象上的 `noindex` 属性，而不管这些对象的特定类型（博客、文档、用户概要文件等）。将针对每个结果返回一个文档。
{: tip}

**重要信息：**用于搜寻 SharePoint 站点的 SharePoint 帐户必须至少具有完全读访问权。

### 配置 SharePoint 连接器

下面是使用 SharePoint 连接器时需要设置的基本配置选项。要设置这些值，请打开 `config/connectors/sharepoint.conf` 文件，并针对您的用例修改以下值：

-   **`protocol`** - 用于搜寻的连接器协议的名称。使用此连接器时，该值为 `io-sp`。
-   **`collection`** - 该属性用于解包临时文件。
-   **`classname`** - 连接器的 Java 类名。对于此连接器，请使用 `plugin:io-sharepoint.plugin@connector`。
-   **`logging-config`** - 指定用于配置日志记录选项的文件；它必须格式化为 `log4j` XML 字符串。
-   **`seed-url-type`** - 标识所提供的种子 URL 所指向的 SharePoint 对象类型：站点集合或 Web 应用程序（也称为虚拟服务器）。

    -   `站点集合` - 如果“种子 URL 类型”设置为“站点集合”，那么将仅搜寻该 URL 所引用站点集合的子代。
    -   `Web 应用程序` - 如果“种子 URL 类型”设置为“Web 应用程序”，那么将搜寻属于每个 URL 所引用 Web 应用程序的所有站点集合（及其子代）。
-   **`auth-type`** - 在联系 SharePoint 服务器时要使用的认证机制：`BASIC`、`NTLM2`、`KERBEROS` 或 `CBA`。缺省认证类型为 `NTLM2`。
-   **`spUser`** - 用于访问内容的 SharePoint 用户的用户名。该用户必须有权访问要搜寻和建立索引的所有目标站点和列表，并且必须能够检索和解析相关许可权。输入此用户名时最好带有域名，例如：`MYDOMAIN\\Administrator`。
-   **`spPassword`** - 用于访问内容的 SharePoint 用户的密码。必须使用 Data Crawler 随附的 vcrypt 程序来加密密码。
-   **`cba-sts`** - 尝试认证搜寻用户的安全性令牌服务 (STS) 端点的 URL。对于预置 ADFS 的 SharePoint，此值应该是 ADFS 端点。如果“认证类型”设置为 CBA（基于声明的认证），那么此字段是必需的。
-   **`cba-realm`** - 从 STS 请求安全性令牌时要使用的中继方信任标识。有时称为“AppliesTo”值或“域”。对于 SharePoint Online，此值应该是 SharePoint Online 实例根目录的 URL（例如，`https://mycompany.sharepoint.com`）。对于 ADF，此值是 SharePoint 和 ADF 之间的中继方信任的标识值（例如，`"urn:SHAREPOINT:adfs"`）。
-   **`everyone-group`** - 如果指定此选项，那么当为所有人提供访问权时，ACL 中将使用该组名。如果启用了搜寻用户概要文件，那么此字段为必填字段。

    **注：**“检索和排名”服务不会考虑安全性。

-   **`user-profile-master-url`** - 连接器用于构建用户概要文件链接的基本 URL。此 URL 应配置为指向用户概要文件的显示表单。如果发现令牌 `%FIRST_SEED%`，该令牌将替换为第一个种子 URL。启用了搜寻用户概要文件的功能时，这为必填项。
-   **`urls`** - 要搜寻的 SharePoint Web 应用程序或站点集合的 HTTP URL 的换行符分隔列表。
-   **`ehcache-config`** - 未使用的选项。
-   **`method`** - 用于传递参数的方法（`GET` 或 `POST`。
-   **`cache-types`** - 未使用的选项。
-   **`cache-size`** - 未使用的选项。
-   **`enable-acl`** - 支持搜寻 SharePoint 用户概要文件；值为 `true` 或 `false`；缺省值为 `false`。

### 配置 SharePoint 搜寻种子

可配置 SharePoint 搜寻种子文件的以下值。要设置这些值，请打开 `config/seeds/sharepoint-seed.conf` 文件，并针对您的用例指定以下值：

-   **`url`** - 要搜寻的 SharePoint Web 应用程序或站点集合的 URL 的换行符分隔列表。例如：

    ```
    io-sp://a.com
    io-sp://b.com:83/site
    io-sp://c.com/site2
    ```
    {: codeblock}

    同时还会搜寻这些站点的子站点（除非它们被其他搜寻规则排除在外）。

-   **`filter-url`** - 要搜寻的 SharePoint Web 应用程序或站点集合的 URL 的换行符分隔列表。例如：

    ```
    http://a.com
    http://b.com:83/site
    http://c.com/site2
    ```
    {: codeblock}

-   **`hops`** - 仅供内部使用。
-   **`n-concurrent-requests`** - 仅供内部使用。
-   **`delay`** - 仅供内部使用。
-   **`default-allow`** - 仅供内部使用。
-   **`seed-protocol`** - 设置站点集合子代的种子协议。如果站点集合的协议为 SSL、HTTP 或 HTTPS，这为必需项。必须将此值设置为与站点集合的协议相同。

## 配置 Box 搜寻选项

您可以使用 Box 连接器来搜寻 Enterprise Box 实例，并对其包含的信息建立索引。

### 配置 Box 连接器

下面是使用 Box 连接器时需要设置的基本配置选项。要设置这些值，请打开 `config/connectors/box.conf` 文件，并针对您的用例修改以下值：

-   **`protocol`** - 用于搜寻的连接器协议的名称。使用此连接器时，该值为 `box`。
-   **`classname`** - 连接器的 Java 类名。对于此连接器，请使用 `plugin:box.plugin@connector`。
-   **`logging-config`** - 指定用于配置日志记录选项的文件；它必须格式化为 `log4j` XML 字符串。
-   **`box-crawl-seed-url`** - Box 的基本 URL。此连接器的这个值为 `box://app.box.com/`。

    您可以搜寻不同类型的 URL，例如：

    -   要搜寻整个企业：`box://app.box.com/`
    -   要搜寻特定文件夹：`box://app.box.com/user/USER_ID/folder/FOLDER_ID/FolderName`
    -   要搜寻特定用户：`box://app.box.com/user/USER_ID/`
-   **`client-id`** - 输入创建 Box 应用程序时由 Box 提供的客户端标识。
-   **`client-secret`** - 输入创建 Box 应用程序时由 Box 提供的客户端密钥。
-   **`path-to-private-key`** - 这是本地文件系统上专用密钥的位置，该专用密钥是为与 Box 通信而生成的专用-公用密钥对的一部分。
-   **`kid`** - 指定公用密钥标识。这是为了与 Box 通信而生成的专用/公用密钥对的另一半。
-   **`enterprise-id`** - 对应用程序授权的企业。企业标识会在 Box 管理员控制台的主页中列出。
-   **`enable-acl`** - 仅供内部使用。启用用于检索已搜寻数据 ACL 的功能。
-   **`user-agent`** - 搜寻文档时发送到服务器的头。
-   **`method`** - 用于传递参数的方法（`GET` 或 `POST`。
-   **`url-logging`** - 已搜寻 URL 的日志记录范围。可能的值为：

    -   `full-logging` - 记录有关 URL 的所有信息。
    -   `refined-logging` - 仅记录浏览搜寻器日志和连接器正常运行所需的信息；这是缺省值。
    -   `minimal-logging` - 仅记录连接器正常运行所需的最少信息量。

    因为将所记录的数据量降至最少会减少 I/O，因此将此选项设置为 `minimal-logging` 可减小日志大小并略微提高性能。
-   **`ssl-version`** - 指定要用于 HTTPS 连接的 SSL 版本。缺省情况下，会使用安全性最高的协议。

### 配置 Box 搜寻种子
{: #box-crawl-options}

可以为 Box 搜寻种子文件配置以下更多值。要设置这些值，请打开 `config/seeds/boxseed.conf` 文件，并针对您的用例指定以下值：

-   **`url`** - 要用作搜寻起点的 URL。缺省值为 `box://app.box.com/`。
-   **`default-allow`** - 仅供内部使用。

## 限制

Box 连接器确实存在一些限制：

-   不检索关于文件的注释或任务。
-   注释内容正文将作为 JSON 进行检索。可能需要对 Notes 数据进行其他转换。
-   不能通过 Test-It 检索单个文档。只能通过 Test-It 检索种子 URL、文件夹 URL 和用户 URL。
