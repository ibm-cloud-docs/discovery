---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-01-29"

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

# Discovery pricing plans

The {{site.data.keyword.discoveryfull}} service offers three plans -- **Lite**, **Advanced**, and **Premium** -- that provide different levels of resources and capabilities to suit your needs.
{: shortdesc}

**Private data use cases** have the following features, limits, and prices:

## Lite
{: #lite}

Size | Doc Storage Limit | Number of Docs\* | Price 
------ | ------ | ------ | ------  
N/A | 50 MB | 1,000 per month | Free 

The Lite plan is a starter plan and should not be used for production. When you upgrade to a paid plan, you can keep all ingested documents.  Lite plan instances are deleted after 30 days of inactivity. 

Attributes:
- 1 environment
- Up to 2 collections
- Free NLU enrichments\*\*

Additional options:<br> [Custom Models](/docs/services/discovery/integrate-wks.html#integrating-your-custom-model):<br>
One Watson Knowledge Studio model included. Additional models: Not available<br>[Element Classification](/docs/services/discovery/element-classification.html)\*\*\*:
500 pages included per month. Additional pages: Not available <br>[News Queries](/docs/services/discovery/watson-discovery-news.html): 
200 News queries included per month. Additional queries:  Not available<br>[Query Expansions](/docs/services/discovery/using.html#query-expansion):
500 query expansions with 1,000 total terms. Additional expansions: Not available

For information about upgrading from Lite to Advanced, see [Upgrading your service](/docs/services/discovery/upgrading.html#service)

For query performance information, see [Query performance](/docs/services/discovery/qp.html#qp). Queries are limited based on plan. Estimated Average Query rates per **Lite** plan: 1 QPS for reranked queries with two top-level text fields.

## Advanced
{: #advanced}

When choosing an Advanced Plan size, note that resources are required for both document storage and querying. Therefore, you may require a larger environment if you are close to the maximum document limit for a plan size and also have the following requirements: 

-  Higher query performance requirements (for example, using relevancy training)
-  You anticipate a large number of concurrent users
-  Complex query needs 

For additional details on factors that influence query performance, see [Query performance](/docs/services/discovery/qp.html). Queries are limited based on plan. Estimated Average Query rates per **Advanced** (S, MS) plans: 10 QPS for reranked queries with two top-level text fields.

Size | Doc Storage Limit | Number of Docs\* | Price 
------ | ------ | ------ | ------ 
X-Small\*\*\*\*\* | 40 GB | Up to 50,000 docs per month | Starting at $500 per month  
Small | 160 GB | Up to 1M docs per month | Starting at $1,500 per month  
Medium-Small | 320 GB | Up to 2M docs per month | Starting at $3,000 per month 
Medium| 640 GB | Up to 4M docs per month | Starting at $5,000 per month 
Medium-Large | 1.2 TB | Up to 8M docs per month | Starting at $10,000 per month 
Large| 2.4 TB | Up to 16M docs per month | Starting at $15,000 per month 
X-Large| 4 TB | Up to 32M docs per month | Starting at $20,000 per month 
XX-Large | 5.5 TB | Up to 64M docs per month | Starting at $35,000 per month 
XXX-Large | 12 TB | Up to 100M docs per month | Starting at $45,000 per month 

X-Small is the smallest environment available, and is recommended for development and testing only.\*\*\*\*\*

Moving from one level of Advanced to another does not require the creation of new instances. New instances will be required if switching from an Advanced to a Premium plan. For information about upgrading from one tier of Advanced to another, see [Moving from one Advanced tier to another](/docs/services/discovery/upgrading.html#advanced).

\*\*\*\*\*Attributes of X-Small plans: 
- 1 environment
- Up to 4 collections
- Free NLU enrichments\*\*

Attributes of all other Advanced plans:
- 1 environment
- Up to 100 collections
- Free NLU enrichments\*\*

Additional options:<br> [Custom Models](/docs/services/discovery/integrate-wks.html#integrating-your-custom-model):<br>
One Watson Knowledge Studio model included. Additional models: $800 each<br>[Element Classification](/docs/services/discovery/element-classification.html)\*\*\*:
500 pages included per month. Additional pages: $0.40 each<br>[News Queries](/docs/services/discovery/watson-discovery-news.html): 
200 News queries included per month  
10,000 additional queries (per month): $0.10 per query<br>
10,001 - 100,000 additional queries (per month): $0.05 per query<br>
Over 100,000 queries (per month): $0.03 per query<br>
[Query Expansions](/docs/services/discovery/using.html#query-expansion):
5,000 query expansions with 25,000 total terms

## Premium
   
Premium plans offer developers and organizations a single tenant instance of one or more Watson services for better isolation and security. These plans offer compute-level isolation on the existing shared platform, as well as end-to-end encrypted data while in transit and at rest. 

For more information, or to purchase a Premium plan, contact [Sales](https://ibm.biz/contact-wdc-premium). 
<br>
<br> 

**Note:** The version date of the API has been updated to `2018-08-01`. To take advantage of the new environment sizing options (`LT`, `XS`, `S`, `MS`, `M`, `ML`, `L`, `XL`, `XXL`, `XXXL`), you must use this version date when creating environments with the API. The environment sizes now have the type of `string` (previously the type was `integer`.)

\* The document limit assumes an average document size of 100KB on disk. Document size is calculated after it has gone through conversion and enrichment, so document size may change significantly from the original input. You can view the number of documents stored and the total amount of storage used by either using the [Environments](https://{DomainName}/apidocs/discovery#get-environment-info) or [Collections](https://{DomainName}/apidocs/discovery#get-collection-details) API, or by using the tooling. If your documents are on average larger than 100KB on disk, you will hit the storage limit of a plan before the maximum document limit. If you perform [document segmentation](https://cloud.ibm.com/docs/services/discovery/building.html#doc-segmentation) on your documents, each segment counts as a separate document.

\*\* The [Natural Language Understanding (NLU) enrichments](https://cloud.ibm.com/docs/services/discovery/building.html#adding-enrichments) are: Entity Extraction, Sentiment Analysis, Category Classification, Concept Tagging, Keyword Extraction, Relation Extraction, Emotion Analysis, Element Classification, and Semantic Role Extraction.  Only the first 50,000 characters of each document are enriched. 

\*\*\* Element Classification is an enrichment that parses through governing documents to convert, identify, and classify elements of importance. It uses Natural Language Processing to extract the following elements from PDF documents: party (who it refers to), nature (type of element), and category (specific class).

For query performance information, see [Query performance](/docs/services/discovery/qp.html#qp). Queries are limited based on plan. Estimated Average Query rates per plan:

- **Lite** and **Standard** plans: 1 QPS for reranked queries with two top-level text fields.
- **Advanced** (S, MS) plans: 10 QPS for reranked queries with two top-level text fields.

For information about calculating costs, see the [IBM Cloud Pricing Calculator ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/pricing/platform/watson){: new_window}.

For information about IBM Cloud security, see [Cloud Services data security and privacy ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/software/sla/sladb.nsf/sla/csdsp?OpenDocument){: new_window}.

For additional pricing information, see the [{{site.data.keyword.discoveryshort}} catalog ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/catalog/services/discovery){: new_window}.

## Notes for Customers with Existing Plans

- Beginning **August 1, 2018**, your billing and usage will be based on this pricing plan.
- The Lite plan has been reduced from 2,000 documents/400 {{site.data.keyword.discoverynewsshort}} queries per month to 1,000 documents/200 {{site.data.keyword.discoverynewsshort}} queries per month.  If you have already exceeded the new Lite plan limits, you can't add any more documents. However, you can continue using it or upgrade to an Advanced or Premium plan.
- The Standard plan has been retired and will no longer be available to new users. If you are currently on an existing Standard plan, you can continue using it or upgrade to an Advanced or Premium plan.
- The Advanced and Premium plans are now based on document tiers, they are no longer based on document hours. Your monthly bill will not fluctuate based on the number of documents unless you switch between tiers.
- Premium customers, contact [Sales](https://ibm.biz/contact-wdc-premium) for details on billing changes.	