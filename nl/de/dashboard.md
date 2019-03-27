---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-25"

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

# Metriken anzeigen und Abfrageergebnisse mit dem Leistungsdashboard verbessern
{: #performance-dashboard}

Das Leistungsdashboard in den {{site.data.keyword.discoveryshort}}-Tools kann verwendet werden, um Abfragemetriken anzuzeigen und die Abfrageergebnisse, einschließlich der Abfragerelevanz, zu verbessern.

Sie können auf das Leistungsdashboard zugreifen, indem Sie links auf das Symbol **Datenmetriken anzeigen** klicken. Das Dashboard ist in Premium- oder Dedicated-Umgebungen nicht verfügbar.

Zur Verbesserung der Abfrageergebnisse in natürlicher Sprache stehen zwei Optionen zur Verfügung:
- [Abfragen ohne Ergebnisse durch Hinzufügen weiterer Daten korrigieren](/docs/services/discovery?topic=discovery-performance-dashboard#addmore)
- [Relevante Ergebnisse durch Trainieren der Daten nach oben bringen](/docs/services/discovery?topic=discovery-performance-dashboard#traindata)

Sie können die Datenmetriken in der [Abfrageübersicht](/docs/services/discovery?topic=discovery-performance-dashboard#overview) anzeigen. 

## Abfragen ohne Ergebnisse durch Hinzufügen weiterer Daten korrigieren
{: #addmore}

In diesem Abschnitt des Dashboards können Sie Abfragen überprüfen, die keine Ergebnisse zurückgegeben haben, und weitere Daten zur Abfrage hinzufügen, damit diese zukünftig Ergebnisse zurückgibt. Klicken Sie zum Einstieg auf die Schaltfläche **Alle anzeigen und Daten hinzufügen**. 

## Relevante Ergebnisse durch Trainieren der Daten nach oben bringen
{: #traindata}

In diesem Abschnitt können Sie Ihre Sammlungen trainieren, um die Relevanz von Abfrageergebnissen in natürlicher Sprache zu verbessern. Klicken Sie zum Einstieg auf die Schaltfläche **Alle anzeigen und Relevanztraining durchführen**. Entsprechende Anweisungen finden Sie dann im Abschnitt [Abfragen hinzufügen und die Relevanz der Ergebnisse bewerten](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#results).

Weitere Informationen zu Trainingsvoraussetzungen und -optionen finden Sie unter [Ergebnisrelevanz mit den Tools verbessern](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling).

## Abfrageübersicht
{: #overview}

Im Abschnitt mit der Abfrageübersicht wird Folgendes angezeigt:
- Die Gesamtzahl der Abfragen, die von Benutzern vorgenommen wurden.
- Der Prozentsatz der Abfragen mit einem oder mehreren Ergebnissen, auf die geklickt wurde.
- Der Prozentsatz der Abfragen, für die keine Ergebnisse geklickt wurden.
- Der Prozentsatz der Abfragen, für die keine Ergebnisse zurückgegeben wurden.
- Ein Diagramm, das diese Ergebnisse im Zeitverlauf anzeigt, damit Sie verfolgen können, wie die Verbesserung der Leistung durch das Hinzufügen von Daten und Relevanztraining verbessert wird.

Diese Ergebnisse werden unter Verwendung der Ereignis- und Feedback-API erfasst. Weitere Informationen finden Sie in der [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/discovery#create-event).
