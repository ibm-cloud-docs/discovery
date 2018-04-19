---

copyright:
  years: 2015, 2018
lastupdated: "2018-04-17"

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

# Watson Discovery Visual Insights
{: #visual-insights}

{{site.data.keyword.discoveryfull}} Visual Insights is an experimental feature that you can use to visually explore connections identified by {{site.data.keyword.discoveryshort}}'s understanding of semantic elements, relations, concepts, and more.

You can use {{site.data.keyword.discoveryfull}} Visual Insights to learn more about your collections, before using {{site.data.keyword.discoveryshort}} to create queries that you can integrate into your new application or existing solution that will point users to the information they need.

During the experimental release, Visual Insights is only available in public environments.

**Disclaimer:** Visual Insights is an experimental feature, which means it can be unstable, can change frequently, and can be discontinued with short notice. It is provided so you can evaluate its functionality. It may not provide the same level of performance or compatibility that generally released capabilities provide. It is not designed for use in a production environment, and any such use is at your own risk. See [Beta/Experimental features](/docs/services/discovery/release-notes.html#beta-features) for details.

This feature is currently supported in English only, see [Language support](/docs/services/discovery/language-support.html#feature-support) for details.

## A quick tour of Visual Insights
{: #quick-tour-visual-insights}

![Discovery visual insights quick tour](images/discovery-visualinsights-quicktour.png)

The Visual Insights screen is divided into 4 main areas.

### Search bar
{: #search-bar}

You can query {{site.data.keyword.discoveryshort}} collections using the **Search bar** at the top.

- If you have logged in with your {{site.data.keyword.Bluemix_notm}} credentials, all the collections from the {{site.data.keyword.discoveryshort}} instances associated with your account will be available from the collection drop-down ({{site.data.keyword.discoverynewsfull}} by default). If you are not logged in, only the {{site.data.keyword.discoverynewsfull}} collection will be available.
- Choose your collection, enter your query (for example, `What is net neutrality`) in the search box, and click the **search** button to search. For large collections, it could potentially take a minute or more before results are displayed. You can filter your search by clicking the `documents`, `concepts`, `people`, `locations`, `organizations`, or `companies` buttons.
- You can optionally select any item in the displayed results (entity, concept, or document) by clicking on the ![Query icon](images/discovery-query-icon.png) icon in the header.
- If a private collection is selected and no query has been entered, up to 1000 documents from the collection will be displayed in the [Details pane](/docs/services/discovery/visual-insights.html#details-pane). If the {{site.data.keyword.discoverynewsshort}} collection is chosen and no query has been entered, a selection of 100 recent articles will be displayed.

### Network display
{: #network-display}

The center panel beneath the search bar is the **Network display**. This is the interactive visualization of your query results.

- The **Network display** is a graphical representation of the documents, entities, and concepts extracted from the query results. The pink nodes represent documents; the blue ones represent entities or concepts. Each document node is linked to all the entity and concept nodes that were detected in that document by {{site.data.keyword.discoveryshort}}. The more similar documents are, the closer they will be located to each other in the visualization.
- Hovering over any node in the **Network display** will display its associated title and highlight its links to other nodes.
- Clicking on any node will display information about that node in the [Details pane](/docs/services/discovery/visual-insights.html#details-pane).

### Details pane
{: #details-pane}

To the right of the Network display is the **Details pane**.

- The Details pane provides more details about each document, including its classification and date (if available), a brief excerpt (with the option to open the full document), as well as the entities and concepts it is linked to.
- If a non-document node has been selected in the Network display, information about that node will display at the top of the Details pane.
- Clicking on any of the linked entities or concepts in the Details pane will select the corresponding node in the Network display.

### Navigation pane
{: #navigation-pane}

To the left of the Network display is the **Navigation pane**. This pane provides a tag cloud overview of the most common terms extracted from the query results in the chosen collection. The larger the term, the more common it is in the query results.

- Selecting any term in the tag cloud will turn it pink, and highlight any documents in the Network display that are associated with it. The Details pane will display the list of highlighted documents. The other terms in the tag cloud will now indicate their relationship to the selected term:
  - Grayed out terms are not associated with any of the highlighted documents.
  - If a term turns violet, it is associated with all the highlighted documents, and will not be helpful if trying to distinguish among the documents.
  - Terms that remain blue are associated with some, but not all, of the highlighted documents, and can thus be used to further refine the set of highlighted documents. Selecting one of these terms will reduce the set of highlighted documents to only those that are associated with both tags and zoom the network display down to the region where those documents are located. This method can be used to refine large set of documents down to a smaller set with just a few clicks.
- To unselect a selected term, click the term again.  To clear all selected terms, click on a blank spot between the words in the tag cloud. Clicking on a gray tag will clear the existing selection and select that term.
- The types and counts of the documents, people, concepts, organizations, locations, and companies are displayed above the tag cloud. Click on any of them to filter the tag cloud and the Network display visualization.

## Using Visual Insights
{: #using-visual-insights}

You can use Visual Insights to query {{site.data.keyword.discoverynewsfull}} without logging in. In order to use Visual Insights with your own collections, you will need:

- An {{site.data.keyword.Bluemix_notm}} account that contains a {{site.data.keyword.discoveryshort}} instance.
- One or more collections in that {{site.data.keyword.discoveryshort}} instance that have been enriched with the [Entity extraction](/docs/services/discovery/building.html#entity-extraction) enrichment, plus optionally any of the [Concept tagging](/docs/services/discovery/building.html#concept-tagging), [Keyword extraction](/docs/services/discovery/building.html#keyword-extraction), [Relation extraction](/docs/services/discovery/building.html#relation-extraction), and [Category classification](/docs/services/discovery/building.html#category-classification) enrichments. Other enrichments may be included, but will not be represented by Visual Insights.
- Visual Insights can visualize collections consisting of any combination of PDF, HTML, Word, and JSON documents with an enriched `text` field.

More information about {{site.data.keyword.discoveryshort}} and how to get started for free, see [Watson {{site.data.keyword.discoveryshort}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/services/discovery/){: new_window}.

Once you have an {{site.data.keyword.Bluemix_notm}} account, a {{site.data.keyword.discoveryshort}} instance, and one or more collections populated, you will see your collections in Visual Insights when you log in.

Logging into Visual Insights

1. Open {{site.data.keyword.discoveryshort}} Visual Insights. Choose the region your collections are stored in:
   - [US South ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://visual-insights.bluemix.net){: new_window}.
   - [Germany ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://visual-insights.eu-de.bluemix.net/){: new_window}.
   - [Sydney, Australia ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://visual-insights.au-syd.bluemix.net/){: new_window}.
   - [United Kingdom ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://visual-insights.eu-gb.bluemix.net/){: new_window}.

1. Click on the ![Profile icon](images/discovery-profile-icon.png) icon in the Search bar.
1. Enter your {{site.data.keyword.Bluemix_notm}} id and password. In a few moments your collections will be available for selection in the Search bar.

## Providing feedback
{: #providing-feedback}

We are interested in your feedback on {{site.data.keyword.discoveryshort}} Visual Insights. To access the feedback link, click the ![Info icon](images/discovery-info-icon.png) icon in the header.
