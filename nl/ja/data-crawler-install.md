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

# Data Crawler のダウンロードとインストール
{: #downloading-and-installing-the-data-crawler}

Data Crawler は、最終的に {{site.data.keyword.discoveryshort}} サービスの検索結果を作成するために使用される生データを収集します。 クローラーがデータ・リポジトリーをクロールする際は、ユーザー指定のシード URL から開始して文書とメタデータをダウンロードします。 クローラーは階層内の文書またはシード URL からリンクされた文書を検出し、取得するためにこれらの文書をエンキューします。
{: shortdesc}

Data Crawler は、ファイル共有またはデータベースをクロールする場合にのみ使用してください。それ以外の場合は、適切な {{site.data.keyword.discoveryshort}} コネクターを使用してください。詳しくは、『[データ・ソースへの接続](/docs/services/discovery?topic=discovery-sources#sources)』を参照してください。 {{site.data.keyword.discoveryshort}} コネクターでサポートされているデータ・ソースで Data Crawler を使用する場合、Data Crawler に対する支援は行われなくなりました。
{: important}

## 前提条件
{: #dc-prerequisites}

-   Java ランタイム環境バージョン 8 以上

    Crawler を実行するには、`JAVA_HOME` 環境変数を正しく設定するか、まったく設定しないようにする必要があります。
    {: tip}
-   Red Hat Enterprise Linux 6 または 7、あるいは Ubuntu Linux 15 または 16。 最適なパフォーマンスを得るために、専用の Linux インスタンス上で Data Crawler を実行することが強く推奨されています。この Linux インスタンスは、仮想マシン、コンテナー、ハードウェアのいずれでもかまいません。

-   少なくとも 2 GB の RAM (Linux システム)

## Data Crawler のダウンロードとインストール
{: #dc-download-install}

1.  ブラウザーを開いて、[{{site.data.keyword.Bluemix}} アカウント ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/){: new_window} にログインします。

1.  {{site.data.keyword.Bluemix_notm}} ダッシュボードで、前に作成した {{site.data.keyword.discoveryshort}} サービスを選択します。

1.  **「Discovery サービスへのコンテンツのアップロードの自動化 (Automate the upload of content to the Discovery service)」**セクションで、DEB、RPM、および ZIP 形式の Data Crawler for Linux をダウンロードするための適切なリンクをクリックします。

1.  Java ランタイム環境バージョン 8 以上が実行されていることを確認します。 コマンド `java -version` を実行して、**1.8** を見つけてください。 **1.8** より前のものが実行されている場合は、Java Developer Kit (JDK) 8 をパッケージ管理システム、[IBM JDK ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/developerworks/java/jdk/){: new_window} Web サイト、または [java.com ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.java.com){: new_window} からインストールして、Java をアップグレードする必要があります。

    Crawler を実行するには、`JAVA_HOME` 環境変数を正しく設定するか、まったく設定しないようにする必要があります。
    {: tip}

1.  管理者として、適切なコマンドを使用して、ダウンロードしたアーカイブ・ファイルをインストールします。

    -   rpm パッケージを使用する Red Hat や CentOS などのシステムでは、次のようなコマンドを使用します: `rpm -i /full/path/to/rpm/package/rpm-file-name`
    -   deb パッケージを使用する Ubuntu や Debian などのシステムでは、次のようなコマンドを使用します: `dpkg -i /full/path/to/deb/package/deb-file-name`
    -   Crawler スクリプトは、`{installation_directory directory}/bin` (例えば `/opt/ibm/crawler/bin`) にインストールされます。 Crawler コマンドが正しく機能するように、`{installation_directory}/bin` が `PATH` 環境変数に含まれるようにしてください。

    Crawler スクリプトは `/usr/local/bin` にもインストールされるので、このディレクトリーも `PATH` 環境変数に追加できます。
    {: tip}
1.  作業ディレクトリーを作成します。これは、`{installation_directory}/share/examples/config` ディレクトリーの内容をシステム上の作業ディレクトリー (例えば `/home/config`) にコピーすることで行います。

    **警告:** 提供されたサンプル構成ファイルは、直接変更しないでください。 コピーしてから編集するようにしてください。 サンプル・ファイルを直接編集すると、Data Crawler をアップグレードする際に構成が上書きされたり、Data Crawler をアンインストールする際に削除されたりすることがあります。

    **注:** 本書でこれ以降 `config` ディレクトリー内のファイル (`config/crawler.conf` など) について言及する場合は、インストールされた `{installation_directory}/share/examples/config` ディレクトリー内ではなく、作業ディレクトリー内の当該ファイルを指しています。

1.  これで、[リポジトリーに接続するために Data Crawler を構成する](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-connector-and-seed-options)準備ができました。

## Data Crawler の構造
{: #dc-structure}

Data Crawler のダウンロードによって、次のフォルダーがシステム上に作成されます。

-   `doc` - 著作権情報やライセンス情報のファイルが入っています。
-   `bin` - クローラーを実行するためのスクリプト・ファイル。
-   `connectorFramework` - このディレクトリー内のファイルを使用すると、企業の内部データか Web 上やクラウド内の外部データかにかかわらず、データにアクセスできます。
-   `lib` - クローラーが使用するライブラリー・ファイル。
-   `share`
    -   `doc` - 資料ファイルが HTML 形式とマークダウン形式で用意されています。
    -   `examples/config` - クローラーに対し、クロールに使用するデータ、クロールが完了した後のクロール済みデータのコレクションの送信先、その他のクロール管理オプションを指示するためのファイルが含まれています。
    -   `man` - 製品内マニュアル・ページでのクローラーの資料。

## 本リリースの既知の制限事項
{: #dc-limitations}

-   無効な URL または欠落した URL を使用して Filesystem コネクターを実行すると、Data Crawler がハングすることがあります。
-   すべてのホワイトリスト URL または RegEx が 1 つの RegEx 式に組み込まれるように、`crawler.conf` ファイル内の `urls_to_filter` 値を構成してください。 詳しくは、「[クロール・オプションの構成](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-crawl-options)」を参照してください。
-   `--config -c` オプションに渡される構成ファイルへのパスは、修飾されたパスにしてください。 つまり、そのパスを相対形式 (`config/crawler.conf` や `./crawler.conf`)、または絶対パス (`/path/to/config/crawler.conf`) にする必要があります。 `crawler.conf` のみを指定できるのは、`crawler.conf` ファイルで `include` を使用して参照せずに、`orchestration_service.conf` ファイルがインラインで記述されている場合です。
