---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-28"

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

# Data Crawler の構成
{: #configuring-the-data-crawler}

リポジトリーをクロールするように Data Crawler をセットアップするには、適切な入力アダプターを `crawler.conf` ファイルで指定した上で、リポジトリー固有の情報を入力アダプター構成ファイルで構成する必要があります。
{: shortdesc}

Data Crawler は、ファイル共有またはデータベースをクロールする場合にのみ使用してください。それ以外の場合は、適切な {{site.data.keyword.discoveryshort}} コネクターを使用してください。詳しくは、『[データ・ソースへの接続](/docs/services/discovery?topic=discovery-sources#sources)』を参照してください。 {{site.data.keyword.discoveryshort}} コネクターでサポートされているデータ・ソースで Data Crawler を使用する場合、Data Crawler に対する支援は行われなくなりました。
{: important}

以下のステップで示される変更を行う前に、`{installation_directory}/share/examples/config` ディレクトリーの内容をシステム上の作業ディレクトリー (例えば、`/home/config`) にコピーして作業ディレクトリーを作成してあることを確認してください。

**重要:** 提供されたサンプル構成ファイルは、直接変更しないでください。 コピーしてから編集するようにしてください。 サンプル・ファイルを直接編集すると、Data Crawler をアップグレードする際に構成が上書きされたり、Data Crawler をアンインストールする際に削除されたりすることがあります。

**注:** 本書で `config` ディレクトリー内のファイル(`config/crawler.conf` など) について言及する場合は、インストールされた `{installation_directory}/share/examples/config` ディレクトリー内ではなく、作業ディレクトリー内の当該ファイルを指しています。

指定された値は `config/crawler.conf` でのデフォルトであり、Filesystem コネクターを構成します。

1.  テキスト・エディターで `config/crawler.conf` ファイルを開きます。

    -   `crawl_config_file` オプションを、以前に変更した `.conf` (例えば、`connectors/filesystem.conf`) に設定します。
    -   `crawl_seed_file` オプションを、以前に変更した `-seed.conf` (例えば、`seeds/filesystem-seed.conf`) に設定します。
    -   {{site.data.keyword.discoveryshort}} サービスの `output_adapter` `class` オプションと `config` オプションを次のように指定します。

        ```
        class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

        config - "discovery_service"

        discovery_service {
          include "discovery/discovery_service.conf"
        }
        ```
        {: codeblock}

    このファイルには、ご使用の環境に応じて設定される可能性がある他のオプション設定があります。これらの値の設定について詳しくは、「[クロール・オプションの構成](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-crawl-options)」、「[入力アダプターの構成](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#input-adapter)」、「[出力アダプターの構成](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#output-adapter)」、「[追加のクロール管理オプション](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#additional-crawl-management-options)」を参照してください。

1.  テキスト・エディターで `discovery/discovery_service.conf` ファイルを開きます。 {{site.data.keyword.Bluemix}} で前に作成した {{site.data.keyword.discoveryshort}} サービス固有の以下の値を変更します。

    -   `environment_id` - {{site.data.keyword.discoveryshort}} サービスの環境 ID。
    -   `collection_id` - {{site.data.keyword.discoveryshort}} サービスのコレクション ID。
    -   `configuration_id` - {{site.data.keyword.discoveryshort}} サービスの構成 ID。
    -   `configuration` - この `discovery_service.conf` ファイルを示すフルパスのロケーション (例: `/home/config/discovery/discovery_service.conf`)。
    -   `username` - {{site.data.keyword.discoveryshort}} サービスのユーザー名資格情報。
    -   `apikey` - {{site.data.keyword.discoveryshort}} サービスの資格情報。

    このファイルには、ご使用の環境に応じて設定される可能性がある他のオプション設定があります。 これらの値の設定について詳しくは、「[サービス・オプションの構成](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-service-options)」を参照してください。

1.  これらのファイルを変更したら、データをクロールする準備が完了です。 引き続き、「[データ・リポジトリーのクロール](/docs/services/discovery?topic=discovery-crawling-your-data-repository#crawling-your-data-repository) 」に進んでください。

## クロール・オプションの構成
{: #configuring-crawl-options}

ファイル `config/crawler.conf` には、Data Crawler に対し、クロールに使用するファイル (入力アダプター)、クロールが完了した後のクロール済みファイルのコレクションの送信先 (出力アダプター)、その他のクロール管理オプションを指示する情報が含まれています。

**注:** すべてのファイル・パスは、特に説明がない限り `config` ディレクトリーを基準にした相対パスです。

`crawler.conf` ファイルの最新情報について製品内マニュアルにアクセスするには、Crawler のインストール・ディレクトリーから `man crawler.conf` コマンドを入力します。
{: tip}

このファイルで設定できるオプションは、以下のとおりです。

### 入力アダプター
{: #input-adapter}

-   **`class`** - 内部使用専用。Data Crawler の入力アダプター・クラスを定義します。 デフォルト値は `com.ibm.watson.crawler.connectorframeworkinputadapter.Crawl` です。
-   **`config`** - 内部使用専用。コネクター・フレームワーク構成を定義します。 選択した入力アダプターに渡すこのブロック内のデフォルトの構成キーは `connector_framework` です。

    コネクター・フレームワークによって、データへのアクセスが可能になります。 データは、企業の内部データである場合も、Web 上やクラウド内の外部データである場合もあります。 コネクターによって複数の異なるデータ・ソースへのアクセスが可能になりますが、接続を実際に制御するのはクロール・プロセスです。

    **重要:** コネクター・フレームワークの入力アダプターで取り出されたデータは、ローカルでキャッシュされます。 このデータは、暗号化での保存はされません。 デフォルトの場合、データは一時ディレクトリーにキャッシュされます。このディレクトリーは、リブート時にクリアするとともに、クローラー・コマンドを実行したユーザーだけが読み取れるように設定する必要があります。

    コネクター・フレームワークがクリーンアップの前に終了してしまうと、クローラーの終了後にそのディレクトリーが存在し続ける可能性があります。 データをキャッシュする場所を慎重に検討してください。暗号化されたファイル・システムに置くこともできますが、その場合はパフォーマンスへの影響に注意しなければなりません。 クロールのスピードとセキュリティーのバランスをよく考えて決める必要があります。
-   **`crawl_config_file`** - クロールに使用する構成ファイル。 デフォルト値は `connectors/filesystem.conf` です。
-   **`crawl_seed_file`** - クロールに使用するクロール・シード・ファイル。 デフォルト値は `seeds/filesystem-seed.conf` です。
-   **`id_vcrypt_file`** - Crawler でデータ暗号化に使用される鍵ファイル。Crawler に組み込まれているデフォルト鍵は `id_vcrypt` です。 新規 `id_vcrypt` ファイルを生成する必要がある場合は、`bin` フォルダー内の vcrypt スクリプトを使用します。
-   **`crawler_temp_dir`** - コネクター・ログ用の Crawler の一時フォルダー。 デフォルト値は `tmp` です。 このフォルダーがまだ存在しない場合は、現在の作業ディレクトリーに `tmp` フォルダーが作成されます。
-   **`extra_jars_dir`** - 追加の JAR のディレクトリーをコネクター・フレームワーク・クラスパスに追加します。

    **注:** コネクター・フレームワークの `lib/java` ディレクトリーを基準にした相対パスです。

    -   データベース・コネクターを使用する場合、この値は `database` でなければなりません。

    その他のコネクターを使用する場合、この値は空 (空のストリング "") のままにすることができます。

-   **`urls_to_filter`** - クロールしてはならない URL のブラックリスト (正規表現形式)。 Data Crawler は、指定された正規表現のいずれかに一致する URL をクロールしません。

    `domain list` には、クロールできないドメインが含まれています。 必要に応じてこれに追加してください。

    `filetype list` には、オーケストレーション・サービスがサポートしていないファイル拡張子が含まれています。

    サポートされるファイル・タイプを正規表現から削除してください。

    ご使用のシード URL のドメインがこのフィルターで許可されていることを確認してください。 `allow everything` 動作には空のフィルターを使用してください。

    Crawler がハングする場合があるため、シード URL がフィルターで除外されないようにしてください。

-   **`max_text_size`** - 文書に許容される最大サイズ (バイト)。これを超えると、コネクター・フレームワークによってディスクに文書が書き込まれます。 この値を調整して増やすとディスクに書き込まれる文書の量が少なくなりますが、メモリーの必要量が増えます。 デフォルト値は `1048576` です。
-   **`extra_vm_params`** - コネクター・フレームワークを起動するために使用するコマンドにさらに Java パラメーターを追加できます。

-   **`bootstrap_logging`** - コネクター・フレームワークの開始ログを書き込みます。詳細デバッグの場合にのみ便利です。 可能な値は、`true` または `false` です。 ログ・ファイルは `crawler_temp_dir` に書き込まれます。

-   **`read-timeout`** - クローラーがコネクター・フレームワークからの応答を待つ時間 (秒) を設定します。 デフォルト値は 5 秒です。

### 出力アダプター
{: #output-adapter}

-   **`class`** - Data Crawler の出力アダプター・クラスを定義します。
-   **`config`** - 出力アダプターに渡す構成キーを定義します。 この構成オブジェクト内のキーに対応するストリングを指定してください。 以下に、コード例を示します。

    ```
    class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

    config - "discovery_service"

    discovery_service {
        include "discovery/discovery_service.conf"
      }
    ```
    {: codeblock}

    構成キーは `discovery_service` です。

出力アダプターを選択するには、`class` パラメーターと `config` キーを指定しなければなりません。

-   **{{site.data.keyword.discoveryshort}} Service 出力アダプター** - クロール済みの文書を {{site.data.keyword.discoveryfull}} サービスにアップロードします。 このアダプターを選択する場合は、`class` パラメーターと `config` キーを以下のように設定します。

```
class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

config - "discovery_service"

discovery_service {
            include "discovery/discovery_service.conf"
          }
```
{: codeblock}

-   **Test 出力アダプター** - Test 出力アダプターは、クロール済みのファイルを表す項目を、指定されたロケーションにあるディスクに書き込みます。 このアダプターを選択する場合は、`class` パラメーターと `config` キーを以下のように設定します。

    追加のパラメーター `output_directory` を使用して、クロール済みのデータを表す項目を書き込むディレクトリーを選択できます。

```
class - "com.ibm.watson.crawler.testoutputadapter.TestOutputAdapter"

config - "test"

output_directory - "/tmp/crawler-test-output"`
```
{: codeblock}

-   **`retry`** - 出力アダプターへのプッシュ処理が失敗した場合の再試行のオプションを指定します。

    -   `max_attempts` - 再試行の最大回数。 デフォルト値は `10` です。
    -   `delay` - 再試行と再試行の間の最小遅延時間 (秒)。 デフォルト値は `2` です。
    -   `exponent_base` - 試行が失敗するたびに遅延時間を長く設定するための係数。 デフォルト値は `2` です。

    数式は以下のとおりです。

        **`d(nth_retry) - delay * (exponent_base ^ nth_retry)`**

    例えば、delay が 1 秒、exponent base が 2 のデフォルト設定の場合、2 回目と 3 回目の再試行の間の遅延時間は 1 秒ではなく 2 秒になり、その次の遅延時間は 4 秒になります。

        `d(0) - 1 * (2 ^ 0)` - 1 秒
        `d(1) - 1 * (2 ^ 1)` - 2 秒
        `d(2) - 1 * (2 ^ 2)` - 4 秒

    このため、デフォルト設定の場合、実行依頼の最大試行回数は 10 回になり、最大で約 1022 秒の (17 分を少し超える) 待ち時間が生じます。 この時間が概数になるのは、複数の再実行依頼が同時に実行されるのを避けるために、余分の時間が追加されるからです。 その追加時間は最大で 10% なので、前の例における最後の再試行の遅延時間は最大で 7.7 秒になります。 待ち時間には、サービスへの接続やデータのアップロードにかかる時間、応答の待ち時間は含まれていません。

    `output_timeout` 値は、ここでの待機時間より優先されます。再試行の待ち時間の合計がその設定を超えると、実行依頼は再試行すべき場合でも失敗します。
    {: tip}

### 追加のクロール管理オプション
{: #additional-crawl-management-options}

-   **`full_node_debugging`** - デバッグ・モードをアクティブにします。可能な値は `true` または `false` です。

    **重要**: この設定により、クロール済みの各文書の全データがログに書き込まれます。   

-   **`logging.log4j.configuration_file`*** - ロギングに使用する構成ファイル。 サンプルの `crawler.conf` ファイルでは、このオプションは `logging.log4j` 内に定義され、そのデフォルト値は `log4j_custom.properties` です。 このオプションは、`.properties` ファイルまたは `.conf` ファイルのいずれを使用するかにかかわらず、同様に定義する必要があります。   
-   **`shutdown_timeout`** - アプリケーションがシャットダウンされるまでのタイムアウト値 (分) を指定します。 デフォルト値は `10` です。   
-   **`output_limit`** - Crawler が出力アダプターへの同時送信を試行する索引付け可能な項目の最大数。 この数は、処理に使用できるコア数によってさらに制限される場合があります。 これは、リターンを待機している出力アダプターに送信される索引付け可能な項目がいずれの時点でも「x」個以下であることを示します。 デフォルト値は `10` です。   
-   **`input_limit`** - 入力アダプターから一度に要求できる URL の数を制限します。 デフォルト値は `30` です。   
-   **`output_timeout`** - Data Crawler が出力アダプターへの要求を中止し、処理量を増やすために出力アダプター・キューから項目を削除するまでの時間 (秒)。 デフォルト値は `1200` です。

    出力アダプターによる制約を考慮してください。その制約は、ここで定義する制限値に関係する場合があるからです。 定義された `output_limit` は、出力アダプターに一度に送信できる索引付け可能なオブジェクト数にのみ関係します。 索引付け可能なオブジェクトが出力アダプターに送信されると、`output_timeout` 変数で定義された「クロック」が有効になります。 出力アダプター自体にスロットルがあり、受け取った数と同数の入力が処理されないようになっている場合があります。 例えば、オーケストレーション出力アダプターが、サービスへの HTTP 接続用に構成できる接続プールを持つ場合があります。 例えば、これがデフォルトで 8 に設定されているときに `output_limit` を 8 より大きい数値に設定すると、クロックに従って実行の順番を待つプロセスが生じます。 その後、タイムアウトになる場合があります。   
-   **`num_threads`** - 一度に実行できる並列スレッドの数。 この値は、並列スレッドの数を直接指定する整数か、使用可能なプロセッサー数に乗ずる係数を `"xNUM"` という形式で指定するストリング (例: `"x1.5"`) のいずれかです。 デフォルト値は `"30"` です。

## サービス・オプションの構成
{: #configuring-service-options}

{{site.data.keyword.discoveryshort}} サービスは、{{site.data.keyword.discoveryfull}} サービスを使用するときにクロール済みファイルをどのように管理するのかをクローラーに指示します。

`discovery-service.conf` ファイルの最新情報について製品内マニュアルにアクセスするには、Crawler のインストール・ディレクトリーから次のコマンドを入力します。

  ```bash
  man discovery_service.conf
  ```
  {: pre}
{: tip}

デフォルト・オプションを直接変更する場合は、`config/discovery/discovery_service.conf` ファイルを開き、それぞれのユース・ケースに合わせて以下の値を指定します。

-   **`http_timeout`** - 文書の読み取り/索引付け操作のタイムアウト (秒)。デフォルトは `125` です。
-   **`proxy_host_port`** - (オプション) データ・クローラーをファイアウォールの背後で実行する場合、データ・クローラーが {{site.data.keyword.discoveryshort}} サービスに接続できるようにするために、プロキシー・ホスト名とプロキシー・ポート番号の設定が必要になることがあります。 このオプションのデフォルト値は空のストリングですが、値の変更が必要な場合は `"<host>:<port>"` という形式にしてください。
-   **`concurrent_upload_connection_limit`** - 文書のアップロード用に許可される同時接続の数。 デフォルトは `2` です。

    **注:** Orchestration Service 出力アダプターを使用する場合、この数値は、クロール・オプションの構成時に設定された `output_limit` 以上でなければなりません。   

-   **`base_url`** - クロールされた文書の送信先の URL。 {{site.data.keyword.discoveryshort}} サービスの現行リリースでは、この値は `https://gateway.watsonplatform.net/discovery/api` です。   
-   **`environment_id`** - ベース URL でクロールされた文書コレクションの場所。   
-   **`collection_id`** - {{site.data.keyword.discoveryshort}} サービスでセットアップした文書コレクションの名前。
-   **`api_version`** - 内部使用専用。 API バージョンの最終変更日。   
-   **`configuration_id`** - {{site.data.keyword.discoveryshort}} サービスが使用する構成ファイルのファイル名。
-   **`apikey`** - クロールした文書コレクションの場所への認証を行うための資格情報。

{{site.data.keyword.discoveryshort}} Service 出力アダプターは、{{site.data.keyword.IBM}} がユーザーへの理解を深めてサービスを向上させるための統計を送信できます。 `send_stats` 変数には、以下のオプションを設定できます。

-   **`jvm`** - 送信される Java 仮想マシン (JVM) 統計には、データ・クローラーの実行に使用した JVM から報告された Java のベンダーとバージョンが含まれます。 値は、`true` または `false` のいずれかです。 デフォルト値は `true` です。
-   **`os`** - 送信されるオペレーティング・システム (OS) 統計には、データ・クローラーの実行に使用した JVM から報告された OS 名、バージョン、およびアーキテクチャーが含まれます。 値は、`true` または `false` のいずれかです。 デフォルト値は `true` です。
