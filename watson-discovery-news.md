---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-25"

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

# Watson Discovery News

{{site.data.keyword.discoverynewsfull}} is included with {{site.data.keyword.discoveryshort}}. {{site.data.keyword.discoverynewsfull}} is a dataset of English-language news sources that is updated continuously, with approximately 300,000 new articles and blogs added daily. This indexed dataset is pre-enriched with the following cognitive insights: **Keyword Extraction**, **Entity Extraction**, **Semantic Role Extraction**, **Sentiment Analysis**, **Relations**, and **Category Classification**. (To learn more about enrichments, see [Adding enrichments](building.html#adding-enrichments).) The following additional metadata is also added: crawl date and publication date. Historical search is available for the past 60 days of news data. See a demo of what you can build with {{site.data.keyword.discoverynewsfull}} [here ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://discovery-news-demo.mybluemix.net/){: new_window}.

Use cases for Watson Discovery News:

- News alerting - Create news alerts by taking advantage of the support for entities, keywords, categories, and sentiment analysis to watch for both news and how it is perceived.

- Event detection - The subject/action/object semantic role extraction checks for terms/actions such as "acquisition", "election results", or "IPO".

- Trending topics in the news -  Identify popular topics and monitor increases and decreases in how frequently they (or related topics) are mentioned.

For information about writing queries for {{site.data.keyword.discoverynewsfull}}, see [Query concepts](/docs/services/discovery/using.html) and [Query reference](/docs/services/discovery/query-reference.html).

You cannot adjust the {{site.data.keyword.discoverynewsfull}} configuration, train, or add documents to the {{site.data.keyword.discoverynewsfull}} collection.

**Note:** The maximum number of results returned for a Watson Discovery News query is `50`. Use additional queries and the `offset` parameter to return more than `50` results.

**Note:** This version of {{site.data.keyword.discoverynewsfull}} debuted on **31, July 2017**. The original version has been renamed {{site.data.keyword.discoverynewsfull}} Original and has been retired with a removal from service date of **15, January 2018**. For information on migrating, see [Migrating from Watson Discovery News Original](/docs/services/discovery/migrate-bwdn.html).
