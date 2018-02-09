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

# 照会演算子
{: #query-operators}

演算子は、照会のさまざまな部分の分離文字です。使用可能な演算子の完全リストについては、[照会リファレンス](/docs/services/discovery/query-reference.html#operators)を参照してください。

## . \[JSON delimiter\]
{: #delimiter}

この区切り文字は、JSON スキーマの階層のレベルを分離します。

例:
```bash
enriched_text.concepts.text
```
{: codeblock}

## : \[Includes\]
{: #includes}

この演算子は、照会用語の一致を指定します。

例:
```bash
enriched_text.concepts.text:cloud computing
```
{: codeblock}

## :: \[Exact match\]
{: #match}

この演算子は、照会用語の完全一致を指定します。

例:
```bash
enriched_text.concepts.text::cloud computing
```
{: codeblock}

## :! \[Does not include\]
{: #notinclude}

この演算子は、結果に照会用語の一致が含まれていないことを指定します。

例:
```bash
enriched_text.concepts.text:!cloud computing
```
{: codeblock}

## ::! \[Not an exact match\]
{: #notamatch}

この演算子は、結果が照会用語に完全に一致しないことを指定します。

例:
```bash
enriched_text.concepts.text::!cloud computing
```
{: codeblock}

## \\ \[Escape character\]
{: #escape}

制御文字を含むストリング・リテラルを使用して用語を照会できる必要がある照会のエスケープ文字。

例:
```bash
enriched_text.concepts.text:\!cloud computing
```
{: codeblock}

## "" \[Phrase query\]
{: #phrase}

句照会の内容はすべて、エスケープとして処理されます。したがって、エスケープ処理 (`\"`) する必要がある、句照会内の二重引用符 (`"`) を除き、句内の特殊文字は解析されません。句照会は、フルテキストおよびランク・ベースの照会で使用し、ブール値のフィルター操作では使用しないでください。句照会ではワイルドカード (`*`) は使用しないでください。**注**: 単一引用符 (`'`) はサポートされません。

例:
```bash
enriched_text.concepts.text:"IBM watson"
```
{: codeblock}

## (), \[\] \[Nested grouping\]
{: #nestedquery}

より具体的な情報を指定するために論理グループを形成できます。

例:
```bash
enriched_text.entities:(text:IBM,type:Company)
```
{: codeblock}

## \| \[or\]
{: #or}

「or」のブール演算子。

例:
```bash
enriched_text.entities.text:Google|IBM
```
{: codeblock}

## , \[and\]
{: #and}

「and」のブール演算子。

例:
```bash
enriched_text.entities.text:Google,IBM
```
{: codeblock}

## <=, >=, >, < \[Numerical comparisons\]
{: #comparisons}

より小か等しい、より大か等しい、より大、およびより小の数値比較を作成します。

例:
```bash
enriched_text.sentiment.document.score>0.679
```
{: codeblock}

## ^x \[Score multiplier\]
{: #multiplier}

検索語のスコア値を増加します。

例:
```bash
enriched_text.concepts.text:IBM^3
```
{: codeblock}

## * \[Wildcard\]
{: #Wildcard}

検索式内の不明の文字を一致させます。

例:
```bash
enriched_text.concepts.text:IBM*
```
{: codeblock}

## ~n \[String variation\]
{: #variation}

あるストリングをもう 1 つのストリングと同じにするために、そのストリングに対して行う必要がある 1 文字変更の数。例えば、`car~1` は、`car`、`cap`、`cat`、`can` などに一致します。

例:
```bash
enriched_text.concepts.text:Watson~3
```
{: codeblock}
