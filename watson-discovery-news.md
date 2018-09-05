---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-05"

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

{{site.data.keyword.discoverynewsfull}} is included with {{site.data.keyword.discoveryshort}}. {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} is an indexed dataset that is pre-enriched with the following cognitive insights: **Keyword Extraction**, **Entity Extraction**, **Semantic Role Extraction**, **Sentiment Analysis**, **Relation Extraction**, and **Category Classification**. (To learn more about enrichments, see [Adding enrichments](building.html#adding-enrichments).) The following additional metadata is also added: crawl date and publication date. Historical search is available for the past 60 days of news data. See a demo of what you can build with {{site.data.keyword.discoverynewsfull}} [here ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://discovery-news-demo.ng.bluemix.net/){: new_window}.

{{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} is updated continuously with new articles, and is available in English, Spanish, German, Korean, and Japanese. {{site.data.keyword.discoverynewsshort}} English is updated with approximately 300,000 new articles daily. {{site.data.keyword.discoverynewsshort}} Spanish is updated with approximately 60,000 new articles daily; {{site.data.keyword.discoverynewsshort}} German is updated with approximately 40,000 new articles daily; {{site.data.keyword.discoverynewsshort}} Korean with 10,000 new articles daily. {{site.data.keyword.discoverynewsshort}} Japanese is updated with approximately 17,000 new articles daily. The news sources vary by language, so the query results for each collection will not be identical.

Use cases for {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}}:

- News alerting - Create news alerts by taking advantage of the support for entities, keywords, categories, and sentiment analysis to watch for both news and how it is perceived.

- Event detection - The subject/action/object semantic role extraction checks for terms/actions such as "acquisition", "election results", or "IPO".

- Trending topics in the news -  Identify popular topics and monitor increases and decreases in how frequently they (or related topics) are mentioned.

For information about writing queries for {{site.data.keyword.discoverynewsfull}}, see:
- [Querying Watson Discovery News](/docs/services/discovery/using.html#querying-news)
- [Query concepts](/docs/services/discovery/using.html)
- [Query reference](/docs/services/discovery/query-reference.html).

You cannot adjust the {{site.data.keyword.discoverynewsfull}} configuration, train, or add documents to the {{site.data.keyword.discoverynewsfull}} collection.

{{site.data.keyword.discoverynewsfull}} queries display the first 50 words of each article in the `text` JSON field.

The maximum number of results returned for a {{site.data.keyword.discoverynewsfull}} query is `50`. Use additional queries and the `offset` parameter to return more than `50` results.

**Note:** This version of {{site.data.keyword.discoverynewsfull}} debuted on **31, July 2017**. {{site.data.keyword.discoverynewsfull}} Original was retired from service **15, January 2018**. For information on migrating, see [Migrating from Watson Discovery News Original](/docs/services/discovery/migrate-bwdn.html).
