---

copyright:
  years: 2015, 2018
lastupdated: "2018-02-12"

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

# Configuring the Data Crawler

To set up the Data Crawler to crawl your repository, you must specify the appropriate input adapter in the `crawler.conf` file, and then configure repository-specific information in the input adapter configuration files.
{: shortdesc}

Before making the changes listed in these steps, make sure that you have created your  working directory by copying the contents of the `{installation_directory}/share/examples/config` directory to a working directory on your system, for example `/home/config`.

**Important:** Do not modify the provided configuration example files directly. Copy and then edit them. If you edit the example files in-place, your configuration may be overwritten when upgrading the Data Crawler, or may be removed when uninstalling it.

**Note:** References in this guide to files in the `config` directory, such as `config/crawler.conf`, refer to that file in your working directory, and NOT in the installed `{installation_directory}/share/examples/config` directory.

The specified values are the defaults in `config/crawler.conf`, and configure the Filesystem connector:

1.  Open the `config/crawler.conf` file in a text editor.

    -   Set the `crawl_config_file` option to the `.conf` that you previously modified, for example: `connectors/filesystem.conf`.
    -   Set the `crawl_seed_file` option to the `-seed.conf` that you previously modified, for example: `seeds/filesystem-seed.conf`.
    -   Set the `output_adapter` `class` and `config` options for the {{site.data.keyword.discoveryshort}} service as follows:

        ```
        class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

        config - "discovery_service"

        discovery_service {
          include "discovery/discovery_service.conf"
        }
        ```
        {: codeblock}

    There are other optional settings in this file that may be set as appropriate to your environment, see: [Configuring crawl options](/docs/services/discovery/data-crawler-discovery.html#configuring-crawl-options), [Configuring the input adapter](/docs/services/discovery/data-crawler-discovery.html#input-adapter), [Configuring the output adapter](/docs/services/discovery/data-crawler-discovery.html#output-adapter), and [Additional crawl management options](/docs/services/discovery/data-crawler-discovery.html#additional-crawl-management-options) for detailed information about setting these values.

1.  Open the `discovery/discovery_service.conf` file in a text editor. Modify the following values specific to the {{site.data.keyword.discoveryshort}} service you previously created on {{site.data.keyword.Bluemix}}:

    -   `environment_id` - Your {{site.data.keyword.discoveryshort}} service environment ID.
    -   `collection_id` - Your {{site.data.keyword.discoveryshort}} service collection ID.
    -   `configuration_id` - Your {{site.data.keyword.discoveryshort}} service configuration ID.
    -   `configuration` - The full path location of this `discovery_service.conf` file, for example, `/home/config/discovery/discovery_service.conf`.
    -   `username` - Username credential for your {{site.data.keyword.discoveryshort}} service.
    -   `password` - Password credential for your {{site.data.keyword.discoveryshort}} service.

    There are other optional settings in this file that may be set as appropriate to your environment. See [Configuring Service Options](/docs/services/discovery/data-crawler-discovery.html#configuring-service-options) for detailed information about setting these values.

1.  After modifying these files, you are ready to crawl your data. Proceed to [Crawling your data repository](/docs/services/discovery/data-crawler-run.html#crawling-your-data-repository) to continue.

## Configuring crawl options
{: #configuring-crawl-options}

The file `config/crawler.conf` contains information that tells the Data Crawler which files to use for its crawl (input adapter), where to send the collection of crawled files once the crawl has been completed (output adapter), and other crawl management options.

**Note:** All file paths are relative to the `config` directory, except where noted.

To access the in-product manual for the `crawler.conf` file, with the most up-to-date information, type the following command from the Crawler installation directory: `man crawler.conf`
{: tip}

The options that can be set in this file are:

### Input adapter
{: #input-adapter}

-   **`class`** - Internal use only; defines the Data Crawler input adapter class. The default value is: `com.ibm.watson.crawler.connectorframeworkinputadapter.Crawl`
-   **`config`** - Internal use only; defines the connector framework configuration. The default configuration key within this block to pass to the chosen input adapter is: `connector_framework`

    The connector framework is what allows you to talk to your data. It could be internal data within the enterprise, or it could be external data on the web or in the cloud. The connectors allow access to a number of different data sources, while connecting is actually controlled by the crawling process.

    **Important:** Data retrieved by the Connector Framework Input Adapter is cached locally. It is not stored encrypted. By default, the data is cached to a temporary directory that should be cleared on reboot, and should be readable only by the user who executed the crawler command.

    There is a chance that this directory could outlive the crawler if the connector framework was to go away before it could clean up after itself. Carefully consider the location for your cached data - you may put it on an encrypted filesystem, but be aware of the performance implications of doing so. Only you can decide the appropriate balance between speed and security for your crawls.
-   **`crawl_config_file`** - The configuration file to use for the crawl. Default value is: `connectors/filesystem.conf`
-   **`crawl_seed_file`** - The crawl seed file to use for the crawl. Default value is: `seeds/filesystem-seed.conf`
-   **`id_vcrypt_file`** - Keyfile used for data encryption by the Crawler; the default key included with the crawler is `id_vcrypt`. Use the vcrypt script in the `bin` folder if you need to generate a new `id_vcrypt` file.
-   **`crawler_temp_dir`** - The Crawler temporary folder for connector logs. Default value, `tmp`, is provided. If it doesn't already exist, the `tmp` folder will be created in the current working directory.
-   **`extra_jars_dir`** - Adds a directory of extra JARs to the connector framework classpath.

    **Note:** Relative to the connector framework `lib/java` directory.

    -   This value must be `oakland` when using the SharePoint connector.
    -   This value must be `database` when using the Database connector.

    You can leave this value empty (i.e., empty string "") when using other connectors.

-   **`urls_to_filter`** - Blacklist of URLs that should not be crawled, in regular expression form. The Data Crawler will not crawl URLs that match any of the regular expressions provided.

    The `domain list` contains the domains that cannot be crawled. Add to it if necessary.

    The `filetype list` contains the file extensions that the Orchestration Service does not support.

    Remove any supported filetypes from the regular expressions.

    Ensure that your seed URL domain is allowed by the filter. Use an empty filter for `allow everything` behavior.

    Ensure that your seed URL will not be excluded by a filter, or the Crawler may hang.

-   **`max_text_size`** - The maximum size, in bytes, that a document can be before it is written to disk by the Connector Framework. Adjusting this higher decreases the amount of documents written to disk, but increases the memory requirement. Default value is `1048576`
-   **`extra_vm_params`** - Allows you to add extra Java parameters to the command used to launch the Connector Framework.

-   **`bootstrap_logging`** - Writes connector framework startup log; useful for advanced debugging only. Possible values are `true` or `false`. Log file will be written to `crawler_temp_dir`

-   **`read-timeout`** - Sets the time (in seconds) that the crawler will wait for a response from the connector framework. The default value is 5 seconds.

### Output adapter
{: #output-adapter}

-   **`class`** - Defines the Data Crawler output adapter class.
-   **`config`** - Defines which configuration key to pass to the output adapter. The string must correspond to a key within this configuration object. In the following code example:

    ```
    class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

    config - "discovery_service"

    discovery_service {
        include "discovery/discovery_service.conf"
      }
    ```
    {: codeblock}

    the configuration key is `discovery_service`.

You must select an output adapter by specifying its `class` parameter and `config` key.

-   **{{site.data.keyword.discoveryshort}} Service Output Adapter** - Uploads crawled documents to the {{site.data.keyword.discoveryfull}} Service. Select this adapter by setting the `class` parameter and `config` key as follows.

```
class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

config - "discovery_service"

discovery_service {
            include "discovery/discovery_service.conf"
          }
```
{: codeblock}

-   **Test Output Adapter** - The Test Output Adapter writes a representation of the crawled files to disk in a specified location. Select this adapter by setting the `class` parameter and `config` key as follows.

    An additional parameter, `output_directory`, selects the directory to which the representation of the crawled data should be written.

```
class - "com.ibm.watson.crawler.testoutputadapter.TestOutputAdapter"

config - "test"

output_directory - "/tmp/crawler-test-output"`
```
{: codeblock}

-   **`retry`** - Specifies the options for retry in case of failed attempts to push to the output adapter.

    -   `max_attempts` - Maximum number of retry attempts. Default value is `10`
    -   `delay` - Minimum amount of delay between attempts, in seconds. Default value is `2`
    -   `exponent_base` - Factor that determines the growth of the delay time over each failed attempt. Default value is `2`

    The formula is:

        **`d(nth_retry) - delay * (exponent_base ^ nth_retry)`**

    For example, the default settings with a delay of 1 second and an exponent base of 2, will cause the second retry - the third attempt - to delay 2 seconds instead of 1, and the next to delay 4 seconds.

        `d(0) - 1 * (2 ^ 0)` - 1 second
        `d(1) - 1 * (2 ^ 1)` - 2 seconds
        `d(2) - 1 * (2 ^ 2)` - 4 seconds

    So, with the default settings, a submission will be attempted up to 10 times, waiting up to approximately 1022 seconds - a little more than 17 minutes. This time is approximate because there is additional time added in order to avoid having multiple resubmissions execute simultaneously. This "fuzzed" time is up to 10%, so the last retry in the previous example could delay up to 7.7 seconds. The wait time does not include the time spent connecting to the service, uploading data, or waiting for a response.

    The `output_timeout` value takes precedence over the wait time here: if the total retry wait time exceeds that setting, the submission will fail even if it should have been retried.
    {: tip}

### Additional crawl management options
{: #additional-crawl-management-options}

-   **`full_node_debugging`** - Activates debugging mode; possible values are `true` or `false`.

    **Important:** This will put the full data of every document crawled into the logs.   

-   **`logging.log4j.configuration_file`*** - The configuration file to use for logging. In the sample `crawler.conf` file, this option is defined in `logging.log4j` and its default value is `log4j_custom.properties`. This option must be similarly defined whether using a `.properties` or `.conf` file.   
-   **`shutdown_timeout`** - Specifies the timeout value, in minutes, before shutting down the application. Default value is `10`.   
-   **`output_limit`** - The highest number of indexable items that the Crawler will try to send simultaneously to the output adapter. This can be further limited by the number of cores available to do the work. It says that at any given point there will be no more than "x" indexable items sent to the output adapter waiting to return. Default value is `10`.   
-   **`input_limit`** - Limits the number of URLs that can be requested from the input adapter at one time. Default value is `30`.   
-   **`output_timeout`** - The amount of time, in seconds, before the Data Crawler gives up on a request to the output adapter, and then removes the item from the output adapter queue to allow more processing. Default value is `1200`.

    Consideration should be given to the constraints imposed by the output adapter, as those constraints may relate to the limits defined here. The defined `output_limit` only relates to how many indexable objects can be sent to the output adapter at once. Once an indexable object is sent to the output adapter, it is "on the clock," as defined by the `output_timeout` variable. It is possible that the output adapter itself has a throttle preventing it from being able to process as many inputs as it receives. For instance, the orchestration output adapter may have a connection pool, configurable for HTTP connections to the service. If it defaults to 8, for example, and if you set the `output_limit` to a number greater than 8, then you will have processes, on the clock, waiting for a turn to execute. You may then experience timeouts.   
-   **`num_threads`** - The number of parallel threads that can be run at one time. This value can be either an integer, which specifies the number of parallel threads directly, or it can be a string, with the format `"xNUM"`, specifying the multiplication factor of the number of available processors, for example, `"x1.5"`. The default value is `"30"`

## Configuring service options
{: #configuring-service-options}

The {{site.data.keyword.discoveryshort}} service tells the crawler how to manage crawled files when using the {{site.data.keyword.discoveryfull}} service.

To access the in-product manual for the `discovery-service.conf` file, with the most up-to-date information, type the following command from the Crawler installation directory:

  ```bash
  man discovery_service.conf
  ```
  {: pre}
{: tip}

Default options can be changed directly by opening the `config/discovery/discovery_service.conf` file, and specifying the following values specific to your use case:

-   **`http_timeout`** - The timeout, in seconds, for the document read/index operation; the default is `125`.
-   **`proxy_host_port`** - (optional) When running the data crawler behind a firewall, you might need to set the proxy hostname and proxy port number in order for the data crawler to talk to the {{site.data.keyword.discoveryshort}} service. The default value for this option is an empty string and if you need to change it the value should be of the form `"<host>:<port>"`.
-   **`concurrent_upload_connection_limit`** - The number of simultaneous connections allowed for uploading documents. The default is `2`.

    **Note:** When using the Orchestration Service Output Adapter, this number should be greater than, or equal to, the `output_limit` set when configuring crawl options.   

-   **`base_url`** - The URL to which your crawled documents will be sent. For the current release of the {{site.data.keyword.discoveryshort}} service, the value is `https://gateway.watsonplatform.net/discovery/api`.   
-   **`environment_id`** - The location of your crawled document collection at the base URL.   
-   **`collection_id`** - Name of the document collection that you set up in the {{site.data.keyword.discoveryshort}} service.
-   **`api_version`** - Internal use only. Date of the last API version change.   
-   **`configuration_id`** - The filename of the configuration file that the {{site.data.keyword.discoveryshort}} service uses.
-   **`username`** - Username to authenticate to the location of your crawled document collection.   
-   **`password`** - Password to authenticate to the location of your crawled document collection.

The {{site.data.keyword.discoveryshort}} Service Output Adapter can send statistics in order for {{site.data.keyword.IBM}} to better understand and serve its users. The following options can be set for the `send_stats` variable:

-   **`jvm`** - Java Virtual Machine (JVM) statistics sent include the Java vendor and version, as reported by the JVM used to execute the data crawler. Value is either `true` or `false`. Default value is `true`.
-   **`os`** - Operating system (OS) statistics sent include OS name, version, and architecture, as reported by the JVM used to execute the data crawler. Value is either `true` or `false`. Default value is `true`.
