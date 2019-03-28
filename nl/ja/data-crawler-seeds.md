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

# コネクターとシードのオプションの構成
{: #configuring-connector-and-seed-options}

データをクロールするとき、情報のダウンロードを開始するために、Crawler はまず、データ・リポジトリーのタイプ (コネクター) とユーザー指定の開始位置 (シード) を識別します。
{: shortdesc}

Data Crawler は、ファイル共有またはデータベースをクロールする場合にのみ使用してください。それ以外の場合は、適切な {{site.data.keyword.discoveryshort}} コネクターを使用してください。詳しくは、『[データ・ソースへの接続](/docs/services/discovery?topic=discovery-sources#sources)』を参照してください。 {{site.data.keyword.discoveryshort}} コネクターでサポートされているデータ・ソースで Data Crawler を使用する場合、Data Crawler に対する支援は行われなくなりました。
{: important}

**重要:** Data Crawler を使用する場合、データ・リポジトリーのセキュリティー設定は無視されます。

シードはクロールの開始点で、Data Crawler が、コネクターによって識別されたリソースからデータを取得するために使用します。 通常、シードは、各種プロトコルでアクセス可能なファイル共有、SMB 共有、データベース、その他のデータ・リポジトリーなど、プロトコル・ベースのリソースにアクセスするための URL を構成します。 さらに、各種のシード URL には、それぞれ異なる機能があります。 シードをリポジトリー固有にして、特定のサード・パーティー・アプリケーション (カスタマー・リレーションシップ・マネジメント (CRM) システム、製品ライフサイクル (PLC) システム、コンテンツ管理システム (CMS)、クラウド・ベースのアプリケーション、および Web データベース・アプリケーションなど) をクロールできるようにすることも可能です。

データを正しくクロールするには、データ・リポジトリーを読み取るために Crawler を適切に構成する必要があります。 Data Crawler には、以下のリポジトリーからのデータ収集をサポートするコネクターが用意されています。

-   [ファイル・システム](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-filesystem-crawl-options)
-   [データベース (JDBC 経由)](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-database-crawl-options)
-   [CMIS (Content Management Interoperability Services)](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-cmis-crawl-options)
-   [SMB (Server Message Block)、CIFS (Common Internet Filesystem)、Samba のファイル共有](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#smb-cifs-samba-crawl-options)

コネクターをカスタマイズできるコネクター構成テンプレートも用意されています。

コネクターを構成するには、次のようにします。

1.  接続先のリポジトリーに対応する `connectors` ディレクトリー内のファイル (例えば、`filesystem.conf` は、ファイル・システム・コネクターの構成ファイル) をテキスト・エディターで開きます。

1.  ご使用のリポジトリーに合わせて値を変更します。

    -   [ファイル・システム](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#filesystem-crawl-options)
    -   [データベース (JDBC 経由)](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#database-crawl-seed)
    -   [CMIS (Content Management Interoperability Services)](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#cmis-crawl-options)
    -   [SMB (Server Message Block)、CIFS (Common Internet Filesystem)、Samba のファイル共有](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#smb-cifs-samba-crawl-options)
1.  ファイルを保存して閉じます。
1.  接続先のリポジトリーに対応する `connectors/seeds` ディレクトリー内の `-seed.conf` ファイル (例えば、`filesystem-seed.conf` はファイル・システム・コネクターのシード (接続先の場所) 構成ファイル) について、テキスト・エディターで同様の処理を繰り返します。
1.  [{{site.data.keyword.discoveryshort}} に接続するための Data Crawler の構成](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-the-data-crawler)に進みます。

最新情報が含まれているコネクターとシードの構成ファイルの製品内マニュアルにアクセスするには、Crawler インストール・ディレクトリーから次のコマンドを入力します。
-   コネクター構成オプションの場合:
    ```bash
    man crawler-options.conf
    ```
    {: pre}
-   クロール・シード構成オプションの場合:
    ```bash
    man crawler-seed.conf
    ```
    {: pre}


## ファイル・システム・クロール・オプションの構成
{: #filesystem-crawl-options}

ファイル・システム・コネクターを使用すると、Data Crawler インストール済み環境にローカルのファイルをクロールできます。

多数のファイルを {{site.data.keyword.discoveryshort}} にアップロードするもう 1 つの方法は、GitHub 上の [discovery-files ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/IBM/discovery-files){: new_window} です。
{: note}

### ファイル・システム・コネクターの構成
{: #filesystem-connector}

以下に、ファイル・システム・コネクターを使用する際に必要な基本構成オプションを示します。 これらの値を設定するには、`config/connectors/filesystem.conf` ファイルを開き、それぞれのユース・ケースに合わせて以下の値を変更します。

-   **`protocol`** - クロールに使用するコネクター・プロトコルの名前。 このコネクターには、`sdk-fs` を使用します。
-   **`collection`** - この属性は、一時ファイルの解凍に使用します。 デフォルト値は `crawler-fs` です。
-   **`logging-config`** - ロギング・オプションの構成に使用するファイルを指定します。これは、`log4j` XML ストリングとしてフォーマット設定する必要があります。
-   **`classname`** - コネクターの Java クラス名。 このコネクターを使用する場合の値は、`plugin:filesystem.plugin@filesystem` でなければなりません。

### ファイル・システム・クロール・シードの構成
{: #filesystem-crawl-seed}

以下に、ファイル・システム・クロール・シード・ファイル用に構成できる値を示します。 これらの値を設定するには、`config/seeds/filesystem-seed.conf` ファイルを開き、それぞれのユース・ケースに合わせて以下の値を指定します。

-   **`url`** - クロールするファイルとフォルダーの改行で区切られたリスト。 UNIX ユーザーは、`/usr/local/` などのパスを使用できます。

    **注:** URL は `sdk-fs://` で始める必要があります。 したがって、例えば、`/home/watson/mydocs` をクロールするには、この URL の値は `sdk-fs:///home/watson/mydocs` になります。3 番目の `/` が必要です。

    Linux、UNIX、UNIX 系の各コンピューター・システムで使用されるファイル・システムは、ブロック・デバイスおよびキャラクター型デバイスのノードや、名前付きパイプを表すファイルなど、特殊なファイル・タイプを含む可能性があります。これらはデータを含まないためクロールできませんが、デバイスまたは入出力アクセス・ポイントとして機能します。 このようなファイルをクロールしようとすると、クロール中にエラーが生成されます。 このようなエラーを回避するには、Linux、UNIX、または UNIX 系のファイル・システム上のすべての最上位クロールで `/dev` ディレクトリーを除外する必要があります。 クロール中のシステムに、一過性のファイルやシステム情報が含まれている一時システム・ディレクトリー (`/proc`、`/sys`、`/tmp` など) が存在する場合は、これらを除外することも必要です。   **`hops`** - 内部使用のみ。   **`default-allow`** - 内部使用のみ。
    {: tip}

## データベース・クロール・オプションの構成
{: #database-crawl}

データベース・コネクターを使用すると、カスタム SQL コマンドを実行して、行 (レコード) ごとに 1 つの文書、および列 (フィールド) ごとに 1 つのコンテンツ・要素を作成することにより、データベースをクロールできます。 固有キーとして使用する列のほかに、各レコードの最終変更日を表すタイム・スタンプを含む列も指定できます。 このコネクターは、指定したデータベースからすべてのレコードを取得します。また、このコネクターを SQL ステートメント内の特定のテーブル、結合などに制限することもできます。

データベース・コネクターを使用すると、以下のデータベースをクロールできます。

-   {{site.data.keyword.IBM}} DB2
-   MySQL
-   Oracle PostgreSQL
-   Microsoft SQL Server
-   Sybase
-   その他の SQL 準拠のデータベース (JDBC 3.0 準拠のドライバーを経由)

このコネクターは、指定したデータベースとテーブルからすべてのレコードを取得します。

***JDBC ドライバー*** - データベース・コネクターは、Oracle JDBC (Java Database Connectivity) ドライバーのバージョン 1.5 に付属しています。 Data Crawler に付属のサード・パーティー JDBC ドライバーは、すべて、Data Crawler インストール済み環境の `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` ディレクトリーにあります。このディレクトリーで、これらのドライバーを必要に応じて追加、削除、変更できます。 `crawler.conf` ファイル内の `extra_jars_dir` 設定を使用して、別の場所を指定することもできます。

***DB2 JDBC ドライバー*** - ライセンスの問題により、Data Crawler には、DB2 用の JDBC ドライバーは付属していません。 ただし、JDBC サポートがインストールされているすべての DB2 インストール済み環境には、Data Crawler が DB2 インストール済み環境をクロールできるようにするために必要な JAR ファイルが含まれています。 DB2 インスタンスをクロールするには、Data Crawler インストール済み環境内の該当するディレクトリーにこれらのファイルをコピーして、データベース・コネクターでこれらのファイルを使用できるようにする必要があります。 Data Crawler で DB2 インストール済み環境をクロールできるようにするには、DB2 インストール済み環境内で `db2jcc.jar` とライセンス (通常は `db2jcc_license_cu.jar`) JAR ファイルを見つけ、これらのファイルを Data Crawler インストール・ディレクトリーの `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` サブディレクトリーにコピーします。あるいは、`crawler.conf` ファイル内の `extra_jars_dir` 設定を使用して、別の場所を指定できます。

***MySQL JDBC ドライバー*** - 製品の一部として配布された場合にライセンスの問題が生じる可能性があるため、Data Crawler には MySQL 用の JDBC ドライバーは付属していません。 ただし、以下のように、MySQL JDBC ドライバーが含まれている JAR ファイルをダウンロードして、その JAR ファイルを Data Crawler インストール済み環境に統合するのは、極めて簡単です。

1.  Web ブラウザーを使用して MySQL のダウンロード・サイトにアクセスし、使用するアーカイブ形式 (通常、Microsoft Windows システムの場合は zip、Linux システムの場合は gzip された tarball) のソースとバイナリーのダウンロード・リンクを見つけます。 そのリンクをクリックすると、ダウンロード・プロセスが開始されます。 登録が必要な場合があります。
1.  該当する unzip archive-file-name コマンドまたは tar zxf archive-file-name コマンドを使用し、ダウンロードしたアーカイブ・ファイルのタイプと名前に基づいて、そのアーカイブの内容を解凍します。
1.  アーカイブ・ファイルから解凍したディレクトリーに移動し、このディレクトリーから Data Crawler インストール・ディレクトリーの `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` サブディレクトリーへ、JAR ファイルをコピーします。あるいは、`crawler.conf` ファイル内の `extra_jars_dir` 設定を使用して、別の場所を指定できます。

### データベース・コネクターの構成
{: #database-connector}

以下に、データベース・コネクターを使用する際に必要な基本構成オプションを示します。 これらの値を設定するには、config/connectors/database.conf ファイルを開き、それぞれのユース・ケースに合わせて以下の値を変更します。

-   **`protocol`** - クロールに使用するコネクター・プロトコルの名前。 このコネクターの値は、アクセスするデータベース・システムに基づいています。
-   **`collection`** - この属性は、一時ファイルの解凍に使用します。
-   **`classname`** - コネクターの Java クラス名。 このコネクターを使用する場合の値は、`plugin:database.plugin@database` でなければなりません。
-   **`logging-config`** - ロギング・オプションの構成に使用するファイルを指定します。これは、`log4j` XML ストリングとしてフォーマット設定する必要があります。

### データベース・クロール・シードの構成
{: #database-crawl-seed}

以下に、データベース・クロール・シード・ファイル用に構成できる値を示します。 これらの値を設定するには、`config/seeds/database-seed.conf` ファイルを開き、それぞれのユース・ケースに合わせて以下の値を指定します。

-   **`url`** - 取得するテーブルまたはビューの URL。 カスタムの SQL データベース・シード URL を定義します。 構造は次のとおりです。

    -   `database-system://host:port/database?[per=num]&[sql=SQL]`

    シード URL をテストすると、エンキューされた URL がすべて表示されます。 例えば、次のような、200 のレコードが含まれているデータベースの URL をテストします。
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?per=100&sql=select%20*%20from%20vessel&`

    エンキューされた以下の URL が表示されます。
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=0&`
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=100&`
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=200&`

    一方、次の URL をテストすると、行 43 から取得したデータが表示されます。
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?per-1&key-val=43`
-   **`hops`** - 内部使用のみ。
-   **`default-allow`** - 内部使用のみ。
-   **`user-password`** - データベース・システムの資格情報。 ユーザー名とパスワードは `:` で区切る必要があり、パスワードは Data Crawler に付属の vcrypt プログラムを使用して暗号化する必要があります。 例: `username:[[vcrypt/3]]passwordstring`
-   **`max-data-size`** - 文書のデータの最大サイズ。 これは、一度にロードされるメモリーの最大ブロックです。 コンピューター上に十分なメモリーがある場合に限り、この限度を増やしてください。
-   **`filter-exact-duplicates`** - 内部使用のみ。
-   **`timeout`** - 内部使用のみ。
-   **`jdbc-class`** (エクステンダー・オプション) - 指定すると、データベース・システムとして `(other)` が選択されている場合に、コネクターで使用される JDBC クラスがこのストリングによってオーバーライドされます。
-   **`connection-string`** (エクステンダー・オプション) - 指定すると、自動生成された JDBC 接続ストリングがこのストリングによってオーバーライドされます。 これにより、ロード・バランシングや SSL 接続など、データベース接続に関するより詳細な構成を指定できます。 例: `jdbc:netezza://127.0.0.1:5480/databasename`
-   **`save-frequency-for-resume`** (エクステンダー・オプション) - クロールの再開や、部分的なリフレッシュを可能にするために、列または関連付けられているラベルの名前を指定します。 シードでクロールが進行するときに、シードによってこの列の名前が定期的な間隔で保存され、データベースの最後の行がクロールされると、この列の名前が再度保存されます。 クロールを再開したり、リフレッシュしたりする場合、クロールはこのフィールドの保存値で指定された行で開始します。

## CMIS クロール・オプションの構成
{: #cmis-crawl-options}

CMIS (Content Management Interoperability Services) コネクターを使用すると、CMIS 対応の CMS (Content Management System) リポジトリー (Alfresco、Documentum、{{site.data.keyword.IBM}} Content Manager など) をクロールし、それらに含まれているデータに索引を付けることができます。

### CMIS コネクターの構成
{: #cmis-connector}

以下に、CMIS コネクターを使用する際に必要な基本構成オプションを示します。 これらの値を設定するには、`config/connectors/cmis.conf` ファイルを開き、それぞれのユース・ケースに合わせて以下の値を指定します。

-   **`protocol`** - クロールに使用するコネクター・プロトコルの名前。 このコネクターを使用する場合の値は、`cmis` でなければなりません。
-   **`collection`** - この属性は、一時ファイルの解凍に使用します。
-   **`dns`** - このオプションは使用されません。
-   **`classname`** - コネクターの Java クラス名。 このコネクターには、`plugin:cmis-v1.1.plugin@connector` を使用します。
-   **`logging-config`** - ロギング・オプションの構成に使用するファイルを指定します。これは、`log4j` XML ストリングとしてフォーマット設定する必要があります。
-   **`endpoint`** - CMIS 準拠のリポジトリーのサービス・エンドポイント URL。 
-   **`username`** - コンテンツへのアクセスに使用する CMIS リポジトリー・ユーザーのユーザー名。 このユーザーは、クロールと索引付けの対象となるすべてのフォルダーと文書へのアクセス権限を持っている必要があります。
-   **`password`** - コンテンツへのアクセスに使用する CMIS リポジトリーのパスワード。 パスワードは暗号化せず、プレーン・テキストで指定してください。
-   **`repositoryid`** - CMIS リポジトリーのコンテンツへのアクセスに使用する、その具体的な CMIS リポジトリーの ID。
-   **`bindingtype`** - CMIS リポジトリーへの接続に使用するバインディングのタイプを識別します。 値は AtomPub または WebServices のいずれかです。
-   **`authentication`** - CMIS 互換リポジトリーへの接続時に使用する認証メカニズムのタイプ (基本 HTTP 認証、NTLM、または WS-Security (ユーザー名トークン)) を識別します。
-   **`enable-acl`** - クロールされたデータの ACL を取得できるようにします。 このコレクション内の文書のセキュリティーを考慮しない場合は、このオプションを無効にすると、文書でこの情報が要求されず、この情報の取得やエンコードが行われないため、パフォーマンスが向上します。 値は true または false のいずれかです。
-   **`user-agent`** - 文書をクロールする際にサーバーに送信されるヘッダー。
-   **`method`** - パラメーターを渡すときに使用するメソッド (GET または POST)。
-   **`url-logging`** - クロールされた URL をログに記録する範囲。 可能な値は以下のとおりです。

    -   `full-logging` - その URL に関する情報をすべてログに記録します。
    -   `refined-logging` - クローラー・ログの参照に必要な情報およびコネクターが正しく機能するために必要な情報のみをログに記録します。これがデフォルト値です。
    -   `minimal-logging` - コネクターが正しく機能するために必要な最小限の情報のみをログに記録します。

    このオプションを `minimal-logging` に設定すると、ログのサイズが小さくなり、ログに記録されるデータ量が最少化されて入出力が減少するため、パフォーマンスが若干向上します。
-   **`ssl-version`** - HTTPS 接続に使用する SSL のバージョンを指定します。 デフォルトでは、使用可能な最強のプロトコルが使用されます。

### CMIS クロール・シードの構成
{: #cmis-crawl-seed}

以下に、CMIS クロール・シード・ファイル用に構成できる値を示します。 これらの値を設定するには、`config/seeds/cmis-seed.conf` ファイルを開き、それぞれのユース・ケースに合わせて以下の値を変更します。

-   **`url`** - クロールの開始点として使用される、CMIS リポジトリーのフォルダーの URL。例: `cmis://alfresco.test.com:8080/alfresco/cmisatom?folderToProcess-workspace://SpacesStore/guid`

    ルート・フォルダーからクロールするには、URL を以下のように指定する必要があります。`cmis://alfresco.test.com:8080/alfresco/cmisatom?folderToProcess-`
-   **`at`** - このオプションは使用されません。
-   **`default-allow`** - 内部使用のみ。

## SMB/CIFS/Samba クロール・オプションの構成
{: #smb-cifs-samba-crawl-options}

Samba コネクターを使用すると、Server Message Block (SMB) および Common Internet filesystem (CIFS) のファイル共有をクロールできます。 このタイプのファイル共有は Windows ネットワーク上で一般的であり、オープン・ソース・プロジェクト Samba を介しても提供されます。

### Samba コネクターの構成
{: #smb-cifs-samba-crawl-connector}

以下に、Samba コネクターを使用する際に必要な基本構成オプションを示します。 これらの値を設定するには、`config/connectors/samba.conf` ファイルを開き、それぞれのユース・ケースに合わせて以下の値を指定します。

-   **`protocol`** - クロールに使用するコネクター・プロトコルの名前。 このコネクターを使用する場合の値は、smb です。
-   **`collection`** - この属性は、一時ファイルの解凍に使用します。
-   **`classname`** - コネクターの Java クラス名。 このコネクターを使用する場合の値は、`plugin:smb.plugin@connector` でなければなりません。
-   **`logging-config`** - ロギング・オプションの構成に使用するファイルを指定します。これは、`log4j` XML ストリングとしてフォーマット設定する必要があります。
-   **`username`** - 認証で使用する Samba ユーザー名。 指定する場合は、ドメインとパスワードも指定する必要があります。 指定しない場合は、ゲスト・アカウントが使用されます。
-   **`password`** - 認証で使用する Samba パスワード。 ユーザー名を指定する場合、これは必須です。 パスワードは、Data Crawler に付属の vcrypt プログラムを使用して暗号化する必要があります。
-   **`archive`** - アーカイブ・ファイル内の圧縮されたファイルを Samba コネクターでクロールし、索引を付けられるようにします。 値は true または false のいずれかで、デフォルト値は false です。
-   **`max-policies-per-handle`** - 単一の RPC ハンドル用に開くことができるローカル・セキュリティー権限 (LSA) ポリシーの最大数を指定します。 これらのポリシーによって、さまざまな条件下で特定のシステムを照会または変更する際に必要なアクセス許可が定義されます。 このオプションのデフォルト値は 255 です。
-   **`crawl-fs-metadata`** - このオプションをオンにすると、Data Crawler によって、ファイルに関する使用可能なファイル・システムのメタデータ (作成日、最終変更日、ファイル属性など) を含む VXML 文書が追加されます。
-   **`enable-arc-connector`** - このオプションは使用されません。
-   **`disable-indexes`** - 無効化する索引の改行で区切られたリスト。これにより、クロールの速度が上がる場合があります。以下に例を示します。

    -   `disable-url-index`
    -   `disable-error-state-index`
    -   `disable-crawl-time-index`
-   **`exact-duplicates-hash-size`** - 完全重複を解決するために使用するハッシュ・テーブルのサイズを設定します。 この数値を変更する場合は、十分な注意が必要です。 選択する値は最適なものにする必要があります。サイズを大きくすると、検索の速度が上がる可能性がありますが、より多くのメモリーが必要になります。サイズを小さくすると、クロールの速度が低下する可能性がありますが、メモリー使用量がかなり削減されます。
-   **`user-agent`** - このオプションは使用されません。
-   **`timeout`** - このオプションは使用されません。
-   **`n-concurrent-requests`** - 単一の IP アドレスと同時に送信される要求の数。 デフォルトは `1` です。
-   **`enqueue-persistence`** - このオプションは使用されません。

### Samba クロール・シードの構成
{: #smb-cifs-samba-crawl-seed}

以下に、Samba クロール・シード・ファイル用に構成できる値を示します。 これらの値を設定するには、`config/seeds/samba-seed.conf` ファイルを開き、それぞれのユース・ケースに合わせて以下の値を指定します。

-   **`url`** - クロールする共有の改行で区切られたリスト。以下に例を示します。

    ```
    smb://share.test.com/office
    smb://share.test.com/cash/money/change
    smb://share.test.com/C$/Program Files
    ```
    {: codeblock}

-   **`hops`** - 内部使用のみ。
-   **`default-allow`** - 内部使用のみ。
