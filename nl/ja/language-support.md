---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-18"

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

# 言語サポート
{: #language-support}

{{site.data.keyword.discoveryfull}} サービスでは、**基本**と**フル**という 2 つのレベルの言語サポートを提供しています。
{: shortdesc}

| 言語                         |  サポート・レベル         |
|---------------------------------|------------------------|
| 英語 (en)                    |  フル         |
| アラビア語 (ar)                     |  基本         |
| 中国語 (簡体字) (zh-CN)     |  基本         |
| オランダ語 (nl)                     |  基本         |
| フランス語 (fr)                     |  フル         |
| ドイツ語 (de)                     |  フル         |
| イタリア語 (it)                    |  フル        |
| 日本語 (ja)                  |  フル         |
| 韓国語 (ko)                    |  フル         |
| ブラジル・ポルトガル語 (pt-br)   |  フル         |
| スペイン語 (es)                    |  フル         |

## 基本サポート
{: #basic-support}

- {{site.data.keyword.discoveryshort}} のサポートには以下が含まれます。
    - 文書変換
    - オーケストレーション
    - {{site.data.keyword.discoveryshort}} ツール機能
    - フロントエンド API (フロントエンド照会 API を除く)
    - 言語ごとに最適化された索引
    - 関連性トレーニング
    - 照会拡張
    - ストップワード
    - 9 言語での文書: 英語、フランス語、ドイツ語、日本語、韓国語、ブラジル・ポルトガル語、スペイン語、中国語 (簡体字)、中国語 (繁体字)。 {{site.data.keyword.Bluemix_notm}} 資料の下部までスクロールして、言語を選択します。
- エンリッチメント
    - {{site.data.keyword.knowledgestudiofull}} カスタム・モデルとの統合
    - 言語検出

## フル・サポート
{: #full-support}

フル・サポートには、基本サポートに加えて以下が含まれます。

- パッセージ取り出し
- 翻訳された {{site.data.keyword.knowledgestudiofull}} インターフェース
- すべての {{site.data.keyword.nlushort}} (NLU) エンリッチメント、およびメタデータ抽出。 NLU エンリッチメントは以下のとおりです。
    - エンティティー抽出 (Entity Extraction)
    - キーワード抽出 (Keyword Extraction)
    - カテゴリー分類 (Category Classification)
    - 概念のタグ付け (Concept Tagging)
    - 意味役割抽出 (Semantic Role Extraction)
    - センチメント分析 (Sentiment Analysis)
    - 感情分析 (Emotion Analysis) (英語のみ)

## 英語のみのサポート
{: #feature-support}

以下の機能は、現在、英語でのみサポートされています。

- 要素分類エンリッチメント
- {{site.data.keyword.discoveryfull}} Knowledge Graph (ベータ)
- 文書の非重複化 (ベータ)

## 日本語のみのサポート
{: #japanese-support}

以下の機能は、現在、日本語でのみサポートされています。

- カスタムのトークン化辞書
