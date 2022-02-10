---

copyright:
  years: 2020, 2022
lastupdated: "2022-02-10"

subcollection: discovery

---

{{site.data.keyword.attribute-definition-list}}

# Using the COVID-19 kit
{: #covidkit}

The COVID-19 kit is a special collection available in **US instances** of {{site.data.keyword.discoveryfull}}. This pre-built collection includes more than 10  data sources you can use to fuel a dynamic chatbot built with {{site.data.keyword.conversationfull}} and {{site.data.keyword.discoveryshort}} to answer your customers' questions about COVID-19.
{: shortdesc}

FAQ extraction is a beta feature that was used to create question and answer pairs for the kit. The FAQ extraction beta feature is now deprecated and will stop being supported in v1 Discovery service instances on 1 March 2022. As a consequence, the COVID-19 kit data collection will stop being supported also.
{: deprecated}

The COVID-19 kit extracts answers from trusted sources and automatically updates your chatbot as the content from those sources are updated. It uses FAQ extraction machine learning models developed by IBM Research labs to extract question/answer pairs. The kit is pre-configured with web crawl seeds from trusted sources such as the CDC, Harvard, and the United States Department of Labor. An expanded stopwords list and query expansions are also included in this collection to improve search results. It is designed to be augmented with your own data and customized to your needs. 

For more information about this kit, and how you can create a chatbot and connect it to a data source with the {{site.data.keyword.conversationfull}} search skill using {{site.data.keyword.conversationfull}} and {{site.data.keyword.discoveryshort}}, see [COVID-19 — Are Your Virtual Assistant’s Answers Up-To-Date?](https://medium.com/ibm-watson/covid-19-are-your-virtual-assistants-answers-up-to-date-c9e1ba70eb65#654b){: external}. 

To learn how to create a search skill in {{site.data.keyword.conversationshort}}, see [Creating a search skill](/docs/services/assistant?topic=assistant-skill-search-add). (This feature is available only to {{site.data.keyword.conversationshort}} **Plus** or **Premium** plan users.)

See the following to learn more about working with {{site.data.keyword.discoveryshort}}:
 
 - To learn how to create a service instance, see [Getting started with the {{site.data.keyword.discoveryshort}} tooling](/docs/discovery?topic=discovery-getting-started). Select `Washington, DC` or `Dallas` as the region for your instance. The COVID-19 kit is available in all pricing plans, including **Lite** plans. See [Discovery pricing plans](/docs/discovery?topic=discovery-discovery-pricing-plans) for details on each plan.
 - After you create your instance, click **Launch Watson Discovery**. On the **Manage data** screen, choose **Create COVID-19 kit** to create a collection that uses the pre-configured web sources. After the collection is created, click the **Sync settings** tab to view the names of the web sites in the collection. To learn more about working with collections, see [Managing collections](/docs/discovery?topic=discovery-sources#manage-collections).
 - You can create additional collections by uploading documents, crawling other websites, or connecting to other data sources (including Box, Salesforce, Microsoft SharePoint Online, Microsoft SharePoint 2016 On-Premise, and IBM Cloud Object Storage). See [Creating a collection using the tooling](/docs/discovery?topic=discovery-sources#source_tooling) and [Available data sources](/docs/discovery?topic=discovery-sources#available) for details.
 - To learn how to extract custom fields from your documents, see [Smart Document Understanding](/docs/discovery?topic=discovery-sdu).
 - You can automatically filter stopwords (words that add little value) out of queries. For details, see [Defining stopwords](/docs/discovery?topic=discovery-query-concepts#stopwords).
 - With query expansion, you can expand the scope of queries beyond exact matches. See [Query expansion](/docs/discovery?topic=discovery-query-concepts#query-expansion) for details.
 - By default, {{site.data.keyword.discoveryshort}} adds cognitive metadata to your documents with these four enrichments - Entity Extraction, Sentiment Analysis, Category Classification, and Concept Tagging. To learn more about these and other enrichments, see [Adding enrichments](/docs/services/discovery?topic=discovery-configservice#adding-enrichments).
 
See [IBM's response to Covid-19](https://www.ibm.com/impact/covid-19/?cm_sp=ThinkDigitalResources-_-CHQ-_-IBMCOVIDResponse){: external} for additional resources from IBM.
{: tip}
