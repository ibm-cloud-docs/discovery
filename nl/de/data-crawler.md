---

copyright:
  years: 2015, 2017, 2019
lastupdated: "2019-02-08"

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

# Inhalt mit Data Crawler hinzufügen
{: #adding-content-with-data-crawler}

Mit Data Crawler können Sie das Hochladen von Inhalt in den {{site.data.keyword.discoveryshort}}-Service automatisieren.
{: shortdesc}

Data Crawler sollte nur zum Durchsuchen von Dateifreigaben oder Datenbanken verwendet werden, in allen anderen Fällen sollten Sie den entsprechenden {{site.data.keyword.discoveryshort}}-Connector verwenden. Weitere Informationen finden Sie unter [Verbindung zu Datenquellen herstellen](/docs/services/discovery?topic=discovery-sources#sources). Data Crawler wird nicht mehr unterstützt, falls Sie ihn mit einer Datenquelle verwenden, die von den {{site.data.keyword.discoveryshort}}-Connectoren unterstützt wird.
{: important}

## Daten mit Data Crawler durchsuchen
{: #dc-crawling}

Data Crawler ist ein Befehlszeilentool, mit dem Sie Ihre Dokumente zur Verwendung durch den {{site.data.keyword.discoveryshort}}-Service aus den Repositorys entnehmen können, in denen sie sich befinden (z. B. Dateifreigaben, Datenbanken).

Data Crawler sollte nur zur Crawlersuche in Dateifreigaben oder Datenbanken verwendet werden. In allen anderen Fällen verwenden Sie den jeweiligen {{site.data.keyword.discoveryshort}}-Connector für Box, SharePoint, Salesforce, IBM Cloud Object Storage oder die Web-Crawler-Suche. Weitere Informationen finden Sie unter [Verbindung zu Datenquellen herstellen](/docs/services/discovery?topic=discovery-sources#sources). Data Crawler wird nicht mehr unterstützt, falls Sie ihn mit einer Datenquelle verwenden, die von den {{site.data.keyword.discoveryshort}}-Connectoren unterstützt wird.
{: important}

## Einsatzbereiche für Data Crawler
{: #dc-use}

Data Crawler sollte verwendet werden, falls Sie ein verwaltetes Upload für eine erhebliche Anzahl von Dateien aus einem fernen System durchführen möchten oder wenn Sie Inhalt aus einem unterstützten Repository (z. B. einer Db2-Datenbank) extrahieren wollen.

Data Crawler ist nicht als Lösung für das Upload von Dateien aus Ihrem lokalen Laufwerk gedacht. Dateien aus einem lokalen Laufwerk sollten mit den Tools oder mithilfe von direkten API-Aufrufen hochgeladen werden. Eine weitere Option zum Hochladen einer großen Anzahl von Dateien in {{site.data.keyword.discoveryshort}} ist [discovery-files ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/IBM/discovery-files){: new_window} auf GitHub.
{: note}

## Data Crawler verwenden
{: #dc-using}

1. [Konfigurieren Sie den {{site.data.keyword.discoveryshort}}-Service.](/docs/services/discovery?topic=discovery-configservice#configservice)
1. [Laden Sie Data Crawler herunter und installieren Sie Data Crawler](/docs/services/discovery?topic=discovery-downloading-and-installing-the-data-crawler#downloading-and-installing-the-data-crawler) auf einem unterstützten Linux-System, das Zugriff auf den Inhalt besitzt, den Sie durchsuchen wollen.
1. [Verbinden Sie Data Crawler](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-connector-and-seed-options) mit Ihrem Inhalt.
1. [Konfigurieren Sie Data Crawler](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-the-data-crawler) für die Verbindung zum {{site.data.keyword.discoveryshort}}-Service.
1. [Führen Sie eine Crawlersuche für Ihren Inhalt durch](/docs/services/discovery?topic=discovery-crawling-your-data-repository#crawling-your-data-repository).

Ein Schnelleinstieg in die Verwendung von Data Crawler wird durch das Beispiel in [Einführung in Data Crawler](/docs/services/discovery?topic=discovery-getting-started-with-the-data-crawler#getting-started-with-the-data-crawler) ermöglicht.
