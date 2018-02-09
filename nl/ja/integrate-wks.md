---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-15"

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

# Watson Knowledge Studio との統合

{{site.data.keyword.knowledgestudiofull}} のカスタム・モデルを {{site.data.keyword.discoveryshort}} サービスと統合して、カスタムのエンティティーおよび関係のエンリッチメントを提供することができます。
{: shortdesc}

これにより、業界や科学的専門分野など、特定のフォーカス領域に固有の情報を使用して、{{site.data.keyword.discoveryshort}} サービスの文書拡張機能を柔軟に適用することができます。エンリッチメント・モデルでは、公開データとユーザーが所有するデータの両方を使用できます。

{{site.data.keyword.knowledgestudioshort}} モデルを {{site.data.keyword.discoveryshort}} サービスに統合するには、サービス API または {{site.data.keyword.discoveryshort}} ツールを使用することができます。

## 始めに

{{site.data.keyword.knowledgestudioshort}} のカスタム・モデルを {{site.data.keyword.discoveryshort}} サービスと統合するには、その前に、{{site.data.keyword.knowledgestudioshort}} を使用してそのモデルを作成してデプロイしておく必要があります。モデルの作成およびデプロイについては、[{{site.data.keyword.knowledgestudioshort}} の資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.bluemix.net/docs/services/knowledge-studio/tutorials-create-project.html#wks_tutintro){: new_window} を参照してください。デプロイされたモデルを {{site.data.keyword.discoveryshort}} サービスと統合するには、そのモデルの固有 ID が必要です。

## API を使用したカスタム・モデルの統合

1.  [List environments ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_environments){: new_window} に説明されている方法で、{{site.data.keyword.discoveryshort}} 環境の ID を入手します。その環境 ID を書き留めます。
1.  [List configurations ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_configurations){: new_window} に説明されている方法で、1 つ以上の {{site.data.keyword.discoveryshort}} 現行構成の ID をリストします。{{site.data.keyword.knowledgestudiofull}} カスタム・モデルと統合する構成の ID を書き留めます。
1.  bash シェルまたは同等のもの (Windows 用の Cygwin など) で以下のコマンドを実行して、{{site.data.keyword.discoveryshort}} 現行構成のコピーをダウンロードします。`{environment_id}` と `{configuration_id}` は、前の 2 つのステップで書き留めた ID に置き換えてください。

    ```bash
    curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-11-07" > my_config.json
    ```
    {: pre}

このコマンドでは、コレクション・ファイルの内容をリストして、それらを JSON ファイル `my_config.json` に入れます。
1.  テキスト・エディターで `my_config.json` ファイルを開き、以下の変更を行います。
    1.  `"name"` フィールドの値を新しい構成の目的を示す値に変更します。オプションで、`"description"` フィールドの値も変更できます。

        ```json
        ...
        "name": "wks-config",
        "description": "This is a configuration to use with a WKS model",
        ...
        ```
        {: codeblock}

    1.  {{site.data.keyword.knowledgestudioshort}} モデルの情報を使用して、エンリッチメント・フィールドを更新します。当初、エンリッチメント・フィールドが以下のとおりであったとします。

        ```json
        "enrichments": [
        {
            "source_field": "text",
            "destination_field": "enriched_text",
            "enrichment": "natural_language_understanding",
            "options": {
                "features": {
                    "entities": {
                        "sentiment": true,
                        "emotion": false,
                        "limit": 50
                    },
                    "sentiment": {
                        "document": true
                    },
                    "categories": {},
                    "concepts": {
                        "limit": 8
                    },
                    "relations": {}
                }
            }
        }]
        ```
        {: codeblock}

    1.  `{watson_knowledge_studio_model_ID}` を「始めに」で説明した {{site.data.keyword.knowledgestudioshort}} モデルの固有 ID に置き換え、ファイルを次のように更新します。

        ```json
        "enrichments": [
        {
            "source_field": "text",
            "destination_field": "enriched_text",
            "enrichment": "natural_language_understanding",
            "options": {
                "features": {
                    "entities": {
                        "sentiment": true,
                        "emotion": false,
                        "limit": 50,
                        "model": "{watson_knowledge_studio_model_ID}"
                    },
                    "sentiment": {
                        "document": true
                    },
                    "categories": {},
                    "concepts": {
                        "limit": 8
                    },
                    "relations": {
                      "model": "{watson_knowledge_studio_model_ID}"
                    }
                }
            }
        }]
        ```
        {: codeblock}

1.  オプションで、[エンティティーを正規化するカスタム構成の作成](/docs/services/discovery/normalize-entities.html)に説明されているように、エンティティーの正規化を有効にします。
1.  `my_config.json` ファイルを保存します。
1.  次のステップを実行する前に、[JSLint ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://jslint.com){: new_window} などの JSON バリデーターを使用して、編集した JSON を検証し、必要であれば修正します。
1.  以下のようにして構成を更新します。この手順の最初に収集した `{environment_id}` と `{configuration_id}` の ID が再び必要になります。

    ```bash
    curl -X PUT -u "{username}":"{password}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-11-07"
    ```
    {: pre}

    **注:** 新しい構成を作成する場合やデフォルト構成を変更する場合は、既存の構成を更新するのではなく、新しいカスタム構成を作成する必要があります。新しい構成を作成する前に、`my_config.json` ファイルから `"configuration_id":` フィールドが削除されていることを確認し、以下のコマンドを実行します。

    ```bash
    curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07"
    ```
    {: pre}

    両方のコマンドは、更新された構成ファイルの内容を返します。

## Discovery ツールを使用したカスタム・モデルの統合

{{site.data.keyword.discoveryshort}} ツールを使用して、{{site.data.keyword.knowledgestudioshort}} カスタム・モデルを [エンティティー抽出 (Entity Extraction) ](/docs/services/discovery/building.html#entity-extraction)エンリッチメントまたは[関係抽出 (Relation Extraction) ](/docs/services/discovery/building.html#relation-extraction)エンリッチメントに統合することができます。

1. {{site.data.keyword.knowledgestudioshort}} モデルの `Model ID` を取得します。
1. {{site.data.keyword.discoveryshort}} ツールで、**「データの管理 (Manage data)」**画面を開き、コレクションを作成するか開き、新規構成を作成します。
1. **「エンリッチメントの追加 (Add enrichments)」**をクリックし、**「エンティティー抽出 (Entity Extraction)」**エンリッチメントまたは**「関係抽出 (Relation Extraction)」**エンリッチメントのいずれかを選択します。
1. 選択したエンリッチメントの「`Custom Model ID`」ボックスに「`Model ID`」を入力します。カスタム {{site.data.keyword.knowledgestudiofull}} モデルが、そのエンリッチメントのデフォルトをオーバーライドします。**「適用」**をクリックし、次に**「完了」**をクリックします。

文書はデータ・コレクションにアップロードされると、そのコレクション用に選択された構成ファイルを使用して変換およびエンリッチされます。文書がアップロードされた後で既存のコレクションを新規構成ファイルに切り替えると、アップロードされたそれらの文書は、引き続き元の構成ファイルによって変換されます。構成ファイルの切り替え後にアップロードされた文書はすべて、新規構成ファイルを使用します。コレクション**全体**で新規構成ファイルを使用したい場合は、新しいコレクションを作成し、その新規構成ファイルを選択し、すべての文書を再アップロードする必要があります。

**注:** 1 つのエンリッチメントに割り当てられるのは、1 つの {{site.data.keyword.knowledgestudiofull}} モデルのみになります。

## 次のステップ

{{site.data.keyword.discoveryshort}} サービスを新規構成で使用して、プライベート・データを取り込みます。更新された構成を使用して取り込んだ文書は、カスタム・モデルのデータによって自動的にエンリッチされます。
