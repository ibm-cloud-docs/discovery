---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-15"

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

# Operadores de consulta
{: #query-operators}

Los operadores son los separadores entre diferentes partes de una consulta. Si desea ver una lista completa de los operadores disponibles, consulte la [Referencia de consultas](/docs/services/discovery?topic=discovery-query-reference#operators).

## . \[Delimitador JSON\]
{: #delimiter}

Este delimitador separa los niveles de jerarquía en el esquema JSON.

Por ejemplo:
```bash
enriched_text.concepts.text
```
{: codeblock}

## : \[Incluye\]
{: #includes}

Este operador especifica una coincidencia para el término de la consulta.

Por ejemplo:
```bash
enriched_text.concepts.text:"cloud computing"
```
{: codeblock}

## :: \[Coincidencia exacta\]
{: #match}

Este operador especifica una coincidencia exacta para el término de la consulta.

Por ejemplo:
```bash
enriched_text.concepts.text::"Cloud computing"
```
{: codeblock}

Las coincidencias exactas son sensibles a mayúsculas y minúsculas.

## :! \[No incluye\]
{: #notinclude}

Este operador especifica que los resultados no contienen una coincidencia para el término de la consulta.

Por ejemplo:
```bash
enriched_text.concepts.text:!"cloud computing"
```
{: codeblock}

## ::! \[No una coincidencia exacta\]
{: #notamatch}

Este operador especifica que los resultados no contienen una coincidencia exacta para el término de la consulta.

Por ejemplo:
```bash
enriched_text.concepts.text::!"Cloud computing"
```
{: codeblock}

Las coincidencias exactas son sensibles a mayúsculas y minúsculas.

## \\ \[Carácter de escape\]
{: #escape}

Carácter de escape para las consultas que en las que se tiene la necesidad de consultar términos con literales de series que contienen caracteres que de otra manera serían de control.

Por ejemplo:
```bash
title::"Dorothy said: \"There's no place like home\""
```
{: codeblock}

## "" \[Consulta de frase\]
{: #phrase}

Todo el contenido de una consulta de frase se procesa como si se codificase con caracteres de escape. Así que no se analiza ningún carácter especial dentro de la consulta de frase, excepto las comillas dobles (`"`) dentro de consulta de frase, que se debe codificar con un carácter de escape (`\"`). Las consultas de frase se utilizan con consultas basadas en clasificación y texto completo, y no con operaciones de filtros booleanos. No utilice comodines (`*`) en las consultas de frase. 

Las comillas simples (`'`) no están soportadas.
{: note}

Por ejemplo:
```bash
enriched_text.entities.text:"IBM watson"
```
{: codeblock}

## (), \[\] \[Agrupación anidada\]
{: #nestedquery}

Las agrupaciones lógicas se pueden definir para especificar información más específica.

Por ejemplo:
```bash
enriched_text.entities:(text:IBM,type:Company)
```
{: codeblock}

## \| \[or\]
{: #or}

Operador booleano "or".

Por ejemplo:
```bash
enriched_text.entities.text:Google|IBM
```
{: codeblock}

## , \[and\]
{: #and}

Operador booleano "and".

Por ejemplo:
```bash
enriched_text.entities.text:Google,IBM
```
{: codeblock}

## <=, >=, >, < \[Comparaciones numéricas\]
{: #comparisons}

Crea comparaciones numéricas de menor que o igual a, mayor que o igual que, mayor que y menor que.

Por ejemplo:
```bash
enriched_text.sentiment.document.score>0.679
```
{: codeblock}

## ^x \[Multiplicador de puntuación\]
{: #multiplier}

Incrementa el valor de puntuación de un término de búsqueda.

Por ejemplo:
```bash
enriched_text.concepts.text:IBM^3
```
{: codeblock}

## * \[Comodín\]
{: #Wildcard}

Establece la coincidencia de un número cualquiera de caracteres en una expresión de búsqueda. No utilice mayúsculas con comodines.

Por ejemplo:
```bash
enriched_text.entities.text:ib*
```
{: codeblock}

## ~n \[Variación de serie\]
{: #variation}

Número de cambios de caracteres individuales que se necesitan realizar para que una serie se considere que coincide con otra. Por ejemplo, `car~1` coincidirá con `car`,`cap`,`cat`,`can`, etc.

Por ejemplo:
```bash
enriched_text.concepts.text:Watson~3
```
{: codeblock}

## :* \[Existe\]
{: #exists}

Se utiliza para devolver todos los resultados en los que existe el `campo` especificado.

Por ejemplo:
```bash
title:*
```
{: codeblock}

## !* \[No existe\]
{: #dnexist}

Se utiliza para devolver todos los resultados que no incluye el `campo` especificado.

Por ejemplo:
```bash
title:!*
```
{: codeblock}
