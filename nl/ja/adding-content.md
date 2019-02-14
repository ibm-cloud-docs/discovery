---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-15"

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

# コンテンツの追加

文書のアップロードに使用する方法は、どのように決めますか?
{: shortdesc}

-   コンテンツのアップロードを既存のアプリケーションに統合するか、独自のカスタム・アップロード・メカニズムを作成する場合は、[API](/docs/services/discovery/getting-started.html) を使用します。
-   ローカルでアクセス可能なファイルを迅速にアップロードする場合は、[{{site.data.keyword.discoveryshort}} ツール](/docs/services/discovery/getting-started-tool.html)を使用します。
    {{site.data.keyword.discoveryshort}} ツールを使用して文書をアップロードする場合は、すべての文書が固有のファイル名を持っている必要があります。 2 つのファイルが同じ名前を持つ場合は、新しいバージョンのアップロード時にオリジナルが上書きされます。 同じファイル名を持つ文書をコレクション内に共存させたい場合は、文書 ID を指定する必要があります。 API またはデータ・クローラーを使用して文書をアップロードする場合は、文書 ID を指定できます。
-   Box、Salesforce、および Microsoft SharePoint Online データ・ソースに接続するには、{{site.data.keyword.discoveryshort}} ツールまたは API を使用します。詳しくは、『[データ・ソースへの接続](/docs/services/discovery/connect.html)』を参照してください。
-   管理対象アップロードで多数のファイルを扱う場合、またはサポートされているリポジトリー (DB2 データベースなど) からコンテンツを抽出する場合は、[データ・クローラー](/docs/services/discovery/data-crawler.html)を使用します。

## API またはツールを使用したコンテンツの追加

コレクションに文書を追加する準備ができたら、以下を検討します。

-   {{site.data.keyword.discoveryshort}} サービスにアップロードできる最大ファイル・サイズは 50 MB です。
-   サンプル文書は、自動的にはコレクションに追加されません。 サンプル文書をコレクションの一部にしたい場合は、そのサンプル文書を追加する必要があります。
-   エンリッチメントのために選択された各 JSON フィールドの最初の 50,000 文字のみがエンリッチされます。
-   コレクションを作成するときは、文書言語を選択します (デフォルトは英語)。 言語のリストについては、[言語サポート](/docs/services/discovery/language-support.html)を参照してください。 選択した言語で文書がエンリッチされます。 同じコレクション内で言語を混用しないでください。
-   Microsoft Word、PDF、HTML、および JSON の各文書をコレクションに追加できます。 **注:** スキャンされたイメージ・ファイルの PDF は、変換およびエンリッチできません。
-   コレクション内の文書は、別の構成ファイルを選択しない限り、Default Configuration という名前で提供された構成ファイルを使用して変換されます。 構成ファイルの作成については、「[カスタム構成](/docs/services/discovery/building.html#custom-configuration)」を参照してください。
-   文書はデータ・コレクションにアップロードされると、そのコレクション用に選択された構成ファイルを使用して変換およびエンリッチされます。後でコレクションを別の構成ファイルに切り替えたい場合、切り替えは可能ですが、既にアップロードされている文書は元の構成ファイルによって変換されたままとなります。 構成ファイルの切り替え後にアップロードされたすべての文書は、新しい構成ファイルを使用します。 コレクション**全体**で新しい構成を使用する場合は、新規コレクションを作成し、新しい構成ファイルを選択してから、すべての文書を再度アップロードすることが必要になります。
-   フィールドの`データ・タイプ` (例: `text` や `date`) を指定することはできません。文書の取り込み中に、索引にまだ存在しないフィールドが検出されると、{{site.data.keyword.discoveryshort}} は、索引付けられた最初の文書のそのフィールドの値に基づいて、そのフィールドの`データ・タイプ`を自動的に検出します。
-   現行文書内のデータと前に取り込まれた文書内の類似データとの間にタイプの不一致があるため、文書の取り込みが失敗することがあります。 例えば、ある文書内で `date` タイプとされているフィールドが後続の文書では `string` である場合、その後続文書は正しく索引付けされません。
-   カスタムのトークン化 (現在は {{site.data.keyword.discoveryshort}} API の使用時に日本語コレクションでのみ使用可能) を使用する予定の場合、文書をアップロードする前にコレクション用のトークン化辞書を追加する必要があります。

文書のアップロード時には、以下の制限が適用されます。

-   **ライト**・プラン: 21 個のインフライト文書
-   **拡張**プラン: 105 個のインフライト文書 (インフライト文書が 50 個に制限されている X-Small 拡張プランを除く)
-   **プレミアム**・プラン: 210 個のインフライト文書

これらの制限は変更されることがあります。 

Discovery サービスを使用する際、インフライトのアップロードというのは、文書がコレクションに追加される前にアップロードおよび処理されている状態であることを表します。インフライト制限に達した場合、取り込み速度を遅くする必要があります。1 つの選択肢として、再試行を行う自動バックオフ・メカニズムを追加することを検討できます。

## Discovery ツールによる文書のアップロード

1.  コレクションを作成します。 「[文書用のサービスの準備](/docs/services/discovery/building.html#preparing-the-service-for-your-documents)」を参照してください。
1.  コレクションをクリックして開きます。
1.  **「文書のアップロード」**ボタンをクリックし、ドラッグ・アンド・ドロップまたはブラウズによって文書のアップロードを開始します。

これで、文書が変換およびエンリッチされるためにエンキューされます。 この所要時間はコレクションのサイズによって決まります。 索引付けとエンリッチが行われたあと、コレクションの詳細が**「概要」**セクションに表示されます。

-   **作成**日と**最終更新**日 (`collection_id`、`configuration_id`、`environment_id` を表示するには、**「このコレクションを API で使用 (Use this collection in API)」**をクリックします)
-   コレクション内の**文書の数**
-   **構成** — このコレクションの変換に使用された構成ファイルの名前
-   **エラーと警告**

Box、Salesforce、および Microsoft SharePoint Online データ・ソースを {{site.data.keyword.discoveryshort}} ツールと接続する手順については、『[データ・ソースへの接続](/docs/services/discovery/connect.html)』を参照してください。


## API を使用した文書のアップロード

ステップバイステップのチュートリアルについては、「[{{site.data.keyword.discoveryshort}} API の入門 (Getting started with the Discovery API) ](/docs/services/discovery/getting-started.html)」を参照してください。

API について詳しくは、「[API reference ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}」を参照してください。

1.  `POST /v1/environments/{environment_id}/collections` メソッドを使用してコレクションを作成します。
1.  次に、`POST /v1/environments/{environment_id}/collections/{collection_id}/documents` メソッドを使用して文書をコレクションに追加します。

## URL のクロール

URL をクロールし、{{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} {{site.data.keyword.discoveryshort}} サービスの [Apache Nutch 向け索引付けプラグイン![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/IBM-Watson/nutch-indexer-discovery)を使用して索引付けを行うことができます。 クロールは自動的には更新されないため、索引を最新の状態に保つには、この手順を定期的に繰り返す必要があります。
