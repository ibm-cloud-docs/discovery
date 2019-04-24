---

copyright:
  years: 2015, 2017, 2019
lastupdated: "2019-04-24"

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

# Configuring connector and seed options
{: #configuring-connector-and-seed-options}

The Data Crawler is no longer supported or available for download beginning [17 April 2019](/docs/services/discovery?topic=discovery-release-notes#17apr19). This content is provided for existing installations only. See [Connecting to Data Sources](/docs/services/discovery?topic=discovery-sources#sources) for other available connectivity options.
{:important}

When crawling data, the Crawler first identifies the type of data repository (connector) and the user-specified starting location (seed) to begin downloading information.
{: shortdesc}

**Important:** When using the Data Crawler, data repository security settings are ignored.

Seeds are the starting points of a crawl, and are used by the Data Crawler to retrieve data from the resource that is identified by the connector. Typically, seeds configure URLs to access protocol-based resources such as fileshares, SMB shares, databases, and other data repositories that are accessible by various protocols. Moreover, different seed URLs have different capabilities. Seeds can also be repository-specific, to enable crawling of specific third-party applications such as customer relationship management (CRM) systems, product life cycle (PLC) systems, content management systems (CMS), cloud-based applications, and web database applications.

To crawl your data correctly, you must ensure that the Crawler is properly configured to read your data repository. The Data Crawler provides connectors to support data collection from the following repositories:

-   [Filesystem](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-filesystem-crawl-options)
-   [Databases, via JDBC](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-database-crawl-options)
-   [CMIS (Content Management Interoperability Services)](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-cmis-crawl-options)
-   [SMB (Server Message Block), CIFS (Common Internet Filesystem), or Samba fileshares](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#smb-cifs-samba-crawl-options)

A connector configuration template is also provided, which allows you to customize a connector.

To configure your connector do the following:

1.  Open the file in the `connectors` directory that corresponds to the repository you are connecting to (for example `filesystem.conf` is the configuration file for the filesystem connector) in a text editor.

1.  Modify the values that are appropriate to your repository:

    -   [Filesystem](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#filesystem-crawl-options)
    -   [Databases, via JDBC](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#database-crawl-seed)
    -   [CMIS (Content Management Interoperability Services)](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#cmis-crawl-options)
    -   [SMB (Server Message Block), CIFS (Common Internet Filesystem), or Samba fileshares](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#smb-cifs-samba-crawl-options)
1.  Save and close the file.
1.  Repeat for the `-seed.conf` file in the `connectors/seeds` directory that corresponds to the repository you are connecting to (for example `filesystem-seed.conf` is the seed (where to connect to) configuration file for the filesystem connector) in a text editor.
1.  Proceed to [configuring the Data Crawler to connect to {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-the-data-crawler).

To access the in-product manual for the connector and seed configuration files, with the most up-to-date information, type the following commands from the Crawler installation directory:
-   For connector configuration options:
    ```bash
    man crawler-options.conf
    ```
    {: pre}
-   For crawl seed configuration options:
    ```bash
    man crawler-seed.conf
    ```
    {: pre}


## Configuring filesystem crawl options
{: #filesystem-crawl-options}

The filesystem connector allows you to crawl files local to the Data Crawler installation.

Another option to upload large numbers of files into {{site.data.keyword.discoveryshort}} is [discovery-files ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM/discovery-files){: new_window} on GitHub.
{: note}

### Configuring the filesystem connector
{: #filesystem-connector}

Following are the basic configuration options that are required to use the filesystem connector. To set these values, open the file `config/connectors/filesystem.conf`, and modify the following values specific to your use cases:

-   **`protocol`** - The name of the connector protocol used for the crawl. Use `sdk-fs` for this connector.
-   **`collection`** - This attribute is used to unpack temporary files. The default value is `crawler-fs`
-   **`logging-config`** - Specifies the file used for configuring logging options; it must be formatted as a `log4j` XML string.
-   **`classname`** - Java class name for the connector. The value to use this connector must be `plugin:filesystem.plugin@filesystem`.

### Configuring the filesystem crawl seed
{: #filesystem-crawl-seed}

The following values can be configured for the filesystem crawl seed file. To set these values, open the file `config/seeds/filesystem-seed.conf` and specify the following values specific to your use cases:

-   **`url`** - Newline-separated list of files and folders to crawl. UNIX users can use a path such as `/usr/local/`.

    **Note:** The URLs must start with `sdk-fs://`. So to crawl, for example, `/home/watson/mydocs`, the value of this URL would be `sdk-fs:///home/watson/mydocs` - the third `/` is necessary!

    The filesystems used by Linux, UNIX, and UNIX-like computer systems can contain special types of files, such as block and character device nodes and files that represent named pipes, which cannot be crawled because they do not contain data, but serve as device or I/O access points. Attempting to crawl such files will generate errors during the crawl. To avoid such errors, you should exclude the `/dev` directory in any top-level crawl on a Linux, UNIX, or UNIX-like filesystem. If present on the system that you are crawling, you should also exclude temporary system directories such as `/proc`, `/sys`, and `/tmp`, that contain transient files and system information.   **`hops`** - Internal use only.   **`default-allow`** - Internal use only.
    {: tip}

## Configuring Database crawl options
{: #database-crawl}

The database connector allows you to crawl a database by executing a custom SQL command and creating one document per row (record) and one content element per column (field). You can specify a column to be used as a unique key, as well as a column containing a timestamp representing the last-modification date of each record. The connector retrieves all records from the specified database, and can also be restricted to specific tables, joins, and so on in the SQL statement.

The Database connector allows you to crawl the following databases:

-   {{site.data.keyword.IBM}} DB2
-   MySQL
-   Oracle PostgreSQL
-   Microsoft SQL Server
-   Sybase
-   Other SQL-compliant databases, via a JDBC 3.0-compliant driver

The connector retrieves all records from the specified database and table.

***JDBC Drivers*** - The Database connector ships with Oracle JDBC (Java Database Connectivity) driver version 1.5. All third-party JDBC drivers shipped with the Data Crawler are located in the `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` directory of your Data Crawler installation, where you can add, remove, and modify them as necessary. You can also use the `extra_jars_dir` setting in the `crawler.conf` file to specify another location.

***DB2 JDBC Drivers*** - The Data Crawler does not ship with the JDBC drivers for DB2 due to licensing issues. However, all DB2 installations in which you have installed JDBC support include the JAR files that the Data Crawler requires, in order to be able to crawl a DB2 installation. To crawl a DB2 instance, you must copy these files into the appropriate directory in your Data Crawler installation so that the Database connector can use them. To enable the Data Crawler to crawl a DB2 installation, locate the `db2jcc.jar` and license (typically, `db2jcc_license_cu.jar`) JAR files in your DB2 installation, and copy those files to the `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` subdirectory of your Data Crawler installation directory, or you can use the `extra_jars_dir` setting in the `crawler.conf` file to specify another location.

***MySQL JDBC Drivers*** - The Data Crawler does not ship with the JDBC drivers for MySQL because of possible license issues if they were delivered as part of the product. However, downloading the JAR file that contains the MySQL JDBC drivers and integrating that JAR file into your Data Crawler installation is quite easy to do:

1.  Use a web browser to visit the MySQL download site, and locate the source and binary download link for the archive format that you want to use (typically zip for Microsoft Windows systems or a gzipped tarball for Linux systems). Click that link to initiate the download process. Registration may be required.
1.  Use the appropriate unzip archive-file-name or tar zxf archive-file-name command to extract the contents of that archive, based on the type and name of the archive file that you download.
1.  Change to the directory that was extracted from the archive file, and copy the JAR file from this directory to the `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` subdirectory of your Data Crawler installation directory, or you can use the `extra_jars_dir` setting in the `crawler.conf` file to specify another location.

### Configuring the Database Connector
{: #database-connector}

Following are the basic configuration options that are required to use the Database connector. To set these values, open the file config/connectors/database.conf and modify the following values specific to your use cases:

-   **`protocol`** - The name of the connector protocol used for the crawl. The value for this connector is based on the database system to be accessed.
-   **`collection`** - This attribute is used to unpack temporary files.
-   **`classname`** - Java class name for the connector. The value to use this connector must be `plugin:database.plugin@database`.
-   **`logging-config`** - Specifies the file used for configuring logging options; it must be formatted as a `log4j` XML string.

### Configuring the Database Crawl Seed
{: #database-crawl-seed}

The following values can be configured for the Database crawl seed file. To set these values, open the file `config/seeds/database-seed.conf` and specify the following values specific to your use cases:

-   **`url`** - The URL of the table or view to retrieve. Defines your custom SQL database seed URL. The structure is:

    -   `database-system://host:port/database?[per=num]&[sql=SQL]`

    Testing a seed URL will show all of the enqueued URLs. For example, testing the following URL for a database containing 200 records:
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?per=100&sql=select%20*%20from%20vessel&`

    shows the following enqueued URLs:
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=0&`
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=100&`
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=200&`

    While testing the following URL will show the data retrieved from row 43:
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?per-1&key-val=43`
-   **`hops`** - Internal use only.
-   **`default-allow`** - Internal use only.
-   **`user-password`** - Credentials for the database system. The username and password need to be separated by a `:`, and the password must be encrypted using the vcrypt program shipped with the Data Crawler. For example: `username:[[vcrypt/3]]passwordstring`
-   **`max-data-size`** - Maximum size of the data for a document. This is the largest block of memory that will be loaded at one time. Only increase this limit if you have sufficient memory on your computer.
-   **`filter-exact-duplicates`** - Internal use only.
-   **`timeout`** - Internal use only.
-   **`jdbc-class`** (Extender option) - When specified, this string will override the JDBC class used by the connector when `(other)` is chosen as the database system.
-   **`connection-string`** (Extender option) - When specified, this string will override the automatically generated JDBC connection string. This allows you to provide more detailed configuration about the database connection, such as load-balancing or SSL connections. For example: `jdbc:netezza://127.0.0.1:5480/databasename`
-   **`save-frequency-for-resume`** (Extender option) - Specifies the name of a column or associated label, in order to be able to resume a crawl or do a partial refresh. The seed saves the name of this column at regular intervals as it proceeds with the crawl, and saves it again once the last row of your database has been crawled. When resuming the crawl or refreshing it, the crawl begins with the row that is identified in the saved value for this field

## Configuring CMIS crawl options
{: #cmis-crawl-options}

The CMIS (Content Management Interoperability Services) connector lets you crawl CMIS-enabled CMS (Content Management System) repositories, such as Alfresco, Documentum or {{site.data.keyword.IBM}} Content Manager, and index the data that they contain.

### Configuring the CMIS Connector
{: #cmis-connector}

Following are the basic configuration options that are required to use the CMIS connector. To set these values, open the file `config/connectors/cmis.conf` and specify the following values specific to your use cases:

-   **`protocol`** - The name of the connector protocol used for the crawl. The value to use this connector must be `cmis`.
-   **`collection`** - This attribute is used to unpack temporary files.
-   **`dns`** - Unused option.
-   **`classname`** - Java class name for the connector. Use `plugin:cmis-v1.1.plugin@connector` for this connector.
-   **`logging-config`** - Specifies the file used for configuring logging options; it must be formatted as a `log4j` XML string.
-   **`endpoint`** - The service endpoint URL of a CMIS-compliant repository. 
-   **`username`** - The user name of the CMIS repository user used to access the content. This user must have access to all the target folders and documents to be crawled and indexed.
-   **`password`** - Password of the CMIS repository used to access the content. Password must NOT be encrypted; it should be given in plain text.
-   **`repositoryid`** - The ID of the CMIS repository used to access the content for that specific repository.
-   **`bindingtype`** - Identifies what type of binding is to be used to connect to a CMIS repository. Value is either AtomPub or WebServices.
-   **`authentication`** - Identifies what type of authentication mechanism to use while contacting a CMIS-compatible repository: Basic HTTP Authentication, NTLM, or WS-Security(Username token).
-   **`enable-acl`** - Enables retrieving ACLs for crawled data. If you are not concerned about security for the documents in this collection, disabling this option will increase performance by not requesting this information with the document and not retrieving and encoding this information. Value is either true or false.
-   **`user-agent`** - A header sent to the server when crawling documents.
-   **`method`** - The method (GET or POST) by which parameters will be passed.
-   **`url-logging`** - The extent to which crawled URLs are logged. Possible values are:

    -   `full-logging` - Log all information about the URL.
    -   `refined-logging` - Only log the information necessary to browse the crawler log and for the connector to function correctly; this is the default value.
    -   `minimal-logging` - Only log the minimum amount of information necessary for the connector to function correctly.

    Setting this option to `minimal-logging` will reduce the size of the logs and gain a slight performance increase due to the smaller I/O associated with minimizing the amount of data that is being logged.
-   **`ssl-version`** - Specifies a version of SSL to use for HTTPS connections. By default the strongest protocol available is used.

### Configuring the CMIS Crawl Seed
{: #cmis-crawl-seed}

The following values can be configured for the CMIS crawl seed file. To set these values, open the file `config/seeds/cmis-seed.conf` and modify the following values specific to your use cases:

-   **`url`** - The URL of a folder from the CMIS repository to be used as a starting point of the crawl, for example: `cmis://alfresco.test.com:8080/alfresco/cmisatom?folderToProcess-workspace://SpacesStore/guid`

    To crawl from the root folder, you need to give the URL as: `cmis://alfresco.test.com:8080/alfresco/cmisatom?folderToProcess-`
-   **`at`** - Unused option.
-   **`default-allow`** - Internal use only.

## Configuring SMB/CIFS/Samba crawl options
{: #smb-cifs-samba-crawl-options}

The Samba connector allows you to crawl Server Message Block (SMB) and Common Internet filesystem (CIFS) fileshares. This type of fileshare is common on Windows networks, and is also provided through the open source project Samba.

### Configuring the Samba Connector
{: #smb-cifs-samba-crawl-connector}

Following are the basic configuration options that are required to use the Samba connector. To set these values, open the file `config/connectors/samba.conf` and specify the following values specific to your use cases:

-   **`protocol`** - The name of the connector protocol used for the crawl. The value to use this connector is smb.
-   **`collection`** - This attribute is used to unpack temporary files.
-   **`classname`** - Java class name for the connector. The value to use this connector must be `plugin:smb.plugin@connector`.
-   **`logging-config`** - Specifies the file used for configuring logging options; it must be formatted as a `log4j` XML string.
-   **`username`** - The Samba username to authenticate with. If provided, domain and password must also be provided. If not provided, the guest account is used.
-   **`password`** - The Samba password to authenticate with. If the username is provided, this is required. Password must be encrypted using the vcrypt program shipped with the Data Crawler.
-   **`archive`** - Enables the Samba connector to crawl and index files that are compressed within archive files. Value is either true or false; default value is false.
-   **`max-policies-per-handle`** - Specifies the maximum number of Local Security Authority (LSA) policies that can be opened for a single RPC handle. These policies define the access permissions that are required to query or modify a particular system under various conditions. The default value for this option is 255.
-   **`crawl-fs-metadata`** - Turning on this option will cause the Data Crawler to add a VXML document containing the available filesystem metadata about the file (creation date, last modified date, file attributes, etc.).
-   **`enable-arc-connector`** - Unused option.
-   **`disable-indexes`** - Newline-separated list of indexes to disable, which may result in a faster crawl, for example:

    -   `disable-url-index`
    -   `disable-error-state-index`
    -   `disable-crawl-time-index`
-   **`exact-duplicates-hash-size`** - Sets the size of the hash table used for resolving exact duplicates. Be very careful when modifying this number. The value that you select should be prime, and larger sizes can provide faster lookups but will require more memory, while smaller sizes can slow down crawls but will substantially reduce memory usage.
-   **`user-agent`** - Unused option.
-   **`timeout`** - Unused option
-   **`n-concurrent-requests`** - The number of requests that will be sent in parallel to a single IP address. The default is `1`.
-   **`enqueue-persistence`** - Unused option.

### Configuring the Samba Crawl Seed
{: #smb-cifs-samba-crawl-seed}

The following values can be configured for the Samba crawl seed file. To set these values, open the file `config/seeds/samba-seed.conf` and specify the following values specific to your use cases:

-   **`url`** - A newline-separated list of shares to crawl, for example:

    ```
    smb://share.test.com/office
    smb://share.test.com/cash/money/change
    smb://share.test.com/C$/Program Files
    ```
    {: codeblock}

-   **`hops`** - Internal use only.
-   **`default-allow`** - Internal use only.