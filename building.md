---

copyright:
  years: 2015, 2022
lastupdated: "2022-06-01"

subcollection: discovery

---

{{site.data.keyword.attribute-definition-list}}

# Configuring Discovery
{: #configservice}

Configuring {{site.data.keyword.discoveryshort}} makes it possible to gain useful insights by enriching your own data and then delivering it in a query-able form.
{: shortdesc}

Before you add your own content to {{site.data.keyword.discoveryshort}}, you must configure the basic parameters of the service ([Preparing the service for your documents](/docs/discovery?topic=discovery-configservice#preparing-the-service-for-your-documents)). This includes creating an environment and creating one or more collections within that environment. 

## Preparing the service for your documents
{: #preparing-the-service-for-your-documents}

<!-- Learn more topic WDS -->
In {{site.data.keyword.discoveryshort}}, the content that you upload is stored in a collection that is part of your environment. You must create the environment and collection before you can upload your content.

-   **Environment** — The environment defines the amount of storage space that you have for content in {{site.data.keyword.discoveryshort}}. A maximum of one environment can be created for each instance of {{site.data.keyword.discoveryshort}}.

    You have several plans (Lite, Advanced, Premium) to choose from, see the [{{site.data.keyword.discoveryshort}} catalog](https://cloud.ibm.com/catalog/services/discovery){: external} and [{{site.data.keyword.discoveryshort}} Pricing Plans](/docs/discovery?topic=discovery-discovery-pricing-plans) for details. Your source files do not count against your plan size limit, only the size of the converted JSON that is indexed counts towards your size limit.

-   **Collection** — A collection is a grouping of your content within the environment. You must create at least one collection to be able to upload your content.

    Collections are comprised of your private data, but {{site.data.keyword.discoveryshort}} also includes {{site.data.keyword.discoverynewsshort}}, a pre-enriched, public dataset. 

    {{site.data.keyword.discoverynewsshort}}, a public data set that is pre-enriched with cognitive insights, is also included with {{site.data.keyword.discoveryshort}}. You can use it to query for insights; for example: news alerts, event detecting, and trending topics in the news; that you can integrate into your applications. See [Watson Discovery News](/docs/discovery?topic=discovery-watson-discovery-news) for more information. You cannot adjust the {{site.data.keyword.discoverynewsshort}} configuration or add documents to this collection.

To create an environment and private data collection with the {{site.data.keyword.discoveryshort}} tooling do the following:

1.  On the **Manage Data** screen, click the ![Environment](images/icon_settings.png) icon on the upper right and choose **Create environment**. The environment is created based on the {{site.data.keyword.Bluemix_notm}} plan you selected earlier. The status of your environment is always available from this drop-down.

1.  Once your environment is ready, click the **Upload your own data** button, then you can **Name your new collection**.

     You can select the language of the documents you want to add to this collection: English, German, Spanish, Arabic, Japanese, French, Italian, Korean, or Brazilian Portuguese. There must only be one language in each of your collections. After you click **Create**, your data collection appears as a tile.

Your environment and data collection are ready. You can start [Adding content](/docs/discovery?topic=discovery-addcontent) immediately. 

You can use the {{site.data.keyword.discoveryshort}} tooling or API to crawl various data sources, or do a web crawl. See [Connecting to data sources](/docs/discovery?topic=discovery-sources) for more information.
{: tip}

## Adding enrichments
{: #adding-enrichments}

<!-- Learn more topic WDS -->
{{site.data.keyword.discoveryshort}} enriches (adds cognitive metadata to) the `text` field of your ingested documents with semantic information collected by these four {{site.data.keyword.watson}} functions - Entity Extraction, Sentiment Analysis, Category Classification, and Concept Tagging. (There are a total of nine {{site.data.keyword.watson}} enrichments available; the others are Keyword Extraction, Relation Extraction, Emotion Analysis, Element Classification, and Semantic Role Extraction.)

Some {{site.data.keyword.watson}} enrichments might be unavailable in certain plans or environments.

You can also integrate one or more custom models from {{site.data.keyword.knowledgestudiofull}} with {{site.data.keyword.discoveryshort}} to provide custom entity and relations enrichments. See [Integrating with Watson Knowledge Studio](/docs/discovery?topic=discovery-integrating-with-wks).

Only the first 50,000 characters of each JSON field selected for enrichment are enriched.
{: important}

You can further augment your documents by adding more enrichments to the `text` field, or enriching other fields. To do so using Smart Document Understanding, open the **Enrich Fields** tab, choose the field(s) you'd like to enrich and select from the list of available {{site.data.keyword.nlushort}} enrichments:

### Entity extraction
{: #entity-extraction}

Returns items such as persons, places, and organizations that are present in the input text. Entity extraction adds semantic knowledge to content to help understand the subject and context of the text that is being analyzed. The entity extraction techniques are based on sophisticated statistical algorithms and natural language processing technology, and are unique in the industry with their support for multilingual analysis and context-sensitive disambiguation. For a complete list of entity type systems, see [Entity type systems](/docs/discovery?topic=discovery-entity-type-systems), or for a list of entity types and subtypes that are used in the Version 1 and Version 2 entity type systems, see [Entity types (Version 1)](/docs/discovery?topic=discovery-entity-types-version-1) or [Entity types (Version 2)](/docs/discovery?topic=discovery-entity-types-version-2). You can also create and add a [custom entity model](/docs/discovery?topic=discovery-configservice#custom-entity-model) with {{site.data.keyword.knowledgestudiofull}}.

Example portion of a document enriched with Entity Extraction:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
  "enriched_text": {
    "entities": [
      {
        "count": 1,
        "sentiment": {
          "score": 0
        },
        "text": "Acme Corporation",
        "relevance": 0.98389,
        "type": "Company"
      },
      {
        "count": 1,
        "sentiment": {
          "score": 0
        },
        "text": "Atlanta",
        "relevance": 0.532754,
        "type": "Location",
        "disambiguation": {
          "subtype": [
            "AdministrativeDivision",
            "GovernmentalJurisdiction",
            "OlympicHostCity",
            "PlaceWithNeighborhoods",
            "City"
          ],
          "name": "Atlanta",
          "dbpedia_resource": "http://dbpedia.org/resource/Atlanta"
        }
      },
      {
        "count": 1,
        "sentiment": {
          "score": 0
        },
        "text": "Georgia",
        "relevance": 0.469643,
        "type": "Location",
        "disambiguation": {
          "subtype": [
            "StateOrCounty"
          ]
        }
      }
    ]
  }
}
```
{: codeblock}

In the preceding example, you could query the entity type by accessing `enriched_text.entities.type`

`sentiment` is calculated for entity types even if the **sentiment** enrichment is not selected. To learn more about sentiment scoring, see [Sentiment analysis](/docs/discovery?topic=discovery-configservice#sentiment-analysis).

The `relevance` score ranges from `0.0` to `1.0`. The higher the score, the more relevant the entity. The `disambiguation` field contains the disambiguation information for the entity, which includes the entity `subtype` information and links to the resource(s), if applicable. The `count` is the number of times the entity is mentioned in the document.

#### Using a custom entity model
{: #custom-entity-model}

If you wish to create a custom enrichment model, you can do so in {{site.data.keyword.knowledgestudiofull}} and import the model into {{site.data.keyword.discoveryshort}} by adding the ID in the `Custom Model ID` box of the {{site.data.keyword.discoveryshort}} tooling. For more information about integrating with {{site.data.keyword.knowledgestudiofull}}, see [Integrating with {{site.data.keyword.knowledgestudiofull}}](/docs/discovery?topic=discovery-integrating-with-wks). The custom {{site.data.keyword.knowledgestudiofull}} model overrides the default Entity Extraction enrichment.

Only one {{site.data.keyword.knowledgestudiofull}} model can be assigned to an enrichment.
{: note}

### Relation extraction
{: #relation-extraction}

Recognizes when two entities are related and identifies the type of relation. You can also create and add a [custom relation model](/docs/discovery?topic=discovery-configservice#custom-relation-model) with {{site.data.keyword.knowledgestudiofull}}.

Example portion of a document enriched with Relation Extraction:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
  "enriched_text": {
    "relations": [
      {
        "type": "locatedAt",
        "sentence": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
        "score": 0.989245,
        "arguments": [
         {
            "text": "Atlanta",
            "location": [
             94,
             101
            ],
            "entities": [
              {
                "type": "GeopoliticalEntity",
                "text": "Atlanta"
              }
            ]
         },
          {
            "text": "Georgia",
            "location": [
             103,
             110
            ],
            "entities": [
              {
                "type": "GeopoliticalEntity",
                "text": "Georgia"
              }
            ]
          }
        ]
      }
    ]
  }
}
```
{: codeblock}

In the preceding example, you could query the relation type by accessing `enriched_text.relations.type`.

The related entities are listed in the `arguments`.

The `score` ranges from `0.0` to `1.0`. The higher the score, the more relevant the relation.

#### Using a custom relation model
{: #custom-relation-model}

To create a custom enrichment model, you can use {{site.data.keyword.knowledgestudiofull}} and import the model into {{site.data.keyword.discoveryshort}} by adding the ID in the `Custom Model ID` box of the {{site.data.keyword.discoveryshort}} tooling. For more information about integrating with {{site.data.keyword.knowledgestudiofull}}, see [Integrating with {{site.data.keyword.knowledgestudiofull}}](/docs/discovery?topic=discovery-integrating-with-wks). The custom {{site.data.keyword.knowledgestudiofull}} model overrides the default Relation extraction enrichment.

Only one {{site.data.keyword.knowledgestudiofull}} model can be assigned to an enrichment.
{: note}

### Keyword extraction
{: #keyword-extraction}

Important topics in your content that are typically used when indexing data, generating tag clouds, or when searching. {{site.data.keyword.discoveryshort}} automatically identifies supported languages in your input content, and then identifies and ranks keywords in that content.

Example portion of a document enriched with Keyword Extraction:

```json
  {
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "keywords": [
        {
          "text": "Acme Corporation",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.985203
        },
        {
          "text": "new factory",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.821033
        },
        {
          "text": "stockholders",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.66497
        },
        {
          "text": "title",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.332438
        },
        {
          "text": "Atlanta",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.307723
        },
        {
          "text": "Georgia",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.306485
        }
      ]
    }
  }
```
{: codeblock}

In the preceding example, you could query the keyword text by accessing `enriched_text.keywords.text`

`sentiment` is calculated for keywords even if the **sentiment** enrichment is not selected. To learn more about sentiment scoring, see [Sentiment analysis](/docs/discovery?topic=discovery-configservice#sentiment-analysis).

The `relevance` score ranges from `0.0` to `1.0`. The higher the score, the more relevant the keyword.

### Category classification
{: #category-classification}

Categorizes input text, HTML, or web-based content into a hierarchical taxonomy up to five levels deep. Deeper levels allow you to classify content into more accurate and useful subsegments.

Example portion of a document enriched with Category Classification:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "categories": [
        {
          "score": 0.361614,
          "label": "/business and industrial"
        },
        {
          "score": 0.329377,
          "label": "/business and industrial/company/merger and acquisition"
        },
        {
          "score": 0.154254,
          "label": "/business and industrial/business operations/business plans"
        }
      ]
```
{: codeblock}

In the preceding example, you could query the category label by accessing `enriched_text.categories.label`

The `label` is the detected category. The hierarchy levels are separated by forward slashes. The `score` for that category ranges from `0.0` to `1.0`. The higher the score, the greater the confidence in that category.

### Concept tagging
{: #concept-tagging}

Identifies concepts with which the input text is associated, based on other concepts and entities that are present in that text. Concept tagging understands how concepts relate, and can identify concepts that are not directly referenced in the text. For example, if an article mentions CERN and the Higgs boson, the Concepts API functions identifies Large Hadron Collider as a concept even if that term is not mentioned explicitly in the page. Concept tagging enables higher level analysis of input content than just basic keyword identification.

Example portion of a document enriched with Concept Tagging:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "concepts": [
        {
          "text": "Acme Corporation",
          "relevance": 0.91136,
          "dbpedia_resource": "http://dbpedia.org/resource/Acme_Corporation"
        },
        {
          "text": "Factory",
          "relevance": 0.886784,
          "dbpedia_resource": "http://dbpedia.org/resource/Factory"
        }
      ]
```
{: codeblock}

In the preceding example, you can query the concept text type by accessing `enriched_text.concepts.text`

The `relevance` score ranges from `0.0` to `1.0`. The higher the score, the more relevant the concept. Links to the resource(s) are provided, if applicable.

### Semantic Role extraction
{: #semantic-role-extraction}

Identifies subject, action, and object relations within sentences in the input content. Relation information can be used to automatically identify buying signals, key events, and other important actions.

Example portion of a document enriched with Semantic Role Extraction:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
      "enriched_text": {
      "semantic_roles": [
        {
          "subject": {
            "text": "The stockholders",
            "keywords": [
              {
                "text": "stockholders"
              }
            ]
          },
          "sentence": " The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
          "object": {
            "text": "pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia",
            "keywords": [
              {
                "text": "Acme Corporation"
              },
              {
                "text": "new factory"
              },
              {
                "text": "Atlanta"
              },
              {
                "text": "Georgia"
              }
            ],
            "entities": [
              {
                "type": "Company",
                "text": "Acme Corporation"
              },
              {
                "type": "Location",
                "text": "Atlanta",
                "disambiguation": {
                  "subtype": [
                    "AdministrativeDivision",
                    "GovernmentalJurisdiction",
                    "OlympicHostCity",
                    "PlaceWithNeighborhoods",
                    "CityTown",
                    "City"
                  ],
                  "name": "Atlanta",
                  "dbpedia_resource": "http://dbpedia.org/resource/Atlanta"
                }
              },
              {
                "type": "Location",
                "text": "Georgia",
                "disambiguation": {
                  "subtype": [
                    "StateOrCounty"
                  ]
                }
              }
            ]
          },
          "action": {
            "verb": {
              "text": "be",
              "tense": "past"
            },
            "text": "were",
            "normalized": "be"
          }
        }
      ]
```
{: codeblock}

In the preceding example, you could query the relation subject text by accessing `enriched_text.relations.subject.text`

`sentiment` is calculated for relations even if the **sentiment** enrichment is not selected. To learn more about sentiment scoring, see [Sentiment analysis](/docs/discovery?topic=discovery-configservice#sentiment-analysis). It does not extract `entities` or `keywords` (as shown in the example) unless you also select the **entity** and **keyword** enrichments. See [Entity extraction](/docs/discovery?topic=discovery-configservice#entity-extraction) and [Keyword extraction](/docs/discovery?topic=discovery-configservice#keyword-extraction) about those enrichments.

The `subject`, `action`, and `object` are extracted for every sentence that contains a relation.

### Sentiment analysis
{: #sentiment-analysis}

Identifies attitude, opinions, or feelings in the content that is being analyzed. {{site.data.keyword.discoveryshort}} can calculate overall sentiment within a document, sentiment for user-specified targets, entity-level sentiment, quotation-level sentiment, directional-sentiment, and keyword-level sentiment. The combination of these capabilities supports a variety of use cases ranging from social media monitoring to trend analysis.

Example portion of a document enriched with Sentiment Analysis:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "sentiment": {
        "document": {
        "score": 0.459813,
        "label": "positive"
  }
}
```
{: codeblock}

In the preceding example, you could query the sentiment label by accessing `enriched_text.sentiment.document.label`

The `label` is the overall sentiment of the document (`positive`, `negative`, or `neutral`). The sentiment `label` is based on the `score`; a score of `0.0` would indicate that the document is `neutral`, a positive number would indicate the document is `positive`, a negative number would indicate the document is `negative`.

### Emotion analysis
{: #emotion-analysis}

Detects anger, disgust, fear, joy, and sadness implied in English text. Emotion Analysis can detect emotions that are associated with targeted phrases, entities, or keywords, or it can analyze the overall emotional tone of your content.

Example portion of a document enriched with Emotion Analysis:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "emotion": {
        "document": {
          "emotion": {
          "disgust": 0.102578,
          "joy": 0.626655,
          "anger": 0.02303,
          "fear": 0.018884,
          "sadness": 0.096802
    }
  }
}
```
{: codeblock}

In the preceding example, you could query the `joy` Emotion by accessing `enriched_text.emotion.document.emotion.joy`

Emotion Analysis analyzes your text and calculates a score for each emotion (anger, disgust, fear, joy, sadness) on a scale of `0.0` to `1.0`. If the score of any emotion is `0.5` or higher, then that emotion is detected. The higher the score above `0.5`, the higher the relevance. In the snippet shown, `joy` has a score above 0.5, so {{site.data.keyword.watson}} detected joy.

Emotion Analysis is supported in English only.
{: note}

### Element classification
{: #elements}

The Element Classification enrichment is deprecated and will no longer be available, effective **10 July 2020**.
{: important}

Parses elements (sentences, lists, tables) in governing documents to classify important types and categories
For more information, see [Element classification](/docs/discovery?topic=discovery-element-classification).

[Smart Document Understanding](/docs/discovery?topic=discovery-sdu) is unavailable if this enrichment is used.

#### Enrichment pricing
{: #enrichment-pricing}

Enrichment pricing information is available on [{{site.data.keyword.Bluemix_notm}}](https://cloud.ibm.com/catalog/services/discovery){: external}.

#### Enrichment language support
{: #enrichment-language-support}

For information about enrichment language support, see [{{site.data.keyword.discoveryshort}} language support](/docs/discovery?topic=discovery-language-support).

### Understanding the difference between Entities, Concepts, and Keywords
{: #udbeck}

At first glance, **Entity extraction**, **Concept tagging** and **Keyword extraction** appear to be similar enrichments. We'll use the text from the enrichment examples to show the differences between them.

```json
"text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia."
```
{: codeblock}

Since the **Entity Extraction** enrichment extracts persons, places, and organizations in the input text, **Entity extraction** returns the following entity types:

```json
"type": "City"
"text": "Atlanta"

"type": "Company"
"text": "Acme"

"type": "StateOrCounty"
"text": "Georgia"
```
{: codeblock}

Since the **Concept tagging** enrichment understands how concepts relate, it can identify concepts that are not directly referenced in the text. For example, if an article mentions CERN and the Higgs boson, it identifies Large Hadron Collider as a concept even if that term is not mentioned explicitly. Since our example document text is only one sentence, there are no related concepts, so **Concept tagging** returns the following concepts:

```json
"text": "Acme Corporation"
"text": "factory"
```
{: codeblock}

Since the **Keyword extraction** enrichment identifies content typically used when indexing data, generating tag clouds, or searching, **Keyword extraction** returns the following keywords:

```json
"text": "Acme Corporation"
"text": "new factory"
"text": "stockholders"
"text": "Atlanta"
"text": "Georgia"
```
{: codeblock}

These enrichments work together to help you build better queries.

## Customizing field extraction
{: #normalizing-entities}

### Using CSS selectors to extract fields from HTML documents
{: #using-css}

You can extract fields from HTML documents using the {{site.data.keyword.discoveryshort}} API.

If you are ingesting well-formed HTML, you can use CSS selectors to extract JSON fields and then apply enrichments to the extracted fields. Edit your configuration file to enable this feature. Specifically, add an `extracted_fields` element to the `conversions/html` hierarchy, then specify field names, CSS selectors, and field types, as follows:

```json
{
  "name": "Extract JSON config",
  "description": "New configuration enabling extraction of JSON fields from HTML",
  "conversions": {
    ...
    "html": {
      ...
      "extracted_fields": {
        "{field_name_1}": {
          "css_selector": "{CSS_selector_expression_1}",
          "type": "{field_type}"
        },
        ...
        "{field_name_N}": {
          "css_selector": "{CSS_selector_expression_N}",
          "type": "{field_type}"
        }
      }
    ...
    }
  }
}
```
{: codeblock}

Specify values for the new fields as follows:

-   `field_name` — The name of the field that you want to add to the JSON output.
-   `CSS_selector_expression` — The CSS selector that is to be run against the input HTML to extract the fields. The expression can have one or more matches.

    Valid CSS selectors are those specified by the [JSoup parser](https://jsoup.org/apidocs/org/jsoup/select/Selector.html){: external} and its [selector syntax](https://jsoup.org/cookbook/extracting-data/selector-syntax){: external}. A short list is provided at [Common selectors](/docs/discovery?topic=discovery-configservice#common-selectors).
-   `field_type` — Either `array` or `string`. If the field type is not specified, it defaults to `array`. Both the `string` and `array` types can be enriched.

If a CSS selector matches both a parent node and one or more of its children, the text content of the nodes are duplicated in the JSON output.
{: important}

Field names must meet the restrictions defined in [Field name requirements](/docs/discovery?topic=discovery-configref#field_reqs).
{: note}

The following JSON passage shows the relevant section of the configuration to which you add CSS selector information.

```json
{
  "name": "Default Configuration",
  "description": "The configuration used by default when creating a new collection without specifying a configuration_id.",
  "conversions": {
    ...
    "html": {
      "exclude_tags_completely": [
        "script",
        "sup"
      ],
      "exclude_tags_keep_content": [
        "font",
        "em",
        "span"
      ],
      "exclude_content": {
        "xpaths": []
      },
      "keep_content": {
        "xpaths": []
      },
      "exclude_tag_attributes": [
        "EVENT_ACTIONS"
      ]
    }
    ...
  }
}
```
{: codeblock}

The following passage shows the configuration with a new name and description, as well as the location where you can specify CSS selectors.

```json
{
  "name": "Extract JSON config",
  "description": "New configuration enabling extraction of JSON fields from HTML",
  "conversions": {
    ...
    "html": {
      "exclude_tags_completely": [
        "script",
        "sup"
      ],
      "exclude_tags_keep_content": [
        "font",
        "em",
        "span"
      ],
      "exclude_content": {
        "xpaths": []
      },
      "keep_content": {
        "xpaths": []
      },
      "exclude_tag_attributes": [
        "EVENT_ACTIONS"
      ],
      "extracted_fields": {
        "{field_name_1}": {
          "css_selector": "{CSS_selector_expression_1}",
          "type": "{field_type}"
        },
        ...
        "{field_name_N}": {
          "css_selector": "{CSS_selector_expression_N}",
          "type": "{field_type}"
        }
      }
    }
  }
  ...
}
```
{: codeblock}

Finally, the following passage shows the configuration the new name and description as well as some CSS selectors. The selectors match items in the HTML example listed below the passage.

```json
{
  "name": "Extract JSON config",
  "description": "New configuration enabling extraction of JSON fields from HTML",
  "conversions": {
    ...
    "html": {
      "exclude_tags_completely": [
        "script",
        "sup"
      ],
      "exclude_tags_keep_content": [
        "font",
        "em",
        "span"
      ],
      "exclude_content": {
        "xpaths": []
      },
      "keep_content": {
        "xpaths": []
      },
      "exclude_tag_attributes": [
        "EVENT_ACTIONS"
      ],
      "extracted_fields": {
        "chapters": {
          "css_selector": ".chapter",
          "type": "array"
        },
        "authors": {
          "css_selector": ".author"
        },
        "authors_str": {
          "css_selector": ".author",
          "type": "string"
        },
        "comments": {
          "css_selector": "[^comments-content]"
        }
      }
    }
  }
  ...
}
```
{: codeblock}

If you load the following HTML document into a collection that uses an updated configuration, the CSS selectors match the appropriate attributes and values in the HTML.

```html
<html>
  <body>
    <div id="authors">
      <div class="author"><span class="first_name">Jane</span> <span class="last_name">Rain</span></div>
      <div class="author">Joe Snow</div>
  </div>
  <div class="chapter"><h1>The Rain in Spain</h1><p>falls mainly on the plain.</p></div>
  <div class="chapter"><h1>How I Learned to Stop Worrying</h1><p>and love my snowblower.</p></div>
  <span id="comments-section">
    <h4>Comments:</h4>
    <span id="comments-content-1">Rain gives me pain.</span>
    <span id="comments-content-2">All snow must go!</span>
  </span>
</body></html>
```
{: codeblock}

After the preceding HTML is ingested and enhanced, {{site.data.keyword.discoveryshort}} returns the following JSON:

```json
{
  "extracted_metadata": { ... },
  "html": "...",
  "text": "...",
  "extracted_fields": {
    "authors": [ "Jane Rain", "Joe Snow" ],
    "authors_str": "Jane Rain\n\nJoe Snow",
    "chapters": [ "The Rain in Spain\n\nfalls mainly on the plain.", "How I Learned to Stop Worrying\n\nand love my snowblower." ],
    "comments": [ "Rain gives me pain.", "All snow must go!" ]
  }
}
```
{: codeblock}

After deciding which HTML elements you want to extract, you can then further modify the configuration file to specify the enrichments you want to apply to them.

#### Common selectors
{: #common-selectors}

Some common CSS selectors include the following:

  - `tag` — Matches the `tag` name
  - `.class` — Matches the value of `class`
  - `#id` — Matches the value of `id`
  - `[attribute]` — Matches any tag with the specified `attribute`, regardless of value
  - `[attribute=value]` or `[attribute="value"]` — Matches the specified `attribute` and `value`

## Splitting documents with document segmentation
{: #doc-segmentation}

If your source documents are supported by Smart Document Understanding (see [Supported document types](/docs/discovery?topic=discovery-sdu#doctypes)), use document splitting instead of document segmentation. For details, see [document splitting](/docs/discovery?topic=discovery-sdu#splitting).
{: note}

You can split your HTML documents into segments based on HTML heading tags. Once split, each segment is a separate document that is enriched and indexed separately. Since queries return these segments as separate documents, document segmentation can be used to:

  - Perform aggregations on individual segments of a document. For example, your aggregation would count each time a segment mentions a specific entity, instead of only counting it once for the entire document.
  - Perform relevancy training on segments instead of documents, which improves result reranking.

Documents can be split based on the following HTML tags: `h1` `h2` `h3` `h4` `h5` and `h6`.

Considerations:

  - In the Lite plan, the number of segments per document is limited to `250`. Any document content remaining after `249` segments are stored within segment `250`. In the Advanced plan, the number of segments per document is limited to `1,000`. Any document content remaining after `999` segments are stored within segment `1,000`. Segmentation limits are dependent on your plan. For more information, see [Discovery pricing plans](/docs/discovery?topic=discovery-discovery-pricing-plans).

  - Each segment counts towards the document limit of your plan. {{site.data.keyword.discoveryshort}} indexes segments until the plan limit is reached. See [Discovery pricing plans](/docs/discovery?topic=discovery-discovery-pricing-plans) for document limits.

  - You can not use CSS selectors to extract fields (see [Using CSS selectors to extract fields](/docs/discovery?topic=discovery-configservice#using-css)) when using document segmentation.

  - Documents are segmented each time the specified HTML tag is detected. Consequently, segmentation could lead to malformed HTML because the documents could be split before closing tags and after opening tags.

  - HTML metadata; the title; plus any custom metadata, is extracted and included in the index with each segment. Every segment of a document includes identical metadata.

  - Document segmentation is not supported when the **Element Classification** (`elements`) enrichment is specified.

  - Re-ingesting a segmented document has additional considerations, see [Updating a segmented document](/docs/discovery?topic=discovery-configservice#update-seg).

### Performing segmentation
{: #performing-segmentation}

If your source documents are supported by Smart Document Understanding (see [Supported document types](/docs/discovery?topic=discovery-sdu#doctypes)), use document splitting instead of document segmentation. For details, see [document splitting](/docs/discovery?topic=discovery-sdu#splitting).
{: note}

Segmentation is setup via the API in the `conversions` section.

```json
{
  "configuration_id": "a23c467d-1212-4b3a-5555-93e788a3622a",
  "name": "Example configuration",
  "conversions": {
    "segment": {
      "enabled": true,
      "selector_tags": ["h1", "h2", "h3", "h4", "h5", "h6"]
    }
  }
}
```
{: codeblock}

`enabled` = `true` turns on document segmentation.

`selector_tags` is an array that specifies the heading tags documents can be segmented on.

#### Example
{: #example-segmentation}

Configuration:

```json
"conversions": {
  "segment": {
    "enabled": true,
    "selector_tags": ["h1", "h2"]
```
{: codeblock}

Original HTML document:

```
<html>
 <head>
  <title>My Document</title>
 </head>
 <body>
  first line
   <div name="section 1">
    <h1>heading 1</h1>
     <div name="section 2">This is the text that falls under <b>heading 1</b> and should be therefore split into its own segment.
      <h2>heading 2</h2>
      line under heading 2
     </div>
       <h3>heading 3</h3>
       line under heading 3
   </div>
  last line
 </body>
</html>
```
{: codeblock}

The first document segment looks like this:

```json
{
  "id": "94c686c3-a790-4d8d-ba42-2bddf01b311c",
  "result_metadata": {
    "parent_id": "94c686c3-a790-4d8d-ba42-2bddf01b311c",
    "segment": 1,
    "total_segments": 3
  },
  "text": "This is the text that falls under heading 1 and should be therefore split into its own segment."
  },
  "extracted_metadata": {
    "sha1": "45ede479df67d78f2205ea7e714843375d3029c0",
    "filename": "doc-with-different-heading-levels.html",
    "file_type": "html",
    "title": "My Document"
  },
  "title": "My Document",
  "html": "<?xml version='1.0' encoding='UTF-8' standalone='yes'?><html>\n<head>"
}
```
{: codeblock}

All segments include an:

  - `id` - The `id` of this segment.
  - `title` - The `title` field is extracted from the HTML `title` field. (`2019-03-25` or later API version string.)
  - `segment_metadata` section which contains:
    - `parent_id` - The `parent_id` is the id of the original document. For the first segment, the `id` and `parent_id` are identical.
    - `segment` - The number of this segment.
    - `total_segments` - The total number of segments the document was split into.
  - `extracted_metadata` section which contains:
    - `sha1` - Corresponds to the original document.
    - `title` - The `title` field is extracted from the HTML `title` field. (`2019-03-25` or later API version string.)
    - `filename` - Corresponds to the original document.
    - `file_type`- Corresponds to the original document.
  - `text` field
  - `html` field

### Updating a segmented document
{: #update-seg}

If a segmented document is updated and needs to be ingested again, it can be replaced by using the [Update document](/apidocs/discovery#update-a-document){: external} method.

When updating a segmented document, you must upload the document by using the POST method of the `/environments/{environment_id}/collections/{collection_id}/documents/{document_id}` API, specifying the contents of the `parent_id` field of one of the current segments as the `{document_id}` path variable.

When updating, all segments are overwritten, unless the updated version of the document has fewer total sections than the original. Those older segments remain in the index and might be individually deleted, using the API. See the [API Reference](/apidocs/discovery#delete-a-document){: external} for details. You can identify how many segments were created by querying the `notices`. Each segment is given a `document_id` field that is comprised of the `{parent_id}`, followed by an underscore, followed by the segment number.

If any of the segments of the document that you intend to update are ranked for relevancy training, you must first delete all the segments of that document and then ingest the updated document as a new document. This results in a new `document_id` for each segment and any trained segments must be retrained. The trained index becomes inaccurate if you don't delete the old content first.

Alternately, consider creating a new document that contains only the new content and ingest it separately.
