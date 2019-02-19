---

copyright:
years: 2018
lastupdated: "2018-10-23"

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

# 了解输出模式
{: #output_schema}

使用“元素分类”摄入文档后，对于日期为 `2018-10-15` 的版本或更高版本，服务会使用以下模式来提供 JSON 输出。输出将包含在 `enriched_html_elements` 对象中。 

```
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
          "column_header_texts_normalized": [ string ]
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
        "level": int
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
      "location": { "begin": int, "end": int }
     },
     ...
  ],
  "contract_amounts": [
    {
      "text": string,
      "location": { "begin": int, "end": int }
    },
    ...
  ]
}
```

该模式的布局如下所示。

  - `document`：一个对象，用于列出有关文档的基本信息，包括：
    - `title`：文档标题（如果检测到）。
    - `html`: HTML 格式的输入文档的完整文本。
    - `hash`：输入文档的 MD5 散列。
  - `model_id`：要用于对文档进行分类的分析模型。缺省值为 `contracts`。 
  - `model_version`：由 `model_id` 参数值指定的分析模型的版本。
  - `elements`：服务检测到的文档元素的数组。
    - `location`：元素的位置，由其 `begin` 和 `end` 索引来定义。
    - `text`：元素的文本。
    - `types`：一个数组，用于描述元素的定义及元素影响的对象。
      - `label`：一个对象，用于通过以下一对元素来定义类型：
        - `nature`：语句需要的操作的类型。当前值为 `Definition`、`Disclaimer`、`Exclusion`、`Obligation` 和 `Right`。
        - `party`：一个字符串，用于标识语句所适用的当事方。
      - `provenance_ids`：一个或多个散列值的数组，您可以将这些散列值发送给 IBM 以提供反馈或接收支持。
    - `categories`：一个数组，用于列出元素所属的功能类别；换句话说，就是元素的主题。
      - `label`：一个字符串，用于列出识别到的类别。您可以在[了解合同解析](/docs/services/discovery/parsing.html#contract_parsing)中找到[类别](/docs/services/discovery/parsing.html#contract_categories)列表。
      - `provenance_ids`：一个或多个散列值的数组，您可以将这些散列值发送给 IBM 以提供反馈或接收支持。
    - `attributes`：一个数组，用于标识文档属性。数组中的每个对象包含以下三个元素：
      - `type`：属性的类型。可能的值为 `Location`、`DateTime` 和 `Currency`。
      - `text`：与属性相关联的文本。
      - `location`：属性的位置，由其 `begin` 和 `end` 索引来定义。
  - `tables`\*：一个数组，用于定义在输入文档中识别到的表。
    - `location`：当前表的位置，由其在输入文档中的 `begin` 和 `end` 索引来定义。
    - `text`：输入文档中当前表的文本内容，没有关联的标记内容。
    - `section_title`：如果识别到节标题，那么为包含当前表的节标题的位置。如果未识别到节标题，那么为空。
      - `text`：识别到的节标题的文本。
      - `location`：节标题在输入文档中的位置，由其 `begin` 和 `end` 索引来定义。
    - `table_headers`：一个表级别单元格数组，其中每个单元格可用作当前表的所有其他单元格的标题。每个表头都由以下内容的集合来定义：
      - `cell_id`：格式为 `tableHeader-x-y` 的字符串值，其中 `x` 和 `y` 是原始输入文档中单元格值的 begin 和 end 偏移量。
      - `location`：单元格在输入文档中的位置，由其 `begin` 和 `end` 索引来定义。
      - `text`：输入文档中单元格的文本内容，没有关联的标记内容。
      - `row_index_begin`：当前表中此单元格的 `row` 位置的 `begin` 索引。
      - `row_index_end`：当前表中此单元格的 `row` 位置的 `end` 索引。
      - `column_index_begin`：当前表中此单元格的 `column` 位置的 `begin` 索引。
      - `column_index_end`：当前表中此单元格的 `column` 位置的 `end` 索引。
    - `column_headers`：当前表中列级别单元格的数组，其中每个单元格都可用作同一列中其他单元格的标题。每个列标题都由以下内容的集合来定义：
      - `cell_id`：格式为 `columnHeader-x-y` 的字符串值，其中 `x` 和 `y` 是输入文档中此列标题单元格的 begin 和 end 偏移量。
      - `location`：单元格在输入文档中的位置，由其 `begin` 和 `end` 索引来定义。
      - `text`：输入文档中单元格的文本内容，没有关联的标记内容。
      - `text_normalized`：如果提供了定制输入，那么为根据定制设置的单元格文本规范化版本；否则，将使用与 `text` 相同的值。 
      - `row_index_begin`：当前表中此单元格的 `row` 位置的 `begin` 索引。
      - `row_index_end`：当前表中此单元格的 `row` 位置的 `end` 索引。
      - `column_index_begin`：当前表中此单元格的 `column` 位置的 `begin` 索引。
      - `column_index_end`：当前表中此单元格的 `column` 位置的 `end` 索引。
    - `row_headers`：当前表中行级单元格的数组，其中每个单元格都可用作同一行中其他单元格的标题。每个行标题都由以下内容的集合来定义：
      - `cell_id`：格式为 `rowHeader-x-y` 的字符串值，其中 `x` 和 `y` 是输入文档中此行标题单元格的 begin 和 end 偏移量。
      - `location`：单元格在输入文档中的位置，由其 `begin` 和 `end` 索引来定义。
      - `text`：输入文档中单元格的文本内容，没有关联的标记内容。
      - `text_normalized`：如果提供了定制输入，那么为根据定制设置的单元格文本规范化版本；否则，将使用与 `text` 相同的值。 
      - `row_index_begin`：当前表中此单元格的 `row` 位置的 `begin` 索引。
      - `row_index_end`：当前表中此单元格的 `row` 位置的 `end` 索引。
      - `column_index_begin`：当前表中此单元格的 `column` 位置的 `begin` 索引。
      - `column_index_end`：当前表中此单元格的 `column` 位置的 `end` 索引。
    - `body_cells`：一个单元格数组，这些单元格既不是当前表的表头，也不是列标题，也不是行标题，但与行标题和列标题具有相应的关联。每个正文单元格都由以下内容的集合来定义：
      - `cell_id`：格式为 `bodyCell-x-y` 的字符串值，其中 `x` 和 `y` 是输入文档中此正文单元格的 begin 和 end 偏移量。
      - `location`：单元格在输入文档中的位置，由其 `begin` 和 `end` 索引来定义。
      - `text`：输入文档中单元格的文本内容，没有关联的标记内容。
      - `row_index_begin`：当前表中此单元格的 `row` 位置的 `begin` 索引。
      - `row_index_end`：当前表中此单元格的 `row` 位置的 `end` 索引。
      - `column_index_begin`：当前表中此单元格的 `column` 位置的 `begin` 索引。
      - `column_index_end`：当前表中此单元格的 `column` 位置的 `end` 索引。
      - `row_header_ids`：一个值数组，其中每个值都是适用于此正文单元格的行标题的 `cell_id` 值。
      - `row_header_texts`：一个值数组，其中每个值都是适用于此正文单元格的行标题的 `text` 值。
      - `row_header_texts_normalized`：如果提供了定制输入，那么为根据定制设置的行标题文本规范化版本；否则，将使用与 `row_header_texts` 相同的值。 
      - `column_header_ids`：一个值数组，其中每个值都是适用于此正文单元格的列标题的 `cell_id` 值。
      - `column_header_texts`：一个值数组，其中每个值都是适用于此正文单元格的列标题的 `text` 值。
      - `column_header_texts_normalized`：如果提供了定制输入，那么为根据定制设置的列标题文本规范化版本；否则，将使用与 `column_header_texts` 相同的值。
  - `document_structure`：一个对象，用于描述输入文档的结构。
    - `section_titles`：一个数组，用于包含在输入文档中检测到的每个节或子节的一个对象。不会对节和子节进行嵌套；而是会对其进行序列化，并且可以使用元素的 `begin` 和 `end` 值以及节的 `level` 值使其恢复正常顺序。
      - `text`：一个字符串，用于列出节标题（如果检测到）。
      - `location`：标题在输入文档中的位置，由其 `begin` 和 `end` 索引来定义。
      - `level`：一个整数，用于指示节在输入文档中所处的级别。例如，`1` 表示顶级节，`2` 表示级别为 `1` 的节内的子节，依此类推。
      - `element_locations`：一个数组，用于包含指定节中语句的 `begin` 和 `end` 值的对象。
    - `leading_sentences`：包含每个节或子节的一个对象的数组，与 `section_titles` 数组并行，用于详细描述匹配节或子节中的主题句。与在 `section_titles` 数组中一样，不会对对象进行嵌套；而是会对其进行序列化，并且可以使用输入文档中元素的 `begin` 和 `end` 值或任何级别标记使其恢复正常顺序。
      - `text`：一个字符串，用于列出主题句（如果检测到）。
      - `location`：主题句在输入文档中的位置，由其 `begin` 和 `end` 索引来定义。
      - `element_locations`：一个数组，用于包含指定节中主题句的 `begin` 和 `end` 值的对象。
  - `parties`：一个数组，用于定义服务识别到的当事方。
    - `party`：一个字符串值，用于标识当事方。
    - `role`：一个字符串值，用于标识当事方的角色。
    - `addresses`：用于标识地址的对象的数组。
      - `text`：一个包含地址的元素。
      - `location`：地址的位置，由其 `begin` 和 `end` 索引来定义。
    - `contacts`：一个数组，用于定义在输入文档中识别到的联系人的姓名和角色。
      - `name`：一个字符串，用于列出识别到的联系人的姓名。
      - `role`：一个字符串，用于列出识别到的联系人的角色。  
  - `effective_dates`：一个数组，用于标识文档的生效日期。
    - `text`：生效日期，以字符串格式列出。
    - `location`：日期的位置，由其 `begin` 和 `end` 索引来定义。
  - `contract_amounts`：一个数组，用于标识文档中识别到的货币金额。
    - `text`：合同金额，以字符串格式列出。
    - `location`：金额的位置，由其 `begin` 和 `end` 索引来定义。

**\* 有关表的说明：**
  - 每个单元格的行和列索引值都是从零开始的，因此起始值为 `0`。
  - `row_header_ids` 和 `row_header_texts` 元素数组中的多个值表示行标题的层次结构。
  - `column_header_ids` 和 `column_header_texts` 元素数组中的多个值表示列标题的层次结构。
