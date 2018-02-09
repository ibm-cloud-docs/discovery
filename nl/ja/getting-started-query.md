---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-16"

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

# 照会入門

このチュートリアルでは、{{site.data.keyword.discoveryshort}} での、いくつかの異なるタイプの照会の作成方法について学習します。
{: shortdesc}

照会の作成について詳しくは、以下を参照してください。
- [照会の概念](/docs/services/discovery/using.html)
- [照会リファレンス](/docs/services/discovery/query-reference.html) ({{site.data.keyword.discoveryshort}} 照会言語で使用可能なパラメーター、演算子、および集約のリストを含む)

これらのサンプル照会は、{{site.data.keyword.discoveryshort}} ツールを使用して作成されます。代わりに API を使用したい場合は、API 呼び出しに照会パラメーターを追加してください。詳細情報および例については、[API reference ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection){: new_window} の『Queries』セクションを参照してください。

また、{{site.data.keyword.discoveryshort}} ツールを使用して自然言語照会 (「IBM Watson partnerships」など) を作成することもできます。このチュートリアルでは、主に {{site.data.keyword.discoveryshort}} 照会言語での照会の作成方法を重点的に説明します。この理由は、構造化照会がユーザーの条件に必要な場合があるためと、フィルターと集約は {{site.data.keyword.discoveryshort}} 照会言語で作成しなければならないからです。
{: tip}

## 始めに

**[入門](/docs/services/discovery/getting-started-tool.html)**のステップを完了します。**入門**が完了していない場合は、**「データの管理 (Manage data)」**画面に移動し、{{site.data.keyword.IBM_notm}} Press Releases という名前の新規コレクションを作成し、それに次の 4 つの文書を追加してください (**「デフォルト構成 (Default Configuration)」**を使用)。 <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン" class="style-scope doc-content"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン" class="style-scope doc-content"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン" class="style-scope doc-content"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン" class="style-scope doc-content"></a>

## ステップ 1: Discovery データ・スキーマのクイック・ツアー

まず、{{site.data.keyword.discoveryshort}} JSON を知ることから始めましょう。{{site.data.keyword.discoveryshort}} 照会言語での照会の作成方法を理解するには、{{site.data.keyword.discoveryshort}} がコレクション内の文書をエンリッチした後に作成する JSON に精通していると役立ちます。

1.  [{{site.data.keyword.discoveryshort}} ツールを起動](/docs/services/discovery/getting-started-tool.html#launch-the-tooling)します。**「データの管理 (Manage data)」**画面で、{{site.data.keyword.IBM_notm}} Press Releases コレクションを選択します。

1.  エンリッチされた文書で、Watson が発見した洞察を確認します。

    -  **「一般的センチメント (General sentiments)」**には、センチメント分析 (Sentiment Analysis) エンリッチメントによって発見された、肯定的 (positive)、中立 (neutral)、否定的 (negative) のタグが付いた文書のパーセンテージの明細が表示されます。
    -  **「最上位エンティティー (Top entities)」**には、エンティティー抽出 (Entity Extraction) エンリッチメントによって文書内で発見された人物 (person)、場所 (place)、および組織 (organization) が表示されます。
    -  **「コンテンツ階層 (Content hierarchy)」**には、カテゴリー分類 (Category Classification) エンリッチメントによって文書内で発見された階層タクソノミーが表示されます。
    -  **「関連する概念 (Related concepts)」**には、概念のタグ付け (Concept Tagging) エンリッチメントによって文書内で発見された概念が表示されます。

         いずれかのカードで**「スキーマで表示 (View in schema)」**をクリックすると、これらの結果を構成するエンリッチメントが表示されます。
         {: tip}

1.  文書のデータ・スキーマをよく知るために、**「データ・スキーマの表示 (View data schema)」**画面を見てみましょう。この画面には、文書別 (**文書ビュー (Document view)**) またはフィールド別 (**コレクション・ビュー (Collection view)**) の 2 つの方法で、変換された文書内のフィールドと値が表示されます。**「コレクション・ビュー (Collection view)」**には、コレクション内のすべてのフィールドが表示されます。

    **「データ・スキーマの表示 (View data schema)」**ボタンをクリックします。**「コレクション・ビュー (Collection view)」**の `enriched_text` の下で、**「デフォルト構成 (Default Configuration)」**ファイルを使用して適用したエンリッチメントを調べることができます。`categories`、`concepts`、`entities`、および `sentiment` をクリックすると、コレクションが Watson の洞察によってどのようにエンリッチされたかを確認できます。

一致する結果が照会で返されるはずなのに返されない場合は、照会で使用されているフィールド/値を、データ・スキーマで確認できるフィールド/値に交換してみてください。
{: tip}    

## ステップ 2: 基本的照会の作成

最初に、`Cloud computing` という概念をコレクション内で検出する照会を作成します。

1.  「照会の作成 (Build queries)」アイコン ![照会アイコン](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> をクリックして照会ページを開きます。{{site.data.keyword.IBM_notm}} Press Releases を含むコレクションを選択し、**「開始 (Get started)」**をクリックします。
1.  **「照会の作成 (Build queries)」**画面で**「文書の検索 (Search for Documents)」**をクリックし、次に**「Discovery 照会言語の使用 (Use the {{site.data.keyword.discoveryshort}} Query Language)」**をクリックします。
    - 次に、**「フィールド (Field)」**ドロップダウンをクリックして「`enriched_text.concepts.text`」を選択します。**「演算子 (Operator)」**には「`contains`」を選択し、「`Cloud computing`」の**「値 (Value)」**を入力します。照会 `enriched_text.concepts.text:Cloud computing` が **Visual Query Builder** の下に表示されます。

    - または、**「照会言語で編集 (Edit in query language)」**をクリックし、次に**「Discovery 照会言語の使用 (Use the {{site.data.keyword.discoveryshort}} Query Language)」**をクリックします。**「ここに照会を入力 (Enter query here)」**フィールドに「`enriched_text.concepts.text:Cloud computing`」と入力します。

1.  **「照会の実行 (Run query)」**をクリックします。1 つの一致 (`"matching_results": 1`) が検出されるはずです。**「要約 (Summary)」**タブまたは**「JSON」**タブの上部の**「照会 URL (Query URL」**をコピーしてアプリケーションで使用します。

**ボーナス:** **「詳細オプション (More options)」**の下に、**「関連するパッセージを含める (Include relevant passages)」**ラジオ・ボタンを使用してパッセージの取り出しをオンにするオプションがあります。パッセージとは、照会によって返された完全文書から抽出される、短く、関連性のある抜粋のことです。的を絞ったこれらのパッセージは、コレクション内の文書の `text` フィールドから抽出されます。詳しくは、[パッセージ](/docs/services/discovery/query-parameters.html#passages)を参照してください。パッセージ取り出しは、{{site.data.keyword.discoveryshort}} News コレクションでは使用できません。

いくつかの事前作成済み照会を確認したい場合は、**「サンプル照会の使用 (Use a sample query)」**ボタンをクリックしてください。
{: tip}

## ステップ 3: さまざまな照会を試す

以下の照会を試してみてください。

`positive` センチメントを持つすべての文書を返すには、**「文書の検索 (Search for Documents)」**、**「Discovery 照会言語の使用 (Use the {{site.data.keyword.discoveryshort}} Query Language)」**をクリックします。
-  次に、**「フィールド (Field)」**ドロップダウンをクリックして「`enriched_text.sentiment.document.label`」を選択します。**「演算子 (Operator)」**には「`contains`」を選択し、「`positive`」の**「値 (Value)」**を入力します。  

   照会 `enriched_text.sentiment.document.label:positive` が **Visual Query Builder** の下に表示されます。

「`health and fitness`」カテゴリーに含まれるすべての文書を返すには、**「文書の検索 (Search for Documents)」**、**「Discovery 照会言語の使用 (Use the {{site.data.keyword.discoveryshort}} Query Language)」**をクリックします。
-  次に、**「フィールド (Field)」**ドロップダウンをクリックして「`enriched_text.categories.label`」を選択します。**「演算子 (Operator)」**には「`is`」を選択し、「`"health and fitness"`」の**「値 (Value)」**を入力します。

   照会 `enriched_text.categories.label::"health and fitness"` が **Visual Query Builder** の下に表示されます。演算子「`::`」は完全一致を指定します。

エンティティー「`IBM`」を含むが、エンティティー「`Watson`」を含まないすべての文書を返すには、**「文書の検索 (Search for Documents)」**、**「Discovery 照会言語の使用 (Use the {{site.data.keyword.discoveryshort}} Query Language)」**をクリックします。
-  次に、**「フィールド (Field)」**ドロップダウンをクリックして「`enriched_text.entities.text`」を選択します。**「演算子 (Operator)」**には「`contains`」を選択し、「`IBM`」の**「値 (Value)」**を入力します。**「ルールの追加 (Add rule)」**をクリックし、**「フィールド (Field)」**には「`enriched_text.entities.text`」を選択し、**「演算子 (Operator)」**には「`does not contain`」を選択して、「`Watson`」の**「値 (Value)」**を入力します。

   照会 `enriched_text.entities.text:IBM,enriched_text.entities.text:!Watson` が **Visual Query Builder** の下に表示されます。演算子「`:!`」は「does not contain」を指定します。

## ステップ 4: 結合照会の作成

複数の照会パラメーターを結合することで、さらに的を絞った照会を作成できます。`filter` パラメーターと `query` パラメーターの両方を使用して、{{site.data.keyword.IBM_notm}} の買収に関する文書を返してみます。filter パラメーターが、`IBM` に言及している文書のみに結果を絞り込みます。次に、query パラメーターが、`acquisitions` に関するすべての結果を関連性の高い順に返します。

1.  「照会の作成 (Build queries)」アイコン ![照会アイコン](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> をクリックして照会ページを開きます。{{site.data.keyword.IBM_notm}} Press Releases を含むコレクションを選択し、**「開始 (Get started)」**をクリックします。

1.  **「照会する文書のフィルタリング (Filter which documents you query)」**の下で、以下を実行します。
    -  **「フィールド (Field)」**ドロップダウンをクリックして「`enriched_text.entities.text`」を選択します。**「演算子 (Operator)」**には「`contains`」を選択し、「`IBM`」の**「値 (Value)」**を入力します。

       照会「`enriched_text.entities.text:IBM`」が、エンティティー「`IBM`」に言及している文書のみに文書を絞り込みます。

1.  **「文書の検索 (Search for Documents)」**の下で、**「Discovery 照会言語の使用 (Use the {{site.data.keyword.discoveryshort}} Query Language)」**をクリックします。
    -  次に、**「フィールド (Field)」**ドロップダウンをクリックして「`enriched_text.concepts.text`」を選択します。**「演算子 (Operator)」**には「`contains`」を選択し、「`world wide web`」の**「値 (Value)」**を入力します。

       照会「`enriched_text.concepts.text:world wide web`」が、「`world wide web`」の概念を含むすべての文書を返し、それらの文書は関連性の高い順にランク付けされます。

1.  **「詳細オプション (More options)」**をクリックし、次に**「返すフィールド (Fields to return)」**をクリックし、**「指定 (Specify)」**を選択します。「`text`」を選択します。これにより、関連する記事のテキストに応答が制限され、それ以外はすべて除外されます。

1.  **「照会の実行 (Run query)」**をクリックします。1 つの一致する文書 `"matching_results": 1` が検出されます。

## Step 5: 集約の作成

集約は、上位キーワードやエンティティーの全体的なセンチメントなどの一連のデータ値を返します。

{{site.data.keyword.IBM_notm}} Press Releases コレクション内の上位 10 個の概念を返す集約を作成してみます。

1.  「照会のビルド (build queries)」アイコン ![照会アイコン](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> をクリックして照会ページを開きます。{{site.data.keyword.IBM_notm}} Press Releases を含むコレクションを選択し、**「開始 (Get started)」**をクリックします。

1.  **「結果の分析を含める (Include analysis of your results)」**の下で以下を実行します。
    -  **「出力 (Output)」**ドロップダウンをクリックして`「上位の値 (Top values)」`を選択します。**「フィールド (Field)」**には「`enriched_text.concepts.text`」を選択し、**「カウント (Count)」**には「`10`」を入力します。

       「`Term`」は、「`concepts` `text`」フィールドの最も一般的な値を返します。**「カウント (Count)」**は、返す結果の数を指定します。照会`term(enriched_text.concepts.text,count:10)` が **Visual Query Builder** の下に表示されます。   

1.  **「詳細オプション (More options)」**をクリックし、**「戻す文書の数 (Number of documents to return)」**フィールドに `0` と入力します。

1.  **「照会の実行 (Run query)」**をクリックします。上位 10 個の概念が、**「要約 (Summary)」**タブと**「JSON」**タブの両方に表示されます。「要約 (Summary)」の例を以下に示します。

## ステップ 6: Watson Discovery News での照会の作成

{{site.data.keyword.discoverynewsshort}} は、コグニティブ洞察によって事前にエンリッチされた公開データ・セットです。{{site.data.keyword.discoveryshort}} に含まれています。このコレクションについて詳しくは、[Watson Discovery News](/docs/services/discovery/watson-discovery-news.html#watson-discovery-news) を参照してください。

{{site.data.keyword.discoverynewsshort}} の構成を調整したり、トレーニングを行ったり、{{site.data.keyword.discoverynewsshort}} コレクションに文書を追加したりすることはできません。{{site.data.keyword.discoverynewsshort}} で何を作成できるかのデモについては、[こちら ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://discovery-news-demo.mybluemix.net/){: new_window} を参照してください。

以下のサンプル照会は、{{site.data.keyword.discoverynewsfull}} から、肯定的なセンチメントを持つ、Pittsburgh Steelers に関する上位 10 個の記事を返します。

1.  「照会のビルド (build queries)」アイコン ![照会アイコン](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> をクリックして照会ページを開きます。{{site.data.keyword.discoverynewsshort}} コレクションを選択し、**「開始 (Get started)」**をクリックします。

1.  **「文書の検索 (Search for documents)」**の下で、**「Discovery 照会言語の使用 (Use the {{site.data.keyword.discoveryshort}} Query Language)」**をクリックします。
    -  次に、**「フィールド (Field)」**ドロップダウンをクリックして「`text`」を選択します。**「演算子 (Operator)」**には「`contains`」を選択し、「`Pittsburgh Steelers`」の**「値 (Value)」**を入力します。**「ルールの追加 (Add rule)」**をクリックし、次に**「フィールド (Field)」**ドロップダウンをクリックして「`enriched_text.sentiment.document.label`」を選択します。**「演算子 (Operator)」**には「`contains`」を選択し、「`positive`」の**「値 (Value)」**を入力します。

       照会 `text:Pittsburgh Steelers, enriched_text.sentiment.document.label:positive` が **Visual Query Builder** の下に表示されます。

1.  **「詳細オプション (More options)」**をクリックし、次に**「戻す文書の数 (Number of documents to return)」**フィールドに「`10`」(デフォルト) を入力します。

1.  **「照会の実行 (Run query)」**をクリックします。肯定的なセンチメントを持つ、Pittsburgh Steelers に関する上位 10 個の記事が表示されます。

**注:** Watson Discovery News 照会で返される結果の最大数は `50` です。

ニュース記事は複数の報道機関に配信されている可能性があり、{{site.data.keyword.discoverynewsfull}} はそのそれぞれを取得するため、記事が重複します。つまり、{{site.data.keyword.discoverynewsfull}} への照会で、照会結果に複数の同一またはほぼ同一の記事が返される可能性があります。重複排除をオンにするには、**「詳細オプション (More options)」**の下から、**「重複する結果の除外 (Exclude duplicate results)」**を選択します。このベータ機能の詳細については、[照会結果から重複する文書を除外](/docs/services/discovery/query-parameters.html#deduplication) を参照してください。
