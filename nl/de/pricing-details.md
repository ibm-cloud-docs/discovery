---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-09"

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

Der {{site.data.keyword.discoveryfull}}-Service bietet drei Pläne, die für Sie je nach Bedarf verschiedene Ebenen von Ressourcen und Funktionalität bereitstellen.
{: shortdesc}

Für **private Datenanwendungsfälle** gelten die folgenden Begrenzungen und Preise:

| Lite                     |  Standard         | Advanced          | Premium          |
|--------------------------|-------------------|-------------------|-------------------|
| Bis zu 2.000 gleichzeitige Dokumente pro Monat\*   | Bis zu 100.000 gleichzeitige Dokumente pro Monat\*<br/> $10 je 1.000 gleichzeitige Dokumenten pro Monat ($0.0139USD/1000 Dokumente/Std.)\*\*\*<br/> 2.000 Dokumente pro Monat kostenlos\*\*\*\*  | **Reservierte Umgebung**</br>$1.000/Monat Basispreis<br/> Bis zu 1.000.000 Dokumente pro Monat\*<br/> $5 je 1.000 gleichzeitige Dokumente pro Monat ($0.00694 USD/1000 Dokumente/Std.)\*\*\*<br/> 100.000 Dokumente pro Monat inklusive\*\*\*\*</br> Wenden Sie sich bei größeren Umgebungen an den [Vertrieb ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/marketing/iwm/dre/signup?source=MAIL-watson){: new_window}.| **Premium-Pläne** bieten Entwicklern und Organisationen zur besseren Isolierung und Sicherheit eine einzige Tenantinstanz von einem oder mehreren Watson-Services. Diese Pläne ermöglichen die Isolation auf Berechnungsebene auf der bestehenden gemeinsam genutzten Plattform sowie durchgängig verschlüsselte Daten sowohl bei der Übertragung als auch in ruhendem Zustand. Wenn Sie weitere Informationen benötigen oder einen Premium-Plan erwerben möchten, wenden Sie sich an den [Vertrieb ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://ibm.biz/contact-wdc-premium){: new_window}. |
| 200 MB\*\*                  |10 GB\*\*  | 80 GB\*\* |-|
| Bis zu 2 Sammlungen      |Bis zu 4 Sammlungen | Bis zu 100 Sammlungen|-|
| Bis zu 1 angepasstes {{site.data.keyword.knowledgestudiofull}}-Modell    |Bis zu 1 angepasstes {{site.data.keyword.knowledgestudioshort}}-Modell    | Keine Begrenzung für angepasste {{site.data.keyword.knowledgestudioshort}}-Modelle<br/>1 angepasstes {{site.data.keyword.knowledgestudioshort}}-Modell inklusive<br/>Zusätzlich $800 pro {{site.data.keyword.knowledgestudioshort}} Modell und Monat|-|

**Hinweis:** Bei allen Plänen sind die ersten 1.000 Abfragen für {{site.data.keyword.discoverynewsshort}} im Monat kostenlos. Nach den ersten 1000 Abfragen werden alle weiteren Abfragen von {{site.data.keyword.discoverynewsshort}} mit $0,10 pro Abfrage berechnet.

**Hinweis:** Services eines Lite-Plans werden nach 30 Tagen Inaktivität gelöscht. Bei Lite-Plänen ist eine Umgebung pro Organisation kostenlos.

 \* Die Dokumentbegrenzung geht von einer durchschnittlichen Dokumentgröße von 100 KB auf Platte aus. Dies ist die Größe eines Dokuments in einer Sammlung, nachdem es der Konvertierung und Aufbereitung unterzogen wurde. Die Größe kann daher erheblich von der ursprünglichen Eingabe abweichen. Sie können die Anzahl der gespeicherten Dokumente und das Gesamtvolumen des belegten Speichers mit der API `environments` oder `collections` bzw. mithilfe der Tools anzeigen.

 \*\* Falls Ihre Dokumente durchschnittlich größer als 100 KB auf Platte sind, erreichen Sie die Speicherbegrenzung eines Plans vor der maximalen Dokumentbegrenzung.

 \*\*\* Der Preis basiert auf der Anzahl der Stunden, die ein Stapel von 1.000 Dokumenten im Service gespeichert ist (wird als '1000-Dokument-Stunde' bezeichnet). Für den Preisrechner ist dies die Anzahl, die eingegeben werden sollte  (`Anzahl der Dokumente * Anzahl der Stunden, die diese Dokumente pro Monat gespeichert sind / 1000`).

 \*\*\*\* Kostenlose Volumina basieren auf dem Äquivalent der einen Monat lang gespeicherten Dokumente. Im Standard-Plan ist das kostenlose Volumen äquivalent zu 2.000 Dokumenten * 720 Stunden / 1000-Dokument-Stapel  = 1440 Tausend-Dokument-Stunden.

**Beispiel:** Ein Benutzer mit dem Standard-Plan speichert 4.000 Dokumente für den gesamten Monat. Diese werden wie folgt berechnet:

- `4000 Dokumente * 720 Stunden (in einem Monat) / 1000 = 2.880` verbrauchte Tausend-Dokument-Stunden.

- `2.880 - 1.440 (kostenlose Dokumentstunden) = 1.440` berechnungsfähige Tausend-Dokument-Stunden.

- `1.440 * $0,0139` (Preis je Tausend-Dokument-Stunde) = `$20,00` für den Monat.

**Hinweis:** Bei der Berechnung des in Rechnung gestellten Betrags für jede Stunde wird die Gesamtzahl der gespeicherten Dokumente auf den nächsten Tausender aufgerundet. Falls Sie beispielsweise 4.678 Dokumente für 1 Stunde gespeichert haben, würden die Dokumente auf 5.000 gerundet und 5 Tausend-Dokument-Stunden ergeben, die für das Konto in Rechnung gestellt werden.

**Hinweis:** Für Aufbereitungen entstehen keine zusätzlichen Kosten.

Angaben über die {{site.data.keyword.Bluemix_notm}}-Sicherheit enthält der Abschnitt [{{site.data.keyword.Bluemix_notm}}-Servicebeschreibung ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](../../icons/launch-glyph.svg "Symbol für externen Link")] (http://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=IBM+Bluemix+Service+Description){: new_window}.

## Aus vorherigen Preisstrukturplänen konvertieren

Kunden, die einen Plan vor dem **1. August 2017** abonniert haben, wurden auf einen der neuen Pläne migriert.

- Kunden, die zuvor den Plan für den dreißigtägigen kostenlosen Test verwendeten, wurden auf den **Lite**-Plan migriert.
  Infolge dieser Überführung haben Bestandskunden möglicherweise die Begrenzung des Lite-Plans für Dokumente _(2000)_, Speicher _(200Mb)_ oder Anzahl der Sammlungen _(2)_ erreicht bzw. überschritten. Falls Sie die Begrenzung des **Lite**-Plans überschritten haben, können Sie keinen zusätzlichen Inhalt im Service hinzufügen, Ihre Sammlungen jedoch weiterhin abfragen. Den aktuellen Status aller dieser Grenzwerte können Sie mithilfe der {{site.data.keyword.discoveryshort}}-Tools oder der API anzeigen. Damit Sie das Hinzufügen von Inhalt zur {{site.data.keyword.discoveryshort}}-Instanz fortsetzen können, müssen Sie eine der folgenden Maßnahmen ergreifen:
  - Entfernen Sie Sammlungen und/oder Dokumente, damit die Begrenzungen des **Lite**-Plans nicht mehre überschritten werden.
    Dokumente können entweder einzeln über die API mit der Methode [delete-doc ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-doc){: new_window} oder als ganze Sammlungen mithilfe der Tools oder der API unter Verwendung der Methode [delete-collection ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-collection){: new_window} gelöscht werden.
  - Führen Sie für Ihren Plan ein Upgrade auf eine Stufe durch, die Ihren Speicherbedarf erfüllt.
- Kunden mit Umgebungen der Größe **`1`**, **`2`** oder **`3`** wurden automatisch auf den **Advanced**-Plan migriert.
  Falls Sie auf die Stufe 'Advanced' versetzt wurden und weniger als 100.000 Dokumente und 4 Sammlungen verwenden, können Sie zur Kostenersparnis auf die Stufe 'Standard' wechseln. Dies erfordert das Erstellen einer neuen Discovery-Instanz im Standard-Plan und das erneute Einpflegen der Daten in die neue Instanz. Das Einpflegen kann über die Tools, die APIs oder mit Data Crawler erfolgen.

Zusätzliche Preisinformationen finden Sie im [{{site.data.keyword.discoveryshort}}-Katalog ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window}.
