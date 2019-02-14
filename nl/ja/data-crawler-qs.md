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

# Data Crawler を使い始める

このトピックでは、{{site.data.keyword.discoveryfull}} サービスで使用するために、データ・クローラーを用いてファイルをローカル・ファイル・システムから取り込む方法を説明します。
{: shortdesc}

このタスクを試行する前に、{{site.data.keyword.Bluemix}} 内で {{site.data.keyword.discoveryshort}} サービスのインスタンスを生成します。 このガイドを実行するには、作成したサービスのインスタンスに関連付けられている資格情報を使用する必要があります。

{{site.data.keyword.discoveryshort}} ツールまたは API を使用して、Box、Salesforce、および Microsoft SharePoint Online データ・ソースをクロールできます。詳しくは、『[データ・ソースへの接続](/docs/services/discovery/connect.html)』を参照してください。
{: tip}

## 環境の作成

bash の POST /v1/environments メソッドを使用して環境を作成します。 環境とは、すべての文書を箱に入れて保管する倉庫のようなものです。 次の例では、`my-first-environment` という名前の環境を作成します。

`{username}` と `{password}` は、ご使用のサービス資格情報に置き換えます。

```bash
curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
```
{: pre}

この API は、環境 ID、環境状況、環境が使用しているストレージ量などの情報を含む応答を返します。 使用する環境の状況が `ready` になるまで、次のステップに進まないでください。 環境を作成するときに `status:pending` という状況が返された場合は、ready になるまで、`GET /v1/environments/{environment_id}` メソッドを使用して状況をチェックしてください。 この例では、`{username}` と `{password}` はご使用のサービス資格情報に置き換え、`{environment_id}` は環境の作成時に返された環境 ID に置き換えます。

```bash
curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}?version=2017-11-07
```
{: pre}

## コレクションの作成

次に、`POST /v1/environments/{environment_id}/collections` メソッドを使用してコレクションを作成します。 コレクションとは、環境内で資料を保管する箱のようなものです。 この例では、前のステップで作成した環境内に `my-first-collection` という名前のコレクションを作成し、以下のデフォルト構成を使用します。

-   `{username}` と `{password}` は、ご使用のサービス資格情報に置き換えます。
-   `{environment_id}` は、ステップ 1 で作成した環境の環境 ID に置き換えます。

コレクションを作成する前に、デフォルト構成の ID を取得する必要があります。 デフォルトの `configuration_id` を見つけるには、次のように `GET /v1/environments/{environment_id}/configurations` メソッドを使用します。

```bash
curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07
```
{: pre}

デフォルトの構成 ID を取得したら、それを使用してコレクションを作成します。 `{configuration_id}` は、ご使用の環境のデフォルト構成 ID に置き換えます。

```bash
curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{configuration_id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07
```
{: pre}

この API は、コレクション ID、コレクション状況、コレクションが使用しているストレージ量などの情報を含む応答を返します。 コレクション状況が `online` になるまで、次のステップに進まないでください。 コレクションを作成するときに `status:pending` という状況が返された場合は、ready になるまで、`GET /v1/environments/{environment_id}/collections/{collection_id}` メソッドを使用して状況をチェックしてください。 この例では、`{username}` と `{password}` はご使用のサービス資格情報に置き換えます。また、`{environment_id}` はご使用の環境 ID に、`{collection_id}` はこのステップで先ほど返されたコレクション ID にそれぞれ置き換えます。

```bash
curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07
```
{: pre}

## サンプル文書のダウンロード
以下の文書をダウンロードします。

-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン" class="style-scope doc-content"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン" class="style-scope doc-content"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン" class="style-scope doc-content"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン" class="style-scope doc-content"></a>

## Data Crawler のダウンロードとインストール

1.  システムの前提条件を確認します。

    -   Java ランタイム環境バージョン 8 以上

        **注:** Crawler を実行するには、`JAVA_HOME` 環境変数を正しく設定するか、まったく設定しないようにする必要があります。
    -   Red Hat Enterprise Linux 6 または 7、あるいは Ubuntu Linux 15 または 16。 最適なパフォーマンスを得るために、専用の Linux インスタンス上で Data Crawler を実行することが強く推奨されています。この Linux インスタンスは、仮想マシン、コンテナー、ハードウェアのいずれでもかまいません。
    -   少なくとも 2 GB の RAM (Linux システム)

1.  ブラウザーを開いて、[{{site.data.keyword.Bluemix_notm}} アカウント ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net){: new_window} にログインします。
1.  {{site.data.keyword.Bluemix_notm}} ダッシュボードで、前に作成した {{site.data.keyword.discoveryshort}} サービスを選択します。
1.  **「Discovery サービスへのコンテンツのアップロードの自動化 (Automate the upload of content to the Discovery service)」**の下で、ご使用のシステムに適したダウンロード・リンク (DEB、RPM、または ZIP) を選択して Data Crawler をダウンロードします。
1.  管理者として、適切なコマンドを使用して、ダウンロードしたアーカイブ・ファイルをインストールします。

    -   rpm パッケージを使用する Red Hat や CentOS などのシステムでは、次のようなコマンドを使用します: `rpm -i /full/path/to/rpm/package/rpm-file-name`
    -   deb パッケージを使用する Ubuntu や Debian などのシステムでは、次のようなコマンドを使用します: `dpkg -i /full/path/to/deb/package/deb-file-name`
    -   Crawler スクリプトは `{installation directory}/bin` (例えば、`/opt/ibm/crawler/bin`) にインストールされます。 Crawler コマンドが正しく機能するように、`{installation_directory}/bin` が `PATH` 環境変数に含まれるようにしてください。

    Crawler スクリプトは `/usr/local/bin` にもインストールされるので、このディレクトリーも `PATH` 環境変数に追加できます。
    {: tip}

## 作業ディレクトリーの作成

`{installation_directory}/share/examples/config` ディレクトリーの内容をシステム上の作業ディレクトリー (例えば、`/home/config`) にコピーします。

**警告:** 提供されたサンプル構成ファイルは、直接変更しないでください。 コピーしてから編集するようにしてください。 サンプル・ファイルを直接編集すると、Data Crawler をアップグレードする際に構成が上書きされたり、Data Crawler をアンインストールする際に削除されたりすることがあります。

**注:** 本書で `config` ディレクトリー内のファイル(`config/crawler.conf` など) について言及する場合は、インストールされた `{installation_directory}/share/examples/config` ディレクトリー内ではなく、作業ディレクトリー内の当該ファイルを指しています。

## クロール・オプションの構成

リポジトリーをクロールするよう Data Crawler をセットアップするには、クロールするローカル・システムのファイルを指定するだけでなく、クロールが完了した後のクロール済みファイルのコレクションの送信先である {{site.data.keyword.discoveryshort}} サービスを指定する必要があります。

1.  **`filesystem-seed.conf`** - テキスト・エディターで `seeds/filesystem-seed.con` ファイルを開きます。 `name-"url"` 属性直下の `value` 属性を、クロールするファイル・パスに変更します。 例: `value-"sdk-fs:///TMP/MY_TEST_DATA/"`

    **注:** URL は `sdk-fs://` で始める必要があります。したがって、例えば `/home/watson/mydocs` をクロールするには、この URL の値を `sdk-fs:///home/watson/mydocs` にします。3 番目の / は必須です。

    ファイルを保存して閉じます。

1.  **`discovery_service.conf`** - テキスト・エディターで `discovery/discovery_service.conf` ファイルを開きます。 {{site.data.keyword.Bluemix_notm}} で前に作成した {{site.data.keyword.discoveryshort}} サービス固有の次の値を変更します。

    -   `environment_id` - {{site.data.keyword.discoveryshort}} サービスの環境 ID。
    -   `collection_id` - {{site.data.keyword.discoveryshort}} サービスのコレクション ID。
    -   `configuration_id` - {{site.data.keyword.discoveryshort}} サービスの構成 ID。
    -   `configuration` - この `discovery_service.conf` ファイルを示すフルパスのロケーション (例: `/home/config/discovery/discovery_service.conf`)。
    -   `username` - {{site.data.keyword.discoveryshort}} サービスのユーザー名資格情報。
    -   `password` - {{site.data.keyword.discoveryshort}} サービスのパスワード資格情報。
1.  **`crawler.conf`** - テキスト・エディターで `config/crawler.conf` ファイルを開きます。

    -   {{site.data.keyword.discoveryshort}} サービスの `output_adapter` `class` オプションと `config` オプションを次のように指定します。

        ```bash
        class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

        config - "discovery_service"

        discovery_service {
          include "discovery/discovery_service.conf"
        }
        ```
        {: pre}

1.  これらのファイルを変更したら、データをクロールする準備が完了です。

## データのクロール

コマンド `crawler crawl --config [config/crawler.conf]` を実行します。

このコマンドにより、構成ファイル `crawler.conf` を使用してクロールが実行されます。

**注:** `--config` オプションに渡される構成ファイルへのパスは、修飾されたパスにしてください。 つまり、そのパスを相対形式 (`config/crawler.conf` または `./crawler.conf`) にするか、絶対パス (`/path/to/config/crawler.conf`) にする必要があります。

## 文書の検索

最後に、`GET /v1/environments/{environment_id}/collections/{collection_id}/query` メソッドを使用して、文書のコレクションを検索します。 次の例では、`IBM` という名前のエンティティーがすべて返されます。

-   `{username}` と `{password}` は、ご使用のサービス資格情報に置き換えます。
-   `{environment_id}` は、ステップ 1 で作成した環境の環境 ID に置き換えます。
-   `{collection_id}` は、ステップ 2 で作成したコレクションのコレクション ID に置き換えます。

```bash
curl -u "{username}":"{password}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query-enriched_text.entities.text:IBM'
```
{: pre}

## 結果

これで、作成した環境とコレクションで文書を正しく照会できました。 さらに文書をコレクションに追加して、カスタマイズを開始できます。
