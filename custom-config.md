---

copyright:
  years: 2015, 2017
lastupdated: "2017-09-22"

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

# Custom configuration with JSON

You can create your own {{site.data.keyword.discoveryshort}} configuration in JSON if your data ingestion has special [conversion](#conversion), [enrichment](#enrichment), or [normalization](#normalization) needs.
{: shortdesc}

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
- `"enrichments": []` - What enrichments are applied to which parts of the JSON.
- `"normalizations": []` - Any post enrichment adjustments that are required before the document is stored.

Additionally, the following items are added to the base object by discovery when the configuration is created/updated and are returned .

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
        "name": "ariel"
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

### Word
{: #word}

```json
"word": {
  "heading": {
    "fonts": [
      {
        "level": 1,
        "min_size": 24,
        "bold": true,
        "italic": false
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
  ]
},
```
{: codeblock}


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

## Enrichments
{: #enrichments}

```json
"enrichments": [
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
          "limit": 50
        },
        "sentiment": {
          "document": true
        },
        "emotion": {
          "document": true
        },
        "categories": {},
        "concepts": {
          "limit": 8
        },
        "semantic_roles": {
          "entities": true,
          "keywords": true,
          "limit": 50
        }
      }
    }
  }
]
```
{: codeblock}

## Normalization
{: #normalization}

`normalizations` is an array of JSON `operation` objects that are used to clean the ingested JSON before it is stored.

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

The `operation` object options are listed [here](#operations)

{: codeblock}
