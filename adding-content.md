---

copyright:
  years: 2015, 2022
lastupdated: "2022-09-13"

subcollection: discovery

---

{{site.data.keyword.attribute-definition-list}}

# Adding content
{: #addcontent}

How do I decide which document upload method to use?
{: shortdesc}

This documentation applies to {{site.data.keyword.discoveryshort}} service instances that you create with a Lite or an Advanced plan, or that you created with a Premium plan before 16 July 2020. For more information about features in Premium plan instances created on or after 16 July 2020, and in Plus (including Plus Trial) plan instances, see [these docs](/docs/discovery-data?topic=discovery-data-upload-data){: external}.
{: important}

-   Use the [API](/docs/discovery?topic=discovery-gs-api) if you are integrating the upload of content with an existing application or creating your own custom upload mechanism.
-   Use the [{{site.data.keyword.discoveryshort}} tooling](/docs/discovery?topic=discovery-getting-started) if you want to quickly upload locally accessible files.
    When uploading documents using the {{site.data.keyword.discoveryshort}} tooling, all documents must have a unique file name. If two files have the same name, the original is overwritten when the newer version is uploaded. If you would prefer that documents with the same file name coexist in your collection, the Document ID needs to be specified. You can specify the Document ID if you upload documents using the API.
-   Use the {{site.data.keyword.discoveryshort}} tooling or API to connect to Box, Salesforce, Microsoft SharePoint Online, IBM Cloud Object Storage, and Microsoft SharePoint 2016 data sources, or do a web crawl. See [Connecting to data sources](/docs/discovery?topic=discovery-sources) for more information.

You can use an IBM App Connect default connector to send data from a large set of popular data sources to {{site.data.keyword.discoveryshort}} by creating flows within the App Connect tooling. Note that creating a separate App Connect instance is required to use this App Connect default connector and that any costs that you incur when you use a paid App Connect instance are not included with the cost for using {{site.data.keyword.discoveryshort}}. Additionally, except for indexing, {{site.data.keyword.discoveryshort}} does not support any integration with App Connect that you perform on your own. For information about integrating App Connect with {{site.data.keyword.discoveryshort}} or for integration support or questions, see [How to use IBM App Connect with {{site.data.keyword.discoveryfull}}](https://www.ibm.com/support/knowledgecenter/SS6KM6/com.ibm.appconnect.dev.doc/how-to-guides-for-apps/watson-discovery.html){: external}. For the available data sources that you can use with the App Connect default connector to send data to {{site.data.keyword.discoveryshort}}, see [Connectors A-Z](https://www.ibm.com/cloud/app-connect/connectors/){: external}.


## Adding content with the API or tooling
{: #adding-content-with-the-api-or-tooling}

Consider the following when you are ready to add documents to your collection:

-   The maximum file size that can be uploaded to {{site.data.keyword.discoveryshort}} is 50MB.
-   Only the first 50,000 characters of each JSON field selected for enrichment are enriched.
-   A maximum of 1,000 fields can be added to the document index.
-   When creating a collection, you select the document language (English is the default). See [Language support](/docs/discovery?topic=discovery-language-support) for the list of languages. Your documents are enriched in the selected language. Do not mix languages within the same collection.
-   The following file types can be ingested by {{site.data.keyword.discoveryshort}}, all other document types are ignored:

Lite plans | Advanced plans 
------------------------------ | ------------------------------------------- 
PDF, Word, PowerPoint, Excel, JSON\*, HTML\* | PDF, Word, PowerPoint, Excel, PNG\*\*, TIFF\*\*, JPG\*\*, JSON\*, HTML\* 


\* JSON and HTML documents are supported by {{site.data.keyword.discoveryfull}}, but can not be edited using the SDU editor. To change the configuration of HTML and JSON docs, you need to use the API. For more information, see the [API reference](/apidocs/discovery/){: external}.

\*\* Individual image files (PNG, TIFF, JPG) are scanned and the text (if any) is extracted. PNG, TIFF, and JPEG images embedded in PDF, Word, PowerPoint, and Excel files are also scanned and the text (if any) extracted.

-   You cannot specify the `data type` (For example: `text` or `date`) of fields. During document ingestion, if a field is detected that does not yet exist in the index, {{site.data.keyword.discoveryshort}} automatically detects the `data type` of that field based on the value of the field for the first document indexed.
-   A document can fail to be ingested because of a type mismatch between data in the current document and similar data in a previously ingested document. For example, a field might be typed as a `date` in one document and a `string` in a subsequent document, preventing the subsequent document from being indexed correctly.
-   If you plan to use custom tokenization (currently only available for Japanese collections when using the {{site.data.keyword.discoveryshort}} API), the tokenization dictionary for your collection must be added before uploading documents.

## Uploading documents with the Discovery tooling
{: #upload_tooling}

1.  Create a collection. See [Preparing the service for your documents](/docs/discovery?topic=discovery-configservice#preparing-the-service-for-your-documents).
1.  Click on the collection to open it.
1.  Click the **Upload documents** button and start uploading your documents via drag and drop or browse.

Your documents are now enqueued to be converted and enriched. The time this takes depends on the size of your collection. After it is indexed and enriched, the details of the collection are displayed in the **Overview** section.

-   **Fields identified** in your collection.
-   **Created** and **Last updated** dates (Click **Use this collection in API** to see the `collection_id`, `configuration_id`, and `environment_id`.)
-   **Number of documents** in your collection
-   **Errors and Warnings**

For information on how to connect to various data sources, or do a web crawl with the {{site.data.keyword.discoveryshort}} tooling, see [Connecting to data sources](/docs/discovery?topic=discovery-sources).


## Uploading documents with the API
{: #upload_api}

See [Getting started with the {{site.data.keyword.discoveryshort}} API](/docs/discovery?topic=discovery-gs-api) for a step-by-step tutorial.

For more information about the API, see the [API reference](/apidocs/discovery/){: external}.

1.  Use the `POST /v1/environments/{environment_id}/collections` method to create a collection.
1.  Then use the `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` method to add documents to your collection.

## Crawling URLs
{: #crawl_urls}

You can crawl URLs and index them using the Web Crawl connector. See [Connecting to data sources](/docs/discovery?topic=discovery-sources#connectwebcrawl).

## Troubleshooting ingestion issues
{: #adding-ts}

Learn about steps you can take to mitigate issues that you might encounter when you are adding documents.

-   Microsoft Office document is too large

    If a document is large or complex, the step in the ingestion process that extracts the document structure can take too long to complete. If a message is displayed that indicates that a `document is too large for content structure extraction` to occur, decrease the size of the document. To decrease the document size, you can split the document into many smaller documents. For example, if you are adding an Excel spreadsheet, split a large XLXS file by sheets or rows into several smaller XLXS files. For a DOC file, split the document by pages. How small should each chunk of the document be? There is no one size that is best for all documents; it depends on the document. Aim to make each chunk as small as possible, while keeping plan-based document limits in mind.
