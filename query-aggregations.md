---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-09"

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

# Query aggregations
{: #query-aggregations}

Aggregations return a set of data values. For the complete list of available aggregations, see the [Query reference](/docs/services/discovery/query-reference.html#aggregations).

## term
{: #term}

Returns the top values (by score and by frequency) for the selected enrichments. All enrichments are valid values. You can optionally use `count` to specify the number of terms to return. The `count` parameter has a default value of 10. This example returns the full text and enrichments of the top values with the concept enrichment, and specifies to return 10 terms.

For example:
```bash
term(enriched_text.concepts.text,count:10)
```
{: codeblock}

## filter
{: #filter}

A modifier that will narrow down the document set of the aggregation query it precedes. This example filters down to the set of documents that include the concept Cloud computing.

For example:
```bash
filter(enriched_text.concepts.text:"cloud computing")
```
{: codeblock}

## nested
{: #nested}

Applying nested before an aggregation query restricts the aggregation to the area of the results specified. For example: `nested(enriched_text.entities)` means that only the `enriched_text.entities` components of any result are used to aggregate against.

For example:
```bash
nested(enriched_text.entities)
```
{: codeblock}

## histogram
{: #histogram}

Creates numeric interval segments to categorize documents. Uses field values from a single numeric field to describe the category. The field used to create the histogram must be of number (`integer`, `float`, `double`, or `date`) type. Non-number types such as `string` are not supported. For example, "price": 1.30 is a number value that works, and "price": "1.30" is a string, so it wouldn’t work. Use the `interval` argument to define the size of the sections the results are split into. Interval values must be whole, non-negative numbers, and are set to make sense for segmenting your possible field values. For example, if your data set includes the price of several items, like: “price”: 1.30, “price”: 1.99, and “price”: 2.99, you might use intervals of 1, so that you see everything grouped between 1 and 2, and 2 and 3. You would probably not use an interval of 100, because then all the data would end up in the same segment. Histograms can process decimal values, but intervals have to be whole numbers. The syntax is `histogram(<field>,<interval>)`, as shown in the following example.

For example:
```bash
histogram(product.price,interval:1)
```
{: codeblock}

## timeslice
{: #timeslice}

A specialized histogram that uses dates to create interval segments. Valid date interval values are `second/seconds` `minute/minutes`, `hour/hours`, `day/days`, `week/weeks`, `month/months`, and `year/years`. The syntax is `timeslice(<field>,<interval>,<time_zone>)`. To use `timeslice`, the time fields in your documents must be of the `date` data type and in [UNIX time ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://en.wikipedia.org/wiki/Unix_time){: new_window} format. Unless both of these requirements are met, the `timeslice` parameter does not work correctly. You can create a timeslice if your documents contain `date` fields with values such as `1496228512`. The value must be in a numeric format (for example, `float` or `double`) and not enclosed in quotation marks. The service treats dates in text and dates in ISO 8601 format as data type `string`, not as data type `date`. You can detect anomalous points in timeslice aggregations. See [Timeslice anomaly detection](#anomaly-detection) for additional information. This example returns values for "sales" ("product.sales") at intervals of 2 days in the New York City time zone.

For example:
```bash
timeslice(product.sales,2day,America/New York)
```
{: codeblock}

### Timeslice anomaly detection
{: #anomaly-detection}

You can optionally apply anomaly detection to the results of a `timeslice` aggregation. Anomaly detection is used to locate unusual datapoints within a time series and to flag them for further review. Example uses for anomaly detection include identifying spikes in credit-card usage and searching Watson Discovery News for clusters of articles regarding a particular topic.

To apply anomaly detection, use the following syntax in your aggregation:

```bash
timeslice(field:<date>,interval:<interval>,anomaly:true)`
```
{: codeblock}

If you specify `anomaly:true` with the `timeslice` aggregation, the output includes the following two additional fields, which are shown in the example.

  - `"anomaly": true` to indicate that anomaly detection was performed
  - An `anomaly` field in the points that are anomalous in the output's results array. The anomaly field has a value of the `float` data type indicating the magnitude of the anomalous behavior. The closer the value of the anomaly field is to `1`, the more likely the result is anomalous.

  - The `key` and `key_as_string` in each of the objects in the `results` array corresponds to a UNIX timestamp in seconds.
  - The anomaly score is relative to the original query only.

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

## top_hits
{: #top_hits}

Returns the documents ranked by the score of the query or enrichment. Can be used with any query parameter or aggregation. This example returns the 10 top hits for a term aggregation.

For example:
```bash
term(enriched_text.concepts.text).top_hits(10)
```
{: codeblock}

## unique_count
{: #unique_count}

Returns a count of the unique instances of the specified field in the collection.

Examples:
```bash
unique_count(enriched_text.keyword.text)
```
{: codeblock}

```bash
nested(enriched_text.entities).term(enriched_text.entities.text,count:3).unique_count(enriched_text.entities.type)
```
{: codeblock}

## max
{: #max}

Returns the highest value in the specified field across all matching documents.

For example:
```bash
max(product.price)
```
{: codeblock}

## min
{: #min}

Returns the lowest value in the specified field across all matching documents.

For example:
```bash
min(product.price)
```
{: codeblock}

## average
{: #average}

Returns the mean of values of the specified field across all matching documents.

For example:
```bash
average(product.price)
```
{: codeblock}

## sum
{: #sum}

Adds together the values of the specified field across all matching documents.

For example:
```bash
sum(product.price)
```
{: codeblock}
