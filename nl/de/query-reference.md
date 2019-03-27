---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-04"

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

# Abfragereferenz
{: #query-reference}

Der {{site.data.keyword.discoveryfull}}-Service bietet durch Abfragen leistungsfähige Funktionen für die Inhaltssuche. Nachdem Ihr Inhalt hochgeladen und durch den {{site.data.keyword.discoveryshort}}-Service aufbereitet wurde, können Sie Abfragen erstellen und {{site.data.keyword.discoveryshort}} in Ihre eigenen Projekte integrieren oder mit {{site.data.keyword.watson}} Explorer Application Builder eine angepasste Anwendung erstellen.
{: shortdesc}

Weitere Informationen zum Schreiben von Abfragen enthalten die folgenden Abschnitte:
- [Einführung in die Ausführung von Abfragen](/docs/services/discovery?topic=discovery-getting-started-with-querying#getting-started-with-querying)
- [Abfragekonzepte](/docs/services/discovery?topic=discovery-query-concepts#query-concepts)

## Parameterbeschreibungen
{: #parameter-descriptions}

Mithilfe von Abfrageparametern können Sie Ihre Sammlung durchsuchen, eine Ergebnismenge ermitteln und eine Analyse für die Ergebnismenge durchführen.


| Parameter | Beschreibung | Beispiel |
|:-------------------:|------------------------------------------------------------|--------------------------------|
|** Suchparameter **|  |  |
| [query](/docs/services/discovery?topic=discovery-query-parameters#query) | Eine Suche in Abfragesprache mit Einstufung nach übereinstimmenden Dokumenten. | `query=bees` |
| [filter](/docs/services/discovery?topic=discovery-query-parameters#filter) | Eine Suche in Abfragesprache ohne Einstufung nach übereinstimmenden Dokumenten. | `filter=bees` |
| [natural_language_query](/docs/services/discovery?topic=discovery-query-parameters#nlq) | Eine Suche in natürlicher Sprache mit Einstufung nach übereinstimmenden Dokumenten. | `natural_language_query="How do bees fly"` |
| [aggregation](/docs/services/discovery?topic=discovery-query-parameters#aggregation) | Eine statistische Abfrage der Ergebnismenge. | `aggregation=term(enriched_text.entities.type)` |
| **Strukturparameter** | | |
| [count](/docs/services/discovery?topic=discovery-query-parameters#count) | Die Anzahl der zurückzugebenden Dokumente im Ergebnis (`result`). | `count=15` |
| [offset](/docs/services/discovery?topic=discovery-query-parameters#offset) | Die Anzahl der Ergebnisse, die vor der Rückgabe von Dokumenten aus der Ergebnismenge in `result` ignoriert werden sollen. | `offset=100` |
| [return](/docs/services/discovery?topic=discovery-query-parameters#return) | Die Liste der zurückzugebenden Felder. | `return=title,url` |
| [sort](/docs/services/discovery?topic=discovery-query-parameters#sort) | Das Feld, nach dem die Ergebnismenge sortiert werden soll. | `sort=enriched_text.sentiment.document.score` |
| [bias](/docs/services/discovery?topic=discovery-query-parameters#bias) | Das Feld, für das Ergebnisse beeinflusst werden sollen. | `bias=publication_date` |
| [passages.fields](/docs/services/discovery?topic=discovery-query-parameters#passages_fields) | Die Felder, aus denen Passagen extrahiert werden sollen. | `passages=true&passages.fields=text,abstract,conclusion` |
| [passages.count](/docs/services/discovery?topic=discovery-query-parameters#passages_count) | Die Anzahl der zurückzugebenden Passagen. | `passages=true&passages.count=6` |
| [passages.characters](/docs/services/discovery?topic=discovery-query-parameters#passages_characters) | Die Länge der Passagen. | `passages=true&passages.characters=144` |
| [highlight](/docs/services/discovery?topic=discovery-query-parameters#highlight) | Hebt Übereinstimmungen mit der Abfrage hervor. | `highlight=true` |
| [deduplicate](/docs/services/discovery?topic=discovery-query-parameters#deduplicate) | Dedupliziert aus {{site.data.keyword.discoverynewsfull}} zurückgegebene Ergebnisse. | `deduplicate=true` |
| [deduplicate.field](/docs/services/discovery?topic=discovery-query-parameters#deduplicate_field) | Dedupliziert zurückgegebene Ergebnisse auf der Basis eines Feldes. | `deduplicate.field=title` |
| [collection_ids](/docs/services/discovery?topic=discovery-query-parameters#collection_ids) | Fragt mehrere Sammlungen ab. | `collection_ids={1},{2},{3}` |
| [similar](/docs/services/discovery?topic=discovery-query-parameters#similar) | Ermöglicht die Suche nach ähnlichen Dokumenten. | `similar=true` |
| [similar.document_ids](/docs/services/discovery?topic=discovery-query-parameters#similar_document_ids) | Gibt an, für welche Dokumente ähnliche Dokumente gesucht werden sollen. | `similar.document_ids={id1},{id2}` |
| [similar.fields](/docs/services/discovery?topic=discovery-query-parameters#similar_fields) | Gibt an, welche Felder bei der Suche nach ähnlichen Dokumenten verglichen werden sollen. | `similar.fields=text,title` |

### Einschränkungen für Abfragen
{: #query-limitations}

Feldnamen, die Folgendes enthalten, können nicht abgefragt werden:
- Numerische Zeichen (`0 - 9`) im Suffix für den Feldnamen (z. B. `extracted-content2`).
- Die Zeichen `_`, `+` und `-` im Präfix im Feldnamen (`field_name`) (z. B. `+extracted-content`).
- Die Zeichen `.`, `,` und `:` im Feldnamen (`field_name`) (z. B. `new:extracted-content`)

## Operatoren
{: #operators}

Operatoren trennen die einzelnen Bestandteile einer Abfrage voneinander. Die folgenden Operatoren sind verfügbar:

| Operator | Beschreibung | Beispiel |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [.](/docs/services/discovery?topic=discovery-query-operators#delimiter) | JSON-Begrenzer | `enriched_text.concepts.text` |
| [:](/docs/services/discovery?topic=discovery-query-operators#includes) | Enthält | `text:computer` |
| [::](/docs/services/discovery?topic=discovery-query-operators#match) | Exakte Übereinstimmung | `title::"Query building"` |
| [:!](/docs/services/discovery?topic=discovery-query-operators#notinclude) | Enthält nicht | `text:!computer` |
| [::!](/docs/services/discovery?topic=discovery-query-operators#notamatch) | Keine exakte Übereinstimmung | `text::!winter` |
| [\\](/docs/services/discovery?topic=discovery-query-operators#escape) | Escapezeichen | `title::"Dorothy said: \"There's no place like home\""` |
| [""](/docs/services/discovery?topic=discovery-query-operators#phrase) | Ausdrucksabfrage | `enriched_text.concepts.text:"IBM Watson"` |
| [(), \[\]](/docs/services/discovery?topic=discovery-query-operators#nestedquery) | Verschachtelte Gruppierung | `filter-entities:(text:Turkey,type:Location)` |
| [<code>&#124;</code>](/docs/services/discovery?topic=discovery-query-operators#or) | oder | <code>query-enriched.entities.text:Google&#124;IBM</code> |
| [,](/docs/services/discovery?topic=discovery-query-operators#and) | und | `query-enriched.entities.text:Google,IBM` |
| [<=, >=, >, <](/docs/services/discovery?topic=discovery-query-operators#comparisons) | Numerische Vergleiche |  `enriched_text.sentiment.document.score>0.679`     |
| [^x](/docs/services/discovery?topic=discovery-query-operators#multiplier) | Bewertungsmultiplikator | `text:IBM^3` |
| [*](/docs/services/discovery?topic=discovery-query-operators#wildcard) | Platzhalter | `query-enriched_text.concepts.text:pre*` |
| [~n](/docs/services/discovery?topic=discovery-query-operators#variation) | Zeichenfolgenvariante | `query-enriched_text.entities.text:cat~1` |
| [:*](/docs/services/discovery?topic=discovery-query-operators#exists) | Ist vorhanden | `title:*` |
| [!*](/docs/services/discovery?topic=discovery-query-operators#dnexist) | Ist nicht vorhanden | `title!*` |

## Aggregationen
{: #aggregations}

Aggregationen geben eine Gruppe von Datenwerten zurück. Die folgenden Aggregationen sind verfügbar:

| Aggregation | Beschreibung | Beispiel |
|:-------------------:|------------------------------------------------------------|--------------------------------|
| [term](/docs/services/discovery?topic=discovery-query-aggregations#term) | Zählt identische Werte. | `term(enriched_text.concepts.text,count:10)` |
| [filter](/docs/services/discovery?topic=discovery-query-aggregations#aggfilter) | Filtert die Ergebnismenge mit einem definierten Muster. | `filter(enriched_text.concepts.text:cloud computing)`
| [nested](/docs/services/discovery?topic=discovery-query-aggregations#nested) | Beschränkt die Aggregation. | `nested(enriched_text.entities)` |
| [histogram](/docs/services/discovery?topic=discovery-query-aggregations#histogram) | Intervallbasierte Verteilung. | `histogram(product.price,interval:1)` |
| [timeslice](/docs/services/discovery?topic=discovery-query-aggregations#timeslice) | Zeitbasierte Verteilung. | `timeslice(last_modified,2day,America/New York)` |
| [top_hits](/docs/services/discovery?topic=discovery-query-aggregations#top_hits) | Gibt die am höchsten eingestuften Ergebnisdokumente für die aktuelle Aggregation an. | `term(enriched_text.concepts.text).top_hits(10)` |
| [unique_count](/docs/services/discovery?topic=discovery-query-aggregations#unique_count) | Zählt die eindeutigen Werte für ein Feld in einer Aggregation. | `unique_count(enriched_text.entities.type)` |
| [max](/docs/services/discovery?topic=discovery-query-aggregations#max) | Gibt den Maximalwert für das angegebene Feld in der Ergebnismenge an. | `max(product.price)` |
| [min](/docs/services/discovery?topic=discovery-query-aggregations#min) | Gibt den Minimalwert für das angegebene Feld in der Ergebnismenge an. | `min(product.price)` |
| [average](/docs/services/discovery?topic=discovery-query-aggregations#average) |Gibt den Mittelwert für das angegebene Feld in der Ergebnismenge an. | `average(product.price)` |
| [sum](/docs/services/discovery?topic=discovery-query-aggregations#sum) | Gibt die Summe aller Felder in der Ergebnismenge an. | `sum(product.price)` |
