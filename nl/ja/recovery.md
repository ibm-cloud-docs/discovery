---

copyright:
  years: 2019
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

# 高可用性および災害復旧
{: #recovery}

{{site.data.keyword.discoveryfull}} は、単一障害点のない高可用性をサポートしています。また、サービスを再作成できるように独自の災害復旧計画に沿って {{site.data.keyword.discoveryshort}} データをバックアップする作業は、お客様が行う作業です。
{: shortdesc}

{{site.data.keyword.discoveryshort}} のトラフィックは、1 つの地域内の複数のゾーン間でロード・バランシングされます。ゾーン 1 つは、同じ地域内の 1 データ・センターに相当します。詳しくは、[ダウン時間をゼロにする方法 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/docs/overview?topic=overview-zero-downtime#zero-downtime){: new_window} を参照してください。

## Watson Discovery にあるデータのバックアップ
{: #backup}

{{site.data.keyword.discoveryfull}} に保管されたデータをバックアップする方法は複数あります。災害復旧計画に、それらの方法を含める必要があります。

-  コピーを保持する必要があるデータ (ソース文書など)
-  {{site.data.keyword.discoveryshort}} に保管され、抽出とバックアップが必要なデータ
  
最初から再作成する必要があるデータもあります (例えば、フィードバック・イベントなどのバックアップできないデータ)。 

### 取り込まれた文書
{: #backupdocs}

アップロードした文書は、変換され、エンリッチされた後に、検索索引に保管されます。検索索引は災害時に復旧できないため、すべてのソース文書のバックアップを安全な場所に保管する必要があります。

また、外部データ・ソースに対してスケジュールしたクロールによって文書をインポートする場合は、そのデータ・ソースの資格情報を外部に保存して、データ・ソースを迅速に再確立できるようにしておく必要があります。利用可能なソースとそれぞれに必要な資格情報のリストについては、[データ・ソースへの接続](/docs/services/discovery?topic=discovery-sources#sources)を参照してください。

### 構成
{: #backupconfigs}

災害時のためにインスタンス構成をバックアップし、ローカルに保存する必要があります。 

これらの構成をバックアップするには、まず、各インスタンスの[構成をリスト](https://cloud.ibm.com/apidocs/discovery#list-configurations)します。 

構成のリストを取得したら、各構成の[詳細を取得](https://cloud.ibm.com/apidocs/discovery#get-configuration-details)します。

### トレーニング・データ
{: #backuptraining}

災害時のために、トレーニング対象のコレクションごとにトレーニング・データをバックアップし、ローカルに保存する必要があります。 

トレーニング・データは、コレクションの明示的トレーニングに使用され、コレクション単位で保管されます。 

トレーニング・データを抽出するには、API を使用して {{site.data.keyword.discoveryshort}} から照会と評価をダウンロードします。 

1.  [トレーニング・データをリスト](https://cloud.ibm.com/apidocs/discovery#list-training-data)します。
1.  各照会の[例をリスト](https://cloud.ibm.com/apidocs/discovery#list-examples-for-a-training-data-query)します。
1.  トレーニング・データの例の[詳細を取得](https://cloud.ibm.com/apidocs/discovery#get-details-for-training-data-example)します。 

トレーニング・データで使用する`文書 ID` は、現在のコレクションにある文書を指しています。新規コレクションで必ず同じ`文書 ID` を使用して、正しい ID が参照されるようにする必要があります。そうしないと、復元した関連性トレーニングが機能しません。
{: important} 

### 照会
{: #backupqueries}

デフォルトでは (設定解除しない限り)、{{site.data.keyword.discoveryshort}} は、送信された照会を保管します。 

それらを[統計の目的](https://cloud.ibm.com/apidocs/discovery#number-of-queries-over-time)でリストアできるようにする場合は、それらの照会を別途保存する必要があります。 

{{site.data.keyword.discoveryshort}} から[照会を抽出](https://cloud.ibm.com/apidocs/discovery#search-the-query-and-event-log)できますが、最大で 10,000 個の照会が保存されています。ページング API はありません。照会のリストアは推奨されていません。最初から再作成することをお勧めします。

### フィードバック/クリック
{: #clicks}

フィードバック・イベントの形式でクリック・データを保管する場合、現時点では、この情報をバックアップおよびリストアする簡単な方法はありません。[クリック/フィードバック・データ](https://cloud.ibm.com/apidocs/discovery#create-event) API を使用して、最初から再作成することをお勧めします。

### 拡張リスト
{: #backupexpansions}

照会に変更を加えるために拡張を使用している場合、拡張リストをバックアップし、ローカルに保存する必要があります。これを行うには、[拡張リスト取得](https://cloud.ibm.com/apidocs/discovery#get-the-expansion-list) API コマンドを使用して、拡張リストを要求し、ローカルに保存します。

### トークン化辞書またはストップワード
{: #backupstopwords}

これらの機能を使用する場合、これらのファイルをバックアップし、ローカルに保存する必要があります。ストップワードの場合はテキスト・ファイルをバックアップし、トークン化の場合は JSON ファイルをバックアップする必要があります。それぞれのファイル・タイプについて詳しくは、[カスタムのトークン化辞書の作成](/docs/services/discovery?topic=discovery-query-concepts#tokenization)および[ストップワードの定義](/docs/services/discovery?topic=discovery-query-concepts#stopwords)を参照してください。

### コレクション情報
{: #collectioninfo}

必須ではありませんが、定期的に各コレクションの[状況情報を取得](https://cloud.ibm.com/apidocs/discovery#get-collection-details)し、その情報をローカルに保存することをベスト・プラクティスとしてお勧めします。これらの統計を保持しておくと、後で必要に応じて、回復プロセスが成功したことを確認できます。
{: tip} 


### Smart Document Understanding モデル
{: #backupsdu}

Smart Document Understanding (SDU) を使用している場合、モデルが構成に関連付けられます。この情報がなくならないように、[モデルをエクスポート](/docs/services/discovery?topic=discovery-sdu#import)し、バックアップし、ローカルに保存する必要があります。SDU モデルのファイル拡張子は `.sdumodel` です。


## 新規 Watson Discovery インスタンスへのデータのリストア
{: #restore}

バックアップを使用して、別のデータ・センター (地域/ロケーションとも呼びます。例: ダラス、ヒューストン、ワシントン DC、ロンドン) 内の新規 {{site.data.keyword.discoveryshort}} インスタンスにリストアすることを検討してください。
{: note}

リストアを開始するには、コレクション、関連付けられたデータ・ソース、およびファイル・バックアップのリストをまず確認します。

-  保存されている構成情報を使用して、[環境](https://cloud.ibm.com/apidocs/discovery#create-an-environment)と[コレクション](https://cloud.ibm.com/apidocs/discovery#create-a-collection)を作成します。構成が適切に定義されていること、またコレクションの言語が適切に設定されていることを確認します。これを行わないと、システムの再稼働が遅れます。
-  {{site.data.keyword.discoveryshort}} でカスタム構成をセットアップしていた場合は、[それらのカスタム構成を再作成](/docs/services/discovery?topic=discovery-configservice#when-you-need-a-custom-configuration)する必要があります。 
-  トークン化辞書またはストップワードをコレクションに再追加します。[カスタムのトークン化辞書の作成](/docs/services/discovery?topic=discovery-query-concepts#tokenization)および[ストップワードの定義](/docs/services/discovery?topic=discovery-query-concepts#stopwords)を参照してください。 
-  カスタム照会拡張を使用していた場合は、コレクションごとに[照会拡張を追加](https://cloud.ibm.com/apidocs/discovery#create-or-update-expansion-list)する必要もあります。 
-  エンリッチメントのために Watson Knowledge Studio (WKS) のカスタム・エンティティー・モデルを使用していた場合は、{{site.data.keyword.discoveryshort}} インスタンスに[そのモデルをインポート](/docs/services/discovery?topic=discovery-configservice#custom-entity-model)する必要があります。

コレクションを前と同じようにセットアップしたら、ソース文書の取り込みを開始する必要があります。これを行うには、前にその文書を取り込んだ方法に応じて、以下を使用します。
-  [API](https://cloud.ibm.com/apidocs/discovery#add-a-document)
-  [コネクター](/docs/services/discovery?topic=discovery-sources#sources) 
-  [Data Crawler](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)
-  その他の方式

### トレーニング・データのリストア
{: #restoretraining}

コレクションをリストアしたら、[関連性トレーニング・モデルの再作成](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api)プロセスを開始できます。 

バックアップしたトレーニング・データを取り出してから、以下を行います。

1. [照会をアップロード](https://cloud.ibm.com/apidocs/discovery#add-query-to-training-data)します。
1. 照会ごとに[サンプル文書をアップロード](https://cloud.ibm.com/apidocs/discovery#add-example-to-training-data-query)します。
1.  トレーニング・データをアップロードしたら、この[ブログ投稿](https://developer.ibm.com/dwblog/2017/get-relevancy-training/)を参照して、前の正確度の数値に合致しているか確認します。以前の`文書 ID` を新規トレーニング・データに移すか、または新規コレクションの新規文書 ID を反映するように更新する必要があることに留意してください。


### 外部データ・ソースへの接続のリストア
{: #restoreconnections}

予期しないデータ損失が発生すると、外部データ・ソースに対してスケジュールしたクロールが失われる可能性があります。利用可能なソースのリストについては、[データ・ソースへの接続](/docs/services/discovery?topic=discovery-sources#sources)を参照してください。

外部データをリストアするには、それらのデータ・ソースへの接続を再確立し、再クロールする必要があります。

前に保管したデータ・ソース資格情報を見つけ、[こちら](/docs/services/discovery?topic=discovery-sources#sources)の手順に従ってください。これにより、データ・ソースに再接続して {{site.data.keyword.discoveryshort}} にデータをインポートできるようになります。


### Smart Document Understanding モデルのリストア
{: #restoresdu}

前にエクスポートした Smart Document Understanding (SDU) モデルをインポートするには、[こちら](/docs/services/discovery?topic=discovery-sdu#import)の手順に従ってください。SDU モデルのファイル拡張子は `.sdumodel` です。

既存の SDU モデルを新規コレクションにインポートするときには、ベスト・プラクティスとして、新規コレクションを作成し、文書を 1 つ追加してモデルをインポートした後に、残りの文書をアップロードすることをお勧めします。
