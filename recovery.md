---

copyright:
  years: 2019, 2023
lastupdated: "2023-01-26"

subcollection: discovery

---

{{site.data.keyword.attribute-definition-list}}

# High availability and disaster recovery
{: #recovery}

{{site.data.keyword.discoveryfull}} is highly available within multiple {{site.data.keyword.cloud_notm}} locations (for example, Dallas and Washington, DC). However, recovering from potential disasters that affect an entire location requires planning and preparation.
{: shortdesc}

You are responsible for understanding your configuration, customization, and usage of the service. You are also responsible for being ready to re-create an instance of the service in a new location and to restore your data in any location. See [How do I ensure zero downtime?](/docs/overview?topic=overview-zero-downtime#zero-downtime){: external} for more information.

## High availability
{: #ha}

{{site.data.keyword.discoveryfull}} supports high availability with no single point of failure. The service achieves high availability automatically and transparently by using the multi-zone region (MZR) feature provided by {{site.data.keyword.cloud_notm}}.

{{site.data.keyword.cloud_notm}} enables multiple zones that do not share a single point of failure within a single location. It also provides automatic load balancing across the zones within a region.

## Disaster recovery
{: #dr}

Disaster recovery can become an issue if an {{site.data.keyword.cloud_notm}} location experiences a significant failure that includes the potential loss of data. Because MZR is not available across locations, wait for IBM to bring a location back online if it becomes unavailable. If underlying data services are compromised by the failure, also wait for IBM to restore those data services.

If a catastrophic failure occurs, IBM might not be able to recover data from database backups. In this case, you need to restore your data to return your service instance to its most recent state. You can restore the data to the same or to a different location.

Your disaster recovery plan includes knowing, preserving, and being prepared to restore all data that is maintained on {{site.data.keyword.cloud_notm}}.

## Backing up your data in Watson Discovery
{: #backup}

There are several methods for backing up the data stored in {{site.data.keyword.discoveryfull}}. Consider including these methods in your disaster recovery plan. Also consider backing up the following data types:

-  Data that you might want a copy of, such as source documents
-  Data that {{site.data.keyword.discoveryshort}} stores and that you want to extract and back up
  
Some data you cannot back up and must be recreated. For example, feedback events.

### Ingested documents
{: #backupdocs}

Your uploaded documents are converted, enriched, and stored in the search index. In the event of a disaster, the search index is not recoverable. Store a backup of all your source documents in a safe place.

If you also import documents by doing scheduled crawls of external data sources, you might want to retain your data source credentials externally so that you can re-establish your data sources quickly. For the list of available sources and the credentials needed for each one, see [Connecting to data sources](/docs/discovery?topic=discovery-sources).

### Configurations
{: #backupconfigs}

Back up your instance configurations, and store them locally.

To back up these configurations, first [list your configurations](/apidocs/discovery#list-configurations){: external} for each instance.

After obtaining the list of configurations, [get the details](/apidocs/discovery#get-configuration-details){: external} for each configuration.

### Training data
{: #backuptraining}

Back up your training data for each trained collection, and store it locally.  

Training data is used for explicit training of your collections and is stored on a per collection basis.

To extract the training data, use the API to download the queries and the ratings from {{site.data.keyword.discoveryshort}}.

1.  [List the training data](/apidocs/discovery#list-training-data){: external}
1.  [List the examples](/apidocs/discovery#list-examples-for-a-training-data-query){: external} for each query.
1.  [Get the details](/apidocs/discovery#get-details-for-training-data-example){: external} for a training data examples.

The document IDs that you use in your training data point to the documents in your current collection. Use the same IDs in your new collections to ensure that the correct documents are referenced. If the IDs do not match, your restored relevancy training will not work.
{: important}

### Queries
{: #backupqueries}

By default, {{site.data.keyword.discoveryshort}} stores the queries that you send to it, unless you opt out.

If you want to be able to restore your queries for [statistical purposes](https://cloud.ibm.com/apidocs/discovery#number-of-queries-over-time), it is recommended that you store those queries separately.

You can [extract queries](/apidocs/discovery#search-the-query-and-event-log){: external} from {{site.data.keyword.discoveryshort}}, however a maximum of 10,000 queries are stored. There is no paging API. Restoring queries is not recommended; we recommend starting from scratch.

### Feedback/clicks
{: #clicks}

If you are storing clicks in the form of feedback events, there is currently no easy way to back up and restore this information. The recommendation is to start from scratch with the [clicks/feedback data](/apidocs/discovery#create-event){: external} API.

### Expansion lists
{: #backupexpansions}

If you are using expansions for query modification, back up your expansion list, and store it locally. To do so, request the expansion list ,using the [get expansion list](/apidocs/discovery#get-the-expansion-list){: external} API command, and store it locally.

### Tokenization dictionaries or stopwords
{: #backupstopwords}

If you use these capabilities, back up these files, and store them locally. In the case of stopwords, back up the text file, and in the case of the tokenizations, back up the JSON file. For more information about each file type, see [Creating custom tokenization dictionaries](/docs/discovery?topic=discovery-query-concepts#tokenization) and [Defining stopwords](/docs/discovery?topic=discovery-query-concepts#stopwords).

### Collection information
{: #collectioninfo}

This is not required, but it is a good best practice to [retrieve the status](/apidocs/discovery#get-collection-details){: external} for each collection on a regular basis and store the information locally. By retaining these statistics, you can later verify that your restoration processes were successful if needed.
{: tip} 


### Smart Document Understanding models
{: #backupsdu}

If you use Smart Document Understanding (SDU), you have models associated with your configuration. To avoid loss of this information, [export your models](/docs/discovery?topic=discovery-sdu#import), back them up, and store them locally. SDU models have the file extension of `.sdumodel`.


## Restoring your data to a new Watson Discovery instance
{: #restore}

Consider using your backups to restore to a new {{site.data.keyword.discoveryshort}} instance in a different Data Center, also known as a region or location. For example, these regions or locations include Dallas, Washington DC, and London).
{: note}

To begin restoration, first start by reviewing your list of collections and associated data sources, as well as your file backups.

-  Create your [environment](/apidocs/discovery#create-an-environment){: external} and [collections](/apidocs/discovery#create-a-collection){: external} using the saved configuration information. Ensure that the appropriate configuration is defined appropriately, and that the language for the collection is set properly. Failure to do so delays getting your system back up and running.
-  If you have any custom configurations set up in {{site.data.keyword.discoveryshort}}, recreate them. See the [API reference](/apidocs/discovery#add-configuration){: external} for details.
-  Add back tokenization dictionaries or stopwords into the collections. See [Creating custom tokenization dictionaries](/docs/discovery?topic=discovery-query-concepts#tokenization) and [Defining stopwords](/docs/discovery?topic=discovery-query-concepts#stopwords).  
-  If you use custom query expansion, [add your query expansions](/apidocs/discovery#create-or-update-expansion-list){: external} for each collection, as well.
-  If you use any custom entity models from {{site.data.keyword.knowledgestudiofull}} for enrichment, [reimport that model](/docs/discovery?topic=discovery-configservice#custom-entity-model) into your {{site.data.keyword.discoveryshort}} instance.

After you set up your collections as it was before, begin ingesting your source documents. Depending upon how you ingested your documents previously, you can do so by using your own solution or one of the following methods:
-  The [API](/apidocs/discovery#add-a-document){: external}
-  A [connector](/docs/discovery?topic=discovery-sources)

### Restoring training data
{: #restoretraining}

After you restore the collections, you can begin the process of [recreating your relevancy training models](/docs/discovery?topic=discovery-improving-result-relevance-with-the-api). 

Retrieve the training data you backed up, then:

1. [Upload your queries](/apidocs/discovery#add-query-to-training-data){: external}.
1. [Upload the example documents](/apidocs/discovery#add-example-to-training-data-query){: external} for each query.
1.  After training data is uploaded, review this [blog post](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: external} to ensure you meet the previous accuracy numbers. Keep in mind that old `document ids` must be transferred to the new training data, or updated to reflect the new document ids in your new collection.


### Restoring connections to external data sources
{: #restoreconnections}

In case of an unanticipated loss of data, you might lose your scheduled crawls of external data sources. See [Connecting to data sources](/docs/discovery?topic=discovery-sources) for the list of available sources.

To restore your external data, re-establish your connections to these data sources, and then re-crawl them.

To find the data source credentials that you stored, follow the instructions for your chosen data source in [Connecting to Data Sources](/docs/discovery?topic=discovery-sources). These instructions explain how you can reconnect to your data sources and get the data imported into {{site.data.keyword.discoveryshort}}.


### Restoring Smart Document Understanding models
{: #restoresdu}

To import a previously exported Smart Document Understanding (SDU) model, see [Importing and exporting models](/docs/discovery?topic=discovery-sdu#import). SDU models have the file extension of `.sdumodel`.

When importing an SDU existing model into a new collection, it is a good best practice to create the new collection and add one document, then import the model and upload the remainder of your documents.