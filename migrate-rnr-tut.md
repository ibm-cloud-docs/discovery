---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-03-29"

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


# Tutorial: Migrating from Retrieve and Rank
{: #migrate-rnr}

Migrating from {{site.data.keyword.retrieveandrankshort}} to {{site.data.keyword.discoveryfull}}. A continuation of the Cranfield Getting Started Tutorial

## Overview
{: #overview-rnr}

This tutorial guides you through the process of creating and training {{site.data.keyword.discoveryfull}} with sample data. 

The process for users migrating data from {{site.data.keyword.retrieveandrankshort}} to {{site.data.keyword.discoveryshort}} consists of two main steps.

1. Migrate the collection data.
2. Migrate the training data.

When migrating your trained collection data, what is **most** important is _to keep the document ids the same_. This is because your training data uses those ids to reference the ground truth, and if the ids are changed in moving from {{site.data.keyword.retrieveandrankshort}} to {{site.data.keyword.discoveryshort}} then the reranking is going to be completely off (or training might not even start). {{site.data.keyword.discoveryshort}} allows you to specify the document ID in the API upload process, so this problem can be avoided by following the guidelines in this document.  The {{site.data.keyword.retrieveandrankshort}} Training data is usually stored in a `csv` file. In this tutorial, this `csv` file is used to upload the sample training data into {{site.data.keyword.discoveryshort}}.  Migration of training data exported from the {{site.data.keyword.retrieveandrankshort}} tooling is detailed in [migrating training data from the service](/docs/services/discovery?topic=discovery-migrate-dcs-rr#extract-train).

This tutorial assumes {{site.data.keyword.retrieveandrankshort}} was setup similar to the {{site.data.keyword.retrieveandrankshort}} Getting Started Tutorial and uses the migrate from source path described [here](/docs/services/discovery?topic=discovery-migrate-dcs-rr#source). See [Evaluate your migration path to Watson Discovery service](/docs/services/discovery?topic=discovery-migrate-dcs-rr#evaluate) for other migration options.

To complete the tutorial, you need the following:

-  **cURL.**  You can install the version of cURL for your operating system from  [haxx.se ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://curl.haxx.se/){: new_window}. You must install the version that supports the Secure Sockets Layer (SSL) protocol. Make sure to include the installed binary file on your PATH environment variable.
-  Sample Cranfield data. This tutorial uses the sample collection data from the {{site.data.keyword.retrieveandrankshort}} Getting Started Tutorial. [cranfield json data ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-data.json){: new_window}
-  **Sample data ground truth** This tutorial uses sample Cranfield ground truth from the {{site.data.keyword.retrieveandrankshort}} Getting Started Tutorial. [cranfield ground truth csv![External link icon](../../icons/launch-glyph.svg "External link icon")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-gt.csv){: new_window}
-  **Python version 2.**  To check whether Python is installed, enter `python --version` at a command prompt and ensure that the version number starts with 2. If you need to install Python, see [Downloading Python ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://wiki.python.org/moin/BeginnersGuide/Download){: new_window}.
-  Data upload script: [Discovery document uploader ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-upload.py){: new_window}
-  Training Data upload script:  [Discovery training uploader ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-train.py){: new_window}

The following pre-requisites are necessary before beginning this tutorial:

-  This tutorial assumes you have already created a {{site.data.keyword.discoveryshort}} instance, if you need directions on how to create a {{site.data.keyword.discoveryshort}} instance, please refer to the [following tutorial](/docs/services/discovery?topic=discovery-gs-api#gs-api).

-  This tutorial assumes that you have your service credentials.
   -  From {{site.data.keyword.discoveryfull}} on {{site.data.keyword.Bluemix_notm}}, click **Service credentials**.
   -  Click **View credentials** under Actions.
   -  Copy the `apikey` value and make sure that the `url` value matches the one in the examples below, if it doesn't, replace it as well.

## Adding Cranfield data to Discovery
{: #cranfield-rnr}

1.  Create an Environment.

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{ "name": "my_environment", "description": "My environment" }' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    Copy the `environment-id` that is listed in the returned JSON.

1. Create a Collection.

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{ "name": "test_collection", "description": "My test collection", "configuration_id": "{configuration_id}", "language_code": "en" }' "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07"
    ```
    {: pre}

    Copy the `collection-id` that is listed in the returned JSON.

1.  Add the documents that are to be searched.
    1.  Download the [cranfield-data.json ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-data.json){: new_window} file if you haven't already. This is the source of documents that are used in {{site.data.keyword.retrieveandrankshort}}. The Cranfield collection documents are in JSON format, which is the format {{site.data.keyword.retrieveandrankshort}} accepted and which works well for Watson {{site.data.keyword.discoveryshort}} as well.
        **Note:** {{site.data.keyword.discoveryshort}} does not require uploading the Solr schema. This is because {{site.data.keyword.discoveryshort}} infers the schema from the JSON structure automatically.
    1.  Download the Data upload script [here ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-upload.py){: new_window}. This script will upload the Cranfield json into {{site.data.keyword.discoveryshort}}.
        The script reads through the JSON file and sends each individual JSON document to {{site.data.keyword.discoveryshort}} using a default configuration in {{site.data.keyword.discoveryshort}}.
        **Note:** The default configuration in {{site.data.keyword.discoveryshort}} provides similar settings to the default Solr config in {{site.data.keyword.retrieveandrankshort}}.
    1.  Issue the following command to upload the `cranfield-data-json` data to the `cranfield_collection` collection. replace `{apikey_value}`, `{path_to_file}`,  `{environment_id}`, `{collection_id}` with your information.  Note that there are additional options, -d for debug and –v for verbose output from curl.

        ```bash
        python ./disco-upload.py -u apikey:{apikey_value} -i {path_to_file}/cranfield-data.json -e {environment_id} -c {collection_id}
        ```
        {: pre}

1.  Once the upload process has completed, you can check that the documents are there by issuing the following command to view the collection details:

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07"
    ```
    {: pre}

    The output will look something like this:

    ```json
    {
      "collection_id": "f1360220-ea2d-4271-9d62-89a910b13c37",
      "name": "democollection",
      "configuration_id": "6963be41-2dea-4f79-8f52-127c63c479b0",
      "language": "en",
      "status": "available",
      "description": "this is a demo collection",
      "created": "2015-08-24T18:42:25.324Z",
      "updated": "2015-08-24T18:42:25.324Z",      
      "document_counts": {
        "available": 1000,
        "processing": 20,
        "failed": 180
      },
      "disk_usage": {
        "used_bytes": 260
      },
      "training_status": {
        "data_updated": null,
        "total_examples": 0,
        "sufficient_label_diversity": false,
        "processing": false,
        "minimum_examples_added": true,
        "successfully_trained": null,
        "available": false,
        "notices": 0,
        "minimum_queries_added": false        
      }
    }
    ```
    {: codeblock}

Look at the section `document_counts` to see how many documents were uploaded successfully. We aren't expecting any document failures with this sample data set. However, with other data sets, you may see failed document counts. If you have any failed document counts, then you can view the notices API to see the error messages. Look at the section [here ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#query-system-notices){: new_window} to review the notices API command.

The `training` section of the return gives you information about your training. We'll review that section after you upload your training data.

## Adding Training data into Discovery
{: #trainingdata-rnr}

Watson {{site.data.keyword.discoveryshort}} Service uses a machine learning model to re-rank documents. To do so you need to train a model. Training occurs after you have loaded enough queries along with the appropriate rated documents. By loading enough examples with enough variance to Watson {{site.data.keyword.discoveryshort}}, you are teaching it what a "good" document is. In this step, we will use the existing Cranfield "ground truth" that is used in {{site.data.keyword.retrieveandrankshort}} to train Watson {{site.data.keyword.discoveryshort}}.

1.  Download the sample [Cranfield ground truth csv file ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-gt.csv){: new_window} from the {{site.data.keyword.retrieveandrankshort}} tutorial if you haven't already done so.

   The file is a set of questions that a user might ask about the documents. The file provides the example information to train the ranker in {{site.data.keyword.retrieveandrankshort}} and relevancy training in {{site.data.keyword.discoveryshort}} about questions and relevant answers.

   For each question, there is at least one identifier to an answer (the document ID). Each document ID includes a number to indicate how relevant the answer is to the question. The document ID points to the answer in the `cranfield-data.json` file that you uploaded to {{site.data.keyword.discoveryshort}} in the previous step.

1.  Download the Training Data upload script. You will use this script to upload the training data into {{site.data.keyword.discoveryshort}}. The script transforms the `csv` file into a set of JSON queries and examples and sends them to {{site.data.keyword.discoveryshort}} using the [training data APIs ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#list-training-data){: new_window}
    **Note:** {{site.data.keyword.discoveryshort}} manages training data within the service, so when generating new examples and training queries they can be stored in {{site.data.keyword.discoveryshort}} itself rather than as part of a separate CSV file that needs to be maintained.
1.  Execute the training upload script to upload the training data into {{site.data.keyword.discoveryshort}}. Replace `{apikey_value}`, `{path_to_file}`, `{environment_id}`, `{collection_id}` with your information. Note that there are additional options, `-d` for debug and `–v` for verbose output from curl.

    ```bash
    python ./disco-train.py -u apikey:{apikey_value} -i {path_to_file}/cranfield-gt.csv –e {environment_id} -c {collection_id}
    ```
    {: pre}

1.  Once the data is loaded, you can check the status of training using the collection details command we saw in the previous section. {{site.data.keyword.discoveryshort}} will check about once per hour to see if there is any new data, and if there is it will begin processing it and turn it into a machine learning model. When a model is training, you will see the state of the training section change from `"processing": false` to `"processing": true`. Once the model has been trained, you will see the state in the training section to change from `"available": false` to `"available": true`. You will also see the date change for the value `"successfully_trained"`.  If there are any errors, you can view them by looking at the **notices API** as described in the previous section.

## Search for documents
{: #search-rnr}

{{site.data.keyword.discoveryshort}} will automatically use a trained model to re-rank search results if available. When [an API call ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window} is made with `natural_language_query` instead of `query`, a check is made to see if there is a model available. If a model is available then {{site.data.keyword.discoveryshort}} uses that model to re-rank results. First, we will do a search over unranked documents, and then we will do a search using the ranking model.

1.  You can search for documents in your collection by using a cURL command. Perform a query using the query API call to see unranked results. Replace `{apikey_value}`, `{environment_id}`, `{collection_id}`, with your own values.  The results returned will be unranked results, and will use the default {{site.data.keyword.discoveryshort}} ranking formulas. You can try other queries by opening the training data `csv` file and copying the value of the first column into the query parameter.

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query=what is the basic mechanism of the transonic aileron buzz"
    ```
    {: pre}

1.  Now perform a search using the model by setting the `natural_language_query` parameter. Before you do so, make sure you check that you have a trained model as described in the previous section.  Paste the following code in your console, replacing the `{apikey_value}`, `{environment_id}`, `{collection_id}` with your values.

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&natural_language_query=what is the basic mechanism of the transonic aileron buzz"
    ```
    {: pre}

    This command will return re-ranked results using the model you trained earlier. Compare the results of this search as well as the results of some of the other searches you tried earlier. You may see some differences in results compared to what you see in {{site.data.keyword.retrieveandrankshort}}. This is because some of the techniques used for search have changed to simplify the experience and improve results, but overall the quality of results will be similar.

After evaluating the reranked search results, you can refine them in {{site.data.keyword.discoveryshort}} by repeating the step of uploading training data with additional training queries and examples, and viewing the search results.  You can also add new documents, as described in the first step, to broaden the scope of the search. Similar to {{site.data.keyword.retrieveandrankshort}}, improving results with training is an iterative process.
