---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-01-24"

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

# Adding content
{: #addcontent}

How do I decide which document upload method to use?
{: shortdesc}

-   Use the [API](/docs/services/discovery/getting-started.html) if you are integrating the upload of content with an existing application or creating your own custom upload mechanism.
-   Use the [{{site.data.keyword.discoveryshort}} tooling](/docs/services/discovery/getting-started-tool.html) if you want to quickly upload locally accessible files.
    When uploading documents using the {{site.data.keyword.discoveryshort}} tooling, all documents should have a unique file name. If two files have the same name, the original will be overwritten when the newer version is uploaded. If you would prefer that documents with the same file name coexist in your collection, the Document ID needs to be specified. You can specify the Document ID if you upload documents using the API or the Data Crawler.
-   Use the {{site.data.keyword.discoveryshort}} tooling or API to connect to Box, Salesforce, Microsoft SharePoint Online, and Microsoft SharePoint 2016 data sources, or do a web crawl. See [Connecting to data sources](/docs/services/discovery/connect.html) for more information.
-   Use the [Data Crawler](/docs/services/discovery/data-crawler.html) if you want to have a managed upload of a significant number of files, or you want to extract content from a supported repository (such as a DB2 database).

## Adding content with the API or tooling

Consider the following when you are ready to add documents to your collection:

-   The maximum file size that can be uploaded to the {{site.data.keyword.discoveryshort}} service is 50MB.
-   The sample documents are not automatically added to the collection. You must add them if you want them as part of your collection. (Applies only to collections created before the release of [Smart Document Understanding](/docs/services/discovery/sdu.html).)
-   Only the first 50,000 characters of each JSON field selected for enrichment will be enriched.
-   When creating a collection, you select the document language (English is the default). See [Language support](/docs/services/discovery/language-support.html) for the list of languages. Your documents will be enriched in the selected language. Do not mix languages within the same collection.
-   You can add Microsoft Word, PDF, HTML, and JSON documents to your collection. **Note:** PDFs that are scanned image files can not be converted and enriched. (Applies only to collections created before the release of [Smart Document Understanding](/docs/services/discovery/sdu.html).)
-   The documents in your collection will be converted using the current configuration, unless you choose a different configuration file. For information about creating a configuration file, see [Custom configuration](/docs/services/discovery/building.html#custom-configuration). (Applies only to collections created before the release of [Smart Document Understanding](/docs/services/discovery/sdu.html).)
-   When documents are uploaded to a data collection, they are converted and enriched using the configuration file chosen for that collection. If you decide later that you would like to switch a collection to a different configuration file, you can do that, but the documents that have already been uploaded will remain converted by the original configuration file. All documents uploaded after switching the configuration file will use the new configuration file. If you want the **entire** collection to use the new configuration, you will need to create a new collection, choose that new configuration file, and re-upload all the documents. (If using [Smart Document Understanding](/docs/services/discovery/sdu.html), you will be prompted to re-upload your documents after you click the **Apply changes to collection** button.)
-   You cannot specify the `data type` (For example: `text` or `date`) of fields. During document ingestion, if a field is detected that does not yet exist in the index, {{site.data.keyword.discoveryshort}} will automatically detect the `data type` of that field based on the value of the field for the first document indexed.
-   A document can fail to be ingested because of a type mismatch between data in the current document and similar data in a previously ingested document. For example, a field might be typed as a `date` in one document and a `string` in a subsequent document, preventing the subsequent document from being indexed correctly.
-   If you plan to use custom tokenization (currently only available for Japanese collections when using the {{site.data.keyword.discoveryshort}} API), the tokenization dictionary for your collection must be added before uploading documents.

## Uploading documents with the Discovery tooling

1.  Create a collection. See [Preparing the service for your documents](/docs/services/discovery/building.html#preparing-the-service-for-your-documents).
1.  Click on the collection to open it.
1.  Click the **Upload documents** button and start uploading your documents via drag and drop or browse.

Your documents are now enqueued to be converted and enriched. The time this takes will depend on the size of your collection. After it is indexed and enriched, the details of the Collection will be displayed in the **Overview** section.

-   **Fields identified** in your collection (Smart Document Understanding only.)
-   **Created** and **Last updated** dates (Click **Use this collection in API** to see the `collection_id`, `configuration_id`, and `environment_id`.)
-   **Number of documents** in your collection
-   **Configuration** — The name of the configuration file used to convert this collection (Only for collections created before the release of [Smart Document Understanding](/docs/services/discovery/sdu.html).)
-   **Errors and Warnings**

For information on how to connect to Box, Salesforce, Microsoft SharePoint Online, and Microsoft SharePoint 2016 data sources, or do a web crawl with the {{site.data.keyword.discoveryshort}} tooling, see [Connecting to data sources](/docs/services/discovery/connect.html).


## Uploading documents with the API

See [Getting started with the {{site.data.keyword.discoveryshort}} API](/docs/services/discovery/getting-started.html) for a step-by-step tutorial.

For more information about the API, see the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery/){: new_window}.

1.  Use the `POST /v1/environments/{environment_id}/collections` method to create a collection.
1.  Then use the `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` method to add documents to your collection.

## Crawling URLs

You can crawl URLs and index them using the {{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} {{site.data.keyword.discoveryshort}} Service [Indexing plugin for Apache Nutch ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Watson/nutch-indexer-discovery). The crawl does not update automatically, so the procedure will need to be repeated periodically to keep the index up-to-date. 

You also have the option to use the beta Web Crawl connector. See [Connecting to data sources](/docs/services/discovery/connect.html#connectwebcrawl).
