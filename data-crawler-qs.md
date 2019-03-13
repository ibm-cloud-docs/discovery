---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-28"

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

# Getting started with the Data Crawler
{: #getting-started-with-the-data-crawler}

This topic explains how to use the data crawler to ingest files from your local filesystem, to use with the {{site.data.keyword.discoveryfull}} service.
{: shortdesc}

The Data Crawler should only be used to crawl file shares or databases, in all other cases you should use the appropriate {{site.data.keyword.discoveryshort}} connector. See [Connecting to data sources](/docs/services/discovery?topic=discovery-sources#sources) for details. Assistance is no longer provided for the Data Crawler if you are using it with a data source supported by the {{site.data.keyword.discoveryshort}} connectors.
{: important}

Before attempting this task, create an instance of the {{site.data.keyword.discoveryshort}} service in {{site.data.keyword.Bluemix}}. In order to complete this guide, you will need to use the credentials that are associated with the instance of the service that you created.

## Create an environment
{: #dc-create-environment}

Use the bash POST /v1/environments method to create an environment. Think of an environment as the warehouse where you are storing all your boxes of documents. The following example creates an environment that is called `my-first-environment`:

Replace `{apikey}` with your service credentials.

(For more detailed information about using {apikey} credentials, see [Getting started with the API](/docs/services/discovery?topic=discovery-gs-api#gs-api).)

```bash
curl -X POST -u "apikey:{apikey}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
```
{: pre}

The API returns a response that includes information such as your environment ID, environment status, and how much storage your environment is using. Do not go on to the next step until your environment status is `ready`. When you create the environment, if the status returns `status:pending`, use the `GET /v1/environments/{environment_id}` method to check the status until it is ready. In this example, replace `{apikey}` with your service credentials, and replace `{environment_id}` with the environment ID that was returned when you created the environment.

```bash
curl -u "apikey:{apikey}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}?version=2017-11-07
```
{: pre}

## Create a collection
{: #dc-create-collection}

Next, use the `POST /v1/environments/{environment_id}/collections` method to create a collection. Think of a collection as a box where you will store your documents in your environment. This example creates a collection that is called `my-first-collection` in the environment that you created in the previous step, and uses the following default configuration:

-   Replace `{apikey}` with your service credentials.
-   Replace `{environment_id}` with the environment ID for the environment that you created in step 1.

Before creating a collection you must get the ID of your default configuration. To find your default `configuration_id`, use the `GET /v1/environments/{environment_id}/configurations` method:

```bash
curl -u "apikey:{apikey}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07
```
{: pre}

Once you have the default configuration ID, use it to create your collection. Replace `{configuration_id}` with the default configuration ID for your environment.

```bash
curl -X POST -u "apikey:{apikey}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{configuration_id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07
```
{: pre}

The API returns a response that includes information such as your collection ID, collection status, and how much storage your collection is using. Do not go on to the next step until your collection status is `online`. When you create the collection, if the status returns `status:pending`, use the `GET /v1/environments/{environment_id}/collections/{collection_id}` method to check the status until it is ready. In this example, replace `{apikey}` with your service credentials, replace `{environment_id}` with your environment ID, and replace `{collection_id}` with the collection ID that was returned earlier in this step.

```bash
curl -u "apikey:{apikey}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07
```
{: pre}

## Download example documents
{: #dc-download-documents}

Download these documents:

-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>

## Download and install the Data Crawler
{: #download-and-install-the-data-crawler}

1.  Verify your system prerequisites

    -   Java Runtime Environment version 8 or higher

        **Note:** Your `JAVA_HOME` environment variable must be set correctly, or not be set at all, in order to run the Crawler.
    -   Red Hat Enterprise Linux 6 or 7, or Ubuntu Linux 15 or 16. For optimal performance, the Data Crawler should run on its own instance of Linux, whether it is a virtual machine, a container, or hardware.
    -   Minimum 2 GB RAM on the Linux system

1.  Open a browser and log into your [{{site.data.keyword.Bluemix_notm}} account ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/){: new_window}.
1.  From your {{site.data.keyword.Bluemix_notm}} Dashboard, select the {{site.data.keyword.discoveryshort}} service you previously created.
1.  Under **Automate the upload of content to the Discovery service**, select the appropriate download link for your system (DEB, RPM, or ZIP) to download the Data Crawler.
1.  As an administrator, use the appropriate commands to install the archive file that you downloaded:

    -   On systems such as Red Hat and CentOS that use rpm packages, use a command such as the following: `rpm -i /full/path/to/rpm/package/rpm-file-name`
    -   On systems such as Ubuntu and Debian that use deb packages, use a command such as the following: `dpkg -i /full/path/to/deb/package/deb-file-name`
    -   The Crawler scripts are installed into `{installation directory}/bin`; for example, `/opt/ibm/crawler/bin`. Ensure that `{installation_directory}/bin` is in your `PATH` environment variable for the Crawler commands to work correctly.

    Crawler scripts are also installed to `/usr/local/bin`, so this can be added to your `PATH` environment variable as well.
    {: tip}

## Create your working directory
{: #dc-working-directory}

Copy the contents of the `{installation_directory}/share/examples/config` directory to a working directory on your system, for example `/home/config`.

**Warning:** Do not modify the provided configuration example files directly. Copy and then edit them. If you edit the example files in-place, your configuration may be overwritten when upgrading the Data Crawler, or may be removed when uninstalling it.

**Note:** References in this guide to files in the `config` directory, such as `config/crawler.conf`, refer to that file in your working directory, and NOT in the installed `{installation_directory}/share/examples/config` directory.

## Configure crawl options
{: #dc-configure-crawl-options}

To set up the Data Crawler to crawl your repository, you must specify which local system files you want to crawl, and which {{site.data.keyword.discoveryshort}} service to send the collection of crawled files to, once the crawl has been completed.

1.  **`filesystem-seed.conf`** - Open the `seeds/filesystem-seed.con` file in a text editor. Modify the `value` attribute directly under the `name-"url"` attribute to the file path that you want to crawl. For example: `value-"sdk-fs:///TMP/MY_TEST_DATA/"`

    **Note:** The URLs must start with `sdk-fs://`. So to crawl, for example, `/home/watson/mydocs`, the value of this URL would be `sdk-fs:///home/watson/mydocs` - the third / is necessary!

    Save and close the file.

1.  **`discovery_service.conf`** - Open the `discovery/discovery_service.conf` file in a text editor. Modify the following values specific to the {{site.data.keyword.discoveryshort}} service you previously created on {{site.data.keyword.Bluemix_notm}}:

    -   `environment_id` - Your {{site.data.keyword.discoveryshort}} service environment ID.
    -   `collection_id` - Your {{site.data.keyword.discoveryshort}} service collection ID.
    -   `configuration_id` - Your {{site.data.keyword.discoveryshort}} service configuration ID.
    -   `configuration` - The full path location of this `discovery_service.conf` file, for example, `/home/config/discovery/discovery_service.conf`.
    -   `apikey` - Credential for your {{site.data.keyword.discoveryshort}} service.
1.  **`crawler.conf`** - Open the `config/crawler.conf` file in a text editor.

    -   Set the `output_adapter` `class` and `config` options for the {{site.data.keyword.discoveryshort}} service as follows:

        ```bash
        class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

        config - "discovery_service"

        discovery_service {
          include "discovery/discovery_service.conf"
        }
        ```
        {: pre}

1.  After modifying these files, you are ready to crawl your data.

## Crawl your data
{: #dc-crawl}

Run the following command: `crawler crawl --config [config/crawler.conf]`

This will run a crawl with the configuration file `crawler.conf`.

**Note:** The path to the configuration file passed in the `--config` option must be a qualified path. That is, it must be in relative formats, such as `config/crawler.conf` or `./crawler.conf`, or in an absolute path such as `/path/to/config/crawler.conf`.

## Search your documents
{: #dc-search}

Finally, use the `GET /v1/environments/{environment_id}/collections/{collection_id}/query` method to search your collection of documents. The following example returns all entities that are called `IBM`:

-   Replace `{apikey}` with your service credentials.
-   Replace `{environment_id}` with the environment ID for the environment you created in step 1.
-   Replace `{collection_id}` with the collection ID of the collection that you created in step 2.

```bash
curl -u "apikey:{apikey}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query-enriched_text.entities.text:IBM'
```
{: pre}

## Results
{: #dc-results}

You have now successfully queried documents in an environment and collection you created. Now you can begin customizing by adding more documents to the collection.
