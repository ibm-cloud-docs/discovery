---

copyright:
  years: 2015, 2022
lastupdated: "2022-08-16"

subcollection: discovery

---

{{site.data.keyword.attribute-definition-list}}

# Discovery pricing plans
{: #discovery-pricing-plans}

<!-- Learn more topic WDS -->
{{site.data.keyword.discoveryfull}} offers three plans -- **Lite**, **Advanced**, and **Premium** -- that provide different levels of resources and capabilities to suit your needs.
{: shortdesc}

For more information about Premium plans that were created after 16 July 2020 or about Plus plans (including Plus Trial), see [these docs](/docs/discovery-data?topic=discovery-data-pricing-plans){: external}.
{: note}

**Private data use cases** have the following features, limits, and prices:

## Lite
{: #lite}

Size | Number of Docs\* | Price
------ | ------ | ------
N/A | 1,000 docs total | Free

The Lite plan is a starter plan, so do not use it in your production environment. When you upgrade to a paid plan, you can keep all ingested documents.  Lite plan instances are deleted after 30 days of inactivity.

Attributes:
- 1 environment
- Up to 2 collections
- Free NLU enrichments\*\*

Additional options:<br> [Custom Models](/docs/discovery?topic=discovery-integrating-with-wks):<br>
One {{site.data.keyword.knowledgestudiofull}} model included. Additional models: Not available<br>[Element Classification](/docs/discovery?topic=discovery-element-classification)\*\*\*:
500 pages included per month. Additional pages: Not available <br>[News Queries](/docs/discovery?topic=discovery-watson-discovery-news):
200 News queries included per month. Additional queries:  Not available<br>[Query Expansions](/docs/discovery?topic=discovery-query-concepts#query-expansion):
500 query expansions with 1,000 total terms. Additional expansions: Not available<br>
[Document splitting](/docs/discovery?topic=discovery-configservice#doc-segmentation): 250 segments per plan. Additional segments: Not available

For information about upgrading from Lite to Advanced, see [Upgrading your service](/docs/discovery?topic=discovery-upgrading-your-plan#service)

For query performance information, see [Query performance](/docs/discovery?topic=discovery-qp). Queries are limited based on plan. Estimated Average Query rates per **Lite** plan: 1 QPS for reranked queries with two top-level text fields.

The Element Classification enrichment is deprecated and will no longer be available, effective **10 July 2020**.
{: important}

## Advanced
{: #advanced}

When choosing an Advanced Plan size, note that resources are required for both document storage and querying. Therefore, you might require a larger environment if you are close to the maximum document limit for a plan size and also have the following requirements:

-  Higher query performance requirements (for example, using relevancy training)
-  You anticipate a large number of concurrent users
-  Complex query needs

For additional details on factors that influence query performance, see [Query performance](/docs/discovery?topic=discovery-qp). Queries are limited based on plan. Estimated Average Query rates per **Advanced** (S, MS) plans: 10 QPS for reranked queries with two top-level text fields.

Size | Number of Docs\* | Price
------ | ------ | ------
X-Small\*\*\*\* | Up to 50,000 docs total | Starting at $500 per month
Small | Up to 1M docs total | Starting at $1,500 per month
Medium-Small | Up to 2M docs total | Starting at $3,000 per month
Medium| Up to 4M docs total | Starting at $5,000 per month
Medium-Large | Up to 8M docs total | Starting at $10,000 per month
Large| Up to 16M docs total | Starting at $15,000 per month
X-Large| Up to 32M docs total | Starting at $20,000 per month
XX-Large | Up to 64M docs total | Starting at $35,000 per month
XXX-Large | Up to 100M docs total | Starting at $45,000 per month

X-Small is the smallest environment available, and is recommended for development and testing only.\*\*\*\*

Moving from one level of Advanced to another does not require the creation of new instances. New instances are required if switching from an Advanced to a Premium plan. For information about upgrading from one tier of Advanced to another, see [Moving from one Advanced tier to another](/docs/discovery?topic=discovery-upgrading-your-plan).

\*\*\*\*Attributes of X-Small plans:
- 1 environment
- Up to 4 collections
- Free NLU enrichments\*\*

Attributes of all other Advanced plans:
- 1 environment
- Up to 100 collections
- Free NLU enrichments\*\*

Additional options:<br> [Custom Models](/docs/discovery?topic=discovery-integrating-with-wks):<br>
One {{site.data.keyword.knowledgestudioshort}} model included. Additional models: $800 each<br>[Element Classification](/docs/discovery?topic=discovery-element-classification)\*\*\*:
500 pages included per month. Additional pages: $0.40 each<br>[News Queries](/docs/discovery?topic=discovery-watson-discovery-news):
200 News queries included per month
10,000 additional queries (per month): $0.10 per query<br>
10,001 - 100,000 additional queries (per month): $0.05 per query<br>
Over 100,000 queries (per month): $0.03 per query<br>
[Query Expansions](/docs/discovery?topic=discovery-query-concepts#query-expansion):
5,000 query expansions with 25,000 total terms<br>
[Document splitting](/docs/discovery?topic=discovery-configservice#doc-segmentation): 1,000 segments per plan. Additional segments: Not available

The Element Classification enrichment is deprecated and will no longer be available, effective **10 July 2020**.
{: important}

`-----`
<br>
\* The document limit assumes an average document size of 100KB on disk. Document size is calculated after it goes through conversion and enrichment, so document size might change significantly from the original input. You can view the number of documents stored and the total amount of storage used by either using the [Environments](/apidocs/discovery#get-environment-info) or [Collections](/apidocs/discovery#get-collection-details) API, or by using the tooling. If your documents are, on average, larger than 100KB on disk, you will hit the storage limit of a plan before the maximum document limit. If you perform [document segmentation](/docs/discovery?topic=discovery-configservice#doc-segmentation) on your documents, each segment counts as a separate document.

\*\* The [{{site.data.keyword.nlufull}} enrichments](/docs/discovery?topic=discovery-configservice#adding-enrichments) are: Entity Extraction, Sentiment Analysis, Category Classification, Concept Tagging, Keyword Extraction, Relation Extraction, Emotion Analysis, Element Classification, and Semantic Role Extraction.  Only the first 50,000 characters of each document are enriched.

\*\*\* Element Classification is an enrichment that parses through governing documents to convert, identify, and classify elements of importance. It uses Natural Language Processing to extract the following elements from PDF documents: party (who it refers to), nature (type of element), and category (specific class).

To take advantage of the new string environment sizing values (`LT`, `XS`, `S`, `MS`, `M`, `ML`, `L`, `XL`, `XXL`, `XXXL`), use the version date of `2018-08-01` or later in your API request when you create an environment. Before version `2018-08-01`, the value was an `integer`.
{: note}

## Premium
{: #premiumplan}

Premium plans offer developers and organizations a single tenant instance of one or more Watson services for better isolation and security. These plans offer compute-level isolation on the existing shared platform, as well as end-to-end encrypted data while in transit and at rest.

For more information, or to purchase a Premium plan, contact [Sales](https://ibm.biz/contact-wdc-premium){: external}.

## Additional information
{: #pricingadd}

For information about calculating costs, see the [IBM Cloud Pricing Calculator](https://cloud.ibm.com/estimator/review){: external}.

For additional pricing information, see the [{{site.data.keyword.discoveryshort}} catalog](https://cloud.ibm.com/catalog/services/discovery){: external}.

## Notes for Customers with Existing Plans
{: #pricingnotes}

- Beginning **1 August 2018**, your billing and usage is based on this pricing plan.
- The Lite plan is now reduced from 2,000 documents/400 {{site.data.keyword.discoverynewsshort}} queries per month to 1,000 documents/200 {{site.data.keyword.discoverynewsshort}} queries per month.  If you already exceeded the new Lite plan limits, you cannot add any more documents. However, you can continue using it or upgrade to an Advanced or Premium plan.
- The Standard plan is retired and is no longer available to new users. If you are currently on an existing Standard plan, you can continue using it or upgrade to an Advanced or Premium plan.
- The Advanced and Premium plans are now based on document tiers. They are no longer based on document hours. Your monthly bill will not fluctuate, based on the number of documents, unless you switch between tiers.
- Premium customers, contact [Sales](https://ibm.biz/contact-wdc-premium){: external} for details on billing changes.
