---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-06"

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

# Ergebnisrelevanz mithilfe der Tools verbessern

Die Relevanz der Ergebnisse von Abfragen in natürlicher Sprache kann im {{site.data.keyword.discoveryfull}}-Service mit einem Training verbessert werden. Sie können das Training für Ihre privaten Sammlungen entweder mit den {{site.data.keyword.discoveryshort}}-Tools oder den {{site.data.keyword.discoveryshort}}-APIs durchführen. Wenn Sie die APIs verwenden möchten, lesen Sie den Abschnitt [Relevanz von Abfrageergebnissen mithilfe der API verbessern](/docs/services/discovery/train.html).
{: shortdesc}

Das Relevanztraining ist optional. Falls die Ergebnisse Ihrer Abfragen Ihren Anforderungen entsprechen, ist kein weiteres Training erforderlich. Eine Übersicht über den Aufbau von Anwendungsfällen für das Training enthält der Blogbeitrag [How to get the most out of Relevancy Training ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window}.

Um Watson zu trainieren, müssen Sie Folgendes ausführen:

  -   Sie müssen Beispielabfragen angeben, die repräsentativ für die von den Benutzern eingegebenen Abfragen sind.
  -   Sie müssen Einstufungen angeben, um festzulegen, welche Ergebnisse für jede Abfrage relevant sind und welche nicht.

Nachdem Watson ausreichend Eingabe für das Training erhalten hat, werden anhand der Informationen, die Sie über die Qualität - also gut oder schlecht - der einzelnen Ergebnisse für jede Abfrage bereitgestellt haben, weitere Erkenntnisse über Ihre Sammlung ermittelt. Watson memoriert nicht einfach nur, sondern lernt aus den speziellen Informationen zu einzelnen Abfragen und wendet die Muster, die erkannt wurden, auf alle neuen Abfragen an. Hierzu werden Watson-Verfahren für das maschinelle Lernen verwendet, die Signale in Inhalt und Fragestellungen erkennen. Nachdem das Training angewendet wurde, ordnet {{site.data.keyword.discoveryshort}} die Abfrageergebnisse neu an und zeigt die relevantesten Ergebnisse an erster Stelle an. Je mehr Trainingsdaten Sie hinzufügen, desto genauer sollten die Abfrageergebnisse durch {{site.data.keyword.discoveryshort}} sortiert werden.

**Hinweis:** Das Relevanztraining ist gegenwärtig nur auf Abfragen in natürlicher Sprache für private Sammlungen anwendbar. Es ist nicht für die Verwendung bei strukturierten Abfragen in der {{site.data.keyword.discoveryshort}}-Abfragesprache gedacht. Weitere Informationen zur {{site.data.keyword.discoveryshort}}-Abfragesprache finden Sie unter [Abfragekonzepte](/docs/services/discovery/using.html).

Sammlungen, für die ein Training durchgeführt wurde, geben im Ergebnis für eine Abfrage in natürlicher Sprache eine Konfidenzbewertung (Feld `confidence`) zurück. Details enthält der Abschnitt [Konfidenzbewertung](/docs/services/discovery/train-tooling.html#confidence).

Unter [Anforderungen an Trainingsdaten](/docs/services/discovery/train.html#reqs) finden Sie die Mindestanforderungen für das Training sowie die Trainingsbegrenzungen.

Unter [Nutzungsüberwachung](/docs/services/discovery/feedback.html) finden Sie Details zur Nutzungsüberwachung und zur Verwendung der Daten, um Ihre Anwendungen besser verstehen und verbessern zu können.

## Abfragen hinzufügen und Relevanz der Ergebnisse einstufen
{: #results}

Das Training besteht aus drei Teilen, nämlich einer Abfrage in natürlicher Sprache, den Ergebnissen der Abfrage und den Einstufungen, die Sie auf diese Ergebnisse anwenden.

1.  Es gibt zwei Möglichkeiten für den Zugriff auf die Trainingsseite in den {{site.data.keyword.discoveryshort}}-Tools:
    - Klicken Sie für eine einzelne Sammlung in der Anzeige **Abfragen erstellen** in der rechten oberen Ecke auf **Watson zur Ergebnisverbesserung trainieren**. Um das Training zu starten, ist es nicht erforderlich, eine Abfrage in der Anzeige **Abfragen erstellen** einzugeben. 
    - Über das Leistungsdashboard. Klicken Sie auf das Symbol **Datenmetriken anzeigen** auf der linken Seite, um das Dashboard zu öffnen. Sie werden aufgefordert, eine Sammlung auszuwählen, die Sie trainieren möchten.
1.  Klicken Sie in der Anzeige **Watson trainieren** auf **Abfrage in natürlicher Sprache hinzufügen** (z. B. 'IBM Watson im Gesundheitswesen') und fügen Sie die Abfrage hinzu. Achten Sie darauf, Ihre Abfragen so zu schreiben, wie sie voraussichtlich auch von den Benutzern formuliert werden. Außerdem sollten Trainingsabfragen mit einigen Begriffsüberschneidungen zwischen der Abfrage und der gewünschten Antwort geschrieben werden. Dies verbessert anfangs die Ergebnisse, wenn die Abfrage in natürlicher Sprache ausgeführt wird. Das Relevanztraining verwendet ausschließlich Abfragen in natürlicher Sprache; geben Sie keine Abfragen ein, die in der {{site.data.keyword.discoveryshort}}-Abfragesprache geschrieben sind.
1.  Um die Ergebnisse Ihrer Abfrage anzuzeigen, klicken Sie auf die Schaltfläche **Ergebnisse einstufen** neben der Abfrage. Wenn Sie der Ansicht sind, dass nicht genug Ergebnisse vorhanden sind, könnten Sie versuchen, die Abfrage neu zu schreiben oder über die Anzeige **Daten verwalten** weitere Dokumente zu dieser Sammlung hinzuzufügen.
1.  Stufen Sie Ergebnisse zunächst als `relevant` oder `nicht relevant` ein. Wenn Sie damit fertig sind, klicken Sie auf **Zurück zu Abfragen**. In den {{site.data.keyword.discoveryshort}}-Tools hat `Relevant` die Bewertung `10` und `Not relevant` die Bewertung `0`. Wenn Sie bereits über die API mit der Einstufung von Ergebnissen für diese Sammlung begonnen und dabei eine andere Bewertungsskala verwendet haben, wird eine Warnung ausgegeben, die Optionen für die Korrektur des Problems enthält.
    Im oberen Bereich der Anzeige protokolliert Watson den Trainingsstatus für Sie und gibt Ihnen Tipps, wie Sie die Ergebnisse verbessern können. Beispielsweise bedeutet 'Variieren Sie Ihre Einstufungen stärker', dass Sie beide Einstufungen `relevant` und `nicht relevant` verwenden sollen. Sobald Sie die Anforderungen erfüllen, wird das Training in regelmäßigen Abständen aktualisiert. Nach dem Start ist es in weniger als 30 Minuten abgeschlossen; während Watson die Aktualisierung durchführt, können Sie wie gewohnt weiterarbeiten.
1.  Fügen Sie laufend Abfragen hinzu und setzen Sie die Einstufung der Ergebnisse fort.

Sie können jederzeit zur Hauptanzeige **Abfragen erstellen** zurückkehren, indem Sie in der linken oberen Ecke auf **Abfragen erstellen** klicken.
{: tip}
Um zur Anzeige **Daten verwalten** zurückzukehren, klicken Sie in der rechten oberen Ecke auf den Namen der Sammlung.
{: tip}

Falls Sie alle Trainingsdaten in Ihrer Sammlung auf einmal löschen wollen, müssen Sie hierzu die API verwenden. Weitere Informationen finden Sie unter [Alle Trainingsdaten für eine Sammlung löschen](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-all-training-data). Zusätzliche Angaben über das Training mithilfe der API enthält der Abschnitt [Relevanz von Abfrageergebnissen mithilfe der API verbessern](/docs/services/discovery/train.html).

## Relevanz der Ergebnisse testen und iterieren

Nachdem Sie die Einstufung der Ergebnisse abgeschlossen haben und Watson das Training angewendet hat, sollten Sie testen, ob sich die Abfrageergebnisse verbessert haben. Hierzu führen Sie Testabfragen durch, die Ihren Trainingsabfragen ähnlich, jedoch nicht mit diesen identisch sind. Ermitteln Sie, ob sich die Ergebnisse der Testabfragen verbessert haben.

Falls Sie die Ergebnisse nach dem Test weiter verbessern wollen, könnten Sie Folgendes ausführen:
- Fügen Sie weitere Dokumente zu Ihrer Sammlung hinzu.
- Fügen Sie weitere Trainingsabfragen hinzu.
- Stufen Sie weitere Ergebnisse ein; achten Sie hierbei darauf, beide Einstellungen `relevant` und `nicht relevant` zu verwenden.

Zusätzliche Anleitungen für das Training finden Sie unter [Tipps für das Relevanztraining](/docs/services/discovery/train-tips.html#relevancy-tips).

## Konfidenzbewertungen
{: #confidence}

Sammlungen, für die ein Training durchgeführt wurde, geben im Ergebnis für eine Abfrage in natürlicher Sprache eine Konfidenzbewertung (Feld `confidence`) zurück. Diese Zahl für das Feld `confidence` wird danach berechnet, wie relevant das Ergebnis im Vergleich zum trainierten Modell eingeschätzt wird. Die Bewertung der `Konfidenz` ist **nicht** mit der `Bewertung` identisch. Weitere Informationen zum Bestimmen von Schwellenwerten für Konfidenzbewertungen finden Sie unter [How to select a threshold for acting using confidence scores ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/watson/blog/2016/06/23/how-to-select-a-threshold-for-acting-using-confidence-scores/). Die `Bewertung` sollte nicht zum Festlegen von absoluten Schwellenwerten verwendet werden, weil es sich hierbei um eine relative Berechnung handelt.

Die `Konfidenz` kann von 0.0 bis 1.0 reichen. Je höher die Zahl, desto relevanter das Dokument.

Das Feld `confidence` mit der Konfidenzbewertung befindet sich in den Abfrageergebnissen für jedes Dokument unter `result_metadata`. Beispiel:

```json
    "results": [
        {
            "id": "eea16dfd5fe6139a25324e7481a32f89_13",
            "result_metadata": {
                "confidence": 0.5893963975910735,
                "score": 0.5006834
            },
```

**Hinweis:** Das Feld `confidence` wird nur zurückgegeben, wenn das Relevanztraining erfolgreich abgeschlossen wurde. Es kann auch Fälle geben, in denen das trainierte Modell nicht verfügbar ist und das Feld `confidence` nicht zurückgegeben wird. 

Beispielsweise wird das trainierte Modell vorübergehend ungültig, wenn neue Felder der höchsten Ebene eingeführt werden oder das Schema der Sammlung anderweitig geändert wurde, weil neue Dokumente mit einem anderen Schema eingepflegt wurden. In diesem Szenario wird `confidence` nicht mit Ergebnissen zurückgegeben und die Ergebnisse werden so lange aus der nicht trainierten Suche kommen, bis das Modell automatisch erneut trainiert wird und wieder verfügbar ist. Während des erneuten Trainings wird kein Wert für `confidence` zurückgegeben.

Bei Anwendungen, die einen Wert für `confidence` als Schwellenwert verwenden, sollte sichergestellt werden, dass sie für solche Szenarios geeignet sind. Da der Wert für `score` relativ zur Abfrage ist, wird er nicht für die Verwendung als fester Schwellenwert empfohlen. Stattdessen wird empfohlen, dass Anwendungen immer das gleiche Verhalten für alle Ergebnisse aufweisen, die nicht das Feld `confidence` enthalten. Beispielsweise kann eine Anwendung alle Ergebnisse ohne das Feld `confidence` anzeigen oder alle Ergebnisse ohne das Feld `confidence` ausblenden. Es sollte jedoch nicht der Wert für `score` zum Anzeigen einiger Ergebnisse und Ausblenden anderer Ergebnisse verwendet werden.
