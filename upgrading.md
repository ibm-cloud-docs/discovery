---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-25"

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

# Upgrading your plan

The {{site.data.keyword.discoveryfull}} service offers three plans that provide different levels of resources and capabilities to suit your needs.
{: shortdesc}

See [{{site.data.keyword.discoveryshort}} Pricing Plans](/docs/services/discovery/pricing-details.html) and [{{site.data.keyword.discoveryshort}} catalog ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window} for details.

## Upgrading your service
{: #service} 

To resize your plan from Lite to Advanced:

1. Open the [{{site.data.keyword.Bluemix_notm}} dashboard](https://console.{DomainName}/dashboard). 
1. Click on your {{site.data.keyword.discoveryshort}} service instance to open the {{site.data.keyword.discoveryshort}} service dashboard.
1. From the **Manage** page of your {{site.data.keyword.discoveryshort}} service, click **Upgrade** to choose the Advanced plan. This will open the **Plan** page. Follow the steps to complete your upgrade. 
1. Return to the **Manage** page and click **Launch Tool** to open the {{site.data.keyword.discoveryshort}} tooling.
   - If you had never created an environment for your Lite plan before the upgrade to Advanced, click the ![Cog](images/icon_settings.png) icon and choose **Create environment**. A screen will display the options for your Advanced plan. Choose the one that fits your needs.  (`X-Small`, `Small`, `Medium-Small`, `Medium`, `Medium-Large`, `Large`, `X-Large`, `XX-Large`).
   - If you had created an environment for your Lite plan before the upgrade to Advanced, your new Advanced plan environment will be `Small` by default. 

## Switching from one Advanced tier to another
{: #advanced} 

If you already have an Advanced plan, and would like to upgrade it to a larger plan size, you can do so using the [API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#update-environment){: new_window}. 

For detailed information on Advanced plan storage limits and pricing, see [Advanced pricing plans](/docs/services/discovery/pricing-details.html#advanced).

You can upgrade your Advanced plan size, but you can't downsize to a smaller size. Available Advanced plan sizes are: 

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

## Upgrading to a Premium plan
{: #premium}

If you are interested in a Premium plan, contact [Sales](https://ibm.biz/contact-wdc-premium).  
