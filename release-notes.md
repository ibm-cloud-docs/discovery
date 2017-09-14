---

copyright:
  years: 2015, 2017
lastupdated: "2017-09-14"

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

# Release notes

The release notes provide information about changes to the {{site.data.keyword.discoveryfull}} service since the previous release.
{: shortdesc}

## Service API Versioning
{: shortdesc}

API requests require a version parameter that takes a date in the format `version=YYYY-MM-DD`. Whenever we change the API in a backwards-incompatible way, we release a new minor version of the API.

Send the version parameter with every API request. The service uses the API version for the date you specify, or the most recent version before that date. Don't default to the current date. Instead, specify a date that matches a version that is compatible with your app, and don't change it until your app is ready for a later version.

The current version is `2017-09-01`.

## Beta features
{: #beta-features}

IBM will release services, features, and language support that are classified as beta or experimental. These capacities can be unstable, can change frequently, and can be discontinued with short notice. They are provided so you can evaluate their functionality. A beta or experimental capacity might not provide the same level of performance or compatibility that generally released capacities provide. These capacities are not designed for use in a production environment, and any such use is at your own risk.


## Changes
{: #change-log}

The following new features and changes to the service are available.

### 14 September 2017

{{site.data.keyword.discoveryshort}} tooling:

- Added the Data Schema Explorer, which displays the fields and values in your transformed documents. This information can be used to understand the data structure of your collection before building queries using the Discovery Query Language. The data schema can be viewed two ways: by document (Document view), or by field (Collection view). To access the Data Schema Explorer: on the **My Data Insights** screen, click the **View data schema** button, or click the **View Data Schema** icon on the left.

### 6 September 2017

- Added the beta ability to deduplicate documents returned from your query. This beta feature works for both private and Watson Discovery News collections. See [Excluding duplicate documents from query results](/docs/services/discovery/query-reference.html#deduplication) for details.

Document deduplication is currently supported only as a beta capability. See the statement regarding betas at the top of this document for more information.

### 31 August 2017

- The version string for all API calls has changed to `2017-09-01` from `2017-08-01`. This version includes updates that will filter out the following invalid JSON fields during preview and ingestion so that only valid JSON fields are ingested. Update your version string to `2017-09-01` to avoid conflicts and possible errors.

   - `id`, `score`, and `highlight` at the top level (You can continue to add documents to your collection using document IDs with the `add a document` function. See the [API Reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#add-doc){: new_window} for details.
   - `_` prefixed field names at the top level (as a result, when querying for a document by ID, you can query for `id` instead of `_id`.)
   - `#` and `,` in the field name
   - `+` and `-` prefixed field names
   - `"` `"` empty values for a field name

**Note:** If your JSON documents include these characters in the field names, or `id`, `score`, and `highlight` at the top level, you need to remove them before adding the documents to your collection, or those fields will be empty. You can create a custom configuration and normalize your JSON before adding documents to your collection to avoid this issue. See [Custom Configuration](/docs/services/discovery/building.html#custom-configuration).  In addition, documents that include the punctuation characters `?`, `:`, or `#` in the file name will cause errors at ingestion time. Rename any documents that include these characters before ingesting them.

- The retrieval methods for `natural_language_query` have been updated to improve the relevance of results by matching words with related semantics. This update only affects collections that have not had relevance training. If you are using `natural_language_query` and have not conducted relevance training, you may see improvement in the order of results returned.

{{site.data.keyword.discoveryshort}} tooling:

- Changes to the query builder to make it easier to toggle between the Discovery Query Language and Natural Language query options, as well as among query, filter, and aggregation.


### 25 August 2017

- The `passages` array now includes `field`, `start_offset`, and `end _offset`. `field` is the name of the field the passage was extracted from. `start_offset` is the starting character of the passage text within the field. `end_offset` is the ending character of the passage text within the field.

{{site.data.keyword.discoveryshort}} tooling:
This query building enhancement can be found on the **Build your own query** screen.

-  Added the beta ability to write queries in the {{site.data.keyword.discoveryshort}} Query Language with a visual builder. Click **Build in visual mode** in the **Search for documents** and **Limit which documents you query** sections to try it out.  As you build your query visually, it will display in the **{{site.data.keyword.discoveryshort}} Query Language** below it.

   The visual query builder is currently supported only as a beta capability. See the statement regarding betas at the top of this document for more information.

### 18 August 2017

{{site.data.keyword.discoveryshort}} tooling:

- Added support for nested aggregations and conditions to the beta visual aggregation builder introduced [11 August 2017](/docs/services/discovery/release-notes.html#11aug). There is a limit of 3 conditions per aggregation row.

   The visual aggregation builder is currently supported only as a beta capability. See the statement regarding betas at the top of this document for more information.

### 11 August 2017
{: #11aug}

{{site.data.keyword.discoveryshort}} tooling:

Both features are query building enhancements and can be found on the **Build your own query** screen.

- Added the option to select a query from a set of pre-built sample queries and aggregations. Click **Use a sample query** at the top right to access the list. If you are querying a private data collection, the samples use `top entities`, `categories`, etc. found in your collection. These queries can be used as a starting point for writing your own queries. Sample queries are available for both {{site.data.keyword.discoverynewsfull}} and private collections.

-  Added the beta ability to write aggregations with a visual builder. Click **Build in visual mode** above the **Write an aggregation query using the {{site.data.keyword.discoveryshort}} Query Language** field to try it out.  As you build your aggregation visually, the query will display in the **{{site.data.keyword.discoveryshort}} Query Language** below it.  

   The visual aggregation builder is currently supported only as a beta capability. See the statement regarding betas at the top of this document for more information.

### 31 July 2017

- A new version of {{site.data.keyword.discoverynewsfull}} was released. The original version has been renamed {{site.data.keyword.discoverynewsfull}} Original and has been retired with a removal from service date of **15, January 2018**. See [Migrating from Watson Discovery News Original](/docs/services/discovery/migrate-bwdn.html) for migration instructions.
  **Note:** If you have created a new instance of {{site.data.keyword.discoveryshort}}, you will only have access to the new version of {{site.data.keyword.discoverynewsfull}}.

- A new pricing plan for {{site.data.keyword.discoveryfull}} was released. See [{{site.data.keyword.discoveryshort}} pricing plans](/docs/services/discovery/pricing-details.html) for details.

- The version string for all API calls has changed to `2017-08-01` from `2017-07-19`. This version includes updates for the new pricing plan and the new version of Watson Discovery News. Update the version string to avoid conflicts and possible errors.

### 19 July 2017

 - As part of the pricing change that has been announced for August 1st 2017, users that are currently on the deprecated **30 day free trial** plan will be automatically migrated to the **Lite** plan. As a result of this transition, existing users may have met or exceeded the lite plan limit on documents _(2000)_, storage _(200Mb)_, or number of collections _(2)_. If you have exceeded the limit of the **Lite** plan, you will not be able to add any additional content into the service but you can still query collections. You can view the current status of all these limits by using the {{site.data.keyword.discoveryshort}} tooling or API. To be able to resume adding content to the {{site.data.keyword.discoveryshort}} instance, you must do one of the following:
   - remove collections and/or documents so that limits of the **Lite** plan are not exceeded.
     Documents can be deleted either individually through the API using the [delete-doc](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-doc) method, or whole collections can be deleted using the Tooling or API using the [delete-collection](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-collection) method
   - upgrade your plan to a level that meets your storage needs.
 - Customers with size **`1`** **`2`** or **`3`** environments will be automatically migrated to the **Advanced** plan.

### 17 July 2017

 - The following capabilities have been moved from beta status to GA status:

   - Relevancy training
   - Natural language query
   - Highlighting

 - As of this release, {{site.data.keyword.discoveryfull}} is changing its enrichment mechanism from {{site.data.keyword.alchemylanguageshort}} to {{site.data.keyword.nlushort}}. {{site.data.keyword.alchemylanguageshort}} is in the process of being deprecated, you should start using {{site.data.keyword.nlushort}} as soon as possible.  See [Migrating from {{site.data.keyword.alchemylanguageshort}} enrichments to {{site.data.keyword.nlushort}} enrichments](/docs/services/discovery/migrate-nlu.html) for details.
   **Note:** When integrating with Watson Knowledge Studio, the {{site.data.keyword.alchemylanguageshort}} enrichment configuration must be still used. See [Integrating with {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery/integrate-wks.html) for details.

 - The version string for all API calls has been changed to `2017-07-19` from `2017-06-25`. This version enables a NLU default config on collection creation. You should still be able to enrich with {{site.data.keyword.alchemylanguageshort}} in previous versions.

    The default configuration has been updated to use {{site.data.keyword.nlushort}}. You should update the version string as soon as possible to avoid conflicts and possible errors.

    {{site.data.keyword.discoveryshort}} supports English, German, and Spanish language collections, however, several enrichments are not supported in German and Spanish. The supported enrichments for each language are:

|  | Sentiment Analysis | Semantic Role Extraction | Keyword Extraction | Entity Extraction | Emotion Analysis | Concept Tagging | Category Classification |
|--|--------------------|--------------------------|--------------------|--------------------|-----------------|-----------------|-------------------------|
| English    | X                        | X                  | X                  | X               | X               | X              | X              |
| German     | X                        |                    | X                  | X               |                 |                |                |
| Spanish    | X                        | X                  | X                  | X               |                 | X              | X             |

 - Discovery Tooling:

    The Insight Cards for collections enriched with {{site.data.keyword.alchemylanguageshort}} enrichments will no longer update automatically. You must migrate your collection to {{site.data.keyword.nlushort}} Enrichments for the insight cards to update.

    If you created a collection prior to **18 July, 2017** and applied the **Default Configuration**, that collection was enriched with the {{site.data.keyword.alchemylanguageshort}} enrichments. If you apply the **Default Configuration** to a collection after this date, the {{site.data.keyword.nlushort}} enrichments will be used (the configuration name will switch to **Default Configuration with NLU** in the tooling). Since {{site.data.keyword.alchemylanguageshort}} enrichments are being deprecated, they should not be used with new collections.

### 30 June 2017

 -  The entity normalization capability introduced as a beta feature on 5 May 2017 has been moved to GA status. See [Creating a custom configuration to normalize entities](/docs/services/discovery/normalize-entities.html) for details.

### 23 June 2017

 - The version string for all API calls has changed to `2017-06-25` from `2016-12-01`. The new version string enables enrichments in German (`de`) or Spanish (`es`) if the language of a collection is set to one of those languages. Previously, all enrichments were performed in English regardless of a collection's language setting.

    If you do not use enrichments in non-English languages, you can continue to use the `2016-12-01` version string. However, you should update the version string as soon as possible to avoid potential future conflicts.

 - Anomaly detection is now available as part of `timeslice` aggregations as a GA capability. See the [Query building reference](/docs/services/discovery/query-reference.html#anomaly-detection) for details.

 - Discovery Tooling:

   - Added the beta ability to improve the relevancy of query results using the Discovery tooling (relevancy tooling). See [Improving the relevance of your query results with the Discovery tooling](/docs/services/discovery/train-tooling.html).

### 19 June 2017

  - Discovery Tooling:

    - Added option to specify the language of the documents in a new collection as English, Spanish, or German. To use it, choose **Select the language of your documents** on the **Name your new collection** dialog.

    - Added a **Summary** tab to the **Build your own query** screen. The **Summary** tab displays an overview of the full query results provided in the existing **JSON** tab. The **Summary** display will vary based on your query and enrichments. Information that may be displayed includes: document name or ID, aggregation statistics, document passages in order of relevance, and results by enrichment.

    - Added a Natural Language Query option to the **Build your own query** screen. To use it, click **Ask a question in plain language** in the **Search for documents** section and a field will appear where you can enter your question. The original query field (formerly titled **Enter a query or keyword**) can now be accessed by clicking the **Use the Discovery Query Language** button.

    - The **Build your own query** screen was redesigned, but all fields and options remain. Following are the old and new names for the fields.

| **Old field name**                                           | **New field or section name**                                                                                             |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| Write and run a query                                    | Search for documents                                                                                                  |
| Narrow your query results (Filter)                       | Limit which documents you query                                                                                       |
| Group query results (Aggregation)                        | Include analysis of your results                                                                                      |
| Fields to display                                        | Name did not change, but moved to the new **Customize display options** section.                                      |
| Number of documents to return (Count)                    | Number of documents to return [This field was moved to the **Customize display options** section.]                    |
| Include matching passages                                | Include relevant passages [This field was moved to the **Customize display options** section.]                        |
| Number of query fields to skip at the beginning (Offset) | Number of query results to skip at the beginning [This field was moved to the **Customize display options** section.] |

### 5 June 2017

 - Watson Discovery News queries now display only the first 150 words of each article in the `text` and `alchemyapi_text` JSON fields. The `blekko.snippet` field will display only the first sentence of the snippet array.

### 30 May 2017

 - The `passages` parameter on the query API has been moved from beta to GA status.

### 25 May 2017

 - Discovery Tooling: query field highlighting was added in this release. This feature adds yellow highlighting to field names in the JSON of the Results pane. All fields that are queried or filtered on are highlighted for each result even if the content of the field does not match the query. Any fields used in aggregations are also highlighted in the query results, but only the first aggregation operation is highlighted.

### 10 May 2017

 - The `query` and `notices` methods now support the `highlight` parameter. The parameter is a boolean. When you run a query and specified `highlight` as `true`, the service returns output that includes a new `highlight` field in which words that match the query are wrapped in HTML `*` (emphasis) tags. See the [Query building reference](/docs/services/discovery/query-reference.html) for details.

 - It is possible for the deletion of an environment to complete only partially, resulting in a situation in which a new environment cannot be created because only a single environment per service instance is permitted. If you attempt to delete and then create an environment but see either operation stuck in the `pending` state, it is likely you have encountered this problem. To work around it, re-run the deletion operation to complete it, then create the new environment.

### 8 May 2017

 - Updated the emotion tone score model to improve precision on emotion analysis (`docEmotion`) enrichments. The training dataset was expanded and feature engineering was altered and as a result, the model has higher precision on the benchmark dataset.

### 5 May 2017

 - Entity normalization is now available for use with the Discovery service that use a custom model generated by Watson Knowledge Studio. Entity normalization inserts normalized (canonical) names for different references to the same person or object in the source document. See [Creating a custom configuration to normalize entities](/docs/services/discovery/normalize-entities.html) for details.

     **Note:** Entity normalization is currently supported only as a beta capability. See the statement regarding betas at the top of this document for more information.

 - The Tooling error log is no longer limited to a maximum of eight (8) pages of results. The error log still displays the document ID if the document name is not available.

 - Configuration names are limited to 50 characters and must consist of the characters `[a-zA-Z0-9-_]`.

 - The `passages` parameter previously available only through the API is now available through the Tooling as well as the API.

### 25 April 2017

  - The service now enables you to provide *training data* to improve the accuracy of your query results. When you provide a Discovery instance with training data, the service uses advanced Watson algorithms to determine the most relevant results. As you add more training data, the service instance becomes more accurate and sophisticated in the results it returns. See ["Improving the relevance of your query results"](/docs/services/discovery/train.html) and the [API Reference ](http://www.ibm.com/watson/developercloud/discovery/api/v1/#training-data) for information.

  - The API now supports the `natural_language_query` parameter as a beta release. This parameter enables you to specify a query in natural language instead of in the Discovery service's query language. See the ["Query your collection"](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection) method in the API reference for information.

  - Documentation updates and errata corrections.

### 14 April 2017

Enhancements have been added to the query API (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`). See the ["Query your collection"](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection) method in the API reference for information.

  - The query API now supports the `passages` parameter. If the parameter is set to `true`, the query returns a set of the most relevant passages from the documents in your collection. The passages are generated by sophisticated Watson algorithms to determine the best passages of text from all of the documents returned by the query. This enables you to find information and context more precisely. See the ["Query your collection"](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection) method in the API reference for information.

    - Specifying `passages=true` in your query can reduce performance as a result of increased processing to extract passages. With larger environments, the performance impact can be lessened.

    - The `passages` parameter is supported only on private collections. It is not supported in the Watson Discovery News collection.

    - The `passages` parameter currently returns a maximum of 10 results. The number of returned results cannot be changed.

    - The `passages` parameter returns a maximum of three (3) passages from any given document in the collection. If a document contains more than three additional relevant passages, the parameter does not return them.

### 7 April 2017

- The query API (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`) now supports the `sort` parameter, which enables you to specify a comma-separated list of fields in the document to sort on. See the ["Query your collection"](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection) method in the API reference for information.
- The `timeslice` parameter for query aggregations now correctly handles dates in UNIX epoch format. See the ["Query building reference"](/docs/services/discovery/query-reference.html#aggregations) for information about aggregations and the `timeslice` parameter.
- Improvements to error messages.
- Updates to the service's Java SDK. See the [API Reference](http://www.ibm.com/watson/developercloud/discovery/api/v1/?java) for details.
- The following limitations to the use of wildcards in queries are now fixed and work correctly:

  - Only one wildcard worked in any given query. For example, `query-month:*ctober` worked, but `query-month:*ctobe*` generated a parsing error.
  - Wildcards did not work with queries that contained capital letters. For example, given the key/field pair ``{"borrower": "GOVERNMENT OF INDIA"}``, `query-borrower:*ndia` returned results but `query-borrower:*NDIA` did not.
  - Wildcards did not work in the middle of phrases in queries. For example, given the key/field pair `{"borrower": "GOVERNMENT OF TIMOR"}`, `query-borrower:"GOVERNMENT OF TIMOR"` returned results but `query-borrower:"GOVERNMENT OF TI*OR"` did not.

### 24 March 2017

- Added filtering to the "My data insights" screen in the Discovery tooling

### 15 March 2017

The following known issues have been discovered.

-  All fields that are ingested from HTML, PDF, and Word documents are typed as **string**. JSON fields and calculated fields, such as sentiment score, are typed as defined.
- The `preview` operation does not currently check for nested JSON arrays within a submitted JSON document. The service does not currently support nested JSON arrays, so a document with nested arrays can successfully pass the `preview` operation but fail upon an ingestion attempt.
- If you encounter ingestion errors with the message `unsupported text language`, update your configuration with the `"language": "english"` enrichment option to force all text to be interpreted as English, as shown in the following example.

```json
"enrichments": [
   {
     "enrichment": "alchemy_language",
     "source_field": "author.label",
     "options": {
       "extract": "taxonomy,entity,relation,doc-emotion,doc-sentiment,concept,keyword",
       "sentiment": true,
       "quotations": true,
       "language": "english"
     }
   }
 ]
```
{: codeblock}

The following bugs have been fixed.

- Improved performance and stability of the service.

### 8 March 2017

 - Optimized the back end, including the addition of new timeouts, to improve overall performance.
 - Fixed a bug that caused the environment status of free (`0`-sized) environments to report a status of `pending` regardless of the real status.
 - The only national language currently supported by {{site.data.keyword.discoveryshort}} is U.S. English (`en_US`).

### 3 March 2017

- Added the "My data insights" screen to the Discovery tooling.

### 26 February 2017

-     The performance of the {{site.data.keyword.discoverynewsshort}} environment has been improved.
-  The {{site.data.keyword.discoverynewsshort}} service returns only 50 results at a time. As a workaround, use the `offset` parameter in your query to page through results.
-  You can submit a new configuration with an individual document by using the following command:

```bash
curl -X POST -u {username}:{password} -F "file=@wikipedia-sample.html" -F "configuration=$(cat config.json)" "https://gateway.watsonplatform.net/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2016-12-01"
```
{: pre}
-  The service's PDF and Word converters create HTML as a middle step. The service can apply additional transforms and normalizations on the intermediary HTML before the final transformation to normalized JSON.

The following bugs have been fixed.

-  Improved error codes.
-  Corrected several documentation errata.

### 16 February 2017

-  You can now use CSS selectors to select JSON fields that you can then apply enrichments to. See [Using CSS selectors to extract fields](/docs/services/discovery/building.html#using-css) for information.
-  You can now increase the size of an environment by passing a new `size: X` parameter to the [update-environment method](http://www.ibm.com/watson/developercloud/discovery/api/v1/#update_environment), where `X` is an integer between 0 and 3. See the [create-environment method](http://www.ibm.com/watson/developercloud/discovery/api/v1/#create_environment) for information about environment sizes and attributes.

    **Note:** You cannot reduce the size of an existing environment. If you want to reduce the size of your environment, contact {{site.data.keyword.IBM}} support for assistance.

-  A new query operator is available. The `::!` operator has been added as a unary not-equals operator. For example, you can now run `query=field::!value` (not equals). Previously the only exclusionary operator was `:!` for the not-contains operator (for example, `query=field:!value`).

The following bugs have been fixed.

-  Applied security updates.
-  Improved status messages for search alerts.

### 1 February 2017

The following notes apply specifically to the Data Crawler 1.3.0 release.

-   The Data Crawler records the `document_id` values used to upload documents, and the status of the upload. Conversion notices are not persisted outside of the log. There is not presently a tool to interact with that data, but such tools are expected to be developed as time permits. The data is accessible via H2 database, which could be configured to use a remote DBMS.

### 16 January 2017

The following notes apply specifically to the Data Crawler 1.2.5 release.

-  The Data Crawler can optionally poll for document status immediately after uploading a file. This check is a part of the Crawler's concept of "uploading a document", so when this check is enabled, it is virtually impossible for the Crawler to upload concurrently more documents than what the {{site.data.keyword.discoveryshort}} service can process concurrently for the user.

    A side effect of the `check_for_completion` feature is that the Crawler also can expose to the user why a document failed, when it failed. Any notices attached to a document that was successfully uploaded, but failed to process, are displayed in the Crawler log. The notices are not exported to a processable file, but IBM would welcome a feature suggestion for that.

### 5 January 2017

The following notes describe issues that were identified after the GA release on 15 December 2016.

-   If you add a document by using the `POST /v1/environments/{environment_id}/collections/{collection_id}/documents`
    or `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]` call, the call returns a document ID and the **processing** status. If you then query the document by using the `GET /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]` call, the status remains at **processing** until ingestion is completed, at which point the status changes to **available**.

    If you **update** an existing document by using the `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]` call, the corresponding **GET** call returns the `available` status even if the service has not yet fully processed the updated document. The `available` status can refer to either the original document or the updated document. Unless the update operation returns an error, there is not currently a way to determine the status of the updated document.

    You can work around this by waiting up to 10 minutes after submitting a document update before attempting to query the updated content.
-   You cannot upload JSON arrays. To upload a JSON array, you must upload each section individually. For example, the following JSON cannot be uploaded to the service:

    ```json
    [{
      "accepted": 1,
      "answer": "You shouldn't have any issues keeping it on all the time however some thing to consider is any counters you may have like the use of millis code . From the Arduino docs on millis a This number will overflow go back to zero after approximately 50 days. blockquote So for projects that are on for long periods of time you may not see an issue immediately but something like this could pop up and cause errors down the road. ",
      "answerScore": "49",
      "authorUserId": "3",
      "authorUsername": "Butzke",
      "downModVotes": 0,
      "id": 2,
      "subtitle": "I'm making a simple Arduino web server and I want to keep it turned on all the time. So it must endure to stay working continuously. I'm using an Arduino Uno with a Ethernet Shield. It's powered with a simple outlet power supply 5V 1A. My Questions Will I have any problems leaving the Arduino turned on all the time? li Is there some other Arduino board better recommended for this? li Are there any precautions that I need to heed regarding this? li ul ",
      "tags": "<arduino-uno><web-server><ethernet>",
      "title": "Is an Arduino capable of running 24 7?",
      "upModVotes": 49,
      "userId": "11",
      "userReputation": 4535,
      "username": "sachleen",
      "views": 3234
    }, {
      "accepted": 0,
      "answer": "A couple of things to keep in mind outside of Sachleen's mention of Milli's Like any electronics heat can be disruptive. The micro controller itself isn't likely going to be a huge issue from the perspective of heat but other components like the power supply might cause issues. li If your code uses EEPROMWrite a be aware that the EEPROM is only rated for something in the neighbourhood of 100 000 writes. li ul ",
      "answerScore": "24",
      "authorUserId": "3",
      "authorUsername": "Butzke",
      "downModVotes": 0,
      "id": 3,
      "subtitle": "I'm making a simple Arduino web server and I want to keep it turned on all the time. So it must endure to stay working continuously. I'm using an Arduino Uno with a Ethernet Shield. It's powered with a simple outlet power supply 5V 1A. My Questions Will I have any problems leaving the Arduino turned on all the time? li Is there some other Arduino board better recommended for this? li Are there any precautions that I need to heed regarding this? li ul ",
      "tags": "<arduino-uno><web-server><ethernet>",
      "title": "Is an Arduino capable of running 24 7?",
      "upModVotes": 24,
      "userId": "13",
      "userReputation": 489,
      "username": "Matthew G.",
      "views": 3234
    }]
    ```
    {: codeblock}

    To upload this information to the service, break down the array and upload each section, as follows:

    Section 1:

    ```json
    {
      "accepted": 1,
      "answer": "You shouldn't have any issues keeping it on all the time however some thing to consider is any counters you may have like the use of millis code . From the Arduino docs on millis a This number will overflow go back to zero after approximately 50 days. blockquote So for projects that are on for long periods of time you may not see an issue immediately but something like this could pop up and cause errors down the road. ",
      "answerScore": "49",
      "authorUserId": "3",
      "authorUsername": "Butzke",
      "downModVotes": 0,
      "id": 2,
      "subtitle": "I'm making a simple Arduino web server and I want to keep it turned on all the time. So it must endure to stay working continuously. I'm using an Arduino Uno with a Ethernet Shield. It's powered with a simple outlet power supply 5V 1A. My Questions Will I have any problems leaving the Arduino turned on all the time? li Is there some other Arduino board better recommended for this? li Are there any precautions that I need to heed regarding this? li ul ",
      "tags": "<arduino-uno><web-server><ethernet>",
      "title": "Is an Arduino capable of running 24 7?",
      "upModVotes": 49,
      "userId": "11",
      "userReputation": 4535,
      "username": "sachleen",
      "views": 3234
    }
    ```
    {: codeblock}

    Section 2:

    ```json
    {
      "accepted": 0,
      "answer": "A couple of things to keep in mind outside of Sachleen's mention of Milli's Like any electronics heat can be disruptive. The micro controller itself isn't likely going to be a huge issue from the perspective of heat but other components like the power supply might cause issues. li If your code uses EEPROMWrite a be aware that the EEPROM is only rated for something in the neighbourhood of 100 000 writes. li ul ",
      "answerScore": "24",
      "authorUserId": "3",
      "authorUsername": "Butzke",
      "downModVotes": 0,
      "id": 3,
      "subtitle": "I'm making a simple Arduino web server and I want to keep it turned on all the time. So it must endure to stay working continuously. I'm using an Arduino Uno with a Ethernet Shield. It's powered with a simple outlet power supply 5V 1A. My Questions Will I have any problems leaving the Arduino turned on all the time? li Is there some other Arduino board better recommended for this? li Are there any precautions that I need to heed regarding this? li ul ",
      "tags": "<arduino-uno><web-server><ethernet>",
      "title": "Is an Arduino capable of running 24 7?",
      "upModVotes": 24,
      "userId": "13",
      "userReputation": 489,
      "username": "Matthew G.",
      "views": 3234
    }
    ```
    {: codeblock}

### General Availability release, 15 December 2016

The following notes apply to the General Availability (GA) release of the {{site.data.keyword.discoveryfull}} service.

#### General notes

-   You cannot currently specify the data type of fields. All fields are indexed as text (data type **string**).
-   If you use the API to work with the service, you must specify the API version with each call. The current API version is **2016-12-01**.

    **Note:** The specific version is not enforced in the GA release, but it still must be listed to enable compatibility with future releases.

-   You can use the service with a custom model created with {{site.data.keyword.knowledgestudiofull}}. The custom model can be used to enrich ingested documents. You must use the API to integrate the custom model with the {{site.data.keyword.discoveryshort}} service; you cannot perform the integration by using the tooling. See [Integrating with {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery/integrate-wks.html "You can integrate a custom model from {{site.data.keyword.knowledgestudiofull}} with the {{site.data.keyword.discoveryshort}} service to provide custom enrichments.") for details.

#### Data management

-   Search indexes are not encrypted.
-   Backup and restore functions are not user controllable.

#### Environments

-   You can create only one environment per service instance to upload your own data.
-   {{site.data.keyword.discoveryshort}} service is located in a single availability zone (US South).
-   Dedicated and premium plans are not available at the current time.

#### Environment sizing

-   You can choose an environment size only when creating a new environment. The ability to resize an environment is not currently available to users.
-   Choosing an environment size with more RAM increases performance.
-   There are currently no prescriptive sizing recommendations available for specific use cases.
-   Custom sizing for {{site.data.keyword.knowledgestudiofull}} models is not self-serve. Contact your {{site.data.keyword.IBM}} representative for more information.

#### Ingestion limitations

-   The ingestion rate is currently limited to 100 concurrent document ingestion operations. An application that submits documents to the service for ingestion needs to respect HTTP 429 errors and throttle down ingestion requests accordingly.
-   {{site.data.keyword.alchemylanguageshort}} enrichments are limited to the first 50 kB per field.
-   Enrichments from {{site.data.keyword.knowledgestudiofull}} custom models are not limited, but split documents into 10-kB chunks. No relationships are annotated across chunk boundaries.

#### Query limitations

-   Excessive query load can cause the search-index process to restart automatically.
-   Applications that issue queries must enforce reasonable limits on the number of concurrent queries.

### Known issues

-   You cannot delete a document by using the tooling. If you need to delete a document, you must use the API's ["Delete a document"](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-doc) method as described in the API reference.

-   The API does not currently support getting a list of notices (warnings and error) that are generated during document ingestion. The tooling is therefore unable to show a list of ingestion notices, and there is no easy way to determine which, if any, documents crawled by the Data Crawler failed to be ingested.
-   Document status information is not always accurate.
    -   If an ingestion operation takes longer than the configured timeout of 10 minutes, the service reports that the document is not known to the service until the ingestion operation completes. After the operation completes, the document status is available and accurate.
    -   Documents that are successfully indexed but generated errors can have a status of **failed** for a short period of time until the document has been fully committed to the index. After the document has been committed to the index, the listed status is accurate.
-   You cannot use the tooling to replace a specific document. If you attempt to do so, the second document is uploaded as a separate document. If you are using the API and know the ID of the document you want to replace, you can do so; see ["Update a document"](http://www.ibm.com/watson/developercloud/discovery/api/v1/#update-doc) in the API reference. If you are using the Data Crawler, uploading an updated document from the same URL as a previous document replaces the original document.
-   If you are using the tooling to edit the enrichments in your configuration, you can edit only enrichments used for extraction. If you want to add or edit other enrichments (for example, custom enrichments from a {{site.data.keyword.knowledgestudiofull}} model), you must use the API. See the ["Update a configuration"](http://www.ibm.com/watson/developercloud/discovery/api/v1/#replace_configuration) method in the API reference for information.
-   The following notes apply specifically to the Data Crawler.
    -   The Data Crawler retries uploads if it encounters an upload failure.
    -   The Data Crawler is unable to retry documents that uploaded successfully but failed to be converted or indexed.
    -   The Data Crawler does not have a function to check downstream status and attempt to re-upload URLs that failed downstream.
    -   There is no easy way to determine which documents have been ingested by the Data Crawler. For example, if you run the Data Crawler against a set of 500 documents, the Data Crawler might report failures submitting 65 documents with a total collection of 212 documents. The status of the remaining 223 documents is undetermined.

        A workaround is available, but it is complicated and involves invoking the API directly. Contact {{site.data.keyword.IBM}} support for assistance.
-   The Java, Python, and Node.js SDKs for {{site.data.keyword.discoveryshort}} do not provide all of the functionality provided by the default REST (cURL) API. Not all cURL methods have an equivalent method in the non-cURL SDKs, and not all non-cURL methods provide all of the same features that their cURL equivalents have. In other words, the Java, Python, and Node.js SDKs currently provide only a subset of the cURL API's capabilities.
-   If you use the Word converter, matching on headings by using the `style` key is much more accurate and efficient than it by using the `level` key.
