---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-17"

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

# Nutzungsüberwachung
{: #usage}

Sie können die Nutzung der {{site.data.keyword.discoveryshort}}-Instanz überwachen und verfolgen, um anhand dieser Daten Ihre Anwendungen besser verstehen und verbessern zu können. Die [Ereignis-API ![Symbol für externen](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#events-and-feedback-api){: new_window} kann verwendet werden, um Protokolleinträge zu erstellen, die bestimmten Abfragen und Aktionen in natürlicher Sprache zugeordnet sind. Beispielsweise können Sie aufzeichnen, welche Dokumente in einer Ergebnismenge durch einen Benutzer "angeklickt" wurden und wann dieser Klick erfolgt ist.

**Hinweis:** Protokolle und Ereignisse werden nur für Abfragen in natürlicher Sprache in privaten Datensammlungen überwacht. Für {{site.data.keyword.discoverynewsfull}} werden keine Protokolle zusammengestellt.

{{site.data.keyword.discoveryshort}} kann die folgenden Informationen protokollieren:
- **Abfragen**: Abfragen in natürlicher Sprache werden für Sammlungen in Ihrer Umgebung ausgeführt. 
- **Einblendungen** (oder **Ergebnisse**): Die für eine bestimmte Abfrage zurückgegebenen Ergebnisse, in der Regel Dokumente oder Passagen. 
- **Ereignisse**: Interaktionen, die ein Benutzer für ein Ergebnis oder eine Gruppe von Ergebnissen in {{site.data.keyword.discoveryshort}} ausführt (z. B. einen Klick auf ein Dokumentergebnis).

**Abfragen** und **Einblendungen** werden automatisch protokolliert; die Protokollierung von **Ereignissen** kann über die API in Ihre Anwendung integriert werden.

## Protokolle anzeigen
{: #viewlogs}

Sie können das Abfrage- und das Ereignisprotokoll durchsuchen, um nach Abfragesitzungen zu suchen, die mit den angegebenen Kriterien übereinstimmen. Die Suche nach dem Endpunkt `logs` verwendet die Standardabfragesyntax von {{site.data.keyword.discoveryshort}} für die unterstützten Parameter. Der Endpunkt stellt grundlegende Abfragefunktionen für die Anzeige und Suche in den aufgezeichneten Daten bereit.  

Der Endpunkt `/api/v1/logs` unterstützt die folgenden {{site.data.keyword.discoveryshort}}-Abfrageparameter.
- Parameter 'query' 
- Parameter 'filter'
- Parameter 'sort'
- Parameter 'count' 
- Parameter 'offset'
- Parameter 'version'

Zusätzliche Details zu der Funktion und der Syntax für die Parameter finden Sie unter [Abfrageparameter](/docs/services/discovery/query-parameters.html).

Beispiel für das Durchsuchen von Protokollen nach einer Abfrage in natürlicher Sprache, die den Begriff "train" enthält:

`https://gateway.watsonplatform.net/discovery/api/v1/logs?version=2018-03-28&query=train`

Die Antwort auf eine `logs`-Abfrage enthält Ergebnisse, die ähnlich wie {{site.data.keyword.discoveryshort}}-Dokumentergebnisse angezeigt werden. Jedes Ergebnis ist entweder eine Abfrage oder ein Ereignis, die/das im Feld `type` des Dokuments angegeben ist.  

Beispielabfrageprotokoll:

```
{
            "customer_id": "",
            "environment_id": "252e6e82-c2d2-450e-9670-0008b0a3a99c",
            "natural_language_query": "how do i get from the airport to the city",
            "query_id": "_Qs35yOoa7",
            "document_results": {
                "count": 2,
                "results": [
                    {
                        "collection_id": "af9e1f41-6114-4d77-bca6-c9b99b2601b1",
                        "score": 6.724753491503856,
                        "position": 1,
                        "document_id": "4193eaa727d79b0f74597356dbcbb9a7"
                    },
                    {
                        "collection_id": "af9e1f41-6114-4d77-bca6-c9b99b2601b1",
                        "score": 5.791631414211986,
                        "position": 2,
                        "document_id": "bdcd6a9cc1438a3faa8c925f6a8d9429"
                    }
                ]
            },
            "event_type": "query",
            "session_token": "1_LKczxWGEWx5TJAi1_Qs35yOoa7",
            "created_timestamp": "2018-09-12T05:20:07.469Z"
        }
```

Mit Abfrageprotokollen können Sie den Typ der Ergebnisse untersuchen, die an Ihre Endbenutzer zurückgegeben werden, und untersuchen, wie die Ergebnisqualität mithilfe der in {{site.data.keyword.discoveryshort}} verfügbaren Methoden verbessert werden kann. Beispiel: 
- Relevanztraining, siehe [Ergebnisrelevanz mithilfe der API verbessern](/docs/services/discovery/train.html) und [Ergebnisrelevanz mithilfe der Tools verbessern](/docs/services/discovery/train-tooling.html)
- [Abfrageoperatoren](/docs/services/discovery/query-operators.html)
- [Abfrageerweiterung](/docs/services/discovery/using.html#query-expansion)
- Angepasste Konfigurationen, siehe [Konfigurationsreferenz](/docs/services/discovery/custom-config.html)

## Ereignisprotokolle erstellen
{: #eventlogs}

Ereignisprotokolle werden verwendet, um die Interaktionen von Benutzern in Ihrer Anwendung zu verfolgen. Dies kann Ihnen dabei helfen, die aktuelle Leistung der Anwendung zu verstehen und Bereiche zu ermitteln, auf die Sie sich zum Optimieren der Ergebnisse fokussieren sollten. {{site.data.keyword.discoveryshort}} stellt eine API bereit, die in Ihre Anwendung eingebettet werden kann, um Ereignisse zu verfolgen. Wenn Sie diese API mit den entsprechenden Informationen aufrufen, wenn ein Benutzer eine Aktion ausführt, wird ein Signal zurück an {{site.data.keyword.discoveryshort}} gesendet, das dann in den Protokollen angezeigt werden kann. 

Ereignisse können dazu beitragen, Informationen über die Berechnung von Metriken (wie die Klickrate) zu sammeln, um zu messen, wie effektiv die Anwendung ist, Endbenutzer bei der Suche nach relevanten Informationen zu unterstützen. Sie können auch verwendet werden, um ein Seeding für Trainings auszuführen, indem die Abfragen und Klicks überprüft werden, um mit der Erstellung der Ground Truth zu beginnen. 

Sie können diese API überall hinzufügen, wo Benutzer mit Ihren Ergebnissen interagieren. In einer Suchbenutzerschnittstelle können Sie sie beispielsweise hinzufügen, wenn ein Benutzer auf einen Dokumentlink klickt; in einer Chatbot-Schnittstelle können Sie die API zum Verfolgen verwenden, wenn der Benutzer auf eine Schaltfläche des Typs **Erweitern** oder **Weitere Details** klickt.

{{site.data.keyword.discoveryshort}}-Ergebnisse geben zusätzliche Informationen zurück, die für die Verfolgung von Ereignissen verwendet werden können, einschließlich eines Sitzungstokens. 

`"matching_results": 179,`
`"session_token": "1_LKczxWGEWx59fYD0_VV8HFUpb6"`

Um ein Ereignis aufzuzeichnen, nehmen Sie einen POST an den Endpunkt `/api/v1/events` vor. Details finden Sie im Abschnitt zur
[Ereignis-API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#events-and-feedback-api){: new_window}.

Nachdem ein Ereignis aufgezeichnet wurde, kann es mit dem Endpunkt `/api/v1/logs` wieder herausgelesen werden. Verknüpfen Sie Ereignisse mit der zugehörigen Abfrage unter Verwendung des Werts für `session_token`.
