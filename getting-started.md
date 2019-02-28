---
copyright:
  years: 2015, 2019
lastupdated: "2019-02-14"
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
{:curl: .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}

# Getting started with the API
{: #gs-api}

In this short tutorial, we introduce the {{site.data.keyword.discoveryshort}} API and go through the process of creating a private data collection and searching it.
{: shortdesc}

If you prefer to work in the {{site.data.keyword.discoveryshort}} tooling, see [Getting started](/docs/services/discovery/getting-started-tool.html).
{: tip}

## Before you begin
{: #before-you-begin-api}

- Create an instance of the service:
    1.  Go to the [{{site.data.keyword.discoveryshort}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/catalog/services/discovery) page in the {{site.data.keyword.cloud_notm}} catalog.
        The service instance is created in the **default** resource group if you do not choose a different one, and it *cannot* be changed later. This group is sufficient for the purposes of trying out the service.
        If you're creating an instance for more robust use, then learn more about [resource groups ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/docs/resources/bestpractice_rgs.html#bp_resourcegroups){: new_window}.
    1.  Sign up for a free {{site.data.keyword.cloud_notm}} account or log in.
    1.  Click **Create**. After you create an instance of the {{site.data.keyword.discoveryshort}} service, you're taken to your list of services.
- Copy the credentials to authenticate to your service instance:
    1.  From the [resource list](https://{DomainName}/dashboard/), click on your {{site.data.keyword.discoveryshort}} service instance to go to the {{site.data.keyword.discoveryshort}} service dashboard page.
    1.  On the **Manage** page, click **Show Credentials** to view your credentials.
    1.  Copy the `API Key` and `URL` values.
- {: curl} Make sure that you have the `curl` command.
    - Test whether `curl` is installed. Run the following command on the command line. If the output lists the `curl` version with SSL support, you are set for the tutorial.

        ```bash
        curl -V
        ```
        {: pre}

    - If necessary, install a version with SSL enabled from [curl.haxx.se ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://curl.haxx.se/){: new_window}. Add the location of the file to your PATH environment variables if you want to run `curl` from any command line location.
- {:go} Install the [Go SDK ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/watson-developer-cloud/go-sdk){: new_window}.

    ```go
    go get -u github.com/watson-developer-cloud/go-sdk/...
    ```
    {: go}
    {: pre}

- {: java} Install the [Java SDK ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/watson-developer-cloud/java-sdk){: new_window}.
    - {:java} Maven

        ```java
        <dependency>
          <groupId>com.ibm.watson.developer_cloud</groupId>
          <artifactId>java-sdk</artifactId>
          <version>{version}</version>
        </dependency>
        ```
        {: codeblock}

    - {:java} Gradle

        ```bash
        compile 'com.ibm.watson.developer_cloud:java-sdk:{version}'
        ```
        {:pre}
- {: javascript} Install the [Node SDK ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/watson-developer-cloud/node-sdk){: new_window}.

    ```bash
    npm install --save watson-developer-cloud
    ```
    {:pre}
- {: python} Install the [Python SDK ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/watson-developer-cloud/python-sdk){: new_window}.

    ```bash
    pip install --upgrade watson-developer-cloud
    ```
    {:pre}
- {: ruby} Install the [Ruby SDK ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/watson-developer-cloud/ruby-sdk){: new_window}.

    ```bash
    gem install ibm_watson
    ```
    {:pre}

## Step 1: Create an environment
{: #create-an-environment}

First, create an environment. Think of an environment as the warehouse where you are storing all your boxes of documents.

This tutorial uses an API key to authenticate. For production uses, make sure that you review the API key [best practices](/docs/services/watson/apikey-bp.html#api-bp).
{: important}

1.  Issue the following command to create an environment that is called `my-first-environment`. Replace `{apikey}` and `{url}` with the API key and URL you copied earlier:

    ```bash
    curl -X POST -u "apikey:{apikey}" -H "Content-Type: application/json" -d "{\"name\":\"my-first-environment\", \"description\":\"exploring environments\"}" "{url}/v1/environments?version=2018-12-03"
    ```
    {: pre}
    {: curl}

    ```go
    package main

    import (
      "encoding/json"
      "fmt"
      "github.com/watson-developer-cloud/go-sdk/core"
      "github.com/watson-developer-cloud/go-sdk/discoveryv1"
    )

    func main() {
      discovery, discoveryErr := discoveryv1.
      NewDiscoveryV1(&discoveryv1.DiscoveryV1Options{
        URL: "{url}",
        Version: "2018-03-05",
        IAMApiKey: "{apikey}",
      })
      if discoveryErr != nil {
      panic(discoveryErr)
      }

      response, responseErr := discovery.CreateEnvironment(
        &discoveryv1.CreateEnvironmentOptions{
          Name: core.StringPtr("my-first-environment"),
          Description: core.StringPtr("exploring environments"),
        },
      )
      if responseErr != nil {
        panic(responseErr)
      }
      result := discovery.GetCreateEnvironmentResult(response)
      b, _ := json.MarshalIndent(result, "", "  ")
      fmt.Println(string(b))
    }
    ```
    {: codeblock}
    {: go}

    ```java
    IamOptions options = new IamOptions.Builder()
      .apiKey("{apikey}")
      .build();

    Discovery discovery = new Discovery("2018-12-03", options);
    discovery.setEndPoint("{url}");

    String environmentName = "my-first-environment";
    String environmentDesc = "exploring environments";

    CreateEnvironmentOptions.Builder createOptionsBuilder = new CreateEnvironmentOptions.Builder(environmentName);
    createOptionsBuilder.description(environmentDesc);
    CreateEnvironmentResponse createResponse = discovery.createEnvironment(createOptionsBuilder.build()).execute();
    System.out.println(createResponse);
    ```
    {: codeblock}
    {: java}

    ```javascript
    var DiscoveryV1 = require('watson-developer-cloud/discovery/v1');

    var discovery = new DiscoveryV1({
      version: '2018-12-03',
      iam_apikey: '{apikey}',
      url: "{url}"
    });

    discovery.createEnvironment({
      name: 'my-first-environment',
      description: 'exploring environments'
    },
      function (err, response) {
        if (err)
          console.log('error:', err);
        else
          console.log(JSON.stringify(response, null, 2));
    });
    ```
    {: codeblock}
    {: javascript}

    ```python
    import json
    from watson_developer_cloud import DiscoveryV1

    discovery = DiscoveryV1(
        version="2018-12-03",
        iam_api_key='{apikey}')
        url: "{url}"
    )

    response = discovery.create_environment(
        name="my-first-environment",
        description="exploring environments"
    ).get_result()

    print(json.dumps(response, indent=2))
    ```
    {: codeblock}
    {: python}

    ```ruby
    require "json"
    require "ibm_watson/discovery_v1"
    include IBMWatson

    discovery = DiscoveryV1.new(
      version: "2018-12-03",
      iam_apikey: "{apikey}",
      url: "{url}"
    )

    response = discovery.create_environment(
      name: "my-first-environment",
      description: "exploring environments"
    )

    puts JSON.pretty_generate(response.result)
    ```
    {: codeblock}
    {: ruby}

    The API returns information such as your environment ID, environment status, and how much storage your environment is using.

1.  Check the environment status periodically until you see a status of `active`.

    Issue a call to the **Get environment info** method to retrieve the status of your environment. Replace `{apikey}`, `{url}`, and `{environment_id}` with your information:

    ```bash
    curl -u "apikey:{apikey}" "{url}/v1/environments/{environment_id}?version=2018-12-03"
    ```
    {: pre}
    {: curl}

    ```go
    package main

    import (
      "encoding/json"
      "fmt"
      "github.com/watson-developer-cloud/go-sdk/core"
      "github.com/watson-developer-cloud/go-sdk/discoveryv1"
    )

    func main() {
      discovery, discoveryErr := discoveryv1.
      NewDiscoveryV1(&discoveryv1.DiscoveryV1Options{
        URL: "{url}",
        Version: "2018-03-05",
        IAMApiKey: "{apikey}",
      })
      if discoveryErr != nil {
        panic(discoveryErr)
      }

      response, responseErr := discovery.GetEnvironment(
        &discoveryv1.GetEnvironmentOptions{
          EnvironmentID: core.StringPtr("{environment_id}"),
        },
      )
      if responseErr != nil {
        panic(responseErr)
      }
      result := discovery.GetGetEnvironmentResult(response)
      b, _ := json.MarshalIndent(result, "", "  ")
      fmt.Println(string(b))
    }
    ```
    {: codeblock}
    {: go}

    ```java
    IamOptions options = new IamOptions.Builder()
      .apiKey("{apikey}")
      .build();

    Discovery discovery = new Discovery("2018-12-03", options);
    discovery.setEndPoint("{url}");

    String environmentId = "{environment_id}";

    GetEnvironmentOptions getOptions = new GetEnvironmentOptions.Builder(environmentId).build();
    GetEnvironmentResponse getResponse = discovery.getEnvironment(getOptions).execute();
    ```
    {: codeblock}
    {: java}

    ```javascript
    var DiscoveryV1 = require('watson-developer-cloud/discovery/v1');

    var discovery = new DiscoveryV1({
      version: '2018-12-03',
      iam_apikey: '{apikey}',
      url: "{url}"
    });

    discovery.getEnvironment({ environment_id: '{environment_id}' }, function(error, data) {
      console.log(JSON.stringify(data, null, 2));
    });
    ```
    {: codeblock}
    {: javascript}

    ```python
    import os
    import json
    from watson_developer_cloud import DiscoveryV1

    discovery = DiscoveryV1(
        version="2018-12-03",
        iam_api_key='{apikey}')
        url: "{url}"
    )

    environment_info = discovery.get_environment('{environment_id}').get_result()
    print(json.dumps(environment_info, indent=2))
    ```
    {: codeblock}
    {: python}

    ```ruby
    require "json"
    require "ibm_watson/discovery_v1"
    include IBMWatson

    discovery = DiscoveryV1.new(
      version: "2018-12-03",
      iam_apikey: "{apikey}",
      url: "{url}"
    )

    environment_info = discovery.get_environment(
      environment_id: "{environment_id}"
    )
    puts JSON.pretty_generate(environment_info.result)
    ```
    {: codeblock}
    {: ruby}

    The status must be `active` before you can create a collection.

## Step 2: Create a collection
{: #create-a-collection-api}

Now that the environment is ready, you can create a collection. Think of a collection as a box where you will store your documents in your environment.

1.  You need the ID of your default configuration first. To find your default `configuration_id`, use the **List configurations** method. Replace `{apikey}`, `{url}`, and `{environment_id}` with your information:

    ```bash
    curl -u "apikey:{apikey}" "{url}/v1/environments/{environment_id}/configurations?version=2018-12-03"
    ```
    {: pre}
    {: curl}

    ```go
    package main

    import (
      "encoding/json"
      "fmt"
      "github.com/watson-developer-cloud/go-sdk/core"
      "github.com/watson-developer-cloud/go-sdk/discoveryv1"
    )

    func main() {
      discovery, discoveryErr := discoveryv1.
        NewDiscoveryV1(&discoveryv1.DiscoveryV1Options{
          URL: "{url}",
          Version: "2018-03-05",
          IAMApiKey: "{apikey}",
        })
      if discoveryErr != nil {
        panic(discoveryErr)
      }

      response, responseErr := discovery.ListConfigurations(
        &discoveryv1.ListConfigurationsOptions{
          EnvironmentID: core.StringPtr("{environment_id}"),
        },
      )
      if responseErr != nil {
        panic(responseErr)
      }
      result := discovery.GetListConfigurationsResult(response)
      b, _ := json.MarshalIndent(result, "", "  ")
      fmt.Println(string(b))
    }
    ```
    {: codeblock}
    {: go}

    ```java
    IamOptions options = new IamOptions.Builder()
      .apiKey("{apikey}")
      .build();

    Discovery discovery = new Discovery("2018-12-03", options);
    discovery.setEndPoint("{url}");

    String environmentId = "{environment_id}";

    ListConfigurationsOptions listOptions = new ListConfigurationsOptions.Builder(environmentId).build();
    ListConfigurationsResponse listResponse = discovery.listConfigurations(listOptions).execute();
    ```
    {: codeblock}
    {: java}

    ```javascript
    var DiscoveryV1 = require('watson-developer-cloud/discovery/v1');

    var discovery = new DiscoveryV1({
      version: '2018-12-03',
      iam_apikey: '{apikey}',
      url: "{url}"
    });

    discovery.listConfigurations({ environment_id: '{environment_id}' }), function(error, data) {
      console.log(JSON.stringify(data, null, 2));
    });
    ```
    {: codeblock}
    {: javascript}

    ```python
    import os
    import json
    from watson_developer_cloud import DiscoveryV1

    discovery = DiscoveryV1(
        version="2018-12-03",
        iam_api_key='{apikey}')
        url: "{url}"
    )

    configs = discovery.list_configurations('{environment_id}').get_result()
    print(json.dumps(configs, indent=2))
    ```
    {: codeblock}
    {: python}

    ```ruby
    require "json"
    require "ibm_watson/discovery_v1"
    include IBMWatson

    discovery = DiscoveryV1.new(
      version: "2018-12-03",
      iam_apikey: "{apikey}",
      url: "{url}"
    )

    configs = discovery.list_configurations(
      environment_id: "{environment_id}"
    )
    puts JSON.pretty_generate(configs.result)
    ```
    {: codeblock}
    {: ruby}

1.  Use the **Create a collection** method to create a collection called `my-first-collection`. Replace `{apikey}`, `{url}`, `{environment_id}` and `{configuration_id}` with your information:

    ```bash
    curl -X POST -u "apikey:{apikey}" -H "Content-Type: application/json" -d "{\"name\": \"my-first-collection\", \"description\": \"exploring collections\", \"configuration_id\":\"{configuration_id}\" , \"language": \"en_us\"}" "{url}/v1/environments/{environment_id}/collections?version=2018-12-03"
    ```
    {: pre}
    {: curl}

    ```go
    package main

    import (
      "encoding/json"
      "fmt"
      "github.com/watson-developer-cloud/go-sdk/core"
      "github.com/watson-developer-cloud/go-sdk/discoveryv1"
    )

    func main() {
      discovery, discoveryErr := discoveryv1.
        NewDiscoveryV1(&discoveryv1.DiscoveryV1Options{
          URL: "{url}",
          Version: "2018-03-05",
          IAMApiKey: "{apikey}",
        })
      if discoveryErr != nil {
        panic(discoveryErr)
      }

      response, responseErr := discovery.CreateCollection(
        &discoveryv1.CreateCollectionOptions{
          EnvironmentID: core.StringPtr("{environment_id}"),
          ConfigurationID: core.StringPtr("{configuration_id}"),
          Name: core.StringPtr("my-first-collection"),
          Description: core.StringPtr("exploring collections"),
          Language: core.StringPtr("en_us"),
        },
      )
      if responseErr != nil {
        panic(responseErr)
      }
      result := discovery.GetCreateCollectionResult(response)
      b, _ := json.MarshalIndent(result, "", "  ")
      fmt.Println(string(b))
    }
    ```
    {: codeblock}
    {: go}

    ```java
    IamOptions options = new IamOptions.Builder()
      .apiKey("{apikey}")
      .build();

    Discovery discovery = new Discovery("2018-12-03", options);
    discovery.setEndPoint("{url}");

    String environmentId = "{environment_id}";
    String configurationId = "{configuration_id}";
    String collectionName = "my-first-collection";
    String collectionDescription = "exploring collections";
    String languageCode = "en_us";

    CreateCollectionOptions.Builder createCollectionBuilder = new CreateCollectionOptions.Builder(environmentId, configurationId, collectionName, collectionDescription, languageCode);

    CreateCollectionResponse createResponse = discovery.createCollection(createCollectionBuilder.build()).execute();
    ```
    {: codeblock}
    {: java}

    ```javascript
    var DiscoveryV1 = require('watson-developer-cloud/discovery/v1');

    var discovery = new DiscoveryV1({
      version: '2018-12-03',
      iam_apikey: '{apikey}',
      url: "{url}"
    });

    discovery.createCollection({ environment_id: '{environment_id}', collection_name: 'my-first-collection', description: 'exploring collections', configuration_id: '{configuration_id}', language: 'en_us' }, function(error, data) {
      console.log(JSON.stringify(data, null, 2));
    });
    ```
    {: codeblock}
    {: javascript}

    ```python
    import os
    import json
    from watson_developer_cloud import DiscoveryV1

    discovery = DiscoveryV1(
        version="2018-12-03",
        iam_api_key='{apikey}')
        url: "{url}"
    )

    new_collection = discovery.create_collection(environment_id='{environment_id}', configuration_id='{configuration_id}', name='my-first-collection', description='exploring collections', language='en_us').get_result()

    print(json.dumps(new_collection, indent=2))
    ```
    {: codeblock}
    {: python}

    ```ruby
    require "json"
    require "ibm_watson/discovery_v1"
    include IBMWatson

    discovery = DiscoveryV1.new(
      version: "2018-12-03",
      iam_apikey: "{apikey}",
      url: "{url}"
    )

    new_collection = discovery.create_collection(
      environment_id: "{environment_id}",
      configuration_id: "{configuration_id}",
      name: "my-first-collection",
      description: "exploring collections",
      language: "en_us"
    )
    puts JSON.pretty_generate(new_collection.result)
    ```
    {: codeblock}
    {: ruby}

    The API returns information such as your collection ID, collection status, and how much storage your collection is using.
1.  Check the collection status periodically until you see a status of `active`.

    Issue a call to the **Get collection details** method to retrieve the status of your collection. Again, replace `{apikey}`, `{url}`, `{environment_id}` and `{configuration_id}` with your information:

    ```bash
    curl -u "apikey:{apikey}" "{url}/v1/environments/{environment_id}/collections/{collection_id}?version=2018-12-03"
    ```
    {: pre}
    {: curl}

    ```go
    package main

    import (
      "encoding/json"
      "fmt"
      "github.com/watson-developer-cloud/go-sdk/core"
      "github.com/watson-developer-cloud/go-sdk/discoveryv1"
    )

    func main() {
      discovery, discoveryErr := discoveryv1.
        NewDiscoveryV1(&discoveryv1.DiscoveryV1Options{
          URL: "{url}",
          Version: "2018-03-05",
          IAMApiKey: "{apikey}",
        })
      if discoveryErr != nil {
        panic(discoveryErr)
      }

      response, responseErr := discovery.GetCollection(
        &discoveryv1.GetCollectionOptions{
          EnvironmentID: core.StringPtr("{environment_id}"),
          CollectionID: core.StringPtr("{collection_id}"),
        },
      )
      if responseErr != nil {
        panic(responseErr)
      }
      result := discovery.GetGetCollectionResult(response)
      b, _ := json.MarshalIndent(result, "", "  ")
      fmt.Println(string(b))
    }
    ```
    {: codeblock}
    {: go}

    ```java
    IamOptions options = new IamOptions.Builder()
      .apiKey("{apikey}")
      .build();

    Discovery discovery = new Discovery("2018-12-03", options);
    discovery.setEndPoint("{url}");

    String environmentId = "{environment_id}";
    String collectionId = "{collection_id}";

    GetCollectionOptions getOptions = new GetCollectionOptions.Builder(environmentId, collectionId).build();
    GetCollectionResponse getResponse = discovery.getCollection(getOptions).execute();
    ```
    {: codeblock}
    {: java}

    ```javascript
    var DiscoveryV1 = require('watson-developer-cloud/discovery/v1');

    var discovery = new DiscoveryV1({
      version: '2018-12-03',
      iam_apikey: '{apikey}',
      url: "{url}"
    });

    discovery.getCollection({ environment_id: '{environment_id}', collection_id: '{collection_id}' }, function(error, data) {
      console.log(JSON.stringify(data, null, 2));
    });
    ```
    {: codeblock}
    {: javascript}

    ```python
    import os
    import json
    from watson_developer_cloud import DiscoveryV1

    discovery = DiscoveryV1(
        version="2018-12-03",
        iam_api_key='{apikey}')
        url: "{url}"
    )

    collection = discovery.get_collection('{environment_id}', '{collection_id}').get_result()
    print(json.dumps(collection, indent=2))
    ```
    {: codeblock}
    {: python}

    ```ruby
    import (
      "encoding/json"
      "fmt"
      "github.com/watson-developer-cloud/go-sdk/core"
      "github.com/watson-developer-cloud/go-sdk/discoveryv1"
    )

    discovery, discoveryErr := discoveryv1.
      NewDiscoveryV1(&discoveryv1.DiscoveryV1Options{
        URL: "{url}",
        Version: "2018-03-05",
        IAMApiKey: "{apikey}",
      })
    if discoveryErr != nil {
      panic(discoveryErr)
    }

    response, responseErr := discovery.GetCollection(
      &discoveryv1.GetCollectionOptions{
        EnvironmentID: core.StringPtr("{environment_id}"),
        CollectionID: core.StringPtr("{collection_id}"),
      },
    )
    if responseErr != nil {
      panic(responseErr)
    }
    result := discovery.GetGetCollectionResult(response)
    b, _ := json.MarshalIndent(result, "", "  ")
    fmt.Println(string(b))
    ```
    {: codeblock}
    {: ruby}

## Step 3: Download the sample documents
{: #download-sample-documents}

Download the sample documents:

<ul>
  <li><a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a></li>
  <li><a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a></li>
  <li><a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a></li>
  <li><a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a></li>
</ul>

## Step 4: Upload the documents
{: #upload-the-documents}

1.  Now, add the sample documents to your collection with the **Add a document** method. This sample code uploads the `test-doc1.html` document to your collection.
    - Replace `{apikey}`, `{url}`, `{environment_id}` and `{collection_id}` with your information.
    - Modify the location of the sample document to point to where you saved the `test-doc1.html` file.

    ```bash
    curl -X POST -u "apikey:{apikey}" -F "file=@test-doc1.html" "{url}/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2018-12-03"
    ```
    {: pre}
    {: curl}

    ```go
    package main

    import (
      "encoding/json"
      "fmt"
      "os"
      "github.com/watson-developer-cloud/go-sdk/core"
      "github.com/watson-developer-cloud/go-sdk/discoveryv1"
    )

    func main() {
      discovery, discoveryErr := discoveryv1.
        NewDiscoveryV1(&discoveryv1.DiscoveryV1Options{
          URL: "{url}",
          Version: "2018-03-05",
          IAMApiKey: "{apikey}",
        })
      if discoveryErr != nil {
        panic(discoveryErr)
      }

      file, fileErr := os.Open("./test-doc1.html")
        if fileErr != nil {
      panic(fileErr)
      }
      defer file.Close()

      response, responseErr := discovery.AddDocument(
        &discoveryv1.AddDocumentOptions{
          EnvironmentID: core.StringPtr("{environment_id}"),
          CollectionID: core.StringPtr("{collection_id}"),
          File: file),
        },
      )
      if responseErr != nil {
        panic(responseErr)
      }
      result := discovery.GetAddDocumentResult(response)
      b, _ := json.MarshalIndent(result, "", "  ")
      fmt.Println(string(b))
    }
    ```
    {: codeblock}
    {: go}

    ```java
    IamOptions options = new IamOptions.Builder()
      .apiKey("{apikey}")
      .build();

    Discovery discovery = new Discovery("2018-12-03");
    discovery.setEndPoint("{url}");

    InputStream imagesStream = new FileInputStream("./test-doc1.html");
    AddDocumentOptions addDocumentOptions = new AddDocumentOptions.Builder()
      .filename("test-doc1.html")
      .environmentId("{environment_id}")
      .collectionId("{collection_id}")
      .build();

    DocumentAccepted result = discovery.createDocument(addDocumentOptions).execute();
    System.out.println(result);
    ```
    {: codeblock}
    {: java}

    ```javascript
    var DiscoveryV1 = require('watson-developer-cloud/discovery/v1');
    var fs = require('fs');

    var discovery = new DiscoveryV1({
      version_date: '2018-12-03',
      iam_apikey: '{apikey}',
      url: '{url}'
    });

    var file= fs.createReadStream('./test-doc1.html');
    var environment_id: '{environment_id}';
    var collection_id: '{collection_id}';

    var params = {
      file= file;
      environment_id = environment_id;
      collection_id = collection_id;
    };

    discovery.addDocument(params, function(error, response) {
      if (err) {
        console.log(err);
      } else {
        console.log(JSON.stringify(response, null, 2));
      }
    );
    ```
    {: codeblock}
    {: javascript}

    ```python
    import os
    import sys
    import json
    from watson_developer_cloud import DiscoveryV1

    discovery = DiscoveryV1(
        version='2018-12-03',
        iam_apikey='{apikey}',
        url='{url}'
    )
    with open('./test-doc1.html', 'rb') as file:
        add_doc = discovery.add_document(
            file,
            '{environment_id}',
            '{collection_id}',
    print(json.dumps(add_doc, indent=2))
    ```
    {: codeblock}
    {: python}

    ```ruby
    //todo
    ```
    {: codeblock}
    {: ruby}

1.  Update the code and run for each of the other 3 sample files.

## Step 5: Query your collection
{: #query-your-collection}

Finally, use the **Query your collection**{:curl} **Long collection queries**{: java} **Long collection queries**{: javascript} **Long collection queries**{: python} **Long collection queries**{: go} method to search your collection of documents.

The following example returns all entities that are called **IBM**. Replace `{apikey}`, `{environment_id}` and `{collection_id}` with your information:

```bash
curl -u "apikey:{apikey}" "{url}/v1/environments/{environment_id}/collections/{collection_id}/query?version=2018-12-03&query=enriched_text.entities.text:IBM"
```
{: pre}
{: curl}

```go
package main

import (
  // todo
)

func main() {
  // todo
}

// todo
```
{: codeblock}
{: go}

```java
IamOptions options = new IamOptions.Builder()
  .apiKey("{apikey}"{: apikey})
  .build();

Discovery discovery = new Discovery("2018-12-03", options);
discovery.setEndPoint("{url}");

String environmentId = "{environment_id}";
String collectionId = "{collection_id}";

// todo

{: codeblock}
{: java}

```javascript
var DiscoveryV1 = require('watson-developer-cloud/discovery/v1');

var discovery = new DiscoveryV1({
  version: '2018-12-03',
  iam_apikey: '{apikey}',
  url: "{url}"
});

// todo
```
{: codeblock}
{: javascript}

```python
import //todo

discovery = DiscoveryV1(
    version='2018-12-03',
    iam_apikey='{apikey}',
    url='{url}'
)

// todo
```
{: codeblock}
{: python}

```ruby
// todo
```
{: codeblock}
{: ruby}

## Next steps
{: #next-steps-api}

You successfully queried documents in the environment and collection you created. You can now begin customizing your collection by adding more documents and enrichments, and customizing conversion settings.

- {: curl} Read about the API in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery){: new_window}.
- {: go} Read about the API in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery?language=go){: new_window}.
- {: java} Read about the API in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery?language=java){: new_window}.
- {: javascript} Read about the API in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery?language=node){: new_window}.
- {: python} Read about the API in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery?language=python){: new_window}.
- {: ruby} Read about the API in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery?language=ruby){: new_window}.

- [Configure](/docs/services/discovery/building.html) your service.
- Learn about [authenticating with IAM](/docs/services/watson/getting-started-iam.html#iam).
