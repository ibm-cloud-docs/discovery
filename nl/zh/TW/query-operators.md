---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-09"

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

# 查詢運算子
{: #query-operators}

運算子是在查詢的不同部分之間的分隔字元。如需可用運算子的完整清單，請參閱[查詢參照](/docs/services/discovery/query-reference.html#operators)。

## . \[JSON 定界字元\]
{: #delimiter}

此定界字元會區隔 JSON 綱目中的階層層次

例如：
```bash
enriched_text.concepts.text
```
{: codeblock}

## : \[包含\]
{: #includes}

此運算子指定查詢詞彙的相符項。

例如：
```bash
enriched_text.concepts.text:cloud computing
```
{: codeblock}

## :: \[完全相符\]
{: #match}

此運算子指定與查詢詞彙完全相符的項目。

例如：
```bash
enriched_text.concepts.text::cloud computing
```
{: codeblock}

## :! \[不包含\]
{: #notinclude}

此運算子指定結果不包含查詢詞彙的相符項

例如：
```bash
enriched_text.concepts.text:!cloud computing
```
{: codeblock}

## ::! \[不完全相符\]
{: #notamatch}

此運算子指定結果不完全符合查詢詞彙

例如：
```bash
enriched_text.concepts.text::!cloud computing
```
{: codeblock}

## \\ \[跳出字元\]
{: #escape}

需要有能力使用包含控制字元的字串文字來查詢詞彙之查詢的跳出字元。

例如：
```bash
enriched_text.concepts.text:\!cloud computing
```
{: codeblock}

## "" \[詞組查詢\]
{: #phrase}

詞組查詢的所有內容都會以跳出方式來處理。因此，除了詞組查詢內的雙引號（`"`）必須跳出 (`\"`) 之外，不會剖析詞組查詢內的特殊字元。使用詞組查詢時請搭配全文分級式查詢，而不要搭配布林過濾器運算。請勿在詞組查詢中使用萬用字元 (`*`)。**附註**：不支援單引號 (`'`)。

例如：
```bash
enriched_text.concepts.text:"IBM watson"
```
{: codeblock}

## (), \[\] \[巢狀分組\]
{: #nestedquery}

可以形成邏輯分組以指定更具體的資訊。

例如：
```bash
enriched_text.entities:(text:IBM,type:Company)
```
{: codeblock}

## \| \[或\]
{: #or}

"or" 的布林運算子。

例如：
```bash
enriched_text.entities.text:Google|IBM
```
{: codeblock}

## , \[及\]
{: #and}

"and" 的布林運算子。

例如：
```bash
enriched_text.entities.text:Google,IBM
```
{: codeblock}

## <=, >=, >, < \[數值比較\]
{: #comparisons}

建立小於或等於、大於或等於、大於及小於的數值比較。

例如：
```bash
enriched_text.sentiment.document.score>0.679
```
{: codeblock}

## ^x \[評分乘數\]
{: #multiplier}

增加搜尋詞彙的評分值。

例如：
```bash
enriched_text.concepts.text:IBM^3
```
{: codeblock}

## * \[萬用字元\]
{: #Wildcard}

比對搜尋表示式中的不明字元。

例如：
```bash
enriched_text.concepts.text:IBM*
```
{: codeblock}

## ~n \[字串變異\]
{: #variation}

需要對一個字串進行的單字元變更次數，以使它與另一個字串相同。例如，`car~1` 將符合 `car`、`cap`、`cat`、`can` 等等。

例如：
```bash
enriched_text.concepts.text:Watson~3
```
{: codeblock}
