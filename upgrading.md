---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-03-07"

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

# Upgrading your plan
{: #upgrading-your-plan}

The {{site.data.keyword.discoveryfull}} service offers three plans that provide different levels of resources and capabilities to suit your needs.
{: shortdesc}

See [{{site.data.keyword.discoveryshort}} pricing plans](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans) and [{{site.data.keyword.discoveryshort}} catalog ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/catalog/services/discovery){: new_window} for details.

## Upgrading your service
{: #service}

To resize your plan from Lite to Advanced:

1. Open the [{{site.data.keyword.Bluemix_notm}} dashboard](https://{DomainName}/dashboard). 
1. Click on your {{site.data.keyword.discoveryshort}} service instance to open the {{site.data.keyword.discoveryshort}} service dashboard.
1. From the **Manage** page of your {{site.data.keyword.discoveryshort}} service, click **Upgrade** to choose the Advanced plan. This will open the **Plan** page. Follow the steps to complete your upgrade. 
1. Return to the **Manage** page and click **Launch Tool** to open the {{site.data.keyword.discoveryshort}} tooling.
   - If you had never created an environment for your Lite plan before the upgrade to Advanced, click the ![Cog](images/icon_settings.png) icon and choose **Create environment**. A screen will display the options for your Advanced plan. Choose the one that fits your needs.  (`X-Small`, `Small`, `Medium-Small`, `Medium`, `Medium-Large`, `Large`, `X-Large`, `XX-Large`).
   - If you had created an environment for your Lite plan before the upgrade to Advanced, your new Advanced plan environment will be `Small` by default. 

## Switching from one Advanced tier to another
{: #switchadvanced} 

If you already have an Advanced plan, and would like to upgrade it to a larger plan size, you can do so using the [API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#update-an-environment){: new_window}. 

For detailed information on Advanced plan storage limits and pricing, see [Advanced pricing plans](/docs/services/discovery?topic=discovery-discovery-pricing-plans#advanced).

Available Advanced plan sizes are: 

Plan size | Label  
--------- | ------ 
X-Small | XS 
Small | S 
Medium-Small | MS 
Medium | M 
Medium-Large | ML 
Large | L
X-Large | XL 
XX-Large | XXL 

- Querying and indexing can proceed during upgrading. The time required for upgrading depends on a number of factors. You can poll your environment using the API while the upgrade completes.
- Moving from one level of Advanced to another does not require the creation of new instances. 
- Once the upgrade is complete, you will be billed at the new plan rate.
- If you later find that you need a smaller plan size, you should set up the appropriate plan size, migrate your data, then cancel the larger plan. 

## Upgrading to a Premium plan
{: #premium}

If you are interested in a Premium plan, contact [Sales](https://ibm.biz/contact-wdc-premium).  
