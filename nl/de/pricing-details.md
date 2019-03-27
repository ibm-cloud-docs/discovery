---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-28"

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

# Preisstrukturpläne für Discovery
{: #discovery-pricing-plans}

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

Zusätzliche Optionen:<br> [Angepasste Modelle](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-your-custom-model):<br>
Ein Watson Knowledge Studio-Modell enthalten. Zusätzliche Modelle: Nicht verfügbar<br>[Elementklassifizierung](/docs/services/discovery?topic=discovery-element-classification#element-classification)\*\*\*:
500 Seiten pro Monat enthalten. Zusätzliche Seiten: Nicht verfügbar <br>[News-Abfragen](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news):
200 News-Abfragen pro Monat enthalten. Zusätzliche Abfragen: Nicht verfügbar<br>[Abfrageerweiterungen](/docs/services/discovery?topic=discovery-query-concepts#query-expansion):
500 Abfrageerweiterungen mit insgesamt 1.000 Begriffen. Zusätzliche Erweiterungen: Nicht verfügbar

Informationen zum Upgrade von Lite auf Advanced finden Sie unter [Upgrade für Ihren Service durchführen](/docs/services/discovery?topic=discovery-upgrading-your-plan#service).

Informationen zur Abfrageleistung finden Sie unter [Abfrageleistung](/docs/services/discovery?topic=discovery-qp#qp). Die Einschränkungen für Abfragen sind vom jeweiligen Plan abhängig. Geschätzte durchschnittliche Abfrageraten pro **Lite**- bzw. **Standard**-Plan: 1 Abfrage/Sekunde für erneut eingestufte Abfragen mit zwei Textfeldern der höchsten Ebene.

## Advanced
{: #advanced}

Wenn Sie die Größe des Advanced-Plans auswählen, ist zu beachten, dass Ressourcen sowohl für den Dokumentspeicher als auch für die Abfrage erforderlich sind. Daher benötigen Sie möglicherweise eine größere Umgebung, wenn Sie nahe an der maximalen Dokumentbegrenzung für eine Plangröße liegen und zudem folgende Anforderungen erfüllen müssen: 

-  Höhere Anforderungen an die Abfrageleistung (z. B. bei Verwendung von Relevanztraining)
-  Sie erwarten eine große Anzahl gleichzeitiger Benutzer
-  Komplexe Abfrageanforderungen 

Weitere Informationen zu Faktoren, die die Abfrageleistung beeinflussen, finden Sie unter [Abfrageleistung](/docs/services/discovery?topic=discovery-qp#qp). Die Einschränkungen für Abfragen sind vom jeweiligen Plan abhängig. Geschätzte durchschnittliche Abfrageraten pro **Advanced**-Plan (S, MS): 10 Abfragen/Sekunde für erneut eingestufte Abfragen mit zwei Textfeldern der höchsten Ebene.

Größe | Dokumentspeichergrenze | Anzahl der Dokumente\* | Preis 
------ | ------ | ------ | ------ 
X-Small\*\*\*\* | 40 GB | Bis zu 50.000 Dokumente pro Monat | Ab $500 pro Monat  
Small | 160 GB | Bis zu 1 Mio. Dokumente pro Monat | Ab $1.500 pro Monat  
Medium-Small | 320 GB | Bis zu 2 Mio. Dokumente pro Monat | Ab $3.000 pro Monat 
Medium| 640 GB | Bis zu 4 Mio. Dokumente pro Monat | Ab $5.000 pro Monat 
Medium-Large | 1,2 TB | Bis zu 8 Mio. Dokumente pro Monat | Ab $10.000 pro Monat 
Large| 2,4 TB | Bis zu 16 Mio. Dokumente pro Monat | Ab $15.000 pro Monat 
X-Large| 4 TB | Bis zu 23 Mio. Dokumente pro Monat | Ab $20.000 pro Monat 
XX-Large | 5,5 TB | Bis zu 64 Mio. Dokumente pro Monat | Ab $35.000 pro Monat 
XXX-Large | 12 TB | Bis zu 100 Mio. Dokumente pro Monat | Ab $45.000 pro Monat 

X-Small ist die kleinste verfügbare Umgebung und wird nur als Entwicklungs- und Testumgebung empfohlen.\*\*\*\*

Wenn Sie von einer Ebene von Advanced zu einer anderen wechseln, müssen Sie keine neuen Instanzen erstellen. Neue Instanzen sind allerdings erforderlich, wenn Sie von einem Advanced- zu einem Premium-Plan wechseln. Informationen zum Durchführen eines Upgrades von einer Ebene von Advanced auf eine andere finden Sie unter [Von einer Advanced-Ebene zu einer anderen wechseln](/docs/services/discovery?topic=discovery-upgrading-your-plan#upgrading-your-plan).

\*\*\*\*Attribute von X-Small-Plänen: 
- 1 Umgebung
- Bis zu 4 Sammlungen
- Kostenlose NLU-Aufbereitungen\*\*

Attribute für alle anderen Advanced-Pläne:
- 1 Umgebung
- Bis zu 100 Sammlungen
- Kostenlose NLU-Aufbereitungen\*\*

Zusätzliche Optionen:<br> [Angepasste Modelle](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-your-custom-model):<br>
Ein Watson Knowledge Studio-Modell enthalten. Zusätzliche Modelle: Jeweils $800<br>[Elementklassifizierung](/docs/services/discovery?topic=discovery-element-classification#element-classification)\*\*\*:
500 Seiten pro Monat enthalten. Zusätzliche Seiten: Je $0,40<br>[News-Abfragen](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news):
200 News-Abfragen pro Monat enthalten  
10.000 zusätzliche Abfragen (pro Monat): $0,10 pro Abfrage<br>
10.001 - 100.000 zusätzliche Abfragen (pro Monat): $0,05 pro Abfrage<br>
Über 100.000 zusätzliche Abfragen (pro Monat): $0,03 pro Abfrage<br>
[Abfrageerweiterungen](/docs/services/discovery?topic=discovery-query-concepts#query-expansion):
5.000 Abfrageerweiterungen mit insgesamt 25.000 Begriffen

`-----`
<br>
\* Die Dokumentbegrenzung geht von einer durchschnittlichen Dokumentgröße von 100 KB auf Platte aus. Die Dokumentgröße wird berechnet, nachdem das Dokument der Konvertierung und Aufbereitung unterzogen wurde. Die Größe kann daher erheblich von der ursprünglichen Eingabe abweichen. Sie können die Anzahl der gespeicherten Dokumente und das Gesamtvolumen des belegten Speichers mit der [Umgebungs-](https://{DomainName}/apidocs/discovery#get-environment-info) oder [Sammlungs](https://{DomainName}/apidocs/discovery#get-collection-details)-API bzw. mithilfe der Tools anzeigen. Falls Ihre Dokumente durchschnittlich größer als 100 KB auf Platte sind, erreichen Sie die Speicherbegrenzung eines Plans vor der maximalen Dokumentbegrenzung. Wenn Sie für Ihre Dokumente die [Dokumentsegmentierung](/docs/services/discovery?topic=discovery-configservice#doc-segmentation) ausführen, wird jedes Segment als separates Dokument gezählt.

\*\* Die [Aufbereitungen von Natural Language Understanding (NLU)](/docs/services/discovery?topic=discovery-configservice#adding-enrichments) sind Entitätsextraktion, Stimmungsanalyse, Kategorieklassifizierung, Konzepttagging, Schlüsselwortextraktion, Beziehungsextraktion, Emotionsanalyse, Elementklassifizierung und Semantikrollenextraktion.  Es werden nur die ersten 50.000 Zeichen jedes Dokuments aufbereitet. 

\*\*\* Die Elementklassifizierung ist eine Aufbereitung, die die Analyse von maßgeblichen Dokumenten ermöglicht, um relevante Elemente zu konvertieren, zu identifizieren und zu klassifizieren. Dabei wird die Verarbeitung natürlicher Sprachen genutzt, um die folgenden Elemente aus PDF-Dokumenten zu extrahieren: Partei (der Bezug), die Gattung (der Typ des Elements) und die Kategorie (die spezifische Klasse).

Um die Vorteile der neuen Optionen für Umgebungsgrößen (`LT`, `XS`, `S`, `MS`, `M`, `ML`, `L`, `XL`, `XXL`, `XXXL`) zu nutzen, müssen Sie beim Erstellen von Umgebungen mit der API das API-Versionsdatum `2018-08-01` oder höher verwenden. Die Umgebungsgrößen weisen jetzt den Typ `string` auf (bisher war der Typ `integer`.)
{: note}

## Premium
{: #premiumplan}
   
Premium-Pläne bieten Entwicklern und Organisationen zur besseren Isolierung und Sicherheit eine einzige Tenantinstanz von einem oder mehreren Watson-Services. Diese Pläne ermöglichen die Isolation auf Berechnungsebene auf der bestehenden gemeinsam genutzten Plattform sowie durchgängig verschlüsselte Daten sowohl bei der Übertragung als auch in ruhendem Zustand. 

Für weitere Informationen oder für den Kauf eines Premium-Plans wenden Sie sich an den [Vertrieb](https://ibm.biz/contact-wdc-premium). 

## Weitere Informationen
{: #pricingadd}

Informationen zur Berechnung der Kosten finden Sie im Abschnitt zum [IBM Cloud-Preisrechner![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/pricing/platform/watson){: new_window}.

Informationen zur Sicherheit bei IBM Cloud finden Sie im Abschnitt zur [Datensicherheit und zum Datenschutz von Cloud-Services ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/software/sla/sladb.nsf/sla/csdsp?OpenDocument){: new_window}.

Zusätzliche Preisinformationen finden Sie im [{{site.data.keyword.discoveryshort}}-Katalog ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/catalog/services/discovery){: new_window}.

## Hinweise für Kunden mit bestehenden Plänen
{: #pricingnotes}

- Seit dem **1. August 2018** basiert Ihre Abrechnung und Nutzung auf diesem Preisstrukturplan.
- Der Lite-Plan wurde von 2.000 Dokumenten/400 {{site.data.keyword.discoverynewsshort}}-Abfragen pro Monat auf 1.000 Dokumente/200 {{site.data.keyword.discoverynewsshort}}-Abfragen pro Monat reduziert.  Wenn Sie die neuen Lite-Planbegrenzungen bereits überschritten haben, können Sie keine weiteren Dokumente hinzufügen. Sie können das Programm jedoch weiterhin verwenden oder ein Upgrade auf einen Advanced- oder Premium-Plan durchführen.
- Der Standard-Plan wurde außer Kraft gesetzt und ist für neue Benutzer nicht mehr verfügbar. Wenn Sie sich derzeit in einem vorhandenen Standard-Plan befinden, können Sie die Anwendung weiter verwenden oder ein Upgrade auf einen Advanced- oder Premium-Plan durchführen.
- Die Advanced- und Premium-Pläne basieren jetzt auf Preisstufen für Dokumente und nicht mehr auf Dokumentstunden. Ihre monatlichen Rechnungen orientieren sich daher nicht mehr an der Anzahl der Dokumente, es sei denn, Sie wechseln zwischen Preisstufen.
- Premium-Kunden wenden sich an den [Vertrieb![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://ibm.biz/contact-wdc-premium){: new_window}, um Details zur geänderten Rechnungsstellung zu erhalten.	
