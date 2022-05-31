---

copyright:
  years: 2015, 2022
lastupdated: "2022-05-20"

subcollection: discovery

---

{{site.data.keyword.attribute-definition-list}}

# Improving result relevance with the tooling
{: #improving-result-relevance-with-the-tooling}

<!-- Learn more topic WDS -->
The relevance of natural language query results can be improved in {{site.data.keyword.discoveryfull}} with training. You can train your private collections using either the {{site.data.keyword.discoveryshort}} tooling, or the {{site.data.keyword.discoveryshort}} APIs. See [Improving the relevance of your query results with the API](/docs/discovery?topic=discovery-improving-result-relevance-with-the-api) if you would prefer to use the APIs.
{: shortdesc}

Relevancy training is optional; if the results of your queries meet your needs, no further training is necessary. For information about use cases for relevancy training, see [Improve your natural language query results from Watson Discovery](https://developer.ibm.com/blogs/improving-your-natural-language-query-results-from-watson-discovery/){: external}.

To train Watson, you must provide the following:

  -   Example queries that are representative of the queries your users enter
  -   Ratings that indicate which results for each query are relevant and not relevant

After Watson has enough training input, the information that you provide about which results are good and bad for each query is used to learn about your collection. Watson does not just memorize, but it also learns from the specific information about individual queries and applies the patterns it detects to all new queries. It does so, using machine-learning Watson techniques that find signals in your content and questions. After training, {{site.data.keyword.discoveryshort}} then reorders the query results to display the most relevant results at the top. As you add more and more training data, {{site.data.keyword.discoveryshort}} becomes more accurate in the ordering of query results.

Relevance training currently applies only to natural language queries in private collections. It is not intended for use with structured {{site.data.keyword.discoveryshort}} Query Language queries. For more about the {{site.data.keyword.discoveryshort}} Query Language, see [Query concepts](/docs/discovery?topic=discovery-query-concepts).
{: note}

All private collections return a `confidence` score in the query results in most cases. For more information, see [Confidence scores](/docs/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence).

Adding a custom stopwords list can improve the relevance of results for natural language queries. See [Defining stopwords](/docs/discovery?topic=discovery-query-concepts#stopwords) for more information.

See [Training data requirements](/docs/discovery?topic=discovery-improving-result-relevance-with-the-api#reqs) for the minimum requirements for training, as well as the training limits.

See [Usage monitoring](/docs/discovery?topic=discovery-usage) for details on tracking usage and using this data to help you understand and improve your applications.

## Adding queries and rating the relevancy of results
{: #results}

Training consists of three parts: a natural language query, the results of the query, and the ratings you apply to those results.

1.  There are two ways to access the training page in the {{site.data.keyword.discoveryshort}} tooling:
    - For an individual collection, on the **Build queries** screen, click **Train Watson to improve results** on the upper right. You don't need to enter a query on the **Build queries** screen to start training. 
    - From the Performance dashboard. Click on the **View data metrics** icon on the left to open the dashboard. You are prompted to choose a collection to train.
1.  On the **Train Watson** screen, click **Add a natural language query**, for example: "IBM Watson in healthcare", and add it. Make sure your queries are written the way your users would ask them. Also, it is recommended that training queries be written with some term overlap between the query and the desired answer. This overlap improves initial results, when the natural language query is run. Relevance training only uses natural language queries, so do not enter queries written in the {{site.data.keyword.discoveryshort}} Query Language.
1.  To view the results of your query, click the **Rate Results** button next to it. If you don't think there are enough results, you could try rewriting the query, or adding more documents to this collection via the **Manage data** screen.
1.  Begin rating results as either `Relevant` or `Not relevant`. When you are done, click **Back to queries**. In the {{site.data.keyword.discoveryshort}} tooling, `Relevant` has a score of `10` and `Not relevant`has a score of `0`. If you already started rating results for this collection, using the API, and used a different scoring scale, a warning is displayed, with options to fix the issue.
    At the top of the screen, Watson tracks the training status and provides tips about what you can do to improve results. "Add more variety to your ratings" means that you might want to use both the `Relevant` and `Not relevant` ratings. After you meet the requirements, training starts updating periodically. Most training takes less than 30 minutes to complete, but you can continue working while training is underway.
1.  Continue adding queries and rating results.

To return to the main **Build queries** screen at any time, click **Build queries** on the upper left.
{: tip}
To return to the **Manage data** screen, click the name of the collection on the upper right.
{: tip}

If you would like to delete all of the training data in your collection at one time, you must do so via the API. See [Delete all training data for a collection](/apidocs/discovery#delete-all-training-data){: external} for more information. For more information about training via the API, see [Improving the relevance of your query results with the API](/docs/discovery?topic=discovery-improving-result-relevance-with-the-api).

## Testing and iterating on the relevancy of results
{: #testing-results}

After you complete rating results and Watson applies the training, test to see if your query results improved. To do so, run test queries that are related, but not identical to, your training queries. Check to see if the results of your test queries improved.

If you would like to further improve results after testing, you could:
- Add more documents to your collection.
- Add more training queries.
- Rate more results, making sure to use both the `Relevant` and `Not relevant` ratings.

For additional training guidance, see [Relevancy training tips](/docs/discovery?topic=discovery-relevancy-tips).

## Confidence scores
{: #confidence}

{{site.data.keyword.discoveryshort}} returns a `confidence` score for both natural language queries and those written in the {{site.data.keyword.discoveryshort}} Query Language.

The `confidence` score is returned for both trained and untrained private collections (with the exception of filter-only queries of untrained collections). In addition, {{site.data.keyword.discoveryshort}} returns a `document_retrieval_strategy` field that indicates the source of the `confidence` score: 
-  `untrained`
-  `relevancy_training`, or
-  `continuous_relevancy_training`

The `document_retrieval_strategy` can be used along with the `confidence` score to determine how the results provided should be used. In cases where load is high, the `document_retrieval_strategy` returned might be `untrained`, even if the collection is trained.

`confidence` can range from 0.0 to 1.0. The higher the number, the more relevant the document.

The `confidence` score can be found in the query results, under the `result_metadata` for each document. The `document_retrieval_strategy` is listed under the `retrieval_details`.

```json
{
  "matching_results": 4,
  "session_token": "1_2gYuWJyaWx792Ni4_DQ4C5cbnW",
  "retrieval_details" : {
    "document_retrieval_strategy" : "relevancy_training",
  },
  "results": [
    {
      "id": "eea16dfd5fe6139a25324e7481a32f89_13",
      "result_metadata": {
        "confidence": 0.5893963975910735,
        "score": 0.5006834
      }
    }
  ]
}
```
{: codeblock}

For trained collections, the `confidence` number is calculated based on how relevant the result is estimated to be, compared to the trained model. Trained collections calculate `confidence` scores only for natural language queries. If you query a trained collection using the {{site.data.keyword.discoveryshort}} Query Language, or the trained model is temporarily unavailable, the `confidence` number returned has a `document_retrieval_strategy` of `untrained`. The `confidence` score for a result with the `document_retrieval_strategy` of `untrained` is an unsupervised estimate of how relevant the document results are to the query; it is not interchangeable with the the score returned for trained collections. A trained collection can provide better answers to natural language queries than untrained collections.

Note that the `confidence` score is **not** the same as the `score`. It is recommended that the `score` not be used to set absolute thresholds, as it is a relative calculation. Instead, we recommend that applications always perform the same behavior for all results that do not include the `confidence` field. For example, an application might show all results without the `confidence` field or hide all results without the `confidence` field, but we recommend that you not use the value of `score` to show some and hide others. Because the way `confidence` is calculated varies between the different retrieval methods, consider the `document_retrieval_strategy`, when setting a threshold, and review the values before and after training.

For more information about querying, see [Getting started with querying](/docs/discovery?topic=discovery-getting-started-with-querying).

For more on supervised training methods, see
-  [Relevancy training](/docs/discovery?topic=discovery-improving-result-relevance-with-the-tooling)
-  [Continuous Relevancy Training](/docs/discovery?topic=discovery-crt)