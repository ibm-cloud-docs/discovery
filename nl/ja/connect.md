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

# データ・ソースへの接続
{: #sources}

{{site.data.keyword.discoveryshort}} サービスを使用すると、リモート・ソースに接続したり、リモート・ソースから文書をクロールしたりすることができます。
{: shortdesc}

データ・ソースに関連付けるコレクションを構成することによって、(必要に応じて) スケジュールに基づいてデータ・ソースに接続し、{{site.data.keyword.discoveryshort}} サービスに文書をプルできます。 {{site.data.keyword.discoveryshort}} ツールを使用する場合は、データ・ソースはコレクションごとに 1 つ構成できます。API を使用する場合は、複数のデータ・ソースの文書を単一のコレクションに送信できます。{{site.data.keyword.discoveryshort}} サービスは、クロールと呼ばれるプロセスを使用して、データ・ソースから文書をプルします。 クロールとは、指定された開始ロケーションから文書を体系的に参照および取得するプロセスです。 ユーザーが明示的に指定した項目のみが、{{site.data.keyword.discoveryshort}} サービスによってクロールされます。 以下のタイプのデータ・ソースをクロールできます。

-  [Box](/docs/services/discovery?topic=discovery-sources#connectbox)
-  [Salesforce](/docs/services/discovery?topic=discovery-sources#connectsf)
-  [Microsoft SharePoint Online](/docs/services/discovery?topic=discovery-sources#connectsp)
-  [Microsoft SharePoint 2016 On-Premise](/docs/services/discovery?topic=discovery-sources#connectsp_op)
-  [Web Crawl](/docs/services/discovery?topic=discovery-sources#connectwebcrawl) (ベータ)
-  [IBM Cloud オブジェクト・ストレージ](/docs/services/discovery?topic=discovery-sources#connectcos)

データ・ソースへの接続は、{{site.data.keyword.discoveryshort}} ツールまたは API を使用して実行できます。 {{site.data.keyword.discoveryshort}} ツールは、ソース・システムについての理解をそれほど必要としない簡略化された接続方式を提供します。API は、接続先のソースについてより深く理解する必要がある、より細分化された、かつ詳細に構成することが可能なインターフェースを提供します。 以下のプロセスの概要では、本資料で次に読むセクションが示されています。

1.  [一般ソース要件](/docs/services/discovery?topic=discovery-sources#gen_req)を読んで、何が必要になるのかを全般的に理解してください。
2.  ソース・システムに固有の要件をお読みください。
    -  [Box](/docs/services/discovery?topic=discovery-sources#connectbox)
    -  [Salesforce](/docs/services/discovery?topic=discovery-sources#connectsf)
    -  [Microsoft SharePoint Online](/docs/services/discovery?topic=discovery-sources#connectsp)
    -  [Microsoft SharePoint 2016 On-Premise](/docs/services/discovery?topic=discovery-sources#connectsp_op)
    -  [Web Crawl](/docs/services/discovery?topic=discovery-sources#connectwebcrawl) (ベータ)
    -  [IBM Cloud オブジェクト・ストレージ](/docs/services/discovery?topic=discovery-sources#connectcos)
3.  構成の選択に基づいて、ソース構成の手順をお読みください。
    -  [ツールの使用](/docs/services/discovery?topic=discovery-sources#source_tooling)
    -  [API の使用](/docs/services/discovery?topic=discovery-sources#source_api)

オンプレミスのデータ・ソースを選択する場合は、先に IBM Secure Gateway をインストールして構成しておく必要があります。詳しくは、『[オンプレミス・データのための IBM Secure Gateway のインストール](/docs/services/discovery?topic=discovery-sources#gateway)』を参照してください。

## 一般ソース要件
{: #gen_req}

以下の一般要件は、すべてのデータ・ソースに適用されます。

-  Box、Salesforce、SharePoint Online、SharePoint 2016、IBM Cloud オブジェクト・ストレージ、および Web Crawl の個々の文書ファイルのサイズ制限は 10 MB です。
-  各データ・ソースの資格情報とファイルの場所 (または URL) が必要になります。これらは通常、データ・ソースの開発者/システム管理者によって提供されます。
-  データ・ソースのどのリソースをクロールするのかを把握している必要があります。 これは、ソース管理者によって提供されます。 Box または Salesforce をクロールする際に、{{site.data.keyword.discoveryshort}} ツールを使用してソースを構成している場合は、使用可能なリソースのリストが表示されます。
-  {{site.data.keyword.discoveryshort}} ツールを使用する場合は、1 つのコレクションに 1 つのデータ・ソースを構成できます。API を使用する場合は、複数のデータ・ソースの文書を単一のコレクションに送信できます。
-  データ・ソースのクロールでは、データ・ソースのリソース (API 呼び出し) が使用されます。 API 呼び出しの回数は、クロールする文書の数によって決まります。データ・ソースの適切なレベルのサービス・ライセンス (例: Enterprise) を取得している必要があります。ソース・システムの管理者に確認してください。
-  {{site.data.keyword.discoveryshort}} のソース・クロールでは、コレクションに保管されている文書は削除されません。 ソースが再クロールされると、新規文書が追加され、更新された文書は現行バージョンに変更され、削除された文書は最後に保管されたバージョンのままになります。
-  {{site.data.keyword.discoveryshort}} は以下のファイル・タイプを取り込むことができますが、他のすべての文書タイプは無視されます。

コレクション | ライト・プラン | 拡張プラン 
---------------- | ------------------------------ | ------------------------------------------- 
[Smart Document Understanding (SDU)](/docs/services/discovery?topic=discovery-release-notes#22jan19) のリリース前に、{{site.data.keyword.discoveryfull}} 用に特別に作成された既存のコレクション | Microsoft Word、PDF、HTML、JSON | Microsoft Word、PDF、HTML、JSON     
[SDU](/docs/services/discovery?topic=discovery-sdu#sdu) のリリース後に作成されたコレクション | PDF、Word、PowerPoint、Excel、JSON\*、HTML\* | PDF、Word、PowerPoint、Excel、PNG\*\*、TIFF\*\*、JPG\*\*、JSON\*、HTML\* 
    
\* JSON 文書と HTML 文書は {{site.data.keyword.discoveryfull}} でサポートされていますが、SDU エディターでは編集できません。HTML 文書と JSON 文書の構成を変更するには、API を使用する必要があります。詳しくは、「[API reference ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery/){: new_window}」を参照してください。

\*\* 個々の画像ファイル (PNG、TIFF、JPG) がスキャンされ、テキスト (存在する場合) が抽出されます。PDF、Word、PowerPoint、および Excel の各ファイルに埋め込まれている PNG、TIFF、および JPEG の各画像もスキャンされ、テキスト (存在する場合) が抽出されます。

## Box
{: #connectbox}

{{site.data.keyword.discoveryfull}} に接続する Box カスタム・アプリケーションを新規作成する必要があります。作成する Box アプリケーションには、エンタープライズ・レベルまたはアプリケーション・レベルのアクセスが必要です。

-  組織の Box 管理者でない場合は、[**アプリケーション・レベル**のアクセス](/docs/services/discovery?topic=discovery-sources#applevelbox)をお勧めします。管理者にアプリケーションを承認してもらう必要があります。
-  組織の Box 管理者である場合は、[**エンタープライズ・レベル**のアクセス](/docs/services/discovery?topic=discovery-sources#entlevelbox)をお勧めします。

Box のアップデートによって、Box のアクセスをセットアップするこの手順は変わる可能性があります。アップデートについて確認するには、[Box 開発者の資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.box.com/){: new_window} を参照してください。
{: note}

### アプリケーション・レベルのアクセスのセットアップ
{: #applevelbox}

1.   `https://app.box.com/developers/console` (自社の Box URL を使用してください) にナビゲートし、**「アプリの新規作成」**をクリックします。
1.   **「アプリの新規作成」**画面で、**「企業統合」**を選択し、**「次へ」**をクリックします。
1.   **「認証方法」**画面で、**「JWT を使用した OAuth 2.0 (サーバー認証)」**を選択し、**「次へ」**をクリックします。
1.   アプリに名前を付け、**「アプリの作成」**ボタンをクリックします。 Box アプリが作成されたら、**「アプリの表示」**をクリックします。
1.   アプリを表示したら、**「アプリケーションアクセス」**で**「アプリケーション」**を選択します。既存の管理対象ユーザーを使用して続行できます。新規ユーザーを作成する必要はありません。
1.   このページの**「アプリケーションスコープ」**セクションまでスクロールダウンし、以下のチェック・ボックスを有効にします。 
     - `Box に格納されているすべてのファイルとフォルダの読み取りと書き込み`
     - `ユーザーを管理`
1.   **「高度な機能」**セクションまでスクロールダウンし、以下のトグルを有効にします。
     - `ユーザーとして操作を実行`
     - `ユーザーアクセストークンを生成` 
1.  **「変更の保存」**ボタンをクリックします。

次の数手順は、組織の Box アカウントの管理者に支援してもらう必要があります。自分が組織の Box 管理者でない場合は、Box の開発者コンソールを開き、**「アカウント設定」**>**「アカウントの詳細」**>**「設定」**の下を参照して、管理者が誰か確認してください。

1.  [管理者の手順] `https://app.box.com/master/settings/openbox` で**「新しいアプリケーションを承認」**ボタンをクリックし、アプリケーションのクライアント ID を承認します。
1.  [管理者の手順] `https://app.box.com/developers/console` で取得した**クライアント ID** を**「API キー」**フィールドに入力し、**「承認」**ボタンをクリックします。
1.  [管理者の手順] アプリケーション用の開発者トークンを取得します。これを行うには、`https://app.box.com/developers/console` にナビゲートし、**「開発者トークン」**セクションまでスクロールし、トークンを生成します。
1.  これでアプリケーションが管理者から承認されました。次は、`https://developer.box.com/reference#page-create-an-enterprise-user` にナビゲートし、API リファレンス・ページを使用してアプリ・ユーザーを作成します。

   アプリ・ユーザーを作成する curl の例:

   ```bash
    curl https://api.box.com/2.0/users -H "Authorization: Bearer ACCESS_TOKEN" -d '{"name": "NedStark", "is_platform_access_only": true}' -X POST
   ```
   {: pre}

1.  新しく生成された **id** フィールドの内容をコピーし、Box アプリケーションを {{site.data.keyword.discoveryfull}} に接続する非管理者に提供します。
1.  アプリ・ユーザーを作成したら、クロールするフォルダーをそのアプリ・ユーザーと共有する必要があります。そのために、それらのフォルダーに対する`ビューアー`の許可をアプリ・ユーザーに付与する必要があります。これには、上記 curl コマンドの応答に含まれているアプリ・ユーザーのログイン名が必要です。例えば、`"login":"AppUser_737729_jmUo@boxdevedition.com"` です。
1.  Box 開発者のコンソール (`https://app.box.com/developers/console`) に戻り、**「公開キーの追加と管理」**セクションまでスクロールします。**「公開/秘密キーペアを生成」**をクリックして、鍵ペア・ファイルをダウンロードします。ファイルを開きます。
1.  鍵ペア・ファイルの以下のフィールドを {{site.data.keyword.discoveryshort}} ツールにカット・アンド・ペーストします。
    -  `client_id`
    -  `enterprise_id`
    -  `client_secret` 
    -  `public_key_id` 
    -  `private_key` 
    -  `passphrase` 

### エンタープライズ・レベルのアクセス権限のセットアップ
{: #entlevelbox}

1.  `https://app.box.com/developers/console` (自社の Box URL を使用してください) にナビゲートし、**「アプリの新規作成」**をクリックします。
1.  **「アプリの新規作成」**画面で、**「企業統合」**を選択し、**「次へ」**をクリックします。
1.  **「認証方法」**画面で、**「JWT を使用した OAuth 2.0 (サーバー認証)」**を選択し、**「次へ」**をクリックします。
1.  アプリに名前を付け、**「アプリの作成」**ボタンをクリックします。 Box アプリが作成されたら、**「アプリの表示」**をクリックします。
1.  アプリを表示したら、**「アプリケーションアクセス」**で**「Enterprise」**を選択します。既存の管理対象ユーザーを使用して続行できます。新規ユーザーを作成する必要はありません。
1.  このページの**「アプリケーションスコープ」**セクションまでスクロールダウンし、以下のチェック・ボックスを有効にします。 
    - `Box に格納されているすべてのファイルとフォルダの読み取りと書き込み`
    - `ユーザーを管理`
    - `エンタープライズのプロパティを管理`
1.  **「高度な機能」**セクションまでスクロールダウンし、以下のトグルを有効にします。
    - `ユーザーとして操作を実行`
    - `ユーザーアクセストークンを生成` 
1.  **「変更の保存」**ボタンをクリックします。

`リフレッシュ`は、エンタープライズ・レベルのアクセス権限でのみサポートされます。
{: note}

Box アプリの設定を変更した場合は、変更を有効にするためにアプリを`再承認`してください。
{: tip}

次の数手順は、組織の Box アカウントの管理者に支援してもらう必要があります。自分が組織の Box 管理者でない場合は、Box の開発者コンソールを開き、**「アカウント設定」**>**「アカウントの詳細」**>**「設定」**の下を参照して、管理者が誰か確認してください。

1.  [管理者の手順] **「管理コンソール」**>**「Enterprise 設定」**>**「アプリ」**の順にナビゲートし、`「カスタムアプリケーション」`までスクロールし、アプリケーションのクライアント ID を承認します。URL の例は、`https://app.box.com/master/settings/openbox` です。
1.  [管理者の手順] `https://app.box.com/developers/console` で取得した**クライアント ID** を**「API キー」**フィールドに入力し、**「承認」**ボタンをクリックします。
1.  Box 開発者のコンソール (`https://app.box.com/developers/console`) に戻り、**「公開キーの追加と管理」**セクションまでスクロールします。**「公開/秘密キーペアを生成」**をクリックして、鍵ペア・ファイルをダウンロードします。ファイルを開きます。
1.  鍵ペア・ファイルの以下のフィールドを {{site.data.keyword.discoveryshort}} ツールにカット・アンド・ペーストします。
    -  `client_id`
    -  `enterprise_id`
    -  `client_secret` 
    -  `public_key_id` 
    -  `private_key` 
    -  `passphrase` 

Box のクロール時に考慮すべきその他の項目:

-  Box Note は JSON 形式で保管されるため、指定されたフォルダー内の Box Note はすべて {{site.data.keyword.discoveryshort}} によって取り込まれます。
-  API を使用する場合、クロールするフォルダーごとに、フォルダー ID と関連する所有者 ID のリストが必要になります。 {{site.data.keyword.discoveryshort}} ツールを使用すると、クロールするコンテンツを参照および選択できます。

## Salesforce
{: #connectsf}

Salesforce ソースに接続する場合は、接続先のインスタンスが Enterprise プラン以上であることを確認してください。

Salesforce ソースに接続するには、以下の資格情報が必要です。これらは、Salesforce 管理者から入手する必要があります。
-  `url` - これらの資格情報が接続するソースの `url`。
-  `username` - これらの資格情報が接続するソースの `username`。
-  `password` - Salesforce パスワードと有効な Salesforce セキュリティー・トークンを連結したもので構成された `password`。 この値が返されることはありません。資格情報の作成時または変更時にのみ使用されます。

資格情報を識別する際には、[Salesforce 開発者向けの資料![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.salesforce.com/docs/){: new_window}を参照すると役立つ場合があります。

Salesforce のクロール時に注意すべきその他の項目:

-  ナレッジ記事は、それらの **version** が `published` で、言語が `en-us` の場合にのみクロールされます。
-  API を使用する場合、クロールする Salesforce オブジェクトのリストが必要になります。 {{site.data.keyword.discoveryshort}} ツールを使用すると、クロールするコンテンツを参照および選択できます。

## SharePoint Online
{: #connectsp}

Microsoft SharePoint Online ソースに接続する場合は、接続先のインスタンスが Enterprise (E1) プラン以上であることを確認してください。

SharePoint Online ソースに接続するには、以下の資格情報が必要です。これらは、SharePoint 管理者から入手する必要があります。

-  `organization_url` - これらの資格情報が接続するソースの `organization_url`。
-  `site_collection_path` - これらの資格情報が接続するソースの `site_collection_path`。
-  `username` - これらの資格情報が接続するソースの `client_id`。 このユーザーは、クロールして索引を作成するすべてのサイトとリストに対してアクセス権限を持っている必要があります。
-  `password` - これらの資格情報が接続するソースの `password`。 この値が返されることはありません。資格情報の作成時または変更時にのみ使用されます。

資格情報を識別する際には、[Microsoft SharePoint 開発者向けの資料![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.microsoft.com/en-us/sharepoint/dev/){: new_window}を参照すると役立つ場合があります。

Microsoft SharePoint Online のクロール時に注意すべきその他の項目:

-  SharePoint をクロールするには、`クロール・ユーザー`・アカウントが `SiteCollection Administrator` 許可を持っていなければなりません。
-  SharePoint をクロールする場合には、クロールする SharePoint サイト・コレクション・パスのリストが必要です。{{site.data.keyword.discoveryshort}} では、フォルダー・パスは入力できません。 

## Web Crawl
{: #connectwebcrawl}

このベータ版フィーチャーを使用すると、パスワードを必要としない公開 Web サイトをクロールできます。{{site.data.keyword.discoveryshort}} を Web サイトに同期する頻度や、言語、ホップ数を選択できます。

-  `マイ・データの同期 (Sync my data)` - 同期間隔として 5 分単位、毎時、毎日、毎週、または毎月から選択できます。 
-  `言語の選択 (Select language)` - サポートされる言語のリストから、Web サイトの言語を選択します。{{site.data.keyword.discoveryshort}} でサポートされている言語のリストについては、[言語サポート](/docs/services/discovery?topic=discovery-language-support#supported-languages)を参照してください。言語ごとに別々のコレクションを作成することをお勧めします。
-  `同期する URL グループ (URL group to sync)` - 使用する URL を入力し、正符号をクリックして URL グループにその URL を追加します。この URL グループの**クロール設定**を指定するには、![Cog](images/icon_settings.png) アイコンをクリックします。**「最大ホップ数 (Maximum hops)」**を設定できます。これは、先頭 URL (先頭 URL は `0` になります) の後に続く連続したリンクの数です。デフォルトのホップ数は `2` で、最大数は `20` です (API を使用する場合は、最大数は `1000` です)。 

このベータ版では、クロールする Web ページの数に制限があるため、最大ホップ数に到達するまで、指定したすべての Web サイトを Web クローラーがクロールしない場合があります。
{: note}

他の URL 用に別の**「クロール設定 (Crawl settings)」**が必要な場合は、**「URL グループの追加 (Add URL group)」**をクリックして、新規グループを作成します。URL グループは、必要な数だけ作成できます。
{: tip}

## SharePoint 2016 On-Premise
{: #connectsp_op}

Microsoft SharePoint 2016 (別名 SharePoint Server 2016) は、オンプレミスのデータ・ソースです。これに接続するには、まず IBM Secure Gateway をインストールして構成しておく必要があります。詳しくは、『[オンプレミス・データのための IBM Secure Gateway のインストール](/docs/services/discovery?topic=discovery-sources#gateway)』を参照してください。
{: note}

SharePoint 2016 データ・ソースに接続するには、以下の資格情報が必要です。これらは、SharePoint 管理者から入手する必要があります。

-  `username` - これらの資格情報が接続するソースの `client_id`。 このユーザーは、クロールして索引を作成するすべてのサイトとリストに対してアクセス権限を持っている必要があります。
-  `password` - これらの資格情報が接続するソースの `password`。 この値が返されることはありません。資格情報の作成時または変更時にのみ使用されます。
-  `web_application_url` - SharePoint 2016 の `web_application_url` (例えば https://sharepointwebapp.com:8443)。ポートを指定しない場合は、デフォルトでポート `80` (http) とポート `443` (https) が設定されます。
-  `domain` - SharePoint 2016 アカウントの `domain`。

資格情報を識別する際には、[Microsoft SharePoint 開発者向けの資料![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.microsoft.com/en-us/sharepoint/dev/){: new_window}を参照すると役立つ場合があります。

Microsoft SharePoint 2016 のクロール時に注意すべきその他の項目:

-  SharePoint 2016 をクロールするには、`クロール・ユーザー`・アカウントが `SiteCollection Administrator` 許可を持っていなければなりません。
-  SharePoint をクロールする場合には、クロールする SharePoint サイト・コレクション・パスのリストが必要です。{{site.data.keyword.discoveryshort}} では、フォルダー・パスは入力できません。 

## IBM Cloud オブジェクト・ストレージ
{: #connectcos}

IBM Cloud オブジェクト・ストレージのソースに接続する場合は、以下の資格情報が必要です。これらは、IBM Cloud オブジェクト・ストレージ管理者から取得する必要があります。

-  `endpoint` - IBM Cloud オブジェクト・ストレージ・データとの対話に使用する`エンドポイント`。
-  `access_key_id` - IBM Cloud オブジェクト・ストレージ・インスタンスの作成時に取得した `access_key_id`。
-  `secret_access_key` - IBM Cloud オブジェクト・ストレージ・インスタンスの作成時に取得した、要求に署名するための `secret_access_key`。

この情報を入力したら、データの同期頻度を選択し、同期先にするバケットを選択できます。

IBM Cloud オブジェクト・ストレージのクロールに関するその他の注意事項を次に示します。

-  このコネクターでは、プライベート・エンドポイントのクロールはサポートされません。
-  すべてのバケットを選択すると、パフォーマンスに若干問題が生じることがあります。この場合、文書の索引作成が完了する前に、遅延が発生することがあります。

## ツールの使用
{: #source_tooling}

{{site.data.keyword.discoveryshort}} ツールを使用したデータ・ソースへの接続は、ソース専用のコレクションを作成することで実行されます。 ソース・コレクションを作成してクロールするには、以下のステップを実行します。

1.  {{site.data.keyword.discoveryshort}} ツールの**「データの管理」**画面で、**「データ・ソースの接続 (Connect a data source)」**を選択します。
2.  接続先にするデータ・ソースを選択します。 オンプレミスのデータ・ソースを選択した場合は、まず IBM Secure Gateway をインストールする必要があります。詳しくは、『[オンプレミス・データのための IBM Secure Gateway のインストール](/docs/services/discovery?topic=discovery-sources#gateway)』を参照してください。 
3.  ソース資格情報を入力し、「接続」をクリックします。 ソース資格情報は、ソース・システム管理者から入手する必要があります。
4.  クロールするデータと、それを同期する頻度を選択します。 同期オプションは、以下のとおりです。
    -  5 分ごと: 5 分ごとに実行する
    -  毎時: 1 時間ごとに実行する
    -  毎日: 毎日、指定したタイム・ゾーンの 00:00 から 06:00 までの間に実行する
    -  毎週: 毎週日曜日に、指定したタイム・ゾーンの 00:00 から 06:00 までの間に実行する
    -  毎月: 毎月の第 1 日曜日に、指定したタイム・ゾーンの 00:00 から 06:00 までの間に実行する
    
    以下に、クロールの状況の例を示します。
    
    ```json
    "crawl_status" : {
    "source_crawl" : {
      "status" : "completed",
      "next_crawl" : "2019-02-10T05:00:00-05:00"
    }
    ```
5.  **「保存してオブジェクトを同期 (Save & Sync objects)」**をクリックし、データ・ソースのクロールを開始します。 そうすると、コレクション状況画面にリダイレクトされます。この画面は、文書がコレクションに追加されると更新されます。

クロールは、最初にデータを同期し、次に指定した頻度で同期します。
**注:** **「同期の設定 (Sync settings)」**画面で変更を加えた場合、**「保存してオブジェクトを同期 (Save and Sync objects)」**をクリックすると、その時点でクロールが開始 (または既に実行中の場合は再始動) されます。

## API の使用
{: #source_api}

以下のプロセスを使用し、API を使用してデータ・ソースに接続されたコレクションを作成します。

オンプレミスのデータ・ソースに接続する場合は、まず IBM Secure Gateway をインストールする必要があります。詳しくは、『[オンプレミス・データのための IBM Secure Gateway のインストール](/docs/services/discovery?topic=discovery-sources#gateway)』を参照してください。 

以下の例では、SharePoint データ・ソースを使用します。

1.  [ソース資格情報 API![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery#create-credentials){: new_window} を使用して、接続先のソースの資格情報を作成します。 返された、新しく作成した資格情報の **credential_id** を記録します。
2.  [構成 API![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery#add-configuration){: new_window} を使用して、新規の構成を作成します。 この構成には、クロール対象を定義する **source** オブジェクトが含まれている必要があります。 **source** オブジェクトには、前に記録した **credential_id** が含まれている必要があります。
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
3.  [コレクション API![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery#create-a-collection){: new_window} を使用して、新規のコレクションを作成します。 コレクションを定義するオブジェクトには、前に記録した **configuration_id** が含まれている必要があります。

ソース・クロールは、コレクションが作成されるとすぐに開始され、指定した頻度で再び開始されます。
**注:** 構成の **source** オブジェクト内で変更を加えた場合、その時点で新規クロールが開始 (または既に実行中の場合は再始動) されます。

### `customer_id` の指定
{: #source_customer_id}

取り込まれた {{site.data.keyword.discoveryshort}} 文書内の`「customer_id」`フィールドは、API の **user-data** メソッドを使用して `customer_id` に基づいたコンテンツの削除を行う際に使用できます。 データ・ソースから受け取る文書には、取り込まれたときに `customer_id` が自動的に割り当てられることはありません。 アプリケーションで `customer_id` を定義する必要がある場合は、ソース・システムから受け取る 1 つ以上のフィールドを、コピーして `customer_id` として使用するように指定できます。 これを行うには、ソースへの接続に使用されている構成を変更する必要があります。

1.  サンプル照会を実行し、`customer_id` として使用するフィールドを特定します。
2.  構成を変更します。 `「customer_id」`フィールドを作成するには、**「正規化 (Normalization)」**セクションを追加する必要があります。
    -  ツールでコレクションにナビゲートし、「構成 (configuration)」セクションの**「編集 (edit)」**リンクをクリックします。 次に、**「正規化 (Normalization)」** タブをクリックし、**「コピー」** の正規化を追加して `「customer_id」`フィールドを作成します。 次に、**「適用して保存 (Apply & save)」** をクリックします。
    ![コピーの正規化](images/norm_copy.png)
    -  API を使用する場合は、次のオブジェクトを **normalizations** 配列に追加します。
       ```json
       {
         "operation" : "copy",
         "source_field" : "{original_field_name}",
         "destination_field" : "customer_id"
       }
       ```
       {: codeblock}
3.  スケジュールされた次回のクロールで、`「customer_id」`フィールドがすべての文書に追加されます。 クロールを即時に開始する場合は、ソース構成 (ツールの **「同期の設定 (Sync settings)」**) を変更します。

詳細および `customer_id` に基づく削除について詳しくは、[機密保護 (Information security)](/docs/services/discovery?topic=discovery-information-security#information-security)を参照してください。

## オンプレミス・データのための IBM Secure Gateway のインストール 
{: #gateway}

オンプレミスのデータ・ソースに接続するには、まず IBM Secure Gateway をダウンロードし、インストールして構成する必要があります。最初のオンプレミスのデータ・ソース用に IBM Secure Gateway をインストールしたら、このプロセスを繰り返す必要はありません。

1.  {{site.data.keyword.discoveryshort}} ツールの**「データの管理」**画面で、**「データ・ソースの接続 (Connect a data source)」**を選択します。
1.  接続先にするデータ・ソースを選択します。 オンプレミスのデータ・ソースを選択する場合は、**「オンプレミス・ネットワークへの接続 (Connect to your on-premise network)」**セクションに移動し、**「接続の確立 (Make connection)」**ボタンをクリックします。
1.  **「Secure Gateway Client のダウンロードとインストール (Download and install the Secure Gateway Client)」**画面で、適切なバージョンの IBM Secure Gateway をダウンロードします。
1.  ダウンロードが完了したら、**「Secure Gateway をダウンロードして続行 (Download Secure Gateway and Continue)」**ボタンをクリックします。インストール中に、Secure Gateway Client からプロンプトが出されたら、画面に**ゲートウェイ ID** と**トークン**を指定する必要があります。インストール手順については、Secure Gateway の資料にある[クライアントのインストール ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/docs/services/SecureGateway/securegateway_install.html#installing-the-client){: new_window} を参照してください。
1.  Secure Gateway Client が実行されているマシンで、Secure Gateway ダッシュボード (http://localhost:9003) を開きます。
1.  ダッシュボードで**「ACL の追加 (add ACL)」**をクリックします。各 SharePoint コレクションのエンドポイント URL を**「アクセスの許可 (Allow access)」**リストに追加します。例えば、ホスト名 `mycompany.sharepoint.com`、ポート `80` などです。
1.  {{site.data.keyword.discoveryshort}} ツールに戻り、**「続行」**をクリックします。接続に成功すると、`「接続に成功しました (Connection successful)」`というメッセージが表示されます。接続に失敗した場合は、Secure Gateway ダッシュボードを開いて、**「アクセスの許可 (Allow access)」**リストのエンドポイントが正しいこと確認してください。

接続に成功したら、オンプレミスのデータ・ソースの資格情報の入力を開始できます。

## データ・ソースの接続とデータ分離
{: #source_isolation}

[外部データ・ソースへの接続](/docs/services/discovery?topic=discovery-sources#sources)では、ソースとサービスの間で転送中のデータを分離できないため、サービス・インスタンスのデータ分離が少なくなります。他のデータ分離 (保存中、管理、照会) はすべてそのままです。サービスとデータ・ソースの間、およびそれらの内部で転送中の通信はすべて、TLS v1.2 を使用して暗号化されます。TLS 証明書の秘密鍵は、AES-256-GCM を使用して暗号化された状態で保存されます。サービス証明書は 3 年ごとに期限が切れ、証明書失効リストが毎月更新されます。資格情報はすべて、TLS v1.2 を使用して暗号化された接続を介して送信され、AES-256 を使用して暗号化された状態で保存されます。これらのデータ・ソースへの接続では、これらのデータ・ソースでサポートされているすべてのセキュア・プロトコルを使用できます。
