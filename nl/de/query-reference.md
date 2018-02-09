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

# Abfragereferenz

Der {{site.data.keyword.discoveryfull}}-Service bietet durch Abfragen leistungsfähige Funktionen für die Inhaltssuche. Nachdem Ihr Inhalt hochgeladen und durch den {{site.data.keyword.discoveryshort}}-Service aufbereitet wurde, können Sie Abfragen erstellen und {{site.data.keyword.discoveryshort}} in Ihre eigenen Projekte integrieren oder mit {{site.data.keyword.watson}} Explorer Application Builder eine angepasste Anwendung erstellen.
{: shortdesc}

Weitere Informationen zum Schreiben von Abfragen enthalten die folgenden Abschnitte:
- [Einführung in die Ausführung von Abfragen](/docs/services/discovery/getting-started-query.html)
- [Abfragekonzepte](/docs/services/discovery/using.html)

## Parameterbeschreibungen
{: #parameter-descriptions}

Mithilfe von Abfrageparametern können Sie Ihre Sammlung durchsuchen, eine Ergebnismenge ermitteln und eine Analyse für die Ergebnismenge durchführen.


| Parameter | Beschreibung | Beispiel |
|:-------------------:|------------------------------------------------------------|--------------------------------|
|** Suchparameter **|  |  |
| [query](/docs/services/discovery/query-parameters.html#query) | Eine Suche in Abfragesprache mit Einstufung nach übereinstimmenden Dokumenten. | `query=bees` |
| [filter](/docs/services/discovery/query-parameters.html#filter) | Eine Suche in Abfragesprache ohne Einstufung nach übereinstimmenden Dokumenten. | `filter=bees` |
| [natural_language_query](/docs/services/discovery/query-parameters.html#nlq) | Eine Suche in natürlicher Sprache mit Einstufung nach übereinstimmenden Dokumenten. | `natural_language_query="How do bees fly"` |
| [aggregation](/docs/services/discovery/query-parameters.html#aggregation) | Eine statistische Abfrage der Ergebnismenge. | `aggregation=term(enriched_text.entities.type)` |
| **Strukturparameter** | | |
| [count](/docs/services/discovery/query-parameters.html#count) | Die Anzahl der zurückzugebenden Dokumente im Ergebnis (`result`). | `count=15` |
| [offset](/docs/services/discovery/query-parameters.html#offset) | Die Anzahl der Ergebnisse, die vor der Rückgabe von Dokumenten aus der Ergebnismenge in `result` ignoriert werden sollen. | `offset=100` |
| [return](/docs/services/discovery/query-parameters.html#return) | Die Liste der zurückzugebenden Felder. | `return=title,url` |
| [sort](/docs/services/discovery/query-parameters.html#sort) | Das Feld, nach dem die Ergebnismenge sortiert werden soll. | `sort=enriched_text.sentiment.document.score` |
| [passages.fields](/docs/services/discovery/query-parameters.html#passages_fields) | Die Felder, aus denen Passagen extrahiert werden sollen. | `passages=true&passages.fields=text,abstract,conclusion` |
| [passages.count](/docs/services/discovery/query-parameters.html#passages_count) | Die Anzahl der zurückzugebenden Passagen. | `passages=true&passages.count=6` |
| [passages.characters](/docs/services/discovery/query-parameters.html#passages_characters) | Die Länge der Passagen. | `passages=true&passages.characters=144` |
| [highlight](/docs/services/discovery/query-parameters.html#highlight) | Hebt Übereinstimmungen mit der Abfrage hervor. | `highlight=true` |
| [deduplicate](/docs/services/discovery/query-parameters.html#deduplicate) | Dedupliziert aus {{site.data.keyword.discoverynewsfull}} zurückgegebene Ergebnisse. | `deduplicate=true` |
| [deduplicate.field](/docs/services/discovery/query-parameters.html#deduplicated_field) | Dedupliziert zurückgegebene Ergebnisse auf der Basis eines Feldes. | `deduplicate.field=title` |
| [collection_ids](/docs/services/discovery/query-parameters.html#collection_ids) | Fragt mehrere Sammlungen ab. | `collection_ids={1},{2},{3}` |

## Operatoren
{: #operators}

Operatoren trennen die einzelnen Bestandteile einer Abfrage voneinander. Die folgenden Operatoren sind verfügbar:

| Operator | Beschreibung | Beispiel |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [.](/docs/services/discovery/query-operators.html#delimiter) | JSON-Begrenzer | `enriched_text.concepts.text` |
| [:](/docs/services/discovery/query-operators.html#includes) | Enthält | `text:computer` |
| [::](/docs/services/discovery/query-operators.html#match) | Exakte Übereinstimmung | `title::Query building` |
| [:!](/docs/services/discovery/query-operators.html#notinclude) | Enthält nicht | `text:!computer` |
| [::!](/docs/services/discovery/query-operators.html#notamatch) | Keine exakte Übereinstimmung | `title::!Query building` |
| [\\](/docs/services/discovery/query-operators.html#escape) | Escapezeichen | `enriched_text.entitle.text:Trinidad \& Tobago` |
| [""](/docs/services/discovery/query-operators.html#phrase) | Ausdrucksabfrage | `enriched_text.concepts.text:"IBM Watson"` |
| [(), \[\]](/docs/services/discovery/query-operators.html#nestedquery) | Verschachtelte Gruppierung | `filter-entities:(text:Turkey,type:Location)` |
| [<code>&#124;</code>](/docs/services/discovery/query-operators.html#or) | Oder | <code>query-enriched.entities.text:Google&#124;IBM</code> |
| [,](/docs/services/discovery/query-operators.html#and) | Und | `query-enriched.entities.text:Google,IBM` |
| [<=, >=, >, <](/docs/services/discovery/query-operators.html#comparisons) | Numerische Vergleiche |  `enriched_text.sentiment.document.score>0.679`     |
| [^x](/docs/services/discovery/query-operators.html#multiplier) | Bewertungsmultiplikator | `text:IBM^3` |
| [*](/docs/services/discovery/query-operators.html#wildcard) | Platzhalter | `query-enriched_text.concepts.text:pre*` |
| [~n](/docs/services/discovery/query-operators.html#variation) | Zeichenfolgenvariante | `query-enriched_text.entities.text:cat~1` |

## Aggregationen
{: #aggregations}

Aggregationen geben eine Gruppe von Datenwerten zurück. Die folgenden Aggregationen sind verfügbar:

| Aggregation | Beschreibung | Beispiel |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [term](/docs/services/discovery/query-aggregations.html#term) | Zählt identische Werte. | `term(enriched_text.concepts.text,count:10)` |
| [filter](/docs/services/discovery/query-aggregations.html#filter) | Filtert die Ergebnismenge mit einem definierten Muster. | `filter(enriched_text.concepts.text:cloud computing)`
| [nested](/docs/services/discovery/query-aggregations.html#nested) | Beschränkt die Aggregation. | `nested(enriched_text.entities)` |
| [histogram](/docs/services/discovery/query-aggregations.html#histogram) | Intervallbasierte Verteilung. | `histogram(product.price,interval:1)` |
| [timeslice](/docs/services/discovery/query-aggregations.html#timeslice) | Zeitbasierte Verteilung. | `timeslice(last_modified,2day,America/New York)` |
| [top_hits](/docs/services/discovery/query-aggregations.html#top_hits) | Gibt die am höchsten eingestuften Ergebnisdokumente für die aktuelle Aggregation an. | `term(enriched_text.concepts.text).top_hits(10)` |
| [unique_count](/docs/services/discovery/query-aggregations.html#unique_count) | Zählt die eindeutigen Werte für ein Feld in einer Aggregation. | `unique_count(enriched_text.entities.type)` |
| [max](/docs/services/discovery/query-aggregations.html#min) | Gibt den Maximalwert für das angegebene Feld in der Ergebnismenge an. | `max(product.price)` |
| [min](/docs/services/discovery/query-aggregations.html#max) | Gibt den Minimalwert für das angegebene Feld in der Ergebnismenge an. | `min(product.price)` |
| [average](/docs/services/discovery/query-aggregations.html#average) | Gibt den Mittelwert für das angegebene Feld in der Ergebnismenge an. | `average(product.price)` |
| [sum](/docs/services/discovery/query-aggregations.html#sum) | Gibt die Summe aller Felder in der Ergebnismenge an. | `sum(product.price)` |
