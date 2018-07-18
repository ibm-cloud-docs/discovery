---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}

# Getting started with the API

In this short tutorial, we introduce the {{site.data.keyword.discoveryshort}} API and go through the process of creating a private data collection and searching it.
{: shortdesc}

If you prefer to work in the {{site.data.keyword.discoveryshort}} tooling, see [Getting started](/docs/services/discovery/getting-started-tool.html).
{: tip}

## Before you begin
{: #before-you-begin}

- Create an instance of the service:
    1.  Go to the [{{site.data.keyword.discoveryshort}} page ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.{DomainName}/catalog/services/discovery){: new_window} in the {{site.data.keyword.Bluemix_notm}} Catalog.
    1.  Sign up for a free {{site.data.keyword.Bluemix_notm}} account or log in.
    1.  Click **Create**.
- Copy the credentials to authenticate to your service instance:
    1. From the [{{site.data.keyword.Bluemix_notm}} dashboard](https://console.{DomainName}/dashboard/apps), click on your {{site.data.keyword.discoveryshort}} service instance to go to the {{site.data.keyword.discoveryshort}} service dashboard page.
    1.  On the **Manage** page, click **Show** to view your credentials.
    1.  Copy the `username`, `password`, and `url` values.

    **Important:** The tutorial uses service instance credentials to authenticate to the {{site.data.keyword.discoveryshort}} service. In some regions, new service instances instead use {{site.data.keyword.Bluemix}} Identity and Access Management (IAM) tokens for authentication. Authenticate by using the approach that is right for your region and service instance.

    For more information about where the service uses IAM access tokens and how to use them for authentication, see the May 17th service update in the [Release notes](/docs/services/discovery/release-notes.html).


## Step 1: Create an environment
{: #create-an-environment}

In a bash shell or equivalent environment such as Cygwin with the `curl` application installed, use the `POST /v1/environments` method to create an environment. Think of an environment as the warehouse where you are storing all your boxes of documents.

1.  Issue the following command to create an environment that is called `my-first-environment`. Replace `{username}` and `{password}` with the service credentials you copied earlier:

    ```bash
    curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    The API returns information such as your environment ID, environment status, and how much storage your environment is using.

1.  Check the environment status periodically until you see a status of `active`.
    - Issue a call to the `GET /v1/environments/{environment_id}` method to retrieve the status of your environment. Replace `{username}`, `{password}`, and `{environment_id}` with your information:

    ```bash
    curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}?version=2017-11-07"
    ```
    {: pre}

    The status must be `active` before you can create a collection.

## Step 2: Create a collection
{: #create-a-collection}

Now that the environment is ready, you can create a collection. Think of a collection as a box where you will store your documents in your environment.

1.  You need the ID of your default configuration first. To find your default `configuration_id`, use the `GET /v1/environments/{environment_id}/configurations` method. Replace `{username}`, `{password}`, and `{environment_id}` with your information:

    ```bash
      curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07
    ```
    {: pre}
1.  Use the `POST /v1/environments/{environment_id}/collections` method to create a collection called **my-first-collection**. Replace `{username}`, `{password}`, `{environment_id}` and `{configuration_id}` with your information:

    ```bash
    curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{configuration_id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07
    ```
    {: pre}

    The API returns information such as your collection ID, collection status, and how much storage your collection is using.
1.  Check the collection status periodically until you see a status of `active`.
    - Issue a call to the `GET /v1/environments/{environment_id}/collections/{collection_id}` method to retrieve the status of your collection.  Again, replace `{username}`, `{password}`, `{environment_id}` and `{configuration_id}` with your information:

    ```bash
    curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07
    ```
    {: pre}

## Step 3: Download the sample documents
{: #download-sample-documents}

Download these sample documents: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>, and <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>.

**Note:** In some browsers, the preceding links will open in a new window instead of saving locally. If this occurs, select `Save As` in your browser's `File` menu to save a copy of the file.

## Step 4: Upload the documents
{: #upload-the-documents}

1.  Now, add the example documents to your collection. This example uploads the document **test-doc1.html** to your collection. Replace `{username}`, `{password}`, `{environment_id}` and `{configuration_id}` with your information. Modify the location of the sample document to point to where you saved the `test-doc1.html` file.
    - Use the `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` method:

        ```bash
        curl -X POST -u "{username}":"{password}" -F "file=@test-doc1.html" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2017-11-07
        ```
        {: pre}

    Alternatively, use one of the SDKs listed in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}:
    - Java:

      ```java
      Discovery discovery = new Discovery("2017-11-07");
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
        version="2017-11-07"
      )

      with open((os.path.join(os.getcwd(), '{path_element}', '{filename}' as fileinfo:
        add_doc = discovery.add_document('{environment_id}', '{collection_id}', file_info=fileinfo)
      print(json.dumps(add_doc, indent=2))
      ```
      {: codeblock}

    - Node.js:

      ```javascript
      var DiscoveryV1 = require('watson-developer-cloud/discovery/v1');
      var fs = require('fs');

      var discovery = new DiscoveryV1({
        username: '{username}',
        password: '{password}',
        version_date: '2017-11-07'
      });

      var file = fs.readFileSync('{/path/to/file}');

      discovery.addDocument({ environment_id: '{environment_id}', collection_id: '{collection_id}', file: file },
      function(error, data) {
        console.log(JSON.stringify(data, null, 2));
        }
      );
      ```
      {: codeblock}

1.  Repeat this process for each of the other 3 sample files.

## Step 5: Query your collection
{: #query-your-collection}

Finally, use the `GET /v1/environments/{environment_id}/collections/{collection_id}/query` method to search your collection of documents.

The following example returns all entities that are called **IBM**. Replace `{username}`, `{password}`, `{environment_id}` and `{configuration_id}` with your information:

```bash
curl -u "{username}":"{password}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

## Next steps
{: #next-steps}

You have successfully queried documents in the environment and collection you created. You can now begin customizing your collection by adding more documents and enrichments, and customizing conversion settings. For more information about the API, see the [API Reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}.
