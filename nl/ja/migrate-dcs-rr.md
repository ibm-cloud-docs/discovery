---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-03"

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


# Watson の Document Conversion および Retrieve and Rank からのマイグレーション
{: #migrate-dcs-rr}

{{site.data.keyword.documentconversionfull}} および {{site.data.keyword.retrieveandrankfull}} は非推奨となり、{{site.data.keyword.discoveryfull}} に置き換えられています。 通常、これらの 2 つのサービスは、結果の取り込み、ランク付け、およびアプリケーションへの送信を行うために一緒に使用されます。 本資料は、{{site.data.keyword.documentconversionshort}} および {{site.data.keyword.retrieveandrankshort}} から {{site.data.keyword.discoveryshort}} へのマイグレーション・プロセスをご案内するために用意されています。

{{site.data.keyword.discoveryfull}} は、より堅固な照会インターフェース、簡素化されたデータ取り込み、改善されたトレーニング管理、および拡大されたスケールを提供します。 {{site.data.keyword.discoveryshort}} は、サポート・エージェント支援、組織的知識ベース検索、および調査支援など、{{site.data.keyword.retrieveandrankshort}} と同じ多くのコア・ユースケースに対処しています。 {{site.data.keyword.retrieveandrankshort}} のユーザーが直面する多くの困難を念頭に置いて構築されており、それらの多くの問題に対処しています。 また、{{site.data.keyword.discoveryshort}} には、パッセージ取り出しや、より関連性の高い結果を検出するための改善された検索アルゴリズムなど、{{site.data.keyword.retrieveandrankshort}} では使用できなかった情報検索の新規機能も用意されています。

**機能の比較**
{: #features-dcs-rr}

| 機能 | {{site.data.keyword.retrieveandrankshort}} | {{site.data.keyword.discoveryshort}} |
|:-------------|:--------------------:|:-------------:|
| 自然言語検索 | あり | あり |
| 機械学習の関連性トレーニング | あり | あり |
| トレーニング用の UI ツール | あり | あり |
| JSON 回答ユニットの入力 | あり | あり |
| 文書の分割 | あり | あり |
| パッセージ取り出し |   | あり |
| 文書 CRUD | あり | あり |
| JSON のバッチ・アップロード | あり |   |
| 自動の文書 NLP エンリッチメント |   | あり |
| エンリッチメントのためのカスタム NLP モデルの統合 |   | あり |
| サービス内へのトレーニング・データの保管 |   | あり |
| 自動化されたモデル・ライフサイクル管理 |   | あり |
| トレーニングなしで関連性を向上させる、意味の類似性 |   | あり |
| テスト・セットに基づく、ツールでの正確度測定 | あり |   |
| カスタム機能ベクトル・サポート | あり |   |
| カスタム・アナライザー構成 | あり | 事前構成済み |
| カスタム・ストップワード | あり | 事前構成済み |
| カスタム言語辞書 | あり | 事前構成済み |
| カスタム同義語 | あり | あり |
**注:** この表は、{{site.data.keyword.discoveryshort}} の新機能が追加されると更新されます。

マイグレーションのアクションを開始する前に、まず {{site.data.keyword.retrieveandrankshort}} サービスに保管されているデータを[評価](#evaluate)し、現在のソリューションを構成するさまざまなコンポーネントをどのように移動するかを理解する必要があります。

多くのお客様は、{{site.data.keyword.documentconversionshort}} を {{site.data.keyword.retrieveandrankshort}} と併せて使用しています。 {{site.data.keyword.documentconversionshort}} を使用して、コンテンツを検索可能索引に保管できるように変換していない場合は、[スタンドアロンの {{site.data.keyword.documentconversionshort}} をマイグレーションするためのオプション](#dcs)の確認に進んでください。

最初に {{site.data.keyword.retrieveandrankshort}} のチュートリアルを使用し、そのチュートリアルに基づいて独自のサービス・インスタンスを作成した場合は、同じデータを {{site.data.keyword.discoveryshort}} に取り込む、そのチュートリアルの拡張機能が[ここ](/docs/services/discovery?topic=discovery-migrate-rnr#migrate-rnr)にあります。

**注:** 変換とエンリッチメントの機能は、{{site.data.keyword.discoveryshort}} に含まれています。 {{site.data.keyword.documentconversionshort}} と {{site.data.keyword.nlushort}}、またはそのいずれかを使用して、ソースの HTML 文書、PDF 文書、または Microsoft Word 文書を変換およびエンリッチした場合、それらのサービスは、{{site.data.keyword.discoveryshort}} サービス内の機能に置き換えられています。

## Watson Discovery サービスへのマイグレーション・パスの評価
{: #evaluate}

{{site.data.keyword.retrieveandrankshort}} からのマイグレーションには、ソース・コンテンツからのマイグレーションと、索引付きコンテンツからのマイグレーションという 2 つの実用的オプションがあります。 どちらのオプションを使用するか決める前に、両方のオプションを評価してください。

### ソース・コンテンツからのマイグレーション
{: #source}

ソース・コンテンツからマイグレーションするには、以下のことが必要です。

-  コンテンツの取り込み元であった、元のソース・ファイルへのアクセス権を持っている
-  各文書の ID をプログラマチックに抽出する (結果は、索引付けされる前に既に ID を持っています)

マイグレーション基準をすべて満たすことができたら、以下の方法を使用して {{site.data.keyword.discoveryshort}} サービスに移動することをお勧めします。

ソース・コンテンツをマイグレーションするには、[マイグレーション・チュートリアル](/docs/services/discovery?topic=discovery-migrate-rnr#migrate-rnr)で説明されている手順を、ご使用のソース・データの特性を満たすように変更します。

#### 回答ユニットのマイグレーション
{: #answerunit-dcs-rr}

{{site.data.keyword.documentconversionshort}} を使用して回答ユニットを作成した場合は、そのコンテンツをマイグレーションするためのオプションを以下から選択してください。

-  ランカーをトレーニングしており、ランキングのマイグレーションが必要な場合は、{{site.data.keyword.documentconversionshort}} から返されたコンテンツを {{site.data.keyword.discoveryshort}} に取り込む必要があります。
-  マイグレーションするトレーニング・データがない場合は、[文書セグメンテーション機能](/docs/services/discovery?topic=discovery-configservice#doc-segmentation)を使用して、元のソース文書を {{site.data.keyword.discoveryshort}} に取り込みます。

### 索引付きコンテンツからのマイグレーション
{: #indexed}

元のソース文書にアクセスできない場合や以下の場合は、{{site.data.keyword.retrieveandrankshort}} 内の索引付きコンテンツからマイグレーションする必要があります。

- 自動文書 ID 生成を使用し、ランカーをトレーニングした。
- {{site.data.keyword.documentconversionshort}} で回答ユニットを作成してランク付けしたが、{{site.data.keyword.documentconversionshort}} サービスによって生成された回答ユニットを保存しなかった。

**注:** この方法は、すべての必要なコンテンツが、{{site.data.keyword.retrieveandrankshort}} の保管済みフィールド内にある場合のみ可能です。 コンテンツが索引付けされただけで保管されなかった場合は、サービスからコンテンツを照会できないので、再度ソースからデータを変換して分割する必要があります。

文書は、ブランクの照会 `q=*:*` を使用する [/v1/solr_clusters/{solr_cluster_id}/solr/\{collection_name\}/select ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/retrieve-and-rank/api/v1/#index_doc){: new_window} メソッドを使用してサービスから抽出されます。 返される文書の数は、実用的な最大リターン数 (ほとんどのコレクションで `200`) より多くなる可能性があります。 その場合は、適切な [ページング![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://lucene.apache.org/solr/guide/6_6/pagination-of-results.html){: new_window} で複数の呼び出しを行い、すべての文書を収集する必要があります。

指定された **ID** を持つ文書は、[/v1/environments/\{environment_id\}/collections/\{collection_id\}/documents/\{document_id\} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery#update-a-document){: new_window} メソッドを使用して {{site.data.keyword.discoveryshort}} サービスにアップロードされます。 それぞれの文書アップロードは、別々の API 呼び出しです。

## トレーニング・データのマイグレーション
{: #trainingdata-dcs-rr}

結果をマイグレーションしたら、次のステップでは、コンテンツ用に作成されたすべてのトレーニング・データをマイグレーションします。 トレーニング・データのマイグレーションには、ソース (`csv`) からのマイグレーションと、サービスからのマイグレーションという 2 つのオプションがあります。 `csv` ファイルからトレーニング・データをアップロードし、まだそのファイルにアクセスできる場合は、ソースからマイグレーションします。 {{site.data.keyword.retrieveandrankshort}} ツールを使用した場合、または元の `csv` ファイルにアクセスできない場合は、サービスからマイグレーションする必要があります。

### ソース・コンテンツからのトレーニングのマイグレーション
{: #csv}

ランキング・ソース・コンテンツからマイグレーションするには、以下が必要になります。

- 最初にトレーニング情報のアップロードに使用された、元のソースの `csv` ファイルへのアクセス権を持っている。
- 索引付けされる時のトレーニング済み文書の ID が、{{site.data.keyword.retrieveandrankshort}} で索引付けされた時のトレーニング済み文書の ID と一致するようにする。

マイグレーション基準をすべて満たすことができたら、以下の方法を使用してトレーニングを {{site.data.keyword.discoveryshort}} サービスに移動することをお勧めします。

トレーニング・データをマイグレーションするには、[マイグレーション・チュートリアル](/docs/services/discovery?topic=discovery-migrate-rnr#migrate-rnr)に記載されている手順を、ご使用のソース・データの特性を満たすように変更します。

### サービスからのトレーニング・データのマイグレーション
{: #extract-train}

{{site.data.keyword.retrieveandrankshort}} サービスからトレーニング・データをマイグレーションするには、{{site.data.keyword.retrieveandrankshort}} API を使用してトレーニング・データを抽出し、{{site.data.keyword.retrieveandrankshort}} トレーニング JSON を {{site.data.keyword.discoveryshort}} で使用可能なフォーマットに変換し、最後に API を使用してトレーニング・データを {{site.data.keyword.discoveryshort}} に取り込む必要があります。

{{site.data.keyword.retrieveandrankshort}} からトレーニング・データを抽出するには、{{site.data.keyword.retrieveandrankshort}} ツール内の `Export` 機能を使用します。 完全なエクスポートを正常にダウンロードしたら、保存された `.zip` ファイルを抽出します。 アーカイブ・ファイルには 2 つファイルが含まれています。 トレーニング・データは、`export-questions.json` という名前のファイルに保管されています。 このファイルには、JSON トレーニング・オブジェクトの配列が含まれています。

配列内の各トレーニング結果は、以下の形式で表されます。

**サンプルの {{site.data.keyword.retrieveandrankshort}} トレーニング・データ**
```json
{
    "text":"Who was the first royal to attend Wimbledon?",
    "cluster":{
        "id":"f62c11d3-30fa-11e7-8a0c-333f7f431ce8",
        "answers":{
            "f62c11d3-30fa-11e7-8a0c-33":[
                {
                    "id":"dac41335-0e96-40c9-983f-cc3f1c395782",
                    "ranking":1,
                    "source":{
                        "id":"e26a3d20-30fa-11e7-aa5e-d1632b06e0b1",
                        "file":"wimbledon-wikipedia.html",
                        "sequence":17,
                        "strategy":"retrieve"
                    }
                },
                {
                    "id":"661b4c9f-ecdb-4dad-aafc-6ae561a148c0",
                    "ranking":2,
                    "source":{
                        "id":"da1bc620-30fa-11e7-8f90-3305f35a93c9",
                        "file":"generated-otherFactsFigures.docx",
                        "sequence":67,
                        "strategy":"retrieve"
                    }
                },
                {
                    "id":"0053fdb8-c77e-4fcf-b0e0-6a4cd377266a",
                    "ranking":3,
                    "source":{
                        "id":"d9c0add0-30fa-11e7-aa5e-d1632b06e0b1",
                        "file":"generated-allEngland.docx",
                        "sequence":20,
                        "strategy":"retrieve"
                    }
                },
                {
                    "id":"506d3d50-19ed-49c8-b32f-65f848e60e86",
                    "ranking":4,
                    "source":{
                        "id":"da1bc620-30fa-11e7-8f90-3305f35a93c9",
                        "file":"generated-otherFactsFigures.docx",
                        "sequence":63,
                        "strategy":"retrieve"
                    }
                }
            ]
        },
        "flags":{

        }
    }
},
```
{: codeblock}

{{site.data.keyword.discoveryshort}} には、{{site.data.keyword.retrieveandrankshort}} からエクスポートされた一部の情報は必要ありません。 以下のスニペットは、{{site.data.keyword.discoveryshort}} トレーニング項目の、必要な構造を示しています。

```json
{
  "natural_language_query": "{natural_language_query}",
  "examples": [
    {
      "document_id": "{document_id_1}",
      "relevance": 0
    },
    {
      "document_id": "{document_id_2}",
      "relevance": 10
    }
  ]
}
```
{: codeblock}

この時点で、{{site.data.keyword.retrieveandrankshort}} トレーニング情報を {{site.data.keyword.discoveryshort}} トレーニング情報に変換する必要があります。 変換する際は、以下の点を考慮してください。

- **関連性がない (Not relevant)** は、{{site.data.keyword.discoveryshort}} では `relevance` スコア `0` で指定されますが、{{site.data.keyword.retrieveandrankshort}} では `ranking` `1` で指定されます。{{site.data.keyword.discoveryshort}} では、すべての `"ranking": 1` 項目を `"relevance": 0` に変換する必要があります。
- {{site.data.keyword.discoveryshort}} ツールは、バイナリー・スケール `0` と `10` を使用します。 より多くの結果をランク付けしたいと望んでおり、{{site.data.keyword.discoveryshort}} ツールを使用している場合は、すべての `"ranking": 1` 項目と `"ranking": 2` 項目を `"relevance": 0` に変換し、すべての `"ranking": 3` 項目と `"ranking": 4` 項目を `"relevance": 10` に変換する必要があります。 追加の結果をランキングしない場合、または {{site.data.keyword.discoveryshort}} ツールを使用していない場合、この作業は必要ありません。
- 未回答の質問は、{{site.data.keyword.discoveryshort}} には必要ありません。手動で関連性トレーニングの妥当性検査が行われます。

![ランキングのマイグレーションの流れ](images/migrate-ranking.png)

例として、上記リストに記載されている**サンプルの {{site.data.keyword.retrieveandrankshort}} トレーニング・データ**は、{{site.data.keyword.discoveryshort}} ツールで使用するために以下のように変換されます。

```json
{
  "natural_language_query": "Who was the first royal to attend Wimbledon?",
  "examples": [
    {
      "document_id": "e26a3d20-30fa-11e7-aa5e-d1632b06e0b1",
      "relevance": 0
    },
    {
      "document_id": "da1bc620-30fa-11e7-8f90-3305f35a93c9",
      "relevance": 0
    },
    {
      "document_id": "d9c0add0-30fa-11e7-aa5e-d1632b06e0b1",
      "relevance": 10
    },
    {
      "document_id": "da1bc620-30fa-11e7-8f90-3305f35a93c9",
      "relevance": 10
    }
  ]
}
```
{: codeblock}

## 言語サポート
{: #language}

[{{site.data.keyword.discoveryshort}} の言語サポート表](/docs/services/discovery?topic=discovery-language-support#language-support)を参照してください。 {{site.data.keyword.retrieveandrankshort}} の機能は、主として**基本**の {{site.data.keyword.discoveryshort}} 言語サポートによってサポートされています。

## 照会のマイグレーション
{: #queries}

{{site.data.keyword.discoveryfull}} 照会言語は、{{site.data.keyword.retrieveandrankshort}} によって使用される Solr 照会言語と異なります。 既存の照会は、いずれかの {{site.data.keyword.discoveryfull}} 照会メソッドに転送し、{{site.data.keyword.discoveryfull}} 照会言語を使用するよう変換する必要があります。 以下の表では、ほとんどの照会で使用される標準的演算子のいくつかについて説明します。

**Solr 照会から {{site.data.keyword.discoveryshort}} へのマイグレーション - 標準的演算子**

| Solr の演算子 | Discovery の演算子 | 説明 |
|:-------------:|--------------------|-------------|
| `.` | `.` | JSON 区切り文字 |
| `:` | `:` | 含む |
|  | `::` | 完全一致 |
| `-{fieldname}:` | `:!` | 含まない |
|  | `::!` | 完全一致ではない |
| ``\` | ``\` | エスケープ文字 |
| `""` | `""` | 句照会 |
| `()` | `()`, `[]` | ネストされたグループ |
| `OR` | [<code>&#124;</code>] | または |
| `AND` | [,] | および |
| `[* TO 100]` | `<=`, `>=`, `>`, `<` | 数値比較 |
| `^x` | `^x` | スコア乗数 |
| `*` | `*` | ワイルドカード |
| `~`(0 から 1) | [~n] | 文字列変化 |

{{site.data.keyword.discoveryfull}} 照会言語について詳しくは、[照会の概念](/docs/services/discovery?topic=discovery-query-concepts#query-concepts)および[照会リファレンス](/docs/services/discovery?topic=discovery-query-reference#query-reference)の文書を参照してください。


## スタンドアロン Watson Document Conversion サービスのマイグレーション
{: #dcs}

{{site.data.keyword.retrieveandrankshort}} へのコンテンツの取り込みに役立つ {{site.data.keyword.documentconversionshort}} を使用している場合、その機能は単一サービスの {{site.data.keyword.discoveryshort}} に進化しました。 {{site.data.keyword.discoveryshort}} を使用すれば、Microsoft Word、PDF、HTML、および JSON の各文書を、トレーニング可能で検索可能な索引に容易に変換し、強化し、取り込むことができます。 ご使用のユースケースで、変換されたコンテンツの索引への保管が行われない場合、このセクションはお客様に関係があります。 文書を索引に取り込む場合は、[{{site.data.keyword.discoveryshort}} サービスへの取り込み](/docs/services/discovery?topic=discovery-configservice#configservice)を参照してください。

IBM では、Microsoft Word、PDF、および HTML の各文書のスタンドアロン変換用に設計されたサービスはもう提供していません。 現在 {{site.data.keyword.documentconversionshort}} サービスを使用していて、オンラインの索引付きサービス ({{site.data.keyword.discoveryshort}} など) に出力を取り込んでいない場合は、[Apache Tika ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://tika.apache.org/){: new_window} などのオープン・ソースの代替サービスへのマイグレーションを検討することをお勧めします。
