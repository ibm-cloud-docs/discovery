---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-14"

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

# Tipps für das Relevanztraining
{: #relevancy-tips}

 Dieser Abschnitt enthält Antworten auf häufig gestellte Fragen zum Training einer Sammlung sowie Erläuterungen für häufige Fehlernachrichten und Warnungen. Weitere Informationen zum Verbessern der Relevanz bei Abfragen in natürlicher Sprache finden Sie unter [Ergebnisrelevanz mithilfe der Tools verbessern](/docs/services/discovery/train-tooling.html) und [Ergebnisrelevanz mithilfe der API verbessern](/docs/services/discovery/train.html).
{: shortdesc}

## Basiswissen über das Training

Nachfolgend finden Sie Antworten auf häufig gestellte Fragen zum Training einer Sammlung.

### Woran erkenne ich, ob mein System trainiert wird?

Prüfen Sie mit dem API-Befehl zum [Auflisten der Sammlungsdetails ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/discovery/api/v1/?curl#list-collection-details){: new_window}, ob Ihr System trainiert wurde.  

```bash
curl -u "{benutzername}":"{kennwort}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/collections/{sammlungs-id}?version=2017-11-07"
```
{: pre}

Beispielantwort:

```json
{
  "training": {
    "total_examples": 54,
    "available": true,
    "processing": false,
    "minimum_queries_added": true,
    "minimum_examples_added": true,
    "sufficient_label_diversity": false,
    "notices": 13,
    "successfully_trained": "2017-02-08T14:18:22.786Z",
    "data_updated": "2017-02-10T14:18:22.786Z"
    }
}
```

Damit die Voraussetzungen für das Training erfüllt sind, muss für alle folgenden Felder der Wert `true` zurückgegeben werden:
- `minimum_queries_added`
- `minimum_examples_added`
- `sufficient_label_diversity`   

Die Felder der Antwort haben die folgende Bedeutung:
- `successfully_trained` gibt den Zeitpunkt für die letzte erfolgreiche Ausführung des Trainings an.
- `available: true` gibt an, dass das Training stattgefunden hat und ein Modell verfügbar ist.
- `processing: true` gibt an, dass das Training gerade ausgeführt wird.
-  Falls das für `data_updated` angegebene Datum nach dem für `successfully_trained` angegebenen Datum liegt, wurde nach einem kürzlich erfolgten Datenupload ein neues Modell noch nicht trainiert.  

### Wie prüfe ich, ob Fehler und Warnungen vorliegen?

Fehler oder Warnungen können Sie mit der [API für Abfragehinweise ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-notices){: new_window} anzeigen.  

```bash
curl -u "{benutzername}":"{kennwort}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/collections/{sammlungs-id}/notices?version=2017-11-07"
```
{: pre}

Weitere API-Operationen sind im Abschnitt [Andere Operationen für Trainingsdatenabfragen ausführen](/docs/services/discovery/train.html#training-data-operations) aufgelistet.

### Wie interpretierene ich die Konfidenzbewertung (`confidence`), die in Ergebnissen für Abfragen in natürlicher Sprache nach dem Training angezeigt wird?

Trainierte Sammlungen geben im Feld `confidence` des Ergebnisses für eine Abfrage in natürlicher Sprache eine Konfidenzbewertung zurück. Diese Zahl für das Feld `confidence` wird danach berechnet, wie relevant das Ergebnis im Vergleich zum trainierten Modell ist. Die Bewertung der `Konfidenz` ist **nicht** mit der `Bewertung` identisch. Weitere Informationen finden Sie unter [Konfidenzbewertungen](/docs/services/discovery/train-tooling.html#confidence).  

## Fehler und Warnungen interpretieren

Nachfolgend werden gängige Fehlernachrichten und Warnungen erläutert.

### Warnung: `Invalid training data found: The document was not returned in the top 100 search results for the given query, and will not be used for training`

Diese Warnung wird dadurch verursacht, dass die `Dokument-IDs` in Ihren Trainingsdaten nicht mit den `Dokument-IDs` in einer Suche übereinstimmen, die für die Sammlung ausgeführt wurde. Sie sollten Ihre Abfragen überprüfen und sicherstellen, dass die `Dokument-ID` des Dokuments, das Sie einstufen wollen, in den wichtigsten 100 Ergebnissen für diese Abfrage zurückgegeben wird. Wenn dies nicht der Fall ist, ist es sinnvoll, die beiden folgenden Punkte zu überprüfen:  

- Falls das Dokument nicht unter den ersten 100 zurückgegeben wird, ist es möglicherweise kein gutes Beispiel für ein qualitätiv hochwertiges Ergebnis. Es kann sinnvoll sein, die Auswahl dieses Dokuments zu überdenken.  

- Falls das Dokument überhaupt nicht zurückgegeben wird, sollten Sie prüfen, warum dies der Fall ist, und ermitteln, ob das Dokument Text enthält, der mit Teilen der Abfrage übereinstimmt.  

**Hinweis:** Diese Warnung gibt an, dass möglicherweise eine oder mehrere ungeeignete Abfragen vorhanden sind; sie ist kein Anzeichen dafür, dass das Training nicht stattfindet.  

### Fehler: `Invalid training data found: Syntax error when parsing query`

- Dies bedeutet, dass ein Problem hinsichtlich der eigentlichen Abfragesyntax vorliegt. Überprüfen Sie, ob die Abfragen Ergebnisse zurückgeben und keinen Syntaxfehler auslösen. Dieser Fehler kann nur dann auftreten, wenn Sie einen Filter zu einer Abfrage in natürlicher Sprache hinzugefügt haben.

### Fehler: `Invalid training data found: The query string provided exceeds the maximum length, please provide a shorter one`

- Die maximale Länge der Abfragezeichenfolge ist `X`. Sie müssen die angegebene Abfrage verkürzen. Die Aufnahme eines Filters in Ihre Abfrage ist eine der möglichen Umgehungen für dieses Problem.  

### Fehler: `This collection cannot be trained: your plan does not support training on this many top-level text fields.`

- Dieser Fehler tritt nur bei Verwendung eines `Lite`-Plans auf. Das Training kann für maximal `X` Textfelder der höchsten Ebene durchgeführt werden. Textfelder der höchsten Ebene sind Felder, die nicht unter einem andeeren Feld verschachtelt sind. Das Training wird nur für die Felder der höchsten Ebene durchgeführt und die Anzahl der Felder, die im Trainingsprozess verwendet werden können, ist begrenzt.  

### Fehler: `Training data quality standards not met: You will need additional training queries with labeled examples. (To be considered for training, each example must appear in the top 100 search results for its query.)`

- Dieser Fehler bedeutet, dass Sie weitere Trainingsdaten hinzufügen müssen, damit das Training erfolgreich durchgeführt werden kann. Sie benötigen mindestens 49 endeutige Trainingabfragen und für jede Abfrage muss es mindestens ein eingestuftes Dokument geben. Minimum ist hier nicht gleich Optimum; die Größe der Sammlung und weitere Faktoren können die Anzahl der Trainingsbeispiele erhöhen, die zur Erfüllung des Minimums erforderlich sind.  

### Fehler: `Training data quality standards not met: Insufficient number of unique training queries. Expected at least n, but found m.`

- Damit die Mindestvoraussetzungen für das Training erfüllt sind, benötigen Sie mindestens 49 eindeutige Trainingsabfragen und für jede Abfrage muss es mindestens ein eingestuftes Dokument geben. Falls mehr als 49 Abfragen vorhanden sind und Sie diese Fehlernachricht weiterhin empfangen, sollten Sie prüfen, ob die Hinweise weitere Fehler enthalten.  

### Fehler: `Training data quality standards not met: No documents found with non-zero relevance labels.`

- Die Trainingsdaten benötigen ausreichend gekennzeichnete Daten, die angeben, welche Dokumente einen hohen Wert besitzen. Dies bedeutet, dass einige Dokumente mit einem anderen Wert als Null eingestuft sein müssen. Bei Verwendung der Discovery-Tools müssen Sie einige Dokumente als relevant einstufen (`10`); bei Verwendung der API müssen Sie einige Dokumente mit `1` oder höher kennzeichnen.   

### Fehler: `Training data quality standards not met: Training examples have no relevance label variety for X queries.`

- Eine der Voraussetzungen für das Training ist eine ausreichende Diversität der Kennzeichnungen. Wenn Sie ein gut trainiertes System erzielen wollen, sollten Sie daher nicht nur Dokumente mit der bestmöglichen Relevanz hinzufügen, sondern auch Dokumente, die eine zufriedenstellende Relevanz bieten. Anders ausgedrückt ist es bei einer Skala von 0 bis 4 hilfreich, neben den mit 4 bewerteten Dokumenten auch Dokumente mit der Einstufung 2 und 3 hinzuzufügen. (Falls Sie die Discovery-Tools verwenden, werden Dokumente entweder als relevant (`10`) oder als nicht relevant (`0`) eingestuft). Mindestens 25% der Fragen müssen eine gewisse Vielfalt der Kennzeichnungen besitzen.   
