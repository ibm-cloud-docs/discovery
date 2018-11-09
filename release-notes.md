---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-08"

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

# Release notes

The release notes provide information about changes to the {{site.data.keyword.discoveryfull}} service since the previous release.
{: shortdesc}

## Service API Versioning
{: shortdesc}

API requests require a version parameter that takes a date in the format `version=YYYY-MM-DD`. Whenever we change the API in a backwards-incompatible way, we release a new minor version of the API.

Send the version parameter with every API request. The service uses the API version for the date you specify, or the most recent version before that date. Don't default to the current date. Instead, specify a date that matches a version that is compatible with your app, and don't change it until your app is ready for a later version.

The current version is `2018-10-15`.

## Beta features
{: #beta-features}

IBM will release services, features, and language support that are classified as beta or experimental. These capacities can be unstable, can change frequently, and can be discontinued with short notice. They are provided so you can evaluate their functionality. A beta or experimental capacity might not provide the same level of performance or compatibility that generally released capacities provide. These capacities are not designed for use in a production environment, and any such use is at your own risk.


## Changes
{: #change-log}

The following new features and changes to the service are available.

## 8 November 2018

- {{site.data.keyword.discoveryshort}} launched in the `Tokyo` location 8 November, 2018. Premium and Dedicated environments are not currently available in `Tokyo`.

## 30 October 2018
{: #30oct}

- The {{site.data.keyword.discoveryshort}} service now supports token-based Identity and Access Management (IAM) authentication in all regions. IAM uses access tokens rather than service credentials for authentication with a service. For more information about using IAM tokens with existing and new applications, see the [17 May 2018](#17May2018) release update.

## 25 October 2018
{: #25oct}

The schema for the [Element Classification](/docs/services/discovery/element-classification.html) enrichment has changed. If you wish to use the updated schema, you must ingest your documents with the API, using the version date of `2018-10-15` or later. The {{site.data.keyword.discoveryshort}} tooling does not yet use this API version (it currently uses `2018-08-01`), so documents ingested using the {{site.data.keyword.discoveryshort}} tooling will be enriched with the original schema.

## 24 October 2018
{: #24oct2018}

- {{site.data.keyword.discoverynewsfull}} queries display approximately 50 words from each article in the `text` JSON field. These words will now be extracted from the highlights, rather than simply displaying the first 50 words of the article. See [highlight](https://console.bluemix.net/docs/services/discovery/query-parameters.html#highlight) for an explanation of highlights. Highlights do not need to be explicitly included in your query to enable this behavior.

## 25 September 2018
{: #25sept}

- Released Continuous Relevancy Training, which uses interactions from users to learn how to surface the most relevant results. It can learn from user behavior automatically, significantly reducing the effort required to improve the relevancy ranking of results.  See [Continuous Relevancy Training](/docs/services/discovery/continuous-training.html#crt) for details.

- Added API support for performing longer queries. This increases the character limit to 10,000 characters, and makes it possible to increase the number of filters in your queries and perform more complex aggregations. See the POST Query at [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/discovery#long-collection-queries){: new_window} and [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/discovery#long-environment-queries){: new_window} for details.

- You can now upgrade your Advanced plan using the API. See [Upgrading your plan](/docs/services/discovery/upgrading.html#advanced) for details. 

- The Element Classification enrichment has updated the classified elements, contract elements, and parties and tables identified. See [Element Classification](https://console.bluemix.net/docs/services/discovery/element-classification.html) for the updates.

- Added full support for Brazilian Portuguese. For more information, see [Language support](/docs/services/discovery/language-support.html).

- The query API (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`) now supports the `bias` parameter, which allows you to bias towards certain results, for example, documents that were published most recently. See the [Query your collection ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/discovery#query-your-collection){: new_window} method in the API reference for information.

- The **Default Contract Configuration** file provided to enrich collections for [Element Classification](/docs/services/discovery/element-classification.html#element-collection) was found to have an issue with HTML normalizations. A new **Default Contract Configuration** is included with this release. Follow the steps below to apply the new **Default Contract Configuration** to your collections.

     1. Determine which of your collections are using either the **Default Contract Configuration** configuration file, or a custom configuration based on **Default Contract Configuration**.
     1. Make note of the changes you made to any custom configurations based on **Default Contract Configuration**.
     1. Since the old **Default Contract Configuration** file needs to be deleted from your environment before the new one is used, use the API [Delete configuration ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/discovery#delete-a-configuration){: new_window} to delete the current **Default Contract Configuration** associated with any of your collections. Also delete any configurations based on the old **Default Contract Configuration**.
     1. Now you can use the new **Default Contract Configuration** file. For each collection using one of those configurations, create a new collection. Apply the new **Default Contract Configuration** or create a new custom configuration based on the new **Default Contract Configuration** using the notes you made in step 2.
     1. Upload the files previously ingested to the original collections.
     1. Delete the old collections.

## 15 August 2018
{: #15aug}

- Two new query operators are available. `Exists` (`:*`) can be used to return all results where the specified `field` exists. `Does not exist` (`!*`) can be used to return all results that do not include the specified `field`. See [Query operators](/docs/services/discovery/query-operators.html) for more information. 

## 2 August 2018
{: #2aug}

- {{site.data.keyword.discoveryfull}} now supports English, Spanish, German, Italian, Portuguese, French, Arabic, Korean, and Japanese language collections when connecting and syncing to Box, Salesforce, and SharePoint Online with the {{site.data.keyword.discoveryshort}} tooling. 

## 31 July 2018
 
 - Beginning **August 1, 2018**, {{site.data.keyword.discoveryfull}} has a new pricing structure. It features a simpler pricing model (document hours are no longer part of the calculation) and tiered pricing for {{site.data.keyword.discoverynewsfull}} queries. In addition, the Standard plan has been retired, and the Lite plan has reduced document and {{site.data.keyword.discoverynewsshort}} query limits. The pricing changes will require no action by current {{site.data.keyword.discoverynewsshort}} users. See [{{site.data.keyword.discoveryshort}} Pricing Plans](/docs/services/discovery/pricing-details.html) for details.
 
**Note:** The version date of the API has been updated to `2018-08-01`. To take advantage of the new environment sizing options (`LT`, `XS`, `S`, `MS`, `M`, `ML`, `L`, `XL`, `XXL`, `XXXL`), you must use this version date when creating environments with the API. The environment sizes now have the type of `string` (previously the type was `integer`.)

## 27 July 2018

- Released [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery/watson-discovery-news.html) in one additional language: Japanese (`collection_id`: `news-ja`). {{site.data.keyword.discoverynewsfull}} is also available in English, Spanish, German, and Korean.

## 25 June 2018

- Added the option to connect to and sync with Salesforce, Microsoft SharePoint Online, and Box data sources. These data sources are not available in Premium environments. Released the [Source Credential ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/discovery#list-credentials){: new_window} and [Configuration ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/discovery#add-configuration){: new_window} APIs for these data sources. 
  - {{site.data.keyword.discoveryfull}} supports only English language collections when connecting and syncing to Box, Salesforce, and SharePoint Online with the {{site.data.keyword.discoveryshort}} tooling. [Resolved](/docs/services/discovery/release-notes.html#2aug)
  - The individual document file size limit for Box, Salesforce, and SharePoint Online is 10MB.
- Added a new Performance Dashboard in {{site.data.keyword.discoveryshort}} tooling. See [Viewing metrics and improving query results with the Performance dashboard](/docs/services/discovery/dashboard.html). The new dashboard is not available in Premium or Dedicated environments.
- Added full support for Japanese. For more information, see [Language support](/docs/services/discovery/language-support.html).

## 22 June 2018

- Released the Events and Feedback API. See the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/discovery#create-event){: new_window} for more information.

## 11 June 2018

-  For applications that are hosted in Washington, DC (US East), the service now supports token-based Identity and Access Management (IAM) authentication. IAM uses access tokens rather than service credentials for authentication with a service. For more information about using IAM tokens with existing and new applications, see the [17 May 2018](#17May2018) release update.
-  An additional contract element is now supported in Element Classification: `Safety and Security`. See [Understanding Contract Elements](/docs/services/discovery/element-classification.html#contract-elements) for details.

## 6 June 2018

- {{site.data.keyword.discoverynewsfull}} queries now display the first 50 words of each article in the `text` JSON field. [Update](#24oct2018)

## 5 June 2018
{: #5jun}

- Element Classification is now available to those subscribed to Premium plans.
- The `assurance` rating of `Low` is no longer available for Element Classification.

## 31 May 2018

- Added full support for French. For more information, see [Language support](/docs/services/discovery/language-support.html).

## 30 May 2018

- Fixed a known issue in {{site.data.keyword.discoverynewsfull}}. Previously, when querying {{site.data.keyword.discoverynewsshort}} it was possible to receive an incorrect document count because documents in other languages would be counted along with the language you requested. This is no longer the case.
- Beginning with collections created on `22 May 2018` and after {{site.data.keyword.discoveryshort}} now returns query results that include special characters for the following languages: English, German, French, Dutch, Italian, and Portuguese. For example, if you query for `aqui`, you will now receive results for both for `aqui` and <code>aqu&iacute;</code>.

## 21 May 2018

- Released [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery/watson-discovery-news.html) in one additional language: German (`collection_id`: `news-de`). {{site.data.keyword.discoverynewsfull}} is also available in English, Spanish, and Korean.

## 17 May 2018
{: #17May2018}

- {{site.data.keyword.discoverynewsfull}} queries now display only the first 20 words of each article in the `text` JSON field.

-   The service now supports a new API authentication process for service instances for applications that are hosted in Sydney (**au-syd**) as of May 15, 2018. They will be enabled for applications that are hosted in other regions soon. {{site.data.keyword.Bluemix}} is in the process of migrating to token-based Identity and Access Management (IAM) authentication. IAM uses access tokens rather than service credentials for authentication with a service.

   In the Sydney location, you use IAM access tokens with the {{site.data.keyword.discoveryshort}} service for

    -   *New service instances* that you create after May 15. For more information, see [Authenticating with IAM tokens](/docs/services/watson/getting-started-iam.html).
    -   *Existing service instances* that you migrate from Cloud Foundry to a resource group that is managed by the Resource Controller (RC). Service instances that were created before May 15 continue to use service credentials for authentication until you migrate them. For more information, see [Migrating Cloud Foundry service instances to a resource group](/docs/resources/instance_migration.html).

    All new and existing service instances in other regions continue to use service credentials (`apikey:{apikey_value}`) for authentication.

### Using an IAM access token to authenticate

When you use IAM access tokens, you authenticate before you send a request to the {{site.data.keyword.discoveryshort}} service.

1.  Get an API key from IBM Cloud. Use that key to generate an IAM access token. For more information, see [How to get an IAM token by using a {{site.data.keyword.watson}} service API key](/docs/services/watson/getting-started-iam.html#iamtoken).
1.  Pass the IAM access token to the {{site.data.keyword.discoveryshort}} service by using the `Authorization` header. In the header, indicate that the access token is a `Bearer` token by specifying `Authorization: Bearer {access_token}`.

    The following simple cURL example uses an access token:

    ```bash
    curl -X GET
    --header "Authorization: Bearer eyJhbGciOiJIUz......sgrKIi8hdFs"
    "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    For more information, see [Using a token to authenticate](/docs/services/watson/getting-started-iam.html#use_token).

### Refreshing an IAM access token

IAM access tokens that you generate have the following structure. You use the value of the `access_token` field to make an authenticated request to the service.

```javascript
{
  "access_token": "eyJhbGciOiJIUz......sgrKIi8hdFs",
  "refresh_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353
}
```
{: codeblock}

Access tokens have a limited time to live. The `expires_in` field indicates how long the token lasts, in this case one hour. The `expiration` field shows when the token expires as a UNIX timestamp that specifies the number of seconds since January 1, 1970 (midnight UTC/GMT).

In your application, check the access token's expiration time before you use it to make an authenticated request. If it is expired, you must refresh the access token before you can use it. You use the value of the `refresh_token` field to refresh the access token. For more information, see [Refreshing a token](/docs/services/watson/getting-started-iam.html#refresh_token).


## 11 May 2018

- Details about information security can be found here: [Information security](/docs/services/discovery/information-security.html).
- The following {{site.data.keyword.discoveryfull}} Knowledge Graph `query_entities` known issue has been fixed with the `2018-05-04` API version update. This fix only applies if entities are ingested or replaced after `2018-05-04`. Entities can be replaced by re-ingesting old documents or by ingesting new documents containing those entities. If old entities are not replaced, then `query_entities` will return all upper case with `2018-05-04` API version.
  - All entity names were previously converted to camel case in `query_entities`. For example, the entity name "IBM Corporation" was converted to "Ibm Corporation". This is no longer the case.

## 9 May 2018

- Sample documents are now stored locally, in your browser's local roaming data folder. For more information about sample documents, see [Uploading sample documents](/docs/services/discovery/building.html#uploading-sample-documents).

## 4 May 2018

- Two additional contract elements are now supported in Element Classification: Attributes and Provenance. See [Understanding Contract Elements](/docs/services/discovery/element-classification.html#contract-elements) for details.

## 26 April 2018

- The following ingestion issue has been fixed: In some cases where post-enrichment `json_normalizations` and/or `normalizations` were specified, the normalizations may have been applied in the wrong order. This could result in documents being indexed with unexpected field values. This is no longer the case.
- The maximum file size for a sample document is now 1MB. The maximum file size was previously 5MB.

## 12 April 2018

- Knowledge Graph: [Evidence](/docs/services/discovery/building-kg.html#evidence) and [Canonicalization and filtering](/docs/services/discovery/building-kg.html#canonicalization) are now available in all collections. In any collections created before `03-05-2018`, you need to reingest your documents to use these features. Previously, you needed to create a new collection and reingest your documents.

## 11 April 2018

- Two additional categories are now supported in Element Classification: `Asset Use` and `Communication`. See [Understanding Contract Elements](/docs/services/discovery/element-classification.html#contract-elements) for details.

## 2 April 2018

- Sample documents are now automatically deleted after 24 hours, instead of 1 month.

## 16 March 2018

- Added full support for German. For more information, see [Language support](/docs/services/discovery/language-support.html).

{{site.data.keyword.discoveryshort}} tooling:
- A new configuration named **Default Contract Configuration** has been added to support Element Classification, which can be used to extract party, nature, and category from elements in PDFs. See [Element Classification](/docs/services/discovery/element-classification.html#element-collection) for details.

Updated to general availability:
- Documentation segmentation has moved from beta status to GA status. The segmentation limit has been increased to 250 segments. It is no longer limited to 50 segments per document. See [Documentation segmentation](/docs/services/discovery/building.html#doc-segmentation) for details.

Known issue:
- Wildcards do not work with queries that contain capital letters. For example, given the key/field pair ``{"borrower": "GOVERNMENT OF INDIA"}``, `query-borrower:*ndia` will return results but `query-borrower:*NDIA` will not.

## 8 March 2018
{: #8mar}

- The beta version of {{site.data.keyword.discoveryfull}} Knowledge Graph added several features. During the beta release, [Knowledge Graph](/docs/services/discovery/building-kg.html) functionality and the methods associated with it are only available for service instances that are subscribed to **Advanced** plans, **Premium** plans, and all **Dedicated** environments. The new features are:
  - [Entity similarity](/docs/services/discovery/building-kg.html#similarity)
  - [Evidence](/docs/services/discovery/building-kg.html#evidence)
  - [Canonicalization and filtering](/docs/services/discovery/building-kg.html#canonicalization)

## 7 March 2018

- The following ingestion known issue has been fixed: Between 28 February and 6 March, a small percentage of documents were indexed with only the `id` and `extracted_metadata` fields (other document content was not indexed). The underlying problem has been fixed, however, you will need to resubmit any affected documents for ingestion. There is no simple way to identify the affected documents.

## 5 March 2018
{: #5mar}

- The following {{site.data.keyword.discoveryfull}} Knowledge Graph known issue has been fixed with the `2018-03-05` API version update. This fix only applies to newly created collections that use the `2018-03-05` version update.  
  - All entity type names and relation type names were previously converted to uppercase during ingestion. For example, the entity "GeoPoliticalEntity" was converted to "GEOPOLITICALENTITY," and the relation "partOf" was converted to "PARTOF." This is no longer the case.

## 1 March 2018

- [Query expansion](/docs/services/discovery/using.html#query-expansion) limits have been increased for Advanced and Premium plans to 5,000 query expansions and 25,000 total terms. See [Discovery pricing plans](/docs/services/discovery/pricing-details.html) for details.

## 28 February 2018

- {{site.data.keyword.alchemylanguageshort}} enrichments have been deprecated effective **1 March 2018**. For information on migrating existing collections and configuration files that utilize the {{site.data.keyword.alchemylanguageshort}} enrichments, see [Migrating enrichments to {{site.data.keyword.nlushort}}](/docs/services/discovery/migrate-nlu.html).

## 23 February 2018

- Added the ability to query by document similarity. You can query for similar documents by  document ids, and optionally further refine the similarity by specifying fields. See [Document similarity](/docs/services/discovery/using.html#doc-similarity) for more information.

- The [`highlight` parameter](/docs/services/discovery/query-parameters.html#highlight) in query results has been enhanced. Query results will return complete sentences, ordered by their `score`.

## 21 February 2018
{: #21feb}

- Previously, when ingesting PDF documents, the `file_type` returned when ingestion notices were queried, in the `extracted_metadata` object, and from the document details API was `html`. This is no longer the case. The `file_type` returned will now be `pdf`. 

## 26 January 2018
{: #26jan}

{{site.data.keyword.discoveryshort}} tooling:

- Added the ability to access Korean and Spanish collections to the [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery/watson-discovery-news.html) tile in the tooling. Previously, these collections could only be queried via the API.

## 23 January 2018

- Added the ability to expand the scope of a query - for example, you can expand a query for "car" to include "automobile" and "motor vehicle". In addition, you can replace commonly misspelled terms, for example, you can replace queries for "seabizcuit" with "seabiscuit." Query expansion is implemented with the {{site.data.keyword.discoveryshort}} API. See [Query expansion](/docs/services/discovery/using.html#query-expansion) for details.  

## 15 January 2018

- {{site.data.keyword.discoverynewsfull}} Original was retired from service. It was replaced 31 July 2017 with a new version, named {{site.data.keyword.discoverynewsfull}}. For instructions on migrating from {{site.data.keyword.discoverynewsfull}} Original to the new version, see [Migrating from Watson Discovery News Original](/docs/services/discovery/migrate-bwdn.html).

## 11 January 2018

- Added full support for Korean. For more information, see [Language support](/docs/services/discovery/language-support.html).

## 15 December 2017

- Released the **Element Classification** enrichment, which parses elements (sentences, lists, tables) in governing documents to classify important categories and types. See [Element classification](/docs/services/discovery/element-classification.html) for more information. Element Classification is not available for service instances that are subscribed to the **Premium** plan. [Resolved](/docs/services/discovery/release-notes.html#5jun)
- Added Basic language support for Simplified Chinese and Dutch. See [Language Support](/docs/services/discovery/language-support.html) for more information. Currently, Simplified Chinese and Dutch collections must be created with the API.
- Added two new parameters for the Data Crawler: `proxy_host_port` and `read-timeout`. See [Configuring the Data Crawler](/docs/services/discovery/data-crawler-discovery.html) for details.
- The following issues may be seen when ingesting PDF documents: [Resolved](/docs/services/discovery/release-notes.html#21feb)
  - When ingestion notices are queried, the field `file_type` for pdf documents is returned as `html`.
  - The field `file_type` in the `extracted_metadata` object of results for pdf documents is set to `html`.
  - The document details API also returns the field `file_type` for pdf documents as `html`.
- If you are ingesting JSON, mixed-type arrays are not supported.  

{{site.data.keyword.discoveryshort}} tooling:

- Added a visual query builder for the beta version of {{site.data.keyword.discoveryfull}} Knowledge Graph. See [Querying Knowledge Graph using the {{site.data.keyword.discoveryshort}} tooling](/docs/services/discovery/building-kg.html#querying-kg)

## 30 November 2017

- Released the beta version of {{site.data.keyword.discoveryfull}} Knowledge Graph, which provides new end-points for querying entities and relations across documents. This includes context-based searches and relevance ranking. This beta feature is available to **Advanced** plan users only. It is not available on **Dedicated** environments. [Resolved](/docs/services/discovery/release-notes.html#8mar) See [{{site.data.keyword.discoveryfull}} Knowledge Graph](/docs/services/discovery/building-kg.html) for more information.  A statement explaining beta features can be found [here](/docs/services/discovery/release-notes.html#beta-features).
  - Known issue in {{site.data.keyword.discoveryfull}} Knowledge Graph: All entity type names and relation type names are converted to uppercase during ingestion. For example, the entity "GeoPoliticalEntity" is converted to "GEOPOLITICALENTITY," and the relation "partOf" is converted to "PARTOF." [Resolved](/docs/services/discovery/release-notes.html#5mar)
- Released [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery/watson-discovery-news.html) in two additional languages: Korean (`collection_id`: `news-ko`) and Spanish (`collection_id`: `news-es`). {{site.data.keyword.discoverynewsfull}} Korean and Spanish are available for use via the API-only; for information about querying a collection via the API, see [API Reference ![External link icon](../../icons/launch-glyph.svg "External link icon")] [Resolved](/docs/services/discovery/release-notes.html#26jan)(https://console.bluemix.net/apidocs/discovery#query-your-collection){: new_window}. {{site.data.keyword.discoverynewsfull}} English now has the `collection_id` of `news-en`. Formerly, the `collection_id` was `news` - if you have been using the former `collection_id`, it will continue to work, however, you may want to switch to the new `collection_id` for new projects.
- Query results return a `score` value, which indicates the relative relevancy between query results. Starting 30 November 2017, the way that `score` is calculated changed. The `score` value should only be used to rank documents in a single search, not across searches or sessions. If you have trained a collection, a `score` value is returned in the results of a natural language query. Since the `score` indicates the relative relevancy between query results, it should not be used as a threshold. Instead, use the `confidence`, which indicates the relevance of the result as compared to the trained model, to set thresholds. See [Confidence scores](/docs/services/discovery/train-tooling.html#confidence) for more information on setting thresholds.
- Beginning with this release, Passage retrieval detects sentence boundaries - it attempts to return passages that start at the beginning of a sentence and stop at the end. Previously, many passages would begin or end somewhere mid-sentence. See [Passages](/docs/services/discovery/query-parameters.html#passages) for more information about Passage retrieval.

## 15 November 2017
{: #15nov}

{{site.data.keyword.discoveryshort}} tooling:

- Added the [Relation Extraction](/docs/services/discovery/building.html#relation-extraction) enrichment, which includes the option to incorporate a custom relation model created with {{site.data.keyword.knowledgestudiofull}}.
- The [Entity Extraction](/docs/services/discovery/building.html#entity-extraction) enrichment {{site.data.keyword.discoveryshort}} tooling now includes the option to incorporate a custom entity model created with {{site.data.keyword.knowledgestudiofull}}.
- The option to create a Japanese collection was removed from the {{site.data.keyword.discoveryshort}} tooling, however, the option to create a Japanese collection using the {{site.data.keyword.discoveryshort}} API remains.
- {{site.data.keyword.discoveryshort}} Tooling now supports syndicated environments.

## 10 November 2017

{{site.data.keyword.discoveryshort}} tooling:

- Added additional options for Passage retrieval to the {{site.data.keyword.discoveryshort}} tooling. When querying, you can now specify the fields you would like the passages to be returned from, the number of passages to return, and the maximum character count for each passage. See [Passages](/docs/services/discovery/query-parameters.html#passages) for limits, minimums, and maximums.

## 8 November 2017
{: #8nov}

The version string for all API calls has changed to `2017-11-07` from `2017-10-16`. This version:
- Moved the `score` in each query result to a new object named `result_metadata`.
- If the collection queried was trained, and the query is a natural language query, `result_metadata` will include a `confidence` field that displays the confidence score for that result. See [Confidence scores](/docs/services/discovery/train-tooling.html#confidence) for details.
- Fields that include whitespaces (for example: `body.additional reading`) will be filtered out during ingestion. The `notices` description will read `The field 'additional reading' is invalid: whitespace, '.', '#' and ',' are invalid in a field name`.
- The field `result_metadata` will be filtered out during ingestion.

## 16 October 2017

- The version string for all API calls has changed to `2017-10-16` from `2017-09-01`. This version deprecates support for uploading new documents into existing collections enriched with {{site.data.keyword.alchemylanguageshort}} enrichments, and for creating new collections and enriching them with {{site.data.keyword.alchemylanguageshort}} enrichments. Existing collections enriched with {{site.data.keyword.alchemylanguageshort}} should be migrated to {{site.data.keyword.nlushort}} enrichments as soon as possible. See [Migrating enrichments to {{site.data.keyword.nlushort}}](/docs/services/discovery/migrate-nlu.html#migrating-enrichments-to-natural-language-understanding) for details. The {{site.data.keyword.discoveryshort}} tooling also uses the `2017-10-16` version, see below for more information.

{{site.data.keyword.discoveryshort}} tooling:

- The {{site.data.keyword.discoveryshort}} tooling uses the `2017-10-16` API version string, so if you are using the tooling, you will no longer be able to upload documents into existing {{site.data.keyword.alchemylanguageshort}} collections or create new collections enriched with {{site.data.keyword.alchemylanguageshort}} enrichments after `2017-10-16`.  If you want to continue using the {{site.data.keyword.discoveryshort}} tooling for enriching collections, migrate your collections to {{site.data.keyword.nlushort}} first. See [Migrating enrichments to {{site.data.keyword.nlushort}}](/docs/services/discovery/migrate-nlu.html#migrating-enrichments-to-natural-language-understanding) for details.
- The **Data schema explorer** displays sample queries for several enrichments in the {{site.data.keyword.discoverynewsfull}} collection. It also now has a **Show more values** link that will display additional example values for that enrichment in {{site.data.keyword.discoverynewsfull}}.
- Multiple productivity enhancements, including combining the collection statistics, errors and warnings, and data insights on the **Manage data** screen.
- A message was added that displays an alert when documents are finished processing.

## 9 October 2017

- A new aggregation metric `unique_count` is available in the API. It will return a count of the unique instances of the specified field in a collection. See [unique_count](/docs/services/discovery/query-aggregations.html#unique_count) for more information.

{{site.data.keyword.discoveryshort}} tooling:

- Histogram and Timeslice aggregations are now supported in the **Visual Query Builder**. You also have the option to turn on anomaly detection for Timeslice queries.
- The **Data schema explorer** displays sample queries for the enrichment chosen. It also now has a **Show more values" link that will display additional example values for that enrichment.
- A hamburger menu has been added to make it faster to navigate the **Manage data**, **View data schema**, and **Build queries** screens.

### 3 October 2017

- Document segmentation is now available. See [Splitting documents with document segmentation](/docs/services/discovery/building.html#doc-segmentation).

### 29 September 2017

- {{site.data.keyword.discoveryshort}} launched in the `Germany` location 29 September, 2017. In order to comply with EU data regulations, AlchemyLanguage enrichments are not supported in this location.
- Known issue: Query fields cannot contain whitespaces.  When writing a query in {{site.data.keyword.discoveryshort}}, if any query field contains whitespace (for example, `body.additional reading`), you will receive a `400: Invalid query syntax error`. [Resolved](/docs/services/discovery/release-notes.html#8nov)

### 25 September 2017

- A Premium pricing plan is now available. For more information, see [{{site.data.keyword.discoveryshort}} pricing plans](/docs/services/discovery/pricing-details.html).
- The ability to query, list fields, and query notices across collections within the same environment has been added. See [Querying multiple collections](/docs/services/discovery/using.html#multiple-collections) for details.
- Language support information for {{site.data.keyword.discoveryshort}} is available at [Language support](/docs/services/discovery/language-support.html)

{{site.data.keyword.discoveryshort}} tooling:
- The Visual Query Builder moved from beta status to GA status. Filter, Timeslice, and Histogram aggregations are not currently supported with the Visual Query Builder. Click **Include analysis of your results**, then **Edit in Query Language** on the **Build queries** screen to write those aggregations.
- Added the beta capability to deduplicate on {{site.data.keyword.discoverynewsfull}} queries.
- In addition to English, German, and Spanish language collections, you can now create Arabic, French, Italian, Korean, Japanese, and Brazilian Portuguese collections.
- Known issue: {{site.data.keyword.discoveryshort}} Tooling does not support syndicated environments. [Resolved](/docs/services/discovery/release-notes.html#15nov)

### 14 September 2017

{{site.data.keyword.discoveryshort}} tooling:

- Added the Data Schema Explorer, which displays the fields and values in your transformed documents. This information can be used to understand the data structure of your collection before building queries using the Discovery Query Language. The data schema can be viewed two ways: by document (Document view), or by field (Collection view). To access the Data Schema Explorer: on the **My Data Insights** screen, click the **View data schema** button, or click the **View Data Schema** icon on the left.

### 6 September 2017

- Added the beta ability to deduplicate documents returned from your query. This beta feature works for both private and Watson Discovery News collections. See [Excluding duplicate documents from query results](/docs/services/discovery/query-parameters.html#deduplication) for details.

Document deduplication is currently supported only as a beta capability. See the statement regarding betas at the top of this document for more information.

### 31 August 2017

- The version string for all API calls has changed to `2017-09-01` from `2017-08-01`. This version includes updates that will filter out the following invalid JSON fields during preview and ingestion so that only valid JSON fields are ingested. Update your version string to `2017-09-01` to avoid conflicts and possible errors.

   - `id`, `score`, and `highlight` at the top level (You can continue to add documents to your collection using document IDs with the `add a document` function. See the [API Reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/discovery#add-a-document){: new_window} for details.
   - `_` prefixed field names at the top level (as a result, when querying for a document by ID, you can query for `id` instead of `_id`.)
   - `#` and `,` in the field name
   - `+` and `-` prefixed field names
   - `"` `"` empty values for a field name

**Note:** If your JSON documents include these characters in the field names, or `id`, `score`, and `highlight` at the top level, you need to remove them before adding the documents to your collection, or those fields will be empty. You can create a custom configuration and normalize your JSON before adding documents to your collection to avoid this issue. See [Custom Configuration](/docs/services/discovery/building.html#custom-configuration).  In addition, documents that include the punctuation characters `?`, `:`, or `#` in the file name will cause errors at ingestion time. Rename any documents that include these characters before ingesting them.

- The retrieval methods for `natural_language_query` have been updated to improve the relevance of results by matching words with related semantics. This update only affects collections that have not had relevance training. If you are using `natural_language_query` and have not conducted relevance training, you may see improvement in the order of results returned.

{{site.data.keyword.discoveryshort}} tooling:

- Changes to the query builder to make it easier to toggle between the Discovery Query Language and Natural Language query options, as well as among query, filter, and aggregation.


### 25 August 2017

- The `passages` array now includes `field`, `start_offset`, and `end _offset`. `field` is the name of the field the passage was extracted from. `start_offset` is the starting character of the passage text within the field. `end_offset` is the ending character of the passage text within the field.

{{site.data.keyword.discoveryshort}} tooling:
This query building enhancement can be found on the **Build queries** screen.

-  Added the beta ability to write queries in the {{site.data.keyword.discoveryshort}} Query Language with a visual builder. Click **Build in visual mode** in the **Search for documents** and **Limit which documents you query** sections to try it out.  As you build your query visually, it will display in the **{{site.data.keyword.discoveryshort}} Query Language** below it.

   The visual query builder is currently supported only as a beta capability. See the statement regarding betas at the top of this document for more information.

### 18 August 2017

{{site.data.keyword.discoveryshort}} tooling:

- Added support for nested aggregations and conditions to the beta visual aggregation builder introduced [11 August 2017](/docs/services/discovery/release-notes.html#11aug). There is a limit of 3 conditions per aggregation row.

   The visual aggregation builder is currently supported only as a beta capability. See the statement regarding betas at the top of this document for more information.

### 11 August 2017
{: #11aug}

{{site.data.keyword.discoveryshort}} tooling:

Both features are query building enhancements and can be found on the **Build queries** screen.

- Added the option to select a query from a set of pre-built sample queries and aggregations. Click **Use a sample query** at the top right to access the list. If you are querying a private data collection, the samples use `top entities`, `categories`, etc. found in your collection. These queries can be used as a starting point for writing your own queries. Sample queries are available for both {{site.data.keyword.discoverynewsfull}} and private collections.

-  Added the beta ability to write aggregations with a visual builder. Click **Build in visual mode** above the **Write an aggregation query using the {{site.data.keyword.discoveryshort}} Query Language** field to try it out.  As you build your aggregation visually, the query will display in the **{{site.data.keyword.discoveryshort}} Query Language** below it.  

   The visual aggregation builder is currently supported only as a beta capability. See the statement regarding betas at the top of this document for more information.

### 31 July 2017

- A new version of {{site.data.keyword.discoverynewsfull}} was released. The original version has been renamed {{site.data.keyword.discoverynewsfull}} Original and has been retired with a removal from service date of **15, January 2018**. See [Migrating from Watson Discovery News Original](/docs/services/discovery/migrate-bwdn.html) for migration instructions.
  **Note:** If you have created a new instance of {{site.data.keyword.discoveryshort}}, you will only have access to the new version of {{site.data.keyword.discoverynewsfull}}.

- A new pricing plan for {{site.data.keyword.discoveryfull}} was released. See [{{site.data.keyword.discoveryshort}} pricing plans](/docs/services/discovery/pricing-details.html) for details.

- The version string for all API calls has changed to `2017-08-01` from `2017-07-19`. This version includes updates for the new pricing plan and the new version of Watson Discovery News. Update the version string to avoid conflicts and possible errors.

### 19 July 2017

 - As part of the pricing change that has been announced for August 1st 2017, users that are currently on the deprecated **30 day free trial** plan will be automatically migrated to the **Lite** plan. As a result of this transition, existing users may have met or exceeded the lite plan limit on documents _(2000)_, storage _(200Mb)_, or number of collections _(2)_. If you have exceeded the limit of the **Lite** plan, you will not be able to add any additional content into the service but you can still query collections. You can view the current status of all these limits by using the {{site.data.keyword.discoveryshort}} tooling or API. To be able to resume adding content to the {{site.data.keyword.discoveryshort}} instance, you must do one of the following:
   - remove collections and/or documents so that limits of the **Lite** plan are not exceeded.
     Documents can be deleted either individually through the API using the [delete-doc](https://console.bluemix.net/apidocs/discovery#delete-a-document) method, or whole collections can be deleted using the Tooling or API using the [delete-collection](https://console.bluemix.net/apidocs/discovery#delete-a-collection) method
   - upgrade your plan to a level that meets your storage needs.
 - Customers with size **`1`** **`2`** or **`3`** environments will be automatically migrated to the **Advanced** plan.

### 17 July 2017

 - The following capabilities have been moved from beta status to GA status:

   - Relevancy training
   - Natural language query
   - Highlighting

 - As of this release, {{site.data.keyword.discoveryfull}} is changing its enrichment mechanism from {{site.data.keyword.alchemylanguageshort}} to {{site.data.keyword.nlushort}}. {{site.data.keyword.alchemylanguageshort}} is in the process of being deprecated, you should start using {{site.data.keyword.nlushort}} as soon as possible.  See [Migrating from {{site.data.keyword.alchemylanguageshort}} enrichments to {{site.data.keyword.nlushort}} enrichments](/docs/services/discovery/migrate-nlu.html) for details.
   **Note:** When integrating with Watson Knowledge Studio, the {{site.data.keyword.alchemylanguageshort}} enrichment configuration must be still used. See [Integrating with {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery/integrate-wks.html) for details.

 - The version string for all API calls has been changed to `2017-07-19` from `2017-06-25`. This version enables a NLU default config on collection creation. You should still be able to enrich with {{site.data.keyword.alchemylanguageshort}} in previous versions.

    The default configuration has been updated to use {{site.data.keyword.nlushort}}. You should update the version string as soon as possible to avoid conflicts and possible errors.

 - Discovery Tooling:

    The Insight Cards for collections enriched with {{site.data.keyword.alchemylanguageshort}} enrichments will no longer update automatically. You must migrate your collection to {{site.data.keyword.nlushort}} Enrichments for the insight cards to update.

    If you created a collection prior to **18 July, 2017** and applied the **Default Configuration**, that collection was enriched with the {{site.data.keyword.alchemylanguageshort}} enrichments. If you apply the **Default Configuration** to a collection after this date, the {{site.data.keyword.nlushort}} enrichments will be used (the configuration name will switch to **Default Configuration with NLU** in the tooling). Since {{site.data.keyword.alchemylanguageshort}} enrichments are being deprecated, they should not be used with new collections.

### 30 June 2017
{: #30jun}

 -  The entity normalization capability introduced as a beta feature on 5 May 2017 has been moved to GA status. See [Creating a custom configuration to normalize entities](/docs/services/discovery/normalize-entities.html) for details.

### 23 June 2017

 - The version string for all API calls has changed to `2017-06-25` from `2016-12-01`. The new version string enables enrichments in German (`de`) or Spanish (`es`) if the language of a collection is set to one of those languages. Previously, all enrichments were performed in English regardless of a collection's language setting.

    If you do not use enrichments in non-English languages, you can continue to use the `2016-12-01` version string. However, you should update the version string as soon as possible to avoid potential future conflicts.

 - Anomaly detection is now available as part of `timeslice` aggregations as a GA capability. See [Timeslice anomaly detection](/docs/services/discovery/query-aggregations.html#anomaly-detection) for details.

 - Discovery Tooling:

   - Added the beta ability to improve the relevancy of query results using the Discovery tooling (relevancy tooling). See [Improving the relevance of your query results with the Discovery tooling](/docs/services/discovery/train-tooling.html).

### 19 June 2017

  - Discovery Tooling:

    - Added option to specify the language of the documents in a new collection as English, Spanish, or German. To use it, choose **Select the language of your documents** on the **Name your new collection** dialog.

    - Added a **Summary** tab to the **Build queries** screen. The **Summary** tab displays an overview of the full query results provided in the existing **JSON** tab. The **Summary** display will vary based on your query and enrichments. Information that may be displayed includes: document name or ID, aggregation statistics, document passages in order of relevance, and results by enrichment.

    - Added a Natural Language Query option to the **Build queries** screen. To use it, click **Ask a question in plain language** in the **Search for documents** section and a field will appear where you can enter your question. The original query field (formerly titled **Enter a query or keyword**) can now be accessed by clicking the **Use the Discovery Query Language** button.

    - The **Build queries** screen was redesigned, but all fields and options remain. Following are the old and new names for the fields.

| **Old field name**                                           | **New field or section name**                                                                                             |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| Write and run a query                                    | Search for documents                                                                                                  |
| Narrow your query results (Filter)                       | Limit which documents you query                                                                                       |
| Group query results (Aggregation)                        | Include analysis of your results                                                                                      |
| Fields to display                                        | Name did not change, but moved to the new **Customize display options** section.                                      |
| Number of documents to return (Count)                    | Number of documents to return [This field was moved to the **Customize display options** section.]                    |
| Include matching passages                                | Include relevant passages [This field was moved to the **Customize display options** section.]                        |
| Number of query fields to skip at the beginning (Offset) | Number of query results to skip at the beginning [This field was moved to the **Customize display options** section.] |

### 5 June 2017

 - Watson Discovery News queries now display only the first 150 words of each article in the `text` and `alchemyapi_text` JSON fields. The `blekko.snippet` field will display only the first sentence of the snippet array.

### 30 May 2017
{: #30may}

 - The `passages` parameter on the query API has been moved from beta to GA status.

### 25 May 2017

 - Discovery Tooling: query field highlighting was added in this release. This feature adds yellow highlighting to field names in the JSON of the Results pane. All fields that are queried or filtered on are highlighted for each result even if the content of the field does not match the query. Any fields used in aggregations are also highlighted in the query results, but only the first aggregation operation is highlighted.

### 10 May 2017

 - The `query` and `notices` methods now support the `highlight` parameter. The parameter is a boolean. When you run a query and specified `highlight` as `true`, the service returns output that includes a new `highlight` field in which words that match the query are wrapped in HTML `*` (emphasis) tags. See the [Query parameters](/docs/services/discovery/query-parameters.html#highlight) for details.

 - It is possible for the deletion of an environment to complete only partially, resulting in a situation in which a new environment cannot be created because only a single environment per service instance is permitted. If you attempt to delete and then create an environment but see either operation stuck in the `pending` state, it is likely you have encountered this problem. To work around it, re-run the deletion operation to complete it, then create the new environment.

### 8 May 2017

 - Updated the emotion tone score model to improve precision on emotion analysis (`docEmotion`) enrichments. The training dataset was expanded and feature engineering was altered and as a result, the model has higher precision on the benchmark dataset.

### 5 May 2017

 - Entity normalization is now available for use with the Discovery service that use a custom model generated by Watson Knowledge Studio. Entity normalization inserts normalized (canonical) names for different references to the same person or object in the source document. See [Creating a custom configuration to normalize entities](/docs/services/discovery/normalize-entities.html) for details.

     **Note:** Entity normalization is currently supported only as a beta capability. See the statement regarding betas at the top of this document for more information. [Resolved](/docs/services/discovery/release-notes.html#30jun)

{{site.data.keyword.discoveryshort}} tooling:

 - The Tooling error log is no longer limited to a maximum of eight (8) pages of results. The error log still displays the document ID if the document name is not available.

 - Configuration names are limited to 50 characters and must consist of the characters `[a-zA-Z0-9-_]`. 

 - The `passages` parameter previously available only through the API is now available through the Tooling as well as the API.

### 25 April 2017

  - The service now enables you to provide *training data* to improve the accuracy of your query results. When you provide a Discovery instance with training data, the service uses advanced Watson algorithms to determine the most relevant results. As you add more training data, the service instance becomes more accurate and sophisticated in the results it returns. See [Improving the relevance of your query results](/docs/services/discovery/train.html) and the [API Reference ](https://console.bluemix.net/apidocs/discovery#list-training-data) for information.

  - The API now supports the `natural_language_query` parameter as a beta release. This parameter enables you to specify a query in natural language instead of in the Discovery service's query language. See the [Query your collection](https://console.bluemix.net/apidocs/discovery#query-your-collection) method in the API reference for information.

  - Documentation updates and errata corrections.

### 14 April 2017

Enhancements have been added to the query API (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`). See the [Query your collection](https://console.bluemix.net/apidocs/discovery#query-your-collection) method in the API reference for information.

  - The query API now supports the `passages` parameter. If the parameter is set to `true`, the query returns a set of the most relevant passages from the documents in your collection. The passages are generated by sophisticated Watson algorithms to determine the best passages of text from all of the documents returned by the query. This enables you to find information and context more precisely. See the [Query your collection](https://console.bluemix.net/apidocs/discovery#query-your-collection) method in the API reference for information.

    - Specifying `passages=true` in your query can reduce performance as a result of increased processing to extract passages. With larger environments, the performance impact can be lessened.

    - The `passages` parameter is supported only on private collections. It is not supported in the Watson Discovery News collection.

    - The `passages` parameter currently returns a maximum of 10 results. The number of returned results cannot be changed. [Update](/docs/services/discovery/query-parameters.html#passages_count)

    - The `passages` parameter returns a maximum of three (3) passages from any given document in the collection. If a document contains more than three additional relevant passages, the parameter does not return them.

### 7 April 2017

- The query API (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`) now supports the `sort` parameter, which enables you to specify a comma-separated list of fields in the document to sort on. See the [Query your collection ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/discovery#query-your-collection){: new_window} method in the API reference for information.
- The `timeslice` parameter for query aggregations now correctly handles dates in UNIX epoch format. See [Query reference](/docs/services/discovery/query-reference.html#aggregations) for information about aggregations and the `timeslice` parameter.
- Improvements to error messages.
- Updates to the service's Java SDK. See the [API Reference](https://console.bluemix.net/apidocs/discovery?language=java) for details.
- The following limitations to the use of wildcards in queries are now fixed and work correctly:

  - Only one wildcard worked in any given query. For example, `query-month:*ctober` worked, but `query-month:*ctobe*` generated a parsing error.
  - Wildcards did not work with queries that contained capital letters. For example, given the key/field pair ``{"borrower": "GOVERNMENT OF INDIA"}``, `query-borrower:*ndia` returned results but `query-borrower:*NDIA` did not.

**Note:** Wildcards are not necessary within phrases in queries. For example, given the key/field pair `{"borrower": "GOVERNMENT OF TIMOR"}`, `query-borrower:"GOVERNMENT OF TIMOR"` returns results but `query-borrower:"GOVERNMENT OF TI*OR"` will not. Using a wildcard is not applicable within phrases because all of the characters within the quotation marks (`"`) of a phrase are escaped.

### 24 March 2017

- Added filtering to the "My data insights" screen in the Discovery tooling

### 15 March 2017

The following known issues have been discovered.

-  All fields that are ingested from HTML, PDF, and Word documents are typed as **string**. JSON fields and calculated fields, such as sentiment score, are typed as defined. [Update](/docs/services/discovery/adding-content.html#adding-content-with-the-api-or-tooling)
- The `preview` operation does not currently check for nested JSON arrays within a submitted JSON document. The service does not currently support nested JSON arrays, so a document with nested arrays can successfully pass the `preview` operation but fail upon an ingestion attempt. See [Can I upload JSON arrays?](/docs/services/discovery/troubleshooting.html#array)
- If you encounter ingestion errors with the message `unsupported text language`, update your configuration with the `"language": "english"` enrichment option to force all text to be interpreted as English, as shown in the following example. 
[Update](/docs/services/discovery/migrate-nlu.html)
```json
"enrichments": [
   {
     "enrichment": "alchemy_language",
     "source_field": "author.label",
     "options": {
       "extract": "taxonomy,entity,relation,doc-emotion,doc-sentiment,concept,keyword",
       "sentiment": true,
       "quotations": true,
       "language": "english"
     }
   }
 ]
```
{: codeblock}

The following bugs have been fixed.

- Improved performance and stability of the service.

### 8 March 2017

 - Optimized the back end, including the addition of new timeouts, to improve overall performance.
 - Fixed a bug that caused the environment status of free (`0`-sized) environments to report a status of `pending` regardless of the real status.
 - The only national language currently supported by {{site.data.keyword.discoveryshort}} is U.S. English (`en_US`). [Update](/docs/services/discovery/language-support.html)

### 3 March 2017

- Added the "My data insights" screen to the Discovery tooling.

### 26 February 2017

-     The performance of the {{site.data.keyword.discoverynewsshort}} environment has been improved.
-  The {{site.data.keyword.discoverynewsshort}} service returns only 50 results at a time. As a workaround, use the `offset` parameter in your query to page through results.
-  You can submit a new configuration with an individual document by using the following command:

```bash
curl -X POST -u apikey:{apikey_value} -F "file=@wikipedia-sample.html" -F "configuration=$(cat config.json)" "https://gateway.watsonplatform.net/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2016-12-01"
```
{: pre}
-  The service's PDF and Word converters create HTML as a middle step. The service can apply additional transforms and normalizations on the intermediary HTML before the final transformation to normalized JSON.

The following bugs have been fixed.

-  Improved error codes.
-  Corrected several documentation errata.

### 16 February 2017

-  You can now use CSS selectors to select JSON fields that you can then apply enrichments to. See [Using CSS selectors to extract fields](/docs/services/discovery/building.html#using-css) for information.
-  You can now increase the size of an environment by passing a new `size: X` parameter to the [update-environment method](https://console.bluemix.net/apidocs/discovery#update-an-environment), where `X` is an integer between 0 and 3. See the [create-environment method](https://console.bluemix.net/apidocs/discovery#create-an-environment) for information about environment sizes and attributes. [Update](/docs/services/discovery/pricing-details.html)

    **Note:** You cannot reduce the size of an existing environment. If you want to reduce the size of your environment, contact {{site.data.keyword.IBM}} support for assistance.

-  A new query operator is available. The `::!` operator has been added as a unary not-equals operator. For example, you can now run `query=field::!value` (not equals). Previously the only exclusionary operator was `:!` for the not-contains operator (for example, `query=field:!value`).

The following bugs have been fixed.

-  Applied security updates.
-  Improved status messages for search alerts.

### 1 February 2017

The following notes apply specifically to the Data Crawler 1.3.0 release.
[Update](/docs/services/discovery/data-crawler.html)

-   The Data Crawler records the `document_id` values used to upload documents, and the status of the upload. Conversion notices are not persisted outside of the log. There is not presently a tool to interact with that data, but such tools are expected to be developed as time permits. The data is accessible via H2 database, which could be configured to use a remote DBMS.

### 16 January 2017

The following notes apply specifically to the Data Crawler 1.2.5 release.
[Update](/docs/services/discovery/data-crawler.html)

-  The Data Crawler can optionally poll for document status immediately after uploading a file. This check is a part of the Crawler's concept of "uploading a document", so when this check is enabled, it is virtually impossible for the Crawler to upload concurrently more documents than what the {{site.data.keyword.discoveryshort}} service can process concurrently for the user.

    A side effect of the `check_for_completion` feature is that the Crawler also can expose to the user why a document failed, when it failed. Any notices attached to a document that was successfully uploaded, but failed to process, are displayed in the Crawler log. The notices are not exported to a processable file, but IBM would welcome a feature suggestion for that.

### 5 January 2017

The following notes describe issues that were identified after the GA release on 15 December 2016.

[Update: API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/discovery){: new_window}

-   If you add a document by using the `POST /v1/environments/{environment_id}/collections/{collection_id}/documents`
    or `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]` call, the call returns a document ID and the **processing** status. If you then query the document by using the `GET /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]` call, the status remains at **processing** until ingestion is completed, at which point the status changes to **available**.

    If you **update** an existing document by using the `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]` call, the corresponding **GET** call returns the `available` status even if the service has not yet fully processed the updated document. The `available` status can refer to either the original document or the updated document. Unless the update operation returns an error, there is not currently a way to determine the status of the updated document.

    You can work around this by waiting up to 10 minutes after submitting a document update before attempting to query the updated content.

### General Availability release, 15 December 2016

The following notes apply to the General Availability (GA) release of the {{site.data.keyword.discoveryfull}} service.

#### General notes
[Update: Adding content](/docs/services/discovery/adding-content.html)

See [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/discovery){: new_window} for current API version.

[Update: Integrating with {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery/integrate-wks.html).

-   You cannot currently specify the data type of fields. All fields are indexed as text (data type **string**). 
-   If you use the API to work with the service, you must specify the API version with each call. The current API version is **2016-12-01**. 

    **Note:** The specific version is not enforced in the GA release, but it still must be listed to enable compatibility with future releases.

-   You can use the service with a custom model created with {{site.data.keyword.knowledgestudiofull}}. The custom model can be used to enrich ingested documents. You must use the API to integrate the custom model with the {{site.data.keyword.discoveryshort}} service; you cannot perform the integration by using the tooling.

#### Data management
[Update](/docs/services/discovery/pricing-details.html)

-   Search indexes are not encrypted.
-   Backup and restore functions are not user controllable.

#### Environments
[Update](/docs/services/discovery/pricing-details.html)

-   You can create only one environment per service instance to upload your own data.
-   {{site.data.keyword.discoveryshort}} service is located in a single availability zone (US South).
-   Dedicated and premium plans are not available at the current time.

#### Environment sizing
[Update](/docs/services/discovery/pricing-details.html)

-   You can choose an environment size only when creating a new environment. The ability to resize an environment is not currently available to users.
-   Choosing an environment size with more RAM increases performance.
-   There are currently no prescriptive sizing recommendations available for specific use cases.
-   Custom sizing for {{site.data.keyword.knowledgestudiofull}} models is not self-serve. Contact your {{site.data.keyword.IBM}} representative for more information.

#### Ingestion limitations
[Update](/docs/services/discovery/pricing-details.html)

-   The ingestion rate is currently limited to 100 concurrent document ingestion operations. An application that submits documents to the service for ingestion needs to respect HTTP 429 errors and throttle down ingestion requests accordingly.
-   {{site.data.keyword.alchemylanguageshort}} enrichments are limited to the first 50 kB per field.
-   Enrichments from {{site.data.keyword.knowledgestudiofull}} custom models are not limited, but split documents into 10-kB chunks. No relationships are annotated across chunk boundaries.

#### Query limitations
[Update](/docs/services/discovery/using.html#query-concepts)

-   Excessive query load can cause the search-index process to restart automatically.
-   Applications that issue queries must enforce reasonable limits on the number of concurrent queries.

### Known issues
[Update: API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/discovery){: new_window}

[Update: tooling](/docs/services/discovery/getting-started-tool.html)

[Update: Data Crawler](/docs/services/discovery/data-crawler.html)

[Update: Enrichments](/docs/services/discovery/building.html#adding-enrichments)

[Update: Adding content](/docs/services/discovery/adding-content.html)

-   You cannot delete a document by using the tooling. If you need to delete a document, you must use the API's [Delete a document](https://console.bluemix.net/apidocs/discovery#delete-a-document) method as described in the API reference.

-   The API does not currently support getting a list of notices (warnings and error) that are generated during document ingestion. The tooling is therefore unable to show a list of ingestion notices, and there is no easy way to determine which, if any, documents crawled by the Data Crawler failed to be ingested. 
-   Document status information is not always accurate.
    -   If an ingestion operation takes longer than the configured timeout of 10 minutes, the service reports that the document is not known to the service until the ingestion operation completes. After the operation completes, the document status is available and accurate.
    -   Documents that are successfully indexed but generated errors can have a status of **failed** for a short period of time until the document has been fully committed to the index. After the document has been committed to the index, the listed status is accurate.
-   You cannot use the tooling to replace a specific document. If you attempt to do so, the second document is uploaded as a separate document. If you are using the API and know the ID of the document you want to replace, you can do so; see [Update a document](https://console.bluemix.net/apidocs/discovery#update-a-document) in the API reference. If you are using the Data Crawler, uploading an updated document from the same URL as a previous document replaces the original document.
-   If you are using the tooling to edit the enrichments in your configuration, you can edit only enrichments used for extraction. If you want to add or edit other enrichments (for example, custom enrichments from a {{site.data.keyword.knowledgestudiofull}} model), you must use the API. See the [Update a configuration](https://console.bluemix.net/apidocs/discovery#update-a-configuration) method in the API reference for information.
-   The following notes apply specifically to the Data Crawler. 
    -   The Data Crawler retries uploads if it encounters an upload failure.
    -   The Data Crawler is unable to retry documents that uploaded successfully but failed to be converted or indexed.
    -   The Data Crawler does not have a function to check downstream status and attempt to re-upload URLs that failed downstream.
    -   There is no easy way to determine which documents have been ingested by the Data Crawler. For example, if you run the Data Crawler against a set of 500 documents, the Data Crawler might report failures submitting 65 documents with a total collection of 212 documents. The status of the remaining 223 documents is undetermined.

        A workaround is available, but it is complicated and involves invoking the API directly. Contact {{site.data.keyword.IBM}} support for assistance.
-   The Java, Python, and Node.js SDKs for {{site.data.keyword.discoveryshort}} do not provide all of the functionality provided by the default REST (cURL) API. Not all cURL methods have an equivalent method in the non-cURL SDKs, and not all non-cURL methods provide all of the same features that their cURL equivalents have. In other words, the Java, Python, and Node.js SDKs currently provide only a subset of the cURL API's capabilities.
-   If you use the Word converter, matching on headings by using the `style` key is much more accurate and efficient than it by using the `level` key.
