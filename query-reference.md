---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-31"

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

# Query building

The {{site.data.keyword.discoveryfull}} service offers powerful content search capabilities through queries. After your content is uploaded and enriched by the {{site.data.keyword.discoveryshort}} service, you can build queries, integrate {{site.data.keyword.discoveryshort}} into your own projects, or create a custom application by using the {{site.data.keyword.watson}} Explorer Application Builder. To get started with queries, see [Building queries and delivering content](/docs/services/discovery/using.html).
{: shortdesc}

## Parameter descriptions
{: #parameter-descriptions}

Query parameters enable you to search your collection, and customize the output of the data you return.

### Search parameters

- `filter`: A cacheable query that excludes any documents that don't mention the query content. Filter search results are **not** returned in order of relevance. (These queries are written using the {{site.data.keyword.discoveryshort}} Query Language.)
- `query`: A query search returns all documents in your data set with full enrichments and full text in order of relevance. A query also excludes any documents that don't mention the query content. (These queries are written using the {{site.data.keyword.discoveryshort}} Query Language.)
- `aggregation`: Aggregation queries return a count of documents matching a set of data values; for example, top keywords, overall sentiment of entities, and more. For the full list of aggregation options, see the [Aggregations table](/docs/services/discovery/query-reference.html#aggregations). (These queries are written using the {{site.data.keyword.discoveryshort}} Query Language.)
- `natural_language_query`: A natural language query enables you to perform queries expressed in natural language, as might be received from an end user in a conversational or free-text interface - for example: "IBM Watson in healthcare". The parameter uses the entire input as the query text. It does **not** recognize operators. The `natural_language_query` parameter enables capabilities such as passage search and relevancy training.

#### Difference between the filter and query parameters

If you test the same search term on a small data set, you might find that the `filter` and `query` parameters return very similar (if not identical) results. However, there is a difference between the two parameters.

- Using a filter parameter alone will return search results in no specific order.
- Using a query parameter alone will return search results in order of relevance.

In large data sets, if you need results returned in order of relevance, you should combine the `filter` and `query` parameters, because using them together will improve performance. This is because the `filter` parameter will run first and cache results, then the `query` parameter will rank them. For an example of using filters and queries together, see [Building combined queries](/docs/services/discovery/using.html#building-combined-queries). Filters can also be used in aggregations.

When you write a query that includes both a `filter`, and an `aggregation`, `query`, or `natural_language_query` parameter; the `filter` parameters run first, after which any `aggregation`, `query`, or `natural_language_query` parameters run in parallel.

With a simple query, especially on a small data set, `filter` and `query` often return the exact same (or similar) results. If a `filter` and `query` call return similar results, and getting a response in order of relevance does not matter, it is better to use filter because filter calls are faster and are cached. Caching means that the next time you make that call, you get a much quicker response, particularly in a big data set.

### Structure parameters

-  `count`: The number of documents that you want returned in the response. The default is `10`. The maximum for the `count` and `offset` values together in any one query is `10000`.
-  `offset`: The number of query results to skip at the beginning. For example, if the total number of results that are returned is 10, and the offset is 8, it returns the last two results. The default is `0`. The maximum for the `count` and `offset` values together in any one query is `10000`.
-  `return`: A comma-separated list of the portion of the document hierarchy to return. Any of the document hierarchy are valid values.
-  `sort`: A comma-separated list of fields in the document to sort on. You can optionally specify a sort direction by prefixing the field with `-` for descending order or `+` for ascending order. Ascending order is the default sort direction.

   The `sort` parameter is currently available for use only with the API; it is not available through the tooling.

-  `passages`: A boolean that specifies whether the service returns a set of the most relevant passages from the documents returned by a query that uses the `natural_language_query` parameter. The passages are generated by sophisticated Watson algorithms to determine the best passages of text from all of the documents returned by the query. The default is `false`.

    The `passages` parameter can only be used on private collections. It cannot be used on the {{site.data.keyword.discoverynewsfull}} collection.
    {: tip}

-  `passages.fields`: A comma-separated list of fields in the index that passages will be drawn from. If this parameter not specified then all top level field are included.

-  `passages.count`: The maximum number of passages to return. The search will return fewer if that is the total number found. The default is `10`. The maximum is `100`.

-  `passages.characters`: The approximate number of characters that any one passage should have. The default is `400`. The minimum is `50`. The maximum is `2000`.

   The `passages` parameter returns matching passages (`passage_text`), as well as the `score`, `document_id`, the name of the field the passage was extracted from (`field`), and the starting and ending characters of the passage text within the field (`start_offset` and `end_offset`), as shown in the following example from a collection about dogs. The query is shown at the top of the example.

   ```bash
    curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-06-25&natural_language_query='collie'&passages=true"
   ```
   {: pre}

   The JSON that is returned will be of the following format:

   ```json
    {
      "matching_results":2,
      "passages":[
        {
          "passage_text":">\n\n\n<h1>Dogs</h1>\n<p>Dogs are popular pets. Some notable breeds include German shepherds, collies, sharpeis, and beagles. Shepherds and collies bark. Sharpeis sharp. Beagles howl.</p>\n<h2>Collie</h2"
          "passage_score":15.230205287402338,
          "document_id":"ab7be56bcc9476493516b511169739f0",
          "start_offset":120
          "end_offset":300
          "field":"html"       
        },
        {
          "passage_text":">   \n</tr>\n<tr>\n  <td>Mandy</td>\n  <td>German shepherd/collie mix</td>\n  <td>7 years</td> \n  <td>Rat bite</td>   \n  <td>N/A</td>   \n</tr>\n<tr>\n  <td>Mindy</td>\n  <td>Border Collie/terrier mix</td>\n  <td>17"
          "passage_score":10.153470191601558,
          "document_id":"fbb5dcb4d8a6a29f572ebdeb6fbed20e",              
          "start_offset":70
          "end_offset":120
          "field":"html"
        },
     ...
   ```
   {: codeblock}                        

-  `highlight`: A boolean that specifies whether the returned output includes a `highlight` object in which the keys are field names and the values are arrays that contain segments of query-matching text highlighted by the HTML `*` tag.

    The output lists the `highlight` object after the `enriched_text` object, as shown in the following example.

```bash
curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-06-25&natural_language_query=beagle&highlight=true"
```
{: pre}

The JSON that is returned will be of the following format:

```json
{
  "matching_results":4,
  "results":[
    {
      "id":"ce78aba1288151fe5dc391cb480e9f98",
      "score":1.212413,
      "extracted_metadata":{
        "title":"Liam and pets",
        "sha1":"9a617d49dde77019dc324666767bf08cfd7f30f8",
        "filename":"disco-Liam.html20170718-10-ki3l59.html",
        "file_type":"html"
      },
  ...
      "highlight":{
        "enriched_text.relations.sentence":[
          " He would very much like to get a *beagle*.",
          " Getting a *beagle* would make Liam happy."
        ],
        "enriched_text.relations.subject.keywords.text":[
          "*beagle*"
        ],
        "enriched_text.relations.subject.text":[
          "a *beagle*"
        ],
        "text":[
          "Liam and pets\n\nLiam\n\nLiam does not currently have a pet of his own. He would very much like to get a *beagle*. Getting a *beagle* would make Liam happy."
        ],
        "enriched_text.relations.object.keywords.text":[
          "*beagle*"
        ],
        "enriched_text.keywords.text":[
          "*beagle*"
        ],
        "enriched_text.relations.object.text":[
          "a *beagle*"
        ],
        "html":[
          "</h1>\n<p>Liam does not currently have a pet of his own. He would very much like to get a *beagle*",
          ". Getting a *beagle* would make Liam happy.\n\n</p></body></html>"
        ]
      }
    },
 ...
```
{: codeblock}

## Operators
{: #operators}

Operators are the separators between different parts of a query. These are the available operators:

| Operator | Description | Example |
|:-------------------:|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------|
| `.` | This delimiter separates the levels of hierarchy in the JSON schema | `enriched_text.concepts.text` |
| `:` | This marker specifies a match for the query term. | `enriched_text.concepts.text:cloud computing` |
| `::` | This marker specifies an exact match for the query term. | `enriched_text.concepts.text::cloud computing` |
| `:!` | This marker specifies that the results do not contain a match for the query term | `enriched_text.concepts.text:!cloud computing` |
| `::!` | This marker specifies that the results do not exactly match the query term | `enriched_text.concepts.text::!cloud computing` |
| `\` | Escape character for queries that require the ability to query terms by using string literals that contain control characters. | `enriched_text.concepts.text:\!cloud computing` |
| `"IBM Watson"` | All contents of a phrase query are processed as escaped. So no special characters within a phrase query are parsed, except for double quotes (`"`) inside a phrase query, which must be escaped (`\"`). Use phrase queries with full-text, rank-based queries, and not with boolean filter operations. **Note**: single quotes (`'`) are not supported.) | `enriched_text.concepts.text:"IBM watson"` |
| `~ + Number` | The number of one character changes that need to be made to one string to make it the same as another string. For example `car~1` will match `car`,`cap`,`cat`,`can`, etc.. | `query-enriched_text.concepts.text:Watson~3` |
| `(), []` | Logical groupings can be formed to specify more specific information. | `filter-entities:(text:IBM,type:Company)` |
| <code>&#124;</code> | Boolean operator for "or". | <code>query-enriched.entities.text:Google&#124;IBM</code> |
| `,` | Boolean operator for "and". | `query-enriched.entities.text:Google,IBM` |
| `<=, >=, >, <` | Creates numerical comparisons of less than or equal to, greater than or equal to, greater than, and less than. |       |
| `^multiplier` | Increases the score value of a search term. | `query-enriched_text.concepts.text:IBM^3` |
| `*` | Matches unknown characters in a search expression. | `query-enriched_text.concepts.text:IBM*` |

## Aggregations
{: #aggregations}

Aggregations return a set of data values. These are the available aggregations:

| Aggregations | Description | Example |
|:------------:|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| `term` | Returns the top values (by score and by frequency) for the selected enrichments. All enrichments are valid values. You can optionally use `count` to specify the number of terms to return. This example returns the full text and enrichments of the top values with the concept enrichment, and specifies to return 10 terms. | `term(enriched_text.concepts.text,count:10)` |
| `filter` | A modifier that will narrow down the document set of the aggregation query it precedes. This example filters down to the set of documents that include the concept Cloud computing. | `filter(enriched_text.concepts.text:cloud computing)`
| `nested` | Applying nested before an aggregation query restricts the aggregation to the area of the results specified. For example: `nested(enriched_text.entities)` means that only the `enriched_text.entities` components of any result are used to aggregate against.| `nested(enriched_text.entities)` |
| `histogram` | Creates numeric interval segments to categorize documents. Uses field values from a single numeric field to describe the category. The field used to create the histogram must be of number (`integer`, `float`, `double`, or `date`) type. Non number types such as `string` are not supported. For example, "price": 1.30 is a number value that works, and "price": "1.30" is a string, so it wouldn’t work. Use the `interval` argument to define the size of the sections the results are split into. Interval values must be whole, non-negative numbers, and are set to make sense for segmenting your possible field values. For example, if your data set includes the price of several items, like: “price”: 1.30, “price”: 1.99, and “price”: 2.99, you might use intervals of 1, so that you see everything grouped between 1 and 2, and 2 and 3. You would probably not use an interval of 100, because then all the data would end up in the same segment. Histograms can process decimal values, but intervals have to be whole numbers. The syntax is `histogram(<field>,<interval>)`, as shown in the following example. | `histogram(product.price,interval:1)` |
| `timeslice` | A specialized histogram that uses dates to create interval segments. Valid date interval values are `minute`, `hour`, `day`, `week`, `month`, and `year`. The syntax is `timeslice(<field>,<interval>,<time_zone>)`. To use `timeslice`, the time fields in your documents must be of the `date` data type and in [UNIX time ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://en.wikipedia.org/wiki/Unix_time){: new_window} format. Unless both of these requirements are met, the `timeslice` parameter does not work correctly. You can create a timeslice if your documents contain `date` fields with values such as `1496228512`. The value must be in a numeric format (for example, `float` or `double`) and not enclosed in quotation marks. The service treats dates in text and dates in ISO 8601 format as data type `string`, not as data type `date`. You can detect anomalous points in timeslice aggregations. See [Timeslice anomaly detection](#anomaly-detection) for additional information. This example returns values for "sales" ("product.sales") at intervals of 2 days in the New York City time zone.| `timeslice(product.sales,2day,America/New York)` |
| `top_hits` | Returns the documents ranked by the score of the query or enrichment. Can be used with any query parameter or aggregation. This example returns the 10 top hits for a term aggregation. | `term(enriched_text.concepts.text).top_hits(10)` |
| `max` | Returns the highest value in the specified field across all matching documents. | `max(product.price)` |
| `min` | Returns the lowest value in the specified field across all matching documents. | `min(product.price)` |
| `average` | Returns the mean of values of the specified field across all matching documents. | `average(product.price)` |
| `sum` | Adds together the values of the specified field across all matching documents. | `sum(product.price)` |

### Timeslice anomaly detection
{: #anomaly-detection}

You can optionally apply anomaly detection to the results of a `timeslice` aggregation. Anomaly detection is used to locate unusual datapoints within a time series and to flag them for further review. Example uses for anomaly detection include identifying spikes in credit-card usage and searching Watson Discovery News for clusters of articles regarding a particular topic.

To apply anomaly detection, use the following syntax in your aggregation:

```
timeslice(field:<date>,interval:<interval>,anomaly:true)`
```
{: codeblock}

If you specify `anomaly:true` with the `timeslice` aggregation, the output includes the following two additional fields, which are shown in the example.

  - `"anomaly": true` to indicate that anomaly detection was performed
  - An `anomaly` field in the points that are anomalous in the output's results array. The anomaly field has a value of the `float` data type indicating the magnitude of the anomalous behavior. The closer the value of the anomaly field is to `1`, the more likely the result is anomalous.

  - The `key` and `key_as_string` in each of the objects in the `results` array corresponds to a UNIX timestamp in seconds.
  - The anomaly score is relative to a query, not across queries.

```json
"type": "timeslice",
"field": "blekko.chrondate",
"interval": "1d",
"anomaly": true,
"results": [
  {
    "matching_results": 2933,
    "anomaly": 1,
    "key_as_string": "1496880000",
    "key": 1496880000000
  },
  {
    "matching_results": 3435,
    "anomaly": 1,
    "key_as_string": "1496966400",
    "key": 1496966400000
  },
  {
    "matching_results": 3692,
    "anomaly": 0.598226,
    "key_as_string": "1496016000",
    "key": 1496016000000
  },
  {
    "matching_results": 4551,
    "anomaly": 0.828498,
    "key_as_string": "1495411200",
    "key": 1495411200000
  },
  {
    "matching_results": 947,
    "key_as_string": "1489968000",
    "key": 1489968000000
  },
 ...
]
...
```
{: codeblock}

#### Limitations of anomaly detection

- Anomaly detection is currently available only on top-level `timeslice` aggregations. It is not available in lower-level (nested) aggregations.
- The maximum number of points that can be processed by anomaly detection in any given `timeslice` aggregation is `1500`.
- The maximum number of top-level timeslice aggregations that can be processed by anomaly detection is `20`.

<!--
#### Anomaly detection workflow

The following example workflow detects an anomaly for the text entity `London` and retrieves additional information about the anomalous datapoint.

  1. Timeslice aggregation: `query=entities.text:London&count=0&aggregation=timeslice(blekko.last_crawled,1day,anomaly:true)`
  1. Term aggregation to retrieve top keywords: `query=entities.text:London&count=0&aggregation=term(keywords.text,count:5)&filter=blekko.last_crawled>=1490140800,<=1490227200`
  1. Query to retrieve top enriched title: `query=entities.text:London,keywords.text:Westminster Bridge|police officer|people|Prime Minister Theresa|parliament&count=1&filter=blekko.last_crawled>=1490140800,<=1490227200&return=enrichedTitle.text`
  -->
