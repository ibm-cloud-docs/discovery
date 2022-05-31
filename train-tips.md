---

copyright:
  years: 2015, 2020
lastupdated: "2020-02-10"

subcollection: discovery

---

{{site.data.keyword.attribute-definition-list}}

# Relevancy training tips
{: #relevancy-tips}

 Answers to common questions about training a collection and explanations of common error and warning messages. For more information about improving the relevancy of natural language queries, see [Improving result relevance with the tooling](/docs/discovery?topic=discovery-improving-result-relevance-with-the-tooling) and [Improving result relevance with the API](/docs/discovery?topic=discovery-improving-result-relevance-with-the-api).
{: shortdesc}

## Understanding training
{: #understanding-training}

Answers to common questions about training a collection.

### How do I know if my system is trained?
{: #understanding-system}

Use the [List collection details](/apidocs/discovery#get-collection-details){: external} API method to verify that your system is trained.  

```bash
curl -u "apikey":"{apikey_value}" {url}/v1/environments/{environment_id}/collections/{collection_id}?version=2019-04-30"
```
{: pre}

Example response:

```json
{
  "training_status": {
    "data_updated": "2017-02-10T14:18:22.786Z",
    "total_examples": 54,
    "sufficient_label_diversity": false,
    "processing": false,
    "minimum_examples_added": true,
    "successfully_trained": "2017-02-08T14:18:22.786Z",
    "available": true,
    "notices": 13,
    "minimum_queries_added": true
    }
}
```

To satisfy the requirements for training, the following must all be `true`:
- `minimum_queries_added`
- `minimum_examples_added`
- `sufficient_label_diversity`

In the response:
- `successfully_trained` is the last time training was successfully completed. 
- `available: true` indicates that training occurred and a model is available.
- `processing: true` indicates that training is in progress.
-  If the `data_updated` date is later than the `successfully_trained` date, then a new model has not been trained since a recent data upload.  

### How do I check errors and warnings?
{: #understanding-errors}

You can use the [Query notices API](/apidocs/discovery#query-system-notices){: external} to view errors or warnings.  

```bash
curl -u "apikey":"{apikey_value}" {url}/v1/environments/{environment_id}/collections/{collection_id}/notices?version=2019-04-30"
```
{: pre}

Replace `{apikey}` and `{url}` with your API key and URL.

Other API operations are listed in [Performing other training-data query operations](/docs/discovery?topic=discovery-improving-result-relevance-with-the-api#training-data-operations).

### How do I interpret the `confidence` score that appears in natural language query results after training?
{: #interpret-confidence}

See [Confidence scores](/docs/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence) for more information.  

## Interpreting Errors and Warnings
{: #interpreting-errors}

Explanations of common error and warning messages.

### Warning: `Invalid training data found: The document was not returned in the top 100 search results for the given query, and will not be used for training`
{: #warning-docnotreturned}

This warning is caused by the `document_ids` in your training data not matching the `document_ids` in a search performed against the collection. Check your queries, and make sure that the `document_id` of the document you are rating is returned in the top 100 results for that query. If it is not, then you might want to check two things:  

- If the document is not returned in the top 100, it might not be a good example of a high-quality result, and you might want to revisit why this document was chosen.  

- If the document is not returned at all, then review why it is not returned, and see if there is any text in the document that matches portions of the query.  

This warning indicates that you might have one or more bad queries. It is not an indication that training cannot happen.
{: note}

### Error: `Invalid training data found: Syntax error when parsing query`
{: #error-syntax}

- This means there is an issue with the actual query syntax. Validate that the queries return results and don’t raise a syntax error. This can only occur if you added a filter to your natural language query.

### Error: `Invalid training data found: The query string provided exceeds the maximum length, please provide a shorter one`
{: #error-exceedlength}

- The maximum query string length is `2048`. You’ll need to shorten the specific query. Including a filter in your query is one way to work around this.  

### Error: `This collection cannot be trained: your plan does not support training on this many top-level text fields.`
{: #error-toplevelfields}

- This error only occurs with `Lite` plans. Top-level fields are fields that are not nested underneath another field. The training only occurs on top-level fields, and there are limits to how many fields can be used in the training process. The more top level fields in a collection, the more training data is required. Also, in cases where there are more than `10` top level fields, training is more likely to encounter errors. 

### Error: `Training data quality standards not met: You will need additional training queries with labeled examples. (To be considered for training, each example must appear in the top 100 search results for its query.)`
{: #error-labels}

- This error means that you need to add more training data to train successfully. You need at least 49 unique training queries at a minimum, and each one needs at least one rated document. Minimum does not equate to optimal; the size of the collection and other factors can increase the number of training examples needed to meet the minimum.  

### Error: `Training data quality standards not met: Insufficient number of unique training queries. Expected at least n, but found m.`
{: #error-notunique}

- To meet the minimum training requirements, you need at least 49 unique training queries, and each one needs at least one rated document. If you have more than that and are still receiving this error message, check your notices for additional errors.  

### Error: `Training data quality standards not met: No documents found with non-zero relevance labels.`
{: #error-relevance}

- Training data needs enough labeled data that specifies what documents are high value. This means that you need to rate some documents with non-zero values. If using the Discovery tooling, you need to rate some documents as Relevant (`10`); if using the API, you need to label some document as `1` or above.   

### Error: `Training data quality standards not met: Training examples have no relevance label variety for X queries.`
{: #error-variety}

- One of the requirements for training is to have sufficient label diversity, meaning that if you want to get a well-trained system, it is recommended that you not only add documents that are the best relevance match, but also documents that are “good” relevant documents. In other words, if you have a scale of 0-4, it helps to have documents rated as 2's and 3's, in addition to those rated as 4's. If you are using the Discovery tooling, documents are rated either Relevant (`10`) or Not relevant (`0`). At least 25% of the questions must have some label variety.
