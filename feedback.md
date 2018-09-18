---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-17"

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

# Usage monitoring
{: #usage}

You can monitor and track usage of your {{site.data.keyword.discoveryshort}} instance and use this data to help you understand and improve your applications. The [Events API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#events-and-feedback-api){: new_window} can be used to create log entries that are associated with specific natural language queries and actions. For example, you can record which documents in a results set were "clicked" by a user, and when that click occurred.

**Note:** Logs and events are monitored only for natural language queries on private data collections. No logs are gathered on {{site.data.keyword.discoverynewsfull}}.

{{site.data.keyword.discoveryshort}} can log the following information:
- **Queries** - Natural language queries run against collections in your environment 
- **Impressions** (or **Results**) -  The results returned for a particular query, usually documents or passages 
- **Events** - Interactions a user performs on a result or set of results in {{site.data.keyword.discoveryshort}} (for example, a click on a document result)

**Queries** and **Impressions** are logged automatically; **Events** logging can be integrated into your application via the API.

## Viewing the logs
{: #viewlogs}

You can search the query and event log to find query sessions that match the specified criteria. Searching the `logs` endpoint uses the standard {{site.data.keyword.discoveryshort}} query syntax for the parameters that are supported. The endpoint provides basic query functionality for viewing and searching through the recorded data.  

The `/api/v1/logs` endpoint supports the following {{site.data.keyword.discoveryshort}} query parameters.
- query 
- filter
- sort
- count 
- offset
- version

For additional details on the function and syntax for the parameters see [Query parameters](/docs/services/discovery/query-parameters.html).

Example of searching logs for a natural language query that contains the term “train”:

`https://gateway.watsonplatform.net/discovery/api/v1/logs?version=2018-03-28&query=train`

The response of a `logs` query includes results that appear similar to {{site.data.keyword.discoveryshort}} document results. Each result will either be a query or event, specified in the document `type` field.  

Example query log:

```
{
            "customer_id": "",
            "environment_id": "252e6e82-c2d2-450e-9670-0008b0a3a99c",
            "natural_language_query": "how do i get from the airport to the city",
            "query_id": "_Qs35yOoa7",
            "document_results": {
                "count": 2,
                "results": [
                    {
                        "collection_id": "af9e1f41-6114-4d77-bca6-c9b99b2601b1",
                        "score": 6.724753491503856,
                        "position": 1,
                        "document_id": "4193eaa727d79b0f74597356dbcbb9a7"
                    },
                    {
                        "collection_id": "af9e1f41-6114-4d77-bca6-c9b99b2601b1",
                        "score": 5.791631414211986,
                        "position": 2,
                        "document_id": "bdcd6a9cc1438a3faa8c925f6a8d9429"
                    }
                ]
            },
            "event_type": "query",
            "session_token": "1_LKczxWGEWx5TJAi1_Qs35yOoa7",
            "created_timestamp": "2018-09-12T05:20:07.469Z"
        }
```

With query logs you can investigate the type of results returned to your end users and investigate ways to improve result quality using the approaches available in {{site.data.keyword.discoveryshort}}. For example: 
- relevancy training, see [Improving result relevance with the API](/docs/services/discovery/train.html) and [Improving result relevance with the tooling](/docs/services/discovery/train-tooling.html)
- [query operators](/docs/services/discovery/query-operators.html)
- [query expansion](/docs/services/discovery/using.html#query-expansion)
- custom configurations, see the [Configuration reference](/docs/services/discovery/custom-config.html)

## Creating event logs
{: #eventlogs}

Event logs are used to track the interactions of users within your application. This can help you understand how well your application is performing, as well as identify areas you may need to focus on to improve results. {{site.data.keyword.discoveryshort}} provides an API that can be embedded in your application to track events. Calling this API with the appropriate information when a user performs an action sends a signal back to {{site.data.keyword.discoveryshort}}, which can then be viewed in the logs. 

Events can help gather information on computing metrics (like clickthrough rate) to measure how effective the application is at helping end users find relevant information, or can be used to help seed training by reviewing the queries and clicks to start to build ground truth. 

You can add this API wherever users interact with your results. For example, in a search UI you may want to add it when a user clicks on a document link, or in a chatbot interface you may want to use it to track when the user clicks on an **Expand** or **More details** button.

{{site.data.keyword.discoveryshort}} results will return additional information that can be used for tracking events, including a session token. 

`"matching_results": 179,`
`"session_token": "1_LKczxWGEWx59fYD0_VV8HFUpb6"`

To record an event, make a POST to the `/api/v1/events` endpoint. See the 
[Events API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#events-and-feedback-api){: new_window} for details.

Once an event is recorded, it can be read back out using the `/api/v1/logs` endpoint. Join events to the associated query using the `session_token`.