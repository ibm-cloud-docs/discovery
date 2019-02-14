---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-17"

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

# 使用状況のモニター
{: #usage}

{{site.data.keyword.discoveryshort}} インスタンスの使用状況をモニターおよび追跡し、そのデータをアプリケーションの理解と改善に役立てることができます。[Events API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#events-and-feedback-api){: new_window} を使用して、特定の自然言語照会およびアクションと関連付けられたログ・エントリーを作成できます。例えば、結果セット内のどの文書がユーザーによって「クリック」されたのか、およびそのクリックがいつ起こったのかを記録できます。

**注:** ログおよびイベントのモニターは、プライベート・データ・コレクションでの自然言語照会についてのみ行われます。{{site.data.keyword.discoverynewsfull}} ではログは収集されません。

{{site.data.keyword.discoveryshort}} は、以下の情報をログに記録できます。
- **照会** - 環境内のコレクションに対して実行される自然言語照会 
- **インプレッション** (または**結果**) -  特定の照会に対して返された結果 (通常は文書または文節) 
- **イベント** - {{site.data.keyword.discoveryshort}} で 1 つまたは複数の結果に対してユーザーが実行する対話 (例えば、文書結果のクリック)

**照会**と**インプレッション**は自動的にログに記録されます。**イベント**のロギングは、API を介してアプリケーションに組み込むことができます。

## ログの表示
{: #viewlogs}

照会およびイベント・ログを検索して、指定された基準に一致する照会セッションを見つけることができます。 `logs` エンドポイントの検索では、サポートされるパラメーターに標準 {{site.data.keyword.discoveryshort}} 照会構文が使用されます。このエンドポイントは、記録されたデータを表示および検索するための基本的な照会機能を提供します。  

`/api/v1/logs` エンドポイントは、以下の {{site.data.keyword.discoveryshort}} 照会パラメーターをサポートします。
- query 
- filter
- sort
- count 
- offset
- version

パラメーターの機能および構文について詳しくは、『[照会パラメーター](/docs/services/discovery/query-parameters.html)』を参照してください。

「train」という語を含む自然言語照会をログで検索する例を以下に示します。

`https://gateway.watsonplatform.net/discovery/api/v1/logs?version=2018-03-28&query=train`

`logs` 照会の応答には、{{site.data.keyword.discoveryshort}} 文書結果に似た結果が含まれます。各結果は、文書 `type` フィールドで指定された、照会またはイベントのいずれかになります。  

照会ログの例:

```
{
            "customer_id": "",
            "environment_id": "252e6e82-c2d2-450e-9670-0008b0a3a99c",
            "natural_language_query": "how do i get from the airport to the city",
            "query_id": "_Qs35yOoa7",
            "document_results": {
                "count": 2,
                "results": [
                    {
                        "collection_id": "af9e1f41-6114-4d77-bca6-c9b99b2601b1",
                        "score": 6.724753491503856,
                        "position": 1,
                        "document_id": "4193eaa727d79b0f74597356dbcbb9a7"
                    },
                    {
                        "collection_id": "af9e1f41-6114-4d77-bca6-c9b99b2601b1",
                        "score": 5.791631414211986,
                        "position": 2,
                        "document_id": "bdcd6a9cc1438a3faa8c925f6a8d9429"
                    }
                ]
            },
            "event_type": "query",
            "session_token": "1_LKczxWGEWx5TJAi1_Qs35yOoa7",
            "created_timestamp": "2018-09-12T05:20:07.469Z"
        }
```

照会ログを使用して、エンド・ユーザーに返された結果のタイプを調査し、{{site.data.keyword.discoveryshort}} で使用可能な手法を使用して結果品質を向上させる方法を調査できます。以下に例を示します。 
- 関連性トレーニング (『[API を使用した結果関連性の改善](/docs/services/discovery/train.html)』および『[ツールを使用した結果関連性の改善](/docs/services/discovery/train-tooling.html)』を参照)
- [照会演算子](/docs/services/discovery/query-operators.html)
- [照会拡張](/docs/services/discovery/using.html#query-expansion)
- カスタム構成 (『[構成リファレンス](/docs/services/discovery/custom-config.html)』を参照)

## イベント・ログの作成
{: #eventlogs}

イベント・ログは、アプリケーション内でのユーザーの対話を追跡するために使用されます。これは、アプリケーションのパフォーマンスがどれほど良好かを把握し、さらに、焦点を当てる必要がある領域を特定して、結果を改善するのに役立ちます。アプリケーションに組み込んでイベントを追跡できる API が {{site.data.keyword.discoveryshort}} で提供されています。ユーザーがアクションを実行するときに適切な情報を指定してこの API を呼び出すと、{{site.data.keyword.discoveryshort}} にシグナルが送り返され、それを後でログで確認できます。 

イベントは、コンピューティング測定基準 (クリックスルー率など) の情報を収集して、エンド・ユーザーが関連情報を検索する際にアプリケーションがどのくらい効果的に支援しているかを測定するのに役立てることができます。また、イベントの使用は、照会とクリックを検討することでトレーニングをシードして、グランドトゥルース構築を始めるのに役立てることもできます。 

ユーザーが結果と対話する任意の場所に、この API を追加できます。例えば、検索 UI では、ユーザーが文書リンクをクリックするところにこれを追加でき、チャットボット・インターフェースでは、ユーザーが**「展開」**ボタンまたは**「詳細」**ボタンをクリックしたのを追跡するためにこれを使用できます。

{{site.data.keyword.discoveryshort}} の結果は、セッション・トークンなど、イベントの追跡に使用できる追加情報を返します。 

`"matching_results": 179,`
`"session_token": "1_LKczxWGEWx59fYD0_VV8HFUpb6"`

イベントを記録するにには、`/api/v1/events` エンドポイントに POST を実行します。詳しくは、[Events API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#events-and-feedback-api){: new_window} を参照してください。

イベントは、記録された後、`/api/v1/logs` エンドポイントを使用して読み取ることができます。`session_token` を使用して、複数のイベントを結合して、関連する照会にすることができます。
