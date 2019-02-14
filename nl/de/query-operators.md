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

# Abfrageoperatoren
{: #query-operators}

Operatoren trennen die einzelnen Bestandteile einer Abfrage voneinander. Eine vollständige Liste der verfügbaren Operatoren enthält die [Abfragereferenz](/docs/services/discovery/query-reference.html#operators).

## . \[JSON-Begrenzer\]
{: #delimiter}

Dieser Begrenzer grenzt die Hierarchieebenen im JSON-Schema voneinander ab.

Beispiel:
```bash
enriched_text.concepts.text
```
{: codeblock}

## : \[Enthält\]
{: #includes}

Dieser Operator gibt eine Übereinstimmung für den Abfragebegriff an.

Beispiel:
```bash
enriched_text.concepts.text:"cloud computing"
```
{: codeblock}

## :: \[Exakte Übereinstimmung\]
{: #match}

Dieser Operator gibt eine exakte Übereinstimmung für den Abfragebegriff an.

Beispiel:
```bash
enriched_text.concepts.text::"Cloud computing"
```
{: codeblock}

Bei exakten Übereinstimmungen muss die Groß-/Kleinschreibung beachtet werden.

## :! \[Enthält nicht\]
{: #notinclude}

Dieser Operator gibt an, dass die Ergebnisse keine Übereinstimmung für den Abfragebegriff enthalten.

Beispiel:
```bash
enriched_text.concepts.text:!"cloud computing"
```
{: codeblock}

## ::! \[Keine exakte Übereinstimmung\]
{: #notamatch}

Dieser Operator gibt an, dass die Ergebnisse nicht genau mit dem Abfragebegriff übereinstimmen.

Beispiel:
```bash
enriched_text.concepts.text::!"Cloud computing"
```
{: codeblock}

Bei exakten Übereinstimmungen muss die Groß-/Kleinschreibung beachtet werden.

## \\ \[Escapezeichen\]
{: #escape}

Escapezeichen werden für Abfragen verwendet, die in der Lage sein müssen, Begriffe unter Verwendung von Zeichenfolgeliteraln abzufragen, in denen Steuerzeichen enthalten sind.

Beispiel:
```bash
title::"Dorothy said: \"There's no place like home\""
```
{: codeblock}

## "" \[Ausdrucksabfrage\]
{: #phrase}

Der gesamte Inhalt einer Ausdrucksabfrage wird so verarbeitet, wie er mit Escapezeichen versehen ist. Daher werden keine Sonderzeichen innerhalb einer Ausdrucksabfrage analysiert. Hiervon ausgenommen sind Anführungszeichen (`"`) in einer Ausdrucksabfrage, die mit Escapezeichen versehen werden müssen (`\"`). Verwenden Sie Ausdrucksabfragen bei einstufungsbasierten Volltextabfragen und nicht bei booleschen Filteroperationen. Verwenden Sie in Ausdrucksabfragen keine Platzhalter (`*`). **Hinweis**: Einfache Anführungszeichen (`'`) werden nicht unterstützt.

Beispiel:
```bash
enriched_text.entities.text:"IBM watson"
```
{: codeblock}

## (), \[\] \[Verschachtelte Gruppierung\]
{: #nestedquery}

Durch die Bildung von logischen Gruppierungen können spezifischere Informationen angegeben werden.

Beispiel:
```bash
enriched_text.entities:(text:IBM,type:Company)
```
{: codeblock}

## \| \[or\]
{: #or}

Der boolesche Operator für 'oder'.

Beispiel:
```bash
enriched_text.entities.text:Google|IBM
```
{: codeblock}

## , \[and\]
{: #and}

Der boolesche Operator für 'und'.

Beispiel:
```bash
enriched_text.entities.text:Google,IBM
```
{: codeblock}

## <=, >=, >, < \[Numerische Vergleiche\]
{: #comparisons}

Erstellt numerische Vergleiche (kleiner-gleich, größer-gleich, größer als bzw. kleiner als).

Beispiel:
```bash
enriched_text.sentiment.document.score>0.679
```
{: codeblock}

## ^x \[Bewertungsmultiplikator\]
{: #multiplier}

Erhöht den Wert für die Bewertung eines Suchbegriffs.

Beispiel:
```bash
enriched_text.concepts.text:IBM^3
```
{: codeblock}

## * \[Platzhalter\]
{: #Wildcard}

Ergibt eine Übereinstimmung mit unbekannten Zeichen in einem Suchausdruck. Verwenden Sie bei Platzhaltern keine Großbuchstaben.

Beispiel:
```bash
enriched_text.entities.text:ib*
```
{: codeblock}

## ~n \[Zeichenfolgenvariante\]
{: #variation}

Die Anzahl der Einzelzeichenänderungen, die an einer Zeichenfolge vorgenommen werden müssen, damit sie mit einer anderen Zeichenfolge identisch ist. Beispiel: `car~1` ergibt eine Übereinstimmung mit `car`, `cap`, `cat`, `can` usw.

Beispiel:
```bash
enriched_text.concepts.text:Watson~3
```
{: codeblock}

## :* \[Vorhanden\]
{: #exists}

Wird verwendet, um alle Ergebnisse zurückzugeben, bei denen das angegebene `Feld` vorhanden ist.

Beispiel:
```bash
title:*
```
{: codeblock}

## !* \[Ist nicht vorhanden\]
{: #dnexist}

Wird verwendet, um alle Ergebnisse zurückzugeben, die das angegebene `Feld` nicht enthalten.

Beispiel:
```bash
title!*
```
{: codeblock}
