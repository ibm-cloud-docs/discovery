---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-15"

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

# Element Classification
{: #element-classification}

Element Classification を使用すると、規定を記述した文書を迅速に解析して重要なエレメントを変換、識別、分類することができます。最先端の自然言語処理を利用して、パーティー (対象者)、ネーチャー (エレメントのタイプ)、およびカテゴリー (特定の種別) が文書のエレメントから抽出されます。

Element Classification は、以下を提供するように設計されています。

- ソフトウェア調達契約と規制文書に重点を置いた契約の自然言語理解
- プログラマチック PDF を注釈付き JSON に変換する機能
- 主題の専門知識に沿った法的なエンティティーとカテゴリーの識別

Element Classification では、機能が豊富な一連の組み込み自動化 Watson API を合わせて、プログラマチック PDF を入力し、セクション、リスト (番号および黒丸)、脚注、表を識別して、これらの項目を構造化された HTML 形式に変換します。さらに、この構造化形式の分類は、ラベル付きのエレメント、タイプ、およびカテゴリーを含む JSON として注釈付けして出力されます。

Element Classification は、送信時および保管時に暗号化を行って、データを安全に伝送します。IBM クラウドのセキュリティーについては、[IBM クラウド・サービス記述書 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=IBM+Bluemix+Service+Description){: new_window} を参照してください。

## 分類の要件

Element Classification を使用して文書を分類するには、構成文書とソース文書が以下の要件を満たしている必要があります

- 分析されるファイルは PDF 形式です。
- PDF のコンテンツはテキスト形式です (スキャン済みだが OCR 処理されていない文書は解析できません)。

  **注:** PDF ビューアーで文書を開き、**「テキスト選択」**ツールを使用して 1 つの単語を選択することによって、PDF がテキストであるかを確認できます。文書内で 1 つの単語を選択できない場合、そのファイルは解析できません。

- ファイルのサイズは 50 MB 以下です。
- 保護された PDF (開くためにパスワードが必要) と編集制限付きの PDF (編集するためにパスワードが必要) は解析できません。
- `elements` エンリッチメントを含むカスタム {{site.data.keyword.discoveryshort}} 構成を作成する必要があります。この構成は、PDF 文書の取り込みにのみ使用できます。
- **ライト**・プランと**標準**プランでは、1 カ月当たり最大 500 ページを処理することができます。
- **プレミアム**・プランに登録されたサービス・インスタンスには使用できません。

## コレクションの要件

Element Classification を使用するには、以下の具体的な要件を満たすようにコレクションを構成する必要があります。

- `PDF` 変換設定は、指定された場合、無視されます。
- Element Classification が指定された場合 Microsoft Word ファイルは取り込めないため、`WORD` 変換設定は省略できます。
- `html` 正規化設定は、指定された場合、無視されます。
- `elements` エンリッチメントが指定された場合、文書分割はサポートされません。
- {{site.data.keyword.discoveryshort}} 構成で、`html` フィールドが `elements` エンリッチメントでエンリッチされ、`model` が `contract` と指定される必要があります。以下の例で、`destination_field` は `enriched_html` ですが、任意の有効な名前を使用できます。

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

これらのオプションは {{site.data.keyword.discoveryshort}} ツールを使用して追加できます。カスタム構成を作成し、**Element Classification** のエンリッチメントを `html` フィールドに追加します。

**注:** ツールを使用して **Element Classification** を追加すると、`destination_field` は `enriched_html_elements` に設定されます。

作成したカスタム構成は、どのコレクションでも使用できます。カスタム構成が指定されている限り、どの文書アップロード方法でも使用できます。コレクションの作成と文書のアップロードに精通していない場合は、[ツール入門](/docs/services/discovery/getting-started-tool.html)を参照してください。

## 分類されたエレメント

文書は、Element Classification で索引付けされると、検索可能な文書の一部として `elements` 配列を含んで戻されます。

`elements` 配列内の各オブジェクトは、契約の中で Element Classification が識別したエレメントを記述します。以下のコードは、標準的なエレメントを表しています。

```
{
   "sentence" : {
     "begin" : 34941,
     "end" : 35307
   },
   "sentence_text" : "A buyer must buy from the supplier.",
   "types" : [ {
     "label" : {
       "nature" : "Obligation",
       "party" : "Supplier"
     },
     "assurance" : "High"
   } ],
   "categories" : [ {
     "label : "Responsibilities",
     "assurance : "High"
     }
   ]
}
```

エレメントには、以下の 4 つの重要なセクションがあります。

- `sentence_text` - 分析されたテキスト。
- `sentence` - このオブジェクトは、変換された HTML 内でエレメントが検出された位置を記述します。開始文字の値と終了文字の値が含まれます。
- `types` – この配列は、エレメントが何であるか、誰に影響するかを記述します。`party` (この文の影響を受ける人) と `nature` (識別されたパーティーに文が与える影響) の 1 つ以上のセットから構成されます。
- `categories` – この配列は、識別された文が入る機能カテゴリーをリストします。文の主題。

**注**: どのタイプおよびカテゴリーにも入らない文もあります。その場合、`types` 配列と `categories` 配列は空で戻ります。

**注:** 複数のトピックに該当するために、複数の `types` と `categories` の項目がリストされて戻る文もあります。

さらに、識別されたパーティーは、parties 配列でも定義されます。

```
  "parties" : [ {
    "party" : "Customer",
    "role" : "Buyer"
  } ]
```

parties 配列の各エレメントには、次の 2 つの重要なセクションがあります。

- `party` – 文書内でパーティーとして識別されたテキスト。
- `role` – パーティーについて識別された役割。役割はサブドメインに基づいて変わります。可能な役割のリストについては、指定されたサブドメインの情報を参照してください。特定の役割に識別できないパーティーには、「Unknown」というラベルが付けられます。


## 契約のエレメントの概要

Element Classification で解析された契約は、分析で識別された各エレメントとともに戻されます。

以下のセクションでは、戻された JSON で分析がどのように記述されるかについて説明します。

### タイプ

エレメント `types` の情報は、当該エレメントに識別された nature と party の対を含むオブジェクトの配列です。以下の表で、識別可能な `nature` と `party`の値について説明します。

ネーチャー (nature) は、文で要求されるアクションのタイプです。

| **nature**| **説明**|
| --- | --- |
| Definition | このエレメントは、用語/関係などを明確化します。このエレメントの履行にアクションは不要で、影響を受けるパーティーはありません。|
| Disclaimer | エレメント内のパーティーは、エレメント内の特定の条件を履行する義務はありませんが、それを禁止されてはいません。|
| Exclusion | エレメント内のパーティーは、エレメントに提示された特定の条件を履行しません。|
| Obligation | エレメント内のパーティーは、エレメントの条件の履行が要求されます。|
| Right | エレメント内のパーティーは、エレメントの条件の受理が保証されます。|

### パーティー

識別された各節について、影響を受けるパーティーは名前で識別されます。その後、識別された各パーティーは、`role` で分類されます。パーティーとは、契約内の当事者です。契約について識別できる役割 (role) は以下のとおりです。

| **role** | **説明**|
| --- | --- |
| `Buyer` | 商品/サービスの代金支払いに責任を持つパーティー。|
| `End User` | Buyer と明確に区別された、実際の商品/サービスと関わり合うパーティー。|
| `None` | このエレメントにパーティーが識別されていません。Definition の nature と常に対で使用されます。|
| `Supplier` | 商品/サービスの提供に責任を持つパーティー。|

### カテゴリー

カテゴリーは、文の主題を定義します。以下のカテゴリー (categories) を識別できます。

| **categories**| **説明**|
| --- | --- |
| `Amendments` | 条件を変更する状況を規定した、元の契約の修正。|
| `Asset Use` | いずれかのパーティーが使用する、合意内の資産の詳細。|
| `Assignments` | パーティーが保有する権利を別のパーティーに移すことに関して記述します。|
| `Audits` | この節は、購入者が、提供されるサービスの提供業者を調査または検査できるようにします。|
| `Communication` | 可能な連絡方法と連絡先情報を記述します。|
| `Confidentiality` | 機密情報または秘密情報の取り扱い方法 (誰が何をどう共有できるかなど) を記述します。|
| `Business Continuity` | 中断インシデントの発生時に、事前定義されたレベルでどのように業務を継続するかを記述します。|
| `Definitions` | 文書で使用される用語を定義するセクション。|
| `Deliverables` | 1 つの作業の終了時に提供される項目またはサービス。|
| `Delivery` | プロジェクトを完了するための具体的なスケジュールまたはプロセス。|
| `Dispute Resolution` | 契約パーティー間で発生する紛争とその対応方法を規定します。|
| `Force Majeure` | 中断事象の発生時に、両方のパーティーを免責する節。|
| `Indemnification` | 条件に違反した場合の救済または結果を記述します。|
| `Insurance` | 提供業者が保持する必要がある保険の補償範囲のレベルを記述します。|
| `Intellectual Property` | 特許、著作権、および商標に関する節。一般的には、創案、著者、ノウハウに関係します。|
| `Liability` | 各パーティーの責任に関する義務および制限を記述します。|
| `Miscellaneous` | 他のカテゴリーに適合しない利害関係のセクション。|
| `Payment Terms & Billing` | 支払いの期限およびスケジュールを記述します。|
| `Pricing & Taxes` | 価格の構成方法と税金の適用方法を記述します。|
| `Privacy` | 適用されるプライバシー規定を記述します。|
| `Responsibilities` | 各パーティーの責務を記述します。|
| `Safety and Security` | パーティーへの危害の防止方法を記述します。人と物理資産の両方の安全を含みます。|
| `Scope of Work` | 作業指示書で詳述されたパーティーの遂行内容を記述します。|
| `Subcontracts` | 要件の履行に関与する第三者に関連します。|
| `Term & Termination` | 対象とする期間と終了条件。|
| `Warranties` | 商品の動作に関する提供業者による保証。|

### アシュアランス

Element Classification によって識別されるすべての項目 (タイプまたはカテゴリー) に `assurance` のレーティングが示されます。アシュアランス (assurance) に可能な値を以下に説明します。

| **assurance** | **説明**|
| --- | --- |
| `High` | 示された分類が内容を表していることを支持する重大な証拠があります。|
| `Low` | 分類を支持する証拠がいくつかありますが、確認のためにさらに検討が必要な場合があります。|
