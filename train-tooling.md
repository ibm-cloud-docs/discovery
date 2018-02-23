---

copyright:
  years: 2015, 2018
lastupdated: "2018-02-22"

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

# Improving result relevance with the tooling

The relevance of natural language query results can be improved in the {{site.data.keyword.discoveryfull}} service with training. You can train your private collections using either the {{site.data.keyword.discoveryshort}} tooling, or the {{site.data.keyword.discoveryshort}} APIs. See [Improving the relevance of your query results with the API](/docs/services/discovery/train.html) if you would prefer to use the APIs.
{: shortdesc}

Relevancy training is optional; if the results of your queries meet your needs, no further training is necessary. For an overview of building use cases for training, see the blog post [How to get the most out of Relevancy Training ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window}.

In order to train Watson, you'll need to:

  -   Provide example queries that are representative of the queries your users enter and
  -   Provide ratings to say which results for each query are relevant and not relevant

Once Watson has enough training input, the information you've provided about which results are good and bad for each query will be used to learn about your collection. Watson doesn't just memorize, it learns from the specific information about individual queries and applies the patterns it has detected to all new queries. It does this with machine-learning Watson techniques that find signals in your content and questions. After training is applied, {{site.data.keyword.discoveryshort}} then reorders the query results to display the most relevant results at the top. As you add more and more training data, {{site.data.keyword.discoveryshort}} should become more accurate in the ordering of query results.

Training must meet the following **minimum** requirements for {{site.data.keyword.discoveryshort}} to begin applying your ratings:

  - You must train a minimum of 49 queries, and possibly more. Watson will give you feedback if it needs more queries in order to train.
  - You should apply both available ratings to your results: `Relevant` and `Not relevant`. Only rating the `Relevant` documents will not provide the data needed.

**Note:** Relevance training needs certain training-data requirements before it takes effect. The service checks the training data periodically to determine if these requirements are met, and automatically updates itself based on any changes.

**Note:** Relevance training currently applies only to natural language queries in private collections. It is not intended for use with structured, {{site.data.keyword.discoveryshort}} Query Language queries.  For more about the {{site.data.keyword.discoveryshort}} Query Language, see [Query concepts](/docs/services/discovery/using.html).

**Note:** There is a maximum of 25 trained collections per environment.  

## Adding queries and rating the relevancy of results

Training consists of three parts: a natural language query, the results of the query, and the ratings you apply to those results.

1.  In the {{site.data.keyword.discoveryshort}} tooling, you can reach the training page for a collection from the **Build queries** screen. Click **Train Watson to improve results** on the upper right. You don't need to enter a query on the **Build queries** screen to start training.
1.  On the **Train Watson** screen, click **Add a natural language query**, for example: "IBM Watson in healthcare" and add it. Make sure your queries are written the way your users would ask them. Also, training queries should be written with some term overlap between the query and the desired answer. This will improve initial results when the natural language query is run. Relevance training only uses natural language queries, do not enter queries written in the {{site.data.keyword.discoveryshort}} Query Language.
1.  To view the results of your query, click the **Rate Results** button next to it. If you don't think there are enough results, you could try rewriting the query, or adding more documents to this collection via the **Manage data** screen.
1.  Begin rating results as either `Relevant` or `Not relevant`. When you are done, click **Back to queries**. In the {{site.data.keyword.discoveryshort}} tooling, `Relevant` has a score of `10` and `Not relevant`has a score of `0`. If you have already starting rating results for this collection using the API, and used a different scoring scale, a warning will be displayed, with options to fix the issue.
    At the top of the screen, Watson keeps track of the training status for you, and provides tips about what you can do to improve results. "Add more variety to your ratings" means that you should use both the `Relevant` and `Not relevant` ratings. Once you meet the requirements, training will start updating periodically. It will take less than 30 minutes to complete after it begins, and you can continue working as Watson updates.
1.  Continue adding queries and rating results.

To return to the main **Build queries** screen at any time, click **Build queries** on the upper left.
{: tip}
To return to the **Manage data** screen, click the name of the collection on the upper right.
{: tip}

If you would like to delete all of the training data in your collection at one time, you must do so via the API. See [Delete all training data for a collection](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-all-training-data) for more information. For more information about training via the API, see [Improving the relevance of your query results with the API](/docs/services/discovery/train.html).

## Testing and iterating on the relevancy of results

After you have completed rating results, and Watson has applied the training, you should test to see if your query results have improved. To do so, run test queries that are related (but not identical to) your training queries. Check to see if the results of your test queries have improved.

If you would like to further improve results after testing, you could:
- Add more documents to your collection.
- Add more training queries.
- Rate more results, making sure to use both the `Relevant` and `Not relevant` ratings.

For additional training guidance, see [Relevancy training tips](/docs/services/discovery/train-tips.html#relevancy-tips).

## Confidence scores
{: #confidence}

Trained collections will return a `confidence` score in the result of a natural language query. This `confidence` number is calculated based on how relevant the result is estimated to be, compared to the trained model. The `confidence` score is **not** the same as the  `score`. For more information about determining thresholds for confidence scores, see [How to select a threshold for acting using confidence scores ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/watson/blog/2016/06/23/how-to-select-a-threshold-for-acting-using-confidence-scores/). The `score` should not be used to set absolute thresholds as it is a relative calculation.

`confidence` can range from 0.0 to 1.0. The higher the number, the more relevant the document.

The `confidence` score can be found in the query results, under the `result_metadata` for each document, for example:

```json
    "results": [
        {
            "id": "eea16dfd5fe6139a25324e7481a32f89_13",
            "result_metadata": {
                "confidence": 0.5893963975910735,
                "score": 0.5006834
            },
```

**Note:** The `confidence` field is only returned when relevancy training has been successfully completed. There may also be cases where the trained model is not available and the `confidence` field will not be returned. Applications using `confidence` as a threshold should ensure they can handle these scenarios. Since `score` is relative to the query, it is not recommended for use as a fixed threshold. Instead, we recommend that applications always perform the same behavior for all results that do not include the `confidence` field. For example, an application may show all results without the `confidence` field or hide all results without the `confidence` field, but should not use the value of `score` to show some and hide others.
