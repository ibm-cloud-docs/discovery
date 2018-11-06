---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-10"

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

# Smart Document Understanding

Smart Document Understanding (SDU) is a new way to annotate your documents within {{site.data.keyword.discoveryfull}}. 

The editor makes it simpler to train custom conversion models. Customizing how your documents are indexed into Discovery will improve the answers returned for your application.

SDU is in beta release. A statement explaining beta features can be found [here](/docs/services/discovery/release-notes.html#beta-features).

## Supported document types and browsers
{: #doctypes}

Supported document types: PDF, Word, HTML. JSON documents are supported by {{site.data.keyword.discoveryfull}}, but do not open in the SDU editor, because they are structured documents.

Supported browsers for this beta release: Chrome and Firefox

## How to annotate your documents
{: #annotate}

To open the Smart Document Understanding editor:

1. Open {{site.data.keyword.discoveryfull}} using the beta link.
1. Open a Private data collection, and on the **Manage Data** screen, click **Go to Data Settings**. 
1. On the **Data Settings** screen, there will be two tabs: **Extract fields** and **Enrich fields**.

   - **Extract fields** contains the SDU editor. This tab replaces both the **Convert** and **Normalize** tabs on your original {{site.data.keyword.discoveryshort}} screen. 
   - **Enrich fields** is identical to the **Enrich** tab on the original screen. For more information about enrichments, see [Adding enrichments](/docs/services/discovery/building.html#adding-enrichments). The **Upload sample documents** option is not available on the **Enrich fields**, because it is not necessary.

1. Twenty (20) documents from your collection will automatically load under the **Extract fields** tab, in the Smart Document Understanding editor.

The toolbar at the top will allow you to:
- Choose a document
- Navigate the document displayed
- Adjust the page view (`single page view`, `zoom in`, `zoom out`), `clear changes`, and `export/import models`. Click on `single page view` to toggle to a screen that will display your annotations and document separately. 

### Annotating a document in the SDU editor
{: #documents}

**Note:** Tables are annotated in a separate step.

See [Best practices for labeling documents and tables](/docs/services/discovery/sdu.html#bestpractices) before you begin annotating.

1. A default set of fields will appear to the right of your document. (For the beta, you cannot create custom fields, but this feature will be available in the future.) The available fields are `answer`, `author`, `footer`, `header`, `question`, `subtitle`, `table_of_contents`, `text`, and `title`.
1. Click on a field name on the right to activate it.
1. Click on the content representing that field in the SDU editor. It will highlight. 
   - Alternately, you can select a field name on the right, and drag it to the content in the SDU editor. 
   - To clear a change, click the **Clear change** button on the toolbar.
1. Click **Submit**.
   **Note:** As you annotate, Watson is learning and will start predicting annotations. Continue annotating until Watson correctly and consistently identifies fields.
1. When you have completed annotating, click **Apply changes to collection.** The **Upload your documents** screen opens. (This will change after beta.) You can now upload your documents so that the updated settings are applied to the entire collection. After uploading is complete, you will be redirected to the **Manage Data** screen.

Field | Definition  
------ | ------ 
answer | In a Q/A pair (often in an FAQ), the answer to the question.
author | Name of author (or authors).
footer | Use this tag to denote meta-information about the document (such as the page number or references), that appear at the bottom of the page.
header | Use this tag to denote meta-information about the document that appears at the top of the page.
question | In a Q/A pair (often in an FAQ), the question.
subtitle | The secondary title of the document being annotated. Use this label only once per document.
table-of-contents | Use this tag on listings in the document table of contents.
text | Use this tag for standard copy text, including paragraphs, definitions, or any set of words that is not a title, part of a table, answer, author, subtitle, header, or a footer. 
title | The main title of the document being annotated. Use this label only once per document.

### Annotating a table in the SDU editor
{: #tables} 

1. Select the `table` field on the right, then select the table in the SDU editor. 
1. Hover over the table in the SDU editor to display the **Annotate table** button. Click the button to open the table editor.
1. First, outline the table:
   - Select the `column` field.
   - Click on a column in the table to activate it.
   - Select the `row` field.
   - Click on a row in the table to activate it.

   The outline of the table will appear in the table preview on the left.

   **Note:** You can click **Predict** to view a model prediction of your table annotation.
1. Second, label the content within the table.
1. When you have completed annotating the table, click **Done annotating**.
1. Click **Apply changes to collection.** The **Upload your documents** screen opens. (This will change after beta.) After uploading is complete, you will be redirected to the **Manage Data** screen.

Field | Definition  
------ | ------ 
table body | Any non-header cell containing information
column header | The heading cell (if present) for each column in the table 
multi-column header | Any heading cell that spans more than one column
subsection title | The column header for the column of row headings (if present)
row header | The row label (if present) for each row in the table
multi-row header | Any row label that spans more than one row

## Best practices for labeling documents and tables
{: #bestpractices}

- Follow all guidelines and use consistent labeling on all documents
- Do not label whitespace
- Do not label diagrams and images
- Do not treat **bold**, _italic_, or underlined text differently, label based on the context, not the style. 
- When labeling a document, work from the first page to the last. Each page must be submitted, even if nothing has been labeled. 
- If you incorrectly label an item, choose another label for the item to overwrite the first.
- Pages can be submitted at any time. Ensure that all appropriate labeling is complete before submitting.
- Do not use the zoom function on your browser when labeling documents.
- Documents and tables that appear to have text overlaying other text are considered “double overlaid” and cannot be annotated. Report these documents to your administrator.
- Documents and tables that contain multiple columns of text on a single page cannot be annotated. Report these documents to your administrator.
- Footnotes should be marked as only when they appear at the bottom of the page and are referenced in the main body of text in the document.
- Notes appearing within sections or lists (e.g., explicitly called out as “Notes”) should be labeled as `text`.
- If you are unsure that the table has been labeled correctly and the preview pane has become unresponsive, the page should be reloaded in your browser and the table re-labeled in order to ensure correctness.

