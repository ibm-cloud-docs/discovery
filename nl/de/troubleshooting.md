---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-18"

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

# Fehlerbehebung

Dieser Abschnitt enthält Tipps zur Fehlerbehebung beim {{site.data.keyword.discoveryshort}}-Service.

Falls bei der Verwendung des {{site.data.keyword.discoveryshort}}-Service Probleme auftreten, können Sie versuchen, das Problem mit einem oder mehreren der folgenden Tipps zur Fehlerbehebung zu lösen.

-   Das Einpflegen eines Dokuments kann fehlschlagen, weil keine Typübereinstimmung zwischen Daten im aktuellen Dokument und ähnlichen Daten in einem zuvor eingepflegten Dokument besteht. Beispielsweise kann ein Feld in einem Dokument den Typ **date** und in einem nachfolgenden Dokument den Typ **string** besitzen.

    Die Vorschauoperation kann Typabweichungen nicht vorhersagen, weil sie lediglich ein einzelnes Dokument testet und keinen Datensatz über das Ergebnis der Konvertierung aufbewahrt.
-   Eine schnelle oder umfangreiche Indexierung von Dokumenten kann manchmal dazu führen, dass der Back-End-Suchservice erneut gestartet wird. Bitten Sie in einem solchen Fall den {{site.data.keyword.IBM}} Support um Unterstützung.
