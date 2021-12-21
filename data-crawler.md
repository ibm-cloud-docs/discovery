---

copyright:
  years: 2015, 2020
lastupdated: "2020-02-06"

subcollection: discovery

---

{{site.data.keyword.attribute-definition-list}}

# Adding content with the Data Crawler
{: #adding-content-with-data-crawler}

The Data Crawler is no longer supported or available for download beginning [17 April 2019](/docs/discovery?topic=discovery-release-notes#17apr19). This content is provided for existing installations only. See [Connecting to Data Sources](/docs/discovery?topic=discovery-sources) for other available connectivity options.
{: important}

The data crawler lets you automate the upload of content to the {{site.data.keyword.discoveryshort}} Service.
{: shortdesc}

## Crawling data with the Data Crawler
{: #dc-crawling}

The Data Crawler is a command line tool that helps you take your documents from the repositories where they reside (for example: file shares, databases) and push them to the cloud, to be used by {{site.data.keyword.discoveryshort}}.

## When to use the Data Crawler
{: #dc-use}

Use the Data Crawler if you want to have a managed upload of a significant number of files from a remote system or if you want to extract content from a supported repository, such as a DB2 database.

The Data Crawler is not intended to be a solution for uploading files from your local drive. If you upload files from a local drive, use the tooling or direct API calls. Another option to upload large numbers of files into {{site.data.keyword.discoveryshort}} is [discovery-files](https://github.com/IBM/discovery-files){: external} on GitHub.
{: note}

## Using the Data Crawler
{: #dc-using}

1. [Configure {{site.data.keyword.discoveryshort}}](/docs/discovery?topic=discovery-configservice).
1. [Download and install the Data Crawler](/docs/discovery?topic=discovery-downloading-and-installing-the-data-crawler) on a supported Linux system that has access to the content that you want to crawl.
1. [Connect the Data Crawler](/docs/discovery?topic=discovery-configuring-connector-and-seed-options) to your content.
1. [Configure the Data Crawler](/docs/discovery?topic=discovery-configuring-the-data-crawler) to connect to the {{site.data.keyword.discoveryshort}} Service.
1. [Crawl your content](/docs/discovery?topic=discovery-crawling-your-data-repository).

You can get started quickly with the Data Crawler by following the example in [Getting started with the Data Crawler](/docs/discovery?topic=discovery-getting-started-with-the-data-crawler).
