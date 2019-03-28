---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-06"

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

# 照会入門
{: #getting-started-with-querying}

このチュートリアルでは、{{site.data.keyword.discoveryshort}} 照会言語でいくつかの異なるタイプの照会を作成する方法について学習します。
{: shortdesc}

照会の作成について詳しくは、以下を参照してください。
- [照会の概念](/docs/services/discovery?topic=discovery-query-concepts#query-concepts)
- [照会リファレンス](/docs/services/discovery?topic=discovery-query-reference#query-reference) ({{site.data.keyword.discoveryshort}} 照会言語で使用可能なパラメーター、演算子、および集約のリストが記載されています)

これらのサンプル照会は、{{site.data.keyword.discoveryshort}} ツールを使用して作成されます。 代わりに API を使用したい場合は、API 呼び出しに照会パラメーターを追加してください。 詳細情報および例については、[API reference ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window} の『Queries』セクションを参照してください。

また、{{site.data.keyword.discoveryshort}} ツールを使用して自然言語照会 (「IBM Watson partnerships」など) を作成することもできます。 このチュートリアルでは、主に {{site.data.keyword.discoveryshort}} 照会言語での照会の作成方法を重点的に説明します。この理由は、構造化照会がユーザーの条件に必要な場合があるためと、フィルターと集約は {{site.data.keyword.discoveryshort}} 照会言語で作成しなければならないからです。
{: tip}

## 始めに
{: #querying-before-you-begin}

**「データの管理 (Manage data)」**画面に移動し、{{site.data.keyword.IBM_notm}} Press Releases という名前の新規コレクションを作成し、それに 4 つの文書 (<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン"></a>、<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン"></a>) を追加してください。

一部のブラウザーでは、ローカルに保存するのではなく、リンクが新しいウィンドウで開きます。 これが発生した場合は、ブラウザーの`「ファイル」`メニューで `「名前を付けて保存」`を選択して、ファイルのコピーを保存します。
{: tip}

## ステップ 1: Discovery データ・スキーマのクイック・ツアー
{: #querying-step1}

まず、{{site.data.keyword.discoveryshort}} JSON を知ることから始めましょう。 {{site.data.keyword.discoveryshort}} 照会言語での照会の作成方法を理解するには、{{site.data.keyword.discoveryshort}} がコレクション内の文書をエンリッチした後に作成する JSON に精通していると役立ちます。

1.  [{{site.data.keyword.discoveryshort}} ツールを起動](/docs/services/discovery?topic=discovery-getting-started#launch-the-tooling)します。 **「データの管理 (Manage data)」**画面で、{{site.data.keyword.IBM_notm}} Press Releases コレクションを選択します。

1.  エンリッチされた文書で、Watson が発見した洞察を確認します。

    -  **「センチメント分析 (Sentiment Analysis)」**には、センチメント分析 (Sentiment Analysis) エンリッチメントによって発見された、肯定的 (positive)、中立 (neutral)、否定的 (negative) のタグが付いた文書のパーセンテージの明細が表示されます。
    -  **「エンティティー抽出 (Entity Extraction)」**には、エンティティー抽出 (Entity Extraction) エンリッチメントによって文書内で発見された人物 (person)、場所 (place)、および組織 (organization) が表示されます。
    -  **「カテゴリー分類 (Category Classification)」**には、カテゴリー分類 (Category Classification) エンリッチメントによって文書内で発見された階層タクソノミーが表示されます。
    -  **「概念のタグ付け (Concept Tagging)」**には、概念のタグ付け (Concept Tagging) エンリッチメントによって文書内で発見された概念が表示されます。

1.  文書のデータ・スキーマをよく知るために、**「データ・スキーマの表示 (View data schema)」**画面を見てみましょう。 この画面には、文書別 (**文書ビュー (Document view)**) またはフィールド別 (**コレクション・ビュー (Collection view)**) の 2 つの方法で、変換された文書内のフィールドと値が表示されます。 **「コレクション・ビュー (Collection view)」**には、コレクション内のすべてのフィールドが表示されます。

    左側の**「データ・スキーマの表示 (View data schema)」**アイコンをクリックします。**「コレクション (Collection)」ビュー**の `enriched_text` の下で、コレクションに適用したエンリッチメントを調べることができます。`categories`、`concepts`、`entities`、および `sentiment` をクリックすると、Watson の洞察によってコレクションがどのようにエンリッチされたのかを確認できます。

一致する結果が照会で返されるはずなのに返されない場合は、照会で使用されているフィールド/値を、データ・スキーマで確認できるフィールド/値に交換してみてください。
{: tip}    

## ステップ 2: 基本的照会の作成
{: #querying-step2}

最初に、`Cloud computing` という概念をコレクション内で検出する照会を作成します。

1.  **「照会の作成 (Build queries)」**アイコン ![照会アイコン](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> をクリックして照会ページを開きます。 {{site.data.keyword.IBM_notm}} Press Releases を含むコレクションを選択し、**「開始 (Get started)」**をクリックします。
1.  **「照会の作成 (Build queries)」**画面で**「文書の検索 (Search for Documents)」**をクリックし、次に**「Discovery 照会言語の使用 (Use the {{site.data.keyword.discoveryshort}} Query Language)」**をクリックします。
    - 次に、**「フィールド (Field)」**ドロップダウンをクリックして「`enriched_text.concepts.text`」を選択します。**「演算子 (Operator)」**には「`contains`」を選択し、「`Cloud computing`」の**「値 (Value)」**を入力します。 照会 `enriched_text.concepts.text:Cloud computing` が **Visual Query Builder** の下に表示されます。

    - または、**「照会言語で編集 (Edit in query language)」**をクリックし、次に**「Discovery 照会言語の使用 (Use the {{site.data.keyword.discoveryshort}} Query Language)」**をクリックします。 **「ここに照会を入力 (Enter query here)」**フィールドに `enriched_text.concepts.text:" Cloud computing"` と入力します。

1.  **「照会の実行 (Run query)」**をクリックします。 1 つの一致 (`"matching_results": 1`) が検出されるはずです。 **「要約 (Summary)」**タブまたは**「JSON」**タブの上部の**「照会 URL (Query URL」**をコピーしてアプリケーションで使用します。

**ボーナス:** **「詳細オプション (More options)」**の下に、**「関連するパッセージを含める (Include relevant passages)」**ラジオ・ボタンを使用してパッセージの取り出しをオンにするオプションがあります。 パッセージは、照会から返される全文書から抽出される、関連する短い抜粋です。 的を絞ったこれらのパッセージは、コレクション内の文書の `text` フィールドから抽出されます。 詳しくは、[パッセージ](/docs/services/discovery?topic=discovery-query-parameters#passages)を参照してください。 パッセージ取り出しは、{{site.data.keyword.discoveryshort}} News コレクションでは使用できません。

いくつかの事前作成済み照会を確認したい場合は、**「サンプル照会の使用 (Use a sample query)」**ボタンをクリックしてください。
{: tip}

## ステップ 3: さまざまな照会を試す
{: #querying-step3}

以下の照会を試してみてください。

`positive` センチメントを持つすべての文書を返すには、**「文書の検索 (Search for Documents)」**、**「Discovery 照会言語の使用 (Use the {{site.data.keyword.discoveryshort}} Query Language)」**をクリックします。
-  次に、**「フィールド (Field)」**ドロップダウンをクリックして「`enriched_text.sentiment.document.label`」を選択します。**「演算子 (Operator)」**には「`contains`」を選択し、「`positive`」の**「値 (Value)」**を入力します。  

   照会 `enriched_text.sentiment.document.label:positive` が **Visual Query Builder** の下に表示されます。

「`health and fitness`」カテゴリーに含まれるすべての文書を返すには、**「文書の検索 (Search for Documents)」**、**「Discovery 照会言語の使用 (Use the {{site.data.keyword.discoveryshort}} Query Language)」**をクリックします。
-  次に、**「フィールド (Field)」**ドロップダウンをクリックして「`enriched_text.categories.label`」を選択します。**「演算子 (Operator)」**には「`is`」を選択し、「`"health and fitness"`」の**「値 (Value)」**を入力します。

   照会 `enriched_text.categories.label::"health and fitness"` が **Visual Query Builder** の下に表示されます。 演算子「`::`」は完全一致を指定します。

エンティティー「`IBM`」を含むが、エンティティー「`Watson`」を含まないすべての文書を返すには、**「文書の検索 (Search for Documents)」**、**「Discovery 照会言語の使用 (Use the {{site.data.keyword.discoveryshort}} Query Language)」**をクリックします。
-  次に、**「フィールド (Field)」**ドロップダウンをクリックして「`enriched_text.entities.text`」を選択します。**「演算子 (Operator)」**には「`contains`」を選択し、「`IBM`」の**「値 (Value)」**を入力します。 **「ルールの追加 (Add rule)」**をクリックし、**「フィールド (Field)」**には「`enriched_text.entities.text`」を選択し、**「演算子 (Operator)」**には「`does not contain`」を選択して、「`Watson`」の**「値 (Value)」**を入力します。

   照会 `enriched_text.entities.text:IBM,enriched_text.entities.text:!Watson` が **Visual Query Builder** の下に表示されます。 演算子「`:!`」は「does not contain」を指定します。

## ステップ 4: 結合照会の作成
{: #querying-step4}

複数の照会パラメーターを結合することで、さらに的を絞った照会を作成できます。 `filter` パラメーターと `query` パラメーターの両方を使用して、{{site.data.keyword.IBM_notm}} の買収に関する文書を返してみます。 filter パラメーターが、`IBM` に言及している文書のみに結果を絞り込みます。次に、query パラメーターが、`acquisitions` に関するすべての結果を関連性の高い順に返します。

1.  「照会の作成 (Build queries)」アイコン![照会アイコン](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->をクリックして照会ページを開きます。 {{site.data.keyword.IBM_notm}} Press Releases を含むコレクションを選択し、**「開始 (Get started)」**をクリックします。

1.  **「照会する文書のフィルタリング (Filter which documents you query)」**の下で、以下を実行します。
    -  **「フィールド (Field)」**ドロップダウンをクリックして「`enriched_text.entities.text`」を選択します。**「演算子 (Operator)」**には「`contains`」を選択し、「`IBM`」の**「値 (Value)」**を入力します。

       照会「`enriched_text.entities.text:IBM`」が、エンティティー「`IBM`」に言及している文書のみに文書を絞り込みます。

1.  **「文書の検索 (Search for Documents)」**の下で、**「Discovery 照会言語の使用 (Use the {{site.data.keyword.discoveryshort}} Query Language)」**をクリックします。
    -  次に、**「フィールド (Field)」**ドロップダウンをクリックして「`enriched_text.concepts.text`」を選択します。**「演算子 (Operator)」**には「`contains`」を選択し、「`world wide web`」の**「値 (Value)」**を入力します。

       照会「`enriched_text.concepts.text:"world wide web"`」が、「`world wide web`」の概念を含むすべての文書を返し、それらの文書は関連性の高い順にランク付けされます。

1.  **「詳細オプション (More options)」**をクリックし、次に**「返すフィールド (Fields to return)」**をクリックし、**「指定 (Specify)」**を選択します。 「`text`」を選択します。 これにより、関連する記事のテキストに応答が制限され、それ以外はすべて除外されます。

1.  **「照会の実行 (Run query)」**をクリックします。 1 つの一致する文書 `"matching_results": 1` が検出されます。

## Step 5: 集約の作成
{: #querying-step5}

集約は、データ値の集合 (例えば、上位キーワード、エンティティーのセンチメント全体など) を返します。

{{site.data.keyword.IBM_notm}} Press Releases コレクション内の上位 10 個の概念を返す集約を作成してみます。

1.  **「照会の作成 (Build queries)」**アイコン ![照会アイコン](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> をクリックして照会ページを開きます。 {{site.data.keyword.IBM_notm}} Press Releases を含むコレクションを選択し、**「開始 (Get started)」**をクリックします。

1.  **「結果の分析を含める (Include analysis of your results)」**の下で以下を実行します。
    -  **「出力 (Output)」**ドロップダウンをクリックして`「上位の値 (Top values)」`を選択します。**「フィールド (Field)」**には「`enriched_text.concepts.text`」を選択し、**「カウント (Count)」**には「`10`」を入力します。

       「`Term`」は、「`concepts` `text`」フィールドの最も一般的な値を返します。 **「カウント (Count)」**は、返す結果の数を指定します。 照会`term(enriched_text.concepts.text,count:10)` が **Visual Query Builder** の下に表示されます。   

1.  **「詳細オプション (More options)」**をクリックし、**「戻す文書の数 (Number of documents to return)」**フィールドに `0` と入力します。

1.  **「照会の実行 (Run query)」**をクリックします。 上位 10 個の概念が、**「要約 (Summary)」**タブと**「JSON」**タブの両方に表示されます。 「要約 (Summary)」の例を以下に示します。

## ステップ 6: Watson Discovery News での照会の作成
{: #querying-step6}

{{site.data.keyword.discoverynewsshort}} は、コグニティブ洞察によって事前にエンリッチされた公開データ・セットです。 {{site.data.keyword.discoveryshort}} に含まれています。 このコレクションについて詳しくは、[Watson Discovery News](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) を参照してください。

{{site.data.keyword.discoverynewsshort}} の構成を調整したり、トレーニングを行ったり、{{site.data.keyword.discoverynewsshort}} コレクションに文書を追加したりすることはできません。 {{site.data.keyword.discoverynewsshort}} を使用して何を作成できるのかを示すデモを[ここ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://discovery-news-demo.ng.bluemix.net/){: new_window}で見ることができます。

以下のサンプル照会は、{{site.data.keyword.discoverynewsfull}} から、肯定的なセンチメントを持つ、Pittsburgh Steelers に関する上位 10 個の記事を返します。

1.  **「照会の作成 (Build queries)」**アイコン ![照会アイコン](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> をクリックして照会ページを開きます。 {{site.data.keyword.discoverynewsshort}} コレクションを選択し、**「開始 (Get started)」**をクリックします。 (スペイン語、ドイツ語、または韓国語の {{site.data.keyword.discoverynewsshort}} コレクションを照会するには、まず![「データの管理」](/images/icon_yourData.png)アイコンをクリックし、ドロップダウンから適切な言語を選択する必要があります。)

1.  **「文書の検索 (Search for documents)」**の下で、**「Discovery 照会言語の使用 (Use the {{site.data.keyword.discoveryshort}} Query Language)」**をクリックします。
    -  次に、**「フィールド (Field)」**ドロップダウンをクリックして「`text`」を選択します。**「演算子 (Operator)」**には「`contains`」を選択し、「`Pittsburgh Steelers`」の**「値 (Value)」**を入力します。 **「ルールの追加 (Add rule)」**をクリックし、次に**「フィールド (Field)」**ドロップダウンをクリックして「`enriched_text.sentiment.document.label`」を選択します。**「演算子 (Operator)」**には「`contains`」を選択し、「`positive`」の**「値 (Value)」**を入力します。

       **ビジュアル照会ビルダー**の下に、照会 `text:"Pittsburgh Steelers",enriched_text.sentiment.document.label:"positive"` が表示されます。

1.  **「詳細オプション (More options)」**をクリックし、次に**「戻す文書の数 (Number of documents to return)」**フィールドに「`10`」(デフォルト) を入力します。

1.  **「照会の実行 (Run query)」**をクリックします。 肯定的なセンチメントを持つ、Pittsburgh Steelers に関する上位 10 個の記事が表示されます。

**注:** Watson Discovery News 照会で返される結果の最大数は `50` です。

ニュース記事はいくつかの報道機関に配信される可能性があり、{{site.data.keyword.discoverynewsfull}} はそれらの中から各記事を選出するため、記事が重複することがあります。 これは、{{site.data.keyword.discoverynewsfull}} への照会の結果、複数の同じ記事またはほぼ同じ記事が返される可能性があることを意味します。 重複排除をオンにするには、**「詳細オプション (More options)」**の下から、**「重複する結果の除外 (Exclude duplicate results)」**を選択します。 このベータ機能について詳しくは、[照会結果から重複する文書を除外](/docs/services/discovery?topic=discovery-query-parameters#deduplication)を参照してください。
