---

copyright:
  years: 2015, 2018, 2019
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

# プランのアップグレード
{: #upgrading-your-plan}

{{site.data.keyword.discoveryfull}} サービスでは、お客様のニーズに合わせて異なるレベルのリソースと機能を選択できるように 3 つのプランが用意されています。
{: shortdesc}

詳しくは、[{{site.data.keyword.discoveryshort}} の料金プラン](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)および [{{site.data.keyword.discoveryshort}} カタログ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/catalog/services/discovery){: new_window} を参照してください。

## サービスのアップグレード
{: #service}

プランをライトから拡張にサイズ変更するには、以下のようにします。

1. [{{site.data.keyword.Bluemix_notm}} ダッシュボード](https://{DomainName}/dashboard)を開きます。 
1. {{site.data.keyword.discoveryshort}} サービス・インスタンスをクリックして、{{site.data.keyword.discoveryshort}} サービス・ダッシュボードを開きます。
1. {{site.data.keyword.discoveryshort}} サービスの**「管理」**ページで、**「アップグレード」**をクリックして拡張プランを選択します。 これにより、**「プラン」**ページが開きます。 手順に従って、アップグレードを完了してください。 
1. **「管理」**ページに戻り、**「ツールの起動」**をクリックして、{{site.data.keyword.discoveryshort}} ツールを開きます。
   - 拡張プランへのアップグレード前に、ライト・プラン用の環境を作成したことがない場合、![Cog](images/icon_settings.png) アイコンをクリックし、**「環境の作成 (Create environment)」**を選択します。 画面に、拡張プラン用のオプションが表示されます。 お客様のニーズに合ったものを選択してください。  (`X スモール`、`スモール`、`ミディアム・スモール`、`ミディアム`、`ミディアム・ラージ`、`ラージ`、`X ラージ`、`XX ラージ`)。
   - 拡張プランへのアップグレード前に、ライト・プラン用の環境を作成したことがある場合、新しい拡張プランの環境は、デフォルトで`スモール`になります。 

## 拡張プラン内のティアの切り替え
{: #switchadvanced} 

既に拡張プランを使用中で、それをより大きなプラン・サイズにアップグレードする場合、[API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery#update-an-environment){: new_window} を使用してそれを実行できます。 

拡張プランのストレージ制限および価格設定について詳しくは、[拡張の価格設定](/docs/services/discovery?topic=discovery-discovery-pricing-plans#advanced)を参照してください。

使用可能な拡張プランのサイズは以下のとおりです。 

プラン・サイズ | ラベル  
--------- | ------ 
X スモール | XS 
スモール | S 
ミディアム・スモール | MS 
ミディアム | M 
ミディアム・ラージ | ML 
ラージ | L
X ラージ | XL 
XX ラージ | XXL 

- アップグレード中も、照会および索引付けは進行できます。 アップグレードに必要な時間は、いくつかの要因によって異なります。 アップグレード実行中、API を使用して環境をポーリングできます。
- 拡張プラン内でレベルを変更する場合、新しいインスタンスを作成する必要はありません。 
- アップグレード完了後は、新しいプラン料金で請求されます。
- 小さいプラン・サイズが必要なことが後でわかった場合は、適切なプラン・サイズをセットアップし、データをマイグレーションした後に、大きいほうのプランをキャンセルする必要があります。 

## プレミアム・プランへのアップグレード
{: #premium}

プレミアム・プランに関心があるお客様は、[営業担当](https://ibm.biz/contact-wdc-premium)にお問い合わせください。  
