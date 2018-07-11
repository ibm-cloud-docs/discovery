---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-03"

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

# Adding content with Data Crawler

The data crawler lets you automate the upload of content to the {{site.data.keyword.discoveryshort}} Service.
{: shortdesc}

## Crawling data with the Data Crawler

The Data Crawler is a command line tool that will help you take your documents from the repositories where they reside (for example: file shares, databases, Microsoft SharePoint) and push them to the cloud, to be used by the {{site.data.keyword.discoveryshort}} Service.

You can use the {{site.data.keyword.discoveryshort}} tooling or API to crawl Box, Salesforce, and Microsoft SharePoint Online data sources. See [Connecting to data sources](/docs/services/discovery/connect.html) for more information.
{: tip}

## When to use the Data Crawler

The Data Crawler should be used if you want to have a managed upload of a significant number of files from a remote system, or you want to extract content from a supported repository (such as a DB2 database).

The Data Crawler is not intended to be a solution for uploading files from your local drive. Uploading files from a local drive should be done using the tooling or by using direct API calls.
{: tip}

## Using the Data Crawler

1. [Configure the {{site.data.keyword.discoveryshort}} service](/docs/services/discovery/building.html#configuring-your-service)
1. [Download and install the Data Crawler](/docs/services/discovery/data-crawler-install.html) on a supported Linux system that has access to the content that you want to crawl.
1. [Connect the Data Crawler](/docs/services/discovery/data-crawler-seeds.html) to your content.
1. [Configure the Data Crawler](/docs/services/discovery/data-crawler-discovery.html) to connect to the {{site.data.keyword.discoveryshort}} Service.
1. [Crawl your content](/docs/services/discovery/data-crawler-run.html).

You can get started quickly with the Data Crawler by following the example in: [Getting started with the Data Crawler](/docs/services/discovery/data-crawler-qs.html)
