---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-18"

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

# Abfrageleistung
{: #qp}

Die Abfrageleistung in {{site.data.keyword.discoveryshort}} ist von einer Reihe von Faktoren abhängig. 

## Leistung bewerten 
{: #qp-evaluate}

Wenn Sie hohe gleichzeitige Auslastungen Ihrer Anwendung erwarten, ist es wichtig, die Leistung Ihrer {{site.data.keyword.discoveryshort}}-Anwendung bewerten zu können. Zur Messung der Leistung werden mehrere Dimensionen häufig verwendet:
1.  **Antwort-Latenz** : Die Zeit, die {{site.data.keyword.discoveryshort}} für die Rückgabe der Ergebnisse Ihrer Abfrage benötigt. 
    - Die Latenz kann abhängig von einer Reihe von Faktoren variieren. Weitere Informationen hierzu finden Sie unter [Faktoren mit Einfluss auf die Leistung](/docs/services/discovery?topic=discovery-qp#perffactors). 
    - Es ist wichtig, unter Verwendung einer repräsentativen Gruppe von Abfragen Tests in Ihrer Produktionsumgebung auszuführen, um die durchschnittliche Latenz zu ermitteln. 
1.   **Abfragerate**: Die Anzahl der Anforderungen, die innerhalb einer bestimmten Zeit verarbeitet werden können, in der Regel in Abfragen pro Sekunde (QPS) gemessen. Dieser Wert ist dann wichtig, wenn Sie hohe gleichzeitige Auslastungen Ihrer Anwendung erwarten.  
     - Welche Rate erreicht werden kann, variiert auf Grundlage vieler derselben Faktoren wie z. B. der Latenz. 
     - Die Abfragerate sollte auch mit repräsentativen Abfragen und bei den Lasten, die voraussichtlich eintreten werden, ausgewertet werden. Denken Sie daran, während der Tests auch Spitzenlasten zu berücksichtigen.

## Faktoren mit Einfluss auf die Leistung
{: #perffactors}

Die Abfrageleistung in {{site.data.keyword.discoveryshort}} variiert abhängig von einer Reihe von Faktoren wie z. B. Plangröße, Komplexität der Abfragen, verwendete Funktionen sowie Größe und Komplexität der Sammlung.

### Plangröße
{: #qp-plansize}

Die {{site.data.keyword.discoveryshort}}-Preisstrukturpläne begrenzen die Anzahl der verfügbaren Dokumente und bieten auch unterschiedliche Funktionen zur Bewältigung der Abfragelast. Je umfassender die Plangröße, desto mehr Ressourcen stehen für die Bearbeitung der Abfragen zur Verfügung. Auch die Durchschnittswerte für die Rate variieren je nach Plangröße. Durch ein Upgrade Ihres Plans kann die Leistung verbessert werden. Informationen zu den Plänen und ihren Begrenzungen finden Sie im Abschnitt [{{site.data.keyword.discoveryshort}}-Preisstrukturpläne](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans). 

### Abfragekomplexität
{: #qp-query}

Es gibt viele Möglichkeiten, Abfragen für {{site.data.keyword.discoveryshort}} auszuführen, und die verschiedenen verwendeten Operationen können sich auf die Leistung auswirken. Folgende Abfragemerkmale haben Auswirkungen auf die Leistung:

1.   **Länge**: Längere Abfragen zeigen mit einiger Wahrscheinlichkeit schlechtere Leistung. 
1.   **Aggregationen**: Aggregationen sind ein komplexerer Abfragetyp, wobei verschachtelte Aggregationen den größten Einfluss auf die Leistung haben. 
1.   **Operatoren**: Die Verwendung von Platzhaltern sowie unscharfe Suchen können die Leistung beeinträchtigen.
1.   **Anzahlen**: Durch Reduktion der Anzahl zurückgegebener Dokumente kann die Leistung verbessert werden. Wenn Sie die Ergebnisse seitenweise durchblättern müssen, verwenden Sie den Parameter `offset`. 
1.   **Rückgabefelder**: Eine Beschränkung der Felder auf die für Ihre Anwendung benötigten kann helfen (z. B. die nicht vollständige Rückgabe von Text des Dokuments, wenn nur der Titel und die Passage benötigt werden). 

Weitere Informationen enthält der Abschnitt [Abfragereferenz](/docs/services/discovery?topic=discovery-query-reference#query-reference).

### Verwendete Funktionen
{: #qp-features}

Es gibt eine Reihe von Funktionen, mit denen sich die Abfrageergebnisse verbessern lassen. Mit folgenden Funktionen kann die Leistung verbessert werden:
 
1.   **Passagenabruf**: Mit dem Passagenabruf werden Dokumente nach für Ihre Abfrage relevanten Snippets durchsucht. Sie können die Felder in den Dokumenten, die mit dem Passagenabruf durchsucht werden, mit dem Parameter `passages.fields` anpassen; wenn Ihr Inhalt viele Felder enthält, wird dadurch die Latenz beim Passagenabruf reduziert. Weitere Informationen zum Passagenabruf finden Sie unter [Passagen](/docs/services/discovery?topic=discovery-query-parameters#passages).
1.   **Relevanztraining**: Beim Relevanztraining werden Funktionen für jedes Textfeld der höchsten Ebene (Felder auf derselben Ebene wie `document_id` in den JSON-Daten) in der Sammlung berechnet. Wenn viele Felder der höchsten Ebene vorhanden sind, kann dies zu einer Leistungsbeeinträchtigung für eine `natural_language_query` beim Training führen. Durch eine Verringerung der Anzahl von Feldern der höchsten Ebene kann die Leistung verbessert werden. Dies kann durch Normalisierung oder manuelle Bearbeitung der JSON-Daten erfolgen, bei der Felder, die zum Finden relevanter Inhalte nicht nutzbringend sind, in einer verschachtelten Struktur untergebracht werden. Das Ändern der Felder, die zum Training verwendet werden, wirkt sich auch das Modell aus. Deshalb ist bei einer solchen Änderung sowohl die Auswirkung auf die Leistung als auch die Genauigkeit der Ergebnisse zu berücksichtigen. Weitere Informationen zum Relevanztraining finden Sie unter [Ergebnisrelevanz verbessern](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling).
1.  **Continuous Relevancy Training**: Beim Continuous Relevancy Training wird in allen Sammlungen einer Umgebung gesucht. Je mehr Sammlungen in einer Umgebung vorhanden sind, desto größer sind die Auswirkungen auf die Leistung. Weitere Informationen hierzu finden Sie unter [Continuous Relevancy Training](/docs/services/discovery?topic=discovery-crt#crt).

### Sammlungsgröße und -komplexität
{: #qp-collection} 

Auch der Aufbau der Dokumente innerhalb einer privaten Sammlung kann sich auf die Abfrageleistung auswirken:
1.  **Gesamtzahl der Dokumente**: Die Leistung kann beeinträchtigt werden, wenn bei Advanced-Plangrößen die Obergrenze von `Anzahl der Dokumente` erreicht wird. 
1.  **Größe der Dokumente**: Sehr umfangreiche Dokumente (mit einer Größe von mehreren MB) erfordern das Verschieben großer Datenmengen pro Anforderung, was sich negativ auf die Leistung auswirken kann, insbesondere wenn Passagenabruf oder Relevanztraining eingesetzt werden. 
1.  **Anzahl der Aufbereitungen**: Aufbereitungen machen Dokumente komplexer, weil eine erhebliche Anzahl verschachtelter Felder hinzugefügt wird. Wenn eine Aufbereitung für Ihren Anwendungsfall nicht erforderlich ist, erwägen Sie ihre Inaktivierung zum Zeitpunkt des Einpflegens. Aufbereitungen werden nicht direkt für die Suchrelevanz von `natural_language_query` verwendet. Weitere Informationen zu Aufbereitungen enthält der Abschnitt [Aufbereitungen hinzufügen](/docs/services/discovery?topic=discovery-configservice#adding-enrichments).
