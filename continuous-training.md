---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-25"

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

# Continuous Relevancy Training
{: #crt}

{{site.data.keyword.discoveryshort}} Continuous Relevancy Training can learn from user behavior automatically, significantly reducing the effort required to improve the relevancy ranking of results. It uses interactions from users to learn how to surface the most relevant results. It can learn from interactions like clicks to determine which results are most valuable for users and uncover the most important signals for future queries. Continuous Relevancy Training will rerank documents to surface the most relevant information at the top of the results. It can be used to:

- Help improve the relevance of results for support agents, based on the results they click on
- Display more relevant results in a customer chatbot based on the long-tail results selected 
- Provide experts with more relevant responses, based on the results they explore

To setup Continuous Relevancy Training:

- Because {{site.data.keyword.discoveryshort}} `events` (clicks) are used to create the training data needed, first integrate event tracking. See [Usage monitoring](/docs/services/discovery/feedback.html#usage) for details.
- A minumum of 1000 natural language queries with an associated click event are required for Continuous Relevancy Training to start. Events and logs are retained for 30 days across your instance so the 1000 clicks must be collected during that time period.

To use Continuous Relevancy Training:

Continuous Relevancy Training can be used at query time by running a multi-collection `natural_language_query` across all collections in your environment. See [Querying multiple collections](/docs/services/discovery/using.html#multiple-collections) for instructions. 

**Note:** Querying a single trained collection that is explicitly provided through the `/api/v1/training_data` endpoint or {{site.data.keyword.discoveryshort}} tooling is unchanged. 

Tracking status:

The status of Continuous Relevancy Training can be viewed from the `/api/v1/environments` endpoint. See the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#environments-api){: new_window}. `status` will provide information on the state of the training operations and will inform you if Continuous Relevancy Training is active:

```
"search_status" : [
        {
            "scope" : "environment",
            "status" : "NO_DATA",
            "status_description" : "Discovery is employing a default strategy for document search natural_language_query. Enable query and event logging so we can initiate relevancy training to improve search accuracy.”
        }
    ]
```

Continuous Relevancy Training limitations:

- Since Continuous Relevancy Training works across multiple collections, both query and training times may be extended. 
- Continuous Relevancy Training is available for Advanced plans size `Small` or larger, and Premium plans. It is not available for Lite plans.