---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-31"

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

# Discovery archives

This topic contains information about {{site.data.keyword.discoveryshort}} features that might still be available, but have been replaced with newer options.
{: tip}

## AlchemyLanguage enrichments
{: #AlchemyLanguage-enrichments}

Starting on **18 July, 2017** {{site.data.keyword.discoveryfull}} introduced a new enrichment technology, named {{site.data.keyword.nlushort}}.  These enrichments are the same as your existing enrichments but require a slightly different configuration and schema. The original enrichments, named {{site.data.keyword.alchemylanguageshort}} enrichments, will be deprecated.

{{site.data.keyword.alchemylanguageshort}} enrichment support will end on **15 January, 2018**.

**Note:** New collections should be enriched with {{site.data.keyword.nlushort}} and any existing collections with {{site.data.keyword.alchemylanguageshort}} configuration files migrated as soon as possible. {{site.data.keyword.alchemylanguageshort}} enrichment ingestion support ends **15 January, 2018**. For information on migrating collections and configuration files that utilize the {{site.data.keyword.alchemylanguageshort}} enrichments, see [Migrating enrichments to {{site.data.keyword.nlushort}}](/docs/services/discovery/migrate-nlu.html).

### Entity extraction (AlchemyLanguage)
{: #entity-extraction-al}

Returns items such as persons, places, and organizations that are present in the input text. Entity extraction adds semantic knowledge to content to help understand the subject and context of the text that is being analyzed. The entity extraction techniques are based on sophisticated statistical algorithms and natural language processing technology, and are unique in the industry with their support for multilingual analysis, context-sensitive disambiguation, and quotations extraction.

Example portion of a document enriched with Entity Extraction:

```json
{
      "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
      "enriched-text": {
        "status": "OK",
        "language": "english",
        "entities": [
          {
            "type": "City",
            "relevance": 0.532754,
            "sentiment": {
              "type": "positive",
              "score": 0.527541,
              "mixed": false
            },
            "count": 1,
            "text": "Atlanta",
            "disambiguated": {
              "subType": [
                "AdministrativeDivision",
                "GovernmentalJurisdiction",
                "OlympicHostCity",
                "PlaceWithNeighborhoods"
              ],
              "name": "Atlanta",
              "website": "http://www.atlantaga.gov/",
              "dbpedia": "http://dbpedia.org/resource/Atlanta",
              "freebase": "http://rdf.freebase.com/ns/m.013yq"
            }
          }
        ]
      }
    }
```
{: codeblock}
In the preceding example, you could query the entity type by accessing `enriched_text.entities.type`

`sentiment` is calculated for entity types even if the **sentiment** enrichment is not selected. To learn more about sentiment scoring, see [Sentiment analysis](/docs/services/discovery/discovery-auxiliary.html#sentiment-analysis-al).

The `relevance` score will range from `0.0` to `1.0`. The higher the score, the more relevant the entity. The `disambiguated` field contains the disambiguation information for the entity, which includes the entity `subType` information and links to the resource(s), if applicable. The `count` is the number of times the entity is mentioned in the document.

### Keyword extraction (AlchemyLanguage)
{: #keyword-extraction-al}

Important topics in your content that are typically used when indexing data, generating tag clouds, or when searching. The {{site.data.keyword.discoveryshort}} service automatically identifies supported languages in your input content, and then identifies and ranks keywords in that content.

Example portion of a document enriched with Keyword Extraction:

```json
{
    "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched-text": {
        "status": "OK",
        "language": "english",
        "keywords": [
          {
            "relevance": 0.66497,
            "sentiment": {
              "score": 0.527541,
              "type": "positive",
              "mixed": false
            },
            "text": "stockholders"
          }
        ]
      }
    }
```
{: codeblock}

In the preceding example, you could query the keyword text by accessing `enriched_text.keywords.text`

`sentiment` is calculated for keywords even if the **sentiment** enrichment is not selected. To learn more about sentiment scoring, see [Sentiment analysis](/docs/services/discovery/discovery-auxiliary.html#sentiment-analysis-al).

The `relevance` score will range from `0.0` to `1.0`. The higher the score, the more relevant the keyword.

### Taxonomy classification (AlchemyLanguage)
{: #taxonomy-classification-al}

Categorizes input text, HTML or web-based content into a hierarchical taxonomy up to five levels deep. Deeper levels allow you to classify content into more accurate and useful subsegments.

Example portion of a document enriched with Taxonomy Classification:

```json
  {
    "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched-text": {
        "status": "OK",
        "language": "english",
        "taxonomy": [
          {
            "label": "/business and industrial/company/merger and acquisition",
            "score": 0.517533,
            "confident": false
          }
        ]
      }
    }
```
{: codeblock}

In the preceding example, you could query the taxonomy label by accessing `enriched_text.taxonomy.label`

The `label` is the detected taxonomy category. The hierarchy levels are separated by forward slashes. The `score` for that category will range from `0.0` to `1.0`. The higher the score, the greater the confidence in that category.

### Concept tagging (AlchemyLanguage)
{: #concept-tagging-al}

Identifies concepts with which the input text is associated, based on other concepts and entities that are present in that text. Concept tagging understands how concepts relate, and can identify concepts that are not directly referenced in the text. For example, if an article mentions CERN and the Higgs boson, the Concepts API functions will identify Large Hadron Collider as a concept even if that term is not mentioned explicitly in the page. Concept tagging enables higher level analysis of input content than just basic keyword identification.

Example portion of a document enriched with Concept Tagging:

```json
{
    "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
        "status": "OK",
        "language": "english",
        "concepts": [
          {
            "text": "Acme Corporation",
            "relevance": 0.91136,
            "dbpedia": "http://dbpedia.org/resource/Acme_Corporation",
            "freebase": "http://rdf.freebase.com/ns/m.0dndy",
            "yago": "http://yago-knowledge.org/resource/Acme_Corporation"
          }
        ]
      }
    }
```
{: codeblock}

In the preceding example, you can query the concept text type by accessing `enriched_text.concepts.text`

The `relevance` score will range from `0.0` to `1.0`. The higher the score, the more relevant the concept. Links to the resource(s) are provided, if applicable.

### Relation extraction (AlchemyLanguage)
{: #relation-extraction-al}

Identifies subject, action, and object relations within sentences in the input content. Relation information can be used to automatically identify buying signals, key events, and other important actions.

Example portion of a document enriched with Relation Extraction:

```json
{
      "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
      "enriched-text": {
        "status": "OK",
        "language": "english",
        "relations": [
          {
            "sentence": " The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, GA.",
            "subject": {
              "text": "The stockholders",
              "keywords": [
                {
                  "text": "stockholders"
                }
              ]
            },
            "action": {
              "text": "were",
              "lemmatized": "be",
              "verb": {
              "text": "be",
              "tense": "past"
            }
            },
            "object": {
              "text": "pleased that Acme Corporation plans to build a new factory in Atlanta, GA",
              "sentiment": {
                "type": "positive",
                "score": 0.834516,
                "mixed": false
              },
              "entities": [
                {
                  "type": "Company",
                  "text": "Acme Corporation"
                },
                {
                  "type": "City",
                  "text": "Atlanta",
                  "disambiguated": {
                    "subType": [
                      "AdministrativeDivision",
                      "GovernmentalJurisdiction",
                      "OlympicHostCity",
                      "PlaceWithNeighborhoods"
                    ],
                    "name": "Atlanta",
                    "website": "http://www.atlantaga.gov/",
                    "dbpedia": "http://dbpedia.org/resource/Atlanta",
                    "freebase": "http://rdf.freebase.com/ns/m.013yq"
                  }
                },
                {
                  "type": "StateOrCounty",
                  "text": "GA"
                }
              ],
              "keywords": [
                {
                  "text": "Acme Corporation"
                },
                {
                  "text": "new factory"
                },
                {
                  "text": "GA"
                },
                {
                "text": "Atlanta"
                }
              ]
            }
          }
        ]
      }
    }
```
{: codeblock}

In the preceding example, you could query the relation subject text by accessing `enriched_text.relations.subject.text`

`sentiment` is calculated for relations even if the **sentiment** enrichment is not selected. To learn more about sentiment scoring, see [Sentiment analysis](/docs/services/discovery/discovery-auxiliary.html#sentiment-analysis-al). It will not extract `entities` or `keywords` (as shown in the example) unless you also select the **entity** and **keyword** enrichments. See [Entity extraction](/docs/services/discovery/discovery-auxiliary.html#entity-extraction-al) and [Keyword extraction](/docs/services/discovery/discovery-auxiliary.html#keyword-extraction-al) for more information on those enrichments.

The `subject`, `action`, and `object` are extracted for every sentence that contains a relation.

### Sentiment analysis (AlchemyLanguage)
{: #sentiment-analysis-al}

Identifies attitude, opinions, or feelings in the content that is being analyzed. The {{site.data.keyword.discoveryshort}} service can calculate overall sentiment within a document, sentiment for user-specified targets, entity-level sentiment, quotation-level sentiment, directional-sentiment, and keyword-level sentiment. The combination of these capabilities supports a variety of use cases ranging from social media monitoring to trend analysis.

Example portion of a document enriched with Sentiment Analysis:

```json
{
      "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
      "enriched_text": {
        "status": "OK",
        "language": "english",
        "docSentiment": {
          "type": "positive",
          "score": 0.0966252,
          "mixed": true
        }
      }
    }
```
{: codeblock}

In the preceding example, you could query the docSentiment type by accessing `enriched_text.docSentiment.type`

The `type` is the overall sentiment of the document (`positive`, `negative`, or `neutral`). The sentiment `type` is based on the `score`; a score of `0.0` would indicate that the document is `neutral`, a positive number would indicate the document is `positive`, a negative number would indicate the document is `negative`. If `mixed` is `true`, it indicates that the document contains both positive and negative sentiments (this field is not determined by the `score`).

### Emotion analysis (AlchemyLanguage)
{: #emotion-analysis-al}

Detects anger, disgust, fear, joy, and sadness implied in English text. Emotion Analysis can detect emotions that are associated with targeted phrases, entities, or keywords, or it can analyze the overall emotional tone of your content.

Example portion of a document enriched with Emotion Analysis:

```json
{
      "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
      "enriched_text": {
        "status": "OK",
        "language": "english",
        "docEmotions": {
          "anger": "0.077394",
          "disgust": "0.044024",
          "fear": "0.092664",
          "joy": "0.553327",
          "sadness": "0.3969"
        }
      }
    }
```
{: codeblock}

In the preceding example, you could query the `joy` docEmotion by accessing `enriched_text.docEmotions.joy`

Emotion Analysis analyzes your text and calculates a score for each emotion (anger, disgust, fear, joy, sadness) on a scale of `0.0` to `1.0`. If the score of any emotion is `0.5` or higher, then that emotion has been detected (the higher the score above `0.5`, the higher the relevance). In the snippet shown, `joy` has a score above 0.5, so {{site.data.keyword.watson}} detected joy.


## Watson Discovery News Original

A new version of {{site.data.keyword.discoverynewsfull}} debuted on **31, July 2017**. {{site.data.keyword.discoverynewsfull}} Original was retired with a removal from service date of **15, January 2018**. See [Watson Discovery News](watson-discovery-news.html) for information on this new version.

{{site.data.keyword.discoverynewsfull}} Original is a dataset of primarily English-language news sources that is updated continuously, with approximately 300,000 new articles and blogs added daily. This indexed dataset is pre-enriched with the following {{site.data.keyword.alchemylanguageshort}} enrichments: **Keyword Extraction**, **Entity Extraction**, **Concept Tagging**, **Relation Extraction**, **Sentiment Analysis**, and **Taxonomy Classification**. The following additional metadata is also added: crawl date, publication date, URL ranking, host rank, and anchor text. Historical search is available for the past 60 days of news data.

{{site.data.keyword.discoverynewsfull}} Original is enriched with {{site.data.keyword.alchemylanguageshort}} enrichments. For more information about these enrichments, see [{{site.data.keyword.alchemylanguageshort}} enrichments](discovery-auxiliary.html#AlchemyLanguage-enrichments).

### Querying Watson Discovery News Original

A new version of {{site.data.keyword.discoverynewsfull}} debuted on **31, July 2017**. {{site.data.keyword.discoverynewsfull}} Original was retired with a removal from service date of **15, January 2018**. See [Watson Discovery News](watson-discovery-news.html) for information on this new version.

**Note:** The maximum number of results returned for a Watson Discovery News query is `50`. Use additional queries and the `offset` parameter to return more than `50` results.

{{site.data.keyword.discoverynewsfull}} Original uses a similar, but slightly different JSON schema from the one used for private collections. You do not need to include `enriched_text` in your queries, for example:

**How to structure a {{site.data.keyword.discoverynewsfull}} Original query**

![Example Watson Discovery News Original query structure](images/news_query_structure.png)

The following example query returns the top 10 articles in {{site.data.keyword.discoverynewsfull}} Original about the Pittsburgh Steelers that have a positive sentiment.

1.  On the **Your data** screen, choose the {{site.data.keyword.discoverynewsfull}} collection.
1.  Click **Query this collection**, then **Build your own query**.
1.  Under **Search for documents**, click **Use the {{site.data.keyword.discoveryshort}} Query Language**, then enter `text:Pittsburgh Steelers, docSentiment.type:positive` into the **Enter query here** field.
1.  Click **Customize display options**, then enter `10` (this is the default) in the `Number of documents to return` field.
1.  Click **Run query**. The top 10 articles about the Pittsburgh Steelers with a positive sentiment are displayed.

**Additional example {{site.data.keyword.discoverynewsfull}} Original queries**

-  `concepts.text:"Health care"` - Under **Search for documents**, click **Use the {{site.data.keyword.discoveryshort}} Query Language**, then enter this query. It returns all articles that include the concept of `health care`. If you specify a count, such as 50, in the **Number of documents to return** field you receive only the top 50 most relevant articles.

**How to structure a {{site.data.keyword.discoverynewsfull}} Original aggregation**

![Example Watson Discovery News Original aggregation query structure](images/news_aggregation_structure.png)

The following example aggregation returns the number of articles found in {{site.data.keyword.discoverynewsfull}} Original about the Pittsburgh Steelers by sentiment.

1.  On the **Your data** screen, choose the {{site.data.keyword.discoverynewsfull}} Original collection.
1.  Click **Query this collection**, then **Build your own query**.
1.  Under **Include analysis of your results**, enter `filter(text:"Pittsburgh Steelers").term(docSentiment.type,count:3)` in the **Write an aggregation query using the {{site.data.keyword.discoveryshort}} Query Language** field.
1.  Click **Customize display options**, then enter `0` in the **Number of documents to return** field.
1.  Click **Run query**. The results show the number of documents about the Pittsburgh Steelers and how many of those results have a `positive`, `negative`, or `neutral` docSentiment.

**Additional example {{site.data.keyword.discoverynewsfull}} Original aggregation**

-  `filter(entities.text:twitter).term(docSentiment.type,count:3)` - If you enter this aggregation query in the **Write an aggregation query using the {{site.data.keyword.discoveryshort}} Query Language** field, it will first narrow down (filter) the set of articles to only the ones that include the entities text of twitter, then divides those articles by the document sentiment types. Only the top three document sentiment types (`positive`, `negative`, `neutral`) are returned.

Adding `nested` before an aggregation query restricts the aggregation to the area of the results specified. For example: `nested(text.entities)` means that only the `text.entities` components of any result are used to aggregate against. This affect can be seen easily by looking at the differences between the following two queries: `filter(text.entities.type::City)` - the aggregation counts the number of *Results* that contain one or more `entity` with the type `City` and `nested(text.entities).filter(text.entities.type::City)` - the aggregation counts the number of instances of an `entity` with the type `City` in the results.  Additionally, any subsequent operation will further restrict the result set that can be aggregated against. For example `nested(text.entities).filter(text.entities.type::City)` means that any only entities of `type::City` will be aggregated. For example: `nested(text.entities).filter(text.entities.type::City).term(text.entities.text,count:3)` will aggregate the top three entities of type `City`, Where as: `filter(text.entities.type::City).term(text.entities.text,count:3)` will return the top three entities whereas the result contains at least one entity of type `City`.

**Note**: You cannot adjust the {{site.data.keyword.discoverynewsfull}} Original configuration, train, or add documents to this collection.

## Integrating with Watson Knowledge Studio using AlchemyLanguage Enrichments

You can integrate a custom model from {{site.data.keyword.knowledgestudiofull}} with the {{site.data.keyword.discoveryshort}} service to provide custom enrichments.
{: shortdesc}

### Before you begin

Before you can integrate a custom model from {{site.data.keyword.knowledgestudioshort}} with the {{site.data.keyword.discoveryshort}} service, you must create and deploy the model by using {{site.data.keyword.knowledgestudioshort}}. See the {{site.data.keyword.knowledgestudioshort}} documentation for information on creating and deploying models. You need the unique ID of the deployed model to integrate it with the {{site.data.keyword.discoveryshort}} service.

### About this task

You can use a custom model developed in {{site.data.keyword.knowledgestudioshort}} to enrich documents in the {{site.data.keyword.discoveryshort}} service. This gives you the flexibility to apply the {{site.data.keyword.discoveryshort}} service's document-enhancing capabilities with information specific to areas of particular focus, such as industry or scientific discipline. You can use both public data and your own proprietary data in your enrichment model.

You must use the service API to integrate a {{site.data.keyword.knowledgestudioshort}} model with the {{site.data.keyword.discoveryshort}} service. You cannot use the {{site.data.keyword.discoveryshort}} tooling to integrate a custom model.

### Procedure

1.  Get the ID of your {{site.data.keyword.discoveryshort}} environment as described at [List environments ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_environments){: new_window}. Note the environment ID.
1.  List the IDs of your current {{site.data.keyword.discoveryshort}} configuration or configurations as described at [List configurations ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_configurations){: new_window} Note the ID of the configuration that you want to integrate with your {{site.data.keyword.knowledgestudiofull}} custom model.
1.  Download a copy of your current {{site.data.keyword.discoveryshort}} configuration by running the following commands in a bash shell or equivalent, such as Cygwin for Windows. Substitute `{environment_id}` and `{configuration_id}` with the IDs you noted down in the previous two steps.

    ```bash
    curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-09-01" > my_config.json
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
            "destination_field": "enriched_text",
            "source_field": "text",
            "enrichment": "alchemy_language",
            "options": {
              "extract": "keyword, entity, doc-sentiment, taxonomy, concept, relation",
              "sentiment": true,
              "quotations": true
            }
          }
        ]
        ```
        {: codeblock}

    1.  Update the file as follows, substituting the unique ID of the {{site.data.keyword.knowledgestudioshort}} model described in "Before you begin" for `{watson_knowledge_studio_model_ID}`.

        ```json
        "enrichments": [
          {
            "destination_field": "enriched_text",
            "source_field": "text",
            "enrichment": "alchemy_language",
            "options": {
              "extract": "keyword, entity, doc-sentiment, taxonomy, concept, relation, typed-rels",
              "sentiment": true,
              "quotations": true,
              "model": "{watson_knowledge_studio_model_ID}"
            }
          }
        ]
        ```
        {: codeblock}

1.  Optionally enable entity normalization as described in [Creating a custom configuration to normalize entities](/docs/services/discovery/normalize-entities.html).
1.  Save the `my_config.json` file.
1.  Use a JSON validator, such as [JSLint ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://jslint.com){: new_window} to validate and, if necessary, correct your edited JSON before you perform the next steps.
1.  Update the configuration as follows. You again need the `{environment_id}` and `{configuration_id}` IDs you collected at the start of this procedure.

    ```bash
    curl -X PUT -u "{username}":"{password}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-09-01"
    ```
    {: pre}

    The command returns the contents of the updated configuration file.
1.  Use the {{site.data.keyword.discoveryshort}} service normally. Documents you ingest with the updated configuration are automatically enriched with the data from your custom model.

## Creating a custom configuration to normalize AlchemyLanguage entities
{: #normalizing-entities}

You can configure {{site.data.keyword.discoveryshort}} service to include *normalized entities*, also known as *canonical names*, in the output of your queries.
{: shortdesc}

**Note:** Editing the configuration to enable normalized entities is a manual task that must be performed by using a text editor and API calls. It is not currently supported by the Tooling.

**Note:** Entity normalization is available only when you use the Discovery service with a custom model generated by Watson Knowledge Studio, as described in [Integrating with {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery/integrate-wks.html).

Entity normalization inserts normalized (canonical) names for different references to the same person or object in the source document. For instance, if you enable entity normalization and then ingest a document or documents that discuss "J.R. Cash" and "John R. Cash," the processed output will include the `canonical_name` "Johnny Cash" along with each matched term. It will also include relevant canonical names for other text entities encountered in the document. See the end of this section for example output.

After you enrich a document with canonical names, you can search more easily for specific items with the same canonical name.

Canonical names are derived from a public dictionary. If a suitable canonical name cannot be located in the dictionary, the service uses the most suitable entity reference in the document as the canonical name. Before querying an entity-normalized document for a canonical name or names, examine the enriched JSON document to verify that the canonical name or names generated by the service match the names you expect.

### Procedure

1.  Get the ID of your {{site.data.keyword.discoveryshort}} environment as described at [List environments ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_environments){: new_window}. Note the environment ID.
1.  List the IDs of your current {{site.data.keyword.discoveryshort}} configuration or configurations as described at [List configurations ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_configurations){: new_window}. Note the ID of the configuration that you want to update.
1.  Download a copy of your current {{site.data.keyword.discoveryshort}} configuration by running the following commands in a bash shell or equivalent, such as Cygwin for Windows. Substitute `{environment_id}` and `{configuration_id}` with the IDs you noted down in the previous two steps.

    ```bash
    curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-09-01" > new_config.json
    ```
    {: pre}

    This command lists the contents of your collection file and puts them in a JSON file named `new_config.json`.

1.  Open the `new_config.json` file in a text editor and make the following changes:
    1. Change the value of the `"name"` field to something that indicates the purpose of the new configuration. You can optionally change the value of the `"description"` field as well.

       ```json
        ...
        "name": "normalize-entities-config",
        "description": "This configuration enables entity normalization",
        ...
       ```
       {: codeblock}

    1. Update the enrichment fields with information for the {{site.data.keyword.knowledgestudioshort}} model. Assuming that the enrichment fields originally read:

       ```json
       "enrichments": [
         {
           "destination_field": "enriched_text",
           "source_field": "text",
           "enrichment": "alchemy_language",
           "options": {
             "extract": "keyword, entity, doc-sentiment, taxonomy, concept, relation, typed-rels",
             "sentiment": true,
             "quotations": true,
             "model": "{watson_knowledge_studio_model_ID}"
           }
         }
       ]
       ```
       {: codeblock}

    1. Update the file as follows.

       ```json
       "enrichments": [
         {
           "destination_field": "enriched_text",
           "source_field": "text",
           "enrichment": "alchemy_language",
           "options": {
             "extract": "keyword, entity, doc-sentiment, taxonomy, concept, relation, typed-rels",
             "sentiment": true,
             "quotations": true,
             "model": "{watson_knowledge_studio_model_ID}"
             "normalizeEntities": 1
           }
         }
       ]
       ```
       {: codeblock}

    1. Save the `new_config.json` file.

1.  Use a JSON validator, such as [JSLint ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://jslint.com){: new_window}, to validate your edited JSON before you perform the next steps.

1.  Update the configuration as follows. You again need the `{environment_id}` and `{configuration_id}` IDs you collected at the start of this procedure.

    ```bash
    curl -X PUT -u "{username}":"{password}" -H "Content-Type: application/json" -F configuration-@new_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-09-01"
    ```
    {: pre}

    The command returns the contents of the updated configuration file.

1.  Use the {{site.data.keyword.discoveryshort}} service normally. Documents you ingest with the updated configuration are automatically enriched with normalized entities, as shown in the following output excerpts.

### Output examples

Output snippet **without** `"normalizeEntities": 1`:

```json
{
  "enriched_text": {
  ...
  ...
  ...
    "entity_relations": {
      "entities": {
        "entity": [
          {
            "class": "SPC",
            "eid": "-E0",
            "generic": false,
            "level": "NAM",
            "mentref": [
              {
                "mid": "-M0",
                "text": "J.R. Cash"
              },
              {
                "mid": "-M6",
                "text": "musician"
              },
              {
                "mid": "-M7",
                "text": "who"
              },
              {
                "mid": "-M13",
                "text": "He"
              },
              {
                "mid": "-M20",
                "text": "He"
              }
            ],
            "score": 0.7874817061794613,
            "subtype": "OTHER",
            "type": "PERSON"
          },
        ...
        ...
        ...
        ]
      },
      "relations": {
        "relation": [
          {
            "rel_entity_arg": [
              {
                "argnum": 1,
                "eid": "-E0"
              },
              {
                "argnum": 2,
                "eid": "-E1"
              }
            ],
            "relmentions": {
              "relmention": [
                {
                  "class": "SPECIFIC",
                  "modality": "ASSERTED",
                  "rel_mention_arg": [
                    {
                      "argnum": 1,
                      "mid": "-M0",
                      "text": "John R. Cash",
                    },
                    {
                      "argnum": 2,
                      "mid": "-M1",
                      "text": "country"
                    }
                  ],
                  "rmid": "-R1-1",
                  "score": 0.49918343781296,
                  "tense": "UNSPECIFIED"
                }
              ]
            },
            "rid": "-R1",
            "subtype": "OTHER",
            "type": "knownAs"
          },
          ...
          ...
          ...
        ]
      }
    }
  }
}
```
{: codeblock}

Output snippet **with** `"normalizeEntities": 1`:

```json
{
  "enriched_text": {
  ...
  ...
  ...
    "entity_relations": {
      "entities": {
        "entity": [
          {
            "class": "SPC",
            "eid": "-E0",
            "generic": false,
            "level": "NAM",
            "mentref": [
              {
                "mid": "-M0",
                "text": "J.R. Cash"
              },
              {
                "mid": "-M6",
                "text": "musician"
              },
              {
                "mid": "-M7",
                "text": "who"
              },
              {
                "mid": "-M13",
                "text": "He"
              },
              {
                "mid": "-M20",
                "text": "He"
              }
            ],
            "score": 0.7874817061794613,
            "subtype": "OTHER",
            "type": "PERSON",
            "canonical_name": "Johnny Cash"
          },
        ...
        ...
        ...
        ]
      },
      "relations": {
        "relation": [
          {
            "rel_entity_arg": [
              {
                "argnum": 1,
                "eid": "-E0"
              },
              {
                "argnum": 2,
                "eid": "-E1"
              }
            ],
            "relmentions": {
              "relmention": [
                {
                  "class": "SPECIFIC",
                  "modality": "ASSERTED",
                  "rel_mention_arg": [
                    {
                      "argnum": 1,
                      "mid": "-M0",
                      "text": "John R. Cash",
                      "canonical_name": "Johnny Cash"
                    },
                    {
                      "argnum": 2,
                      "mid": "-M1",
                      "text": "country",
                      "canonical_name": "country music"
                    }
                  ],
                  "rmid": "-R1-1",
                  "score": 0.49918343781296,
                  "tense": "UNSPECIFIED"
                }
              ]
            },
            "rid": "-R1",
            "subtype": "OTHER",
            "type": "knownAs"
          },
          ...
          ...
          ...
        ]
      }
    }
  }
}
```
{: codeblock}
