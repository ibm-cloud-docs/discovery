---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-05"

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

# Watson Discovery News
{: #watson-discovery-news}

{{site.data.keyword.discoverynewsfull}} は {{site.data.keyword.discoveryshort}} に付属しています。 {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} は、**キーワード抽出**、**エンティティー抽出**、**セマンティック役割抽出**、**センチメント分析**、**関係抽出**、および**カテゴリー分類**の各コグニティブ洞察によって事前にエンリッチされた索引付きデータ・セットです (エンリッチメントについて詳しくは、『[エンリッチメントの追加](building.html#adding-enrichments)』を参照してください)。 クロール日付および公開日付もメタデータとして追加されます。 過去 60 日間のニュース・データの履歴検索が可能です。 {{site.data.keyword.discoverynewsfull}} を使用して何を作成できるのかを示すデモを[ここ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://discovery-news-demo.ng.bluemix.net/){: new_window} で見ることができます。

{{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} は、新しい記事で継続的に更新され、英語、スペイン語、ドイツ語、韓国語、および日本語で利用できます。英語版の {{site.data.keyword.discoverynewsshort}} は毎日約 300,000 の新しい記事で更新されます。 スペイン語版の {{site.data.keyword.discoverynewsshort}} は毎日約 60,000 の新しい記事で更新されます。ドイツ語版の {{site.data.keyword.discoverynewsshort}} は毎日約 40,000 の新しい記事で更新されます。韓国語版の {{site.data.keyword.discoverynewsshort}} は毎日約 10,000 の新しい記事で更新されます。日本語版の {{site.data.keyword.discoverynewsshort}} は毎日約 17,000 の新しい記事で更新されます。 ニュース・ソースは言語によって異なるため、各コレクションの照会結果は同一ではありません。

{{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} のユース・ケース:

- ニュース・アラート - 本サービスでサポートされている、エンティティー、キーワード、カテゴリー、およびセンチメントの分析を利用してニュース・アラートを作成することによって、ニュースおよびニュース知覚方法の両方を監視します。

- イベント検出 - 主語/動作/目的語のセマンティック役割抽出によって、 "acquisition" (買収)、"election results"  (選挙結果)、または "IPO" などの用語や動作がないか検査します。

- 話題になっているニュース・トピック -  話題のトピックを特定し、それらのトピック (または関連トピック) への言及頻度の増減をモニターします。

{{site.data.keyword.discoverynewsfull}} に対する照会の作成については、以下を参照してください。
- [Watson Discovery News の照会](/docs/services/discovery/using.html#querying-news)
- [照会の概念](/docs/services/discovery/using.html)
- [照会リファレンス](/docs/services/discovery/query-reference.html)

{{site.data.keyword.discoverynewsfull}} 構成の調整、トレーニング、{{site.data.keyword.discoverynewsfull}} コレクションへの文書の追加を行うことはできません。

{{site.data.keyword.discoverynewsfull}} 照会では、`text` JSON フィールドに各記事の最初の 50 ワードが表示されます。

{{site.data.keyword.discoverynewsfull}} の 1 回の照会で返される結果の最大数は `50` です。`50` を超える結果を返すには、追加の照会と `offset` パラメーターを使用してください。

**注:** このバージョンの {{site.data.keyword.discoverynewsfull}} は **2017 年 7 月 31 日**に初登場しました。 {{site.data.keyword.discoverynewsfull}} Original のサービスは、**2018 年 1 月 15 日**に廃止されました。マイグレーションについて詳しくは、[Watson Discovery News Original からのマイグレーション](/docs/services/discovery/migrate-bwdn.html)を参照してください。
