---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-30"

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

# Watson Discovery Visual Insights
{: #visual-insights}

{{site.data.keyword.discoveryfull}} Visual Insights は、試験的フィーチャーであり、これを使用すると、セマンティック・エレメント、関係、コンセプトなどを {{site.data.keyword.discoveryshort}} が理解することによって識別される関連を視覚的に探索できます。

新規アプリケーションまたは既存ソリューションに統合してユーザーが必要とする情報をユーザーに提示できるような照会を {{site.data.keyword.discoveryshort}} を使用して作成する前に、{{site.data.keyword.discoveryfull}} Visual Insights を使用してコレクションについての知識を深めることができます。

Visual Insights は、試験的リリースの間はパブリック環境でのみ使用可能です。

**特記事項:** Visual Insights は試験的フィーチャーです。試験的というのは、不安定であったり、頻繁に変更されたり、十分な通知期間を設けずに中止されたりすることがあることを意味します。これはお客様が機能性を評価できるように提供されています。一般にリリースされる機能が提供するのと同レベルの性能または互換性は提供されない可能性があります。実稼働環境での使用を目的として設計されたものではなく、そういった使用はお客様の責任で行っていただくものです。詳しくは、『[ベータ版/試験的フィーチャー](/docs/services/discovery/release-notes.html#beta-features)』を参照してください。

## Visual Insights のクイック・ツアー
{: #quick-tour-visual-insights}

![Discovery Visual Insights クイック・ツアー](images/discovery-visualinsights-quicktour.png)

Visual Insights 画面は 4 つの主要エリアに分割されています。

### 検索バー
{: #search-bar}

最上位にある**検索バー**を使用して、{{site.data.keyword.discoveryshort}} コレクションを照会できます。

- {{site.data.keyword.Bluemix_notm}} 資格情報を使用してログインしている場合、ご使用のアカウントに関連付けられた {{site.data.keyword.discoveryshort}} インスタンスからのすべてのコレクションが、コレクションのドロップダウンで使用可能になります (デフォルトでは {{site.data.keyword.discoverynewsfull}})。ログインしていない場合、{{site.data.keyword.discoverynewsfull}} コレクションのみが使用可能になります。
- コレクションを選択し、検索ボックスに照会 (例: `What is net neutrality`) を入力し、**「検索 (search)」**ボタンをクリックして検索します。大きなコレクションの場合、結果が表示されるまでに 1 分以上かかることがあります。`documents`、`concepts`、`people`、`locations`、`organizations`、または `companies` ボタンをクリックして、検索をフィルタリングできます。
- オプションで、ヘッダーにある ![照会アイコン](images/discovery-query-icon.png) アイコンをクリックすることによって、表示された結果中の任意の項目 (エンティティー、コンセプト、または文書) を選択できます。
- プライベート・コレクションが選択され、照会が入力されなかった場合、そのコレクションから最大 1000 個の文書が[詳細ペイン](/docs/services/discovery/visual-insights.html#details-pane)に表示されます。{{site.data.keyword.discoverynewsshort}} コレクションが選択され、照会が入力されなかった場合、最近の 100 の記事が選択されて表示されます。

### ネットワーク表示
{: #network-display}

検索バーの下にある中央パネルは**ネットワーク表示**です。これは、照会結果のインタラクティブな視覚化です。

-  **ネットワーク表示**は、照会結果から抽出された文書、エンティティー、およびコンセプトのグラフィカル表現です。ピンク色のノードは文書を表し、青いノードはエンティティーまたはコンセプトを表します。各文書ノードは、{{site.data.keyword.discoveryshort}} によってその文書内で検出されたすべてのエンティティーおよびコンセプトのノードにリンクされます。この視覚化では、似ている文書ほど、互いの近くに配置されます。
- **ネットワーク表示**の任意のノードにマウスを移動させると、それに関連付けられたタイトルが表示され、他のノードへのリンクが強調表示されます。
- 任意のノードをクリックすると、そのノードに関する情報が[詳細ペイン](/docs/services/discovery/visual-insights.html#details-pane)に表示されます。

### 詳細ペイン
{: #details-pane}

ネットワーク表示の右は**詳細ペイン**です。

- 詳細ペインには、文書の機密区分と日付 (使用可能な場合)、短い抜粋 (文書全体を開くオプションがあります)、リンクしている先のエンティティーおよびコンセプトなど、文書についての詳細が表示されます。
- ネットワーク表示で文書以外のノードが選択された場合、そのノードに関する情報が詳細ペインの最上部に表示されます。
- リンクされたエンティティーまたはコンセプトのいずれかを詳細ペインでクリックすると、対応するノードがネットワーク表示で選択されます。

### ナビゲーション・ペイン
{: #navigation-pane}

ネットワーク表示の左は**ナビゲーション・ペイン**です。このペインは、選択されたコレクションの照会結果から抽出された最もよく使われている用語のタグ・クラウド概観を提供します。大きく表示されている用語ほど、照会結果内にある頻度が高い用語です。

- タグ・クラウド内の任意の用語を選択するとピンク色に変わり、ネットワーク表示ではそれに関連付けられているすべての文書が強調表示されます。詳細ペインには、強調表示された文書のリストが表示されます。タグ・クラウド内の他の用語は、次のように、選択した用語との関係を示すようになります。
  - グレー表示された用語は、強調表示された文書のどれとも関連付けられていません。
  - 紫色になった用語は、強調表示されたすべての文書に関連付けられており、それらの文書を区別しようとしても役に立ちません。
  - 青色のままの用語は、強調表示された文書の一部 (すべてではない) に関連付けられており、したがって、強調表示された文書の集合を絞り込むために使用できます。これらの用語の 1 つを選択すると、強調表示された文書の集合が、両方のタグに関連付けられている文書のみに縮小され、ネットワーク表示ではそれらの文書が配置されている領域に表示が絞られます。この方法を使用すると、大きな文書集合を数回のクリックで小さな集合に絞り込むことができます。
- 選択された用語を選択解除するには、その用語をもう一度クリックします。選択されたすべての用語をクリアするには、タグ・クラウドで単語のすき間の空白部分をクリックします。グレー表示されたタグをクリックすると、既存の選択がクリアされ、その用語が選択されます。
- タグ・クラウドの上部に、文書 (documents)、人 (people)、コンセプト (concepts)、組織 (organizations)、場所 (locations)、および企業 (companies) のタイプと数が表示されます。いずれかの項目をクリックすると、タグ・クラウドおよびネットワーク表示の視覚化をフィルター操作できます。

## Visual Insights の使用
{: #using-visual-insights}

Visual Insights を使用すれば、ログインせずに {{site.data.keyword.discoverynewsfull}} を照会できます。独自のコレクションで Visual Insights を使用するには以下が必要です。

- {{site.data.keyword.discoveryshort}} インスタンスを含んでいる {{site.data.keyword.Bluemix_notm}} アカウント。
- その {{site.data.keyword.discoveryshort}} インスタンス内の、[エンティティー抽出](/docs/services/discovery/building.html#entity-extraction)エンリッチメントを使用してエンリッチされ、それに加えてオプションで、[概念タグ付け](/docs/services/discovery/building.html#concept-tagging)、[キーワード抽出](/docs/services/discovery/building.html#keyword-extraction)、[関係抽出](/docs/services/discovery/building.html#relation-extraction)、および[カテゴリー分類](/docs/services/discovery/building.html#category-classification)エンリッチメントを使用してエンリッチされた、1 つ以上のコレクション。他のエンリッチメントを含めることもできますが、Visual Insights では表されません。

{{site.data.keyword.discoveryshort}} の詳細と、無料での開始方法については、[Watson {{site.data.keyword.discoveryshort}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/services/discovery/){: new_window} を参照してください。

{{site.data.keyword.Bluemix_notm}} アカウント、{{site.data.keyword.discoveryshort}} インスタンス、およびデータを設定した 1 つ以上のコレクションを準備できたら、ログインしたときに Visual Insights でコレクションが表示されるようになります。

Visual Insights へのログイン

1. [{{site.data.keyword.discoveryshort}} Visual Insights ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://visual-insights.bluemix.net){: new_window} を開きます。
1. 検索バーの ![プロファイル・アイコン](images/discovery-profile-icon.png) アイコンをクリックします。
1. {{site.data.keyword.Bluemix_notm}} ID およびパスワードを入力します。少し経つと、コレクションが検索バーで選択できるようになります。

## フィードバックの提供
{: #providing-feedback}

{{site.data.keyword.discoveryshort}} Visual Insights に関するフィードバックをお待ちしています。フィードバックのリンクにアクセスするには、ヘッダーの ![情報アイコン](images/discovery-info-icon.png) アイコンをクリックしてください。
