---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-18"

subcollection: discovery

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

# Query performance
{: #qp}

Query performance in {{site.data.keyword.discoveryshort}} is dependent on a number of factors. 

## Evaluating performance 
{: #qp-evaluate}

If you expect high simultaneous load on your application, it is important to evaluate the performance of your {{site.data.keyword.discoveryshort}} application. There are several dimensions commonly used to measure performance:
1.  **Response latency** - The time it takes for {{site.data.keyword.discoveryshort}} to return the results of your query. 
    - Latency can vary depending on a number of factors, see [Factors that impact performance](/docs/services/discovery?topic=discovery-qp#perffactors) for more information. 
    - It is important to run tests in your production environment using a representative set of queries to determine your average latency. 
1.   **Query rate** - The number of requests that can be processed in a given time, usually measured in Queries per Second (QPS). This measure is most important when you expect high simultaneous load on your application.  
     - The rate that can be achieved varies based on many of the same factors as latency. 
     - Query rate should also be evaluated with representative queries and at the loads you would expect to see. Remember to account for peak loads during testing.

## Factors that impact performance
{: #perffactors}

Query performance in {{site.data.keyword.discoveryshort}} will vary based on a number of factors, including plan size, query complexity, features used, and collection size and complexity.

### Plan size
{: #qp-plansize}

{{site.data.keyword.discoveryshort}} pricing plans limit the number of available documents and also provide differing ability to handle query load. The larger the plan size, the more resources that will be available to handle queries. The average rate limits also vary by plan size. Upgrading your plan can improve performance. See [{{site.data.keyword.discoveryshort}} pricing plans](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans) for plans and limits. 

### Query complexity
{: #qp-query}

There are many ways to run queries against {{site.data.keyword.discoveryshort}} and the different operations used can impact performance. These query characteristics can impact performance:

1.   **Length** - Longer queries will most likely have poorer performance. 
1.   **Aggregations** - Aggregations are a more complex query type, with nested aggregations having the highest impact on performance. 
1.   **Operators** - Wldcarding and fuzzy matching can impact performance.
1.   **Counts** - Reducing the count of documents returned can improve performance; if you need to page through results, use the `offset` parameter. 
1.   **Return fields** - Limiting the fields returned to only those needed for your application can help (For example, don’t return the full text of the document if only the title and passage are needed.) 

See [Query reference](/docs/services/discovery?topic=discovery-query-reference#query-reference) for details.

### Features used
{: #qp-features}

There are a number of features that enhance query results. The following features can impact performance:
 
1.   **Passage Retrieval** - Passage retrieval searches within documents to find relevant snippets of text for your query. You can adjust the fields in the documents over which passage retrieval searches with the `passages.fields` parameter; if your content has many fields this will help reduce the latency of passage retrieval. See [Passages](/docs/services/discovery?topic=discovery-query-parameters#passages) for more information about passage retrieval.
1.   **Relevancy Training** - Relevancy training computes features for each top-level text field (fields at the same level as `document_id` in the JSON) in the collection. If there are many top level fields, this can cause a performance impact for a `natural_language_query` when using training. Reducing the number of top level fields can improve performance. This can be done via normalization or by manually editing the JSON to put fields that are not helpful to finding relevant content in a nested structure. Changing the fields used for training also has an impact on the model so you’ll need to consider both the impact to performance and accuracy of results if making this change. See [Improving result relevance](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling) for more information on relevancy training.
1.  **Continuous Relevancy Training** - Continuous relevancy training searches across all collections in an environment. The more collections in an environment, the larger the impact on performance.  See [Continuous Relevancy Training](/docs/services/discovery?topic=discovery-crt#crt) for more information.

### Collection size and complexity
{: #qp-collection} 

The makeup of the documents in a private collection can also impact query performance:
1.  **Total number of documents** - Performance may be affected when approaching the upper limits of `Number of Documents` for Advanced plan sizes. 
1.  **Size of documents** - Very large documents (those several MB in size) require movement of a large amount of data per request, which can negatively impact performance especially when using passage retrieval and relevancy training. 
1.  **Number of enrichments** - Enrichments add complexity to documents by adding a significant number of nested fields. If an enrichment is not necessary for your use case, consider disabling it at ingestion time. Enrichments are not directly used for `natural_language_query` search relevance. See [Adding enrichments](/docs/services/discovery?topic=discovery-configservice#adding-enrichments) for more about information on enrichments.