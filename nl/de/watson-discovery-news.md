---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-05"

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

# Watson Discovery News
{: #watson-discovery-news}

{{site.data.keyword.discoverynewsfull}} ist in {{site.data.keyword.discoveryshort}} enthalten. {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} ist ein indexierter Datenbestand, der vorab mit den folgenden kognitiven Erkenntnissen aufbereitet wurde: **Schlüsselwortextraktion**, **Entitätsextraktion**, **Semantikrollenextraktion**, **Stimmungsanalyse**, **Beziehungsextraktion** und **Kategorieklassifizierung**. (Weitere Informationen zu Aufbereitungen finden Sie unter [Aufbereitungen hinzufügen](building.html#adding-enrichments).) Auch die folgenden zusätzlichen Metadaten werden hinzugefügt: Suchlaufdatum und Veröffentlichungsdatum. Eine Archivsuche ist für die Nachrichtendaten der letzten 60 Tage verfügbar. Was Sie mit {{site.data.keyword.discoverynewsfull}} erstellen können, wird in einer [Demo ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://discovery-news-demo.ng.bluemix.net/){: new_window} gezeigt.

{{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} wird ständig mit neuen Artikeln aktualisiert und ist in Englisch, Spanisch, Deutsch, Koreanisch und Japanisch verfügbar. Die englischsprachige Version von {{site.data.keyword.discoverynewsshort}} wird täglich mit ca. 300.000 neuen Artikeln aktualisiert. Die spanischsprachige Version von {{site.data.keyword.discoverynewsshort}} wird täglich mit ca. 60.000 neuen Artikeln aktualisiert, die deutschsprachige Version von {{site.data.keyword.discoverynewsshort}} mit ca. 40.000 neuen Artikeln und die koreanischsprachige Version von {{site.data.keyword.discoverynewsshort}} mit ca. 10.000 neuen Artikeln pro Tag. Die japanischsprachige Version von {{site.data.keyword.discoverynewsshort}} wird täglich mit ca. 17.000 neuen Artikeln aktualisiert. Die Nachrichtenquellen variieren je nach Sprache, daher sind die Abfrageergebnisse für die einzelnen Sammlungen nicht identisch.

Anwendungsfälle für {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}}:

- Alertausgabe für Nachrichten: Sie können neue Alerts erstellen und hierzu die Unterstützung für Entitäten, Schlüsselwörter, Kategorien und Stimmungsanalyse nutzen. Hierdurch können Sie nicht nur Nachrichten überwachen, sondern erhalten außerdem Informationen zu deren Aufnahme.

- Ereigniserkennung: Die Semantikrollenextraktion für Subjekt/Aktion/Objekt überprüft auf Begriffe/Aktionen wie 'acquisition' (Akquisition), 'election results' (Wahlergebnisse) oder 'IPO'.

- Trendermittlung für Nachrichtenthemen: Sie können gängige Themen erkennen und Zu- oder Abnahmen für die Häufigkeit der Erwähnung dieser (oder verwandter) Themen überwachen.

Informationen zum Schreiben von Abfragen für {{site.data.keyword.discoverynewsfull}} finden Sie unter:
- [Watson Discovery News abfragen](/docs/services/discovery/using.html#querying-news)
- [Abfragekonzepte](/docs/services/discovery/using.html)
- [Abfragereferenz](/docs/services/discovery/query-reference.html)

Das Anpassen der {{site.data.keyword.discoverynewsfull}}-Konfiguration, das Durchführen eines Trainings oder das Hinzufügen von Dokumenten zur Sammlung '{{site.data.keyword.discoverynewsfull}}' ist nicht möglich.

{{site.data.keyword.discoverynewsfull}}-Abfragen zeigen die ersten 50 Wörter jedes Artikels im JSON-Feld `text` an.

Die maximale Anzahl der Ergebnisse, die für eine {{site.data.keyword.discoverynewsfull}}-Abfrage zurückgegeben werden, beträgt `50`. Verwenden Sie zusätzliche Abfragen und den Parameter `offset`, um mehr als `50` Ergebnisse zurückzugeben.

**Hinweis:** Diese Version von {{site.data.keyword.discoverynewsfull}} ist seit dem **31. Juli 2017** verfügbar. {{site.data.keyword.discoverynewsfull}} Original wurde am **15. January 2018** außer Kraft gesetzt. Informationen zur Migration finden Sie unter [Migration von Watson Discovery News Original durchführen](/docs/services/discovery/migrate-bwdn.html).
