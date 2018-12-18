---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-11"

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

# Improving result relevance with the tooling

The relevance of natural language query results can be improved in the {{site.data.keyword.discoveryfull}} service with training. You can train your private collections using either the {{site.data.keyword.discoveryshort}} tooling, or the {{site.data.keyword.discoveryshort}} APIs. See [Improving the relevance of your query results with the API](/docs/services/discovery/train.html) if you would prefer to use the APIs.
{: shortdesc}

Relevancy training is optional; if the results of your queries meet your needs, no further training is necessary. For an overview of building use cases for training, see the blog post [How to get the most out of Relevancy Training ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window}.

In order to train Watson, you'll need to:

  -   Provide example queries that are representative of the queries your users enter and
  -   Provide ratings to say which results for each query are relevant and not relevant

Once Watson has enough training input, the information you've provided about which results are good and bad for each query will be used to learn about your collection. Watson doesn't just memorize, it learns from the specific information about individual queries and applies the patterns it has detected to all new queries. It does this with machine-learning Watson techniques that find signals in your content and questions. After training is applied, {{site.data.keyword.discoveryshort}} then reorders the query results to display the most relevant results at the top. As you add more and more training data, {{site.data.keyword.discoveryshort}} should become more accurate in the ordering of query results.

**Note:** Relevance training currently applies only to natural language queries in private collections. It is not intended for use with structured, {{site.data.keyword.discoveryshort}} Query Language queries. For more about the {{site.data.keyword.discoveryshort}} Query Language, see [Query concepts](/docs/services/discovery/using.html).

All private collections will return a `confidence` score in the query results in most cases. See [Confidence scores](/docs/services/discovery/train-tooling.html#confidence) for details.

Adding a custom stopwords list can improve the relevance of results for natural language queries. See [Defining stopwords](/docs/services/discovery/using.html#stopwords) for more information.

See [Training data requirements](/docs/services/discovery/train.html#reqs) for the minimum requirements for training, as well as the training limits.

See [Usage monitoring](/docs/services/discovery/feedback.html) for details on tracking usage and using this data to help you understand and improve your applications.

## Adding queries and rating the relevancy of results
{: #results}

Training consists of three parts: a natural language query, the results of the query, and the ratings you apply to those results.

1.  There are two ways to access the training page in the {{site.data.keyword.discoveryshort}} tooling:
    - For an individual collection, on the **Build queries** screen, click **Train Watson to improve results** on the upper right. You don't need to enter a query on the **Build queries** screen to start training. 
    - From the Performance dashboard. Click on the **View data metrics** icon on the left to open the dashboard. You will be prompted to choose a collection to train.
1.  On the **Train Watson** screen, click **Add a natural language query**, for example: "IBM Watson in healthcare" and add it. Make sure your queries are written the way your users would ask them. Also, training queries should be written with some term overlap between the query and the desired answer. This will improve initial results when the natural language query is run. Relevance training only uses natural language queries, do not enter queries written in the {{site.data.keyword.discoveryshort}} Query Language.
1.  To view the results of your query, click the **Rate Results** button next to it. If you don't think there are enough results, you could try rewriting the query, or adding more documents to this collection via the **Manage data** screen.
1.  Begin rating results as either `Relevant` or `Not relevant`. When you are done, click **Back to queries**. In the {{site.data.keyword.discoveryshort}} tooling, `Relevant` has a score of `10` and `Not relevant`has a score of `0`. If you have already starting rating results for this collection using the API, and used a different scoring scale, a warning will be displayed, with options to fix the issue.
    At the top of the screen, Watson keeps track of the training status for you, and provides tips about what you can do to improve results. "Add more variety to your ratings" means that you should use both the `Relevant` and `Not relevant` ratings. Once you meet the requirements, training will start updating periodically. It will take less than 30 minutes to complete after it begins, and you can continue working as Watson updates.
1.  Continue adding queries and rating results.

To return to the main **Build queries** screen at any time, click **Build queries** on the upper left.
{: tip}
To return to the **Manage data** screen, click the name of the collection on the upper right.
{: tip}

If you would like to delete all of the training data in your collection at one time, you must do so via the API. See [Delete all training data for a collection](https://{DomainName}/apidocs/discovery#delete-all-training-data) for more information. For more information about training via the API, see [Improving the relevance of your query results with the API](/docs/services/discovery/train.html).

## Testing and iterating on the relevancy of results

After you have completed rating results, and Watson has applied the training, you should test to see if your query results have improved. To do so, run test queries that are related (but not identical to) your training queries. Check to see if the results of your test queries have improved.

If you would like to further improve results after testing, you could:
- Add more documents to your collection.
- Add more training queries.
- Rate more results, making sure to use both the `Relevant` and `Not relevant` ratings.

For additional training guidance, see [Relevancy training tips](/docs/services/discovery/train-tips.html#relevancy-tips).

## Confidence scores
{: #confidence}

{{site.data.keyword.discoveryshort}} returns a `confidence` score for both natural language queries and those written in the {{site.data.keyword.discoveryshort}} Query Language.

The `confidence` score will be returned for both trained and untrained private collections (with the exception of filter-only queries of untrained collections). In addition, {{site.data.keyword.discoveryshort}} returns a `document_retrieval_strategy` field that indicates the source of the `confidence` score: 
-  `untrained`
-  `relevancy_training`, or
-  `continuous_relevancy_training`

The `document_retrieval_strategy` can be used along with the `confidence` score to determine how the results provided should be used. In cases where load is high, the `document_retrieval_strategy` returned may be `untrained`, even if the collection has been trained.

`confidence` can range from 0.0 to 1.0. The higher the number, the more relevant the document.

The `confidence` score can be found in the query results, under the `result_metadata` for each document. The `document_retrieval_strategy` will be listed under the `retrieval_details`.

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

For trained collections, the `confidence` number is calculated based on how relevant the result is estimated to be, compared to the trained model. Trained collections calculate `confidence` scores only for natural language queries. If you query a trained collection using the {{site.data.keyword.discoveryshort}} Query Language, or the trained model is temporarily unavailable, the `confidence` number returned will have a `document_retrieval_strategy` of `untrained`. The `confidence` score for a result with the `document_retrieval_strategy` of `untrained` is an unsupervised estimate of how relevant the document results are to the query; it is not interchangeable with the the score returned for trained collections. A trained collection can provide better answers to natural language queries than untrained collections.

Note that the `confidence` score is **not** the same as the `score`. For more information about determining thresholds for confidence scores, see [How to select a threshold for acting using confidence scores ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/watson/blog/2016/06/23/how-to-select-a-threshold-for-acting-using-confidence-scores/). The `score` should not be used to set absolute thresholds as it is a relative calculation. Instead, we recommend that applications always perform the same behavior for all results that do not include the `confidence` field. For example, an application may show all results without the `confidence` field or hide all results without the `confidence` field, but should not use the value of `score` to show some and hide others. Since the way `confidence` is calculated varies between the different retrieval methods, you should consider the `document_retrieval_strategy` when setting a threshold, and review the values before and after training.

For more information on querying, see [Getting started with querying](/docs/services/discovery/getting-started-query.html).

For more on supervised training methods, see
-  [Relevancy training](/docs/services/discovery/train-tooling.html#improving-result-relevance-with-the-tooling) and
-  [Continuous Relevancy Training](/docs/services/discovery/continuous-training.html#crt)