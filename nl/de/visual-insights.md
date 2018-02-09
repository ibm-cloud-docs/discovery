---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-30"

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

# Watson Discovery Visual Insights
{: #visual-insights}

{{site.data.keyword.discoveryfull}} Visual Insights ist ein experimentelles Feature, mit dem Sie Verbindungen grafisch orientiert untersuchen können, die aufgrund des Verständnisses von {{site.data.keyword.discoveryshort}} für semantische Elemente, Beziehungen, Konzepte und anderes erkannt wurden. 

{{site.data.keyword.discoveryfull}} Visual Insights vermittelt Ihnen genauere Erkenntnisse über Ihre Sammlungen, bevor Sie mit {{site.data.keyword.discoveryshort}} Abfragen erstellen, die Sie in eine neue Anwendung oder eine bestehende Lösung integrieren können und die Benutzer mit den von ihnen benötigten Informationen versorgt.

Beim experimentellen Release ist Visual Insights nur in öffentlichen Umgebungen verfügbar.

**Haftungsausschluss:** Visual Insights ist ein experimentelles Feature. Dies bedeutet, dass es möglicherweise instabil ist, häufig geändert werden kann und seine Verwendung und Unterstützung kurzfristig eingestellt werden kann. Das Feature wird bereitgestellt, damit Sie seine Funktionalität bewerten können. Es bietet möglicherweise nicht dasselbe Leistungs- oder Kompatibilitätsniveau wie eine allgemein freigegebene Funktionalität. Es ist nicht zur Verwendung in einer Produktionsumgebung gedacht; eine solche Verwendung erfolgt auf eigenes Risiko. Details finden Sie unter [Betaversion und experimentelle Features](/docs/services/discovery/release-notes.html#beta-features).

## Schnelleinführung in Visual Insights
{: #quick-tour-visual-insights}

![Schnelleinführung in Discovery Visual Insights](images/discovery-visualinsights-quicktour.png)

Die Visual Insights-Anzeige besteht aus vier Hauptbereichen.

### Suchleiste
{: #search-bar}

Sie können {{site.data.keyword.discoveryshort}}-Sammlungen mithilfe der **Suchleiste** oben in der Anzeige abfragen.

- Falls Sie sich mit Ihren {{site.data.keyword.Bluemix_notm}}-Berechtigungsnachweisen angemeldet haben, sind alle Sammlungen aus den {{site.data.keyword.discoveryshort}}-Instanzen, die Ihrem Konto zugeordnet sind, in der Dropdown-Liste für die Sammlungen (standardmäßig {{site.data.keyword.discoverynewsfull}}) verfügbar. Falls Sie nicht angemeldet sind, ist nur die Sammlung '{{site.data.keyword.discoverynewsfull}}' verfügbar.
- Wählen Sie Ihre Sammlung aus, geben Sie Ihre Abfrage im Suchfeld ein (z. B. `Was ist Netzneutralität`) und klicken Sie auf die Schaltfläche **Suchen**, um die Suche auszuführen. Bei größeren Sammlungen kann es unter Umständen eine Minute oder länger dauern, bis Ergebnisse angezeigt werden. Sie können Ihre Suche filtern, indem Sie auf die Schaltflächen für `Dokumente`, `Konzepte`, `Personen`, `Standorte`, `Organisationen` oder `Unternehmen` klicken.
- Optional können Sie in den angezeigten Ergebnissen ein beliebiges Element (Entität, Konzept oder Dokument) auswählen, indem Sie im Header auf das Symbol ![Abfragesymbol](images/discovery-query-icon.png) klicken.
- Falls eine private Sammlung ausgewählt ist und keine Abfrage eingegeben wurde, werden bis zu 1000 Dokumente aus der Sammlung im [Detailteilfenster](/docs/services/discovery/visual-insights.html#details-pane) angezeigt. Falls die Sammlung '{{site.data.keyword.discoverynewsshort}}' ausgewählt ist und keine Abfrage eingegeben wurde, wird eine Auswahl von 100 kürzlich erschienenen Artikeln angezeigt.

### Netzanzeige
{: #network-display}

Unter der Suchleiste befindet sich in der Mitte die **Netzanzeige**. Sie enthält die interaktive Darstellung Ihrer Abfrageergebnisse.

- Die **Netzanzeige** ist eine grafische Darstellung der Dokumente, Entitäten und Konzepte, die aus den Abfrageergebnissen extrahiert wurden. Pinkfarbige Knoten stehen für Dokumente, blaue Knoten stellen Entitäten oder Konzepte dar. Jeder Dokumentknoten ist mit allen Entitäts- und Konzeptknoten verknüpft, die in diesem Dokument durch {{site.data.keyword.discoveryshort}} erkannt wurden. Je ähnlicher sich Dokumente sind, desto kleiner ist der Abstand zwischen ihnen in der Visualisierung.
- Wenn Sie den Mauszeiger über einen Knoten in der **Netzanzeige** bewegen, wird sein zugehöriger Titel angezeigt und seine Verknüpfungen mit anderen Knoten werden hervorgehoben.
- Wenn Sie auf einen Knoten klicken, werden Informationen zu diesem Knoten im [Detailteilfenster](/docs/services/discovery/visual-insights.html#details-pane) angezeigt.

### Detailteilfenster
{: #details-pane}

Rechts neben der Netzanzeige befindet sich das **Detailteilfenster**.

- Das Detailteilfenster stellt weitere Details zu jedem Dokument bereit, einschließlich seiner Klassifizierung und seines Datums (sofern verfügbar), eines kurzen Auszugs (mit der Option, das gesamte Dokument zu öffnen) sowie der Entitäten und Konzepte, mit denen das Dokument verknüpft ist.
- Falls in der Netzanzeige ein Knoten ausgewählt wurde, bei dem es sich nicht um ein Dokument handelt, werden Informationen zu diesem Knoten oben im Detailteilfenster angezeigt.
- Wenn Sie im Detailteilfenster auf eine/s der verknüpften Entitäten bzw. Konzepte klicken, wird der entsprechende Knoten in der Netzansicht ausgewählt.

### Navigationsbereich
{: #navigation-pane}

Links neben der Netzanzeige befindet sich der **Navigationsbereich**. In diesem Bereich sehen Sie in Form einer Tagwolke eine Übersicht über die häufigsten Begriffe, die aus den Abfrageergebnissen in der ausgewählten Sammlung extrahiert wurden. Je häufiger der Begriff in den Abfrageergebnissen enthalten ist, desto größer ist er dargestellt.

- Wenn Sie einen Begriff in der Tagwolke auswählen, wird er in Pink angezeigt und alle Dokumente, denen er zugeordnet ist, werden in der Netzanzeige hervorgehoben. Im Detailteilfenster wird dann die Liste der hervorgehobenen Dokumente angezeigt. Für die anderen Begriffe in der Tagwolke ist nun ihre Beziehung zum ausgewählten Begriff angegeben:
  - Abgeblendete Begriffe sind keinem der hervorgehobenen Dokumente zugeordnet.
  - Wird ein Begriff in Violett angezeigt, ist er allen hervorgehobenen Dokumenten zugeordnet und für die Unterscheidung der Dokumente nicht von Nutzen.
  - Weiterhin in Blau angezeigte Begriffe sind einigen, jedoch nicht allen hervorgehobenen Dokumenten zugeordnet und können somit zur Präzisierung der Gruppe mit den hervorgehobenen Dokumenten verwendet werden. Wenn Sie einen dieser Begriffe auswählen, verkleinert sich die Gruppe der hervorgehobenen Dokumente auf diejenigen Dokumente, denen beide Tags zugeordnet sind, und die Netzanzeige wird auf die Region gezoomt, in der sich diese Dokumente befinden. Mit diesem Verfahren können größere Gruppen von Dokumenten durch wenige Klicks auf eine kleinere Gruppe eingegrenzt werden.
- Um einen ausgewählten Begriff abzuwählen, klicken Sie erneut auf den Begriff. Um alle ausgewählten Begriffe abzuwählen, klicken Sie in der Tagwolke auf eine leere Stelle zwischen den Wörtern. Wenn Sie auf einen in Grau dargestellten Tag klicken, wird die bestehende Auswahl aufgehoben und dieser Begriff ausgewählt.
- Die Typen und Anzahlen der Dokumente, Personen, Konzepte, Organisationen, Standorte und Unternehmen werden über der Tagwolke angezeigt. Wenn Sie auf eines dieser Elemente klicken, werden die Tagwolke und die Darstellung in der Netzanzeige gefiltert.

## Visual Insights verwenden
{: #using-visual-insights}

Mit Visual Insights können Sie {{site.data.keyword.discoverynewsfull}} ohne vorherige Anmeldung abfragen. Damit Sie Visual Insights für Ihre eigenen Sammlungen verwenden können, benötigen Sie Folgendes:

- Ein {{site.data.keyword.Bluemix_notm}}-Konto, das eine {{site.data.keyword.discoveryshort}}-Instanz enthält.
- Eine oder mehrere Sammlungen in dieser {{site.data.keyword.discoveryshort}}-Instanz, die mit der Aufbereitung für die [Entitätsextraktion](/docs/services/discovery/building.html#entity-extraction) sowie optional einer der Aufbereitungen für das [Konzepttagging](/docs/services/discovery/building.html#concept-tagging), die [Schlüsselwortextraktion](/docs/services/discovery/building.html#keyword-extraction), die [Beziehungsextraktion](/docs/services/discovery/building.html#relation-extraction) und die [Kategorieklassifizierung](/docs/services/discovery/building.html#category-classification) aufbereitet wurden. Weitere Aufbereitungen können eingeschlossen sein, werden jedoch nicht durch Visual Insights dargestellt.

Weitere Informationen zu {{site.data.keyword.discoveryshort}} sowie zu einem kostenlosen Einstieg in seine Verwendung finden Sie unter [Watson {{site.data.keyword.discoveryshort}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/services/discovery/){: new_window}.

Wenn Sie über ein {{site.data.keyword.Bluemix_notm}}-Konto, eine {{site.data.keyword.discoveryshort}}-Instanz sowie eine oder mehrere gefüllte Sammlungen verfügen, werden Ihre Sammlungen in Visual Insights angezeigt, sobald Sie sich anmelden.

Bei Visual Insights anmelden

1. Öffnen Sie [{{site.data.keyword.discoveryshort}} Visual Insights ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://visual-insights.bluemix.net){: new_window}.
1. Klicken Sie auf das Symbol ![Profilsymbol](images/discovery-profile-icon.png) in der Suchleiste.
1. Geben Sie Ihre {{site.data.keyword.Bluemix_notm}}-ID und Ihr Kennwort ein. Nach einigen Augenblicken sind Ihre Sammlungen in der Suchleiste zur Auswahl verfügbar.

## Feedback senden
{: #providing-feedback}

Ihre Meinung über {{site.data.keyword.discoveryshort}} Visual Insights interessiert uns. Auf den Link für das Feedback können Sie zugreifen, indem Sie im Header auf das Symbol ![Infosymbol](images/discovery-info-icon.png) klicken.
