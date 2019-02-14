---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-14"

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

# データ・ソースへの接続
{: #sources}

{{site.data.keyword.discoveryshort}} サービスを使用すると、リモート・ソースに接続したり、リモート・ソースから文書をクロールしたりすることができます。
{: shortdesc}

データ・ソースに関連付けるコレクションを構成することによって、(必要に応じて) スケジュールに基づいてデータ・ソースに接続し、{{site.data.keyword.discoveryshort}} サービスに文書をプルできます。各コレクションには、1 つのデータ・ソースを関連付けて構成できます。{{site.data.keyword.discoveryshort}} サービスは、クロールと呼ばれるプロセスを使用して、データ・ソースから文書をプルします。クロールとは、指定された開始ロケーションから文書を体系的に参照および取得するプロセスです。ユーザーが明示的に指定した項目のみが、{{site.data.keyword.discoveryshort}} サービスによってクロールされます。以下のタイプのデータ・ソースをクロールできます。

-  [Box](/docs/services/discovery/connect.html#connectbox)
-  [Salesforce](/docs/services/discovery/connect.html#connectsf)
-  [Microsoft SharePoint Online](/docs/services/discovery/connect.html#connectsp)

データ・ソースへの接続は、{{site.data.keyword.discoveryshort}} ツールまたは API を使用して実行できます。{{site.data.keyword.discoveryshort}} ツールは、ソース・システムについての理解をそれほど必要としない簡略化された接続方式を提供します。API は、接続先のソースについてより深く理解する必要がある、より細分化された、かつ詳細に構成することが可能なインターフェースを提供します。以下のプロセスの概要では、本資料で次に読むセクションが示されています。

1.  [一般ソース要件](/docs/services/discovery/connect.html#gen_req)を読んで、何が必要になるのかを全般的に理解してください。
2.  ソース・システムに固有の要件をお読みください。
    -  [Box](/docs/services/discovery/connect.html#connectbox)
    -  [Salesforce](/docs/services/discovery/connect.html#connectsf)
    -  [Microsoft SharePoint Online](/docs/services/discovery/connect.html#connectsp)
3.  構成の選択に基づいて、ソース構成の手順をお読みください。
    -  [ツールの使用](/docs/services/discovery/connect.html#source_tooling)
    -  [API の使用](/docs/services/discovery/connect.html#source_api)

## 一般ソース要件
{: #gen_req}

以下の一般要件は、すべてのデータ・ソースに適用されます。

-  Box、Salesforce、および SharePoint Online の個々の文書ファイルのサイズ制限は 10 MB です。
-  各データ・ソースの資格情報とファイルの場所 (または URL) が必要になります。これらは通常、データ・ソースの開発者/システム管理者によって提供されます。
-  データ・ソースのどのリソースをクロールするのかを把握している必要があります。これは、ソース管理者によって提供されます。Box または Salesforce をクロールする際に、{{site.data.keyword.discoveryshort}} ツールを使用してソースを構成している場合は、使用可能なリソースのリストが表示されます。
-  データ・ソースのクロールでは、データ・ソースのリソース (API 呼び出し) が使用されます。呼び出し回数は、クロールされる文書の数によって異なります。データ・ソースの適切なサービス・レベル (例: Enterprise) を取得する必要があります。ソース・システム管理者に確認してください。
-  {{site.data.keyword.discoveryshort}} は以下のファイル・タイプを取り込むことができますが、他のすべてのタイプの文書は無視されます。
   -  Microsoft Word
   -  PDF
   -  HTML
   -  JSON
-  {{site.data.keyword.discoveryshort}} のソース・クロールでは、コレクションに保管されている文書は削除されません。ソースが再クロールされると、新規文書が追加され、更新された文書は現行バージョンに変更され、削除された文書は最後に保管されたバージョンのままになります。

## Box
{: #connectbox}

Box ソースに接続する場合は、接続先のインスタンスが Enterprise プラン以上であることを確認してください。

{{site.data.keyword.discoveryshort}} と連携するための Box アカウントのセットアップ:

1.  `https://app.box.com/developers/console` (自社の Box URL を使用してください) で、新規の Box カスタム・アプリケーションを作成します。
1.  次に、以下のいずれかを実行します。
    - **「アプリケーションアクセス」**で`「Enterprise」`を選択し、既存の管理対象ユーザーを使用して続行します。または
    - **「アプリケーションアクセス」**で`「アプリケーション」`を選択し、[Box API![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.box.com/reference#create-app-user){: new_window} を使用して、新規に作成したアプリケーションで`アプリケーションユーザー`を作成します。
1.  以下の**「アプリケーションスコープ」**を有効にします。
    - `Box に格納されているすべてのファイルとフォルダの読み取りと書き込み`
    - `ユーザーの管理`
1.  以下の**「高度な機能」**を有効にします。
    - `ユーザーとして操作を実行`
    - `ユーザーアクセストークンを生成`
1.  `https://app.box.com/developers/console` の`クライアント ID` を`「API キー」`フィールドに入力することによって、アプリケーションのクライアント ID `https://app.box.com/master/settings/openbox` に権限を与えるように管理者に依頼します。
1.  `公開/秘密キーペア`を生成します (ご使用のコンピューターにダウンロードされます)。
1.  ダウンロードされたファイルを開き、フィールドを {{site.data.keyword.discoveryshort}} にコピー・アンド・ペーストします。{{site.data.keyword.discoveryshort}} にコピーするときに、`privateKey` の終わりにある末尾の改行 `\n` を削除します。

**注:** {{site.data.keyword.discoveryshort}} は、それ自体のカスタム・アプリケーション・クロールをサポートしません (自分自身の偽名を使用することはできません)。 

Box ソースに接続するには、以下の資格情報が必要です。これらは、Box 管理者から入手する必要があります (前のステップを使用し、Box カスタム・アプリケーションをセットアップして既に入手している場合を除きます)。

-  `client_id` - これらの資格情報が接続するソースの `client_id`。    
-  `enterprise_id` - これらの資格情報が接続する Box サイトの `enterprise_id`。
-  `client_secret` - これらの資格情報が接続するソースの `client_secret`。この値が返されることはありません。資格情報の作成時または変更時にのみ使用されます。
-  `public_key_id` - これらの資格情報が接続するソースの `public_key_id`。この値が返されることはありません。資格情報の作成時または変更時にのみ使用されます。
-  `private_key` - これらの資格情報が接続するソースの `private_key`。この値が返されることはありません。資格情報の作成時または変更時にのみ使用されます。
-  `passphrase` - これらの資格情報が接続するソースの `passphrase`。この値が返されることはありません。資格情報の作成時または変更時にのみ使用されます。

資格情報を識別する際には、[Box 開発者向けの資料![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.box.com/){: new_window}を参照すると役立つ場合があります。

Box のクロール時に考慮すべきその他の項目:

-  Box Note は JSON 形式で保管されるため、指定されたフォルダー内の Box Note はすべて {{site.data.keyword.discoveryshort}} によって取り込まれます。
-  API を使用する場合、クロールするフォルダーごとに、フォルダー ID と関連する所有者 ID のリストが必要になります。{{site.data.keyword.discoveryshort}} ツールを使用すると、クロールするコンテンツを参照および選択できます。

## Salesforce
{: #connectsf}

Salesforce ソースに接続する場合は、接続先のインスタンスが Enterprise プラン以上であることを確認してください。

Salesforce ソースに接続するには、以下の資格情報が必要です。これらは、Salesforce 管理者から入手する必要があります。
-  `url` - これらの資格情報が接続するソースの `url`。
-  `username` - これらの資格情報が接続するソースの `username`。
-  `password` - Salesforce パスワードと有効な Salesforce セキュリティー・トークンを連結したもので構成された `password`。この値が返されることはありません。資格情報の作成時または変更時にのみ使用されます。

資格情報を識別する際には、[Salesforce 開発者向けの資料![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.salesforce.com/docs/){: new_window}を参照すると役立つ場合があります。

Salesforce のクロール時に注意すべきその他の項目:

-  ナレッジ記事は、それらの **version** が `published` で、言語が `en-us` の場合にのみクロールされます。
-  API を使用する場合、クロールする Salesforce オブジェクトのリストが必要になります。{{site.data.keyword.discoveryshort}} ツールを使用すると、クロールするコンテンツを参照および選択できます。


## SharePoint Online
{: #connectsp}

Microsoft SharePoint Online ソースに接続する場合は、接続先のインスタンスが Enterprise (E1) プラン以上であることを確認してください。

SharePoint Online ソースに接続するには、以下の資格情報が必要です。これらは、SharePoint 管理者から入手する必要があります。

-  `organization_url` - これらの資格情報が接続するソースの `organization_url`。
-  `site_collection.path` - これらの資格情報が接続するソースの `site_collection.path`。
-  `username` - これらの資格情報が接続するソースの `client_id`。
-  `password` - これらの資格情報が接続するソースの `password`。この値が返されることはありません。資格情報の作成時または変更時にのみ使用されます。

資格情報を識別する際には、[Microsoft SharePoint 開発者向けの資料![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.microsoft.com/en-us/sharepoint/dev/){: new_window}を参照すると役立つ場合があります。

Microsoft SharePoint Online のクロール時に注意すべきその他の項目:

-  SharePoint をクロールする場合、クロールする SharePoint サイト・コレクション・パスのリストが必要になります。{{site.data.keyword.discoveryshort}} ツールを使用すると、クロールするコンテンツを参照および選択できます。SharePoint Online サイト全体をクロールする場合は、このフィールドで複数のパス (URL) を選択しないでください。その場合は、`site_collection.path` フィールドに `/` を入力します。

## ツールの使用
{: #source_tooling}

{{site.data.keyword.discoveryshort}} ツールを使用したデータ・ソースへの接続は、ソース専用のコレクションを作成することで実行されます。ソース・コレクションを作成してクロールするには、以下のステップを実行します。

1.  {{site.data.keyword.discoveryshort}} ツールの**「データの管理」**画面で、**「データ・ソースの接続 (Connect a data source)」**を選択します。
2.  接続先にするデータ・ソースを選択します。
3.  ソース資格情報を入力し、「接続」をクリックします。ソース資格情報は、ソース・システム管理者から入手する必要があります。
4.  クロールするデータと、それを同期する頻度を選択します。
5.  **「保存してオブジェクトを同期 (Save & Sync objects)」**をクリックし、データ・ソースのクロールを開始します。そうすると、コレクション状況画面にリダイレクトされます。この画面は、文書がコレクションに追加されると更新されます。

クロールは、最初にデータを同期し、次に指定した頻度で同期します。
**注:** **「同期の設定 (Sync settings)」**画面で変更を加えた場合、**「保存してオブジェクトを同期 (Save and Sync objects)」**をクリックすると、その時点でクロールが開始 (または既に実行中の場合は再始動) されます。

## API の使用
{: #source_api}

以下のプロセスを使用し、API を使用してデータ・ソースに接続されたコレクションを作成します。
1.  [ソース資格情報 API![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#credentials-api){: new_window} を使用して、接続先のソースの資格情報を作成します。返された、新しく作成した資格情報の **credential_id** を記録します。
2.  [構成 API![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#configurations-api){: new_window} を使用して、新規の構成を作成します。この構成には、クロール対象を定義する **source** オブジェクトが含まれている必要があります。**source** オブジェクトには、前に記録した **credential_id** が含まれている必要があります。
    ```json
    "source" : {
      "type" : "salesforce",
      "credential_id" : "{credential_id}",
      "schedule" : {
        "enabled" : true,
        "time_zone" : "America/New_York",
        "frequency" : "weekly"
      },
      "options" : {
         "site_collections" : [ {
         "site_collection_path" : "/sites/TestSiteA",
         "limit" : 10
         } ]
      }
    }
    ```
    {: codeblock}
    返された、新しく作成した構成の **configuration_id** を記録します。
3.  [コレクション API![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#configurations-api){: new_window} を使用して、新規のコレクションを作成します。コレクションを定義するオブジェクトには、前に記録した **configuration_id** が含まれている必要があります。

ソース・クロールは、コレクションが作成されるとすぐに開始され、指定した頻度で再び開始されます。
**注:** 構成の **source** オブジェクト内で変更を加えた場合、その時点で新規クロールが開始 (または既に実行中の場合は再始動) されます。

## `customer_id` の指定
{:# source_customer_id}

取り込まれた {{site.data.keyword.discoveryshort}} 文書内の`「customer_id」`フィールドは、API の **user-data** メソッドを使用して `customer_id` に基づいたコンテンツの削除を行う際に使用できます。データ・ソースから受け取る文書には、取り込まれたときに `customer_id` が自動的に割り当てられることはありません。 アプリケーションで `customer_id` を定義する必要がある場合は、ソース・システムから受け取る 1 つ以上のフィールドを、コピーして `customer_id` として使用するように指定できます。これを行うには、ソースへの接続に使用されている構成を変更する必要があります。

1.  サンプル照会を実行し、`customer_id` として使用するフィールドを特定します。
2.  構成を変更します。`「customer_id」`フィールドを作成するには、**「正規化 (Normalization)」**セクションを追加する必要があります。
    -  ツールでコレクションにナビゲートし、「構成 (configuration)」セクションの**「編集 (edit)」**リンクをクリックします。 次に、**「正規化 (Normalization)」** タブをクリックし、**「コピー」** の正規化を追加して `「customer_id」`フィールドを作成します。次に、**「適用して保存 (Apply & save)」** をクリックします。
    ![コピーの正規化](images/norm_copy.png)
    -  API を使用する場合は、以下のオブジェクトを **noramizations** 配列に追加します。
       ```json
       {
         "operation" : "copy",
         "source_field" : "{original_field_name}",
         "destination_field" : "customer_id"
       }
       ```
       {: codeblock}
3.  スケジュールされた次回のクロールで、`「customer_id」`フィールドがすべての文書に追加されます。クロールを即時に開始する場合は、ソース構成 (ツールの **「同期の設定 (Sync settings)」**) を変更します。

詳細および `customer_id` に基づく削除について詳しくは、 [機密保護 (Information security)![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.bluemix.net/docs/services/discovery/information-security.html){: new_window} を参照してください。
