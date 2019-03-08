---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-08"

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

# 与 Watson Knowledge Studio 集成
{: #integrating-with-wks}

可以将 {{site.data.keyword.knowledgestudiofull}} 中的定制模型与 {{site.data.keyword.discoveryshort}} 服务集成，以提供定制实体和关系扩充项。
{: shortdesc}

这使您能够灵活地应用 {{site.data.keyword.discoveryshort}} 服务的文档扩充功能，并提供特定于特定焦点领域的信息，如行业规程或科学学科。您可以在扩充模型中同时使用公共数据和您自己的专有数据。

可以使用服务 API 或 {{site.data.keyword.discoveryshort}} 工具将 {{site.data.keyword.knowledgestudioshort}} 模型与 {{site.data.keyword.discoveryshort}} 服务集成。

## 开始之前

要能够将 {{site.data.keyword.knowledgestudioshort}} 中的定制模型与 {{site.data.keyword.discoveryshort}} 服务集成，必须先使用 {{site.data.keyword.knowledgestudioshort}} 创建并部署该模型。请参阅 [{{site.data.keyword.knowledgestudioshort}} 文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.bluemix.net/docs/services/knowledge-studio/tutorials-create-project.html#wks_tutintro){: new_window}，以获取有关创建和部署模型的信息。您需要所部署模型的唯一标识，才能将其与 {{site.data.keyword.discoveryshort}} 服务集成。

## 将定制模型与 API 集成

1.  获取您的 {{site.data.keyword.discoveryshort}} 环境的标识，如[列出环境 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_environments){: new_window} 中所述。记下环境标识。
1.  列出您的当前 {{site.data.keyword.discoveryshort}} 配置的标识，如[列出配置 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_configurations){: new_window} 中所述。记下要与 {{site.data.keyword.knowledgestudiofull}} 定制模型集成的配置的标识。
1.  通过在 bash shell 或等效程序（例如，Cygwin for Windows）中运行以下命令，下载您的当前 {{site.data.keyword.discoveryshort}} 配置的副本。将 `{environment_id}` 和 `{configuration_id}` 替换为在前两个步骤中记下的标识。

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-11-07" > my_config.json
    ```
    {: pre}

    此命令会列出集合文件的内容，并将其放入名为 `my_config.json` 的 JSON 文件中。
1.  在文本编辑器中打开 `my_config.json` 文件，并进行以下更改：
    1.  将 `"name"` 字段的值更改为指示新配置用途的值。还可以选择更改 `"description"` 字段的值。

        ```json
        ...
        "name": "wks-config",
        "description": "This is a configuration to use with a WKS model",
        ...
        ```
        {: codeblock}

    1.  使用 {{site.data.keyword.knowledgestudioshort}} 模型的信息更新扩充字段。假定这些扩充字段初始为：

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

    1.  如下所示更新此文件，使用“开始之前”中所述的 {{site.data.keyword.knowledgestudioshort}} 模型的唯一标识来替换 `{watson_knowledge_studio_model_ID}`。

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

1.  保存 `my_config.json` 文件。
1.  使用 JSON 验证器（例如 [JSLint ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://jslint.com){: new_window}）进行验证，并根据需要更正编辑的 JSON，然后再执行后续步骤。
1.  如下所示更新配置。同样需要在此过程开始时收集的 `{environment_id}` 和 `{configuration_id}` 标识。

    ```bash
    curl -X PUT -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-11-07"
    ```
    {: pre}

    **注：**如果要创建新配置或修改缺省配置，那么将需要创建新的定制配置，而不是更新现有配置。在创建新配置之前，请确保从 `my_config.json` 文件中除去 `"configuration_id":` 字段，然后运行以下命令：

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07"
    ```
    {: pre}

    这两个命令都会返回更新后的配置文件的内容。

## 将定制模型与 Discovery 工具集成

可以使用 {{site.data.keyword.discoveryshort}} 工具将 {{site.data.keyword.knowledgestudioshort}} 定制模型集成到[实体抽取](/docs/services/discovery/building.html#entity-extraction)或[关系抽取](/docs/services/discovery/building.html#relation-extraction)扩充项中。

1. 获取 {{site.data.keyword.knowledgestudioshort}} 模型的`模型标识`。
1. 在 {{site.data.keyword.discoveryshort}} 工具中，单击左上角的**管理数据**图标将打开**管理数据**屏幕，然后创建或打开集合。**注：**如果选择现有集合，那么该集合应该为空。否则，应在创建新的配置文件后重新摄入这些文档。
1. 在集合的**管理数据**屏幕的**配置**部分中，单击**切换**，然后单击**创建新配置**。对配置命名。 
1. 单击**添加扩充项**，然后选择**实体抽取**或**关系抽取**扩充项。
1. 在所选扩充项的`定制模型标识`框中，输入`模型标识`。定制 {{site.data.keyword.knowledgestudiofull}} 模型将覆盖该扩充项的缺省值。 
1. 单击**应用**，然后单击**完成**。

将文档上传到数据集合后，将使用为该集合选择的配置文件对这些文档进行转换和扩充。如果在上传文档后将现有集合切换到新的配置文件，那么这些上传的文档仍将通过原始配置文件进行转换。切换配置文件后上传的任何文档都将使用新的配置文件。如果您希望**整个**集合使用新配置，那么需要创建新的集合，选择该新的配置文件，然后重新上传所有文档。

**注：**一个扩充项只能分配有一个 {{site.data.keyword.knowledgestudiofull}} 模型。

## 后续步骤

将 {{site.data.keyword.discoveryshort}} 服务与新配置配合使用来摄入专用数据。使用更新后的配置摄入的文档会自动通过定制模型中的数据进行扩充。
