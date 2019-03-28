---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-01-10"

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

# 機密保護
{: #information-security}

IBM は、お客様やパートナーに、データ・プライバシー、セキュリティー、およびガバナンスに関する革新的なソリューションを提供することに努めています。
{: shortdesc}

**注意:**
お客様自身が欧州連合の一般データ保護規則を含む各種法令を遵守するために必要な措置を講ずるのはお客様の責任です。 お客様のビジネスに影響を及ぼす可能性のある関連法令の特定およびそれらの解釈、ならびにかかる関連法令を遵守するためにお客様が講ずるべき必要措置に関する助言は、お客様の責任により適格な弁護士から得るものとします。

本書に記載の製品、サービス、および他の機能が、すべてのお客様の状況に適しているとは限らず、使用する際に制約を受ける場合があります。 IBM は、法律、会計または監査に関する助言を提供することはしませんし、IBM のサービスまたは製品が、お客様のあらゆる法令遵守の裏付けとなる表明または保証もいたしません。

以下の場所で作成された {{site.data.keyword.cloud}} {{site.data.keyword.watson}} リソースの GDPR サポートを要請する必要がある場合の手順

-   EU 内の場合、[EU で作成された IBM Cloud Watson リソースのサポートの要求 (Requesting support for IBM Cloud Watson resources created in the European Union)](/docs/services/watson/getting-started-gdpr-sar.html#request-EU) を参照してください。
-   EU 外の場合、[EU 外でのリソースのサポートの要求 (Requesting support for resources outside the European Union)](/docs/services/watson/getting-started-gdpr-sar.html#request-non-EU) を参照してください。

## EU 一般データ保護規則 (GDPR)
{: #gdpr}

IBM は、お客様やパートナーに、データ・プライバシー、セキュリティー、およびガバナンスに関する革新的なソリューションを提供して、GDPR  に対する準拠が完了するまでの過程を支援することに努めています。

GDPR に対する準備を整えるための IBM 独自の過程と、準拠が完了するまでの過程をサポートする弊社の GDPR 機能とオファリングについて詳しくは、[ここ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/gdpr){: new_window} を参照してください。

## {{site.data.keyword.discoveryshort}} でのデータのラベル付けと削除
{: #gdpr-discovery}

{{site.data.keyword.discoveryshort}} サービスには、呼び出しごとにデータにラベルを付けるための API が含まれています。

この API により、以下のようなことが可能になります。

- データに顧客 ID をラベル付けする。
- 特定の顧客 ID のすべてのデータ (関連する通知を含む) を削除する。

データには、任意の `customer_id` ([データのラベル付け方法](/docs/services/discovery?topic=discovery-information-security#labeling) の制限を参照) をオプションの `X-Watson-Metadata` ヘッダーに追加することでラベルが付けられます。 これにより、{{site.data.keyword.discoveryshort}} は、`customer_id` を使用してデータを削除できます。

任意の REST 呼び出しで、オプションのヘッダー `X-Watson-Metadata` を、セミコロンで区切った `field=value` のペアを指定して送信できます。現時点では `customer_id` のみが保持されます。 その `customer_id` を `X-Watson-Metadata` ヘッダーに追加することにより、要求には、この `customer_id` に属するデータが含まれていることが示されます。

`customer_id` は、単一の {{site.data.keyword.discoveryshort}} サービス・インスタンス内で固有です。 これらは、環境またはコレクションごとに固有ではありません。 個人データを含めることはできません。

**注:** 試験およびベータの機能は、実稼働環境での使用を意図していないため、データのラベル付けおよび削除時に期待どおりに機能することは保証されません。 データのラベル付けと削除を必要とするソリューションを実装する場合は、試験およびベータの機能を使用しないでください。

## データのラベル付けをサポートするメソッド
{: #pi_methods}

関連付けられたメソッドを使用して情報が最初に追加されたときに `customer_id` が指定された場合、`customer_id`を使用して以下の保管された情報を削除できます。

- 照会 (`/v1/environments/{environment_id}/collections/{collection_id}/query`) `passages` パラメーターまたは `natural_language_query` パラメーターと共に使用した場合のみ
- イベント (`/v1/events`)
- 文書 (`/v1/environments/{environment_id}/collections/{collection_id}/documents`)
- 通知 (`/v1/environments/{environment_id}/collections/{collection_id}/notices`) 取り込み `notices` のみにラベルが付けられます。
- Knowledge Graph エンティティー (`/v1/environments/{environment_id}/collections/{collection_id}/query_entities`)
- Knowledge Graph 関係 (`/v1/environments/{environment_id}/collections/{collection_id}/query_relations`)
- トレーニング・データ (`/v1/environments/{environment_id}/collections/{collection_id}/training_data`)

以下の保管された情報は明示的にラベル付けされず、`customer_id` を指定して削除することはできません。 これらのフィールドでは個人データはサポートされていません。

以下の保管項目のストリング・フィールド (`name` および `description` を含みますが、これに限定されるものではありません) が該当します。
- 構成
- コレクション
- 環境

## データのラベル付け
{: #labeling}

文書の取り込み時に、`POST /v1/environments/{environment_id}/collections/{collection_id}/documents` または `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/ID` 操作を使用して `X-Watson-Metadata` ヘッダーを組み込みます。 `customer_id` フィールドが、文書の `extracted_metadata` に追加されます。 操作の実行時に `X-Watson-Metadata` ヘッダーに `customer_id` を提供するようにアプリケーションを構成する必要があります。

オプションで、`X-Watson-Metadata` ヘッダーを使用する代わりに、`customer_id` フィールドを `metadata` マルチパート・フォーム・パーツに組み込むことができます。

**注:** 文書が既に取り込まれている場合は、それらを再取り込みして `X-Watson-Metadata` ヘッダーと `customer_id` を追加する必要があります。

**注:** `metadata` マルチパート・フォーム・パーツで `customer_id` を指定し、同じ文書の `X-Watson-Metadata` ヘッダーを指定すると、`X-Watson-Metadata` ヘッダーの `customer_id` が使用されます。

制約事項:

- `X-Watson-Metadata` ヘッダーの値は、4 キロバイトのテキストを超えることはできません。
- `X-Watson-Metadata` ヘッダーには、`field = value` ペアのセミコロン区切りリストが含まれている必要があります。 `field` と `value` には、セミコロン (`;`) または等号 (`=`) を含めることはできません。
- `customer_id` は、各 {{site.data.keyword.discoveryshort}} インスタンス内で固有です。 これらは、環境またはコレクションごとに固有ではありません。
- `customer_id` の長さは 256 文字を超えることはできません。
- `customer_id` に空白文字のみが含まれているか、完全に空の場合、`customer_id` がまったく指定されていないかのように扱われ、エラー・メッセージは返されません。

### Discovery ツールによるデータのラベル付け
{: #labelingtooling}

{{site.data.keyword.discoveryshort}} ツールを使用する場合、`customer_id` フィールドでデータにラベルを付けることができます。 ![環境詳細](images/env_icon.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> をクリックし、**「GDPR データ・ラベル」**フィールドに `customer_id` を入力します。このフィールドが設定されると、このブラウザー・セッションを使用してアップロードされたすべてのデータに、指定された `customer_id` のラベルが付けられます。関連付けられた顧客 ID が変更された場合は、このフィールドを手動で変更する必要があります。

**「GDPR データ・ラベル」**フィールドを使用して `customer_id` を追加すると、その URL ドメイン内の文書、通知、ナレッジ・グラフ・エンティティー、ナレッジ・グラフ関係、およびトレーニング・データが、そのドメインの下の各インスタンスも含めて、その時点以降にラベル付けされます。 **「GDPR データ・ラベル」**フィールドを追加する前に {{site.data.keyword.discoveryshort}} ツールで発生したアクション (文書のアップロードを含む) は、ラベル付けされません。

**注:** {{site.data.keyword.discoveryshort}} ツールの**「GDPR データ・ラベル」**フィールドを使用して `customer_id` を指定した後にドメイン、ブラウザー、空のブラウザー・キャッシュを切り替えるか、匿名セッションを開始すると、`customer_id` は保持されず、データにラベルは付けられません。 ドメインまたはブラウザーを切り替える必要がある場合は、**「GDPR データ・ラベル」**フィールドに `customer_id` を再入力します。

### Data Crawler を使用した文書のラベル付け
{: #labelingdc}

Data Crawler を使用して文書がクロールされている場合は、それらを再クロールして `X-Watson-Metadata` ヘッダーと `customer_id` を追加する必要があります。

1. {{site.data.keyword.discoveryshort}} Data Crawler 出力アダプター構成を更新して、`customer_id`を含めます。 [出力アダプターの構成](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#output-adapter)を参照してください。
1. クロールをスケジュールします。 文書は `X-Watson-Metadata` ヘッダーを使用して {{site.data.keyword.discoveryshort}} に送信され、文書には構成された `customer_id` のラベルが付けられます。

## ラベル付きデータの削除
{: #deletingdata}

後でデータを削除するには、データに `customer_id` のラベルを付ける必要があります。

1. `DELETE /v1/user_data` 操作を使用して、削除するデータの `customer_id` を指定します。 `DELETE /v1/user_data` は、[データのラベル付けをサポートするメソッド](/docs/services/discovery?topic=discovery-information-security#pi_methods)で指定されているように、そのサービス・インスタンス内の特定の `customer_id` に関連付けられたすべてのデータを削除します。 [API リファレンス![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery#delete-labeled-data){: new_window}も参照してください。

削除は非同期で実行されます。 削除の進行状況は追跡できません。

ラベル付きのすべてのコンテンツを正常に削除するには、環境内のすべてのコレクションの `processing` カウントと `pending` カウントが `0` を返してから `user_delete` を実行する必要があります。

存在しない `customer_id` が指定された場合、何も削除されませんが、`200 - OK` 応答が返されます。

環境またはコレクションを作成する要求に `X-Watson-Metadata` ヘッダーが含まれていても、環境およびコレクションには `customer_id` のラベルは付きません。 環境内のコレクション内の個々の文書のみにラベルが付けられます。 したがって、データが削除されても、個々の環境およびコレクションは削除されません。

{{site.data.keyword.discoveryshort}} ツールを使用してラベル付きデータを削除することはできません。
