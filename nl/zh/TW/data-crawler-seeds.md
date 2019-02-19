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

# 配置連接器和種子選項

搜索資料時，「搜索器」會先識別資料儲存庫的類型（連接器），以及使用者指定的起始位置（種子）來開始下載資訊。
{: shortdesc}

**重要事項：**使用「資料搜索器」時，會忽略資料儲存庫安全設定。

種子是搜索的起點，「資料搜索器」會使用它從連接器所識別的資源擷取資料。一般而言，種子會配置 URL 以存取通訊協定型資源，例如檔案共用、SMB 共用、資料庫，以及可由各種通訊協定存取的其他資料儲存庫。此外，不同的種子 URL 會有不同的功能。種子也可以是儲存庫特定，以啟用特定協力廠商應用程式（例如客戶關係管理 (CRM) 系統、產品生命週期 (PLC) 系統、內容管理系統 (CMS)、雲端型應用程式及 Web 資料庫應用程式）的搜索。

若要正確地搜索資料，您必須確定「搜索器」已適當配置為讀取資料儲存庫。「資料搜索器」提供連接器來支援從下列儲存庫進行資料收集：

-   [檔案系統](/docs/services/discovery/data-crawler-seeds.html#configuring-filesystem-crawl-options)
-   [資料庫，透過 JDBC](/docs/services/discovery/data-crawler-seeds.html#configuring-database-crawl-options)
-   [CMIS（內容管理交互作業能力服務）](/docs/services/discovery/data-crawler-seeds.html#configuring-cmis-crawl-options)
-   [SMB（伺服器訊息區塊）、CIFS（一般網際網路檔案系統）或 Samba 檔案共用](/docs/services/discovery/data-crawler-seeds.html#configuring-smbcifssamba-crawl-options)
-   [SharePoint 與 SharePoint Online](/docs/services/discovery/data-crawler-seeds.html#configuring-sharepoint-crawl-options)
-   [Box](/docs/services/discovery/data-crawler-seeds.html#configuring-box-crawl-options)

也會提供連接器配置範本，可讓您自訂連接器。

若要配置連接器，請執行下列動作：

1.  在文字編輯器中，開啟 `connectors` 目錄中對應於所連接儲存庫的檔案（例如，`filesystem.conf` 是檔案系統連接器的配置檔）。

1.  修改儲存庫所適用的值：

    -   [檔案系統](/docs/services/discovery/data-crawler-seeds.html#filesystem-crawl-options)
    -   [資料庫，透過 JDBC](/docs/services/discovery/data-crawler-seeds.html#database-crawl-seed)
    -   [CMIS（內容管理交互作業能力服務）](/docs/services/discovery/data-crawler-seeds.html#cmis-crawl-options)
    -   [SMB（伺服器訊息區塊）、CIFS（一般網際網路檔案系統）或 Samba 檔案共用](/docs/services/discovery/data-crawler-seeds.html#smb-cifs-samba-crawl-options)
    -   [SharePoint 與 SharePoint Online](/docs/services/discovery/data-crawler-seeds.html#sharepoint-crawl-options)
    -   [Box](/docs/services/discovery/data-crawler-seeds.html#box-crawl-options)
1.  儲存並關閉檔案。
1.  在文字編輯器中，針對 `connectors/seeds` 目錄中對應於您要連接之儲存庫的 `-seed.conf` 檔案重複執行（例如，`filesystem-seed.conf` 是檔案系統連接器的種子（即連接目的地）配置檔）。
1.  繼續[配置資料搜索器以連接至 {{site.data.keyword.discoveryshort}}](/docs/services/discovery/data-crawler-discovery.html)。

若要存取連接器及種子配置檔的產品手冊及最新資訊，請從「搜索器」安裝目錄中鍵入下列指令：
-   針對連接器配置選項：
    ```bash
    man crawler-options.conf
    ```
    {: pre}
-   針對搜索種子配置選項：
    ```bash
    man crawler-seed.conf
    ```
    {: pre}


## 配置檔案系統搜索選項
{: #filesystem-crawl-options}

檔案系統連接器可讓您搜索「資料搜索器」安裝的本端檔案。

### 配置檔案系統連接器

下列是使用檔案系統連接器所需的基本配置選項。若要設定這些值，請開啟 `config/connectors/filesystem.conf` 檔案，並修改您的使用案例特有的下列值：

-   **`protocol`** - 用於搜索的連接器通訊協定的名稱。對此連接器使用 `sdk-fs`。
-   **`collection`** - 此屬性是用來解壓縮暫存檔。預設值為 `crawler-fs`
-   **`logging-config`** - 指定用於配置記載選項的檔案；必須以 `log4j` XML 字串的形式將它格式化。
-   **`classname`** - 連接器的 Java 類別名稱。用來使用此連接器的值必須是 `plugin:filesystem.plugin@filesystem`。

### 配置檔案系統搜索種子

可以針對檔案系統搜索種子檔配置下列值。若要設定這些值，請開啟 `config/seeds/filesystem-seed.conf` 檔案，並指定您的使用案例特有的下列值：

-   **`url`** - 要搜索的檔案與資料夾以換行區隔清單。UNIX 使用者可以使用 `/usr/local/` 之類的路徑。

    **附註：**URL 必須以 `sdk-fs://` 為開頭。因此比方說，若要搜索 `/home/watson/mydocs`，此 URL 的值會是 `sdk-fs:///home/watson/mydocs` - 第三個 `/` 是必要的！

    Linux、UNIX 及 UNIX 型電腦系統所使用的檔案系統可包含特殊類型的檔案，例如，代表具名管道的區塊和字元裝置節點及檔案，因為它們不包含資料，而是作為裝置或 I/O 存取點，因此無法進行搜索。試圖搜索這類檔案將在搜索期間產生錯誤。若要避免這類錯誤，您應該在 Linux、UNIX 或 UNIX 型檔案系統的任何最上層搜索中排除 `/dev` 目錄。如果您要搜索的系統上有諸如 `/proc`、`/sys` 及 `/tmp` 之類的暫存系統目錄（其包含暫時性檔案和系統資訊），則您也應該除排它們。**`hops`** - 僅供內部使用。**`default-allow`** - 僅供內部使用。
    {: tip}

## 配置資料庫搜索選項

資料庫連接器可讓您藉由執行自訂的 SQL 指令，並每一列（記錄）建立一個文件與每一直欄（欄位）建立一個內容元素來搜索資料庫。您可以指定要作為唯一索引鍵的直欄，以及包含代表每一筆記錄前次修改日期的時間戳記直欄。連接器會從指定的資料庫擷取所有記錄，也可以在 SQL 陳述式中限制於特定的表格、結合等等。

「資料庫」連接器可讓您搜索下列資料庫：

-   {{site.data.keyword.IBM}} DB2
-   MySQL
-   Oracle PostgreSQL
-   Microsoft SQL Server
-   Sybase
-   其他符合 SQL 標準的資料庫（透過符合 JDBC 3.0 標準的驅動程式）

連接器會從指定的資料庫和表格擷取所有記錄。

***JDBC 驅動程式*** - 資料庫連接器隨附於 Oracle JDBC（Java 資料庫連線功能）驅動程式 1.5 版。「資料搜索器」隨附的所有協力廠商 JDBC 驅動程式都位於「資料搜索器」安裝的 `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` 目錄中，您可以在其中視需要來新增、移除及修改它們。您也可以使用 `crawler.conf` 檔案中的 `extra_jars_dir` 設定來指定其他位置。

***DB2 JDBC 驅動程式*** - 由於授權問題，「資料搜索器」不會隨附於 DB2 的 JDBC 驅動程式。不過，您已安裝 JDBC 支援的所有 DB2 安裝，都包含「資料搜索器」要搜索 DB2 安裝所需要的 JAR 檔。若要搜索 DB2 實例，您必須將這些檔案複製到「資料搜索器」安裝中的適當目錄，以便「資料庫」連接器可以使用它們。若要讓「資料搜索器」搜索 DB2 安裝，請在 DB2 安裝中找出 `db2jcc.jar` 和授權（通常是 `db2jcc_license_cu.jar`）JAR 檔，並將那些檔案複製到「資料搜索器」安裝目錄的 `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` 子目錄，也可以使用 `crawler.conf` 檔案中的 `extra_jars_dir` 設定來指定另一個位置。

***MySQL JDBC 驅動程式*** - 「資料搜索器」未隨附於 MySQL 的 JDBC 驅動程式，因為如果是作為產品的一部分來提供它們，可能會有授權問題。不過，下載包含 MySQL JDBC 驅動程式的 JAR 檔，並將該 JAR 檔整合至「資料搜索器」安裝是很容易的事：

1.  使用 Web 瀏覽器來造訪 MySQL 下載網站，並找出您要使用的保存格式的原始檔及二進位下載鏈結（Microsoft Windows 系統通常是 zip，或 Linux 系統則是 gzip Tarball）。按一下該鏈結來起始下載程序。可能需要登錄。
1.  根據您下載的保存檔的類型和名稱，使用適當的 unzip archive-file-name or tar zxf archive-file-name 指令，將該保存檔的內容解壓縮。
1.  切換至從保存檔解壓縮的目錄，並將這個目錄中的 JAR 檔複製到「資料搜索器」安裝目錄的 `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` 子目錄，也可以使用 `crawler.conf` 檔案中的 `extra_jars_dir` 設定來指定另一個位置。

### 配置資料庫連接器

下列是使用「資料庫」連接器所需的基本配置選項。若要設定這些值，請開啟 config/connectors/database.conf 檔案，並修改您的使用案例特有的下列值：

-   **`protocol`** - 用於搜索的連接器通訊協定的名稱。此連接器的值是根據要存取的資料庫系統。
-   **`collection`** - 此屬性是用來解壓縮暫存檔。
-   **`classname`** - 連接器的 Java 類別名稱。用來使用此連接器的值必須是 `plugin:database.plugin@database`。
-   **`logging-config`** - 指定用於配置記載選項的檔案；必須以 `log4j` XML 字串的形式將它格式化。

### 配置資料庫搜索種子
{: #database-crawl-seed}

您可以為資料庫搜索種子檔配置下列值。若要設定這些值，請開啟 `config/seeds/database-seed.conf` 檔案，並指定您的使用案例特有的下列值：

-   **`url`** - 要擷取表格或視圖的 URL。定義您的自訂 SQL 資料庫種子 URL。結構為：

    -   `database-system://host:port/database?[per=num]&[sql=SQL]`

    測試種子 URL 將顯示放入佇列的所有 URL。例如，測試下列 URL 可取得含有 200 筆記錄的資料庫：
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?per=100&sql=select%20*%20from%20vessel&`

    顯示下列已放入佇列的 URL：
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=0&`
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=100&`
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=200&`

    當測試下列 URL 時，將顯示從列 43 擷取的資料：
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?per-1&key-val=43`
-   **`hops`** - 僅供內部使用。
-   **`default-allow`** - 僅供內部使用。
-   **`user-password`** - 資料庫系統的認證。使用者名稱及密碼必須以 `:` 區隔，而且必須使用「資料搜索器」隨附的 vcrypt 程式將密碼加密。例如：`username:[[vcrypt/3]]passwordstring`
-   **`max-data-size`** - 文件資料的大小上限。這是一次將載入的最大記憶體區塊。只有在您的電腦上有足夠的記憶體時才增加此限制。
-   **`filter-exact-duplicates`** - 僅供內部使用。
-   **`timeout`** - 僅供內部使用。
-   **`jdbc-class`**（延伸器選項）- 若指定，當您選擇 `(other)` 作為資料庫系統時，此字串會置換連接器所使用的 JDBC 類別。
-   **`connection-string`**（延伸器選項）- 若指定，此字串會置換連接器自動產生的 JDBC 連線字串。如此一來，您就可以提供關於資料庫連線更詳細的配置，例如負載平衡或 SSL 連線。例如：`jdbc:netezza://127.0.0.1:5480/databasename`
-   **`save-frequency-for-resume`**（延伸器選項）- 指定直欄或關聯標籤的名稱，以便能夠回復搜索或執行局部重新整理。種子會在繼續進行搜索時定期儲存此直欄的名稱，並在搜索您的資料庫最後一列之後，再次儲存該名稱。繼續搜索或重新整理時，搜索會從此欄位的儲存值中所識別的列開始

## 配置 CMIS 搜索選項
{: #cmis-crawl-options}

CMIS (Content Management Interoperability Services) 連接器可讓您搜索已啟用 CMIS 的 CMS (Content Management System) 儲存庫，例如 Alfresco、Documentum 或 {{site.data.keyword.IBM}} Content Manager，並檢索其包含的資料。

### 配置 CMIS 連接器

下列是使用 CMIS 連接器所需的基本配置選項。若要設定這些值，請開啟 `config/connectors/cmis.conf` 檔案，並指定您的使用案例特有的下列值：

-   **`protocol`** - 用於搜索的連接器通訊協定的名稱。用來使用此連接器的值必須是 `cmis`。
-   **`collection`** - 此屬性是用來解壓縮暫存檔。
-   **`dns`** - 未使用的選項。
-   **`classname`** - 連接器的 Java 類別名稱。對此連接器使用 `plugin:cmis-v1.1.plugin@connector`。
-   **`logging-config`** - 指定用於配置記載選項的檔案；必須以 `log4j` XML 字串的形式將它格式化。
-   **`endpoint`** - CMIS 相容儲存庫的服務端點 URL。例如，SharePoint 的 URL 結構是：

    -   若為 AtomPub 連結：`http://yourserver/_vti_bin/cmis/rest?getRepositories`
    -   若為 WebServices 連結：`http://yourserver/_vti_bin/cmissoapwsdl.aspx`
-   **`username`** - 用來存取內容的 CMIS 儲存庫使用者的使用者名稱。此使用者必須可存取要搜索及建立索引的所有目標資料夾和文件。
-   **`password`** - 用來存取內容的 CMIS 儲存庫的密碼。密碼「不能」加密；必須以純文字提供。
-   **`repositoryid`** - 用來存取該特定儲存庫內容的 CMIS 儲存庫的 ID。
-   **`bindingtype`** - 識別要用於連接 CMIS 儲存庫的連結類型。值為 AtomPub 或 WebServices。
-   **`authentication`** - 識別在聯絡 CMIS 相容儲存庫時要使用的鑑別機制的類型：基本 HTTP 鑑別、NTLM 或 WS-Security（使用者名稱記號）。
-   **`enable-acl`** - 啟用擷取已搜索資料的 ACL。如果您對於這個集合中文件的安全沒有疑慮，則停用此選項將會增加效能，因為不會向文件要求此資訊，且不會擷取和編碼此資訊。值為 true 或 false。
-   **`user-agent`** - 搜索文件時傳送至伺服器的標頭。
-   **`method`** - 傳遞參數的方法（GET 或 POST）。
-   **`url-logging`** - 記載搜索的 URL 到何種程度。可能值如下：

    -   `full-logging` - 記載 URL 的所有相關資訊。
    -   `refined-logging` - 只記載瀏覽搜索器日誌並讓連接器正確運作所需的資訊；這是預設值。
    -   `minimal-logging` - 只記載讓連接器正確運作所需的最少資訊量。

    將此選項設定為 `minimal-logging` 將減少日誌的大小，而且由於與最大限度減少所要記載的資料量相關聯的 I/O 較少，因此效能會稍微增加。
-   **`ssl-version`** - 指定用於 HTTPS 連線的 SSL 版本。預設會使用最強大的通訊協定。

### 配置 CMIS 搜索種子

您可以為 CMIS 搜索種子檔配置下列值。若要設定這些值，請開啟 `config/seeds/cmis-seed.conf` 檔案，並修改您的使用案例特有的下列值：

-   **`url`** - 要作為搜索起點使用之 CMIS 儲存庫中的資料夾 URL，例如：`cmis://alfresco.test.com:8080/alfresco/cmisatom?folderToProcess-workspace://SpacesStore/guid`

    若要從根資料夾搜索，您需要提供如下的 URL：`cmis://alfresco.test.com:8080/alfresco/cmisatom?folderToProcess-`
-   **`at`** - 未使用的選項。
-   **`default-allow`** - 僅供內部使用。

## 配置 SMB/CIFS/Samba 搜索選項
{: #smb-cifs-samba-crawl-options}

Samba 連接器可讓您搜索「伺服器訊息區塊 (SMB)」及「共用網際網路檔案系統 (CIFS)」檔案共用。此類型的檔案共用在 Windows 網路上很常見，也可以透過開放程式碼專案 Samba 提供。

### 配置 Samba 連接器

下列是使用 Samba 連接器所需的基本配置選項。若要設定這些值，請開啟 `config/connectors/samba.conf` 檔案，並指定您的使用案例特有的下列值：

-   **`protocol`** - 用於搜索的連接器通訊協定的名稱。用來使用此連接器的值為 smb。
-   **`collection`** - 此屬性是用來解壓縮暫存檔。
-   **`classname`** - 連接器的 Java 類別名稱。用來使用此連接器的值必須是 `plugin:smb.plugin@connector`。
-   **`logging-config`** - 指定用於配置記載選項的檔案；必須以 `log4j` XML 字串的形式將它格式化。
-   **`username`** - 用來進行鑑別的 Samba 使用者名稱。如果提供，也必須提供網域和密碼。如果未提供，則使用來賓帳戶。
-   **`password`** - 用來進行鑑別的 Samba 密碼。如果提供使用者名稱，這是必要項目。必須使用「資料搜索器」隨附的 vcrypt 程式加密密碼。
-   **`archive`** - 讓 Samba 連接器可搜索及為保存檔內壓縮的檔案建立索引。值為 true 或 false；預設值為 false。
-   **`max-policies-per-handle`** - 指定可針對單一 RPC 控點開放的「本端安全權限 (LSA)」原則的數量上限。這些原則可定義在各種情況下查詢或修改特定系統所需的存取權。此選項的預設值為 255。
-   **`crawl-fs-metadata`** - 開啟此選項將導致「資料搜索器」新增一個 VXML 文件，其中包含關於該檔案的可用檔案系統 meta 資料（建立日期、前次修改日期、檔案屬性等）。
-   **`enable-arc-connector`** - 未使用的選項。
-   **`disable-indexes`** - 要停用的以換行區隔索引清單，這可會使搜索速度更快，例如：

    -   `disable-url-index`
    -   `disable-error-state-index`
    -   `disable-crawl-time-index`
-   **`exact-duplicates-hash-size`** - 設定用來解析確切複製的雜湊表大小。修改此數量時請務必小心。選取的值應該是質數，較大的大小可以提供更快速的查閱，但會需要更多的記憶體，而較小的大小可能會降低搜索速度，但實質上可減少記憶體用量。
-   **`user-agent`** - 未使用的選項。
-   **`timeout`** - 未用的選項
-   **`n-concurrent-requests`** - 將平行傳送至單一 IP 位址的要求數量。預設值是 `1`。
-   **`enqueue-persistence`** - 未使用的選項。

### 配置 Samba 搜索種子

您可以為 Samba 搜索種子檔配置下列值。若要設定這些值，請開啟 `config/seeds/samba-seed.conf` 檔案，並指定您的使用案例特有的下列值：

-   **`url`** - 要搜索的共用以換行區隔清單，例如：

    ```
    smb://share.test.com/office
    smb://share.test.com/cash/money/change
    smb://share.test.com/C$/Program Files
    ```
    {: codeblock}

-   **`hops`** - 僅供內部使用。
-   **`default-allow`** - 僅供內部使用。

## 配置 SharePoint 搜索選項
{: #sharepoint-crawl-options}

**重要事項：**SharePoint 連接器需要 Microsoft SharePoint Server 2007 (MOSS 2007)、SharePoint Server 2010、SharePoint Server 2013 或 SharePoint Online。

SharePoint 連接器可讓您搜索 SharePoint 物件，並檢索其包含的資訊。諸如文件、使用者設定檔、網站集合、部落格、清單項目、成員資格清單、目錄頁面等之類的物件，可以使用其相關聯的 meta 資料進行檢索。對於清單項目和文件，索引可以包括附件。

SharePoint 連接器會遵循所有 SharePoint 物件上的 `noindex` 屬性，而不論其特定類型為何（部落格、文件、使用者設定檔等）。系統會針對每一個結果傳回單一文件。
{: tip}

**重要事項：**您用來搜索 SharePoint 網站的 SharePoint 帳戶至少必須有完整的讀取權。

### 配置 SharePoint 連接器

下列是使用 SharePoint 連接器所需的基本配置選項。若要設定這些值，請開啟 `config/connectors/sharepoint.conf` 檔案，並修改您的使用案例特有的下列值：

-   **`protocol`** - 用於搜索的連接器通訊協定的名稱。用來使用此連接器的值是 `i-sp`。
-   **`collection`** - 此屬性是用來解壓縮暫存檔。
-   **`classname`** - 連接器的 Java 類別名稱。請對此連接器使用 `plugin:io-sharepoint.plugin@connector`。
-   **`logging-config`** - 指定用於配置記載選項的檔案；必須以 `log4j` XML 字串的形式將它格式化。
-   **`seed-url-type`** - 識別提供的種子 URL 指向的 SharePoint 物件的類型：網站集合或 Web 應用程式（亦稱為虛擬伺服器）。

    -   `網站集合` - 如果「種子 URL 類型」是設為「網站集合」，則只會搜索該 URL 所參照之網站集合的子項。
    -   `Web 應用程式` - 如果「種子 URL 類型」是設為 Web 應用程式，則會搜索屬於每個 URL 所參照之 Web 應用程式的所有網站集合（及其子項）。
-   **`auth-type`** - 聯絡 SharePoint 伺服器時要使用的鑑別機制：`BASIC`、`NTLM2`、`KERBEROS` 或 `CBA`。預設鑑別類型是 `NTLM2`。
-   **`spUser`** - 用來存取內容的 SharePoint 使用者的使用者名稱。此使用者必須可存取要搜索及建立索引的所有目標網站和清單，並且必須能擷取及解析相關聯的許可權。建議您使用網域名稱輸入它，像是：`MYDOMAIN\\Administrator`。
-   **`spPassword`** - 用來存取內容的 SharePoint 使用者的密碼。必須使用「資料搜索器」隨附的 vcrypt 程式加密密碼。
-   **`cba-sts`** - 用來嘗試對搜索使用者進行鑑別的「安全記號服務 (STS)」端點的 URL。對於 ADFS 的 SharePoint 內部部署，這應該是 ADFS 端點。如果「鑑別類型」設為 CBA（「宣告型鑑別」），則此為必要欄位。
-   **`cba-realm`** - 從 STS 要求安全記號時要使用的中繼方信任 ID。這有時稱為 "AppliesTo" 值，或「領域」。針對 SharePoint Online，這應該是 SharePoint Online 實例根目錄的 URL（例如，`https://mycompany.sharepoint.com`）。針對 ADFS，這是介於 SharePoint 與 ADFS 之間「依賴方信任」的 ID 值（例如，`"urn:SHAREPOINT:adfs"`）。
-   **`everyone-group`** - 若指定，在應該提供每個人存取時，會在 ACL 中使用此群組名稱。啟用搜索使用者設定檔時，這是必要欄位。

    **附註：**Retrieve and Rank 服務不會遵循安全。

-   **`user-profile-master-url`** - 連接器用來建置使用者設定檔鏈結的基礎 URL。應該配置此項目，以指向使用者設定檔的顯示表單。如果發現記號 `%FIRST_SEED%`，會將它以第一個種子 URL 取代。啟用搜索使用者設定檔時，這是必要欄位。
-   **`urls`** - 要搜索的 SharePoint Web 應用程式或網站集合的 HTTP URL 以換行區隔清單。
-   **`ehcache-config`** - 未使用的選項。
-   **`method`** - 將藉以傳遞參數的方法（`GET` 或 `POST`）。
-   **`cache-types`** - 未使用的選項。
-   **`cache-size`** - 未使用的選項。
-   **`enable-acl`** - 啟用 SharePoint 使用者設定檔的搜索；值為 `true` 或 `false`；預設值為 `false`。

### 配置 SharePoint 搜索種子

您可以為 SharePoint 搜索種子檔配置下列額外的值。若要設定這些值，請開啟 `config/seeds/sharepoint-seed.conf` 檔案，並指定您的使用案例特有的下列值：

-   **`url`** - 要搜索的 SharePoint Web 應用程式或網站集合之 URL 的換行區隔清單。例如：

    ```
    io-sp://a.com
    io-sp://b.com:83/site
    io-sp://c.com/site2
    ```
    {: codeblock}

    也會搜索這些網站的子網站（除非它們已由其他搜索規則排除）。

-   **`filter-url`** - 要搜索的 SharePoint Web 應用程式或網站集合之 URL 的換行區隔清單。例如：

    ```
    http://a.com
    http://b.com:83/site
    http://c.com/site2
    ```
    {: codeblock}

-   **`hops`** - 僅供內部使用。
-   **`n-concurrent-requests`** - 僅供內部使用。
-   **`delay`** - 僅供內部使用。
-   **`default-allow`** - 僅供內部使用。
-   **`seed-protocol`** - 設定網站集合子項的種子通訊協定。當網站集合的通訊協定是 SSL、HTTP 或 HTTPS 時為必要。此值必須設定為與網站集合的通訊協定相同。

## 配置 Box 搜索選項

「Box 連接器」可讓您搜索您的「企業 Box」實例，並將它所包含的資訊建立索引。

### 配置 Box 連接器

下列是使用 Box 連接器所需的基本配置選項。若要設定這些值，請開啟 `config/connectors/box.conf` 檔案，並修改您的使用案例特有的下列值：

-   **`protocol`** - 用於搜索的連接器通訊協定的名稱。用來使用此連接器的值是 `box`。
-   **`classname`** - 連接器的 Java 類別名稱。請對此連接器使用 `plugin:box.plugin@connector`。
-   **`logging-config`** - 指定用於配置記載選項的檔案；必須以 `log4j` XML 字串的形式將它格式化。
-   **`box-crawl-seed-url`** - Box 的基礎 URL。此連接器的值是 `box://app.box.com/`。

    您也可以搜索不同類型的 URL，例如：

    -   搜索整個企業：`box://app.box.com/`
    -   搜索特定資料夾：`box://app.box.com/user/USER_ID/folder/FOLDER_ID/FolderName`
    -   搜索特定使用者：`box://app.box.com/user/USER_ID/`
-   **`client-id`** - 輸入建立 Box 應用程式時 Box 所提供的用戶端 ID。
-   **`client-secret`** - 輸入建立 Box 應用程式時 Box 所提供的用戶端機密。
-   **`path-to-private-key`** - 這是在您的本端檔案系統上私密金鑰的位置，該金鑰屬於產生用來與 Box 進行通訊的私密-公開金鑰組的一部分。
-   **`kid`** - 指定公開金鑰 ID。這是為了與 Box 通訊而產生的私密-公開金鑰組的另一半。
-   **`enterprise-id`** - 應用程式獲得授權的企業。「企業 ID」會列在「Box 管理者主控台」的主頁面。
-   **`enable-acl`** - 僅供內部使用。啟用擷取已搜索資料的 ACL。
-   **`user-agent`** - 搜索文件時傳送至伺服器的標頭。
-   **`method`** - 將藉以傳遞參數的方法（`GET` 或 `POST`）。
-   **`url-logging`** - 記載搜索的 URL 到何種程度。可能值如下：

    -   `full-logging` - 記載 URL 的所有相關資訊。
    -   `refined-logging` - 只記載瀏覽搜索器日誌並讓連接器正確運作所需的資訊；這是預設值。
    -   `minimal-logging` - 只記載讓連接器正確運作所需的最少資訊量。

    將此選項設定為 `minimal-logging` 將減少日誌的大小，而且由於與最大限度減少所要記載的資料量相關聯的 I/O 較少，因此效能會稍微增加。
-   **`ssl-version`** - 指定用於 HTTPS 連線的 SSL 版本。預設會使用最強大的通訊協定。

### 配置 Box 搜索種子
{: #box-crawl-options}

可以為 Box 搜索種子檔配置下列其他值。若要設定這些值，請開啟 `config/seeds/box-seed.conf` 檔案，並指定您的使用案例特有的下列值：

-   **`URL`** - 要作為搜索起始點的 URL。預設值是 `box://app.box.com/`。
-   **`default-allow`** - 僅供內部使用。

## 限制

Box 連接器具有部分限制：

-   不會擷取檔案上的「評論」或「作業」。
-   會將附註內容主體擷取為 JSON。Notes 資料可能需要其他轉換。
-   無法透過 Test-It 擷取個別文件。只有種子 URL、「資料夾 URL」和「使用者 URL」可以透過 Test-It 擷取。
