---

copyright:
  years: 2015, 2017, 2019
lastupdated: "2019-02-08"

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

# Data Crawler を使用したコンテンツの追加
{: #adding-content-with-data-crawler}

データ・クローラーを使用すると、{{site.data.keyword.discoveryshort}} サービスへのコンテンツのアップロードを自動化できます。
{: shortdesc}

Data Crawler は、ファイル共有またはデータベースをクロールする場合にのみ使用してください。それ以外の場合は、適切な {{site.data.keyword.discoveryshort}} コネクターを使用してください。詳しくは、『[データ・ソースへの接続](/docs/services/discovery?topic=discovery-sources#sources)』を参照してください。 {{site.data.keyword.discoveryshort}} コネクターでサポートされているデータ・ソースで Data Crawler を使用する場合、Data Crawler に対する支援は行われなくなりました。
{: important}

## Data Crawler を使用したデータのクロール
{: #dc-crawling}

Data Crawler は、{{site.data.keyword.discoveryshort}} サービスで使用するために、文書をリポジトリー (例えば、ファイル共有、データベース) から取り出し、クラウドにプッシュすることができるコマンド・ライン・ツールです。

Data Crawler は、ファイル共有またはデータベースをクロールする場合にのみ使用してください。それ以外の場合は、Box、SharePoint、Salesforce、IBM Cloud オブジェクト・ストレージ、または Web Crawl 用の適切な {{site.data.keyword.discoveryshort}} コネクターを使用してください。詳しくは、『[データ・ソースへの接続](/docs/services/discovery?topic=discovery-sources#sources)』を参照してください。 {{site.data.keyword.discoveryshort}} コネクターでサポートされているデータ・ソースで Data Crawler を使用する場合、Data Crawler に対する支援は行われなくなりました。
{: important}

## Data Crawler を使用するケース
{: #dc-use}

多数のファイルをリモート・システムから管理アップロードする場合や、サポートされているリポジトリー (DB2 データベースなど) からコンテンツを抽出する場合は、Data Crawler を使用すべきです。

Data Crawler は、ローカル・ドライブからファイルをアップロードするためのソリューションではありません。 ローカル・ドライブからのファイルのアップロードには、ツールまたはダイレクト API 呼び出しを使用してください。 多数のファイルを {{site.data.keyword.discoveryshort}} にアップロードするもう 1 つの方法は、GitHub 上の [discovery-files ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/IBM/discovery-files){: new_window} です。
{: note}

## Data Crawler の使用
{: #dc-using}

1. [{{site.data.keyword.discoveryshort}} サービスの構成](/docs/services/discovery?topic=discovery-configservice#configservice)
1. クロールするコンテンツにアクセスできるサポート対象の Linux システムへの[Data Crawler のダウンロードとインストール](/docs/services/discovery?topic=discovery-downloading-and-installing-the-data-crawler#downloading-and-installing-the-data-crawler)
1. コンテンツへの [Data Crawler の接続](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-connector-and-seed-options)
1. {{site.data.keyword.discoveryshort}} サービスに接続するための [Data Crawler の構成](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-the-data-crawler)
1. [コンテンツのクロール](/docs/services/discovery?topic=discovery-crawling-your-data-repository#crawling-your-data-repository)

「[Data Crawler を使い始める](/docs/services/discovery?topic=discovery-getting-started-with-the-data-crawler#getting-started-with-the-data-crawler)」のサンプルに従うと、Data Crawler を迅速に開始できます。
