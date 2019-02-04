---

copyright:
  years: 2015, 2017, 2019
lastupdated: "2019-01-28"

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

# Adding content with Data Crawler

The data crawler lets you automate the upload of content to the {{site.data.keyword.discoveryshort}} Service.
{: shortdesc}

The Data Crawler should only be used to crawl file shares or databases, in all other cases you should use the appropriate {{site.data.keyword.discoveryshort}} connector. See [Connecting to data sources](/docs/services/discovery/connect.html) for details. Assistance is no longer provided for the Data Crawler if you are using it with a data source supported by the {{site.data.keyword.discoveryshort}} connectors.
{: important}

## Crawling data with the Data Crawler

The Data Crawler is a command line tool that will help you take your documents from the repositories where they reside (for example: file shares, databases) and push them to the cloud, to be used by the {{site.data.keyword.discoveryshort}} service.

The Data Crawler should only be used to crawl file shares or databases, in all other cases you should use the appropriate {{site.data.keyword.discoveryshort}} connector for Box, SharePoint, Salesforce or web crawl. See [Connecting to data sources](/docs/services/discovery/connect.html) for details. Assistance is no longer provided for the Data Crawler if you are using it with a data source supported by the {{site.data.keyword.discoveryshort}} connectors.
{: important}

## When to use the Data Crawler

The Data Crawler should be used if you want to have a managed upload of a significant number of files from a remote system, or you want to extract content from a supported repository (such as a DB2 database).

The Data Crawler is not intended to be a solution for uploading files from your local drive. Uploading files from a local drive should be done using the tooling or by using direct API calls. Another option to upload large numbers of files into {{site.data.keyword.discoveryshort}} is [discovery-files ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM/discovery-files){: new_window} on GitHub.
{: note}

## Using the Data Crawler

1. [Configure the {{site.data.keyword.discoveryshort}} service](/docs/services/discovery/building.html#configservice)
1. [Download and install the Data Crawler](/docs/services/discovery/data-crawler-install.html) on a supported Linux system that has access to the content that you want to crawl.
1. [Connect the Data Crawler](/docs/services/discovery/data-crawler-seeds.html) to your content.
1. [Configure the Data Crawler](/docs/services/discovery/data-crawler-discovery.html) to connect to the {{site.data.keyword.discoveryshort}} Service.
1. [Crawl your content](/docs/services/discovery/data-crawler-run.html).

You can get started quickly with the Data Crawler by following the example in: [Getting started with the Data Crawler](/docs/services/discovery/data-crawler-qs.html)
