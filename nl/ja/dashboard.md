---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-25"

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

# パフォーマンス・ダッシュボードを使用したメトリックの表示および照会結果の改善
{: #performance-dashboard}

{{site.data.keyword.discoveryshort}} ツールのパフォーマンス・ダッシュボードを使用して、照会メトリックを表示したり、照会の関連性などの照会結果を改善したりすることができます。

左側の**「データ・メトリックの表示 (View data metrics)」**アイコンをクリックすると、パフォーマンス・ダッシュボードにアクセスできます。このダッシュボードは、プレミアム環境および専用環境では使用できません。

自然言語照会結果を改善する場合、以下の 2 つのオプションがあります。
- [データの追加により結果なし照会を修正 (Fix queries with no results by adding more data)](/docs/services/discovery/dashboard.html#addmore)
- [データのトレーニングにより関連性の高い結果を最上位に表示 (Bring relevant results to the top by training your data)](/docs/services/discovery/dashboard.html#traindata)

「[照会の概要 (Query overview)](/docs/services/discovery/dashboard.html#overview)」でデータ・メトリックを表示できます。 

## データの追加により結果なし照会を修正 (Fix queries with no results by adding more data)
{: #addmore}

ダッシュボードのこのセクションでは、返された結果がゼロの照会を確認し、今後照会が結果を返すようにデータを追加することができます。**「すべて表示してデータを追加 (View all and add data)」** ボタンをクリックして開始します。 

## データのトレーニングにより関連性の高い結果を最上位に表示 (Bring relevant results to the top by training your data)
{: #traindata}

このセクションでは、コレクションをトレーニングして、自然言語照会結果の関連性を向上させることができます。**「すべて表示して関連性トレーニングを実行 (View all and perform relevancy training)」**ボタンをクリックして開始します。次に、手順について、[照会の追加および結果の関連性の評価](/docs/services/discovery/train-tooling.html#results)を参照してください。

トレーニングの要件とオプションについて詳しくは、[ツールを使用した結果関連性の改善](/docs/services/discovery/train-tooling.html)を参照してください。

## 照会の概要 (Query overview)
{: #overview}

「照会の概要 (Query overview)」セクションには、以下が表示されます。
- ユーザーによる照会の総数
- 1 つ以上の結果がクリックされた照会の割合
- 結果がクリックされなかった照会の割合
- 結果が返されなかった照会の割合
- これらの結果を時系列に沿って表示するグラフ。これにより、データの追加および関連性トレーニングによってパフォーマンスがどのように改善されているかを追跡できます。

これらの結果は、イベントおよびフィードバック API (Events and Feedback API) を使用して収集されます。 詳しくは、[API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#events-and-feedback-api) を参照してください。
