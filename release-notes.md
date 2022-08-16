---

copyright:
  years: 2015, 2022
lastupdated: "2022-07-26"
keywords:  discovery release notes,discovery for IBM cloud release notes,what's new,new features,change log,changelog
subcollection: discovery
content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for {{site.data.keyword.discoveryshort}}
{: #release-notes}

The release notes provide information about updates and improvements to {{site.data.keyword.discoveryfull}} since the previous release.
{: shortdesc}

## Service API Versioning
{: #apiversioning}

API requests require a version parameter that takes a date in the format `version=YYYY-MM-DD`. Whenever we change the API in a backwards-incompatible way, we release a new minor version of the API.

Send the version parameter with every API request. The service uses the API version for the date you specify, or the most recent version before that date. Don't default to the current date. Instead, specify a date that matches a version that is compatible with your app, and don't change it until your app is ready for a later version.

The current version is `2019-04-30`.

## Discovery v1 deprecation announcement
{: #discovery-v1-deprecation-12july2022}

Watson Discovery v1 is being deprecated. Existing clients who use Watson Discovery v1 are asked to migrate to Watson Discovery v2 before the end-of-support date of **11 July 2023**. End of Support means that no v1 instance will work on or after 11 July 2023. For more information about migration, see [Getting the most from Discovery](/docs/discovery-data?topic=discovery-data-version-choose){: external}.
{: deprecated}

## 25 January 2022
{: #discovery-26january2022}
{: release-note}

FAQ extraction beta feature is deprecated
:   Support for the FAQ extraction beta feature was removed. The beta feature was available only for Web crawl connectors that were used from Watson Assistant Search skills.  FAQ extraction will stop being supported in v1 {{site.data.keyword.discoveryshort}} service instances on 1 March 2022. As a consequence of the end of FAQ extraction support, the COVID-19 kit data collection will stop being supported also.

Known issue for training. You might encounter the following issue when you try to train your data collection:

-   **Error**: If you are training your collection, you might see the message, `Your query can not be run because you have exceeded the rate limit for your plan. Your current plan limits the number of complex queries you can run simultaneously, so you can fix this by upgrading or reducing the number of queries.`
-   **Cause**: If you have a very small plan (XS or S), you might encounter this problem because your plan limits the number of queries that you can submit at one time. This message might be displayed even when you aren't submitting test queries because the product user interface can send some queries in the background to update the training page.
-   **Solution**: Close the training page or view a different page and then try to submit your query again. As a longer term fix, consider upgrading your plan.

## 11 January 2022
{: #discovery-11january2021}
{: release-note}

Operation limits
:   New limits were applied to long-running operations, such as ingestion. For more information, see [Troubleshooting ingestion issues](/docs/discovery?topic=discovery-addcontent#adding-ts).

## 8 October 2021
{: #discovery-8october2021}
{: release-note}

Deprecated Discovery News
:   The Watson Discovery News feature is deprecated as of 8 October 2021. Existing News collections are available and support continues until 8 October 2022, after which date they will no longer be accessible. The Discovery News collection is not available in Watson Discovery v2 service instances.

## 22 September 2020
{: #discovery-22september2020}
{: release-note}

New beta FAQ extraction
:   Released the beta version of [FAQ extraction](/docs/discovery?topic=discovery-sources#connectwebcrawl). This beta feature is only available if you build a search skill in {{site.data.keyword.conversationshort}} and configure a web crawl. FAQ extraction automatically extracts question-and-answer pairs from your FAQ web pages so that {{site.data.keyword.conversationshort}} returns more precise answers. 

## 12 August 2020
{: #discovery-12august2020}
{: release-note}

Deprecated anomaly detection
:   Anomaly detection is deprecated and no longer available, effective **12 September 2020**. You can no longer apply anomaly detection to a timeslice aggregation.


## 30 July 2020
{: #discovery-30july2020}
{: release-note}

Improved training data limit
:   The maximum number of trained collections has been increased from 24 to 40. For more information, see [Training data requirements](/docs/discovery?topic=discovery-improving-result-relevance-with-the-api#reqs).

## 6 May 2020
{: #discovery-6may2020}
{: release-note}

Deprecated Element Classification
:   The Element Classification enrichment deprecation date announced [6 March 2020](/docs/services/discovery?topic=discovery-release-notes#6mar2020) has been changed. The Element Classification enrichment is deprecated and will no longer be available, effective **10 July 2020**. 


## 6 March 2020
{: #6mar2020}

Change to Element Classification deprecation date
:   The Element Classification enrichment is deprecated and no longer be available, effective **15 May 2020**. Data already in {{site.data.keyword.discoveryshort}} collections enriched with Element Classification is not affected, nor are any other existing queries or operations affected. You can no longer apply the Element Classification enrichment to any new or existing collection.

## 17 January 2020
{: #discovery-17january2020}
{: release-note}

New French language support for Discovery News
:   Released [{{site.data.keyword.discoverynewsfull}}](/docs/discovery?topic=discovery-watson-discovery-news) in one additional language: French (`collection_id`: `news-fr`).

## 12 December 2019
{: #discovery-12december2019}
{: release-note}

Full support for IBM Cloud IAM
:   {{site.data.keyword.discoveryshort}} now supports the full implementation of {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). API keys for Watson services are no longer limited to a single service instance. You can create access policies and API keys that apply to more than one service, and you can grant access between services.
:   To support this change, the API service endpoints use a different domain and include the service instance ID. The pattern is `api.{location}.{offering}.watson.cloud.ibm.com/instances/{instance_id}`.

        Example URL for an instance hosted in the Dallas location: `api.us-south.discovery.watson.cloud.ibm.com/instances/6bbda3b3-d572-45e1-8c54-22d6ed9e52c2`

        The previous public endpoint domain was `watsonplatform.net`.

        For more information about the URLs, see the [API reference](/apidocs/discovery/discovery#service-endpoint){: external}.

        These URLs do not introduce a breaking change. The new URLs work both for your existing service instances and for new instances. The original URLs continue to work on your existing service instances for at least one year (until December 2020). For more information about IAM, see [Authenticating to Watson services](/docs/watson?topic=watson-iam).

New network and data security features
:   Support for data encryption with customer-managed keys - Users of new premium and dedicated instances can integrate {{site.data.keyword.keymanagementservicefull}} with {{site.data.keyword.discoveryshort}} to encrypt their data and manage encryption keys. For more information, see [Protecting sensitive information in your Watson service](/docs/discovery?topic=watson-keyservice).
:   Support for private network endpoints - Users of Premium plans can create private network endpoints to connect to {{site.data.keyword.discoveryshort}} over a private network. Connections to private network endpoints do not require public internet access. For more information, see [Public and private network endpoints](/docs/discovery?topic=watson-public-private-endpoints).

## 6 December 2019
{: #discovery-6december2019}
{: release-note}

Known issue for Lite plan crawl status
:   If your Lite plan reaches the document limit of the environment, any running crawls do not progress any further. The displayed crawl status changes to `not_configured`.

## 11 October 2019
{: #discovery-11october2019}
{: release-note}

New Seoul location now available
:   You can now create {{site.data.keyword.discoveryshort}} instances in the Seoul data center. Like all locations, the {{site.data.keyword.cloud}} Seoul location (seo) uses token-based Identity and Access Management (IAM) authentication. The following features are not available in the Seoul data center: {{site.data.keyword.discoverynewsfull}}, connectors, custom stopwords, and Japanese tokenization dictionaries.

## 30 September 2019
{: #discovery-30september2019}
{: release-note}

Deprecated Knowledge Graph Beta APIs and Knowledge Graph relationship query
:   As announced [3 September 2019](/docs/discovery?topic=discovery-release-notes#3sept19), the {{site.data.keyword.discoveryfull}} Knowledge Graph Beta APIs (Knowledge graph entity query `/v1/environments/{environment_id}/collections/{collection_id}/query_entities` and Knowledge Graph relationship query `/v1/environments/{environment_id}/collections/{collection_id}/query_relations`) are no longer accessible.

Deprecated Preview API
:   As announced [4 June 2019](/docs/discovery?topic=discovery-release-notes#4jun19), the Preview API is deprecated and is no longer available.

## 3 September 2019
{: #discovery-3september2019}
{: release-note}

Change to Knowledge Graph Beta APIs and Knowledge Graph relationship query
:   {{site.data.keyword.discoveryfull}} Knowledge Graph Beta APIs (Knowledge graph entity query `/v1/environments/{environment_id}/collections/{collection_id}/query_entities` and Knowledge Graph relationship query `/v1/environments/{environment_id}/collections/{collection_id}/query_relations`) are no longer be accessible, as of **30 September 2019**. Data already in {{site.data.keyword.discoveryshort}} collections is not affected, nor are any other existing queries or operations affected. You can find the documentation for Knowledge Graph in the [{{site.data.keyword.discoveryshort}} archives](/docs/discovery?topic=discovery-discovery-archives#kg) until 30 September 2019.

## 29 August 2019
{: #discovery-29august2019}
{: release-note}
	
Updated Web crawl connector status
:   The Web crawl connector moved from beta status to GA status. See [Web crawl](/docs/discovery?topic=discovery-sources#connectwebcrawl) for more information about this connector.

## 4 June 2019
{: #discovery-4june2019}
{: release-note}

Change to Preview API
:   The Preview API is deprecated and is no longer available, effective **30 September 2019**.

## 30 April 2019
{: #discovery-30april2019}
{: release-note}

New management of Query expansion and Stopword from Search settings
:   [Query expansion](/docs/discovery?topic=discovery-query-concepts#query-expansion) and [Stopword](/docs/discovery?topic=discovery-query-concepts#stopwords) lists can now be uploaded or deleted using the **Search settings** screen in the {{site.data.keyword.discoveryshort}} tooling. Previously, these lists could only be managed using the API.

Update to version string
:   The version string for all API calls changed to `2019-04-30` from `2019-03-25`.

## 26 April 2019
{: #discovery-26april2019}
{: release-note}

Improved accuracy of scoring algorithms
:   The {{site.data.keyword.discoveryfull}} update announced on [April 2, 2019](/docs/discovery?topic=discovery-release-notes#2apr19) is complete. This upgrade included changes to improve the accuracy of the scoring algorithms used in {{site.data.keyword.discoveryshort}} for ranking documents and passages. It is likely that the changes to your `score` and `confidence` are small, and there might also be some small changes to the ranking order. If your applications make use of the `score` or `confidence` fields directly, it is recommended that you update your applications, as necessary.

New multi-token query expansion support
:   Multi-token query expansion is now supported. See [Query expansion](/docs/discovery?topic=discovery-query-concepts#query-expansion) for more information.

## 17 April 2019
{: #discovery-17april2019}
{: release-note}

Deprecated Data Crawler
:   The Data Crawler is no longer available for download and is no longer supported. See [Connecting to Data Sources](/docs/discovery?topic=discovery-sources) for other connectivity options.

## 2 April 2019
{: #discovery-2april2019}
{: release-note}

Update to scoring algorithms
:   Beginning April 9, 2019, there is an upgrade to {{site.data.keyword.discoveryfull}}. This upgrade includes changes to the scoring algorithms used in {{site.data.keyword.discoveryshort}} for ranking documents and passages. This means score and confidence results might change, following the upgrade. If your applications make use of the `score` or `confidence` fields directly, be prepared to update the application as necessary. See [Upgrading the infrastructure of the {{site.data.keyword.discoveryfull}}](https://www.ibm.com/blogs/cloud-archive/2019/03/announcement-for-the-ibm-watson-discovery-community/){: external} for details.

## 25 March 2019
{: #discovery-25march2019}
{: release-note}

Update to version string
:   The version string for all API calls changed to `2019-03-25` from `2019-01-01`

Improved extraction of title field from HTML documents
:   The `title` field is now extracted from HTML documents as a top-level field during conversion. This `title` field is included in each segment of any documents split, using document segmentation. For an example, see [Splitting documents with document segmentation](/docs/discovery?topic=discovery-configservice#doc-segmentation). This might improve the `confidence` score for query results, and might change the `passages` returned because the `title` might be returned, as part of a passage. Existing collections must be reindexed to extract the `title` field.
:   The {{site.data.keyword.discoveryshort}} tooling does not yet use the current API version: `2019-03-25` (it currently uses `2018-12-03`), so the `title` is not extracted when ingesting HTML documents by uploading or using the Web Crawl connector in the {{site.data.keyword.discoveryshort}} tooling.

New enrichment for arrays
:   Arrays can now be enriched (previously, arrays could not be enriched). When using Smart Document Understanding, this means that you can now enrich both default (for example: `answer`, `author`, `footer`, `header`, `question`, `subtitle`, `table_of_contents`, `text`, and `title`) and custom fields. Previously, you were limited to enriching only the `text` field.

## 21 March 2019
{: #discovery-21march2019}
{: release-note}

Update to visibility of user role credentials
:   From March 21, 2019, you can only see service credential information associated with the role that is assigned to your {{site.data.keyword.cloud_notm}} account. For example, if you assign a `reader` role, any `writer` or higher levels of service credentials are not visible.
:   This change does not affect API access for users or applications with existing service key credentials. Only the viewing of credentials within {{site.data.keyword.cloud_notm}} is affected. For more information about service keys and user roles, see [IAM service API keys](/docs/watson?topic=watson-iam).

## 10 February 2019
{: #discovery-10february2019}
{: release-note}

New option to connect and sync with IBM Cloud Object storage
:   Added the option to connect to and sync with IBM Cloud Object Storage. This data source is not available in Dedicated environments. See [IBM Cloud Object Storage](/docs/discovery?topic=discovery-sources#connectcos) for more information.

## 4 February 2019
{: #discovery-4february2019}
{: release-note}

Updates to Smart Document Understanding
:   [Smart Document Understanding (SDU)](/docs/discovery?topic=discovery-sdu) moved from beta status to GA status. The beta of SDU was announced [January 22, 2019](/docs/discovery?topic=discovery-release-notes#22jan19).  
:   Table annotation remains in beta status. For a statement explaining beta features, see [Beta features](/docs/discovery?topic=discovery-release-notes#beta-features).
:   The `Data settings` button on the upper right is renamed as `Configure data`.
:   Uploading a document is no longer required to access the `Configure data` (formerly `Data settings`) button.
    
## 28 January 2019
{: #discovery-28january2019}
{: release-note}

Deprecated support for Data Crawler
:   Assistance is no longer provided for the Data Crawler if you are using it with a data source supported by the {{site.data.keyword.discoveryshort}} connectors. The {{site.data.keyword.discoveryshort}} connectors support crawling Box, SharePoint, Salesforce, and more. See [Connecting to data sources](/docs/discovery?topic=discovery-sources) for details. It is recommended that the Data Crawler only be used to crawl file shares or databases. In all other cases, use the {{site.data.keyword.discoveryshort}} connector. Another option to upload large numbers of files into {{site.data.keyword.discoveryshort}} is [discovery-files](https://github.com/IBM/discovery-files){: external} on GitHub.

## 22 January 2019
{: #discovery-22january2019}
{: release-note}

New beta Smart Document Understanding
:   Released the beta version of [Smart Document Understanding (SDU)](/docs/discovery?topic=discovery-sdu), a new way to train {{site.data.keyword.discoveryfull}} to extract custom fields in your documents. With Smart Document Understanding, you annotate fields within your documents to train custom conversion models. 
:   The beta SDU editor is only available for new collections that contain supported document types and do not have the Element Classification enrichment applied. Existing private collections use the original configuration method.
:   If you were part of the closed beta for Smart Document Understanding, do not import models created in that beta into this version. Smart Document Understanding is currently not available in Dedicated environments.
:   The SDU editor functions are only available in the {{site.data.keyword.discoveryshort}} tooling. They are not available in the API.

## 15 January 2019
{: #discovery-15january2019}
{: release-note}

Updates to Element Classification enrichment
:   The Element Classification enrichment has updated parties, categories, and attributes in API version `2018-10-15` or later. See [Parsing contracts](/docs/discovery?topic=discovery-contract_parsing) for the updates.
:   The output of the `/v1/element_classification` method now includes the following:
    - The `parties` array now includes an `importance` field that indicates whether the party is a `Primary` party or an `Unknown` (non-primary) party.
    - The `effective_dates`, `contract_amounts`, and `termination_dates` arrays now each include a `confidence_level` field that indicates a value of `High`, `Medium`, or `Low`.
   For more information, see [Classifying elements](/docs/discovery?topic=discovery-output_schema) and [Parsing contracts](/docs/discovery?topic=discovery-contract_parsing).
:   The {{site.data.keyword.discoveryshort}} tooling does not yet use the current API version: `2019-01-01` (it currently uses `2018-12-03`), so you cannot see these new fields in the Element Classification output in the {{site.data.keyword.discoveryshort}} tooling.

## 10 January 2019
{: #discovery-10january2019}
{: release-note}

Known issue for customer-id
:   If you specify a `customer-id`, using the normalization method described in [Specifying a `customer_id`](/docs/discovery?topic=discovery-sources#source_customer_id) and subsequently attempt to delete documents containing that `customer_id`, using the method described in [Deleting labeled data](/docs/discovery?topic=discovery-information-security#deletingdata), the associated source document is not deleted.

## 1 January 2019
{: #discovery-1january2019}
{: release-note}

Update to version string
:   The version string for all API calls changed to `2019-01-01` from `2018-12-03`. This version introduces a new document ingestion status: `pending`. The `pending` status is returned for documents that are accepted but did not yet start processing. Previously, these documents had the status of `processing`. The {{site.data.keyword.discoveryshort}} tooling does not yet use this API version (it currently uses `2018-12-03`), so when you check document status in the {{site.data.keyword.discoveryshort}} tooling, the `pending` status is not returned.

## 21 December 2018
{: #discovery-21december2018}
{: release-note}

New option to connect and sync with Microsoft Sharepoint 2016 On-Premise
:   Added the option to connect to and sync with Microsoft SharePoint 2016 On-Premise. This data source is not available in Dedicated environments. See [SharePoint 2016 On-Premise](/docs/discovery?topic=discovery-sources#connectsp_op) for more information.

New beta Web crawl connector
:   Added the beta version of the Web crawl connector, which can be used connect to, crawl, and sync with websites. This data source is not available in Dedicated environments. See [Web crawl](/docs/discovery?topic=discovery-sources#connectwebcrawl) for more information. For a statement explaining beta features, see [Beta features](/docs/discovery?topic=discovery-release-notes#beta-features).

New data source availability for Premium plan
:   Microsoft SharePoint Online, Salesforce, and Box data sources are now available in Premium environments. They are not available in Dedicated environments.

## 17 December 2018
{: #discovery-17december2018}
{: release-note}

New full support for Italian language
:   Added full support for Italian. For more information, see [Language support](/docs/discovery?topic=discovery-language-support).

## 14 December 2018
{: #discovery-14december2018}
{: release-note}

New London location now available
:   You can now create {{site.data.keyword.discoveryshort}} instances that are hosted in the London data center without syndication. Like all locations, the {{site.data.keyword.cloud}} London location (eu-gb) uses token-based Identity and Access Management (IAM) authentication. All new services instances that you create in this location use IAM authentication.

Update to version string
:   The {{site.data.keyword.discoveryshort}} tooling now uses the API version of `2018-12-03`(it previously used `2018-08-01`).

## 12 December 2018
{: #discovery-12december2018}
{: release-note}

New feature for Stopwords
:   Added the ability to define and upload a custom stopwords list. Custom stopwords are implemented with the {{site.data.keyword.discoveryshort}} API. See [Defining stopwords](/docs/discovery?topic=discovery-query-concepts#stopwords) for details. 

## 3 December 2018
{: #discovery-3december2018}
{: release-note}

New confidence score support
:   For all queries written, using the API version of `2018-12-03` or above, with the exception of filter-only queries, {{site.data.keyword.discoveryshort}} now returns a `confidence` score in the query results set, even if the collection was not trained, using a supervised training method, such as [Relevancy training](/docs/discovery?topic=discovery-improving-result-relevance-with-the-tooling) or [Continuous Relevancy Training](/docs/discovery?topic=discovery-crt). In addition, {{site.data.keyword.discoveryshort}} returns a `document_retrieval_strategy` field that indicates the source of the `confidence` score of `untrained`, `relevancy_training`, or `continuous_relevancy_training`. For more information, see [Confidence scores](/docs/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence).

Update to version string
:   The version string for all API calls changed to `2018-12-03` from `2018-10-15`. The {{site.data.keyword.discoveryshort}} tooling does not yet use this API version (it currently uses `2018-08-01`), so queries written using the {{site.data.keyword.discoveryshort}} tooling does not return a `confidence` score for untrained collections.

## 8 November 2018
{: #discovery-8november2018}
{: release-note}

New Tokyo location now available
:   {{site.data.keyword.discoveryshort}} launched in the `Tokyo` location 8 November 2018. Premium and Dedicated environments are not currently available in `Tokyo`.

## 30 October 2018
{: #discovery-30october2018}
{: release-note}

New IAM support in all regions
:   {{site.data.keyword.discoveryshort}} now supports token-based Identity and Access Management (IAM) authentication in all regions. IAM uses access tokens rather than service credentials for authentication with a service. For more information about using IAM tokens with existing and new applications, see the [17May2018](#discovery-17may2018) release update.

## 25 October 2018
{: #discovery-25october2018}
{: release-note}

Update to Element Classification enrichment schema
:   The schema for the [Element Classification](/docs/discovery?topic=discovery-element-classification) enrichment changed. If you wish to use the updated schema, you must ingest your documents with the API, using the version date of `2018-10-15` or later. The {{site.data.keyword.discoveryshort}} tooling does not yet use this API version (it currently uses `2018-08-01`), so documents ingested, using the {{site.data.keyword.discoveryshort}} tooling, are enriched with the original schema.

## 24 October 2018
{: #discovery-24october2018}
{: release-note}

New highlights to replace queries display from JSON field
:   {{site.data.keyword.discoverynewsfull}} queries display approximately 50 words from each article in the `text` JSON field. These words are now extracted from the highlights, rather than simply displaying the first 50 words of the article. See [highlight](/docs/discovery?topic=discovery-query-parameters#highlight) for an explanation of highlights. Highlights do not need to be explicitly included in your query to enable this behavior.

## 25 September 2018
{: #discovery-25september2018}
{: release-note}

New Continuous Relevancy Training feature
:   Released Continuous Relevancy Training, which uses interactions from users to learn how to surface the most relevant results. It can learn from user behavior automatically, significantly reducing the effort required to improve the relevancy ranking of results.  See [Continuous Relevancy Training](/docs/discovery?topic=discovery-crt) for details.

New API support for longer queries
:   Added API support for performing longer queries. This increases the character limit to 10,000 characters, and makes it possible to increase the number of filters in your queries and perform more complex aggregations. See the POST Query at [API reference](/apidocs/discovery#long-collection-queries){: external} and [API reference](/apidocs/discovery#long-environment-queries){: external} for details.

Improved ability to upgrade to Advanced plan
:   You can now upgrade your Advanced plan using the API. See [Upgrading your plan](/docs/discovery?topic=discovery-upgrading-your-plan#switchadvanced) for details.

New Element Classification objects
:   The Element Classification enrichment now has updated classified elements, contract elements, and parties and tables identified. For the updates, see [Element Classification](/docs/discovery?topic=discovery-element-classification).

New full support for Brazilian Portuguese
:   Added full support for the Brazilian Portuguese language. For more information, see [Language support](/docs/discovery?topic=discovery-language-support).

New support for 'bias' parameter in the query API
:   The query API (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`) now supports the `bias` parameter, which allows you to bias towards certain results, for example, documents that were published most recently. See the [Query your collection](/apidocs/discovery#query-your-collection){: external} method in the API reference for information.

New Default Contract Configuration
:   The **Default Contract Configuration** file provided to enrich collections for [Element Classification](/docs/discovery?topic=discovery-element-classification#element-collection) was found to have an issue with HTML normalizations. A new **Default Contract Configuration** is included with this release. Follow the steps below to apply the new **Default Contract Configuration** to your collections.

     1. Determine which of your collections are using either the **Default Contract Configuration** configuration file, or a custom configuration based on **Default Contract Configuration**.
     1. Make note of the changes you made to any custom configurations based on **Default Contract Configuration**.
     1. Since the old **Default Contract Configuration** file needs to be deleted from your environment before the new one is used, use the API [Delete configuration](/apidocs/discovery#delete-a-configuration){: external} to delete the current **Default Contract Configuration** associated with any of your collections. Also delete any configurations based on the old **Default Contract Configuration**.
     1. Now you can use the new **Default Contract Configuration** file. For each collection using one of those configurations, create a new collection. Apply the new **Default Contract Configuration** or create a new custom configuration based on the new **Default Contract Configuration** using the notes you made in step 2.
     1. Upload the files previously ingested to the original collections.
     1. Delete the old collections.

## 15 August 2018
{: #discovery-15august2018}
{: release-note}

New query operators
:   Two new query operators are available. `Exists` (`:*`) can be used to return all results where the specified `field` exists. `Does not exist` (`!*`) can be used to return all results that do not include the specified `field`. See [Query operators](/docs/discovery?topic=discovery-query-operators) for more information. 

## 2 August 2018
{: #discovery-2august2018}
{: release-note}

New multiple language support for connecting and syncing to Box, Salesforce, and SharePoint Online
:   {{site.data.keyword.discoveryfull}} now supports Arabic, English, French, German, Italian, Japanese, Korean, Portuguese, and Spanish language collections when connecting and syncing to Box, Salesforce, and SharePoint Online with the {{site.data.keyword.discoveryshort}} tooling. 

## 31 July 2018
{: #discovery-31july2018}
{: release-note}
 
New Pricing structure
:   Beginning **August 1, 2018**, {{site.data.keyword.discoveryfull}} has a new pricing structure. It features a simpler pricing model (document hours are no longer part of the calculation) and tiered pricing for {{site.data.keyword.discoverynewsfull}} queries. In addition, the Standard plan is retired, and the Lite plan has reduced document and {{site.data.keyword.discoverynewsshort}} query limits. The pricing changes require no action by current {{site.data.keyword.discoverynewsshort}} users. For details, see [{{site.data.keyword.discoveryshort}} Pricing Plans](/docs/discovery?topic=discovery-discovery-pricing-plans).
 
Update to version string
:   The version date of the API is updated to `2018-08-01`. To take advantage of the new environment sizing options (`LT`, `XS`, `S`, `MS`, `M`, `ML`, `L`, `XL`, `XXL`, `XXXL`), you must use this version date when creating environments, using the API. The environment sizes now have the type of `string` (previously the type was `integer`.)

## 27 July 2018
{: #discovery-27july2018}
{: release-note}

New Japanese language support for Discovery News
:   Released [{{site.data.keyword.discoverynewsfull}}](/docs/discovery?topic=discovery-watson-discovery-news) in one additional language: Japanese (`collection_id`: `news-ja`). {{site.data.keyword.discoverynewsfull}} is also available in English, German, Korean, and Spanish.

## 25 June 2018
{: #discovery-25june2018}
{: release-note}

New connect and sync with Box, Microsoft SharePoint Online, and Salesforce
:   Added the option to connect to and sync with Salesforce, Microsoft SharePoint Online, and Box data sources. These data sources are not available in Premium environments. 
:   Released the [Source Credential](/apidocs/discovery#list-credentials){: external} and [Configuration](/apidocs/discovery#add-configuration){: external} APIs for these data sources. 
:   {{site.data.keyword.discoveryfull}} supports only English language collections when connecting and syncing to Box, Salesforce, and SharePoint Online with the {{site.data.keyword.discoveryshort}} tooling. [Resolved](/docs/discovery?topic=discovery-release-notes#2aug18)
:   The individual document file size limit for Box, Salesforce, and SharePoint Online is 10MB.

New Performance Dashboard
:   Added a new Performance Dashboard in {{site.data.keyword.discoveryshort}} tooling. See [Viewing metrics and improving query results with the Performance dashboard](/docs/discovery?topic=discovery-performance-dashboard). The new dashboard is not available in Premium or Dedicated environments.

New full support for Japanese language
:   Added full support for Japanese. For more information, see [Language support](/docs/discovery?topic=discovery-language-support).

## 22 June 2018
{: #discovery-22june2018}
{: release-note}

New Events and Feedback API
:   Released the Events and Feedback API. See the [API reference](/apidocs/discovery#create-event){: external} for more information.

## 11 June 2018
{: #discovery-11june2018}
{: release-note}

New IAM authentication support for Washington, DC location
:   For applications that are hosted in Washington, DC (US East), the service now supports token-based Identity and Access Management (IAM) authentication. IAM uses access tokens rather than service credentials for authentication with a service. For more information about using IAM tokens with existing and new applications, see the [17 May 2018](/docs/discovery?topic=discovery-release-notes#discovery-17may2018) release update.

New Element Classification contract element
:   An additional contract element is now supported in Element Classification: `Safety and Security`. See [Understanding Contract Elements](/docs/discovery?topic=discovery-element-classification) for details.

## 6 June 2018
{: #discovery-6june2018}
{: release-note}

Improved query text display
:   {{site.data.keyword.discoverynewsfull}} queries now display the first 50 words of each article in the `text` JSON field. [Update](#discovery-24october2018)

## 5 June 2018
{: #discovery-5june2018}
{: release-note}

Improved Element Classification
:   Element Classification is now available to those subscribed to Premium plans.
:   The `assurance` rating of `Low` is no longer available for Element Classification.

## 31 May 2018
{: #discovery-31may2018}
{: release-note}

New full support for French language
:   Added full support for French. For more information, see [Language support](/docs/discovery?topic=discovery-language-support).

## 30 May 2018
{: #discovery-30may2018}
{: release-note}

Fixed incorrect count known issue
:   Previously, when querying {{site.data.keyword.discoverynewsshort}} it was possible to receive an incorrect document count because documents in other languages would be counted along with the language you requested. This is no longer the case.

New query results with special characters in multiple languages
:   Beginning with collections created on `22 May 2018` and after {{site.data.keyword.discoveryshort}} now returns query results that include special characters for the following languages: Dutch, English, French, German, Italian, and Portuguese. For example, if you query for `aqui`, you now receive results for both for `aqui` and <code>aqu&iacute;</code>.

## 21 May 2018
{: #discovery-21may2018}
{: release-note}

New German language support for Discovery News
:   Released [{{site.data.keyword.discoverynewsfull}}](/docs/discovery?topic=discovery-watson-discovery-news) in one additional language: German (`collection_id`: `news-de`). {{site.data.keyword.discoverynewsfull}} is also available in English, Korean, and Spanish.

## 17 May 2018
{: #discovery-17may2018}
{: release-note}

Improved query text display
:   {{site.data.keyword.discoverynewsfull}} queries now display only the first 20 words of each article in the `text` JSON field.

New API authentication for Sydney location
:   The service now supports a new API authentication process for service instances for applications that are hosted in Sydney (**au-syd**) as of 15 May 2018. They are enabled for applications that are hosted in other regions soon. {{site.data.keyword.Bluemix}} is in the process of migrating to token-based Identity and Access Management (IAM) authentication. IAM uses access tokens rather than service credentials for authentication with a service.
:   In the Sydney location, you use IAM access tokens with {{site.data.keyword.discoveryshort}} for

    -   *New service instances* that you create after May 15. For more information, see [Authenticating with IAM tokens](/docs/watson?topic=watson-iam).
    -   *Existing service instances* that you migrate from Cloud Foundry to a resource group that is managed by the Resource Controller (RC). Service instances that were created before May 15 continue to use service credentials for authentication until you migrate them. 

:   All new and existing service instances in other regions continue to use service credentials (`apikey:{apikey_value}`) for authentication.

### Using an IAM access token to authenticate
{: #iam-token}

When you use IAM access tokens, you authenticate before you send a request to {{site.data.keyword.discoveryshort}}.


1.  Get an API key from IBM Cloud. Use that key to generate an IAM access token. For more information, see [Authenticating to Watson services](/docs/watson?topic=watson-iam).
1.  Pass the IAM access token to {{site.data.keyword.discoveryshort}} by using the `Authorization` header. In the header, indicate that the access token is a `Bearer` token by specifying `Authorization: Bearer {access_token}`.

    The following simple cURL example uses an access token:

    ```bash
    curl -X GET
    --header "Authorization: Bearer eyJhbGciOiJIUz......sgrKIi8hdFs"
    "{url}/v1/environments?version=2017-11-07"
    ```
    {: pre}

    Replace `{url}` with your URL.

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

In your application, check the access token's expiration time before you use it to make an authenticated request. If it is expired, you must refresh the access token before you can use it. You use the value of the `refresh_token` field to refresh the access token. For more information, see [Authenticating to Watson services](/docs/watson?topic=watson-iam).


## 11 May 2018
{: #discovery-11may2018}
{: release-note}

New page for Discovery information security
:   Details about information security can be found at [Information security](/docs/discovery?topic=discovery-information-security).

Fixed Knowlege Graph known issue
:   The following {{site.data.keyword.discoveryfull}} Knowledge Graph `query_entities` known issue is fixed with the `2018-05-04` API version update. This fix only applies if entities are ingested or replaced after `2018-05-04`. Entities can be replaced by re-ingesting old documents or by ingesting new documents containing those entities. If old entities are not replaced, then `query_entities` return all uppercase with `2018-05-04` API version.

Improved entity names
:   All entity names were previously converted to camel case in `query_entities`. For example, the entity name "IBM Corporation" was converted to "Ibm Corporation". This is no longer the case.

## 9 May 2018
{: #discovery-9may2018}
{: release-note}

Change to sample document storage
:   Sample documents are now stored locally, in your browser's local roaming data folder.

## 4 May 2018
{: #discovery-4may2018}
{: release-note}

New Element Classification contract elements
:   Two additional contract elements are now supported in Element Classification: Attributes and Provenance. See [Understanding Contract Elements](/docs/discovery?topic=discovery-element-classification) for details.

## 26 April 2018
{: #discovery-26april2018}
{: release-note}

Fixed ingestion normalization known issue
:   The following ingestion issue is fixed: In some cases where post-enrichment `json_normalizations` and/or `normalizations` were specified, the normalizations might be applied in the wrong order, possibly resulting in documents being indexed with unexpected field values. This is no longer the case.

Change to maximum file size
:   The maximum file size for a sample document is now 1MB. The maximum file size was previously 5MB.

## 12 April 2018
{: #discovery-12april2018}
{: release-note}

New Knowledge Graph filters
:   Knowledge Graph: **Evidence** and **Canonicalization and filtering** are now available in all collections. In any collections created before `03-05-2018`, you need to reingest your documents to use these features. Previously, you needed to create a new collection and reingest your documents.
:   Update: As of **30 September 2019**, the {{site.data.keyword.discoveryfull}} Knowledge Graph Beta APIs are no longer accessible. See the [3 September 2019 release notes](/docs/discovery?topic=discovery-release-notes#discovery-3september2019) for more information.

## 11 April 2018
{: #discovery-11april2018}
{: release-note}

New Element Classification categories
:   Two additional categories are now supported in Element Classification: `Asset Use` and `Communication`. See [Understanding Contract Elements](/docs/discovery?topic=discovery-element-classification) for details.

## 2 April 2018
{: #discovery-2april2018}
{: release-note}

Change to sample document deletion
:   Sample documents are now automatically deleted after 24 hours, instead of 1 month.

## 16 March 2018
{: #discovery-16march2018}
{: release-note}

New full support for German language
:   Added full support for German. For more information, see [Language support](/docs/discovery?topic=discovery-language-support).

New Element Classification configuration
:   A new {{site.data.keyword.discoveryshort}} tooling configuration named **Default Contract Configuration** is added to support Element Classification, which can be used to extract party, nature, and category from elements in PDFs. See [Element Classification](/docs/discovery?topic=discovery-element-classification#element-collection) for details.

Update to documentation segmentation
:   Documentation segmentation moved from beta status to GA status. The segmentation limit is increased to 250 segments. It is no longer limited to 50 segments per document. See [Documentation segmentation](/docs/discovery?topic=discovery-configservice#doc-segmentation) for details.

Known issue with wildcards
:   Wildcards do not work with queries that contain capital letters. For example, given the key/field pair ``{"borrower": "GOVERNMENT OF INDIA"}``, `query-borrower:*ndia` returns results, but `query-borrower:*NDIA` does not.

## 8 March 2018
{: #discovery-8march2018}
{: release-note}

New beta Knowledge Graph features
:   The beta version of {{site.data.keyword.discoveryfull}} Knowledge Graph added several features. During the beta release, Knowledge Graph functionality and the methods associated with it are only available for service instances that are subscribed to **Advanced** plans, **Premium** plans, and all **Dedicated** environments. The new features are: entity similarity, evidence, and canonicalization and filtering
:   Update: As of **30 September 2019**, the {{site.data.keyword.discoveryfull}} Knowledge Graph Beta APIs are no longer accessible. See the [3 September 2019 release notes](/docs/discovery?topic=discovery-release-notes#discovery-3september2019) for more information.

## 7 March 2018
{: #discovery-7march2018}
{: release-note}

Fixed known issue with ingestion
:   The following ingestion known issue is fixed: Between 28 February and 6 March, a small percentage of documents were indexed with only the `id` and `extracted_metadata` fields (other document content was not indexed). The underlying problem is fixed; however, you must resubmit any affected documents for ingestion. There is no simple way to identify the affected documents.

## 5 March 2018
{: #discovery-5march2018}
{: release-note}

Fixed Knowledge Graph known issue
:   The following {{site.data.keyword.discoveryfull}} Knowledge Graph known issue is fixed with the `2018-03-05` API version update. This fix only applies to newly created collections that use the `2018-03-05` version update.  

Fixed names defect in ingestion
:   All entity type names and relation type names were previously converted to uppercase during ingestion. For example, the entity "GeoPoliticalEntity" was converted to "GEOPOLITICALENTITY," and the relation "partOf" was converted to "PARTOF." This is no longer the case.

## 1 March 2018
{: #discovery-1march2018}
{: release-note}

Improved query limits for Advanced and Premium plans
:   [Query expansion](/docs/discovery?topic=discovery-query-concepts#query-expansion) limits are increased for Advanced and Premium plans to 5,000 query expansions and 25,000 total terms. See [Discovery pricing plans](/docs/discovery?topic=discovery-discovery-pricing-plans) for details.

## 28 February 2018
{: #discovery-28february2018}
{: release-note}

Deprecated AlchemyLanguage enrichments
:   {{site.data.keyword.alchemylanguageshort}} enrichments are deprecated, effective **1 March 2018**.

## 23 February 2018
{: #discovery-23february2018}
{: release-note}

New document similarity query feature
:   Added the ability to query by document similarity. You can query for similar documents by  document ids, and optionally further refine the similarity by specifying fields. See [Document similarity](/docs/discovery?topic=discovery-query-concepts#doc-similarity) for more information.

Improved highlight parameter 
:   The [`highlight` parameter](/docs/discovery?topic=discovery-query-parameters#highlight) in query results is enhanced. Query results return complete sentences, ordered by their `score`.

## 21 February 2018
{: #discovery-21february2018}
{: release-note}

Fixed PDF file type
:   Previously, when ingesting PDF documents, the `file_type` returned when ingestion notices were queried, in the `extracted_metadata` object, and from the document details API was `html`. This is no longer the case. The `file_type` returned is now `pdf`.

## 26 January 2018
{: #discovery-26january2018}
{: release-note}

New Korean and Spanish accessibility in Discovery News
:   Added the ability to access Korean and Spanish collections to the [{{site.data.keyword.discoverynewsfull}}](/docs/discovery?topic=discovery-watson-discovery-news) tile in the tooling. Previously, these collections could only be queried via the API.

## 23 January 2018
{: #discovery-23january2018}
{: release-note}

New query expansion
:   Added the ability to expand the scope of a query - for example, you can expand a query for "car" to include "automobile" and "motor vehicle". In addition, you can replace commonly misspelled terms, for example, you can replace queries for "seabizcuit" with "seabiscuit." Query expansion is implemented with the {{site.data.keyword.discoveryshort}} API. See [Query expansion](/docs/discovery?topic=discovery-query-concepts#query-expansion) for details.  

## 15 January 2018
{: #discovery-15january2018}
{: release-note}

New version of Discovery News
:   {{site.data.keyword.discoverynewsfull}} Original was retired from service. It was replaced 31 July 2017 with a new version, named {{site.data.keyword.discoverynewsfull}}. 

## 11 January 2018
{: #discovery-11january2018}
{: release-note}

New full supoort for Korean language
:   Added full support for Korean. For more information, see [Language support](/docs/discovery?topic=discovery-language-support).

## 15 December 2017
{: #discovery-15december2017}
{: release-note}

New Element Classification enrichment
:   Released the **Element Classification** enrichment, which parses elements (sentences, lists, tables) in governing documents to classify important categories and types. See [Element classification](/docs/discovery?topic=discovery-element-classification) for more information. Element Classification is not available for service instances that are subscribed to the **Premium** plan. [Resolved](/docs/discovery?topic=discovery-release-notes#5jun18)

New Simplified Chinese and Dutch language support
:   Added Basic language support for Simplified Chinese and Dutch. See [Language Support](/docs/discovery?topic=discovery-language-support) for more information. Currently, Simplified Chinese and Dutch collections must be created with the API.

New parameters for Data Crawler
:   Added two new parameters for the Data Crawler: `proxy_host_port` and `read-timeout`. See [Configuring the Data Crawler](/docs/discovery?topic=discovery-configuring-the-data-crawler) for details.

Known issues during PDF ingestion
:   When ingestion notices are queried, the field `file_type` for pdf documents is returned as `html`.
:   The field `file_type` in the `extracted_metadata` object of results for pdf documents is set to `html`.
:   The document details API also returns the field `file_type` for pdf documents as `html`.
:   If you are ingesting JSON, mixed-type arrays are not supported.  
:   Update: [Resolved](/docs/discovery?topic=discovery-release-notes#21feb18)

New visual query builder in beta Knowledge Graph
:   Added a visual query builder for the beta version of {{site.data.keyword.discoveryfull}} Knowledge Graph.
:   Update: As of **30 September 2019**, the {{site.data.keyword.discoveryfull}} Knowledge Graph Beta APIs are no longer accessible. See the [3 September 2019 release notes](/docs/discovery?topic=discovery-release-notes#discovery-3september2019) for more information.

## 30 November 2017
{: #discovery-30november2017}
{: release-note}

New beta Knowledge Graph
:   Released the beta version of {{site.data.keyword.discoveryfull}} Knowledge Graph, which provides new end-points for querying entities and relations across documents. This includes context-based searches and relevance ranking. 
:   Update: As of **30 September 2019**, the {{site.data.keyword.discoveryfull}} Knowledge Graph Beta APIs are no longer accessible. See the [3 September 2019 release notes](/docs/discovery?topic=discovery-release-notes#discovery-3september2019) for more information.
  
New Korean and Spanish language support for Discovery News
:   Released [{{site.data.keyword.discoverynewsfull}}](/docs/discovery?topic=discovery-watson-discovery-news) in two additional languages: Korean (`collection_id`: `news-ko`) and Spanish (`collection_id`: `news-es`). {{site.data.keyword.discoverynewsfull}} Korean and Spanish are available for use via the API-only; for information about querying a collection via the API, see [API Reference](/apidocs/discovery#query-your-collection){: external}. :   Update: [Resolved](/docs/discovery?topic=discovery-release-notes#26jan18). {{site.data.keyword.discoverynewsfull}} English now has the `collection_id` of `news-en`. Formerly, the `collection_id` was `news`. If you use the former `collection_id`, it continues to work; however, you might want to switch to the new `collection_id` for new projects.

Updated confidence score calculations
:   Query results return a `score` value, which indicates the relative relevancy between query results. Starting 30 November 2017, the way that `score` is calculated changed. It is recommended that you only use the `score` value to rank documents in a single search, not across searches or sessions. If you trained a collection, a `score` value is returned in the results of a natural language query. Because the `score` indicates the relative relevancy between query results, it is not recommended tht it be used as a threshold. Instead, use the `confidence`, which indicates the relevance of the result as compared to the trained model, to set thresholds. For more information about setting thresholds, see [Confidence scores](/docs/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence).

Improved sentence boundaries in Passages
:   Beginning with this release, Passage retrieval detects sentence boundaries - it attempts to return passages that start at the beginning of a sentence and stop at the end. Previously, many passages would begin or end somewhere mid-sentence. See [Passages](/docs/discovery?topic=discovery-query-parameters#passages) for more information about Passage retrieval.

## 15 November 2017
{: #discovery-15november2017}
{: release-note}

New Relation Extraction enrichment
:   Added the [Relation Extraction](/docs/discovery?topic=discovery-configservice#relation-extraction) enrichment, which includes the option to incorporate a custom relation model created with {{site.data.keyword.knowledgestudiofull}}.

New custom entity model in Entity Extraction
:   The [Entity Extraction](/docs/discovery?topic=discovery-configservice#entity-extraction) enrichment {{site.data.keyword.discoveryshort}} tooling now includes the option to incorporate a custom entity model created with {{site.data.keyword.knowledgestudiofull}}.

Change to Japanese-language collections
:   The option to create a Japanese collection was removed from the {{site.data.keyword.discoveryshort}} tooling, however, the option to create a Japanese collection using the {{site.data.keyword.discoveryshort}} API remains.

New support for syndicated environments
:   {{site.data.keyword.discoveryshort}} Tooling now supports syndicated environments.

## 10 November 2017
{: #discovery-10november2017}
{: release-note}

New retrieval options for Passages
:   Added additional options for Passage retrieval to the {{site.data.keyword.discoveryshort}} tooling. When querying, you can now specify the fields you would like the passages to be returned from, the number of passages to return, and the maximum character count for each passage. See [Passages](/docs/discovery?topic=discovery-query-parameters#passages) for limits, minimums, and maximums.

## 8 November 2017
{: #discovery-8november2017}
{: release-note}

Update to version string
:   The version string for all API calls changed to `2017-11-07` from `2017-10-16`. 
:   This version moves the `score` in each query result to a new object named `result_metadata`. If the collection queried was trained, and the query is a natural language query, `result_metadata` includes a `confidence` field that displays the confidence score for that result. For details, see [Confidence scores](/docs/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence). Fields that include whitespaces (for example: `body.additional reading`) are filtered out during ingestion. The `notices` description reads `The field 'additional reading' is invalid: whitespace, '.', '#' and ',' are invalid in a field name`. The field `result_metadata` is filtered out during ingestion.

## 16 October 2017
{: #discovery-16october2017}
{: release-note}

Update to version string
:   The version string for all API calls changed to `2017-10-16` from `2017-09-01`. 
:   This version deprecates support for uploading new documents into existing collections enriched with {{site.data.keyword.alchemylanguageshort}} enrichments, and for creating new collections and enriching them with {{site.data.keyword.alchemylanguageshort}} enrichments. It is recommended that existing collections enriched with {{site.data.keyword.alchemylanguageshort}} be migrated to {{site.data.keyword.nlushort}} enrichments as soon as possible. The {{site.data.keyword.discoveryshort}} tooling also uses the `2017-10-16` version, see below for more information.
:   The {{site.data.keyword.discoveryshort}} tooling uses the `2017-10-16` API version string, so if you are using the tooling, you can no longer upload documents into existing {{site.data.keyword.alchemylanguageshort}} collections or create new collections enriched with {{site.data.keyword.alchemylanguageshort}} enrichments after `2017-10-16`.  If you want to continue using the {{site.data.keyword.discoveryshort}} tooling for enriching collections, migrate your collections to {{site.data.keyword.nlushort}} first.

New sample queries and link in Data schema explorer
:   The **Data schema explorer** displays sample queries for several enrichments in the {{site.data.keyword.discoverynewsfull}} collection. It also now has a **Show more values** link that displays additional example values for that enrichment in {{site.data.keyword.discoverynewsfull}}.

Improved **Manage data** screen
:   Multiple productivity enhancements, including combining the collection statistics, errors and warnings, and data insights on the **Manage data** screen.

New completion notification
:   A message was added that displays an alert when documents are finished processing.

## 9 October 2017
{: #discovery-9october2017}
{: release-note}

New unique count metric in the API
:   A new aggregation metric `unique_count` is available in the API. It returns a count of the unique instances of the specified field in a collection. See [unique_count](/docs/discovery?topic=discovery-query-aggregations#unique_count) for more information.

New support for Histogram and Timeslice in Visual Query Builder
:   Histogram and Timeslice aggregations are now supported in the **Visual Query Builder**. You also have the option to turn on anomaly detection for Timeslice queries.

New enrichment options in Data schema explorer
:   The **Data schema explorer** displays sample queries for the enrichment chosen. It also now has a **Show more values** link that displays additional example values for that enrichment.

New navigation menu in data and query screens
:   A hamburger menu is added to make it faster to navigate the **Manage data**, **View data schema**, and **Build queries** screens.

### 3 October 2017
{: #discovery-3october2017}
{: release-note}

New document segmentation
:   Document segmentation is now available. See [Splitting documents with document segmentation](/docs/discovery?topic=discovery-configservice#doc-segmentation).

### 29 September 2017
{: #discovery-29september2017}
{: release-note}

New Germany location now available
:   {{site.data.keyword.discoveryshort}} launched in the `Germany` location 29 September 2017. To comply with EU data regulations, AlchemyLanguage enrichments are not supported in this location.

Known issue in query fields
:   Known issue: Query fields cannot contain whitespaces.  When writing a query in {{site.data.keyword.discoveryshort}}, if any query field contains whitespace (for example, `body.additional reading`), you receive a `400: Invalid query syntax error`. [Resolved](/docs/discovery?topic=discovery-release-notes#8nov17)

### 25 September 2017
{: #discovery-25september2017}
{: release-note}

New Premium pricing plan
:   A Premium pricing plan is now available. For more information, see [{{site.data.keyword.discoveryshort}} pricing plans](/docs/discovery?topic=discovery-discovery-pricing-plans).

New feature for querying multiple collections
:   The ability to query, list fields, and query notices across collections within the same environment is added. For details, see [Querying multiple collections](/docs/discovery?topic=discovery-query-concepts#multiple-collections).

New language support
:   Language support information for {{site.data.keyword.discoveryshort}} is available at [Language support](/docs/discovery?topic=discovery-language-support).

Change to Visual Query Builder
:   The Visual Query Builder moved from beta status to GA status. Filter, Timeslice, and Histogram aggregations are not currently supported with the Visual Query Builder. Click **Include analysis of your results**, then **Edit in Query Language** on the **Build queries** screen to write those aggregations.

New beta deduplicate queries in Discovery News
:   Added the beta capability to deduplicate on {{site.data.keyword.discoverynewsfull}} queries.

New multiple language support for collections
:   In addition to English, German, and Spanish language collections, you can now create Arabic, French, Italian, Korean, Japanese, and Brazilian Portuguese collections.

Known issue in syndicated environments
:   {{site.data.keyword.discoveryshort}} Tooling does not support syndicated environments. [Resolved](/docs/discovery?topic=discovery-release-notes#15nov17)

### 14 September 2017
{: #discovery-14september2017}
{: release-note}

New Data Schema Explorer
:   Added the Data Schema Explorer, which displays the fields and values in your transformed documents. This information can be used to understand the data structure of your collection before building queries using the Discovery Query Language. The data schema can be viewed two ways: by document (Document view), or by field (Collection view). To access the Data Schema Explorer: on the **My Data Insights** screen, click the **View data schema** button, or click the **View Data Schema** icon on the left.

### 6 September 2017
{: #discovery-6september2017}
{: release-note}

New beta deduplicate documents function in Discovery News
:   Added the beta ability to deduplicate documents returned from your query. This beta feature works for both private and Watson Discovery News collections. See [Excluding duplicate documents from query results](/docs/discovery?topic=discovery-query-parameters#deduplication) for details.
:   Document deduplication is currently supported only as a beta capability.

### 31 August 2017
{: #discovery-31august2017}
{: release-note}

Update to version string
:   The version string for all API calls changed to `2017-09-01` from `2017-08-01`. This version includes updates that filter out the following invalid JSON fields during preview and ingestion so that only valid JSON fields are ingested. Update your version string to `2017-09-01` to avoid conflicts and possible errors.

Improved query and add functions at top level
:   `id`, `score`, and `highlight` at the top level (You can continue to add documents to your collection using document IDs with the `add a document` function. See the [API Reference](/apidocs/discovery#add-a-document){: external} for details.
:   `_` prefixed field names at the top level (as a result, when querying for a document by ID, you can query for `id` instead of `_id`.)
:   `#` and `,` in the field name
:   `+` and `-` prefixed field names
:   `"` `"` empty values for a field name
:   If your JSON documents include these characters in the field names, or `id`, `score`, and `highlight` at the top level, you need to remove them before adding the documents to your collection, or those fields are empty. You can create a custom configuration and normalize your JSON before adding documents to your collection to avoid this issue. See the [API reference](/apidocs/discovery#add-configuration){: external} for details. In addition, documents that include the punctuation characters `?`, `:`, or `#` in the file name cause errors during ingestion. Before ingesting them, rename any documents that include these characters.

Improved 'natural_language_query' retrieval methods
:   The retrieval methods for `natural_language_query` are updated to improve the relevance of results by matching words with related semantics. This update only affects collections that did not undergo relevance training. If you are using `natural_language_query` and did not conduct relevance training, you might see improvement in the order of results returned.

Improved query builder navigation
:   Changes to the query builder to make it easier to toggle between the Discovery Query Language and Natural Language query options, as well as among query, filter, and aggregation.

### 25 August 2017
{: #discovery-25august2017}
{: release-note}

Improved 'passages' array
:   The `passages` array now includes `field`, `start_offset`, and `end _offset`. `field` is the name of the field the passage was extracted from. `start_offset` is the starting character of the passage text within the field. `end_offset` is the ending character of the passage text within the field.

New beta enhancement on the **Build queries** screen
:   Added the beta ability to write queries in the {{site.data.keyword.discoveryshort}} Query Language with a visual builder. Click **Build in visual mode** in the **Search for documents** and **Limit which documents you query** sections to try it out.  As you build your query visually, it displays in the **{{site.data.keyword.discoveryshort}} Query Language** below it.
:   The visual query builder is currently supported only as a beta capability. 

### 18 August 2017
{: #discovery-18august2017}
{: release-note}

New nested aggregations and conditions in beta visual aggregation builder
:   Added support for nested aggregations and conditions to the beta visual aggregation builder introduced [11 August 2017](/docs/discovery?topic=discovery-release-notes#11aug17). There is a limit of 3 conditions per aggregation row.
:   The visual aggregation builder is currently supported only as a beta capability. 

### 11 August 2017
{: #discovery-11august2017}
{: release-note}

New pre-built sample queries and aggregations on the **Build queries** screen.
:   Added the option to select a query from a set of pre-built sample queries and aggregations. Click **Use a sample query** at the top right to access the list. If you are querying a private data collection, the samples use `top entities`, `categories`, etc. found in your collection. These queries can be used as a starting point for writing your own queries. Sample queries are available for both {{site.data.keyword.discoverynewsfull}} and private collections.

New beta visual aggregation builder
:   Added the beta ability to write aggregations with a visual builder. Click **Build in visual mode** above the **Write an aggregation query using the {{site.data.keyword.discoveryshort}} Query Language** field to try it out.  As you build your aggregation visually, the query displays in the **{{site.data.keyword.discoveryshort}} Query Language** below it.  
:   The visual aggregation builder is currently supported only as a beta capability. 

### 31 July 2017
{: #discovery-31july2017}
{: release-note}

New release of Discovery News
:   A new version of {{site.data.keyword.discoverynewsfull}} was released. The original version is renamed as {{site.data.keyword.discoverynewsfull}} Original and is retired, with a removal from service date of **15 January 2018**.
:   If you create a new instance of {{site.data.keyword.discoveryshort}}, you only have access to the new version of {{site.data.keyword.discoverynewsfull}}.
  {: note}

New pricing structure
:   A new pricing plan for {{site.data.keyword.discoveryfull}} was released. See [{{site.data.keyword.discoveryshort}} pricing plans](/docs/discovery?topic=discovery-discovery-pricing-plans) for details.

Update to version string
:   The version string for all API calls changed to `2017-08-01` from `2017-07-19`. This version includes updates for the new pricing plan and the new version of Watson Discovery News. Update the version string to avoid conflicts and possible errors.

### 19 July 2017
{: #discovery-19july2017}
{: release-note}

Change to Pricing plans
:   Pricing changes will take effect on 1 August 2017.
:   Users that are currently on the deprecated **30 day free trial** plan will be automatically migrated to the **Lite** plan. As a result of this transition, existing users might meet or exceed the lite plan limit on documents _(2000)_, storage _(200Mb)_, or number of collections _(2)_. If you exceed the limit of the **Lite** plan, you cannot add any additional content into the service, but you can still query collections. 
:   View the current status of all these limits by using the {{site.data.keyword.discoveryshort}} tooling or API. To resume adding content to the {{site.data.keyword.discoveryshort}} instance, you must complete one of the following actions:
:   Remove collections or documents so that limits of the **Lite** plan are not exceeded.
:   You can delete documents either individually in the API, using the [delete-doc](/apidocs/discovery#delete-a-document){: external} method, or you can delete whole collections, using the tooling or API, by using the [delete-collection](/apidocs/discovery#delete-a-collection){: external} method.
:   Upgrade your plan to a level that meets your storage needs.
:   Customers with size **`1`** **`2`** or **`3`** environments will be automatically migrated to the **Advanced** plan.

### 17 July 2017
{: #discovery-17july2017}
{: release-note}

Update to relevancy training, natural language query, and highlighting
:   Relevancy training announced on 23 June 2017 moved from beta to GA status.
:   Natural language query announced on 19 June 2017 movedd from beta to GA status.
:   Highlighting announced on 25 May 2017 moved from beta to GA status.

Update to enrichment mechanism
:   {{site.data.keyword.discoveryfull}} is changing its enrichment mechanism from {{site.data.keyword.alchemylanguageshort}} to {{site.data.keyword.nlushort}} as of this release. 
:   {{site.data.keyword.alchemylanguageshort}} is in the process of being deprecated, so it is recommended that you start using {{site.data.keyword.nlushort}} as soon as possible.
:   If you integrate with Watson Knowledge Studio, you must still use the {{site.data.keyword.alchemylanguageshort}} enrichment configuration. For details, see [Integrating with {{site.data.keyword.knowledgestudiofull}}](/docs/discovery?topic=discovery-integrating-with-wks).

Update to version string
:   The version string for all API calls changed to `2017-07-19` from `2017-06-25`. This version enables an NLU default config on collection creation. You should still be able to enrich with {{site.data.keyword.alchemylanguageshort}} in previous versions.
:   The default configuration is updated to use {{site.data.keyword.nlushort}}. To avoid conflicts and possible errors, it is recommended that you update the version string as soon as possible.

Known issue for Insight Cards
:   The Insight Cards for collections with {{site.data.keyword.alchemylanguageshort}} enrichments do not update automatically any longer. You must migrate your collection to {{site.data.keyword.nlushort}} Enrichments for the insight cards to update.
:   If you created a collection prior to **18 July, 2017** and applied the **Default Configuration**, that collection was enriched with the {{site.data.keyword.alchemylanguageshort}} enrichments. If you apply the **Default Configuration** to a collection after this date, the {{site.data.keyword.nlushort}} enrichments are used. The configuration name switches to **Default Configuration with NLU** in the tooling. Because {{site.data.keyword.alchemylanguageshort}} enrichments are being deprecated, it is recommended that they not be used with new collections.

### 30 June 2017
{: #discovery-30june2017}
{: release-note}

Update to entity normalization 
:   The entity normalization capability introduced as a beta feature on 5 May 2017 moved to GA status.

### 23 June 2017
{: #discovery-23june2017}
{: release-note}

Update to version string
:   The version string for all API calls changed to `2017-06-25` from `2016-12-01`. 
:   The new version string enables enrichments in German (`de`) or Spanish (`es`) if the language of a collection is set to one of those languages. Previously, all enrichments were performed in English regardless of a collection's language setting.
:   If you do not use enrichments in non-English languages, you can continue to use the `2016-12-01` version string. However, to avoid potential future conflicts, it is recommended that you update the version string as soon as possible.

New anomaly detection availability
:   Anomaly detection is now available as part of `timeslice` aggregations as a GA capability.

New beta improvement to relevancy tooling
:   Added the beta ability to improve the relevancy of query results using the Discovery tooling (relevancy tooling). See [Improving the relevance of your query results with the Discovery tooling](/docs/discovery?topic=discovery-improving-result-relevance-with-the-tooling).

### 19 June 2017
{: #discovery-19june2017}
{: release-note}

New select language of documents
:   Added option to specify the language of the documents in a new collection as English, Spanish, or German. To use it, choose **Select the language of your documents** on the **Name your new collection** dialog.

Added a **Summary** tab to the **Build queries** screen
:   The **Summary** tab displays an overview of the full query results provided in the existing **JSON** tab. The **Summary** display varies, based on your query and enrichments. Information that might be displayed includes: document name or ID, aggregation statistics, document passages in order of relevance, and results by enrichment.

Added a Natural Language Query option to the **Build queries** screen
:   To use it, click **Ask a question in plain language** in the **Search for documents** section, and a field displays where you can enter your question. You can now access the original query field, formerly titled **Enter a query or keyword**, by clicking the **Use the Discovery Query Language** button.

The **Build queries** screen was redesigned, but all fields and options remain. 
:   Following are the old and new names for the fields.

    | **Old field name**                                           | **New field or section name**                                                                                                 |
    |----------------------------------------------------------|-------------------------------------------------------------------------------------------------- ---------------------|
    | Write and run a query                                    | Search for documents                                                                                                  |
    | Narrow your query results (Filter)                       | Limit which documents you query                                                                                       |
    | Group query results (Aggregation)                        | Include analysis of your results                                                                                      |
    | Fields to display                                        | Name did not change, but moved to the new **Customize display options** section.                                      |
    | Number of documents to return (Count)                    | Number of documents to return [This field was moved to the **Customize display options** section.]                    |
    | Include matching passages                                | Include relevant passages [This field was moved to the **Customize display options** section.]                        |
    | Number of query fields to skip at the beginning (Offset) | Number of query results to skip at the beginning [This field was moved to the **Customize display options** section.] |

### 5 June 2017
{: #discovery-5june2017}
{: release-note}

Updated text display for Discovery News 
:   Discovery News queries now display only the first 150 words of each article in the `text` and `alchemyapi_text` JSON fields. The `blekko.snippet` field displays only the first sentence of the snippet array.

### 30 May 2017
{: #discovery-30may2017}
{: release-note}

Update to 'passages' parameter
:   The `passages` parameter on the query API moved from beta to GA status.

### 25 May 2017
{: #discovery-25may2017}
{: release-note}

New query field highlighting for tooling
:   Added query field highlighting in this release. This feature adds yellow highlighting to field names in the JSON of the Results pane. All fields that are queried or filtered on are highlighted for each result even if the content of the field does not match the query. Any fields used in aggregations are also highlighted in the query results, but only the first aggregation operation is highlighted.

### 10 May 2017
{: #discovery-10may2017}
{: release-note}

New support for 'highlight' parameter
:   The `query` and `notices` methods now support the `highlight` parameter. The parameter is a boolean. When you run a query and specified `highlight` as `true`, the service returns output that includes a new `highlight` field in which words that match the query are wrapped in HTML `*` (emphasis) tags. See the [Query parameters](/docs/discovery?topic=discovery-query-parameters#highlight) for details.

Known issue when deleting an environment
:   It is possible for the deletion of an environment to complete only partially, resulting in a situation in which a new environment cannot be created because only a single environment per service instance is permitted. If you attempt to delete and then create an environment but see either operation stuck in the `pending` state, it is likely that you encountered this problem. To work around it, re-run the deletion operation to complete it, then create the new environment.

### 8 May 2017
{: #discovery-8may2017}
{: release-note}

Improved precision for emotion analysis and training dataset
:   Updated the emotion tone score model to improve precision on emotion analysis (`docEmotion`) enrichments. The training dataset was expanded and feature engineering was altered and as a result, the model has higher precision on the benchmark dataset.

### 5 May 2017
{: #discovery-5may2017}
{: release-note}

New beta support for entity normalization
:   Entity normalization is now available for use with the Discovery service that use a custom model generated by Watson Knowledge Studio. Entity normalization inserts normalized (canonical) names for different references to the same person or object in the source document. 
:   Entity normalization is currently supported only as a beta capability. 
:   [Resolved](/docs/discovery?topic=discovery-release-notes#discovery-30june2017)

Improved tooling error log
:   The Tooling error log is no longer limited to a maximum of eight (8) pages of results. The error log still displays the document ID if the document name is not available.

Update to configuration names
:   Configuration names are limited to 50 characters and must consist of the characters `[a-zA-Z0-9-_]`. 

Improved availability of 'passages' parameter
:   The `passages` parameter previously available only through the API is now available through the Tooling as well as the API.

### 25 April 2017
{: #discovery-25april2017}
{: release-note}

New training data functionality
:   Use *training data* to improve the accuracy of your query results. When you provide a Discovery instance with training data, the service uses advanced Watson algorithms to determine the most relevant results. As you add more training data, the service instance becomes more accurate and sophisticated in the results it returns. See [Improving the relevance of your query results](/docs/discovery?topic=discovery-improving-result-relevance-with-the-api) and the [API Reference](/apidocs/discovery#list-training-data){: external} for information.

New beta support for 'natural_language_query' parameter
:   The API now supports the `natural_language_query` parameter as a beta release. This parameter enables you to specify a query in natural language instead of in the Discovery service's query language. See the [Query your collection](/apidocs/discovery#query-your-collection){: external} method in the API reference for information.

### 14 April 2017
{: #discovery-14april2017}
{: release-note}

New enhancements to query API
:   Enhancements are now available for the query API (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`). See the [Query your collection](/apidocs/discovery#query-your-collection){: external} method in the API reference for information.

New support for 'passages' parameter in the query API
:   The query API now supports the `passages` parameter. If the parameter is set to `true`, the query returns a set of the most relevant passages from the documents in your collection. The passages are generated by sophisticated Watson algorithms to determine the best passages of text from all of the documents returned by the query. This enables you to find information and context more precisely. See the [Query your collection](/apidocs/discovery#query-your-collection){: external} method in the API reference for information.
:   Specifying `passages=true` in your query can reduce performance as a result of increased processing to extract passages. With larger environments, the performance impact can be lessened.
:   The `passages` parameter is supported only on private collections. It is not supported in the Watson Discovery News collection.
:   The `passages` parameter currently returns a maximum of 10 results. The number of returned results cannot be changed. [Update](/docs/discovery?topic=discovery-query-parameters#passages_count)
:   The `passages` parameter returns a maximum of three (3) passages from any given document in the collection. If a document contains more than three additional relevant passages, the parameter does not return them.

### 7 April 2017
{: #discovery-7april2017}
{: release-note}

New support for 'sort' parameter in the query API
:   The query API (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`) now supports the `sort` parameter, which enables you to specify a comma-separated list of fields in the document to sort on. See the [Query your collection](/apidocs/discovery#query-your-collection){: external} method in the API reference for information.

Improved handling by 'timeslice' parameter
:   The `timeslice` parameter for query aggregations now correctly handles dates in UNIX epoch format. See [Query reference](/docs/discovery?topic=discovery-query-reference#aggregations) for information about aggregations and the `timeslice` parameter.

Update to JavaSDK
:   The {{site.data.keyword.discoveryshort}} Java SDK has been updated. See the [API Reference](/apidocs/discovery?language=java){: external} for details.

Fixed known issues with wildcard limitations in queries
:   Only one wildcard worked in any given query. For example, `query-month:*ctober` worked, but `query-month:*ctobe*` generated a parsing error. This is resolved.
:   Wildcards did not work with queries that contained capital letters. For example, given the key/field pair ``{"borrower": "GOVERNMENT OF INDIA"}``, `query-borrower:*ndia` returned results but `query-borrower:*NDIA` did not. This is resolved.
:   Wildcards are not necessary within phrases in queries. For example, given the key/field pair `{"borrower": "GOVERNMENT OF TIMOR"}`, `query-borrower:"GOVERNMENT OF TIMOR"` returns results, but `query-borrower:"GOVERNMENT OF TI*OR"` does not. Using a wildcard is not applicable within phrases because all of the characters within the quotation marks (`"`) of a phrase are escaped.

### 24 March 2017
{: #discovery-24march2017}
{: release-note}

New feature for My data insights 
:   Added filtering to the "My data insights" screen in the Discovery tooling.

### 15 March 2017
{: #discovery-15march2017}
{: release-note}

Known issues
:   All fields that are ingested from HTML, PDF, and Word documents are typed as **string**. JSON fields and calculated fields, such as sentiment score, are typed as defined. [Update](/docs/discovery?topic=discovery-addcontent#adding-content-with-the-api-or-tooling)
:   The `preview` operation does not currently check for nested JSON arrays within a submitted JSON document. The service does not currently support nested JSON arrays, so a document with nested arrays can successfully pass the `preview` operation but fail upon an ingestion attempt. See [Can I upload JSON arrays?](/docs/discovery?topic=discovery-troubleshoot#faq-array)
:   If you encounter ingestion errors with the message `unsupported text language`, update your configuration with the `"language": "english"` enrichment option to force all text to be interpreted as English, as shown in the following example. 
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

Fixed known issue
:   Improved performance and stability of the service.

### 8 March 2017
{: #discovery-8march2017}
{: release-note}

Improved back end performance
:   Optimized the back end, including the addition of new timeouts, to improve overall performance.

Fixed defect 
:   Fixed a bug that caused the environment status of free (`0`-sized) environments to report a status of `pending` regardless of the real status.

English language support
:   The only national language currently supported by {{site.data.keyword.discoveryshort}} is U.S. English (`en_US`). [Update](/docs/discovery?topic=discovery-language-support)

### 3 March 2017
{: #discovery-3march2017}
{: release-note}

New *My data insights* screen
:   Added the *My data insights* screen to the Discovery tooling.

### 26 February 2017
{: #discovery-26february2017}
{: release-note}

Improved performance and error codes
:   The performance of the {{site.data.keyword.discoverynewsshort}} environment is faster and stable.
:   Improved error codes messaging and delivery.

Change to number of results
:   The {{site.data.keyword.discoverynewsshort}} service returns only 50 results at a time. As a workaround, use the `offset` parameter in your query to page through results.
:   You can submit a new configuration with an individual document by using the following command:

    ```bash
    curl -X POST -u apikey:{apikey_value} -F "file=@wikipedia-sample.html" -F "configuration=$(cat config.json)" "https://gateway.watsonplatform.net/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2016-12-01"
    ```
{: pre}

:   The PDF and Word converters create HTML as a middle step. The service can apply additional transforms and normalizations on the intermediary HTML before the final transformation to normalized JSON.

### 16 February 2017
{: #discovery-16february2017}
{: release-note}

New features for JSON fields and environments
:   You can now use CSS selectors to select JSON fields that you can then apply enrichments to. See [Using CSS selectors to extract fields](/docs/discovery?topic=discovery-configservice#using-css) for information.
:   You can now increase the size of an environment by passing a new `size: X` parameter to the [update-environment method](/apidocs/discovery#update-an-environment){: external}, where `X` is an integer between 0 and 3. See the [create-environment method](/apidocs/discovery#create-an-environment){: external} for information about environment sizes and attributes. If you want to update your pricing plan, see [{{site.data.keyword.discoveryshort}} pricing plans](/docs/discovery?topic=discovery-discovery-pricing-plans).
:   You cannot reduce the size of an existing environment. If you want to reduce the size of your environment, contact {{site.data.keyword.IBM}} support for assistance.

New query operator
:   The `::!` operator is added as a unary not-equals operator. For example, you can now run `query=field::!value` (not equals). Previously the only exclusionary operator was `:!` for the not-contains operator (for example, `query=field:!value`).

Fixed defects
:   Applied security updates.
:   Improved status messages for search alerts.

### 1 February 2017
{: #discovery-1february2017}
{: release-note}

New release of Data Crawler now available
:   These notes apply specifically to the Data Crawler 1.3.0 release. [Update](/docs/discovery?topic=discovery-adding-content-with-data-crawler)
:   The Data Crawler records the `document_id` values used to upload documents, and the status of the upload. Conversion notices are not persisted outside of the log. There is not presently a tool to interact with that data, but such tools are expected to be developed as time permits. The data is accessible via H2 database, which could be configured to use a remote DBMS.

### 16 January 2017
{: #discovery-16january2017}
{: release-note}

New release of Data Crawler now available
:   These notes apply specifically to the Data Crawler 1.2.5 release. [Update](/docs/discovery?topic=discovery-adding-content-with-data-crawler)
:   The Data Crawler can optionally poll for document status immediately after uploading a file. This check is a part of the Crawler's concept of "uploading a document", so when this check is enabled, it is virtually impossible for the Crawler to upload concurrently more documents than what {{site.data.keyword.discoveryshort}} can process concurrently for the user.
:   A side effect of the `check_for_completion` feature is that the Crawler also can expose to the user why a document failed, when it failed. Any notices attached to a document that was successfully uploaded, but failed to process, are displayed in the Crawler log. The notices are not exported to a processable file, but IBM would welcome a feature suggestion for that.

### 5 January 2017
{: #discovery-5january2017}
{: release-note}

Known issues identified after the GA release on 15 December 2016.
:   [Update: API reference](/apidocs/discovery){: external}
:   If you add a document by using the `POST /v1/environments/{environment_id}/collections/{collection_id}/documents`
    or `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]` call, the call returns a document ID and the **processing** status. If you then query the document by using the `GET /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]` call, the status remains at **processing** until ingestion is completed, at which point the status changes to **available**.
:   If you **update** an existing document by using the `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]` call, the corresponding **GET** call returns the `available` status, even if the service did not yet fully process the updated document. The `available` status can refer to either the original document or the updated document. Unless the update operation returns an error, there is not currently a way to determine the status of the updated document.
:   You can work around this by waiting up to 10 minutes after submitting a document update before attempting to query the updated content.

### General Availability release, 15 December 2016
{: #discovery-15december2016}
{: release-note}

A GA release is now available
:   The following notes apply to the General Availability (GA) release of {{site.data.keyword.discoveryfull}}.

#### General notes
{: #rn-general-notes}

General notes
:   Adding content [Update: Adding content](/docs/discovery?topic=discovery-addcontent)
:   [API reference](/apidocs/discovery){: external} for current API version.
:   Integration [Update: Integrating with {{site.data.keyword.knowledgestudiofull}}](/docs/discovery?topic=discovery-integrating-with-wks).
:   You cannot currently specify the data type of fields. All fields are indexed as text (data type **string**).
:   If you use the API to work with the service, you must specify the API version with each call. The current API version is **2016-12-01**. The specific version is not enforced in the GA release, but it still must be listed to enable compatibility with future releases.
:   You can use the service with a custom model created with {{site.data.keyword.knowledgestudiofull}}. The custom model can be used to enrich ingested documents. You must use the API to integrate the custom model with {{site.data.keyword.discoveryshort}}; you cannot perform the integration by using the tooling.

#### Data management
{: #rn-data}

Update
:   Pricing plans [Update](/docs/discovery?topic=discovery-discovery-pricing-plans)

Data management
:   Search indexes are not encrypted.
:   Backup and restore functions are not user controllable.

#### Environments
{: #rn-environments}

Update
:   Pricing plans [Update](/docs/discovery?topic=discovery-discovery-pricing-plans)

Environments
:   You can create only one environment per service instance to upload your own data.
:   {{site.data.keyword.discoveryshort}} is located in a single availability zone (US South).
:   Dedicated and Premium plans are not available at the current time.

#### Environment sizing
{: #rn-sizing}

Update
:   Pricing plans [Update](/docs/discovery?topic=discovery-discovery-pricing-plans)

Environment sizing
:   You can choose an environment size only when creating a new environment. The ability to resize an environment is not currently available to users.
:   Choosing an environment size with more RAM increases performance.
:   There are currently no prescriptive sizing recommendations available for specific use cases.
:   Custom sizing for {{site.data.keyword.knowledgestudiofull}} models is not self-serve. Contact your {{site.data.keyword.IBM}} representative for more information.

#### Ingestion limitations
{: #rn-ingestion}

Update
:   Pricing plans [Update](/docs/discovery?topic=discovery-discovery-pricing-plans)

Ingestion limitations
:   The ingestion rate is currently limited to 100 concurrent document ingestion operations. An application that submits documents to the service for ingestion needs to respect HTTP 429 errors and throttle down ingestion requests accordingly.
:   {{site.data.keyword.alchemylanguageshort}} enrichments are limited to the first 50 kB per field.
:   Enrichments from {{site.data.keyword.knowledgestudiofull}} custom models are not limited, but split documents into 10-kB chunks. No relationships are annotated across chunk boundaries.

#### Query limitations
{: #rn-query}

Update
: Query concepts [Update](/docs/discovery?topic=discovery-query-concepts)

Query limitations
:   Excessive query load can cause the search-index process to restart automatically.
:   Applications that issue queries must enforce reasonable limits on the number of concurrent queries.

### Known issues
{: #rn-issues}

Updates
:   API Reference [Update: API reference](/apidocs/discovery){: external}
:   Tooling [Update: tooling](/docs/discovery?topic=discovery-getting-started)
:   Data Crawler [Update: Data Crawler](/docs/discovery?topic=discovery-adding-content-with-data-crawler)
:   Enrichments [Update: Enrichments](/docs/discovery?topic=discovery-configservice#adding-enrichments)
:   Adding content [Update: Adding content](/docs/discovery?topic=discovery-addcontent)

Known issues
:   You cannot delete a document by using the tooling. If you need to delete a document, you must use the API's [Delete a document](/apidocs/discovery#delete-a-document){: external} method as described in the API reference.
:   The API does not currently support getting a list of notices (warnings and error) that are generated during document ingestion. The tooling is therefore unable to show a list of ingestion notices, and there is no easy way to determine which, if any, documents crawled by the Data Crawler failed to be ingested. 
:   Document status information is not always accurate.
:   If an ingestion operation takes longer than the configured timeout of 10 minutes, the service reports that the document is not known to the service until the ingestion operation completes. After the operation completes, the document status is available and accurate.
:   Documents that are successfully indexed but generated errors can have a status of **failed** for a short period of time until the document fully commits to the index. After the document commits to the index, the listed status is accurate.
:   You cannot use the tooling to replace a specific document. If you attempt to do so, the second document is uploaded as a separate document. If you are using the API and know the ID of the document you want to replace, you can do so; see [Update a document](/apidocs/discovery#update-a-document){: external} in the API reference. If you are using the Data Crawler, uploading an updated document from the same URL as a previous document replaces the original document.
:   If you are using the tooling to edit the enrichments in your configuration, you can edit only enrichments used for extraction. If you want to add or edit other enrichments (for example, custom enrichments from a {{site.data.keyword.knowledgestudiofull}} model), you must use the API. See the [Update a configuration](/apidocs/discovery#update-a-configuration){: external} method in the API reference for information.
:   The Java, Python, and Node.js SDKs for {{site.data.keyword.discoveryshort}} do not provide all of the functionality provided by the default REST (cURL) API. Not all cURL methods have an equivalent method in the non-cURL SDKs, and not all non-cURL methods provide all of the same features that their cURL equivalents have. In other words, the Java, Python, and Node.js SDKs currently provide only a subset of the cURL API's capabilities.
:   If you use the Word converter, matching on headings by using the `style` key is much more accurate and efficient than it by using the `level` key.

Data Crawler
:   The Data Crawler retries uploads if it encounters an upload failure.
:   The Data Crawler is unable to retry documents that uploaded successfully but failed to be converted or indexed.
:   The Data Crawler does not have a function to check downstream status and attempt to re-upload URLs that failed downstream.
:   There is no easy way to determine which documents are ingested by the Data Crawler. For example, if you run the Data Crawler against a set of 500 documents, the Data Crawler might report failures submitting 65 documents with a total collection of 212 documents. The status of the remaining 223 documents is undetermined.
:   A workaround is available, but it is complicated and involves invoking the API directly. Contact {{site.data.keyword.IBM}} support for assistance.

