---

copyright:
  years: 2015, 2018
lastupdated: "2018-01-23"

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

# Configuration reference

You can create your own {{site.data.keyword.discoveryshort}} ingestion configuration in JSON if your data has special [conversion](#conversion), [enrichment](#enrichment), or [normalization](#normalization) needs.
{: shortdesc}

 The following sections detail the structure of this JSON and the object that can be defined in it.

## Configuration structure
{: #structure}

A {{site.data.keyword.discoveryshort}} configuration is structured as follows:

```json
{
  "name": "Configuration Name",
  "description": "Descriptive text about the configuration",
  "conversions": {
    "word": {},
    "pdf": {},
    "html": {},
    "segment": {},
    "json_normalizations": []
  },
  "enrichments": [],
  "normalizations": []
}
```
{: codeblock}

The base JSON object contains the following items:

-  `"name": "Configuration Name"` - The name of your configuration
-  `"description": "Descriptive text about the configuration"` - A description of your configuration

The following objects and arrays must be defined to convert, enrich and normalize documents that are uploaded to your collection.

- `"conversions": {}` - How documents are transformed into JSON that can be enriched.
- `"enrichments": []` - Which enrichments are applied to which parts of the JSON.
- `"normalizations": []` - Any post enrichment adjustments that are required before the document is stored.

Additionally, the following items are added to the base object by {{site.data.keyword.discoveryshort}} when the configuration is created/updated:

```json
{
  "configuration_id": "4f5b7c7b-ebf4-4963-882e-27eff08f08e3",
  "created": "2017-09-13T14:45:03.575Z",
  "updated": "2017-09-13T14:45:03.575Z"
}
```
{: codeblock}

## Conversion
{: #conversion}

Converting documents takes the original source format and using one or more steps transforms it into JSON that can be used for the rest of the ingestion process. Depending on the type of file uploaded, the process is as follows:

- **PDF** files are converted to HTML using the `pdf` options, the resulting **HTML** is then converted to JSON using the `html` options, and finally the resulting **JSON** is converted using the `json` options.

- **Microsoft Word** files are converted to HTML using the `word` options, the resulting **HTML** is then converted to JSON using the `html` options, and finally the resulting **JSON** is converted using the `json` options.

- **HTML** files are converted to JSON using the `html` options, and the resulting **JSON** is converted using the `json` options.

- **JSON** files are converted using the `json` options.

These options are described in the following sections. After conversion has completed, [enrichment](#enrichment) and [normalization](#normalization) are performed before the content is stored.

### PDF
{: #pdf}

The `pdf` conversion object defines how PDF documents should be converted into HTML and has the following structure:

```json
"pdf": {
  "heading": {
    "fonts": [
      {
        "level": 1,
        "min_size": 24,
        "max_size": 80,
        "bold": false,
        "italic": true,
        "name": "arial"
      },
      {
        "level": 2,
        "min_size": 18,
        "max_size": 24,
        "bold": true,
        "italic": false,
        "name": "ariel"
      }
    ]
  }
},
```
{: codeblock}

When converting PDF files headings in those files can be identified (and converted into an appropriate HTML "`h`" tag) by identifying the size, font and style of each heading level. Heading levels can be specified multiple times if necessary in order to correctly identify all relevant sections. HTML heading levels are important to identify if you plan on extracting the contents using CSS selectors, or intend to split the document using document splitting. The `heading` object contains the `fonts` array and each item in that array specifies a heading level using the following parameters:

- `"level": INT` - *required* - the HTML `h` level that text identified with these parameters will be converted into.
- `"min_size": INT` - _optional_ - the smallest font size that is identified as this heading level.
- `"max_size": INT` - _optional_ - the largest font size that is identified as this heading level.
- `"bold": boolean` - _optional_ - When `true` only bold fonts are identified as this heading level.
- `"italic": boolean` - _optional_ - When `true` only italic fonts are identified as this heading level.
- `"name": "string"` - _optional_ - The name of the font that is identified as this heading level.

For an area of text to be identified as a heading it must match all of the parameters defined in the specific array item. If the parameters defined are too flexible, you may have more headings identified than you anticipated. You will have better results if you strictly define each heading level multiple times to ensure all heading level variations are included without invalid matches.


### Word
{: #word}

The `word` conversion object defines how PDF documents should be converted into HTML and has the following structure:

```json
"word": {
  "heading": {
    "fonts": [
      {
        "level": 1,
        "min_size": 24,
        "bold": true,
        "italic": false,
        "name": "arial"
      },
      {
        "level": 2,
        "min_size": 18,
        "max_size": 23,
        "bold": true,
        "italic": false
      }
    ],
    "styles": [
      {
        "level": 1,
        "names": [
          "pullout heading",
          "pulloutheading",
          "header"
        ]
      },
      {
        "level": 2,
        "names": [
          "subtitle"
        ]
      }
    ]
  }
},
```
{: codeblock}

The Microsoft Word conversion object works in a similar way to the PDF conversion object. However, there are two different arrays that can be specified inside the `heading` object when extracting headings from Microsoft Word documents. You can use either or both heading extraction arrays to extract heading level elements from your Microsoft Word documents.

Each item in the `fonts` array specifies a heading level using the following parameters using font characteristics:

- `"level": INT` - *required* - the HTML `h` level that text identified with these parameters will be converted into.
- `"min_size": INT` - _optional_ - the smallest font size that is identified as this heading level.
- `"max_size": INT` - _optional_ - the largest font size that is identified as this heading level.
- `"bold": boolean` - _optional_ - When `true` only bold fonts are identified as this heading level.
- `"italic": boolean` - _optional_ - When `true` only italic fonts are identified as this heading level.
- `"name": "string"` - _optional_ - The name of the font that is identified as this heading level.

For an area of text to be identified as a heading in the `font` array it must match all of the parameters defined in the specific array item. If the parameters defined are too flexible, you may have more headings identified than you anticipated. You will have better results if you strictly define each heading level multiple times to ensure all heading level variations are included without invalid matches.

Each item in the `styles` array specifies a heading level from the Microsoft Word styles that are applied to that paragraph.

- `"level": INT` - *required* - the HTML `h` level that text identified with these parameters will be converted into.
- `"names": array` - *required* - a comma separated array of style names that will be identified as this heading level.

*When to use fonts and when to use styles* - If your Microsoft Word documents conform well to the style sheet with each paragraph correctly tagged with the appropriate style, then it is recommended that you use `styles` to extract headings. However, you may find that some documents have styles that have been manually overwritten by the writer. These documents are more likely to provide good conversion when the `fonts` extraction method is used.
{: tip}


### HTML
{: #html}

```json
"html": {
  "exclude_tags_completely": [
    "script",
    "sup"
  ],
  "exclude_tags_keep_content": [
    "font",
    "em"
  ],
  "exclude_content": {
    "xpaths": [
      "//*[@id='list-old']",
      "//*[@id='unstable']"
    ]
  },
  "keep_content": {
    "xpaths": [
      "//*[@id='footer']",
      "//*[@id='header']"
    ]
  },
  "exclude_tag_attributes": [
    "EVENT_ACTIONS"
  ],
  "keep_tag_attributes": [
    "id"
  ],
  "extracted_fields": {
    "{field_name}": {
      "css_selector": "{CSS_selector_expression_1}",
      "type": "{field_type}"
    }
  }
},
```
{: codeblock}

#### exclude_tags_completely

`"exclude_tags_completely" : array` - An array of HTML tag names that will be excluded. This includes the tag, the content and any tag attributes that are defined.

#### exclude_tags_keep_content

`"exclude_tags_keep_content" : array` - An array of HTML tag names where the tag information is removed. This results in the HTML tag and any tag attributes being stripped. The content of the tag is not further stripped unless specified. For example if you specify `exclude_tags_keep_content` for the `span` HTML tag, then `<span class="info">Some <strong>Information</strong></span>` will be stripped to: `Some <strong>Information</strong>`

#### exclude_content

`"xpaths" : array` - An array of XPaths that identify content that is removed. If this value is set, anything that matches one of the XPaths are removed from the output.

#### keep_content

`"xpaths" : array` - An array of XPaths that identify content that is converted. If this value is set, anything that matches one of the XPaths are included in the output. The inclusions specified by this parameter are processed after any processing specified by `exclude_content`.

#### exclude_tag_attributes

`"exclude_tag_attributes" : array` - An array of HTML attribute names that are removed by the conversion regardless of which HTML tag they are present in. **Note:** You will receive an error message if you specify both `exclude_tag_attributes` and `keep_tag_attributes` in the same configuration - only one may be specified per configuration. If present, `keep_tag_attributes` must be completely removed from the configuration; it cannot be present as an empty array.

#### keep_tag_attributes

`"keep_tag_attributes" : array` - An array of HTML attribute names that are retained by the conversion. **Note:** You will receive an error message if you specify both `keep_tag_attributes` and `exclude_tag_attributes` in the same configuration - only one may be specified per configuration. If present, `exclude_tag_attributes` must be completely removed from the configuration; it cannot be present as an empty array.

#### extracted_fields

This object defines any content from the HTML source that is to be extracted into a separate JSON field as part of the conversion. The content is identified by using CSS selectors.

Each field that you want to create is defined by an object as follows:

```json
"{field_name}": {
  "css_selector": "{CSS_selector_expression_1}",
  "type": "{field_type}"
}
```
{: codeblock}

- `"{field_name}"` - The name of the field to be created.

**Note:** Field names defined in your configuration must meet the restrictions defined in [Field Name Requirements](#field_reqs).

- `"css_selector" : string` *required* - a CSS selector expression that defines the area of content to be stored in a field.
- `"type" : string` *required* - The type of field to be created, can be `string`, `date`
For detailed information, see [Using CSS selectors to extract fields](/docs/services/discovery/building.md#using-css).

### Segment
{: #segment}

The `segment` object is a set of configuration options that split ingested documents into one or more segments based on the identified HTML headings (`h1`, `h2`).

```json
"segment": {
  "enabled": true,
  "selector_tags": ["h1", "h2", "h3", "h4", "h5", "h6"]
}
```
{: codeblock}

- `"enabled": boolean` - *required* - must be set to `true` to enable document segmentation.
- `"selector_tags": array` - *required* - a comma separated array of HMTL `h` tags on which to split documents.

As an overview, when document segmentation is enabled the following cannot be specified:

-  `json_normalizations` cannot be specified as part of the configuration.
-  `normalizations` cannot be specified as part of the configuration.
-  The `extracted_fields` option of the `html` conversion cannot be specified as part of the configuration.

For detailed information, see [Performing segmentation](/docs/services/discovery/building.html#performing-segmentation).


### JSON
{: #json}

You can perform pre-enrichment normalization of the ingested JSON by defining `operation` objects in the `json_normalizations` array.

```json
"json_normalizations": [
  {
    "operation": "remove",
    "source_field": "header"
  },
  {
    "operation": "copy",
    "source_field": "title",
    "destination_field": "title_old"
  },
  {
    "operation": "move",
    "destination_field": "content",
    "source_field": "body"
  },
  {
    "operation": "merge",
    "source_field": "synopsis",
    "destination_field": "preamble"
  },
  {
    "operation": "remove_nulls"
  }
]
```
{: codeblock}

#### Operations objects
{: #operations}

- `"operation": string` - *required* - the operation that will be performed on the JSON, must be one of the following:
  - `remove` - the specified `source_field` will be removed from the JSON.
  - `copy` - the specified `source_field` content will be copied to a new instance of the `destination_field`.
  - `move` - the specified `source_field` is renamed to the `destination_field`. If the `destination_field` already exists a new instance of the `destination_field` is created.
  - `merge` - the contents of the `source_field` and the `destination_field` are merged into the `destination_field`.
  - `remove_nulls` - fields with `null` content are removed.
- `"source_field": string` - _optional_ - the field that the operation will be performed on.
- `"destination_field": string` - _optional_ - the destination field the the operation will output to.  

  **Note:** Field names defined in your configuration must meet the restrictions defined in [Field Name Requirements](#field_reqs).


## Enrichments
{: #enrichments}

```json
"enrichments": [
  {
    "enrichment": "elements",
    "source_field": "html",
    "destination_field": "enriched_html",
    "options": {
      "model": "contract"
    }
  },
  {
    "enrichment": "natural_language_understanding",
    "source_field": "title",
    "destination_field": "enriched_title",
    "options": {
      "features": {
        "keywords": {
          "sentiment": true,
          "emotion": false,
          "limit": 50
        },
        "entities": {
          "sentiment": true,
          "emotion": false,
          "limit": 50,
          "mentions": true,
          "mention_types": true,
          "sentence_locations": true,        
          "model": "WKS-model-id"
        },
        "sentiment": {
          "document": true,
          "targets": [
            "IBM",
            "Watson"
          ]

        },
        "emotion": {
          "document": true,
          "targets": [
            "IBM",
            "Watson"
          ]
        },
        "categories": {},
        "concepts": {
          "limit": 8
        },
        "semantic_roles": {
          "entities": true,
          "keywords": true,
          "limit": 50
        },
        "relations": {
          "model": "WKS-model-id"
        }
      }
    }
  }
]
```
{: codeblock}

{{site.data.keyword.discoveryshort}} supports adding {{site.data.keyword.nlushort}} and Element Classification enrichments. Each field that you want to enrich is defined by an object in the `enrichments` array. Each enrichment object requires a `source_field`, a `destination_field` and enrichments to specified.

- `"enrichment" : string` - *required* - The type of enrichment to use on this field. To extract {{site.data.keyword.nlushort}} enrichments use `natural_language_understanding`, to perform Element Classification use `elements`.

  **Note:** When using the `elements` enrichment, it is important to follow the guidelines specified in [Element Classification](/docs/services/discovery/element-classification.html) documentation. Specifically, only PDF files can be ingested when this enrichment is specified.

- `"source_field" : string` - *required* - The source field that will be enriched. This field must exist in your source after the `json_normalizations` operation has completed.
- `"destination_field" : string` - *required* - The name of the container object where enrichments will be created.

  **Note:** Field names defined in your configuration must meet the restrictions defined in [Field Name Requirements](#field_reqs).

### Element Classification enrichments

When using Element Classification, each `elements` enrichment object must contain an `"options": {}` object with the following parameters specified:

- `"model" : string` - *required* - The element extraction model to be used with on this document. Currently supported models are: `contract`

**Note:** When using the `elements` enrichment, it is important to follow the guidelines specified in [Element Classification](/docs/services/discovery/element-classification.html) documentation. Specifically, only PDF files can be ingested when this enrichment is specified.

### Natural Language Understanding Enrichments

When using {{site.data.keyword.nlushort}}, each object within the `enrichments` array must also contain an `"options": { "features": { } }` object that contains one or more of the following enrichments:

### categories

The `categories` enrichment identifies any general categories in the ingested document. This enrichment has no options and must be specified as an empty object `"categories" : {}`

### concepts

The `concepts` enrichment finds concepts with which the input text is associated, based on other concepts and entities that are present in that text.

- `"limit" : INT` - *required* - The maximum number of concepts to extract from the ingested document.

### emotion

The `emotion` enrichment evaluates the overall emotional tone (for example `anger`) of entire document or specified target strings in the entire document. This enrichment can only be used with English content.

- `"document" : boolean ` _optional_ - When `true` the emotional tone of the entire document is evaluated.
- `"targets" : array ` _optional_ - A comma-separated array of target strings of which to evaluate the emotional state within the document.

### entities

The `entities` enrichment extracts instances of known entities such as people, places, and organizations. Optionally, a {{site.data.keyword.knowledgestudioshort}} custom model can be specified to extract custom entities.

- `"sentiment" : boolean` - _optional_ - When `true`, sentiment analysis is performed on the extracted entity in the context of the surrounding content.
- `"emotion" : boolean` - _optional_ - When `true`, emotional tone analysis is performed on the extracted entity in the context of the surrounding content.
- `"limit" : INT` - _optional_ - The maximum number of entities to extract from the ingested document. The default is `50`.
- `"mentions": boolean` - _optional_ - When `true`, the number of times that this entity is mentioned is recorded. The default is `false`.
- `"mention_types": boolean` - _optional_ - When `true`, the mention type for each mention of this entity is stored. The default is `false`.
- `"sentence_location": boolean` - _optional_ - When `true`, the sentence location of each entity mention is stored. The default is `false`.
- `"model" : string` - _optional_ - When specified, the custom model is used to extract entities instead of the public model. This option requires a {{site.data.keyword.knowledgestudioshort}} custom model to be associated with your instance of {{site.data.keyword.discoveryshort}}. See [Integrating with Watson Knowledge Studio](/docs/services/discovery/integrate-wks.html) for more information.

### keywords

The `keywords` enrichment extracts instances of significant words within the text. To understand the difference between keywords, concepts, and entities see: [Understanding the difference between Entities, Concepts, and Keywords](/docs/services/discovery/building.html#udbeck).

- `"sentiment" : boolean` - _optional_ - When `true`, sentiment analysis is performed on the extracted keyword in the context of the surrounding content.
- `"emotion" : boolean` - _optional_ - When `true`, emotional tone analysis is performed on the extracted keyword in the context of the surrounding content.
- `"limit" : INT` - _optional_ - The maximum number of keywords to extract from the ingested document. The default is `50`.

### semantic_roles

The `semantic_roles` enrichment identifies sentence components such as subject, action, and object within the ingested text.

- `"entities" : boolean` - _optional_ When `true`, entities are extracted from the sentence components.
- `"keywords" : boolean` - _optional_ When `true`, keywords are extracted from the sentence components.
- `"limit" : INT` - _optional_ - The maximum number of `semantic_roles` objects to extract (sentences to parse) from the ingested document. The default is `50`.

### sentiment

The `sentiment` enrichment evaluates the overall sentiment level of entire document or specified target strings in the entire document.

- `"document" : boolean ` _optional_ - When `true` the sentiment of the entire document is evaluated.
- `"targets" : array ` _optional_ - A comma-separated array of target strings to evaluate sentiment of within the document.

### relations

The `relations` enrichment extracts known relationships between identified entities within the document. Optionally, a {{site.data.keyword.knowledgestudioshort}} custom model can be specified to extract custom relationships.

- `"model" : string` - _optional_ - When specified, the custom model is used to extract relations instead of the public model. This option requires a {{site.data.keyword.knowledgestudioshort}} custom model to be associated with your instance of {{site.data.keyword.discoveryshort}}. See [Integrating with Watson Knowledge Studio](/docs/services/discovery/integrate-wks.html) for more information.

## Normalization
{: #normalization}

`normalizations` is an array of JSON `operation` objects that are used to clean the ingested JSON after the `enrichments` have been applied and before it is stored.

```json
"normalizations": [
  {
    "operation": "remove",
    "source_field": "enriched_title.entities.text"
  },
  {
    "operation": "copy",
    "source_field": "enriched_title.sentiment.document.score",
    "destination_field": "titlescore"
  }
]
```
{:codeblock}

The `operation` object options are listed [here](#operations)

## Field name requirements
{: #field_reqs}

Field names cannot contain spaces. The following characters and strings are reserved and cannot be used in field names:


```
  .  ,  # ? :
  id
  score
  highlight
  result_metadata
```
{: pre}

The characters `_`, `+`, and `-` cannot be used to prefix the `field_name`

Numerical characters `0 - 9` should not be the suffix of a field name (for example `extracted-content2`). These field names will be indexed, but cannot be queried.
