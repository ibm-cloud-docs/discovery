---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-15"

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

# リリース・ノート

リリース・ノートは、前回のリリース以降に {{site.data.keyword.discoveryfull}} サービスに加えられた変更について説明します。
{: shortdesc}

## サービス API のバージョン管理
{: shortdesc}

API 要求には、`version=YYYY-MM-DD` という形式で日付を設定する version パラメーターが必要です。後方互換性のない方法で API が変更されると、API の新規マイナー・バージョンがリリースされます。

API 要求のたびに version パラメーターを送信してください。本サービスでは、指定された日付の API バージョン、またはその日付より前の最新のバージョンが使用されます。現在日付をデフォルトに設定しないでください。代わりに、ご使用のアプリと互換性のあるバージョンに一致する日付を指定し、より新しいバージョン用にアプリの準備ができるまでその日付を変更しないでください。

現行バージョンは `2017-11-07` です。

## ベータ版フィーチャー
{: #beta-features}

IBM は、ベータ版または試験的と分類される、サービス、フィーチャー、および言語サポートをリリースします。こうした機能は、不安定であったり、頻繁に変更されたり、十分な通知期間を設けずに中止されたりすることがあります。これらは、お客様が機能性を評価できるように提供されています。ベータ版または試験的な機能は、一般にリリースされる機能が提供するのと同レベルの性能または互換性を提供しない場合があります。これらの機能は、実稼働環境での使用を目的として設計されたものではなく、そういった使用はお客様の責任で行っていただくものです。


## 変更内容
{: #change-log}

使用可能な新機能とサービスに対する変更は、次のとおりです。

## 2017 年 12 月 15 日

- **エレメント分類**エンリッチメントがリリースされました。これは、文書管理においてエレメント (センテンス、リスト、表) を構文解析して、重要なカテゴリーおよびタイプを分類するものです。詳しくは、[エレメント分類](/docs/services/discovery/element-classification.html)を参照してください。**プレミアム**・プランに登録されたサービス・インスタンスではエレメント分類は使用できません。
- 中国語 (簡体字) およびオランダ語の基本的な言語サポートが追加されました。詳しくは、[言語サポート](/docs/services/discovery/language-support.html)を参照してください。現在のところ、中国語 (簡体字) およびオランダ語のコレクションの作成には API を使用する必要があります。
- Data Crawler に 2 つの新規パラメーター `proxy_host_port` および `read-timeout` が追加されました。詳しくは、[Data Crawler の構成](/docs/services/discovery/data-crawler-discovery.html)を参照してください。
- PDF 文書を取り込む際に以下の問題が発生することがあります。
  - 取り込み通知が照会されると、PDF 文書に対する `file_type` フィールドが `html` として返されます。
  - PDF 文書に対する結果の `extracted_metadata` オブジェクト内の `file_type` フィールドが `html` に設定されます。
  - 文書詳細 API も、PDF 文書に対する `file_type` フィールドを `html` として返します。

{{site.data.keyword.discoveryshort}} ツール:

- ベータ版の {{site.data.keyword.discoveryfull}} Knowledge Graph 用にビジュアル照会ビルダーが追加されました。 『[{{site.data.keyword.discoveryshort}} ツールを使用した Knowledge Graph の照会](/docs/services/discovery/building-kg.html#querying-kg)』を参照してください。

## 2017 年 11 月 30 日

- {{site.data.keyword.discoveryfull}} Visual Insights の試験的バージョンがリリースされました。Visual Insights を使用すると、セマンティック・エレメント、関係、コンセプトなどを {{site.data.keyword.discoveryshort}} が理解することによって識別される関連を視覚的に探索できます。詳しくは、[Visual Insights](/docs/services/discovery/visual-insights.html) を参照してください。試験的フィーチャー/ベータ版フィーチャーの説明については、[ここ](/docs/services/discovery/release-notes.html#beta-features)を参照してください。
- {{site.data.keyword.discoveryfull}} Knowledge Graph のベータ版がリリースされました。これは、複数の文書にわたってエンティティーおよび関連を照会するための新しいエンドポイントを提供します。これには、コンテキスト・ベースの検索および関連性ランキングが含まれます。このベータ版フィーチャーは、**拡張**プランのユーザーのみが使用できます。**専用** 環境では使用できません。詳しくは、[{{site.data.keyword.discoveryfull}} Knowledge Graph](/docs/services/discovery/building-kg.html) を参照してください。ベータ版フィーチャーの説明については、[ここ](/docs/services/discovery/release-notes.html#beta-features)を参照してください。
  - {{site.data.keyword.discoveryfull}} Knowledge Graph の既知の問題: すべてのエンティティー・タイプ名および関係タイプ名が、取り込み中に大文字に変換されます。例えば、エンティティー「GeoPoliticalEntity」は「GEOPOLITICALENTITY」に変換され、関係「partOf」は「PARTOF」に変換されます。
- さらに 2 つの言語の [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery/watson-discovery-news.html) がリリースされました。韓国語 (`collection_id`: `news-ko`) とスペイン語 (`collection_id`: `news-es`) です。韓国語およびスペイン語の {{site.data.keyword.discoverynewsfull}} は、API を介してのみ使用可能です。API を介したコレクションの照会について詳しくは、[API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection){: new_window} を参照してください。英語の {{site.data.keyword.discoverynewsfull}} の `collection_id` は `news-en` です。以前は、`collection_id` は `news` でした。以前の `collection_id` を使用している場合、引き続き機能しますが、新しいプロジェクト用に新しい `collection_id` に切り替えることをお勧めします。
- 照会結果間の相対的な関連性を示す `score` 値が照会結果で返されます。2017 年 11 月 30 日以降、`score` の計算方法が変わりました。`score` 値は、複数の検索またはセッションにまたがって使用するのではなく、1 回の検索での文書のランク付けにのみ使用されます。コレクションをトレーニングした場合、自然言語照会の結果に `score` 値が入って返されます。`score` は照会結果間の相対的な関連性を示すものであるため、しきい値として使用してはなりません。代わりに、トレーニングされたモデルと比較して結果の関連性を示す `confidence` を、しきい値を設定するために使用してください。しきい値の設定について詳しくは、『[信頼度スコア](/docs/services/discovery/train-tooling.html#confidence)』を参照してください。
- このリリース以降、パッセージ取り出しはセンテンス境界を検出し、センテンスの先頭から始まって末尾で終わるパッセージを返そうとします。以前は、多くのパッセージがセンテンスの途中で始まったり、終わったりすることがありました。パッセージ取り出しについて詳しくは、『[パッセージ](/docs/services/discovery/query-parameters.html#passages)』を参照してください。

## 2017 年 11 月 15 日

{{site.data.keyword.discoveryshort}} ツール:

- {{site.data.keyword.knowledgestudiofull}} で作成されたカスタム関係モデルを取り込むオプションが含まれている[関係抽出](/docs/services/discovery/building.html#relation-extraction)エンリッチメントが追加されました。
- [エンティティー抽出](/docs/services/discovery/building.html#entity-extraction)エンリッチメント {{site.data.keyword.discoveryshort}} ツールに、{{site.data.keyword.knowledgestudiofull}} で作成されたカスタム・エンティティー・モデルを取り込むオプションが含まれるようになりました。
- 日本語のコレクションを作成するオプションが {{site.data.keyword.discoveryshort}} ツールから削除されました。ただし、{{site.data.keyword.discoveryshort}} API を使用して日本語コレクションを作成するオプションは残っています。
- {{site.data.keyword.discoveryshort}} ツールはシンジケート環境をサポートするようになりました。

## 2017 年 11 月 10 日

{{site.data.keyword.discoveryshort}} ツール:

- {{site.data.keyword.discoveryshort}} ツールにパッセージ取り出しに関するオプションが追加されました。照会を行うときに、パッセージが返されるようにしたいフィールド、返されるパッセージの数、および、各パッセージの最大文字数を指定できるようになりました。限度、最小、および最大について詳しくは、『[パッセージ](/docs/services/discovery/query-parameters.html#passages)』を参照してください。

## 2017 年 11 月 8 日

すべての API 呼び出しの version ストリングが `2017-10-16` から `2017-11-07` に変更されました。このバージョンには以下の特徴があります。
- 各照会結果内の `score` は、`results_metadata` という名前の新しいオブジェクトに移行しました。
- 照会されるコレクションがトレーニングされており、照会が自然言語照会である場合、`results_metadata` に、結果の信頼度スコアを表す `confidence` フィールドが含まれます。詳しくは、『[信頼度スコア](/docs/services/discovery/train-tooling.html#confidence)』を参照してください。
- 空白が含まれているフィールド (例: `body.additional reading`) は、取り込み中にフィルター操作で除外されます。`notices` 記述は `The field 'additional reading' is invalid: whitespace, '.', '#' and ',' are invalid in a field name` になります。
- `result_metadata` フィールドは取り込み中にフィルター操作で除外されます。

## 2017 年 10 月 16 日

- すべての API 呼び出しの version ストリングが `2017-09-01` から `2017-10-16` に変更されました。このバージョンでは、{{site.data.keyword.alchemylanguageshort}} エンリッチメントを使用してエンリッチされた既存コレクションに新規文書をアップロードすることのサポートと、新規コレクションを作成してそれを {{site.data.keyword.alchemylanguageshort}} エンリッチメントを使用してエンリッチすることのサポートが非推奨になりました。{{site.data.keyword.alchemylanguageshort}} を使用してエンリッチされた既存コレクションは、できるだけ早く {{site.data.keyword.nlushort}} エンリッチメントにマイグレーションする必要があります。詳しくは、『[{{site.data.keyword.nlushort}} へのエンリッチメントのマイグレーション](/docs/services/discovery/migrate-nlu.html#migrating-enrichments-to-natural-language-understanding)』を参照してください。{{site.data.keyword.discoveryshort}} ツールも `2017-10-16` バージョンを使用します。詳しくは、以下の説明を参照してください。

{{site.data.keyword.discoveryshort}} ツール:

- {{site.data.keyword.discoveryshort}} ツールは、API の version ストリングに `2017-10-16` を使用します。したがって、このツールを使用する場合、`2017-10-16` より後に、既存の {{site.data.keyword.alchemylanguageshort}} コレクションに文書をアップロードすることはできず、 {{site.data.keyword.alchemylanguageshort}} エンリッチメントを使用してエンリッチされた新規コレクションを作成することもできません。コレクションをエンリッチするために引き続き {{site.data.keyword.discoveryshort}} ツールを使用したい場合は、まず最初にコレクションを {{site.data.keyword.nlushort}} にマイグレーションしてください。詳しくは、『[{{site.data.keyword.nlushort}} へのエンリッチメントのマイグレーション](/docs/services/discovery/migrate-nlu.html#migrating-enrichments-to-natural-language-understanding)』を参照してください。
- **データ・スキーマ・エクスプローラー**は、{{site.data.keyword.discoverynewsfull}} コレクション内のいくつかのエンリッチメントのサンプル照会を表示します。また、{{site.data.keyword.discoverynewsfull}} 内のそのエンリッチメントの例の値をさらに表示する「値をもっと表示 (Show more values)」リンクも表示されるようになりました。
- **「データの管理 (Manage data)」**画面で、コレクション統計情報の結合、エラーおよび警告、およびデータ洞察など、複数の生産性強化が行われました。
- 文書処理が終了したときにアラートを表示するメッセージが追加されました。

## 2017 年 10 月 9 日

- 新しい集約メトリック `unique_count` が API で使用可能になりました。これは、コレクション内の指定されたフィールドのユニークなインスタンスの数を返します。詳しくは、『[unique_count](/docs/services/discovery/query-aggregations.html#unique_count)』を参照してください。

{{site.data.keyword.discoveryshort}} ツール:

- **ビジュアル照会ビルダー**で、ヒストグラム集約およびタイム・スライス集約がサポートされるようになりました。タイム・スライス照会の異常検出をオンにするオプションもあります。
- **データ・スキーマ・エクスプローラー**は、選択されたエンリッチメントのサンプル照会を表示します。また、そのエンリッチメントの例の値をさらに表示する「値をもっと表示 (Show more values)」リンクも表示されるようになりました。
- **「データの管理 (Manage data)」**画面、**「データ・スキーマの表示 (View data schema)」**画面、および**「照会の作成 (Build queries)」**画面のナビゲートを速くするため、ハンバーガー・メニューが追加されました。

### 2017 年 10 月 3 日

- 文書分割が使用可能になりました。『[文書セグメンテーションによる文書の分割](/docs/services/discovery/building.html#doc-segmentation)』を参照してください。

### 2017 年 9 月 29 日

- 2017 年 9 月 29 日に、{{site.data.keyword.discoveryshort}} が`ドイツ`地域で使用可能になりました。EU データ規定に準拠するようにするため、この地域では AlchemyLanguage エンリッチメントはサポートされません。
- 既知の問題: 照会フィールドに空白を含むことはできません。{{site.data.keyword.discoveryshort}} で照会を作成するとき、照会フィールドに空白が含まれている (例: `body.additional reading`) と `400: Invalid query syntax error` を受け取ります。

### 2017 年 9 月 25 日

- プレミアム価格プランが使用可能になりました。詳しくは、[{{site.data.keyword.discoveryshort}} 価格プラン](/docs/services/discovery/pricing-details.html)を参照してください。
- 同じ環境内の複数のコレクションにまたがった、照会、フィールドのリスト表示、および通知の照会を行う機能が追加されました。詳しくは、『[複数コレクションの照会](/docs/services/discovery/using.html#multiple-collections)』を参照してください。
- {{site.data.keyword.discoveryshort}} の言語サポート情報は[言語サポート](/docs/services/discovery/language-support.html)にあります。

{{site.data.keyword.discoveryshort}} ツール:
- ビジュアル照会ビルダーはベータ版状況から GA 状況に移りました。現在、ビジュアル照会ビルダーでは、フィルター集約、タイム・スライス集約、およびヒストグラム集約はサポートされていません。それらの集約を作成するには、**「照会の作成 (Build queries)」**画面で、**「結果の分析を含める (Include analysis of your results)」**をクリックし、**「照会言語での編集 (Edit in Query Language)」**をクリックします。
- {{site.data.keyword.discoverynewsfull}} 照会の重複排除を行うベータ版機能が追加されました。
- 英語、ドイツ語、およびスペイン語でのコレクションに加えて、アラビア語、フランス語、イタリア語、韓国語、およびブラジル・ポルトガル語のコレクションを作成できるようになりました。
- 既知の問題: {{site.data.keyword.discoveryshort}} ツールはシンジケート環境をサポートしません。

### 2017 年 9 月 14 日

{{site.data.keyword.discoveryshort}} ツール:

- 変換された文書内のフィールドおよび値を表示するデータ・スキーマ・エクスプローラーが追加されました。この情報を使用すると、Discovery 照会言語を使用して照会を作成する前にコレクションのデータ構造を把握できます。データ・スキーマは、文書別 (「文書 (Document)」ビュー) またはフィールド別 (「コレクション (Collection)」ビュー) の 2 つの方法で表示できます。データ・スキーマ・エクスプローラーにアクセスするには、**「マイ・データ洞察 (My Data Insights)」**画面で**「データ・スキーマの表示 (View data schema)」**ボタンをクリックするか、左側の**「データ・スキーマの表示 (View Data Schema)」**アイコンをクリックします。

### 2017 年 9 月 6 日

- 照会から返される文書の重複を排除するベータ版機能が追加されました。このベータ版フィーチャーは、プライベート・コレクションと Watson Discovery News コレクションの両方に対して機能します。詳しくは、『[照会結果から重複する文書を除外](/docs/services/discovery/query-parameters.html#deduplication)』を参照してください。

現在のところ、文書の重複排除はベータ版機能としてのみサポートされています。詳しくは、この資料の上部にあるベータ版に関する説明を参照してください。

### 2017 年 8 月 31 日

- すべての API 呼び出しの version ストリングが `2017-08-01` から `2017-09-01` に変更されました。このバージョンに含まれている更新によって、プレビューおよび取り込み中に以下の無効な JSON フィールドはフィルター操作で除外され、有効な JSON フィールドのみが取り込まれるようにされます。競合および起こり得るエラーを回避するため、version ストリングを `2017-09-01` に更新してください。

   - 最上位レベルの `id`、`score`、および `highlight` (`add a document` 機能で文書 ID を使用して、コレクションへの文書の追加を引き続き行うことができます。詳しくは、[API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#add-doc){: new_window} を参照してください)
   - 最上位レベルの `_` 接頭部が付いたフィールド名 (結果として、ID で文書を照会するとき、`_id` の代わりに `id` を照会できます)
   - フィールド名の中の `#` および `,` 
   - `+` および `-` 接頭部が付いたフィールド名
   - フィールド名の `"` `"` 空の値

**注:** JSON 文書に、これらの文字が使われているフィールド名があるか、または、最上位レベルに `id`、`score`、および `highlight` がある場合、文書をコレクションに追加する前にそれらを除去する必要があります。そうしないと、それらのフィールドは空になります。文書をコレクションに追加する前にカスタム構成の作成と JSON の正規化を行うことによって、この問題を回避できます。『[カスタム構成](/docs/services/discovery/building.html#custom-configuration)』を参照してください。さらに、ファイル名の中に句読文字 `?`、`:`、または `#` がある文書では、取り込み時にエラーが発生します。これらの文字を含む文書は、取り込み前に名前変更してください。

- 関連する意味構造を持つ単語の突き合わせの結果の関連性を向上させるために `natural_language_query` の取得方式が更新されました。この更新は、関連性トレーニングがされていないコレクションにのみ影響します。`natural_language_query` を使用していて、関連性トレーニングを実施しなかった場合、返される結果の順序が改善される可能性があります。

{{site.data.keyword.discoveryshort}} ツール:

- Discovery 照会言語オプションと自然言語照会オプションとの切り替え、および、照会、フィルター、集約の間での切り替えを簡単にするために、照会ビルダーに変更が加えられました。


### 2017 年 8 月 25 日

- `passages` 配列に `field`、`start_offset`、および `end _offset` が含まれるようになりました。`field` は、パッセージの抽出元のフィールドの名前です。`start_offset` は、フィールド内のパッセージ・テキストの先頭文字です。`end_offset` は、フィールド内のパッセージ・テキストの終了文字です。

{{site.data.keyword.discoveryshort}} ツール:
**「照会の作成 (Build queries)」**画面でこの照会作成の機能強化を確認できます。

-  ビジュアル・ビルダーで {{site.data.keyword.discoveryshort}} 照会言語を使用して照会を作成するためのベータ版機能が追加されました。試してみるには、**「文書の検索 (Search for documents)」**セクションおよび**「照会する文書の制限 (Limit which documents you query)」**セクションで**「ビジュアル・モードでの作成 (Build in visual mode)」**をクリックします。照会をビジュアルに作成するときには、その下に **{{site.data.keyword.discoveryshort}} 照会言語**での照会が表示されます。

   現在のところ、ビジュアル照会ビルダーはベータ版機能としてのみサポートされています。詳しくは、この資料の上部にあるベータ版に関する説明を参照してください。

### 2017 年 8 月 18 日

{{site.data.keyword.discoveryshort}} ツール:

- [2017 年 8 月 11 日](/docs/services/discovery/release-notes.html#11aug)に導入されたベータ版ビジュアル集約ビルダーに、ネストされた集約および条件のサポートが追加されました。集約行当たり 3 つまでの条件という制限があります。

   現在のところ、ビジュアル集約ビルダーはベータ版機能としてのみサポートされています。詳しくは、この資料の上部にあるベータ版に関する説明を参照してください。

### 2017 年 8 月 11 日
{: #11aug}

{{site.data.keyword.discoveryshort}} ツール:

以下のフィーチャーは両方とも照会の作成に関する機能強化であり、**「照会の作成 (Build queries)」**画面で確認できます。

- 事前作成されたサンプル照会および集約のセットから照会を選択できるオプションが追加されました。右上の**「サンプル照会の使用 (Use a sample query)」**をクリックするとリストにアクセスできます。プライベート・データ・コレクションを照会する場合、サンプルでは、コレクション内で見つかった `top entities`、`categories` などが使用されます。これらの照会を、独自の照会を作成するための開始点として使用できます。サンプル照会は、{{site.data.keyword.discoverynewsfull}} コレクションおよびプライベート・コレクションの両方に使用可能です。

-  ビジュアル・ビルダーで集約を作成するためのベータ版機能が追加されました。試してみるには、**「{{site.data.keyword.discoveryshort}} 照会言語を使用した集約照会の作成 (Write an aggregation query using the {{site.data.keyword.discoveryshort}} Query Language)」**フィールドの上の**「ビジュアル・モードでの作成 (Build in visual mode)」**をクリックします。集約をビジュアルに作成するときには、その下に **{{site.data.keyword.discoveryshort}} 照会言語**で照会が表示されます。  

   現在のところ、ビジュアル集約ビルダーはベータ版機能としてのみサポートされています。詳しくは、この資料の上部にあるベータ版に関する説明を参照してください。

### 2017 年 7 月 31 日

- {{site.data.keyword.discoverynewsfull}} の新バージョンがリリースされました。元のバージョンは {{site.data.keyword.discoverynewsfull}} Original という名前に変更され、**2018 年 1 月 15 日**のサービス日付から除去されて廃止されました。マイグレーションの方法については、[Watson Discovery News Original からのマイグレーション](/docs/services/discovery/migrate-bwdn.html)を参照してください。
  **注:** {{site.data.keyword.discoveryshort}} の新規インスタンスを作成した場合、新バージョンの {{site.data.keyword.discoverynewsfull}} にのみアクセスできます。

- {{site.data.keyword.discoveryfull}} の新しい価格プランがリリースされました。詳しくは、[{{site.data.keyword.discoveryshort}} 価格プラン](/docs/services/discovery/pricing-details.html)を参照してください。

- すべての API 呼び出しの version ストリングが `2017-07-19` から `2017-08-01` に変更されました。このバージョンには、新しい価格プランおよび Watson Discovery News の新バージョンに関する更新が含まれています。競合および起こり得るエラーを回避するため、version ストリングを更新してください。

### 2017 年 7 月 19 日

 - 2017 年 8 月 1 日付けで発表された価格変更の一環として、非推奨の **30 日間無料トライアル**のプランを現在使用しているユーザーは**ライト**・プランに自動的に移行されます。この移行の結果として、既存ユーザーは、ライト・プランでの制限である、文書 _(2000)_、ストレージ _(200Mb)_、またはコレクション数 _(2)_ に達したり、それを超えたりすることがあります。 **ライト**・プランの制限を超えた場合、本サービスにさらにコンテンツを追加することはできませんが、コレクションの照会は引き続き実行できます。これらのすべての制限について、現在の状況を {{site.data.keyword.discoveryshort}} ツールまたは API を使用して確認できます。{{site.data.keyword.discoveryshort}} インスタンスへのコンテンツの追加を再開できるようにするには、以下のいずれかを行う必要があります。
   - **ライト**・プランの制限を超えないように、コレクションまたは文書、あるいは両方を削除します。
     API で [delete-doc](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-doc) メソッドを使用して文書を個々に削除するか、または、ツールを使用するか API で [delete-collection](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-collection) メソッドを使用してコレクション全体を削除することができます。
   - ストレージ必要量を満たすレベルにプランをアップグレードします。
 - 環境サイズが **`1`**、**`2`**、または **`3`** のお客様は、**拡張**プランに自動的に移行されます。

### 2017 年 7 月 17 日

 - 以下の機能がベータ版状況から GA 状況に移りました。

   - 関連性トレーニング
   - 自然言語照会
   - 強調表示

 - このリリース以降、{{site.data.keyword.discoveryfull}} は、エンリッチメントのメカニズムを {{site.data.keyword.alchemylanguageshort}} から {{site.data.keyword.nlushort}} に変更していきます。 {{site.data.keyword.alchemylanguageshort}} を非推奨にする処理が進行中であり、できるだけ早く {{site.data.keyword.nlushort}} の使用を開始するべきです。詳しくは、[{{site.data.keyword.alchemylanguageshort}} エンリッチメントから {{site.data.keyword.nlushort}} エンリッチメントへのマイグレーション](/docs/services/discovery/migrate-nlu.html)を参照してください。
   **注:** Watson Knowledge Studio と統合する場合は、引き続き {{site.data.keyword.alchemylanguageshort}} エンリッチメント構成が使用される必要があります。詳しくは、[{{site.data.keyword.knowledgestudiofull}} との統合](/docs/services/discovery/integrate-wks.html)を参照してください。

 - すべての API 呼び出しの version ストリングが `2017-06-25` から `2017-07-19` に変更されました。このバージョンでは、コレクション作成時に NLU デフォルト構成が有効になります。以前のバージョンの {{site.data.keyword.alchemylanguageshort}} でのエンリッチも引き続き可能です。

    デフォルト構成は {{site.data.keyword.nlushort}} を使用するように更新されました。競合および起こり得るエラーを回避するため、できるだけ早く version ストリングを更新してください。

 - Discovery ツール:

    {{site.data.keyword.alchemylanguageshort}} エンリッチメントを使用してエンリッチされたコレクションの洞察カードは自動的に更新されなくなりました。洞察カードが更新されるようにするには、コレクションを {{site.data.keyword.nlushort}} エンリッチメントに移行する必要があります。

    **2017 年 7 月 18 日**より前にコレクションを作成し、**デフォルト構成**を適用した場合、そのコレクションは {{site.data.keyword.alchemylanguageshort}} エンリッチメントを使用してエンリッチされています。この日付より後にコレクションに**デフォルト構成**を適用すると、{{site.data.keyword.nlushort}} エンリッチメントが使用されます (構成の名前はツール内で **Default Configuration with NLU** に切り替えられます)。 {{site.data.keyword.alchemylanguageshort}} エンリッチメントは非推奨になるため、新規コレクションでは使用しないでください。

### 2017 年 6 月 30 日

 -  2017 年 5 月 5 日にベータ版フィーチャーとして導入されたエンティティー正規化機能が GA 状況に移りました。詳しくは、[エンティティーを正規化するカスタム構成の作成](/docs/services/discovery/normalize-entities.html)を参照してください。

### 2017 年 6 月 23 日

 - すべての API 呼び出しの version ストリングが `2016-12-01` から `2017-06-25` に変更されました。この新しい version ストリングは、コレクションの言語がドイツ語 (`de`) またはスペイン語 (`es`) のどちらかに設定されている場合にその言語でエンリッチメントすることを可能にします。以前は、コレクションの言語設定に関わらず、すべてのエンリッチメントが英語で実行されていました。

    英語以外の言語でのエンリッチメントを使用しない場合は、引き続き version ストリング `2016-12-01` を使用できます。ただし、将来起こり得る競合を回避するため、できるだけ早く version ストリングを更新してください。

 - `timeslice` 集約の一部として異常検出が GA 機能として使用可能になりました。詳しくは、[タイム・スライス異常検出](/docs/services/discovery/query-aggregations.html#anomaly-detection)を参照してください。

 - Discovery ツール:

   - Discovery ツール (関連性ツール) を使用して照会結果の関連性を向上させるためのベータ版機能が追加されました。[Discovery ツールを使用した照会結果関連性の改善](/docs/services/discovery/train-tooling.html)を参照してください。

### 2017 年 6 月 19 日

  - Discovery ツール:

    - 新規コレクション内の文書の言語を、英語、スペイン語、またはドイツ語であると指定するためのオプションが追加されました。これを使用するには、**「新規コレクションの命名 (Name your new collection)」**ダイアログで**「文書の言語の選択 (Select the language of your documents)」**を選択します。

    - **「照会の作成 (Build queries)」**画面に**「サマリー (Summary)」**タブが追加されました。**「サマリー (Summary)」**タブには、既存の**「JSON」**タブで提供されるすべての照会結果の概要が表示されます。**「サマリー (Summary)」**に表示される内容は、照会およびエンリッチメントによって異なります。表示される可能性のある情報は、文書名または ID、集約の統計情報、関連性の順に並べられた文書パッセージ、およびエンリッチメント結果です。

    - **「照会の作成 (Build queries)」**画面に自然言語照会オプションが追加されました。これを使用するには、**「文書の検索 (Search for documents)」**セクションで**「自然言語で質問 (Ask a question in plain language)」**をクリックすると、質問を入力できるフィールドが表示されます。元の照会フィールド (以前のタイトルは**「照会またはキーワードを入力 (Enter a query or keyword)」**) には、**「Discovery 照会言語の使用 (Use the Discovery Query Language)」**ボタンをクリックしてアクセスできるようになりました。

    - **「照会の作成 (Build queries)」**画面のデザインが変更されましたが、フィールドおよびオプションはすべて残っています。古いフィールド名と新しいフィールド名は次のとおりです。

| **旧フィールド名**                                       | **新しいフィールド名またはセクション名**                                                                                             |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| 照会の作成と実行 (Write and run a query)                                    | 文書の検索 (Search for documents)|
| 照会結果の絞り込み (フィルター) (Narrow your query results (Filter))        | 照会する文書の制限 (Limit which documents you query)|
| 照会結果のグループ化 (集約) (Group query results (Aggregation))             | 結果の分析を含める (Include analysis of your results)|
| 表示するフィールド (Fields to display)                                      | 名前は変更されていませんが、新しい**「表示オプションのカスタマイズ (Customize display options)」**セクションに移されました。|
| 返す文書の数 (カウント) (Number of documents to return (Count))             | 返す文書の数 (Number of documents to return) [このフィールドは**「表示オプションのカスタマイズ (Customize display options)」**セクションに移されました。] |
| 一致するパッセージを含める (Include matching passages)                      | 関連するパッセージを含める (Include relevant passages) [このフィールドは**「表示オプションのカスタマイズ (Customize display options)」**セクションに移されました。] |
| 最初にスキップする照会フィールドの数 (オフセット) (Number of query fields to skip at the beginning (Offset)) | 最初にスキップする照会結果の数 (Number of query results to skip at the beginning) [このフィールドは**「表示オプションのカスタマイズ (Customize display options)」**セクションに移されました。] |

### 2017 年 6 月 5 日

 - Watson Discovery News 照会では、`text` および `alchemyapi_text` JSON フィールドに、各記事の最初の 150 個の単語のみが表示されるようになりました。`blekko.snippet` フィールドには、スニペット配列の最初のセンテンスのみが表示されます。

### 2017 年 5 月 30 日

 - 照会 API の `passages` パラメーターがベータ版から GA 状況に移りました。

### 2017 年 5 月 25 日

 - Discovery ツール: このリリースで、照会フィールドの強調表示が追加されました。この機能によって、結果ペインの JSON のフィールド名に黄色の強調表示が追加されます。照会またはフィルター操作の対象になったすべてのフィールドは、フィールドの内容が照会に一致しない場合でも、各結果で強調表示されます。集約で使用されるすべてのフィールドも照会結果で強調表示されますが、最初の集約操作のみが強調表示されます。

### 2017 年 5 月 10 日

 - `query` メソッドおよび `notices` メソッドで `highlight` パラメーターがサポートされるようになりました。このパラメーターはブール値です。照会を実行し、`highlight` を `true` と指定した場合、本サービスが返す出力には新しい `highlight` フィールドが含まれるようになりました。このフィールド内では、照会に一致する単語が HTML `*` (強調) タグで囲まれます。詳しくは、『[照会パラメーター](/docs/services/discovery/query-parameters.html#highlight)』を参照してください。

 - 環境の削除が部分的にのみ実行され、その結果として新しい環境を作成できない状況になることがあります。これはサービスごとに 1 つの環境しか許可されないためです。環境を削除してから作成しようとして、どちらかの操作が `pending` 状態で進まなくなる場合、この問題が起こっている可能性があります。これを回避するには、削除操作を再実行して完了させ、その後で新しい環境を作成します。

### 2017 年 5 月 8 日

 - 感情分析 (`docEmotion`) エンリッチメントの精度を向上させるため、感情トーン・スコア・モデルが更新されました。トレーニング・データ・セットが拡張され、フィーチャー・エンジニアリングが変更されました。その結果として、ベンチマーク・データ・セットでのモデルの精度が高くなりました。

### 2017 年 5 月 5 日

 - Watson Knowledge Studio で生成されたカスタム・モデルを使用するエンティティー正規化が Discovery サービスと一緒に使用できるようになりました。エンティティー正規化は、ソース文書中の同じ人または物に対する別々の参照に対して、正規化された (正準) 名前を挿入します。詳しくは、[エンティティーを正規化するカスタム構成の作成](/docs/services/discovery/normalize-entities.html)を参照してください。

     **注:** 現在のところ、エンティティー正規化はベータ版機能としてのみサポートされています。詳しくは、この資料の上部にあるベータ版に関する説明を参照してください。

 - ツールのエラー・ログは最大 8 ページの結果までに制限されなくなりました。文書名が使用可能でない場合でも、エラー・ログには文書 ID が表示されます。

 - 構成名は 50 文字に制限され、文字 `[a から z A から Z 0 から 9 から _]` のみを使用する必要があります。

 - 以前は API を介してのみ使用可能だった `passages` パラメーターが API と同様にツールでも使用できるようになりました。

### 2017 年 4 月 25 日

  - 本サービスでは、照会結果の正確性を高めるために*トレーニング・データ*を提供することが可能になりました。Discovery インスタンスにトレーニング・データを提供すると、本サービスは高機能 Watson アルゴリズムを使用して、最も関連性の高い結果を判別します。さらにトレーニング・データを追加すると、サービス・インスタンスが返す結果がより正確で洗練されたものになります。詳しくは、[照会結果の関連性の改善](/docs/services/discovery/train.html)および[API リファレンス](http://www.ibm.com/watson/developercloud/discovery/api/v1/#training-data)を参照してください。

  - ベータ版リリースとして `natural_language_query` パラメーターが API でサポートされるようになりました。このパラメーターを使用すると、Discovery サービスの照会言語ではなく自然言語で照会を指定できます。詳しくは、API リファレンスで [Query your collection](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection) メソッドを参照してください。

  - 資料の更新と誤りの訂正が行われました。

### 2017 年 4 月 14 日

照会 API (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`) に機能強化が加えられました。詳しくは、API リファレンスで [Query your collection](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection) メソッドを参照してください。

  - 照会 API で `passages` パラメーターがサポートされるようになりました。このパラメーターが `true` に設定されていると、照会は、コレクション内の文書から最も関連性の高いパッセージのセットを返します。それらのパッセージは、照会によって返されるすべての文書のテキストから最適なパッセージを判別するために、高度な Watson アルゴリズムによって生成されます。これによって、情報およびコンテキストをより正確に検出できるようになります。詳しくは、API リファレンスで [Query your collection](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection) メソッドを参照してください。

    - 照会で `passages=true` を指定すると、パッセージを抽出する処理が増えるためパフォーマンスが低下する可能性があります。大規模な環境では、パフォーマンスへの影響は軽減されることがあります。

    - `passages` パラメーターは、プライベート・コレクションでのみサポートされます。Watson Discovery News コレクションではサポートされません。

    - `passages` パラメーターは、現在は最大 10 個の結果を返します。返される結果の数を変更することはできません。

    - `passages` パラメーターは、コレクション内のどの文書からも最大 3 つのパッセージを返します。1 つの文書に 3 つを超える関連パッセージがさらに含まれていても、このパラメーターはそれらを返しません。

### 2017 年 4 月 7 日

- 照会 API (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`) で `sort` パラメーターがサポートされるようになりました。これを使用すると、ソート対象にする文書中のフィールドをコンマ区切りリストで指定できます。詳しくは、API リファレンスで [Query your collection](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection) メソッドを参照してください。
- 照会集約の `timeslice` パラメーターが、UNIX エポック・フォーマットの日付を正しく処理するようになりました。集約および `timeslice` パラメーターについて詳しくは、[照会リファレンス](/docs/services/discovery/query-reference.html#aggregations)を参照してください。
- エラー・メッセージが改善されました。
- 本サービスの Java SDK が更新されました。詳しくは、[API リファレンス](http://www.ibm.com/watson/developercloud/discovery/api/v1/?java)を参照してください。
- 照会でのワイルドカード使用についての以下の制限が修正され、正しく動作するようになりました。

  - 照会で機能するのは 1 つのみのワイルドカードでした。例えば、`query-month:*ctober` は機能しましたが、`query-month:*ctobe*` では構文解析エラーが生成されていました。
  - 大文字を含んでいるワイルドカードは照会では機能しませんでした。例えば、キーとフィールドのペア `{"borrower": "GOVERNMENT OF INDIA"}` があるとすると、`query-borrower:*ndia` は結果を返しましたが、`query-borrower:*NDIA` は返しませんでした。

**注:** ワイルドカードは照会の句の中では必要ありません。例えば、キーとフィールドのペア `{"borrower": "GOVERNMENT OF TIMOR"}` があるとすると、`query-borrower:"GOVERNMENT OF TIMOR"` は結果を返しますが、`query-borrower:"GOVERNMENT OF TI*OR"` は返しません。句の中でのワイルドカード使用が適用外である理由は、句の引用符 (`"`) で囲まれたすべての文字がエスケープされるためです。

### 2017 年 3 月 24 日

- Discovery ツールの「マイ・データ洞察 (My data insights)」画面にフィルター操作が追加されました。

### 2017 年 3 月 15 日

以下の既知の問題が検出されました。

-  HTML 文書、PDF 文書、および Word 文書から取り込まれたすべてのフィールドが **string** タイプとして処理されます。JSON フィールドおよび計算されたフィールド (例えば、センチメント・スコアなど) は、定義された通りのタイプとして処理されます。
- 現在、`preview` 操作は、サブミットされた JSON 文書内にネストされた JSON 配列があるかどうか検査しません。現在のところ、本サービスはネストされた JSON 配列をサポートしていないため、ネストされた配列を含んでいる文書は `preview` 操作を正常にパスできますが、取り込みを行おうとすると失敗します。
- 取り込みエラーが起こり、`unsupported text language` というメッセージが出される場合、以下の例のように `"language": "english"` エンリッチメント・オプションで構成を更新して、すべてのテキストが英語として解釈されるように強制します。

```json
"enrichments": [
   {
     "enrichment": "alchemy_language",
     "source_field": "author.label",
     "options": {
       "extract": "taxonomy,entity,relation,doc-emotion,doc-sentiment,concept,keyword",
       "sentiment": true,
       "quotations": true,
       "language": "english"
     }
   }
 ]
```
{: codeblock}

次のバグが修正されました。

- 本サービスのパフォーマンスと安定度が改善されました。

### 2017 年 3 月 8 日

 - 全体的なパフォーマンスを向上させるため、新しいタイムアウトの追加など、バックエンドの最適化が行われました。
 - 空き (`0` サイズ) 環境の環境状況が実際の状況に関係なく `pending` と報告される原因となっていたバグが修正されました。
 - {{site.data.keyword.discoveryshort}} によって現在サポートされている唯一の各国語は米国英語 (`en_US`) です。

### 2017 年 3 月 3 日

- Discovery ツールに「マイ・データ洞察 (My data insights)」画面が追加されました。

### 2017 年 2 月 26 日

-     {{site.data.keyword.discoverynewsshort}} 環境のパフォーマンスが改善されました。
-  {{site.data.keyword.discoverynewsshort}} サービスが一度に返す結果は 50 個のみです。回避策として、照会で `offset` パラメーターを使用して、結果をページ送りするようにします。
-  以下のコマンドを使用して、個々の文書と共に新規構成をサブミットできます。

```bash
curl -X POST -u {username}:{password} -F "file=@wikipedia-sample.html" -F "configuration=$(cat config.json)" "https://gateway.watsonplatform.net/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2016-12-01"
```
{: pre}
-  本サービスの PDF コンバーターおよび Word コンバーターは、中間ステップとして HTML を作成します。本サービスは、正規化された JSON への最終変換の前に、中間 HTML に対して追加の変換および正規化を適用することができます。

次のバグが修正されました。

-  エラー・コードが改善されました。
-  いくつかの資料の誤りが訂正されました。

### 2017 年 2 月 16 日

-  CSS セレクターを使用して JSON フィールドを選択し、それらのフィールドにエンリッチメントを適用できるようになりました。詳しくは、『[CSS セレクターを使用したフィールドの抽出](/docs/services/discovery/building.html#using-css)』を参照してください。
-  [update-environment メソッド](http://www.ibm.com/watson/developercloud/discovery/api/v1/#update_environment)に新しいパラメーター `size: X` を渡すことによって、環境のサイズを増やせるようになりました。ここで、`X` は 0 から 3 までの整数です。環境のサイズおよび属性について詳しくは、『[create-environment メソッド](http://www.ibm.com/watson/developercloud/discovery/api/v1/#create_environment)』を参照してください。

    **注:** 既存環境のサイズを小さくすることはできません。環境のサイズを小さくしたい場合は {{site.data.keyword.IBM}} サポートに連絡してください。

-  新しい照会演算子が使用可能になりました。`::!` 演算子が、「等しくない」を表す単項演算子として追加されました。例えば、`query=field::!value` (等しくない) を実行できるようになりました。以前は、含んでいないことを示す排除演算子は `:!` のみでした (例えば `query=field:!value`)。

次のバグが修正されました。

-  セキュリティー更新が適用されました。
-  検索アラートの状況メッセージが改善されました。

### 2017 年 2 月 1 日

以下の注意事項は、特に Data Crawler 1.3.0 リリースに当てはまります。

-   Data Crawler は、文書をアップロードするために使用された `document_id` の値と、アップロードの状況を記録します。このログの他には、変換通知はどこにも保持されません。現在はこのデータと対話するためのツールはありませんが、時間が許せばそういったツールが開発されることが見込まれます。このデータには、リモート DBMS を使用するよう構成できる H2 データベースを介してアクセス可能です。

### 2017 年 1 月 16 日

以下の注意事項は、特に Data Crawler 1.2.5 リリースに当てはまります。

-  Data Crawler は、オプションで、ファイルのアップロード直後にポーリングを実行して文書状況を調べることができます。この検査は「文書のアップロード」に関する Crawler のコンセプトの一部であるため、この検査が有効になっていると、{{site.data.keyword.discoveryshort}} サービスがユーザーのために並行して処理できるよりも多くの文書を Crawler が並行してアップロードすることは実際には不可能です。

    `check_for_completion` フィーチャーの副作用は、文書で障害が起こったときに Crawler がその原因をユーザーに公開する可能性があることです。正常にアップロードされたが処理で障害が起こった文書に付加されたすべての通知が Crawler ログに表示されます。それらの通知は処理可能なファイルにエクスポートされませんが、IBM はそのための機能提案があれば歓迎します。

### 2017 年 1 月 5 日

以下の注意事項は、2016 年 12 月 15 日の GA リリース後に識別された問題について説明しています。

-   `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` 呼び出しまたは `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]` 呼び出しを使用して文書を追加すると、呼び出しは文書 ID と **processing** 状況を返します。その後、その文書を `GET /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]` 呼び出しを使用して照会すると、取り込みが完了するまで状況は **processing** のままであり、取り込みの完了時点で **available** に変わります。

    `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]` 呼び出しを使用して既存の文書を**更新**すると、対応する **GET** 呼び出しは、更新される文書が本サービスによってまだ完全に処理されていなくても、`available` 状況を返します。`available` 状況が示しているのは元の文書と更新済み文書のどちらの場合もあり得ます。更新操作がエラーを返す場合を除いて、現在は更新後の文書の状況を判別する手段はありません。

文書の更新をサブミットした後で最大 10 分間待機し、その後で更新後の内容を照会するようにすると、これを回避できます。
-   JSON 配列はアップロードできません。JSON 配列をアップロードするには、各セクションを個々にアップロードする必要があります。例えば、以下の JSON をサービスにアップロードすることはできません。

    ```json
    [{
      "accepted": 1,
      "answer": "You shouldn't have any issues keeping it on all the time however some thing to consider is any counters you may have like the use of millis code . From the Arduino docs on millis a This number will overflow go back to zero after approximately 50 days. blockquote So for projects that are on for long periods of time you may not see an issue immediately but something like this could pop up and cause errors down the road. ",
      "answerScore": "49",
      "authorUserId": "3",
      "authorUsername": "Butzke",
      "downModVotes": 0,
      "id": 2,
      "subtitle": "I'm making a simple Arduino web server and I want to keep it turned on all the time. So it must endure to stay working continuously. I'm using an Arduino Uno with a Ethernet Shield. It's powered with a simple outlet power supply 5V 1A. My Questions Will I have any problems leaving the Arduino turned on all the time? li Is there some other Arduino board better recommended for this? li Are there any precautions that I need to heed regarding this? li ul ",
      "tags": "<arduino-uno><web-server><ethernet>",
      "title": "Is an Arduino capable of running 24 7?",
      "upModVotes": 49,
      "userId": "11",
      "userReputation": 4535,
      "username": "sachleen",
      "views": 3234
    }, {
      "accepted": 0,
      "answer": "A couple of things to keep in mind outside of Sachleen's mention of Milli's Like any electronics heat can be disruptive. The micro controller itself isn't likely going to be a huge issue from the perspective of heat but other components like the power supply might cause issues. li If your code uses EEPROMWrite a be aware that the EEPROM is only rated for something in the neighbourhood of 100 000 writes. li ul ",
      "answerScore": "24",
      "authorUserId": "3",
      "authorUsername": "Butzke",
      "downModVotes": 0,
      "id": 3,
      "subtitle": "I'm making a simple Arduino web server and I want to keep it turned on all the time. So it must endure to stay working continuously. I'm using an Arduino Uno with a Ethernet Shield. It's powered with a simple outlet power supply 5V 1A. My Questions Will I have any problems leaving the Arduino turned on all the time? li Is there some other Arduino board better recommended for this? li Are there any precautions that I need to heed regarding this? li ul ",
      "tags": "<arduino-uno><web-server><ethernet>",
      "title": "Is an Arduino capable of running 24 7?",
      "upModVotes": 24,
      "userId": "13",
      "userReputation": 489,
      "username": "Matthew G.",
      "views": 3234
    }]
    ```
    {: codeblock}

    この情報を本サービスにアップロードするには、以下の例のように、配列を切断して各セクションをアップロードします。

    セクション 1:

    ```json
    {
      "accepted": 1,
      "answer": "You shouldn't have any issues keeping it on all the time however some thing to consider is any counters you may have like the use of millis code . From the Arduino docs on millis a This number will overflow go back to zero after approximately 50 days. blockquote So for projects that are on for long periods of time you may not see an issue immediately but something like this could pop up and cause errors down the road. ",
      "answerScore": "49",
      "authorUserId": "3",
      "authorUsername": "Butzke",
      "downModVotes": 0,
      "id": 2,
      "subtitle": "I'm making a simple Arduino web server and I want to keep it turned on all the time. So it must endure to stay working continuously. I'm using an Arduino Uno with a Ethernet Shield. It's powered with a simple outlet power supply 5V 1A. My Questions Will I have any problems leaving the Arduino turned on all the time? li Is there some other Arduino board better recommended for this? li Are there any precautions that I need to heed regarding this? li ul ",
      "tags": "<arduino-uno><web-server><ethernet>",
      "title": "Is an Arduino capable of running 24 7?",
      "upModVotes": 49,
      "userId": "11",
      "userReputation": 4535,
      "username": "sachleen",
      "views": 3234
    }
    ```
    {: codeblock}

    セクション 2:

    ```json
    {
      "accepted": 0,
      "answer": "A couple of things to keep in mind outside of Sachleen's mention of Milli's Like any electronics heat can be disruptive. The micro controller itself isn't likely going to be a huge issue from the perspective of heat but other components like the power supply might cause issues. li If your code uses EEPROMWrite a be aware that the EEPROM is only rated for something in the neighbourhood of 100 000 writes. li ul ",
      "answerScore": "24",
      "authorUserId": "3",
      "authorUsername": "Butzke",
      "downModVotes": 0,
      "id": 3,
      "subtitle": "I'm making a simple Arduino web server and I want to keep it turned on all the time. So it must endure to stay working continuously. I'm using an Arduino Uno with a Ethernet Shield. It's powered with a simple outlet power supply 5V 1A. My Questions Will I have any problems leaving the Arduino turned on all the time? li Is there some other Arduino board better recommended for this? li Are there any precautions that I need to heed regarding this? li ul ",
      "tags": "<arduino-uno><web-server><ethernet>",
      "title": "Is an Arduino capable of running 24 7?",
      "upModVotes": 24,
      "userId": "13",
      "userReputation": 489,
      "username": "Matthew G.",
      "views": 3234
    }
    ```
    {: codeblock}

### 一般出荷版リリース (2016 年 12 月 15 日)

以下の注意事項は、{{site.data.keyword.discoveryfull}} サービスの一般出荷版 (GA) リリースに当てはまります。

#### 一般的な注意事項

-   現在のところ、フィールドのデータ・タイプを指定することはできません。すべてのフィールドはテキスト (データ・タイプ **string**) として索引付けられます。
-   本サービスでの作業に API を使用する場合、各呼び出しに API バージョンを指定する必要があります。現行の API バージョンは **2016-12-01** です。

    **注:** GA リリースでは特定のバージョンが強制されるわけではありませんが、将来のリリースとの互換性のためにリストしておく必要があります。

-   {{site.data.keyword.knowledgestudiofull}} で作成されたカスタム・モデルと共に本サービスを使用できます。取り込まれた文書をエンリッチするためにカスタム・モデルを使用できます。カスタム・モデルを {{site.data.keyword.discoveryshort}} サービスと統合するには API を使用する必要があり、ツールを使用して統合を実行することはできません。詳しくは、[ {{site.data.keyword.knowledgestudiofull}} との統合](/docs/services/discovery/integrate-wks.html "{{site.data.keyword.knowledgestudiofull}} からのカスタム・モデルを {{site.data.keyword.discoveryshort}} サービスと統合してカスタム・エンリッチメントを提供できます。")を参照してください。

#### データ管理

-   検索索引は暗号化されません。
-   バックアップ機能および復元機能をユーザーが制御することはできません。

#### 環境

-   独自のデータをアップロードするために作成できる環境はサービス・インスタンス当たり 1 つのみです。
-   {{site.data.keyword.discoveryshort}} サービスが置かれているアベイラビリティー・ゾーンは 1 つのみ (米国南部) です。
-   現時点では、専用プランおよびプレミアム・プランは利用できません。

#### 環境のサイズ設定

-   新しい環境を作成するときにのみ、環境のサイズを選択できます。環境のサイズを変更する機能は、現在のところユーザーには使用可能でありません。
-   RAM の大きい環境サイズを選択するとパフォーマンスが高くなります。
-   現在、具体的なユース・ケースに使用できる規範的なサイズ設定推奨値はありません。
-   {{site.data.keyword.knowledgestudiofull}} モデルのカスタム・サイズ変更をユーザーが行うことはできません。詳しくは、お客様担当の {{site.data.keyword.IBM}} 担当員にお問い合わせください。

#### 取り込みに関する制限

-   現在、取り込みレートは、並行して 100 までの文書取り込み操作に制限されています。取り込みのために本サービスに文書をサブミットするアプリケーションは、HTTP 429 エラーに注意を払い、状況に応じて取り込み要求を減速する必要があります。
-   {{site.data.keyword.alchemylanguageshort}} エンリッチメントは、フィールドごとに先頭 50 KB までに制限されています。
-   {{site.data.keyword.knowledgestudiofull}} カスタム・モデルからのエンリッチメントは制限されませんが、文書を 10 KB のチャンクに分割してください。チャンク境界をまたがる関係には注釈は付けられません。

#### 照会に関する制限

-   過大な照会負荷が原因で検索索引プロセスが自動的に再始動されることがあります。
-   照会を実行するアプリケーションは、並行照会の数について妥当な制限を設ける必要があります。

### 既知の問題

-   ツールを使用して文書を削除することはできません。文書を削除する必要がある場合は、API リファレンスの説明に従って、API の [Delete a document](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-doc) メソッドを使用する必要があります。

-   現在のところ、API は文書の取り込み中に生成された通知 (警告およびエラー) のリスト取得をサポートしていません。したがって、ツールは取り込み通知のリストを表示できません。そのため、Data Crawler によってクロールされる文書の取り込みが失敗した場合でも、どの文書なのかを判別する簡単な方法はありません。
-   文書の状況情報は常に正確であるとは限りません。
    -   構成されたタイムアウトである 10 分よりも長い取り込み操作があると、本サービスは、その取り込み操作が完了するまではその文書を認識しないことを報告します。操作が完了した後は、文書状況は使用可能であり、正確です。
    -   正常に索引付けされたがエラーが生成された文書では、文書が完全に索引付けされるまでの短い間 **failed** の状況になることがあります。文書が完全に索引付けされた後にリストされる状況は正確です。
-   ツールを使用して特定の文書を置換することはできません。これを行おうとすると、2 番目の文書は別の文書としてアップロードされます。API を使用していて、置換する文書の ID が分かっている場合は、置換を行うことができます。API リファレンスの [Update a document ](http://www.ibm.com/watson/developercloud/discovery/api/v1/#update-doc)を参照してください。Data Crawler を使用している場合、更新された文書を前の文書と同じ URL からアップロードすると、元の文書が置き換えられます。
-   ツールを使用して構成内のエンリッチメントを編集する場合は、抽出のために使用されるエンリッチメントのみを編集できます。その他のエンリッチメント (例えば、{{site.data.keyword.knowledgestudiofull}} モデルからのカスタム・エンリッチメント) を追加または編集したい場合は、API を使用する必要があります。詳しくは、API リファレンスで [Update a configuration](http://www.ibm.com/watson/developercloud/discovery/api/v1/#replace_configuration) メソッドを参照してください。
-   以下の注意事項は、特に Data Crawler に当てはまります。
    -   Data Crawler は、アップロードの失敗を検出した場合、アップロードを再試行します。
    -   Data Crawler は、正常にアップロードされたが、変換または索引付けが失敗した文書を再試行できません。
    -   Data Crawler は、ダウンストリーム状況を検査する機能を持たず、ダウンストリームで障害が起こった URL を再アップロードしません。
    -   どの文書が Data Crawler によって取り込まれたのかを判別する簡単な方法はありません。例えば、500 文書のセットに対して Data Crawler を実行した場合に、Data Crawler が合計 212 文書のコレクションと 65 文書のサブミット失敗を報告することが考えられます。残りの 223 文書の状況は判別不能です。

        回避策はありますが、複雑であり、API の直接呼び出しが必要です。{{site.data.keyword.IBM}} サポートに連絡してください。
-   {{site.data.keyword.discoveryshort}} 用の Java、Python、および Node.js の SDK は、デフォルト REST (cURL) API で提供されるすべての機能を提供するわけではありません。すべての cURL メソッドに対して非 cURL SDK で等価のメソッドがあるわけではなく、すべての非 cURL メソッドが等価の cURL のすべての機能を同じように提供するわけではありません。言い換えると、Java、Python、および Node.js の SDK は、現在のところ、cURL API の機能のサブセットのみを提供します。
-   Word コンバーターを使用する場合、`style` キーを使用してヘッダーを突き合わせるほうが、`level` キーを使用して行うよりもずっと正確で効率的です。
