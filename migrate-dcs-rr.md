---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-03"

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


# Migrating from Watson Document Conversion and Retrieve and Rank

{{site.data.keyword.documentconversionfull}} and {{site.data.keyword.retrieveandrankfull}} have been deprecated and replaced by {{site.data.keyword.discoveryfull}}. Typically, these two services are used together to ingest, rank, and then deliver results to your applications. This document is provided to guide you through the process of migrating from {{site.data.keyword.documentconversionshort}} and {{site.data.keyword.retrieveandrankshort}} to {{site.data.keyword.discoveryshort}}.

{{site.data.keyword.discoveryfull}} provides a more robust query interface, simplified data ingestion, improved training management, and increased scale. {{site.data.keyword.discoveryshort}} addresses many of the same core use cases as {{site.data.keyword.retrieveandrankshort}} including support agent assist, organizational knowledge base search, and research assistance. It was built with many of challenges faced by users of {{site.data.keyword.retrieveandrankshort}} in mind, and addresses many of those issues. {{site.data.keyword.discoveryshort}} also provides new capabilities for information retrieval not available in {{site.data.keyword.retrieveandrankshort}} including passage retrieval and improved search algorithms to find more relevant results.

**Feature Comparison**

| Feature | {{site.data.keyword.retrieveandrankshort}} | {{site.data.keyword.discoveryshort}} |
|:-------------|:--------------------:|:-------------:|
| Natural language search | Yes | Yes |
| Machine learning relevancy training | Yes | Yes |
| UI tooling for training | Yes | Yes |
| JSON answer unit input | Yes | Yes |
| Document splitting | Yes | Yes |
| Passage retrieval |   | Yes |
| Document CRUD | Yes | Yes |
| Batch JSON upload | Yes |   |
| Automatic document NLP enrichment |   | Yes |
| Custom NLP model integration for enrichment |   | Yes |
| Training data stored in service |   | Yes |
| Automated model lifecycle management |   | Yes |
| Semantic similarity to improve relevancy without training |   | Yes |
| Accuracy measure in tooling based on test set | Yes |   |
| Custom feature vector support | Yes |   |
| Custom analyzer configuration | Yes | Pre-configured |
| Custom Stopwords | Yes | Pre-configured |
| Custom language dictionaries | Yes | Pre-configured |
| Custom Synonyms | Yes | Yes |
**Note:** This table will be updated as new {{site.data.keyword.discoveryshort}} capabilities are added.

Before you begin the action of migrating, you must first [evaluate](#evaluate) the data stored in your {{site.data.keyword.retrieveandrankshort}} service and understand how you will move the different components that make up your current solution.

Most customers use {{site.data.keyword.documentconversionshort}} in conjunction with {{site.data.keyword.retrieveandrankshort}}. If you are not using {{site.data.keyword.documentconversionshort}} to convert content so that it can be stored in a searchable index, proceed to review [options for migrating standalone {{site.data.keyword.documentconversionshort}}](#dcs).

If you originally used the {{site.data.keyword.retrieveandrankshort}} tutorial and based your own instance of the service on that tutorial, an extension of the tutorial ingesting the same data into {{site.data.keyword.discoveryshort}} can be found [here](/docs/services/discovery/migrate-rnr-tut.html).

**Note:** Conversion and enrichment functionality is included with {{site.data.keyword.discoveryshort}}. If you have used {{site.data.keyword.documentconversionshort}}, and/or {{site.data.keyword.nlushort}} to convert and enrich source HTML, PDF, or Microsoft Word documents these services are replaced by features within the {{site.data.keyword.discoveryshort}} service.

## Evaluate your migration path to Watson Discovery service
{: #evaluate}

There are two practical options to migrate from {{site.data.keyword.retrieveandrankshort}}: migrating from source content, and migrating from indexed content. Evaluate both options before deciding which option to use.

### Migrating from source content
{: #source}

In order to migrate from the source content you will:

-  need to have access to the original source files that the content was ingested from.
-  need to programmatically extract the ID for each document (the result already has an ID before it is indexed)

If you can meet all of the migration criteria, it is recommended that you use this method to move to the {{site.data.keyword.discoveryshort}} service.

To migrate your source content, modify the procedure described in [the migration tutorial](/docs/services/discovery/migrate-rnr-tut.html) to meet the specifics of your source data.

#### Migrating answer units

If you created answer units using {{site.data.keyword.documentconversionshort}} choose one of the following options to migrate that content:

-  if you have trained a ranker and need to migrate the ranking, you should take the content that was returned from {{site.data.keyword.documentconversionshort}} and ingest that into {{site.data.keyword.discoveryshort}}
-  if you don't have any training data to migrate, ingest the original source documents into {{site.data.keyword.discoveryshort}} using the [document segmentation feature](/docs/services/discovery/building.html#doc-segmentation)

### Migrating from indexed content
{: #indexed}

You should migrate from the indexed content in {{site.data.keyword.retrieveandrankshort}} if you do not have access to the original source documents, or:

- you used automatic document ID generation and have trained a ranker.
- created answer units in {{site.data.keyword.documentconversionshort}} and ranked them but did not retain the answer units that were generated by the {{site.data.keyword.documentconversionshort}} service.

**Note:** This method is possible only if all the necessary content is in stored fields in {{site.data.keyword.retrieveandrankshort}}. If the content was only indexed but not stored, it will not be possible to query the content out of the service, and the data will have to be converted and split again from the source.

Documents are extracted from the service using the [/v1/solr_clusters/{solr_cluster_id}/solr/\{collection_name\}/select ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/retrieve-and-rank/api/v1/#index_doc){: new_window} method using a blank query `q=*:*`. The number of documents returned might be more than the practical maximum return count (`200` for most collections). If this is the case, multiple calls should be made with appropriate [paging ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://lucene.apache.org/solr/guide/6_6/pagination-of-results.html){: new_window} to collect all the documents.

Documents with specified **ID's** are uploaded to the {{site.data.keyword.discoveryshort}} service using the [/v1/environments/\{environment_id\}/collections/\{collection_id\}/documents/\{document_id\} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#update-a-document){: new_window} method. Each document upload is a separate API call.

## Migrating training data

After migrating your results, the next step is to migrate any training data that has been created for the content. There are two options for migrating training data: migrate from source (`csv`), and migrate from service. If you uploaded training data from a `csv` file and still have access to that file, you should migrate from source. If you used the {{site.data.keyword.retrieveandrankshort}} tooling or don't have access to the original `csv` file you should migrate from the service.

### Migrating training from source content
{: #csv}

In order to migrate from the ranking source content you will:

- need to have access to the original source `csv` files that the training information was originally uploaded with.
- ensure that the IDs of the trained documents when they are indexed in match the IDs of the trained documents when they were indexed in {{site.data.keyword.retrieveandrankshort}}.

If you can meet all of the migration criteria, it is recommended that you use this method to move training to the {{site.data.keyword.discoveryshort}} service.

To migrate your training data, modify the procedure described in [the migration tutorial](/docs/services/discovery/migrate-rnr-tut.html) to meet the specifics of your source data.

### Migrating training data from the service
{: #extract-train}

To migrate training data from the {{site.data.keyword.retrieveandrankshort}} service, you will need to: extract the training data using the {{site.data.keyword.retrieveandrankshort}} APIs, convert the {{site.data.keyword.retrieveandrankshort}} training JSON into a format usable by {{site.data.keyword.discoveryshort}}, and finally ingest the training data into {{site.data.keyword.discoveryshort}} using the API.

To extract training data from {{site.data.keyword.retrieveandrankshort}}, use the `Export` function inside the {{site.data.keyword.retrieveandrankshort}} tooling. After successfully downloading a complete export, extract the saved `.zip` file. Inside the archive are two files. The training data is stored in the one named `export-questions.json`. This file contains an array of JSON training objects.

Each training result in the array is presented in the following form:

**Sample {{site.data.keyword.retrieveandrankshort}} Training Data**
```json
{
    "text":"Who was the first royal to attend Wimbledon?",
    "cluster":{
        "id":"f62c11d3-30fa-11e7-8a0c-333f7f431ce8",
        "answers":{
            "f62c11d3-30fa-11e7-8a0c-33":[
                {
                    "id":"dac41335-0e96-40c9-983f-cc3f1c395782",
                    "ranking":1,
                    "source":{
                        "id":"e26a3d20-30fa-11e7-aa5e-d1632b06e0b1",
                        "file":"wimbledon-wikipedia.html",
                        "sequence":17,
                        "strategy":"retrieve"
                    }
                },
                {
                    "id":"661b4c9f-ecdb-4dad-aafc-6ae561a148c0",
                    "ranking":2,
                    "source":{
                        "id":"da1bc620-30fa-11e7-8f90-3305f35a93c9",
                        "file":"generated-otherFactsFigures.docx",
                        "sequence":67,
                        "strategy":"retrieve"
                    }
                },
                {
                    "id":"0053fdb8-c77e-4fcf-b0e0-6a4cd377266a",
                    "ranking":3,
                    "source":{
                        "id":"d9c0add0-30fa-11e7-aa5e-d1632b06e0b1",
                        "file":"generated-allEngland.docx",
                        "sequence":20,
                        "strategy":"retrieve"
                    }
                },
                {
                    "id":"506d3d50-19ed-49c8-b32f-65f848e60e86",
                    "ranking":4,
                    "source":{
                        "id":"da1bc620-30fa-11e7-8f90-3305f35a93c9",
                        "file":"generated-otherFactsFigures.docx",
                        "sequence":63,
                        "strategy":"retrieve"
                    }
                }
            ]
        },
        "flags":{

        }
    }
},
```
{: codeblock}

{{site.data.keyword.discoveryshort}} does not require all the information that is exported from {{site.data.keyword.retrieveandrankshort}}. The following snippet shows the required structure of a {{site.data.keyword.discoveryshort}} training entry.

```json
{
  "natural_language_query": "{natural_language_query}",
  "examples": [
    {
      "document_id": "{document_id_1}",
      "relevance": 0
    },
    {
      "document_id": "{document_id_2}",
      "relevance": 10
    }
  ]
}
```
{: codeblock}

At this point, you will need to translate your {{site.data.keyword.retrieveandrankshort}} training information into {{site.data.keyword.discoveryshort}} training information. Consider the following points when converting.

- **Not relevant** is specified by a `relevance` score of `0` in {{site.data.keyword.discoveryshort}}, but it is specified by a `ranking` of `1` in {{site.data.keyword.retrieveandrankshort}} - all `"ranking": 1` entries must be converted to `"relevance": 0` in {{site.data.keyword.discoveryshort}}
- The {{site.data.keyword.discoveryshort}} tooling uses a binary scale of `0` and `10`. If you want to rank more results and use the {{site.data.keyword.discoveryshort}} tooling, you must convert all `"ranking": 1` and `"ranking": 2` entries to `"relevance": 0`, and all `"ranking": 3` and `"ranking": 4` entries to `"relevance": 10`. This is not required if you are not ranking additional results, or are not using the {{site.data.keyword.discoveryshort}} tooling.
- Unanswered questions are not required by {{site.data.keyword.discoveryshort}}, checking the validity of relevance training is performed manually.

![Ranking migration flow](images/migrate-ranking.png)

As an example, the **Sample {{site.data.keyword.retrieveandrankshort}} Training Data** listed above would be converted to be used in {{site.data.keyword.discoveryshort}} tooling as follows:

```json
{
  "natural_language_query": "Who was the first royal to attend Wimbledon?",
  "examples": [
    {
      "document_id": "e26a3d20-30fa-11e7-aa5e-d1632b06e0b1",
      "relevance": 0
    },
    {
      "document_id": "da1bc620-30fa-11e7-8f90-3305f35a93c9",
      "relevance": 0
    },
    {
      "document_id": "d9c0add0-30fa-11e7-aa5e-d1632b06e0b1",
      "relevance": 10
    },
    {
      "document_id": "da1bc620-30fa-11e7-8f90-3305f35a93c9",
      "relevance": 10
    }
  ]
}
```
{: codeblock}

## Language support
{: #language}

See the [language support table for {{site.data.keyword.discoveryshort}}](/docs/services/discovery/language-support.html). {{site.data.keyword.retrieveandrankshort}} features are primarily supported by **Basic** {{site.data.keyword.discoveryshort}} language support.

## Migrating queries
{: #queries}

The {{site.data.keyword.discoveryfull}} query language is different to the Solr query language used by {{site.data.keyword.retrieveandrankshort}}. Existing queries should be rerouted to one of the {{site.data.keyword.discoveryfull}} query methods and converted to use the {{site.data.keyword.discoveryfull}} query language. The following table describes some of the typical operators that are used in most queries:

**Migrating from Solr querying to {{site.data.keyword.discoveryshort}} - Typical operators**

| Solr Operator | Discovery Operator | Description |
|:-------------:|--------------------|-------------|
| `.` | `.` | JSON delimiter |
| `:` | `:` | Includes |
|  | `::` | Exact match |
| `-{fieldname}:` | `:!` | Does not include |
|  | `::!` | Not an exact match |
| `\` | `\` | Escape character |
| `""` | `""` | Phrase query |
| `()` | `()`, `[]` | Nested grouping |
| `OR` | [<code>&#124;</code>] | or |
| `AND` | [,] | and |
| `[* TO 100]` | `<=`, `>=`, `>`, `<` | Numerical comparisons |
| `^x` | `^x` | Score multiplier |
| `*` | `*` | Wildcard |
| `~`(0 to 1) | [~n] | String variation |

Consult the [Query concepts](/docs/services/discovery/using.html) and [Query reference](/docs/services/discovery/query-reference.html) documentation for detailed information about the {{site.data.keyword.discoveryfull}} query language.


## Standalone Watson Document Conversion service migration
{: #dcs}

If you are using {{site.data.keyword.documentconversionshort}} to help ingest content into {{site.data.keyword.retrieveandrankshort}}, then that functionality has evolved into a single service - {{site.data.keyword.discoveryshort}}. {{site.data.keyword.discoveryshort}} lets you easily convert, enrich, and ingest Microsoft Word, PDF, HTML, and JSON documents into a trainable and searchable index. This section is relevant to you if your use case doesn't involve storing the converted content in an index. If you are ingesting documents into an index, see [ingesting to the {{site.data.keyword.discoveryshort}} service](/docs/services/discovery/building.html).

IBM no longer provides a service that is designed for standalone conversion of Microsoft Word, PDF, and HTML documents. If you are currently using the {{site.data.keyword.documentconversionshort}} service and do not ingest the output into an online indexed service (such as {{site.data.keyword.discoveryshort}}), it is recommended that you consider migrating to an open-source alternative such as [Apache Tika ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://tika.apache.org/){: new_window}.
