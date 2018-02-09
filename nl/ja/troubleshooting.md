---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-18"

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

# トラブルシューティング

{{site.data.keyword.discoveryshort}} サービスの使用に関するトラブルシューティングのヒント

{{site.data.keyword.discoveryshort}} サービスの使用時に問題が発生した場合、以下のトラブルシューティングのヒントを 1 つ以上試してください。

-   現行文書内のデータと前に取り込まれた文書内の類似データとの間にタイプの不一致があるため、文書の取り込みが失敗することがあります。例えば、ある文書内で **date** タイプとされているフィールドが後続の文書では **string** である場合、その後続文書は正しく索引付けされません。

    プレビュー操作は、単一文書のみをテストし、変換結果の記録を保持しないため、タイプの不一致を予測できません。
-   文書の索引付けが高速または大規模な場合、バックエンド検索サービスが再始動することがあります。これが発生する場合は、{{site.data.keyword.IBM}} サポートに支援を依頼してください。
