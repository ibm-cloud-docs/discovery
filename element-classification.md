---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-05"

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

This feature is currently supported in English only, see [Language support](/docs/services/discovery/language-support.html#feature-support) for details. 

## Classification requirements
{: #element-class}

To classify documents using Element Classification your configuration and source documents must meet the following requirements:

- Files to be analyzed are in PDF format.
- The PDF contents are in text form. Documents that have been scanned cannot be parsed, even if they have been OCRed.

  **Note:** You can identify a PDF that is in text by opening the document in a PDF viewer and using the  **Text select**  tool to select a single word. If you cannot select a single word in the document, the file cannot be parsed.

- Files are no larger than 50Mb in size.
- Secure PDFs (with a password to open) and editing restricted PDFs (with a password to edit) cannot be parsed.
- The {{site.data.keyword.discoveryshort}} tooling includes a configuration named **Default Contract Configuration** that can be used to enrich your collection of PDF documents. You also have the option of creating a custom configuration that includes the `elements` enrichment. See [Collection requirements](/docs/services/discovery/element-classification.html#element-collection) for details.
- **Lite** and **Standard** plans can process a maximum of 500 pages per month.
- Not available in **Dedicated** environments.
- Post-enrichment normalization cannot be performed when using Element Classification.

## Collection requirements
{: #element-collection}

To use Element Classification, your collection must be configured to meet specific requirements.

The {{site.data.keyword.discoveryshort}} tooling includes a configuration named **Default Contract Configuration** that has been pre-configured to enrich PDF documents with the **Element Classification** enrichment and other required options. You can choose this configuration when you create your collection. The JSON for this configuration is: 

```json
{
  "description": "Extract party, nature, and category from elements in PDFs.",
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

- `PDF` conversion settings are ignored if specified.
- `WORD` conversion settings can be omitted as Microsoft Word files cannot be ingested when Element Classification is specified.
- `html` normalization settings are ignored if specified.
- Document segmentation is not supported when the `elements` enrichment is specified.
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

After selecting the `Default Contract Configuration` in the tooling, you can upload your documents. If you are unfamiliar with creating collections and uploading documents, see [Getting started with the tooling](/docs/services/discovery/getting-started-tool.html).

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

There are five important sections to the element:

- `sentence_text` – the text that was analyzed.
- `attributes` – this array lists one or more attributes of the element. Currently supported objects in the `attributes` array include `Location` (geographic location or region referenced by the element), `DateTime` (date, time, date range, or time range specified by the element), and `Currency` (monetary values and units). 
- `categories` – An array that lists the functional categories into which the identified sentence falls; in other words, the subject matter of the sentence.
- `types`– An array that describes what the element is and whom it affects. It consists of one or more sets of `nature` keys (the effect of the sentence on the identified `party`) and `party` keys (whom the sentence affects).
- `sentence`– An object that describes where the element was found in the converted HTML. It contains a `start` character value and an `end` character value.

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
{: #contract-elements}

Parsed contracts from Element Classification are returned with each identified element analyzed.

The following sections describe how the returned JSON describes the analysis.

### Type

The element `types` information is an array of objects, each object contains a nature and party that has been identified as a couplet for this element. The following tables describe the `nature` and `party` values that can be identified.

Nature is the type of action the sentence requires.

| **Nature** | **Description** |
| --- | --- |
| `Definition` | This element adds clarity for a term/relationship/etc. Action is not required to fulfill this element and no party is affected. |
| `Disclaimer` | The party in the element is not obligated to fulfill the specific terms in the element, but is not barred from doing so.  |
| `Exclusion` | The party in the element will not fulfill the specific terms laid out in the element.  |
| `Obligation` | The party in the element is required to fulfill the terms of the element.   |
| `Right` | The party in the element is guaranteed to receive the terms of the element.  |

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
|`Amendments`      |Elements that specify changes to the contract after it has been signed, or alterations to a standard contract. Elements referring to alterations to a contract and changes to agreements also fall into this category.|
|`Asset Use`       |Elements that refer to situations in which one party must use the assets (licenses or equipment) of the other party in conducting their duties under the agreement, including permissions and restrictions thereon.|
|`Assignments`     |Elements that describe the transfer of rights, obligations, or both to a third party.|
|`Audits`          |This category includes elements referring to record-keeping and the right of parties to inspect the books or records of the other party, and elements referring to either the right of a party to inspect or review compliance, or requirements that a party be available for inspection or compliance review.|
|`Business Continuity`|A narrow category for elements that reference the effect of a sale, merger, or other substantial change to one of the parties to the agreement.|
|`Communication`  |Elements referring to requirements to notify or provide notice, details about communication methods (the act or process of exchanging information), contact representatives, and contact information. Additionally, elements referring to acceptable means of exchanging information between parties.|
|`Confidentiality` |This category includes elements describing how the parties can use information that they learn in the course of completing the contract; elements that discuss maintaining trade secrets; and elements describing the nondisclosure of business information.|
|`Deliverables`    |This category includes elements specifying the item or items one party gives to the other party in exchange for money, and elements describing the preparation of deliverables.|
|`Delivery`        |Elements that specify the means of transferring the item or items in the `Deliverables` category from one party to another. For example, if one party is selling access or cloud services, the means of getting that access falls into this category.|
|`Dispute Resolution`|This category includes elements that discuss provisions for settling any dispute arising between contracting parties; for example, settlement by a defined procedure such as an arbitration panel. Disputes can be settled by various methods other than arbitration; for example, irreparable harm, obtaining an injunction, or a statement to the effect of "You may not pursue this as a class action". Examples of disputes include labor disputes and disputes about invoices or billing. The category also includes elements that specify the contract's governing law or choice of law, such as a particular country or jurisdiction.|
|`Force Majeure`   |Elements that refer to disruptive events outside a party's control. It is a specific limitation of liability.|
|`Indemnification` |Elements that specify the remediation of certain liabilities. Indemnification is when one party of the contract becomes responsible for paying for another party's liability. The fact of indemnification implies that a liability has occurred.|
|`Insurance`       |Elements referring to any kind of insurance coverage or terms of coverage provided by one party to the other party.|
|`Intellectual Property`|Examples tend to fall into two categories: those using formal definitions of patents, copyrights, and trademarks, typically taken from statutes; and those using broader concepts of inventions, authorship, and know-how. Definitions can also be provided for intellectual property rights, such as the right to sue and claim damages for violation of such property rights. `Intellectual Property` includes patents, rights to apply for patents, trademarks, trade names, service marks, domain names, copyrights, and all applications and registration of such worldwide, schematics, industrial models, inventions, know-how, trade secrets, computer software programs, and other intangible proprietary information. For "Third Party Code", if any part of the code belongs to someone else, IP needs to be called out.|
|`Liability`       |Elements that describe the method for determining when and how fault attaches to any party.|
|`Payment Terms & Billing`|A broad category that includes elements that describe how a party pays or gets paid, including the following: elements that refer to the final mode of payment under the contract or how one party is paying; elements detailing how and when the party is to be be paid or the types of items the parties will be paying or billed for; elements referring to any kind of fee payment, except those that refer to specific prices or figures; and elements referring to the party that receives the payments under the contract.|
|`Pricing & Taxes` |This category includes elements that describe what a party pays or gets paid. The category includes elements that refer to taxes and specific amounts associated with individual deliverables that are exchanged, including details about the costs of a particular element, and elements that describe specific figures or methods for calculating prices.|
|`Privacy`         | Elements that specify the treatment of personal information; that is, private information about a specific individual or individuals that needs to be protected. The category is a very specific subset of the broader `Confidentiality` category.|
|`Responsibilities`|Tasks ancillary to the agreement, over which only one of the parties has oversight and control. The types of elements that fall into this category differ depending on the nature of the contract.|
|`Scope of Work`   |This category defines what is in the contract versus what is not in the contract. Typically, elements that tell the parties how a particular order is to be defined fall into this category. Examples include discussions of "statements of work" or descriptions of applicable communications standards.|
|`Subcontracts`    |Elements referring to the hiring of third parties to perform certain duties under the contract, and the permissions, rights, restrictions, and consequences thereto and arising therefrom.|
|`Term & Termination`|Elements referring to duration of the contract, the schedule and terms of contract termination, and any consequences of termination, including any obligations that apply at or after termination.|
|`Warranties`      |Elements that refer specifically to background, underlying assumptions that the parties can rely on. Consequences of breaching warranties also fall under this category.|

### Attributes
{: #attributes}

The `attributes` array specifies any attributes identified in the sentence. Each object in the array includes three keys: `type` (the type of attribute from the following table), `text` (the applicable text), and `attribute` (the start and end points of the attribute in the document). Currently supported attributes include:

| **Attributes** | **Description** |
| --- | --- |
|`Location`   |A geographical location or region.           |
|`DateTime`   |A date, time, date range, or time range.     |
|`Currency`   |Monetary value and units.                    |

### Assurance

{{site.data.keyword.cnc_short}} gives an assurance rating to each `type` or `category` element it identifies. There is currently one assurance value, `High`, which indicates there is significant evidence that the listed classification is representative of the content.

### Provenance
{: #provenance}
 
Each object in the `types` and `categories` arrays includes a `provenance` object. The `provenance` object has one or more `id` keys. Each `id` key has a hashed value that you can send to IBM to provide feedback or receive support.