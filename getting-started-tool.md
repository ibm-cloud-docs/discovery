---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-01-22"

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

# Getting started

In this short tutorial, we introduce the {{site.data.keyword.discoveryshort}} tooling and go through the process of creating a private data collection and searching it.
{: shortdesc}

If you prefer to work in the API, see [Getting started with the API](/docs/services/discovery/getting-started.html).
{: tip}

## Before you begin
{: #before-you-begin}
{: hide-dashboard}

You need a service instance to start.
{: hide-dashboard}

1.  {: hide-dashboard} Go to the [{{site.data.keyword.discoveryshort}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/catalog/services/discovery) page in the {{site.data.keyword.cloud_notm}} catalog.

    The service instance is created in the **default** resource group if you do not choose a different one, and it *cannot* be changed later. This group is sufficient for the purposes of trying out the service.

    If you're creating an instance for more robust use, then learn more about [resource groups ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/docs/resources/bestpractice_rgs.html#bp_resourcegroups){: new_window}.
1.  {: hide-dashboard} Sign up for a free {{site.data.keyword.cloud_notm}} account or log in.
1.  {: hide-dashboard} Click **Create**.

## Step 1: Launch the tooling
{: #launch-the-tooling}

After you create an instance of the {{site.data.keyword.discoveryshort}} service, you're taken to your list of services.
{: hide-dashboard}

1.  {: hide-dashboard} Click the {{site.data.keyword.discoveryshort}} service instance you created to go to the service dashboard.
1.  On the **Manage** page, click **Launch tool**. If you're prompted to log in to the tooling, provide your {{site.data.keyword.cloud_notm}} credentials.

<!-- To do: Add screenshot for developer console -->

## Step 2: Create a collection
{: #create-a-collection}

Your first step in the {{site.data.keyword.discoveryshort}} tooling is to create a data collection.

A collection is a set of your documents. *Why would I want more than one collection?* There are a few reasons:

- You might want multiple collections in order to separate results for different audiences.
- The data might be so different that it doesn't make sense for it all to be queried at the same time.

The public, pre-enriched {{site.data.keyword.discoverynewsshort}} data collection is also available for your use. It is ready to query, and you can begin to create queries on it immediately. You cannot adjust its configuration or add documents to {{site.data.keyword.discoverynewsshort}}.

1.  Click ![Environment details](images/env_icon.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> and choose **Create environment**.
1.  When your environment is ready, click the **Upload your own data** button, then you can **Name your new collection**. Name your collection. 

    {{site.data.keyword.discoveryshort}} will enrich (add cognitive metadata to) the `text` field of your documents with semantic information collected by four {{site.data.keyword.watson}} Enrichments — Entity Extraction, Sentiment Analysis, Category Classification, and Concept Tagging (learn more about them [here](/docs/services/discovery/building.html#adding-enrichments)). Standard document conversions based on font styles and sizes will also be applied. You can adjust the enrichments later, using the **Overview** tab. (This configuration is named **Default Configuration** in collections created before the release of [Smart Document Understanding](/docs/services/discovery/sdu.html).)

    There is a configuration file available named **Default Contract Configuration** that supports Element Classification, which can be used to extract party, nature, and category from elements in PDFs. Choose it only if you wish to use this enrichment. See [Element Classification](/docs/services/discovery/element-classification.html#element-collection) for details.

You can also crawl Box, Salesforce, Microsoft SharePoint Online, and Microsoft SharePoint 2016 data sources, or do a web crawl with the {{site.data.keyword.discoveryshort}} tooling. Click the **Connect a data source** button and see [Connecting to data sources](/docs/services/discovery/connect.html) for more information.
{: tip}

## Step 3: Create a custom configuration
{: create-custom-configuration}

After your collection is created, you could immediately start uploading content using the upload area, but we want to create and test a custom configuration.

1.  Click **Switch** next to the collection name and choose **Create a new configuration**. Name your configuration and click **Create**.
1.  After you create your configuration, you can customize it:
    1.  Download the <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a> sample document.
    1.  Use the **Upload Sample Documents** panel to upload the sample document. After it uploads, you can click the document name link to view the transformation.
1.  Now it's time to adjust the configuration. For this task, you change the enrichments that are applied to each document:
    1.  Click on the **Enrich** section of the configuration. Look at the generated JSON to the right of the screen. Scroll down to the *enriched_text* section and notice that it contains many *concepts*.
    1.  Next, remove the text enrichment named *concepts* by clicking the **X** next to it and then click **Apply & Save**.
    1.  Finally, look at the JSON again. Notice how the output has changed and no longer includes *concepts*.

## Step 4: Upload your documents
{: #upload-your-documents}

When you're happy with the custom conversion of your sample document it's time to ingest the real content into your collection.

1.  Download these three sample documents: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>.
1.  Click ![File icon](images/icon_yourData.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> and select your collection.
1.  Make sure the custom configuration you created is listed under **Configuration**. If it isn't, click **Switch** next to the configuration name and select it.
1.  Click the **Upload documents** button and start uploading the four sample documents: test-doc1.html, test-doc2.html, test-doc3.html, test-doc4.html.
1.  Wait for the documents to upload. The status of your documents display in the **Overview** section.

## Step 5: Build a query
{: #build-a-query}

1.  Click ![Query icon](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> to open the query page. Select your collection and click **Get started**.
1.  On the **Build queries** screen, click **Search for documents**, then **Use the {{site.data.keyword.discoveryshort}} Query Language**:
    - To search for results with entities named "IBM":
        1.  Click **Field** and select `enriched_text.entities.text`. Select `contains` for **Operator** and `IBM` for **Value**. The query `enriched_text.entities.text:IBM` is displayed in **Visual Query Builder**.
        1.  Click **Run Query**. The query returns 4 results.
    - To search for results with entities named "Watson":
        1.  Click **Field** and select `enriched_text.entities.text`. Select `contains` for  **Operator** and `watson` for **Value**. The query `enriched_text.entities.text:watson` is displayed in **Visual Query Builder**.
        1.  Click **Run Query**. The query returns 2 results.
    - To search for results with both entities named "Watson" and "Slack":
        1.  Click **Field** and select `enriched_text.entities.text`. Select `contains` for **Operator** and `watson` for **Value**. Click **Add rule**, then repeat your selections, but choose the **Value** of `Slack`. The query `enriched_text.entities.text:watson,enriched_text.entities.text:Slack` is displayed in **Visual Query Builder**.
        1.  Click **Run Query**. The query returns 1 result.

    Click **Edit in query language** to build queries using the {{site.data.keyword.discoveryshort}} Query Language. To learn more about the {{site.data.keyword.discoveryshort}} Query Language, see [Query reference](/docs/services/discovery/query-reference.html) and [Query concepts](/docs/services/discovery/using.html).
1.  The results of your query are displayed in the **Results** section:
    - The **Summary** tab provides an overview of the query results,
    - The **JSON** tab displays the full JSON results.

    For the queries listed, the **Summary**  displays the document passages (in order of relevance) first, followed by the names of the documents found, then the results by enrichment. **Passages** are short, relevant excerpts extracted from the full documents returned by your query.

    The **Query URL** link provided under both the **JSON** and **Summary** tabs is ready-to-use in your application.

    You can also click **Use natural language** and write a natural language query, such as "IBM Watson partnerships". To learn more about natural language queries, see [Natural language query](/docs/services/discovery/query-parameters.html#nlq).

    Watson can be trained to improve the results of natural language queries, see [Improving result relevance with the tooling](/docs/services/discovery/train-tooling.html).

    Additional resources:
    - To learn more about the data schema of your documents, click the **View Data Schema** icon or click on the **JSON** tab. See [The Discovery data schema](/docs/services/discovery/using.html#discovery-schema) for details.
    - If editing in the {{site.data.keyword.discoveryshort}} Query Language, click the **Use a sample query** for example queries.

## Next steps
{: #next-steps}

Now you have a functioning and populated {{site.data.keyword.discoveryshort}} service instance. You can now begin customizing your collection by adding more documents and enrichments, customizing conversion settings, or using [Smart Document Understanding](/docs/services/discovery/sdu.html).
