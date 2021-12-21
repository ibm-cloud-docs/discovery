---

copyright:
  years: 2015, 2021
lastupdated: "2021-12-21"

subcollection: discovery

---

{{site.data.keyword.attribute-definition-list}}

# Watson Discovery News
{: #watson-discovery-news}

{{site.data.keyword.discoverynewsfull}} is included with {{site.data.keyword.discoveryshort}}. {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} is an indexed dataset that is pre-enriched with the following cognitive insights: **Keyword Extraction**, **Entity Extraction**, **Semantic Role Extraction**, **Sentiment Analysis**, **Relation Extraction**, and **Category Classification**. (To learn more about enrichments, see [Adding enrichments](/docs/discovery?topic=discovery-configservice#adding-enrichments).) The following additional metadata is also added: crawl date and publication date. Historical search is available for the past 60 days of news data.

The Watson Discovery News feature is deprecated as of 8 October 2021. Existing News collections are available and support continues until 8 October 2022, after which date they will no longer be accessible.
{: deprecated}

{{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} is updated continuously with new articles, and is available in English, Spanish, German, Korean, French, and Japanese. {{site.data.keyword.discoverynewsshort}} English is updated with approximately 200,000 new articles daily; {{site.data.keyword.discoverynewsshort}} Spanish is updated with approximately 60,000 new articles daily; {{site.data.keyword.discoverynewsshort}} German is updated with approximately 15,000 new articles daily; {{site.data.keyword.discoverynewsshort}} Korean with 10,000 new articles daily; {{site.data.keyword.discoverynewsshort}} French with 23,000 new articles daily; {{site.data.keyword.discoverynewsshort}} Japanese is updated with approximately 17,000 new articles daily. The news sources vary by language, so the query results for each collection are not identical.

Use cases for {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}}:

- News alerting - Create news alerts by taking advantage of the support for entities, keywords, categories, and sentiment analysis to watch for both news and how it is perceived.

- Event detection - The subject/action/object semantic role extraction checks for terms/actions such as "acquisition", "election results", or "IPO".

- Trending topics in the news -  Identify popular topics and monitor increases and decreases in how frequently they (or related topics) are mentioned.

For information about writing queries for {{site.data.keyword.discoverynewsfull}}, see:
- [Querying Watson Discovery News](/docs/discovery?topic=discovery-query-concepts#querying-news)
- [Query concepts](/docs/discovery?topic=discovery-query-concepts)
- [Query reference](/docs/discovery?topic=discovery-query-reference)

You cannot adjust the {{site.data.keyword.discoverynewsfull}} configuration, train, or add documents to the {{site.data.keyword.discoverynewsfull}} collection.

{{site.data.keyword.discoverynewsfull}} queries display approximately 50 words from each article in the `text` JSON field. These words are extracted from the highlights. See [highlight](/docs/discovery?topic=discovery-query-parameters#highlight) for an explanation of highlights. Highlights do not need to be explicitly included in your query to enable this behavior.

The maximum number of results returned for a {{site.data.keyword.discoverynewsfull}} query is `50`. Use additional queries and the `offset` parameter to return more than `50` results.

This version of {{site.data.keyword.discoverynewsfull}} debuted on **31 July 2017**. {{site.data.keyword.discoverynewsfull}} Original was retired from service **15 January 2018**.
{: note}
