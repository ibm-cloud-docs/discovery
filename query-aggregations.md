---

copyright:
  years: 2015, 2020
lastupdated: "2020-10-14"

subcollection: discovery

---

{{site.data.keyword.attribute-definition-list}}

# Query aggregations
{: #query-aggregations}

Aggregations return a set of data values. For the complete list of available aggregations, see the [Query reference](/docs/discovery?topic=discovery-query-reference#aggregations).

## term
{: #term}

Returns the top values (by score and by frequency) for the selected enrichments. All enrichments are valid values. You can optionally use `count` to specify the number of terms to return. The `count` parameter has a default value of 10. This example returns the full text and enrichments of the top values with the concept enrichment, and specifies to return 10 terms.

For example:
```bash
term(enriched_text.concepts.text,count:10)
```
{: codeblock}

## filter
{: #aggfilter}

A modifier that narrows the document set of the aggregation query it precedes. This example filters down to the set of documents that include the concept Cloud computing.

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

A specialized histogram that uses dates to create interval segments. Valid date interval values are `second/seconds` `minute/minutes`, `hour/hours`, `day/days`, `week/weeks`, `month/months`, and `year/years`. The syntax is `timeslice(<field>,<interval>,<time_zone>)`. To use `timeslice`, the time fields in your documents must be of the `date` data type and in [UNIX time](http://en.wikipedia.org/wiki/Unix_time){: external} format. Unless both of these requirements are met, the `timeslice` parameter does not work correctly. You can create a timeslice if your documents contain `date` fields with values such as `1496228512`. The value must be in a numeric format (for example, `float` or `double`) and not enclosed in quotation marks. The service treats dates in text and dates in ISO 8601 format as data type `string`, not as data type `date`. This example returns values for "sales" ("product.sales") at intervals of 2 days in the New York City time zone.

For example:
```bash
timeslice(product.sales,2day,America/New York)
```
{: codeblock}

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
