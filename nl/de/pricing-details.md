---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-17"

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

# Preisstrukturpläne für Discovery

Der {{site.data.keyword.discoveryfull}}-Service bietet drei Pläne: **Lite**, **Advanced** und **Premium**, die für Sie je nach Bedarf verschiedene Ebenen von Ressourcen und Funktionalität bereitstellen.
{: shortdesc}

Für **private Datenanwendungsfälle** gelten die folgenden Features, Begrenzungen und Preise:

## Lite
{: #lite}

Größe | Dokumentspeichergrenze | Anzahl der Dokumente\* | Preis 
------ | ------ | ------ | ------  
N/Z | 50 MB | 1.000 pro Monat | Kostenlos 

Der Lite-Plan ist ein Startplan und sollte nicht für die Produktion verwendet werden. Wenn Sie ein Upgrade auf einen bezahlten Plan durchführen, können Sie alle eingepflegten Dokumente beibehalten.  Lite-Planinstanzen werden nach 30 Tagen Inaktivität gelöscht. 

Attribute:
- 1 Umgebung
- Bis zu 2 Sammlungen
- Kostenlose NLU-Aufbereitungen\*\*
- 20 Inflight-Dokumente\*\*\*\* 

Zusätzliche Optionen:<br> [Angepasste Modelle](/docs/services/discovery/integrate-wks.html#integrating-your-custom-model):<br>
Ein Watson Knowledge Studio-Modell enthalten. Zusätzliche Modelle: Nicht verfügbar<br>[Elementklassifizierung](/docs/services/discovery/element-classification.html)\*\*\*:
500 Seiten pro Monat enthalten. Zusätzliche Seiten: Nicht verfügbar <br>[News-Abfragen](/docs/services/discovery/watson-discovery-news.html):
200 News-Abfragen pro Monat enthalten. Zusätzliche Abfragen: Nicht verfügbar<br>[Abfrageerweiterungen](/docs/services/discovery/using.html#query-expansion):
500 Abfrageerweiterungen mit insgesamt 1.000 Begriffen. Zusätzliche Erweiterungen: Nicht verfügbar

Informationen zum Upgrade von Lite auf Advanced finden Sie unter [Upgrade für Ihren Service durchführen](/docs/services/discovery/upgrading.html#service).

## Advanced
{: #advanced}

Größe | Dokumentspeichergrenze | Anzahl der Dokumente\* | Preis 
------ | ------ | ------ | ------ 
X-Small\*\*\*\*\* | 40 GB | Bis zu 50.000 Dokumente pro Monat | Ab $500 pro Monat  
Small | 160 GB | Bis zu 1 Mio. Dokumente pro Monat | Ab $1.500 pro Monat  
Medium-Small | 320 GB | Bis zu 2 Mio. Dokumente pro Monat | Ab $3.000 pro Monat  
Medium| 640 GB | Bis zu 4 Mio. Dokumente pro Monat | Ab $5.000 pro Monat  
Medium-Large | 1,2 TB | Bis zu 8 Mio. Dokumente pro Monat | Ab $10.000 pro Monat  
Large| 2,4 TB | Bis zu 16 Mio. Dokumente pro Monat | Ab $15.000 pro Monat  
X-Large| 4 TB | Bis zu 23 Mio. Dokumente pro Monat | Ab $20.000 pro Monat  
XX-Large | 5,5 TB | Bis zu 64 Mio. Dokumente pro Monat | Ab $35.000 pro Monat  
XXX-Large | 12 TB | Bis zu 100 Mio. Dokumente pro Monat | Ab $45.000 pro Monat  

X-Small ist die kleinste verfügbare Umgebung und wird nur für Entwicklungs- und Testumgebungen empfohlen.\*\*\*\*\*

Wenn Sie von einer Ebene von Advanced zu einer anderen wechseln, müssen Sie keine neuen Instanzen erstellen. Neue Instanzen sind allerdings erforderlich, wenn Sie von einem Advanced- zu einem Premium-Plan wechseln. Informationen zum Durchführen eines Upgrades von einer Ebene von Advanced auf eine andere finden Sie unter [Von einer Advanced-Ebene zu einer anderen wechseln](/docs/services/discovery/upgrading.html#advanced).

\*\*\*\*\*Attribute von X-Small-Plänen: 
- 1 Umgebung
- Bis zu 4 Sammlungen
- Kostenlose NLU-Aufbereitungen\*\*
- 50 Inflight-Dokumente\*\*\*\*

Attribute für alle anderen Advanced-Pläne:
- 1 Umgebung
- Bis zu 100 Sammlungen
- Kostenlose NLU-Aufbereitungen\*\*
- 105 Inflight-Dokumente\*\*\*\*

Zusätzliche Optionen:<br> [Angepasste Modelle](/docs/services/discovery/integrate-wks.html#integrating-your-custom-model):<br>
Ein Watson Knowledge Studio-Modell enthalten. Zusätzliche Modelle: Jeweils $800<br>[Elementklassifizierung](/docs/services/discovery/element-classification.html)\*\*\*:
500 Seiten pro Monat enthalten. Zusätzliche Seiten: Je $0,40<br>[News-Abfragen](/docs/services/discovery/watson-discovery-news.html):
200 News-Abfragen pro Monat enthalten  
10.000 zusätzliche Abfragen (pro Monat): $0,10 pro Abfrage<br>
10.001 - 100.000 zusätzliche Abfragen (pro Monat): $0,05 pro Abfrage<br>
Über 100.000 zusätzliche Abfragen (pro Monat): $0,03 pro Abfrage<br>
[Abfrageerweiterungen](/docs/services/discovery/using.html#query-expansion):
5.000 Abfrageerweiterungen mit insgesamt 25.000 Begriffen

## Premium
   
Premium-Pläne bieten Entwicklern und Organisationen zur besseren Isolierung und Sicherheit eine einzige Tenantinstanz von einem oder mehreren Watson-Services. Diese Pläne ermöglichen die Isolation auf Berechnungsebene auf der bestehenden gemeinsam genutzten Plattform sowie durchgängig verschlüsselte Daten sowohl bei der Übertragung als auch in ruhendem Zustand. 

Für weitere Informationen oder für den Kauf eines Premium-Plans wenden Sie sich an den [Vertrieb](https://ibm.biz/contact-wdc-premium). 
<br>
<br> 

**Hinweis:** Das Versionsdatum der API wurde auf `2018-08-01` aktualisiert. Um die Vorteile der neuen Optionen für Umgebungsgrößen (`LT`, `XS`, `S`, `MS`, `M`, `ML`, `L`, `XL`, `XXL`, `XXXL`) nutzen zu können, müssen Sie beim Erstellen von Umgebungen über die API dieses Versionsdatum verwenden. Die Umgebungsgrößen weisen jetzt den Typ `string` auf (bisher war der Typ `integer`.)

\* Die Dokumentbegrenzung geht von einer durchschnittlichen Dokumentgröße von 100 KB auf Platte aus. Die Dokumentgröße wird berechnet, nachdem das Dokument der Konvertierung und Aufbereitung unterzogen wurde. Die Größe kann daher erheblich von der ursprünglichen Eingabe abweichen. Sie können die Anzahl der gespeicherten Dokumente und das Gesamtvolumen des belegten Speichers mit der [Umgebungs-](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#environments-api) oder [Sammlungs](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#collections-api)-API bzw. mithilfe der Tools anzeigen. Falls Ihre Dokumente durchschnittlich größer als 100 KB auf Platte sind, erreichen Sie die Speicherbegrenzung eines Plans vor der maximalen Dokumentbegrenzung. Wenn Sie für Ihre Dokumente die [Dokumentsegmentierung](https://console.bluemix.net/docs/services/discovery/building.html#doc-segmentation) ausführen, wird jedes Segment als separates Dokument gezählt.

\*\* Die [Aufbereitungen von Natural Language Understanding (NLU)](https://console.bluemix.net/docs/services/discovery/building.html#adding-enrichments) sind Entitätsextraktion, Stimmungsanalyse, Kategorieklassifizierung, Konzepttagging, Schlüsselwortextraktion, Beziehungsextraktion, Emotionsanalyse, Elementklassifizierung und Semantikrollenextraktion. Es werden nur die ersten 50.000 Zeichen jedes Dokuments aufbereitet. 

\*\*\* Die Elementklassifizierung ist eine Aufbereitung, die die Analyse von maßgeblichen Dokumenten ermöglicht, um relevante Elemente zu konvertieren, zu identifizieren und zu klassifizieren. Dabei wird die Verarbeitung natürlicher Sprachen genutzt, um die folgenden Elemente aus PDF-Dokumenten zu extrahieren: Partei (der Bezug), die Gattung (der Typ des Elements) und die Kategorie (die spezifische Klasse).

\*\*\*\* Wenn Sie Ihre InFlight-Begrenzung erreichen, sollten Sie die Einpflegerate verlangsamen. Bei der Verwendung des Discovery-Service wird ein Dokument während des Uploads, der Aufbereitung und der Verarbeitung als "Inflight" bezeichnet, bevor es zu einer Sammlung hinzugefügt wird.

Informationen zur Berechnung der Kosten finden Sie im Abschnitt zum [IBM Cloud-Preisrechner ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link") ](https://console.bluemix.net/pricing/platform/watson){: new_window}.

Informationen zur Sicherheit bei IBM Cloud finden Sie im Abschnitt zur [Datensicherheit und zum Datenschutz von Cloud-Services ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/software/sla/sladb.nsf/sla/csdsp?OpenDocument){: new_window}.

Zusätzliche Preisinformationen finden Sie im [{{site.data.keyword.discoveryshort}}-Katalog ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link") ](https://console.bluemix.net/catalog/services/discovery){: new_window}.

## Hinweise für Kunden mit bestehenden Plänen

- Seit dem **1. August 2018** basiert Ihre Abrechnung und Nutzung auf diesem Preisstrukturplan.
- Der Lite-Plan wurde von 2.000 Dokumenten/400 {{site.data.keyword.discoverynewsshort}}-Abfragen pro Monat auf 1.000 Dokumente/200 {{site.data.keyword.discoverynewsshort}}-Abfragen pro Monat reduziert. Wenn Sie die neuen Lite-Planbegrenzungen bereits überschritten haben, können Sie keine weiteren Dokumente hinzufügen. Sie können das Programm jedoch weiterhin verwenden oder ein Upgrade auf einen Advanced- oder Premium-Plan durchführen.
- Der Standard-Plan wurde außer Kraft gesetzt und ist für neue Benutzer nicht mehr verfügbar. Wenn Sie sich derzeit in einem vorhandenen Standard-Plan befinden, können Sie die Anwendung weiter verwenden oder ein Upgrade auf einen Advanced- oder Premium-Plan durchführen.
- Die Advanced- und Premium-Pläne basieren jetzt auf Preisstufen für Dokumente und nicht mehr auf Dokumentstunden. Ihre monatlichen Rechnungen orientieren sich daher nicht mehr an der Anzahl der Dokumente, es sei denn, Sie wechseln zwischen Preisstufen.
- Als Premium-Kunde wenden Sie sich an den [Vertrieb](https://ibm.biz/contact-wdc-premium), um mehr zur geänderten Rechnungsstellung zu erfahren.	
