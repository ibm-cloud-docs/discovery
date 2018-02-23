---

copyright:
  years: 2015, 2018
lastupdated: "2018-01-15"

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

# Element Classification
{: #element-classification}

Element Classification makes it possible to rapidly parse through governing documents to convert, identify, & classify elements of importance. Using state of the art Natural Language Processing, party (who it refers to), nature (type of element), and category (specific class) are extracted from elements of a document.

Element Classification is designed to provide:

- Natural Language Understanding of Contracts with emphasis on Software Procurement Contracts
- The ability to convert programmatic PDF to annotated JSON
- Identification of legal Entities and Categories that align with subject matter expertise

Element Classification brings together a functionally rich set of integrated, automated Watson APIs to input a programmatic PDF to identify: sections, lists (numbered and bulleted), footnotes, and tables converting these items into a structured HTML format. Furthermore, classification of this structured format is annotated and output as JSON with labeled elements, types and categories.

Element Classification securely transmits your data performing encryption in flight and at rest. For information about IBM Cloud security, see the [IBM Cloud Service Description ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=IBM+Bluemix+Service+Description){: new_window}.

## Classification requirements

To classify documents using Element Classification your configuration and source documents must meet the following requirements:

- Files to be analyzed are in PDF format.
- The PDF contents are in text form (documents that have been scanned, but not OCRed cannot be parsed)

  **Note:** You can identify a PDF that is in text by opening the document in a PDF viewer and using the  **Text select**  tool to select a single word. If you cannot select a single word in the document, the file cannot be parsed.

- Files are no larger than 50Mb in size.
- Secure PDFs (with a password to open) and editing restricted PDFs (with a password to edit) cannot be parsed.
- A custom {{site.data.keyword.discoveryshort}} configuration must be created that includes the `elements` enrichment. This configuration can only be used to ingest PDF documents.
- **Lite** and **Standard** plans can process a maximum of 500 pages per month.
- Not available for service instances that are subscribed to a **Premium** plan, or in **Dedicated** environments.

## Collection requirements

To use Element Classification, your collection must be configured to meet specific requirements as follows:

- `PDF` conversion settings are ignored if specified.
- `WORD` conversion settings can be omitted as Microsoft Word files cannot be ingested when Element Classification is specified.
- `html` normalization settings are ignored if specified.
- Document splitting is not supported when the `elements` enrichment is specified.
- In the {{site.data.keyword.discoveryshort}} configuration, the `html` field must be enriched by the `elements` enrichment and the `model` specified as `contract`. In the following example, the `destination_field` is `enriched_html`, but any valid name can be used:

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

These options can be added using the {{site.data.keyword.discoveryshort}} tooling, create a custom configuration and add the **Element Classification** enrichment to the `html` field.

**Note:** When adding **Element Classification** using the tooling, the `destination_field` is set to `enriched_html_elements`.

After the custom configuration has been created it can be used in any collection, any method to upload documents can be used as long as the custom configuration is specified. If you are unfamiliar with creating collections and uploading documents, see [Getting started with the tooling](/docs/services/discovery/getting-started-tool.html).

## Classified Elements

Once a document has been indexed with Element Classification, it will be returned with an `elements` array as part of the searchable document.

Each object in the `elements` array describes an element of the contract that Element Classification has identified. The following code represents a typical element:

```
{
   "sentence" : {
     "begin" : 34941,
     "end" : 35307
   },
   "sentence_text" : "Buyer may, upon written notice to Supplier, terminate a SOW or WA.",
   "types" : [ {
     "label" : {
       "nature" : "Right",
       "party" : "Buyer"
     },
     "assurance" : "High"
   } ],
   "categories" : [ {
     "label : "Term & Termination",
     "assurance : "High"
     }
   ]
}
```

There are four important sections to the element:

- `sentence_text` – the text that was analyzed.
- `sentence` – this object describes where the element was found in the converted HTML, it contains a start character value and an end character value.
- `types` – this array describes what the element is and who it affects it consists of one or more sets of `party` (who is being affected by the sentence) and `nature` (the effect of the sentence on the identified party)
- `categories` – this array lists the functional categories (the subject matter) of the identified sentence.

**Note**: Some sentences do not fall under any type or category and in that case the `types` and `categories` arrays are returned empty.

**Note:**  Some sentences cover multiple topics and will therefore be returned with multiple `types` and `categories` items listed.

Additionally, any identified parties are also defined in the parties array:

```
  "parties" : [ {
    "party" : "Customer",
    "role" : "Buyer"
  } ]
```

There are two important sections to each element of the parties array:

- `party` – the text that was identified as a party within the document.
- `role` – the role of the party that has been identified. Roles change based on sub-domain, see the information on the specified sub-domain for a list of possible roles. Parties that cannot be identified to a specific role are labeled as `Unknown`.


## Understanding Contract Elements

Parsed contracts from Element Classification are returned with each identified element analyzed.

The following sections describe how the returned JSON describes the analysis.

### Type

The element `types` information is an array of objects, each object contains a nature and party that has been identified as a couplet for this element. The following tables describe the `nature` and `party` values that can be identified.

Nature is the type of action the sentence requires.

| **Nature** | **Description** |
| --- | --- |
| Definition | This element adds clarity for a term/relationship/etc. Action is not required to fulfill this element and no party is affected. |
| Disclaimer | The party in the element is not obligated to fulfill the specific terms in the element, but is not barred from doing so.  |
| Exclusion | The party in the element will not fulfill the specific terms laid out in the element.  |
| Obligation | The party in the element is required to fulfill the terms of the element.   |
| Right | The party in the element is guaranteed to receive the terms of the element.  |

### Parties

For each identified clause, affected parties are identified by name. Each identified party is then classified by `role`. Parties are the participants in the contract. The roles that can be identified for contract are as follows:

| **Role** | **Description** |
| --- | --- |
| `Buyer` | The party responsible for paying for the goods/services. |
| `End User` | The party who will interact with the actual goods/services, explicitly distinguished from the Buyer. |
| `None` | No party has been identified for this element, always paired with the Definition nature. |
| `Supplier` | The party responsible for providing the goods/services. |

### Categories

Categories define the subject matter of the sentence. The following currently supported categories can be identified:

| **Categories** | **Description** |
| --- | --- |
| `Assignments` | Encompasses the transfer of rights held by one party to another.  |
| `Confidentiality` | Describes how confidential or private information will be handled such as who can share what, and how. |
| `Deliverables` | The items or services to be delivered at the end of a piece of work. |
| `Dispute Resolution` | Provides for any dispute arising between contracting parties, and how it will be handled. |
| `Force Majeure` | A clause that frees both parties from liability in case of a disruptive event. |
| `Indemnification` | Describes the remedies or consequences if terms are breached. |
| `Insurance` | Describes the level of insurance coverage a supplier must carry. |
| `Intellectual Property` | A clause that relates to patents, copyrights and trademarks. More generally may relate to invention, authorship or know-how.  |
| `Liability` | Describes obligations and limitations on the responsibility of each party. |
| `Payment Terms & Billing` | Describes what payments are due and what the schedule for payment is.  |
| `Pricing & Taxes` | Describes how the prices are made up and how the taxes are to be applied |
| `Privacy` | Describes the privacy regulations which apply. |
| `Responsibilities` | Describes what the responsibilities of each party are. |
| `Term & Termination` | The time over which something will happen, and the conditions under which it may end.  |
| `Warranties` | Guarantee by a supplier of how a product will work. |

### Assurance

Every item (type or category) identified by Element Classification is given a `assurance` rating. The possible assurance values are described below:

| **Assurance** | **Description** |
| --- | --- |
| `High` | There is significant evidence that the classification given is representative of the content. |
| `Low` | There is some evidence to support the classification, but it may need further review to confirm. |
