---

copyright:
  years: 2015, 2017, 2019
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

# 配置連接器和種子選項
{: #configuring-connector-and-seed-options}

搜索資料時，「搜索器」會先識別資料儲存庫的類型（連接器），以及使用者指定的起始位置（種子）來開始下載資訊。
{: shortdesc}

「資料搜索器」應該只用來搜索檔案共用或資料庫，針對所有其他用途，您應使用適當的 {{site.data.keyword.discoveryshort}} 連接器。如需詳細資訊，請參閱[連接至資料來源](/docs/services/discovery?topic=discovery-sources#sources)。如果您將「資料搜索器」用於 {{site.data.keyword.discoveryshort}} 連接器支援的資料來源，則不再為其提供協助。
{: important}

**重要事項：**使用「資料搜索器」時，會忽略資料儲存庫安全設定。

種子是搜索的起點，「資料搜索器」會使用它從連接器所識別的資源擷取資料。一般而言，種子會配置 URL 以存取通訊協定型資源，例如檔案共用、SMB 共用、資料庫，以及可由各種通訊協定存取的其他資料儲存庫。此外，不同的種子 URL 會有不同的功能。種子也可以是儲存庫特定，以啟用特定協力廠商應用程式（例如客戶關係管理 (CRM) 系統、產品生命週期 (PLC) 系統、內容管理系統 (CMS)、雲端型應用程式及 Web 資料庫應用程式）的搜索。

若要正確地搜索資料，您必須確定「搜索器」已適當配置為讀取資料儲存庫。「資料搜索器」提供連接器來支援從下列儲存庫進行資料收集：

-   [檔案系統](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-filesystem-crawl-options)
-   [資料庫，透過 JDBC](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-database-crawl-options)
-   [CMIS（內容管理交互作業能力服務）](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-cmis-crawl-options)
-   [SMB（伺服器訊息區塊）、CIFS（一般網際網路檔案系統）或 Samba 檔案共用](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#smb-cifs-samba-crawl-options)

也會提供連接器配置範本，可讓您自訂連接器。

若要配置連接器，請執行下列動作：

1.  在文字編輯器中，開啟 `connectors` 目錄中對應於所連接儲存庫的檔案（例如，`filesystem.conf` 是檔案系統連接器的配置檔）。

1.  修改儲存庫所適用的值：

    -   [檔案系統](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#filesystem-crawl-options)
    -   [資料庫，透過 JDBC](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#database-crawl-seed)
    -   [CMIS（內容管理交互作業能力服務）](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#cmis-crawl-options)
    -   [SMB（伺服器訊息區塊）、CIFS（一般網際網路檔案系統）或 Samba 檔案共用](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#smb-cifs-samba-crawl-options)
1.  儲存並關閉檔案。
1.  在文字編輯器中，針對 `connectors/seeds` 目錄中對應於您要連接之儲存庫的 `-seed.conf` 檔案重複執行（例如，`filesystem-seed.conf` 是檔案系統連接器的種子（即連接目的地）配置檔）。
1.  繼續[配置資料搜索器以連接至 {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-the-data-crawler)。

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

將大量檔案上傳至 {{site.data.keyword.discoveryshort}} 的另一個選項，就是 GitHub 上的 [discovery-files ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/IBM/discovery-files){: new_window}。
{: note}

### 配置檔案系統連接器
{: #filesystem-connector}

下列是使用檔案系統連接器所需的基本配置選項。若要設定這些值，請開啟 `config/connectors/filesystem.conf` 檔案，並修改您的使用案例特有的下列值：

-   **`protocol`** - 用於搜索的連接器通訊協定的名稱。對此連接器使用 `sdk-fs`。
-   **`collection`** - 此屬性是用來解壓縮暫存檔。預設值為 `crawler-fs`
-   **`logging-config`** - 指定用於配置記載選項的檔案；必須以 `log4j` XML 字串的形式將它格式化。
-   **`classname`** - 連接器的 Java 類別名稱。用來使用此連接器的值必須是 `plugin:filesystem.plugin@filesystem`。

### 配置檔案系統搜索種子
{: #filesystem-crawl-seed}

可以針對檔案系統搜索種子檔配置下列值。若要設定這些值，請開啟 `config/seeds/filesystem-seed.conf` 檔案，並指定您的使用案例特有的下列值：

-   **`url`** - 要搜索的檔案與資料夾以換行區隔清單。UNIX 使用者可以使用 `/usr/local/` 之類的路徑。

    **附註：**URL 必須以 `sdk-fs://` 為開頭。因此比方說，若要搜索 `/home/watson/mydocs`，此 URL 的值會是 `sdk-fs:///home/watson/mydocs` - 第三個 `/` 是必要的！

    Linux、UNIX 及 UNIX 型電腦系統所使用的檔案系統可包含特殊類型的檔案，例如，代表具名管道的區塊和字元裝置節點及檔案，因為它們不包含資料，而是作為裝置或 I/O 存取點，因此無法進行搜索。試圖搜索這類檔案將在搜索期間產生錯誤。若要避免這類錯誤，您應該在 Linux、UNIX 或 UNIX 型檔案系統的任何最上層搜索中排除 `/dev` 目錄。如果您要搜索的系統上有諸如 `/proc`、`/sys` 及 `/tmp` 之類的暫存系統目錄（其包含暫時性檔案和系統資訊），則您也應該除排它們。**`hops`** - 僅供內部使用。**`default-allow`** - 僅供內部使用。
    {: tip}

## 配置資料庫搜索選項
{: #database-crawl}

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
{: #database-connector}

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
{: #cmis-connector}

下列是使用 CMIS 連接器所需的基本配置選項。若要設定這些值，請開啟 `config/connectors/cmis.conf` 檔案，並指定您的使用案例特有的下列值：

-   **`protocol`** - 用於搜索的連接器通訊協定的名稱。用來使用此連接器的值必須是 `cmis`。
-   **`collection`** - 此屬性是用來解壓縮暫存檔。
-   **`dns`** - 未使用的選項。
-   **`classname`** - 連接器的 Java 類別名稱。對此連接器使用 `plugin:cmis-v1.1.plugin@connector`。
-   **`logging-config`** - 指定用於配置記載選項的檔案；必須以 `log4j` XML 字串的形式將它格式化。
-   **`endpoint`** - CMIS 相容儲存庫的服務端點 URL。 
-   **`username`** - 用來存取內容的 CMIS 儲存庫使用者的使用者名稱。此使用者必須有權存取要搜索及建立索引的所有目標資料夾和文件。
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
{: #cmis-crawl-seed}

您可以為 CMIS 搜索種子檔配置下列值。若要設定這些值，請開啟 `config/seeds/cmis-seed.conf` 檔案，並修改您的使用案例特有的下列值：

-   **`url`** - 要作為搜索起點使用之 CMIS 儲存庫中的資料夾 URL，例如：`cmis://alfresco.test.com:8080/alfresco/cmisatom?folderToProcess-workspace://SpacesStore/guid`

    若要從根資料夾搜索，您需要提供如下的 URL：`cmis://alfresco.test.com:8080/alfresco/cmisatom?folderToProcess-`
-   **`at`** - 未使用的選項。
-   **`default-allow`** - 僅供內部使用。

## 配置 SMB/CIFS/Samba 搜索選項
{: #smb-cifs-samba-crawl-options}

Samba 連接器可讓您搜索「伺服器訊息區塊 (SMB)」及「共用網際網路檔案系統 (CIFS)」檔案共用。此類型的檔案共用在 Windows 網路上很常見，也可以透過開放程式碼專案 Samba 提供。

### 配置 Samba 連接器
{: #smb-cifs-samba-crawl-connector}

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
{: #smb-cifs-samba-crawl-seed}

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
