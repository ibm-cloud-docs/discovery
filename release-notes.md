---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-06-04"

subcollection: discovery

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

# Release notes
{: #release-notes}

The release notes provide information about changes to {{site.data.keyword.discoveryfull}} since the previous release.
{: shortdesc}

## Service API Versioning
{: #apiversioning}

API requests require a version parameter that takes a date in the format `version=YYYY-MM-DD`. Whenever we change the API in a backwards-incompatible way, we release a new minor version of the API.

Send the version parameter with every API request. The service uses the API version for the date you specify, or the most recent version before that date. Don't default to the current date. Instead, specify a date that matches a version that is compatible with your app, and don't change it until your app is ready for a later version.

The current version is `2019-04-30`.

## Beta features
{: #beta-features}

IBM will release services, features, and language support that are classified as beta or experimental. These capacities can be unstable, can change frequently, and can be discontinued with short notice. They are provided so you can evaluate their functionality. A beta or experimental capacity might not provide the same level of performance or compatibility that generally released capacities provide. These capacities are not designed for use in a production environment, and any such use is at your own risk.


## Changes
{: #change-log}

The following new features and changes to the service are available.

## 4 June 2019
{: #4jun19}

The Preview API has been deprecated and will no longer be available effective **30 September 2019**. 

## 30 April 2019
{: #30apr19}

[Query expansion](/docs/services/discovery?topic=discovery-query-concepts#query-expansion) and [Stopword](/docs/services/discovery?topic=discovery-query-concepts#stopwords) lists can now be uploaded or deleted using the **Search settings** screen in the {{site.data.keyword.discoveryshort}} tooling. Previously, these lists could only be managed using the API.

- The version string for all API calls has changed to `2019-04-30` from `2019-03-25`.

## 26 April 2019
{: #26apr19}

The {{site.data.keyword.discoveryfull}} update announced on [April 2, 2019](/docs/services/discovery?topic=discovery-release-notes#2apr19) is complete. This upgrade included changes to improve the accuracy of the scoring algorithms used in {{site.data.keyword.discoveryshort}} for ranking documents and passages. The changes to your `score` and `confidence` should be small, and there may also be some small changes to the ranking order. If your applications make use of the `score` or `confidence` fields directly, you should update your applications as necessary.

- Multi-token query expansion is now supported. See [Query expansion](/docs/services/discovery?topic=discovery-query-concepts#query-expansion) for more information.

## 17 April 2019
{: #17apr19}

The Data Crawler is no longer available for download and is no longer supported. See [Connecting to Data Sources](/docs/services/discovery?topic=discovery-sources#sources) for other connectivity options.

## 2 April 2019
{: #2apr19}

Beginning April 9, 2019, there will be an upgrade to {{site.data.keyword.discoveryfull}}. This upgrade will include changes to the scoring algorithms used in {{site.data.keyword.discoveryshort}} for ranking documents and passages. This means score and confidence results may change following the upgrade. If your applications make use of the `score` or `confidence` fields directly, be prepared to update the application as necessary. See [Upgrading the infrastructure of the {{site.data.keyword.discoveryfull}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/cloud-archive/2019/03/announcement-for-the-ibm-watson-discovery-community/){: new_window} for details.

## 25 March 2019
{: #25mar19}

- The version string for all API calls has changed to `2019-03-25` from `2019-01-01`

- The `title` field is now extracted from HTML documents as a top-level field during conversion. See [HTML conversion](/docs/services/discovery?topic=discovery-configservice#html-conversion). This `title` field will be also be included in each segment of any documents split using document segmentation, see [Splitting documents with document segmentation](/docs/services/discovery?topic=discovery-configservice#doc-segmentation) for an example. This may improve the `confidence` score for query results, and may change the `passages` returned, because the `title` may be returned as part of a passage. Existing collections will need to be reindexed to extract the `title` field.

The {{site.data.keyword.discoveryshort}} tooling does not yet use the current API version: `2019-03-25` (it currently uses `2018-12-03`), so the `title` will not be extracted when ingesting HTML documents by uploading or using the Web Crawl connector in the {{site.data.keyword.discoveryshort}} tooling.
{: note}

- Arrays can now be enriched (previously, arrays could not be enriched). When using Smart Document Understanding, this means that you can now enrich both default (for example: `answer`, `author`, `footer`, `header`, `question`, `subtitle`, `table_of_contents`, `text`, and `title`) and custom fields. Previously, you were limited to enriching only the `text` field.

## 21 March 2019
{: #21mar19}

From March 21 2019, you will see only service credential information associated with the role that has been assigned to your {{site.data.keyword.cloud_notm}} account. For example, if you have assigned a `reader` role, any `writer` or higher levels of service credentials will not be visible.

This change does not affect API access for users or applications with existing service key credentials. Only the viewing of credentials within {{site.data.keyword.cloud_notm}} is affected.

For more information about service keys and user roles, see [IAM service API keys](/docs/services/watson?topic=watson-api-key-bp#api-key-bp).

## 10 February 2019
{: #10feb19}

- Added the option to connect to and sync with IBM Cloud Object Storage. This data source is not available in Dedicated environments. See [IBM Cloud Object Storage](/docs/services/discovery?topic=discovery-sources#connectcos) for more information.

## 4 February 2019
{: #4feb19}

Updated to general availability:

-  [Smart Document Understanding (SDU)](/docs/services/discovery?topic=discovery-sdu#sdu) has moved from beta status to GA status.
   -  Table annotation remains in beta status. A statement explaining beta features can be found [here](/docs/services/discovery?topic=discovery-release-notes#beta-features).
   -  The `Data settings` button on the upper right has been renamed `Configure data`.
   -  Uploading a document is no longer required to access the `Configure data` (formerly `Data settings`) button.

The beta of SDU was announced [January 22, 2019](/docs/services/discovery?topic=discovery-release-notes#22jan19).   
    
## 28 January 2019
{: #28jan19}

Assistance is no longer provided for the Data Crawler if you are using it with a data source supported by the {{site.data.keyword.discoveryshort}} connectors. The {{site.data.keyword.discoveryshort}} connectors support crawling Box, SharePoint, Salesforce, and more. See [Connecting to data sources](/docs/services/discovery?topic=discovery-sources#sources) for details. The Data Crawler should only be used to crawl file shares or databases, in all other cases, use the {{site.data.keyword.discoveryshort}} connector. Another option to upload large numbers of files into {{site.data.keyword.discoveryshort}} is [discovery-files ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM/discovery-files){: new_window} on GitHub.

## 22 January 2019
{: #22jan19}

- Released the beta version of [Smart Document Understanding (SDU)](/docs/services/discovery?topic=discovery-sdu#sdu), a new way to train {{site.data.keyword.discoveryfull}} to extract custom fields in your documents. With Smart Document Understanding, you annotate fields within your documents to train custom conversion models. A statement explaining beta features can be found [here](/docs/services/discovery?topic=discovery-release-notes#beta-features).

The beta SDU editor is only available for new collections that contain supported document types and do not have the Element Classification enrichment applied. Existing Private collections will use the original configuration method.

If you were part of the closed beta for Smart Document Understanding, do not import models created in that beta into this version. Smart Document Understanding is currently not available in Dedicated environments.

The SDU editor functions are only available in the {{site.data.keyword.discoveryshort}} tooling, they are not available in the API.

## 15 January 2019
{: #15jan19}

Element Classification updates:
-  The Element Classification enrichment has updated parties, categories, and attributes in API version `2018-10-15` or later. See [Parsing contracts](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing) for the updates.

- The output of the `/v1/element_classification` method now includes the following:
    - The `parties` array now includes an `importance` field that indicates whether the party is a `Primary` party or an `Unknown` (non-primary) party.
    - The `effective_dates`, `contract_amounts`, and `termination_dates` arrays now each include a `confidence_level` field that indicates a value of `High`, `Medium`, or `Low`.
    For more information, see [Classifying elements](/docs/services/discovery?topic=discovery-output_schema#output_schema) and [Parsing contracts](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing).

    The {{site.data.keyword.discoveryshort}} tooling does not yet use the current API version: `2019-01-01` (it currently uses `2018-12-03`), so you will not see these new fields in the Element Classification output in the {{site.data.keyword.discoveryshort}} tooling.

## 10 January 2019
{: #10jan19}

Known issue:

-  If you specify a `customer-id` using the normalization method described in [Specifying a `customer_id`](/docs/services/discovery?topic=discovery-sources#source_customer_id) and subsequently attempt to delete documents containing that `customer_id` using the method described here: [Deleting labeled data](/docs/services/discovery?topic=discovery-information-security#deletingdata), the associated source document will not be deleted.

## 1 January 2019
{: #1jan19}

- The version string for all API calls has changed to `2019-01-01` from `2018-12-03`. This version introduces a new document ingestion status: `pending`. The `pending` status will be returned for documents that have been accepted, but have not yet started processing. Previously, these documents would have the status of `processing`. The {{site.data.keyword.discoveryshort}} tooling does not yet use this API version (it currently uses `2018-12-03`), so when you check document status in the {{site.data.keyword.discoveryshort}} tooling, the `pending` status will not be returned.

## 21 December 2018
{: #21dec18}

- Added the option to connect to and sync with Microsoft SharePoint 2016 On-Premise. This data source is not available in Dedicated environments. See [SharePoint 2016 On-Premise](/docs/services/discovery?topic=discovery-sources#connectsp_op) for more information.

- Added the beta version of the Web crawl connector, which can be used connect to, crawl, and sync with websites. This data source is not available in Dedicated environments. See [Web crawl](/docs/services/discovery?topic=discovery-sources#connectwebcrawl) for more information. A statement explaining beta features can be found [here](/docs/services/discovery?topic=discovery-release-notes#beta-features).

- The Microsoft SharePoint Online, Salesforce, and Box data sources are now available in Premium environments. They are not available in Dedicated environments.

## 17 December 2018
{: #17dec18}

- Added full support for Italian. For more information, see [Language support](/docs/services/discovery?topic=discovery-language-support#language-support).

## 14 December 2018
{: #14dec18}

-  You can now create {{site.data.keyword.discoveryshort}} instances that are hosted in the London data center without syndication. Like all locations, the {{site.data.keyword.cloud}} London location (eu-gb) uses token-based Identity and Access Management (IAM) authentication. All new services instances that you create in this location use IAM authentication.

-  The {{site.data.keyword.discoveryshort}} tooling now uses the API version of `2018-12-03`(it previously used `2018-08-01`).

## 12 December 2018
{: #12dec18}

- Added the ability to define and upload a custom stopwords list. Custom stopwords are implemented with the {{site.data.keyword.discoveryshort}} API. See [Defining stopwords](/docs/services/discovery?topic=discovery-query-concepts#stopwords) for details. 

## 3 December 2018
{: #3dec18}

- For all queries (with the exception of filter-only queries) written using the API version of `2018-12-03` or above, {{site.data.keyword.discoveryshort}} will now return a `confidence` score in the query results set, even if the collection was not trained using a supervised training method, such as [Relevancy training](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling) or [Continuous Relevancy Training](/docs/services/discovery?topic=discovery-crt#crt). In addition, {{site.data.keyword.discoveryshort}} will return a `document_retrieval_strategy` field that indicates the source of the `confidence` score of `untrained`, `relevancy_training`, or `continuous_relevancy_training`. For more information, see [Confidence scores](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence).

- The version string for all API calls has changed to `2018-12-03` from `2018-10-15`. The {{site.data.keyword.discoveryshort}} tooling does not yet use this API version (it currently uses `2018-08-01`), so queries written using the {{site.data.keyword.discoveryshort}} tooling will not return a `confidence` score for untrained collections.

## 8 November 2018
{: #8nov18}

- {{site.data.keyword.discoveryshort}} launched in the `Tokyo` location 8 November, 2018. Premium and Dedicated environments are not currently available in `Tokyo`.

## 30 October 2018
{: #30oct18}

- {{site.data.keyword.discoveryshort}} now supports token-based Identity and Access Management (IAM) authentication in all regions. IAM uses access tokens rather than service credentials for authentication with a service. For more information about using IAM tokens with existing and new applications, see the [17 May 2018](#17May18) release update.

## 25 October 2018
{: #25oct18}

The schema for the [Element Classification](/docs/services/discovery?topic=discovery-element-classification#element-classification) enrichment has changed. If you wish to use the updated schema, you must ingest your documents with the API, using the version date of `2018-10-15` or later. The {{site.data.keyword.discoveryshort}} tooling does not yet use this API version (it currently uses `2018-08-01`), so documents ingested using the {{site.data.keyword.discoveryshort}} tooling will be enriched with the original schema.

## 24 October 2018
{: #24oct18}

- {{site.data.keyword.discoverynewsfull}} queries display approximately 50 words from each article in the `text` JSON field. These words will now be extracted from the highlights, rather than simply displaying the first 50 words of the article. See [highlight](/docs/services/discovery?topic=discovery-query-parameters#highlight) for an explanation of highlights. Highlights do not need to be explicitly included in your query to enable this behavior.

## 25 September 2018
{: #25sept18}

- Released Continuous Relevancy Training, which uses interactions from users to learn how to surface the most relevant results. It can learn from user behavior automatically, significantly reducing the effort required to improve the relevancy ranking of results.  See [Continuous Relevancy Training](/docs/services/discovery?topic=discovery-crt#crt) for details.

- Added API support for performing longer queries. This increases the character limit to 10,000 characters, and makes it possible to increase the number of filters in your queries and perform more complex aggregations. See the POST Query at [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#long-collection-queries){: new_window} and [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#long-environment-queries){: new_window} for details.

- You can now upgrade your Advanced plan using the API. See [Upgrading your plan](/docs/services/discovery?topic=discovery-upgrading-your-plan#switchadvanced) for details. 

- The Element Classification enrichment has updated the classified elements, contract elements, and parties and tables identified. See [Element Classification](/docs/services/discovery?topic=discovery-element-classification#element-classification) for the updates.

- Added full support for Brazilian Portuguese. For more information, see [Language support](/docs/services/discovery?topic=discovery-language-support#language-support).

- The query API (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`) now supports the `bias` parameter, which allows you to bias towards certain results, for example, documents that were published most recently. See the [Query your collection ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window} method in the API reference for information.

- The **Default Contract Configuration** file provided to enrich collections for [Element Classification](/docs/services/discovery?topic=discovery-element-classification#element-collection) was found to have an issue with HTML normalizations. A new **Default Contract Configuration** is included with this release. Follow the steps below to apply the new **Default Contract Configuration** to your collections.

     1. Determine which of your collections are using either the **Default Contract Configuration** configuration file, or a custom configuration based on **Default Contract Configuration**.
     1. Make note of the changes you made to any custom configurations based on **Default Contract Configuration**.
     1. Since the old **Default Contract Configuration** file needs to be deleted from your environment before the new one is used, use the API [Delete configuration ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#delete-a-configuration){: new_window} to delete the current **Default Contract Configuration** associated with any of your collections. Also delete any configurations based on the old **Default Contract Configuration**.
     1. Now you can use the new **Default Contract Configuration** file. For each collection using one of those configurations, create a new collection. Apply the new **Default Contract Configuration** or create a new custom configuration based on the new **Default Contract Configuration** using the notes you made in step 2.
     1. Upload the files previously ingested to the original collections.
     1. Delete the old collections.

## 15 August 2018
{: #15aug18}

- Two new query operators are available. `Exists` (`:*`) can be used to return all results where the specified `field` exists. `Does not exist` (`!*`) can be used to return all results that do not include the specified `field`. See [Query operators](/docs/services/discovery?topic=discovery-query-operators#query-operators) for more information. 

## 2 August 2018
{: #2aug18}

- {{site.data.keyword.discoveryfull}} now supports English, Spanish, German, Italian, Portuguese, French, Arabic, Korean, and Japanese language collections when connecting and syncing to Box, Salesforce, and SharePoint Online with the {{site.data.keyword.discoveryshort}} tooling. 

## 31 July 2018
{: #31jul18}
 
 - Beginning **August 1, 2018**, {{site.data.keyword.discoveryfull}} has a new pricing structure. It features a simpler pricing model (document hours are no longer part of the calculation) and tiered pricing for {{site.data.keyword.discoverynewsfull}} queries. In addition, the Standard plan has been retired, and the Lite plan has reduced document and {{site.data.keyword.discoverynewsshort}} query limits. The pricing changes will require no action by current {{site.data.keyword.discoverynewsshort}} users. See [{{site.data.keyword.discoveryshort}} Pricing Plans](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans) for details.
 
**Note:** The version date of the API has been updated to `2018-08-01`. To take advantage of the new environment sizing options (`LT`, `XS`, `S`, `MS`, `M`, `ML`, `L`, `XL`, `XXL`, `XXXL`), you must use this version date when creating environments with the API. The environment sizes now have the type of `string` (previously the type was `integer`.)

## 27 July 2018
{: #27jul18}

- Released [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) in one additional language: Japanese (`collection_id`: `news-ja`). {{site.data.keyword.discoverynewsfull}} is also available in English, Spanish, German, and Korean.

## 25 June 2018
{: #25jun18}

- Added the option to connect to and sync with Salesforce, Microsoft SharePoint Online, and Box data sources. These data sources are not available in Premium environments. Released the [Source Credential ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#list-credentials){: new_window} and [Configuration ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#add-configuration){: new_window} APIs for these data sources. 
  - {{site.data.keyword.discoveryfull}} supports only English language collections when connecting and syncing to Box, Salesforce, and SharePoint Online with the {{site.data.keyword.discoveryshort}} tooling. [Resolved](/docs/services/discovery?topic=discovery-release-notes#2aug18)
  - The individual document file size limit for Box, Salesforce, and SharePoint Online is 10MB.
- Added a new Performance Dashboard in {{site.data.keyword.discoveryshort}} tooling. See [Viewing metrics and improving query results with the Performance dashboard](/docs/services/discovery?topic=discovery-performance-dashboard#performance-dashboard). The new dashboard is not available in Premium or Dedicated environments.
- Added full support for Japanese. For more information, see [Language support](/docs/services/discovery?topic=discovery-language-support#language-support).

## 22 June 2018
{: #22jun18}

- Released the Events and Feedback API. See the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#create-event){: new_window} for more information.

## 11 June 2018
{: #11jun18}

-  For applications that are hosted in Washington, DC (US East), the service now supports token-based Identity and Access Management (IAM) authentication. IAM uses access tokens rather than service credentials for authentication with a service. For more information about using IAM tokens with existing and new applications, see the [17 May 2018](#17May18) release update.
-  An additional contract element is now supported in Element Classification: `Safety and Security`. See [Understanding Contract Elements](/docs/services/discovery?topic=discovery-element-classification#contract-elements) for details.

## 6 June 2018
{: #6jun18}

- {{site.data.keyword.discoverynewsfull}} queries now display the first 50 words of each article in the `text` JSON field. [Update](#24oct18)

## 5 June 2018
{: #5jun18}

- Element Classification is now available to those subscribed to Premium plans.
- The `assurance` rating of `Low` is no longer available for Element Classification.

## 31 May 2018
{: #31may18}

- Added full support for French. For more information, see [Language support](/docs/services/discovery?topic=discovery-language-support#language-support).

## 30 May 2018
{: #30may18}

- Fixed a known issue in {{site.data.keyword.discoverynewsfull}}. Previously, when querying {{site.data.keyword.discoverynewsshort}} it was possible to receive an incorrect document count because documents in other languages would be counted along with the language you requested. This is no longer the case.
- Beginning with collections created on `22 May 2018` and after {{site.data.keyword.discoveryshort}} now returns query results that include special characters for the following languages: English, German, French, Dutch, Italian, and Portuguese. For example, if you query for `aqui`, you will now receive results for both for `aqui` and <code>aqu&iacute;</code>.

## 21 May 2018
{: #21may18}

- Released [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) in one additional language: German (`collection_id`: `news-de`). {{site.data.keyword.discoverynewsfull}} is also available in English, Spanish, and Korean.

## 17 May 2018
{: #17May18}

- {{site.data.keyword.discoverynewsfull}} queries now display only the first 20 words of each article in the `text` JSON field.

-   The service now supports a new API authentication process for service instances for applications that are hosted in Sydney (**au-syd**) as of May 15, 2018. They will be enabled for applications that are hosted in other regions soon. {{site.data.keyword.Bluemix}} is in the process of migrating to token-based Identity and Access Management (IAM) authentication. IAM uses access tokens rather than service credentials for authentication with a service.

   In the Sydney location, you use IAM access tokens with {{site.data.keyword.discoveryshort}} for

    -   *New service instances* that you create after May 15. For more information, see [Authenticating with IAM tokens ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/docs/services/watson?topic=watson-iam#iam){: new_window}.
    -   *Existing service instances* that you migrate from Cloud Foundry to a resource group that is managed by the Resource Controller (RC). Service instances that were created before May 15 continue to use service credentials for authentication until you migrate them. For more information, see [Migrating Cloud Foundry service instances to a resource group ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/docs/resources?topic=resources-migrate#migrate){: new_window}.

    All new and existing service instances in other regions continue to use service credentials (`apikey:{apikey_value}`) for authentication.

### Using an IAM access token to authenticate
{: #iam-token}

When you use IAM access tokens, you authenticate before you send a request to {{site.data.keyword.discoveryshort}}.


1.  Get an API key from IBM Cloud. Use that key to generate an IAM access token. For more information, see [How to get an IAM token by using a {{site.data.keyword.watson}} service API key ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/docs/services/watson?topic=watson-iam#iamtoken){: new_window}.
1.  Pass the IAM access token to {{site.data.keyword.discoveryshort}} by using the `Authorization` header. In the header, indicate that the access token is a `Bearer` token by specifying `Authorization: Bearer {access_token}`.

    The following simple cURL example uses an access token:

    ```bash
    curl -X GET
    --header "Authorization: Bearer eyJhbGciOiJIUz......sgrKIi8hdFs"
    "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    For more information, see [Using a token to authenticate ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/docs/services/watson?topic=watson-iam#use_token){: new_window}.

### Refreshing an IAM access token
{: #iam-refreshing}

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

In your application, check the access token's expiration time before you use it to make an authenticated request. If it is expired, you must refresh the access token before you can use it. You use the value of the `refresh_token` field to refresh the access token. For more information, see [Refreshing a token ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/docs/services/watson?topic=watson-iam#iamtoken){: new_window}.


## 11 May 2018
{: #11may18}

- Details about information security can be found here: [Information security](/docs/services/discovery?topic=discovery-information-security#information-security).
- The following {{site.data.keyword.discoveryfull}} Knowledge Graph `query_entities` known issue has been fixed with the `2018-05-04` API version update. This fix only applies if entities are ingested or replaced after `2018-05-04`. Entities can be replaced by re-ingesting old documents or by ingesting new documents containing those entities. If old entities are not replaced, then `query_entities` will return all upper case with `2018-05-04` API version.
  - All entity names were previously converted to camel case in `query_entities`. For example, the entity name "IBM Corporation" was converted to "Ibm Corporation". This is no longer the case.

## 9 May 2018
{: #9may18}

- Sample documents are now stored locally, in your browser's local roaming data folder. For more information about sample documents, see [Uploading sample documents](/docs/services/discovery?topic=discovery-configservice#uploading-sample-documents).

## 4 May 2018
{: #4may18}

- Two additional contract elements are now supported in Element Classification: Attributes and Provenance. See [Understanding Contract Elements](/docs/services/discovery?topic=discovery-element-classification#contract-elements) for details.

## 26 April 2018
{: #26apr18}

- The following ingestion issue has been fixed: In some cases where post-enrichment `json_normalizations` and/or `normalizations` were specified, the normalizations may have been applied in the wrong order. This could result in documents being indexed with unexpected field values. This is no longer the case.
- The maximum file size for a sample document is now 1MB. The maximum file size was previously 5MB.

## 12 April 2018
{: #12apr18}

- Knowledge Graph: [Evidence](/docs/services/discovery?topic=discovery-kg#kg_evidence) and [Canonicalization and filtering](/docs/services/discovery?topic=discovery-kg#kg_canonicalization) are now available in all collections. In any collections created before `03-05-2018`, you need to reingest your documents to use these features. Previously, you needed to create a new collection and reingest your documents.

## 11 April 2018
{: #11apr18}

- Two additional categories are now supported in Element Classification: `Asset Use` and `Communication`. See [Understanding Contract Elements](/docs/services/discovery?topic=discovery-element-classification#contract-elements) for details.

## 2 April 2018
{: #2apr18}

- Sample documents are now automatically deleted after 24 hours, instead of 1 month.

## 16 March 2018
{: #16mar18}

- Added full support for German. For more information, see [Language support](/docs/services/discovery?topic=discovery-language-support#language-support).

{{site.data.keyword.discoveryshort}} tooling:
- A new configuration named **Default Contract Configuration** has been added to support Element Classification, which can be used to extract party, nature, and category from elements in PDFs. See [Element Classification](/docs/services/discovery?topic=discovery-element-classification#element-collection) for details.

Updated to general availability:
- Documentation segmentation has moved from beta status to GA status. The segmentation limit has been increased to 250 segments. It is no longer limited to 50 segments per document. See [Documentation segmentation](/docs/services/discovery?topic=discovery-configservice#doc-segmentation) for details.

Known issue:
- Wildcards do not work with queries that contain capital letters. For example, given the key/field pair ``{"borrower": "GOVERNMENT OF INDIA"}``, `query-borrower:*ndia` will return results but `query-borrower:*NDIA` will not.

## 8 March 2018
{: #8mar18}

- The beta version of {{site.data.keyword.discoveryfull}} Knowledge Graph added several features. During the beta release, [Knowledge Graph](/docs/services/discovery?topic=discovery-kg#kg) functionality and the methods associated with it are only available for service instances that are subscribed to **Advanced** plans, **Premium** plans, and all **Dedicated** environments. The new features are:
  - [Entity similarity](/docs/services/discovery?topic=discovery-kg#kg_similarity)
  - [Evidence](/docs/services/discovery?topic=discovery-kg#kg_evidence)
  - [Canonicalization and filtering](/docs/services/discovery?topic=discovery-kg#kg_canonicalization)

## 7 March 2018
{: #7mar18}

- The following ingestion known issue has been fixed: Between 28 February and 6 March, a small percentage of documents were indexed with only the `id` and `extracted_metadata` fields (other document content was not indexed). The underlying problem has been fixed, however, you will need to resubmit any affected documents for ingestion. There is no simple way to identify the affected documents.

## 5 March 2018
{: #5mar18}

- The following {{site.data.keyword.discoveryfull}} Knowledge Graph known issue has been fixed with the `2018-03-05` API version update. This fix only applies to newly created collections that use the `2018-03-05` version update.  
  - All entity type names and relation type names were previously converted to uppercase during ingestion. For example, the entity "GeoPoliticalEntity" was converted to "GEOPOLITICALENTITY," and the relation "partOf" was converted to "PARTOF." This is no longer the case.

## 1 March 2018
{: #1mar18}

- [Query expansion](/docs/services/discovery?topic=discovery-query-concepts#query-expansion) limits have been increased for Advanced and Premium plans to 5,000 query expansions and 25,000 total terms. See [Discovery pricing plans](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans) for details.

## 28 February 2018
{: #28feb18}

- {{site.data.keyword.alchemylanguageshort}} enrichments have been deprecated effective **1 March 2018**.

## 23 February 2018
{: #23feb18}

- Added the ability to query by document similarity. You can query for similar documents by  document ids, and optionally further refine the similarity by specifying fields. See [Document similarity](/docs/services/discovery?topic=discovery-query-concepts#doc-similarity) for more information.

- The [`highlight` parameter](/docs/services/discovery?topic=discovery-query-parameters#highlight) in query results has been enhanced. Query results will return complete sentences, ordered by their `score`.

## 21 February 2018
{: #21feb18}

- Previously, when ingesting PDF documents, the `file_type` returned when ingestion notices were queried, in the `extracted_metadata` object, and from the document details API was `html`. This is no longer the case. The `file_type` returned will now be `pdf`. 

## 26 January 2018
{: #26jan18}

{{site.data.keyword.discoveryshort}} tooling:

- Added the ability to access Korean and Spanish collections to the [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) tile in the tooling. Previously, these collections could only be queried via the API.

## 23 January 2018
{: #23jan18}

- Added the ability to expand the scope of a query - for example, you can expand a query for "car" to include "automobile" and "motor vehicle". In addition, you can replace commonly misspelled terms, for example, you can replace queries for "seabizcuit" with "seabiscuit." Query expansion is implemented with the {{site.data.keyword.discoveryshort}} API. See [Query expansion](/docs/services/discovery?topic=discovery-query-concepts#query-expansion) for details.  

## 15 January 2018
{: #15jan18}

- {{site.data.keyword.discoverynewsfull}} Original was retired from service. It was replaced 31 July 2017 with a new version, named {{site.data.keyword.discoverynewsfull}}. 

## 11 January 2018
{: #11jan18}

- Added full support for Korean. For more information, see [Language support](/docs/services/discovery?topic=discovery-language-support#language-support).

## 15 December 2017
{: #15dec17}

- Released the **Element Classification** enrichment, which parses elements (sentences, lists, tables) in governing documents to classify important categories and types. See [Element classification](/docs/services/discovery?topic=discovery-element-classification#element-classification) for more information. Element Classification is not available for service instances that are subscribed to the **Premium** plan. [Resolved](/docs/services/discovery?topic=discovery-release-notes#5jun18)
- Added Basic language support for Simplified Chinese and Dutch. See [Language Support](/docs/services/discovery?topic=discovery-language-support#language-support) for more information. Currently, Simplified Chinese and Dutch collections must be created with the API.
- Added two new parameters for the Data Crawler: `proxy_host_port` and `read-timeout`. See [Configuring the Data Crawler](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-the-data-crawler) for details.
- The following issues may be seen when ingesting PDF documents: [Resolved](/docs/services/discovery?topic=discovery-release-notes#21feb18)
  - When ingestion notices are queried, the field `file_type` for pdf documents is returned as `html`.
  - The field `file_type` in the `extracted_metadata` object of results for pdf documents is set to `html`.
  - The document details API also returns the field `file_type` for pdf documents as `html`.
- If you are ingesting JSON, mixed-type arrays are not supported.  

{{site.data.keyword.discoveryshort}} tooling:

- Added a visual query builder for the beta version of {{site.data.keyword.discoveryfull}} Knowledge Graph. See [Querying Knowledge Graph using the {{site.data.keyword.discoveryshort}} tooling](/docs/services/discovery?topic=discovery-kg#querying-kg)

## 30 November 2017
{: #30nov17}

- Released the beta version of {{site.data.keyword.discoveryfull}} Knowledge Graph, which provides new end-points for querying entities and relations across documents. This includes context-based searches and relevance ranking. This beta feature is available to **Advanced** plan users only. It is not available on **Dedicated** environments. [Resolved](/docs/services/discovery?topic=discovery-release-notes#8mar18) See [{{site.data.keyword.discoveryfull}} Knowledge Graph](/docs/services/discovery?topic=discovery-kg#kg) for more information.  A statement explaining beta features can be found [here](/docs/services/discovery?topic=discovery-release-notes#beta-features).
  - Known issue in {{site.data.keyword.discoveryfull}} Knowledge Graph: All entity type names and relation type names are converted to uppercase during ingestion. For example, the entity "GeoPoliticalEntity" is converted to "GEOPOLITICALENTITY," and the relation "partOf" is converted to "PARTOF." [Resolved](/docs/services/discovery?topic=discovery-release-notes#5mar18)
- Released [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) in two additional languages: Korean (`collection_id`: `news-ko`) and Spanish (`collection_id`: `news-es`). {{site.data.keyword.discoverynewsfull}} Korean and Spanish are available for use via the API-only; for information about querying a collection via the API, see [API Reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window} [Resolved](/docs/services/discovery?topic=discovery-release-notes#26jan18). {{site.data.keyword.discoverynewsfull}} English now has the `collection_id` of `news-en`. Formerly, the `collection_id` was `news` - if you have been using the former `collection_id`, it will continue to work, however, you may want to switch to the new `collection_id` for new projects.
- Query results return a `score` value, which indicates the relative relevancy between query results. Starting 30 November 2017, the way that `score` is calculated changed. The `score` value should only be used to rank documents in a single search, not across searches or sessions. If you have trained a collection, a `score` value is returned in the results of a natural language query. Since the `score` indicates the relative relevancy between query results, it should not be used as a threshold. Instead, use the `confidence`, which indicates the relevance of the result as compared to the trained model, to set thresholds. See [Confidence scores](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence) for more information on setting thresholds.
- Beginning with this release, Passage retrieval detects sentence boundaries - it attempts to return passages that start at the beginning of a sentence and stop at the end. Previously, many passages would begin or end somewhere mid-sentence. See [Passages](/docs/services/discovery?topic=discovery-query-parameters#passages) for more information about Passage retrieval.

## 15 November 2017
{: #15nov17}

{{site.data.keyword.discoveryshort}} tooling:

- Added the [Relation Extraction](/docs/services/discovery?topic=discovery-configservice#relation-extraction) enrichment, which includes the option to incorporate a custom relation model created with {{site.data.keyword.knowledgestudiofull}}.
- The [Entity Extraction](/docs/services/discovery?topic=discovery-configservice#entity-extraction) enrichment {{site.data.keyword.discoveryshort}} tooling now includes the option to incorporate a custom entity model created with {{site.data.keyword.knowledgestudiofull}}.
- The option to create a Japanese collection was removed from the {{site.data.keyword.discoveryshort}} tooling, however, the option to create a Japanese collection using the {{site.data.keyword.discoveryshort}} API remains.
- {{site.data.keyword.discoveryshort}} Tooling now supports syndicated environments.

## 10 November 2017
{: #10nov17}

{{site.data.keyword.discoveryshort}} tooling:

- Added additional options for Passage retrieval to the {{site.data.keyword.discoveryshort}} tooling. When querying, you can now specify the fields you would like the passages to be returned from, the number of passages to return, and the maximum character count for each passage. See [Passages](/docs/services/discovery?topic=discovery-query-parameters#passages) for limits, minimums, and maximums.

## 8 November 2017
{: #8nov17}

The version string for all API calls has changed to `2017-11-07` from `2017-10-16`. This version:
- Moved the `score` in each query result to a new object named `result_metadata`.
- If the collection queried was trained, and the query is a natural language query, `result_metadata` will include a `confidence` field that displays the confidence score for that result. See [Confidence scores](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence) for details.
- Fields that include whitespaces (for example: `body.additional reading`) will be filtered out during ingestion. The `notices` description will read `The field 'additional reading' is invalid: whitespace, '.', '#' and ',' are invalid in a field name`.
- The field `result_metadata` will be filtered out during ingestion.

## 16 October 2017
{: #16oct17}

- The version string for all API calls has changed to `2017-10-16` from `2017-09-01`. This version deprecates support for uploading new documents into existing collections enriched with {{site.data.keyword.alchemylanguageshort}} enrichments, and for creating new collections and enriching them with {{site.data.keyword.alchemylanguageshort}} enrichments. Existing collections enriched with {{site.data.keyword.alchemylanguageshort}} should be migrated to {{site.data.keyword.nlushort}} enrichments as soon as possible. The {{site.data.keyword.discoveryshort}} tooling also uses the `2017-10-16` version, see below for more information.

{{site.data.keyword.discoveryshort}} tooling:

- The {{site.data.keyword.discoveryshort}} tooling uses the `2017-10-16` API version string, so if you are using the tooling, you will no longer be able to upload documents into existing {{site.data.keyword.alchemylanguageshort}} collections or create new collections enriched with {{site.data.keyword.alchemylanguageshort}} enrichments after `2017-10-16`.  If you want to continue using the {{site.data.keyword.discoveryshort}} tooling for enriching collections, migrate your collections to {{site.data.keyword.nlushort}} first.
- The **Data schema explorer** displays sample queries for several enrichments in the {{site.data.keyword.discoverynewsfull}} collection. It also now has a **Show more values** link that will display additional example values for that enrichment in {{site.data.keyword.discoverynewsfull}}.
- Multiple productivity enhancements, including combining the collection statistics, errors and warnings, and data insights on the **Manage data** screen.
- A message was added that displays an alert when documents are finished processing.

## 9 October 2017
{: #9oct17}

- A new aggregation metric `unique_count` is available in the API. It will return a count of the unique instances of the specified field in a collection. See [unique_count](/docs/services/discovery?topic=discovery-query-aggregations#unique_count) for more information.

{{site.data.keyword.discoveryshort}} tooling:

- Histogram and Timeslice aggregations are now supported in the **Visual Query Builder**. You also have the option to turn on anomaly detection for Timeslice queries.
- The **Data schema explorer** displays sample queries for the enrichment chosen. It also now has a **Show more values" link that will display additional example values for that enrichment.
- A hamburger menu has been added to make it faster to navigate the **Manage data**, **View data schema**, and **Build queries** screens.

### 3 October 2017
{: #3oct17}

- Document segmentation is now available. See [Splitting documents with document segmentation](/docs/services/discovery?topic=discovery-configservice#doc-segmentation).

### 29 September 2017
{: #29sept17}

- {{site.data.keyword.discoveryshort}} launched in the `Germany` location 29 September, 2017. In order to comply with EU data regulations, AlchemyLanguage enrichments are not supported in this location.
- Known issue: Query fields cannot contain whitespaces.  When writing a query in {{site.data.keyword.discoveryshort}}, if any query field contains whitespace (for example, `body.additional reading`), you will receive a `400: Invalid query syntax error`. [Resolved](/docs/services/discovery?topic=discovery-release-notes#8nov17)

### 25 September 2017
{: #25sept17}

- A Premium pricing plan is now available. For more information, see [{{site.data.keyword.discoveryshort}} pricing plans](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans).
- The ability to query, list fields, and query notices across collections within the same environment has been added. See [Querying multiple collections](/docs/services/discovery?topic=discovery-query-concepts#multiple-collections) for details.
- Language support information for {{site.data.keyword.discoveryshort}} is available at [Language support](/docs/services/discovery?topic=discovery-language-support#language-support)

{{site.data.keyword.discoveryshort}} tooling:
- The Visual Query Builder moved from beta status to GA status. Filter, Timeslice, and Histogram aggregations are not currently supported with the Visual Query Builder. Click **Include analysis of your results**, then **Edit in Query Language** on the **Build queries** screen to write those aggregations.
- Added the beta capability to deduplicate on {{site.data.keyword.discoverynewsfull}} queries.
- In addition to English, German, and Spanish language collections, you can now create Arabic, French, Italian, Korean, Japanese, and Brazilian Portuguese collections.
- Known issue: {{site.data.keyword.discoveryshort}} Tooling does not support syndicated environments. [Resolved](/docs/services/discovery?topic=discovery-release-notes#15nov17)

### 14 September 2017
{: #14sept17}

{{site.data.keyword.discoveryshort}} tooling:

- Added the Data Schema Explorer, which displays the fields and values in your transformed documents. This information can be used to understand the data structure of your collection before building queries using the Discovery Query Language. The data schema can be viewed two ways: by document (Document view), or by field (Collection view). To access the Data Schema Explorer: on the **My Data Insights** screen, click the **View data schema** button, or click the **View Data Schema** icon on the left.

### 6 September 2017
{: #6sept17}

- Added the beta ability to deduplicate documents returned from your query. This beta feature works for both private and Watson Discovery News collections. See [Excluding duplicate documents from query results](/docs/services/discovery?topic=discovery-query-parameters#deduplication) for details.

Document deduplication is currently supported only as a beta capability. See the statement regarding betas at the top of this document for more information.

### 31 August 2017
{: #31aug17}

- The version string for all API calls has changed to `2017-09-01` from `2017-08-01`. This version includes updates that will filter out the following invalid JSON fields during preview and ingestion so that only valid JSON fields are ingested. Update your version string to `2017-09-01` to avoid conflicts and possible errors.

   - `id`, `score`, and `highlight` at the top level (You can continue to add documents to your collection using document IDs with the `add a document` function. See the [API Reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#add-a-document){: new_window} for details.
   - `_` prefixed field names at the top level (as a result, when querying for a document by ID, you can query for `id` instead of `_id`.)
   - `#` and `,` in the field name
   - `+` and `-` prefixed field names
   - `"` `"` empty values for a field name

**Note:** If your JSON documents include these characters in the field names, or `id`, `score`, and `highlight` at the top level, you need to remove them before adding the documents to your collection, or those fields will be empty. You can create a custom configuration and normalize your JSON before adding documents to your collection to avoid this issue. See [Custom Configuration](/docs/services/discovery?topic=discovery-configservice#custom-configuration).  In addition, documents that include the punctuation characters `?`, `:`, or `#` in the file name will cause errors at ingestion time. Rename any documents that include these characters before ingesting them.

- The retrieval methods for `natural_language_query` have been updated to improve the relevance of results by matching words with related semantics. This update only affects collections that have not had relevance training. If you are using `natural_language_query` and have not conducted relevance training, you may see improvement in the order of results returned.

{{site.data.keyword.discoveryshort}} tooling:

- Changes to the query builder to make it easier to toggle between the Discovery Query Language and Natural Language query options, as well as among query, filter, and aggregation.


### 25 August 2017
{: #25aug17}

- The `passages` array now includes `field`, `start_offset`, and `end _offset`. `field` is the name of the field the passage was extracted from. `start_offset` is the starting character of the passage text within the field. `end_offset` is the ending character of the passage text within the field.

{{site.data.keyword.discoveryshort}} tooling:
This query building enhancement can be found on the **Build queries** screen.

-  Added the beta ability to write queries in the {{site.data.keyword.discoveryshort}} Query Language with a visual builder. Click **Build in visual mode** in the **Search for documents** and **Limit which documents you query** sections to try it out.  As you build your query visually, it will display in the **{{site.data.keyword.discoveryshort}} Query Language** below it.

   The visual query builder is currently supported only as a beta capability. See the statement regarding betas at the top of this document for more information.

### 18 August 2017
{: #18aug17}

{{site.data.keyword.discoveryshort}} tooling:

- Added support for nested aggregations and conditions to the beta visual aggregation builder introduced [11 August 2017](/docs/services/discovery?topic=discovery-release-notes#11aug17). There is a limit of 3 conditions per aggregation row.

   The visual aggregation builder is currently supported only as a beta capability. See the statement regarding betas at the top of this document for more information.

### 11 August 2017
{: #11aug17}

{{site.data.keyword.discoveryshort}} tooling:

Both features are query building enhancements and can be found on the **Build queries** screen.

- Added the option to select a query from a set of pre-built sample queries and aggregations. Click **Use a sample query** at the top right to access the list. If you are querying a private data collection, the samples use `top entities`, `categories`, etc. found in your collection. These queries can be used as a starting point for writing your own queries. Sample queries are available for both {{site.data.keyword.discoverynewsfull}} and private collections.

-  Added the beta ability to write aggregations with a visual builder. Click **Build in visual mode** above the **Write an aggregation query using the {{site.data.keyword.discoveryshort}} Query Language** field to try it out.  As you build your aggregation visually, the query will display in the **{{site.data.keyword.discoveryshort}} Query Language** below it.  

   The visual aggregation builder is currently supported only as a beta capability. See the statement regarding betas at the top of this document for more information.

### 31 July 2017
{: #31jul17}

- A new version of {{site.data.keyword.discoverynewsfull}} was released. The original version has been renamed {{site.data.keyword.discoverynewsfull}} Original and has been retired with a removal from service date of **15, January 2018**.
  **Note:** If you have created a new instance of {{site.data.keyword.discoveryshort}}, you will only have access to the new version of {{site.data.keyword.discoverynewsfull}}.

- A new pricing plan for {{site.data.keyword.discoveryfull}} was released. See [{{site.data.keyword.discoveryshort}} pricing plans](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans) for details.

- The version string for all API calls has changed to `2017-08-01` from `2017-07-19`. This version includes updates for the new pricing plan and the new version of Watson Discovery News. Update the version string to avoid conflicts and possible errors.

### 19 July 2017
{: #19jul17}

 - As part of the pricing change that has been announced for August 1st 2017, users that are currently on the deprecated **30 day free trial** plan will be automatically migrated to the **Lite** plan. As a result of this transition, existing users may have met or exceeded the lite plan limit on documents _(2000)_, storage _(200Mb)_, or number of collections _(2)_. If you have exceeded the limit of the **Lite** plan, you will not be able to add any additional content into the service but you can still query collections. You can view the current status of all these limits by using the {{site.data.keyword.discoveryshort}} tooling or API. To be able to resume adding content to the {{site.data.keyword.discoveryshort}} instance, you must do one of the following:
   - remove collections and/or documents so that limits of the **Lite** plan are not exceeded.
     Documents can be deleted either individually through the API using the [delete-doc](https://{DomainName}/apidocs/discovery#delete-a-document) method, or whole collections can be deleted using the Tooling or API using the [delete-collection](https://{DomainName}/apidocs/discovery#delete-a-collection) method
   - upgrade your plan to a level that meets your storage needs.
 - Customers with size **`1`** **`2`** or **`3`** environments will be automatically migrated to the **Advanced** plan.

### 17 July 2017
{: #17jul17}

 - The following capabilities have been moved from beta status to GA status:

   - Relevancy training
   - Natural language query
   - Highlighting

 - As of this release, {{site.data.keyword.discoveryfull}} is changing its enrichment mechanism from {{site.data.keyword.alchemylanguageshort}} to {{site.data.keyword.nlushort}}. {{site.data.keyword.alchemylanguageshort}} is in the process of being deprecated, you should start using {{site.data.keyword.nlushort}} as soon as possible.
   **Note:** When integrating with Watson Knowledge Studio, the {{site.data.keyword.alchemylanguageshort}} enrichment configuration must be still used. See [Integrating with {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-with-wks) for details.

 - The version string for all API calls has been changed to `2017-07-19` from `2017-06-25`. This version enables a NLU default config on collection creation. You should still be able to enrich with {{site.data.keyword.alchemylanguageshort}} in previous versions.

    The default configuration has been updated to use {{site.data.keyword.nlushort}}. You should update the version string as soon as possible to avoid conflicts and possible errors.

 - Discovery Tooling:

    The Insight Cards for collections enriched with {{site.data.keyword.alchemylanguageshort}} enrichments will no longer update automatically. You must migrate your collection to {{site.data.keyword.nlushort}} Enrichments for the insight cards to update.

    If you created a collection prior to **18 July, 2017** and applied the **Default Configuration**, that collection was enriched with the {{site.data.keyword.alchemylanguageshort}} enrichments. If you apply the **Default Configuration** to a collection after this date, the {{site.data.keyword.nlushort}} enrichments will be used (the configuration name will switch to **Default Configuration with NLU** in the tooling). Since {{site.data.keyword.alchemylanguageshort}} enrichments are being deprecated, they should not be used with new collections.

### 30 June 2017
{: #30jun17}

 -  The entity normalization capability introduced as a beta feature on 5 May 2017 has been moved to GA status. 

### 23 June 2017
{: #23jun17}

 - The version string for all API calls has changed to `2017-06-25` from `2016-12-01`. The new version string enables enrichments in German (`de`) or Spanish (`es`) if the language of a collection is set to one of those languages. Previously, all enrichments were performed in English regardless of a collection's language setting.

    If you do not use enrichments in non-English languages, you can continue to use the `2016-12-01` version string. However, you should update the version string as soon as possible to avoid potential future conflicts.

 - Anomaly detection is now available as part of `timeslice` aggregations as a GA capability. See [Timeslice anomaly detection](/docs/services/discovery?topic=discovery-query-aggregations#anomaly-detection) for details.

 - Discovery Tooling:

   - Added the beta ability to improve the relevancy of query results using the Discovery tooling (relevancy tooling). See [Improving the relevance of your query results with the Discovery tooling](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling).

### 19 June 2017
{: #19jun17}

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
{: #5jun17}

 - Watson Discovery News queries now display only the first 150 words of each article in the `text` and `alchemyapi_text` JSON fields. The `blekko.snippet` field will display only the first sentence of the snippet array.

### 30 May 2017
{: #30may17}

 - The `passages` parameter on the query API has been moved from beta to GA status.

### 25 May 2017
{: #25may17}

 - Discovery Tooling: query field highlighting was added in this release. This feature adds yellow highlighting to field names in the JSON of the Results pane. All fields that are queried or filtered on are highlighted for each result even if the content of the field does not match the query. Any fields used in aggregations are also highlighted in the query results, but only the first aggregation operation is highlighted.

### 10 May 2017
{: #10may17}

 - The `query` and `notices` methods now support the `highlight` parameter. The parameter is a boolean. When you run a query and specified `highlight` as `true`, the service returns output that includes a new `highlight` field in which words that match the query are wrapped in HTML `*` (emphasis) tags. See the [Query parameters](/docs/services/discovery?topic=discovery-query-parameters#highlight) for details.

 - It is possible for the deletion of an environment to complete only partially, resulting in a situation in which a new environment cannot be created because only a single environment per service instance is permitted. If you attempt to delete and then create an environment but see either operation stuck in the `pending` state, it is likely you have encountered this problem. To work around it, re-run the deletion operation to complete it, then create the new environment.

### 8 May 2017
{: #8may17}

 - Updated the emotion tone score model to improve precision on emotion analysis (`docEmotion`) enrichments. The training dataset was expanded and feature engineering was altered and as a result, the model has higher precision on the benchmark dataset.

### 5 May 2017
{: #5may17}

 - Entity normalization is now available for use with the Discovery service that use a custom model generated by Watson Knowledge Studio. Entity normalization inserts normalized (canonical) names for different references to the same person or object in the source document. 

     **Note:** Entity normalization is currently supported only as a beta capability. See the statement regarding betas at the top of this document for more information. [Resolved](/docs/services/discovery?topic=discovery-release-notes#30jun17)

{{site.data.keyword.discoveryshort}} tooling:

 - The Tooling error log is no longer limited to a maximum of eight (8) pages of results. The error log still displays the document ID if the document name is not available.

 - Configuration names are limited to 50 characters and must consist of the characters `[a-zA-Z0-9-_]`. 

 - The `passages` parameter previously available only through the API is now available through the Tooling as well as the API.

### 25 April 2017
{: #25apr17}

  - The service now enables you to provide *training data* to improve the accuracy of your query results. When you provide a Discovery instance with training data, the service uses advanced Watson algorithms to determine the most relevant results. As you add more training data, the service instance becomes more accurate and sophisticated in the results it returns. See [Improving the relevance of your query results](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api) and the [API Reference ](https://{DomainName}/apidocs/discovery#list-training-data) for information.

  - The API now supports the `natural_language_query` parameter as a beta release. This parameter enables you to specify a query in natural language instead of in the Discovery service's query language. See the [Query your collection](https://{DomainName}/apidocs/discovery#query-your-collection) method in the API reference for information.

  - Documentation updates and errata corrections.

### 14 April 2017
{: #14apr17}

Enhancements have been added to the query API (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`). See the [Query your collection](https://{DomainName}/apidocs/discovery#query-your-collection) method in the API reference for information.

  - The query API now supports the `passages` parameter. If the parameter is set to `true`, the query returns a set of the most relevant passages from the documents in your collection. The passages are generated by sophisticated Watson algorithms to determine the best passages of text from all of the documents returned by the query. This enables you to find information and context more precisely. See the [Query your collection](https://{DomainName}/apidocs/discovery#query-your-collection) method in the API reference for information.

    - Specifying `passages=true` in your query can reduce performance as a result of increased processing to extract passages. With larger environments, the performance impact can be lessened.

    - The `passages` parameter is supported only on private collections. It is not supported in the Watson Discovery News collection.

    - The `passages` parameter currently returns a maximum of 10 results. The number of returned results cannot be changed. [Update](/docs/services/discovery?topic=discovery-query-parameters#passages_count)

    - The `passages` parameter returns a maximum of three (3) passages from any given document in the collection. If a document contains more than three additional relevant passages, the parameter does not return them.

### 7 April 2017
{: #7apr17}

- The query API (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`) now supports the `sort` parameter, which enables you to specify a comma-separated list of fields in the document to sort on. See the [Query your collection ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window} method in the API reference for information.
- The `timeslice` parameter for query aggregations now correctly handles dates in UNIX epoch format. See [Query reference](/docs/services/discovery?topic=discovery-query-reference#aggregations) for information about aggregations and the `timeslice` parameter.
- Improvements to error messages.
- Updates to the service's Java SDK. See the [API Reference](https://{DomainName}/apidocs/discovery?language=java) for details.
- The following limitations to the use of wildcards in queries are now fixed and work correctly:

  - Only one wildcard worked in any given query. For example, `query-month:*ctober` worked, but `query-month:*ctobe*` generated a parsing error.
  - Wildcards did not work with queries that contained capital letters. For example, given the key/field pair ``{"borrower": "GOVERNMENT OF INDIA"}``, `query-borrower:*ndia` returned results but `query-borrower:*NDIA` did not.

**Note:** Wildcards are not necessary within phrases in queries. For example, given the key/field pair `{"borrower": "GOVERNMENT OF TIMOR"}`, `query-borrower:"GOVERNMENT OF TIMOR"` returns results but `query-borrower:"GOVERNMENT OF TI*OR"` will not. Using a wildcard is not applicable within phrases because all of the characters within the quotation marks (`"`) of a phrase are escaped.

### 24 March 2017
{: #24mar17}

- Added filtering to the "My data insights" screen in the Discovery tooling

### 15 March 2017
{: #15mar17}

The following known issues have been discovered.

-  All fields that are ingested from HTML, PDF, and Word documents are typed as **string**. JSON fields and calculated fields, such as sentiment score, are typed as defined. [Update](/docs/services/discovery?topic=discovery-addcontent#adding-content-with-the-api-or-tooling)
- The `preview` operation does not currently check for nested JSON arrays within a submitted JSON document. The service does not currently support nested JSON arrays, so a document with nested arrays can successfully pass the `preview` operation but fail upon an ingestion attempt. See [Can I upload JSON arrays?](/docs/services/discovery?topic=discovery-faqs#array)
- If you encounter ingestion errors with the message `unsupported text language`, update your configuration with the `"language": "english"` enrichment option to force all text to be interpreted as English, as shown in the following example. 
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
{: #8mar17}

 - Optimized the back end, including the addition of new timeouts, to improve overall performance.
 - Fixed a bug that caused the environment status of free (`0`-sized) environments to report a status of `pending` regardless of the real status.
 - The only national language currently supported by {{site.data.keyword.discoveryshort}} is U.S. English (`en_US`). [Update](/docs/services/discovery?topic=discovery-language-support#language-support)

### 3 March 2017
{: #3mar17}

- Added the "My data insights" screen to the Discovery tooling.

### 26 February 2017
{: #26feb17}

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
{: #16feb17}

-  You can now use CSS selectors to select JSON fields that you can then apply enrichments to. See [Using CSS selectors to extract fields](/docs/services/discovery?topic=discovery-configservice#using-css) for information.
-  You can now increase the size of an environment by passing a new `size: X` parameter to the [update-environment method](https://{DomainName}/apidocs/discovery#update-an-environment), where `X` is an integer between 0 and 3. See the [create-environment method](https://{DomainName}/apidocs/discovery#create-an-environment) for information about environment sizes and attributes. [Update](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

    **Note:** You cannot reduce the size of an existing environment. If you want to reduce the size of your environment, contact {{site.data.keyword.IBM}} support for assistance.

-  A new query operator is available. The `::!` operator has been added as a unary not-equals operator. For example, you can now run `query=field::!value` (not equals). Previously the only exclusionary operator was `:!` for the not-contains operator (for example, `query=field:!value`).

The following bugs have been fixed.

-  Applied security updates.
-  Improved status messages for search alerts.

### 1 February 2017
{: #1feb17}

The following notes apply specifically to the Data Crawler 1.3.0 release.
[Update](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)

-   The Data Crawler records the `document_id` values used to upload documents, and the status of the upload. Conversion notices are not persisted outside of the log. There is not presently a tool to interact with that data, but such tools are expected to be developed as time permits. The data is accessible via H2 database, which could be configured to use a remote DBMS.

### 16 January 2017
{: #16jan17}

The following notes apply specifically to the Data Crawler 1.2.5 release.
[Update](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)

-  The Data Crawler can optionally poll for document status immediately after uploading a file. This check is a part of the Crawler's concept of "uploading a document", so when this check is enabled, it is virtually impossible for the Crawler to upload concurrently more documents than what {{site.data.keyword.discoveryshort}} can process concurrently for the user.

    A side effect of the `check_for_completion` feature is that the Crawler also can expose to the user why a document failed, when it failed. Any notices attached to a document that was successfully uploaded, but failed to process, are displayed in the Crawler log. The notices are not exported to a processable file, but IBM would welcome a feature suggestion for that.

### 5 January 2017
{: #5jan17}

The following notes describe issues that were identified after the GA release on 15 December 2016.

[Update: API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery){: new_window}

-   If you add a document by using the `POST /v1/environments/{environment_id}/collections/{collection_id}/documents`
    or `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]` call, the call returns a document ID and the **processing** status. If you then query the document by using the `GET /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]` call, the status remains at **processing** until ingestion is completed, at which point the status changes to **available**.

    If you **update** an existing document by using the `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]` call, the corresponding **GET** call returns the `available` status even if the service has not yet fully processed the updated document. The `available` status can refer to either the original document or the updated document. Unless the update operation returns an error, there is not currently a way to determine the status of the updated document.

    You can work around this by waiting up to 10 minutes after submitting a document update before attempting to query the updated content.

### General Availability release, 15 December 2016
{: #15dec16}

The following notes apply to the General Availability (GA) release of {{site.data.keyword.discoveryfull}}.

#### General notes
{: #rn-general-notes}

[Update: Adding content](/docs/services/discovery?topic=discovery-addcontent#addcontent)

See [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery){: new_window} for current API version.

[Update: Integrating with {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-with-wks).

-   You cannot currently specify the data type of fields. All fields are indexed as text (data type **string**). 
-   If you use the API to work with the service, you must specify the API version with each call. The current API version is **2016-12-01**. 

    **Note:** The specific version is not enforced in the GA release, but it still must be listed to enable compatibility with future releases.

-   You can use the service with a custom model created with {{site.data.keyword.knowledgestudiofull}}. The custom model can be used to enrich ingested documents. You must use the API to integrate the custom model with {{site.data.keyword.discoveryshort}}; you cannot perform the integration by using the tooling.

#### Data management
{: #rn-data}

[Update](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

-   Search indexes are not encrypted.
-   Backup and restore functions are not user controllable.

#### Environments
{: #rn-environments}

[Update](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

-   You can create only one environment per service instance to upload your own data.
-   {{site.data.keyword.discoveryshort}} is located in a single availability zone (US South).
-   Dedicated and premium plans are not available at the current time.

#### Environment sizing
{: #rn-sizing}

[Update](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

-   You can choose an environment size only when creating a new environment. The ability to resize an environment is not currently available to users.
-   Choosing an environment size with more RAM increases performance.
-   There are currently no prescriptive sizing recommendations available for specific use cases.
-   Custom sizing for {{site.data.keyword.knowledgestudiofull}} models is not self-serve. Contact your {{site.data.keyword.IBM}} representative for more information.

#### Ingestion limitations
{: #rn-ingestion}

[Update](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

-   The ingestion rate is currently limited to 100 concurrent document ingestion operations. An application that submits documents to the service for ingestion needs to respect HTTP 429 errors and throttle down ingestion requests accordingly.
-   {{site.data.keyword.alchemylanguageshort}} enrichments are limited to the first 50 kB per field.
-   Enrichments from {{site.data.keyword.knowledgestudiofull}} custom models are not limited, but split documents into 10-kB chunks. No relationships are annotated across chunk boundaries.

#### Query limitations
{: #rn-query}

[Update](/docs/services/discovery?topic=discovery-query-concepts#query-concepts)

-   Excessive query load can cause the search-index process to restart automatically.
-   Applications that issue queries must enforce reasonable limits on the number of concurrent queries.

### Known issues
{: #rn-issues}

[Update: API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery){: new_window}

[Update: tooling](/docs/services/discovery?topic=discovery-getting-started#getting-started)

[Update: Data Crawler](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)

[Update: Enrichments](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)

[Update: Adding content](/docs/services/discovery?topic=discovery-addcontent#addcontent)

-   You cannot delete a document by using the tooling. If you need to delete a document, you must use the API's [Delete a document](https://{DomainName}/apidocs/discovery#delete-a-document) method as described in the API reference.

-   The API does not currently support getting a list of notices (warnings and error) that are generated during document ingestion. The tooling is therefore unable to show a list of ingestion notices, and there is no easy way to determine which, if any, documents crawled by the Data Crawler failed to be ingested. 
-   Document status information is not always accurate.
    -   If an ingestion operation takes longer than the configured timeout of 10 minutes, the service reports that the document is not known to the service until the ingestion operation completes. After the operation completes, the document status is available and accurate.
    -   Documents that are successfully indexed but generated errors can have a status of **failed** for a short period of time until the document has been fully committed to the index. After the document has been committed to the index, the listed status is accurate.
-   You cannot use the tooling to replace a specific document. If you attempt to do so, the second document is uploaded as a separate document. If you are using the API and know the ID of the document you want to replace, you can do so; see [Update a document](https://{DomainName}/apidocs/discovery#update-a-document) in the API reference. If you are using the Data Crawler, uploading an updated document from the same URL as a previous document replaces the original document.
-   If you are using the tooling to edit the enrichments in your configuration, you can edit only enrichments used for extraction. If you want to add or edit other enrichments (for example, custom enrichments from a {{site.data.keyword.knowledgestudiofull}} model), you must use the API. See the [Update a configuration](https://{DomainName}/apidocs/discovery#update-a-configuration) method in the API reference for information.
-   The following notes apply specifically to the Data Crawler. 
    -   The Data Crawler retries uploads if it encounters an upload failure.
    -   The Data Crawler is unable to retry documents that uploaded successfully but failed to be converted or indexed.
    -   The Data Crawler does not have a function to check downstream status and attempt to re-upload URLs that failed downstream.
    -   There is no easy way to determine which documents have been ingested by the Data Crawler. For example, if you run the Data Crawler against a set of 500 documents, the Data Crawler might report failures submitting 65 documents with a total collection of 212 documents. The status of the remaining 223 documents is undetermined.

        A workaround is available, but it is complicated and involves invoking the API directly. Contact {{site.data.keyword.IBM}} support for assistance.
-   The Java, Python, and Node.js SDKs for {{site.data.keyword.discoveryshort}} do not provide all of the functionality provided by the default REST (cURL) API. Not all cURL methods have an equivalent method in the non-cURL SDKs, and not all non-cURL methods provide all of the same features that their cURL equivalents have. In other words, the Java, Python, and Node.js SDKs currently provide only a subset of the cURL API's capabilities.
-   If you use the Word converter, matching on headings by using the `style` key is much more accurate and efficient than it by using the `level` key.
