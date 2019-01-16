---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-01-15"

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

# Element Classification
{: #element-classification}

Element Classification makes it possible to rapidly parse through governing documents to convert, identify, & classify elements of importance. Using state of the art Natural Language Processing, party (who it refers to), nature (type of element), and category (specific class) are extracted from elements of a document.

Element Classification is designed to provide:

-  Natural Language Understanding of Contracts with emphasis on Software Procurement Contracts
-  The ability to convert programmatic PDF to annotated JSON
-  Identification of legal Entities and Categories that align with subject matter expertise

Element Classification brings together a functionally rich set of integrated, automated Watson APIs to input a programmatic PDF to identify: sections, lists (numbered and bulleted), footnotes, and tables converting these items into a structured HTML format. Furthermore, classification of this structured format is annotated and output as JSON with labeled elements, types and categories.

Element Classification securely transmits your data performing encryption in-flight and at rest. For information about IBM Cloud security, see the [{{site.data.keyword.Bluemix_notm}} Service Description ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=%28IBM+Cloud+Service+description%29){: new_window}

Element Classification returns a JSON object that contains:

-  A `documents` object that includes the input document's title, an HTML version of the input document, and the MD5 hash of the input document.
-  Information about the model used to classify the input document.  
-  An `elements` array that details semantic elements identified in the input document.
-  A `tables` array that breaks down the tables identified in the input document.
-  A `document_structure` object that lists section titles and leading sentences identified in the input document.
-  A `parties` array that lists the parties, roles, addresses, and contacts of parties identified in the input document.
-  Arrays defining `effective_dates`,`contract_amounts`, and `termination_dates`.

This feature is currently supported in English only, see [Language support](/docs/services/discovery/language-support.html#feature-support) for details.


## Classification requirements
{: #element-class}

To classify documents using Element Classification your configuration and source documents must meet the following requirements:

-  Files to be analyzed are in PDF format.
-  The PDF contents are in text form. Documents that have been scanned cannot be parsed, even if they have been OCRed.
   **Note:** You can identify a PDF that is in text by opening the document in a PDF viewer and using the  **Text select**  tool to select a single word. If you cannot select a single word in the document, the file cannot be parsed.
-  Files are no larger than 50Mb in size.
-  Secure PDFs (with a password to open) and editing restricted PDFs (with a password to edit) cannot be parsed.
-  The {{site.data.keyword.discoveryshort}} tooling includes a configuration named **Default Contract Configuration** that can be used to enrich your collection of PDF documents. You also have the option of creating a custom configuration that includes the `elements` enrichment. See [Collection requirements](/docs/services/discovery/element-classification.html#element-collection) for details.
-  **Lite** plans can process a maximum of 500 pages per month.
-  Not available in **Dedicated** environments.
-  Post-enrichment normalization cannot be performed when using Element Classification.

**Note:** The **Default Contract Configuration** file was updated on September 25, 2018. If you applied this configuration to a collection prior to this date, see the [release notes](/docs/services/discovery/release-notes.html#25sept) for information on updating your collection.

## Collection requirements
{: #element-collection}

To use Element Classification, your collection must be configured to meet specific requirements.

The {{site.data.keyword.discoveryshort}} tooling includes a configuration named **Default Contract Configuration** that has been pre-configured to enrich PDF documents with the **Element Classification** enrichment and other required options. You can choose this configuration when you create your collection. The JSON for this configuration is:

```json
 {
   "name": "Default Contract Configuration",
   "description": "Extract party, nature, and category from elements in PDFs.",
   "conversions": {
     "html": {
       "exclude_tags_completely": [],
       "exclude_tags_keep_content": []
     }
   },
   "enrichments": [
     {
       "source_field": "html",
       "destination_field": "enriched_html_elements",
       "enrichment": "elements",
       "options": {
         "model": "contract"
       }
     }
   ]
 }
```
{: codeblock}

If you wish to create a custom configuration file, configure your collection to meet the following requirements:  

-  `PDF` conversion settings are ignored if specified.
-  `WORD` conversion settings can be omitted as Microsoft Word files cannot be ingested when Element Classification is specified.
-  `html` normalization settings are ignored if specified.
-  Document segmentation is not supported when the `elements` enrichment is specified.
-  In the {{site.data.keyword.discoveryshort}} configuration, the `html` field must be enriched by the `elements` enrichment and the `model` specified as `contract`. In the following example, the `destination_field` is `enriched_html`, but any valid name can be used:

```json
 "enrichments": [
   {
     "source_field": "html",
     "destination_field": "enriched_html",
     "enrichment": "elements",
     "options": {
       "model": "contract"
     }
   }
 ]
```
{: codeblock}

After selecting the `Default Contract Configuration` in the tooling, you can upload your documents. If you are unfamiliar with creating collections and uploading documents, see [Getting started with the tooling](/docs/services/discovery/getting-started-tool.html).

## Classified Elements

Once a document has been indexed with Element Classification, it will be returned with an `elements` array as part of the searchable document.

Each object in the `elements` array describes an element of the contract that {{site.data.keyword.discoveryshort}} has identified. The following code represents a typical element:

```json
 {
    "location" : {
     "begin" : 134323,
     "end" : 135109
    },
    "text" : "9. In the event that the Participant's total vested account balance is determined to be less than or equal to $2,000.00 as of the date that the Order is received, the parties will be informed in writing that the QDRO determination fee may potentially liquidate the account.",
    "types" : [ {
      "label" : {
        "nature" : "Obligation",
        "party" : "All Parties"
      },
      "provenance_ids" : ["Nlu0ogWAEGms4vjhhzpMv3iXhm8b8fBqMBNtT/bXH8JI=", "PlyERkjg5is36RpFjVUFXp69eDmGmCxLCXRs1sDMDUCo="
      ]
    } ],
    "categories" : [ {
      "label" : "Communication",
      "provenance_ids" : [ "Cs38YyU6VBFtJK1/bgtEJBlqqWmX5F6OYUciRxQXf7HrN5TOCPuI7QXbkbj4LRXoxVuB3/i9H15q5TU+vFxorhUBeWFfF998OYQiPYViD2yI="
      ]
    } ],
    "attributes" : [ {
      "type" : "Currency",
      "text" : "$2,000.00",
      "location" : {
        "begin" : 134780,
        "end" : 134789
      }
    } ]
 }
 ```
{: codeblock}

Each element has five important sections:
-  `location`: The `begin` and `end` indexes indicating the location of the element in the input document.
-  `text`: The text of the classified element.
-  `types`: An array that includes zero or more `label` objects. Each `label` object includes a `nature` field that lists the effect of the element on the identified party (for example, `Right` or `Exclusion`) and a `party` field that identifies the party or parties affected by the element. See [Types](/docs/services/discovery/parsing.html#contract_types) in [Understanding contract parsing](/docs/services/discovery/parsing.html#contract_parsing) for additional information.
-  `categories`: An array that contains zero or more `label` objects. The value of each `label` object lists a functional category into which the identified element falls. See [Categories](/docs/services/discovery/parsing.html#contract_categories) in [Understanding contract parsing](/docs/services/discovery/parsing.html#contract_parsing) for additional information.
-  `attributes`: An array that lists zero or more objects that define attributes of the element. Currently supported attribute types include `Location` (geographic location referenced by the element), `DateTime` (date, time, date range, or time range specified by the element), and `Currency` (monetary values and units). Each object in the `attributes` array also includes the identified element's text and location; location is defined by the `begin` and `end` indexes of the text in the input document. See [Attributes](/docs/services/discovery/parsing.html#attributes) in [Parsing contracts](/docs/services/discovery/parsing.html#contract_parsing) for additional information.

Additionally, each object in the `types` and `categories` arrays includes a `provenance_ids` array. The values listed in the `provenance_ids` array are hashed values that you can send to IBM to provide feedback or receive support about the part of the analysis associated with the element. 

Some sentences do not fall under any type or category, in which case the service returns the `types` and `categories` arrays as empty objects.
{: note}

Some sentences cover multiple topics, in which case the service returns multiple sets of `types` and `categories` objects.
{: note}

Some sentences do not contain any identifiable attributes, in which case the service returns the `attributes` array as empty objects.
{: note}
