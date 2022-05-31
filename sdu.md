---

copyright:
  years: 2015, 2021
lastupdated: "2021-06-23"

subcollection: discovery

---

{{site.data.keyword.attribute-definition-list}}

# Smart Document Understanding
{: #sdu}

Smart Document Understanding (SDU) trains {{site.data.keyword.discoveryfull}} to extract custom fields in your documents. Customizing how your documents are indexed into {{site.data.keyword.discoveryshort}} improves the answers that your application returns.

With SDU, you annotate fields within your documents to train custom conversion models. As you annotate, Watson is learning and starts to predict annotations. SDU models can be exported and used on other collections. 

This documentation applies to {{site.data.keyword.discoveryshort}} service instances that you create with a Lite or an Advanced plan, or that you created with a Premium plan before 16 July 2020. For more information about features in Premium plan instances created on or after 16 July 2020, and in Plus (including Plus Trial) plan instances, see [these docs](/docs/discovery-data?topic=discovery-data-configuring-fields){: external}.
{: important}

## Supported document types and browsers
{: #doctypes}

Supported document types for Smart Document Understanding: 
-  Lite plans: PDF, Word, PowerPoint, Excel, JSON\*, HTML\*
-  Advanced plans: PDF, Word, PowerPoint, Excel, PNG\*\*, TIFF\*\*, JPG\*\*, JSON\*, HTML\* 

\* JSON and HTML documents are supported by {{site.data.keyword.discoveryfull}}, but can not be edited using the SDU editor. To change the configuration of HTML and JSON docs, you need to use the API. For more information, see the [API reference](/apidocs/discovery/){: external}.

\*\* Individual image files (PNG, TIFF, JPG) are scanned and the text (if any) is extracted. PNG, TIFF, and JPEG images embedded in PDF, Word, PowerPoint, and Excel files are also scanned and the text, if any, is extracted.

## Using the Smart Document Understanding editor
{: #annotate}

<!-- Learn more topic WDS -->
The SDU editor is only available for collections that contain supported document types and do not have the Element Classification enrichment applied. If you do not want to use the SDU editor, you can set up your configuration using the API, see the [API reference](/apidocs/discovery/){: external}.
{: important}

The SDU editor functions are only available in the {{site.data.keyword.discoveryshort}} tooling, they are not available in the API.
{: note}

Navigating the Smart Document Understanding editor:

If you did not yet create a {{site.data.keyword.discoveryshort}} instance and environment, see [Getting started](/docs/discovery?topic=discovery-getting-started) for instructions.
{: tip}

1. On the **Manage Data** screen, click **Upload your own data**, and create a new private collection in {{site.data.keyword.discoveryshort}}.
1. Drag and drop documents into your collection, or click **select documents** to upload documents. After the upload is complete, this information displays:
   -  The fields identified from your documents.
   -  Enrichments applied to your documents. The Entity Extraction, Sentiment Analysis, Category Classification, and Concept Tagging enrichments are automatically applied to the `text` field by {{site.data.keyword.discoveryshort}} (unless you are importing documents using a connector). You can add (or remove) additional enrichments to the `text` (and other) fields.
   -  Pre-built queries you can run immediately.
1. Click **Configure data** on the upper right. On the **Configure data** screen, there are three tabs: **Identify fields**, **Manage fields**, and **Enrich fields**.

   - **Identify fields** contains the SDU editor. 
   - **Manage fields** lists all indexed fields (all fields are indexed by default). Switch off any fields you do not want to index. For example, your PDFs might contain a running header or footer that does not contain useful information, so you can exclude those fields from the index. You can also split documents here, based on fields, see [Splitting documents](/docs/discovery?topic=discovery-sdu#splitting).
   - **Enrich fields** is identical to the **Enrich** tab on the original screen. For more information about enrichments, see [Adding enrichments](/docs/discovery?topic=discovery-configservice#adding-enrichments). The **Upload sample documents** option is not available with SDU collections.

   If you did not upload any documents earlier, return to the **Overview** screen by clicking the name of your collection in the upper left, or click the ![Manage Data](/images/icon_yourData.png) icon and choose your collection. Drag and drop documents into your collection, or click **browse from computer**. After you initially upload your documents, the **Upload documents** button displays on the upper right.
   {: important}

1. Open the **Identify fields** tab. A subset of documents will be available for annotation purposes, between 20 - 50 documents will appear in the dropdown list. The number will depend on several factors, including the number of documents in your collection in the supported file formats.

You can use the toolbar at the top to complete the following actions:
- Choose a document to annotate
- Navigate the document displayed
- Adjust the page view (`single page view`, `zoom in`, `zoom out`), `clear changes`, and `export/import models`. Click on `single page view` to toggle the display - you can view your annotations and document separately, or together.

You can also crawl various data sources, or do a web crawl with the {{site.data.keyword.discoveryshort}} tooling. Click the **Connect a data source** button and see [Connecting to data sources](/docs/discovery?topic=discovery-sources) for more information. 
{: tip}

## Managing enrichments
{: #mng-enrichments}

You can enrich fields, including custom fields that Smart Document Understanding identifies, in your collection with cognitive metadata.

Many enrichments are available in {{site.data.keyword.discoveryshort}}. You must create some of the enrichments before you can apply them. To access the **Enrichments** tab, click **Manage data** in your collection and then **Configure data**. By default, the **Identify fields** tab opens. Click **Enrich fields**. For more information about collections, see [Connecting to data sources](/docs/discovery?topic=discovery-sources).

To apply an enrichment to a field, complete the following steps:

1. In the **Enrich fields** tab, look for the fields that you want to enrich in **Fields to be enriched**, and delete or **Add enrichments** from or to the field of your choice.
1. If there are any other fields that you want to enrich that are not yet listed in **Fields to be enriched**, enter them in **Add a field to enrich**, and add the enrichments.
1. Click **Apply changes to collection**.

## How to annotate a document
{: #documents}

See [Best practices for annotating documents](/docs/discovery?topic=discovery-sdu#bestpractices) before you begin annotating.

1.  Review the field labels that you can use to annotate the document. They are displayed in the *Field labels* panel.

    See the *Default field labels* table for a list of the fields and their descriptions. 
1.  To create a custom field label, click **Create new**. 

    The field label must consist of all lowercase letters with no spaces. For example, `my_field` is a valid field label.
    {: important}

    The number of custom fields you can add varies by plan type:
    
    - Lite: `0`
    - Advanced: `10`
    - Premium: `100`
1. Click a field label from the list to activate it.
1. Click the content representing that field in the SDU editor. The content highlights with the corresponding field label color.

   - Alternately, you can select a field label, and then drag it to the content in the SDU editor.
   - To clear a change, click the **Clear change** button on the toolbar.
1. Click **Submit page**.
   
   As you annotate, Watson is learning and starts to predict annotations. Continue annotating, until Watson correctly and consistently identifies fields.
   {: note}

1. After you finish annotating, click **Apply changes to collection.** The **Upload your documents** screen opens. Re-upload the documents in your collection. After uploading is complete, you are redirected to the **Overview** screen.

| Field | Definition |
|-------|------------|
| answer | In a Q/A pair (often in an FAQ), the answer to the question. |
| author | Name of author (or authors). |
| footer | Use this tag to denote meta-information about the document (such as the page number or references), that appear at the bottom of the |page. |
| header | Use this tag to denote meta-information about the document that appears at the top of the page. |
| question | In a Q/A pair (often in an FAQ), the question. |
| subtitle | The secondary title of the document being annotated. |
| table_of_contents | Use this tag on listings in the document table of contents. |
| text | Use this tag for standard copy text, including paragraphs, definitions, or any set of words that is not a title, part of a table, answer, author, subtitle, header, or a footer. |
| title | The main title of the document being annotated. |
| table |	Use this tag to annotate tables in your document. |
| image |	Use this tag to annotate images and diagrams in your document. |
{: caption="Default field labels" caption-side="top"}


## Splitting documents
{: #splitting}

<!-- Learn more topic WDS -->
The **Manage fields** tab contains the option to **Improve query results by splitting your documents**. This option allows you to split your documents into segments based on a field name. After the document splits, each segment is a separate document that is enriched, indexed, and returned as a separate query result.

Documents are split based on a single field name, for example: `title`, `author`, `question`. 

Considerations:

  - The number of segments per document is limited to `250`. Any document content remaining after `249` segments are stored within segment `250`.

  - Each segment counts towards the document limit of your plan. {{site.data.keyword.discoveryshort}} indexes segments, until the plan limit is reached. For document limits, see [Discovery pricing plans](/docs/discovery?topic=discovery-discovery-pricing-plans).

  - PDF and Word metadata, as well as any custom metadata, is extracted and included in the index with each segment. Every segment of a document includes identical metadata.

  - If a split document is updated and needs to be re-uploaded, consider replacing the document, using the [Update document](/apidocs/discovery#update-a-document){: external} method. Also, consider uploading the document, using the POST method of the `/environments/{environment_id}/collections/{collection_id}/documents/{document_id}` API, specifying the contents of the `parent_id` field of one of the current segments as the `{document_id}` path variable. All segments are overwritten, unless the updated version of the document has fewer total sections than the original. Those older segments remain in the index and can be individually deleted, using the API. For details, see the [API Reference](/apidocs/discovery#delete-a-document){: external}.

## Importing and exporting models
{: #import}

After you define a model with the SDU editor, you can save it and reuse it on other collections.

You can import or export your completed SDU model using the toolbar at the top of the editor. Click the last icon and choose `Import model` or `Export model`.

Exported models have the file extension of `.sdumodel`.

An imported model is intended to be used without any further annotations. If you continue annotating after importing it, the model is overwritten. If you plan to import a model into a new collection, it is a good best practice to create a new collection that contains only 1 document, import the model, then upload the remainder of your documents.

## Best practices for annotating documents
{: #bestpractices}

If you want to save time reprocessing all the files in a large collection, start with a small collection of documents, build your model, and then export it. For more information about importing and exporting models, see [Importing and exporting models](/docs/discovery?topic=discovery-sdu#import). Create a collection that contains only one document, import the model, and then upload the remainder of the documents.
{: tip}

- Follow all guidelines and use consistent labeling on all documents
- Do not label whitespace
- Use the `image` labels on images and diagrams
- Do not treat **bold**, _italic_, or underlined text differently. Label based on the context, not the style.
- When labeling a document, work from the first page to the last.
- If you incorrectly label an item, choose another label for the item to overwrite the first.
- Pages can be submitted at any time. Ensure that all appropriate labeling is complete before submitting.
- Documents that appear to have text overlaying other text are considered “double overlaid” and cannot be annotated. Report these documents to your administrator.
- Documents that contain multiple columns of text on a single page cannot be annotated. Report these documents to your administrator.
- Consider only labeling footnotes when they appear at the bottom of the page and are referenced in the main body of text in the document.
- Consider labeling notes that appear within sections or lists, for example notes that are explicitly called out as “Notes,” as `text`.
- When you annotate a table, make sure to select the entire table before you apply the `table` label.
- If the visual structure of one set of documents is drastically different from another, group the documents that are structured similarly in separate collections and then retrain each collection.