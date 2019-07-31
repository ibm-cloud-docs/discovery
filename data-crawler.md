---

copyright:
  years: 2015, 2017, 2019
lastupdated: "2019-07-29"

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

# Adding content with the Data Crawler
{: #adding-content-with-data-crawler}

The Data Crawler is no longer supported or available for download beginning [17 April 2019](/docs/services/discovery?topic=discovery-release-notes#17apr19). This content is provided for existing installations only. See [Connecting to Data Sources](/docs/services/discovery?topic=discovery-sources#sources) for other available connectivity options.
{:important}

The data crawler lets you automate the upload of content to the {{site.data.keyword.discoveryshort}} Service.
{: shortdesc}

## Crawling data with the Data Crawler
{: #dc-crawling}

The Data Crawler is a command line tool that will help you take your documents from the repositories where they reside (for example: file shares, databases) and push them to the cloud, to be used by {{site.data.keyword.discoveryshort}}.

## When to use the Data Crawler
{: #dc-use}

The Data Crawler should be used if you want to have a managed upload of a significant number of files from a remote system, or you want to extract content from a supported repository (such as a DB2 database).

The Data Crawler is not intended to be a solution for uploading files from your local drive. Uploading files from a local drive should be done using the tooling or by using direct API calls. Another option to upload large numbers of files into {{site.data.keyword.discoveryshort}} is [discovery-files ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM/discovery-files){: new_window} on GitHub.
{: note}

## Using the Data Crawler
{: #dc-using}

1. [Configure {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-configservice#configservice)
1. [Download and install the Data Crawler](/docs/services/discovery?topic=discovery-downloading-and-installing-the-data-crawler#downloading-and-installing-the-data-crawler) on a supported Linux system that has access to the content that you want to crawl.
1. [Connect the Data Crawler](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-connector-and-seed-options) to your content.
1. [Configure the Data Crawler](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-the-data-crawler) to connect to the {{site.data.keyword.discoveryshort}} Service.
1. [Crawl your content](/docs/services/discovery?topic=discovery-crawling-your-data-repository#crawling-your-data-repository).

You can get started quickly with the Data Crawler by following the example in: [Getting started with the Data Crawler](/docs/services/discovery?topic=discovery-getting-started-with-the-data-crawler#getting-started-with-the-data-crawler)
