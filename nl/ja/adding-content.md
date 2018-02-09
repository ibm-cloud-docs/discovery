---

著作権:
  年: 2015、2017
最終更新日日: "2017-11-10"

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
{{site.data.keyword.discoveryshort}} ツールを使用して文書をアップロードする場合は、すべての文書が固有のファイル名を持っている必要があります。同じ名前のファイルが 2 つある場合は、新しいバージョンのアップロード時にオリジナルが上書きされます。同じファイル名を持つ文書をコレクション内に共存させたい場合は、文書 ID を指定する必要があります。API またはデータ・クローラーを使用して文書をアップロードする場合は、文書 ID を指定できます。
-   管理対象アップロードで多数のファイルを扱う場合、またはサポートされているリポジトリー (DB2 データベースなど) からコンテンツを抽出する場合は、[データ・クローラー](/docs/services/discovery/data-crawler.html)を使用します。

## API またはツールを使用したコンテンツの追加

コレクションに文書を追加する準備ができたら、以下を検討します。

-   {{site.data.keyword.discoveryshort}} サービスにアップロードできる最大ファイル・サイズは 50 MB です。

-   サンプル文書は、自動的にはコレクションに追加されません。サンプル文書をコレクションの一部にしたい場合は、そのサンプル文書を追加する必要があります。

-   コレクションを作成するときは、文書言語を選択します (デフォルトは英語)。言語のリストについては、[言語サポート](/docs/services/discovery/language-support.html)を参照してください。選択した言語で文書がエンリッチされます。同じコレクション内で言語を混用しないでください。

-   Microsoft Word、PDF、HTML、および JSON の各文書をコレクションに追加できます。**注:** スキャンされたイメージ・ファイルの PDF は、変換およびエンリッチできません。 

-   コレクション内の文書は、別の構成ファイルを選択しない限り、Default Configuration という名前の構成ファイルを使用して変換されます。構成ファイルの作成については、「[カスタム構成](/docs/services/discovery/building.html#custom-configuration)」を参照してください。

-   文書がデータ・コレクションにアップロードされると、そのコレクションに対して選択された構成ファイルを使用して文書が変換およびエンリッチされます。後でコレクションを別の構成ファイルに切り替えたい場合、切り替えは可能ですが、既にアップロードされている文書は元の構成ファイルによって変換されたままとなります。構成ファイルの切り替え後にアップロードされたすべての文書は、新しい構成ファイルを使用します。コレクション**全体**で新しい構成を使用する場合は、新規コレクションを作成し、新しい構成ファイルを選択してから、すべての文書を再度アップロードします。

## Discovery ツールによる文書のアップロード

1.  コレクションを作成します。「[文書用のサービスの準備](/docs/services/discovery/building.html#preparing-the-service-for-your-documents)」を参照してください。
1.  コレクションをクリックして開きます。
1.  **「文書のアップロード」**ボタンをクリックし、ドラッグ・アンド・ドロップまたはブラウズによって文書のアップロードを開始します。

これで、文書が変換およびエンリッチされるためにエンキューされます。この所要時間はコレクションのサイズによって決まります。索引付けとエンリッチメントが行われたあと、コレクションの詳細が**「概要」**セクションに表示されます。

-   **作成**日と**最終更新日**日 (`collection_id`、`configuration_id`、`environment_id` を表示するには、**「このコレクションを API で使用 (Use this collection in API)」**をクリックします)
-   コレクション内の**文書の数**
-   **構成** — このコレクションの変換に使用された構成ファイルの名前
-   **エラーと警告**

## API を使用した文書のアップロード

ステップバイステップのチュートリアルについては、「[{{site.data.keyword.discoveryshort}} API の入門 (Getting started with the Discovery API) ](/docs/services/discovery/getting-started.html)」を参照してください。

API について詳しくは、「[API reference ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}」を参照してください。

1.  `POST /v1/environments/{environment_id}/collections` メソッドを使用してコレクションを作成します。
1.  次に、`POST /v1/environments/{environment_id}/collections/{collection_id}/documents` メソッドを使用して文書をコレクションに追加します。

## URL のクロール

URL をクロールし、{{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} {{site.data.keyword.discoveryshort}} サービスの [Apache Nutch 向け索引付けプラグイン![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/IBM-Watson/nutch-indexer-discovery)を使用して索引付けを行うことができます。クロールは自動的には更新されないため、索引を最新の状態に保つには、この手順を定期的に繰り返す必要があります。
