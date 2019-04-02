---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-03-29"

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

# Information security
{: #information-security}

<!-- Learn more topic WDS -->
IBM is committed to providing our clients and partners with innovative data privacy, security and governance solutions.
{: shortdesc}

**Notice:**
Clients are responsible for ensuring their own compliance with various laws and regulations, including the European Union General Data Protection Regulation. Clients are solely responsible for obtaining advice of competent legal counsel as to the identification and interpretation of any relevant laws and regulations that may affect the clients’ business and any actions the clients may need to take to comply with such laws and regulations.

The products, services, and other capabilities described herein are not suitable for all client situations and may have restricted availability. IBM does not provide legal, accounting or auditing advice or represent or warrant that its services or products will ensure that clients are in compliance with any law or regulation.

If you need to request GDPR support for {{site.data.keyword.cloud}} {{site.data.keyword.watson}} resources that are created

-   In the European Union (EU), see [Requesting support for IBM Cloud Watson resources created in the European Union ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/docs/services/watson?topic=watson-gdpr-sar#request-EU){: new_window}.
-   Outside of the EU, see [Requesting support for resources outside the European Union ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/docs/services/watson?topic=watson-gdpr-sar#request-non-EU){: new_window}.

## European Union General Data Protection Regulation (GDPR)
{: #gdpr}

IBM is committed to providing our clients and partners with innovative data privacy, security and governance solutions to assist them on their journey to GDPR compliance.

Learn more about IBM's own GDPR readiness journey and our GDPR capabilities and offerings to support your compliance journey [here ![External link icon](../../icons/launch-glyph.svg "External link icon")](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/gdpr){: new_window}.

## Labeling and deleting data in {{site.data.keyword.discoveryshort}}
{: #gdpr-discovery}

{{site.data.keyword.discoveryshort}} includes an API to label data per call.

With this API you can:

- Label your data with a customer ID.
- Delete all data for a specific customer ID, including related notices.

Data is labeled by adding a `customer_id` of your choice (see restrictions in [How to label data](/docs/services/discovery?topic=discovery-information-security#labeling)) to the optional `X-Watson-Metadata` header. {{site.data.keyword.discoveryshort}} can then delete it by `customer_id`.

On any REST call, an optional header `X-Watson-Metadata` can be sent with semicolon separated `field=value` pairs, where currently only `customer_id` is persisted. By adding that `customer_id` in `X-Watson-Metadata` header, the request indicates that it contains data that belongs to this `customer_id`.

`customer_id`s are unique within a single {{site.data.keyword.discoveryshort}} instance. They are NOT unique per environment or collection. They should not include personal data.

**Note:** Experimental and beta features are not intended for use with a production environment and therefore are not guaranteed to function as expected when labeling and deleting data. Experimental and beta features should not be used when implementing a solution that requires the labeling and deletion of data.

## Methods that support labeling data
{: #pi_methods}

The following stored information can be deleted using a `customer_id` if the `customer_id` was specified when the information was originally added using the associated method:

- queries (`/v1/environments/{environment_id}/collections/{collection_id}/query`) Only when used with the `passages` or `natural_language_query` parameters
- events (`/v1/events`)
- documents (`/v1/environments/{environment_id}/collections/{collection_id}/documents`)
- notices (`/v1/environments/{environment_id}/collections/{collection_id}/notices`) Only ingestion `notices` are labeled.
- Knowledge Graph entities (`/v1/environments/{environment_id}/collections/{collection_id}/query_entities`)
- Knowledge Graph relations (`/v1/environments/{environment_id}/collections/{collection_id}/query_relations`)
- training data (`/v1/environments/{environment_id}/collections/{collection_id}/training_data`)

The following stored information is not explicitly labeled and cannot be deleted by specifying the `customer_id`. Personal Data is not supported in these fields.

Any string fields (including but not limited to `name` and `description`) of the following stored items:
- configurations
- collections
- environments

## Labeling data
{: #labeling}

When ingesting documents, include the `X-Watson-Metadata` header using the `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` or `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/ID` operations. The `customer_id` field is added to the `extracted_metadata` of the documents. Your application should be configured to provide a `customer_id` in the `X-Watson-Metadata` header when performing any operation.

Optionally, you can include the `customer_id` field with the `metadata` multi-part form part instead of using the `X-Watson-Metadata` header.

**Note:** If your documents have already been ingested, you will need to reingest them to add the `X-Watson-Metadata` header and `customer_id`.

**Note:** If you specify a `customer_id` in the `metadata` multi-part form part AND the `X-Watson-Metadata` header for the same document, then the `customer_id` in the `X-Watson-Metadata` header will be used.

Restrictions:

- The value of the `X-Watson-Metadata` header cannot exceed 4 kilobytes of text.
- The `X-Watson-Metadata` header must contain a semicolon separated list of `field=value` pairs. The `field` and `value` must not contain semicolons (`;`) or equals signs (`=`).
- `customer_id`s are unique within each {{site.data.keyword.discoveryshort}} instance. They are NOT unique per environment or collection.
- A `customer_id` cannot be more than 256 characters in length.
- If a `customer_id` contains only whitespace or is completely empty, it will be treated as though the `customer_id` wasn't provided at all and no error messages will be returned.

### Labeling data with the Discovery tooling
{: #labelingtooling}

Data can be labeled with the `customer_id` field when using the {{site.data.keyword.discoveryshort}} tooling. Click the ![Environment details](images/env_icon.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> and enter the `customer_id` in the **GDPR Data Label** field. Once this field is set all data uploaded using this browser session will be labeled with the specified `customer_id`, this field must be manually changed if the associated customer ID changes.

Adding a `customer_id` with the **GDPR Data Label** field will label the documents, notices, Knowledge Graph entities, Knowledge Graph relations, and training data within that URL domain from that point forward, including each instance under that domain. Any actions (including document uploads) that occurred in the {{site.data.keyword.discoveryshort}} tooling before adding the **GDPR Data Label** field will not be labeled.

**Note:** If you switch domains, browsers, empty the browser cache, or start an incognito session after you specify your `customer_id` using the **GDPR Data Label** field of the {{site.data.keyword.discoveryshort}} tooling, the `customer_id` will not be retained and your data will not be labeled. If you must switch domains or browsers, re-enter the `customer_id` in the **GDPR Data Label** field.

### Labeling documents using the Data Crawler
{: #labelingdc}

If any documents have already been crawled with the Data Crawler, you will need to re-crawl them to add the `X-Watson-Metadata` header and `customer_id`.

1. Update your {{site.data.keyword.discoveryshort}} Data Crawler output adapter configuration to include the `customer_id`. See [Configuring the output adapter](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#output-adapter).
1. Schedule a crawl. The documents are submitted to {{site.data.keyword.discoveryshort}} using the `X-Watson-Metadata` header and the documents will be labeled with the configured `customer_id`.

## Deleting labeled data
{: #deletingdata}

Data must be labeled with a `customer_id` in order to delete it later.

1. Use the `DELETE /v1/user_data` operation and provide the `customer_id` of the data you wish to delete. `DELETE /v1/user_data` deletes all data associated with a particular `customer_id` within that service instance, as specified in [Methods that support labeling data](/docs/services/discovery?topic=discovery-information-security#pi_methods). Also see the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/discovery#delete-labeled-data){: new_window}

Deletions are performed asynchronously. You cannot track the progress of deletions.

To ensure all labeled content is correctly removed, `user_delete` should be run after the `processing` and `pending` counts for all collections in your environment return `0`.

If a non-existent `customer_id` is provided, nothing will be deleted, but a `200 - OK` response will be returned.

Environments and Collections are not labeled with a `customer_id`, even if a `X-Watson-Metadata` header is included in the request to create the environment or collection. Only the individual documents within a collection within an environment are labeled. Therefore when data is deleted, individual environments and collections are NOT deleted.

You cannot delete labeled data using the {{site.data.keyword.discoveryshort}} tooling.