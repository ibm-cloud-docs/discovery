---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-09"

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

# Discovery の料金プラン

{{site.data.keyword.discoveryfull}} サービスでは、お客様のニーズに合わせて異なるレベルのリソースと機能を提供する 3 つのプランをご用意しています。
{: shortdesc}

**プライベート・データのユースケース**には、以下の制限と料金があります。

| ライト                     |  スタンダード        | アドバンスト          | プレミアム          |
|--------------------------|-------------------|-------------------|-------------------|
| 1 カ月当たり最大 2,000 個の同時文書\*   |1 カ月当たり最大 100,000 個の同時文書\*<br/> 1 カ月当たり 1,000 個の同時文書につき $10 ($0.0139USD/1000文書/時)\*\*\*<br/> 1 カ月当たり 2,000 個の文書まで無料\*\*\*\*  | **予約済み環境**</br>1 カ月当たり $1,000 の基本レート<br/> 1 カ月当たり最大 1,000,000 個の文書\*<br/> 1 カ月当たり 1,000 個の同時文書につき $5 ($0.00694 USD/1000文書/時)\*\*\*<br/> 1 カ月当たり 100,000 個の文書を含む\*\*\*\*</br> 大規模環境については、[販売窓口 (Sales) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/marketing/iwm/dre/signup?source=MAIL-watson){: new_window} までお問い合わせください。| **プレミアム・プラン**では、開発者および組織に対して、より高い独立性とセキュリティーが確保される、1 つ以上の Watson サービスのシングル・テナント・インスタンスをご提供しています。これらのプランでは、既存の共有プラットフォームにおける計算レベルの独立性が確保され、さらに転送中や静止中のエンドツーエンドの暗号化データが提供されます。詳細情報、またはプレミアム・プランのご購入については、[販売窓口 (Sales) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://ibm.biz/contact-wdc-premium){: new_window} までお問い合わせください。|
| 200MB\*\*                  |10GB\*\*  | 80GB\*\* |-|
| 最大 2 個のコレクション      |最大 4 個のコレクション | 最大 100 個のコレクション|-|
| 最大 1 個の {{site.data.keyword.knowledgestudiofull}} カスタム・モデル     |最大 1 個の {{site.data.keyword.knowledgestudioshort}} カスタム・モデル | 無制限の {{site.data.keyword.knowledgestudioshort}} カスタム・モデル<br/>1 個の {{site.data.keyword.knowledgestudioshort}} カスタム・モデルを含む<br/>{{site.data.keyword.knowledgestudioshort}} モデル 1 個につき 1 カ月当たり ＄800 追加|-|

**注:** すべてのプランにおいて、1 カ月当たり最初の 1,000 個の {{site.data.keyword.discoverynewsshort}} 照会は無料です。最初の 1,000 個を超えると、{{site.data.keyword.discoverynewsshort}} 照会では、照会 1 個当たり $0.10 が課金されます。

**注:** ライト・プラン・サービスは、非アクティブ状態が 30 日間経過すると削除されます。ライト・プランでは、1 つの組織につき 1 つの無料環境が割り振られます。

 \* 文書制限では、ディスク上で平均 100KB の文書サイズを想定しています。これは、変換とエンリッチメント後の、コレクション内の文書のサイズのため、最初の入力時のサイズとは大幅に異なる可能性があります。保管文書の数、および使用済みストレージの合計量は、`environments` API または `collections` API を使用するか、ツールを使用して表示できます。

 \*\* 文書がディスク上で平均 100KB を超えている場合は、最大文書数制限に達する前にプランのストレージ制限に到達します。

 \*\*\* 料金は、1,000 個の文書群がサービス内に保管されている時間数に基づきます (「Thousand Document-Hour」と呼ばれます)。料金カリキュレーターでは、入力すべき数字は (`number of documents * number of hours those documents are stored in a month / 1000`) となります。

 \*\*\*\* 無料の使用量は、1 カ月間保管された文書に相当する量に基づきます。例えば、スタンダード・プランでは、無料の量は、2,000 文書 * 720 時間 / 1000 文書バッチ  = 1440 Thousand Document-Hours となります。

**例:** スタンダード・プランを使用するユーザーが、一カ月間に 4,000 文書を保管しました。この場合の料金は以下のように計算されます。

- `4000 documents * 720 hours (in a month) / 1000 = 2,880` Thousand Document-hours の消費

- `2,880 - 1,440 (free document hours) = 1,440` Thousand Document Hours が請求可能

- `1,440 * $0.0139` (Thousand Document Hour 当たりの料金) = 1 カ月間で `$20.00`

**注:** 各時間の請求量を計算する際の計算の一部として、保管されている文書の合計数は、最も近い 1,000に切り上げられます。例えば、4,678 個の文書を 1 時間保管している場合、合計数は 5,000 に切り上げられ、結果として 5 Thousand document-hours がアカウントに請求されます。

**注:** エンリッチメントに対する追加料金はありません。

{{site.data.keyword.Bluemix_notm}} セキュリティーについては、[{{site.data.keyword.Bluemix_notm}} Service Description ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=IBM+Bluemix+Service+Description){: new_window} を参照してください。

## 以前の料金プランからの変換

**2017 年 8 月 1 日**より前のプランに加入していたお客様は、いずれかの新規プランにマイグレーションされました。

- 30 日間の無料トライアル・プランを以前使用していたお客様は、**ライト**・プランにマイグレーションされました。この移行の結果として、既存のユーザーはライト・プランの制限 (文書数 _(2000)_、ストレージ _(200 Mb)_、またはコレクション数 _(2)_) に達しているか、超えている可能性があります。**ライト**・プランの制限を超えている場合は、追加コンテンツをサービスに追加することはできませんが、コレクションの照会は引き続き行うことができます。これらのすべての制限について、現在の状況を {{site.data.keyword.discoveryshort}} ツールまたは API を使用して確認できます。{{site.data.keyword.discoveryshort}} インスタンスへのコンテンツの追加を再開できるようにするには、以下のいずれかを実行する必要があります。
  - **ライト**・プランの制限を超えないように、コレクションと文書、またはそのいずれかを削除する。文書は、[delete-doc ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-doc){: new_window} メソッドを使用して API から個別に削除できます。コレクション全体の削除は、ツールを使用するか、[delete-collection ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-collection){: new_window} メソッドを使用して API から実行できます。
  - ストレージ必要量を満たすレベルにプランをアップグレードする。
- サイズ **`1`**、**`2`**、または **`3`** の環境のお客様は、自動的に**アドバンスト**・プランにマイグレーションされています。アドバンスト層に移動されたが、文書数が 100,000 個未満で、コレクション数が 4 個未満の場合は、コストを削減するためにスタンダード層に移動することができます。このためには、スタンダード・プラン内に新しい Discovery インスタンスを作成し、その新規インスタンスにデータを再び取り込む必要があります。取り込みは、ツール、API、または Data Crawler を使用して実行できます。

追加の料金情報については、[{{site.data.keyword.discoveryshort}} カタログ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window} を参照してください。
