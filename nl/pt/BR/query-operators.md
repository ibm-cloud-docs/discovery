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

# Operadores de consulta
{: #query-operators}

Os operadores são os separadores entre diferentes partes de uma consulta. Para obter a lista completa de
operadores disponíveis, consulte a
[Referência de consulta](/docs/services/discovery/query-reference.html#operators).

## . \[JSON delimiter\]
{: #delimiter}

Esse delimitador separa os níveis da hierarquia no esquema JSON

Por exemplo:
```bash
enriched_text.concepts.text
```
{: codeblock}

## : \[Includes\]
{: #includes}

Esse operador especifica uma correspondência para o termo de consulta.

Por exemplo:
```bash
enriched_text.concepts.text: "cloud computing "
```
{: codeblock}

## :: \[Exact match\]
{: #match}

Esse operador especifica uma correspondência exata para o termo de consulta.

Por exemplo:
```bash
enriched_text.concepts.text :: "Computação em nuvem"
```
{: codeblock}

Correspondências exatos fazem distinção entre maiúsculas e minúsculas.

## :! \[Does not include\]
{: #notinclude}

Este operador especifica que os resultados não contêm uma correspondência para o termo de consulta

Por exemplo:
```bash
enriched_text.concepts.text:! "computação em nuvem "
```
{: codeblock}

## ::! \[Not an exact match\]
{: #notamatch}

Esse operador especifica que os resultados não correspondem exatamente o termo de consulta

Por exemplo:
```bash
enriched_text.concepts.text ::! "Computação em nuvem "
```
{: codeblock}

Correspondências exatos fazem distinção entre maiúsculas e minúsculas.

## \\ \[Escape character\]
{: #escape}

Caractere de escape para consultas que requerem a capacidade de consultar termos usando
sequências literais que contêm caracteres de controle.

Por exemplo:
```bash
title::"Dorothy said: \"There's no place like home\""
```
{: codeblock}

## "" \[Phrase query\]
{: #phrase}

Todos os conteúdos de uma consulta de frase são processados como escapados. Assim, nenhum caractere
especial em uma consulta de frase é analisado, exceto as aspas duplas (`"`) dentro de uma
consulta de frase, que devem ser escapadas (`\"`). Use consultas de frase com
consultas de texto completo baseadas em classificação, não com as operações de filtro booleanas. Não use caracteres curingas (`*`) em consultas de frase. **Nota**: aspas
simples (`'`) não são suportadas.

Por exemplo:
```bash
enriched_text.entities.text: "IBM watson"
```
{: codeblock}

## (), \[\] \[Nested grouping\]
{: #nestedquery}

Agrupamentos lógicos podem ser formados para definir informações mais específicas.

Por exemplo:
```bash
enriched_text.entities:(text:IBM,type:Company)
```
{: codeblock}

## \| \[or\]
{: #or}

Operador booleano para "ou".

Por exemplo:
```bash
enriched_text.entities.text:Google|IBM
```
{: codeblock}

## , \[and\]
{: #and}

Operador booleano para "e".

Por exemplo:
```bash
enriched_text.entities.text:Google,IBM
```
{: codeblock}

## <=, >=, >, < \[Numerical comparisons\]
{: #comparisons}

Cria comparações numéricas de menor ou igual a, maior ou igual a, maior que e menor que.

Por exemplo:
```bash
enriched_text.sentiment.document.score>0.679
```
{: codeblock}

## ^x \[Score multiplier\]
{: #multiplier}

Aumenta o valor de pontuação de um termo de procura.

Por exemplo:
```bash
enriched_text.concepts.text:IBM^3
```
{: codeblock}

## * \[Wildcard\]
{: #Wildcard}

Corresponde caracteres desconhecidos em uma expressão de procura. Não use letras maiúsculas com curingas.

Por exemplo:
```bash
enriched_text.entities.text:ib *
```
{: codeblock}

## ~n \[String variation\]
{: #variation}

O número de uma mudança de caracteres que precisa ser feita em uma sequência para torná-la igual à
outra sequência. Por exemplo, `car~1` corresponderá a `car`, `cap`, `cat`, `can`, etc.

Por exemplo:
```bash
enriched_text.concepts.text:Watson~3
```
{: codeblock}

## :* \[Exists\]
{: #exists}

Usado para retornar todos os resultados em que o `field` especificado existe.

Por exemplo:
```bash
título: *
```
{: codeblock}

## !* \[Não existe\]
{: #dnexist}

Usado para retornar todos os resultados que não incluem o `field` especificado.

Por exemplo:
```bash
title! *
```
{: codeblock}
