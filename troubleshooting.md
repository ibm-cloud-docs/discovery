---

copyright:
  years: 2015, 2021
lastupdated: "2021-01-21"

subcollection: discovery

content-type: faq

---

{{site.data.keyword.attribute-definition-list}}

# Getting help
{: #troubleshoot}

Frequently asked questions about {{site.data.keyword.discoveryshort}}.

## Where can I get technical support for {{site.data.keyword.discoveryshort}}?
{: #faq-support}
{: faq}
{: support}

If you cannot find a solution to the issue you are having, search this documentation. You can also try the resources available from the **Developer community** section of the table of contents.

If your service plan covers it, you can get help by creating a case from [IBM Cloud Support](https://cloud.ibm.com/unifiedsupport/supportcenter){: external}.

## How do you interpret the confidence score that appears in query results?
{: #faq-confidence}
{: faq}
{: support}

{{site.data.keyword.discoveryshort}} returns a `confidence` score for both natural language queries and those written in the {{site.data.keyword.discoveryshort}} Query Language. For more information, see [Confidence scores](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence).

## How do you integrate Watson Discovery with Watson Assistant?
{: #faq-integrate}
{: faq}
{: support}

If you create a chatbot in {{site.data.keyword.conversationfull}}, you can route complex customer inquiries to {{site.data.keyword.discoveryshort}} using a search skill. When a customer asks a question that the dialog is not designed to answer, your assistant can search for relevant information from {{site.data.keyword.discoveryshort}}, extract the information, and return it as the response. See [Creating a search skill](/docs/services/assistant?topic=assistant-skill-search-add) for details. (This feature is available only to {{site.data.keyword.conversationshort}} Plus or Premium plan users.)

## What does the "Only one free environment is allowed per resource group" error message mean?
{: #faq-env}
{: faq}
{: support}

If you have recently deleted a Lite instance and then receive a `400 - Only one free environment is allowed per resource group` error message when creating a new environment in a new Lite instance, you need to finish deleting the original Lite instance. See [ibmcloud resource reclamations](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_reclamations) and follow the `reclamation-delete` instructions.

## Is there size limitation on the length of Natural Language Queries (NLQ)?
{: #faq-nlqsize}
{: faq}
{: support}

The maximum query string length for a natural language query is `2048`. For more information, see [Natural language query](/docs/discovery?topic=discovery-query-parameters#nlq).

## How do you improve query results?
{: #faq-improving}
{: faq}

The relevance of natural language query results can be improved in IBM Watson Discovery with training.  You can train your private collections using either the Discovery tooling, or the Discovery APIs. For information, see [Improving result relevance with the tooling](/docs/discovery?topic=discovery-improving-result-relevance-with-the-tooling).

## How do you know that relevancy training is complete?
{: #faq-relevancy}
{: faq}
{: support}

For answers to common questions about training a collection and explanations of common error and warning messages, see [Relevancy training tips](/docs/discovery?topic=discovery-relevancy-tips).

## Where can I learn more about uploading documents to Watson Discovery?
{: #faq-uploaddocs}
{: faq}
{: support}

You can upload documents using the API or the {{site.data.keyword.discoveryshort}} tooling. You can also connect to several different data sources (including Box, Salesforce, SharePoint Online, SharePoint 2016, and IBM Cloud Object Storage), or do a web crawl. For details, see [Adding content](/docs/discovery?topic=discovery-addcontent).

## What document types are supported for ingestion?
{: #faq-doctype}
{: faq}

Refer to [Supported document types and browsers](/docs/discovery?topic=discovery-sdu#doctypes) for a list of the available document types by plan.

## How do you use the Smart Document Understanding editor?
{: #faq-sdu}
{: faq}

The SDU editor functions are available in the Discovery tooling. Read [Using the Smart Document Understanding editor](/docs/discovery?topic=discovery-sdu#annotate) to get started.

## How much does Discovery cost?
{: #faq-price}
{: faq}
{: support}

{{site.data.keyword.discoveryshort}} has several options available. See [{{site.data.keyword.discoveryshort}} pricing plans](https://cloud.ibm.com/docs/discovery?topic=discovery-discovery-pricing-plans).

## How do I upgrade my existing Discovery plan?
{: #faq-upgrade}
{: faq}

For information on resizing your plan from Lite to Advanced, or switching from one Advanced tier to another, see [Upgrading your plan](/docs/discovery?topic=discovery-upgrading-your-plan).


## How do I create a stopwords list?
{: #faq-stopwords}
{: faq}

{{site.data.keyword.discoveryshort}} applies a default list of stopwords for several languages at query time. However, you can define and upload a custom list of stopwords that override the default list. {{site.data.keyword.discoveryshort}} applies the appropriate default or custom stopword list to your private collections, based on the language specified for that collection. For more information, see [Defining Stopwords](/docs/discovery?topic=discovery-query-concepts#stopwords).

## What is a query expansion list?
{: #faq-expansion}
{: faq}

Query expansion terms are usually synonyms, antonyms, or typical misspellings for common terms. You can expand the scope of a query beyond exact matches - for example, you can expand a query for "ibm" to include "international business machines" and "big blue" - by uploading a list of query expansion terms. For more information, see [Query expansion](/docs/discovery?topic=discovery-query-concepts#query-expansion).

## What is the length of Watson Discovery News query results?
{: #faq-newsquery}
{: faq}

{{site.data.keyword.discoverynewsfull}} queries display approximately 50 words from each article in the `text` JSON field. For more information, see [{{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}}](/docs/services/discovery?topic=discovery-watson-discovery-news).

## How do you query Watson Discovery News using the API?
{: #faq-newsapi}
{: faq}

For information about querying a collection via the API, see [API Reference](/apidocs/discovery#query-your-collection){: external}. The `collection_id` of the English language version of Watson {{site.data.keyword.discoverynewsshort}} is `news-en`. The `collection_id` of the Korean collection is `news-ko`, the Spanish `collection_id` is `news-es`, the German `collection_id` is `news-de`, the French `collection_id` is `news-fr`, and the Japanese `collection_id` is `news-ja`. For more information, see [Querying Watson Discovery News](/docs/discovery?topic=discovery-query-concepts#querying-news).

## Can I upload JSON arrays?
{: #faq-array}
{: faq}

You can upload a JSON array, but each section must be uploaded individually. For example, the following JSON cannot be uploaded to the service:

```json
[{
  "accepted": 1,
  "answer": "You shouldn't have any issues keeping it on all the time however some thing to consider is any counters you may have like the use of millis code . From the Arduino docs on millis a This number will overflow go back to zero after approximately 50 days. blockquote So for projects that are on for long periods of time you may not see an issue immediately but something like this could pop up and cause errors down the road. ",
  "answerScore": "49",
  "authorUserId": "3",
  "authorUsername": "Butzke",
  "downModVotes": 0,
  "id": 2,
  "subtitle": "I'm making a simple Arduino web server and I want to keep it turned on all the time. So it must endure to stay working continuously. I'm using an Arduino Uno with a Ethernet Shield. It's powered with a simple outlet power supply 5V 1A. My Questions Will I have any problems leaving the Arduino turned on all the time? li Is there some other Arduino board better recommended for this? li Are there any precautions that I need to heed regarding this? li ul ",
  "tags": "<arduino-uno><web-server><ethernet>",
  "title": "Is an Arduino capable of running 24 7?",
  "upModVotes": 49,
  "userId": "11",
  "userReputation": 4535,
  "username": "sachleen",
  "views": 3234
}, {
  "accepted": 0,
  "answer": "A couple of things to keep in mind outside of Sachleen's mention of Milli's Like any electronics heat can be disruptive. The micro controller itself isn't likely going to be a huge issue from the perspective of heat but other components like the power supply might cause issues. li If your code uses EEPROMWrite a be aware that the EEPROM is only rated for something in the neighbourhood of 100 000 writes. li ul ",
  "answerScore": "24",
  "authorUserId": "3",
  "authorUsername": "Butzke",
  "downModVotes": 0,
  "id": 3,
  "subtitle": "I'm making a simple Arduino web server and I want to keep it turned on all the time. So it must endure to stay working continuously. I'm using an Arduino Uno with a Ethernet Shield. It's powered with a simple outlet power supply 5V 1A. My Questions Will I have any problems leaving the Arduino turned on all the time? li Is there some other Arduino board better recommended for this? li Are there any precautions that I need to heed regarding this? li ul ",
  "tags": "<arduino-uno><web-server><ethernet>",
  "title": "Is an Arduino capable of running 24 7?",
  "upModVotes": 24,
  "userId": "13",
  "userReputation": 489,
  "username": "Matthew G.",
  "views": 3234
}]
```
{: codeblock}

To upload this information to the service, break down the array and upload each section, as follows:

Section 1:

```json
{
  "accepted": 1,
  "answer": "You shouldn't have any issues keeping it on all the time however some thing to consider is any counters you may have like the use of millis code . From the Arduino docs on millis a This number will overflow go back to zero after approximately 50 days. blockquote So for projects that are on for long periods of time you may not see an issue immediately but something like this could pop up and cause errors down the road. ",
  "answerScore": "49",
  "authorUserId": "3",
  "authorUsername": "Butzke",
  "downModVotes": 0,
  "id": 2,
  "subtitle": "I'm making a simple Arduino web server and I want to keep it turned on all the time. So it must endure to stay working continuously. I'm using an Arduino Uno with a Ethernet Shield. It's powered with a simple outlet power supply 5V 1A. My Questions Will I have any problems leaving the Arduino turned on all the time? li Is there some other Arduino board better recommended for this? li Are there any precautions that I need to heed regarding this? li ul ",
  "tags": "<arduino-uno><web-server><ethernet>",
  "title": "Is an Arduino capable of running 24 7?",
  "upModVotes": 49,
  "userId": "11",
  "userReputation": 4535,
  "username": "sachleen",
  "views": 3234
}
```
{: codeblock}

Section 2:

```json
{
  "accepted": 0,
  "answer": "A couple of things to keep in mind outside of Sachleen's mention of Milli's Like any electronics heat can be disruptive. The micro controller itself isn't likely going to be a huge issue from the perspective of heat but other components like the power supply might cause issues. li If your code uses EEPROMWrite a be aware that the EEPROM is only rated for something in the neighbourhood of 100 000 writes. li ul ",
  "answerScore": "24",
  "authorUserId": "3",
  "authorUsername": "Butzke",
  "downModVotes": 0,
  "id": 3,
  "subtitle": "I'm making a simple Arduino web server and I want to keep it turned on all the time. So it must endure to stay working continuously. I'm using an Arduino Uno with a Ethernet Shield. It's powered with a simple outlet power supply 5V 1A. My Questions Will I have any problems leaving the Arduino turned on all the time? li Is there some other Arduino board better recommended for this? li Are there any precautions that I need to heed regarding this? li ul ",
  "tags": "<arduino-uno><web-server><ethernet>",
  "title": "Is an Arduino capable of running 24 7?",
  "upModVotes": 24,
  "userId": "13",
  "userReputation": 489,
  "username": "Matthew G.",
  "views": 3234
}
```
{: codeblock}


## How can you protect your data when using Watson Discovery?
{: #faq-secure}
{: faq}

To learn about securing your data when using Watson Discovery, refer to [Protecting sensitive information in your Watson service](/docs/discovery?topic=watson-keyservice).  For general information about the security architecture, review [Securing AI apps: Watson on IBM Cloud security](https://www.ibm.com/cloud/architecture/architectures/securityArchitecture/watson-security).

## What Watson solutions are available to respond to Covid-19 questions?
{: #faq-covid19kit}
{: faq}

[IBM Watson Assistant for Citizens](https://www.ibm.com/watson/covid-response) on the IBM public cloud brings together Watson Assistant, Natural Language Processing capabilities from IBM Research, and state-of-art enterprise AI search capabilities with Watson Discovery, to understand and respond to common questions about COVID-19.  For information on what’s available with Watson Discovery, review [Using the COVID-19 kit](/docs/discovery?topic=discovery-covidkit).

## Can I migrate documents from one Discovery instance to another?
{: #faq-migratecontent}
{: faq}

You cannot migrate original documents from one instance to another. Instead, ingest the documents to the newly created instance.

## How do I delete documents from my Discovery collection?
{: #faq-deletecontent}
{: faq}

Use the [Delete method](/apidocs/discovery#delete-a-document) in the Discovery API to delete documents.  There is no delete option within the user interface.
