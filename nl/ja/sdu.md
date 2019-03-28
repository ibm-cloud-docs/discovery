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
{:gif: data-image-type='gif'}

# Smart Document Understanding
{: #sdu}

Smart Document Understanding (SDU) は、{{site.data.keyword.discoveryfull}} をトレーニングして文書内のカスタム・フィールドを抽出するための新しい方法です。{{site.data.keyword.discoveryshort}} に取り込まれる文書の索引作成方法をカスタマイズすると、アプリケーションから返される回答が改善されます。

SDU では、文書内のフィールドに注釈を付けることでカスタム変換モデルをトレーニングします。ユーザーが注釈を付けることで、Watson は学習を行い、注釈の予測を開始します。 SDU モデルは、エクスポートして他のコレクションで使用することができます。 

## サポートされる文書タイプおよびブラウザー
{: #doctypes}

Smart Document Understanding でサポートされる文書タイプ: 
-  ライト・プラン: PDF、Word、PowerPoint、Excel、JSON\*、HTML\*
-  拡張プラン: PDF、Word、PowerPoint、Excel、PNG\*\*、TIFF\*\*、JPG\*\*、JSON\*、HTML\* 

\* JSON 文書と HTML 文書は {{site.data.keyword.discoveryfull}} でサポートされていますが、SDU エディターでは編集できません。HTML 文書と JSON 文書の構成を変更するには、API を使用する必要があります。詳しくは、「[API reference ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery/){: new_window}」を参照してください。

\*\* 個々の画像ファイル (PNG、TIFF、JPG) がスキャンされ、テキスト (存在する場合) が抽出されます。PDF、Word、PowerPoint、および Excel の各ファイルに埋め込まれている PNG、TIFF、および JPEG の各画像もスキャンされ、テキスト (存在する場合) が抽出されます。

サポートされるブラウザーは、Chrome と Firefox です。

## Smart Document Understanding エディターの使用
{: #annotate}

SDU エディターは、サポートされている文書タイプを含み、要素分類エンリッチメントが適用されていない新しいコレクションにのみ使用できます。既存のプライベート・コレクションには、元の構成方式が使用されます。既存のコレクションで SDU エディターを使用する場合は、新しいコレクションを作成してそれらの文書をそのコレクションにアップロードする必要があります。SDU エディターを使用しない場合は、API を使用して構成をセットアップできます。「[API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery/){: new_window}」を参照してください。
{: important}

SDU エディターの機能は {{site.data.keyword.discoveryshort}} ツールでのみ使用できます。API では使用できません。
{: note}

Smart Document Understanding エディターをナビゲートするには、以下のようにします。

まだ {{site.data.keyword.discoveryshort}} のインスタンスと環境を作成していない場合は、[はじめに](/docs/services/discovery?topic=discovery-getting-started#getting-started)で手順を確認してください。
{: tip}

1. **「データの管理 (Manage Data)」**画面で、**「独自のデータをアップロード (Upload your own data)」**ボタンをクリックし、{{site.data.keyword.discoveryshort}} で新しいプライベート・コレクションを作成します。
1. 必要に応じて、文書をコレクションにドラッグ・アンド・ドロップするか、**「コンピューターから参照 (browse from computer)」**をクリックしてドキュメントをアップロードします。アップロードが完了すると、次の情報が表示されます。
   -  文書から識別されたフィールド。
   -  ドキュメントに適用されたエンリッチメント。エンティティー抽出、センチメント分析、カテゴリー分類、概念のタグ付けの各エンリッチメントが {{site.data.keyword.discoveryshort}} によって `text` フィールドに自動的に適用されます (コネクターを使用して文書をインポートした場合は別です)。`text` フィールドにエンリッチメントを追加 (または削除) できます。
   -  すぐに実行できる事前作成済みの照会。
1. 右上の**「データの構成 (Configure data)」**をクリックします。 
1. **「データの構成 (Configure data)」**画面には、**「フィールドの識別 (Identify fields)」**、**「フィールドの管理 (Manage fields)」**、**「フィールドのエンリッチ (Enrich fields)」**の 3 つのタブがあります。

   - **「フィールドの識別 (Identify fields)」**には、SDU エディターが含まれています。このタブは、元の {{site.data.keyword.discoveryshort}} 画面にある**「変換」**と**「正規化」**の両方のタブに代わるものです。 
   - **「フィールドの管理 (Manage fields)」**には、すべての索引作成フィールドがリストされます (すべてのフィールドにはデフォルトで索引が作成されます)。索引を作成しないフィールドはすべてオフに切り替えてください。例えば、PDF には有用な情報を含まない連続したヘッダーまたはフッターが含まれている可能性があるため、これらのフィールドは索引から除外することができます。ここでフィールドに基づいて文書を分割することもできます。[文書の分割](/docs/services/discovery?topic=discovery-sdu#splitting)を参照してください。
   - **「フィールドのエンリッチ (Enrich fields)」**は、元の画面の**「エンリッチ (Enrich)」**タブと同じです。 エンリッチメントについて詳しくは、[エンリッチメントの追加](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)を参照してください。 **「サンプル文書のアップロード (Upload sample documents)」**オプションは、SDU コレクションでは使用できません。

   まだ文書をアップロードしていない場合は、左上のコレクションの名前をクリックして**「概要」**画面に戻るか、![データの管理 (Manage Data)](/images/icon_yourData.png) アイコンをクリックしてコレクションを選択します。文書をコレクションにドラッグ・アンド・ドロップするか、**「コンピューターから参照 (browse from computer)」**をクリックします。初期アップロードが完了した後、**「文書のアップロード (Upload documents)」**ボタンが右上に表示されます。
   {: important}

   Smart Document Understanding を使用する場合は、`text` フィールドのみをエンリッチできます。それ以外のフィールドはエンリッチしないでください。
   {: important}

1. **「フィールドの識別 (Identify fields)」**タブを開きます。コレクションから最大 20 個の文書が Smart Document Understanding エディターに自動的にロードされます。

上部のツールバーでは、以下を行うことができます。
- 注釈を付ける文書の選択
- 表示された文書のナビゲート
- ページの表示の調整 (`単一ページ表示`、`ズームイン`、`ズームアウト`)、`変更のクリア`、および`モデルのエクスポート/インポート`。 `単一ページ表示`をクリックすると、表示を切り替えられます。注釈と文書を別々に表示することも、一緒に表示することもできます。

{{site.data.keyword.discoveryshort}} ツールを使用して、Box、Salesforce、Microsoft SharePoint Online、IBM Cloud オブジェクト・ストレージ、Microsoft SharePoint 2016 のデータ・ソースをクロールしたり、Web クロールを実行したりすることもできます。**「データ・ソースの接続 (Connect a data source)」**ボタンをクリックします。詳しくは[データ・ソースへの接続](/docs/services/discovery?topic=discovery-sources#sources)を参照してください。 この方法でコレクションを作成した場合、エンリッチメントは自動的には適用されません。
{: tip}

## 文書に注釈を付ける方法
{: #documents}

**注:** 表は、別のステップで注釈が付けられます。

注釈付けを開始する前に、[文書および表に注釈を付けるためのベスト・プラクティス](/docs/services/discovery?topic=discovery-sdu#bestpractices)を参照してください。

1. デフォルトのフィールド・セットが文書の右側に表示されます。 使用可能なフィールドは、`answer`、`author`、`footer`、`header`、`question`、`subtitle`、`table_of_contents`、`text`、および `title` です。 新しいカスタム・フィールドのラベルを 1 つ以上作成する場合は、**「新規作成」**をクリックします。作成可能なカスタム・ラベルの数は、ライト・プランの場合は `0`、拡張プランの場合は `5`、プレミアム・プランの場合は `20` に制限されます。
1. 右側のフィールド・ラベルをクリックしてアクティブにします。
1. SDU エディター内でそのフィールドを表すコンテンツをクリックします。 そこが強調表示されます。 
   - あるいは、右側のフィールド・ラベルを選択し、SDU エディターのコンテンツにドラッグすることもできます。 
   - 変更をクリアするには、ツールバーの**「変更のクリア」**ボタンをクリックします。
1. **「送信」**をクリックします。
   **注:** ユーザーが注釈を付けることで、Watson は学習を行い、注釈の予測を開始します。 Watson が正しく、一貫してフィールドを識別するまで、注釈付けを続行してください。
1. 注釈付けが完了したら、**「変更をコレクションに適用 (Apply changes to collection)」**をクリックします。 **「文書のアップロード (Upload your documents)」**画面が開きます。 コレクションにドキュメントを再アップロードします。アップロードが完了すると、**「データの管理 (Manage Data)」**画面にリダイレクトされます。

フィールド | 定義  
------ | ------ 
answer | Q/A ペアにおける (FAQ の場合も多い)、質問に対する答え。
author | 作成者の名前。
footer | このタグを使用して、ページの下部に表示される、文書に関するメタ情報 (ページ番号や参照など) を示します。
header | このタグを使用して、ページの上部に表示される、文書に関するメタ情報を示します。
question | Q/A ペアにおける (FAQ の場合も多い)、質問。
subtitle | 注釈を付けられる文書の 2 次的なタイトル。 
table_of_contents | このタグは、文書の目次のリストで使用します。
text | このタグは、標準のコピー・テキスト (底本) に使用します。これには、パラグラフや定義が含まれるほか、タイトル、表の一部、答え、作成者、サブタイトル、ヘッダー、およびフッターのいずれでもない単語のセットが含まれます。 
title | 注釈を付けられる文書のメイン・タイトル。

## 表に注釈を付ける方法
{: #tables}

表の注釈付けはベータ版です。ベータ版フィーチャーの説明については、[ここ](/docs/services/discovery?topic=discovery-release-notes#beta-features)を参照してください。
{: important}

注釈付けを開始する前に、[文書および表に注釈を付けるためのベスト・プラクティス](/docs/services/discovery?topic=discovery-sdu#bestpractices)を参照してください。

1. SDU エディターの右側で `table` フィールドを選択してから、文書内の表を選択します。 
1. 表の上にカーソルを移動して、**「表に注釈を付ける (Annotate table)」**ボタンを表示します。 ボタンをクリックして表エディターを開きます。
1. まず、表のアウトラインを作ります。
   - `「列 (column)」`フィールドを選択します。
   - 表内の列をクリックして、列をアクティブにします。
   - `「行 (row)」`フィールドを選択します。
   - 表内の行をクリックして、行をアクティブにします。

   表のアウトラインが、左側の表プレビューに表示されます。

   **注:** ユーザーが表に注釈を付けることで、Watson は学習を行い、注釈の予測を開始します。
1. 次に、表内のコンテンツにラベルを付けます。
1. 表の注釈付けが完了したら、**「注釈付け完了 (Done annotating)」**をクリックします。
1. **「変更をコレクションに適用 (Apply changes to collection)」**をクリックします。 **「文書のアップロード (Upload your documents)」**画面が開きます。 コレクションにドキュメントを再アップロードします。アップロードが完了すると、**「データの管理 (Manage Data)」**画面にリダイレクトされます。

以下のビデオをガイドとして使用してください![table annotation video](images/SDU_table_demo.gif){: gif}

フィールド | 定義  
------ | ------ 
本体 (body) | 情報を含んでいる、ヘッダー以外のセル
列ヘッダー (column header) | 表の各列の見出しセル (存在する場合) 
複数列ヘッダー (multi-column header) | 複数の列にまたがる見出しセル
行のタイトル (row title) | 行見出しの列用の列ヘッダー (存在する場合)
行ヘッダー (row header) | 表の各行の行ラベル (存在する場合)
複数行ヘッダー (multi-row header) | 複数の行にまたがる行ラベル

## 文書の分割
{: #splitting}

**「フィールドの管理 (Manage fields)」**タブには、**「文書を分割して照会結果を改善する (Improve query results by splitting your documents)」**ためのオプションが含まれています。このオプションを使用すると、フィールド名に基づいて文書をセグメントに分割できます。分割すると、セグメントごとに個別の文書になり、エンリッチおよび索引作成も個別に行われ、別々の照会結果として返されるようになります。 

文書は、`title`、`author`、`question` などの単一のフィールド名に基づいて分割されます。 

考慮事項:

  - 文書あたりのセグメント数は `250` に制限されています。 `249` 個のセグメント以降に残っている文書コンテンツは、セグメント `250` に格納されます。

  - 各セグメントは、計画した文書の制限に向けてカウントされます。 {{site.data.keyword.discoveryshort}} は、プランの制限に達するまでセグメントの索引付けを行います。 文書制限については、『[Discovery の料金プラン](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)』を参照してください。

  - PDF および Word のメタデータ、およびすべてのカスタム・メタデータは、抽出され、各セグメントと共に索引に組み込まれます。 文書の各セグメントには、同一のメタデータが含まれます。

  - 分割した文書が更新されたために再アップロードが必要になった場合は、[文書の更新 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery#update-a-document){: new_window} メソッドを使用して置換する必要があります。`/environments/{environment_id}/collections/{collection_id}/documents/{document_id}` API の POST メソッドを使用し、`{document_id}` パス変数としていずれかの現行セグメントの `parent_id` フィールドを指定して、その文書をアップロードする必要があります。 更新版の文書のセクションの総数が元のものより少ない場合を除き、すべてのセグメントが上書きされます。 これらの古いセグメントは索引に残り、API を使用して個別に削除できます。 詳しくは、[API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery#delete-a-document){: new_window} を参照してください) 

## モデルのインポートおよびエクスポート
{: #import}

SDU エディターを使用してモデルを定義したら、それを保存して他のコレクションで再利用することができます。

完成した SDU モデルは、エディター上部のツールバーを使用してインポートまたはエクスポートできます。最後のアイコンをクリックし、`「モデルのインポート」`または`「モデルのエクスポート」`を選択します。

エクスポートされたモデルのファイル拡張子は `.sdumodel` になります。 

インポートされたモデルは、注釈付けを追加せずに使用するためのものです。インポートした後も注釈付けを続けると、モデルは完全に上書きされます。モデルを新しいコレクションにインポートする場合は、ベスト・プラクティスとして、文書を 1 つのみ含む新しいコレクションを作成してモデルをインポートしてから、残りの文書をアップロードすることをお勧めします。

## 文書および表に注釈を付けるためのベスト・プラクティス
{: #bestpractices}

表の注釈付けはベータ版です。ベータ版フィーチャーの説明については、[ここ](/docs/services/discovery?topic=discovery-release-notes#beta-features)を参照してください。
{: important}

- すべてのガイドラインに従い、すべての文書に一貫性のあるラベリングを行う。
- 空白にはラベルを付けない。
- 画像と図には `image` ラベルを使用する。
- **太字**、_イタリック_、または下線付きのテキストの扱いを変えない。 テキストのスタイルではなくコンテキストに基づいてラベルを付けてください。 
- 文書にラベルを付けるときは、最初のページから最後のページまで処理する。
- 項目に誤ってラベルを付けた場合は、その項目に別のラベルを選択して、最初のラベルを上書きする。
- ページはいつでもサブミットできる。 サブミットする前に、適切なラベル付けがすべて完了していることを確認してください。
- 他のテキストをオーバーレイしているテキストがあるような文書や表は、「二重オーバーレイ」と見なされ、注釈を付けることはできない。 これらの文書は管理者に報告してください。
- 単一ページに複数列のテキストを含んでいる文書や表に注釈を付けることはできない。 これらの文書は管理者に報告してください。
- 脚注にラベルを付けるのは、ページ下部の脚注が文書内のテキストの本文で参照されている場合のみにする。
- セクションまたはリスト内に表示される注記 (例えば、明示的な「注記」などのコールアウト) には、`text` としてラベルを付ける。
- 表のラベル付けが正しく行われたかどうかが不明で、プレビュー・ペインが応答しなくなった場合、確実に正しく処理されているようにするには、ブラウザーでページを再ロードし、表の再ラベル付けを行う必要がある。

