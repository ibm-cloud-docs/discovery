---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-03"

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

# Data Crawler を使用したコンテンツの追加

データ・クローラーを使用すると、{{site.data.keyword.discoveryshort}} サービスへのコンテンツのアップロードを自動化できます。
{: shortdesc}

## Data Crawler を使用したデータのクロール

Data Crawler は、リポジトリー (例えば、ファイル共有、データベース、Microsoft SharePoint) に保存されている文書を取り出して、{{site.data.keyword.discoveryshort}} サービスで使用するためにクラウドにプッシュするのに役立つコマンド・ライン・ツールです。

{{site.data.keyword.discoveryshort}} ツールまたは API を使用して、Box、Salesforce、および Microsoft SharePoint Online データ・ソースをクロールできます。詳しくは、『[データ・ソースへの接続](/docs/services/discovery/connect.html)』を参照してください。
{: tip}

## Data Crawler を使用するケース

多数のファイルをリモート・システムから管理アップロードする場合や、サポートされているリポジトリー (DB2 データベースなど) からコンテンツを抽出する場合は、Data Crawler を使用すべきです。

Data Crawler は、ローカル・ドライブからファイルをアップロードするためのソリューションではありません。 ローカル・ドライブからのファイルのアップロードには、ツールまたはダイレクト API 呼び出しを使用してください。
{: tip}

## Data Crawler の使用

1. [{{site.data.keyword.discoveryshort}} サービスの構成](/docs/services/discovery/building.html#configuring-your-service)
1. クロールするコンテンツにアクセスできるサポート対象の Linux システムへの[Data Crawler のダウンロードとインストール](/docs/services/discovery/data-crawler-install.html)
1. コンテンツへの [Data Crawler の接続](/docs/services/discovery/data-crawler-seeds.html)
1. {{site.data.keyword.discoveryshort}} サービスに接続するための [Data Crawler の構成](/docs/services/discovery/data-crawler-discovery.html)
1. [コンテンツのクロール](/docs/services/discovery/data-crawler-run.html)

「[Data Crawler を使い始める](/docs/services/discovery/data-crawler-qs.html)」のサンプルに従うと、Data Crawler を迅速に開始できます。
