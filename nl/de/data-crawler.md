---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-03"

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

# Inhalt mit Data Crawler hinzufügen
{: #adding-content-with-data-crawler}

Mit Data Crawler können Sie das Hochladen von Inhalt in den {{site.data.keyword.discoveryshort}}-Service automatisieren.
{: shortdesc}

## Daten mit Data Crawler durchsuchen

Data Crawler ist ein Befehlszeilentool, mit dem Sie Ihre Dokumente aus den Repositorys entnehmen können, in denen sie sich befinden (z. B. Dateifreigaben, Datenbanken, Microsoft SharePoint), und sie zur Verwendung durch den {{site.data.keyword.discoveryshort}}-Service mit einer Push-Operation in die Cloud übertragen können.

Sie können die {{site.data.keyword.discoveryshort}}-Tools oder die API für die Crawlersuche in Box-, Salesforce- und Microsoft SharePoint Online-Datenquellen verwenden. Weitere Informationen finden Sie unter [Verbindung zu Datenquellen herstellen](/docs/services/discovery/connect.html).
{: tip}

## Einsatzbereiche für Data Crawler

Data Crawler sollte verwendet werden, falls Sie ein verwaltetes Upload für eine erhebliche Anzahl von Dateien aus einem fernen System durchführen möchten oder wenn Sie Inhalt aus einem unterstützten Repository (z. B. einer Db2-Datenbank) extrahieren wollen.

Data Crawler ist nicht als Lösung für das Upload von Dateien aus Ihrem lokalen Laufwerk gedacht. Dateien aus einem lokalen Laufwerk sollten mit den Tools oder mithilfe von direkten API-Aufrufen hochgeladen werden.
{: tip}

## Data Crawler verwenden

1. [Konfigurieren Sie den {{site.data.keyword.discoveryshort}}-Service.](/docs/services/discovery/building.html#configuring-your-service)
1. [Laden Sie Data Crawler herunter und installieren Sie Data Crawler](/docs/services/discovery/data-crawler-install.html) auf einem unterstützten Linux-System, das Zugriff auf den Inhalt besitzt, den Sie durchsuchen wollen.
1. [Verbinden Sie Data Crawler](/docs/services/discovery/data-crawler-seeds.html) mit Ihrem Inhalt.
1. [Konfigurieren Sie Data Crawler](/docs/services/discovery/data-crawler-discovery.html) für die Verbindung zum {{site.data.keyword.discoveryshort}}-Service.
1. [Führen Sie eine Crawlersuche für Ihren Inhalt durch](/docs/services/discovery/data-crawler-run.html).

Ein Schnelleinstieg in die Verwendung von Data Crawler wird durch das Beispiel in [Einführung in Data Crawler](/docs/services/discovery/data-crawler-qs.html) ermöglicht.
