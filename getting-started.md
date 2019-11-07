---
copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-11-07"

subcollection: discovery

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
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

# Getting started with the Discovery API
{: #gs-api}

In this short tutorial, we introduce the {{site.data.keyword.discoveryshort}} API and go through the process of creating a private data collection and searching it.
{: shortdesc}

If you prefer to work in the {{site.data.keyword.discoveryshort}} tooling, see [Getting started](/docs/services/discovery?topic=discovery-getting-started#getting-started).
{: tip}

## Before you begin
{: #before-you-begin-api}

1.  Create an instance of the service:
    1.  Go to the [{{site.data.keyword.discoveryshort}}](https://{DomainName}/catalog/services/discovery){: external} page in the catalog.

        The service instance is created in the **default** resource group if you do not choose a different one, and it *cannot* be changed later. This group is sufficient for the purposes of trying out the service.
        If you're creating an instance for more robust use, then learn more about [resource groups](}/docs/resources/bestpractice_rgs.html#bp_resourcegroups).

    1.  Sign up for a free {{site.data.keyword.cloud_notm}} account or log in.
    1.  Click **Create**.
1.  Copy the credentials to authenticate to your service instance:
    1.  On the **Manage** page, click **Show Credentials**.
    1.  Copy the `API Key` and `URL` values.
1. Make sure that you have the `curl` command.
    - Test whether `curl` is installed. Run the following command on the command line. If the output lists the `curl` version with SSL support, you are set for the tutorial.

        ```sh
        curl -V
        ```
        {: pre}

    - If necessary, install a version with SSL enabled from [curl.haxx.se](https://curl.haxx.se/){: external}. Add the location of the file to your PATH environment variables if you want to run `curl` from any command-line location.

## Step 1: Create an environment
{: #create-an-environment}

In a bash shell or equivalent environment, such as Cygwin with the `curl` application installed, use the `POST /v1/environments` method to create an environment. Think of an environment as the warehouse where you are storing all your boxes of documents.

1.  Issue the following command to create an environment that is called `my-first-environment`. Replace `{apikey}` and `{url}` with the API key and URL you copied earlier:

    ```sh
    curl -X POST -u "apikey:{apikey}" \
    -H "Content-Type: application/json" \
    -d "{\"name\":\"my-first-environment\",\"description\":\"exploring environments\"}" \
    "{url}/v1/environments?version=2019-04-30"
    ```
    {: pre}

    Windows users: Replace the backslash (`\`) at the end of each line with a caret (`^`). Make sure that there are no trailing spaces.
    {: tip}

    The API returns information such as your environment ID, environment status, and how much storage your environment is using.

1.  Check the environment status periodically until you see a status of `active`.

    Issue a call to the `GET /v1/environments/{environment_id}` method to retrieve the status of your environment. Replace `{apikey}`, `{url}`, and `{environment_id}` with your information:

    ```sh
    curl -u "apikey:{apikey}" "{url}/v1/environments/{environment_id}?version=2019-04-30"
    ```
    {: pre}

    The status must be `active` before you can create a collection.

## Step 2: Create a collection
{: #create-a-collection-api}

Now that the environment is ready, you can create a collection. Think of a collection as a box where you will store your documents in your environment.

1.  You need the ID of your default configuration first. To find your default `configuration_id`, use the `GET /v1/environments/{environment_id}/configurations` method. Replace `{apikey}`, `{url}`, and `{environment_id}` with your information:
    ```sh
      curl -u "apikey:{apikey}" "{url}/v1/environments/{environment_id}/configurations?version=2019-04-30"
    ```
    {: pre}
1.  Use the `POST /v1/environments/{environment_id}/collections` method to create a collection called **my-first-collection**. Replace `{apikey}`, `{url}`, `{environment_id}` and `{configuration_id}` with your information:
    ```sh
    curl -X POST -u "apikey:{apikey}" \
    -H "Content-Type: application/json" \
    -d "{\"name\":\"my-first-collection\",\"description\":\"exploring collections\",\"configuration_id\":\"{configuration_id}\",\"language\":\"en_us\"}" \
    "{url}/v1/environments/{environment_id}/collections?version=2019-04-30"
    ```
    {: pre}
    The API returns information such as your collection ID, collection status, and how much storage your collection is using.
1.  Check the collection status periodically until you see a status of `active`.

    Issue a call to the `GET /v1/environments/{environment_id}/collections/{collection_id}` method to retrieve the status of your collection.  Again, replace `{apikey}`, `{url}`, `{environment_id}` and `{configuration_id}` with your information:

    ```sh
    curl -u "apikey:{apikey}" "{url}/v1/environments/{environment_id}/collections/{collection_id}?version=2019-04-30"
    ```
    {: pre}

## Step 3: Download the sample documents
{: #download-sample-documents}

Download these sample documents: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download="test-doc1.html">test-doc1.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download="test-doc2.html">test-doc2.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download="test-doc3.html">test-doc3.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>, and <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download="test-doc4.html">test-doc4.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>.

In some browsers, the preceding links open in a new window. To save locally, select `Save As` in your browser's `File` menu to save a copy of the file.
{: tip}

## Step 4: Upload the documents
{: #upload-the-documents}

1.  Now, add the example documents to your collection. This example uploads the document **test-doc1.html** to your collection. Replace `{apikey}`, `{url}`, `{environment_id}` and `{collection_id}` with your information. Modify the location of the sample document to point to where you saved the `test-doc1.html` file.
    - Use the `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` method:

        ```sh
        curl -X POST -u "apikey:{apikey}" -F "file=@test-doc1.html" "{url}/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2019-04-30"
        ```
        {: pre}

        Alternatively, use one of the SDKs listed in the [API reference](https://{DomainName}/apidocs/discovery){: external}:

    - Java:
      ```java
      IamAuthenticator authenticator = new IamAuthenticator("{apikey}");
      Discovery discovery = new Discovery("2019-04-30", authenticator);
      discovery.setServiceUrl("{url}");

      String environmentId = "{environment_id}";
      String collectionId = "{collection_id}";
      InputStream documentStream = new FileInputStream("./test-doc1.html");

      AddDocumentOptions.Builder builder = new AddDocumentOptions.Builder(environmentId, collectionId);
      builder.file(documentStream);
      builder.fileContentType(HttpMediaType.TEXT_HTML);
      builder.filename("test-doc1.html");
      DocumentAccepted response = discovery.addDocument(builder.build()).execute().getResult();
      ```
      {: codeblock}

    - Node:
      ```javascript
      const fs = require('fs');
      const DiscoveryV1 = require('ibm-watson/discovery/v1');
      const { IamAuthenticator } = require('ibm-watson/auth');

      const discovery = new DiscoveryV1({
        version: '2019-04-30',
        authenticator: new IamAuthenticator({
          apikey: '{apikey}',
        }),
        url: '{url}',
      });

      const addDocumentParams = {
        environmentId: '{environment_id}',
        collectionId: '{collection_id}',
        file: fs.createReadStream('./test-doc1.html'),
      };

      discovery.addDocument(addDocumentParams)
        .then(response => {
          const documentAccepted = response.result;
          console.log(JSON.stringify(documentAccepted, null, 2));
        })
        .catch(err => {
          console.log('error:', err);
        });
      ```
      {: codeblock}

    - Python:
      ```python
      import json
      from ibm_watson import DiscoveryV1
      from ibm_cloud_sdk_core.authenticators import IAMAuthenticator

      authenticator = IAMAuthenticator('{apikey}')
      discovery = DiscoveryV1(
          version='2019-04-30',
          authenticator=authenticator
      )

      discovery.set_service_url('{url}')

      with open('./test-doc1.html') as fileinfo:
          add_doc = discovery.add_document(
              '{environment_id}',
              '{collection_id}',
              file=fileinfo).get_result()
      print(json.dumps(add_doc, indent=2))
      ```
      {: codeblock}


1.  Repeat this process for each of the other 3 sample files.

## Step 5: Query your collection
{: #query-your-collection}

Finally, use the `GET /v1/environments/{environment_id}/collections/{collection_id}/query` method to search your collection of documents.

The following example returns all entities that are called **IBM**. Replace `{apikey}`, `{environment_id}` and `{collection_id}` with your information:

```sh
curl -u "apikey:{apikey}" "{url}/v1/environments/{environment_id}/collections/{collection_id}/query?version=2019-04-30&query=enriched_text.entities.text:IBM"
```
{: pre}

## Next steps
{: #next-steps-api}

You successfully queried documents in the environment and collection you created. You can now begin customizing your collection by adding more documents and enrichments, and customizing conversion settings.

- Read about the API in the [API reference](https://{DomainName}/apidocs/discovery){: external}
- [Configure](/docs/services/discovery?topic=discovery-configservice#configservice) your service
- Learn about [authenticating with IAM](/docs/services/watson/getting-started-iam.html#iam)
