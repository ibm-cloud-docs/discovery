---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-31"

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

# Getting started with the API

In this short tutorial, we introduce the {{site.data.keyword.discoveryshort}} API and go through the process of creating a private data collection and searching it.
{: shortdesc}

## Before you begin

Before beginning with the {{site.data.keyword.discoveryshort}} service, you will need:

- Content to upload - Don't have any? Download the four documents here:

    <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>,
    <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>,
    <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>,
    <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>.

- To create an instance of the {{site.data.keyword.discoveryshort}} service:

  You create your {{site.data.keyword.watson}} services through {{site.data.keyword.Bluemix}}, so you need a free {{site.data.keyword.Bluemix_notm}} account to get started. ({{site.data.keyword.Bluemix_notm}} is IBM's cloud platform. For details, see [What is Bluemix?](https://console.ng.bluemix.net/docs/overview/whatisbluemix.html){: new_window})

  1.  Go to the [{{site.data.keyword.discoveryshort}} service ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window} on {{site.data.keyword.Bluemix_notm}} and either sign up for a free account or log into your {{site.data.keyword.Bluemix_notm}} account.

  1.  Choose your plan (Lite, Standard, or Advanced). See the [{{site.data.keyword.discoveryshort}} service ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window} for details. (Your original source files do not count against your file size limit.) To start, you could choose the free `Lite` plan. You can create a paid instance later.

  1.  Type `discovery-tutorial` in the **Service name** field, click **Create**.

      ![Create the service instance](images/bm-create-dsvc.gif)

  Before using the service, you will need to know your credentials `username`, `password`, and what the endpoint (`url`) is for your instance of the {{site.data.keyword.discoveryshort}} service. Click on **Service credentials** and then **View credentials**. Your service credentials are displayed as follows:

  ```json
  {
  "url": "https://gateway.watsonplatform.net/discovery/api",
  "username": "c61c9111-5f1b-22ba-94a1-01010dce4c2f",
  "password": "ZwkAbErGKwbx"
  }
  ```
  {: codeblock}

  **Note:** You must use the endpoint specified in the `url` field. The examples given in this topic use a default and might need to be changed. For more information see [Service credentials for Watson services](https://console.bluemix.net/docs/services/watson/getting-started-credentials.html).

## Step 1: Create an environment

In a bash shell or equivalent environment such as Cygwin, use the `POST /v1/environments` method to create an environment. Think of an environment as the warehouse where you are storing all your boxes of documents.

The following example creates an environment that is called `my-first-environment`:

Replace `{username}` and `{password}` with your service credentials.

```bash
curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "api/v1/environments?version=2017-09-01"
```
{: pre}

The API returns a response that includes information such as your environment ID, environment status, and how much storage your environment is using. Do not go on to the next step until your environment status is *ready*. When you create the environment, if the status returns *status: pending*, use the `GET /v1/environments/{environment_id}` method to check the status until it is ready. In this example, replace `{username}` and `{password}` with your service credentials, and replace `{environment_id}` with the **environment\_id** that was returned when you created the environment.

```bash
curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}?version=2017-09-01
```
{: pre}

## Step 2: Create a collection

Next, use the `POST /v1/environments/{environment_id}/collections` method to create a collection. Think of a collection as a box where you will store your documents in your environment. This example creates a collection that is called **my-first-collection** in the environment that you created in the previous step, and uses the following default configuration:

-   Replace `{username}` and `{password}` with your service credentials.
-   Replace `{environment_id}` with the **environment\_id** for the environment that you created in step 1.

Before creating a collection you must get the ID of your default configuration. This is done using the following:

To find your default `configuration_id`, use the `GET /v1/environments/{environment_id}/configurations` method:

```bash
  curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-09-01
```
{: pre}

Once you have the default configuration ID, use it to create your collection. Replace `{configuration_id}` with the default **configuration\_id** for your environment.

```bash
curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{"name": "*my-first-collection*", "description": "exploring collections", "configuration_id":"{configuration_id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-09-01
```
{: pre}

The API returns a response that includes information such as your collection ID, collection status, and how much storage your collection is using. Do not go on to the next step until your collection status is `online`. When you create the collection, if the status returns `status: pending`, use the `GET /v1/environments/{environment_id}/collections/{collection_id}` method to check the status until it is ready. In this example, replace `{username}` and `{password}` with your service credentials, replace `{environment_id}` with your environment ID, and replace `{collection_id}` with the collection ID that was returned earlier in this step.

```bash
curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-09-01
```
{: pre}

## Step 3: Download the sample documents

Download these documents: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>.

## Step 4: Upload the documents

Now, use the `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` method to add the example documents to your collection. This example uploads the document **test-doc1.html** to your collection:

-   Replace `{username}` and `{password}` with your service credentials.
-   Replace `{environment_id}` with the **environment\_id** for the environment you created in step 1.
-   Replace `{collection_id}` with the **collection\_id** of the collection that you created in step 2 in this example.

In your shell command, make sure that you specify the folder where you downloaded the example files.

```bash
curl -X POST -u "{username}":"{password}" -F "file=@test-doc1.html" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2017-09-01
```
{: pre}

Alternatively, use one of the SDKs listed in the [API Reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}:

- Java:

  ```java
  Discovery discovery = new Discovery("2017-09-01");
  discovery.setEndPoint("https://gateway.watsonplatform.net/discovery/api/v1");
  discovery.setUsernameAndPassword("{username}", "{password}");
  String environmentId = "{environment_id}";
  String collectionId = "{collection_id}";
  String documentJson = "{\"field\":\"value\"}";
  InputStream documentStream = new ByteArrayInputStream(documentJson.getBytes());

  CreateDocumentRequest.Builder builder = new CreateDocumentRequest.Builder(environmentId, collectionId);
  builder.inputStream(documentStream, HttpMediaType.APPLICATION_JSON);
  CreateDocumentResponse createResponse = discovery.createDocument(builder.build()).execute();
  ```
  {: codeblock}

- Python:

  ```python
  import sys
  import os
  import json
  from watson_developer_cloud import DiscoveryV1

  discovery = DiscoveryV1(
    username="{username}",
    password="{password}",
    version="2017-09-01"
  )

  with open((os.path.join(os.getcwd(), '{path_element}', '{filename}' as fileinfo:
    add_doc = discovery.add_document('{environment_id}', '{collection_id}', file_info=fileinfo)
  print(json.dumps(add_doc, indent=2))
  ```
  {: codeblock}

- Node.js:

  ```javascript
  var watson = require('watson-developer-cloud');
  var fs = require('fs');

  var discovery = new DiscoveryV1({
    username: '{username}',
    password: '{password}',
    version_date: '2017-09-01'
  });

  var file = fs.readFileSync('{/path/to/file}');

  discovery.addDocument(('{environment_id}', '{collection_id}', file),
  function(error, data) {
    console.log(JSON.stringify(data, null, 2));
    }
  );
  ```
  {: codeblock}

Repeat this process for each of the example files.

## Step 5: Query your collection

Finally, use the `GET /v1/environments/{environment_id}/collections/{collection_id}/query` method to search your collection of documents. The following example returns all entities that are called **IBM**:

-   Replace `{username}` and `{password}` with your service credentials.
-   Replace `{environment_id}` with the **environment\_id** for the environment you created in step 1.
-   Replace `{collection_id}` with the **collection\_id** of the collection that you created in step 2.

```bash
curl -u "{username}":"{password}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}*/query?version=2017-09-01&query=enriched_text.entities.text:IBM'
```
{: pre}

## Next steps

You have now successfully queried documents in the environment and collection you created. You can now begin customizing your collection by adding more documents and enrichments, and customizing conversion settings. For more information about the API, see the [API Reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}.
