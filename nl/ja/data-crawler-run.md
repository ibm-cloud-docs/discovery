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

# データ・リポジトリーのクロール
{: #crawling-your-data-repository}

クローラー・オプションをすべて正しく構成したら、データ・リポジトリーに対してクロールを実行できます。
{: shortdesc}

Data Crawler は、ファイル共有またはデータベースをクロールする場合にのみ使用してください。それ以外の場合は、適切な {{site.data.keyword.discoveryshort}} コネクターを使用してください。詳しくは、『[データ・ソースへの接続](/docs/services/discovery?topic=discovery-sources#sources)』を参照してください。 {{site.data.keyword.discoveryshort}} コネクターでサポートされているデータ・ソースで Data Crawler を使用する場合、Data Crawler に対する支援は行われなくなりました。
{: important}

`root` のみが読み取れるファイルへのアクセス権限が必要な場合を除き、クローラーを `root` として実行しないでください。
{: tip}

次のコマンドを実行します。`crawler`

クローラーから、実行内容を説明する資料を示すプロンプトが出されます。 その他のクロール・オプションに加えて、テスト・クロールの実行や、クロールの実行が可能です。

## テスト・クロールの実行
{: #running-test-crawl}

次のコマンドを実行します。`crawler testit`

これは、テスト・クロールを実行します (シード URL だけをクロールし、エンキューされた URL を表示します)。 シード URL の処理結果が索引付け可能なコンテンツ (例えば、文書) になる場合、そのコンテンツが出力アダプターに送信され、画面に出力されます。 シード URL の取得によって URL がエンキューされる場合、それらの URL が表示され、コンテンツは出力アダプターに送信されません。 デフォルトでは、5 つのエンキューされた URL が表示されます。

crawl コマンドのオプションとして、カスタム構成ファイルを指定することもできます。以下に例を示します。`crawler testit --config [config/myconfigfile.conf]`

`--config` オプション内で渡される構成ファイルへのパスは、修飾されたパスでなければなりません。 つまり、これは相対形式 (`config/myconfigfile.conf` や `./myconfigfile.conf` など)、または絶対パス (`/path/to/config/myconfigfile.conf` など) でなければなりません。

さらに、testit コマンドのオプションとして、表示されるエンキューされた URL の数に対して制限を設定できます。以下に例を示します。`crawler testit --limit [number]`

## クロールの実行
{: #running-crawl}

次のコマンドを実行します。`crawler crawl`

これにより、デフォルトの構成ファイル (`crawler.conf`) でクロールが実行されます。

crawl コマンドのオプションとして、カスタム構成ファイルを指定することもできます。以下に例を示します。`crawler crawl --config [config/myconfigfile.conf]`

`--config` オプション内で渡される構成ファイルへのパスは、修飾されたパスでなければなりません。 つまり、これは相対形式 (`config/myconfigfile.conf` や `./myconfigfile.conf` など)、または絶対パス (`/path/to/config/myconfigfile.conf` など) でなければなりません。

## クロールの再始動
{: #restarting-crawl}

次のコマンドを実行します。`crawler restart`

このコマンドは、デフォルトの構成ファイル (`crawler.conf`) で新規のクロールを開始することで、クロールの再始動を実行します。

restart コマンドのオプションとして、カスタム構成ファイルを指定することもできます。以下に例を示します。`crawler restart --config [config/myconfigfile.conf]`

`--config` オプション内で渡される構成ファイルへのパスは、修飾されたパスでなければなりません。 つまり、これは相対形式 (`config/myconfigfile.conf` や `./myconfigfile.conf` など)、または絶対パス (`/path/to/config/myconfigfile.conf` など) でなければなりません。

## クロールの再開
{: #resuming-crawl}

次のコマンドを実行します。`crawler resume`

このコマンドは、デフォルトの構成ファイル (`crawler.conf`) を使用して、停止したところからクロールを再開します。

resume コマンドのオプションとして、カスタム構成ファイルを指定することもできます。以下に例を示します。`crawler resume --config [config/myconfigfile.conf]`

`--config` オプション内で渡される構成ファイルへのパスは、修飾されたパスでなければなりません。 つまり、これは相対形式 (`config/myconfigfile.conf` や `./myconfigfile.conf` など)、または絶対パス (`/path/to/config/myconfigfile.conf` など) でなければなりません。

## クロールのリフレッシュ
{: #refresh-crawl}

次のコマンドを実行します。`crawler refresh`

このコマンドは、デフォルトの構成ファイル (`crawler.conf`) を使用して、前のクロールをリフレッシュします。

refresh コマンドのオプションとして、カスタム構成ファイルを指定することもできます。以下に例を示します。`crawler refresh --config [config/myconfigfile.conf]`

`--config` オプション内で渡される構成ファイルへのパスは、修飾されたパスでなければなりません。 つまり、これは相対形式 (`config/myconfigfile.conf` や `./myconfigfile.conf` など)、または絶対パス (`/path/to/config/myconfigfile.conf` など) でなければなりません。
