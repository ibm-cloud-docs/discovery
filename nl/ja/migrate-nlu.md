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

# Natural Language Understanding へのエンリッチメントのマイグレーション

**2017 年 7 月 18 日**以降、{{site.data.keyword.nlushort}} (NLU) という名前の新しいエンリッチメント・テクノロジーが {{site.data.keyword.discoveryfull}} に導入されました。これらのエンリッチメントは既存のエンリッチメントと同じですが、多少異なる構成とスキーマを必要とします。{{site.data.keyword.alchemylanguageshort}} エンリッチメントという名前の、元のエンリッチメントは非推奨になります。
{: shortdesc}

{{site.data.keyword.alchemylanguageshort}} エンリッチメントのサポートは、**2018 年 1 月 15 日**に終了します。`2017-10-16` API バージョン・ストリングは、{{site.data.keyword.alchemylanguageshort}} によってエンリッチされた既存コレクションへの新規文書のアップロードのサポート、および新規コレクションを作成し、それらを {{site.data.keyword.alchemylanguageshort}} エンリッチメントによってエンリッチするためのサポートを廃止しました。**2018 年 1 月 15 日**にサポートが終了するまで {{site.data.keyword.alchemylanguageshort}} の使用を続ける場合は、前の API バージョン・ストリングを使用してください。

新規コレクションは {{site.data.keyword.nlushort}} によってエンリッチする必要があり、{{site.data.keyword.alchemylanguageshort}} 構成ファイルを持つ既存のコレクションは、できるだけ速やかにマイグレーションする必要があります。{{site.data.keyword.alchemylanguageshort}} エンリッチメントの取り込みのサポートは、**2018 年 1 月 15 日**に終了します。{{site.data.keyword.alchemylanguageshort}} エンリッチメントを使用するコレクションおよび構成ファイルのマイグレーションについては、[エンリッチメントの比較](/docs/services/discovery/migrate-nlu.html#enrichment-comparison)を参照してください。

**注:** {{site.data.keyword.knowledgestudioshort}} との統合については、[{{site.data.keyword.knowledgestudiofull}} との統合](/docs/services/discovery/integrate-wks.html)を参照してください。

## エンリッチメントの比較
{: #enrichment-comparison}

{{site.data.keyword.alchemylanguageshort}} および {{site.data.keyword.nlushort}} で使用可能な 7 つのエンリッチメント、およびそれらの JSON オブジェクト名を以下に示します。

| {{site.data.keyword.alchemylanguageshort}} エンリッチメントの名前         | {{site.data.keyword.alchemylanguageshort}} JSON オブジェクト            | NLU エンリッチメントの名前            | NLU JSON オブジェクト       |
|---------------------------|----------------------------------------|----------------------------------------|--------------------------------|
| エンティティー抽出 (Entity Extraction)| entities                        |エンティティー抽出 (Entity Extraction)|   entities            |
| キーワード抽出 (Keyword Extraction)| keywords                        |キーワード抽出 (Keyword Extraction)|   keywords            |
| タクソノミー分類 (Taxonomy Classification)| taxonomy                        |カテゴリー分類 (Category Classification)*                    |   categories*         |
| 概念のタグ付け (Concept Tagging)| concepts                        |概念のタグ付け (Concept Tagging)|   concepts                        |
| センチメント分析 (Sentiment Analysis)| docSentiment                    |センチメント分析 (Sentiment Analysis)|   sentiment*          |
| 感情分析 (Emotion Analysis)| docEmotions                     |感情分析 (Emotion Analysis)|   emotion*            |
| 関係抽出 (Relation Extraction)| relations                       |意味役割抽出 (Semantic Role Extraction)*                   |   semantic_roles*     |
 \* 名前変更

{{site.data.keyword.alchemylanguageshort}} エンリッチメントについて詳しくは、[{{site.data.keyword.alchemylanguageshort}} エンリッチメント](/docs/services/discovery/discovery-auxiliary.html#AlchemyLanguage-enrichments)を参照してください。
{{site.data.keyword.nlushort}} エンリッチメントについて詳しくは、[エンリッチメントの追加](/docs/services/discovery/building.html#adding-enrichments)を参照してください。

## 主な変更点の概要

- {{site.data.keyword.nlushort}} エンリッチメントの JSON スキーマは、{{site.data.keyword.alchemylanguageshort}} エンリッチメントで使用されているものと異なります。各エンリッチメントの変更の完全リストについては、[エンリッチメント・スキーマの相違点](/docs/services/discovery/migrate-nlu.html#enrichment-schema-differences)を参照してください。
- _タクソノミー分類 (Taxonomy Classification) _ ({{site.data.keyword.alchemylanguageshort}}) エンリッチメントは、現在、_カテゴリー分類 (Category Classification)_ という名前になりました。その JSON オブジェクト名は、`taxonomy` から `categories` に変更されました。
- _関係抽出 (Relation Extraction)_ ({{site.data.keyword.alchemylanguageshort}}) エンリッチメントは、現在、_意味役割抽出 (Semantic Role Extraction)_ という名前になりました。その JSON オブジェクト名は、`relations`から `semantic_roles` に変更されました。
- _センチメント分析 (Sentiment Analysis)_ の JSON オブジェクト名は、`docSentiment` から `sentiment` に変更されました。
- _感情分析 (Emotion Analysis)_ の JSON オブジェクト名は、`docEmotions` から `emotion` に変更されました。

## 構成ファイルの変更

**{{site.data.keyword.alchemylanguageshort}}** のデフォルト構成ファイル (ツールでは `Default configuration` という名前) は、文書のテキスト・フィールドに次のエンリッチメントを適用しました。** エンティティー抽出 (Entity Extraction)**、**キーワード抽出 (Keyword Extraction)**、**タクソノミー分類 (Taxonomy Classification)**、**概念のタグ付け (Concept Tagging)**、**関係抽出 (Relation Extraction)**、および**センチメント分析 (Sentiment Analysis)**。このファイルには、フォントのスタイルとサイズに基づいた標準的な文書変換も含まれています。

**{{site.data.keyword.nlushort}}** のデフォルト構成ファイルは `Default Configuration with NLU` という名前で、文書のテキスト・フィールドに次のエンリッチメントを適用します。**エンティティー抽出 (Entity Extraction)**、**センチメント分析 (Sentiment Analysis)**、**カテゴリー分類 (Category Classification)**、および**概念のタグ付け (Concept Tagging)**。このファイルには、フォントのスタイルとサイズに基づいた標準的な文書変換も含まれています。これらの文書変換は、{{site.data.keyword.alchemylanguageshort}} デフォルト構成ファイルの文書変換とまったく同じです。

## 構成、コレクション、および照会のマイグレーション

カスタム構成を作成した場合は、{{site.data.keyword.nlushort}} エンリッチメントを使用する新しいカスタム構成を作成する必要があります。手順については、以下の資料を参照してください。

- [ツール](/docs/services/discovery/building.html#custom-configuration)
- [API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#add_configuration){: new_window}

{{site.data.keyword.alchemylanguageshort}} のデフォルト構成、またはカスタム {{site.data.keyword.alchemylanguageshort}} 構成が適用された既存のコレクションがある場合は、新規コレクションを作成し、{{site.data.keyword.nlushort}} 構成ファイル (デフォルト構成または新規カスタム構成) を適用し、文書をアップロードする必要があります。手順については、以下の資料を参照してください。

- [ツール](/docs/services/discovery/building.html#preparing-the-service-for-your-documents)
- [API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#create-collection){: new_window}

Discovery 照会言語を使用して作成された照会については、{{site.data.keyword.alchemylanguageshort}} と {{site.data.keyword.nlushort}} の JSON スキーマの相違点を調べ、それに応じて照会と照会 URL を更新する必要があります。詳しくは、[エンリッチメント・スキーマの相違点](/docs/services/discovery/migrate-nlu.html#enrichment-schema-differences)を参照してください。

## エンリッチメント・スキーマの相違点

以下の表は、{{site.data.keyword.nlushort}} エンリッチメントと {{site.data.keyword.alchemylanguageshort}} エンリッチメントでの JSON スキーマの相違点を示しています。

| {{site.data.keyword.alchemylanguageshort}}                         | {{site.data.keyword.nlushort}}       |
|-----------------------------------------|--------------------------------------|
|enriched_text.concepts                      |enriched_text.concepts|
|enriched_text.concepts.census              |非推奨|
|enriched_text.concepts.ciaFactbook          |非推奨|
|enriched_text.concepts.crunchbase                              |非推奨|
|enriched_text.concepts.dbpedia                               |enriched_text.concepts.dbpedia_resource|
|enriched_text.concepts.freebase                              |非推奨|
|enriched_text.concepts.geonames                                |非推奨|
|enriched_text.concepts.knowledgeGraph.typeHierarchy            |非推奨|
|enriched_text.concepts.musicBrainz                              |非推奨|
|enriched_text.concepts.opencyc                                  |非推奨|
|enriched_text.concepts.relevance                                |enriched_text.concepts.relevance|
|enriched_text.concepts.text                                    |enriched_text.concepts.text|
|enriched_text.concepts.website                                  |非推奨|
|enriched_text.concepts.yago                                    |非推奨|
|enriched_text.docSentiment.mixed                                |非推奨|
|enriched_text.docSentiment.score                                |enriched_text.sentiment.document.score|
|enriched_text.docSentiment.type                                |enriched_text.sentiment.document.label|
|enriched_text.entities                                          |enriched_text.entities|
|enriched_text.entities.count                                    |enriched_text.entities.count|
|enriched_text.entities.disambiguated.census                    |非推奨|
|enriched_text.entities.disambiguated.ciaFactbook                |非推奨|
|enriched_text.entities.disambiguated.crunchbase                |非推奨|
|enriched_text.entities.disambiguated.dbpedia                    |enriched_text.entities.disambiguation.dbpedia_resource|
|enriched_text.entities.disambiguated.freebase                  |非推奨|
|enriched_text.entities.disambiguated.geonames                  |非推奨|
|enriched_text.entities.disambiguated.musicBrainz                |非推奨|
|enriched_text.entities.disambiguated.name                      |enriched_text.entities.disambiguation.name|
|enriched_text.entities.disambiguated.opencyc                    |非推奨|
|enriched_text.entities.disambiguated.subType                    |enriched_text.entities.disambiguation.subtype|
|enriched_text.entities.disambiguated.umbel                      |非推奨|
|enriched_text.entities.disambiguated.website                    |非推奨|
|enriched_text.entities.disambiguated.yago                      |非推奨|
|enriched_text.entities.knowledgeGraph.typeHierarchy            |非推奨|
|enriched_text.entities.quotations                              |非推奨|
|enriched_text.entities.quotations.quotation                    |非推奨|
|enriched_text.entities.quotations.sentiment.mixed              |非推奨|
|enriched_text.entities.quotations.sentiment.score              |非推奨|
|enriched_text.entities.quotations.sentiment.type                |非推奨|
|enriched_text.entities.relevance                                |enriched_text.entities.relevance|
|enriched_text.entities.sentiment.mixed                          |非推奨|
|enriched_text.entities.sentiment.score                          |enriched_text.entities.sentiment.score|
|enriched_text.entities.sentiment.type                          |非推奨|
|enriched_text.entities.text                                    |enriched_text.entities.text|
|enriched_text.entities.type                                    |enriched_text.entities.type|
|enriched_text.keywords                                          |enriched_text.keywords|
|enriched_text.keywords.knowledgeGraph.typeHierarchy            |非推奨|
|enriched_text.keywords.relevance                                |enriched_text.keywords.relevance|
|enriched_text.keywords.sentiment.mixed                          |非推奨|
|enriched_text.keywords.sentiment.score                          |enriched_text.keywords.sentiment.score|
|enriched_text.keywords.sentiment.type                          |非推奨|
|enriched_text.keywords.text                                    |enriched_text.keywords.text|
|language                                                        |language|
|enriched_text.typedRelations                                    |enriched_text.relations|
|enriched_text.typedRelations.arguments                          |enriched_text.relations.arguments|
|enriched_text.typedRelations.arguments.entities                |enriched_text.relations.arguments.entities|
|enriched_text.typedRelations.arguments.entities.text            |enriched_text.relations.arguments.entities.text|
|enriched_text.typedRelations.arguments.entities.type            |enriched_text.relations.arguments.entities.type|
|enriched_text.typedRelations.arguments.text                    |enriched_text.relations.arguments.text|
|enriched_text.typedRelations.score                              |enriched_text.relations.score|
|enriched_text.typedRelations.sentence                          |enriched_text.relations.sentence|
|enriched_text.typedRelations.type                              |enriched_text.relations.type|
|enriched_title.typedRelations                                  |enriched_title.relations|
|enriched_title.typedRelations.arguments                        |enriched_title.relations.arguments|
|enriched_title.typedRelations.arguments.entities                |enriched_title.relations.arguments.entities|
|enriched_title.typedRelations.arguments.entities.text          |enriched_title.relations.arguments.entities.text|
|enriched_title.typedRelations.arguments.entities.type          |enriched_title.relations.arguments.entities.type|
|enriched_title.typedRelations.arguments.text                    |enriched_title.relations.arguments.text|
|enriched_title.typedRelations.score                            |enriched_title.relations.score|
|enriched_title.typedRelations.sentence                          |enriched_title.relations.sentence|
|enriched_title.typedRelations.type                              |enriched_title.relations.type|
|enriched_text.relations                                        |enriched_text.semantic_roles|
|enriched_text.relations.action.lemmatized                      |enriched_text.semantic_roles.action.normalized|
|enriched_text.relations.action.text                            |enriched_text.semantic_roles.action.text|
|enriched_text.relations.action.verb.negated                    |enriched_text.semantic_roles.action.verb.negated|
|enriched_text.relations.action.verb.tense                      |enriched_text.semantic_roles.action.verb.tense|
|enriched_text.relations.action.verb.text                        |enriched_text.semantic_roles.action.verb.text|
|enriched_text.relations.location.entities                      |enriched_text.semantic_roles.location.entities|
|enriched_text.relations.location.entities.disambiguated.census    |非推奨|
|enriched_text.relations.location.entities.disambiguated.ciaFactbook    |非推奨|
|enriched_text.relations.location.entities.disambiguated.crunchbase    |非推奨|
|enriched_text.relations.location.entities.disambiguated.dbpedia    |非推奨|
|enriched_text.relations.location.entities.disambiguated.freebase    |非推奨|
|enriched_text.relations.location.entities.disambiguated.geonames    |非推奨|
|enriched_text.relations.location.entities.disambiguated.musicBrainz    |非推奨|
|enriched_text.relations.location.entities.disambiguated.name    |非推奨|
|enriched_text.relations.location.entities.disambiguated.opencyc    |非推奨|
|enriched_text.relations.location.entities.disambiguated.subType    |非推奨|
|enriched_text.relations.location.entities.disambiguated.umbel    |非推奨|
|enriched_text.relations.location.entities.disambiguated.website    |非推奨|
|enriched_text.relations.location.entities.disambiguated.yago    |非推奨|
|enriched_text.relations.location.entities.knowledgeGraph.typeHierarchy    |非推奨|
|enriched_text.relations.location.entities.sentiment.score    |非推奨|
|enriched_text.relations.location.entities.sentiment.type    |非推奨|
|enriched_text.relations.location.entities.text                  |非推奨|
|enriched_text.relations.location.entities.type                  |非推奨|
|enriched_text.relations.location.keywords                      |非推奨|
|enriched_text.relations.location.keywords.text                  |非推奨|
|enriched_text.relations.location.sentiment.score                |非推奨|
|enriched_text.relations.location.sentiment.type                |非推奨|
|enriched_text.relations.location.text                          |非推奨|
|enriched_text.relations.object.entities                        |enriched_text.semantic_roles.object.entities|
|enriched_text.relations.object.entities.disambiguated.census    |非推奨|
|enriched_text.relations.object.entities.disambiguated.ciaFactbook    |非推奨|
|enriched_text.relations.object.entities.disambiguated.crunchbase    |非推奨|
|enriched_text.relations.object.entities.disambiguated.dbpedia    |enriched_text.semantic_roles.object.entities.disambiguation.dbpedia_resource|
|enriched_text.relations.object.entities.disambiguated.freebase    |非推奨|
|enriched_text.relations.object.entities.disambiguated.geonames    |非推奨|
|enriched_text.relations.object.entities.disambiguated.musicBrainz    |非推奨|
|enriched_text.relations.object.entities.disambiguated.name    |enriched_text.semantic_roles.object.entities.disambiguation.name|
|enriched_text.relations.object.entities.disambiguated.opencyc    |非推奨|
|enriched_text.relations.object.entities.disambiguated.subType    |enriched_text.semantic_roles.object.entities.disambiguation.subtype|
|enriched_text.relations.object.entities.disambiguated.umbel    |非推奨|
|enriched_text.relations.object.entities.disambiguated.website    |非推奨|
|enriched_text.relations.object.entities.disambiguated.yago    |非推奨|
|enriched_text.relations.object.entities.knowledgeGraph.typeHierarchy    |非推奨|
|enriched_text.relations.object.entities.sentiment.score    |非推奨|
|enriched_text.relations.object.entities.sentiment.type    |非推奨|
|enriched_text.relations.object.entities.text       |enriched_text.semantic_roles.object.entities.text|
|enriched_text.relations.object.entities.type    |enriched_text.semantic_roles.object.entities.type|
|enriched_text.relations.object.keywords    |enriched_text.semantic_roles.object.keywords|
|enriched_text.relations.object.keywords.knowledgeGraph.typeHierarchy    |非推奨|
|enriched_text.relations.object.keywords.text    |enriched_text.semantic_roles.object.keywords.text|
|enriched_text.relations.object.sentiment.score    |非推奨|
|enriched_text.relations.object.sentiment.type    |非推奨|
|enriched_text.relations.object.sentimentFromSubject.score    |非推奨|
|enriched_text.relations.object.sentimentFromSubject.type    |非推奨|
|enriched_text.relations.object.text    |enriched_text.semantic_roles.object.text|
|enriched_text.relations.sentence    |enriched_text.semantic_roles.sentence|
|enriched_text.relations.subject.entities    |enriched_text.semantic_roles.subject.entities|
|enriched_text.relations.subject.entities.disambiguated.census    |非推奨|
|enriched_text.relations.subject.entities.disambiguated.ciaFactbook    |非推奨|
|enriched_text.relations.subject.entities.disambiguated.crunchbase    |非推奨|
|enriched_text.relations.subject.entities.disambiguated.dbpedia    |enriched_text.semantic_roles.subject.entities.disambiguation.dbpedia_resource|
|enriched_text.relations.subject.entities.disambiguated.freebase    |非推奨|
|enriched_text.relations.subject.entities.disambiguated.geonames    |非推奨|
|enriched_text.relations.subject.entities.disambiguated.musicBrainz    |非推奨|
|enriched_text.relations.subject.entities.disambiguated.name    |enriched_text.semantic_roles.subject.entities.disambiguation.name|
|enriched_text.relations.subject.entities.disambiguated.opencyc    |非推奨|
|enriched_text.relations.subject.entities.disambiguated.subType    |enriched_text.semantic_roles.subject.entities.disambiguation.subtype|
|enriched_text.relations.subject.entities.disambiguated.umbel    |非推奨|
|enriched_text.relations.subject.entities.disambiguated.website    |非推奨|
|enriched_text.relations.subject.entities.disambiguated.yago    |非推奨|
|enriched_text.relations.subject.entities.knowledgeGraph.typeHierarchy    |非推奨|
|enriched_text.relations.subject.entities.sentiment.score    |非推奨|
|enriched_text.relations.subject.entities.sentiment.type    |非推奨|
|enriched_text.relations.subject.entities.text    |enriched_text.semantic_roles.subject.entities.text|
|enriched_text.relations.subject.entities.type    |enriched_text.semantic_roles.subject.entities.type|
|enriched_text.relations.subject.keywords    |enriched_text.semantic_roles.subject.keywords|
|enriched_text.relations.subject.keywords.knowledgeGraph.typeHierarchy    |非推奨|
|enriched_text.relations.subject.keywords.text    |enriched_text.semantic_roles.subject.keywords.text|
|enriched_text.relations.subject.sentiment.score    |非推奨|
|enriched_text.relations.subject.sentiment.type    |非推奨|
|enriched_text.relations.subject.text    |enriched_text.semantic_roles.subject.text|
|enriched_text.taxonomy    |enriched_text.categories|
|enriched_text.taxonomy.confident    |非推奨|
|enriched_text.taxonomy.label    |enriched_text.categories.label|
|enriched_text.taxonomy.score    |enriched_text.categories.score|
|enriched_text.docEmotions.sadness    |enriched_text.emotion.document.emotion.sadness|
|enriched_text.docEmotions.joy    |enriched_text.emotion.document.emotion.joy|
|enriched_text.docEmotions.fear    |enriched_text.emotion.document.emotion.fear|
|enriched_text.docEmotions.disgust    |enriched_text.emotion.document.emotion.disgust|
|enriched_text.docEmotions.anger    |enriched_text.emotion.document.emotion.anger|
|text    |text|
|title    |title|
|url    |url|
