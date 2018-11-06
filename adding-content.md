---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-15"

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

# Adding content

How do I decide which document upload method to use?
{: shortdesc}

-   Use the [API](/docs/services/discovery/getting-started.html) if you are integrating the upload of content with an existing application or creating your own custom upload mechanism.
-   Use the [{{site.data.keyword.discoveryshort}} tooling](/docs/services/discovery/getting-started-tool.html) if you want to quickly upload locally accessible files.
    When uploading documents using the {{site.data.keyword.discoveryshort}} tooling, all documents should have a unique file name. If two files have the same name, the original will be overwritten when the newer version is uploaded. If you would prefer that documents with the same file name coexist in your collection, the Document ID needs to be specified. You can specify the Document ID if you upload documents using the API or the Data Crawler.
-   Use the {{site.data.keyword.discoveryshort}} tooling or API to connect to Box, Salesforce, and Microsoft SharePoint Online data sources. See [Connecting to data sources](/docs/services/discovery/connect.html) for more information.
-   Use the [Data Crawler](/docs/services/discovery/data-crawler.html) if you want to have a managed upload of a significant number of files, or you want to extract content from a supported repository (such as a DB2 database).

## Adding content with the API or tooling

Consider the following when you are ready to add documents to your collection:

-   The maximum file size that can be uploaded to the {{site.data.keyword.discoveryshort}} service is 50MB.
-   The sample documents are not automatically added to the collection. You must add them if you want them as part of your collection.
-   Only the first 50,000 characters of each JSON field selected for enrichment will be enriched.
-   When creating a collection, you select the document language (English is the default). See [Language support](/docs/services/discovery/language-support.html) for the list of languages. Your documents will be enriched in the selected language. Do not mix languages within the same collection.
-   You can add Microsoft Word, PDF, HTML, and JSON documents to your collection. **Note:** PDFs that are scanned image files can not be converted and enriched.
-   The documents in your collection will be converted using the configuration file provided, which is named Default Configuration, unless you choose a different configuration file. For information about creating a configuration file, see [Custom configuration](/docs/services/discovery/building.html#custom-configuration).
-   When documents are uploaded to a data collection, they are converted and enriched using the configuration file chosen for that collection. If you decide later that you would like to switch a collection to a different configuration file, you can do that, but the documents that have already been uploaded will remain converted by the original configuration file. All documents uploaded after switching the configuration file will use the new configuration file. If you want the **entire** collection to use the new configuration, you will need to create a new collection, choose that new configuration file, and re-upload all the documents.
-   You cannot specify the `data type` (For example: `text` or `date`) of fields. During document ingestion, if a field is detected that does not yet exist in the index, {{site.data.keyword.discoveryshort}} will automatically detect the `data type` of that field based on the value of the field for the first document indexed.
-   A document can fail to be ingested because of a type mismatch between data in the current document and similar data in a previously ingested document. For example, a field might be typed as a `date` in one document and a `string` in a subsequent document, preventing the subsequent document from being indexed correctly.
-   If you plan to use custom tokenization (currently only available for Japanese collections when using the {{site.data.keyword.discoveryshort}} API), the tokenization dictionary for your collection must be added before uploading documents.

The following limits apply when uploading documents:

-   **Lite** plans: 21 in-flight documents
-   **Advanced** plans: 105 in-flight documents (except for X-Small Advanced plans, which have a limit of 50 in-flight documents)
-   **Premium** plans: 210 in-flight documents

These limits are subject to change. 

When using the Discovery service, uploading in-flight represents the document being uploaded and processed before it is added to the collection. If you reach your in-flight limit, you should slow down the rate of your ingestion. One option would be to add an automated back-off mechanism with retries.

## Uploading documents with the Discovery tooling

1.  Create a collection. See [Preparing the service for your documents](/docs/services/discovery/building.html#preparing-the-service-for-your-documents).
1.  Click on the collection to open it.
1.  Click the **Upload documents** button and start uploading your documents via drag and drop or browse.

Your documents are now enqueued to be converted and enriched. The time this takes will depend on the size of your collection. After it is indexed and enriched, the details of the Collection will be displayed in the **Overview** section.

-   **Created** and **Last updated** dates (Click **Use this collection in API** to see the `collection_id`, `configuration_id`, and `environment_id`.)
-   **Number of documents** in your collection
-   **Configuration** — The name of the configuration file used to convert this collection
-   **Errors and Warnings**

For information on how to connect to Box, Salesforce, and Microsoft SharePoint Online data sources with the {{site.data.keyword.discoveryshort}} tooling, see [Connecting to data sources](/docs/services/discovery/connect.html).


## Uploading documents with the API

See [Getting started with the {{site.data.keyword.discoveryshort}} API](/docs/services/discovery/getting-started.html) for a step-by-step tutorial.

For more information about the API, see the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/discovery){: new_window}.

1.  Use the `POST /v1/environments/{environment_id}/collections` method to create a collection.
1.  Then use the `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` method to add documents to your collection.

## Crawling URLs

You can crawl URLs and index them using the {{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} {{site.data.keyword.discoveryshort}} Service [Indexing plugin for Apache Nutch ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Watson/nutch-indexer-discovery). The crawl does not update automatically, so the procedure will need to be repeated periodically to keep the index up-to-date.
