---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-03"

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

# Configuring your service

Building a {{site.data.keyword.discoveryshort}} service will make it possible to gain useful insights by enriching your own data and then delivering it in a query-able form.
{: shortdesc}

Before you add your own content to the {{site.data.keyword.discoveryshort}} service, you should configure the service to process the content the way that you want.

The first step is to configure the basic parameters of the service ([Preparing the service for your documents](/docs/services/discovery/building.html#preparing-the-service-for-your-documents)), this includes creating an environment and creating one or more collections within that environment. When a collection is created, a set of defaults ([The default configuration](/docs/services/discovery/building.html#the-default-configuration)) are automatically provided. If you are happy with these defaults, you can proceed to uploading your content ([Adding content](/docs/services/discovery/adding-content.html)).

However, you will most likely want to specify one or more custom configurations (see [When you need a custom configuration](/docs/services/discovery/building.html#when-you-need-a-custom-configuration)). If this is the case, you will need to do the following:

-   identify some sample content (documents that are representative of your files)
-   upload the content ([Uploading sample documents](/docs/services/discovery/building.html#uploading-sample-documents))
-   adjust the conversion process ([Converting sample documents](/docs/services/discovery/building.html#converting-sample-documents))
-   define enrichments ([Adding enrichments](/docs/services/discovery/building.html#adding-enrichments))
-   normalize the results ([Normalizing data](/docs/services/discovery/building.html#normalizing-data))

    After you have created your custom configuration, you can upload your documents ([Adding content](/docs/services/discovery/adding-content.html)).

## Preparing the service for your documents
{: #preparing-the-service-for-your-documents}

In the {{site.data.keyword.discoveryshort}} service, the content that you upload is stored in a collection that is part of your environment. You must create the environment and collection before you can upload your content.

-   **Environment** — The environment defines the amount of storage space that you have for content in the {{site.data.keyword.discoveryshort}} service. A maximum of one environment can be created for each instance of the {{site.data.keyword.discoveryshort}} service.

     You have several plans (Lite, Advanced, Premium) to choose from, see the [{{site.data.keyword.discoveryshort}} catalog ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window}  and [{{site.data.keyword.discoveryshort}} Pricing Plans](/docs/services/discovery/pricing-details.html) for details. Your source files do not count against your file size limit, only the size of the converted JSON that is indexed counts towards your size limit.

-   **Collection** — A collection is a grouping of your content within the environment. You must create at least one collection to be able to upload your content.

    Collections are comprised of your private data, but {{site.data.keyword.discoveryshort}} also includes {{site.data.keyword.discoverynewsshort}}, a pre-enriched, public dataset. You can use it to query for insights; for example: news alerts, event detecting, and trending topics in the news; that you can integrate into your applications.

    {{site.data.keyword.discoverynewsshort}}, a public data set that has been pre-enriched with cognitive insights, is also included with {{site.data.keyword.discoveryshort}}. See [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html#watson-discovery-news) for more information. You cannot adjust the {{site.data.keyword.discoverynewsshort}} configuration or add documents to this collection. See a demo of what you can build with {{site.data.keyword.discoverynewsshort}} [here ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://discovery-news-demo.ng.bluemix.net/){: new_window}.

To create an environment and private data collection with the {{site.data.keyword.discoveryshort}} tooling do the following:

1.  On the **Manage Data** screen, click the ![Cog](images/icon_settings.png) icon and choose **Create environment**. The environment is created based on the {{site.data.keyword.Bluemix_notm}} plan you selected earlier. The status of your environment is always available from this drop-down.

1.  Once your environment is ready, click the **Upload your own data** button, then you can **Name your new collection**.

    By default, the configuration file will be **Default Configuration**. If you have another configuration file available, you can choose it, or you can create a new one later and apply it to this collection. You can also select the language of the documents you will add to this collection: English, German, Spanish, Arabic, Japanese, French, Italian, Korean, or Brazilian Portuguese. There should be only one language in each of your collections. After you click **Create**, your data collection will appear as a tile.

Your environment and data collection are ready! If you wish to use the default configuration file, you can start [Adding content](/docs/services/discovery/adding-content.html) immediately. But if you want to customize your {{site.data.keyword.discoveryshort}} configuration with additional enrichments and conversion settings, you should not begin adding documents right now, you should start creating your custom configuration file. See [Configuring your service](/docs/services/discovery/building.html#custom-configuration).

**Note:** When documents are uploaded to a data collection, they are converted and enriched using the configuration file chosen for that collection. If you decide later that you would like to switch a collection to a different configuration file, you can do that, but the documents that have already been uploaded will remain converted by the original configuration file. All documents uploaded after switching the configuration file will use the new configuration file. If you want the **entire** collection to use the new configuration, you will need to create a new collection, choose that new configuration file, and re-upload all the documents. The {{site.data.keyword.discoveryshort}} service stores the converted text of the documents that you upload, embedded images in **PDF** and **Microsoft Word** files are not stored and will not be returned in results.

You can use the {{site.data.keyword.discoveryshort}} tooling or API to crawl Box, Salesforce, and Microsoft SharePoint Online data sources. See [Connecting to data sources](/docs/services/discovery/connect.html) for more information.
{: tip}

### The default configuration
{: #the-default-configuration}

The {{site.data.keyword.discoveryshort}} service includes a standard configuration that will convert, enrich and normalize your data without requiring you to manually configure these options.

The default configuration named **Default Configuration** contains enrichments, plus standard document conversions based on font styles and sizes. {{site.data.keyword.discoveryshort}} will enrich (add cognitive metadata to) the text field of your documents with semantic information collected by four {{site.data.keyword.watson}} Enrichments — Entity Extraction, Sentiment Analysis, Category Classification, and Concept Tagging (learn more about them [here](/docs/services/discovery/building.html#adding-enrichments)).

-   [Microsoft Word conversion](/docs/services/discovery/building.html#microsoft-word-conversion)
-   [PDF conversion](/docs/services/discovery/building.html#pdf-conversion)
-   [HTML conversion](/docs/services/discovery/building.html#html-conversion)
-   [JSON conversion](/docs/services/discovery/building.html#json-conversion)

A second default configuration named **Default Contract Configuration** is available in the {{site.data.keyword.discoveryshort}} tooling. It is configured to enrich with Element Classification, which can be used to extract party, nature, and category from elements in PDFs. See [Element Classification](/docs/services/discovery/element-classification.html#element-collection) for details.

If you would like to create a custom configuration, see [Custom configuration](/docs/services/discovery/building.html#custom-configuration).

### When you need a custom configuration
{: #when-you-need-a-custom-configuration}

Getting the right information out of your content and returning it to your users is the goal of the {{site.data.keyword.discoveryshort}} service. Identifying what that information is, and how it is stored in your content is defined by the configuration that you use to ingest the content. The content types that the {{site.data.keyword.discoveryshort}} service can ingest are flexible, meaning that even though your unstructured content is saved in a specific format, it is not required that the structure of that content match the structure of other content of the same type.

-   **I understand that my documents may not be structured in the way the default configuration expects. *How do I know if the default
    settings are right for me?***
    -   The easiest way to see if the default works for you is to test it by [Uploading sample documents](/docs/services/discovery/building.html#uploading-sample-documents). If the sample JSON results meet your expectations, then no additional configuration is required.
-   **I understand that default enrichments are added to the text field of my documents. Can I add additional enrichments to other fields?**
    -   Absolutely, you can add additional enrichments to as many fields as you wish. See [Adding enrichments](/docs/services/discovery/building.html#adding-enrichments) for details.

## Custom configuration
{: #custom-configuration}

To create a custom configuration in the {{site.data.keyword.discoveryshort}} tooling, open a Private data collection, and on the **Manage Data** screen, click **Switch** next to the name of your **Configuration**. On the **Switch configuration** dialog, click **Create a new configuration**.

After you have named your new configuration file, that name will be displayed at the top of the configuration screen. This new configuration file will automatically contain the settings and enrichments of the [Default configuration](/docs/services/discovery/building.html#the-default-configuration) file to give you a place to begin.

The three steps of customizing a configuration file are: **Convert**, **Enrich**, and **Normalize**.

1.  [Converting sample documents](/docs/services/discovery/building.html#converting-sample-documents)
1.  [Adding enrichments](/docs/services/discovery/building.html#adding-enrichments)
1.  [Normalizing data](/docs/services/discovery/building.html#normalizing-data)

For detailed information about configurations, see the [Configuration reference](/docs/services/discovery/custom-config.html).

### Uploading sample documents
{: #uploading-sample-documents}

To make the configuration process more efficient, you can upload up to ten Microsoft Word, HTML, JSON, or PDF files that are representative of your document set. These are called **sample documents**. Sample documents are not added to your collection — they are only used to identify fields that are common to your documents and customize those fields to your requirements.

When creating a new configuration file in the {{site.data.keyword.discoveryshort}} tooling, you can upload sample documents via drag and drop or browse. Click on the file name in the **Upload Sample Documents** pane to preview each file.

#### Remember the following items when uploading sample documents:

-   All of your documents are converted to JSON before they are enriched and indexed.
-   Microsoft Word and PDF documents are converted to HTML first, then JSON.
-   HTML documents are converted directly to JSON.
-   The maximum file size for a sample document is 1MB. Sample documents are stored in your browser's local roaming data folder. To delete your sample documents, click the **Delete** icon.

#### Guidelines for choosing good sample documents:

-   You should have (at minimum), one sample document for each file type you intend to ingest - Microsoft Word, PDF, HTML, and JSON. (You cannot preview PDF documents enriched with the **Element Classification** enrichment.)
-   If you have any unique document types (such as financial reports or press releases), include one of each in your set of sample documents.
-   For HTML documents, you should choose documents that include HTML tags you would like to exclude, as well as tag attributes you would like to include or exclude.
-   JSON documents should include any fields you would like to remove or merge together (for example, zipCode and postalCode).

### Converting sample documents
{: #converting-sample-documents}

Converting your sample documents is the process that will let you define how each input type is handled. The file type of content that you upload dictates the number of conversion steps that you will have to consider.

Before you start, [upload your sample documents](/docs/services/discovery/building.html#uploading-sample-documents), and open a sample document of the file type you'd like to configure in the pane on the right.

To work through the Conversion settings, click through the file types.

![Converting a sample document](images/convert.png)

-   **If you are converting Microsoft Word files you must do the following:**
    -   Set the Microsoft Word conversion options
    -   Set the HTML conversion options
    -   Set the JSON conversion options
    -   Review the result

-   **If you are converting PDF files you must do the following:**
    -   Set the PDF conversion options
    -   Set the HTML conversion options
    -   Set the JSON conversion options
    -   Review the result

-   **If you are converting HTML files you must do the following:**
    -   Set the HTML conversion options
    -   Set the JSON conversion options
    -   Review the result

-   **If you are converting JSON files** you must set the JSON conversion options and review the result.

For each configuration file that you create, there is only one set of conversion options for each step of the process. This means the HTML conversion options will be the same for PDF files, Word files, and HTML. If you require different conversion options for each type of content that you are ingesting (or if you have files of the same type that will require different types of conversion) you will need to store your files in different collections and create separate configuration files for each set of conversion settings.

#### Microsoft Word conversion
{: #microsoft-word-conversion}

Microsoft Word font sizes and font styles are used to convert the headings in your documents properly into H1, H2, and so on. H1's are the document title, and H2's and below are subheadings. Use the text boxes and radio buttons to change the default settings if you wish. You can also add additional heading levels and Word styles. If your Word documents tend to use a specific font or style name for headings, make sure to add that information. This will help improve your conversion, which will yield better query results.

**Example:** If it is common for your Word documents to use a 20 pt font, italic for heading 2s - change the **Font size range** to **20** to **23** and the **Font style** to **italic**.

After making any changes, click **Apply and Save**.

#### PDF conversion
{: #pdf-conversion}

PDF font sizes and font names are used to convert the headings in your documents properly into H1, H2, and so on. H1's are the document title, and H2 and below are subheadings. Use the text boxes and radio buttons to change the default settings if you wish. You can also add additional heading levels. If your PDF documents tend to use a specific font for headings, make sure to add that information. This will help improve your conversion, which will yield better query results.

**Example:** If it is common for your PDF documents to use a 20 pt font, bold for heading 1s - change the **Font size range** to **20** to **80** and the **Font style** to **bold**. Adjust the other levels accordingly.

After making any changes, click **Apply and Save**.

#### HTML conversion
{: #html-conversion}

You can use this step to remove unnecessary tags and other document info so that you retain only the information you need for your queries.

Default HTML settings:

- Exclude these tags, as well as their content: **`script`**, **`sup`**
- Exclude these tags, but keep their content: **`font`**, **`em`**, **`span`**
- Keep these tag attributes: no default
- Exclude these tag attributes: **`EVENT_ACTIONS`**
- Keep content that matches this/these XPath(s): no default
- Exclude content that matches this/these XPath(s): no default

After making any changes, click **Apply and Save**.

#### JSON conversion
{: #json-conversion}

The last step of the conversion is to ensure that the converted (or uploaded JSON) is formed the way that you expect it to be before enrichments are applied to the content. You can create rules {{site.data.keyword.watson}} will use to convert your HTML to JSON.

-   You can move, merge, copy or remove fields. For example: You may want to merge **`zipCode`** and **`postalCode`** because they are two similar terms for the same field.
-   Empty fields (fields that contain no information) will be deleted by default. You can change that using the **Remove empty fields** toggle.

After making any changes, click **Apply and Save**.

## Adding enrichments
{: #adding-enrichments}

The {{site.data.keyword.discoveryshort}} [default configuration](/docs/services/discovery/building.html#the-default-configuration) will enrich (add cognitive metadata to) the `text` field of your ingested documents with semantic information collected by these four {{site.data.keyword.watson}} functions - Entity Extraction, Sentiment Analysis, Category Classification, and Concept Tagging. (There are a total of nine {{site.data.keyword.watson}} enrichments available; the others are Keyword Extraction, Relation Extraction, Emotion Analysis, Element Classification, and Semantic Role Extraction.)

Some {{site.data.keyword.watson}} enrichments may not be available in certain plans or environments.

**Important:** Only the first 50,000 characters of each JSON field selected for enrichment will be enriched.

**Note:** {{site.data.keyword.alchemylanguageshort}} enrichments were deprecated 1 March 2018. If you have any existing collections that are using {{site.data.keyword.alchemylanguageshort}} enrichments, you must migrate to {{site.data.keyword.nlushort}} enrichments. For information on migrating existing collections and configuration files that utilize the {{site.data.keyword.alchemylanguageshort}} enrichments, see [Migrating enrichments to {{site.data.keyword.nlushort}}](/docs/services/discovery/migrate-nlu.html). 

You can further augment your documents by adding more enrichments to the `text` field, or enriching other fields. To do so using the {{site.data.keyword.discoveryshort}} tooling, [create a custom configuration](/docs/services/discovery/building.html#custom-configuration), choose the field(s) you'd like to enrich and select from the list of available {{site.data.keyword.nlushort}} enrichments:

### Entity extraction
{: #entity-extraction}

Returns items such as persons, places, and organizations that are present in the input text. Entity extraction adds semantic knowledge to content to help understand the subject and context of the text that is being analyzed. The entity extraction techniques are based on sophisticated statistical algorithms and natural language processing technology, and are unique in the industry with their support for multilingual analysis and context-sensitive disambiguation. View the complete list of entity types and subtypes [here](/docs/services/discovery/entity-types.html). You can also create and add a [custom entity model](/docs/services/discovery/building.html#custom-entity-model) with {{site.data.keyword.knowledgestudiofull}}.

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

`sentiment` is calculated for entity types even if the **sentiment** enrichment is not selected. To learn more about sentiment scoring, see [Sentiment analysis](/docs/services/discovery/building.html#sentiment-analysis).

The `relevance` score ranges from `0.0` to `1.0`. The higher the score, the more relevant the entity. The `disambiguation` field contains the disambiguation information for the entity, which includes the entity `subtype` information and links to the resource(s), if applicable. The `count` is the number of times the entity is mentioned in the document.

#### Using a custom entity model
{: #custom-entity-model}

If you wish to create a custom enrichment model, you can do so in {{site.data.keyword.knowledgestudiofull}} and import the model into {{site.data.keyword.discoveryshort}} by adding the ID in the `Custom Model ID` box of the {{site.data.keyword.discoveryshort}} tooling. For more information on integrating with {{site.data.keyword.knowledgestudiofull}}, see [Integrating with {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery/integrate-wks.html#integrating-with-watson-knowledge-studio). The custom {{site.data.keyword.knowledgestudiofull}} model will override the default Entity Extraction enrichment.

**Note:** Only one {{site.data.keyword.knowledgestudiofull}} model can be assigned to an enrichment.

### Relation extraction
{: #relation-extraction}

Recognizes when two entities are related and identifies the type of relation. You can also create and add a [custom relation model](/docs/services/discovery/building.html#custom-relation-model) with {{site.data.keyword.knowledgestudiofull}}.

View the complete list of relationship types [here](/docs/services/discovery/relation-types.html).

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

The related entities are listed in the `arguments`. The entity types that can be identified by the Relation Extraction enrichment can be found [here](/docs/services/discovery/relation-types.html#specific-entity-types).

The `score` ranges from `0.0` to `1.0`. The higher the score, the more relevant the relation.

#### Using a custom relation model
{: #custom-relation-model}

If you wish to create a custom enrichment model, you can do so in {{site.data.keyword.knowledgestudiofull}} and import the model into {{site.data.keyword.discoveryshort}} by adding the ID in the `Custom Model ID` box of the {{site.data.keyword.discoveryshort}} tooling. For more information on integrating with {{site.data.keyword.knowledgestudiofull}}, see [Integrating with {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery/integrate-wks.html#integrating-with-watson-knowledge-studio). The custom {{site.data.keyword.knowledgestudiofull}} model will override the default Relation extraction enrichment.

**Note:** Only one {{site.data.keyword.knowledgestudiofull}} model can be assigned to an enrichment.

### Keyword extraction
{: #keyword-extraction}

Important topics in your content that are typically used when indexing data, generating tag clouds, or when searching. The {{site.data.keyword.discoveryshort}} service automatically identifies supported languages in your input content, and then identifies and ranks keywords in that content.

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

`sentiment` is calculated for keywords even if the **sentiment** enrichment is not selected. To learn more about sentiment scoring, see [Sentiment analysis](/docs/services/discovery/building.html#sentiment-analysis).

The `relevance` score ranges from `0.0` to `1.0`. The higher the score, the more relevant the keyword.

### Category classification

Categorizes input text, HTML, or web-based content into a hierarchical taxonomy up to five levels deep. Deeper levels allow you to classify content into more accurate and useful subsegments. View the complete list of categories [here](/docs/services/discovery/categories.html).

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

The `label` is the detected category. The hierarchy levels are separated by forward slashes. The `score` for that category will range from `0.0` to `1.0`. The higher the score, the greater the confidence in that category.

### Concept tagging
{: #concept-tagging}

Identifies concepts with which the input text is associated, based on other concepts and entities that are present in that text. Concept tagging understands how concepts relate, and can identify concepts that are not directly referenced in the text. For example, if an article mentions CERN and the Higgs boson, the Concepts API functions will identify Large Hadron Collider as a concept even if that term is not mentioned explicitly in the page. Concept tagging enables higher level analysis of input content than just basic keyword identification.

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

`sentiment` is calculated for relations even if the **sentiment** enrichment is not selected. To learn more about sentiment scoring, see [Sentiment analysis](/docs/services/discovery/building.html#sentiment-analysis). It will not extract `entities` or `keywords` (as shown in the example) unless you also select the **entity** and **keyword** enrichments. See [Entity extraction](/docs/services/discovery/building.html#entity-extraction) and [Keyword extraction](/docs/services/discovery/building.html#keyword-extraction) for more information on those enrichments.

The `subject`, `action`, and `object` are extracted for every sentence that contains a relation.

### Sentiment analysis
{: #sentiment-analysis}

Identifies attitude, opinions, or feelings in the content that is being analyzed. The {{site.data.keyword.discoveryshort}} service can calculate overall sentiment within a document, sentiment for user-specified targets, entity-level sentiment, quotation-level sentiment, directional-sentiment, and keyword-level sentiment. The combination of these capabilities supports a variety of use cases ranging from social media monitoring to trend analysis.

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

Emotion Analysis analyzes your text and calculates a score for each emotion (anger, disgust, fear, joy, sadness) on a scale of `0.0` to `1.0`. If the score of any emotion is `0.5` or higher, then that emotion has been detected (the higher the score above `0.5`, the higher the relevance). In the snippet shown, `joy` has a score above 0.5, so {{site.data.keyword.watson}} detected joy.

**Note:** Emotion Analysis is supported in English only.

### Element classification
{: #elements}

Parses elements (sentences, lists, tables) in governing documents to classify important types and categories
For more information, see [Element classification](/docs/services/discovery/element-classification.html).

#### Enrichment pricing
{: #enrichment-pricing}

Enrichment pricing information is available on [{{site.data.keyword.Bluemix_notm}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window}.

#### Enrichment language support
{: #enrichment-language-support}

For information about enrichment language support, see [{{site.data.keyword.discoveryshort}} language support](/docs/services/discovery/language-support.html).

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

Since the **Concept tagging** enrichment understands how concepts relate, it can identify concepts that are not directly referenced in the text. For example, if an article mentions CERN and the Higgs boson, it will identify Large Hadron Collider as a concept even if that term is not mentioned explicitly. Since our example document text is only one sentence, there are no related concepts, so **Concept tagging** returns the following concepts:

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

## Normalizing data
{: #normalizing-data}

The last step in customizing your configuration file is doing a final cleanup, also known as normalization.

In the **Normalize** section of the {{site.data.keyword.discoveryshort}} tooling:

-   You can move, merge, copy or remove fields.
-   Empty fields (fields that contain no information) will be deleted by default. You can change that using the **Remove empty fields** toggle.

After making any changes, click **Apply and Save**, then **Done**. You will be returned to the **Manage Data** screen, where you can apply this configuration to the collection of your choice.

**Note:** You cannot specify the `data type` (For example: `text` or `date`) of fields. During document ingestion, if a field is detected that does not yet exist in the index, {{site.data.keyword.discoveryshort}} will automatically detect the `data type` of that field based on the value of the field for the first document indexed.

If using the **Element Classification** enrichment, you cannot perform post-enrichment normalization.

## Normalizing entities
{: #normalizing-entities}

### Using CSS selectors to extract fields
{: #using-css}

You can perform an additional normalization by using CSS selectors via the Discovery API.

If you are ingesting well-formed HTML, you can normalize it, use CSS selectors to extract JSON fields from it, and then apply enrichments to the extracted fields. Edit your configuration file to enable this feature. Specifically, add an `extracted_fields` element to the `conversions/html` hierarchy, then specify field names, CSS selectors, and field types, as follows:

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

-   `field_name` — The name of the field that will be added to the JSON output.
-   `CSS_selector_expression` — The CSS selector that is to be run against the input HTML to extract the fields. The expression can have one or more matches.

    Valid CSS selectors are those specified by the [JSoup parser ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://jsoup.org/apidocs/org/jsoup/select/Selector.html){: new_window} and its [selector syntax ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://jsoup.org/cookbook/extracting-data/selector-syntax){: new_window}. A short list is provided at [Common selectors](/docs/services/discovery/building.html#common-selectors).
-   `field_type` — Either `array` or `string`. If the field type is not specified, it defaults to `array`. Note that type `string` can be enriched, but information stored in an `array` cannot be enriched unless the array's items are first extracted into text fields.

**Warning:** If a CSS selector matches both a parent node and one or more of its children, the text content of the nodes will be duplicated in the JSON output.

**Note:** Field names must meet the restrictions defined in [Field name requirements](/docs/services/discovery/custom-config.html#field_reqs).

The following JSON passage shows the relevant section of the Default Configuration to which you add CSS selector information.

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

Finally, the following passage shows the configuration the new name and description as well as some CSS selectors. The selectors match items in an HTML example that is described further down on this page.

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

After the preceding HTML is ingested and enhanced, the {{site.data.keyword.discoveryshort}} service returns the following JSON:

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

Some common CSS selectors include the following:

  - `tag` — Matches the `tag` name
  - `.class` — Matches the value of `class`
  - `#id` — Matches the value of `id`
  - `[attribute]` — Matches any tag with the specified `attribute`, regardless of value
  - `[attribute=value]` or `[attribute="value"]` — Matches the specified `attribute` and `value`

## Splitting documents with document segmentation
{: #doc-segmentation}

You can split your Word, PDF, and HTML documents into segments based on HTML heading tags. Once split, each segment is a separate document that will be enriched and indexed separately. Since queries will return these segments as separate documents, document segmentation can be used to:

  - Perform aggregations on individual segments of a document. For example, your aggregation would count each time a segment mentions a specific entity, instead of only counting it once for the entire document.
  - Perform relevancy training on segments instead of documents, which will improve result reranking.

The segments are created when the documents are converted to HTML (Word and PDF documents are converted to HTML before they are converted to JSON). Documents can be split based on the following HTML tags: `h1` `h2` `h3` `h4` `h5` and `h6`.

Considerations:

  - The number of segments per document is limited to `250`. Any document content remaining after `249` segments will be stored within segment `250`.

  - Each segment counts towards the document limit of your plan. {{site.data.keyword.discoveryshort}} will index segments until the plan limit is reached. See [Discovery pricing plans](/docs/services/discovery/pricing-details.html) for document limits.

  - You can not normalize data (see [Normalizing data](/docs/services/discovery/building.html#normalizing-data)) or use CSS selectors to extract fields (see [Using CSS selectors to extract fields](/docs/services/discovery/building.html#using-css)) when using document segmentation.

  - Documents will segment each time the specified HTML tag is detected. Consequently, segmentation could lead to malformed HTML because the documents could be split before closing tags and after opening tags.

  - HTML, PDF, and Word metadata, as well as any custom metadata, is extracted and included in the index with each segment. Every segment of a document will include identical metadata.
  
  - Document segmentation is not supported when the **Element Classification** (`elements`) enrichment is specified.

  - Re-ingesting a segmented document has additional considerations, see [Updating a segmented document](/docs/services/discovery/building.html#update-seg).

### Performing segmentation
{: #performing-segmentation}

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

The first document segment will look like this:

```json
{
  "id": "94c686c3-a790-4d8d-ba42-2bddf01b311c",
  "segment_metadata": {
    "parent_id": "94c686c3-a790-4d8d-ba42-2bddf01b311c",
    "segment": 1,
    "total_segments": 3
  },
  "extracted_metadata": {
    "title": "Heading 1",
    "sha1": "45ede479df67d78f2205ea7e714843375d3029c0",
    "filename": "doc-with-different-heading-levels.html",
    "file_type": "html"
  },
  "text": "This is the text that falls under heading 1 and should be therefore split into its own segment.",
  "html": "<div name=\"section 2\">This is the text that falls under <b>heading 1</b> and should be therefore split into its own segment."
}
```
{: codeblock}

All segments will include an:

  - `id` - The `id` of this segment.
  - `segment_metadata` section which contains:
    - `parent_id` - The `parent_id` is the id of the original document. For the first segment, the `id` and `parent_id` will be identical.
    - `segment` - The number of this segment.
    - `total_segments` - The total number of segments the document was split into.
  - `extracted_metadata` section which contains:
    - `title` - The `title` field is extracted from the content of the heading tag in that segment (for example, `Chapter 1`). If the first segment does not include a heading tag, the `title` will be `no-title`.
    - `sha1` - Corresponds to the original document.
    - `filename` - Corresponds to the original document.
    - `file_type`- Corresponds to the original document.
  - `text` field
  - `html` field

### Updating a segmented document
{: #update-seg}

If a segmented document has been updated and needs to be ingested again, it can be replaced using the [Update document ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#update-doc){: new_window} method.

When updating a segmented document, the document should be uploaded using the POST method of the `/environments/{environment_id}/collections/{collection_id}/documents/{document_id}` API, specifying the contents of the `parent_id` field of one of the current segments as the `{document_id}` path variable.

When updating, all segments will be overwritten, unless the updated version of the document has fewer total sections than the original. Those older segments will remain in the index and may be individually deleted using the API. See the [API Reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-doc){: new_window} for details. You can identify how many segments were created by querying the `notices`. Each segment is given a `document_id` field that is comprised of the `{parent_id}`, followed by an underscore, followed by the segment number.

If any of the segments of the document that you intend to update have been ranked for relevancy training, you must first delete all the segments of that document and then ingest the updated document as a new document. This will result in a new `document_id` for each segment and any trained segments will need to be retrained. The trained index will become inaccurate if you don't delete the old content first.

Alternately, consider creating a new document that contains only the new content and ingest it separately. 
