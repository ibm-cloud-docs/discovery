---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-01-08"

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

# Watson Knowledge Studio との統合
{: #integrating-with-wks}

{{site.data.keyword.knowledgestudiofull}} の 1 つ以上のカスタム・モデルを {{site.data.keyword.discoveryshort}} サービスと統合して、エンティティーおよび関係のカスタム・エンリッチメントを提供することができます。
{: shortdesc}

これにより、業界や科学的専門分野など、特定のフォーカス領域に固有の情報を使用して、{{site.data.keyword.discoveryshort}} サービスの文書拡張機能を柔軟に適用することができます。 エンリッチメント・モデルでは、公開データとユーザーが所有するデータの両方を使用できます。

{{site.data.keyword.knowledgestudioshort}} モデルを {{site.data.keyword.discoveryshort}} サービスに統合するには、サービス API または {{site.data.keyword.discoveryshort}} ツールを使用することができます。

## 始めに
{: #wks-beforeintegration}

{{site.data.keyword.knowledgestudioshort}} のカスタム・モデルを {{site.data.keyword.discoveryshort}} サービスと統合するには、その前に、{{site.data.keyword.knowledgestudioshort}} を使用してそのモデルを作成してデプロイしておく必要があります。 モデルの作成およびデプロイについては、[{{site.data.keyword.knowledgestudioshort}} の資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/docs/services/knowledge-studio/tutorials-create-project.html#wks_tutintro){: new_window} を参照してください。 デプロイされたモデルを {{site.data.keyword.discoveryshort}} サービスと統合するには、そのモデルの固有 ID が必要です。

## API を使用したカスタム・モデルの統合
{: #integrate-customAPI}

1.  [List environments ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery#list_environments){: new_window} に説明されている方法で、{{site.data.keyword.discoveryshort}} 環境の ID を入手します。 その環境 ID を書き留めます。
1.  [List configurations ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/discovery#list_configurations){: new_window} に説明されている方法で、1 つ以上の {{site.data.keyword.discoveryshort}} 現行構成の ID をリストします。{{site.data.keyword.knowledgestudiofull}} カスタム・モデルと統合する構成の ID を書き留めます。
1.  bash シェルまたは同等のもの (Windows 用の Cygwin など) で以下のコマンドを実行して、{{site.data.keyword.discoveryshort}} 現行構成のコピーをダウンロードします。 `{environment_id}` と `{configuration_id}` は、前の 2 つのステップで書き留めた ID に置き換えてください。

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-11-07" > my_config.json
    ```
    {: pre}

    このコマンドでは、コレクション・ファイルの内容をリストして、それらを JSON ファイル `my_config.json` に入れます。
1.  テキスト・エディターで `my_config.json` ファイルを開き、以下の変更を行います。
    1.  `"name"` フィールドの値を新しい構成の目的を示す値に変更します。 オプションで、`"description"` フィールドの値も変更できます。

        ```json
        ...
        "name": "wks-config",
        "description": "This is a configuration to use with a WKS model",
        ...
        ```
        {: codeblock}

    1.  {{site.data.keyword.knowledgestudioshort}} モデルの情報を使用して、エンリッチメント・フィールドを更新します。 当初、エンリッチメント・フィールドが以下のとおりであったとします。

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

        API を使用する場合は、複数のカスタム・モデルを同一のフィールドに適用できます。[複数のカスタム・モデルの統合](/docs/services/discovery?topic=discovery-integrating-with-wks#integrate-multiplecustom)で例を参照してください。If you are also incorporating [Watson {{site.data.keyword.discoveryshort}} Knowledge Graph](/docs/services/discovery?topic=discovery-kg#kg) も取り込む場合は、単一のエンリッチメント・オブジェクトのエンティティーと関係の両方のエンリッチに同じモデルを使用する必要があります。
        {: note}

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

1.  `my_config.json` ファイルを保存します。
1.  次のステップを実行する前に、[JSLint ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://jslint.com){: new_window} などの JSON バリデーターを使用して、編集した JSON を検証し、必要であれば修正します。
1.  以下のようにして構成を更新します。 この手順の最初に収集した `{environment_id}` と `{configuration_id}` の ID が再び必要になります。

    ```bash
    curl -X PUT -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-11-07"
    ```
    {: pre}

    **注:** 新しい構成を作成する場合やデフォルト構成を変更する場合は、既存の構成を更新するのではなく、新しいカスタム構成を作成する必要があります。 新しい構成を作成する前に、`my_config.json` ファイルから `"configuration_id":` フィールドが削除されていることを確認し、以下のコマンドを実行します。

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07"
    ```
    {: pre}

    両方のコマンドは、更新された構成ファイルの内容を返します。

### 複数のカスタム・モデルの統合 
{: #integrate-multiplecustom}

API を使用して、複数のカスタム・モデルを同一のフィールドに適用できます。[API を使用したカスタム・モデルの統合
](/docs/services/discovery?topic=discovery-integrating-with-wks#integrate-customAPI)の手順に従い、この例をガイドとして使用してください。[Watson {{site.data.keyword.discoveryshort}} Knowledge Graph](/docs/services/discovery?topic=discovery-kg#kg) も取り込む場合は、単一のエンリッチメント・オブジェクトのエンティティーと関係の両方のエンリッチに同じモデルを使用する必要があります。
`"destination_field": "enriched_text"` の例をガイドとしてください。

{{site.data.keyword.discoveryshort}} ツールを使用して複数のカスタム・モデルを適用することはできません。カスタマイズできるのは、エンティティーおよび関係のエンリッチメントのみです。

同一 `source_field` ごとに異なる `destination_field` を指定する必要があります。さらに、各 `source_field` を固有モデルでエンリッチする必要があります。例えば、複数のカスタム・モデルを `text` の `source_field` に適用し、`model` `{watson_knowledge_studio_model_ID}` を `entities` エンリッチメントに適用する場合は、そのモデルを `entities` エンリッチメントに再使用してはなりません。
{: tip}


```json
   "enrichments": [
        {
        "source_field": "text",
            "destination_field": "enriched_text",
            "enrichment": "natural_language_understanding",
            "options": {
            "features": {
                "entities": {
                    "model": "{watson_knowledge_studio_model_ID}"
                },
                    "relations": {
                    "model": "{watson_knowledge_studio_model_ID}"
                    }
        }
    }
},
   {
        "source_field": "text",
        "destination_field": "enriched_text_2",
        "enrichment": "natural_language_understanding",
        "options": {
            "features": {
                "entities": {
                    "model": "{watson_knowledge_studio_model_ID_b}"
            },
                    "relations": {
                    "model": "{watson_knowledge_studio_model_ID_c}"
            }
        }
    }
}]
```
{: codeblock}    

## Discovery ツールを使用したカスタム・モデルの統合
{: #integrate-customtooling}

{{site.data.keyword.discoveryshort}} ツールを使用して、{{site.data.keyword.knowledgestudioshort}} カスタム・モデルを [エンティティー抽出 (Entity Extraction) ](/docs/services/discovery?topic=discovery-configservice#entity-extraction)エンリッチメントまたは[関係抽出 (Relation Extraction) ](/docs/services/discovery?topic=discovery-configservice#relation-extraction)エンリッチメントに統合することができます。

{{site.data.keyword.discoveryshort}} ツールを使用して複数のカスタム・モデルを同じフィールドに適用することはできません。API を使用する場合は、複数のカスタム・モデルを同一のフィールドに適用できます。[API を使用したカスタム・モデルの統合
](/docs/services/discovery?topic=discovery-integrating-with-wks#integrate-customAPI)を参照してください。

1. {{site.data.keyword.knowledgestudioshort}} モデルの `Model ID` を取得します。
1. {{site.data.keyword.discoveryshort}} ツールで、左上にある**「データの管理」**アイコンをクリックして、**「データの管理」**画面を開き、コレクションを作成または開きます。 **注:** 既存のコレクションを選択する場合は、空にする必要があります。 そうでない場合は、新規構成ファイルの作成後にそれらの文書を再取り込みする必要があります。
1. コレクションの**「データの管理 (Manage data)」**画面の**「構成」**セクションで、**「切り替え (Switch) 」**をクリックし、次に**「新規構成の作成 (Create a New Configuration)」**をクリックします。 構成に名前をつけます。 
1. **「エンリッチメントの追加 (Add enrichments)」**をクリックし、**「エンティティー抽出 (Entity Extraction)」**エンリッチメントまたは**「関係抽出 (Relation Extraction)」**エンリッチメントのいずれかを選択します。
1. 選択したエンリッチメントの「`Custom Model ID`」ボックスに「`Model ID`」を入力します。 カスタム {{site.data.keyword.knowledgestudiofull}} モデルが、そのエンリッチメントのデフォルトをオーバーライドします。 
1. **「適用」**をクリックし、次に**「完了」**をクリックします。

文書はデータ・コレクションにアップロードされると、そのコレクション用に選択された構成ファイルを使用して変換およびエンリッチされます。 文書がアップロードされた後で既存のコレクションを新規構成ファイルに切り替えると、アップロードされたそれらの文書は、引き続き元の構成ファイルによって変換されます。 構成ファイルの切り替え後にアップロードされた文書はすべて、新規構成ファイルを使用します。 コレクション**全体**で新しい構成を使用する場合は、新規コレクションを作成し、新しい構成ファイルを選択してから、すべての文書を再度アップロードすることが必要になります。

## 次のステップ
{: #wks-nextsteps}

{{site.data.keyword.discoveryshort}} サービスを新規構成で使用して、プライベート・データを取り込みます。 更新された構成を使用して取り込んだ文書は、カスタム・モデルのデータによって自動的にエンリッチされます。
