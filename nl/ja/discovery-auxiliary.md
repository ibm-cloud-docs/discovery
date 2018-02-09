---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-31"

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

# Discovery アーカイブ

このトピックには、まだ使用できる場合もあるが新しいオプションに置き換えられた {{site.data.keyword.discoveryshort}} 機能に関する情報が記載されています。
{: tip}

## AlchemyLanguage のエンリッチメント
{: #AlchemyLanguage-enrichments}

**2017 年 7 月 18 日**より、{{site.data.keyword.discoveryfull}} に新しいエンリッチメント・テクノロジー {{site.data.keyword.nlushort}} が導入されました。これらのエンリッチメントは既存のエンリッチメントと同じですが、多少異なる構成とスキーマを必要とします。{{site.data.keyword.alchemylanguageshort}} エンリッチメントという元のエンリッチメントは非推奨になり、**2018 年 1 月 15 日**にサポートが終了します。

`2017-10-16` API バージョン・ストリングでは、{{site.data.keyword.alchemylanguageshort}} でエンリッチされた既存のコレクションに新規文書をアップロードするためのサポートと、新しいコレクションを作成してそれらを {{site.data.keyword.alchemylanguageshort}} エンリッチメントでエンリッチするためのサポートが非推奨になります。**2018 年 1 月 15 日**にサポートが終了するまで {{site.data.keyword.alchemylanguageshort}} の使用を続ける場合は、前の API バージョン・ストリングを使用してください。

AlchemyLanguage でエンリッチされている既存のコレクションは、できるだけ早く Natural Language Understanding エンリッチメントにマイグレーションしてください。{{site.data.keyword.alchemylanguageshort}} エンリッチメントを利用するコレクションと構成ファイルのマイグレーションについては、[{{site.data.keyword.nlushort}} へのエンリッチメントのマイグレーション](/docs/services/discovery/migrate-nlu.html)を参照してください。

**注:** {{site.data.keyword.discoveryshort}} ツールは常に最新の API バージョン・ストリングを使用します。そのため、`2017-10-16` API バージョン・ストリングより、{{site.data.keyword.discoveryshort}} ツールを使用して、既存の {{site.data.keyword.alchemylanguageshort}} コレクションに文書をアップロードすること、および {{site.data.keyword.alchemylanguageshort}} エンリッチメントでエンリッチされた新規コレクションを作成することができなくなります。コレクションのエンリッチに Discovery ツールを引き続き使用する場合は、まず、コレクションを Natural Language Understanding にマイグレーションしてください。詳細については、[{{site.data.keyword.nlushort}} へのエンリッチメントのマイグレーション](/docs/services/discovery/migrate-nlu.html)を参照してください。

### エンティティー抽出 (AlchemyLanguage)
{: #entity-extraction-al}

入力テキスト内に存在する人、場所、組織などの項目を返します。エンティティー抽出では、分析するテキストの主題とコンテキストの理解に役立つように、セマンティック情報をコンテンツに追加します。エンティティー抽出技法は、高度な統計アルゴリズムと自然言語処理テクノロジーに基づき、多言語分析、文脈による曖昧性除去、および引用抽出をサポートする、業界でユニークなものです。

例として、エンティティー抽出でエンリッチされた文書の一部を以下に示します。

```json
{
      "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
      "enriched-text": {
        "status": "OK",
        "language": "english",
        "entities": [
          {
            "type": "City",
            "relevance": 0.532754,
            "sentiment": {
              "type": "positive",
              "score": 0.527541,
              "mixed": false
            },
            "count": 1,
            "text": "Atlanta",
            "disambiguated": {
              "subType": [
                "AdministrativeDivision",
                "GovernmentalJurisdiction",
                "OlympicHostCity",
                "PlaceWithNeighborhoods"
              ],
              "name": "Atlanta",
              "website": "http://www.atlantaga.gov/",
              "dbpedia": "http://dbpedia.org/resource/Atlanta",
              "freebase": "http://rdf.freebase.com/ns/m.013yq"
            }
          }
        ]
      }
    }
```
{: codeblock}
上記の例では、`enriched_text.entities.type` にアクセスすることで、エンティティー・タイプを照会できます。

**センチメント**のエンリッチメントが選択されていなくても、エンティティー・タイプの `sentiment` が算出されます。センチメントのスコアについて詳しくは、[センチメント分析](/docs/services/discovery/discovery-auxiliary.html#sentiment-analysis-al)を参照してください。

`relevance` スコアの範囲は `0.0` から `1.0` です。スコアが高いほど、エンティティーの関連性が高くなります。`disambiguated` フィールドには、エンティティーの曖昧性除去情報が入ります。これには、エンティティーの `subType` 情報とリソースへのリンク (該当がある場合) が含まれます。`count` は、エンティティーが文書内で言及された回数です。

### キーワード抽出 (AlchemyLanguage)
{: #keyword-extraction-al}

データの索引付け、タグ・クラウドの生成、または検索時に通常使用される、コンテンツ内の重要なトピック。{{site.data.keyword.discoveryshort}} サービスは、入力コンテンツでサポート言語を自動的に識別し、そのコンテンツ内のキーワードを識別し、ランク付けします。

例として、キーワード抽出でエンリッチされた文書の一部を以下に示します。

```json
{
    "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched-text": {
        "status": "OK",
        "language": "english",
        "keywords": [
          {
            "relevance": 0.66497,
            "sentiment": {
              "score": 0.527541,
              "type": "positive",
              "mixed": false
            },
            "text": "stockholders"
          }
        ]
      }
    }
```
{: codeblock}

上記の例では、`enriched_text.keywords.text` にアクセスすることで、キーワード・テキストを照会できます。

**センチメント**のエンリッチメントが選択されていなくても、キーワードの `sentiment` が算出されます。センチメントのスコアについて詳しくは、[センチメント分析](/docs/services/discovery/discovery-auxiliary.html#sentiment-analysis-al)を参照してください。

`relevance` スコアの範囲は `0.0` から `1.0` です。スコアが高いほど、キーワードの関連性が高くなります。

### タクソノミー分類 (AlchemyLanguage)
{: #taxonomy-classification-al}

入力テキスト、HTML、または Web ベースのコンテンツを、最大 5 レベルの深さまで階層タクソノミーにカテゴリー化します。より深いレベルを使用して、コンテンツをより正確で役に立つサブセグメントに分類することができます。

例として、タクソノミー分類でエンリッチされた文書の一部を以下に示します。

```json
  {
    "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched-text": {
        "status": "OK",
        "language": "english",
        "taxonomy": [
          {
            "label": "/business and industrial/company/merger and acquisition",
            "score": 0.517533,
            "confident": false
          }
        ]
      }
    }
```
{: codeblock}

上記の例では、`enriched_text.taxonomy.label` にアクセスすることで、タクソノミー・ラベルを照会できます。

`label` は、検出されたタクソノミー・カテゴリーです。階層レベルはスラッシュで区切ります。当該カテゴリーに対する `score` の範囲は `0.0` から `1.0` です。スコアが高いほど、当該カテゴリーの信頼度が高くなります。

### 概念のタグ付け (AlchemyLanguage)
{: #concept-tagging-al}

当該テキスト内にある他の概念およびエンティティーに基づいて、入力テキストが関連する概念を識別します。概念のタグ付けは、概念の関連性を理解し、テキスト内で直接参照されない概念を識別することができます。例えば、記事に CERN (欧州原子核研究機構) とヒッグス粒子が含まれる場合、概念 API 関数は、大型ハドロン衝突型加速器がページに明示的に言及されていなくても、この用語を概念として識別します。概念のタグ付けでは、単なる基本的なキーワード識別より、入力コンテンツを高度に分析できます。

例として、概念のタグ付けでエンリッチされた文書の一部を以下に示します。

```json
{
    "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
        "status": "OK",
        "language": "english",
        "concepts": [
          {
            "text": "Acme Corporation",
            "relevance": 0.91136,
            "dbpedia": "http://dbpedia.org/resource/Acme_Corporation",
            "freebase": "http://rdf.freebase.com/ns/m.0dndy",
            "yago": "http://yago-knowledge.org/resource/Acme_Corporation"
          }
        ]
      }
    }
```
{: codeblock}

上記の例では、`enriched_text.concepts.text` にアクセスすることで、概念テキスト・タイプを照会できます。

`relevance` スコアの範囲は `0.0` から `1.0` です。スコアが高いほど、概念の関連性が高くなります。該当がある場合は、リソースへのリンクも提供されます。

### 関係抽出 (AlchemyLanguage)
{: #relation-extraction-al}

入力コンテンツの文内の主語、動作、目的語の関係を識別します。関係情報は、購買シグナル、キー・イベント、およびその他の重要なアクションを自動的に識別するために使用できます。

例として、関係抽出でエンリッチされた文書の一部を以下に示します。

```json
{
      "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
      "enriched-text": {
        "status": "OK",
        "language": "english",
        "relations": [
          {
            "sentence": " The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, GA.",
            "subject": {
              "text": "The stockholders",
              "keywords": [
                {
                  "text": "stockholders"
                }
              ]
            },
            "action": {
              "text": "were",
              "lemmatized": "be",
              "verb": {
              "text": "be",
              "tense": "past"
            }
            },
            "object": {
              "text": "pleased that Acme Corporation plans to build a new factory in Atlanta, GA",
              "sentiment": {
                "type": "positive",
                "score": 0.834516,
                "mixed": false
              },
              "entities": [
                {
                  "type": "Company",
                  "text": "Acme Corporation"
                },
                {
                  "type": "City",
                  "text": "Atlanta",
                  "disambiguated": {
                    "subType": [
                      "AdministrativeDivision",
                      "GovernmentalJurisdiction",
                      "OlympicHostCity",
                      "PlaceWithNeighborhoods"
                    ],
                    "name": "Atlanta",
                    "website": "http://www.atlantaga.gov/",
                    "dbpedia": "http://dbpedia.org/resource/Atlanta",
                    "freebase": "http://rdf.freebase.com/ns/m.013yq"
                  }
                },
                {
                  "type": "StateOrCounty",
                  "text": "GA"
                }
              ],
              "keywords": [
                {
                  "text": "Acme Corporation"
                },
                {
                  "text": "new factory"
                },
                {
                  "text": "GA"
                },
                {
                "text": "Atlanta"
                }
              ]
            }
          }
        ]
      }
    }
```
{: codeblock}

上記の例では、`enriched_text.relations.subject.text` にアクセスすることで、関係の主語のテキストを照会できます。

**センチメント**のエンリッチメントが選択されていなくても、関係の `sentiment` が算出されます。センチメントのスコアについて詳しくは、[センチメント分析](/docs/services/discovery/discovery-auxiliary.html#sentiment-analysis-al)を参照してください。**エンティティー**と**キーワード**のエンリッチメントも選択していなければ、(例に示したような) `entities` および `keywords` は抽出されません。これらのエンリッチメントについて詳しくは、[エンティティー抽出](/docs/services/discovery/discovery-auxiliary.html#entity-extraction-al)と[キーワード抽出](/docs/services/discovery/discovery-auxiliary.html#keyword-extraction-al)を参照してください。

関係を含むすべての文について、`subject`、`action`、および `object` が抽出されます。

### センチメント分析 (AlchemyLanguage)
{: #sentiment-analysis-al}

分析するコンテンツ内の姿勢、意見、または気持ちを識別します。{{site.data.keyword.discoveryshort}} サービスでは、文書内の全体的なセンチメント、ユーザー指定ターゲットのセンチメント、エンティティー・レベルのセンチメント、引用レベルのセンチメント、方向性レベルのセンチメント、およびキーワード・レベルのセンチメントを計算できます。これらの機能を組み合わせて、ソーシャル・メディアのモニターからトレンド分析まで、さまざまなユース・ケースをサポートします。

例として、センチメント分析でエンリッチされた文書の一部を以下に示します。

```json
{
      "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
      "enriched_text": {
        "status": "OK",
        "language": "english",
        "docSentiment": {
          "type": "positive",
          "score": 0.0966252,
          "mixed": true
        }
      }
    }
```
{: codeblock}

上記の例では、`enriched_text.docSentiment.type` にアクセスすることで、docSentiment タイプを照会できます。

`type` は文書に対する全般的なセンチメント (`positive`、`negative`、または `neutral`) です。センチメントの `type` は、`score` に基づきます。スコアが `0.0` の場合は、文書が中立的 (`neutral`) であること、正数の場合は肯定的 (`positive`) であること、負数の場合は否定的 (`negative`) であることをそれぞれ示します。`mixed` が `true` の場合は、肯定と否定の両方のセンチメントが文書に含まれることを示します (このフィールドは `score` によって決まるものではありません)。

### 感情分析 (AlchemyLanguage)
{: #emotion-analysis-al}

英語のテキスト内に暗示された怒り、嫌悪、不安、喜び、悲しみを検出します。感情分析では、対象の句、エンティティー、またはキーワードに関連する感情を検出することや、コンテンツの全体的な感情のトーンを分析することができます。

例として、感情分析でエンリッチされた文書の一部を以下に示します。

```json
{
      "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
      "enriched_text": {
        "status": "OK",
        "language": "english",
        "docEmotions": {
          "anger": "0.077394",
          "disgust": "0.044024",
          "fear": "0.092664",
          "joy": "0.553327",
          "sadness": "0.3969"
        }
      }
    }
```
{: codeblock}

上記の例では、`enriched_text.docEmotions.joy` にアクセスすることで、`joy` の docEmotion を照会できます。

感情分析ではテキストを分析し、`0.0` から `1.0` までの尺度で各感情 (怒り、嫌悪、不安、喜び、悲しみ) のスコアを計算します。感情のスコアが `0.5` 以上であると、その感情が検出されます (スコアが `0.5` を超えて高いほど、関連性が高くなります)。示されているスニペットでは、`joy` のスコアが 0.5 を超えるため、{{site.data.keyword.watson}} は喜びを検出しました。


## Watson Discovery News Original

{{site.data.keyword.discoverynewsfull}} の新しいバージョンが **2017 年 7 月 31 日**に公開されました。{{site.data.keyword.discoverynewsfull}} Original は、**2018 年 1 月 15 日**のサービスからの削除によって廃止されました。この新しいバージョンについては、[Watson Discovery News](watson-discovery-news.html) を参照してください。

{{site.data.keyword.discoverynewsfull}} Original は、継続的に更新される主に英語のニュース・ソースのデータ・セットであり、約 300,000 の新規記事およびブログが毎日追加されています。この索引付きデータ・セットは、**キーワード抽出**、**エンティティー抽出**、**概念のタグ付け**、**関係抽出**、**センチメント分析**、および**タクソノミー分類**の {{site.data.keyword.alchemylanguageshort}} エンリッチメントで事前にエンリッチされています。また、クロール日、公開日、URL ランキング、ホスト・ランク、アンカー・テキストのメタデータも追加されます。過去 60 日間のニュース・データの履歴検索が可能です。

{{site.data.keyword.discoverynewsfull}} Original は、{{site.data.keyword.alchemylanguageshort}} エンリッチメントでエンリッチされます。これらのエンリッチメントについて詳しくは、[{{site.data.keyword.alchemylanguageshort}} のエンリッチメント](discovery-auxiliary.html#AlchemyLanguage-enrichments)を参照してください。

### Watson Discovery News Original の照会

{{site.data.keyword.discoverynewsfull}} の新しいバージョンが **2017 年 7 月 31 日**に公開されました。{{site.data.keyword.discoverynewsfull}} Original は、**2018 年 1 月 15 日**のサービスからの削除によって廃止されました。この新しいバージョンについては、[Watson Discovery News](watson-discovery-news.html) を参照してください。

**注:** Watson Discovery News 照会で返される結果の最大数は `50` です。`50` 件を超える結果を戻すには、追加の照会と `offset` パラメーターを使用します。

{{site.data.keyword.discoverynewsfull}} Original で使用される JSON スキーマは、プライベート・コレクションに使用されるものと似ていますが、少し異なります。照会に `enriched_text` を含める必要はありません。以下に例を示します。

**{{site.data.keyword.discoverynewsfull}} Original の照会の構成方法**

![Watson Discovery News Original の照会構造の例](images/news_query_structure.png)

以下の照会例では、Pittsburgh Steelers に関して肯定的なセンチメントを含む、{{site.data.keyword.discoverynewsfull}} Original の上位 10 件の記事を戻します。

1.  **「データの管理 (Manage data)」**画面で、{{site.data.keyword.discoverynewsfull}} コレクションを選択します。
1.  **「データ・スキーマの表示 (View data schema)」**をクリックし、**「照会の作成 (Build queries)」**をクリックします。
1.  **「文書の検索 (Search for documents)」**の下で**「{{site.data.keyword.discoveryshort}} 照会言語の使用 (Use the {{site.data.keyword.discoveryshort}} Query Language)」**をクリックし、**「ここに照会を入力 (Enter query here)」**フィールドに `text:Pittsburgh Steelers, docSentiment.type:positive` と入力します。
1.  **「詳細オプション (More options)」**をクリックし、`「戻す文書の数 (Number of documents to return)」`フィールドに `10` (これがデフォルト) と入力します。
1.  **「照会の実行 (Run query)」**をクリックします。Pittsburgh Steelers に関して肯定的なセンチメントを含む上位 10 件の記事が表示されます。

**{{site.data.keyword.discoverynewsfull}} Original のその他の照会例**

-  `concepts.text:"Health care"` - **「文書の検索 (Search for documents)」**の下で**「{{site.data.keyword.discoveryshort}} 照会言語の使用 (Use the {{site.data.keyword.discoveryshort}} Query Language)」**をクリックし、この照会を入力します。`health care` の概念を含むすべての記事が戻されます。**「戻す文書の数 (Number of documents to return)」**フィールドに 50 などの数を指定すると、関連性で上位 50 件の記事だけを受け取ります。

**{{site.data.keyword.discoverynewsfull}} Original の集約の構成方法**

![Watson Discovery News Original 集約照会構造の例](images/news_aggregation_structure.png)

以下の集約の例では、{{site.data.keyword.discoverynewsfull}} Original で Pittsburgh Steelers に関して検出された記事数をセンチメント別に戻します。

1.  **「データの管理 (Manage data)」**画面で、{{site.data.keyword.discoverynewsfull}} Original コレクションを選択します。
1.  **「データ・スキーマの表示 (View data schema)」**をクリックし、**「照会の作成 (Build queries)」**をクリックします。
1.  **「結果の分析を含める (Include analysis of your results)」**の下で、**「{{site.data.keyword.discoveryshort}} 照会言語を使用して集約照会を作成 (Write an aggregation query using the {{site.data.keyword.discoveryshort}} Query Language)」**フィールドに `filter(text:"Pittsburgh Steelers").term(docSentiment.type,count:3)` と入力します。
1.  **「詳細オプション (More options)」**をクリックし、**「戻す文書の数 (Number of documents to return)」**フィールドに `0` と入力します。
1.  **「照会の実行 (Run query)」**をクリックします。結果には、Pittsburgh Steelers に関する文書の数と、それらの中で、`positive`、`negative`、または `neutral` の docSentiment を含む結果の数が表示されます。

**{{site.data.keyword.discoverynewsfull}} Original のその他の集約例**

-  `filter(entities.text:twitter).term(docSentiment.type,count:3)` - **「{{site.data.keyword.discoveryshort}} 照会言語を使用して集約照会を作成 (Write an aggregation query using the {{site.data.keyword.discoveryshort}} Query Language)」**フィールドにこの集約照会を入力すると、まず、記事の集合を絞り込んで (フィルタリングして) Twitter のエンティティー・テキストを含む記事のみにし、その後、文書センチメント・タイプ別に記事を分けます。上位 3 つの文書センチメント・タイプ (`positive`、`negative`、`neutral`) のみが戻されます。

集約照会の前に `nested` を追加すると、指定された結果の領域に限定して集約します。例えば、`nested(text.entities)` では、すべての結果の `text.entities` コンポーネントのみを対象にして集約します。この影響は、次の 2 つの照会の違いを見ると、よく分かります。`filter(text.entities.type::City)` の場合は、type が `City` である 1 つ以上の `entity` を含む*結果* の数が集約でカウントされます。`nested(text.entities).filter(text.entities.type::City)` の場合は、結果の中で type が `City` の `entity` のインスタンス数が集約でカウントされます。また、操作を後ろに指定すると、集約対象の結果セットがさらに限定されます。例えば、`nested(text.entities).filter(text.entities.type::City)` では、`type::City` のエンティティーのみが集約されます。例えば、`nested(text.entities).filter(text.entities.type::City).term(text.entities.text,count:3)` の場合、type が `City` の上位 3 つのエンティティーを集約します。一方、`filter(text.entities.type::City).term(text.entities.text,count:3)` の場合、type が `City` の 1 つ以上のエンティティーが結果に含まれる上位 3 つのエンティティーを戻します。

**注**: {{site.data.keyword.discoverynewsfull}} Original で、構成の調整、トレーニング、コレクションへの文書の追加はできません。

## AlchemyLanguage エンリッチメントを使用した Watson Knowledge Studio との統合

{{site.data.keyword.knowledgestudiofull}} のカスタム・モデルを {{site.data.keyword.discoveryshort}} サービスと統合して、カスタム・エンリッチメントを提供することができます。
{: shortdesc}

### 始めに

{{site.data.keyword.knowledgestudioshort}} のカスタム・モデルを {{site.data.keyword.discoveryshort}} サービスと統合するには、その前に、{{site.data.keyword.knowledgestudioshort}} を使用してそのモデルを作成してデプロイしておく必要があります。モデルの作成とデプロイについては、{{site.data.keyword.knowledgestudioshort}} の資料を参照してください。デプロイされたモデルを {{site.data.keyword.discoveryshort}} サービスと統合するには、そのモデルの固有 ID が必要です。

### このタスクについて

{{site.data.keyword.knowledgestudioshort}} で開発されたカスタム・モデルを使用して、{{site.data.keyword.discoveryshort}} サービスで文書をエンリッチできます。これにより、業界や科学的専門分野など、特定のフォーカス領域に固有の情報を使用して、{{site.data.keyword.discoveryshort}} サービスの文書拡張機能を柔軟に適用することができます。エンリッチメント・モデルでは、公開データとユーザーが所有するデータの両方を使用できます。

{{site.data.keyword.knowledgestudioshort}} モデルを {{site.data.keyword.discoveryshort}} サービスと統合するには、サービス API を使用する必要があります。{{site.data.keyword.discoveryshort}} ツールを使用してカスタム・モデルを統合することはできません。

### 手順

1.  [List environments ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_environments){: new_window} に説明されている方法で、{{site.data.keyword.discoveryshort}} 環境の ID を入手します。その環境 ID を書き留めます。
1.  [List configurations ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_configurations){: new_window} に説明されている方法で、1 つ以上の {{site.data.keyword.discoveryshort}} 現行構成の ID をリストします。{{site.data.keyword.knowledgestudiofull}} カスタム・モデルと統合する構成の ID を書き留めます。
1.  bash シェルまたは同等のもの (Windows 用の Cygwin など) で以下のコマンドを実行して、{{site.data.keyword.discoveryshort}} 現行構成のコピーをダウンロードします。`{environment_id}` と `{configuration_id}` は、前の 2 つのステップで書き留めた ID に置き換えてください。

    ```bash
    curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-09-01" > my_config.json
    ```
    {: pre}

        このコマンドでは、コレクション・ファイルの内容をリストして、それらを JSON ファイル `my_config.json` に入れます。
1.  テキスト・エディターで `my_config.json` ファイルを開き、以下の変更を行います。
    1.  `"name"` フィールドの値を新しい構成の目的を示す値に変更します。オプションで、`"description"` フィールドの値も変更できます。

        ```json
        ...
        "name": "wks-config",
        "description": "This is a configuration to use with a WKS model",
        ...
        ```
        {: codeblock}

    1.  {{site.data.keyword.knowledgestudioshort}} モデルの情報を使用して、エンリッチメント・フィールドを更新します。当初、エンリッチメント・フィールドが以下のとおりであったとします。

        ```json
        "enrichments": [
          {
            "destination_field": "enriched_text",
            "source_field": "text",
            "enrichment": "alchemy_language",
            "options": {
              "extract": "keyword, entity, doc-sentiment, taxonomy, concept, relation",
              "sentiment": true,
              "quotations": true
            }
          }
        ]
        ```
        {: codeblock}

    1.  `{watson_knowledge_studio_model_ID}` を「始めに」で説明した {{site.data.keyword.knowledgestudioshort}} モデルの固有 ID に置き換え、ファイルを次のように更新します。

        ```json
        "enrichments": [
          {
            "destination_field": "enriched_text",
            "source_field": "text",
            "enrichment": "alchemy_language",
            "options": {
              "extract": "keyword, entity, doc-sentiment, taxonomy, concept, relation, typed-rels",
              "sentiment": true,
              "quotations": true,
              "model": "{watson_knowledge_studio_model_ID}"
            }
          }
        ]
        ```
        {: codeblock}

1.  オプションで、[エンティティーを正規化するカスタム構成の作成](/docs/services/discovery/normalize-entities.html)に説明されているように、エンティティーの正規化を有効にします。
1.  `my_config.json` ファイルを保存します。
1.  次のステップを実行する前に、[JSLint ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://jslint.com){: new_window} などの JSON バリデーターを使用して、編集した JSON を検証し、必要であれば修正します。
1.  以下のようにして構成を更新します。この手順の最初に収集した `{environment_id}` と `{configuration_id}` の ID が再び必要になります。

    ```bash
    curl -X PUT -u "{username}":"{password}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-09-01"
    ```
    {: pre}

    このコマンドは、更新された構成ファイルの内容を戻します。
1.  通常は {{site.data.keyword.discoveryshort}} サービスを使用します。更新された構成を使用して取り込んだ文書は、カスタム・モデルのデータによって自動的にエンリッチされます。

## AlchemyLanguage エンティティーを正規化するカスタム構成の作成
{: #normalizing-entities}

照会の出力に*正規化されたエンティティー* (*正規名* とも呼ばれる) を組み込むように {{site.data.keyword.discoveryshort}} サービスを構成することができます。
{: shortdesc}

**注:** 正規化されたエンティティーを使用可能にするための構成の編集は、テキスト・エディターおよび API 呼び出しを使用して実行する必要がある手動タスクです。これは現在、ツールではサポートされていません。

**注:** エンティティーの正規化は、[{{site.data.keyword.knowledgestudiofull}} との統合](/docs/services/discovery/integrate-wks.html)で説明されているように、Watson Knowledge Studio で生成されたカスタム・モデルで Discovery サービスを使用する場合にのみ利用可能です。

エンティティーの正規化では、ソース文書内の同じ人またはオブジェクトに対するさまざまな参照に対して、正規化された名前 (正規名) を挿入します。例えば、エンティティーの正規化を有効にして、「J.R. Cash」と「John R. Cash」が出現する 1 つ以上の文書を取り込むと、処理後の出力には、それぞれの一致した表現とともに `canonical_name` "Johnny Cash" が組み込まれます。また、文書内で検出された他のテキスト・エンティティーの関連する正規名も組み込まれます。出力例については、このセクションの末尾を参照してください。

正規名で文書をエンリッチすると、同じ正規名を持つ特定の項目をより簡単に検索できます。

正規名は、パブリック・ディクショナリーから導出されます。ディクショナリーに適切な正規名が見つからない場合、サービスは、文書内で最も適切なエンティティー参照を正規名として使用します。エンティティーを正規化した文書で正規名を照会する場合は、その前に、エンリッチした JSON 文書を調べて、サービスが生成した正規名が、予期した名前に一致することを確認してください。

### 手順

1.  [List environments ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_environments){: new_window} に説明されている方法で、{{site.data.keyword.discoveryshort}} 環境の ID を入手します。その環境 ID を書き留めます。
1.  [List configurations ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_configurations){: new_window} に説明されている方法で、1 つ以上の {{site.data.keyword.discoveryshort}} 現行構成の ID をリストします。更新する構成の ID を書き留めます。
1.  bash シェルまたは同等のもの (Windows 用の Cygwin など) で以下のコマンドを実行して、{{site.data.keyword.discoveryshort}} 現行構成のコピーをダウンロードします。`{environment_id}` と `{configuration_id}` は、前の 2 つのステップで書き留めた ID に置き換えてください。

    ```bash
    curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-09-01" > new_config.json
    ```
    {: pre}

    このコマンドでは、コレクション・ファイルの内容をリストして、それらを JSON ファイル `new_config.json` に入れます。

1.  テキスト・エディターで `new_config.json` ファイルを開き、以下の変更を行います。
    1. `"name"` フィールドの値を新しい構成の目的を示す値に変更します。オプションで、`"description"` フィールドの値も変更できます。

       ```json
        ...
        "name": "normalize-entities-config",
        "description": "This configuration enables entity normalization",
        ...
       ```
       {: codeblock}

    1. {{site.data.keyword.knowledgestudioshort}} モデルの情報を使用して、エンリッチメント・フィールドを更新します。当初、エンリッチメント・フィールドが以下のとおりであったとします。

       ```json
       "enrichments": [
         {
           "destination_field": "enriched_text",
           "source_field": "text",
           "enrichment": "alchemy_language",
           "options": {
             "extract": "keyword, entity, doc-sentiment, taxonomy, concept, relation, typed-rels",
             "sentiment": true,
             "quotations": true,
             "model": "{watson_knowledge_studio_model_ID}"
           }
         }
       ]
       ```
       {: codeblock}

    1. 以下のようにファイルを更新します。

       ```json
       "enrichments": [
         {
           "destination_field": "enriched_text",
           "source_field": "text",
           "enrichment": "alchemy_language",
           "options": {
             "extract": "keyword, entity, doc-sentiment, taxonomy, concept, relation, typed-rels",
             "sentiment": true,
             "quotations": true,
             "model": "{watson_knowledge_studio_model_ID}"
             "normalizeEntities": 1
           }
         }
       ]
       ```
       {: codeblock}

    1. `new_config.json` ファイルを保存します。

1.  次のステップを実行する前に、[JSLint ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://jslint.com){: new_window} などの JSON バリデーターを使用して、編集した JSON を検証します。

1.  以下のようにして構成を更新します。この手順の最初に収集した `{environment_id}` と `{configuration_id}` の ID が再び必要になります。

    ```bash
    curl -X PUT -u "{username}":"{password}" -H "Content-Type: application/json" -F configuration-@new_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-09-01"
    ```
    {: pre}

    このコマンドは、更新された構成ファイルの内容を戻します。

1.  通常は {{site.data.keyword.discoveryshort}} サービスを使用します。更新された構成を使用して取り込んだ文書は、以下の出力の抜粋に示されているように、正規化されたエンティティーで自動的にエンリッチされます。

### 出力例

`"normalizeEntities": 1` を**指定しない場合**の出力の断片:

```json
{
  "enriched_text": {
  ...
  ...
  ...
    "entity_relations": {
      "entities": {
        "entity": [
          {
            "class": "SPC",
            "eid": "-E0",
            "generic": false,
            "level": "NAM",
            "mentref": [
              {
                "mid": "-M0",
                "text": "J.R. Cash"
              },
              {
                "mid": "-M6",
                "text": "musician"
              },
              {
                "mid": "-M7",
                "text": "who"
              },
              {
                "mid": "-M13",
                "text": "He"
              },
              {
                "mid": "-M20",
                "text": "He"
              }
            ],
            "score": 0.7874817061794613,
            "subtype": "OTHER",
            "type": "PERSON"
          },
        ...
        ...
        ...
        ]
      },
      "relations": {
        "relation": [
          {
            "rel_entity_arg": [
              {
                "argnum": 1,
                "eid": "-E0"
              },
              {
                "argnum": 2,
                "eid": "-E1"
              }
            ],
            "relmentions": {
              "relmention": [
                {
                  "class": "SPECIFIC",
                  "modality": "ASSERTED",
                  "rel_mention_arg": [
                    {
                      "argnum": 1,
                      "mid": "-M0",
                      "text": "John R. Cash",
                    },
                    {
                      "argnum": 2,
                      "mid": "-M1",
                      "text": "country"
                    }
                  ],
                  "rmid": "-R1-1",
                  "score": 0.49918343781296,
                  "tense": "UNSPECIFIED"
                }
              ]
            },
            "rid": "-R1",
            "subtype": "OTHER",
            "type": "knownAs"
          },
          ...
          ...
          ...
        ]
      }
    }
  }
}
```
{: codeblock}

`"normalizeEntities": 1` を**指定した場合**の出力の断片:

```json
{
  "enriched_text": {
  ...
  ...
  ...
    "entity_relations": {
      "entities": {
        "entity": [
          {
            "class": "SPC",
            "eid": "-E0",
            "generic": false,
            "level": "NAM",
            "mentref": [
              {
                "mid": "-M0",
                "text": "J.R. Cash"
              },
              {
                "mid": "-M6",
                "text": "musician"
              },
              {
                "mid": "-M7",
                "text": "who"
              },
              {
                "mid": "-M13",
                "text": "He"
              },
              {
                "mid": "-M20",
                "text": "He"
              }
            ],
            "score": 0.7874817061794613,
            "subtype": "OTHER",
            "type": "PERSON",
            "canonical_name": "Johnny Cash"
          },
        ...
        ...
        ...
        ]
      },
      "relations": {
        "relation": [
          {
            "rel_entity_arg": [
              {
                "argnum": 1,
                "eid": "-E0"
              },
              {
                "argnum": 2,
                "eid": "-E1"
              }
            ],
            "relmentions": {
              "relmention": [
                {
                  "class": "SPECIFIC",
                  "modality": "ASSERTED",
                  "rel_mention_arg": [
                    {
                      "argnum": 1,
                      "mid": "-M0",
                      "text": "John R. Cash",
                      "canonical_name": "Johnny Cash"
                    },
                    {
                      "argnum": 2,
                      "mid": "-M1",
                      "text": "country",
                      "canonical_name": "country music"
                    }
                  ],
                  "rmid": "-R1-1",
                  "score": 0.49918343781296,
                  "tense": "UNSPECIFIED"
                }
              ]
            },
            "rid": "-R1",
            "subtype": "OTHER",
            "type": "knownAs"
          },
          ...
          ...
          ...
        ]
      }
    }
  }
}
```
{: codeblock}
