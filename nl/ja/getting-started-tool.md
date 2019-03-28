---

copyright:
  years: 2015, 2018, 2019
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

# はじめに
{: #getting-started}

この短いチュートリアルでは、{{site.data.keyword.discoveryshort}} ツールの概要を説明し、プライベート・データ・コレクションを作成して検索するプロセスをご案内します。
{: shortdesc}

API で作業する場合は、[API 入門](/docs/services/discovery?topic=discovery-gs-api#gs-api)を参照してください。
{: tip}

## 始めに
{: #before-you-begin-tool}
{: hide-dashboard}

始めるにはサービス・インスタンスが必要です。
{: hide-dashboard}

1.  {: hide-dashboard} {{site.data.keyword.cloud_notm}} カタログの [{{site.data.keyword.discoveryshort}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/catalog/services/discovery) ページに移動します。

    特に選択しなければ、サービス・インスタンスは**デフォルト**のリソース・グループに作成されます。後からは変更*できません*。サービスを試す目的であれば、このグループで十分です。

負荷の高い用途のためにインスタンスを作成する場合は、[リソース・グループ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/docs/resources/bestpractice_rgs.html#bp_resourcegroups){: new_window} の詳細を確認してください。
1.  {: hide-dashboard} 無料の {{site.data.keyword.cloud_notm}} アカウントを登録するか、ログインします。
1.  {: hide-dashboard} **「作成」**をクリックします。

## ステップ 1: ツールの起動
{: #launch-the-tooling}

{{site.data.keyword.discoveryshort}} サービスのインスタンスを作成すると、サービスのリストが表示されます。
{: hide-dashboard}

1.  {: hide-dashboard} 作成した {{site.data.keyword.discoveryshort}} サービス・インスタンスをクリックして、サービス・ダッシュボードに移動します。
1.  **「管理」**ページで、**「ツールの起動 (Launch tool)」**をクリックします。ツールへのログインを求めるプロンプトが出されたら、{{site.data.keyword.cloud_notm}} 資格情報を入力します。

<!-- To do: Add screenshot for developer console -->

## ステップ 2: コレクションの作成
{: #create-a-collection-tool}

{{site.data.keyword.discoveryshort}} ツールの最初のステップは、データ・コレクションを作成することです。

コレクションとは、文書の集合のことです。 *なぜ複数のコレクションが必要なのでしょうか?* これには、次のようないくつかの理由があります。

- 異なる対象者ごとに結果を分離するために、複数のコレクションが必要な場合がある。
- データが非常に異なるため、すべてのデータを同時に照会しても意味がない。

公開されている、事前にエンリッチされた {{site.data.keyword.discoverynewsshort}} データ・コレクションを使用することもできます。 いつでも照会できる状態なので、そのコレクションですぐに照会の作成を開始できます。 その構成を調整したり、{{site.data.keyword.discoverynewsshort}} に文書を追加したりすることはできません。

1.  ![環境詳細](images/env_icon.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> をクリックし、**「環境の作成 (Create environment)」**を選択します。
1.  環境の準備ができたら、**「独自のデータをアップロード (Upload your own data)」**ボタンをクリックして、**「新規コレクションに名前を付ける (Name your new collection)」**ことができます。 コレクションに **InstallDocs** という名前を付けます。

    コレクションの作成時に、**「詳細 (Advanced)」**項目に、**Default Contract Configuration** という構成ファイルを選択するオプションがあります。この構成では、PDF 内の要素からパーティー、性質、カテゴリーを抽出するために使用できる要素分類エンリッチメントのみがサポートされます。詳しくは、[要素の分類](/docs/services/discovery?topic=discovery-element-classification#element-collection)を参照してください。このチュートリアルでは、このオプションを選択しないでください。

{{site.data.keyword.discoveryshort}} ツールを使用して、Box、Salesforce、Microsoft SharePoint Online、IBM Cloud オブジェクト・ストレージ、Microsoft SharePoint 2016 のデータ・ソースをクロールしたり、Web クロールを実行したりすることもできます。**「データ・ソースの接続 (Connect a data source)」**ボタンをクリックします。詳しくは[データ・ソースへの接続](/docs/services/discovery?topic=discovery-sources#sources)を参照してください。
{: tip}

## ステップ 3: サンプル文書のダウンロードとコレクションへのアップロード
{: create-custom-configuration}

1.  こちらのサンプル PDF 文書 <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/watsonexplorerinstall.pdf" download>Watson Explorer Installation Guide <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン"></a> をダウンロードします。{{site.data.keyword.discoveryshort}} でサポートされる文書タイプをすべて記載したリストについては、[サポートされる文書タイプ](/docs/services/discovery?topic=discovery-sdu#doctypes)を参照してください。 

    一部のブラウザーでは、ローカルに保存するのではなく、リンクが新しいウィンドウで開きます。 これが発生した場合は、ブラウザーの`「ファイル」`メニューで `「名前を付けて保存」`を選択して、ファイルのコピーを保存します。
    {: tip}

1.  コレクションに文書をアップロードします。コレクションにドラッグ・アンド・ドロップするか、**「コンピューターから参照 (browse from computer)」**をクリックして文書をアップロードします。アップロードが完了すると、以下の情報が表示されます。
    -  文書の数 (1)。
    -  文書から識別されたフィールド。識別された 1 つのフィールド (`text`) が表示されます。間もなく識別するフィールドを追加する予定です。
    -  文書に適用されたエンリッチメント。エンティティー抽出、センチメント分析、カテゴリー分類、概念のタグ付けの各エンリッチメントが、{{site.data.keyword.discoveryshort}} によって自動的に `text` フィールドに適用されます。エンリッチメントについて[こちらで](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)詳細を確認してください。 
    -  すぐに実行できる事前作成済みの照会。
1.  まずは簡単な自然言語照会を試してみましょう。右下の**「独自の照会の作成 (Build your own query)」**をクリックします。
1.  **「照会の作成 (Build queries)」**画面で、**「文書の検索 (Search for documents)」**をクリックし、次に**「自然言語を使用 (Use natural language)」**をクリックします。「`What are the minimum hardware requirements`」と入力し、**「照会の実行」**ボタンをクリックします。右側の**「JSON」**タブをクリックします。結果がまだ正確でないので、Smart Document Understanding を使用して改善しましょう。
1.  左上のコレクションの名前 (**InstallDocs**) をクリックして**「概要」**画面に戻ります。  
 
## ステップ 4: 文書への注釈付け
{: #upload-your-documents}

文書に注釈を付ける方法について詳しくは、[Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu) を参照してください。
{: tip}

1.  右上の**「データの構成 (Configure data)」**をクリックします。 
1.  **「データの構成 (Configure data)」**画面には、**「フィールドの識別 (Identify fields)」**、**「フィールドの管理 (Manage fields)」**、**「フィールドのエンリッチ (Enrich fields)」**の 3 つのタブがあります。
1.  「`Watson Explorer Installation Guide`」が表示され、**「フィールドの識別 (Identify fields)」**タブで注釈が付けられるようになります。存在するすべてのフィールド (`answer`、`author`、`footer`、`header`、`question`、`subtitle`、`table_of_contents`、`text`、`title`) が、右側の**「フィールド・ラベル (Field labels)」**リストに表示されます。拡張プランまたはプレミアム・プランを購入した場合は、独自のカスタム・ラベルを作成できます。

    現時点では文書全体が `text` として識別されるので、右側のマーカーはすべて黄色です。注釈を付けると (そしてシステムが予測を開始すると) 、色が更新されます。
    {: tip}

1.  `title` をクリックし、次に「`Installation and Integration Guide`」の横のマーカーを選択します。**「ページの送信 (Submit page)」**ボタンをクリックします。
1.  左側のページ・プレビューで、ページ 3 をクリックします。このページでは `title` が既に予測されていることに注意してください。**「ページの送信 (Submit page)」**ボタンをクリックします。
1.  ページ 4 で、`footer` ラベルを選択し、フッターの横のマーカーを選択します。**「ページの送信 (Submit page)」**ボタンをクリックします。
1.  ページ 5 とページ 6 で、フッターに `footer` ラベルの注釈を付けます。各ページを送信します。さらに何ページかクリックします。{{site.data.keyword.discoveryshort}} によってフッターが適切に予測されていることがわかります。ページ 7、ページ 9、ページ 10 で `title` (左揃え) と `subtitle` (インデント) に注釈を付け、各ページを個別に送信します。
1.  さらに何ページかクリックして、予測済みのタイトルとサブタイトルを確認します。何かを変更する必要がある場合は、それらのページに注釈を付けて、**「ページの送信 (Submit page)」**ボタンをクリックします。
1.  次は、**「フィールドの管理 (Manage fields)」**タブをクリックし、**「文書を分割して照会結果を改善する (Improve query results by splitting your documents)」**で、`subtitle` に基づいて文書を分割します。 
1.  差し当たって、注釈付けはこれで十分です。右上の**「変更をコレクションに適用 (Apply changes to collection)」**ボタンをクリックします。**「文書のアップロード (Upload your documents)」**ダイアログ・ボックスが表示されます。元の `watsonexplorerinstall.pdf` ファイルを参照し、アップロードします。これにより、すべての注釈が索引に適用されます。索引作成が完了すると、**「概要」**画面が開きます。これで、30 以上の文書と、データから識別された 4 つのフィールド (`footer`、`subtitle`、`text`、`title`) が表示されるようになります。(この変更が数分以内に表示されない場合は、ブラウザー・ウィンドウを最新表示してください。)

    **「フィールドの管理 (Manage fields)」**タブを開いてフィールドを「`オフ`」に切り替えれば、そのフィールド(`footer` など) を索引作成から除外できます。
    {: tip}

## ステップ 5: 照会してみましょう
{: #build-a-query}

1.  右下の**「独自の照会の作成 (Build your own query)」**をクリックします。
1.  **「照会の作成 (Build queries)」**画面で、**「文書の検索 (Search for documents)」**をクリックし、次に**「自然言語を使用 (Use natural language)」**をクリックします。「`What are the minimum hardware requirements`」と入力し、**「照会の実行」**ボタンをクリックします。 
1.  右側の**「JSON」**タブをクリックします。`results` の下の `text` を調べます。照会に対して返された回答は、はるかに正確になっています。

その他のリソース:
-  文書のデータ・スキーマの詳細を確認するには、左端の**「データ・スキーマの表示 (View Data Schema)」**アイコンをクリックするか、**「JSON」**タブをクリックします。詳しくは、[Discovery データ・スキーマ](/docs/services/discovery?topic=discovery-query-concepts#discovery-schema)を参照してください。
-  {{site.data.keyword.discoveryshort}} 照会言語で書かれた照会例を試してみるには、**「サンプル照会の使用 (Use a sample query)」**ボタンをクリックします。

## 次のステップ
{: #next-steps-tool}

これで、機能し、データが取り込まれた {{site.data.keyword.discoveryshort}} サービス・インスタンスが作成されました。 文書とエンリッチメントをさらに追加し、追加の文書に注釈を付けて、コレクションのカスタマイズを開始できます。詳しくは、[Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu) を参照してください。
