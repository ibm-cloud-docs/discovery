---

copyright:
  years: 2015, 2020
lastupdated: "2020-08-17"

subcollection: discovery

---

{{site.data.keyword.attribute-definition-list}}

# Integrating with Watson Knowledge Studio
{: #integrating-with-wks}

<!-- Learn more topic WDS -->
You can integrate one or more custom models from {{site.data.keyword.knowledgestudiofull}} with {{site.data.keyword.discoveryshort}} to provide custom entity and relations enrichments.
{: shortdesc}

This gives you the flexibility to apply {{site.data.keyword.discoveryshort}}'s document-enhancing capabilities with information specific to areas of particular focus, such as industry or scientific discipline. You can use both public data and your own proprietary data in your enrichment model.

You can use the service API or the {{site.data.keyword.discoveryshort}} tooling to integrate a {{site.data.keyword.knowledgestudioshort}} model with {{site.data.keyword.discoveryshort}}.

## Before you begin
{: #wks-beforeintegration}

Before you can integrate a custom model from {{site.data.keyword.knowledgestudioshort}} with {{site.data.keyword.discoveryshort}}, you must create and deploy the model by using {{site.data.keyword.knowledgestudioshort}}. See the [{{site.data.keyword.knowledgestudioshort}} documentation](/docs/watson-knowledge-studio/tutorials-create-project.html#wks_tutintro) for information on creating and deploying models. You need the unique ID of the deployed model to integrate it with {{site.data.keyword.discoveryshort}}.

## Integrating your custom model with the API
{: #integrate-customAPI}

1.  Get the ID of your {{site.data.keyword.discoveryshort}} environment as described at [List environments](/apidocs/discovery#list_environments){: external}. Note the environment ID.
1.  List the IDs of your current {{site.data.keyword.discoveryshort}} configuration or configurations as described at [List configurations](/apidocs/discovery#list_configurations){: external} Note the ID of the configuration that you want to integrate with your {{site.data.keyword.knowledgestudiofull}} custom model.
1.  Download a copy of your current {{site.data.keyword.discoveryshort}} configuration by running the following commands in a bash shell or equivalent, such as Cygwin for Windows. Substitute `{environment_id}` and `{configuration_id}` with the IDs you noted down in the previous two steps.

    ```bash
    curl -u "apikey":"{apikey_value}" "{url}/v1/environments/{environment_id}/configurations/{configuration_id}?version=2019-04-30" > my_config.json
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

        It is possible to apply more than one custom model to identical fields using the API. See the example in [Integrating multiple custom models](/docs/discovery?topic=discovery-integrating-with-wks#integrate-multiplecustom).
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

1.  Save the `my_config.json` file.
1.  Use a JSON validator, such as [JSLint](http://jslint.com){: external} to validate and, if necessary, correct your edited JSON before you perform the next steps.
1.  Update the configuration as follows. You again need the `{environment_id}` and `{configuration_id}` IDs you collected at the start of this procedure.

    ```bash
    curl -X PUT -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d @my_config.json "{url}/v1/environments/{environment_id}/configurations/{configuration_id}?version=2019-04-30"
    ```
    {: pre}

    If you are creating a configuration or modifying the default configuration, create another custom configuration instead of updating an existing configuration. Before you create the configuration, remove the `"configuration_id":` field from your `my_config.json` file, and then run the following command:

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d @my_config.json "{url}/v1/environments/{environment_id}/configurations?version=2019-04-30"
    ```
    {: pre}

    Both commands return the contents of the updated configuration file.

    Replace `{apikey}` and `{url}` with your API key and URL.

### Integrating multiple custom models 
{: #integrate-multiplecustom}

You can apply more than one custom model to identical fields using the API. Follow the steps in [Integrating your custom model with the API](/docs/discovery?topic=discovery-integrating-with-wks#integrate-customAPI) and use the example here as a guide. 

You cannot apply multiple custom models using the {{site.data.keyword.discoveryshort}} tooling. Only the entity and relations enrichments can be customized.

You must specify a different `destination_field` for each identical `source_field`. In addition, each `source_field` must be enriched by a unique model. For example, if you want to apply multiple custom models to the `source_field` of `text` and you apply the `model` `{watson_knowledge_studio_model_ID}` to the `entities` enrichment, you must not use that model again for the `entities` enrichment.
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

## Integrating your custom model with the Discovery tooling
{: #integrate-customtooling}

You can integrate a {{site.data.keyword.knowledgestudioshort}} custom model into the [Entity Extraction](/docs/discovery?topic=discovery-configservice#entity-extraction) or [Relation Extraction](/docs/discovery?topic=discovery-configservice#relation-extraction) enrichments with the {{site.data.keyword.discoveryshort}} tooling.

You cannot apply multiple custom models to the same field using the {{site.data.keyword.discoveryshort}} tooling. It is possible to apply more than one custom model to identical fields using the API. See [Integrating your custom model with the API](/docs/discovery?topic=discovery-integrating-with-wks#integrate-customAPI).

1. Get the `Model ID` of your {{site.data.keyword.knowledgestudioshort}} model.
1. In the {{site.data.keyword.discoveryshort}} tooling, click the **Manage Data** icon to open the **Manage data** screen, then create or open a collection.

If you choose an existing collection, it must be empty. If not, create a new collection and reingest the documents after you have followed these steps.
{: note}

1. Click **Configure data**. The **Enrich fields** tab opens.
1. Click **Add enrichments** and select either the **Entity Extraction** or **Relation Extraction** enrichment.
1. Enter the `Model ID` in the `Custom Model ID` box of the selected enrichment. The custom {{site.data.keyword.knowledgestudiofull}} model overrides the default for that enrichment. 
1. Click **Apply**, then **Done**.

When documents are uploaded to a data collection, they are converted and enriched using the configuration file chosen for that collection. If you switch an existing collection to a new configuration file after documents are uploaded, those uploaded documents remain converted by the original configuration file. Any documents uploaded after switching the configuration file use the new configuration file. If you want the **entire** collection to use the new configuration, you must create a new collection, choose that new configuration file, and re-upload all the documents.

## Next Steps
{: #wks-nextsteps}

Use {{site.data.keyword.discoveryshort}} with your new configuration to ingest private data. Documents you ingest with the updated configuration are automatically enriched with the data from your custom model.
