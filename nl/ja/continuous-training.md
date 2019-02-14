---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-25"

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

# Continuous Relevancy Training
{: #crt}

{{site.data.keyword.discoveryshort}} Continuous Relevancy Training は、ユーザーの行動から自動的に学習することができ、結果の関連性のランク付けを改善するために必要な労力を大幅に削減します。ユーザーからの対話を使用することで、最も関連性の高い結果をどのように表示するのかを学習します。クリックなどの対話から、ユーザーにとって最も価値のある結果を判別し、今後の照会で最も重要なシグナルを明らかにすることができます。Continuous Relevancy Training は、文書を再ランク付けして、最も関連性の高い情報を結果の最上位に表示します。これを使用すると、以下を行うことができます。

- クリックされた結果に基づいて、サポート・エージェントの結果の関連性を向上させる
- 選択されたロングテール結果に基づいて、より関連性の高い結果を顧客チャットボットに表示する 
- 探索された結果に基づいて、より関連性の高い応答を専門家に提供する

Continuous Relevancy Training をセットアップするには、以下のようにします。

- Continuous Relevancy Training は、環境レベルでのみ有効にできます。照会では、`/api/v1/environment/{environment_id}/query` エンドポイントと `/api/v1/environments/{environment_id}/query` エンドポイントのいずれかを使用して、1 つ以上のコレクションを照会する必要があります。
- {{site.data.keyword.discoveryshort}} `イベント` (クリック) は、必要なトレーニング・データの作成に使用されるため、最初にイベント・トラッキングを統合します。詳しくは、[使用状況のモニター](/docs/services/discovery/feedback.html#usage)を参照してください。
- Continuous Relevancy Training を開始するには、クリック・イベントが関連付けられた、少なくとも 1000 個の自然言語照会が必要です。イベントおよびログはインスタンス全体で 30 日間保持されるため、その期間中に 1000 クリックを収集する必要があります。
- Continuous Relevancy Training は、サイズが `スモール` 以上の拡張プラン、およびプレミアム・プランで使用可能です。`ライト`・プランでは使用できません。
- Continuous Relevancy Training のコレクション数は `5` に制限されています。Continuous Relevancy Training は複数のコレクションにわたって機能するため、照会時間とトレーニング時間が延びることがあります。
- Continuous Relevancy Training は最上位フィールドでのみ行われ、トレーニング処理で使用できるフィールド数には制限があります。最上位フィールドが `10` 個を超える場合、トレーニングでエラーが発生する可能性が高くなります。 

Continuous Relevancy Training を使用するには、以下のようにします。

トレーニングが終わると、Continuous Relevancy Training が使用され、環境レベルの照会を使用する際に `natural_language_query` の結果に影響を与えます。 

環境内のすべてのコレクションにわたって複数のコレクションの `natural_language_query` を実行することによって、照会時に Continuous Relevancy Training を使用できます。手順については、[複数コレクションの照会](/docs/services/discovery/using.html#multiple-collections)を参照してください。 

**注:** Continuous Relevancy Training は、トレーニング済みまたはトレーニングされていないコレクション・レベル (`/v1/environments/{environment_id}/collections/{collection_id}/query`) の照会呼び出しに対して行われた照会には影響を与えません。 

状況の追跡:

Continuous Relevancy Training の状況は、`/api/v1/environments` エンドポイントから表示できます。 [API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#environments-api){: new_window} を参照してください。 以下のように、`status` は、トレーニング操作の状態に関する情報を提供し、Continuous Relevancy Training がアクティブかどうかを示します。

```
"search_status" : [
        {
            "scope" : "environment",
            "status" : "NO_DATA",
            "status_description" : "Discovery is employing a default strategy for document search natural_language_query. Enable query and event logging so we can initiate relevancy training to improve search accuracy.”
        }
    ]
```
