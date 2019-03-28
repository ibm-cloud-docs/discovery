---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-01-15"

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

# Element Classification
{: #element-classification}

要素の分類を使用すると、管理文書全体を迅速に解析して、重要な要素を変換、識別、分類することができます。 最先端の自然言語処理を利用して、パーティー (対象者)、ネーチャー (要素のタイプ)、およびカテゴリー (特定の種別) が文書の要素から抽出されます。

要素の分類は、以下を提供するように設計されています。

-  ソフトウェア調達契約に重点を置いた契約の自然言語理解
-  プログラマチック PDF を注釈付き JSON に変換する機能
-  主題の専門知識に沿った法的なエンティティーとカテゴリーの識別

要素の分類では、機能が豊富な一連の組み込み自動化 Watson API を合わせて、プログラマチック PDF を入力し、セクション、リスト (番号および黒丸)、脚注、表を識別して、これらの項目を構造化された HTML 形式に変換します。 さらに、この構造化形式の分類は、ラベル付きの要素、タイプ、およびカテゴリーを含む JSON として注釈付けして出力されます。

要素の分類は、送信時および保管時に暗号化を行って、データを安全に伝送します。 IBM Cloud のセキュリティーについては、[{{site.data.keyword.Bluemix_notm}}サービス記述書 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=%28IBM+Cloud+Service+description%29){: new_window} を参照してください。

要素の分類は、以下を含んでいる JSON オブジェクトを返します。

-  入力文書のタイトル、入力文書の HTML 版、および入力文書の MD5 ハッシュが含まれる、`documents` オブジェクト。
-  入力文書を分類するために使用されたモデルに関する情報。  
-  入力文書内で識別されたセマンティック要素を詳述する `elements` 配列。
-  入力文書内で識別された表を細分化する `tables` 配列。
-  入力文書内で識別されたセクション・タイトルとリード文をリストする `document_structure` オブジェクト。
-  入力文書内で識別されたパーティーと、パーティーの役割、住所、および連絡先をリストする `parties` 配列。
-  `effective_dates`、`contract_amounts`、および `termination_dates` を定義する配列。

この機能は現在は英語でのみサポートされています。詳しくは、『[言語サポート](/docs/services/discovery?topic=discovery-language-support#feature-support)』を参照してください。


## 分類の要件
{: #element-class}

要素の分類を使用して文書を分類するには、構成文書とソース文書が以下の要件を満たしている必要があります

-  分析されるファイルは PDF 形式です。
-  PDF コンテンツはテキスト形式です。 スキャンされた文書は、OCR 処理されている場合でも解析できません。
   **注:** PDF ビューアーで文書を開き、**「テキスト選択」**ツールを使用して 1 つの単語を選択することによって、PDF がテキストであるかを確認できます。 文書内で 1 つの単語を選択できない場合、そのファイルは解析できません。
-  ファイルのサイズは 50 MB 以下です。
-  保護された PDF (開くためにパスワードが必要) と編集制限付きの PDF (編集するためにパスワードが必要) は解析できません。
-  {{site.data.keyword.discoveryshort}} ツールに、PDF 文書のコレクションをエンリッチするために使用できる、**Default Contract Configuration** という名前の構成が含まれています。 `elements` エンリッチメントを含んでいるカスタム構成を作成するというオプションもあります。 詳しくは、『[コレクションの要件](/docs/services/discovery?topic=discovery-element-classification#element-collection)』を参照してください。
-  **ライト**・プランでは、1 カ月当たり最大 500 ページを処理することができます。
-  **専用**環境では使用できません。
-  要素の分類の使用時には、エンリッチメント後の正規化を実行することはできません。

**注:** **Default Contract Configuration** ファイルは、2018 年 9 月 25 日に更新されました。 この日付よりも前にこの構成をコレクションに適用した場合、コレクションの更新について『[リリース・ノート](/docs/services/discovery?topic=discovery-release-notes#25sept)』を参照してください。

## コレクションの要件
{: #element-collection}

要素の分類を使用するには、特定の要件を満たすようにコレクションが構成されている必要があります。

{{site.data.keyword.discoveryshort}} ツールに、**要素の分類**エンリッチメントおよび他の必要なオプションで PDF 文書をエンリッチするために事前構成されている、**Default Contract Configuration** という名前の構成が含まれています。 コレクションを作成するときに、この構成を選択できます。 この構成の JSON は次のとおりです。

```json
 {
   "name": "Default Contract Configuration",
   "description": "Extract party, nature, and category from elements in PDFs.",
  "conversions": {
     "html": {
       "exclude_tags_completely": [],
       "exclude_tags_keep_content": []
     }
   },
   "enrichments": [
     {
       "source_field": "html",
       "destination_field": "enriched_html_elements",
       "enrichment": "elements",
       "options": {
         "model": "contract"
    }
     }
   ]
 }
```
{: codeblock}

カスタム構成ファイルを作成する場合は、以下の要件を満たすようにコレクションを構成します。  

-  `PDF` 変換設定は、指定された場合、無視されます。
-  要素の分類が指定された場合 Microsoft Word ファイルは取り込めないため、`WORD` 変換設定は省略できます。
-  `html` 正規化設定は、指定された場合、無視されます。
-  `elements` エンリッチメントが指定されている場合、文書のセグメンテーションはサポートされません。
-  {{site.data.keyword.discoveryshort}} 構成で、`html` フィールドが `elements` エンリッチメントでエンリッチされ、`model` が `contract` と指定される必要があります。 以下の例で、`destination_field` は `enriched_html` ですが、任意の有効な名前を使用できます。

```json
 "enrichments": [
   {
     "source_field": "html",
    "destination_field": "enriched_html",
    "enrichment": "elements",
    "options": {
       "model": "contract"
    }
   }
 ]
```
{: codeblock}

ツールで `Default Contract Configuration` を選択した後、文書をアップロードできます。 コレクションの作成と文書のアップロードに精通していない場合は、[ツール入門](/docs/services/discovery?topic=discovery-getting-started#getting-started)を参照してください。

## 分類された要素
{: #classified-elements}

文書は、要素の分類で索引付けされると、検索可能な文書の一部として `elements` 配列を含んで戻されます。

`elements` 配列内の各オブジェクトは、契約の中で {{site.data.keyword.discoveryshort}} が識別した要素を記述します。 以下のコードは、標準的な要素を表しています。

```json
 {
    "location" : {
     "begin" : 134323,
     "end" : 135109
    },
    "text" : "9. In the event that the Participant's total vested account balance is determined to be less than or equal to $2,000.00 as of the date that the Order is received, the parties will be informed in writing that the QDRO determination fee may potentially liquidate the account.",
   "types" : [ {
      "label" : {
        "nature" : "Obligation",
        "party" : "All Parties"
      },
      "provenance_ids" : ["Nlu0ogWAEGms4vjhhzpMv3iXhm8b8fBqMBNtT/bXH8JI=", "PlyERkjg5is36RpFjVUFXp69eDmGmCxLCXRs1sDMDUCo="
      ]
    } ],
   "categories" : [ {
      "label" : "Communication",
      "provenance_ids" : [ "Cs38YyU6VBFtJK1/bgtEJBlqqWmX5F6OYUciRxQXf7HrN5TOCPuI7QXbkbj4LRXoxVuB3/i9H15q5TU+vFxorhUBeWFfF998OYQiPYViD2yI="
      ]
    } ],
    "attributes" : [ {
      "type" : "Currency",
      "text" : "$2,000.00",
      "location" : {
        "begin" : 134780,
        "end" : 134789
      }
    } ]
 }
 ```
{: codeblock}

各要素には、以下の 5 つの重要なセクションがあります。
-  `location`: 入力文書内の要素の位置を示す `begin` 索引と `end` 索引。
-  `text`: 分類された要素のテキスト。
-  `types`: ゼロ個以上の `label` オブジェクトを含む配列。 各 `label` オブジェクトには、識別されたパーティーへの要素の影響 (例: `Right` や `Exclusion`) をリストする `nature` フィールドと、要素の影響を受けるパーティーを識別する `party` フィールドが含まれます。 追加情報については、[契約の解析](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing)の『[タイプ](/docs/services/discovery?topic=discovery-contract_parsing#contract_types)』を参照してください。
-  `categories`: ゼロ個以上の `label` オブジェクトを含む配列。 各 `label` オブジェクトの値は、識別された要素が属している機能カテゴリーを示します。 追加情報については、[契約の解析](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing)の『[カテゴリー](/docs/services/discovery?topic=discovery-contract_parsing#contract_categories)』を参照してください。
-  `attributes`: 要素の属性を定義するゼロ個以上のオブジェクトがリストされた配列。 現在サポートされている属性タイプには、`Location` (要素によって参照されている地理的位置)、`DateTime` (要素によって指定されている日付、時刻、日付範囲、または時刻範囲)、および `Currency` (通貨価値と通貨単位) があります。 `attributes` 配列内の各オブジェクトには、識別された要素のテキストおよび位置も含まれます。位置は入力文書内のテキストの `begin` 索引と `end` 索引によって定義されます。 追加情報については、[契約の解析](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing)の『[属性](/docs/services/discovery?topic=discovery-contract_parsing#attributes)』を参照してください。

さらに、`types` 配列および `categories` 配列内の各オブジェクトには、`provenance_ids` 配列が含まれます。 `provenance_ids` 配列にリストされた値はハッシュ値であり、これを IBM に送信して、フィードバックを提供したり、要素と関連した分析部分についてのサポートを受けたりすることができます。 

センテンスによっては、どのようなタイプにもカテゴリーにも分類されないものもあります。その場合、このサービスは、`types` 配列と `categories` 配列を空オブジェクトとして返します。
{: note}

センテンスによっては、複数のトピックを扱っているものもあります。その場合、このサービスは、`types` オブジェクトと `categories` オブジェクトのセットを複数返します。
{: note}

センテンスによっては、識別可能な属性を含んでいないものもあります。その場合、このサービスは、`attributes` 配列を空オブジェクトとして返します。
{: note}
