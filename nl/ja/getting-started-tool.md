---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-18"

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
{:download: .download}

# はじめに

この短いチュートリアルでは、{{site.data.keyword.discoveryshort}} ツールの概要を説明し、プライベート・データ・コレクションを作成して検索するプロセスをご案内します。
{: shortdesc}

API で作業する場合は、[API 入門](/docs/services/discovery/getting-started.html)を参照してください。
{: tip}

## 始めに
{: #before-you-begin}

開始するにはサービス・インスタンスが必要です。

<!-- Remove the text marked `download` after there's no g-s tab in the catalog dashboard -->


サービス・インスタンスは作成済みです。 **「管理」**、**「ツールの起動 (Open tool)」**の順にクリックします。[ステップ 2](/docs/services/discovery/getting-started-tooling.html#create-a-collection) に進みます。
{: download tip}

{{site.data.keyword.discoveryshort}}サービス・インスタンスを作成している場合は、これらの前提条件はすべて設定されています。[ステップ 1](/docs/services/discovery/getting-started-tool.html#launch-the-tooling) に進んでください。

1.  {{site.data.keyword.Bluemix_notm}} カタログの [{{site.data.keyword.discoveryshort}}![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.{DomainName}/catalog/services/discovery){: new_window} ページに移動します。
1.  無料の {{site.data.keyword.Bluemix_notm}} アカウントに登録するか、ログインします。
1.  **「作成」**をクリックします。


## ステップ 1: ツールの起動
{: #launch-the-tooling}

{{site.data.keyword.discoveryshort}} サービスのインスタンスを作成すると、[{{site.data.keyword.Bluemix_notm}} ダッシュボード](https://console.{DomainName}/dashboard)が表示されます。{{site.data.keyword.discoveryshort}} サービス・インスタンスをクリックして、{{site.data.keyword.discoveryshort}} サービス・ダッシュボードに移動します。

**「管理」**ページで、**「ツールの起動 (Open tool)」**をクリックします。

<!-- To do: Add screenshot for developer console -->

ツールへのログインを求めるプロンプトが出されたら、{{site.data.keyword.Bluemix_notm}} 資格情報を入力します。

{{site.data.keyword.discoveryshort}} サービスのプロジェクトの詳細ページが表示されていない場合は、{{site.data.keyword.watson}} Developer Console の「[プロジェクト ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.{DomainName}/developer/watson/projects)」ページに移動して、該当するプロジェクトを選択します。
{: tip}

<!-- Remove this text after dedicated instances have the Developer Console: begin -->

{{site.data.keyword.Bluemix_dedicated_notm}}: ダッシュボードから該当するサービス・インスタンスを選択してツールを起動します。

<!-- Remove this text after dedicated instances have the Developer Console: end -->

## ステップ 2: コレクションの作成
{: #create-a-collection}

{{site.data.keyword.discoveryshort}} ツールの最初のステップは、データ・コレクションを作成することです。

コレクションとは、文書の集合のことです。 *なぜ複数のコレクションが必要なのでしょうか?* これには、次のようないくつかの理由があります。

- 異なる対象者ごとに結果を分離するために、複数のコレクションが必要な場合がある。
- データが非常に異なるため、すべてのデータを同時に照会しても意味がない。

公開されている、事前にエンリッチされた {{site.data.keyword.discoverynewsshort}} データ・コレクションを使用することもできます。 いつでも照会できる状態なので、そのコレクションですぐに照会の作成を開始できます。 その構成を調整したり、{{site.data.keyword.discoverynewsshort}} に文書を追加したりすることはできません。

1.  ![Cog](images/icon_settings.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> をクリックし、**「環境の作成 (Create environment)」**を選択します。
1.  環境の準備ができたら、**「独自のデータをアップロード (Upload your own data)」**ボタンをクリックして、**「新規コレクションに名前を付ける (Name your new collection)」**ことができます。コレクションに名前を付け、**「適用する構成の選択 (Select a configuration to apply)」**から**「デフォルト構成 (Default Configuration)」**を選択します (構成は後で変更できます)。

要素の分類をサポートする **Default Contract Configuration** という名前の別の構成があり、これを使用して、PDF 内の要素からパーティー、性質、およびカテゴリーを抽出できます。詳しくは、[要素の分類](/docs/services/discovery/element-classification.html#element-collection)を参照してください。

{{site.data.keyword.discoveryshort}} ツールを使用して Box、Salesforce、および Microsoft SharePoint Online データ・ソースをクロールすることもできます。**「データ・ソースの接続 (Connect a data source)」**ボタンをクリックします。詳しくは[データ・ソースへの接続](/docs/services/discovery/connect.html)を参照してください。
{: tip}

## ステップ 3: カスタム構成の作成
{: create-custom-configuration}

コレクションが作成されたら、アップロード領域を使用して即時にコンテンツのアップロードを開始できますが、ここでは、カスタム構成の作成とテストを行います。

1.  コレクション名の横の**「切り替え (Switch)」**をクリックし、**「新規構成の作成 (Create a new configuration)」**を選択します。 構成に名前を付け、**「作成 (Create)」**をクリックします。
1.  構成を作成したら、以下のようにしてカスタマイズできます。
    1.  <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン" class="style-scope doc-content"></a> サンプル文書をダウンロードします。
    1.  **「サンプル文書のアップロード (Upload Sample Documents)」**パネルを使用して、サンプル文書をアップロードします。 アップロードされたら、文書名リンクをクリックして変換を表示できます。
1.  次に、構成の調整を行います。 このタスクでは、以下のようにして、各文書に適用されているエンリッチメントを変更します。
    1.  構成の**「エンリッチ (Enrich)」**セクションをクリックします。 画面右側に表示される、生成された JSON を確認します。 *enriched_text* セクションまでスクロールダウンし、多くの *concepts* が含まれていることに注意します。
    1.  次に、*concepts* という名前のテキスト・エンリッチメントの横の **X** をクリックしてそれを削除し、次に**「適用して保存 (Apply & Save)」**をクリックします。
    1.  最後に、JSON を再度確認します。 出力がどのように変化したかを確認し、*concepts* がもう含まれていないことに注意してください。

## ステップ 4: 文書のアップロード
{: #upload-your-documents}

サンプル文書のカスタム変換が正常に行われたら、次に、実際のコンテンツをコレクションに取り込んでみます。

1. 次の 3 つのサンプル文書をダウンロードします: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン" class="style-scope doc-content"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン" class="style-scope doc-content"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン" class="style-scope doc-content"></a>。
1.  ![ファイル・アイコン](images/icon_yourData.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> をクリックし、コレクションを選択します。
1.  作成したカスタム構成が**「構成」**にリストされていることを確認します。 リストされていない場合は、該当する構成名の横の**「切り替え (Switch)」**をクリックして選択してください。
1.  **「文書のアップロード (Upload documents)」**ボタンをクリックし、4 つのサンプル文書 (test-doc1.html、test-doc2.html、test-doc3.html、test-doc4.html) のアップロードを開始します。
1.  文書がアップロードされるまで待ちます。 文書の状況が**「概要」**セクションに表示されます。

## ステップ 5: 照会の作成
{: #build-a-query}

1.  ![照会アイコン](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> をクリックして、照会ページを開きます。 コレクションを選択し、**「開始 (Get started)」**をクリックします。
1.  **「照会の作成 (Build queries)」**画面で**「文書の検索 (Search for documents)」**をクリックし、次に**「Discovery 照会言語の使用 (Use the {{site.data.keyword.discoveryshort}} Query Language)」**をクリックします。
    - 「IBM」という名前のエンティティーを含む結果を検索するには、以下のようにします。
        1.  **「フィールド (Field)」**をクリックし、「`enriched_text.entities.text`」を選択します。 **「演算子 (Operator)」**には「`contains`」を選択し、**「値 (Value)」**には「`IBM`」を選択します。 照会 `enriched_text.entities.text:IBM` が **Visual Query Builder** に表示されます。
        1.  **「照会の実行 (Run Query)」**をクリックします。 この照会は、4 つの結果を返します。
    - 「Watson」という名前のエンティティーを含む結果を検索するには、以下のようにします。
        1.  **「フィールド (Field)」**をクリックし、「`enriched_text.entities.text`」を選択します。 **「演算子 (Operator)」**には「`contains`」を選択し、**「値 (Value)」**には「`watson`」を選択します。 照会 `enriched_text.entities.text:watson` が **Visual Query Builder** に表示されます。
        1.  **「照会の実行 (Run Query)」**をクリックします。 この照会は、2 つの結果を返します。
    - 「Watson」という名前のエンティティーと「Slack」という名前のエンティティーの両方を含む結果を検索するには、以下のようにします。
        1.  **「フィールド (Field)」**をクリックし、「`enriched_text.entities.text`」を選択します。 **「演算子 (Operator)」**には「`contains`」を選択し、**「値 (Value)」**には「`watson`」を選択します。 **「ルールの追加 (Add rule)」**をクリックし、選択を繰り返します。ただし今度は、「`Slack`」の**「値 (Value)」**を選択します。 照会 `enriched_text.entities.text:watson,enriched_text.entities.text:Slack` が **Visual Query Builder** に表示されます。
        1.  **「照会の実行 (Run Query)」**をクリックします。 この照会は 1 つの結果を返します。

    **「照会言語で編集 (Edit in query language)」**をクリックし、{{site.data.keyword.discoveryshort}} 照会言語を使用して照会を作成します。 {{site.data.keyword.discoveryshort}} 照会言語について詳しくは、[照会リファレンス](/docs/services/discovery/query-reference.html)および[照会の概念](/docs/services/discovery/using.html)を参照してください。
1.  照会の結果は、以下のように**「結果 (Results)」**セクションに表示されます。
    - **「要約 (Summary)」**タブは、照会結果の概要を提供します。
    - **「JSON」**タブには、完全な JSON 結果が表示されます。

    リストされる照会について、**「要約 (Summary)」**には、最初に文書のパッセージが (関連性の高い順に) 表示され、その後に、検出された文書の名前が表示され、そしてエンリッチメント順に結果が表示されます。 **「パッセージ (Passages)」**とは、照会によって返された完全文書から抽出される、短く、関連性のある抜粋のことです。

    **「JSON」**タブと**「要約 (Summary)」**タブの下にある**「照会 URL (Query URL)」**リンクは、すぐにアプリケーションで使用できます。

    また、**「自然言語の使用 (Use natural language)」**をクリックし、「IBM Watson partnerships」のような自然言語照会を作成することもできます。 自然言語照会について詳しくは、[自然言語照会](/docs/services/discovery/query-parameters.html#nlq)を参照してください。

    Watson をトレーニングして自然言語照会の結果を向上させることができます。[ツールを使用した結果の関連性の向上](/docs/services/discovery/train-tooling.html)を参照してください。

    その他のリソース:
    - 文書のデータ・スキーマの詳細については、**「データ・スキーマの表示 (View Data Schema)」**アイコンをクリックするか、**「JSON」**タブをクリックしてください。 詳しくは、[Discovery データ・スキーマ](/docs/services/discovery/using.html#discovery-schema)を参照してください。
    - {{site.data.keyword.discoveryshort}} 照会言語で編集している場合、任意の**「ここに照会を入力 (Enter query here)」**フィールドの横の「**?**」アイコンをクリックすると追加の例が表示されます。

## 次のステップ
{: #next-steps}

これで、機能し、データが取り込まれた {{site.data.keyword.discoveryshort}} サービス・インスタンスが作成されました。 次に、さらに文書とエンリッチメントを追加し、変換設定をカスタマイズして、コレクションのカスタマイズを開始できます。
