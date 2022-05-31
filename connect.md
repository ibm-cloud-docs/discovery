---

copyright:
  years: 2015, 2021
lastupdated: "2022-01-26"

subcollection: discovery

---

{{site.data.keyword.attribute-definition-list}}

# Connecting to data sources
{: #sources}

<!-- Learn more topic WDS -->
You can use {{site.data.keyword.discoveryshort}} to connect to and crawl documents from remote sources.
{: shortdesc}

You can connect to a data source and pull documents on a schedule into {{site.data.keyword.discoveryshort}} by configuring a collection to associate with that source. You can configure each collection with one data source. {{site.data.keyword.discoveryshort}} pulls documents from the data source using a process called crawling. Crawling is the process of systematically browsing and retrieving documents from the specified start location. {{site.data.keyword.discoveryshort}} only crawls items that you explicitly specify. The first time that a crawler crawls a data source is a full crawl, and every time that the crawler runs after the full crawl, per the crawl schedule, is a refresh, also called a recrawl.

This documentation applies to {{site.data.keyword.discoveryshort}} service instances that you create with a Lite or an Advanced plan, or that you created with a Premium plan before 16 July 2020. For more information about features in Premium plan instances created on or after 16 July 2020, and in Plus (including Plus Trial) plan instances, see [these docs](/docs/discovery-data?topic=discovery-data-collections){: external}.
{: important}

## General source requirements
{: #gen_req}

The following general requirements apply to all data sources:

-  The individual document file size limit for Box, Salesforce, SharePoint Online, SharePoint OnPrem, {{site.data.keyword.cos_full}}, and Web Crawl is 10MB.
-  You must have the credentials, file locations, or URLs for each data source. A developer or system administrator typically provides the credentials, file locations, and URLs of the data source.
-  You must know which resources of the data source to crawl, which the source administrator can provide. If you crawl Box or Salesforce, a list of available resources is presented when you configure a source, using the {{site.data.keyword.discoveryshort}} tooling.
-  If you are using the {{site.data.keyword.discoveryshort}} tooling, you can configure a collection with a single data source.
-  Crawling a data source uses resources, namely API calls, of the data source. The number of API calls depends on the number of documents that need to be crawled. You must obtain an appropriate level of service license, for example Enterprise, for the data source. For information about the appropriate service level license that you need, contact the source system administrator.
-  {{site.data.keyword.discoveryshort}} source crawls do not delete documents that are stored in a collection, but you can manually delete them using the API. When a source is re-crawled, new documents are added, updated documents are modified to the current version, and deleted documents remain as the version last stored.
-  {{site.data.keyword.discoveryshort}} can only ingest the following file types, and it ignores all other document types:

Lite plans | Advanced plans 
------------------------------ | ------------------------------------------- 
PDF, Word, PowerPoint, Excel, JSON\*, HTML\* | PDF, Word, PowerPoint, Excel, PNG\*\*, TIFF\*\*, JPG\*\*, JSON\*, HTML\* 


\* {{site.data.keyword.discoveryfull}} supports crawling JSON and HTML documents, but you cannot edit these documents using the SDU editor. To change the configuration of HTML and JSON documents, you must use the API. For more information, see the [API reference](/apidocs/discovery/){: external}.

\*\* Individual image files, such as PNG, TIFF, and JPG, are scanned, and any text is extracted. PNG, TIFF, and JPEG images embedded in PDF, Word, PowerPoint, and Excel files are also scanned, and any text is extracted.

View the following table to see the objects that a data source can crawl and which data sources support crawling new and modified documents during a refresh:

Data source                          | Crawls new and modified documents during refresh? | Compatible objects that can be crawled
------------------------------------ | ------------------------------------------------- | --------------------------------------
Box (**Application level** access)   | No                                                | Files, folders
Box (**Enterprise level** access)    | Yes                                               | Files, folders
Salesforce                           | Yes                                               | Any default and custom objects that you have access to, accounts, contacts, cases, contracts, knowledge articles, attachments
Microsoft SharePoint Online          | Yes                                               | SiteCollections, websites, lists, list items, document libraries, custom metadata, list item attachments
Microsoft SharePoint OnPrem          | Yes                                               | SiteCollections, websites, lists, list items, document libraries, custom metadata, list item attachments
Web Crawl                            | No                                                | Websites, website subdirectories
{{site.data.keyword.cos_full_notm}}  | Yes                                               | Buckets, files
{: caption="Table 1. Data sources that support crawling new and modified documents during refresh and objects that can be crawled" caption-side="top"}


## Available data sources
{: #available sources}

You can use {{site.data.keyword.discoveryshort}} to crawl from the following data sources:

-  [Box](/docs/discovery?topic=discovery-sources#connectbox)
-  [Salesforce](/docs/discovery?topic=discovery-sources#connectsf)
-  [Microsoft SharePoint Online](/docs/discovery?topic=discovery-sources#connectsp)
-  [Microsoft SharePoint OnPrem](/docs/discovery?topic=discovery-sources#connectsp_op)
-  [Web Crawl](/docs/discovery?topic=discovery-sources#connectwebcrawl)
-  [IBM Cloud Object Storage](/docs/discovery?topic=discovery-sources#connectcos)

You can connect to a data source using the {{site.data.keyword.discoveryshort}} tooling or the API. The {{site.data.keyword.discoveryshort}} tooling provides a simplified method of connection that requires less understanding of the source systems, and the API provides a more granular and highly configurable interface, which requires a greater understanding of the source that you are connecting to. Consult the following process overview to see which sections of this document to read next:

1.  Read the [General Source Requirements](/docs/discovery?topic=discovery-sources#gen_req).
2.  Read the requirements for your data source. For the available data sources, see the list above.
3.  Read the instructions to connect to {{site.data.keyword.discoveryshort}} by using one of the following methods:
    -  [Using the tooling](/docs/discovery?topic=discovery-sources#source_tooling)
    -  [Using the API](/docs/discovery?topic=discovery-sources#source_api)

To learn about integrating {{site.data.keyword.discoveryshort}} with App Connect, see [Adding content](/docs/discovery?topic=discovery-addcontent).

If you select an on-premises data source, you must first install and configure {{site.data.keyword.SecureGatewayfull}}. For more information about installing {{site.data.keyword.SecureGatewayfull}}, see [Installing IBM Secure Gateway for on-premises data](/docs/discovery?topic=discovery-sources#gateway).


### Box
{: #connectbox}

<!-- Learn more topic WDS -->
You'll need to create a new Box custom application to connect to {{site.data.keyword.discoveryfull}}. The Box application you create requires either Enterprise level or Application level access.

-  If you are not the Box administrator for your organization, [**Application level** access](/docs/discovery?topic=discovery-sources#applevelbox) is recommended. You must have an administrator approve your application.
-  If you are the Box administrator for your organization, [**Enterprise level** access](/docs/discovery?topic=discovery-sources#entlevelbox) is recommended.

If you have **Application level** access, new and modified documents are not crawled during a refresh. This functionality is only supported if you have **Enterprise level** access. If you have **Application level** access, you must first have an administrator approve your application.
{: important}

If there is a Box update, the steps to set up Box access might change. For more information, see the [Box developer documentation](https://developer.box.com/){: external}.
{: note}

#### Setting up Application level access
{: #applevelbox}

1.   Navigate to `https://app.box.com/developers/console` (use your company's Box URL) and click **Create New App**.
1.   From the **Create a New App** screen, select **Enterprise Integration** and click **Next**.
1.   On the **Authentication Method** screen, select **OAuth 2.0 with JWT (Server Authentication)** and click **Next**.
1.   Name your app and click the **Create App** button. After you create your Box app, click **View Your App**.
1.   While viewing your app, select **Application access** as **Application**. You can use your existing managed users as you continue; you are not required to create new ones.
1.   Scroll down to the **Application Scopes** section of the page and enable the following checkboxes:
     - `Read and write all folders stored in Box`
     - `Manage Users`
1.   Scroll down to the **Advanced Features** section and enable the following toggles:
     - `Perform Actions as Users`
     - `Generate User Access Tokens` 
1.  Click the **Save Changes** button.

The next few steps require assistance from the administrator of your organization's Box account. If you are not your organization's Box Administrator, you can identify the Administrator by opening the Box developer's console and looking under **Account settings** > **Account details** > **Settings**.

1.  [Administrator step] Authorize your application client id at `https://app.box.com/master/settings/openbox` by clicking the **Authorize New App** button.
1.  [Administrator step] Type the **client ID** from `https://app.box.com/developers/console` into the **API key** field and then click the **Authorize** button.
1.  [Administrator step] Retrieve a developer token for the application. To do this, navigate to `https://app.box.com/developers/console`, scroll to the **Developer Token** section and generate your token.
1.  Now that the administrator authorized the application, navigate to `https://developer.box.com/reference#page-create-an-enterprise-user` and create an App User using the API reference page.

   Curl example to create an App User:

   ```bash
    curl https://api.box.com/2.0/users -H "Authorization: Bearer ACCESS_TOKEN" -d '{"name": "NedStark", "is_platform_access_only": true}' -X POST
   ```
   {: pre}

1.  Copy the newly generated **id** field contents and provide them to the non-administrator connecting the Box application to {{site.data.keyword.discoveryfull}}.
1.  Once the App User is created, the folders you want to crawl need to be shared with the App User, and the App User must be given `Viewer` permissions on those folders. This requires the App User login name from the above curl command response. Example:`"login":"AppUser_737729_jmUo@boxdevedition.com"`.
1.  Return to the Box developer console `https://app.box.com/developers/console` and scroll to the **Add and Manage Public Keys** section. Click the **Generate the public/private keypair** and download your keypair file. Open the file.
1.  From the keypair file, cut and paste the following fields into the {{site.data.keyword.discoveryshort}} tooling.
    -  `client_id`
    -  `enterprise_id`
    -  `client_secret` 
    -  `public_key_id` 
    -  `private_key` 
    -  `passphrase` 

#### Setting up Enterprise level access
{: #entlevelbox}

1.  Navigate to `https://app.box.com/developers/console` (use your company's Box URL) and click **Create New App**.
1.  From the **Create a New App** screen, select **Enterprise Integration** and click **Next**.
1.  On the **Authentication Method** screen, select **OAuth 2.0 with JWT (Server Authentication)** and click **Next**.
1.  Name your app and click the **Create App** button. After you create your Box app, click **View Your App**.
1.  While viewing your app, select **Application access** as **Enterprise**. You can use your existing managed users as you continue; you are not required to create new ones.
1.  Scroll down to the **Application Scopes** section of the page and enable the following checkboxes:
    - `Read and write all folders stored in Box`
    - `Manage Users`
    - `Manage Enterprise Properties`
1.  Scroll down to the **Advanced Features** section and enable the following toggles:
    - `Perform Actions as Users`
    - `Generate User Access Tokens` 
1.  Click the **Save Changes** button.

If you change your Box App settings, `Reauthorize` your App so the changes take effect.
{: tip}

The next few steps require assistance from the administrator of your organization's Box account. If you are not your organization's Box Administrator, you can identify the Administrator by opening the Box developer's console and looking under **Account settings** > **Account details** > **Settings**.

1.  [Administrator step] Authorize your application client id by navigating to **Admin console** > **Enterprise settings** > **Apps** and scrolling to `Custom applications`. Example URL:`https://app.box.com/main/settings/openbox`.
1.  [Administrator step] Type the **client ID** from `https://app.box.com/developers/console` into the **API key** field and then click the **Authorize** button.
1.  Return to the Box developer console `https://app.box.com/developers/console` and scroll to the **Add and Manage Public Keys** section. Click the **Generate the public/private keypair** and download your keypair file. Open the file.
1.  From the keypair file, cut and paste the following fields into the {{site.data.keyword.discoveryshort}} tooling.
    -  `client_id`
    -  `enterprise_id`
    -  `client_secret` 
    -  `public_key_id` 
    -  `private_key` 
    -  `passphrase` 

Other items to consider when you crawl Box:

-  Box notes are stored in JSON format, so {{site.data.keyword.discoveryshort}} ingests any Box notes in the specified folders.
-  When you use the API, you must have a list of Folders IDs and the associated Owner ID for each folder that you want to crawl. Use the {{site.data.keyword.discoveryshort}} tooling to browse and select which content to crawl.

### Salesforce
{: #connectsf}

<!-- Learn more topic WDS -->
When connecting to a Salesforce source, ensure that the instance you plan to connect to is an Enterprise plan or higher.

The following credentials are required to connect to a Salesforce source. If you do not know these credentials, consult your Salesforce administrator:
-  `url` - The `url` of the source that these credentials connect to.
-  `username` - The `username` of the source that these credentials connect to.
-  `password` - The `password` consists of the Salesforce password and a valid Salesforce security token concatenated. This value is never returned and is only used when creating or modifying credentials.

When identifying the credentials, it might be useful to consult the [Salesforce developer documentation](https://developer.salesforce.com/docs/){: external}.

Other items to note when you crawl Salesforce:

-  Knowledge Articles are only crawled if their **version** is `published` and their languages is `en-us`.
-  When you use the API, you must have a list of Salesforce objects that you want to crawl. Use the {{site.data.keyword.discoveryshort}} tooling to browse and select which content to crawl.

### SharePoint Online
{: #connectsp}

<!-- Learn more topic WDS -->
When connecting to a Microsoft SharePoint Online source, ensure that the instance that you plan to connect to is an Enterprise (E1) plan or higher.

Except for `site_collection_path`, the following fields are required to connect to a SharePoint Online source. If you do not know what to enter in these fields, contact your SharePoint administrator, or consult the [Microsoft SharePoint developer documentation](https://docs.microsoft.com/en-us/sharepoint/dev/){: external}:

-  `username` - The `username` to connect to the SharePoint Online SiteCollection that you want to crawl. This user must have access to all sites and lists that the user wants to crawl and index. Your `username` input must be a default Azure Active Directory (Azure AD) account, which is formatted as follows: `<username>@<domain>.onmicrosoft.com`. If you do not have an Azure AD username, contact your SharePoint site administrator.
-  `password` - The `password` to connect to the SharePoint Online SiteCollection that you want to crawl. This value is never returned and is only used when creating or modifying credentials.
-  `organization_url` - The `organization_url` of the source that you want to crawl. When you enter this input, only enter the domain name of the URL, for example `https://<company>.<domain>.com/`. If you enter a URL that extends beyond the domain name, or `.com/`, the input is invalid. Replace `<company>` and `<domain>` with the corresponding parts of the organization URL that you want to crawl.
-  `site_collection_path` Optional: - The `site_collection_path` to the source that you want to crawl. For example, if your organization URL is `https://<company>.<domain>.com/sites/test`, the `/sites/test` segment is the input to enter in this field. You cannot enter the full organization URL in this field, and you cannot specify any input that has the extension `.aspx`, such as URLs to document libaries, lists, and subsites. For example, the following URL to a list is invalid input: `https://..com/Lists//AllItems.aspx`. If unspecified, the default is `/`, and the root site collection is crawled.

Note the following items when you crawl Microsoft SharePoint Online:

-  To crawl SharePoint, the `username` account does not need `SiteCollection Administrator` permissions.
-  When you crawl SharePoint, you must have the list of SharePoint site collection paths that you want to crawl. {{site.data.keyword.discoveryshort}} does not support folder paths as input.
-  You might want to use the default Azure AD authentication.
-  Because the SharePoint API does not return a unique ID for ListItems, ListItem documents in {{site.data.keyword.discoveryshort}} are overridden when the IDs of different ListItems are the same. To ensure that your ListItems are not overridden and that each has a unique ID, recrawl your collection, or change the configuration settings for your data source so that your ListItems are assigned a unique ID.
-  SharePoint Online cannot crawl `Personal SiteCollections`.

To successfully crawl Microsoft SharePoint Online, you must enable legacy authentication and Contribute level permissions. To enable legacy authentication, visit the [Azure portal](https://portal.azure.com/){: external}, or contact your SharePoint administrator. For assistance with enabling Contribute level permissions, you can also contact your SharePoint administrator.
{: important}

If you created a SharePoint Online account after January 2020, two-factor authentication is enabled for your account, by default. To crawl your SharePoint Online collection, you must disable two-factor authentication. To view and change your multifactor authentication status, see [View the status for a user](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfa-userstates#view-the-status-for-a-user){: external} or [Change the status for a user](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfa-userstates#change-the-status-for-a-user){: external}.
{: important}

### Web Crawl
{: #connectwebcrawl}

<!-- Learn more topic WDS -->
You can use the web crawler to crawl public websites that don’t require a password. You can select how often you'd like {{site.data.keyword.discoveryshort}} to sync with the websites, the language, and the number of hops.

-  `Sync my data` - You can choose to sync hourly, daily, weekly, or monthly.
-  `Select language` - Choose the language of the websites from the list of supported languages. For the list of languages that {{site.data.keyword.discoveryshort}} supports, see [Language support](/docs/discovery?topic=discovery-language-support). You should create a separate collection for each language.
-  `URL group to sync` - Enter your URL and click the **Add** button to add it to the URL group. To specify the **Crawl settings** for this URL group, click the ![Cog](images/icon_settings.png) icon. You can set the **Maximum hops**, which is the number of consecutive links to follow from the starting URL (the starting URL is `0`). The default number of hops is `2` and the maximum is `20`. If you are using the API, the maximum is `1000`. You can specify URL paths to exclude from the crawl in the **Exclude URLs where the path includes** field. Separate the paths, using commas, for example, if you specified the URL `http://domain.com`, you could exclude `http://domain.com/licenses` and `http://domain.com/pricing` by entering `/licenses/, /pricing/`.

FAQ extraction was available as a beta feature that was supported only with web crawl connectors built for use from a Search skill in {{site.data.keyword.conversationshort}}. The beta feature is deprecated. FAQ extraction will stop being supported in v1 {{site.data.keyword.discoveryshort}} service instances on 1 March 2022.
{: deprecated}

When you specify a URL to crawl, the final `/` determines the subtree to crawl. For example, if you enter the URL `https://www.example.com/banking/faqs.html`, all URLs that begin with `https://www.example.com/banking/` are crawled, and the input of `https://www.example.com/banking` crawls all URLs that begin with `https://www.example.com/`. If you would like to restrict the crawl to a specific URL, such as `https://www.example.com/banking/faqs.html`, enter that URL in the `URL group to sync` field, and then set the **Maximum hops** to `0`.

The web crawler does not crawl dynamic websites that use JavaScript to render content. You can confirm the use of JavaScript by viewing the source code of the website in your browser.

The number of web pages crawled is limited to 250,000, so the web crawler might not crawl all the specified websites and might reach the maximum number of hops.
{: note}

The crawler has a limit of 10,000 child URLs per URL that is crawled. If the number of child URLs within any crawled URL exceeds 10,000, the crawler cannot process any of the content in the child URLs.
{: note}

If you require different **Crawl settings** for other URLs, click **Add URL group** and create a new group. You can create as many URL groups as you need.
{: tip}

### SharePoint OnPrem
{: #connectsp_op}

<!-- Learn more topic WDS -->
To connect to SharePoint OnPrem, you must first install and configure {{site.data.keyword.SecureGatewayfull}}. For more information about installing {{site.data.keyword.SecureGatewayfull}}, see [Installing IBM Secure Gateway for on-premises data](/docs/discovery?topic=discovery-sources#gateway).
{: note}

You can use this connector to crawl a SharePoint 2013, 2016, or 2019 on-premises data source. The crawler supports Windows New Technology LAN Manager (NTLM) v1 authentication only. It does not support NTLM v2 or Security Assertion Markup Language (SAML) authentication.

Complete the following fields to connect to the data source. If you do not know what to enter in these fields, contact your SharePoint administrator, or consult the [Microsoft SharePoint developer documentation](https://docs.microsoft.com/en-us/sharepoint/dev/){: external}:

-  `username` - The `username` to connect to the SharePoint OnPrem web application that you want to crawl. This user must have access to all sites and lists that they want to crawl and index.
-  `password` - The `password` to connect to the SharePoint OnPrem web application that you want to crawl. This value is never returned and is only used when creating or modifying credentials.
-  `web_application_url` - The SharePoint OnPrem `web_application_url`, for example `https://sharepointwebapp.com:8443`. If you do not enter a port number, the default is port `80` for HTTP and port `443` for HTTPS.
-  `domain` - The `domain` of the SharePoint OnPrem account.

Note the following items when you crawl Microsoft SharePoint OnPrem:

-  To crawl SharePoint OnPrem, the `username` account must have `SiteCollection Administrator` permissions.
-  To crawl SharePoint OnPrem, you must have the list of SharePoint site collection paths that you want to crawl. {{site.data.keyword.discoveryshort}} does not support folder paths as input.
-  The number of gateways that you can create is limited to 50. If you exceed this limit, you will be unable to create any more gateways, and you will see an error message that states, `Failed to update or create the network resource.`.
-  SharePoint OnPrem cannot crawl `Personal SiteCollections`.

### IBM Cloud Object Storage
{: #connectcos}

<!-- Learn more topic WDS -->
When you connect to an {{site.data.keyword.cos_full_notm}} source, the following credentials are required. You can obtain them from your {{site.data.keyword.cos_full_notm}} administrator:

-  `endpoint` - The `endpoint` name used to interact with {{site.data.keyword.cos_full_notm}} data.
   Do not enter `http://` or `https://`, as part of the {{site.data.keyword.cos_full_notm}} `endpoint` credential. Otherwise, you might receive an error message indicating that you have invalid or expired credentials. For the proper formatting of endpoints, see the column named Endpoint in the table in [Regional Endpoints](/docs/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints-region).
-  `access_key_id` - `access_key_id` obtained when the {{site.data.keyword.cos_full_notm}} instance was created.
-  `secret_access_key` - `secret_access_key` to sign requests obtained when the {{site.data.keyword.cos_full_notm}} instance was created.

IAM authentication is not currently supported for this connector. You need to set up HMAC authentication before you configure this connector. See [Service Credentials](/docs/cloud-object-storage/iam?topic=cloud-object-storage-service-credentials) for instructions.
{: important}

After this information is entered, you can choose how often you want to sync your data and select the buckets you want to sync to.

Other items to note when you crawl {{site.data.keyword.cos_full_notm}}:

-  This connector does not support crawling private endpoints.
-  For more information about {{site.data.keyword.cos_full_notm}} endpoints, see [Endpoints and storage locations](/docs/cloud-object-storage/basics?topic=cloud-object-storage-endpoints).
-  There is a slight performance issue if all buckets are selected. In this case, a delay is possible, before the documents complete indexing.

## Creating a collection using the tooling
{: #source_tooling}

Connecting to a data source using the {{site.data.keyword.discoveryshort}} tooling is performed by creating a collection specifically for a source. Perform the following steps to create a source collection and crawl it:

1.  From the **Manage data** page of the {{site.data.keyword.discoveryshort}} tooling, select **Connect a data source**.
2.  Select the data source that you want to connect to. If you select an on-premises data source, install the {{site.data.keyword.SecureGatewayfull}}. For more information, see [Installing IBM Secure Gateway for on-premises data](/docs/discovery?topic=discovery-sources#gateway).
3.  Enter your source credentials, and click **Connect**. You must obtain your source credentials from your source system administrator.
4.  Choose which data that you want to crawl and how often you want to sync it:
    -  **once an hour**: runs every hour
    -  **once a day**: runs every day between the hours of 00:00 and 06:00
    -  **once a week**: runs every week on Sunday between hours of 00:00 and 06:00
    -  **once a month**: runs every month on the first day of the month between the hours of 00:00 and 06:00
    
    Example crawl status:
    
    ```json
    "crawl_status" : {
    "source_crawl" : {
      "status" : "completed",
      "next_crawl" : "2019-02-10T05:00:00-05:00"
    }
    ```
    {: codeblock}

5.  Click **Save & Sync objects** to start crawling your data source. You are then redirected to the collection status page, which updates as documents are added to the collection.

After the initial sync, all subsequent crawls run on the frequency that you specified. For information about managing a collection, see [Manage collections](/docs/discovery?topic=discovery-sources#manage-collections).

In the tooling, the default time zone of the crawl schedule is set to `America/New_York`. Therefore, {{site.data.keyword.discoveryshort}} recrawls your collection at the interval that you specified for that time zone.
{: note}

If you modify anything in the **Sync settings** screen and then click **Save and Sync objects**, a crawl starts at that time or restarts if one is already running.
{: note}

When you connect to a data source, you can see document level errors under **Errors and warnings** on your collection page. There is a delay in publishing the errors and warnings that are related to a crawl.
{: note}

## Creating a collection using the API
{: #source_api}

Use the following process to create a collection connected to a data source, using the API.

When you create a collection by using the API, the default time setting for crawling and recrawling is set to UTC.
{: note}

If you plan to connect to an on-premises data source, first, you must install {{site.data.keyword.SecureGatewayfull}}. For more information, see [Installing IBM Secure Gateway for on-premises data](/docs/discovery?topic=discovery-sources#gateway).

The following example uses the SharePoint data source.

1.  Create credentials for the source that you are connecting to using the [Source Credentials API](/apidocs/discovery#create-credentials){: external}. Record the returned **credential_id** of the newly created credentials.
2.  Create a new configuration, using the [Add configuration](/apidocs/discovery#add-configuration){: external} API method. To define what to crawl, include a **source** object that contains the **credential_id** that you recorded earlier.

    ```json
    "source" : {
      "type" : "salesforce",
      "credential_id" : "{credential_id}",
      "schedule" : {
        "enabled" : true,
        "time_zone" : "America/New_York",
        "frequency" : "weekly"
      },
      "options" : {
         "site_collections" : [ {
         "site_collection_path" : "/sites/TestSiteA",
         "limit" : 10
         } ]
      }
    }
    ```
    {: codeblock}

    Record the returned **configuration_id** of the newly created configuration.
3.  Create a new collection using the [Collections API](/apidocs/discovery#create-a-collection){: external}. The object defining the collection must contain the **configuration_id** that you recorded earlier.

The source crawl begins as soon as you create the collection. After the initial crawl, all subsequent crawls run on the frequency that you specified. For information about managing a collection, see [Manage collections](/docs/discovery?topic=discovery-sources#manage-collections).

If you modify anything in the **source** object of the configuration, a new crawl starts at that time or restarts if one is already running.
{: note}

### Specifying a `customer_id`
{: #source_customer_id}

A `customer_id` field in an ingested {{site.data.keyword.discoveryshort}} document can be used to delete content based on the `customer_id` using the **user-data** method in the API. Incoming documents from a data source are not automatically assigned a `customer_id` when ingested. If your application requires a `customer_id` to be defined, you can specify one (or more) of the incoming fields from the source system to be copied and used as a `customer_id`. To do this you must modify the configuration that is being used to connect to the source.

1.  Perform a sample query and identify which field you want to use as a `customer_id`.
2.  Modify the configuration. Add a **Normalization** section to create the `customer_id` field.
    -  In the tooling, navigate to your collection and click the **edit** link in the configuration section. Next, click the **Normalization** tab and add in a **copy** normalization to create the `customer_id` field. Then click **Apply & save**.
    ![Copy normalization](images/norm_copy.png)
    -  When you use the API, add the following object to the **normalizations** array:

       ```json
       {
         "operation" : "copy",
         "source_field" : "{original_field_name}",
         "destination_field" : "customer_id"
       }
       ```
       {: codeblock}

3.  The next scheduled crawl adds the `customer_id` field to all documents. To start a crawl immediately, modify the source configuration (**Sync settings** in the tooling).

See [Information security](/docs/discovery?topic=discovery-information-security) for more information and information about deleting based on `customer_id`.

## Managing collections
{: #manage-collections}

After you create a collection, you can view a crawler status or change the content that you want to crawl, your security credentials to connect to a data source, or a crawler schedule.
{: shortdesc}

When you click **Manage data**, these tabs are available after collection processing finishes. The tabs contain data that is associated with your collection and options for managing it.

**Overview** tab:
- The number of documents
- The collection status. While syncing is in progress, the collection status states, `Sync in progress`. If you recrawl your collection when the sync is in progress, the current crawler stops, and a new full crawling session begins. Unless you want to make a change to your collection immediately, you might want to wait until syncing completes before starting a recrawl. When collection processing completes, you receive a status message that states, `Your documents have finished processing! You can now work with your full data set.`.
- The **Next sync scheduled for** date and time. Your current crawl schedule settings determine the **Next sync scheduled for**, which updates if you change your crawl schedule in the **Sync settings** tab. Also, when your next scheduled crawl begins, the **Next sync scheduled for** automatically updates.
- A list of warnings and errors
- Any fields that the crawler identified from your data
- Any enrichments that were added to your data and the option to **Add enrichments**
- Available sample queries and the option to **Build your own query**

**Errors and warnings** tab:
- A list of any warnings and errors that might appear while your collection processes, such as the affected file name and its associated document ID

**Sync settings** tab:
- The option to change your security credentials. If your security credentials for connecting to a data source change, you must update your credentials. To update your credentials, in the **Your service's credentials** pane, click **Edit credentials**.
- The option to edit the content that you want to crawl in the **Enter the data that you would like to sync** pane. You can change or delete any URL or file path that you already specified. To delete a URL or file path, click the minus icon next to the ![Settings](images/icon_settings.png) icon.
- The option to change your crawler schedule in the **Additional settings** pane by clicking **Sync frequency**
- The **Crawl settings** dialog box. For example, if you select **Web Crawl** and you already added a start URL, you can click the ![Settings](images/icon_settings.png) icon next to the start URL to access the **Crawl settings** dialog box. In this dialog box, you can specify the **Maximum hops** or exclude URLs that include specific subdirectories in **Exclude URLs where the path includes**.

**Search settings** tab:
- The option to upload a synonym list file to enhance your query
- The option to upload a stopwords file to further enhance the relevance of your results

For information about creating a collection, see [Creating a collection using the tooling](/docs/discovery?topic=discovery-sources#source_tooling) or [Creating a collection using the API](/docs/discovery?topic=discovery-sources#source_api).

## Installing IBM Secure Gateway for on-premises data 
{: #gateway}

<!-- Learn more topic WDS -->
To connect to an on-premises data source, you first need to download, install, and configure {{site.data.keyword.SecureGatewayfull}}. After you install {{site.data.keyword.SecureGatewayfull}} for your first on-premises data source, you won't need to repeat this process.

1.  From the **Manage data** page of the {{site.data.keyword.discoveryshort}} tooling, select **Connect a data source**.
1.  Select the data source that you want to connect to. When you select an on-premises data source, go to the **Connect to your on-premise network** section and click the **Make connection** button.
1.  On the **Download and install the Secure Gateway Client** screen, download the appropriate version of {{site.data.keyword.SecureGatewayfull}}.
1.  After you complete the download, click **Download Secure Gateway and Continue**. When prompted, enter the **Gateway ID** and **Token** that are displayed. For more information about installation, see [Installing the client](/docs/SecureGateway?topic=SecureGateway-client-install).
1.  On the machine running the Secure Gateway Client, open the Secure Gateway dashboard at `http://localhost:9003`.
1.  Click **add ACL** on the dashboard. Add the endpoint URL of each SharePoint collection to the **Allow access** list. For example, Hostname: `mycompany.sharepoint.com` and port: `80`.
1.  Return to the {{site.data.keyword.discoveryshort}} tooling and click **Continue**. If the connection is successful, a `Connection successful` message displays. If the connection was not successful, open the {{site.data.keyword.SecureGatewayfull}} dashboard, and verify that the endpoints on the **Allow access** list are correct.

After the connection is successful you can begin entering the credentials for your on-premises data source.

## Data source connection and data isolation
{: #source_isolation}

[Connecting to external data sources](/docs/discovery?topic=discovery-sources) reduces the data isolation of your service instance because data in transit between the source and the service cannot be isolated. All other isolation (at-rest, administration, query) remains in full. All in-flight communication between and within services and data sources is encrypted using TLS v1.2. The private keys for the TLS certificates are encrypted at rest using AES-256-GCM, the service certificates expire every three years, and the certificate revocation lists are updated monthly. All credentials are sent over an encrypted connection using TLS v1.2 and encrypted at rest using AES-256. Connections to those data sources use whatever secure protocols are supported by those data sources.
