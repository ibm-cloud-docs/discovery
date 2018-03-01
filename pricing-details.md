---

copyright:
  years: 2015, 2018
lastupdated: "2018-03-01"

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

# Discovery pricing plans

The {{site.data.keyword.discoveryfull}} service offers four plans that provide different levels of resources and capabilities to suit your needs.
{: shortdesc}

**Private data use cases** have the following limits and prices:

| Lite                     |  Standard         | Advanced          | Premium          |
|--------------------------|-------------------|-------------------|-------------------|
| Up to 2,000 concurrent documents per month\*   |Up to 100,000 concurrent documents per month\*<br/> $10 per 1,000 concurrent documents per month ($0.0139USD/1000Doc/Hr)\*\*\*<br/> 2,000 documents per month free\*\*\*\*  | **Reserved environment**</br>$1,000/month base rate<br/> Up to 1,000,000 documents per month\*<br/> $5 per 1,000 concurrent documents per month ($0.00694 USD/1000Doc/Hr)\*\*\*<br/> 100,000 documents per month included\*\*\*\*</br> Additional plans up to 100M documents/6.4 TB are available.</br> For larger environments, contact [Sales ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/marketing/iwm/dre/signup?source=MAIL-watson){: new_window}.| **Premium Plans** offer developers and organizations a single tenant instance of one or more Watson services for better isolation and security. These plans offer compute-level isolation on the existing shared platform, as well as end-to-end encrypted data while in transit and at rest. For more information, or to purchase a premium plan, contact [Sales ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://ibm.biz/contact-wdc-premium){: new_window} |
| 200MB\*\*                  |10GB\*\*  | 80GB\*\* |-|
| Up to 2 Collections      |Up to 4 Collections | Up to 100 Collections|-|
| Up to 1 Custom Model     |Up to 1 Custom Model | 1 Custom Model included<br/> Additional Custom Models $800 per model per month |-|
| 500 Element Classification pages per month      |500 Element Classification pages per month | 500 Element Classification pages per month<br/> Additional Element Classification pages $0.40 USD/Page |-|
| 500 query expansions with 1,000 total terms     |500 query expansions with 1,000 total terms | 5,000 query expansions with 25,000 total terms  |-|

**Note:** In all plans, the first 1,000 {{site.data.keyword.discoverynewsshort}} queries per month are free. {{site.data.keyword.discoverynewsshort}} queries are charged at $0.10 per query after the first 1,000. Lite plans are limited to a maximum of 1,000 {{site.data.keyword.discoverynewsshort}} queries per month.

**Note:** Lite plan instances are deleted after 30 days of inactivity. One free environment is allotted per organization on Lite plans.

 \* Document limit assumes an average document size of 100KB on disk. This is the size of a document in a collection after it has gone through conversion and enrichment, so the size may change significantly from the original input. You can view the number of documents stored and the total amount of storage used by either using the `environments` or `collections` API, or by using the tooling.

 \*\* If your documents are on average larger than 100KB on disk, you will hit the storage limit of a plan before the max document limit.

 \*\*\* Price is based on the number of hours that a batch of 1,000 documents is stored in the service (referred to as a Thousand Document-Hour). For the pricing calculator, this is the number that should be entered (`number of documents * number of hours those documents are stored in a month / 1000`).

 \*\*\*\* Free amounts are based on the equivalent of documents stored for a month. For example, in the Standard plan, the free amount is equivalent to 2,000 documents * 720 hours / 1000 document batch  = 1440 Thousand Document-Hours.

**Example:** A user on the Standard plan stores 4,000 documents for the entire month. They would be charged as follows:

- `4000 documents * 720 hours (in a month) / 1000 = 2,880` Thousand Document-hours consumed

- `2,880 - 1,440 (free document hours) = 1,440` Billable Thousand Document Hours

- `1,440 * $0.0139` (price per Thousand Document Hour) = `$20.00` for the month

**Note:** When calculating the billed amount each hour, the total number of documents stored is rounded up to the nearest 1,000 as part of the calculation. For example, if you have 4,678 documents stored for 1 hour it would be rounded up to 5,000 and result in 5 Thousand document-hours being billed to the account.

For information about calculating costs, see the [{{site.data.keyword.Bluemix_notm}} Pricing Calculator ![External link icon](../../icons/launch-glyph.svg "External link icon")](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/pricing/platform/watson){: new_window}.

**Note:** There is no additional charge for enrichments.

For information about {{site.data.keyword.Bluemix_notm}} security, see the [{{site.data.keyword.Bluemix_notm}} Service Description ![External link icon](../../icons/launch-glyph.svg "External link icon")](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=IBM+Bluemix+Service+Description){: new_window}.

## Converting from previous pricing plans

Customers who subcribed to a plan prior to **1, August 2017** were migrated to one of the new plans.

- Customers that were previously on the 30-day free trial plan have been migrated to the **Lite** plan.
  As a result of this transition, existing users may have met or exceeded the lite plan limit on documents _(2000)_, storage _(200Mb)_, or number of collections _(2)_. If you have exceeded the limit of the **Lite** plan, you will not be able to add any additional content into the service but you can still query collections. You can view the current status of all these limits by using the {{site.data.keyword.discoveryshort}} tooling or API. To be able to resume adding content to the {{site.data.keyword.discoveryshort}} instance, you must do one of the following:
  - remove collections and/or documents so that limits of the **Lite** plan are not exceeded.
    Documents can be deleted either individually through the API using the [delete-doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-doc){: new_window} method, or whole collections can be deleted using the Tooling or API using the [delete-collection ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-collection){: new_window} method
  - upgrade your plan to a level that meets your storage needs.
- Customers with size **`1`** **`2`** or **`3`** environments have been automatically migrated to the **Advanced** plan.
  If you have been moved to the Advanced tier and have fewer than 100,000 documents and 4 collections, you can to move to the Standard tier to reduce costs. This requires creating a new Discovery instance in the Standard plan and reingesting data to the new instance. Ingestion can be done through the tooling, APIs, or Data Crawler.

See the [{{site.data.keyword.discoveryshort}} catalog ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window} for additional pricing information.
