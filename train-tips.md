---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-03"

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

# Relevancy training tips
{: #relevancy-tips}

 Answers to common questions about training a collection and explanations of common error and warning messages. For more information on improving the relevancy of natural language queries, see [Improving result relevance with the tooling](/docs/services/discovery/train-tooling.html) and [Improving result relevance with the API](/docs/services/discovery/train.html).
{: shortdesc}

## Understanding training

Answers to common questions about training a collection.

### How do I know if my system is trained?

Use the [List collection details ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/discovery#get-collection-details){: new_window} API command to verify that your system has been trained.  

```bash
curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07"
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

In order to satisfy the requirements for training, the following must all be `true`:
- `minimum_queries_added`
- `minimum_examples_added`
- `sufficient_label_diversity`   

In the response:
- `successfully_trained` is the last time training was successfully completed. 
- `available: true` indicates that training has occurred and a model is available.
- `processing: true` indicates that training is in progress.
-  If the `data_updated` date is later than the `successfully_trained` date, then a new model has not been trained since a recent data upload.  

### How do I check errors and warnings?

You can use the [Query notices API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/discovery#query-system-notices){: new_window} to view errors or warnings.  

```bash
curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/notices?version=2017-11-07"
```
{: pre}

Other API operations are listed in [Performing other training-data query operations](/docs/services/discovery/train.html#training-data-operations).

### How do I interpret the `confidence` score that appears in natural language query results after training?

See [Confidence scores](/docs/services/discovery/train-tooling.html#confidence) for more information.  

## Interpreting Errors and Warnings

Explanations of common error and warning messages.

### Warning: `Invalid training data found: The document was not returned in the top 100 search results for the given query, and will not be used for training`

This warning is caused by the `document_ids` in your training data not matching the `document_ids` in a search performed against the collection. You should check your queries, make sure that the `document_id` of the document you are rating is returned in the top 100 results for that query. If it is not, then you might want to check two things:  

- If the document is not returned in the top 100, it might not be a good example of a high-quality result, and you might want to revisit why this document was chosen.  

- If the document is not returned at all, then you should review why it is not returned and see if there is any text in the document that matches portions of the query.  

**Note:** This warning indicates that you might have one or more bad queries, it is not an indication that training will not happen.  

### Error: `Invalid training data found: Syntax error when parsing query`

- This means there is an issue with the actual query syntax. Validate that the queries return results and don’t raise a syntax error. This can only occur if you added a filter to your natural language query.

### Error: `Invalid training data found: The query string provided exceeds the maximum length, please provide a shorter one`

- The maximum query string length is `2048`. You’ll need to shorten the specific query. Including a filter in your query is one way to work around this.  

### Error: `This collection cannot be trained: your plan does not support training on this many top-level text fields.`

- This error only occurs with `Lite` plans. Top-level fields are fields that are not nested underneath another field. The training only occurs on top-level fields, and there are limits to how many fields can be used in the training process. The more top level fields in a collection, the more training data is required. Also, in cases where there are more than `10` top level fields, training is more likely to encounter errors. 

### Error: `Training data quality standards not met: You will need additional training queries with labeled examples. (To be considered for training, each example must appear in the top 100 search results for its query.)`

- This means that you need to add more training data in order to train sucessfully. You need at least 49 unique training queries at a minimum, and each one needs at least one rated document. Minimum does not equate to optimal; the size of the collection and other factors can increase the number of training examples needed to meet the minimum.  

### Error: `Training data quality standards not met: Insufficient number of unique training queries. Expected at least n, but found m.`

- In order to meet the minimum training requirements; you need at least 49 unique training queries at a minimum, and each one needs at least one rated document. If you have more than that and are still receiving this error message, you should check your notices for additional errors.  

### Error: `Training data quality standards not met: No documents found with non-zero relevance labels.`

- Training data needs enough labeled data that specifies what documents are high value. This means that you need to rate some documents with non-zero values. If using the Discovery tooling, you need to rate some documents as Relevant (`10`); if using the API, you need to label some document as `1` or above.   

### Error: `Training data quality standards not met: Training examples have no relevance label variety for X queries.`

- One of the requirements for training is to have sufficient label diversity. This means that if you want to get a well-trained system, you should add not only documents that are the best relevance match, but also documents that are “good” relevant documents. In other words, if you have a scale of 0-4, it helps to have documents rated as 2's and 3's in addition to those rated as 4's. (If you are using the Discovery tooling, documents are rated either Relevant (`10`) or Not relevant (`0`)). At least 25% of the questions must have some label variety.   
