---

copyright:
years: 2018, 2019
lastupdated: "2019-01-15"

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

# 了解输出模式
{: #output_schema}

使用“元素分类”摄入文档后，服务会针对版本日期 `2018-10-15` 或更新日期提供以下模式的 JSON 输出。输出将包含在 `enriched_html_elements` 对象中。 

```json
{
  "document": {
          "title": string,
    "html": string,
    "hash": string
  },
  "model_id" : string,
  "model_version" : string,  
  "elements": [
    {
      "location": { 
        "begin": int,
        "end": int
      },
      "text": string,
      "types": [
        {
          "label": { "nature": string, "party": string },
          "provenance_ids": [string, string, ...]
            ...
          ]
        }
        ...
      ],
      "categories": [
        {
          "label": string,
          "provenance_ids": [string, string, ...]
        }
        ...
      ],
      "attributes": [
        {
      	  "type": string,
          "text": string,
          "location": { "begin": int, "end": int }
         }
      ]
    }
    ...
  ],
  "tables": [
    {
      "location" : {
        "begin" : int,
        "end" : int
      },
      "text": string,
      "section_title": {
        "text": string,
        "location": {
          "begin" : int,
          "end" : int
        }
      },
      "table_headers" : [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int
        },
        ...
      ],
      "column_headers" : [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "text_normalized" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int
        },
        ...
      ],
      "row_headers" : [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "text_normalized" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int
        },
        ...
      ],
      "body_cells" : [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int,
          "row_header_ids": [ string ],
          "row_header_texts": [ string ],
          "row_header_texts_normalized": [ string ],
          "column_header_ids": [ string ],
          "column_header_texts": [ string ],
          "column_header_texts_normalized": [ string ],
          "attributes" : [
             {
               "type" : string,
               "text" : string,
               "location" : {
                 "begin" : int,
          "end" : int
        }
      },
             ...
           ]
        },
        ...
      ]
    },
    ...
  ],
  "document_structure": {
    "section_titles": [
      {
        "text": string,
        "location": {
          "begin": int,
          "end": int
        },
        "level": int,
        "element_locations": [
          {
            "begin": int,
            "end": int
          },
          ...
        ]
      },
      ...
    ],
    "leading_sentences": [
      {
        "text": string,
        "location": {
          "begin": int,
          "end": int
        },
        "element_locations": [
          {
            "begin": int,
            "end": int
          },
          ...
        ]
      },
      ...
    ]
  },
  "parties": [
    {
      "party": string,
      "role": string,
      "importance": string,
      "addresses": [
        {
          "text": string,
          "location": {
            "begin": int,
            "end": int
          }
        },
        ...
      ],
      "contacts": [
        {
          "name": string,
          "role": string 
        },
        ...
      ]
    },
    ...
  ],
  "effective_dates": [
    {
      "text": string,
      "confidence_level": string,
      "location": { "begin": int, "end": int }
     },
     ...
  ],
  "contract_amounts": [
    {
      "text": string,
      "confidence_level": string,      
      "location": { "begin": int, "end": int }
    },
    ...
  ],
  "termination_dates": [
    {
      "text": string,
      "confidence_level": string,      
      "location": { "begin": int, "end": int }
    },
    ...
  ]
}
```
{: codeblock}

该模式的布局如下所示。

  - `document`：一个对象，用于列出有关文档的基本信息，包括：
    - `title`：文档标题（如果被检测到）。
    - `html`: HTML 格式的输入文档的完整文本。
    - `hash`：输入文档的 MD5 散列。
  - `model_id`：服务将使用的分析模型。对于 `/v1/element_classification` 和 `/v1/comparison` 方法，缺省值为 `contracts`。对于 `/v1/tables` 方法，缺省值为 `tables`。这些缺省值适用于独立方法以及这些方法在批处理请求中的使用。
  - `model_version`：由 `model_id` 参数值指定的分析模型的版本。
  - `elements`：服务所检测到的文档元素的数组。
    - `location`：元素的位置，由其 `begin` 和 `end` 下标来定义。
    - `text`：元素的文本。
    - `types`：一个数组，用于描述元素的定义及其影响的对象。
      - `label`：一个对象，用于通过使用以下一对元素来定义类型：
        - `nature`：语句所需的操作的类型。当前值为 `Definition`、`Disclaimer`、`Exclusion`、`Obligation` 和 `Right`。
        - `party`：一个字符串，用于标识语句所适用的当事方。
      - `provenance_ids`：一个或多个散列值的数组，您可以将这些散列值发送给 IBM 来提供反馈或获取支持。
    - `categories`：一个数组，用于列出元素所属的功能类别；换句话说，就是元素的主题。
      - `label`：一个字符串，用于列出所识别到的类别。您可以在[了解合同解析](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing)中找到[类别](/docs/services/discovery?topic=discovery-contract_parsing#contract_categories)列表。
      - `provenance_ids`：一个或多个散列值的数组，您可以将这些散列值发送给 IBM 来提供反馈或获取支持。
    - `attributes`：一个数组，用于标识文档属性。数组中的每个对象都包含以下三个元素：
      - `type`：属性的类型。可能的值为 `Address`、`Currency`、`DateTime`、`Location`、`Organization` 和 `Person`。
      - `text`：与属性相关联的文本。
      - `location`：属性的位置，由其 `begin` 和 `end` 下标来定义。
  - `tables`\*：一个数组，用于定义在输入文档中识别到的表。
    - `location`：输入文档中当前表的位置，由其 `begin` 和 `end` 下标来定义。
    - `text`：输入文档中当前表的文本内容，没有关联的标记内容。
    - `section_title`：如果被识别到，那么表示包含当前表中包含的某个节标题的位置。如果未识别到任何节标题，那么为空。
      - `text`：所识别到的节标题的文本。
      - `location`：输入文档中节标题的位置，由其 `begin` 和 `end` 下标来定义。
    - `table_headers`：一个表级别单元格数组，其中每个单元格都可用作当前表中所有其他单元格的标题。每个表头都由以下元素的集合来定义：
      - `cell_id`：格式为 `tableHeader-x-y` 的字符串值，其中 `x` 和 `y` 是原始输入文档中单元格值的开始和结束偏移量。
      - `location`：输入文档中单元格的位置，由其 `begin` 和 `end` 下标来定义。
      - `text`：输入文档中单元格的文本内容，没有关联的标记内容。
      - `row_index_begin`：当前表中此单元格的 `row` 位置的 `begin` 索引。
      - `row_index_end`：当前表中此单元格的 `row` 位置的 `end` 索引。
      - `column_index_begin`：当前表中此单元格的 `column` 位置的 `begin` 索引。
      - `column_index_end`：当前表中此单元格的 `column` 位置的 `end` 索引。
    - `column_headers`：当前表中列级别单元格的数组，其中每个单元格都可用作同一列中其他单元格的标题。每个列标题定义为以下各项的集合：
      - `cell_id`：格式为 `columnHeader-x-y` 的字符串值，其中 `x` 和 `y` 是输入文档中此列标题单元格的开始和结束偏移量。
      - `location`：输入文档中单元格的位置，由其 `begin` 和 `end` 下标来定义。
      - `text`：输入文档中单元格的文本内容，没有关联的标记内容。
      - `text_normalized`：如果提供了定制输入，那么为根据定制规范化的单元格文本；否则，将使用与 `text` 相同的值。 
      - `row_index_begin`：当前表中此单元格的 `row` 位置的 `begin` 索引。
      - `row_index_end`：当前表中此单元格的 `row` 位置的 `end` 索引。
      - `column_index_begin`：当前表中此单元格的 `column` 位置的 `begin` 索引。
      - `column_index_end`：当前表中此单元格的 `column` 位置的 `end` 索引。
    - `row_headers`：当前表中行级别单元格的数组，其中每个单元格都可用作同一行中其他单元格的标题。每个行标题定义为以下各项的集合：
      - `cell_id`：格式为 `rowHeader-x-y` 的字符串值，其中 `x` 和 `y` 是输入文档中此行标题单元格的开始和结束偏移量。
      - `location`：输入文档中单元格的位置，由其 `begin` 和 `end` 下标来定义。
      - `text`：输入文档中单元格的文本内容，没有关联的标记内容。
      - `text_normalized`：如果提供了定制输入，那么为根据定制规范化的单元格文本；否则，将使用与 `text` 相同的值。 
      - `row_index_begin`：当前表中此单元格的 `row` 位置的 `begin` 索引。
      - `row_index_end`：当前表中此单元格的 `row` 位置的 `end` 索引。
      - `column_index_begin`：当前表中此单元格的 `column` 位置的 `begin` 索引。
      - `column_index_end`：当前表中此单元格的 `column` 位置的 `end` 索引。
    - `body_cells`：一个单元格数组，这些单元格不是当前表的表头、列标题或行标题单元格，但与行标题和列标题具有相应的关联。每个正文单元格定义为以下各项的集合：
      - `cell_id`：格式为 `bodyCell-x-y` 的字符串值，其中 `x` 和 `y` 是输入文档中此正文单元格的开始和结束偏移量。
      - `location`：输入文档中单元格的位置，由其 `begin` 和 `end` 下标来定义。
      - `text`：输入文档中单元格的文本内容，没有关联的标记内容。
      - `row_index_begin`：当前表中此单元格的 `row` 位置的 `begin` 索引。
      - `row_index_end`：当前表中此单元格的 `row` 位置的 `end` 索引。
      - `column_index_begin`：当前表中此单元格的 `column` 位置的 `begin` 索引。
      - `column_index_end`：当前表中此单元格的 `column` 位置的 `end` 索引。
      - `row_header_ids`：一个值数组，其中每个值都是适用于此正文单元格的行标题的 `cell_id` 值。
      - `row_header_texts`：一个值数组，其中每个值都是适用于此正文单元格的行标题的 `text` 值。
      - `row_header_texts_normalized`：如果提供了定制输入，那么为根据定制规范化的行标题文本；否则，将使用与 `row_header_texts` 相同的值。 
      - `column_header_ids`：一个值数组，其中每个值都是适用于此正文单元格的列标题的 `cell_id` 值。
      - `column_header_texts`：一个值数组，其中每个值都是适用于此正文单元格的列标题的 `text` 值。
      - `column_header_texts_normalized`：如果提供了定制输入，那么为根据定制规范化的列标题文本；否则，将使用与 `column_header_texts` 相同的值。
      - `attributes`：一个数组，用于标识文档属性。数组中的每个对象都包含以下三个元素：
        - `type`：属性的类型。可能的值为 `Address`、`Currency`、`DateTime`、`Location`、`Organization` 和 `Person`。
        - `text`：与属性相关联的文本。
        - `location`：属性的位置，由其 `begin` 和 `end` 下标来定义。
  - `document_structure`：一个对象，用于描述输入文档的结构。
    - `section_titles`：一个数组，其中针对输入文档中检测到的每个节或子节包含一个对象。节和子节不是按嵌套方式排列的，而是按平铺方式排列的。您可以使用元素的 `begin` 和 `end` 值以及节的 `level` 值，将其重新按顺序排列。
      - `text`：一个字符串，用于列出节标题（如果被检测到）。
      - `location`：输入文档中标题的位置，由其 `begin` 和 `end` 下标来定义。
      - `level`：一个整数，用于指示节在输入文档中所处的级别。例如，可表示顶级节，或表示某级别节内的子节。
      - `element_locations`：一个数组，用于指定节中语句的 `begin` 和 `end` 值。
    - `leading_sentences`：与 `section_titles` 数组平行的数组，其中针对每个节或子节包含一个对象，用于详细描述匹配节或子节中的主题句。与 `section_titles` 数组一样，其中的对象不是按嵌套方式排列的；而是按平铺方式排列的。您可以使用输入文档中元素的 `begin` 和 `end` 值或任何级别标记，重新按顺序排列这些对象。
      - `text`：一个字符串，用于列出主题句（如果被检测到）。
      - `location`：输入文档中主题句的位置，由其 `begin` 和 `end` 下标来定义。
      - `element_locations`：一个数组，用于指定节中主题句的 `begin` 和 `end` 值。
  - `parties`：一个数组，用于定义服务所识别到的当事方。
    - `party`：一个字符串值，用于标识当事方。
    - `role`：一个字符串值，用于标识当事方的角色。
    - `importance`：一个字符串值，用于标识当事方的重要性。可能的值包括 `Primary`（主要当事方）和 `Unknown`（非主要当事方）。
    - `addresses`：一个对象数组，这些对象用于标识地址。
      - `text`：一个包含地址的字符串。
      - `location`：地址的位置，由其 `begin` 和 `end` 下标来定义。
    - `contacts`：一个数组，用于定义输入文档中所识别到的联系人的姓名和角色。
      - `name`：一个字符串，用于列出所识别到的联系人的姓名。
      - `role`：一个字符串，用于列出所识别到的联系人的角色。  
  - `effective_dates`：一个数组，用于标识文档的生效日期。
    - `text`：生效日期，以字符串形式列出。
    - `confidence_level`：所识别生效日期的置信度级别。可能的值包括 `High`、`Medium` 和 `Low`。
    - `location`：日期的位置，由其 `begin` 和 `end` 下标来定义。
  - `contract_amounts`：一个数组，用于标识在文档中识别到的货币金额。
    - `text`：合同金额，以字符串形式列出。
    - `confidence_level`：所识别合同金额的置信度级别。可能的值包括 `High`、`Medium` 和 `Low`。    
    - `location`：金额的位置，由其 `begin` 和 `end` 下标来定义。
  - `termination_dates`：一个数组，用于识别文档的终止日期。
    - `text`：终止日期，以字符串形式列出。
    - `confidence_level`：所识别终止日期的置信度级别。可能的值包括 `High`、`Medium` 和 `Low`。    
    - `location`：日期的位置，由其 `begin` 和 `end` 下标来定义。

**\* 有关表的说明：**
  - 每个单元格的行和列索引值都是从零开始的，因此起始值为 `0`。
  - `row_header_ids` 和 `row_header_texts` 元素数组中的多个值表示行标题的可能层次结构。
  - `column_header_ids` 和 `column_header_texts` 元素数组中的多个值表示列标题的可能层次结构。
