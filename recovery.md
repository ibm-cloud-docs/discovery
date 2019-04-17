---

copyright:
  years: 2019
lastupdated: "2019-04-17"

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

# High availability and disaster recovery
{: #recovery}

{{site.data.keyword.discoveryfull}} is highly available within multiple {{site.data.keyword.cloud_notm}} locations (for example, Dallas and Washington, DC). However, recovering from potential disasters that affect an entire location requires planning and preparation.
{: shortdesc}

You are responsible for understanding your configuration, customization, and usage of the service. You are also responsible for being ready to re-create an instance of the service in a new location and to restore your data in any location. See [How do I ensure zero downtime? ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/overview?topic=overview-zero-downtime#zero-downtime){: new_window} for more information.

## High availability
{: #ha}

{{site.data.keyword.discoveryfull}} supports high availability with no single point of failure. The service achieves high availability automatically and transparently by using the multi-zone region (MZR) feature provided by {{site.data.keyword.cloud_notm}}.

{{site.data.keyword.cloud_notm}} enables multiple zones that do not share a single point of failure within a single location. It also provides automatic load balancing across the zones within a region.

## Disaster recovery
{: #dr}

Disaster recovery can become an issue if an {{site.data.keyword.cloud_notm}} location experiences a significant failure that includes the potential loss of data. Because MZR is not available across locations, you must wait for IBM to bring a location back online if it becomes unavailable. If underlying data services are compromised by the failure, you must also wait for IBM to restore those data services.

If a catastrophic failure occurs, IBM might not be able to recover data from database backups. In this case, you need to restore your data to return your service instance to its most recent state. You can restore the data to the same or to a different location.

Your disaster recovery plan includes knowing, preserving, and being prepared to restore all data that is maintained on {{site.data.keyword.cloud_notm}}. 

## Backing up your data in Watson Discovery
{: #backup}

There are several methods for backing up the data stored in {{site.data.keyword.discoveryfull}}. These methods should be included in your disaster recovery plan. 

-  Data you should keep a copy of, such as source documents
-  Data {{site.data.keyword.discoveryshort}} stores and you should extract and backup
  
There will be data that will need to be recreated from scratch (for example, data that you can't backup, such as feedback events.) 

### Ingested documents
{: #backupdocs}

Your uploaded documents are converted and enriched, then stored in the search index. The search index is not recoverable in the case of a disaster, and therefore you should store a backup of all your source documents in a safe place.

If you also import documents by doing scheduled crawls of external data sources, you should retain your data source credentials externally so that you can reestablish your data sources quickly. See [Connecting to data sources](/docs/services/discovery?topic=discovery-sources#sources) for the list of available sources and the credentials needed for each one.

### Configurations
{: #backupconfigs}

You should back up your instance configurations and store it locally in the event of a disaster. 

To backup these configurations, first [list your configurations](https://cloud.ibm.com/apidocs/discovery#list-configurations) for each instance. 

After obtaining the list of configurations, [get the details](https://cloud.ibm.com/apidocs/discovery#get-configuration-details) for each configuration.

### Training data
{: #backuptraining}

You should backup your training data for each trained collection and store it locally in the event of a disaster.  

Training data is used for explicit training of your collections and is stored on a per collection basis. 

To extract the training data, use the API to download the queries and the ratings from {{site.data.keyword.discoveryshort}}. 

1.  [List the training data](https://cloud.ibm.com/apidocs/discovery#list-training-data)
1.  [List the examples](https://cloud.ibm.com/apidocs/discovery#list-examples-for-a-training-data-query) for each query.
1.  [Get the details](https://cloud.ibm.com/apidocs/discovery#get-details-for-training-data-example) for a training data examples. 

The `document ids` you use in your training data point to the documents in your current collection. You MUST use the same `document ids` in your new collections to ensure that the correct ids are referenced. If you do not, your restored relevancy training WILL NOT WORK.
{: important} 

### Queries
{: #backupqueries}

By default (unless you opt out), {{site.data.keyword.discoveryshort}} will store the queries you send to it. 

If you want to be able to restore these for [statistical purposes](https://cloud.ibm.com/apidocs/discovery#number-of-queries-over-time), you should store those queries separately. 

You can [extract queries](https://cloud.ibm.com/apidocs/discovery#search-the-query-and-event-log) from {{site.data.keyword.discoveryshort}}, however a maximum of 10,000 queries are stored. There is no paging API. Restoring queries is not recommended; we recommend starting from scratch. 

### Feedback/clicks
{: #clicks}

If you are storing clicks in the form of feedback events, there is currently no easy way to backup and restore this information. The recommendation is to start from scratch with the [clicks/feedback data](https://cloud.ibm.com/apidocs/discovery#create-event) API. 

### Expansion lists
{: #backupexpansions}

If you are using expansions for query modification, you should backup your expansion list and store it locally. To do so, request the expansion list using the [get expansion list](https://cloud.ibm.com/apidocs/discovery#get-the-expansion-list) API command and store it locally.

### Tokenization dictionaries or stopwords
{: #backupstopwords}

If you use these capabilities, you will need to backup these files and store them locally. In the case of stopwords, backup the text file, and in the case of the tokenizations you should backup the JSON file. See [Creating custom tokenization dictionaries](/docs/services/discovery?topic=discovery-query-concepts#tokenization) and [Defining stopwords](/docs/services/discovery?topic=discovery-query-concepts#stopwords) for more information about each file type.

### Collection information
{: #collectioninfo}

This is not required, but it is a good best practice to [retrieve the status](https://cloud.ibm.com/apidocs/discovery#get-collection-details) for each collection on a regular basis and store the information locally. By retaining these statistics, you can later verify that your restoration processes were successful if needed.
{: tip} 


### Smart Document Understanding models
{: #backupsdu}

If you are using Smart Document Understanding (SDU), you will have models associated with your configuration. To avoid loss of this information you should [export your models](/docs/services/discovery?topic=discovery-sdu#import), back them up and store them locally. SDU models have the file extension of `.sdumodel`.


## Restoring your data to a new Watson Discovery instance
{: #restore}

Consider using your backups to restore to a new {{site.data.keyword.discoveryshort}} instance in a different Data Center (also known as a region/location - for example, Dallas, Houston, Washington, DC, London). 
{: note}

To begin restoration, first start by reviewing your list of collections and associated data sources, as well as your file backups.

-  Create your [environment](https://cloud.ibm.com/apidocs/discovery#create-an-environment) and [collections](https://cloud.ibm.com/apidocs/discovery#create-a-collection) using the saved configuration information. Ensure that the appropriate configuration is defined appropriately, and that the language for the collection is set properly. Failure to do so will delay getting your system back up and running.
-  If you had any custom configurations set up in {{site.data.keyword.discoveryshort}}, you'll need to [re-create those custom configurations](/docs/services/discovery?topic=discovery-configservice#when-you-need-a-custom-configuration). 
-  Add back tokenization dictionaries or stopwords into the collections. See [Creating custom tokenization dictionaries](/docs/services/discovery?topic=discovery-query-concepts#tokenization) and [Defining stopwords](/docs/services/discovery?topic=discovery-query-concepts#stopwords).  
-  If you had custom query expansion, you will need to [add your query expansions](https://cloud.ibm.com/apidocs/discovery#create-or-update-expansion-list) for each collection as well. 
-  If you were using any custom entity models from Watson Knowledge Studio (WKS) for enrichment, you'll need to [re-import that model](/docs/services/discovery?topic=discovery-configservice#custom-entity-model) into your {{site.data.keyword.discoveryshort}} instance. 

After you have your collections setup as before - then you will need to begin ingesting your source documents. Depending upon how you ingested your documents previously, you can do so using:
-  The [API](https://cloud.ibm.com/apidocs/discovery#add-a-document)
-  A [connector](/docs/services/discovery?topic=discovery-sources#sources) 
-  or other method

### Restoring training data
{: #restoretraining}

After collections have been restored, you can begin the process of [recreating your relevancy training models](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api). 

Retrieve the training data you backed up, then:

1. [Upload your queries](https://cloud.ibm.com/apidocs/discovery#add-query-to-training-data)
1. [Upload the example documents](https://cloud.ibm.com/apidocs/discovery#add-example-to-training-data-query) for each query.
1.  After training data is uploaded, review this [blog post](https://developer.ibm.com/dwblog/2017/get-relevancy-training/) to ensure you meet the previous accuracy numbers. Keep in mind that old `document ids` must be transferred to the new training data, or updated to reflect the new document ids in your new collection.


### Restoring connections to external data sources
{: #restoreconnections}

In case of an unanticipated loss of data, you may lose your scheduled crawls of external data sources. See [Connecting to data sources](/docs/services/discovery?topic=discovery-sources#sources) for the list of available sources.

To restore your external data, you'll need to reestablish your connections to these data sources, and then re-crawl them.

Find the data source credentials you stored previously and follow the instructions [here](/docs/services/discovery?topic=discovery-sources#sources). This will allow you to re-connect to your data sources, and get the data imported into {{site.data.keyword.discoveryshort}}.


### Restoring Smart Document Understanding models
{: #restoresdu}

To import a previously exported Smart Document Understanding (SDU) model follow the instructions [here](/docs/services/discovery?topic=discovery-sdu#import). SDU models have the file extension of `.sdumodel`.

When importing an SDU existing model into a new collection, it is a good best practice to create the new collection and add one document, then import the model and upload the remainder of your documents.