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

# 照会のパフォーマンス
{: #qp}

{{site.data.keyword.discoveryshort}} の照会のパフォーマンスは、さまざまな要因に左右されます。 

## パフォーマンスの評価 
{: #qp-evaluate}

高い同時負荷が予期されるアプリケーションの場合は、{{site.data.keyword.discoveryshort}} アプリケーションのパフォーマンスを評価することが重要です。パフォーマンスを測定するためによく使用される特性がいくつかあります。
1.  **応答待ち時間** - {{site.data.keyword.discoveryshort}} が照会の結果を返すのに要する時間。 
    - 待ち時間は、さまざまな要因に左右されます。詳しくは、[パフォーマンスに影響する要因](/docs/services/discovery?topic=discovery-qp#perffactors)を参照してください。 
    - 典型的な照会のセットを使用して実稼働環境でテストを実行し、平均待ち時間を求めることが重要です。 
1.   **照会速度** - 特定の時間内に処理できる要求の数。通常は、1 秒あたりの照会数 (Queries per Second (QPS)) が測定されます。これは、高い同時負荷が予期されるアプリケーションの場合に、最重要の指標になります。  
     - 達成可能な速度を左右する要因は、待ち時間を左右する要因の多くと同じです。 
     - 照会速度を評価するためには、典型的な照会を使用し、予想される負荷をかける必要もあります。テストの際には、必ず、ピーク時の負荷を考慮に入れてください。

## パフォーマンスに影響する要因
{: #perffactors}

{{site.data.keyword.discoveryshort}} の照会のパフォーマンスは、プラン・サイズ、照会の複雑度、使用する機能、コレクションのサイズと複雑度など、さまざまな要因に左右されます。

### プラン・サイズ
{: #qp-plansize}

{{site.data.keyword.discoveryshort}} の料金プランごとに、使用可能な文書の数に制限があり、照会ロードの処理能力が異なります。プラン・サイズが大きいほど、照会の処理に使用できるリソースが多くなります。平均速度制限もプラン・サイズごとに異なります。プランをアップグレードすると、パフォーマンスを向上させることができます。各プランと制限については、[{{site.data.keyword.discoveryshort}} の料金プラン](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)を参照してください。 

### 照会の複雑度
{: #qp-query}

{{site.data.keyword.discoveryshort}} に対して照会を実行する方法は数多くあります。使用するさまざまな操作によって、パフォーマンスは影響を受けます。パフォーマンスに影響を与える可能性がある照会の特性を以下に示します。

1.   **長さ** - 通常、照会が長いほどパフォーマンスは低くなります。 
1.   **集約** - 集約は比較的に複雑な照会タイプです。集約がネストされているとパフォーマンスに多大な影響を及ぼします。 
1.   **演算子** - ワイルドカードおよびファジー・マッチングを使用すると、パフォーマンスに影響を与えます。
1.   **数** - 戻される文書の数を減らすと、パフォーマンスが向上します。結果をページ送りする必要がある場合は、`offset` パラメーターを使用してください。 
1.   **戻りフィールド** - アプリケーションで必要とされるフィールドだけが戻されるように制限すると、効果があります (例えば、文書のタイトルとパッセージのみが必要な場合に、文書の全文を戻さないようにします。) 

詳しくは、[照会リファレンス](/docs/services/discovery?topic=discovery-query-reference#query-reference)を参照してください。

### 使用する機能
{: #qp-features}

照会結果を向上させる機能が数多くあります。パフォーマンスに影響を与える可能性がある機能を以下に示します。
 
1.   **パッセージ取り出し** - パッセージ取り出しは、文書内を検索し、照会に関連したテキスト・スニペットを検出します。`passages.fields` パラメーターを使用すると、パッセージ取り出しで検索する文書内のフィールドを調整できます。コンテンツに多数のフィールドがある場合に、この方法を使用するとパッセージ取り出しの待ち時間を短縮できます。パッセージ取り出しについて詳しくは、『[パッセージ](/docs/services/discovery?topic=discovery-query-parameters#passages)』を参照してください。
1.   **関連性トレーニング** - 関連性トレーニングは、コレクション内の最上位テキスト・フィールド (JSON 内の `document_id` と同じレベルのフィールド) ごとに特性を計算します。最上位フィールドが多数あると、トレーニング使用時の `natural_language_query` のパフォーマンスに影響が及ぶ可能性があります。最上位フィールドの数を減らすと、パフォーマンスが向上する可能性があります。そのためには、正規化を実行するか、手動で JSON を編集して、関連するコンテンツの検出に役立たないフィールドをネスト構造に入れます。トレーニングに使用するフィールドを変更することは、モデルにも影響を及ぼします。したがって、この変更を行う場合は、パフォーマンスへの影響と結果の正確度の両方について検討する必要があります。関連性トレーニングについて詳しくは、[結果関連性の改善](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling)を参照してください。
1.  **Continuous Relevancy Training** - Continuous Relevancy Training は、環境内のすべてのコレクションに対して検索を実行します。環境内のコレクションが多くなるほど、パフォーマンスに与える影響が大きくなります。詳しくは、[Continuous Relevancy Training](/docs/services/discovery?topic=discovery-crt#crt) を参照してください。

### コレクションのサイズと複雑度
{: #qp-collection} 

プライベート・コレクション内の文書の構成も、照会のパフォーマンスに影響を与えます。
1.  **文書の総数** - 拡張プラン・サイズの`文書数`の上限に近づくと、パフォーマンスに影響を及ぼす可能性があります。 
1.  **文書のサイズ** - 非常に大規模な文書 (数 MB のサイズのもの) の場合、要求ごとに大量のデータを移動する必要が生じます。そのため、特にパッセージ取り出しと関連性トレーニングの使用時に、パフォーマンスに悪影響を及ぼす可能性があります。 
1.  **エンリッチメントの数** - エンリッチメントにより、ネストされたフィールドが相当数追加され、文書の複雑度が増します。エンリッチメントが不要なユース・ケースでは、取り込み時にエンリッチメントを無効化することを検討してください。エンリッチメントは、`natural_language_query` 検索の関連性で直接使用されません。エンリッチメントについて詳しくは、[エンリッチメントの追加](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)を参照してください。
