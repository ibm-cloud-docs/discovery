---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-15"

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

# 查询运算符
{: #query-operators}

运算符是一个查询中不同部分之间的分隔符。有关可用运算符的完整列表，请参阅[查询参考](/docs/services/discovery/query-reference.html#operators)。

## . \[JSON 定界符\]
{: #delimiter}

此定界符用于分隔 JSON 模式中的层次结构级别。

例如：
```bash
enriched_text.concepts.text
```
{: codeblock}

## : \[包含\]
{: #includes}

此运算符指定查询项的匹配项。

例如：
```bash
enriched_text.concepts.text:"cloud computing"
```
{: codeblock}

## :: \[完全匹配\]
{: #match}

此运算符指定查询项的完全匹配项。

例如：
```bash
enriched_text.concepts.text::"Cloud computing"
```
{: codeblock}

完全匹配是区分大小写的。

## :! \[不包含\]
{: #notinclude}

此运算符指定结果不包含查询项的匹配项。

例如：
```bash
enriched_text.concepts.text:!"cloud computing"
```
{: codeblock}

## ::! \[不完全匹配\]
{: #notamatch}

此运算符指定结果不与查询项完全匹配

例如：
```bash
enriched_text.concepts.text::!"Cloud computing"
```
{: codeblock}

完全匹配是区分大小写的。

## \\ \[转义字符\]
{: #escape}

转义字符用于需要有能力使用包含控制字符的字符串字面值来查询项的查询。

例如：
```bash
title::"Dorothy said: \"There's no place like home\""
```
{: codeblock}

## "" \[短语查询\]
{: #phrase}

一个短语查询的所有内容会作为转义内容进行处理。因此，不会解析短语查询内的特殊字符，但短语查询内的双引号 (`"`) 除外，必须对其进行转义 (`\"`)。请将短语查询与基于排名的全文查询配合使用，而不要与布尔过滤器操作配合使用。不要在短语查询中使用通配符 (`*`)。**注**：不支持单引号 (`'`)。

例如：
```bash
enriched_text.entities.text:"IBM watson"
```
{: codeblock}

## () 和 \[\] \[嵌套分组\]
{: #nestedquery}

可以构成逻辑分组来指定更具体的信息。

例如：
```bash
enriched_text.entities:(text:IBM,type:Company)
```
{: codeblock}

## \| \[或\]
{: #or}

“or”的布尔运算符。

例如：
```bash
enriched_text.entities.text:Google|IBM
```
{: codeblock}

## , \[和\]
{: #and}

“and”的布尔运算符。

例如：
```bash
enriched_text.entities.text:Google,IBM
```
{: codeblock}

## <=、>=、> 和 < \[数字比较\]
{: #comparisons}

创建数字比较运算：小于或等于、大于或等于、大于，以及小于。

例如：
```bash
enriched_text.sentiment.document.score>0.679
```
{: codeblock}

## ^x \[分数乘数\]
{: #multiplier}

增加搜索项的分数值。

例如：
```bash
enriched_text.concepts.text:IBM^3
```
{: codeblock}

## * \[通配符\]
{: #Wildcard}

与搜索表达式中的未知字符相匹配。不要将大写字母与通配符一起使用。

例如：
```bash
enriched_text.entities.text:ib*
```
{: codeblock}

## ~n \[字符串变体\]
{: #variation}

将一个字符串转换为另一个字符串所需的单字符更改次数。例如，`car~1` 将与 `car`、`cap`、`cat`、`can` 等相匹配。

例如：
```bash
enriched_text.concepts.text:Watson~3
```
{: codeblock}

## :* \[存在\]
{: #exists}

用于返回包含指定 `field` 的所有结果。

例如：
```bash
title:*
```
{: codeblock}

## !* \[不存在\]
{: #dnexist}

用于返回不包含指定 `field` 的所有结果。

例如：
```bash
title!*
```
{: codeblock}
