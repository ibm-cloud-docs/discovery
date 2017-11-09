---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-08"

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

# Integrating with Watson Knowledge Studio

You can integrate a custom model from {{site.data.keyword.knowledgestudiofull}} with the {{site.data.keyword.discoveryshort}} service to provide custom entity and relations enrichments.
{: shortdesc}

This gives you the flexibility to apply the {{site.data.keyword.discoveryshort}} service's document-enhancing capabilities with information specific to areas of particular focus, such as industry or scientific discipline. You can use both public data and your own proprietary data in your enrichment model.

You must use the service API to integrate a {{site.data.keyword.knowledgestudioshort}} model with the {{site.data.keyword.discoveryshort}} service. You cannot use the {{site.data.keyword.discoveryshort}} tooling to integrate a custom model.

## Before you begin

Before you can integrate a custom model from {{site.data.keyword.knowledgestudioshort}} with the {{site.data.keyword.discoveryshort}} service, you must create and deploy the model by using {{site.data.keyword.knowledgestudioshort}}. See the {{site.data.keyword.knowledgestudioshort}} documentation for information on creating and deploying models. You need the unique ID of the deployed model to integrate it with the {{site.data.keyword.discoveryshort}} service.

## Integrating your custom model

1.  Get the ID of your {{site.data.keyword.discoveryshort}} environment as described at [List environments ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_environments){: new_window}. Note the environment ID.
1.  List the IDs of your current {{site.data.keyword.discoveryshort}} configuration or configurations as described at [List configurations ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_configurations){: new_window} Note the ID of the configuration that you want to integrate with your {{site.data.keyword.knowledgestudiofull}} custom model.
1.  Download a copy of your current {{site.data.keyword.discoveryshort}} configuration by running the following commands in a bash shell or equivalent, such as Cygwin for Windows. Substitute `{environment_id}` and `{configuration_id}` with the IDs you noted down in the previous two steps.

    ```bash
    curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-11-07" > my_config.json
    ```
    {: pre}

    This command lists the contents of your collection file and puts them in a JSON file named `my_config.json`.
1.  Open the `my_config.json` file in a text editor and make the following changes:
    1.  Change the value of the `"name"` field to something that indicates the purpose of the new configuration. You can optionally change the value of the `"description"` field as well.

        ```json
        ...
        "name": "wks-config",
        "description": "This is a configuration to use with a WKS model",
        ...
        ```
        {: codeblock}

    1.  Update the enrichment fields with information for the {{site.data.keyword.knowledgestudioshort}} model. Assuming that the enrichment fields originally read:

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

    1.  Update the file as follows, substituting the unique ID of the {{site.data.keyword.knowledgestudioshort}} model described in "Before you begin" for `{watson_knowledge_studio_model_ID}`.

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

1.  Optionally enable entity normalization as described in [Creating a custom configuration to normalize entities](/docs/services/discovery/normalize-entities.html).
1.  Save the `my_config.json` file.
1.  Use a JSON validator, such as [JSLint ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://jslint.com){: new_window} to validate and, if necessary, correct your edited JSON before you perform the next steps.
1.  Update the configuration as follows. You again need the `{environment_id}` and `{configuration_id}` IDs you collected at the start of this procedure.

    ```bash
    curl -X PUT -u "{username}":"{password}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-11-07"
    ```
    {: pre}

    The command returns the contents of the updated configuration file.

## Next Steps

Use the {{site.data.keyword.discoveryshort}} service with your new configuration to ingest private data. Documents you ingest with the updated configuration are automatically enriched with the data from your custom model.
