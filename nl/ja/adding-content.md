---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-03-07"

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

# コンテンツの追加
{: #addcontent}

文書のアップロードに使用する方法は、どのように決めますか?
{: shortdesc}

-   コンテンツのアップロードを既存のアプリケーションに統合するか、独自のカスタム・アップロード・メカニズムを作成する場合は、[API](/docs/services/discovery?topic=discovery-gs-api#gs-api) を使用します。
-   ローカルでアクセス可能なファイルを迅速にアップロードする場合は、[{{site.data.keyword.discoveryshort}} ツール](/docs/services/discovery?topic=discovery-getting-started#getting-started)を使用します。
    {{site.data.keyword.discoveryshort}} ツールを使用して文書をアップロードする場合は、すべての文書が固有のファイル名を持っている必要があります。 2 つのファイルが同じ名前を持つ場合は、新しいバージョンのアップロード時にオリジナルが上書きされます。 同じファイル名を持つ文書をコレクション内に共存させたい場合は、文書 ID を指定する必要があります。 API またはデータ・クローラーを使用して文書をアップロードする場合は、文書 ID を指定できます。
-   {{site.data.keyword.discoveryshort}} ツールまたは API を使用して、Box、Salesforce、Microsoft SharePoint Online、IBM Cloud オブジェクト・ストレージ、および Microsoft SharePoint 2016 のデータ・ソースに接続したり、Web クロールを実行したりできます。詳しくは、『[データ・ソースへの接続](/docs/services/discovery?topic=discovery-sources#sources)』を参照してください。
-   管理対象アップロードで多数のファイルを扱う場合、またはサポートされているリポジトリー (DB2 データベースなど) からコンテンツを抽出する場合は、[データ・クローラー](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)を使用します。

## API またはツールを使用したコンテンツの追加
{: #adding-content-with-the-api-or-tooling}

コレクションに文書を追加する準備ができたら、以下を検討します。

-   {{site.data.keyword.discoveryshort}} サービスにアップロードできる最大ファイル・サイズは 50 MB です。
-   サンプル文書は、自動的にはコレクションに追加されません。 サンプル文書をコレクションの一部にしたい場合は、そのサンプル文書を追加する必要があります。 ([Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu) のリリース前に作成されたコレクションにのみ適用されます。)
-   エンリッチメントのために選択された各 JSON フィールドの最初の 50,000 文字のみがエンリッチされます。
-   コレクションを作成するときは、文書言語を選択します (デフォルトは英語)。 言語のリストについては、[言語サポート](/docs/services/discovery?topic=discovery-language-support#language-support)を参照してください。 選択した言語で文書がエンリッチされます。 同じコレクション内で言語を混用しないでください。
-   {{site.data.keyword.discoveryshort}} は以下のファイル・タイプを取り込むことができますが、他のすべての文書タイプは無視されます。

コレクション | ライト・プラン | 拡張プラン 
---------------- | ------------------------------ | ------------------------------------------- 
[Smart Document Understanding (SDU)](/docs/services/discovery?topic=discovery-release-notes#22jan19) のリリース前に、{{site.data.keyword.discoveryfull}} 用に特別に作成された既存のコレクション | Microsoft Word、PDF、HTML、JSON | Microsoft Word、PDF、HTML、JSON     
[SDU](/docs/services/discovery?topic=discovery-sdu#sdu) のリリース後に作成されたコレクション | PDF、Word、PowerPoint、Excel、JSON\*、HTML\* | PDF、Word、PowerPoint、Excel、PNG\*\*、TIFF\*\*、JPG\*\*、JSON\*、HTML\* 
    
\* JSON 文書と HTML 文書は {{site.data.keyword.discoveryfull}} でサポートされていますが、SDU エディターでは編集できません。HTML 文書と JSON 文書の構成を変更するには、API を使用する必要があります。詳しくは、「[API reference ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery/){: new_window}」を参照してください。

\*\* 個々の画像ファイル (PNG、TIFF、JPG) がスキャンされ、テキスト (存在する場合) が抽出されます。PDF、Word、PowerPoint、および Excel の各ファイルに埋め込まれている PNG、TIFF、および JPEG の各画像もスキャンされ、テキスト (存在する場合) が抽出されます。
-   コレクション内の文書は、別の構成ファイルを選択しない限り、現在の構成を使用して変換されます。構成ファイルの作成については、「[カスタム構成](/docs/services/discovery?topic=discovery-configservice#custom-configuration)」を参照してください。 ([Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu) のリリース前に作成されたコレクションにのみ適用されます。)
-   文書はデータ・コレクションにアップロードされると、そのコレクション用に選択された構成ファイルを使用して変換およびエンリッチされます。 後でコレクションを別の構成ファイルに切り替えたい場合、切り替えは可能ですが、既にアップロードされている文書は元の構成ファイルによって変換されたままとなります。 構成ファイルの切り替え後にアップロードされたすべての文書は、新しい構成ファイルを使用します。 コレクション**全体**で新しい構成を使用する場合は、新規コレクションを作成し、新しい構成ファイルを選択してから、すべての文書を再度アップロードすることが必要になります。 ([Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu) を使用している場合、**「変更をコレクションに適用 (Apply changes to collection)」**ボタンをクリックすると、文書の再アップロードを求めるプロンプトが出されます。)
-   フィールドの`データ・タイプ` (例: `text` や `date`) を指定することはできません。 文書の取り込み中に、索引にまだ存在しないフィールドが検出されると、{{site.data.keyword.discoveryshort}} は、索引付けられた最初の文書のそのフィールドの値に基づいて、そのフィールドの`データ・タイプ`を自動的に検出します。
-   現行文書内のデータと前に取り込まれた文書内の類似データとの間にタイプの不一致があるため、文書の取り込みが失敗することがあります。 例えば、ある文書内で `date` タイプとされているフィールドが後続の文書では `string` である場合、その後続文書は正しく索引付けされません。
-   カスタムのトークン化 (現在は {{site.data.keyword.discoveryshort}} API の使用時に日本語コレクションでのみ使用可能) を使用する予定の場合、文書をアップロードする前にコレクション用のトークン化辞書を追加する必要があります。

## Discovery ツールによる文書のアップロード
{: #upload_tooling}

1.  コレクションを作成します。 「[文書用のサービスの準備](/docs/services/discovery?topic=discovery-configservice#preparing-the-service-for-your-documents)」を参照してください。
1.  コレクションをクリックして開きます。
1.  **「文書のアップロード」**ボタンをクリックし、ドラッグ・アンド・ドロップまたはブラウズによって文書のアップロードを開始します。

これで、文書が変換およびエンリッチされるためにエンキューされます。 この所要時間はコレクションのサイズによって決まります。 索引付けとエンリッチが行われたあと、コレクションの詳細が**「概要」**セクションに表示されます。

-   コレクションの**識別されたフィールド** (Smart Document Understanding のみ。)
-   **作成**日と**最終更新**日 (`collection_id`、`configuration_id`、`environment_id` を表示するには、**「このコレクションを API で使用 (Use this collection in API)」**をクリックします)
-   コレクション内の**文書の数**
-   **構成** — このコレクションの変換に使用された構成ファイルの名前 ([Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu) のリリース前に作成されたコレクションの場合のみ。)
-   **エラーと警告**

{{site.data.keyword.discoveryshort}} ツールを使用した Box、Salesforce、Microsoft SharePoint Online、IBM Cloud オブジェクト・ストレージ、および Microsoft SharePoint 2016 の各データ・ソースへの接続、または Web クロールを行う方法については、[データ・ソースへの接続](/docs/services/discovery?topic=discovery-sources#sources)を参照してください。


## API を使用した文書のアップロード
{: #upload_api}

ステップバイステップのチュートリアルについては、「[{{site.data.keyword.discoveryshort}} API の入門 (Getting started with the Discovery API) ](/docs/services/discovery?topic=discovery-gs-api#gs-api)」を参照してください。

API について詳しくは、「[API reference ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery/){: new_window}」を参照してください。

1.  `POST /v1/environments/{environment_id}/collections` メソッドを使用してコレクションを作成します。
1.  次に、`POST /v1/environments/{environment_id}/collections/{collection_id}/documents` メソッドを使用して文書をコレクションに追加します。

## URL のクロール
{: #crawl_urls}

URL をクロールし、{{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} {{site.data.keyword.discoveryshort}} サービスの [Apache Nutch 向け索引付けプラグイン![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/IBM-Watson/nutch-indexer-discovery)を使用して索引付けを行うことができます。 クロールは自動的には更新されないため、索引を最新の状態に保つには、この手順を定期的に繰り返す必要があります。 

ベータ版 Web Crawl コネクターを使用するオプションもあります。[データ・ソースへの接続](/docs/services/discovery?topic=discovery-sources#connectwebcrawl)を参照してください。
