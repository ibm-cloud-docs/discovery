---

copyright:
  years: 2015, 2022
lastupdated: "2022-06-01"

subcollection: discovery

---

{{site.data.keyword.attribute-definition-list}}

# Upgrading your plan
{: #upgrading-your-plan}

{{site.data.keyword.discoveryfull}} offers three plans that provide different levels of resources and capabilities to suit your needs.
{: shortdesc}

See [{{site.data.keyword.discoveryshort}} pricing plans](/docs/discovery?topic=discovery-discovery-pricing-plans) and [{{site.data.keyword.discoveryshort}} catalog](https://cloud.ibm.com/catalog/services/discovery){: external} for details.

You cannot directly upgrade your plan from `Lite` to `XS` because `XS` plans are not suitable for production usage. If you have the `Lite` plan but want the `XS` plan, you must create a new instance by using the `XS` size and then manually recreate your collections. In addition, you cannot directly downgrade from `S` to `XS`. If you have the `S` plan but want the `XS` plan, follow the same steps in the case of moving to an `XS` plan from a `Lite` plan.

You cannot upgrade from a Lite (v1) plan to a Plus (v2) plan. And you cannot upgrade from an Advanced (v1) plan to a Premium (v2) plan. To start using v2, create a new Plus or Premium plan. For more information about Premium plan instances that were created on or after 16 July 2020 or about Plus (including Plus Trial) plan instances, see [these docs](/docs/discovery-data?topic=discovery-data-upgrade){: external}.
{: important}

## Upgrading your service
{: #service}

To resize your plan from Lite to Advanced:

1. From the [resource list](https://cloud.ibm.com/resources/){: external}, click on your {{site.data.keyword.discoveryshort}} instance to go to the {{site.data.keyword.discoveryshort}} dashboard page.
1. From the **Manage** page of {{site.data.keyword.discoveryshort}}, click **Upgrade** to choose the Advanced plan. Follow the steps on the **Plan** page to complete your upgrade.
1. Return to the **Manage** page and click **Launch Watson Discovery** to open the {{site.data.keyword.discoveryshort}} tooling.
   - If you never created an environment for your Lite plan before the upgrade to Advanced, click the ![Cog](images/icon_settings.png) icon, and choose **Create environment**. Choose the options for the Advanced plan that fit your needs.  (`X-Small`, `Small`, `Medium-Small`, `Medium`, `Medium-Large`, `Large`, `X-Large`, `XX-Large`).
   - If you created an environment for your Lite plan before the upgrade to Advanced, your new Advanced plan environment is set to `Small` by default.

## Switching from one Advanced tier to another
{: #switchadvanced} 

If you already have an Advanced plan, and would like to upgrade it to a larger plan size, you can do so using the [API](/apidocs/discovery#updateenvironment){: external}. 

For detailed information on Advanced plan storage limits and pricing, see [Advanced pricing plans](/docs/discovery?topic=discovery-discovery-pricing-plans#advanced).

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

- Querying and indexing can proceed during upgrading. The time required for upgrading depends on a number of factors. You can poll your environment, using the API, while the upgrade completes.
- Moving from one level of Advanced to another does not require the creation of new instances.
- After the upgrade is complete, you are billed at the new plan rate.
- If you later find that you need a smaller plan size, set up the appropriate plan size, migrate your data, and cancel the larger plan.

## Upgrading to a Premium plan
{: #premium}

If you are interested in a Premium plan, contact [Sales](https://ibm.biz/contact-wdc-premium){: external}.  
