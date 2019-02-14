---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-09"

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

# Abfrageaggregationen
{: #query-aggregations}

Aggregationen geben eine Gruppe von Datenwerten zurück. Eine vollständige Liste der verfügbaren Aggregationen enthält die [Abfragereferenz](/docs/services/discovery/query-reference.html#aggregations).

## term
{: #term}

Gibt die höchsten Werte (nach Bewertung und Häufigkeit) für die ausgewählten Aufbereitungen zurück. Gültige Werte sind alle Aufbereitungen. Mit `count` können Sie optional die Anzahl der zurückzugebenden Begriffe angeben. Der Parameter `count` hat den Standardwert 10. Das folgende Beispiel gibt den vollständigen Text und die Aufbereitungen der höchsten Werte bei der Aufbereitung 'concept' zurück und definiert die Rückgabe von 10 Begriffen.

Beispiel:
```bash
term(enriched_text.concepts.text,count:10)
```
{: codeblock}

## filter
{: #filter}

Ein Modifikator, der die Dokumentgruppe der Aggregationsabfrage eingrenzt, der er vorangestellt ist. Das folgende Beispiel filtert die Gruppe der Dokumente heraus, die das Konzept 'Cloud computing' enthalten.

Beispiel:
```bash
filter(enriched_text.concepts.text:"cloud computing")
```
{: codeblock}

## nested
{: #nested}

Die Anwendung der Aggregration 'nested' vor einer Aggregationsabfrage begrenzt die Aggregation auf den angegebenen Bereich von Ergebnissen. Beispielsweise bedeutet `nested(enriched_text.entities)`, dass nur die Komponenten `enriched_text.entities` von Ergebnissen als Grundlage für die Aggregation verwendet werden.

Beispiel:
```bash
nested(enriched_text.entities)
```
{: codeblock}

## histogram
{: #histogram}

Erstellt numerische Intervallsegmente, um Dokumente zu kategorisieren. Verwendet Feldwerte aus einem einzelnen numerischen Feld, um die Kategorie zu beschreiben. Das Feld, das zum Erstellen des Histogramms verwendet wird, muss ein Feld mit einem Zahlenwert (Typ `integer`, `float`, `double` oder `date`) sein. Nicht numerische Typen wie beispielsweise `string` werden nicht unterstützt. Beispielsweise ist **"price": 1.30** ein funktionierender Zahlenwert, während es sich bei **"price": "1.30"** um einen Zeichenfolgenwert handelt, der nicht unterstützt wird. Mit dem Argument `interval` definieren Sie die Größe der Abschnitte, in die die Ergebnisse unterteilt werden. Intervallwerte müssen ganze und nicht negative Zahlen sein und werden so festgelegt, dass die möglichen Feldwerte auf sinnvolle Weise segmentiert werden. Falls Ihre Daten beispielsweise den Preis verschiedener Artikel enthalten (“price”: 1.30, “price”: 1.99, “price”: 2.99), könnten Sie 1 als Wert für die Intervalle verwenden, damit alle zwischen 1 und 2 sowie 2 und 3 gruppierten Elemente angezeigt werden. Ein Intervall von 100 wäre in diesem Fall nicht sinnvoll, da dann alle Daten demselben Segment zugeordnet werden würden. Histogramme können Dezimalwerte verarbeiten, aber Intervalle müssen als ganze Zahlen angegeben werden. Die Syntax lautet `histogram(<field>,<interval>)`. Dies ist im folgenden Beispiel gezeigt.

Beispiel:
```bash
histogram(product.price,interval:1)
```
{: codeblock}

## timeslice
{: #timeslice}

Ein spezielles Histogramm, das Datumswerte verwendet, um Intervallsegmente zu erstellen. Gültige Werte für Datumsintervalle sind `second/seconds` `minute/minutes`, `hour/hours`, `day/days`, `week/weeks`, `month/months` und `year/years`. Die Syntax lautet `timeslice(<field>,<interval>,<time_zone>)`. Damit die Aggregation `timeslice` verwendet werden kann, müssen die Zeitfelder in Ihren Dokumenten den Datentyp `date` und das [UNIX-Zeitformat ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://en.wikipedia.org/wiki/Unix_time){: new_window} verwenden. Wenn nicht beide dieser Voraussetzungen erfüllt sind, funktioniert der Parameter `timeslice` nicht ordnungsgemäß. Sie können eine Zeitscheibe (timeslice) erstellen, falls Ihre Dokumente Feldern `date` mit Werten wie `1496228512` enthalten. Der Wert muss ein numerisches Format besitzen (z. B. `float` oder `double`) und darf nicht in Anführungszeichen eingeschlossen sein. Der Service behandelt Datumsangaben in Text und Datumsangaben im ISO-8601-Format als Datentyp `string` und nicht als Datentyp `date`. In Zeitscheibenaggregationen können Sie anomale Punkte erkennen. Weitere Informationen finden Sie unter [Anomalieerkennung in Zeitscheiben](#anomaly-detection). Das folgende Beispiel gibt Werte für 'sales' ('product.sales') in Intervallen von 2 Tagen in der Zeitzone von New York City zurück.

Beispiel:
```bash
timeslice(product.sales,2day,America/New York)
```
{: codeblock}

### Anomalieerkennung in Zeitscheiben
{: #anomaly-detection}

Auf die Ergebnisse einer Aggregation des Typs `timeslice` können Sie optional eine Anomalieerkennung anwenden. Mit der Anomalieerkennung werden ungewöhnliche Datenpunkte innerhalb einer Zeitreihe lokalisiert und zur genaueren Prüfung markiert. Einsatzbeispiele für die Anomalieerkennung sind unter anderem die Erkennung von Spitzenwerten bei der Kreditkartennutzung oder die Suche nach Artikelclustern zu einem bestimmten Thema in Watson Discovery News.

Zur Anwendung der Anomalieerkennung verwenden Sie die folgende Syntax in Ihrer Aggregation:

```bash
timeslice(field:<date>,interval:<interval>,anomaly:true)`
```
{: codeblock}

Falls Sie `anomaly:true` bei der Aggregation des Typs `timeslice` angeben, enthält die Ausgabe die beiden folgenden zusätzlichen Felder, die im Beispiel dargestellt sind.

  - Ein Feld `"anomaly": true`, mit dem angegeben wird, dass die Anomalieerkennung ausgeführt wurde.
  - Ein Feld `anomaly` an den Stellen im Ergebnisarray der Ausgabe, die eine Anomalie darstellen. Das Feld 'anomaly' enthält einen Wert mit dem Datentyp `float`, der das Ausmaß für die Verhaltensanomalie angibt. Je näher der Wert des Feldes 'anomaly' an `1` liegt, desto größer ist die Wahrscheinlichkeit, dass das Ergebnis eine Anomalie darstellt.

  - Die Felder `key` und `key_as_string` in jedem Objekt des Arrays `results` entsprechen einer in Sekunden angegebenen UNIX-Zeitmarke.
  - Die Anomaliebewertung bezieht sich auf eine einzelne Abfrage und wird nicht abfrageübergreifend ermittelt.

```json
"type": "timeslice",
"field": "blekko.chrondate",
"interval": "1d",
"anomaly": true,
"results": [
  {
    "matching_results": 2933,
    "anomaly": 1,
    "key_as_string": "1496880000",
    "key": 1496880000000
  },
  {
    "matching_results": 3435,
    "anomaly": 1,
    "key_as_string": "1496966400",
    "key": 1496966400000
  },
  {
    "matching_results": 3692,
    "anomaly": 0.598226,
    "key_as_string": "1496016000",
    "key": 1496016000000
  },
  {
    "matching_results": 4551,
    "anomaly": 0.828498,
    "key_as_string": "1495411200",
    "key": 1495411200000
  },
  {
    "matching_results": 947,
    "key_as_string": "1489968000",
    "key": 1489968000000
  },
 ...
]
...
```
{: codeblock}

#### Einschränkungen bei der Anomalieerkennung

- Die Anomalieerkennung ist gegenwärtig nur für Aggregationen der höchsten Ebene mit dem Parameter `timeslice` verfügbar. In untergeordneten (also verschachtelten) Aggregationen kann sie nicht verwendet werden.
- Die maximale Anzahl der Punkte, die durch die Anomalieerkennung in einer Aggregation des Typs `timeslice` verarbeitet werden können, beträgt `1500`.
- Die maximale Anzahl der Aggregationen der höchsten Ebene mit dem Parameter 'timeslice', die durch die Anomalieerkennung verarbeitet werden können, beträgt `20`.

<!--
#### Anomaly detection workflow

The following example workflow detects an anomaly for the text entity `London` and retrieves additional information about the anomalous datapoint.

  1. Timeslice aggregation: `query=entities.text:London&count=0&aggregation=timeslice(blekko.last_crawled,1day,anomaly:true)`
  1. Term aggregation to retrieve top keywords: `query=entities.text:London&count=0&aggregation=term(keywords.text,count:5)&filter=blekko.last_crawled>=1490140800,<=1490227200`
  1. Query to retrieve top enriched title: `query=entities.text:London,keywords.text:Westminster Bridge|police officer|people|Prime Minister Theresa|parliament&count=1&filter=blekko.last_crawled>=1490140800,<=1490227200&return=enrichedTitle.text`
  -->

## top_hits
{: #top_hits}

Gibt die Dokumente in der Rangfolge für die Bewertung der Abfrage oder Aufbereitung zurück. Dieser Parameter kann mit jedem beliebigen Abfrageparameter und jeder beliebigen Aggregation kombiniert werden. Das folgende Beispiel gibt die 10 höchsten Treffer für eine Aggregation des Typs 'term' zurück.

Beispiel:
```bash
term(enriched_text.concepts.text).top_hits(10)
```
{: codeblock}

## unique_count
{: #unique_count}

Gibt die Anzahl der eindeutigen Instanzen für das angegebene Feld in der Sammlung zurück.

Beispiele:
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

Gibt den höchsten Wert für das angegebene Feld in allen übereinstimmenden Dokumenten zurück.

Beispiel:
```bash
max(product.price)
```
{: codeblock}

## min
{: #min}

Gibt den niedrigsten Wert für das angegebene Feld in allen übereinstimmenden Dokumenten zurück.

Beispiel:
```bash
min(product.price)
```
{: codeblock}

## average
{: #average}

Gibt den Durchschnitt der Werte für das angegebene Feld in allen übereinstimmenden Dokumenten zurück.

Beispiel:
```bash
average(product.price)
```
{: codeblock}

## sum
{: #sum}

Addiert die Werte für das angegebene Feld in allen übereinstimmenden Dokumenten.

Beispiel:
```bash
sum(product.price)
```
{: codeblock}
