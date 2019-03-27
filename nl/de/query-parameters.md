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

# Abfrageparameter
{: #query-parameters}

Der {{site.data.keyword.discoveryfull}}-Service bietet durch Abfragen leistungsfähige Funktionen für die Inhaltssuche. Nachdem Ihr Inhalt hochgeladen und durch den {{site.data.keyword.discoveryshort}}-Service aufbereitet wurde, können Sie Abfragen erstellen und {{site.data.keyword.discoveryshort}} in Ihre eigenen Projekte integrieren oder mit {{site.data.keyword.watson}} Explorer Application Builder eine angepasste Anwendung erstellen. Lesen Sie zur Vorbereitung für die Verwendung von Abfragen zunächst den Abschnitt [Abfragekonzepte](/docs/services/discovery?topic=discovery-query-concepts#query-concepts). Eine vollständige Liste der Parameter enthält die [Abfragereferenz](/docs/services/discovery?topic=discovery-query-reference#parameter-descriptions).
{: shortdesc}

**Suchparameter**

Mithilfe von Suchparametern können Sie Ihre Sammlung durchsuchen, eine Ergebnismenge ermitteln und eine Analyse für die Ergebnismenge durchführen.

Die **Ergebnismenge** ist die Gruppe der Dokumente, die durch die kombinierten Suchvorgänge der Suchparameter ermittelt wurden. Die Ergebnismenge kann deutlich umfangreicher als die zurückgegebenen Ergebnisse sein. Falls eine leere Abfrage ausgeführt wird, entspricht die Ergebnismenge allen Dokumenten in der Sammlung.

## Parameter 'query'
{: #query}

Eine Suche mit dem Parameter 'query' gibt alle Dokumente in Ihrem Datenbestand mit vollständigen Aufbereitungen und dem vollständigen Text in der Reihenfolge ihrer Relevanz zurück. Eine Abfrage schließt außerdem alle Dokumente aus, in denen der Abfrageinhalt nicht erwähnt wird. Derartige Abfragen werden in der [{{site.data.keyword.discoveryshort}}-Abfragesprache geschrieben](/docs/services/discovery?topic=discovery-query-operators#query-operators).

## filter
{: #filter}

Dieser Parameter gibt eine zwischenspeicherbare Abfrage an, die alle Dokumente ausschließt, in denen der Abfrageinhalt nicht erwähnt wird. Ergebnisse der Filtersuche werden **nicht** in der Reihenfolge ihrer Relevanz zurückgegeben. Derartige Abfragen werden in der [{{site.data.keyword.discoveryshort}}-Abfragesprache](/docs/services/discovery?topic=discovery-query-operators#query-operators) geschrieben.

### Unterschiede zwischen den Parametern 'query' und 'filter'
{: #filtervquery}

Falls Sie denselben Suchbegriff für einen kleinen Datenbestand testen, stellen Sie möglicherweise fest, dass die Parameter `filter` und `query` sehr ähnliche (oder sogar identische) Ergebnisse zurückgeben. Es gibt jedoch einen Unterschied zwischen den beiden Parametern.

- Wenn lediglich ein Parameter 'filter' verwendet wird, werden die Suchergebnisse nicht in einer bestimmten Reihenfolge zurückgegeben.
- Wenn lediglich ein Parameter 'query' verwendet wird, werden die Suchergebnise in der Reihenfolge ihrer Relevanz zurückgegeben.

Wenn Sie bei großen Datenbeständen die Rückgabe der Ergebnisse in der Reihenfolge ihrer Relevanz benötigen, sollten Sie die Parameter `filter` und `query` kombinieren, da ihre gemeinsame Verwendung die Leistung verbessert. Dies liegt daran, dass zunächst der Parameter `filter` zur Anwendung kommt und die Ergebnisse zwischengespeichert werden, die danach durch den Parameter `query` in eine Rangordnung gebracht werden. Ein Beispiel für die kombinierte Verwendung von Filtern und Abfragen finden Sie unter [Kombinierte Abfragen erstellen](/docs/services/discovery?topic=discovery-query-concepts#building-combined-queries). Filter können auch in Aggregationen verwendet werden.

Wenn Sie eine Abfrage schreiben, die sowohl einen Parameter `filter` als auch einen Parameter `aggregation`, `query` oder `natural_language_query` enthält, wird zuerst der Parameter `filter` ausgeführt. Anschließend werden alle gegebenenfalls definierten Parameter `aggregation`, `query` oder `natural_language_query` parallel ausgeführt.

Für eine einfache Abfrage geben die Parameter `filter` und `query`, insbesondere bei einem kleinen Datenbestand, häufig genau identische (oder ähnliche) Ergebnisse zurück. Falls ein Aufruf von `filter` und `query` ähnliche Ergebnisse zurückgibt und eine Rückgabe in der Reihenfolge der Relevanz ohne Belang ist, sollte besser eine Filterung verwendet werden, da Filteraufrufe schneller ausgeführt werden und eine Zwischenspeicherung möglich ist. Die Zwischenspeicherung bedeutet, dass Sie bei der nächsten Ausführung dieses Aufrufs - besonders bei einem großen Datenbestand - viel schneller eine Antwort erhalten.

## Parameter 'aggregation'
{: #aggregation}

Aggregationsabfragen geben die Anzahl von Dokumenten zurück, die mit einer Gruppe von Datenwerten übereinstimmen, beispielsweise wichtige Schlüsselwörter, Gesamtstimmung von Entitäten und anderes. Eine vollständige Liste der Aggregationsoptionen enthält die [Tabelle 'Aggregationen'](/docs/services/discovery?topic=discovery-query-aggregations#query-aggregations). Diese Aggregationen werden in der [{{site.data.keyword.discoveryshort}}-Abfragesprache](/docs/services/discovery?topic=discovery-query-operators#query-operators) geschrieben.

## Parameter 'natural_language_query'
{: #nlq}

Bei einer Abfrage in natürlicher Sprache können Sie die Abfrage in natürlicher Sprache ausdrücken, also so, wie sie von einem Endbenutzer in einer dialogorientierten Schnittstelle oder einer Schnittstelle für Text mit freiem Format empfangen werden könnte (z. B. 'IBM Watson im Gesundheitswesen'). Der Parameter verwendet die gesamte Eingabe als Abfragetext. Operatoren werden **nicht** erkannt. Der Parameter `natural_language_query` ermöglicht die Verwendung von Funktionen wie Passagensuche und Relevanztraining. Alle privaten Sammlungen geben in den meisten Fällen eine `confidence`-Bewertung in den Abfrageergebnissen zurück. Details enthält der Abschnitt [Konfidenzbewertung](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence). Die maximale Länge der Abfragezeichenfolge für eine Abfrage in natürlicher Sprache ist `2048`.

**Strukturparameter**

Strukturparameter definieren den Inhalt und den Aufbau der Dokumente in der JSON-Rückgabe. Hierzu gehören die Anzahl der zurückgegebenen Ergebnisse, die Anfangsposition in der Ergebnismenge für die Rückgabe von Dokumenten, die Sortierung der Ergebnismenge, die für jedes Dokument zurückzugebenden Felder, die Einstellung für das Entfernen von Dokumentduplikaten sowie die Einstellung für das Extrahieren von relevanten Passagen aus der Ergebnismenge. Strukturparameter haben keinen Einfluss darauf, aus welchen Dokumenten die gesamte Ergebnismenge besteht.

## Parameter 'count'
{: #count}

Die Anzahl der Dokumente, die in der Antwort zurückgegeben werden soll. Der Standardwert ist `10`. Der maximale Wert für die Summe der Parameter `count` und `offset` in einer einzigen Abfrage beträgt `10000`.

## Parameter 'offset'
{: #offset}

Die Anzahl der Abfrageergebnisse, die am Beginn übersprungen werden sollen. Falls beispielsweise die Gesamtzahl der zurückgegebenen Ergebnisse 10 ist und für die relative Position (offset) der Wert 8 angegeben ist, werden die letzten beiden Ergebnisse zurückgegeben. Der Standardwert ist `0`. Der maximale Wert für die Summe der Parameter `count` und `offset` in einer einzigen Abfrage beträgt `10000`.

## Parameter 'return'
{: #return}

Eine durch Kommas getrennte Liste für den Teil der Dokumenthierarchie, der zurückgegeben werden soll. Gültige Werte sind alle beliebigen Teile der Dokumenthierarchie.

## Parameter 'sort'
{: #sort}

Eine durch Kommas getrennte Liste der Felder im Dokument, nach denen die Sortierung vorgenommen werden soll. Sie können optional eine Sortierrichtung angeben, indem Sie dem Feld das Zeichen `-` (= absteigende Reihenfolge) oder das Zeichen `+` (= aufsteigende Reihenfolge) voranstellen. Die Standardeinstellung für die Sortierrichtung ist die aufsteigende Reihenfolge.

Der Parameter `sort` kann gegenwärtig nur bei der API verwendet werden; in den Tools ist er nicht verfügbar.

## Parameter 'bias'
{: #bias}

Passt die Suchergebnisse an, um bestimmte Ergebnisse zu beeinflussen, z. B. Dokumente, die zuletzt veröffentlicht wurden. Der Parameter `bias` muss entweder auf ein Feld vom Typ `date` oder auf ein Feld vom Typ `number` gesetzt sein, z. B. `bias=publication_date` oder `bias=field_1`.  Wenn ein Feld `date` angegeben wird, werden die zurückgegebenen Ergebnisse auf Feldwerte ausgerichtet, die dem aktuellen Datum näher liegen. Wenn ein Feld `number` angegeben wird, werden die Ergebnisse auf höhere Feldwerte ausgerichtet. Dieser Parameter kann nicht in derselben Abfrage wie der Parameter `sort` verwendet werden.

Der Parameter `bias` steht derzeit nur für die API zur Verfügung; er ist nicht über die Tools verfügbar.

## Parameter 'passages'
{: #passages}

Dieser boolesche Parameter gibt an, ob der Service eine Gruppe mit den relevantesten Passagen aus den Dokumenten zurückgibt, die von einer Abfrage mit Verwendung des Parameters `natural_language_query` zurückgegeben wurden. Die Passagen werden durch hoch entwickelte Watson-Algorithmen generiert, mit denen die besten Textpassagen aus allen durch die Abfrage zurückgegebenen Dokumenten ermittelt werden. Der Standardwert ist `false`.

Der Parameter `passages` kann nur für private Sammlungen verwendet werden. Seine Verwendung für die Sammlung '{{site.data.keyword.discoverynewsfull}}' ist nicht möglich.
{: tip}

{{site.data.keyword.discoveryshort}} versucht mittels Erkennung von Satzgrenzen, Passagen zurückzugeben, deren Anfang der Beginn eines Satzes und deren Ende das Satzende ist. Hierzu wird zunächst nach Passagen gesucht, deren Länge ungefähr dem im [Parameter `passages.characters`](/docs/services/discovery?topic=discovery-query-parameters#passages_characters) angegebenen Wert entspricht (Standardwert ist `400`). Anschließend wird jede Passage bis auf das Doppelte der angegebenen Länge erweitert, damit vollständige Sätze zurückgegeben werden. Falls der Parameter `passages.characters` auf einen kleinen Wert festgelegt ist und/oder die Sätze in Ihren Dokumenten sehr lang sind, gibt es möglicherweise keine Satzgrenzen, die so eng sind, dass der vollständige Satz ohne Überschreitung des doppelten Wertes für die angeforderte Länge zurückgegeben werden kann. In diesem Fall bleibt {{site.data.keyword.discoveryshort}} innerhalb der Grenze gemäß dem doppelten Wert des Parameters `passages.characters`; die zurückgegebene Passage enthält somit nicht den gesamten Satz und der Anfang und/oder das Ende fehlt.

Da sich bei einer Anpassung der Satzgrenzen die Größe der Passagen erhöht, ergibt sich eine erhebliche Vergrößerung der durchschnittlichen Passagenlänge. Falls der Anzeigebereich Ihrer Anwendung begrenzt ist, kann es sinnvoll sein, einen kleineren Wert für den Parameter `passages.characters` festzulegen und/oder die von {{site.data.keyword.discoveryshort}} zurückgegebenen Passagen abzuschneiden. Die Erkennung von Satzgrenzen funktioniert bei allen unterstützten Sprachen und verwendet sprachspezifische Logik.

Der Parameter `passages` gibt passende Passagen (`passage_text`) und die Bewertung (`score`), die Dokument-ID (`document_id`), den Namen des Feldes, aus dem die Passage extrahiert wurde (`field`) sowie das Start- und Endezeichen des Passagentextes innerhalb des Feldes (`start_offset` und `end_offset`) zurück. Dies ist im folgenden Beispiel gezeigt. Die Abfrage ist oben im Beispiel dargestellt.

```bash
 curl -u "apikey":"{wert_des_api-schlüssels}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/collections/{sammlungs-id}/query?version=2017-06-25&natural_language_query='Hybrid%20cloud%20companies'&passages=true"
```
{: pre}

Die JSON-Rückgabe besitzt das folgende Format:

```json
 {
   "matching_results":2,
   "passages":[
     {
       "document_id":"ab7be56bcc9476493516b511169739f0",
       "passage_score":15.230205287402338,
       "passage_text":"a privately held company that provides hybrid cloud recovery, cloud migration and business continuity software for enterprise data centers and cloud infrastructure."
       "start_offset":120
       "end_offset":300
       "field":"text"       
     },
     {
       "passage_text":"Disaster Recovery Services for Hybrid Cloud</title></head>\n<body>\n\n\n<p>Published: Thu, 27 Oct 2016 07:01:21 GMT</p>\n"
       "passage_score":10.153470191601558,
       "document_id":"fbb5dcb4d8a6a29f572ebdeb6fbed20e",              
       "start_offset":70
       "end_offset":120
       "field":"html"
     },
  ...
```
{: codeblock}                        

### Parameter 'passages.fields'
{: #passages_fields}

Eine durch Kommas getrennte Liste der Felder im Index, aus denen die Passagen entnommen werden. Falls dieser Parameter nicht angegeben ist, werden alle Felder der höchsten Ebene einbezogen.

### Parameter 'passages.count'
{: #passages_count}

Die maximale Anzahl der zurückzugebenden Passagen. Die Suche gibt weniger Passagen zurück, wenn die gefundene Gesamtzahl diesen Wert unterschreitet. Der Standardwert ist `10`. Der maximale Wert ist `100`.

### Parameter 'passages.characters'
{: #passages_characters}

Die ungefähre Anzahl der Zeichen, die jede Passage umfassen sollte. Der Standardwert ist `400`. Der Mindestwert ist `50`. Der maximale Wert ist `2000`. Zurückgegebene Passagen können bis zu doppelt so lang wie die angeforderte Länge sein (sofern erforderlich), damit sie an Satzgrenzen beginnen und enden.

## Parameter 'highlight'
{: #highlight}

Dieser boolesche Parameter gibt an, ob die zurückgegebene Ausgabe ein Objekt `highlight` enthält, in dem die Schlüssel die Feldnamen und die Werte die Arrays sind, die Segmente eines mit der Abfrage übereinstimmenden Textes enthalten, hervorgehoben durch den HTML-Tag `*`.

In der Ausgabe ist das Objekt `highlight` nach dem Objekt `enriched_text` angegeben. Dies ist im folgenden Beispiel gezeigt.

```bash
curl -u "apikey":"{wert_des_api-schlüssels}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/collections/{sammlungs-id}/query?version=2017-06-25&natural_language_query=Hybrid%20cloud%20companies&highlight=true"
```
{: pre}

Die JSON-Rückgabe besitzt das folgende Format:

```json
{
   "highlight": {
     "extracted_metadata.title": [
       "IBM to Acquire Sanovi Technologies to Expand Disaster Recovery Services for <em>Hybrid</em> <em>Cloud</em>"
       ],
     "enriched_text.concepts.text": [
       "Privately held <em>company</em>",
       "<em>Cloud</em> computing"
       ],
     "text": [
       " Sanovi Technologies, a privately held <em>company</em> that provides <em>hybrid</em> <em>cloud</em> recovery, <em>cloud</em> migration",
       "IBM to Acquire Sanovi Technologies to Expand Disaster Recovery Services for <em>Hybrid</em> <em>Cloud</em>\n\nPublished",
       " undergoing digital and <em>hybrid</em> <em>cloud</em> transformation.\n\nURL: http://www.ibm.com/press/us/en/pressrelease/50837.wss",
       " and business continuity software for enterprise data centers and <em>cloud</em> infrastructure. Adding"
       ],
     "enriched_text.categories.label": [
       "/business and industrial/<em>company</em>/bankruptcy"
       ],
     "enriched_text.entities.type": [
       "<em>Company</em>"
       ],
     "html": [
       " Technologies, a privately held <em>company</em> that provides <em>hybrid</em> <em>cloud</em>\n recovery, <em>cloud</em> migration and business",
       " Disaster Recovery Services for <em>Hybrid</em> <em>Cloud</em></title></head>\n<body>\n\n\n<p>Published: Thu, 27 Oct 2016 07:01",
       " digital and <em>hybrid</em> <em>cloud</em> transformation.</p>\n<p>URL: http://www.ibm.com/press/us/en/pressrelease/50837.wss</p>\n\n\n\n</body></html>",
       " continuity software for \nenterprise data centers and <em>cloud</em> infrastructure. Adding these \ncapabilities"
       ]
   }
}
```
{: codeblock}

## Parameter 'deduplicate'
{: #deduplicate}

 Diese Betafunktionalität schließt Dokumentduplikate aus Abfrageergebnissen für die Sammlung '{{site.data.keyword.discoverynewsfull}}' aus. Basis hierfür ist der Wert des Feldes `title`. Weitere Informationen enthält der Abschnitt [Doppelte Dokumente aus Abfrageergebnissen ausschließen](/docs/services/discovery?topic=discovery-query-parameters#deduplication).

### Parameter 'deduplicate.field'
{: #deduplicate_field}

Diese Betafunktionalität schließt Dokumentduplikate aus Abfrageergebnissen aus. Basis hierfür ist das anstelle von `{feld}` angegebene Feld. Weitere Informationen enthält der Abschnitt [Doppelte Dokumente aus Abfrageergebnissen ausschließen](/docs/services/discovery?topic=discovery-query-parameters#deduplication).

### Doppelte Dokumente aus Abfrageergebnissen ausschließen
{: #deduplication}

Falls Sie die Sammlung '{{site.data.keyword.discoverynewsfull}}' abfragen oder Ihre private Datensammlung mehrere identische (oder nahezu identische) Dokumente enthält, können Sie mithilfe der Dokumentdeduplizierung einen Großteil dieser Dokumente aus den Abfrageergebnissen ausschließen.

**Hinweis:** Die Dokumentdeduplizierung wird gegenwärtig nur als Betafunktionalität unterstützt. Weitere Informationen enthält der Abschnitt [Features als Betaversion](/docs/services/discovery?topic=discovery-release-notes#beta-features) in den Releaseinformationen. Dieses Beta-Feature wird derzeit nur in Englisch unterstützt. Details hierzu finden Sie unter [Sprachunterstützung](/docs/services/discovery?topic=discovery-language-support#feature-support).

**Hinweis:** Jede Abfrage wird unabhängig dedupliziert. Eine offsetübergreifende Deduplizierung wird daher nicht unterstützt.

Die Deduplizierung wird nach der Extraktion von `Passagen` und der Berechnung von Aggregationen vorgenommen. Wenn Sie den Parameter `passages` in Ihre Abfrage einbeziehen, werden daher Passagen aus allen Dokumenten in den Abfrageergebnissen zurückgegeben, bevor die Deduplizierung stattfindet. Wenn Sie eine Abfrage zusammen mit einer Aggregation ausführen, enthalten die Aggregationsergebnisse Daten aus allen zurückgegebenen Dokumenten, bevor die Deduplizierung vorgenommen wird.

Die Deduplizierung wird nur für zurückgegebene Felder ausgeführt. Falls Sie `return=` in Ihrer Abfrage angeben, beziehen Sie das Feld ein, auf dessen Grundlage die Deduplizierung erfolgen soll.

Zur Anwendung der Deduplizierung verwenden Sie die folgende Syntax in Ihrer Abfrage.  Ersetzen Sie `{feld}` durch den Namen des Feldes, auf dessen Grundlage die Deduplizierung ausgeführt werden soll. Der für `{feld}` angegebene Wert muss eine Zeichenfolge sein, z. B. `title`.

```
&deduplicate.field={field}
```
{: codeblock}

Bei der Deduplizierung enthält die JSON-Antwort die Angabe `"duplicates_removed": x`; hierbei steht `x` für die Anzahl der Dokumente, die aus den Ergebnissen entfernt wurden.

#### Dokumente in Watson Discovery News deduplizieren
{: #deduplicatewds}

Neue Artikel können für mehrere Nachrichtenausgaben syndiziert werden. {{site.data.keyword.discoverynewsfull}} nimmt alle diese Artikel auf, was zu doppelten Artikeln führt. Dies bedeutet, dass eine Abfrage von {{site.data.keyword.discoverynewsfull}} potenziell identische oder nahezu identische Artikel in Abfrageergebnissen zurückgibt. Bei Verwendung der Deduplizierung werden die meisten doppelten Artikel aus Ihren Suchabfragen entfernt.

{{site.data.keyword.discoveryshort}} dedupliziert mittels einer Suche nach ähnlichen Übereinstimmungen für das Feld `title`; es muss daher kein Feld angegeben werden.

Zur Anwendung der Deduplizierung verwenden Sie den folgenden Parameter in Ihrer Abfrage. Diese Abfrage dedupliziert automatisch anhand des Feldes `title` in {{site.data.keyword.discoverynewsfull}}.

```bash
&deduplicate=true
```
{: codeblock}

Falls Sie für die Deduplizierung ein anderes Feld als `title` zugrunde legen wollen, verwenden Sie in Ihrer Abfrage die folgende Syntax. Ersetzen Sie `{feld}` durch den Namen des Feldes, auf dessen Grundlage die Deduplizierung ausgeführt werden soll. Der für `{feld}` angegebene Wert muss eine Zeichenfolge sein.

```bash
&deduplicate.field={field}
```
{: codeblock}

## Parameter 'collection_ids'
{: #collection_ids}

Eine durch Kommas getrennte Liste von Sammlungen in derselben Umgebung, die abgefragt werden. Dieser Parameter ist nur bei Verwendung der Methode `environments/{umgebungs-id}/query?` verfügbar. Weitere Informationen finden Sie unter [Mehrere Sammlungen abfragen](/docs/services/discovery?topic=discovery-query-concepts#multiple-collections).

```bash
&collection_ids={id1},{id2}
```
{: codeblock}

## Parameter 'similar'
{: #similar}

Die Dokumentähnlichkeit identifiziert Dokumente, die den Dokumenten ähneln, die in den Parametern `similar.document_ids` aufgelistet sind. Dies kann noch weiter optimiert werden, indem Sie angeben, welche Felder für einen Vergleich mithilfe der Parameter `similar.fields` herangezogen werden sollen. Der Standardwert ist `false`. Weitere Informationen finden Sie unter [Dokumentähnlichkeit](/docs/services/discovery?topic=discovery-query-concepts#doc-similarity).

```bash
&similar=true
```
{: codeblock}

### Parameter 'similar.document_ids'
{: #similar_document_ids}

Eine durch Kommas getrennte Liste der Dokument-IDs, die als Grundlage für die Suche nach ähnlichen Dokumenten verwendet wird. Dieser Parameter ist erforderlich, wenn der Parameter `similar` auf `true` gesetzt ist.

```bash
&similar.document_ids={id1},{id2}
```
{: codeblock}

### Parameter 'similar.fields'
{: #similar_fields}

Eine optionale, durch Kommas getrennte Liste der Felder, die zum Vergleichen von Dokumenten verwendet werden, um ähnliche Dokumente zu finden. Dieser Parameter kann nur in Verbindung mit dem Parameter `similar.document_ids` verwendet werden.

```bash
&similar.fields={field1},{field2}
```
{: codeblock}
