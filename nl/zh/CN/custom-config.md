---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-10"

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

# 配置参考信息

如果您的数据有特殊的[转换](#conversion)、[扩充](#enrichment)或[规范化](#normalization)需求，那么可以采用 JSON 格式创建您自己的 {{site.data.keyword.discoveryshort}} 摄入配置。
{: shortdesc}

 以下各部分详细描述了此 JSON 的结构以及可在其中定义的对象。

## 配置结构
{: #structure}

{{site.data.keyword.discoveryshort}} 配置的结构如下所示：

```json
{
  "name": "Configuration Name",
  "description": "Descriptive text about the configuration",
  "conversions": {
    "word": {},
    "pdf": {},
    "html": {},
    "segment": {},
    "json_normalizations": []
  },
  "enrichments": [],
  "normalizations": []
}
```
{: codeblock}

基本 JSON 对象包含以下各项：

-  `"name": "Configuration Name"` - 配置的名称
-  `"description": "Descriptive text about the configuration"` - 配置的描述

必须定义以下对象和数组，才能对上传到集合的文档执行转换、扩充和规范化。

- `"conversions": {}` - 如何将文档转换为可以扩充的 JSON。
- `"enrichments": []` - 哪些扩充项应用于 JSON 的哪些部分。
- `"normalizations": []` - 存储文档之前需要执行的任何扩充后调整。

此外，在创建/更新配置时，{{site.data.keyword.discoveryshort}} 会向基本对象添加以下各项：

```json
{
  "configuration_id": "4f5b7c7b-ebf4-4963-882e-27eff08f08e3",
  "created": "2017-09-13T14:45:03.575Z",
  "updated": "2017-09-13T14:45:03.575Z"
}
```
{: codeblock}

## 转换
{: #conversion}

转换文档采用原始的源格式，并使用一个或多个步骤将其变换为可用于摄入过程的其余部分的 JSON。根据上传的文件类型，过程如下所示：

- **PDF** 文件将使用 `pdf` 选项转换为 HTML，然后会使用 `html` 选项将生成的 **HTML** 转换为 JSON，最后会使用 `json` 选项转换生成的 **JSON**。

- **Microsoft Word** 文件将使用 `word` 选项转换为 HTML，然后会使用 `html` 选项将生成的 **HTML** 转换为 JSON，最后会使用 `json` 选项转换生成的 **JSON**。

- **HTML** 文件将使用 `html` 选项转换为 JSON，然后会使用 `json` 选项转换生成的 **JSON**。

- **JSON** 文件将使用 `json` 选项进行转换。

以下部分中描述了这些选项。转换完成后，会先对内容执行[扩充](#enrichment)和[规范化](#normalization)，然后存储该内容。

### PDF
{: #pdf}

`pdf` 转换对象用于定义应该如何将 PDF 文档转换为 HTML，其结构如下：

```json
"pdf": {
  "heading": {
    "fonts": [
      {
        "level": 1,
        "min_size": 24,
        "max_size": 80,
        "bold": false,
        "italic": true,
        "name": "arial"
      },
      {
        "level": 2,
        "min_size": 18,
        "max_size": 24,
        "bold": true,
        "italic": false,
        "name": "ariel"
      }
    ]
  }
},
```
{: codeblock}

转换 PDF 文件时，这些文件中的标题可以通过识别每个标题级别的大小、字体和样式进行确定（并转换为相应的 HTML "`h`" 标记）。如有必要，可以多次指定标题级别，以便正确识别所有相关部分。HTML 标题级别对于确定是计划使用 CSS 选择器来抽取内容还是打算使用文档拆分来拆分文档而言非常重要。`heading` 对象包含 `fonts` 数组，该数组中的每一项都使用以下参数指定标题级别：

- `"level": INT` - *必需* - 使用这些参数识别到的文本将转换为的 HTML `h` 级别。
- `"min_size": INT` - _可选_ - 识别为此标题级别的最小字体大小。
- `"max_size": INT` - _可选_ - 识别为此标题级别的最大字体大小。
- `"bold": boolean` - _可选_ - 为 `true` 时，仅将粗体字体识别为此标题级别。
- `"italic": boolean` - _可选_ - 为 `true` 时，仅将斜体字体识别为此标题级别。
- `"name": "string"` - _可选_ - 识别为此标题级别的字体的名称。

对于要识别为标题的文本区域，必须与在特定数组项中定义的所有参数相匹配。如果定义的参数太灵活，识别到的标题可能会多于预期。如果多次严格定义每个标题级别，以确保包含所有标题级别变体而没有无效匹配项，那么您将获得更好的结果。


### Word
{: #word}

`word` 转换对象用于定义应该如何将 Word 文档转换为 HTML，其结构如下：

```json
"word": {
  "heading": {
    "fonts": [
      {
        "level": 1,
        "min_size": 24,
        "bold": true,
        "italic": false,
        "name": "arial"
      },
      {
        "level": 2,
        "min_size": 18,
        "max_size": 23,
        "bold": true,
        "italic": false
      }
    ],
    "styles": [
      {
        "level": 1,
        "names": [
          "pullout heading",
          "pulloutheading",
          "header"
        ]
      },
      {
        "level": 2,
        "names": [
          "subtitle"
        ]
      }
    ]
  }
},
```
{: codeblock}

Microsoft Word 转换对象的工作方式类似于 PDF 转换对象。但是，从 Microsoft Word 文档中抽取标题时，在 `heading` 对象内可以指定两个不同的数组。您可以使用其中一个或同时使用这两个标题抽取数组，从 Microsoft Word 文档中抽取标题级别元素。

`fonts` 数组中的每一项都使用以下参数和字体特征来指定标题级别：

- `"level": INT` - *必需* - 使用这些参数识别到的文本将转换为的 HTML `h` 级别。
- `"min_size": INT` - _可选_ - 识别为此标题级别的最小字体大小。
- `"max_size": INT` - _可选_ - 识别为此标题级别的最大字体大小。
- `"bold": boolean` - _可选_ - 为 `true` 时，仅将粗体字体识别为此标题级别。
- `"italic": boolean` - _可选_ - 为 `true` 时，仅将斜体字体识别为此标题级别。
- `"name": "string"` - _可选_ - 识别为此标题级别的字体的名称。

对于要识别为 `font` 数组中标题的文本区域，必须与在特定数组项中定义的所有参数相匹配。如果定义的参数太灵活，识别到的标题可能会多于预期。如果多次严格定义每个标题级别，以确保包含所有标题级别变体而没有无效匹配项，那么您将获得更好的结果。

`styles` 数组中的每一项都通过应用于该段的 Microsoft Word 样式指定标题级别。

- `"level": INT` - *必需* - 使用这些参数识别到的文本将转换为的 HTML `h` 级别。
- `"names": array` - *必需* - 将识别为此标题级别的样式名称的逗号分隔数组。

*何时使用字体和何时使用样式* - 如果 Microsoft Word 文档非常符合样式表，其中每段都使用相应样式进行了正确标记，那么建议您使用 `styles` 来抽取标题。但是，您可能会发现某些文档具有作者已手动覆盖的样式。这些文档在使用 `fonts` 抽取方法时转换效果更好。
{: tip}


### HTML
{: #html}

```json
"html": {
  "exclude_tags_completely": [
    "script",
    "sup"
  ],
  "exclude_tags_keep_content": [
    "font",
    "em"
  ],
  "exclude_content": {
    "xpaths": [
      "//*[@id='list-old']",
      "//*[@id='unstable']"
    ]
  },
  "keep_content": {
    "xpaths": [
      "//*[@id='footer']",
      "//*[@id='header']"
    ]
  },
  "exclude_tag_attributes": [
    "EVENT_ACTIONS"
  ],
  "keep_tag_attributes": [
    "id"
  ],
  "extracted_fields": {
    "{field_name}": {
      "css_selector": "{CSS_selector_expression_1}",
      "type": "{field_type}"
    }
  }
},
```
{: codeblock}

#### exclude_tags_completely

`"exclude_tags_completely" : array` - 将排除的 HTML 标记名称的数组。这包括标记、内容以及定义的任何标记属性。

#### exclude_tags_keep_content

`"exclude_tags_keep_content" : array` - 将除去标记信息的 HTML 标记名称的数组。这将导致精简 HTML 标记和任何标记属性。除非指定，否则不会进一步精简标记的内容。例如，如果为 `span` HTML 标记指定 `exclude_tags_keep_content`，那么 `<span class="info">Some <strong>Information</strong></span>` 将精简为：`Some <strong>Information</strong>`

#### exclude_content

`"xpaths" : array` - 用于识别所除去内容的 XPath 的数组。如果设置了此值，将从输出中除去与某个 XPath 相匹配的所有内容。

#### keep_content

`"xpaths" : array` - 用于识别所转换内容的 XPath 的数组。如果设置了此值，将在输出中包含与某个 XPath 相匹配的所有内容。此参数指定的包含项将在 `exclude_content` 指定的任何处理之后进行处理。

#### exclude_tag_attributes

`"exclude_tag_attributes" : array` - 由转换除去的 HTML 属性名称的数组，与这些属性名称所在的 HTML 标记无关。

#### keep_tag_attributes

`"keep_tag_attributes" : array` - 由转换保留的 HTML 属性名称的数组。

#### extracted_fields

此对象用于定义将在转换过程中从 HTML 源代码中抽取到单独 JSON 字段中的任何内容。内容使用 CSS 选择器来识别。

要创建的每个字段由一个对象进行定义，如下所示：

```json
"{field_name}": {
  "css_selector": "{CSS_selector_expression_1}",
  "type": "{field_type}"
}
```
{: codeblock}

- `"{field_name}"` - 要创建的字段的名称。

**注：**配置中定义的字段名称必须满足[字段名称需求](#field_reqs)中定义的限制。

- `"css_selector" : string` - *必需* - 用于定义要存储在字段中的内容区域的 CSS 选择器表达式。
- `"type" : string` - *必需* - 要创建的字段的类型，可以是 `string` 或 `date`。有关详细信息，请参阅[使用 CSS 选择器抽取字段](docs/services/discovery/building.md#using-css)。

### 分段
{: #segment}

`segment` 对象是一组配置选项，用于根据识别到的 HTML 标题（`h1` 或 `h2`）将摄入的文档拆分成一个或多个分段。

```json
"segment": {
  "enabled": true,
  "selector_tags": ["h1", "h2", "h3", "h4", "h5", "h6"]
}
```
{: codeblock}

- `"enabled": boolean` - *必需* - 必须设置为 `true` 才能启用文档分段。
- `"selector_tags": array` - *必需* - 据以拆分文档的 HTML `h` 标记的逗号分隔数组。

总之，启用了文档分段时，不能指定以下各项：

-  在配置过程中，不能指定 `json_normalizations`。
-  在配置过程中，不能指定 `normalizations`。
-  在配置过程中，不能指定 `html` 转换的 `extracted_fields` 选项。

有关详细信息，请参阅[执行分段](/docs/services/discovery/building.html#performing-segmentation)。


### JSON
{: #json}

可以通过在 `json_normalizations` 数组中定义 `operation` 对象，对摄入的 JSON 执行扩充前规范化。

```json
"json_normalizations": [
  {
    "operation": "remove",
    "source_field": "header"
  },
  {
    "operation": "copy",
    "source_field": "title",
    "destination_field": "title_old"
  },
  {
    "operation": "move",
    "destination_field": "content",
    "source_field": "body"
  },
  {
    "operation": "merge",
    "source_field": "synopsis",
    "destination_field": "preamble"
  },
  {
    "operation": "remove_nulls"
  }
]
```
{: codeblock}

#### 操作对象
{: #operations}

- `"operation": string` - *必需* - 将对 JSON 执行的操作，必须为以下其中一项：
  - `remove` - 将从 JSON 中除去指定的 `source_field`。
  - `copy` - 指定的 `source_field` 内容将复制到 `destination_field` 的新实例。
  - `move` - 指定的 `source_field` 将重命名为 `destination_field`。如果 `destination_field` 已存在，那么将创建 `destination_field` 的新实例。
  - `merge` - `source_field` 和 `destination_field` 的内容将合并到 `destination_field` 中。
  - `remove_nulls` - 将除去内容为 `null` 的字段。
- `"source_field": string` - _可选_ - 将对其执行操作的字段。
- `"destination_field": string` - _可选_ - 操作将输出到的目标字段。  

  **注：**配置中定义的字段名称必须满足[字段名称需求](#field_reqs)中定义的限制。


## 扩充项
{: #enrichments}

```json
"enrichments": [
  {
    "enrichment": "elements",
    "source_field": "html",
    "destination_field": "enriched_html",
    "options": {
      "model": "contract"
    }
  },
  {
    "enrichment": "natural_language_understanding",
    "source_field": "title",
    "destination_field": "enriched_title",
    "options": {
      "features": {
        "keywords": {
          "sentiment": true,
          "emotion": false,
          "limit": 50
        },
        "entities": {
          "sentiment": true,
          "emotion": false,
          "limit": 50,
          "mentions": true,
          "mention_types": true,
          "sentence_locations": true,        
          "model": "WKS-model-id"
        },
        "sentiment": {
          "document": true,
          "targets": [
            "IBM",
            "Watson"
          ]

        },
        "emotion": {
          "document": true,
          "targets": [
            "IBM",
            "Watson"
          ]
        },
        "categories": {},
        "concepts": {
          "limit": 8
        },
        "semantic_roles": {
          "entities": true,
          "keywords": true,
          "limit": 50
        },
        "relations": {
          "model": "WKS-model-id"
        }
      }
    }
  }
]
```
{: codeblock}

{{site.data.keyword.discoveryshort}} 支持添加 {{site.data.keyword.nlushort}} 和“元素分类”扩充项。您要扩充的每个字段都由 `enrichments` 数组中的对象进行定义。每个扩充对象都需要指定 `source_field`、`destination_field` 和 enrichments。

- `"enrichment": string` - *必需* - 要在此字段上使用的扩充类型。要抽取 {{site.data.keyword.nlushort}} 扩充项，请使用 `natural_language_understanding`；要执行“元素分类”，请使用 `elements`。

  **注：**使用 `elements` 扩充项时，遵循[元素分类](/docs/services/discovery/element-classification.html)文档中指定的准则很重要。具体而言，只有在指定此扩充项时，才能摄入 PDF 文件。
  
- `"source_field" : string` - *必需* - 将扩充的源字段。完成 `json_normalizations` 操作后，源中必须存在此字段。
- `"destination_field" : string` - *必需* - 要在其中创建扩充项的容器对象的名称。

  **注：**配置中定义的字段名称必须满足[字段名称需求](#field_reqs)中定义的限制。

### 元素分类扩充项

使用“元素分类”时，每个 `elements` 扩充对象都必须包含 `"options": {}` 对象，并指定以下参数：

- `"model" : string` - *必需* - 要用于此文档的元素抽取模型。当前支持的模型为：`contract`

**注：**使用 `elements` 扩充项时，遵循[元素分类](/docs/services/discovery/element-classification.html)文档中指定的准则很重要。具体而言，只有在指定此扩充项时，才能摄入 PDF 文件。

### Natural Language Understanding 扩充项

使用 {{site.data.keyword.nlushort}} 时，`enrichments` 数组中的每个对象还必须包含具有以下一个或多个扩充项的 `"options": { "features": { } }` 对象：

### categories

`categories` 扩充项用于识别所摄入文档中的任何常规类别。此扩充项没有选项，必须指定为空对象 `"categories" : {}`

### concepts

`concepts` 扩充项用于根据输入文本中提供的其他概念和实体，查找与该文本关联的概念。

- `"limit" : INT` - *必需* - 要从所摄入文档中抽取的最大概念数。

### emotion

`emotion` 扩充项用于评估整个文档或整个文档中指定目标字符串的总体情绪语气（例如 `anger`）。此扩充项只能用于英语内容。

- `"document" : boolean` - _可选_ - 为 `true` 时，将评估整个文档的情绪语气。
- `"targets" : array` - _可选_ - 文档中评估其情绪状态的目标字符串的逗号分隔数组。

### entities

`entities` 扩充项用于抽取已知实体（例如，人员、场所和组织）的实例。（可选）可以指定 {{site.data.keyword.knowledgestudioshort}} 定制模型来抽取定制实体。

- `"sentiment" : boolean` - _可选_ - 为 `true` 时，将在周围内容的上下文中对抽取的实体执行观点分析。
- `"emotion" : boolean` - _可选_ - 为 `true` 时，将在周围内容的上下文中对抽取的实体执行情绪语气分析。
- `"limit" : INT` - _可选_ - 要从所摄入文档中抽取的最大实体数。缺省值为 `50`。
- `"mentions": boolean` - _可选_ - 为 `true` 时，将记录提及此实体的次数。缺省值为 `false`。
- `"mention_types": boolean` - _可选_ - 为 `true` 时，将存储每次提及此实体的提及类型。缺省值为 `false`。
- `"sentence_location": boolean` - _可选_ - 为 `true` 时，将存储每次实体提及的语句位置。缺省值为 `false`。
- `"model" : string` - _可选_ - 指定此项时，定制模型用于抽取实体，而不抽取公共模型。此选项需要 {{site.data.keyword.knowledgestudioshort}} 定制模型与 {{site.data.keyword.discoveryshort}} 的实例相关联。请参阅[与 Watson Knowledge Studio 集成](/docs/services/discovery/integrate-wks.html)以获取更多信息。

### keywords

`keywords` 扩充项用于在文本内抽取有效字的实例。要了解 keywords、concepts 和 entities 之间的差异，请参阅[了解实体、概念和关键字之间的差异](/docs/services/discovery/building.html#udbeck)。

- `"sentiment" : boolean` - _可选_ - 为 `true` 时，将在周围内容的上下文中对抽取的关键字执行观点分析。
- `"emotion" : boolean` - _可选_ - 为 `true` 时，将在周围内容的上下文中对抽取的关键字执行情绪语气分析。
- `"limit" : INT` - _可选_ - 要从所摄入文档中抽取的最大关键字数。缺省值为 `50`。

### semantic_roles

`semantic_roles` 扩充项用于识别所摄入文本内的语句组成部分，例如主体、操作和受体。

- `"entities" : boolean` - _可选_ - 为 `true` 时，将从语句组成部分中抽取实体。
- `"keywords" : boolean` - _可选_ - 为 `true` 时，将从语句组成部分中抽取关键字。
- `"limit" : INT` - _可选_ - 要从所摄入文档中抽取的最大 `semantic_roles` 对象数（要解析的语句数）。缺省值为 `50`。

### sentiment

`sentiment` 扩充项用于评估整个文档或整个文档中指定目标字符串的总体观点级别。

- `"document" : boolean` - _可选_ - 为 `true` 时，将评估整个文档的观点。
- `"targets" : array` - _可选_ - 文档中要评估其观点的目标字符串的逗号分隔数组。

### relations

`relations` 扩充项用于抽取文档内识别到的实体之间的已知关系。（可选）可以指定 {{site.data.keyword.knowledgestudioshort}} 定制模型来抽取定制关系。

- `"model" : string` - _可选_ - 指定此项时，定制模型用于抽取关系，而不抽取公共模型。此选项需要 {{site.data.keyword.knowledgestudioshort}} 定制模型与 {{site.data.keyword.discoveryshort}} 的实例相关联。请参阅[与 Watson Knowledge Studio 集成](/docs/services/discovery/integrate-wks.html)以获取更多信息。

## 规范化
{: #normalization}

`normalizations` 是 JSON `operation` 对象数组，用于在应用 `enrichments` 后清除摄入的 JSON，然后再存储该 JSON。

```json
"normalizations": [
  {
    "operation": "remove",
    "source_field": "enriched_title.entities.text"
  },
  {
    "operation": "copy",
    "source_field": "enriched_title.sentiment.document.score",
    "destination_field": "titlescore"
  }
]
```
{:codeblock}

[此处](#operations)列出了 `operation` 对象选项

## 字段名称需求
{: #field_reqs}

字段名称不能包含空格。以下字符和字符串是保留项，不能在字段名称中使用：


```
  .  ,  # ? :
  id
  score
  highlight
  result_metadata
```
{: pre}

字符 `_`、`+` 和 `-` 不能用作 `field_name` 的前缀

数字字符 `0 - 9` 不应作为字段名称的后缀（例如，`extracted-content2`）。将对这些字段名称建立索引，但无法对其进行查询。
