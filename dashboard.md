---

copyright:
  years: 2015, 2020
lastupdated: "2020-02-06"

subcollection: discovery

---

{{site.data.keyword.attribute-definition-list}}

# Viewing metrics and improving query results with the Performance dashboard
{: #performance-dashboard}

<!-- Learn more topic WDS -->
The Performance dashboard in the {{site.data.keyword.discoveryshort}} tooling can be used to view query metrics, as well as improve query results, including query relevance.

You can access the Performance dashboard by clicking the **View data metrics** icon. The dashboard is not available in Premium or Dedicated environments.

There are two options to improve natural language query results:
- [Fix queries with no results by adding more data](/docs/discovery?topic=discovery-performance-dashboard#addmore)
- [Bring relevant results to the top by training your data](/docs/discovery?topic=discovery-performance-dashboard#traindata)

You can view the data metrics in the [query overview](/docs/discovery?topic=discovery-performance-dashboard#overview). 

## Fix queries with no results by adding more data
{: #addmore}

In this section of the dashboard, you can review queries that returned zero results and add more data so that the query returns results in the future. Click the **View all and add data** button to get started. 

## Bring relevant results to the top by training your data
{: #traindata}

In this section, you can train your collections to improve the relevance of natural language query results. Click the **View all and perform relevancy training** button to get started. Then see [Adding queries and rating the relevancy of results](/docs/discovery?topic=discovery-improving-result-relevance-with-the-tooling#results) for instructions.

For more about training requirements and options, see [Improving result relevance with the tooling](/docs/discovery?topic=discovery-improving-result-relevance-with-the-tooling).

## Query overview
{: #overview}

The Query overview section displays:
- The total number of queries made by users
- The percentage of queries with one or more results clicked
- The percentage of queries with no results clicked
- The percentage of queries with no results returned
- A graph that displays these results over time, so that you can track how adding more data and relevancy training are improving performance

These results are gathered using the Events and Feedback API. See the [API reference](/apidocs/discovery#create-event){: external} for more information.