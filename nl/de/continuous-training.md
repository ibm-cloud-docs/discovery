---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-25"

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

# Continuous Relevancy Training
{: #crt}

{{site.data.keyword.discoveryshort}} kann aus dem Benutzerverhalten automatisch lernen und so den Aufwand deutlich reduzieren, der zur Optimierung der Relevanzrangfolge der Ergebnisse erforderlich ist. Die Funktion lernt anhand der Interaktionen der Benutzer, wie sie die relevantesten Ergebnisse generiert. Sie kann aus Interaktionen wie Klicks lernen, welche Ergebnisse für die Benutzer am wertvollsten sind und die wichtigsten Signale für zukünftige Abfragen freilegen. Continuous Relevancy Training ordnet die Dokumente mit den relevantesten Informationen oben in den Ergebnissen an. Mit der Funktion ist Folgendes möglich:

- Die Relevanz der Ergebnisse kann für Unterstützungsagenten basierend auf den angeklickten Ergebnissen optimiert werden
- Es können relevantere Ergebnisse in einem Kunden-Chatbot basierend auf den ausgewählten Long-Tail-Ergebnissen angezeigt werden 
- Experten können relevantere Antworten basierend auf den von ihnen untersuchten Ergebnissen bereitgestellt werden

So konfigurieren Sie Continuous Relevancy Training:

- Continuous Relevancy Training kann nur auf der Umgebungsebene aktiviert werden. Abfragen müssen zum Abfragen einer oder mehrere Sammlungen entweder den Endpunkt `/api/v1/environment/{umgebungs-id}/query` oder `/api/v1/environments/{umgebungs-id}/query` verwenden.
- Da {{site.data.keyword.discoveryshort}}-`Ereignisse` (Klicks) verwendet werden, um die benötigten Trainingsdaten zu erstellen, integrieren Sie zunächst die Ereignisüberwachung. Details finden Sie unter [Nutzungsüberwachung](/docs/services/discovery/feedback.html#usage).
- Es werden mindestens 1000 Abfragen in natürlicher Sprache mit einem zugehörigen Klickereignis benötigt, damit Continuous Relevancy Training gestartet werden kann. Ereignisse und Protokolle werden für die gesamte Instanz 30 Tage lang aufbewahrt; die 1000 Klicks müssen daher während dieses Zeitraums erfasst werden.
- Continuous Relevancy Training ist für die Advanced-Plangröße `Small` oder höher und für Premium-Pläne verfügbar. Für `Lite`-Pläne steht die Funktion nicht zur Verfügung.
- Die Anzahl der Sammlungen für Continuous Relevancy Training ist auf `5` begrenzt. Das sich Continuous Relevancy Training auf mehrere Sammlungen bezieht, können sich sowohl Abfrage- als auch Trainingszeiten verlängern.
- Continuous Relevancy Training wird nur für die Felder der höchsten Ebene durchgeführt und die Anzahl der Felder, die im Trainingsprozess verwendet werden können, ist begrenzt. In den Fällen, in denen mehr als `10` Felder der höchsten Ebene vorhanden sind, treten beim Training eher Fehler auf. 

So verwenden Sie Continuous Relevancy Training:

Sobald die Funktion trainiert wurde, können mit Continuous Relevancy Training die Ergebnisse einer Abfrage in natürlicher Sprache (`natural_language_query`) bei der Verwendung einer Abfrage auf Umgebungsebene beeinflusst werden. 

Continuous Relevancy Training kann zur Abfragezeit verwendet werden, indem eine Abfrage in natürlicher Sprache (`natural_language_query`) mit mehreren Sammlungen in allen Sammlungen in Ihrer Umgebung ausgeführt wird. Anweisungen hierzu finden Sie unter [Mehrere Sammlungen abfragen](/docs/services/discovery/using.html#multiple-collections). 

**Hinweis:** Continuous Relevancy Training wirkt sich nicht auf Abfragen aus, die an einen trainierten oder nicht trainierten Abfrageaufruf auf Sammmlungsebene (`/v1/environments/{umgebungs-id}/collections/{sammlungs-id}/query`) gemacht wurde. 

Überwachungsstatus:

Der Status von Continuous Relevancy Training kann über den Endpunkt `/api/v1/environments` angezeigt werden. Weitere Informationen finden Sie in der [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#environments-api){: new_window}. Der Wert für `status` gibt Auskunft über den Status der Trainingsoperationen und informiert Sie darüber, ob Continuous Relevancy Training aktiv ist:

```
"search_status" : [
        {
            "scope" : "environment",
            "status" : "NO_DATA",
            "status_description" : "Discovery is employing a default strategy for document search natural_language_query. Enable query and event logging so we can initiate relevancy training to improve search accuracy.”
        }
    ]
```
